---
category: general
date: 2026-06-19
description: كيفية استخدام OcrEngineConfig للتعرف الضوئي على الحروف العربية في C#.
  تعلّم تعيين اللغة، وتعطيل التحميل التلقائي، وتوجيهه إلى الموارد المخصّصة – دليل
  شامل.
draft: false
keywords:
- how to use ocrengineconfig
- OCR engine configuration
- Arabic OCR language
- disable auto download
- set resources path
- OcrEngineConfig example
language: ar
og_description: كيفية استخدام OcrEngineConfig لتقنية التعرف الضوئي على الحروف العربية
  في C#. يوضح هذا الدليل اختيار اللغة، وتعطيل التحميل التلقائي، ومسارات الموارد المخصصة.
og_title: كيفية استخدام OcrEngineConfig – تكوين محرك OCR في C#
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to use OcrEngineConfig for Arabic OCR in C#. Learn to set language,
    disable auto‑download, and point to custom resources – a complete guide.
  headline: How to Use OcrEngineConfig – OCR Engine Configuration in C#
  type: TechArticle
- description: How to use OcrEngineConfig for Arabic OCR in C#. Learn to set language,
    disable auto‑download, and point to custom resources – a complete guide.
  name: How to Use OcrEngineConfig – OCR Engine Configuration in C#
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code works with .NET Core and .NET Framework 4.7+).
      - A reference to the OCR library that provides `OcrEngineConfig`, `Language`,
      and `OcrEngine` classes (for instance, **IronOCR**, **Tesseract .NET**, or any
      vendor‑specific SDK). - The Arabic language model already unpacked'
  - name: Expected Output
    text: 'If the model is correctly located and the language is set, you should see
      something like:'
  - name: What if I need to support multiple languages?
    text: 'Create separate `OcrEngineConfig` objects—one per language—and store them
      in a dictionary:'
  - name: How to debug a missing model file?
    text: Enable verbose logging on the OCR engine (if the library supports it) and
      watch the console for messages like *“Failed to load language data from …”*.
      Often the issue is a typo in the folder name or a missing `.traineddata` file.
  - name: Can I change the resources path at runtime?
    text: Yes, but you must recreate the `OcrEngine` after altering `ocrConfig.ResourcesPath`.
      The engine caches the model on first use, so changing the path on a live instance
      won’t have any effect.
  type: HowTo
tags:
- OCR
- C#
- .NET
title: كيفية استخدام OcrEngineConfig – تكوين محرك OCR في C#
url: /ar/net/ocr-configuration/how-to-use-ocrengineconfig-ocr-engine-configuration-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OcrEngineConfig – تكوين محرك OCR في C#

استخدام OcrEngineConfig هو سؤال شائع بين المطورين الذين يحتاجون إلى تحكم دقيق في خطوط معالجة OCR الخاصة بهم. سواء كنت تعالج فواتير ممسوحة ضوئياً، أو تقوم برقمنة مخطوطات عربية تاريخية، أو تبني ماسحًا متعدد اللغات، فإن إتقان تكوين محرك OCR يمكن أن يوفر لك الوقت والجهد.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح **كيفية استخدام OcrEngineConfig** لتعيين اللغة العربية، وإيقاف تنزيل الموارد تلقائيًا، وتوجيه المحرك إلى مجلد نموذج محلي. في النهاية ستحصل على مقتطف جاهز للتنفيذ، وتفهم سبب أهمية كل إعداد، وتعرف كيف تعدل الكود للغات أخرى أو نماذج مخصصة.

## ما ستتعلمه

- هدف كائن **OcrEngineConfig** وموقعه داخل سير عمل OCR.  
- كيفية اختيار **لغة OCR العربية** ولماذا قد تفضل نموذجًا محليًا على السحابة.  
- تأثير **تعطيل التحميل التلقائي** على سرعة بدء التشغيل وفي سيناريوهات العمل دون اتصال.  
- كيفية **تحديد مسار الموارد** حتى يحمل المحرك ملفات النموذج الصحيحة.  
- مثال كامل على **OcrEngineConfig** يمكنك نسخه ولصقه في تطبيق .NET Console.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework 4.7+).  
- إشارة إلى مكتبة OCR التي توفر الفئات `OcrEngineConfig`، `Language`، و `OcrEngine` (مثلاً **IronOCR**، **Tesseract .NET**، أو أي SDK خاص بالمورد).  
- نموذج اللغة العربية مُستخرج مسبقًا على القرص (ستحتاج إلى مجلد مثل `ArabicResources`).  
- معرفة أساسية بـ C# – إذا كتبت `Console.WriteLine` من قبل فأنت جاهز للبدء.

---

## الخطوة 1: إنشاء كائن OcrEngineConfig

أول شيء تقوم به عند تخصيص محرك OCR هو إنشاء كائن التكوين الخاص به. فكر في `OcrEngineConfig` كصندوق أدوات يتيح لك تعديل إعدادات المحرك قبل معالجة أي صورة.

```csharp
// Step 1: Create an OCR engine configuration object
var ocrConfig = new OcrEngineConfig();
```

> **لماذا هذا مهم:** بدون كائن تكوين ستُقيد بالإعدادات الافتراضية للمكتبة، والتي غالبًا ما تفترض اللغة الإنجليزية وقد تقوم بتحميل حزم لغات تلقائيًا لا تريدها.

---

## الخطوة 2: اختيار العربية كلغة مستهدفة

معظم SDKs الخاصة بـ OCR توفر تعدادًا يُدعى `Language`. تعيينه إلى `Language.Arabic` يخبر المحرك باستخدام مجموعة الأحرف العربية، وقواعد التخطيط من اليمين إلى اليسار، وجداول الحروف المناسبة.

```csharp
// Step 2: Set the language to Arabic
ocrConfig.Language = Language.Arabic;
```

> **نصيحة:** إذا احتجت لتغيير اللغة أثناء التشغيل، يمكنك إعادة استخدام نفس كائن `ocrConfig` وتعيين قيمة `Language` مختلفة قبل إنشاء `OcrEngine` جديد.

---

## الخطوة 3: تعطيل التحميل التلقائي لموارد اللغة

بشكل افتراضي، العديد من مكتبات OCR ستتصل بالإنترنت في المرة الأولى التي تطلب فيها لغة غير موجودة محليًا. في بيئات الإنتاج—خاصة الأكشاك غير المتصلة أو مراكز البيانات الآمنة—هذا السلوك غير مرغوب فيه.

```csharp
// Step 3: Disable automatic download of language resources
ocrConfig.AutoDownloadResources = false;
```

> **ماذا يحدث إذا تخطيت هذه الخطوة؟** سيتوقف المحرك أثناء تنزيل نموذج العربية، مما قد يضيف عدة ثوانٍ إلى وقت بدء التشغيل وقد يفشل خلف جدار حماية.

---

## الخطوة 4: توجيه المحرك إلى نموذج العربية المحلي

الآن نخبر محرك OCR بمكان العثور على ملفات النموذج المستخرجة مسبقًا. يمكن أن يكون المسار مطلقًا أو نسبيًا؛ فقط تأكد أن المجلد يحتوي على ملفات `.traineddata` (أو ملفات خاصة بالمورد) المتوقعة.

```csharp
// Step 4: Specify the folder that contains the unpacked Arabic model
ocrConfig.ResourcesPath = "YOUR_DIRECTORY/ArabicResources/";
```

> **خطأ شائع:** استخدام شرطة مائلة أو عكسية في نهاية المسار بشكل غير متسق قد يجعل المحرك يبحث في الدليل الخطأ. تحقق من صحة المسار بتصفحه في مستكشف الملفات.

---

## الخطوة 5: تهيئة محرك OCR باستخدام التكوين الخاص بك

بعد إعداد التكوين بالكامل، يمكنك الآن إنشاء كائن محرك OCR الفعلي. هذه الخطوة تربط الإعدادات بالمحرك، مما يجعلها سارية للتعرفات اللاحقة.

```csharp
// Step 5: Create the OCR engine using the configured settings
var ocrEngine = new OcrEngine(ocrConfig);
```

> **لماذا نفصل بين التكوين والمحرك:** يتيح لك ذلك إنشاء محركات متعددة بإعدادات مختلفة (مثلاً واحد للعربية وآخر للإنجليزية) دون الحاجة لإعادة بناء كامل شجرة الكائنات في كل مرة.

---

## الخطوة 6: إجراء اختبار تعرّف بسيط

دعنا نتأكد من أن كل شيء يعمل عن طريق إمداد المحرك بصورة عربية صغيرة. ضع صورة باسم `sample_arabic.png` في مجلد المشروع `Resources`.

```csharp
// Step 6: Load an image and run OCR
string imagePath = Path.Combine(AppContext.BaseDirectory, "Resources", "sample_arabic.png");
var result = ocrEngine.Read(imagePath);

// Output the recognized text
Console.WriteLine("Recognized Arabic Text:");
Console.WriteLine(result.Text);
```

### النتيجة المتوقعة

إذا تم العثور على النموذج بشكل صحيح وتم تعيين اللغة، يجب أن ترى شيئًا مشابهًا لـ:

```
Recognized Arabic Text:
مرحبا بالعالم
```

إذا حصلت على سلسلة فارغة أو خطأ بخصوص الموارد المفقودة، تحقق مرة أخرى من `ResourcesPath` وتأكد أن `AutoDownloadResources` فعلاً `false`.

---

## الخطوة 7: معالجة الحالات الخاصة والأسئلة الشائعة

### ماذا لو أردت دعم عدة لغات؟

أنشئ كائنات `OcrEngineConfig` منفصلة—واحدة لكل لغة—واحتفظ بها في قاموس:

```csharp
var configs = new Dictionary<Language, OcrEngineConfig>
{
    { Language.Arabic, new OcrEngineConfig { Language = Language.Arabic, AutoDownloadResources = false, ResourcesPath = "ArabicResources/" } },
    { Language.English, new OcrEngineConfig { Language = Language.English, AutoDownloadResources = false, ResourcesPath = "EnglishResources/" } }
};
```

عند استلام صورة، اختر التكوين المناسب وأنشئ `OcrEngine` جديدًا.

### كيف أُصَحّح مشكلة ملف نموذج مفقود؟

فعّل تسجيل الأخطاء التفصيلية على محرك OCR (إذا كانت المكتبة تدعم ذلك) وراقب وحدة التحكم للرسائل مثل *“Failed to load language data from …”*. غالبًا ما يكون السبب خطأ إملائي في اسم المجلد أو ملف `.traineddata` مفقود.

### هل يمكن تغيير مسار الموارد أثناء التشغيل؟

نعم، لكن عليك إعادة إنشاء `OcrEngine` بعد تعديل `ocrConfig.ResourcesPath`. المحرك يخزن النموذج في الذاكرة عند الاستخدام الأول، لذا تغيير المسار على نسخة حية لن يؤثر.

---

## نصائح احترافية وأفضل الممارسات

- **احتفظ بالمحرك في ذاكرة التخزين المؤقت**: إنشاء `OcrEngine` قد يكون مكلفًا. احتفظ بنسخة Singleton لكل لغة إذا كان تطبيقك يعالج الكثير من الصور.  
- **تحقق من صحة المجلد**: قبل تمرير المسار إلى `OcrEngineConfig`، استدعِ `Directory.Exists` وارمِ استثناءً واضحًا إذا كان المجلد غير موجود.  
- **استخدم I/O غير متزامن**: إذا كنت تعالج دفعات كبيرة، اقرأ الصور باستخدام `FileStream` و `await` لاستدعاء OCR (العديد من SDKs توفر إصدارات async).  
- **قِس زمن بدء التشغيل**: تعطيل `AutoDownloadResources` يسرّع بدء التشغيل البارد بشكل ملحوظ—قِس الفرق على الأجهزة المستهدفة.  
- **الأمان**: عند التشغيل في بيئة معزولة، تأكد أن مجلد الموارد للقراءة فقط لمنع العبث.

---

## الخلاصة

لقد غطينا **كيفية استخدام OcrEngineConfig** من الصفر: إنشاء كائن التكوين، اختيار اللغة العربية، تعطيل التحميل التلقائي، وتوجيه المحرك إلى مجلد موارد محلي. المثال الكامل يوضح لك كيفية تشغيل `OcrEngine`، إمداده بصورة، والحصول على نص عربي قابل للقراءة—دون أي طلبات شبكة مخفية.

الآن يمكنك تطبيق نمط **تكوين محرك OCR** هذا على لغات أخرى، دمجه في خدمة ويب، أو إدماجه في تطبيق ماسح سطح مكتب. هل تريد التجربة؟ جرّب استبدال `Language.Arabic` بـ `Language.French`، عدّل `ResourcesPath`، وشاهد الكود يعمل على نص مختلف تمامًا.

إذا واجهت أي مشكلة، ارجع إلى قسم استكشاف الأخطاء أعلاه أو راجع وثائق SDK للحصول على علامات إضافية (مثل ضبط DPI، أو أوضاع تقسيم الصفحات). برمجة سعيدة، ولتكن خطوط OCR الخاصة بك سريعة، دقيقة، وتحت سيطرتك الكاملة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Extract OCR – OCR Configuration](/ocr/english/net/ocr-configuration/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}