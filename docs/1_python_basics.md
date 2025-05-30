## 🔹 1-BO‘LIM: Python asoslari – savollar va javoblar

---

**1. `@staticmethod`, `@classmethod`, `@property` farqlari?**

* `@staticmethod` – klassga bog‘liq emas, faqat ichki utility vazifasini bajaradi.
* `@classmethod` – `cls` orqali klassga kirish huquqini beradi (masalan, alternative constructors).
* `@property` – attribute singari chaqiriladigan method yaratadi (`get`, `set`, `del` bilan birga ishlatiladi).

```python
class User:
    def __init__(self, name):
        self._name = name

    @staticmethod
    def greet():
        return "Hello!"

    @classmethod
    def from_dict(cls, data):
        return cls(data["name"])

    @property
    def name(self):
        return self._name
```

---

**2. Python’da GIL nima?**

* GIL (Global Interpreter Lock) – CPython’da bir vaqtning o‘zida faqat bitta thread bajarilishini kafolatlaydi.
* Bu CPU-bound operatsiyalar uchun to‘siq, lekin IO-bound (masalan, tarmoq yoki fayl) vazifalarda async/multithreading yaxshi ishlaydi.

---

**3. Python’da `__slots__` nima?**

* `__slots__` klass attributlarini oldindan belgilash orqali memory usage’ni kamaytiradi.
* Default bo‘lgan `__dict__` o‘chiriladi → kam RAM, tezroq access.

```python
class User:
    __slots__ = ["id", "name"]
```

---

**4. Generatorlar va `yield`?**

* Generator funksiya `yield` orqali qiymat qaytaradi, lekin execution pause bo‘ladi.
* Bu memoryda butun ro‘yxatni saqlamasdan, lazy evaluation qiladi.

```python
def count_up_to(n):
    i = 0
    while i < n:
        yield i
        i += 1
```

---

**5. Python’dagi memory management qanday ishlaydi?**

* Reference counting + cyclic garbage collector.
* `gc` moduli orqali chuqur nazorat mumkin.
* `del`, `weakref`, yoki kontekst managerlar orqali resurslarni boshqarish.

---

**6. Mutable vs Immutable turlar?**

* Immutable: `int`, `str`, `tuple`
* Mutable: `list`, `dict`, `set`
* Tuple ichida mutable element bo‘lsa, tuple "shunchaki" immutable bo‘ladi, ichidagilar emas.

---

**7. Typing: Union, Optional, TypedDict misollar?**

```python
from typing import Union, Optional, TypedDict

def process(value: Union[int, str]):
    ...

def get_name(user: Optional[dict]):
    ...

class UserDict(TypedDict):
    id: int
    name: str
```

---

**8. Python’da context manager (`with`) qanday ishlaydi?**

* `__enter__` va `__exit__` methodlari orqali avtomatik ochish/yopish ishlari.
* Fayl, socket, lock management uchun juda foydali.

```python
with open("file.txt") as f:
    data = f.read()
```

---

**9. Python’da dataclass nima va qachon kerak?**

* `@dataclass` klasslarni tezroq yozish uchun → `__init__`, `__repr__`, `__eq__` avtomatik.
* Faqat data saqlovchi obyektlar uchun ideal.

```python
from dataclasses import dataclass

@dataclass
class User:
    id: int
    name: str
```

---

**10. `*args`, `**kwargs` farqlari va ishlatish holatlari?**

* `*args`: tuple sifatida ko‘p positional argumentlarni oladi
* `**kwargs`: dict ko‘rinishida ko‘p nomli argumentlarni oladi

```python
def example(*args, **kwargs):
    print(args, kwargs)
```

