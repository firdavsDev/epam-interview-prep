
## 🧷 8-BO‘LIM: Real Interview’dan olingan savollar va javoblar

---

### 🔹 **Git: `merge` vs `rebase`**

**Savol:** `git merge` va `git rebase` orasidagi farq nima?

✅ **Javob:**

* `merge` – ikkita branch’ni birlashtiradi, tarixda merge commit qoladi.
* `rebase` – branch tarixini boshqa branch ustiga "ko‘chiradi", **tarixni tozalaydi**.

📌 Ishlatish:

* `merge` → umumiy branchlarda (`main`)
* `rebase` → shaxsiy branchlarda (`feature`) → `git rebase main`

---

### 🔹 **Docker: Image, Container, Volume**

**Savol:** Docker image, container, volume nima?

✅ **Javob:**

* **Image** – Dockerfile asosida yaratilgan immutable snapshot
* **Container** – image asosida ishga tushgan izolyatsiyalangan process
* **Volume** – container data’sini saqlovchi persistent storage

```bash
docker build -t myapp .
docker run -v /data:/app/data myapp
```

---

### 🔹 **Web: REST API va Django arxitekturasi**

**Savol:** REST nima va Django arxitekturasi qanday?

✅ **Javob:**

* **REST** – Stateless API design pattern: `GET`, `POST`, `PUT`, `DELETE`
* Django arxitekturasi:

  * `MTV` pattern (Model, Template, View)
  * DRF: APIView → Serializer → Model
  * Layered: `views`, `services`, `repos`, `serializers`

---

### 🔹 **Database: Index va `INNER JOIN`**

**Savol:** Index nima? `INNER JOIN` qanday ishlaydi?

✅ **Javob:**

* **Index** – ustun ustida tez izlash uchun B-Tree struktura (`btree`, `gin`)
* `INNER JOIN` – ikki jadvaldagi mos qiymatlar asosida bog‘lanadi.

```sql
SELECT * FROM orders
JOIN customers ON orders.customer_id = customers.id
```

---

### 🔹 **CI/CD**

**Savol:** CI/CD tushunchasi qanday?

✅ **Javob:**

* **CI (Continuous Integration)** – kodni test bilan tez-tez birlashtirish
* **CD (Continuous Delivery/Deployment)** – avtomatik build, test, deploy
* Tool misollar: GitHub Actions, GitLab CI, Jenkins

---

### 🔹 **Python Types & Ops: `dict`, `is vs ==`, `copy` vs `deepcopy`, mutable**

---

**1. `dict` ichki ishlashi + hash**

* `dict` – hash table asosida
* `hash(key)` → bucket → collision bo‘lsa probing
* Hash **deterministic**, **constant-time** bo‘lishi kerak

---

**2. `is` vs `==`**

* `is` – identity (id() bir xilmi?)
* `==` – value comparison

```python
a = [1, 2]; b = a
a is b  # True
a == b  # True
```

---

**3. `copy()` vs `deepcopy()`**

```python
from copy import copy, deepcopy

x = [[1], [2]]
shallow = copy(x)
deep = deepcopy(x)
```

* `copy` – faqat 1-nuqta nusxalaydi
* `deepcopy` – rekursiv nusxa

---

**4. Mutable vs Immutable**

| Type  | Mutable? |
| ----- | -------- |
| list  | ✅        |
| tuple | ❌        |
| dict  | ✅        |
| str   | ❌        |

---

### 🔹 **Algorithms: Complexity**

**Savol:** Complexity nima? `O(n log n)` nima anglatadi?

✅ **Javob:**

* **Time complexity** – algoritm ishlash muddati o‘sishiga nisbatan
* `O(n)` – linear
* `O(n log n)` – MergeSort, QuickSort average
* `O(1)` – constant (dict access)

---

### 🔹 **Functions in Python**

**Savol:** Python’da funksiya nima va qanday obyekt?

✅ **Javob:**

* Function – birinchi darajali obyekt
* Funksiya ni parametr sifatida berish, qaytarish, `__call__`, `__closure__`

```python
def outer():
    x = 5
    def inner():
        return x
    return inner
```

---

### 🔹 **Memory: Reference Counting**

✅ Har bir object’ning `ref count` bor. `gc` moduli bilan kuzatish mumkin.

```python
import sys
x = []
print(sys.getrefcount(x))  # 2
```

---

### 🔹 **Multitasking: GIL, thread vs process**

✅ **GIL** (Global Interpreter Lock) – CPython’ning global locki → faqat bitta thread ishlaydi

| Model   | Better for |
| ------- | ---------- |
| Thread  | IO-bound   |
| Process | CPU-bound  |

`multiprocessing`, `asyncio`, `concurrent.futures` → parallelizmga erishish yo‘llari

---

### 🔹 **OOP: Encapsulation, Data hiding**

* **Encapsulation** – ma’lumotni method orqali boshqarish
* **Data hiding** – `__attr` orqali private qilish (name mangling)

```python
class A:
    def __init__(self):
        self.__secret = 123
```

---

## 🔖 Bonus: Advanced Concepts (Real Interview Recommendations)

---

### 🔹 Decorator without `@`:

```python
def dec(f):
    def wrapper(*a, **kw):
        return f(*a, **kw)
    return wrapper

def hello():
    return "hi"

hello = dec(hello)
```

---

### 🔹 Inheritance, MRO, Diamond, C3 Algorithm

```python
class A: pass
class B(A): pass
class C(A): pass
class D(B, C): pass
print(D.__mro__)
```

* Python 3: **New-style classes** (object-inherited)
* `C3` algorithm → deterministik MRO yaratadi

---

### 🔹 LEGB Rule (scope)

| Scope | Description |
| ----- | ----------- |
| L     | Local       |
| E     | Enclosing   |
| G     | Global      |
| B     | Built-in    |

```python
def outer():
    x = "enclosing"
    def inner():
        print(x)
    inner()
```
