---
category: general
date: 2026-05-21
description: يتيح لك Aspose OCR GPU التعرف على النص في الصورة بسرعة. تعلّم كيفية تحميل
  الصورة للتعرف الضوئي على الأحرف، استخراج النص من ملفات TIFF وتعزيز الأداء.
draft: false
keywords:
- aspose ocr gpu
- recognize text image
- ocr tiff image
- load image for ocr
- extract text from tiff
language: ar
og_description: تسرّع تقنية Aspose OCR GPU استخراج النصوص. يوضح هذا الدليل كيفية تحميل
  الصورة للتعرف الضوئي على الأحرف، والتعرف على نص الصورة، واستخراج النص من ملفات TIFF
  بكفاءة.
og_title: Aspose OCR GPU – التعرف على النص من صورة TIFF باستخدام C#
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  headline: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  type: TechArticle
- description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  name: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  steps:
  - name: Enables GPU acceleration (optional, with automatic CPU fallback).
    text: Enables GPU acceleration (optional, with automatic CPU fallback).
  - name: Creates an `OcrEngine` configured for English.
    text: Creates an `OcrEngine` configured for English.
  - name: Loads a large **OCR TIFF image** from disk.
    text: Loads a large **OCR TIFF image** from disk.
  - name: Runs the recognition and prints the result.
    text: Runs the recognition and prints the result.
  type: HowTo
tags:
- aspose
- ocr
- csharp
title: 'Aspose OCR GPU: التعرف على النص في صورة TIFF باستخدام C#'
url: /ar/net/ocr-optimization/aspose-ocr-gpu-recognize-text-image-from-tiff-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU: التعرف على نص صورة من ملف TIFF باستخدام C#

هل تساءلت يومًا كيف **تتعرف على نص صورة** من ملف TIFF ضخم دون أن تُثقل وحدة المعالجة المركزية؟ لست وحدك. في العديد من خطوط معالجة المستندات تكون خطوة OCR هي عنق الزجاجة، خاصةً عندما تتعامل مع جيجابايتات من الصفحات الممسوحة ضوئيًا باستخدام محرك عادي.

الخبر السار؟ **Aspose OCR GPU** يمكنه تسريع العملية، وعينة الشيفرة أدناه توضح بالضبط كيف **تحمّل الصورة للـ OCR**، **استخراج النص من TIFF**، وكيفية الرجوع إلى المعالج المركزي بسلاسة إذا لم يتوفر GPU. هيا نبدأ.

## ما يغطيه هذا الدرس

سنستعرض برنامج C# جاهز للنسخ واللصق يتضمن:

1. تمكين تسريع GPU (اختياري، مع رجوع تلقائي إلى CPU).  
2. إنشاء `OcrEngine` مكوَّن للغة الإنجليزية.  
3. تحميل صورة **OCR TIFF** كبيرة من القرص.  
4. تشغيل عملية التعرف وطباعة النتيجة.  

بنهاية الدرس ستفهم **لماذا** كل خطوة مهمة، وكيفية التعامل مع الحالات الشائعة، وستحصل على مثال قابل للتنفيذ يمكنك تعديله لملفات PDF، TIFF متعددة الصفحات، أو حتى تدفقات الكاميرا في الوقت الفعلي.

> **المتطلبات المسبقة** – .NET 6+ (أو .NET Framework 4.7+)، حزمة NuGet الخاصة بـ Aspose.OCR، وجهاز يدعم GPU إذا رغبت في رؤية تحسين السرعة. لا يلزم أي عتاد خاص؛ سيستخدم البرنامج المعالج المركزي إذا لم يتم اكتشاف GPU.

---

![Aspose OCR GPU processing diagram showing CPU fallback](/images/aspose-ocr-gpu-diagram.png){: .align-center alt="aspose ocr gpu"}

## الخطوة 1: تمكين تسريع GPU (اختياري)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

// Enable GPU if a compatible device is present.
// The call is safe – if no GPU is found Aspose falls back to CPU.
OcrEngine.EnableGpu(true);
```

**لماذا هذا مهم:**  
أنوية GPU تتفوق في التوازي الضخم المطلوب لمعالجة الصور (التنقيط، إزالة الضوضاء) واستنتاج الشبكات العصبية. عبر تفعيل `EnableGpu(true)` تعطي المحرك إشارة للقيام بهذه المهام على الـ GPU. إذا لم يكن الجهاز يحتوي على بطاقة متوافقة مع CUDA، فإن Aspose يتحول صامتًا إلى CPU، وبالتالي لا يحدث تعطل مفاجئ.

**نصيحة احترافية:** على نظام Windows قد تحتاج إلى أحدث برنامج تشغيل NVIDIA وأدوات CUDA مثبتة. على Linux، تأكد من أن `nvidia‑driver` و `libcuda.so` موجودان في مسار المكتبة الخاص بك.

## الخطوة 2: إنشاء وتكوين محرك OCR

```csharp
// Step 2: Instantiate the OCR engine and set the language.
var ocrEngine = new OcrEngine
{
    // English works for most scanned docs; you can pick other languages here.
    Language = OcrLanguage.English
};
```

**لماذا هذا مهم:**  
`OcrEngine` هو قلب **Aspose OCR GPU**. ضبط `Language` يخبر النموذج العصبي الأساسي بمجموعة الأحرف المتوقعة، مما يحسن الدقة بشكل كبير. يمكنك أيضًا تعديل `Resolution`، `PreprocessOptions` أو `RecognitionMode` للوثائق الصعبة.

## الخطوة 3: تحميل الصورة للـ OCR

```csharp
// Step 3: Load a large TIFF image from disk.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/large_doc.tif");
```

**لماذا هذا مهم:**  
ملف TIFF قد يحتوي على عدة صفحات، دقة عالية، وضغط غير فقدان—مناسب للنسخ الأرشيفية لكنه ثقيل على الذاكرة. `ImageStream.FromFile` يقرأ الملف كتيار، متجنبًا تحميله بالكامل في الذاكرة للصور الضخمة.

**حالة خاصة:** إذا احتجت لمعالجة TIFF متعدد الصفحات، استدعِ `ocrEngine.Image = ImageStream.FromFile(path, pageIndex);` داخل حلقة، مع زيادة `pageIndex` حتى تُعيد `ocrEngine.Image.IsNull` القيمة `true`.

## الخطوة 4: تنفيذ عملية التعرف

```csharp
// Step 4: Run the OCR process.
ocrEngine.Recognize();
```

**لماذا هذا مهم:**  
`Recognize()` يقوم بكل الأعمال الشاقة: التحضير المسبق، تحليل التخطيط، تجزئة الأحرف، وأخيرًا استنتاج الشبكة العصبية. عندما يكون الـ GPU نشطًا، تُجرى خطوة الاستنتاج على الـ GPU، مما يقلل وقت المعالجة بنسبة 50‑80 % للـ TIFF الكبيرة.

## الخطوة 5: إخراج النتائج

```csharp
// Step 5: Show how many characters were extracted and how long it took.
Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");

// Optional: print the extracted text (be careful with huge strings!)
Console.WriteLine("--- Extracted Text Start ---");
Console.WriteLine(ocrEngine.Text);
Console.WriteLine("--- Extracted Text End ---");
```

**لماذا هذا مهم:**  
`ocrEngine.Text` يحتوي على السلسلة النصية المتصلة بالكامل المستخرجة من الصورة، بينما `ProcessingTime` يمنحك معيارًا سريعًا لمقارنة تشغيل CPU مقابل GPU. إخراج الكونسول مفيد للتصحيح السريع؛ في بيئة الإنتاج قد تكتب النص إلى قاعدة بيانات أو ملف.

**الناتج المتوقع (مثال لفاتورة من صفحتين):**

```
Recognized 1342 characters in 842 ms
--- Extracted Text Start ---
Invoice #12345
Date: 2026‑04‑30
...
Total: $1,234.56
--- Extracted Text End ---
```

إذا لم يتوفر GPU، قد يرتفع الوقت إلى ~1800 ms على نفس الجهاز، مما يوضح فائدة **aspose ocr gpu**.

---

## التعامل مع المشكلات الشائعة

| الحالة | ما يجب مراقبته | كيفية الإصلاح |
|-----------|-------------------|------------|
| **عدم اكتشاف GPU** | `EnableGpu(true)` يتحول صامتًا إلى CPU، لكن قد تظن أنه لا يزال يستخدم GPU. | تحقق من `OcrEngine.IsGpuEnabled` بعد الاستدعاء؛ سجِّل النتيجة. |
| **نفاد الذاكرة على TIFF ضخم** | تحميل صورة بدقة 10 000 × 10 000 بكسل قد يتجاوز سعة RAM. | استخدم `ImageStream.FromFile(path, pageIndex, maxResolution: 300)` لتقليل الدقة عند التحميل. |
| **لغة غير صحيحة** | نموذج الإنجليزية على مستند فرنسي ينتج نصًا مشوَّهًا. | اضبط `Language = OcrLanguage.French` أو فعّل وضع متعدد اللغات. |
| **TIFF متعدد الصفحات** | يتم معالجة الصفحة الأولى فقط. | كرر الصفحات باستخدام `ImageStream.FromFile(path, pageNumber)`. |

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك وضعه في تطبيق Console. يتضمن معالجة الأخطاء، تسجيل حالة GPU، ومؤقت بسيط للقيام بالاختبارات الخاصة بك.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Enable GPU acceleration (if available)
            OcrEngine.EnableGpu(true);
            Console.WriteLine($"GPU enabled: {OcrEngine.IsGpuEnabled}");

            // 2️⃣ Create the OCR engine and set language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 3️⃣ Load the TIFF image (replace with your actual path)
            string imagePath = @"YOUR_DIRECTORY\large_doc.tif";
            try
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to load image: {ex.Message}");
                return;
            }

            // 4️⃣ Perform recognition
            try
            {
                ocrEngine.Recognize();
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Recognition error: {ex.Message}");
                return;
            }

            // 5️⃣ Output results
            Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");
            Console.WriteLine("--- Extracted Text Start ---");
            Console.WriteLine(ocrEngine.Text);
            Console.WriteLine("--- Extracted Text End ---");
        }
    }
}
```

انسخ، الصق، اضغط **F5**، وشاهد الكونسول يعرض عدد الأحرف والنص المستخرج. استبدل `OcrLanguage.English` بأي لغة أخرى يدعمها Aspose إذا أردت **التعرف على نص صورة** بالإسبانية أو الألمانية، إلخ.

---

## ملخص وخطوات مستقبلية

لقد استعرضنا كيفية **aspose ocr gpu** لت **التعرف على نص صورة** من **صورة OCR TIFF**، وكيفية **تحميل الصورة للـ OCR**، واستخراج النص من TIFF بكفاءة. الأفكار الأساسية—تمكين GPU، ضبط اللغة، تدفق TIFF، وقراءة النتيجة—قابلة للنقل إلى صيغ ملفات أخرى مثل JPEG أو PNG.

### ما يمكنك تجربته لاحقًا

- **معالجة دفعات**: تكرار عبر مجلد من ملفات TIFF، وكتابة كل `ocrEngine.Text` إلى ملف `.txt`.  
- **معالجة متعددة الصفحات**: استخدم `ImageStream.FromFile(path, pageIndex)` داخل حلقة `while` لمعالجة كل صفحة من مستند متعدد الصفحات.  
- **معالجة مسبقة مخصصة**: عدل `ocrEngine.PreprocessOptions` (مثل `Denoise`، `Deskew`) للصور ذات الضوضاء العالية.  
- **قياس أداء GPU**: سجِّل `ProcessingTime` مع وبدون `EnableGpu(true)` على نفس الجهاز لتحديد مقدار التسريع.

لا تتردد في التجربة—تسريع GPU يبرز أكثر مع TIFF عالية الدقة ومتعددة الصفحات، لكن حتى بطاقة 1080 Ti بسيطة ستقلل وقت التعرف بشكل ملحوظ.

هل لديك أسئلة حول نوع مستند معين أو تحتاج مساعدة في دمج النتيجة مع قاعدة بيانات؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

## دروس ذات صلة

- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}