# موقع محسن حيدر الحكيم — الموقع الشخصي

موقع شخصي مبني بـ **React + Node.js + SQL Server**.

---

## المتطلبات

- **Node.js** 18+
- **SQL Server** (Express / Developer) مثبت محلياً — الاتصال عبر Windows Authentication

---

## أول مرة (الإعداد الكامل)

```powershell
cd f:\MohsenWeb

# 1. تثبيت كل الحزم (root + backend + frontend)
npm run install:all

# 2. إنشاء قاعدة البيانات وتشغيل الـ migrations تلقائياً
npm run migrate

# 3. إنشاء حساب المدير الافتراضي (admin / admin123)
npm run seed
```

---

## تشغيل المشروع

```powershell
cd f:\MohsenWeb
npm run dev
```

يفتح **نافذة واحدة** تشغّل الـ backend والـ frontend معاً:

| الخدمة   | الرابط                    |
|----------|---------------------------|
| Frontend | http://localhost:5173     |
| Backend  | http://localhost:4000     |
| Health   | http://localhost:4000/api/health |

---

## الصفحات

| الرابط                              | الوصف                  |
|--------------------------------------|------------------------|
| `http://localhost:5173/`             | الموقع العام           |
| `http://localhost:5173/admin/login`  | دخول لوحة التحكم       |
| `http://localhost:5173/admin`        | لوحة التحكم (محمية)   |

**بيانات الدخول الافتراضية:** `admin` / `admin123`

---

## نظام الـ Migrations

- كل migration هو ملف `.sql` في `backend/src/db/migrations/`
- يتم تطبيق الـ migrations تلقائياً عند كل إقلاع للـ backend (مرة واحدة فقط لكل ملف)
- يمكن إضافة migrations جديدة بأسماء مرتبة: `006_new_feature.sql`

لتشغيل الـ migrations يدوياً:

```powershell
npm run migrate
```

---

## إعدادات قاعدة البيانات

الملف: `backend/.env`

```
DB_SERVER=DESKTOP-MJ34SAJ
DB_NAME=MohsenWebDB
DB_TRUSTED_CONNECTION=true
PORT=4000
JWT_SECRET=... (غيّره قبل النشر)
ADMIN_USERNAME=admin
ADMIN_PASSWORD=admin123
FRONTEND_ORIGIN=http://localhost:5173
```

---

## ملاحظات أمنية قبل النشر

1. **غيّر `JWT_SECRET`** في `.env` إلى قيمة طويلة عشوائية
2. **غيّر كلمة مرور المدير**: عدّل `.env` ثم نفذ `npm run seed`
3. **لا ترفع `.env` إلى GitHub** (مضاف في `.gitignore`)
4. استخدم HTTPS في الإنتاج

---

## هيكل المشروع

```
MohsenWeb/
├── package.json              ← run واحد يشغل الكل
├── images/                   ← الصور الأصلية
├── frontend/
│   ├── public/
│   │   ├── profile.jpg       ← الصورة الشخصية
│   │   └── logo.png          ← شعار الموقع
│   └── src/
│       ├── components/       ← Hero, About, Projects, CareerGraph, Contact
│       ├── admin/            ← لوحة التحكم
│       └── styles/global.css ← كل الـ CSS
├── backend/
│   ├── src/
│   │   ├── server.js
│   │   ├── routes/           ← auth, about, projects, companies, upload
│   │   └── db/
│   │       ├── migrate-auto.js
│   │       ├── migrations/   ← 001...005 .sql
│   │       └── seed-admin.js
│   └── uploads/              ← الصور المرفوعة من لوحة التحكم
└── database/
    └── schema.sql            ← للمرجع فقط (المشروع يستخدم migrations)
```
