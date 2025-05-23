# بک‌اند سیستم ERP یراق‌آلات ناصری

این بخش شامل کد منبع بک‌اند سیستم مدیریت منابع سازمانی (ERP) برای فروشگاه یراق‌آلات ناصری است که با استفاده از Django و Django REST Framework توسعه داده شده است.

## تکنولوژی‌های استفاده شده

- Python 3.8+
- Django 5.0.7+
- Django REST Framework 3.16.0+
- SQLite (برای محیط توسعه)
- JWT برای احراز هویت

## پیش‌نیازها

- Python 3.8 یا بالاتر
- pip (مدیر بسته‌های Python)
- دسترسی به ترمینال یا خط فرمان

## نصب و راه‌اندازی

### روش اول: استفاده از فایل batch (ویندوز)

1. فایل `setup_and_run.bat` را اجرا کنید:
   ```
   setup_and_run.bat
   ```
   
2. این فایل به صورت خودکار محیط مجازی را ایجاد می‌کند، پکیج‌های مورد نیاز را نصب می‌کند و سرور را اجرا می‌کند.

### روش دوم: راه‌اندازی دستی

1. ایجاد محیط مجازی:
   ```
   python -m venv venv
   ```

2. فعال‌سازی محیط مجازی:
   - ویندوز (CMD):
     ```
     venv\Scripts\activate
     ```
   - ویندوز (PowerShell):
     ```
     .\venv\Scripts\Activate.ps1
     ```  
   - لینوکس/مک:
     ```
     source venv/bin/activate
     ```

3. نصب پکیج‌های مورد نیاز:
   ```
   pip install -r requirements.txt
   ```

4. اجرای مایگریشن‌ها:
   ```
   python manage.py migrate
   ```

5. ایجاد کاربر ادمین (اختیاری):
   ```
   python manage.py createsuperuser
   ```

6. اجرای سرور:
   ```
   python manage.py runserver
   ```

7. حالا می‌توانید به آدرس `http://localhost:8000/admin/` مراجعه کنید و وارد پنل مدیریت شوید.

## ساختار پروژه

```
├── manage.py              # فایل اصلی مدیریت پروژه Django
├── requirements.txt       # لیست پکیج‌های مورد نیاز
├── db.sqlite3             # پایگاه داده SQLite
│
├── naseri_erp/            # پکیج اصلی پروژه
│   ├── __init__.py
│   ├── settings.py        # تنظیمات پروژه
│   ├── urls.py            # تنظیمات URL اصلی
│   └── wsgi.py            # تنظیمات WSGI
│
├── products/              # ماژول مدیریت محصولات
│   ├── models.py          # مدل‌های پایگاه داده
│   ├── serializers.py     # سریالایزرها برای API
│   ├── views.py           # نماها برای API
│   └── urls.py            # مسیرهای URL محصولات
│
├── inventory/             # ماژول مدیریت موجودی
│
├── sales/                 # ماژول مدیریت فروش
│   ├── models.py          # مدل‌های مرتبط با فروش
│   ├── serializers.py     # سریالایزرهای فروش
│   ├── views.py           # نماهای API فروش
│   └── urls.py            # مسیرهای URL فروش
│
├── purchases/             # ماژول مدیریت خرید
│
├── accounting/            # ماژول مدیریت حسابداری
│
├── users/                 # ماژول مدیریت کاربران
│   ├── models.py          # مدل کاربر سفارشی
│   ├── serializers.py     # سریالایزرهای کاربران
│   ├── views.py           # نماهای API کاربران
│   └── urls.py            # مسیرهای URL کاربران
│
├── static/                # فایل‌های استاتیک
│
└── media/                 # فایل‌های آپلود شده
```

## API‌های اصلی

### مدیریت کاربران

- `POST /api/users/token/`: دریافت توکن احراز هویت
- `GET /api/users/profile/`: دریافت اطلاعات پروفایل کاربر جاری
- `PUT /api/users/profile/`: به‌روزرسانی اطلاعات پروفایل

### مدیریت محصولات

- `GET /api/products/`: دریافت لیست محصولات
- `POST /api/products/`: ایجاد محصول جدید
- `GET /api/products/<id>/`: دریافت جزئیات یک محصول
- `PUT /api/products/<id>/`: به‌روزرسانی یک محصول
- `DELETE /api/products/<id>/`: حذف یک محصول
- `GET /api/categories/`: دریافت لیست دسته‌بندی‌ها
- `GET /api/units/`: دریافت لیست واحدهای اندازه‌گیری

### مدیریت موجودی

- `GET /api/inventory/stock/`: دریافت موجودی انبار
- `POST /api/inventory/transactions/`: ثبت تراکنش موجودی
- `GET /api/inventory/warehouses/`: دریافت لیست انبارها

### مدیریت فروش

- `GET /api/sales/sales/`: دریافت لیست فروش‌ها
- `POST /api/sales/sales/`: ثبت فروش جدید
- `GET /api/sales/sales/<id>/`: دریافت جزئیات یک فروش
- `PUT /api/sales/sales/<id>/`: به‌روزرسانی اطلاعات فروش
- `DELETE /api/sales/sales/<id>/`: حذف یک فروش
- `GET /api/sales/customers/`: دریافت لیست مشتریان
- `POST /api/sales/customers/`: افزودن مشتری جدید
- `GET /api/sales/invoices/`: دریافت لیست فاکتورها
- `GET /api/sales/reports/`: دریافت گزارش‌های فروش

## سیستم مدیریت فروش

سیستم مدیریت فروش یکی از بخش‌های کلیدی این پروژه است که شامل موارد زیر می‌باشد:

### مدل‌های اصلی

1. **Customer**: 
   - مدل مشتری شامل اطلاعات تماس و خرید
   - دارای فیلدهایی مانند نام، تلفن، ایمیل، آدرس و حد اعتبار
   - متد محاسبه مجموع بدهی مشتری

2. **Sale**:
   - مدل اصلی فروش شامل اطلاعات فاکتور
   - دارای فیلدهایی مانند شماره فاکتور، مشتری، وضعیت، تاریخ و مبلغ
   - ویژگی‌هایی برای محاسبه جمع کل و مالیات

3. **SaleItem**:
   - مدل اقلام فروش برای نگهداری جزئیات محصولات فروخته شده
   - شامل مرجع به فروش، محصول، تعداد، قیمت واحد و تخفیف
   - متد محاسبه قیمت کل هر قلم

4. **Invoice**:
   - مدل فاکتور برای مدیریت جنبه‌های مالی فروش
   - شامل فیلدهایی مانند شماره فاکتور، مشتری، مبلغ کل و مانده

5. **Payment**:
   - مدل پرداخت برای ثبت پرداخت‌های مرتبط با فاکتورها
   - شامل فیلدهایی مانند شماره پرداخت، مرجع فاکتور، مبلغ و روش پرداخت

### API‌های مدیریت فروش

API‌های مدیریت فروش از طریق ViewSet‌ها پیاده‌سازی شده‌اند که امکان انجام عملیات CRUD کامل روی مدل‌ها را فراهم می‌کنند. برخی از ویژگی‌های این API‌ها عبارتند از:

- فیلتر کردن فروش‌ها بر اساس مشتری، تاریخ و وضعیت
- جستجو در فاکتورها بر اساس شماره فاکتور یا نام مشتری
- مرتب‌سازی نتایج بر اساس فیلدهای مختلف
- مدیریت حقوق دسترسی برای کاربران مختلف

## به‌روزرسانی‌های اخیر

- بهبود مدل‌های فروش و ارتباط آن‌ها با سیستم موجودی
- افزودن API‌های مورد نیاز برای مدیریت مشتریان و فاکتورها
- پیاده‌سازی سیستم گزارش‌گیری فروش
- بهینه‌سازی کوئری‌ها برای افزایش سرعت و کارایی
- ساده‌سازی API‌ها برای استفاده آسان‌تر در فرانت‌اند

## عیب‌یابی متداول

### مشکل در اجرای مایگریشن‌ها

اگر با خطا در اجرای مایگریشن‌ها مواجه شدید:
1. فایل پایگاه داده `db.sqlite3` را حذف کنید
2. مایگریشن‌ها را مجدداً اجرا کنید:
   ```
   python manage.py migrate
   ```

### خطای CORS

اگر با خطای CORS در هنگام ارتباط با فرانت‌اند مواجه شدید:
1. مطمئن شوید که `django-cors-headers` نصب شده است
2. تنظیمات CORS را در `settings.py` بررسی کنید:
   ```python
   CORS_ALLOW_ALL_ORIGINS = True  # در محیط توسعه
   # یا
   CORS_ALLOWED_ORIGINS = [
       "http://localhost:5173",
       "http://127.0.0.1:5173",
   ]
   ```

### خطای احراز هویت

اگر با مشکل احراز هویت مواجه شدید:
1. مطمئن شوید که مسیرهای API با `/api/` شروع می‌شوند
2. توکن را در هدر درخواست‌ها قرار دهید: `Authorization: Token <your_token>`
3. ببینید که `rest_framework.authtoken` در `INSTALLED_APPS` در `settings.py` وجود دارد

## مستندات API

برای دسترسی به مستندات کامل API، پس از اجرای سرور، به آدرس‌های زیر مراجعه کنید:

- **Swagger UI**: `http://127.0.0.1:8000/swagger/`
- **ReDoc**: `http://127.0.0.1:8000/redoc/` 