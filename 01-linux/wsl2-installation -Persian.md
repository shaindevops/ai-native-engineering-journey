# مسیر نصب و راه‌اندازی WSL2 و GitHub SSH روی ویندوز 10

## مقدمه

برای شروع توسعه یک پلتفرم SaaS مبتنی بر معماری Cloud-Native و AI-Assisted، نیاز به یک محیط توسعه لینوکسی پایدار وجود داشت.

هدف این محیط توسعه:

* اجرای Docker
* توسعه ASP.NET Core
* آماده‌سازی برای Kubernetes
* اجرای Workflowهای مبتنی بر AI
* توسعه Multi-Tenant SaaS

بود.

به همین دلیل WSL2 (Windows Subsystem for Linux 2) به‌عنوان اولین زیرساخت اصلی انتخاب شد.

---

# شروع نصب WSL2

ابتدا نصب WSL با دستور زیر انجام شد:

```powershell id="xmrhyg"
wsl --install
```

در ابتدا ویندوز شروع به نصب موارد زیر کرد:

* Virtual Machine Platform
* Windows Subsystem for Linux

اما در ادامه خطای زیر نمایش داده شد:

```text id="o7w80p"
Installing: Windows Subsystem for Linux
Catastrophic failure
```

---

# بررسی علت خطا

برای بررسی وضعیت Virtualization سیستم از دستور زیر استفاده شد:

```powershell id="31nd5z"
systeminfo
```

خروجی نشان داد که Hyper-V و Virtualization فعال هستند:

```text id="n5nyc9"
Hyper-V Requirements:
A hypervisor has been detected.
```

این موضوع نشان می‌داد:

* Virtualization در BIOS فعال است
* Hyper-V فعال است
* پردازنده از Virtualization پشتیبانی می‌کند
* مشکل به احتمال زیاد مربوط به نصب ناقص یا خراب WSL بوده است

---

# تعمیر WSL

برای رفع مشکل، ابتدا Featureهای مرتبط غیرفعال شدند.

## غیرفعال‌سازی Featureها

```powershell id="y6kh2x"
dism /online /disable-feature /featurename:Microsoft-Windows-Subsystem-Linux /norestart

dism /online /disable-feature /featurename:VirtualMachinePlatform /norestart

dism /online /disable-feature /featurename:Hyper-V /norestart
```

سپس سیستم Restart شد.

---

# فعال‌سازی مجدد Featureها

بعد از Restart، Featureها دوباره فعال شدند:

```powershell id="r0v3x4"
dism /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

dism /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

dism /online /enable-feature /featurename:Hyper-V /all /norestart
```

و مجدداً سیستم Restart شد.

---

# نصب موفق Ubuntu

این بار Ubuntu مستقیماً با دستور زیر نصب شد:

```powershell id="4m0y06"
wsl --install -d Ubuntu
```

و نصب با موفقیت انجام شد:

```text id="ndjlwm"
Distribution successfully installed.
Launching Ubuntu...
Provisioning the new WSL instance Ubuntu
```

---

# ساخت کاربر لینوکس

در هنگام ساخت User اولیه لینوکس، ابتدا تلاش شد از حروف فارسی استفاده شود که با خطا مواجه شد.

دلیل:

لینوکس برای Username قوانین مشخصی دارد:

* باید با حروف کوچک انگلیسی شروع شود
* فقط شامل:

  * حروف انگلیسی کوچک
  * عدد
  * underscore
  * dash

باشد.

در نهایت User زیر ساخته شد:

```text id="bwj9r7"
shain
```

و محیط Ubuntu با موفقیت اجرا شد.

---

# مشکل Authentication گیت‌هاب

بعد از نصب WSL، هنگام Clone کردن Repository گیت‌هاب، خطای زیر دریافت شد:

```text id="8f5c8h"
Password authentication is not supported for Git operations.
```

دلیل این خطا:

GitHub دیگر از Password معمولی برای Git استفاده نمی‌کند.

---

# راه‌اندازی SSH برای GitHub

برای حل مشکل، SSH Key ساخته شد.

## ساخت SSH Key

```bash id="cqkhpd"
ssh-keygen -t ed25519 -C "shaindevops@gmail.com"
```

در اولین تلاش، اشتباهاً به‌جای استفاده از مسیر پیش‌فرض، نام فایل `default` وارد شد و کلید در مسیر اشتباه ذخیره شد.

در نتیجه دستور زیر خطا داد:

```bash id="1m9e8m"
ssh-add ~/.ssh/id_ed25519
```

چون فایل موردنظر وجود نداشت.

---

# ساخت مجدد SSH Key

فایل‌های اشتباه حذف شدند و SSH Key دوباره با مسیر پیش‌فرض ساخته شد.

سپس SSH Agent اجرا شد:

```bash id="2bqk2o"
eval "$(ssh-agent -s)"
```

و کلید به Agent اضافه شد:

```bash id="h0jfx7"
ssh-add ~/.ssh/id_ed25519
```

---

# اتصال SSH به GitHub

کلید Public با دستور زیر دریافت شد:

```bash id="xwz4u0"
cat ~/.ssh/id_ed25519.pub
```

و داخل تنظیمات GitHub SSH Keys اضافه شد.

---

# تایید Fingerprint گیت‌هاب

در اولین اتصال SSH، پیام زیر نمایش داده شد:

```text id="y4kkrx"
The authenticity of host 'github.com' can't be established.
```

که طبیعی است.

پس از تایپ:

```text id="ll5m1q"
yes
```

اتصال تایید شد.

---

# احراز هویت موفق

در نهایت پیام زیر نمایش داده شد:

```text id="w8f8zt"
Hi shaindevops! You've successfully authenticated
```

که نشان می‌دهد:

* SSH به‌درستی تنظیم شده
* GitHub Authentication فعال است
* WSL آماده استفاده است
* محیط توسعه لینوکسی با موفقیت راه‌اندازی شده است

---

# نتیجه نهایی

اکنون سیستم آماده موارد زیر است:

* توسعه ASP.NET Core
* اجرای Docker
* Containerized Development
* Workflowهای AI-Assisted
* توسعه SaaS چندتنانتی
* آماده‌سازی برای Kubernetes و Cloud Infrastructure

---

# نکات مهمی که یاد گرفتم

## WSL

* بسیاری از خطاهای WSL مربوط به نصب ناقص Featureهای ویندوز هستند
* Hyper-V و Virtualization برای WSL2 حیاتی هستند

## GitHub

* Password Authentication منسوخ شده
* SSH بهترین روش اتصال حرفه‌ای به GitHub است

## Linux Workflow

* توسعه مبتنی بر لینوکس برای Docker و Cloud بسیار پایدارتر و حرفه‌ای‌تر است
* WSL2 بهترین نقطه شروع برای ورود به DevOps و Cloud-Native Development روی ویندوز است
