# 🔌 API Endpoints - Freework Platform

---

## 📋 جميع نقاط الوصول (API Routes)

---

## 🔐 **Authentication Routes** (`/api/auth`)

### **1. Register - التسجيل الجديد**
```
POST /api/auth/register
```
**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123",
  "fullName": "John Doe",
  "userType": "freelancer"  // "client" or "freelancer"
}
```

**Response (201):**
```json
{
  "success": true,
  "message": "User registered successfully",
  "user": {
    "_id": "userId",
    "email": "user@example.com",
    "fullName": "John Doe",
    "userType": "freelancer"
  },
  "token": "jwt_token_here"
}
```

---

### **2. Login - تسجيل الدخول**
```
POST /api/auth/login
```
**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Login successful",
  "user": {
    "_id": "userId",
    "email": "user@example.com",
    "userType": "freelancer"
  },
  "token": "jwt_token_here"
}
```

---

### **3. Logout - تسجيل الخروج**
```
POST /api/auth/logout
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Logged out successfully"
}
```

---

### **4. Refresh Token - تحديث التوكن**
```
POST /api/auth/refresh-token
```
**Request Body:**
```json
{
  "refreshToken": "refresh_token_here"
}
```

**Response (200):**
```json
{
  "success": true,
  "token": "new_jwt_token"
}
```

---

### **5. Forgot Password - نسيت كلمة المرور**
```
POST /api/auth/forgot-password
```
**Request Body:**
```json
{
  "email": "user@example.com"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Password reset email sent"
}
```

---

### **6. Reset Password - إعادة تعيين كلمة المرور**
```
POST /api/auth/reset-password
```
**Request Body:**
```json
{
  "token": "reset_token",
  "newPassword": "newPassword123"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Password reset successfully"
}
```

---

### **7. Verify Email - تحقق من البريد**
```
GET /api/auth/verify-email?token=verification_token
```

**Response (200):**
```json
{
  "success": true,
  "message": "Email verified successfully"
}
```

---

## 👥 **User Routes** (`/api/users`)

### **1. Get User Profile - الحصول على الملف الشخصي**
```
GET /api/users/:userId
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "user": {
    "_id": "userId",
    "fullName": "John Doe",
    "email": "user@example.com",
    "profileImage": "url",
    "bio": "I am a web developer",
    "location": {
      "country": "USA",
      "city": "New York"
    },
    "freelancerData": {
      "title": "Web Developer",
      "rating": 4.9,
      "projectsCompleted": 25
    }
  }
}
```

---

### **2. Update User Profile - تحديث الملف الشخصي**
```
PUT /api/users/:userId
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "fullName": "Jane Doe",
  "bio": "Updated bio",
  "location": {
    "country": "USA",
    "city": "Los Angeles"
  }
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Profile updated successfully",
  "user": { /* updated user data */ }
}
```

---

### **3. Get User by Username - البحث عن مستخدم**
```
GET /api/users/username/:username
```

**Response (200):**
```json
{
  "success": true,
  "user": { /* user data */ }
}
```

---

### **4. Get User Statistics - إحصائيات المستخدم**
```
GET /api/users/:userId/stats
```

**Response (200):**
```json
{
  "success": true,
  "stats": {
    "projectsCompleted": 25,
    "totalEarnings": 5000,
    "rating": 4.9,
    "hoursWorked": 250,
    "completionRate": 98
  }
}
```

---

### **5. Follow User - متابعة مستخدم**
```
POST /api/users/:userId/follow
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "User followed successfully"
}
```

---

### **6. Unfollow User - إلغاء المتابعة**
```
POST /api/users/:userId/unfollow
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "User unfollowed successfully"
}
```

---

## 📋 **Project Routes** (`/api/projects`)

### **1. Get All Projects - قائمة جميع المشاريع**
```
GET /api/projects
GET /api/projects?category=web&budget=1000-5000&experience=intermediate
```

**Query Parameters:**
- `category` - فئة المشروع
- `budget` - نطاق الميزانية (مثل: `1000-5000`)
- `experience` - مستوى الخبرة
- `page` - رقم الصفحة (افتراضي: 1)
- `limit` - عدد النتائج (افتراضي: 10)
- `sort` - ترتيب النتائج (newest, oldest, popular)

**Response (200):**
```json
{
  "success": true,
  "projects": [ /* array of projects */ ],
  "total": 100,
  "page": 1,
  "pages": 10
}
```

---

### **2. Get Project Details - تفاصيل المشروع**
```
GET /api/projects/:projectId
```

**Response (200):**
```json
{
  "success": true,
  "project": {
    "_id": "projectId",
    "title": "Build E-commerce Website",
    "description": "...",
    "budget": 2500,
    "status": "open",
    "requiredSkills": ["React", "Node.js", "MongoDB"],
    "bidsCount": 18,
    "client": { /* client data */ }
  }
}
```

---

### **3. Create Project - إنشاء مشروع جديد**
```
POST /api/projects
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "title": "Build E-commerce Website",
  "description": "I need a modern responsive website...",
  "category": "Web Development",
  "budget": 2500,
  "budgetType": "fixed",
  "duration": 30,
  "requiredSkills": ["React", "Node.js", "MongoDB"],
  "requirements": ["RESTful API", "Payment integration", "Admin panel"]
}
```

**Response (201):**
```json
{
  "success": true,
  "message": "Project created successfully",
  "project": { /* project data */ }
}
```

---

### **4. Update Project - تحديث المشروع**
```
PUT /api/projects/:projectId
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "title": "Updated Title",
  "budget": 3000,
  "status": "in-progress"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Project updated successfully",
  "project": { /* updated project data */ }
}
```

---

### **5. Delete Project - حذف المشروع**
```
DELETE /api/projects/:projectId
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Project deleted successfully"
}
```

---

### **6. Get Project Bids - عروض المشروع**
```
GET /api/projects/:projectId/bids
```

**Query Parameters:**
- `sort` - ترتيب (newest, price-asc, price-desc)
- `status` - حالة العرض (pending, accepted, rejected)

**Response (200):**
```json
{
  "success": true,
  "bids": [ /* array of bids */ ]
}
```

---

### **7. Save Project - حفظ المشروع**
```
POST /api/projects/:projectId/save
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Project saved successfully"
}
```

---

### **8. Unsave Project - إلغاء حفظ**
```
DELETE /api/projects/:projectId/save
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Project unsaved successfully"
}
```

---

## 💼 **Bid Routes** (`/api/bids`)

### **1. Submit Bid - تقديم عرض**
```
POST /api/bids
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "projectId": "projectId",
  "proposedPrice": 2400,
  "deliveryTime": 28,
  "description": "I can deliver high-quality work..."
}
```

**Response (201):**
```json
{
  "success": true,
  "message": "Bid submitted successfully",
  "bid": { /* bid data */ }
}
```

---

### **2. Get Bid Details - تفاصيل العرض**
```
GET /api/bids/:bidId
```

**Response (200):**
```json
{
  "success": true,
  "bid": {
    "_id": "bidId",
    "projectId": "projectId",
    "freelancerId": "freelancerId",
    "proposedPrice": 2400,
    "status": "pending",
    "description": "..."
  }
}
```

---

### **3. Update Bid - تحديث العرض**
```
PUT /api/bids/:bidId
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "proposedPrice": 2200,
  "deliveryTime": 25,
  "description": "Updated bid description"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Bid updated successfully",
  "bid": { /* updated bid data */ }
}
```

---

### **4. Withdraw Bid - سحب العرض**
```
DELETE /api/bids/:bidId
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Bid withdrawn successfully"
}
```

---

### **5. Accept Bid - قبول العرض**
```
POST /api/bids/:bidId/accept
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Bid accepted successfully",
  "contract": { /* contract data */ }
}
```

---

### **6. Reject Bid - رفض العرض**
```
POST /api/bids/:bidId/reject
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Bid rejected successfully"
}
```

---

## 🛍️ **Service Routes** (`/api/services`)

### **1. Get All Services - قائمة الخدمات**
```
GET /api/services
GET /api/services?category=web-design&price=100-500&rating=4&limit=20
```

**Response (200):**
```json
{
  "success": true,
  "services": [ /* array of services */ ]
}
```

---

### **2. Get Service Details - تفاصيل الخدمة**
```
GET /api/services/:serviceId
```

**Response (200):**
```json
{
  "success": true,
  "service": {
    "_id": "serviceId",
    "title": "Design Professional Logo",
    "price": 50,
    "rating": 4.9,
    "freelancer": { /* freelancer data */ }
  }
}
```

---

### **3. Create Service - إنشاء خدمة**
```
POST /api/services
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "title": "Design Professional Logo",
  "description": "I will design a professional logo...",
  "category": "Graphic Design",
  "price": 50,
  "deliveryTime": 3,
  "revisions": 3,
  "thumbnail": "image_url"
}
```

**Response (201):**
```json
{
  "success": true,
  "message": "Service created successfully",
  "service": { /* service data */ }
}
```

---

### **4. Update Service - تحديث الخدمة**
```
PUT /api/services/:serviceId
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "price": 60,
  "deliveryTime": 2
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Service updated successfully",
  "service": { /* updated service data */ }
}
```

---

### **5. Delete Service - حذف الخدمة**
```
DELETE /api/services/:serviceId
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Service deleted successfully"
}
```

---

### **6. Favorite Service - حفظ الخدمة**
```
POST /api/services/:serviceId/favorite
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Service added to favorites"
}
```

---

### **7. Get Similar Services - خدمات مشابهة**
```
GET /api/services/:serviceId/similar
```

**Response (200):**
```json
{
  "success": true,
  "services": [ /* array of similar services */ ]
}
```

---

## 📦 **Order Routes** (`/api/orders`)

### **1. Create Order - طلب خدمة**
```
POST /api/orders
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "serviceId": "serviceId",
  "buyerMessage": "Please start ASAP"
}
```

**Response (201):**
```json
{
  "success": true,
  "message": "Order created successfully",
  "order": { /* order data */ }
}
```

---

### **2. Get My Orders - طلباتي**
```
GET /api/orders
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "orders": [ /* array of orders */ ]
}
```

---

### **3. Get Order Details - تفاصيل الطلب**
```
GET /api/orders/:orderId
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "order": {
    "_id": "orderId",
    "serviceId": "serviceId",
    "status": "active",
    "price": 50,
    "deliveryDate": "2026-08-15"
  }
}
```

---

### **4. Cancel Order - إلغاء الطلب**
```
PUT /api/orders/:orderId/cancel
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Order cancelled successfully"
}
```

---

### **5. Complete Order - إنجاز الطلب**
```
PUT /api/orders/:orderId/complete
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "deliveredFiles": ["file_url1", "file_url2"]
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Order completed successfully"
}
```

---

## 💬 **Message Routes** (`/api/messages`)

### **1. Send Message - إرسال رسالة**
```
POST /api/messages
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "receiverId": "receiverId",
  "content": "Hello, I'm interested in your service",
  "fileAttachments": ["file_url"],
  "imageAttachments": ["image_url"]
}
```

**Response (201):**
```json
{
  "success": true,
  "message": "Message sent successfully",
  "data": { /* message data */ }
}
```

---

### **2. Get Conversations - المحادثات**
```
GET /api/messages/conversations
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "conversations": [ /* array of conversations */ ]
}
```

---

### **3. Get Conversation Messages - رسائل المحادثة**
```
GET /api/messages/conversations/:conversationId
```
**Headers:** `Authorization: Bearer {token}`

**Query Parameters:**
- `limit` - عدد الرسائل (default: 20)
- `skip` - تخطي (للـ pagination)

**Response (200):**
```json
{
  "success": true,
  "messages": [ /* array of messages */ ]
}
```

---

### **4. Mark Message as Read - تأشير القراءة**
```
PUT /api/messages/:messageId/read
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Message marked as read"
}
```

---

### **5. Delete Message - حذف الرسالة**
```
DELETE /api/messages/:messageId
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Message deleted successfully"
}
```

---

## ⭐ **Review Routes** (`/api/reviews`)

### **1. Leave Review - ترك تقييم**
```
POST /api/reviews
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "revieweeId": "freelancerId",
  "rating": 5,
  "comment": "Excellent work!",
  "projectId": "projectId",
  "type": "freelancer"
}
```

**Response (201):**
```json
{
  "success": true,
  "message": "Review submitted successfully",
  "review": { /* review data */ }
}
```

---

### **2. Get User Reviews - تقييمات المستخدم**
```
GET /api/reviews/:userId
```

**Query Parameters:**
- `page` - رقم الصفحة
- `limit` - عدد النتائج

**Response (200):**
```json
{
  "success": true,
  "reviews": [ /* array of reviews */ ],
  "total": 50,
  "average": 4.8
}
```

---

### **3. Update Review - تحديث التقييم**
```
PUT /api/reviews/:reviewId
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "rating": 4,
  "comment": "Updated comment"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Review updated successfully"
}
```

---

### **4. Delete Review - حذف التقييم**
```
DELETE /api/reviews/:reviewId
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Review deleted successfully"
}
```

---

## 🔔 **Notification Routes** (`/api/notifications`)

### **1. Get Notifications - إشعاراتي**
```
GET /api/notifications
```
**Headers:** `Authorization: Bearer {token}`

**Query Parameters:**
- `unread` - true للرسائل غير المقروءة فقط

**Response (200):**
```json
{
  "success": true,
  "notifications": [ /* array of notifications */ ]
}
```

---

### **2. Mark Notification as Read - تأشير الإشعار**
```
PUT /api/notifications/:notificationId/read
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Notification marked as read"
}
```

---

### **3. Delete Notification - حذف الإشعار**
```
DELETE /api/notifications/:notificationId
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "message": "Notification deleted successfully"
}
```

---

## 💳 **Payment Routes** (`/api/payments`)

### **1. Create Payment Intent - إنشاء طلب دفع**
```
POST /api/payments/create-intent
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "amount": 5000,
  "orderId": "orderId",
  "currency": "USD"
}
```

**Response (200):**
```json
{
  "success": true,
  "clientSecret": "pi_1234567890"
}
```

---

### **2. Confirm Payment - تأكيد الدفع**
```
POST /api/payments/confirm
```
**Headers:** `Authorization: Bearer {token}`

**Request Body:**
```json
{
  "paymentIntentId": "pi_1234567890",
  "orderId": "orderId"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Payment confirmed successfully",
  "payment": { /* payment data */ }
}
```

---

### **3. Get Payment History - سجل الدفعات**
```
GET /api/payments/history
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "payments": [ /* array of payments */ ]
}
```

---

## 📊 **Dashboard Routes** (`/api/dashboard`)

### **1. Get Dashboard Stats - إحصائيات لوحة التحكم**
```
GET /api/dashboard/stats
```
**Headers:** `Authorization: Bearer {token}`

**Response (200):**
```json
{
  "success": true,
  "stats": {
    "totalEarnings": 5000,
    "activeProjects": 3,
    "completedProjects": 25,
    "ratings": 4.9,
    "thisMonth": {
      "earnings": 1200,
      "projects": 2
    }
  }
}
```

---

## ⚡ **Response Status Codes**

| Code | المعنى |
|------|--------|
| 200 | OK - نجح |
| 201 | Created - تم الإنشاء |
| 400 | Bad Request - طلب خاطئ |
| 401 | Unauthorized - غير مصرح |
| 403 | Forbidden - ممنوع |
| 404 | Not Found - غير موجود |
| 409 | Conflict - تضارب |
| 500 | Server Error - خطأ الخادم |

---

**آخر تحديث:** 2026-07-15
