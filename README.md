# Elnus — Landing Page

سایت فرود (Landing Page) شرکت Elnus، بر اساس طرح اینفوگرافیک اولیه، به‌صورت یک صفحه استاتیک حرفه‌ای پیاده‌سازی شده است.

## ساختار پروژه
```
elnus-landing/
├── index.html        صفحه اصلی (تمام محتوا و بخش‌ها)
├── css/style.css      استایل کامل صفحه (توکن‌های طراحی، ریسپانسیو، انیمیشن)
├── js/script.js       منوی موبایل، اسکرول نرم، انیمیشن Reveal on Scroll
└── assets/favicon.svg آیکون سایت
```

## ویژگی‌های فنی
- **بدون نیاز به Build/Framework** — HTML/CSS/JS خالص، مستقیماً قابل انتشار روی هر هاستینگ استاتیک
- **کاملاً ریسپانسیو** — از موبایل (۳۲۰px) تا دسکتاپ بزرگ
- **راست‌به‌چپ (RTL)** با فونت Vazirmatn (فارسی) و Space Grotesk (اعداد/لاتین)
- **قابلیت دسترسی (Accessibility)** — Focus state مشخص، `prefers-reduced-motion` رعایت‌شده، ساختار معنایی HTML5
- **بهینه برای سئو** — تگ‌های meta، ساختار heading صحیح
- **بدون وابستگی خارجی** به‌جز فونت گوگل (قابل self-host در صورت نیاز به حذف وابستگی به CDN)

## نحوه اجرا (Local)
فقط فایل `index.html` را در مرورگر باز کنید، یا با یک سرور استاتیک ساده اجرا کنید:
```bash
npx serve elnus-landing
# یا
python3 -m http.server --directory elnus-landing 8080
```

## استقرار روی سرور (Deployment)

### گزینه ۱: هر هاست استاتیک (توصیه‌شده)
کل پوشه `elnus-landing/` را روی یکی از موارد زیر آپلود کنید:
- Nginx / Apache (کپی در `/var/www/elnus` و تنظیم root)
- Vercel / Netlify / Cloudflare Pages (Drag & drop یا اتصال به Git)
- هر CDN استاتیک

### نمونه تنظیمات Nginx
```nginx
server {
    listen 80;
    server_name elnus.example.com;
    root /var/www/elnus-landing;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~* \.(css|js|svg)$ {
        expires 30d;
        add_header Cache-Control "public, immutable";
    }
}
```

## نکات پیش از انتشار نهایی (Checklist)
- [ ] لینک‌های تماس (`tel:`, `sms:`, تلگرام، لینکدین) را با شماره/آدرس واقعی جایگزین کنید — در حال حاضر placeholder هستند
- [ ] در صورت نیاز، بارگذاری فونت گوگل را به‌صورت Self-hosted تغییر دهید تا وابستگی به CDN خارجی حذف شود
- [ ] تصویر QR Code واقعی (لینک به فرم رزرو دمو) را جایگزین نسخه تزئینی موجود کنید
- [ ] Google Analytics / ابزار رصد رفتار کاربر را در صورت نیاز اضافه کنید
- [ ] favicon و متادیتای Open Graph برای اشتراک‌گذاری در شبکه‌های اجتماعی تکمیل شود
