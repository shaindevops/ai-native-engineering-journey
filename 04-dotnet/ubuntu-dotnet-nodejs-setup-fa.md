# نصب .NET SDK و Node.js روی Ubuntu داخل WSL2

## مقدمه

بعد از نصب WSL2 و Ubuntu روی ویندوز، برای شروع توسعه پروژه‌های AI-Native و SaaS نیاز داشتم ابزارهای اصلی توسعه را نصب کنم.

در این مرحله:

* .NET SDK
* Node.js
* npm

را روی Ubuntu نصب کردم.

---

# نصب .NET SDK

ابتدا بررسی کردم که آیا dotnet نصب است یا نه:

```bash
dotnet --version
```

سیستم پیام داد که dotnet نصب نیست.

---

## نصب .NET SDK 10

دستور نصب:

```bash
sudo apt-get update && \
sudo apt-get install -y dotnet-sdk-10.0
```

---

## بررسی نصب

بعد از نصب:

```bash
dotnet --version
```

خروجی:

```bash
10.x.x
```

---

# نصب Node.js و npm

ابتدا بررسی کردم:

```bash
node -v
```

سیستم نشان داد که Node.js نصب نیست.

---

## نصب Node.js

```bash
sudo apt install nodejs
```

در طول نصب، npm و وابستگی‌ها نیز نصب شدند.

---

# بررسی نصب Node.js و npm

```bash
node -v
npm -v
```

خروجی:

```bash
v22.x.x
11.x.x
```

---

# نکات مهم

## 1. استفاده از Linux Development Environment

اجرای پروژه‌ها داخل WSL2 بسیار پایدارتر و حرفه‌ای‌تر از اجرای مستقیم روی ویندوز است، مخصوصاً برای:

* Docker
* Kubernetes
* DevOps
* AI Agents
* پروژه‌های Cloud-Native

---

## 2. اهمیت مستندسازی

ثبت کردن مراحل نصب و خطاها باعث می‌شود:

* بعدها سریع‌تر محیط را بازسازی کنیم
* AI Agentها context بهتری داشته باشند
* اعضای تیم راحت‌تر onboard شوند

---

# وضعیت فعلی Environment

✅ WSL2
✅ Ubuntu
✅ GitHub SSH Auth
✅ Cursor AI
✅ .NET SDK 10
✅ Node.js
✅ npm

---

# قدم بعدی

مرحله بعد:

* نصب Docker Desktop
* اتصال Docker به WSL2
* ساخت Solution پروژه SaaS
* طراحی معماری Clean Architecture
* شروع Foundation پروژه

---

# AI Native Engineering Journey

این ریپو بخشی از مسیر ساخت یک SaaS واقعی با کمک AI Agentها، معماری مدرن و Cloud-Native Engineering است.
