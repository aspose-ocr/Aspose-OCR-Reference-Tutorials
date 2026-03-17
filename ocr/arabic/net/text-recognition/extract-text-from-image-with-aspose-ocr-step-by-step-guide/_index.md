---
category: general
date: 2026-03-17
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية تطبيق مرشح
  المتوسط، تحميل الصورة للتعرف الضوئي على الأحرف، إنشاء محرك OCR، وتشغيل التعرف على
  النص بكفاءة.
draft: false
keywords:
- extract text from image
- apply median filter
- load image for ocr
- run ocr recognition
- create ocr engine
language: ar
og_description: استخراج النص من الصورة بسرعة. يوضح هذا الدليل كيفية إنشاء محرك OCR،
  وتطبيق مرشح المتوسط، وتحميل الصورة للـ OCR، وتشغيل التعرف على النص باستخدام C#.
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل C# الكامل
tags:
- OCR
- C#
- Aspose
title: استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة
url: /ar/net/text-recognition/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة

هل احتجت يومًا إلى **extract text from image** لكنك لم تكن متأكدًا من أي مكتبة تثق بها؟ في مشروعي الأخير، احتجت إلى طريقة موثوقة لاستخراج الملاحظات المكتوبة يدويًا من ملفات JPEG الضوضائية، واتضح أن Aspose OCR خيار قوي. في هذا الدرس ستتعرف بالضبط على كيفية **create OCR engine**، **load image for OCR**، **apply median filter**، وأخيرًا **run OCR recognition** للحصول على نص نظيف.

سنستعرض العملية بالكامل — من تثبيت حزمة NuGet إلى طباعة النتيجة في وحدة التحكم — حتى تتمكن من نسخ مثال يعمل ولصقه في مشروعك. لا مراجع غامضة، بل حل كامل ومستقل يمكنك تشغيله اليوم.

> **Quick preview:** في النهاية ستحصل على تطبيق C# console يقرأ `photo_noisy.jpg`، يزيل الانحراف، ينعم الحبوب بفلتر متوسط، ويطبع السلسلة المستخرجة.

---

## ما ستحتاجه

- **.NET 6+** (أو .NET Core 3.1 – الواجهة البرمجية هي نفسها)
- **Aspose.OCR** حزمة NuGet (`Install-Package Aspose.OCR`)
- صورة نموذجية، ويفضل أن تكون مسحًا ضوضائيًا (`photo_noisy.jpg` works great)
- أي بيئة تطوير تفضلها—Visual Studio، Rider، أو VS Code

هذا كل شيء. لا ملفات DLL إضافية، لا خدمات خارجية، ولا ملفات إعداد مخفية. إذا كان لديك مشروع .NET بالفعل، فقط أضف الحزمة وأنت جاهز للانطلاق.

---

## الخطوة 1 – إنشاء محرك OCR (الإعداد الأساسي)

أول شيء يجب عليك القيام به هو **create OCR engine**. فكر في المحرك كالعقل الذي سيُفسّر البكسلات. بدون ذلك، لا شيء آخر يهم.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **Why this matters:** `OcrEngine` يجمع كل الإعدادات الافتراضية، بما في ذلك اكتشاف اللغة ومعالجة الصورة مسبقًا. إن إنشاءه مبكرًا يمنحك قاعدة نظيفة لتخصيصها لاحقًا.

---

## الخطوة 2 – تطبيق فلتر المتوسط (تقليل الضوضاء)

الصور الضوضائية تجعل OCR يتعثر. خطوة **apply median filter** تُنعّم البقع دون تشويش الحواف، وهو مثالي للنص.

```csharp
// Clear any default filters that Aspose may have added
ocrEngine.Config.Filters.Clear();

// Add a deskew filter to correct any rotation
ocrEngine.Config.Filters.Add(new DeskewFilter());

// Add a median filter with a kernel size of 3
ocrEngine.Config.Filters.Add(new MedianFilter(3));
```

> **Pro tip:** حجم النواة `3` يعمل مع معظم الصور الحبيبية. إذا كانت صورتك شديدة الضوضاء، ارتقِ إلى `5`، لكن احذر من فقدان الخطوط الرفيعة.

---

## الخطوة 3 – تحميل الصورة لـ OCR (تغذية المحرك)

الآن نقوم بـ **load image for OCR**. توفر Aspose أداة مساعدة `ImageStream.FromFile` التي تقرأ الملف إلى صيغة يفهمها المحرك.

```csharp
// Point to your image file – adjust the path as needed
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/photo_noisy.jpg");
```

> **Edge case:** إذا كانت صورتك موجودة كموارد مدمجة، استخدم `ImageStream.FromStream(yourStream)` بدلاً من ذلك. المحرك يقبل أي تدفق يمكن فك تشفيره إلى صورة bitmap.

---

## الخطوة 4 – تشغيل التعرف على OCR (استخراج النص)

مع جاهزية المحرك وتحميل الصورة، حان الوقت لـ **run OCR recognition**. هذه الدعوة الواحدة تقوم بكل الأعمال الثقيلة — المعالجة المسبقة، تقسيم الأحرف، ونمذجة اللغة.

```csharp
// Perform the recognition
var ocrResult = ocrEngine.Recognize();

// The Text property holds the extracted string
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.Text);
```

> **What you’ll see:** إذا كانت الصورة تحتوي على “Hello World”، ستطبع وحدة التحكم ذلك بالضبط، مع حذف أي رموز عشوائية أزالها فلتر المتوسط.

---

## الخطوة 5 – مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل، جاهز للترجمة. احفظه كـ `Program.cs` داخل مشروع console، استبدل `YOUR_DIRECTORY` بالمجلد الفعلي، وشغّل `dotnet run`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create OCR engine
            var ocrEngine = new OcrEngine();

            // Step 2: Apply filters – deskew + median
            ocrEngine.Config.Filters.Clear();
            ocrEngine.Config.Filters.Add(new DeskewFilter());
            ocrEngine.Config.Filters.Add(new MedianFilter(3));

            // Step 3: Load the image you want to process
            // Make sure the path points to a valid JPEG/PNG/TIFF file
            ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/photo_noisy.jpg");

            // Step 4: Run OCR recognition
            var ocrResult = ocrEngine.Recognize();

            // Step 5: Output the extracted text
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**الناتج المتوقع (مثال):**

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

إذا كانت الصورة فارغة تمامًا، سيكون `ocrResult.Text` سلسلة فارغة — لا داعي للقلق، بل إشارة للتحقق من مسار الصورة أو إعدادات الفلتر.

---

## أسئلة شائعة ومشكلات محتملة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كانت الصورة مائلة 90°؟* | يقوم `DeskewFilter` تلقائيًا باكتشاف وتصحيح الانحرافات الطفيفة. بالنسبة للزوايا الشديدة، فكر في إضافة فلتر دوران مخصص قبل عملية تصحيح الانحراف. |
| *هل يمكنني تغيير اللغة؟* | نعم — اضبط `ocrEngine.Config.Language = Language.English;` (أو أي لغة مدعومة) قبل استدعاء `Recognize()`. |
| *هل فلتر المتوسط هو الوحيد لتقليل الضوضاء؟* | ليس كذلك. توفر Aspose أيضًا `GaussianFilter` و `BilateralFilter`. اختر بناءً على نوع الضوضاء التي تواجهها. |
| *كيف أتعامل مع ملفات PDF متعددة الصفحات؟* | قم بالتكرار عبر كل صفحة، حوّلها إلى صورة (مثلاً باستخدام Aspose.PDF)، ثم أدخل كل صورة إلى نفس محرك OCR. |
| *ماذا لو احتجت إلى درجة الثقة؟* | `ocrResult.Confidence` يُعيد قيمة عائمة بين 0 و 1 تُظهر مستوى الثقة العام. |

---

## نظرة بصرية عامة

![مخطط تدفق استخراج النص من الصورة](ocr_flow.png "استخراج النص من الصورة")

المخطط أعلاه يوضح سير العمل: **create OCR engine → apply median filter → load image for OCR → run OCR recognition → get text**. إنه مرجع سريع يمكنك تثبيته على مكتبك.

---

## الخاتمة

لقد استعرضنا للتو كيفية **extract text from image** باستخدام Aspose OCR في C#. من خلال **creating OCR engine**، **applying median filter**، **loading image for OCR**، وأخيرًا **running OCR recognition**، لديك الآن حل موثوق يعمل على المسحات الضوضائية، الإيصالات، أو الملاحظات المكتوبة يدويًا.

إذا كنت ترغب في التعمق أكثر، جرّب:
- التبديل إلى `OcrEngine.Config.Language = Language.Spanish;` للمشاريع متعددة اللغات.
- تصدير `ocrResult.Text` إلى ملف JSON للمعالجة اللاحقة.
- دمج مع `Tesseract` للحصول على نهج هجين عندما تواجه Aspose صعوبة مع بعض الخطوط.

لا تتردد في التجربة، تعديل معلمات الفلتر، ومشاركة نتائجك في التعليقات. برمجة سعيدة، ولتكون صورك دائمًا قابلة للقراءة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}