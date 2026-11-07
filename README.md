# 🛠️ Mihan Platform | منصة مِهَن للخدمات المهنية المتكاملة

[![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?logo=flutter&logoColor=white)](https://flutter.dev)
[![PHP](https://img.shields.io/badge/PHP-8.2+-777BB4?logo=php&logoColor=white)](https://www.php.net/)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?logo=mysql&logoColor=white)](https://www.mysql.com/)
[![License](https://img.shields.io/badge/License-Proprietary-red.svg)](LICENSE)
[![Architecture](https://img.shields.io/badge/Architecture-Monorepo%20Full--Stack-blue.svg)](#)

---

## 📌 نبذة عامة (Project Overview)

**منصة مِهَن (Mihan Platform)** هي حل رقمي متكامل يربط بين طالبي الخدمات (العملاء) ومقدمي الخدمات الحرفية والمهنية (الفنيين والمهنيين) مع لوحات تحكم متقدمة لإدارة العمليات، والمالية، والرسائل اللحظية.

تم بناء النظام بمعمارية **Full-Stack Monorepo** يجمع بين خادم واجهة برمجة التطبيقات (API Backend) وتطبيق الهاتف المتعدد المنصات (Flutter Cross-Platform App).

---

## 🏗️ معمارية النظام (System Architecture)

```
mihan-platform/
├── backend/                  # الخادم الخلفي وواجهة برمجة التطبيقات (RESTful API & Admin)
│   ├── app/                  # منطق التطبيق والـ Controllers والنماذج (MVC)
│   ├── config/               # إعدادات النظام وقواعد البيانات
│   ├── database/             # ملفات الهجرة وقواعد بيانات MySQL
│   ├── docker/               # إعدادات الحاويات و Nginx
│   ├── routes/               # مسارات الـ API ولوحة التحكم
│   ├── Dockerfile            # ملف بناء بيئة الإنتاج
│   └── railway.json          # إعدادات النشر السحابي (Cloud Deployment)
│
└── mobile-app/               # تطبيق الهاتف المحمول (Flutter Cross-Platform)
    ├── lib/                  # الكود المصدري للتطبيق
    │   ├── core/             # الثوابت، الثيمات، والخدمات المركزية
    │   ├── models/           # نماذج البيانات (Data Models)
    │   ├── services/         # خدمات الاتصال بالشبكة وإدارة الجلسات
    │   ├── views/            # واجهات المستخدم (عميل / فني)
    │   └── widgets/          # المكونات القابلة لإعادة الاستخدام
    ├── android/              # إعدادات نظام أندرويد
    ├── ios/                  # إعدادات نظام iOS
    └── pubspec.yaml          # حزم واعتماديات دارت وفلاتر
```

---

## 🌟 الميزات الجوهرية (Core Features)

### 1. نظام الأدوار المتعددة (Role-Based Access Control - RBAC)
* **العميل (Customer):** تصفح الخدمات، تقديم طلبات صيانة وخدمات، تتبع الفني، الدفع الإلكتروني، والتقييم.
* **مقدم الخدمة (Service Provider):** استقبال الطلبات القريبة، قبول أو رفض الطلب، تحديد مواعيد الزيارة، ومتابعة الأرباح وصافي المستحقات.
* **موظف المنصة (Platform Staff):** متابعة النزاعات، إدارة التشغيل اليومي، والتحقق من اعتمادات مقدمي الخدمات.
* **مدير النظام (Super Admin):** إدارة كاملة للمستخدمين، الصلاحيات، نسب العمولة، وتقارير التدقيق المالي.

### 2. محرك الطلبات والمالية (Workflow & Finance Engine)
* احتساب آلي لعمولة المنصة من كل عملية مكتملة.
* نظام سداد إلكتروني متكامل داخل المنصة مع محفظة رقمية.
* سجل مدفوعات شفاف لمستحقات الفنيين (`provider_payouts`).
* نظام تقييم موثق لا يُتاح إلا بعد اكتمال الطلب وسداده.

### 3. التواصل والرسائل اللحظية (In-App Messaging)
* نظام محادثة فوري بين العميل ومقدم الخدمة مرتبط بسياق الطلب دون الحاجة لمشاركة أرقام الهواتف الشخصية.
* إشعارات دفع فورية (Push Notifications) عبر Firebase Cloud Messaging.

---

## 🚀 دليل التشغيل والإعداد (Getting Started)

### أولاً: إعداد وتشغيل الخادم الخلفي (Backend Setup)

#### الخيار 1: باستخدام Docker (الأسهل والأسرع)
```bash
cd backend
cp .env.example .env
# قم بتعديل بيانات قاعدة البيانات في ملف .env
docker compose up -d --build
```

#### الخيار 2: التشغيل المحلي التقليدي
1. تثبيت المتطلبات: `PHP >= 8.2`، `Composer`، ومخدم `MySQL`.
2. استيراد قاعدة البيانات:
```bash
mysql -u root -p mihan_db < backend/database.sql
```
3. ضبط إعدادات الاتصال في ملف `backend/.env`.
4. تشغيل المخدم المحلي:
```bash
cd backend
php -S localhost:8000 -t public
```

---

### ثانياً: إعداد وتشغيل تطبيق الهاتف (Mobile App Setup)

1. التأكد من تثبيت بيئة **Flutter SDK (>= 3.0)**:
```bash
cd mobile-app
flutter doctor
```
2. تثبيت الحزم والمكتبات:
```bash
flutter pub get
```
3. ضبط عنوان خادم الـ API في ملف `lib/core/constants.dart` أو إعدادات الشبكة.
4. تشغيل التطبيق على المحاكي أو جهاز حقيقي:
```bash
flutter run
```
5. لبناء نسخة الإنتاج (Release APK):
```bash
flutter build apk --release
```

---

## 🛡️ الأمان وحماية البيانات (Security)

* تشفير كلمات المرور باستخدام خوارزميات التجزئة الآمنة (Bcrypt).
* حماية الـ Endpoints باستخدام رموز الوصول المؤقتة (Tokens).
* عزل بيئات التشغيل وحماية مسارات رفع الملفات والبيانات الحساسة.

---

## 📄 الترخيص (License)
جميع الحقوق محفوظة للمطور © **3hosa**. هذا المشروع خاص وغير مرخص للاستخدام التجاري أو إعادة التوزيع دون إذن مسبق.
