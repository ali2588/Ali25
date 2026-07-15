# 🗄️ Database Schema - Freework Platform

---

## 📊 جميع نماذج قاعدة البيانات

### 1️⃣ **User Model**

```javascript
{
  _id: ObjectId,                    // معرف فريد
  email: String (unique, required),  // البريد الإلكتروني
  password: String (required),       // كلمة المرور (مشفرة)
  fullName: String (required),       // الاسم الكامل
  userType: String (enum),           // نوع المستخدم: "client" | "freelancer" | "admin"
  profileImage: String,              // صورة الملف الشخصي (URL)
  coverImage: String,                // صورة الغلاف (URL)
  bio: String,                       // السيرة الذاتية
  phone: String,                     // رقم الهاتف
  location: {
    country: String,
    city: String,
    timezone: String
  },
  website: String,                   // الموقع الشخصي
  socialLinks: {
    twitter: String,
    linkedin: String,
    github: String,
    portfolio: String
  },
  isVerified: Boolean (default: false),     // هل تم التحقق من البريد
  isActive: Boolean (default: true),        // هل الحساب نشط
  isBanned: Boolean (default: false),       // هل الحساب محظور
  emailVerified: Date,               // تاريخ تحقق البريد
  createdAt: Date (default: now),    // تاريخ الإنشاء
  updatedAt: Date (default: now),    // تاريخ التحديث
  lastLogin: Date,                   // آخر دخول
  
  // للعاملين فقط:
  freelancerData: {
    title: String,                   // المسمى الوظيفي (مثل: Web Developer)
    rating: Number (default: 0),     // التقييم العام
    reviewsCount: Number (default: 0), // عدد التقييمات
    projectsCompleted: Number (default: 0), // عدد المشاريع المنجزة
    responseRate: Number,            // نسبة الرد (%)
    responseTime: Number,            // متوسط وقت الرد (ساعات)
    hoursWorked: Number (default: 0), // ساعات العمل الكلية
    completionRate: Number,          // نسبة النجاح (%)
    ongoingProjects: Number (default: 0), // المشاريع الجارية
    totalEarnings: Number (default: 0),   // إجمالي الأرباح
    verificationLevel: String,       // مستوى التحقق: "basic" | "verified" | "top-rated"
  }
}
```

---

### 2️⃣ **Project Model**

```javascript
{
  _id: ObjectId,
  title: String (required),          // عنوان المشروع
  description: String (required),    // وصف المشروع
  clientId: ObjectId (ref: User),    // معرف العميل
  category: String (required),       // الفئة: "Web Development", "Design"...
  subcategory: String,               // الفئة الفرعية
  budget: Number (required),         // الميزانية
  budgetType: String (enum),         // نوع الميزانية: "fixed" | "hourly"
  minBudget: Number,                 // الحد الأدنى للميزانية (للساعي)
  maxBudget: Number,                 // الحد الأقصى للميزانية (للساعي)
  duration: Number,                  // المدة بالأيام
  requiredSkills: [String],          // المهارات المطلوبة
  requirements: [String],            // المتطلبات التفصيلية
  attachedFiles: [{
    name: String,
    url: String,
    type: String,                    // "design", "document", "image"
    size: Number,
    uploadedAt: Date
  }],
  status: String (enum),             // حالة المشروع: "open" | "in-progress" | "completed" | "closed" | "cancelled"
  bidsCount: Number (default: 0),    // عدد العروض المقدمة
  acceptedBidId: ObjectId (ref: Bid), // العرض المقبول
  views: Number (default: 0),        // عدد المشاهدات
  createdAt: Date (default: now),
  updatedAt: Date (default: now),
  postedOn: Date,
  
  // معلومات إضافية
  experience: String (enum),         // مستوى الخبرة المطلوب: "entry" | "intermediate" | "expert"
  securityLevel: String,             // مستوى الأمان: "public" | "private"
  estimatedTimeInDays: Number,       // الوقت المتوقع بالأيام
  paymentVerified: Boolean,          // هل تم التحقق من الدفع
}
```

---

### 3️⃣ **Bid Model**

```javascript
{
  _id: ObjectId,
  projectId: ObjectId (ref: Project), // معرف المشروع
  freelancerId: ObjectId (ref: User),  // معرف العامل
  proposedPrice: Number (required),   // السعر المقترح
  deliveryTime: Number (required),    // وقت التسليم بالأيام
  description: String (required),     // وصف العرض
  attachments: [{
    name: String,
    url: String,
    uploadedAt: Date
  }],
  status: String (enum),              // حالة العرض: "pending" | "accepted" | "rejected" | "withdrawn"
  proposal: String,                   // الاقتراح المفصل
  portfolio: [ObjectId] (ref: PortfolioItem), // عينات من الأعمال السابقة
  
  // متعلق بالعقد
  contractStartDate: Date,            // تاريخ بداية العقد
  contractEndDate: Date,              // تاريخ نهاية العقد
  
  createdAt: Date (default: now),
  updatedAt: Date (default: now),
  withdrawnAt: Date,                  // تاريخ السحب (إن وُجد)
  
  // التقييمات والملاحظات
  clientRating: Number,               // تقييم العميل للعرض
  clientReview: String,               // ملاحظات العميل
}
```

---

### 4️⃣ **Service Model**

```javascript
{
  _id: ObjectId,
  title: String (required),           // عنوان الخدمة
  description: String (required),     // وصف الخدمة
  freelancerId: ObjectId (ref: User), // معرف العامل
  category: String (required),        // الفئة
  subcategory: String,
  price: Number (required),           // السعر
  priceType: String (enum),           // نوع السعر: "fixed" | "hourly" | "per-project"
  deliveryTime: Number (required),    // وقت التسليم بالأيام
  revisions: Number (default: 1),     // عدد مرات التعديل
  thumbnail: String,                  // صورة الخدمة
  gallery: [String],                  // معرض الصور
  
  // التقييمات
  rating: Number (default: 0),        // التقييم
  reviewsCount: Number (default: 0),  // عدد التقييمات
  
  // الإحصائيات
  ordersCount: Number (default: 0),   // عدد الطلبات
  completedOrders: Number (default: 0), // الطلبات المنجزة
  
  // الحالة والترويج
  status: String (enum),              // الحالة: "active" | "paused" | "deleted"
  isBestSeller: Boolean (default: false), // هل هي من أفضل البيعات
  isRecommended: Boolean (default: false), // هل موصى بها
  isFeatured: Boolean (default: false), // مميزة
  
  createdAt: Date (default: now),
  updatedAt: Date (default: now),
}
```

---

### 5️⃣ **Order Model**

```javascript
{
  _id: ObjectId,
  serviceId: ObjectId (ref: Service),  // معرف الخدمة
  buyerId: ObjectId (ref: User),       // معرف المشتري
  sellerId: ObjectId (ref: User),      // معرف البائع
  price: Number (required),            // السعر النهائي
  status: String (enum),               // الحالة: "active" | "completed" | "cancelled" | "disputed"
  deliveryDate: Date,                  // تاريخ التسليم
  completedAt: Date,                   // تاريخ الإنجاز
  
  // تفاصيل الطلب
  buyerMessage: String,                // رسالة المشتري
  sellerDelivery: String,              // ما سيسلمه البائع
  sellerMessage: String,               // رسالة البائع
  
  // الملفات
  deliveredFiles: [{
    name: String,
    url: String,
    uploadedAt: Date
  }],
  
  // التقييمات
  buyerRating: Number,                 // تقييم المشتري
  buyerReview: String,
  sellerRating: Number,                // تقييم البائع
  sellerReview: String,
  
  createdAt: Date (default: now),
  updatedAt: Date (default: now),
}
```

---

### 6️⃣ **Message Model**

```javascript
{
  _id: ObjectId,
  conversationId: ObjectId (ref: Conversation), // معرف المحادثة
  senderId: ObjectId (ref: User),      // معرف المرسل
  receiverId: ObjectId (ref: User),    // معرف المستقبل
  content: String (required),          // محتوى الرسالة
  
  // الملفات والمرفقات
  fileAttachments: [{
    name: String,
    url: String,
    type: String,                      // "pdf", "doc", "image"...
    size: Number,
    uploadedAt: Date
  }],
  
  imageAttachments: [{
    url: String,
    alt: String,
    uploadedAt: Date
  }],
  
  linkAttachments: [{
    url: String,
    title: String,
    preview: String,
    addedAt: Date
  }],
  
  // التفاعلات
  reactions: [{
    emoji: String,
    userId: ObjectId (ref: User),
    addedAt: Date
  }],
  
  // قراءة الرسالة
  isRead: Boolean (default: false),
  readAt: Date,
  
  // الحالة
  isDeleted: Boolean (default: false),
  deletedAt: Date,
  
  createdAt: Date (default: now),
  updatedAt: Date (default: now),
}
```

---

### 7️⃣ **Conversation Model**

```javascript
{
  _id: ObjectId,
  participants: [ObjectId] (ref: User), // المشاركون في المحادثة
  lastMessage: String,                 // آخر رسالة
  lastMessageTime: Date,               // وقت آخر رسالة
  lastMessageSenderId: ObjectId,       // من أرسل آخر رسالة
  
  // المعلومات
  subject: String,                     // موضوع المحادثة (إن وُجد)
  relatedProjectId: ObjectId,          // المشروع المرتبط (إن وُجد)
  relatedServiceId: ObjectId,          // الخدمة المرتبطة (إن وُجد)
  
  // قراءة الرسائل
  unreadCount: {
    [userId]: Number                   // عدد الرسائل ��ير المقروءة لكل مستخدم
  },
  
  isArchived: Boolean (default: false), // هل المحادثة مؤرشفة
  
  createdAt: Date (default: now),
  updatedAt: Date (default: now),
}
```

---

### 8️⃣ **Review Model**

```javascript
{
  _id: ObjectId,
  reviewerId: ObjectId (ref: User),    // معرف المراجع
  revieweeId: ObjectId (ref: User),    // معرف المراجع له
  rating: Number (required, min: 1, max: 5), // التقييم
  comment: String,                     // التعليق
  
  // السياق
  projectId: ObjectId (ref: Project),  // المشروع المرتبط
  orderId: ObjectId (ref: Order),      // الطلب المرتبط
  type: String (enum),                 // نوع التقييم: "freelancer" | "client"
  
  // الجوانب
  communication: Number,               // جودة التواصل (1-5)
  professionalism: Number,             // الاحترافية (1-5)
  qualityOfWork: Number,               // جودة العمل (1-5)
  deadlineAdherence: Number,           // الالتزام بالمواعيد (1-5)
  
  anonymous: Boolean (default: false), // هل التقييم مجهول
  
  createdAt: Date (default: now),
  updatedAt: Date (default: now),
}
```

---

### 9️⃣ **Notification Model**

```javascript
{
  _id: ObjectId,
  userId: ObjectId (ref: User),        // معرف المستخدم
  type: String (enum),                 // نوع الإشعار:
                                       // "new-bid", "bid-accepted", "project-completed"
                                       // "new-message", "service-review", "payment-received"
  title: String (required),            // عنوان الإشعار
  message: String (required),          // محتوى الإشعار
  
  // الارتباطات
  relatedUserId: ObjectId (ref: User), // المستخدم المرتبط بالإشعار
  relatedProjectId: ObjectId,
  relatedBidId: ObjectId,
  relatedServiceId: ObjectId,
  relatedOrderId: ObjectId,
  
  isRead: Boolean (default: false),
  readAt: Date,
  
  actionUrl: String,                   // الرابط الذي يقود إليه
  
  createdAt: Date (default: now),
}
```

---

### 🔟 **Skill Model**

```javascript
{
  _id: ObjectId,
  freelancerId: ObjectId (ref: User),  // معرف العامل
  skillName: String (required),        // اسم المهارة
  proficiency: Number (min: 1, max: 10), // مستوى الكفاءة
  level: String (enum),                // مستوى: "Beginner" | "Intermediate" | "Advanced" | "Expert"
  endorsements: Number (default: 0),   // عدد التأييدات
  endorsedBy: [ObjectId],              // من أيدها
  yearsOfExperience: Number,           // سنوات الخبرة
  
  createdAt: Date (default: now),
  updatedAt: Date (default: now),
}
```

---

### 1️⃣1️⃣ **Portfolio Model**

```javascript
{
  _id: ObjectId,
  freelancerId: ObjectId (ref: User),  // معرف العامل
  title: String (required),            // عنوان المشروع
  description: String,                 // الوصف
  image: String,                       // الصورة الرئيسية
  gallery: [String],                   // معرض الصور
  link: String,                        // رابط المشروع
  category: String,                    // الفئة
  technologies: [String],              // التقنيات المستخدمة
  duration: String,                    // مدة المشروع
  role: String,                        // الدور في المشروع
  outcome: String,                     // النتيجة
  featured: Boolean (default: false),  // مميز
  
  createdAt: Date (default: now),
  updatedAt: Date (default: now),
}
```

---

### 1️⃣2️⃣ **Payment Model**

```javascript
{
  _id: ObjectId,
  amount: Number (required),           // المبلغ
  currency: String (default: "USD"),   // العملة
  
  // الأطراف
  payerId: ObjectId (ref: User),       // من يدفع
  payeeId: ObjectId (ref: User),       // من يستقبل
  
  // المرتبط
  relatedProjectId: ObjectId,
  relatedOrderId: ObjectId,
  relatedBidId: ObjectId,
  
  // معلومات الدفع
  paymentMethod: String (enum),        // طريقة الدفع: "stripe" | "paypal" | "bank"
  stripePaymentIntentId: String,
  status: String (enum),               // الحالة: "pending" | "completed" | "failed" | "refunded"
  
  // التفاصيل
  description: String,
  invoiceNumber: String,
  
  // الفاتورة
  tax: Number (default: 0),
  platformFee: Number,
  total: Number,
  
  // التواريخ
  createdAt: Date (default: now),
  completedAt: Date,
  refundedAt: Date,
}
```

---

### 1️⃣3️⃣ **Post Model (News Feed)**

```javascript
{
  _id: ObjectId,
  authorId: ObjectId (ref: User),      // معرف المنشئ
  type: String (enum),                 // نوع المنشور: "project" | "service" | "update" | "story"
  
  // المحتوى
  title: String,
  description: String (required),
  content: String,
  images: [String],
  videos: [String],
  
  // الارتباطات
  relatedProjectId: ObjectId,
  relatedServiceId: ObjectId,
  
  // الحالة
  visibility: String (enum),           // "public" | "private" | "followers"
  isPromoted: Boolean (default: false),
  
  // التفاعلات
  likes: [ObjectId],                   // معرفات المعجبين
  likesCount: Number (default: 0),
  
  comments: [{
    commenterId: ObjectId,
    content: String,
    createdAt: Date,
    replies: [Object]
  }],
  commentsCount: Number (default: 0),
  
  shares: [ObjectId],                  // معرفات من شارك المنشور
  sharesCount: Number (default: 0),
  
  bookmarks: [ObjectId],               // حفظ المنشور
  bookmarksCount: Number (default: 0),
  
  // الإحصائيات
  views: Number (default: 0),
  
  createdAt: Date (default: now),
  updatedAt: Date (default: now),
}
```

---

## 📊 العلاقات بين النماذج

```
User
├── Project (1:N) - العميل لديه مشاريع
├── Bid (1:N) - العامل يقدم عروض
├── Service (1:N) - العامل ينشر خدمات
├── Order (1:N) - العميل يطلب خدمات
├── Message (1:N) - يرسل رسائل
├── Review (1:N) - يترك تقييمات
├── Skill (1:N)
├── Portfolio (1:N)
├── Notification (1:N)
└── Post (1:N)

Project
├── User (1:1) - العميل
├── Bid (1:N) - عروض على المشروع
└── Review (1:N)

Bid
├── Project (1:1)
├── User (1:1) - العامل
└── Review (1:N)

Service
├── User (1:1) - العامل
├── Order (1:N)
└── Review (1:N)

Order
├── Service (1:1)
├── User (1:1) - المشتري
├── User (1:1) - البائع
└── Review (1:N)

Conversation
├── User (N:N) - المشاركون
└── Message (1:N)

Message
├── Conversation (1:1)
├── User (1:1) - المرسل
└── User (1:1) - المستقبل
```

---

## 🔐 مؤشرات قاعدة البيانات

```javascript
// User Indexes
db.users.createIndex({ email: 1 });
db.users.createIndex({ createdAt: -1 });
db.users.createIndex({ userType: 1 });

// Project Indexes
db.projects.createIndex({ clientId: 1 });
db.projects.createIndex({ status: 1 });
db.projects.createIndex({ category: 1 });
db.projects.createIndex({ createdAt: -1 });

// Bid Indexes
db.bids.createIndex({ projectId: 1, freelancerId: 1 });
db.bids.createIndex({ status: 1 });
db.bids.createIndex({ createdAt: -1 });

// Message Indexes
db.messages.createIndex({ conversationId: 1 });
db.messages.createIndex({ createdAt: -1 });

// Conversation Indexes
db.conversations.createIndex({ participants: 1 });
db.conversations.createIndex({ lastMessageTime: -1 });

// Service Indexes
db.services.createIndex({ freelancerId: 1 });
db.services.createIndex({ category: 1 });

// Review Indexes
db.reviews.createIndex({ revieweeId: 1 });
db.reviews.createIndex({ createdAt: -1 });
```

---

**آخر تحديث:** 2026-07-15
