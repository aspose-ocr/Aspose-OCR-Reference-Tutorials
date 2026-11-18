---
category: general
date: 2026-09-13
description: تعلم كيفية تحويل صفحة ممسوحة ضوئياً إلى PDF في C# باستخدام Aspose OCR.
  يوضح هذا الدليل خطوات ما قبل المعالجة، التعرف على النص الكوري، وإنشاء PDF قابل للبحث.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: تعلم كيفية تحويل صفحة ممسوحة ضوئياً إلى PDF في C# باستخدام Aspose
  OCR. يغطي البرنامج التعليمي ما قبل معالجة الصورة، GPU‑accelerated OCR للنص الكوري،
  وإنشاء PDF قابل للبحث خلال دقائق.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: كيفية تحويل صفحة ممسوحة ضوئياً إلى PDF في C# باستخدام OCR
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: كيفية تحويل صفحة ممسوحة ضوئياً إلى PDF في C# باستخدام OCR
url: /ar/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحويل صفحة ممسوحة ضوئياً إلى PDF في C# باستخدام OCR

إذا كنت بحاجة إلى **تحويل صفحة ممسوحة ضوئياً إلى PDF** مع الحفاظ على إمكانية البحث في النص، فأنت في المكان المناسب. يشرح هذا الدليل كيفية استخدام Aspose OCR لـ **preprocess image for OCR**، **recognize Korean text image**، وأخيراً **create searchable PDF image** – كل ذلك من تطبيق كونسول بسيط بلغة C#.

## إجابات سريعة
- **ما المكتبة التي تتعامل مع OCR؟** Aspose.OCR for .NET  
- **هل يمكنني استخدام وحدة معالجة الرسومات GPU؟** نعم – تمكين تسريع GPU للحصول على معالجة أسرع حتى 2×  
- **هل أحتاج إلى حزمة لغة كورية؟** يتم تنزيلها تلقائياً عند الاستخدام الأول  
- **هل سيكون الناتج قابلاً للبحث؟** يحتوي ملف PDF المُولد على طبقة نصية غير مرئية  
- **ما إصدارات .NET المدعومة؟** .NET 6.0 وما بعده (بما في ذلك .NET Core و .NET Framework)

## المتطلبات

- **.NET 6.0 أو أحدث** – يعمل على .NET Core و .NET Framework و .NET 5/6+  
- **Aspose.OCR for .NET** حزمة NuGet (`Aspose.OCR`) – مفاتيح التجربة مجانية على موقع Aspose  
- صورة نموذجية تحتوي على أحرف كورية، مثال: `korean_book_page.jpg`  
- بيئة التطوير المتكاملة المفضلة لديك (Visual Studio 2022، VS Code، Rider، إلخ)

> **نصيحة احترافية:** احفظ الصور في مجلد `Resources/` بحيث تبقى المسارات متسقة عبر الأجهزة.

## نظرة عامة على العملية

1. تهيئة محرك OCR مع دعم GPU.  
2. إضافة مرشحات **preprocess image for OCR** مثل تصحيح الميل (deskew) وإزالة الضوضاء (denoise).  
3. تنزيل وتحميل نموذج اللغة الكورية (يتم التعامل معه تلقائياً).  
4. تشغيل OCR على الصورة.  
5. تصدير النتيجة باستخدام **SearchablePdfExporter** إلى **create searchable PDF image**.  
6. (اختياري) تسلسل مخرجات OCR إلى JSON لاستخدامها في خطوط الأنابيب اللاحقة.

فيما يلي نوسّع كل خطوة، ونشرح *لماذا* هي مهمة، ونزودك بالكود الدقيق الذي يمكنك نسخه‑ولصقه.

## كيف يعمل تحويل الصفحة الممسوحة ضوئياً إلى PDF؟

`OcrEngine` هو الفئة الرئيسية في Aspose.OCR التي تقوم بالتعرف الضوئي على الأحرف في الصور.  
`SearchablePdfExporter` ينشئ ملف PDF يحتوي على الصورة الأصلية وطبقة نصية غير مرئية للبحث.  
`RecognitionResult` يحمل النص وبيانات الثقة التي تُرجعها محرك OCR.

حمّل صورتك باستخدام `new OcrEngine()` واستدعِ `engine.Recognize("korean_book_page.jpg")`، ثم مرّر `RecognitionResult` إلى `SearchablePdfExporter.Export`. هذه العملية ذات الخطوتين تقرأ البت ماب، تستخرج النص Unicode، وتدمج كليهما في ملف PDF واحد حيث تكون طبقة النص غير مرئية لكنها قابلة للبحث. تسريع GPU يقلل وقت التعرف إلى النصف تقريباً، بينما مرشحات deskew و denoise تُحسّن الدقة حتى 15 % في المسحات الضوضائية.

## تحويل الصورة إلى PDF – سير العمل الكامل

المقتطف التالي هو البرنامج *الكامل*. أنشئ مشروع كونسول جديد (`dotnet new console -n OcrPdfDemo`) واستبدل ملف `Program.cs` الذي تم إنشاؤه تلقائياً بالكود المعروض في العنصر النائب.

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

- **GPU acceleration** يقلل وقت التعرف إلى النصف تقريباً مقارنةً بوضعية CPU‑only.  
- **Deskew** و **Denoise** هما تقنيتان كلاسيكيتان لـ *preprocess image for OCR*؛ فهما يصحّحان عيوب المسح الشائعة التي قد تجعل المحرك يفوت الأحرف.  
- **Language model loading** ضروري لـ **recognize Korean text image** – بدون نموذج اللغة الكورية سيعود المحرك إلى أبجدية لاتينية عامة وينتج نتائج غير مفهومة.  
- يقوم **SearchablePdfExporter** بدمج البت ماب الأصلي وطبقة نصية غير مرئية، مما يمنحك نتيجة **create searchable pdf image** يمكنك فهرستها في أي عارض PDF.

## لماذا يعمل هذا

- **GPU acceleration** يقلل وقت التعرف إلى النصف تقريباً مقارنةً بوضعية CPU‑only.  
- **Deskew** و **Denoise** هما تقنيتان كلاسيكيتان لـ *preprocess image for OCR*؛ فهما يصحّحان عيوب المسح الشائعة التي قد تجعل المحرك يفوت الأحرف.  
- **Language model loading** ضروري لـ **recognize Korean text image** – بدون نموذج اللغة الكورية سيعود المحرك إلى أبجدية لاتينية عامة وينتج نتائج غير مفهومة.  
- يقوم **SearchablePdfExporter** بدمج البت ماب الأصلي وطبقة نصية غير مرئية، مما يمنحك نتيجة **create searchable pdf image** يمكنك فهرستها في أي عارض PDF.

## preprocess image for OCR – نصائح وحيل

`DeskewFilter` يصحّح دوران الصفحات الممسوحة ضوئياً.  
`ContrastFilter` يضبط تباين الصورة لتحسين دقة OCR.  
`BinarizationFilter` يحول الصورة إلى أبيض‑أسود بناءً على عتبة، مما يقلل الضوضاء الخلفية.  
`OrientationFilter` يكتشف ويصحّح الصفحات المختلطة بين الوضعية العمودية والأفقية.  

| المشكلة | المرشح الإضافي | كيفية الإضافة |
|-------|-------------------|------------|
| انخفاض التباين | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| ضوضاء خلفية عالية | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| توجيه مختلط (عمودي وأفقي) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **ملاحظة:** إضافة عدد كبير من المرشحات قد يبطئ المعالجة. اختبر كل تعديل على صفحة واحدة قبل التوسع.

## recognize Korean text image – مشاكل شائعة

الخطوط الكورية تحتوي على مقاطع Hangul الكثيفة بصرياً. إذا لاحظت مخرجات مشوشة:

1. **تأكد من أن نموذج اللغة تم تنزيله بالكامل** – تحقق من وحدة التحكم لرسالة مثل “Downloading Korean model…”.  
2. **زيادة قيمة `MaxAngle`** في `DeskewFilter` إذا كانت مسحاتك مائلة بأكثر من 12°.  
3. **زيادة ذاكرة GPU** عن طريق تعيين `ocrEngine.GpuMemoryLimit = 2048;` (القيمة بالميغابايت).  

`LanguageModel.Korean` يحمل بيانات اللغة الكورية لـ OCR، مما يتيح التعرف الدقيق على Hangul.  

هذه التعديلات تؤثر مباشرة على نجاح **recognize Korean text image**.

## create searchable PDF image – التحقق من النتيجة

بعد انتهاء البرنامج، افتح `korean_page.pdf` في أي قارئ PDF (Adobe Acrobat Reader، Foxit، أو حتى Chrome). يجب أن تكون قادرًا على:

- **تحديد النص** باستخدام الفأرة كما لو كان PDF أصلياً.  
- **البحث** عن الكلمات الكورية باستخدام صندوق البحث المدمج.  

إذا ظهرت طبقة النص فارغة، تحقق مرة أخرى من أن طريقة `Export` استلمت مسار الصورة الصحيح وأن نتيجة OCR تحتوي على `RecognitionResult.Text` غير فارغ.

## إخراج JSON كامل – ما المتوقع

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

## استكشاف الأخطاء وإجابات الأسئلة الشائعة

**س: ملف PDF الخاص بي كبير مقارنةً بالصورة الأصلية.**  
ج: يقوم المصدّر بدمج البت ماب الأصلي بدقته الأصلية. إذا كان الحجم مشكلة، قلل أبعاد الصورة *قبل* التعرف:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**س: OCR يُعيد سلاسل فارغة.**  
ج: تحقق من أن مسار الصورة صحيح وأن الملف غير تالف. كما تأكد من أن برنامج تشغيل GPU محدث؛ قد تتسبب الإصدارات القديمة في فشل صامت.

**س: هل يمكنني معالجة صفحات متعددة في حلقة؟**  
ج: بالتأكيد. غلف الخطوات 4‑6 داخل حلقة `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` وغيّر مسار PDF الناتج وفقاً لذلك.

## الخلاصة

لقد قمنا للتو **تحويل الصورة إلى PDF** مع الحفاظ على النص القابل للبحث، كل ذلك بفضل خط أنابيب Aspose OCR القوي. من خلال **preprocess image for OCR**، تُعزز الدقة؛ ومن خلال **recognize Korean text image**، تتعامل مع النصوص المعقدة؛ ومن خلال **create searchable pdf image**، تحصل على مستند قابل للنقل والفهرسة.

احصل على الكود، ووجهه إلى مسحاتك الخاصة، وجرب مرشحات أو نماذج لغة إضافية. النمط نفسه يعمل مع الصينية، اليابانية، أو أي لغة تعتمد على الحروف اللاتينية—فقط استبدل `LanguageModel.Korean` بالعدد المناسب.

هل لديك أسئلة أخرى؟ اترك تعليقاً، وبرمجة سعيدة!

---

**آخر تحديث:** 2026-09-13  
**تم الاختبار مع:** Aspose.OCR 24.11 for .NET  
**المؤلف:** Aspose

## دروس ذات صلة

- [إنشاء PDF قابل للبحث من ملفات ممسوحة باستخدام Aspose Ocr](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [خط أنابيب ما قبل معالجة OCR كيفية التعرف على النص من الصورة](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [التعرف على النص من الصورة باستخدام Aspose Ocr دليل C كامل](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}