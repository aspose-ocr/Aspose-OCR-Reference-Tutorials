---
category: general
date: 2026-02-14
description: كيفية تنفيذ OCR في C# باستخدام Aspose.OCR – تعلم استخراج النص من الصورة،
  تحميل الصورة من ملف وتشغيل OCR على الصورة بسرعة.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image from file
- recognize text from jpg
- run OCR on image
language: ar
og_description: كيفية تنفيذ OCR في C# باستخدام Aspose.OCR. يوضح لك هذا الدليل كيفية
  استخراج النص من الصورة، تحميل الصورة من ملف، وتشغيل OCR على الصورة بكفاءة.
og_title: كيفية تنفيذ OCR في C# – دليل برمجة شامل
tags:
- OCR
- C#
- Aspose
- Image Processing
title: كيفية تنفيذ OCR في C# – دليل خطوة بخطوة
url: /ar/net/text-recognition/how-to-perform-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في C# – دليل برمجة كامل

هل تساءلت يومًا **كيفية تنفيذ OCR** على صورة التقطتها للتو بهاتفك؟ ربما تحتاج إلى استخراج نص علامة الشارع من ملف JPEG لتطبيق الملاحة، أو لديك مجموعة من العقود الممسوحة وتريد تحويلها إلى نص قابل للبحث. باختصار، تريد *استخراج النص من الصورة* دون إرسال أي شيء إلى السحابة.

الخبر السار هو أنه يمكنك القيام بكل ذلك محليًا باستخدام Aspose.OCR لـ .NET. في هذا الدليل سنستعرض تحميل صورة من ملف، التعرف على النص من JPG، وأخيرًا **تشغيل OCR على الصورة** بالكامل دون اتصال. في النهاية ستحصل على مقطع جاهز للتنفيذ يطبع النص العربي المستخرج إلى وحدة التحكم.

> **ما ستحصل عليه:** برنامج C# مستقل قابل للتنفيذ، شروحات لأهمية كل سطر، ونصائح للتعامل مع الحالات الشائعة مثل الموارد المفقودة أو اللغات غير المدعومة.

## المتطلبات المسبقة

| المتطلب | السبب |
|-------------|--------|
| .NET 6.0 أو أحدث (أو .NET Framework 4.7+) | Aspose.OCR تستهدف .NET Standard 2.0، لذا أي بيئة تشغيل حديثة تعمل. |
| Visual Studio 2022 (أو VS Code مع امتداد C#) | IDE يجعل من السهل إدارة حزم NuGet وتشغيل تطبيق وحدة التحكم. |
| حزمة Aspose.OCR NuGet (`Aspose.OCR`) | هذه هي المكتبة التي تقوم فعليًا بأداء عمل OCR. |
| مجلد يحتوي على موارد OCR غير المتصلة (تحميل من Aspose) | الموارد غير المتصلة تتجنب أي طلبات HTTP أثناء التعرف. |
| ملف صورة (مثال: `arabic_sign.jpg`) | سنستخدم ملف JPEG يحتوي على نص عربي، لكن أي لغة تعمل. |

إذا كنت تفتقد أيًا من هذه، احصل عليها الآن—لا فائدة من بدء الدليل فقط لتواجه نقصًا في الاعتماديات في منتصف الطريق.

## الخطوة 1: تثبيت Aspose.OCR وتحضير الموارد

أولاً، أضف حزمة Aspose.OCR إلى مشروعك:

```bash
dotnet add package Aspose.OCR
```

بعد تثبيت الحزمة، قم بتحميل **حزمة موارد OCR غير المتصلة** من موقع Aspose. استخرجها إلى مجلد على جهازك، على سبيل المثال:

```
C:\OCRResources\
```

> **لماذا هذا مهم:** تحميل الموارد مرة واحدة عند بدء التشغيل يزيل تأخير الشبكة ويحافظ على توافق الحل مع GDPR لأن لا شيء يغادر الجهاز.

## الخطوة 2: إنشاء محرك OCR وتوجيهه إلى مجلد الموارد

الآن سنقوم بإنشاء كائن من الفئة `Engine` ونخبره بمكان وجود الموارد. هذا هو جوهر **كيفية تنفيذ OCR** محليًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Step 2: Initialize the OCR engine with the offline resource folder
Engine ocrEngine = new Engine
{
    // Replace with the path you used in the previous step
    ResourceFolder = @"C:\OCRResources"
};

// Load the resources into memory – this prevents any hidden HTTP calls
ocrEngine.LoadResources();
```

> **نصيحة احترافية:** ضع استدعاء `LoadResources` داخل كتلة try‑catch إذا كنت تتوقع أن مسار المجلد قد يكون خاطئًا. سيخبرك الاستثناء بالملف المفقود بالضبط.

## الخطوة 3: تحميل الصورة من ملف

بعد ذلك، نحتاج إلى **تحميل الصورة من ملف** حتى يتمكن المحرك من تحليلها. Aspose.OCR يعمل مع غلاف `ImageStream` الخاص به.

```csharp
// Step 3: Load the JPEG you want to recognize
ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");
```

إذا كانت صورتك موجودة في مكان آخر، فقط غيّر المسار. فئة `ImageStream` تُجرد التعامل مع البت ماب الأساسي، لذا لا تحتاج للقلق بشأن توافق GDI+.

## الخطوة 4: التعرف على النص من JPG باستخدام إعدادات اللغة

الآن يأتي جوهر **كيفية تنفيذ OCR**—التعرف الفعلي على الأحرف. سنطلب التعرف على العربية، لكن يمكنك استبدال `Language.Arabic` بأي لغة مدعومة أخرى.

```csharp
// Step 4: Run OCR specifying the desired language (Arabic in this example)
OcrResult ocrResult = ocrEngine.Recognize(
    image,
    new OcrOptions { Language = Language.Arabic }
);
```

> **لماذا تحديد لغة؟** يستخدم محرك OCR قواميس ونماذج أحرف مخصصة لكل لغة. توفير اللغة الصحيحة يحسن الدقة بشكل كبير، خاصةً للخطوط ذات الأشكال المعقدة مثل العربية.

## الخطوة 5: عرض النص المستخرج

أخيرًا، دعنا **نستخرج النص من الصورة** ونطبعه. هذه أبسط طريقة للتحقق من نجاح OCR.

```csharp
// Step 5: Output the recognized text to the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrResult.Text);
```

عند تشغيل البرنامج، يجب أن ترى العبارة العربية الموجودة على العلامة مطبوعة في وحدة التحكم. إذا كان الإخراج مشوشًا، تحقق مرة أخرى من اختيار اللغة الصحيحة وأن مجلد الموارد يحتوي على ملفات البيانات العربية.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للترجمة يجمع جميع الخطوات معًا. انسخه والصقه في مشروع وحدة تحكم جديد (`dotnet new console`) واضغط **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Configure the OCR engine with offline resources
            // -------------------------------------------------
            Engine ocrEngine = new Engine
            {
                ResourceFolder = @"C:\OCRResources" // <-- change to your folder
            };
            ocrEngine.LoadResources(); // Loads language packs, fonts, etc.

            // -------------------------------------------------
            // Step 2: Load the image you want to process
            // -------------------------------------------------
            ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");

            // -------------------------------------------------
            // Step 3: Recognize text – specify language to improve accuracy
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(
                image,
                new OcrOptions { Language = Language.Arabic } // Change as needed
            );

            // -------------------------------------------------
            // Step 4: Output the result
            // -------------------------------------------------
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**الناتج المتوقع (مثال):**

```
=== OCR Result ===
مطار القاهره الدولي
```

إذا استبدلت الصورة بعلامة إنجليزية وضبطت `Language.English`، سيطبع نفس الكود النص الإنجليزي. هذا يوضح مدى مرونة **تشغيل OCR على الصورة**.

## استخراج النص من الصورة – التعامل مع السيناريوهات الشائعة

### 1. صفحات متعددة أو صور متعددة الإطارات

بعض صيغ الصور (مثل TIFF) يمكن أن تحتوي على عدة صفحات. لـ **استخراج النص من الصورة** في مثل هذه الحالات، قم بالتكرار عبر كل إطار:

```csharp
for (int i = 0; i < image.FramesCount; i++)
{
    image.CurrentFrame = i;
    OcrResult pageResult = ocrEngine.Recognize(image, new OcrOptions { Language = Language.English });
    Console.WriteLine($"Page {i + 1}: {pageResult.Text}");
}
```

### 2. صور منخفضة الدقة

دقة OCR تنخفض بشكل كبير تحت 70 dpi. إذا واجهت نتائج غير واضحة، فكر في تكبير الصورة أولاً:

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;

// Load as Bitmap, resize, then wrap back into ImageStream
Bitmap bmp = new Bitmap(@"C:\OCRResources\lowres.jpg");
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
ImageStream highResStream = ImageStream.FromBitmap(highRes);
```

### 3. حزمة اللغة مفقودة

إذا حصلت على استثناء مثل *“Language data not found”*، تحقق مرة أخرى من وجود ملفات `.dat` المقابلة في `ResourceFolder`. Aspose توفر ملف zip منفصل لكل لغة.

## تشغيل OCR على الصورة – نصائح الأداء

- **تخزين المحرك في الذاكرة المؤقتة:** إنشاء `Engine` جديد لكل صورة يضيف عبءً. احتفظ بنسخة واحدة حية لمعالجة الدفعات.
- **التنفيذ المتوازي بأمان:** `Engine` آمن للقراءة المتعددة بعد `LoadResources`. يمكنك تشغيل مهام متعددة كل منها يستدعي `Recognize` على صور مختلفة.
- **إلغاء التخصيص عند الانتهاء:** رغم أن `Engine` يطبق `IDisposable`، فإن جامع القمامة في .NET سيقوم بالتنظيف في النهاية. استدعاء `ocrEngine.Dispose()` صراحةً داخل كتلة `using` عادة جيدة.

```csharp
using (Engine ocrEngine = new Engine { ResourceFolder = @"C:\OCRResources" })
{
    ocrEngine.LoadResources();
    // run recognitions here
}
```

## التعرف على النص من JPG – الحالات الحدية التي يجب مراقبتها

| الحالة | ما الذي يجب التحقق منه | الإصلاح |
|-----------|---------------|-----|
| **JPEG تالف** | `ImageStream.FromFile` يرمي استثناء `FileNotFoundException` أو `ArgumentException`. | تحقق من سلامة الملف، ربما أعد حفظ الصورة باستخدام محرر رسومات. |
| **لغة غير مدعومة** | `Language` enum لا يحتوي على اللغة المستهدفة. | حدّث Aspose.OCR إلى أحدث نسخة؛ يتم إضافة لغات جديدة بانتظام. |
| **صور متعددة النصوص** (مثال: إنجليزي + عربي) | قد يتجاهل خيار اللغة الواحد النص الثانوي. | قم بتشغيل OCR مرتين بخيارات لغات مختلفة ودمج النتائج. |

## الملخص – الآن تعرف كيفية تنفيذ OCR في C#

في هذا الدليل غطينا **كيفية تنفيذ OCR** باستخدام Aspose.OCR، من تثبيت حزمة NuGet إلى طباعة النص المستخرج. تعلمت **تحميل الصورة من ملف**، **استخراج النص من الصورة**، **التعرف على النص من jpg**، وتشغيل **OCR على الصورة** بأمان بطريقة جاهزة للإنتاج.

### ما التالي؟

- **جرب صيغ ملفات أخرى** مثل PNG أو BMP—فقط غيّر امتداد الملف.
- **دمج مع قاعدة بيانات** لتخزين نتائج OCR لأرشيفات قابلة للبحث.
- **دمج مع رؤية الحاسوب** (مثال: اكتشاف مناطق النص قبل OCR) للحصول على تحسينات في السرعة.

لا تتردد في تعديل إعدادات اللغة، معالجة المجلدات دفعةً، أو ربط الناتج بواجهة برمجة تطبيقات ويب. OCR هو عنصر أساسي؛ القوة الحقيقية تظهر عندما تدمجه في سير عمل أكبر.

برمجة سعيدة، ولتكون صورك دائمًا واضحة كالكريستال!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}