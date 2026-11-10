---
category: general
date: 2026-03-04
description: تشغيل التعرف الضوئي على الحروف (OCR) على صورة باستخدام Aspose OCR في
  C#. تعلم كيفية التعرف على النص الصيني، استخراج النص من الصورة، وتحميل الصورة للتعرف
  الضوئي على الحروف في بضع خطوات فقط.
draft: false
keywords:
- run OCR on image
- recognize chinese text
- extract text from image
- load image for OCR
- recognize simplified chinese
language: ar
og_description: تشغيل OCR على صورة باستخدام Aspose OCR في C#. يوضح لك هذا الدليل كيفية
  التعرف على النص الصيني، استخراج النص من الصورة، وتحميل الصورة للـ OCR بكفاءة.
og_title: تشغيل OCR على الصورة باستخدام Aspose OCR – التعرف السريع على النص الصيني
tags:
- Aspose OCR
- C#
- Chinese OCR
title: تشغيل OCR على الصورة باستخدام Aspose OCR – التعرف على النص الصيني
url: /ar/net/text-recognition/run-ocr-on-image-with-aspose-ocr-recognize-chinese-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على الصورة – دليل C# كامل للنص الصيني

هل احتجت يوماً إلى **run OCR on image** للملفات لكنك لم تكن متأكدًا أي مكتبة ستتعامل مع الصينية المبسطة دون عناء؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحاولون **recognize Chinese text** وينتهي بهم الأمر إلى تمزيق شعرهم بسبب مشاكل الترميز.  

في هذا الدرس سنقضي على الضوضاء ونظهر لك، خطوة بخطوة، كيفية **run OCR on image** للأصول باستخدام Aspose OCR، تحميل نموذج اللغة الضروري مرة واحدة فقط، وأخيرًا **extract text from image** للملفات التي تحتوي على أحرف صينية مبسطة. في النهاية ستحصل على تطبيق console جاهز للتشغيل يطبع النص المعترف به إلى وحدة التحكم.

> **ما ستحصل عليه:** برنامج C# كامل وقابل للترجمة، شروحات *why* لكل سطر، ونصائح للتعامل مع المشكلات الشائعة مثل الموارد المفقودة أو تنسيقات الصور الخاطئة.

## ما ستحتاجه

قبل أن نبدأ، تأكد من تثبيت المتطلبات المسبقة التالية على جهاز التطوير الخاص بك:

| المتطلب | لماذا يهم |
|--------------|----------------|
| .NET 6.0 SDK or later | يوفر وقت التشغيل والمترجم لمشاريع C#. |
| Visual Studio 2022 (or VS Code with C# extension) | يوفر لك IntelliSense وتصحيح الأخطاء بسهولة. |
| Aspose.OCR NuGet package | المكتبة الأساسية التي تشغل قدرات OCR. |
| An image containing Simplified Chinese characters (e.g., `chinese_sample.png`) | المصدر الذي ستقوم **load image for OCR**. |

يمكنك سحب حزمة NuGet باستخدام:

```bash
dotnet add package Aspose.OCR
```

الآن بعد تغطية الأساسيات، دعنا نجعل المحرك يعمل.

## الخطوة 1 – اختيار نموذج اللغة (Recognize Simplified Chinese)

يقوم Aspose OCR بفصل بيانات اللغة عن المحرك الأساسي، مما يعني أنه عليك إخبار SDK أي نموذج تحتاجه. بما أننا نتعامل مع أحرف الصينية القارية، نختار نموذج **Simplified Chinese**.

```csharp
using Aspose.OCR;
using Aspose.OCR.ResourceManagement;

// Select the Simplified Chinese language model
LanguageModel languageModel = LanguageModel.ChineseSimplified;
```

*Why this matters:* يستخدم محرك OCR قواميس وشكل الأحرف المخصصة للغة. اختيار النموذج الصحيح يحسن الدقة بشكل كبير، خاصةً للخطوط الكثيفة مثل الصينية.

## الخطوة 2 – تحميل النموذج مرة واحدة (Extract Text from Image)

في المرة الأولى التي تشغّل فيها الكود ستحتاج إلى جلب ملفات النموذج من خوادم Aspose. يتولى `ResourceDownloader` ذلك نيابةً عنك. في تطبيق إنتاجي قد تجعل ذلك غير متزامن، لكن لتوضيح الدرس سنستخدم الحجب باستخدام `.Wait()`.

```csharp
// Initialise the downloader and fetch the model (runs once)
ResourceDownloader resourceDownloader = new ResourceDownloader();
resourceDownloader.DownloadModelAsync(languageModel).Wait();
```

> **نصيحة احترافية:** احفظ الموارد التي تم تحميلها في مجلد جزء من مشروعك (مثلاً `OcrResources`). بهذه الطريقة تتخطى عمليات التشغيل اللاحقة استدعاء الشبكة، مما يسرّع العملية.

## الخطوة 3 – توجيه المحرك إلى مواردك المحلية (Load Image for OCR)

الآن نقوم بإنشاء محرك OCR ونخبره بمكان وجود ملفات النموذج. يقوم `LocalResourceProvider` بقراءة الملفات من القرص، مما يلغي أي حركة مرور شبكة إضافية.

```csharp
// Create the OCR engine and link it to the local resources folder
OcrEngine ocrEngine = new OcrEngine
{
    ResourceProvider = new LocalResourceProvider(@"YOUR_DIRECTORY/OcrResources")
};
```

استبدل `YOUR_DIRECTORY` بالمسار المطلق أو النسبي الذي يشير إلى مكان تخزين ملفات النموذج.  

*Why this matters:* إذا لم يتمكن المحرك من العثور على موارد اللغة، سيثير استثناء `FileNotFoundException` ولن تتمكن من **run OCR on image** على الإطلاق.

## الخطوة 4 – تعيين اللغة للتعرف (Recognize Chinese Text)

على الرغم من أننا قمنا بتحميل نموذج Simplified Chinese، لا يزال علينا إبلاغ المحرك أي لغة يجب تطبيقها أثناء التعرف.

```csharp
// Tell the engine to use Simplified Chinese for this session
ocrEngine.Language = Language.ChineseSimplified;
```

إذا كنت تحتاج يومًا لتغيير اللغات أثناء التشغيل (مثلاً، من الصينية إلى الإنجليزية)، يمكنك ببساطة تغيير هذه الخاصية قبل استدعاء `Recognize`.

## الخطوة 5 – تحميل الصورة وتشغيل OCR (Run OCR on Image)

هذا هو جوهر الدرس: تحميل ملف صورة واستخراج محتواه النصي. طريقة `ImageInfo.Load` تقرأ الملف إلى صيغة يفهمها محرك OCR.

```csharp
// Load the image that contains Chinese characters
var imageInfo = ImageInfo.Load(@"YOUR_DIRECTORY/chinese_sample.png");

// Perform OCR – this is where we actually run OCR on image
OcrResult ocrResult = ocrEngine.Recognize(imageInfo);
```

إذا كانت الصورة كبيرة أو مليئة بالضوضاء، فكر في معالجتها مسبقًا (مثلاً، التحويل إلى ثنائي) قبل هذه الخطوة. يقدم Aspose OCR أيضًا فلاتر، لكن ذلك خارج نطاق هذا الدليل للمبتدئين.

## الخطوة 6 – إخراج النص المعترف به (Extract Text from Image)

أخيرًا، نطبع السلسلة المستخرجة إلى وحدة التحكم. في سيناريو واقعي قد تكتبها إلى قاعدة بيانات، ملف، أو تمررها إلى خدمة أخرى.

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

تشغيل البرنامج يجب أن يعرض شيئًا مثل:

```
=== Recognized Text ===
你好，世界！这是一个测试。
```

هذا كل شيء—أول **run OCR on image** الخاص بك الذي **recognize Chinese text**.

## مثال كامل وجاهز للتشغيل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع console جديد (`dotnet new console`). تذكر استبدال `YOUR_DIRECTORY` بالمسار الفعلي على جهازك.

```csharp
// ------------------------------------------------------------
// Complete C# example: Run OCR on Image and Recognize Simplified Chinese
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.ResourceManagement;

class Program
{
    static void Main()
    {
        // 1️⃣ Choose the language model (Simplified Chinese)
        LanguageModel languageModel = LanguageModel.ChineseSimplified;

        // 2️⃣ Download the model (only the first time)
        var downloader = new ResourceDownloader();
        downloader.DownloadModelAsync(languageModel).Wait();   // Blocking for tutorial simplicity

        // 3️⃣ Initialise OCR engine with local resources folder
        var ocrEngine = new OcrEngine
        {
            ResourceProvider = new LocalResourceProvider(@"YOUR_DIRECTORY/OcrResources")
        };

        // 4️⃣ Set the language for this session
        ocrEngine.Language = Language.ChineseSimplified;

        // 5️⃣ Load the image that contains Chinese text
        var imageInfo = ImageInfo.Load(@"YOUR_DIRECTORY/chinese_sample.png");

        // 6️⃣ Run OCR on the image and capture the result
        OcrResult result = ocrEngine.Recognize(imageInfo);

        // 7️⃣ Output the extracted text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
```

> **المخرجات المتوقعة:** تقوم وحدة التحكم بطباعة الأحرف الصينية الموجودة في `chinese_sample.png`. إذا كانت الصورة واضحة، غالبًا ما تتجاوز الدقة 95 %.

## المشكلات الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| `FileNotFoundException` on startup | مسار مجلد الموارد غير صحيح | تحقق مرة أخرى من المسار في `LocalResourceProvider`. استخدم `Path.Combine` لأمان عبر الأنظمة. |
| Blank output (`ocrResult.Text` empty) | الصورة صاخبة جدًا أو بتنسيق غير مدعوم | حوّل الصورة إلى PNG عالي التباين، أو استخدم `ocrEngine.PreprocessImage(imageInfo)` قبل `Recognize`. |
| Exception: `Unsupported language` | نموذج اللغة لم يتم تحميله | أعد تشغيل خطوة التحميل، أو احذف المجلد التالف ودعه يحمل مرة أخرى. |
| Slow first run | تحميل النموذج عبر اتصال بطيء | خزن النموذج مؤقتًا في موقع شبكة مشترك أو أدمجه مسبقًا مع المثبت الخاص بك. |

## توسيع الحل (الخطوات التالية)

- **Batch processing:** تكرار عبر دليل يحتوي على صور، واستدعاء طريقة `Recognize` نفسها لكل ملف. هذا يتيح لك **extract text from image** للمجموعات دون جهد يدوي.  
- **Post‑processing:** استخدم التعبيرات النمطية لتنظيف آثار OCR (مثلاً، علامات ترقيم عشوائية).  
- **Language detection:** إذا كنت بحاجة إلى معالجة مستندات متعددة اللغات، فافحص `ocrResult.DetectedLanguage` (متاح في إصدارات Aspose الأحدث) وبدّل `ocrEngine.Language` وفقًا لذلك.  

## الخلاصة

لقد استعرضنا كل ما تحتاجه **run OCR on image** للملفات باستخدام Aspose OCR في C#. من اختيار نموذج **recognize simplified Chinese** الصحيح، إلى تحميل الموارد، تكوين المحرك، وأخيرًا **extract text from image**، يوفر الدرس لك حلاً مستقلاً يمكن نسخه ولصقه.  

الآن يمكنك بثقة **recognize Chinese text** في أي صورة PNG أو JPEG تقدمها للمحرك، ولديك أساس قوي للتوسع إلى وظائف الدُفعات، دعم متعدد اللغات، أو التكامل مع خطوط أنابيب التحليل اللاحقة.

هل لديك أسئلة حول تعديل إعدادات OCR أو التعامل مع نصوص أخرى؟ اترك تعليقًا، وتمنياتنا لك بالبرمجة السعيدة! 

![Run OCR on image example](image.png "Run OCR on image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}