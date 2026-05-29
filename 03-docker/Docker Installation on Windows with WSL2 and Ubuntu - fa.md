# نصب Docker روی ویندوز با WSL2 و Ubuntu

## مقدمه

در این مرحله از مسیر AI-Native Engineering، تصمیم گرفتم Docker را به‌صورت اصولی روی ویندوز نصب کنم و آن را به Ubuntu داخل WSL2 متصل کنم.

هدف اصلی، ساخت یک محیط توسعه واقعی مبتنی بر Linux برای توسعه نرم‌افزارهای Containerized بود.

این زیرساخت برای موارد زیر ضروری است:

* توسعه Backend مدرن
* DevOps
* Kubernetes
* Cloud-Native Applications
* معماری‌های مقیاس‌پذیر

---

# چرا Docker؟

Docker اجازه می‌دهد برنامه‌ها و وابستگی‌های آن‌ها داخل Container اجرا شوند.

مزایا:

* اجرای یکسان در همه محیط‌ها
* استقرار آسان‌تر
* مقیاس‌پذیری بهتر
* سازگاری با Cloud
* ساده‌سازی CI/CD

---

# چرا WSL2؟

Docker ذاتاً برای Linux طراحی شده است.

اجرای Docker داخل محیط Linux بسیار طبیعی‌تر و پایدارتر از اجرای مستقیم روی Windows است.

WSL2 امکانات زیر را فراهم می‌کند:

* کرنل واقعی Linux
* Performance بهتر فایل‌ها
* ابزارهای Native لینوکس
* سازگاری بهتر Docker

به همین دلیل اکثر Backend Developerها و DevOps Engineerها ترجیح می‌دهند محیط Linux داشته باشند.

---

# نصب Docker Desktop روی Windows

ابتدا Docker Desktop را روی Windows نصب کردم.

پس از نصب:

* WSL2 Integration فعال شد
* Ubuntu Integration فعال شد
* Docker Desktop ری‌استارت شد

---

# اتصال Docker به Ubuntu

داخل Docker Desktop:

## مسیر:

```text id="4n4j2o"
Settings → Resources → WSL Integration
```

سپس Ubuntu را فعال کردم.

این کار باعث شد Docker Engine مستقیماً داخل Ubuntu در دسترس باشد.

---

# تست نصب Docker

داخل ترمینال Ubuntu دستور زیر اجرا شد:

```bash id="i2k2gx"
docker run hello-world
```

خروجی موفق:

```bash id="f5v1lb"
Hello from Docker!
```

این یعنی:

* Docker Engine سالم است
* اتصال WSL2 درست کار می‌کند
* Ubuntu به Docker daemon متصل شده است

---

# اولین خطایی که مشاهده کردم

## خطا

```bash id="1m6c1j"
Unable to find image 'hello-world:latest' locally
```

در نگاه اول شبیه Error بود.

اما در واقع Docker اعلام می‌کرد که Image موردنظر روی سیستم وجود ندارد و در حال دانلود آن از Docker Hub است.

پس از دانلود، Container با موفقیت اجرا شد.

---

# تفاوت Docker Desktop و Docker Engine

## Docker Desktop

یک نرم‌افزار مدیریتی برای Windows و Mac است.

شامل:

* Docker Engine
* رابط گرافیکی
* مدیریت Containerها
* WSL Integration

---

## Docker Engine

هسته اصلی Docker است که مسئول:

* اجرای Containerها
* مدیریت Imageها
* Networking
* Volumes

می‌باشد.

در واقع Docker Desktop فقط یک لایه مدیریتی روی Docker Engine است.

---

# چرا Docker در Linux طبیعی‌تر است؟

Docker از ابتدا برای Linux طراحی شده است.

Linux قابلیت‌هایی مثل:

* cgroups
* namespaces
* container primitives

را به‌صورت Native ارائه می‌دهد.

WSL2 باعث می‌شود Windows رفتار Linux-مانند داشته باشد و تجربه توسعه Backend بسیار بهتر شود.

---

# چیزهایی که یاد گرفتم

در این مرحله یاد گرفتم:

* تفاوت Docker Desktop و Docker Engine
* اهمیت Linux در Backend Development
* نحوه اتصال Docker به WSL2
* مفاهیم اولیه Container
* تست اولیه Docker
* پایه‌های Cloud-Native Development

---

# نتیجه نهایی

موفق شدم:

* Docker Desktop
* WSL2
* Ubuntu Integration
* Docker Engine
* Linux Development Environment

را با موفقیت راه‌اندازی کنم.

اکنون سیستم آماده است برای:

* ASP.NET Core
* SQL Server Container
* Redis
* Docker Compose
* Kubernetes
* Microservices
* AI-Native Development

---

# مرحله بعدی

مرحله بعد، ساخت اولین Solution واقعی مبتنی بر Clean Architecture و Modular Monolith است.
