---
category: general
date: 2026-02-28
description: إنشاء ملف PDF قابل للبحث في C# عن طريق دمج الصور عموديًا. تعلم كيفية
  ترتيب الصور عموديًا وتحويل صفحات PDF الممسوحة ضوئيًا باستخدام Aspose OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: ar
og_description: إنشاء ملف PDF قابل للبحث في C# عن طريق دمج الصور عموديًا. يوضح هذا
  الدليل كيفية تجميع الصور عموديًا وتحويل صفحات PDF الممسوحة ضوئيًا باستخدام Aspose
  OCR.
og_title: إنشاء ملف PDF قابل للبحث في C# – دمج الصور عموديًا
tags:
- Aspose OCR
- C#
- PDF generation
title: إنشاء ملف PDF قابل للبحث في C# – دمج الصور عموديًا
url: /ar/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث في C# – دمج الصور عموديًا

هل احتجت يومًا إلى **إنشاء PDF قابل للبحث** من مجموعة من ملفات PNG الممسوحة ضوئيًا لكن لم تعرف من أين تبدأ؟ لست وحدك. في العديد من مشاريع أتمتة المستندات تكون النقطة الأكثر إزعاجًا هي تحويل مجموعة من ملفات الصور إلى PDF واحد مرتب وقابل للبحث يمكنك فهرسته ومشاركته.

في هذا الدرس سنستعرض مثالًا كاملاً جاهزًا للتنفيذ يوضح لك **كيفية رص الصور عموديًا**، **دمج الصور عموديًا**، وأخيرًا **تحويل صفحات PDF الممسوحة ضوئيًا** إلى مستند واحد قابل للبحث باستخدام محرك Aspose.OCR المدعوم بتقنية GPU. في النهاية ستحصل على برنامج مستقل يمكنك إدراجه في أي حل .NET.

> **ما ستتعلمه**
> - تهيئة محرك OCR مع دعم GPU.
> - معالجة دفعة من الصور بشكل متوازي.
> - **دمج الصور عموديًا** لمحاكاة مسح متعدد الصفحات.
> - تصدير PDF قابل للبحث وتقرير JSON مفصل للتحليل اللاحق.

## المتطلبات المسبقة

- .NET 6+ (الكود يُجمّع مع .NET 6 أو .NET 7 أو .NET 8)
- حزمة NuGet الخاصة بـ Aspose.OCR (`Install-Package Aspose.OCR`)
- جهاز يدعم GPU إذا رغبت في الاحتفاظ بإعداد `ProcessingMode.Gpu` (يمكن الاعتماد على CPU كبديل)
- مجلد يحتوي على بعض ملفات PNG/JPEG الممسوحة ضوئيًا (يستخدم المثال `page1.png`، `page2.png`، `page3.png`)

لا توجد خدمات خارجية، ولا ملفات تكوين مخفية—فقط C# نقي.

## الخطوة 1 – إعداد محرك OCR **لإنشاء PDF قابل للبحث**

أولًا نقوم بإنشاء `OcrEngine`، نفعّل تسريع GPU، نحدّد اللغة الإنجليزية، ونضيف بعض مرشحات ما قبل المعالجة. هذه المرشحات تحسّن الدقة عن طريق تصحيح الصفحات المائلة (`DeskewFilter`) وإزالة الضوضاء (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**لماذا هذا مهم:** محرك OCR هو المسؤول عن التعرف على النص. تمكين `ProcessingMode.Gpu` يمكن أن يقلل زمن التعرف إلى النصف على بطاقة رسومية حديثة، بينما تقلل المرشحات من العيوب الشائعة في المسح التي قد تنتج مخرجات مشوشة.

## الخطوة 2 – تكوين معالج دفعي **لتحويل صفحات PDF الممسوحة ضوئيًا** بكفاءة

معالجة كل صفحة على حدة تكون كافية لعدد قليل من الصور، لكن المشاريع الواقعية غالبًا ما تتضمن عشرات أو مئات الصفحات. يتيح لنا `OcrBatchProcessor` من Aspose.OCR تشغيل عمليات التعرف بشكل متوازي، مما يسرّع خطوة **تحويل صفحات PDF الممسوحة ضوئيًا** بشكل كبير.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**نصيحة احترافية:** إذا كنت تستخدم جهازًا لا يحتوي على GPU، عيّن `ProcessingMode = ProcessingMode.Cpu`. سيظل المعالج الدفعي يحترم `MaxDegreeOfParallelism`، لذا يمكنك ضبطه لتجنب التحميل الزائد على الجهاز.

## الخطوة 3 – تشغيل OCR على الدفعة وجمع النتائج

الآن نقوم فعليًا بالتعرف على النص. تُعيد طريقة `Recognize` قائمة من كائنات `OcrResult`، كل منها يحتوي على الصورة الأصلية والنص المستخرج.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

في هذه المرحلة لديك كل ما تحتاجه **لإنشاء PDF قابل للبحث**: الصور (ما زالت في الذاكرة) وطبقات النص المرتبطة بها.

## الخطوة 4 – **دمج الصور عموديًا** وإنشاء PDF القابل للبحث

معظم المستندات الممسوحة ضوئيًا تكون PDFs متعددة الصفحات، لذا نحتاج إلى خياطة صور الصفحات الفردية في صورة واحدة طويلة تحاكي رصًا فعليًا. توفر Aspose.OCR الدالة `Image.CombineVertical` لهذا الغرض بالضبط.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

الملف الناتج (`combined_searchable.pdf`) يحتوي على نص قابل للتحديد والبحث تحت كل صورة صفحة—وهذا بالضبط ما تحتاجه **لإنشاء PDF قابل للبحث** من مصادر ممسوحة ضوئيًا.

![مثال على إنشاء PDF قابل للبحث](/images/create-searchable-pdf.png "مثال على إنشاء PDF قابل للبحث")

*نص بديل للصورة: مثال على إنشاء PDF قابل للبحث يُظهر PDF مدمجًا بنص قابل للبحث.*

**لماذا رص عمودي؟** العديد من مكتبات OCR تتعامل مع كل صورة كصفحة منفصلة. من خلال رصها، نحافظ على ترتيب صفحات PDF بينما نستفيد من تمريرة OCR واحدة للوثيقة بأكملها.

## الخطوة 5 – تصدير JSON مفصل للصفحة الأولى (مفيد لتدفقات العمل اللاحقة)

أحيانًا تحتاج إلى أكثر من PDF؛ ربما تريد إمداد بيانات OCR إلى قاعدة بيانات أو خط أنابيب تعلم آلي. تسمح لك Aspose.OCR بتسلسل كل `OcrResult` إلى JSON، مع الحفاظ على إطارات الحدود، درجات الثقة، والمزيد.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**مقتطف JSON متوقع (مقتطع):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

يمكنك الآن إمداد هذا الـ JSON إلى أي نظام لاحق—سواء كنت تفهرس النص في Elasticsearch أو تُغذيه إلى لوحة تحكم تحليلات مخصصة.

---

## كيف **رص الصور عموديًا** – ملخص سريع

إذا كنت تتساءل **كيف ترص الصور عموديًا** بدون Aspose، يمكنك استخدام `System.Drawing` لإنشاء bitmap جديد ورسم كل صفحة واحدة تلو الأخرى. ومع ذلك، `Image.CombineVertical` المدمج في Aspose يتعامل مع DPI، تنسيق البكسل، وإدارة الذاكرة تلقائيًا، مما يجعله الخيار الأكثر موثوقية للشفرة الإنتاجية.

### بديل: استخدام `System.Drawing` (للتجربة فقط)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

الطريقة اليدوية تعمل، لكنك تفقد سهولة التعامل مع DPI وإمكانية إرجاع النتيجة مباشرة إلى `RecognizeToPdf`. استمر في استخدام `CombineVertical` ما لم تكن لديك متطلبات خاصة جدًا.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | السبب | الحل |
|-------|--------|------|
| **أخطاء نفاد الذاكرة** عند معالجة عشرات المسحات عالية الدقة | كل صورة تبقى في الذاكرة حتى يُكتب الـ PDF | تخلص من كائنات `Image` فور الانتهاء (`using` blocks) أو قلل أبعاد الصور قبل الدمج |
| **نص غير مفهوم** بعد OCR | مسحات مائلة أو منخفضة التباين | احتفظ بـ `DeskewFilter` و `DenoiseFilter`؛ أضف `ContrastFilter` إذا لزم الأمر |
| **غياب طبقة البحث** | استخدمت `Recognize` بدلاً من `RecognizeToPdf` | تأكد من استدعاء `ocrEngine.RecognizeToPdf` على الصورة المدمجة |
| **فشل التحويل إلى GPU** على أجهزة بدون تعريفات مناسبة | `ProcessingMode.Gpu` يرمي استثناءً | احط إنشاء المحرك بكتلة try/catch وارجع إلى `ProcessingMode.Cpu` |

## الخطوات التالية – توسيع سير العمل

الآن بعد أن عرفت كيف **تنشئ PDF قابل للبحث**، قد ترغب في:

- **معالجة دفعات كاملة من المجلدات** باستخدام `Directory.GetFiles` وحلقة `foreach`.
- **إضافة علامات مائية** إلى كل صفحة قبل الدمج (استخدم `ImageProcessor` من Aspose.Imaging).
- **تقسيم PDF القابل للبحث إلى صفحات فردية** إذا احتجت ملفات PDF منفصلة لاحقًا (`PdfDocument.Split` من Aspose.PDF).
- **التكامل مع Azure Blob Storage** لسحب الصور من السحابة ودفع الـ PDF النهائي مرة أخرى.

جميع هذه الامتدادات تعتمد على نفس المفاهيم الأساسية: إعداد OCR، معالجة الصور، وتصدير PDF.

---

## الخلاصة

غطينا كل ما تحتاجه **لإنشاء PDF قابل للبحث** من مجموعة من الصور الممسوحة ضوئيًا في C#. من خلال تهيئة `OcrEngine` المدعوم بـ GPU، تشغيل دفعة متوازية باستخدام `OcrBatchProcessor`، **دمج الصور عموديًا**، وأخيرًا استدعاء `RecognizeToPdf`، ستحصل على مستند مرتب وقابل للبحث جاهز للأرشفة أو الفهرسة. يضيف تصدير JSON إضاءة كاملة على نتائج OCR، ما يفتح أبوابًا للتحليلات أو سير عمل مخصص.

جرّبه، جرب مرشحات مختلفة، وشاهد خط أنابيب أتمتة المستندات يصبح أكثر سلاسة. إذا واجهت أي مشاكل، اترك تعليقًا—برمجة سعيدة!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}