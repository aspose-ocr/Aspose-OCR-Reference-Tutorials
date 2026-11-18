---
category: general
date: 2026-03-28
description: تعلم كيفية استخراج النص من الصورة باستخدام C# أثناء تحميل ملف الصورة
  وتحديد لغة OCR للمعالجة دون اتصال. لا حاجة للإنترنت.
draft: false
keywords:
- extract text from image
- load image file c#
- set ocr language
language: ar
og_description: استخراج النص من الصورة باستخدام وضع OCR غير المتصل من Aspose. دليل
  خطوة بخطوة لتحميل ملف الصورة في C# وتعيين لغة OCR دون استدعاءات شبكة.
og_title: استخراج النص من صورة في C# – دليل OCR كامل دون اتصال
tags:
- OCR
- C#
- Aspose
title: استخراج النص من الصورة في C# – دليل OCR غير المتصل
url: /ar/net/text-recognition/extract-text-from-image-in-c-offline-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة في C# – دليل OCR غير المتصل

هل احتجت يوماً إلى **استخراج النص من صورة** وتكره فكرة إرسال الملفات عبر الإنترنت؟ لست وحدك. في العديد من الصناعات الخاضعة للتنظيم، لا يمكن للبيانات مغادرة الموقع، لذا يصبح حل OCR غير المتصل ضرورياً. يوضح لك هذا الدليل بالضبط كيفية استخراج النص من صورة في C# باستخدام وضع Aspose OCR غير المتصل—بدون أي استدعاءات شبكة، مجرد معالجة محلية خالصة.

سنستعرض معاً تحميل ملف صورة باستخدام كود C#، إعداد نموذج اللغة، وأخيراً استخراج النص المعترف به من الصورة. في النهاية، ستحصل على تطبيق console جاهز للتشغيل ي استخراج النص من صورة دون الحاجة إلى السحابة. لا إضافات غير ضرورية، مجرد حل عملي من البداية إلى النهاية يمكنك دمجه في مشاريعك.

## ما ستحتاجه

- **.NET 6 أو أحدث** (الكود يعمل مع .NET Core و .NET Framework أيضاً)
- حزمة NuGet **Aspose.OCR for .NET** (الإصدار 23.6 أو أحدث)
- صورة نموذجية (PNG أو JPG أو TIFF) تحتوي على نص واضح ومقروء
- Visual Studio أو Rider أو أي محرر C# تفضله

هذا كل شيء—بدون خدمات إضافية، بدون مفاتيح API. إذا كان لديك بيئة تطوير C# جاهزة، فأنت مستعد للبدء.

## الخطوة 1 – إنشاء محرك OCR وتفعيل وضع عدم الاتصال  

أول ما عليك فعله هو إنشاء كائن `OcrEngine` وتفعيل الخاصية `OfflineMode`. هذا يخبر Aspose OCR بالاعتماد فقط على حزم اللغة المرفقة مع المكتبة.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class OfflineModeTutorial
{
    static void Main()
    {
        // Initialize the OCR engine and force offline processing
        var ocrEngine = new OcrEngine
        {
            OfflineMode = true   // <-- crucial for on‑premise scenarios
        };
```

**لماذا هذا مهم:**  
عند كون `OfflineMode` مساويًا لـ `true`، لن يحاول المحرك تنزيل أي بيانات لغة أو إرسال بيانات تتبع. هذا يضمن الامتثال لسياسات خصوصية البيانات الصارمة.

## الخطوة 2 – تحميل ملف الصورة بأسلوب C#  

الآن بعد أن أصبح المحرك جاهزًا، نحتاج إلى تزويده بصورة. تحميل ملف صورة في C# سهل باستخدام `System.Drawing.Image.FromFile`. فقط تأكد أن المسار يشير إلى ملف حقيقي على القرص.

```csharp
        // Step 2: Load the image you want to process
        string imagePath = "YOUR_DIRECTORY/offline_test.png";
        ocrEngine.Image = Image.FromFile(imagePath);
```

> **نصيحة احترافية:** إذا كنت تستهدف .NET Core على Linux، أضف حزمة `System.Drawing.Common` واضبط المتغير `LD_LIBRARY_PATH` ليشير إلى `libgdiplus`. وإلا ستحصل على استثناء وقت التشغيل.

**تحذير حالة حافة:**  
صورة فارغة أو تالفة ستؤدي إلى رمي `FileNotFoundException` أو `ArgumentException`. غلف كود التحميل بكتلة try‑catch إذا كنت تتوقع مدخلات غير موثوقة.

## الخطوة 3 – تعيين لغة OCR قبل التعرف  

تأتي Aspose OCR مع عدة حزم لغات، لكن عليك إخبار المحرك أي منها ستستخدم. هنا نـ **نحدد لغة OCR** للجلسة.

```csharp
        // Step 3: Specify the language model(s) that are available locally
        ocrEngine.Language = new[] { "English" }; // you can add more, e.g., "French", "Spanish"
```

**لماذا يجب عليك تعيين اللغة:**  
تقييد المحرك على اللغات التي تحتاجها فعليًا يسرّع عملية التعرف ويقلل من استهلاك الذاكرة. إذا تخطيت هذه الخطوة، سيحاول المحرك التخمين، مما قد يكون أبطأ وأقل دقة.

## الخطوة 4 – تنفيذ عملية OCR  

مع كل الإعدادات جاهزة، يصبح استخراج النص عملية نداء طريقة واحدة. طريقة `Recognize` تُعيد السلسلة المعترف بها.

```csharp
        // Step 4: Perform the OCR operation
        string recognizedText = ocrEngine.Recognize();

        // Step 5: Output the recognized text to the console
        Console.WriteLine(recognizedText);
    }
}
```

**ما ستراه:**  
إذا كانت الصورة تحتوي على العبارة “Hello World”، سيطبع الـ console:

```
Hello World
```

إذا كان للصورة عدة أسطر، سيفصل كل سطر بحرف سطر جديد (`\n`). يمكنك بعد ذلك معالجة السلسلة—إزالة الفراغات الزائدة، تقسيمها إلى كلمات، أو تمريرها إلى خط أنابيب NLP لاحق.

## مثال كامل يعمل  

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑لصقه في مشروع console جديد. تذكر استبدال `YOUR_DIRECTORY/offline_test.png` بالمسار الفعلي لصورتك التجريبية.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class OfflineModeTutorial
{
    static void Main()
    {
        // 1️⃣ Create OCR engine and enable offline mode
        var ocrEngine = new OcrEngine
        {
            OfflineMode = true
        };

        // 2️⃣ Load image file C# style
        string imagePath = "YOUR_DIRECTORY/offline_test.png";
        ocrEngine.Image = Image.FromFile(imagePath);

        // 3️⃣ Set OCR language (English only in this demo)
        ocrEngine.Language = new[] { "English" };

        // 4️⃣ Run OCR and capture the result
        string recognizedText = ocrEngine.Recognize();

        // 5️⃣ Show the output
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

شغّل البرنامج (`dotnet run` من الطرفية أو اضغط F5 في Visual Studio) وراقب مخرجات الـ console. إذا تم كل شيء بشكل صحيح، فقد **استخراجت النص من صورة** دون مغادرة جهازك.

![استخراج النص من صورة باستخدام وضع Aspose OCR غير المتصل](extract-text-image.png)

*نص بديل للصورة: “استخراج النص من صورة باستخدام وضع Aspose OCR غير المتصل”*  

## أسئلة شائعة ومشكلات محتملة  

- **ماذا لو احتجت إلى التعرف على لغة غير موجودة في الحزمة؟**  
  توفر Aspose OCR حزم لغات إضافية يمكنك تحميلها من بوابة Aspose. ضع ملف `.dat` في نفس مجلد الملف التنفيذي وأضف اسمه إلى مصفوفة `Language`.

- **هل يمكنني معالجة ملفات PDF بدلاً من PNG؟**  
  نعم. حوّل كل صفحة PDF إلى صورة أولاً (مثلاً باستخدام `Aspose.PDF`) ثم مرّر الـ bitmap إلى محرك OCR. يبقى سير العمل نفسه.

- **هل المحرك آمن للاستخدام عبر الخيوط المتعددة؟**  
  لا يُنصح بمشاركة كائن `OcrEngine` واحد بين الخيوط. أنشئ محركًا جديدًا لكل طلب إذا كنت تبني خدمة ويب.

- **نصيحة أداء:**  
  للمعالجة الدفعية، أعد استخدام نفس المحرك لكن استدعِ `ocrEngine.Reset()` بين الصور. هذا يتجنب عبء إعادة تهيئة بيانات اللغة.

## الخطوات التالية  

الآن بعد أن أصبحت قادرًا على **استخراج النص من صورة**، فكر في الأفكار التالية:

1. **حفظ النتائج** – اكتب النص المعترف به إلى قاعدة بيانات أو ملف JSON.  
2. **دمج مع AI** – مرّر المخرجات إلى Azure Cognitive Services لتحليل المشاعر.  
3. **الوضع الدفعي** – كرّر العملية على مجلد من الصور، اجمع النتائج، وأنشئ تقريرًا ملخصًا.  

كل من هذه الإضافات سيتطلب أيضًا تحميل ملفات الصور بـ C# وربما تعيين لغة OCR لكل دفعة، لكن النمط الأساسي يظل كما هو.

---

### TL;DR  

- استخدم `OfflineMode` في Aspose OCR لإبقاء المعالجة داخل الموقع.  
- حمّل الصورة باستخدام `Image.FromFile` (**load image file C#**).  
- حدّد اللغة عبر `ocrEngine.Language` (**set OCR language**).  
- استدعِ `Recognize()` وستكون قد **استخراجت النص من صورة** بنجاح.

جرّبه، عدّل مصفوفة اللغات، وشاهد السرعة التي يمكنك بها تحويل المستندات الممسوحة ضوئياً إلى نص قابل للبحث. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}