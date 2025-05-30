
## 📊 2-BO‘LIM: Pandas, Polars, Data Analysis – savollar va javoblar

---

**1. Pandas’da `apply()` vs `vectorized` operatsiyalar farqi?**

* `apply()` – har bir row yoki column bo‘yicha Python function’ni qo‘llaydi → **sekinroq**
* **Vectorized operations** – NumPy asosida, **C-level** optimizatsiya → **ancha tezroq**

```python
df["new"] = df["a"] + df["b"]  # vectorized
df["new"] = df.apply(lambda row: row["a"] + row["b"], axis=1)  # apply
```

⛔ `apply()` – faqat kerak bo‘lsa, tahlil murakkab bo‘lsa ishlatiladi.

---

**2. `groupby().agg()` misollari va optimizatsiyasi**

```python
df.groupby("category").agg({
    "price": "mean",
    "quantity": ["sum", "count"]
})
```

⚡ `agg()` – bir nechta statistika olish uchun qulay.
Lekin `groupby().transform()` → groupga nisbiy qiymatlar (ratio) uchun ishlatiladi.

---

**3. Pandas'da NaN/None bilan ishlash**

```python
df.fillna(0)
df.dropna()
df["col"].isna()
```

* `isna()`, `notna()` orqali filtering
* `fillna(method="ffill")` – oldingi qiymat bilan to‘ldirish

---

**4. Pandas’dagi memory optimization usullari?**

```python
df["col"] = df["col"].astype("category")
df["id"] = df["id"].astype("int32")
```

* `category` – ayniqsa string bo‘lgan ustunlar uchun foydali
* `info(memory_usage="deep")` – real memory usage’ni ko‘rsatadi

---

**5. Polars – Pandas’dan ustun tomonlari**

* Rust asosidagi engine → **10x tezlik**
* **Lazy evaluation** imkoniyati → optimizatsiyalangan query dagi pipeline
* Multithreaded by default

```python
import polars as pl

df = pl.read_csv("data.csv")
df.lazy().filter(pl.col("price") > 100).select(pl.col("price").mean()).collect()
```

---

**6. Pandas’da `.merge()` va `.join()` farqlari**

* `.merge()` – SQL’dagi `JOIN` kabi ishlaydi, `on=`, `how=`
* `.join()` – faqat index bo‘yicha ulanadi

```python
pd.merge(df1, df2, on="id", how="left")
```

---

**7. `.query()` va `.eval()` haqida**

* `.query()` – sintaktik ravon filtering (`df[df.a > 10]` o‘rniga)
* `.eval()` – expression’ni tezroq va vectorized bajarish

```python
df.query("price > 100 and stock < 50")
df.eval("revenue = price * quantity", inplace=True)
```

---

**8. `pivot_table` va `melt()` – kengaytirish va yo‘naltirish**

```python
df.pivot_table(index="date", columns="region", values="sales", aggfunc="sum")
df.melt(id_vars=["date"], value_vars=["a", "b"])
```

---

**9. Time series bilan ishlash – `.resample()`, `.rolling()`**

```python
df.resample("M").sum()
df["rolling_avg"] = df["value"].rolling(window=7).mean()
```

---

**10. Realtime analytics uchun Polars Streaming yoki Kafka?**

* Polars o‘zi streaming emas, lekin `lazy` chaining optimallashtirish imkonini beradi.
* Kafka → ko‘p kiruvchi ma’lumotni real vaqt track qilishda ishlatiladi (bu keyingi bo‘limda).

