## 🚀 3-BO‘LIM: Deployment, Docker, Ansible, DevOps – savollar va javoblar

---

**1. Dockerfile optimizatsiyasi qanday qilinadi?**

* **Layer sonini kamaytirish** – `RUN` komandalarni birlashtirish
* `.dockerignore` bilan keraksiz fayllarni build'ga kiritmaslik
* Multistage build ishlatish

```dockerfile
FROM python:3.10-slim as builder
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

FROM python:3.10-slim
WORKDIR /app
COPY --from=builder /usr/local/lib/python3.10 /usr/local/lib/python3.10
COPY . .
CMD ["python", "main.py"]
```

---

**2. Docker Compose’ni qanday ishlatgansan?**

* Microservices arxitekturasi uchun `web`, `db`, `redis`, `nginx` container’lari bilan ishlaganman
* Har bir servis `.env` orqali konfiguratsiya qilinadi

```yaml
version: '3.8'

services:
  web:
    build: .
    ports: ["8000:8000"]
    env_file: .env
    depends_on: [db]
  
  db:
    image: postgres:15
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```

---

**3. `.env` faylni Docker'da qanday foydalanamiz?**

* `.env` fayl ichida `KEY=VALUE` juftliklar
* `env_file` orqali servisga ulaymiz
* Yoki `os.getenv("KEY")` bilan Python’da o‘qiymiz

---

**4. Ansible haqida nimalarni bilasan?**

* Idempotent konfiguratsiya manager
* Server provisioning, Nginx, Docker, security sozlamalari uchun ishlatiladi

```yaml
- name: Install and start nginx
  hosts: web
  become: true
  tasks:
    - apt:
        name: nginx
        state: present
    - service:
        name: nginx
        state: started
```

---

**5. CI/CD pipeline tuzganmisan?**

✅ Ha, GitHub Actions va GitLab CI/CD'da quyidagilarni qilganman:

* Testlarni ishga tushurish
* Docker image qurish va push qilish
* Serverga auto-deploy (scp, ssh, rsync orqali)

```yaml
name: Deploy
on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Build & Push
        run: |
          docker build -t myapp .
          docker tag myapp registry/myapp
          docker push registry/myapp
```

---

**6. Healthcheck, volume, secret handling?**

* `healthcheck` – servis sog‘lomligini tekshiradi (retry, interval)
* `volumes` – fayl sistemani saqlab qolish yoki `shared state` uchun
* Secrets: `.env`, Docker secrets, `Vault` yoki `AWS Parameter Store`

---

**7. Monitoring va logging qanday qilgansan?**

* `Sentry` – error’larni kuzatish
* `Grafana + Prometheus` – real-time monitoring
* `ELK stack` (Elasticsearch, Logstash, Kibana) – log tahlili

---

**8. Production serverda qanday troubleshoot qilasan?**

1. `docker logs <container>`
2. `htop`, `df -h`, `top`, `iotop`, `dmesg` – server monitoring
3. `curl`, `telnet`, `nc` – port/layer connectivity
4. `journalctl -u nginx`, `systemctl status` – servis loglari

---

**9. Nginx + SSL bilan reverse proxy?**

```nginx
server {
    listen 443 ssl;
    ssl_certificate /etc/ssl/cert.pem;
    ssl_certificate_key /etc/ssl/key.pem;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

---

**10. Infrastructure as Code haqida nima deysan?**

* Terraform orqali AWS/GCP resurslarini kod orqali boshqarish mumkin
* Version control, repeatability, rollback – katta ustunlik
