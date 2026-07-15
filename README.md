# 🚀 Freework Platform - Interactive Freelance Marketplace

## 📋 نظرة عامة على المشروع

**Freework** هي منصة عمل حر تفاعلية متكاملة تربط بين أصحاب المشاريع والعاملين بالعمل الحر. المنصة تجمع بين ميزات الشبكات الاجتماعية + سوق العمل الحر + منصة الخدمات الجاهزة.

---

## ✨ المميزات الرئيسية

### 1️⃣ **الشبكة الاجتماعية (News Feed)**
- نشر المشاريع والخدمات
- متابعة العاملين والعملاء
- تفاعلات (إعجاب، تعليقات، مشاركة)
- حفظ المنشورات المفضلة

### 2️⃣ **سوق المشاريع (Projects Marketplace)**
- العملاء ينشرون المشاريع
- العاملون يقدمون العروض (Bids)
- نظام متقدم للفلترة والبحث
- عرض تفاصيل المشروع والمتطلبات
- إدارة العروض المقدمة

### 3️⃣ **سوق الخدمات (Services Marketplace)**
- العاملون ينشرون خدمات جاهزة
- العملاء يشترون الخدمات مباشرة
- نظام التقييم والمراجعات
- توصيات مخصصة (Similar Services)

### 4️⃣ **ملفات تعريفية متقدمة (Freelancer Profiles)**
- عرض المهارات والخبرات
- حفظ محفظة الأعمال (Portfolio)
- إحصائيات الأداء (رسوم النجاح، ساعات العمل، المشاريع المنجزة)
- التقييمات والمراجعات
- معلومات الاتصال والتوظيف المباشر

### 5️⃣ **نظام الرسائل (Messaging System)**
- محادثات فورية حقيقية (Real-time with Socket.io)
- مشاركة الملفات والصور والروابط
- مؤشرات الكتابة والحالة (Online/Offline)
- إيصالات القراءة (Read Receipts)
- سجل المحادثات الكامل

### 6️⃣ **الإشعارات والتنبيهات**
- إشعارات فورية بالعروض الجديدة
- تنبيهات بالرسائل الجديدة
- إشعارات بالتحديثات على المشاريع
- تنبيهات بالمنشورات الجديدة من المتابعين

---

## 🏗️ البنية التقنية

### **Frontend:**
- HTML5 + CSS3
- Tailwind CSS (للتصميم)
- JavaScript (Vanilla + optional frameworks)
- Socket.io Client (للرسائل الفورية)

### **Backend:**
- Node.js + Express.js
- MongoDB (قاعدة البيانات)
- Socket.io (الرسائل الفورية)
- JWT (المصادقة)

### **المتطلبات:**
- Node.js v14+
- npm أو yarn
- MongoDB (محلي أو سحابي)

---

## 📁 هيكل المشروع

```
freework-platform/
├── public/
│   ├── index.html              # الصفحة الرئيسية
│   ├── css/
│   │   ├── style.css           # التصميم الرئيسي
│   │   └── tailwind.css        # Tailwind CSS
│   ├── js/
│   │   ├── app.js              # JavaScript الرئيسي
│   │   ├── socket.js           # Socket.io العميل
│   │   └── utils.js            # دوال مساعدة
│   └── pages/
│       ├── home.html           # الصفحة الرئيسية
│       ├── login.html          # تسجيل الدخول
│       ├── signup.html         # التسجيل الجديد
│       ├── dashboard.html      # لوحة التحكم
│       ├── projects.html       # قائمة المشاريع
│       ├── project-details.html # تفاصيل المشروع
│       ├── services.html       # قائمة الخدمات
│       ├── freelancers.html    # قائمة العاملين
│       ├── profile.html        # الملف الشخصي
│       ├── messages.html       # الرسائل
│       ├── notifications.html  # الإشعارات
│       └── settings.html       # الإعدادات
│
├── server/
│   ├── server.js               # نقطة بدء الخادم
│   ├── config/
│   │   ├── database.js         # اتصال MongoDB
│   │   ├── jwt.js              # إعدادات JWT
│   │   └── socket.js           # إعدادات Socket.io
│   ├── models/
│   │   ├── User.js             # نموذج المستخدم
│   │   ├── Post.js             # نموذج المنشور
│   │   ├── Project.js          # نموذج المشروع
│   │   ├── Bid.js              # نموذج العرض
│   │   ├── Service.js          # نموذج الخدمة
│   │   ├── Message.js          # نموذج الرسالة
│   │   ├── Review.js           # نموذج التقييم
│   │   ├── Conversation.js     # نموذج المحادثة
│   │   └── Skill.js            # نموذج المهارة
│   ├── routes/
│   │   ├── auth.js             # مسارات المصادقة
│   │   ├── users.js            # مسارات المستخدمين
│   │   ├── posts.js            # مسارات المنشورات
│   │   ├── projects.js         # مسارات المشاريع
│   │   ├── bids.js             # مسارات العروض
│   │   ├── services.js         # مسارات الخدمات
│   │   ├── messages.js         # مسارات الرسائل
│   │   ├── reviews.js          # مسارات التقييمات
│   │   └── notifications.js    # مسارات الإشعارات
│   ├── middleware/
│   │   ├── auth.js             # التحقق من المصادقة
│   │   ├── errorHandler.js     # معالجة الأخطاء
│   │   └── validation.js       # التحقق من البيانات
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── userController.js
│   │   ├── projectController.js
│   │   ├── bidController.js
│   │   ├── serviceController.js
│   │   ├── messageController.js
│   │   └── reviewController.js
│   └── utils/
│       ├── logger.js           # تسجيل الأخطاء
│       ├── helpers.js          # دوال مساعدة
│       └── validators.js       # دوال التحقق
���
├── .env.example                # مثال متغيرات البيئة
├── .gitignore                  # ملفات Git المتجاهلة
├── package.json                # المكتبات والإصدارات
├── package-lock.json           # قفل الإصدارات
├── IMPLEMENTATION_PLAN.md      # خطة التطوير
├── DATABASE_SCHEMA.md          # قاعدة البيانات
├── API_ENDPOINTS.md            # جميع APIs
└── README.md                   # هذا الملف
```

---

## 🚀 البدء السريع

### **1. تثبيت المتطلبات:**
```bash
# تثبيت Node.js من https://nodejs.org/

# تحقق من التثبيت
node --version
npm --version
```

### **2. استنساخ المشروع:**
```bash
git clone https://github.com/Ali2588/Ali25.git
cd Ali25
```

### **3. تثبيت المكتبات:**
```bash
npm install
```

### **4. إعداد متغيرات البيئة:**
```bash
# انسخ الملف
cp .env.example .env

# عدّل الملف وأضف بيانات اتصالك
```

### **5. تشغيل المشروع:**
```bash
# في بيئة التطوير
npm run dev

# المشروع سيعمل على: http://localhost:3000
```

---

## 📊 مراحل المشروع (10 مراحل)

| المرحلة | الاسم | الحالة | النسبة |
|--------|--------|--------|--------|
| **Phase 0** | الأساسيات | 🔄 جاري | 30% |
| **Phase 1** | المصادقة والمستخدمين | ⏳ قادم | 0% |
| **Phase 2** | الملفات الشخصية والمهارات | ⏳ قادم | 0% |
| **Phase 3** | المشاريع والعروض | ⏳ قادم | 0% |
| **Phase 4** | الخدمات الجاهزة | ⏳ قادم | 0% |
| **Phase 5** | الرسائل والإشعارات | ⏳ قادم | 0% |
| **Phase 6** | التقييمات والمراجعات | ⏳ قادم | 0% |
| **Phase 7** | نظام الدفع | ⏳ قادم | 0% |
| **Phase 8** | لوحة تحكم الإدارة | ⏳ قادم | 0% |
| **Phase 9** | التحسينات والأمان | ⏳ قادم | 0% |

---

## 📖 الملفات المهمة

- 📄 **[IMPLEMENTATION_PLAN.md](./IMPLEMENTATION_PLAN.md)** - خطة التطوير التفصيلية
- 📄 **[DATABASE_SCHEMA.md](./DATABASE_SCHEMA.md)** - قاعدة البيانات الكاملة
- 📄 **[API_ENDPOINTS.md](./API_ENDPOINTS.md)** - جميع نقاط الوصول
- 📄 **[PROJECT_STRUCTURE.md](./PROJECT_STRUCTURE.md)** - شرح هيكل المشروع
- 📄 **[FRONTEND_PAGES.md](./FRONTEND_PAGES.md)** - صفحات الـ Frontend

---

## 🔧 الأوامر المهمة

```bash
# تثبيت المكتبات
npm install

# تشغيل المشروع
npm start

# تشغيل في بيئة التطوير
npm run dev

# تشغيل اختبارات
npm test

# بناء الإصدار النهائية
npm run build
```

---

## 📚 المكتبات المستخدمة

### **Backend:**
```json
{
  "express": "^4.18.0",
  "mongoose": "^7.0.0",
  "socket.io": "^4.5.0",
  "jsonwebtoken": "^9.0.0",
  "bcryptjs": "^2.4.3",
  "dotenv": "^16.0.0",
  "cors": "^2.8.5",
  "body-parser": "^1.20.0"
}
```

### **Frontend:**
```
- HTML5
- CSS3 + Tailwind CSS
- JavaScript (Vanilla)
- Socket.io Client
```

---

## 👥 الفريق

- **المطور:** Ali2588
- **التاريخ:** 2026
- **الترخيص:** MIT

---

## 📞 التواصل والدعم

- 📧 البريد الإلكتروني: [your-email@example.com]
- 🐙 GitHub: [github.com/Ali2588](https://github.com/Ali2588)
- 💬 المشاكل والاقتراحات: [Issues](https://github.com/Ali2588/Ali25/issues)

---

## 📝 ملاحظات مهمة

1. **هذا المشروع قيد التطوير النشط** - قد تتغير الميزات والتفاصيل
2. **استخدم .env للبيانات الحساسة** - لا تضع كلمات المرور في الكود
3. **اتبع معايير الكود** - استخدم ESLint و Prettier
4. **اختبر جيداً** - قبل الرفع للإنتاج

---

## 📄 الترخيص

هذا المشروع مرخص تحت MIT License - انظر [LICENSE](LICENSE) للتفاصيل.

---

**آخر تحديث:** 2026-07-15
**الإصدار:** 0.1.0 (Alpha)
