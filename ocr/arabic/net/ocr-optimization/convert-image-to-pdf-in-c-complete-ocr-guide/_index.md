---
category: general
date: 2025-12-30
description: تحويل الصورة إلى PDF باستخدام Aspose OCR في C#. تعلم كيفية إعداد الصورة
  مسبقًا للتعرف الضوئي على الأحرف، التعرف على صورة نص كورية، وإنشاء صورة PDF قابلة
  للبحث بسرعة.
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: ar
og_description: تحويل الصورة إلى PDF باستخدام Aspose OCR. يوضح هذا البرنامج التعليمي
  كيفية معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف، والتعرف على صورة نص كورية،
  وإنشاء صورة PDF قابلة للبحث.
og_title: تحويل الصورة إلى PDF في C# – دليل OCR الكامل
tags:
- C#
- OCR
- Aspose
- PDF
title: تحويل الصورة إلى PDF في C# – دليل OCR الكامل
url: /ar/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى PDF في C# – دليل OCR الكامل

هل احتجت يومًا إلى **convert image to PDF** ولكنك أيضًا تريد أن يكون النص داخلها قابلًا للبحث؟ لست وحدك. يواجه العديد من المطورين نفس المشكلة عند التعامل مع الصفحات الممسوحة ضوئيًا، خاصة تلك المكتوبة بالكورية. الخبر السار هو أنه باستخدام Aspose OCR يمكنك **preprocess image for OCR**، **recognize Korean text image**، وأخيرًا **create searchable PDF image** في بضع أسطر فقط.

في هذا الدرس سنستعرض كامل خط الأنابيب — من تحميل صورة JPEG خام لصفحة كتاب كورية، تنظيفها، استخراج النص، وتجميع كل ذلك في PDF قابل للبحث. في النهاية ستحصل على تطبيق console C# جاهز للتشغيل يمكنك إدراجه في أي مشروع .NET.

## ما ستحتاجه

- **.NET 6.0 أو أحدث** (الكود يعمل على .NET Core و .NET Framework على حد سواء)  
- **Aspose.OCR for .NET** حزمة NuGet (`Aspose.OCR`) – مفاتيح التجربة المجانية متوفرة على موقع Aspose.  
- صورة نموذجية تحتوي على نص كوري (مثال: `korean_book_page.jpg`).  
- بيئة تطوير حسب اختيارك (Visual Studio, VS Code, Rider — أنا أستخدم VS 2022).

> **نصيحة احترافية:** احتفظ بملفات الصور في مجلد مخصص مثل `Resources/` حتى يبقى المسار ثابتًا عبر الأجهزة.

## نظرة عامة على العملية

1. **Initialize the OCR engine** مع دعم GPU للسرعة.  
2. **Add preprocessing filters** (deskew, denoise) لتحسين دقة التعرف.  
3. **Download and load the Korean language model** – تقوم Aspose بذلك تلقائيًا إذا لزم الأمر.  
4. **Run the recognition** على الصورة المدخلة.  
5. **Export the result as a searchable PDF** باستخدام المصدّر المدمج.  
6. **Optionally, serialize the result to JSON** للتحليل أو التسجيل الإضافي.

فيما يلي سنفصل كل خطوة، نشرح *لماذا* هي مهمة، ونزودك بالكود الدقيق الذي يمكنك نسخه ولصقه.

## ## تحويل الصورة إلى PDF – سير العمل الكامل

المقتطف التالي هو البرنامج *الكامل*. لا تتردد في إنشاء مشروع console جديد (`dotnet new console -n OcrPdfDemo`) واستبدال ملف `Program.cs` الذي تم إنشاؤه تلقائيًا بهذا الكود.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### لماذا يعمل هذا

- **GPU acceleration** يقلل وقت التعرف إلى النصف تقريبًا مقارنةً بوضعية CPU‑only.  
- **Deskew** و **Denoise** هما تقنيتان كلاسيكيتان لـ *preprocess image for OCR*؛ تصحّحان عيوب المسح الشائعة التي قد تجعل المحرك يفقد الأحرف.  
- **Language model loading** ضروري لـ **recognize Korean text image** – بدون نموذج اللغة الكورية سيعود المحرك إلى أبجدية لاتينية عامة وينتج نفايات.  
- يقوم **SearchablePdfExporter** بدمج الصورة الأصلية وطبقة نص غير مرئية، مما يمنحك نتيجة **create searchable pdf image** يمكنك فهرستها في أي عارض PDF.

## ## تحسين الصورة لـ OCR – نصائح وحيل

بينما الفلتران اللذان أضفناهما عادةً كافيان، قد تواجه صورًا صعبة. إليك بعض الخطوات الإضافية التي يمكنك تجربتها:

| المشكلة | فلتر إضافي | كيفية الإضافة |
|-------|-------------------|------------|
| انخفاض التباين | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| ضوضاء خلفية قوية | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| توجيه مختلط (عمودي وأفقي) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **ملاحظة:** إضافة الكثير من الفلاتر قد يبطئ المعالجة. اختبر كل تعديل على صفحة واحدة قبل التوسع.

## ## التعرف على صورة نص كوري – مشاكل شائعة

تحتوي النصوص الكورية على مقاطع Hangul كثيفة بصريًا. إذا لاحظت مخرجات مشوشة:

1. **Ensure the language model is fully downloaded** – تحقق من وحدة التحكم لرسالة مثل “Downloading Korean model…”.  
2. **Increase the `MaxAngle`** في `DeskewFilter` إذا كانت مسحاتك مائلة بأكثر من 12°.  
3. **Boost GPU memory** عن طريق ضبط `ocrEngine.GpuMemoryLimit = 2048;` (القيمة بالميغابايت).  

هذه التعديلات تؤثر مباشرة على نجاح **recognize Korean text image**.

## ## إنشاء صورة PDF قابلة للبحث – التحقق من النتيجة

بعد انتهاء البرنامج، افتح `korean_page.pdf` في أي قارئ PDF (Adobe Acrobat Reader، Foxit، أو حتى Chrome). يجب أن تكون قادرًا على:

- **Select text** باستخدام الفأرة كما لو كانت PDF أصلية.  
- **Search** عن الكلمات الكورية باستخدام صندوق البحث المدمج.  

إذا ظهرت طبقة النص فارغة، تحقق مرة أخرى من أن طريقة `Export` استلمت مسار الصورة الصحيح وأن نتيجة OCR تحتوي على `RecognitionResult.Text` غير فارغ.

## ## مخرجات JSON الكاملة – ما المتوقع

تطبع وحدة التحكم حمولة JSON منسقة بشكل جميل. مثال مختصر يبدو هكذا:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## ## استكشاف الأخطاء وإجابات الأسئلة المتكررة

**س: PDF الخاص بي كبير مقارنةً بالصورة الأصلية.**  
المصدّر يدمج الصورة الأصلية بدقةها الأصلية. إذا كان الحجم مصدر قلق، قلل أبعاد الصورة *قبل* التعرف:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**س: OCR يُرجع سلاسل فارغة.**  
تحقق من أن مسار الصورة صحيح وأن الملف غير تالف. أيضًا، تأكد من أن برنامج تشغيل GPU محدث؛ قد تتسبب الإصدارات القديمة في فشل صامت.

**س: هل يمكنني معالجة صفحات متعددة في حلقة؟**  
بالطبع. ضع الخطوات 4‑6 داخل حلقة `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` وغيّر مسار PDF الناتج وفقًا لذلك.

## ## الخاتمة

لقد قمنا للتو **converted image to PDF** مع الحفاظ على النص القابل للبحث، كل ذلك بفضل خط أنابيب Aspose OCR القوي. من خلال **preprocess image for OCR**، تعزز الدقة؛ ومن خلال **recognize Korean text image**، تتعامل مع النصوص المعقدة؛ ومن خلال **create searchable pdf image**، تحصل على مستند قابل للنقل والفهرسة.

احصل على الكود، وجهه إلى مسحاتك الخاصة، وجرب فلاتر إضافية أو نماذج لغوية. النمط نفسه يعمل مع الصينية، اليابانية، أو أي لغة تعتمد على اللاتينية — فقط استبدل `LanguageModel.Korean` بالعدد المناسب.

هل لديك المزيد من الأسئلة؟ اترك تعليقًا، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}