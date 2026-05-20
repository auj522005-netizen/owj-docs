# أوج (OWJ) - الأركتكتشر الكامل

> مرشدك الذكي الشخصي - تطبيق Flutter بالعربي المصري

---

## 1. نظرة عامة

| العنصر | التفاصيل |
|--------|----------|
| **اسم التطبيق** | أوج (OWJ) |
| **الوصف** | مرشدك الذكي الشخصي - AI Mentor App |
| **اللغة** | عربي مصري فقط (RTL) |
| **المنصة** | Android (minSdk 24, targetSdk 34) |
| **حزمة التطبيق** | com.owj.owj_app |
| **الإصدار** | 3.1.0 |
| **حجم الـ APK** | ~49 MB |

---

## 2. التقنيات المستخدمة

### 2.1 الإطار الأساسي

| التقنية | الإصدار | الاستخدام |
|---------|---------|-----------|
| **Flutter** | 3.24.5 | إطار التطوير الرئيسي |
| **Dart** | 3.5.4 | لغة البرمجة |
| **Android Gradle Plugin** | 8.1.4 | بناء الأندرويد |
| **Gradle** | 8.4 | نظام البناء |
| **Kotlin** | 1.9.22 | دعم Android |
| **JDK** | 17 | Java compiler |

### 2.2 حزم Flutter

| الحزمة | الإصدار | الاستخدام |
|--------|---------|-----------|
| `provider` | 6.1.2 | إدارة الحالة (State Management) |
| `shared_preferences` | 2.3.3 | تخزين محلي (Key-Value) |
| `http` | 1.2.1 | HTTP requests لـ APIs |
| `uuid` | 4.5.1 | توليد معرفات فريدة |
| `intl` | 0.19.0 | تنسيق التواريخ والأرقام |
| `url_launcher` | 6.3.1 | فتح الروابط الخارجية |
| `share_plus` | 10.1.2 | مشاركة المحتوى |
| `cupertino_icons` | 1.0.8 | أيقونات iOS style |
| `collection` | 1.18.0 | أدوات جمع البيانات |

### 2.3 إعدادات Android

| الإعداد | القيمة |
|---------|--------|
| `compileSdk` | 34 |
| `minSdk` | 24 |
| `targetSdk` | 34 |
| `multiDexEnabled` | true |
| `Java Compatibility` | VERSION_17 |
| `minifyEnabled (release)` | true |
| `shrinkResources (release)` | true |
| `R8/ProGuard` | مفعّل مع rules مخصصة |

### 2.4 أذونات Android

| الإذن | الاستخدام |
|-------|-----------|
| `INTERNET` | اتصال بـ AI APIs والبحث |
| `POST_NOTIFICATIONS` | إرسال إشعارات (Android 13+) |
| `RECEIVE_BOOT_COMPLETED` | تشغيل الإشعارات بعد إعادة التشغيل |
| `SCHEDULE_EXACT_ALARM` | جدولة إشعارات دقيقة |
| `VIBRATE` | اهتزاز عند الإشعارات |

---

## 3. مزودي الذكاء الاصطناعي (AI Providers)

### 3.1 المزودون المدعومون

| المزود | الموديل | الـ Endpoint | الأولوية |
|--------|---------|-------------|----------|
| **Gemini** | gemini-2.0-flash | `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent` | الأساسي |
| **Groq** | llama-3.3-70b-versatile | `https://api.groq.com/openai/v1/chat/completions` | Fallback 1 |
| **BigModel** | glm-4-flash | `https://open.bigmodel.cn/api/paas/v4/chat/completions` | Fallback 2 |
| **OpenRouter** | google/gemini-2.0-flash-exp:free | `https://openrouter.ai/api/v1/chat/completions` | Fallback 3 |
| **OpenAI** | gpt-4o-mini | `https://api.openai.com/v1/chat/completions` | Fallback 4 |
| **Cerebras** | llama-3.3-70b | `https://api.cerebras.ai/v1/chat/completions` | Fallback 5 |

### 3.2 آلية Fallback

```
المستخدم يرسل رسالة
    ↓
محاولة الموديل المختار أولاً
    ↓ فشل
محاولة Groq → BigModel → OpenRouter → OpenAI → Cerebras → Gemini
    ↓ كلهم فشلوا
رسالة خطأ: "مفيش مفتاح API شغال"
```

### 3.3 Multi-Model Parallel Call

التطبيق يدعم استدعاء عدة موديلات في نفس الوقت بالتوازي عبر `callMultipleModels()`:
- كل موديل يشتغل بشكل مستقل
- النتائج تتجمع في Map<String, String>
- مفيد للمقارنة بين ردود الموديلات المختلفة

### 3.4 قدرات الموديلات

| المزود | القدرات |
|--------|---------|
| **Gemini** | محادثة - بحث - تحليل - إبداع - ترجمة |
| **Groq** | محادثة - سرعة - برمجة - تحليل - رياضيات |
| **BigModel** | محادثة - تحليل - ترجمة - صيني |
| **OpenRouter** | محادثة - بحث - تحليل - إبداع - متنوع |
| **OpenAI** | محادثة - برمجة - تحليل - إبداع - رياضيات |
| **Cerebras** | محادثة - سرعة - برمجة - رياضيات |

---

## 4. خدمات خارجية (External Services)

### 4.1 Mem0 - الذاكرة السحابية

| العنصر | التفاصيل |
|--------|----------|
| **الاستخدام** | تخزين واسترجاع ذكريات المستخدم سحابياً |
| **Endpoint (كتابة)** | `https://api.mem0.ai/v1/memories/` (POST) |
| **Endpoint (قراءة)** | `https://api.mem0.ai/v1/memories/?user_id=owj_user` (GET) |
| **المصادقة** | Token-based: `Authorization: Token {api_key}` |
| **User ID** | owj_user |
| **المزامنة** | تلقائية عند إضافة ذكرى + يدوية من زر Sync |

### 4.2 Tavily - البحث على الويب

| العنصر | التفاصيل |
|--------|----------|
| **الاستخدام** | بحث في الويب من داخل الشات |
| **Endpoint** | `https://api.tavily.com/search` (POST) |
| **المصادقة** | API Key في body: `{"api_key": "..."}` |
| **المعاملات** | `query`, `max_results: 5`, `include_answer: true` |
| **التفعيل** | تلقائي عند أمر `[بحث: استعلام]` في الشات |

### 4.3 Tavily MCP - الأخبار

| العنصر | التفاصيل |
|--------|----------|
| **الاستخدام** | أخبار MCP وأحداث مباشرة |
| **نوع المفتاح** | `tmcp_live_...` |
| **البروتوكول** | MCP (Model Context Protocol) |

### 4.4 ElevenLabs - تحويل النص لصوت

| العنصر | التفاصيل |
|--------|----------|
| **الاستخدام** | تحويل ردود AI لصوت (مخطط للمستقبل) |
| **API** | ElevenLabs Text-to-Speech |

### 4.5 Firebase

| العنصر | التفاصيل |
|--------|----------|
| **API Key** | AIzaSyC-vP1tL8mScRgj52kj5t0ELDbyCCX50tw |
| **Project ID** | auj-3a770 |
| **App ID** | 1:28899937849:android:d45cdba2a9b703564e07e8 |
| **الاستخدام** | تخزين سحابي وإشعارات push (مخطط) |

### 4.6 تكاملات أخرى

| الخدمة | الاستخدام |
|--------|-----------|
| **GitHub API** | الوصول للريبوهات والكود |
| **Notion API** | مزامنة الملاحظات والمهام |
| **YouTube Data API** | بحث الفيديوهات والبحث عن المحتوى |
| **Gmail API** | إرسال وقراءة الإيميلات (Client ID + Secret + OAuth) |

---

## 5. مفاتيح API (18 مفتاح)

| # | الخدمة | مفتاح التخزين | الافتراضي |
|---|--------|--------------|-----------|
| 1 | Gemini | api_key_gemini | AIzaSyB59... |
| 2 | Groq | api_key_groq | gsk_kjm4y3... |
| 3 | BigModel | api_key_bigmodel | 0637dca6... |
| 4 | OpenRouter | api_key_openrouter | sk-or-v1-f6... |
| 5 | OpenAI | api_key_openai | sk-proj-LXlz... |
| 6 | Cerebras | api_key_cerebras | csk-nrhxh9... |
| 7 | Mem0 | api_key_mem0 | m0-XIe27... |
| 8 | Tavily | api_key_tavily | tvly-dev-Cy... |
| 9 | Tavily MCP | api_key_tavily_mcp | tmcp_live_6... |
| 10 | ElevenLabs | api_key_elevenlabs | sk_50bb91... |
| 11 | GitHub | api_key_github | ghp_cmGRB... |
| 12 | Notion | api_key_notion | ntn_N71191... |
| 13 | YouTube | api_key_youtube | AIzaSyA3N... |
| 14 | Gmail Client ID | api_key_gmail_client_id | 66778730... |
| 15 | Gmail Secret | api_key_gmail_client_secret | GOCSPX-lj... |
| 16 | Firebase API | api_key_firebase_api | AIzaSyC-v... |
| 17 | Firebase Project | api_key_firebase_project_id | auj-3a770 |
| 18 | Firebase App | api_key_firebase_app_id | 1:288999... |

> **ملاحظة:** المفاتيح مخزنة كـ charcode arrays في الكود (تشفير بسيط) وبتتحمل تلقائي أول مرة التطبيق يفتح.

---

## 6. هيكل التطبيق (App Structure)

### 6.1 بنية الملفات

```
lib/
├── main.dart                          # نقطة الدخول - MultiProvider + MaterialApp
├── core/
│   ├── constants.dart                 # كل الثوابت: API keys, endpoints, شخصيات, أوامر
│   └── theme.dart                     # الثيم الداكن والفاتح + ألوان ذهبية
├── providers/
│   ├── app_provider.dart              # الوضع الداكن/الفاتح + أول تشغيل
│   ├── api_keys_provider.dart         # إدارة مفاتيح API + اختيار الموديل
│   ├── chat_provider.dart             # منطق الشات + استدعاء AI + أوامر + بحث
│   ├── tasks_provider.dart            # إدارة المهام (CRUD)
│   ├── goals_provider.dart            # إدارة الأهداف (CRUD + تقدم)
│   ├── habits_provider.dart           # إدارة العادات (تتبع + streak)
│   ├── journal_provider.dart          # إدارة المذكرات (مزاج + تاجات)
│   ├── memory_provider.dart           # الذاكرة المحلية + مزامنة Mem0
│   ├── character_provider.dart        # الشخصيات + شخصيات مخصصة
│   └── notification_provider.dart     # الإشعارات + أنواعها
└── screens/
    ├── home_screen.dart               # الشاشة الرئيسية - Bottom Nav 8 تابات
    ├── chat_screen.dart               # واجهة الشات + اختيار موديل + اقتراحات
    ├── tasks_screen.dart              # المهام + تابات + أولويات
    ├── goals_screen.dart              # الأهداف + شريط تقدم + معالم
    ├── habits_screen.dart             # العادات + تتبع يومي + streak
    ├── journal_screen.dart            # المذكرات + مزاج + تاجات
    ├── memory_screen.dart             # الذاكرة + بحث + تصنيفات + مزامنة
    ├── characters_screen.dart         # الشخصيات + إضافة مخصصة
    └── settings_screen.dart           # الإعدادات + مفاتيح + موديل + ثيم
```

### 6.2 إجمالي الكود

| الفئة | عدد الملفات | عدد السطور |
|-------|------------|-----------|
| Core | 2 | 409 |
| Providers | 9 | 1,223 |
| Screens | 8 | 3,293 |
| **الإجمالي** | **19** | **4,925** |

---

## 7. الشخصيات (Characters)

| الشخصية | الإيموجي | الوصف | الأسلوب |
|---------|----------|-------|---------|
| **وصال** | 💬 | صديقتك المقربة | دافئ وحميمي، تتفهم مشاعرك |
| **حكيم** | 🧠 | مرشدك الروحي | عميق وحكيم، حكم وفلسفة |
| **رفيق** | 🤝 | رفيق الطريق | محفز وإيجابي، تشجيع |
| **معلم** | 📚 | معلمك الشخصي | تعليمي مبسط، شرح واضح |
| **مبشر** | 🌟 | مبشرك اليومي | مرح ومبشر، أخبار إيجابية |

> كل الشخصيات تدعم أوامر الشات (إضافة مهام، أهداف، عادات، مذكرة، بحث)
> يمكن إضافة حتى 5 شخصيات مخصصة

---

## 8. أوامر الشات (Chat Commands)

| الأمر | الصيغة | النتيجة |
|-------|--------|---------|
| إضافة مهمة | `[اضافة_مهمة: العنوان]` | مهمة جديدة في تاب المهام |
| إضافة هدف | `[اضافة_هدف: العنوان]` | هدف جديد في تاب الأهداف |
| إضافة عادة | `[اضافة_عادة: الاسم]` | عادة جديدة في تاب العادات |
| إضافة مذكرة | `[اضافة_مذكرة: العنوان]` | مذكرة جديدة في تاب المذكرات |
| بحث | `[بحث: الاستعلام]` | بحث Tavily + رد مبنى على النتائج |

---

## 9. تصميم الواجهة (UI Design)

### 9.1 نظام الألوان

| اللون | الكود | الاستخدام |
|-------|-------|-----------|
| **Gold** | #D4A843 | اللون الأساسي |
| **Gold Light** | #E8C96A | اللون الثانوي |
| **Gold Dark** | #B8922E | اللون الفاتح |
| **Dark BG** | #0D1117 | خلفية الوضع الداكن |
| **Dark Surface** | #161B22 | السطح الداكن |
| **Dark Card** | #1C2333 | البطاقات الداكنة |
| **Success** | #2EA043 | نجاح/إكمال |
| **Error** | #F85149 | خطأ/حذف |
| **Warning** | #D29922 | تحذير |
| **Info** | #58A6FF | معلومات |

### 9.2 التابات (8 تابات)

1. 💬 الشات - المحادثة مع AI
2. ✅ المهام - إدارة المهام
3. 🎯 الأهداف - تتبع الأهداف
4. 🔄 العادات - بناء العادات
5. 📖 المذكرات - يوميات ومشاعر
6. 🧠 الذاكرة - ذكريات وتصنيفات
7. 🤖 الشخصيات - اختيار وتخصيص
8. ⚙️ الإعدادات - ضبط التطبيق

---

## 10. تخزين البيانات

| البيانات | طريقة التخزين | المفتاح |
|----------|--------------|---------|
| مفاتيح API | SharedPreferences | api_key_* |
| رسائل الشات | SharedPreferences | chat_messages (JSON) |
| الشخصية النشطة | SharedPreferences | active_character |
| الموديل المختار | SharedPreferences | selected_model |
| الوضع الداكن/الفاتح | SharedPreferences | is_dark_mode |
| المهام | SharedPreferences | tasks (JSON) |
| الأهداف | SharedPreferences | goals (JSON) |
| العادات | SharedPreferences | habits (JSON) |
| المذكرات | SharedPreferences | journal_entries (JSON) |
| الذكريات | SharedPreferences | memories (JSON) |
| شخصيات مخصصة | SharedPreferences | custom_char_* |
| إشعارات | In-memory | - |

> آخر 100 رسالة شات بس اللي بتتحفظ لتجنب overflow

---

## 11. بناء ونشر (Build & Deploy)

### 11.1 متطلبات البناء

```
Flutter 3.24.5+
JDK 17
Android SDK (compileSdk 34, build-tools 34.0.0)
Gradle 8.4
AGP 8.1.4
Kotlin 1.9.22
```

### 11.2 أوامر البناء

```bash
# بناء APK
flutter build apk --release

# بناء App Bundle
flutter build appbundle --release

# تنظيف
flutter clean && flutter pub get
```

### 11.3 رابط الريبو والـ Release

```
الريبو: https://github.com/auj522005-netizen/owj-app
APK: https://github.com/auj522005-netizen/owj-app/releases/download/v3.1.0/owj-app.apk
```

---

## 12. MCP (Model Context Protocol)

### 12.1 Tavily MCP Server

| العنصر | التفاصيل |
|--------|----------|
| **المفتاح** | tmcp_live_68x5pfgjq5n4tqwipr1fomqmd2692wdg |
| **الاستخدام** | أخبار وأحداث مباشرة عبر بروتوكول MCP |
| **التخزين** | api_key_tavily_mcp في SharedPreferences |

### 12.2 MCP Protocol Info

بروتوكول MCP (Model Context Protocol) بيسمح للـ AI models بالتفاعل مع أدوات خارجية:
- **Tavily MCP**: يوفر أخبار وأحداث في الوقت الحقيقي
- **MCP Client**: التطبيق يعمل كـ client يبعث طلبات للـ MCP server
- **التكامل**: مفاتيح MCP متضمنة في الـ defaults وموجودة في شاشة الإعدادات

### 12.3 MCP Servers المتاحة (مستقبلية)

| الخدمة | النوع | الحالة |
|--------|-------|--------|
| Tavily MCP | أخبار وبحث | مفتاح متوفر |
| GitHub MCP | ريبوهات وكود | مخطط |
| Notion MCP | ملاحظات ومهام | مخطط |
| Gmail MCP | بريد إلكتروني | مخطط |
| Google Calendar MCP | تقويم | مخطط |
