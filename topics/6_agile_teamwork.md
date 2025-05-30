## 👥 6-BO‘LIM: Agile, Teamwork, Behavioral savollar – savollar va javoblar

---

### **1. Agile jarayonida qanday rol o‘ynagansan?**

✅ Javob (real-case-style):

> Men backend developer sifatida **2 haftalik sprintlar** bilan ishlaganman. Sprint planningda **task estimation** (story point), **tech stack tanlash**, va `API interface`lar kelishishda faol qatnashganman.
> Har bir sprintda `review + retro` bo‘ladi, bu orqali jarayonni yaxshilaymiz.

---

### **2. SCRUM haqida nima bilasan?**

* SCRUM – Agile’ning implementation formasi
* 4 ta asosiy sessiya:

  * Sprint planning
  * Daily stand-up
  * Sprint review
  * Retrospective

👥 Rollar:

* Product Owner
* Scrum Master
* Development Team

---

### **3. Code review’da qanday fikr bildirasan?**

> Men constructive feedback tarafdoriman. Har doim quyidagilarga e’tibor beraman:
>
> * Naming clarity
> * Function length (SRP printsipiga muvofiq)
> * Reusability
> * Test coverage

📌 **Criticize the code, not the coder.**

---

### **4. Konflikt bo‘lgan holatni aytib ber (STAR formatda)**

> **S**: Frontend jamoasi bilan API dizayni borasida ziddiyat bo‘ldi.
> **T**: Ularga kerak bo‘lgan response tuzilmasi juda murakkab edi.
> **A**: Figma, Postman va Swagger asosida `contract first` yondashuvni taklif qildim.
> **R**: Endi har bir endpoint Swagger'da kelishiladi va bu jarayon 40% tezlashdi.

---

### **5. Qanday qilib yangi texnologiyani jamoaga joriy qilganing bor?**

> Pandasdan Polarsga o‘tishni jamoaga taklif qilganman. Avval profiling qildim (`%timeit` + memory check), so‘ng PoC yozdim.
> Natijada 1M qatorli dataset uchun 4x tezlikka erishdik va shundan keyin migration plan yozildi.

---

### **6. Deadline yaqin, lekin vaqt yetmayapti. Nima qilasan?**

> Avvaliga task’ni **T-shirt sizing** orqali tahlil qilaman (S/M/L/XL).
> Keyin:
>
> * Vazifani ajrataman (prioritize)
> * MVP ni belgilayman
> * Stakeholderlarga vaqt yetishmasligini **asosli** tushuntiraman
> * Scope’ni kamaytirib yoki deadline’ni realga o‘zgartiramiz

---

### **7. Remote jamoa bilan qanday ishlagansan?**

> Telegram, Slack, Zoom – barcha vositalar bilan ishlaganman.
> Har kuni 5 daqiqalik status yozamiz (`Done`, `Doing`, `Blockers`).
> Kod birinchi navbatda **doc + test + type hint** bo‘lishi shart. Remote’da bu juda kerakli.

---

### **8. “Impactful contribution”ingni ayt**

> Django REST API'mizda 8.6s javob vaqt bor edi.
> Men `select_related`, `redis caching`, `prefetch_related`, `DRF pagination` yordamida **1.2s** ga tushirdim.
> Bu 400k userli platformada 3x ko‘proq userni ko‘tarishga imkon berdi.

---

### **9. Mentoring qilganmisan?**

> Ha. Junior dev’ga DRF serializer’lar, signal’lar, va model inheritance’ni o‘rgatganman.
> Har hafta `code walk-through`, va GitHub pull requestlarda feedback yozaman.

---

### **10. Kode misollarida kommunikatsiyang qanday?**

> Har bir function’ni `why` va `how` asosida yozaman.
> Git commit message’larim:
>
> ```
> fix(auth): validate user PIN in pre-save signal
> feat(payment): retry failed invoices after webhook delay
> ```

