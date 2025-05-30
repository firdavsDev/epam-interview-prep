
## 🧩 7-BO‘LIM: Django, DRF, FastAPI – Framework Specific savollar va javoblar

---

### 🔹 **Django**

---

**1. Django’da signal’lar bilan nima qilgansan?**

> `post_save`, `pre_save`, `post_delete` signal’lari bilan **Profile yaratish**, **admin notificatsiya**, va **audit log** yozish uchun ishlaganman.

```python
@receiver(post_save, sender=User)
def create_profile(sender, instance, created, **kwargs):
    if created:
        Profile.objects.create(user=instance)
```

---

**2. Middleware’lar qanday ishlaydi va nima uchun kerak?**

* Request va response oqimini intercept qiladi.
* `Authentication`, `Rate limiting`, `Logging`, `Multi-tenant switch` uchun ishlatiladi.

```python
class MyCustomMiddleware:
    def __call__(self, request):
        print("Before view")
        response = self.get_response(request)
        print("After view")
        return response
```

---

**3. Django’da OneToOne, ForeignKey, ManyToMany farqi?**

| Field         | Relationship | Access         |
| ------------- | ------------ | -------------- |
| OneToOneField | 1:1          | `.relatedname` |
| ForeignKey    | Many:1       | `.model_set`   |
| ManyToMany    | Many\:Many   | `.all()`       |

---

**4. `select_for_update()` qachon ishlatiladi?**

* Transaction ichida row’ni **lock** qilish uchun (deadlock yoki race condition’ga qarshi)

```python
with transaction.atomic():
    user = User.objects.select_for_update().get(id=1)
    user.balance -= 100
    user.save()
```

---

**5. `Meta: unique_together` vs `UniqueConstraint`?**

* Django 3.2+ dan `UniqueConstraint` ishlatiladi, bu aniqroq:

```python
class Meta:
    constraints = [
        models.UniqueConstraint(fields=['user', 'course'], name='unique_user_course')
    ]
```

---

### 🔹 **DRF (Django REST Framework)**

---

**6. Serializer’larda `.create()` va `.update()` metodlari qachon kerak?**

* `ModelSerializer` default o‘zi bajaradi
* Custom logic kerak bo‘lsa override qilinadi

```python
class UserSerializer(serializers.ModelSerializer):
    def create(self, validated_data):
        password = validated_data.pop("password")
        user = User(**validated_data)
        user.set_password(password)
        user.save()
        return user
```

---

**7. DRF permission’lari haqida?**

* `IsAuthenticated`, `IsAdminUser`, `AllowAny`
* Custom:

```python
class IsOwner(permissions.BasePermission):
    def has_object_permission(self, request, view, obj):
        return obj.user == request.user
```

---

**8. `APIView` vs `GenericAPIView` vs `ViewSet` farqlari?**

| Class            | Use case                  |
| ---------------- | ------------------------- |
| `APIView`        | full manual control       |
| `GenericAPIView` | mixin bilan ishlaydi      |
| `ViewSet`        | RESTful endpointlar uchun |

---

**9. `@action` dekoratori nima?**

* ViewSet ichida `non-CRUD` endpoint yaratish:

```python
@action(detail=True, methods=["post"])
def activate(self, request, pk=None):
    ...
```

---

**10. Filtering, Search, Ordering qanday qo‘shiladi?**

```python
class MyViewSet(viewsets.ModelViewSet):
    filter_backends = [DjangoFilterBackend, SearchFilter, OrderingFilter]
    filterset_fields = ['status']
    search_fields = ['title', 'description']
    ordering_fields = ['created_at']
```

---

### 🔹 **FastAPI**

---

**11. FastAPI'da dependency injection qanday ishlaydi?**

```python
def get_db():
    db = Session()
    try:
        yield db
    finally:
        db.close()

@app.get("/users/")
def read_users(db: Session = Depends(get_db)):
    return db.query(User).all()
```

* `Depends()` orqali requestda kerakli resurslar inject qilinadi

---

**12. FastAPI’dagi `Pydantic` modellar va `ORM mode`?**

```python
class User(BaseModel):
    id: int
    name: str

    class Config:
        orm_mode = True
```

* `orm_mode = True` → SQLAlchemy instance’ni JSON response’ga avtomatik o‘girish

---

**13. Background tasklar qanday qo‘shiladi?**

```python
from fastapi import BackgroundTasks

def send_email(email: str):
    ...

@app.post("/register/")
def register_user(email: str, bg: BackgroundTasks):
    bg.add_task(send_email, email)
```

---

**14. FastAPI + SQLAlchemy + Alembic migratsiyasi haqida?**

* `alembic init migrations`
* `alembic revision --autogenerate -m "add users"`
* `alembic upgrade head`

FastAPI loyihalarida `models/`, `schemas/`, `routers/` folderlar bilan **modular DDD structure** afzal.

---

**15. FastAPI vs DRF – qachon qaysi biri?**

| Criteria      | DRF             | FastAPI                |
| ------------- | --------------- | ---------------------- |
| Maturity      | Juda katta      | Nisbatan yangi         |
| Async support | Limited         | Native async           |
| Performance   | O‘rtacha        | Yuqori (Starlette)     |
| ORM support   | Django ORM only | SQLAlchemy / others    |
| Swagger       | Custom          | Auto generated, kuchli |

---
