# ساخت اولین Solution مبتنی بر Clean Architecture برای SaaS

## مقدمه

بعد از آماده‌سازی محیط توسعه شامل:

* WSL2
* Ubuntu
* Docker
* .NET SDK
* NodeJS
* GitHub SSH

نوبت ساخت زیرساخت واقعی پروژه SaaS رسید.

هدف فقط ساخت یک Web API ساده نبود.

هدف، ایجاد یک ساختار Enterprise-Level و قابل توسعه از روز اول بود.

---

# چشم‌انداز پروژه

این SaaS برای مدیریت:

* تعویض روغنی‌ها
* مراکز خدمات خودرو
* سیستم چندتنانتی
* معماری Cloud-Native
* توسعه مبتنی بر AI

طراحی شده است.

معماری باید از ابتدا برای رشد بلندمدت آماده باشد.

---

# چرا Clean Architecture؟

Clean Architecture باعث جداسازی Business Logic از زیرساخت می‌شود.

مزایا:

* نگهداری آسان‌تر
* تست‌پذیری بهتر
* وابستگی کمتر
* توسعه‌پذیری بالا
* مهاجرت راحت‌تر در آینده
* همکاری بهتر با AI Agentها

---

# ساختار کلی Solution

به‌جای یک پروژه Monolith ساده، Solution به چند پروژه مستقل تقسیم شد.

ساختار:

```text id="4xh9l5"
src/
│
├── Api
├── Application
├── Domain
├── Persistence
├── Infrastructure
└── Identity
```

---

# ساخت Solution

## ایجاد فایل Solution

```bash id="m3r9kb"
dotnet new sln -n OilChangeSaaS
```

---

# ساخت پروژه‌ها

## پروژه API

```bash id="3x67eg"
dotnet new webapi -n Api
```

---

## لایه‌های Core

```bash id="mk0m75"
dotnet new classlib -n Application
dotnet new classlib -n Domain
```

---

## لایه‌های Infrastructure

```bash id="b7c6vx"
dotnet new classlib -n Persistence
dotnet new classlib -n Infrastructure
dotnet new classlib -n Identity
```

---

# چرا پروژه‌ها جدا شدند؟

هر پروژه مسئولیت مشخصی دارد.

---

# Domain

شامل:

* Entityها
* Enumها
* Value Objectها
* قوانین بیزینسی

این لایه قلب سیستم است.

نباید وابسته به Framework یا Database باشد.

---

# Application

شامل:

* DTOها
* CQRS
* Commands
* Queries
* Handlers
* Validators
* Interfaces

این لایه Use Caseهای سیستم را مدیریت می‌کند.

---

# Persistence

مسئول:

* Entity Framework Core
* DbContext
* Repository
* Migrations
* Configurations

است.

---

# Infrastructure

مسئول ارتباط با سرویس‌های خارجی:

* SMS
* File Storage
* Cache
* Third-party APIs

است.

---

# Identity

مسئول:

* Authentication
* Authorization
* JWT
* مدیریت کاربران

است.

---

# API

مسئول:

* Controllers
* Middleware
* Swagger
* HTTP Endpoints

است.

---

# جهت وابستگی‌ها (Dependency Direction)

یکی از مهم‌ترین مفاهیم Clean Architecture:

وابستگی‌ها باید به سمت داخل باشند.

ساختار:

```text id="jglxje"
Domain
↑
Application
↑
Infrastructure / Persistence / Identity
↑
API
```

این کار باعث می‌شود Business Logic وابسته به Database یا Frameworkها نباشد.

---

# معماری Modular Monolith

در حال حاضر پروژه به‌صورت Modular Monolith طراحی شده است.

چرا؟

چون:

* توسعه اولیه سریع‌تر است
* Debug ساده‌تر است
* Infrastructure سبک‌تر است
* MVP سریع‌تر آماده می‌شود

اما مرزبندی داخلی کاملاً رعایت شده است.

---

# مهاجرت آینده به Microservices

این معماری از ابتدا طوری طراحی شده که بعداً بتوان بخش‌ها را جدا کرد.

مثلاً:

* Identity Service
* Billing Service
* Notification Service
* Tenant Service

می‌توانند در آینده تبدیل به Microservice مستقل شوند.

بدون Rewrite سنگین.

---

# اولین Build موفق

بعد از تعریف Referenceها:

```bash id="rq8n61"
dotnet build
```

Build با موفقیت انجام شد.

این یعنی:

* Dependencyها صحیح هستند
* معماری سالم است
* Foundation پروژه پایدار است

---

# چیزهایی که یاد گرفتم

در این مرحله یاد گرفتم:

* مفاهیم واقعی Clean Architecture
* Dependency Direction
* جداسازی پروژه‌ها
* Modular Monolith
* ساختار Enterprise
* معماری مقیاس‌پذیر Backend

---

# نتیجه نهایی

موفق شدم:

* Foundation پروژه SaaS
* معماری Clean
* ساختار Modular
* Solution چند پروژه‌ای
* Dependency-safe Structure

را ایجاد کنم.

---

# مرحله بعدی

مرحله بعد شامل:

* Authentication
* Multi-Tenant Infrastructure
* SQL Server Container
* Docker Compose
* CQRS
* React Frontend
* AI-Native Workflow

خواهد بود.
