## 🔌 API Documentation - ShadMini Code

---

## 📋 المقدمة

هذا الملف يوثق جميع الـ APIs في ShadMini Code (الخادم والعميل).

**Base URL:** `http://localhost:5000/api`

---

## 🔐 المصادقة (Authentication)

جميع الطلبات المحمية تحتاج على رأس:

```http
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json
```

---

## 👤 APIs المستخدمين

### 1️⃣ تسجيل دخول جديد

```http
POST /api/auth/signup
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "StrongPassword123!",
  "username": "shadmini_user",
  "fullName": "Shadow Mini"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "User registered successfully",
  "data": {
    "id": "user_123",
    "email": "user@example.com",
    "username": "shadmini_user",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

### 2️⃣ تسجيل الدخول

```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "StrongPassword123!"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Login successful",
  "data": {
    "id": "user_123",
    "email": "user@example.com",
    "username": "shadmini_user",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

### 3️⃣ تسجيل الخروج

```http
POST /api/auth/logout
Authorization: Bearer <JWT_TOKEN>
```

**Response (200):**
```json
{
  "success": true,
  "message": "Logged out successfully"
}
```

### 4️⃣ الحصول على بيانات المستخدم

```http
GET /api/users/me
Authorization: Bearer <JWT_TOKEN>
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "id": "user_123",
    "email": "user@example.com",
    "username": "shadmini_user",
    "fullName": "Shadow Mini",
    "avatar": "https://...",
    "createdAt": "2026-05-11T10:00:00Z"
  }
}
```

### 5️⃣ تحديث الملف الشخصي

```http
PUT /api/users/me
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json

{
  "fullName": "Shadow Mini Updated",
  "bio": "Code editor enthusiast",
  "avatar": "https://..."
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Profile updated successfully",
  "data": { ... }
}
```

### 6️⃣ تغيير كلمة المرور

```http
POST /api/auth/change-password
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json

{
  "currentPassword": "OldPassword123!",
  "newPassword": "NewPassword123!"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Password changed successfully"
}
```

---

## 📁 APIs الملفات

### 1️⃣ الحصول على قائمة الملفات

```http
GET /api/files?projectId=project_123
Authorization: Bearer <JWT_TOKEN>
```

**Response (200):**
```json
{
  "success": true,
  "data": [
    {
      "id": "file_1",
      "name": "index.js",
      "language": "javascript",
      "size": 2048,
      "createdAt": "2026-05-11T10:00:00Z",
      "updatedAt": "2026-05-11T12:00:00Z"
    },
    {
      "id": "file_2",
      "name": "styles.css",
      "language": "css",
      "size": 1024,
      "createdAt": "2026-05-11T10:00:00Z",
      "updatedAt": "2026-05-11T12:00:00Z"
    }
  ]
}
```

### 2️⃣ إنشاء ملف جديد

```http
POST /api/files
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json

{
  "projectId": "project_123",
  "name": "main.py",
  "language": "python",
  "content": "print('Hello, World!')"
}
```

**Response (201):**
```json
{
  "success": true,
  "message": "File created successfully",
  "data": {
    "id": "file_3",
    "name": "main.py",
    "language": "python",
    "content": "print('Hello, World!')",
    "createdAt": "2026-05-11T10:00:00Z"
  }
}
```

### 3️⃣ الحصول على محتوى الملف

```http
GET /api/files/file_1
Authorization: Bearer <JWT_TOKEN>
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "id": "file_1",
    "name": "index.js",
    "language": "javascript",
    "content": "console.log('Hello');",
    "size": 2048,
    "updatedAt": "2026-05-11T12:00:00Z"
  }
}
```

### 4️⃣ تحديث محتوى الملف

```http
PUT /api/files/file_1
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json

{
  "content": "console.log('Updated');",
  "language": "javascript"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "File updated successfully",
  "data": { ... }
}
```

### 5️⃣ حذف ملف

```http
DELETE /api/files/file_1
Authorization: Bearer <JWT_TOKEN>
```

**Response (200):**
```json
{
  "success": true,
  "message": "File deleted successfully"
}
```

### 6️⃣ البحث في الملفات

```http
GET /api/files/search?projectId=project_123&query=main
Authorization: Bearer <JWT_TOKEN>
```

**Response (200):**
```json
{
  "success": true,
  "data": [
    {
      "id": "file_3",
      "name": "main.py",
      "language": "python"
    }
  ]
}
```

---

## 📦 APIs المشاريع

### 1️⃣ الحصول على المشاريع

```http
GET /api/projects
Authorization: Bearer <JWT_TOKEN>
```

**Response (200):**
```json
{
  "success": true,
  "data": [
    {
      "id": "project_123",
      "name": "My First Project",
      "description": "Learning web development",
      "language": "javascript",
      "filesCount": 3,
      "createdAt": "2026-05-11T10:00:00Z",
      "updatedAt": "2026-05-11T12:00:00Z"
    }
  ]
}
```

### 2️⃣ إنشاء مشروع جديد

```http
POST /api/projects
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json

{
  "name": "New Project",
  "description": "My new project",
  "language": "python"
}
```

**Response (201):**
```json
{
  "success": true,
  "message": "Project created successfully",
  "data": {
    "id": "project_124",
    "name": "New Project",
    "description": "My new project",
    "language": "python",
    "createdAt": "2026-05-11T10:00:00Z"
  }
}
```

### 3️⃣ الحصول على تفاصيل المشروع

```http
GET /api/projects/project_123
Authorization: Bearer <JWT_TOKEN>
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "id": "project_123",
    "name": "My First Project",
    "description": "Learning web development",
    "language": "javascript",
    "files": [ ... ],
    "createdAt": "2026-05-11T10:00:00Z"
  }
}
```

### 4️⃣ تحديث المشروع

```http
PUT /api/projects/project_123
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json

{
  "name": "Updated Project Name",
  "description": "Updated description"
}
```

### 5️⃣ حذف مشروع

```http
DELETE /api/projects/project_123
Authorization: Bearer <JWT_TOKEN>
```

---

## 🤖 APIs الذكاء الاصطناعي

### 1️⃣ شرح الأكواد

```http
POST /api/ai/explain
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json

{
  "code": "function fibonacci(n) { return n <= 1 ? n : fibonacci(n-1) + fibonacci(n-2); }",
  "language": "javascript",
  "detail": "medium"
}
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "explanation": "هذه الدالة تحسب رقم فيبوناتشي باستخدام Recursion...",
    "complexity": "O(2^n)",
    "tips": [
      "يمكن تحسينها باستخدام Memoization",
      "البديل الأفضل هو Loop"
    ]
  }
}
```

### 2️⃣ توليد أكواد

```http
POST /api/ai/generate
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json

{
  "prompt": "اكتب دالة JavaScript تحسب مجموع الأرقام في مصفوفة",
  "language": "javascript",
  "context": "في React Component"
}
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "code": "const sumArray = (arr) => arr.reduce((a, b) => a + b, 0);",
    "explanation": "هذه الدالة تستخدم reduce...",
    "example": "sumArray([1,2,3,4,5]) // Output: 15"
  }
}
```

### 3️⃣ اكتشاف الأخطاء

```http
POST /api/ai/detect-bugs
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json

{
  "code": "var x = 1; var x = 2;",
  "language": "javascript"
}
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "bugs": [
      {
        "line": 1,
        "severity": "warning",
        "message": "Duplicate variable declaration",
        "suggestion": "استخدم let أو const بدلاً من var"
      }
    ]
  }
}
```

### 4️⃣ تحسين الأكواد

```http
POST /api/ai/optimize
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json

{
  "code": "for(let i=0; i<arr.length; i++) { console.log(arr[i]); }",
  "language": "javascript"
}
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "optimizedCode": "arr.forEach(item => console.log(item));",
    "improvements": [
      "استخدام forEach أكثر وضوحاً",
      "تجنب الوصول المتكرر إلى arr.length"
    ]
  }
}
```

### 5️⃣ محادثة مع AI

```http
POST /api/ai/chat
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json

{
  "message": "كيف أحسب factorial في Python؟",
  "language": "python",
  "context": "learning"
}
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "response": "يمكنك استخدام recursive function أو loop...",
    "codeExample": "def factorial(n):\n    return 1 if n <= 1 else n * factorial(n-1)",
    "suggestions": [ ... ]
  }
}
```

### 6️⃣ توليد اختبارات الوحدة

```http
POST /api/ai/generate-tests
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json

{
  "code": "function add(a, b) { return a + b; }",
  "language": "javascript",
  "framework": "jest"
}
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "tests": "describe('add', () => { test('1 + 1 = 2', () => { expect(add(1, 1)).toBe(2); }); });",
    "coverage": "100%"
  }
}
```

---

## ⚙️ APIs الإعدادات

### 1️⃣ الحصول على الإعدادات

```http
GET /api/settings
Authorization: Bearer <JWT_TOKEN>
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "theme": "dark",
    "fontSize": 14,
    "fontFamily": "JetBrains Mono",
    "lineHeight": 1.5,
    "tabSize": 2,
    "autoFormat": true,
    "autoSave": true
  }
}
```

### 2️⃣ تحديث الإعدادات

```http
PUT /api/settings
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json

{
  "theme": "light",
  "fontSize": 16,
  "tabSize": 4,
  "autoFormat": true
}
```

---

## 🔍 المعالجة والأخطاء

### رموز الأخطاء (Error Codes):

| Code | المعنى |
|------|--------|
| `200` | نجاح |
| `201` | تم الإنشاء بنجاح |
| `400` | طلب خاطئ |
| `401` | غير مصرح |
| `403` | محظور |
| `404` | غير موجود |
| `500` | خطأ في الخادم |

### مثال على رسالة خطأ:

```json
{
  "success": false,
  "error": {
    "code": "INVALID_EMAIL",
    "message": "البريد الإلكتروني غير صحيح",
    "details": "البريد الإلكتروني يجب أن يكون بصيغة صحيحة"
  }
}
```

---

## 📊 معدلات الحد (Rate Limiting)

- **للمستخدمين المجانيين**: 100 طلب/ساعة
- **للمستخدمين المدفوعين**: 1000 طلب/ساعة
- **لـ AI APIs**: 50 طلب/ساعة

---

## 🧪 اختبار الـ APIs

### استخدام Postman:

```
1. استيراد الـ APIs من:
   GET http://localhost:5000/api/docs

2. اضبط الـ Authorization:
   - Type: Bearer Token
   - Token: <YOUR_JWT_TOKEN>

3. اختبر الـ Endpoints
```

### استخدام cURL:

```bash
curl -X GET http://localhost:5000/api/users/me \
  -H "Authorization: Bearer <JWT_TOKEN>" \
  -H "Content-Type: application/json"
```

---

## 📚 موارد إضافية

- [OpenAPI Specification](./openapi.yaml)
- [Webhooks Documentation](./webhooks.md)
- [Rate Limiting Guide](./rate-limiting.md)
- [Error Handling Guide](./error-handling.md)

---

تم! هذه هي جميع الـ APIs الرئيسية. سيتم إضافة المزيد لاحقاً 🚀
