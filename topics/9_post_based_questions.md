
## 🧪 9-BO‘LIM: [Post](https://t.me/davron_coder/328) asosidagi savollar va javoblar (Node.js backend uchun, ammo Python dev uchun moslashtirilgan)

---

### 🔸 1. **Self-Introduction (Pitch) – Ingliz tilida qisqacha nutq**

**Savol:** Tell me about yourself.

✅ **Sample Answer:**

> I’m a backend engineer with 4+ years of experience in Python, Django, and FastAPI. I’ve mainly worked on high-load systems in the education, agriculture, and payments domains.
> I’m proficient in building REST APIs, integrating CI/CD pipelines, containerizing services with Docker, and optimizing SQL/NoSQL databases. I’ve also worked in Agile teams with a strong focus on code quality, testing, and performance.
> Currently, I’m focusing on scalable microservice architecture and real-time analytics with tools like Kafka and Redis.

---

### 🔸 2. **Agile & Scrum savollar**

**Savol:** Agile nima? Scrum jarayonida qanday qatnashgansiz?

✅ **Javob:**

> Agile is an iterative approach to software delivery. Scrum is one of its implementations with fixed-length sprints, daily standups, sprint planning, and retrospectives.
> In my teams, I participated in story point estimations, delivered features every sprint, and regularly discussed blockers and improvements in retros.

---

### 🔸 3. **Git & Gitflow**

**Savol:** Gitflow nima? Branchlar bilan qanday ishlaysiz?

✅ **Javob:**

> Gitflow is a branching strategy with long-lived branches like `main` and `develop`, and short-lived branches like `feature/`, `hotfix/`, and `release/`.
> I usually work with `feature/` branches, submit PRs for code review, and use `rebase` for clean history.

---

### 🔸 4. **Code Review**

**Savol:** Siz loyihada CodeReview qilganmisiz? Nima qilasiz review paytida?

✅ **Javob:**

> Yes, I’ve participated in code reviews regularly. I check for:

* Code readability
* Reusability
* Adherence to project conventions
* Security vulnerabilities
* Test coverage
  I leave constructive comments and often suggest better naming or logic simplifications.

---

### 🔸 5. **CI/CD tushunchasi**

**Savol:** CI/CD nima? Siz qayerda ishlatgansiz?

✅ **Javob:**

> CI is Continuous Integration – tests and builds are run on every push.
> CD is Continuous Delivery or Deployment – new versions are automatically deployed to staging or production.
> I’ve used GitHub Actions and GitLab CI to automate testing, Docker image building, and deployment to EC2 and Kubernetes.

---

### 🔸 6. **Docker asoslari**

**Savol:** Docker haqida nima bilasiz?

✅ **Javob:**

> Docker allows us to package applications in containers, including all dependencies.
> I’ve used it to:

* Build Docker images from Dockerfiles
* Use docker-compose for multi-container setup (web + db + redis)
* Mount volumes for persistent data
* Debug container behavior with logs and `exec` commands

---

### 🔸 7. **REST API tushunchasi**

**Savol:** REST API nima? U bilan qanday ishlagansiz?

✅ **Javob:**

> REST is a stateless API architecture that uses standard HTTP methods.
> In Django REST Framework and FastAPI, I’ve built endpoints using serializers, routers, and response models. I followed REST conventions like:

* `GET /users/`
* `POST /users/`
* `PUT /users/{id}/`
* `DELETE /users/{id}/`

---

### 🔸 8. **Event Loop, Stream, Error Handling (Node.jsga mos, lekin analogi)**

**Savol:** Python’dagi async qanday ishlaydi? Node.js’ga o‘xshashmisiz?

✅ **Javob:**

> Yes, Python has async/await, which is similar to Node.js's event loop model.
> Using `asyncio`, FastAPI, and `aiohttp`, I’ve handled thousands of concurrent requests efficiently without blocking.
> Streams analogi – generatorlar (`yield`), or async iterators.

---

### 🔸 9. **Error handling: DRY & graceful degradation**

**Savol:** Katta tizimda error handlingni qanday qilasiz?

✅ **Javob:**

> I use a centralized exception handler. In Django/DRF I override `ExceptionHandler`, in FastAPI I use `@app.exception_handler`.
> I log detailed errors using Sentry and show users safe, helpful messages.

---

### 🔸 10. **Indexlar va SQL vs NoSQL**

**Savol:** Qachon SQL, qachon NoSQL ishlatish kerak?

✅ **Javob:**

> SQL – relational, structured data, need for complex queries, ACID – use PostgreSQL/MySQL.
> NoSQL – dynamic schema, scalability, high read/write throughput – use MongoDB, DynamoDB.
> Indexlar – searchni tezlashtiradi, lekin yozishdagi performance’ga ta’sir qilishi mumkin.

---

### 🔸 11. **Caching, Logging, Monitoring (Grafana, Sentry)**

**Savol:** Tizimni qanday observability bilan nazorat qilgansiz?

✅ **Javob:**

> I use:

* **Redis** for caching common queries
* **Sentry** for real-time error tracking
* **Grafana + Prometheus** for metrics (CPU, memory, DB queries)
* **Structured logging** (JSON format) for easier debugging in production

---

### 🔸 12. **OWASP Top 10 xavfsizlik xatoliklari**

**Savol:** Qaysi xavfsizlik xatolarni oldini olganmisiz?

✅ **Javob:**

> Ha, OWASP Top 10 asosida men quyidagilarga e’tibor berganman:

* SQL Injection → parametrized queries
* CSRF/XSS → Django’ning default himoyasi
* Broken Auth → JWT tokenlar bilan ishlash
* Sensitive Data Exposure → HTTPS, `env`-based config

---

### 🔸 13. **Manager Interview uchun tayyorlik**

**Savol:** Manager sizdan: “Nima proektga ishlashni istamaysiz?” deb so‘rasa?

✅ **Javob:**

> I prefer not to work on gambling or surveillance-related projects. I enjoy contributing to EdTech, FinTech, or public good systems.
