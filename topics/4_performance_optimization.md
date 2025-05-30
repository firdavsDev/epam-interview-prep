## ⚡ 4-BO‘LIM: Performance Optimization (Backend, DB, API, Pandas) – savollar va javoblar

---

### **1. Django/DRF’da sekin ishlayotgan API’ni qanday optimizatsiya qilganing bor?**

1. **N+1 query** muammosi bormi? → `select_related`, `prefetch_related` bilan hal qilinadi.
2. **Serializer darajasida** – unnecessary nested yoki `depth=2` muammosi.
3. **QueryCountMiddleware** bilan query’lar sonini kuzataman.
4. **Pagination** – har doim ishlatish kerak.
5. **Indexlar** – filtering ustunlariga `db_index=True` yoki `Meta: index_together`.

---

### **2. Django’da `select_related` va `prefetch_related` farqi nima?**

* `select_related` – **OneToOne / ForeignKey** bo‘yicha SQL JOIN qiladi
* `prefetch_related` – **ManyToMany / Reverse FK** uchun alohida query yuboradi

```python
Book.objects.select_related("author")       # JOIN bilan
Author.objects.prefetch_related("books")    # alohida query bilan
```

---

### **3. SQLAlchemy’da slow query’ni optimallashtirish?**

* `joinedload`, `subqueryload`, `lazy='selectin'` orqali N+1 ni kamaytirish
* Query profiling uchun: `echo=True`, `sqlalchemy.engine.logger`
* Index yaratish (`Index`, `unique`, `nullable=False`)

```python
session.query(Post).options(joinedload(Post.comments))
```

---

### **4. DRF API performance: caching qayerda kerak?**

1. **Low-level**: `@lru_cache`, `@cache_page`, `cache.set()`
2. **High-level**: Redis bilan fragment caching
3. **Throttling**: DRF’da per-user, per-IP throttles
4. **Conditional GET**: ETag / `Last-Modified` bilan ishlash

---

### **5. Redis bilan qanday caching qilganing bor?**

```python
# Django caching
from django.core.cache import cache
cache.set("key", "value", timeout=60*5)
cache.get("key")
```

1. **View-level cache** – `@cache_page`
2. **Low-level** – frequently accessed query’lar natijasini saqlash
3. **Rate-limiting** – Redis + `ip:count` pattern

---

### **6. Pandas’da performance profiling qanday qilinadi?**

```python
import pandas as pd
import numpy as np

%timeit df["value"] = df["a"] + df["b"]  # timing
df.memory_usage(deep=True)
```

1. `astype()` bilan turlarni siqish
2. `category` turlar
3. `apply()` dan qochish → vectorized ops
4. `query()`, `eval()` – C backend’da tezroq bajariladi

---

### **7. Async bilan performance oshirish misollari?**

FastAPI misolida:

```python
@app.get("/users")
async def get_users():
    async with async_session() as session:
        result = await session.execute(select(User))
        return result.scalars().all()
```

* **Async SQLAlchemy** yoki Tortoise ORM
* IO-bound task’lar (API, Redis, DB) uchun async kerak

---

### **8. DRF'da `ListAPIView` optimizatsiyasi?**

* `pagination_class`
* `filterset_class`, `search_fields`, `ordering_fields` → DRF'da avtomatik qidiruv
* `only()` bilan faqat kerakli ustunlarni olish

```python
queryset = MyModel.objects.only("id", "name")
```

---

### **9. PostgreSQL performans: qanday tahlil qilasan?**

1. `EXPLAIN ANALYZE` bilan query execution plan
2. Index qilingan ustunlar: `btree`, `gin`, `gist`
3. Connection pool: `pgbouncer` yoki `conn_max_age` sozlamasi

```sql
EXPLAIN ANALYZE SELECT * FROM users WHERE email='a@example.com';
```

---

### **10. API ni 1 million request/second ga tayyor qilishda nima qilasan?**

1. **Horizontal scaling** – Kubernetes + HPA
2. **Redis caching** + async
3. **Gunicorn tuning** – `workers`, `threads`, `keep-alive`
4. **CDN / Edge caching** – Cloudflare
5. **Database connection pooling**
6. **Stateless services** – scale-friendly

---

