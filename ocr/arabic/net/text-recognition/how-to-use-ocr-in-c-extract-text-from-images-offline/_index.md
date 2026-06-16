---
category: general
date: 2026-03-07
description: تعلم كيفية استخدام OCR في C# لاستخراج النص من ملفات الصور. يوضح هذا الدليل
  OCR دون اتصال، تحويل الصورة إلى نص، وتحميل الصورة للـ OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- convert image to text
- load image for ocr
language: ar
og_description: كيفية استخدام OCR في C# لاستخراج النص من الصور دون اتصال. كود خطوة
  بخطوة، نصائح، وشرح كامل لتحويل الصورة إلى نص.
og_title: كيفية استخدام OCR في C# – دليل كامل دون اتصال
tags:
- OCR
- C#
- Aspose
title: كيفية استخدام OCR في C# – استخراج النص من الصور دون اتصال
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-offline/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – استخراج النص من الصور دون اتصال

هل تساءلت يومًا **كيف تستخدم OCR** في مشروع .NET دون إرسال البيانات إلى السحابة؟ لست وحدك. العديد من المطورين يحتاجون إلى *استخراج النص من ملفات الصورة* على محطة عمل مؤمنة، ويخشون أن يكشف مرور الشبكة عن معلومات حساسة.  

الخبر السار؟ باستخدام Aspose.OCR يمكنك التعرف على النص من PNG أو JPEG أو PDF بالكامل دون اتصال. في هذا الدرس سنستعرض تحميل صورة للـ OCR، تهيئة المحرك للوضع غير المتصل، وأخيرًا **تحويل الصورة إلى نص** ببضع أسطر من C#.

بنهاية هذا الدليل ستكون قادرًا على:

* تثبيت حزمة Aspose.OCR عبر NuGet.  
* إعداد محرك OCR للمعالجة دون اتصال.  
* تحميل صورة للـ OCR واستخراج محتواها النصي.  

بدون خدمات خارجية، بدون مفاتيح API—فقط كود C# نقي يعمل على أي جهاز Windows أو Linux.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+).  
* Visual Studio 2022، VS Code، أو أي محرر يدعم C#.  
* نسخة من مكتبة **Aspose.OCR** – يمكنك جلبها من NuGet (`Aspose.OCR`).  
* مجلد موارد OCR (`Resources`) المرفق مع المكتبة (يحتوي على ملفات بيانات اللغات).  
* صورة نموذجية (مثال: `offline_test.png`) موجودة في دليل معروف.

> **نصيحة احترافية:** احفظ مجلد الموارد بجوار الملف التنفيذي؛ فهذا يبسط إعداد `ResourcesPath`.

---

## الخطوة 1: تثبيت حزمة Aspose.OCR من NuGet

أولاً، أضف المكتبة إلى مشروعك. افتح الطرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

أو، إذا كنت تفضّل واجهة Visual Studio، انقر بزر الفأرة الأيمن على **Dependencies → Manage NuGet Packages**، ابحث عن *Aspose.OCR*، ثم اضغط **Install**.

> تثبيت الحزمة يجلب جميع الثنائيات المطلوبة، لذا لن تحتاج إلى أي ملفات DLL إضافية.

---

## الخطوة 2: إنشاء وتكوين محرك OCR (كيفية استخدام OCR – الوضع غير المتصل)

الآن سننشئ محرك OCR ونخبره بالعمل **بدون اتصال**. هذا يضمن عدم حدوث أي حركة مرور شبكة أثناء التعرف.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Switch the engine to offline mode – crucial for privacy‑first apps
ocrEngine.Settings.EngineMode = EngineMode.Offline;
```

**لماذا الوضع غير المتصل؟**  
عندما يتم تعيين `EngineMode` إلى `Online`، يتواصل المحرك مع سحابة Aspose لتحميل حزم اللغات عند الحاجة. في البيئات المنظمة (المالية، الرعاية الصحية) غالبًا ما يُحظر هذا النوع من المرور. بفرض الوضع غير المتصل تضمن بقاء كل شيء على الجهاز المحلي.

---

## الخطوة 3: توجيه المحرك إلى مجلد موارد OCR

يحتاج محرك OCR إلى بيانات اللغة (نماذج مدربة) للتعرف على الأحرف. أخبره بمكان وجود هذه الملفات:

```csharp
// Replace with the absolute or relative path to your Resources folder
ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";
```

إذا لم تكن متأكدًا من موقع المجلد، ابحث عنه داخل دليل حزمة NuGet (`%USERPROFILE%\.nuget\packages\aspose.ocr\*\resources`). انسخ المجلد بالكامل إلى مشروعك لتسهيل النشر.

---

## الخطوة 4: تحميل الصورة للـ OCR (Load Image for OCR)

يمكنك تمرير أي صورة bitmap مدعومة إلى المحرك. هنا سنحمّل ملف PNG موجود على القرص:

```csharp
// Load the image you want to recognize – this is the “load image for OCR” step
ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");
```

**نصيحة:** إذا كنت تحتاج إلى معالجة الصور من تدفق (مثلاً، تم رفعه عبر API)، استخدم `ImageStream.FromStream(yourStream)` بدلاً من ذلك.

---

## الخطوة 5: تشغيل عملية التعرف وتحويل الصورة إلى نص

مع كل شيء جاهز، شغّل OCR. طريقة `Recognize()` تقوم بالعمل الشاق، والنص المستخرج يصبح متاحًا عبر خاصية `Text`.

```csharp
// Perform OCR – this is where the engine reads the pixels and produces text
ocrEngine.Recognize();

// Grab the result – now you have “convert image to text” completed
string extractedText = ocrEngine.Text;
```

---

## الخطوة 6: إخراج النص المستخرج

أخيرًا، اعرض النتيجة. في تطبيق console يمكنك كتابة النص إلى الـ console، أما في Web API فستعيد السلسلة كـ JSON.

```csharp
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

تشغيل البرنامج يجب أن يطبع محتوى `offline_test.png`. على سبيل المثال، إذا كانت الصورة تحتوي على العبارة *“Hello, World!”*، سترى:

```
=== OCR Result ===
Hello, World!
```

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه إلى مشروع console جديد (`dotnet new console`) وعدّل المسارات لتتناسب مع بيئتك.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2: Set offline mode – no network traffic
        // -------------------------------------------------
        ocrEngine.Settings.EngineMode = EngineMode.Offline;

        // -------------------------------------------------
        // Step 3: Provide path to OCR resource files
        // -------------------------------------------------
        ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";

        // -------------------------------------------------
        // Step 4: Load the image you want to recognize
        // -------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");

        // -------------------------------------------------
        // Step 5: Run recognition and extract text
        // -------------------------------------------------
        ocrEngine.Recognize();
        string extractedText = ocrEngine.Text;

        // -------------------------------------------------
        // Step 6: Show the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

> **الناتج المتوقع:** يطبع الـ console النص الدقيق الموجود في ملف PNG. إذا كانت الصورة غير واضحة، قد يتضمن الناتج أحرفًا غير صحيحة—انظر قسم استكشاف الأخطاء وإصلاحها أدناه.

---

## المشكلات الشائعة والنصائح (Recognize Text from PNG Efficiently)

| المشكلة | السبب | طريقة الحل |
|-------|-------|------------|
| **إخراج فارغ** | `ResourcesPath` يشير إلى المجلد الخطأ أو ملفات اللغة مفقودة. | تأكد من وجود `eng.traineddata` (أو ملفات لغات أخرى) في المجلد وتحقق من صحة مسار السلسلة. |
| **حروف غير مفهومة** | دقة الصورة منخفضة أو الصورة غير مفرزة. | عالج الصورة مسبقًا (زيادة DPI، تطبيق `ImageProcessor` للحدّ من الضبابية). |
| **بطء الأداء** | معالجة صور كبيرة بدقة كاملة. | قلّص حجم الصورة إلى عرض أقصى 2000 px قبل تمريرها إلى OCR. |
| **صيغة غير مدعومة** | استخدام BMP بصيغة بكسل غير شائعة. | حوّل الصورة إلى PNG أو JPEG أولًا (`System.Drawing.Image.Save`). |

**نصيحة احترافية:** إذا كنت بحاجة إلى التعرف على عدة لغات، عيّن `ocrEngine.Settings.Language = Language.English | Language.French;` قبل استدعاء `Recognize()`.

---

## الأسئلة المتكررة

**س: هل يمكن تشغيل هذا الكود على Linux؟**  
بالتأكيد. Aspose.OCR متعدد المنصات؛ فقط تأكد من وجود المكتبات الأصلية (مضمنة مع حزمة NuGet).

**س: ماذا أفعل إذا لم يكن لدي مجلد Resources؟**  
يمكنك تحميل حزم اللغات المجانية من موقع Aspose أو استخراجها من حزمة NuGet (`.../aspose.ocr/<version>/resources`).

**س: هل يمكن الحصول على درجات الثقة؟**  
نعم. بعد `Recognize()`، تفقد `ocrEngine.RecognizedWords`—كل كلمة تحتوي على خاصية `Confidence`.

---

## الخلاصة

غطّينا **كيفية استخدام OCR** في C# لاستخراج النص من ملفات الصور بالكامل دون اتصال. عبر تثبيت Aspose.OCR، ضبط `EngineMode.Offline`، توجيه الموارد، تحميل صورة، واستدعاء `Recognize()`، يمكنك تحويل الصورة إلى نص بثقة دون الحاجة للإنترنت.  

خذ الكود أعلاه، استبدل مسارات الصور الخاصة بك، وابدأ في بناء ميزات مثل PDFs قابلة للبحث، أتمتة إدخال البيانات، أو أدوات تحسين الوصول. لاحقًا، يمكنك استكشاف **التعرف على النص من PNG** على نطاق واسع، أو دمج المحرك في API ASP.NET Core لتقديم نتائج OCR لتطبيقات الواجهة الأمامية.

برمجة سعيدة، ولا تتردد في التجربة—OCR يتسامح بشكل مدهش بمجرد إعداد المحرك بشكل صحيح!

--- 

![Diagram showing offline OCR workflow – how to use OCR in a secure environment](https://example.com/ocr-workflow.png "how to use OCR diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}