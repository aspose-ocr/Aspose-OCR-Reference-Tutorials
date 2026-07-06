---
category: general
date: 2026-02-17
description: تعلم كيفية إجراء التعرف الضوئي على الأحرف (OCR) على الصورة واستخراج النص
  من الصورة باستخدام Aspose OCR في C#. يتضمن تحميل ملف الصورة، تحويل الصورة إلى نص،
  وإعداد لغة OCR.
draft: false
keywords:
- perform OCR on image
- extract text from image
- convert image to text
- load image file c#
- setup OCR language
language: ar
og_description: إجراء التعرف الضوئي على الأحرف (OCR) على صورة في C# واستخراج النص
  من الصورة باستخدام Aspose OCR. دليل خطوة بخطوة يغطي تحميل ملف الصورة، إعداد لغة
  OCR، وتحويل الصورة إلى نص.
og_title: تنفيذ التعرف الضوئي على الأحرف (OCR) على صورة في C# – دليل Aspose OCR الكامل
tags:
- C#
- OCR
- Aspose
- Image Processing
title: إجراء OCR على صورة في C# – دليل Aspose OCR الكامل
url: /ar/net/text-recognition/perform-ocr-on-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء التعرف الضوئي على الحروف (OCR) على صورة في C# – دليل Aspose OCR الكامل

هل احتجت يومًا إلى **perform OCR on image** للملفات لكنك لم تكن متأكدًا أي مكتبة تختار لمشروع C#؟ لست وحدك. في العديد من التطبيقات الواقعية—مثل ماسحات الفواتير، قراء اللوحات متعددة اللغات، أو رقمنة الأرشيف—إن القدرة على **extract text from image** بسرعة تُغيّر قواعد اللعبة.  

في هذا الدرس سنستعرض مثالًا عمليًا يوضح بالضبط كيفية **perform OCR on image** باستخدام مكتبة Aspose OCR، وكيفية **load image file C#**، والخطوات اللازمة لـ **setup OCR language** للنص التاميل. في النهاية ستتمكن من **convert image to text** في بضع أسطر من الكود.

## ما ستتعلمه

- كيفية تثبيت وإضافة مرجع Aspose OCR في مشروع .NET.  
- الكود الدقيق اللازم لـ **load image file C#** وإدخاله إلى محرك OCR.  
- كيفية **setup OCR language** (التاميل في هذه الحالة) حتى يعرف المحرك الأحرف المتوقعة.  
- كيفية **extract text from image** وعرضه، مما يمنحك سلسلة جاهزة للاستخدام لمعالجة لاحقة.  

> **Prerequisite:** .NET 6.0 أو أحدث، Visual Studio (أو أي بيئة تطوير C#)، وحزمة Aspose OCR عبر NuGet. لا يلزم وجود خبرة سابقة في OCR.

![perform OCR on image example](https://example.com/placeholder-image.png "perform OCR on image example")

## الخطوة 1: تثبيت حزمة Aspose OCR عبر NuGet

قبل أن تتمكن من **perform OCR on image**، تحتاج إلى مكتبة Aspose OCR في مشروعك. افتح مدير حزم NuGet وشغّل:

```bash
dotnet add package Aspose.OCR
```

*نصيحة احترافية:* إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → **Manage NuGet Packages** → ابحث عن **Aspose.OCR** وانقر **Install**. سيقوم ذلك بجلب جميع الاعتمادات المطلوبة، لذا لن تحتاج إلى البحث عن ملفات DLL إضافية.

## الخطوة 2: إنشاء كائن محرك OCR

القطعة الأولى من الكود تنشئ كائن `OcrEngine`، وهو المكوّن الأساسي الذي سيقوم بـ **convert image to text**. فكر فيه كالعقل الذي يفسّر أنماط البكسل.

```csharp
using System;
using Aspose.OCR;

class TamilOcrDemo
{
    static void Main()
    {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

لماذا ننشئ المحرك هنا؟ لأنه يحتفظ بإعدادات التكوين—مثل اللغة—ويدير الموارد الداخلية. إعادة استخدام نفس المثيل عبر عدة صور يمكن أن يحسن الأداء أيضًا.

## الخطوة 3: **Setup OCR Language** للغة التاميل

يدعم Aspose OCR عشرات اللغات، لكن عليك إبلاغه أي لغة يبحث عنها. هذه هي خطوة **setup OCR language** التي تعزز الدقة بشكل كبير للخطوط غير اللاتينية.

```csharp
        // Step 3: Configure the engine to recognize Tamil text
        ocrEngine.Settings.Language = Language.Tamil;
```

إذا احتجت يومًا إلى التبديل إلى لغة أخرى (مثل الهندية أو الإنجليزية)، ما عليك سوى استبدال `Language.Tamil` بالقيمة المناسبة من الـ enum. المكتبة تستخدم الإنجليزية كإعداد افتراضي، لذا لا تحتاج إلى تكوين صريح إلا للغات الأخرى.

## الخطوة 4: **Load Image File C#** – توفير الصورة للمحرك

الآن نقوم فعليًا بـ **load image file C#**. طريقة `ImageStream.FromFile` تقرأ الملف من القرص وتجهزه لـ OCR.

```csharp
        // Step 4: Load the image containing Tamil characters
        string imagePath = @"YOUR_DIRECTORY/tamil_sign.jpg";
        ImageStream image = ImageStream.FromFile(imagePath);
```

> **Note:** استخدم مسارًا مطلقًا أو تأكد من نسخ الصورة إلى دليل الإخراج (`Copy to Output Directory → Copy always`). إذا لم يتم العثور على الملف، سيطرح المحرك استثناء `FileNotFoundException`.

## الخطوة 5: إجراء OCR و **Extract Text from Image**

مع تكوين المحرك وتحميل الصورة، الاستدعاء النهائي يقوم فعليًا بـ **perform OCR on image** ويعيد كائن `OcrResult` يحتوي على النص المُعترف به.

```csharp
        // Step 5: Perform OCR on the image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 6: Output the recognized text to the console
        Console.WriteLine("Recognized Tamil text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

طريقة `Recognize` تقوم بكل الأعمال الشاقة: المعالجة المسبقة، التجزئة، تصنيف الأحرف، والمعالجة اللاحقة. السلسلة الناتجة يمكن تخزينها، إرسالها إلى قاعدة بيانات، أو استخدامها في أي منطق لاحق.

### النتيجة المتوقعة

إذا كان ملف `tamil_sign.jpg` يحتوي على الكلمة “தமிழ்”، يجب أن ترى شيئًا مشابهًا لـ:

```
Recognized Tamil text:
தமிழ்
```

إذا كانت الصورة غير واضحة أو الإضاءة سيئة، قد تحصل على أحرف مشوشة—لذا اختبر دائمًا باستخدام صور مصدر عالية الجودة.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد. يتضمن جميع الخطوات السابقة في كتلة واحدة متكاملة.

```csharp
using System;
using Aspose.OCR;

class TamilOcrDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Setup OCR language – Tamil in this case
        ocrEngine.Settings.Language = Language.Tamil;

        // Step 3: Load the image containing Tamil characters
        string imagePath = @"YOUR_DIRECTORY/tamil_sign.jpg";
        ImageStream image = ImageStream.FromFile(imagePath);

        // Step 4: Perform OCR on the image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Extract text from image and display it
        Console.WriteLine("Recognized Tamil text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

شغّل البرنامج (`dotnet run` أو اضغط **F5** في Visual Studio) وسترى وحدة التحكم تطبع النص التاميل المستخرج. هذه هي سير عمل **convert image to text** بالكامل في أقل من 30 سطرًا من الكود.

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت لمعالجة صور متعددة؟

أنشئ مثيلًا واحدًا من `OcrEngine`، ثم قم بالتكرار عبر قائمة مسارات الملفات، مستدعيًا `Recognize` في كل مرة. إعادة استخدام المحرك يقلل من استهلاك الذاكرة.

```csharp
foreach (var path in imagePaths)
{
    var img = ImageStream.FromFile(path);
    var result = ocrEngine.Recognize(img);
    Console.WriteLine($"{path}: {result.Text}");
}
```

### كيف أحسن الدقة للصور الضوضائية؟

- استخدم خيارات `ocrEngine.Settings.ImagePreprocessing` (مثل `AutoRotate`، `Deskew`).  
- زد DPI عند التقاط الصورة (300 dpi أو أعلى هو الأفضل).  
- حوّل الصورة إلى تدرجات الرمادي قبل إرسالها إلى المحرك.

### هل يمكنني **convert image to text** بلغات أخرى دون تعديل الكود؟

نعم. ما عليك سوى استبدال قيمة الـ enum للغة:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.Hindi, etc.
```

بقية سير العمل تبقى كما هي.

## الخاتمة

لقد عرضنا للتو كيفية **perform OCR on image** باستخدام Aspose OCR في C#. باتباع الخطوات—تثبيت حزمة NuGet، **setup OCR language**، **load image file C#**، وأخيرًا **extract text from image**—أصبح لديك الآن طريقة موثوقة وجاهزة للإنتاج لـ **convert image to text**.  

من هنا قد ترغب في استكشاف المعالجة الدفعية، دمج ناتج OCR مع واجهة برمجة تطبيقات للترجمة، أو تخزين النتائج في قاعدة بيانات قابلة للبحث. مهما كانت خطوتك التالية، يبقى النمط الأساسي هو نفسه: تهيئة المحرك، ضبط اللغة، إمداده بصورة، وقراءة النص.  

هل لديك المزيد من الأسئلة حول OCR، الدعم متعدد اللغات، أو تحسين الأداء؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}