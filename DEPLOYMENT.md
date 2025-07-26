# دليل النشر على Vercel

## خطوات النشر

### 1. إعداد المشروع
تم تجهيز المشروع بالكامل للنشر على Vercel مع التعديلات التالية:

- ✅ إنشاء ملف `vercel.json` بالإعدادات المطلوبة
- ✅ إضافة ملف `api/index.js` كنقطة دخول للـ serverless functions
- ✅ إنشاء ملف `index.html` في الجذر
- ✅ إضافة ملف `.env.example` مع متغيرات البيئة المطلوبة

### 2. رفع المشروع إلى GitHub
```bash
git init
git add .
git commit -m "Initial commit: Saudi legal consultation app"
git branch -M main
git remote add origin <your-github-repo-url>
git push -u origin main
```

### 3. ندخل إلى Vercel
1. اذهب إلى [vercel.com](https://vercel.com)
2. اربط حسابك مع GitHub
3. اختر "Import Project"
4. اختر مستودع المشروع من GitHub

### 4. إعداد متغيرات البيئة في Vercel
في لوحة تحكم Vercel، اذهب إلى:
Settings → Environment Variables

أضف هذه المتغيرات:
```
GEMINI_API_KEY = مفتاح Google Gemini API الخاص بك
NODE_ENV = production
```

### 5. إعدادات البناء (Build Settings)
Vercel سيكتشف الإعدادات تلقائياً من `vercel.json`:
- **Build Command**: `npm run build`
- **Output Directory**: `dist`
- **Install Command**: `npm install`

### 6. النشر
اضغط على "Deploy" وانتظر حتى يكتمل البناء والنشر.

## ملاحظات مهمة

### الحصول على مفتاح Gemini API
1. اذهب إلى [Google AI Studio](https://aistudio.google.com/app/apikey)
2. أنشئ مفتاح API جديد
3. انسخ المفتاح واستخدمه في متغيرات البيئة

### إعدادات vite.config.ts
⚠️ **تنبيه**: لا يمكن تعديل ملف `vite.config.ts` في Replit، لكن الإعدادات الحالية تعمل مع Vercel.

المشروع يستخدم:
- `root: client/` - مجلد العمل للـ frontend
- `outDir: dist/public` - مجلد المخرجات للبناء
- Aliases محددة للـ imports

### هيكل الملفات بعد البناء
```
dist/
├── public/          # ملفات الـ frontend المبنية
│   ├── index.html
│   ├── assets/
│   └── ...
├── index.js         # الـ backend المبني
└── ...
```

### حل المشاكل الشائعة

**1. مشكلة في استيراد الملفات**
- تأكد من أن جميع المسارات النسبية صحيحة
- تحقق من أن aliases في vite.config.ts تطابق بنية المشروع

**2. مشكلة في API**
- تأكد من إضافة `GEMINI_API_KEY` في متغيرات البيئة
- تحقق من أن الـ API endpoints تعمل محلياً قبل النشر

**3. مشكلة في الـ routing**
- Vercel يعيد توجيه جميع المسارات إلى index.html للـ SPA
- API routes يتم توجيهها إلى `/api/*`

### اختبار محلي للنشر
```bash
# بناء المشروع
npm run build

# تشغيل الإنتاج محلياً
npm run start
```

### الدومين المخصص (اختياري)
بعد النشر الناجح، يمكنك:
1. إضافة دومين مخصص في إعدادات Vercel
2. ربط الدومين بـ DNS الخاص بك
3. Vercel سيوفر SSL تلقائياً

## الخطوات التالية بعد النشر
1. اختبر جميع الوظائف على الموقع المنشور
2. تحقق من عمل الاستشارات القانونية
3. اختبر تصدير PDF
4. تأكد من عمل جميع الصفحات والروابط

المشروع الآن جاهز بالكامل للنشر على Vercel! 🚀