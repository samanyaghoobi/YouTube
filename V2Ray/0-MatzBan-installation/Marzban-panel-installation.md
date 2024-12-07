
# آموزش نصب و راه‌اندازی سرور V2Ray با پنل مرزبان در ۱۰ دقیقه

سلام دوستان! 👋 امروز قصد داریم در کمتر از ۱۰ دقیقه، یک سرور V2Ray را با استفاده از پنل مرزبان راه‌اندازی کنیم. آماده‌اید؟ بزن بریم! 🚀

---

## پیش‌نیازها

قبل از شروع، مطمئن شوید که موارد زیر را در اختیار دارید:

- **یک سرور مجازی (VPS)** با سیستم‌عامل اوبونتو
- **دسترسی به ترمینال** و آشنایی اولیه با دستورات لینوکس
- **یک دامنه یا زیردامنه** برای تنظیمات SSL

---

## مرحله ۱: اتصال به سرور

ابتدا در ترمینال دستور زیر را بزنید تا بتوانید به سرور خودتان یک اتصال SSH برقرار کنید.  
(اگر از ویندوز استفاده می‌کنید ابتدا دکمه ویندوز را بزنید و CMD را جستجو و باز کنید و دستور زیر را وارد کنید):

```bash
ssh username@your_server_ip
```

> **نکته:** `username` و `your_server_ip` را با اطلاعات کاربری و آی‌پی سرور خود جایگزین کنید.

---

## مرحله ۲: به‌روزرسانی و نصب پیش‌نیازها

در این مرحله، مخازن را به‌روزرسانی کرده و پیش‌نیازها را نصب کنید:

```bash
sudo apt update && sudo apt upgrade -y  # اجرای upgrade اختیاری است اما توصیه می‌شود.
sudo apt install -y curl
```

---

## مرحله ۳: نصب پنل مرزبان

مرجع: [Marzban Repository](https://github.com/Gozargah/Marzban)  
آموزش کامل نصب مرزبان به فارسی: [Marzban Installation Guide](https://github.com/Gozargah/Marzban/blob/master/README-fa.md)

برای نصب پنل مرزبان، اسکریپت زیر را اجرا کنید:

```bash
sudo bash -c "$(curl -sL https://github.com/Gozargah/Marzban-scripts/raw/master/marzban.sh)" @ install
```

> **نکته:** این دستور ممکن است چند دقیقه طول بکشد، لطفاً صبور باشید.

---

### رفع مشکلات احتمالی:

#### مشکل `docker-compose`:

![Docker-Compose-not_installed](docker-compose-error.png)

اگر با خطای `docker-compose` مواجه شدید، دستور زیر را اجرا کنید:

```bash
sudo apt install docker-compose
```

> اگر همچنان با `docker-compose` مشکل داشتید، از منبع زیر استفاده کنید:  
> [DigitalOcean Docker-Compose Guide](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04)

---

#### مشکل اتصال به Docker (برای سرورهای ایرانی):

![connection-error-of-docker](error_docker_connection.png)

اگر با مشکل اتصال به Docker مواجه شدید، مراحل زیر را دنبال کنید:

```bash
sudo apt install docker.io
```

سپس فایل تنظیمات Docker را به‌روزرسانی کنید:

```bash
sudo bash -c 'cat > /etc/docker/daemon.json <<EOF
{
  "insecure-registries" : ["https://docker.arvancloud.ir"],
  "registry-mirrors": ["https://docker.arvancloud.ir"]
}
EOF'
```

و در نهایت، Docker را مجدداً راه‌اندازی کنید:

```bash
docker logout
sudo systemctl restart docker
```

پس از این، می‌توانید مجدداً مرحله نصب پنل را انجام دهید.

---

## مرحله ۴: ایجاد کاربر ادمین

بعد از نصب، برای مدیریت پنل نیاز است یک کاربر ادمین با دسترسی روت ایجاد کنید:

```bash
marzban cli admin create --sudo
```

> **نکته:** حتماً نام کاربری و رمز عبور را یادداشت کنید.

---

## مرحله ۵: دسترسی به پنل

در نسخه‌های جدید مرزبان، برای دسترسی به پنل حتماً باید SSL داشته باشید.  
و چون فعلاً نداریم، برای دور زدن این محدودیت، هربار خواستید به پنل مرزبان وصل شوید، ابتدا دستور زیر را در ترمینال بزنید:

```bash
ssh -L 8000:localhost:8000 user@server
```

سپس می‌توانید از طریق مرورگر به آدرس زیر مراجعه کنید:

```
http://localhost:8000/dashboard/login
```

> **نکته:** به جای `user@server`، اطلاعات کاربری و آدرس سرور خود را وارد کنید.

---

## جمع‌بندی

تبریک می‌گویم! 🎉 شما با موفقیت یک سرور V2Ray را با پنل مرزبان راه‌اندازی کردید و دسترسی ایمن به پنل را تنظیم نمودید.  
اکنون می‌توانید از اینترنت با امنیت و سرعت بالا لذت ببرید.  
اگر سوالی داشتید، حتماً در بخش نظرات بپرسید.

تا راهنمای بعدی، خداحافظ! 👋