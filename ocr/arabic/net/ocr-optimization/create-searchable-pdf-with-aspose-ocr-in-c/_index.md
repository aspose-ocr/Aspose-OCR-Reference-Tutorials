---
category: general
date: 2026-04-01
description: إنشاء ملف PDF قابل للبحث في C# باستخدام Aspose OCR – تعلم كيفية تحويل
  PDF الممسوح ضوئياً، إضافة OCR إلى PDF، وتفعيل تسريع GPU للحصول على نتائج سريعة.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- convert pdf to searchable
- add OCR to pdf
- enable GPU acceleration
language: ar
og_description: إنشاء PDF قابل للبحث في C# بسرعة — تحويل PDF الممسوح ضوئياً، إضافة
  OCR إلى PDF، وتمكين تسريع GPU لمعالجة عالية الأداء.
og_title: إنشاء ملف PDF قابل للبحث باستخدام Aspose OCR في C#
tags:
- Aspose OCR
- C#
- PDF processing
title: إنشاء PDF قابل للبحث باستخدام Aspose OCR في C#
url: /ar/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث باستخدام Aspose OCR في C#

هل احتجت يومًا إلى **إنشاء ملفات PDF قابلة للبحث** من مجموعة من المستندات الممسوحة ضوئيًا؟ لست وحدك—فالكثير من الفرق تواجه صعوبة في تحويل ملفات PDF التي تحتوي على صور فقط إلى موارد يمكن البحث فيها نصيًا. الخبر السار؟ باستخدام Aspose OCR يمكنك **تحويل PDF الممسوح** إلى نسخة قابلة للبحث بالكامل في بضع أسطر من كود C#. في هذا الدليل سنستعرض العملية بالكامل، من إضافة OCR إلى PDF إلى تمكين **تسريع GPU** اختياريًا للحصول على زيادة في السرعة.

سنوضح لك أيضًا كيفية **تحويل PDF إلى صيغة قابلة للبحث**، ونناقش لماذا قد ترغب في **إضافة OCR إلى PDF**، ونقدم لك نصائح عملية للتعامل مع دفعات كبيرة. في النهاية ستحصل على تطبيق كونسول جاهز للتنفيذ ينتج PDF قابلًا للبحث يمكنك إدراجه في أي نظام إدارة مستندات.

---

## ما الذي ستحتاجه

قبل أن نبدأ، تأكد من توفر ما يلي:

- **.NET 6.0** أو أحدث (تعمل الواجهة البرمجية أيضًا مع .NET Framework، لكن .NET 6+ هو الخيار المثالي).
- حزمة NuGet **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`).
- ملف PDF ممسوح ضوئيًا (صورة‑فقط) لاستخدامه كمدخل.
- اختياريًا: جهاز متوافق مع GPU مع تثبيت CUDA® إذا رغبت في **تمكين تسريع GPU**.

هذا كل ما تحتاجه—بدون محركات OCR ثقيلة، بدون خدمات خارجية. كل شيء يعمل محليًا.

---

## نظرة عامة خطوة‑بخطوة لإنشاء PDF قابل للبحث

فيما يلي التدفق عالي المستوى الذي سنتبعه:

1. **تهيئة محرك OCR** – أخبر Aspose اللغة التي يجب البحث عنها وما إذا كان سيستخدم GPU.
2. **توجيه المحرك إلى ملف PDF الممسوح** – حدد مسارات الإدخال والإخراج.
3. **تشغيل التحويل** – يقوم Aspose بالعمل الشاق ويكتب PDF قابلًا للبحث.
4. **التحقق من النتيجة** – افتح الملف الناتج وجرب البحث عن نص.

كل خطوة موضحة في قسمها الخاص، بحيث يمكنك اختيار الأجزاء التي تهمك أكثر.

---

## تحويل PDF ممسوح إلى PDF قابل للبحث

أول شيء عليك فعله هو إنشاء نسخة من `OcrEngine`. هذا الكائن هو العامل الأساسي الذي يقرأ الصور النقطية داخل PDF ويستخرج النص.

```csharp
using Aspose.OCR;
using System;

class PdfSearchableDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Optional: enable GPU for faster processing
            UseGpuAcceleration = true
        };

        // Step 2: Specify the input scanned PDF and the output searchable PDF paths
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string searchablePdfPath = @"C:\Docs\output.pdf";

        // Step 3: Convert the scanned PDF into a searchable PDF
        ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

        // Step 4: Notify the user where the searchable PDF was saved
        Console.WriteLine("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**لماذا يعمل هذا:** `ConvertToSearchablePdf` يقرأ كل صفحة، ينفّذ OCR على المحتوى النقطي، ثم يدمج طبقة نصية غير مرئية خلف الصورة الأصلية. النتيجة تبدو تمامًا كالمستند الممسوح الأصلي، لكن الآن يمكنك نسخ النص، تحديده، والبحث فيه.

---

## إضافة OCR إلى PDF باستخدام Aspose

إذا كان لديك بالفعل ملف PDF وتريد فقط **إضافة OCR إلى PDF** دون تحويل الملف بالكامل، يمكنك استدعاء نفس الطريقة—تتعامل Aspose مع العملية كـ “إضافة OCR”. الكود أعلاه يقوم بذلك بالفعل، لكن إليك نسخة مختصرة توضح كيف يمكنك معالجة ملفات متعددة داخل حلقة:

```csharp
string[] pdfFiles = Directory.GetFiles(@"C:\Docs\Scanned", "*.pdf");
foreach (var file in pdfFiles)
{
    string output = Path.Combine(@"C:\Docs\Searchable", Path.GetFileNameWithoutExtension(file) + "_searchable.pdf");
    ocrEngine.ConvertToSearchablePdf(file, output);
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(output)}");
}
```

**نصيحة:** احتفظ بنفس نسخة `OcrEngine` للدفعة بأكملها. إعادة إنشائه في كل مرة يضيف عبئًا غير ضروري، خاصة عندما **تمكن تسريع GPU**.

---

## تمكين تسريع GPU لتسريع OCR

يمكن لتسريع GPU أن يختصر دقائق من وقت المعالجة لدفعات كبيرة. يستخدم Aspose OCR تقنية NVIDIA CUDA تحت الغطاء، لذا كل ما عليك هو تبديل علم منطقي:

```csharp
ocrEngine.UseGpuAcceleration = true; // set to false if no compatible GPU
```

**متى تستخدمه:** إذا كنت تعالج ملفات PDF أكبر من 10 ميغابايت أو تتعامل مع أكثر من بضعة عشر ملفات، سيمنحك الـ GPU عادةً زيادة سرعة 2‑3×. على لابتوب عادي بدون GPU يدعم CUDA، اترك القيمة `false`—ستعود المكتبة تلقائيًا إلى المعالجة على الـ CPU.

**خطأ شائع:** نسيان تثبيت نسخة برنامج تشغيل CUDA المتوافقة قد يسبب استثناءً وقت التشغيل (`CudaException`). تأكد من أن برنامج التشغيل يطابق الإصدار الذي تتوقعه Aspose (تحقق من ملاحظات الإصدار على صفحة NuGet).

---

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي تطبيق كونسول مستقل يمكنك نسخه ولصقه في مشروع .NET جديد. يتضمن تعليقات مفيدة، معالجة أخطاء، وخطوة تحقق نهائية تطبع عدد الصفحات التي تم معالجتها.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class PdfSearchableDemo
{
    static void Main()
    {
        try
        {
            // 1️⃣ Initialize OCR engine – English language, GPU on if available
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                UseGpuAcceleration = true // set to false on non‑GPU machines
            };

            // 2️⃣ Define input and output paths
            string sourcePdfPath = @"C:\Docs\input.pdf";
            string searchablePdfPath = @"C:\Docs\output.pdf";

            // 3️⃣ Perform the conversion – this creates a searchable PDF
            ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

            // 4️⃣ Simple verification – count pages in the new file
            int pageCount = new Aspose.Pdf.Facades.PdfFileInfo(searchablePdfPath).NumberOfPages;
            Console.WriteLine($"✅ Searchable PDF created at: {searchablePdfPath}");
            Console.WriteLine($"📄 The new file contains {pageCount} pages.");

            // 5️⃣ Optional: open the file automatically (Windows only)
            // System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(searchablePdfPath) { UseShellExecute = true });
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
        }
    }
}
```

**الناتج المتوقع**

```
✅ Searchable PDF created at: C:\Docs\output.pdf
📄 The new file contains 12 pages.
```

افتح `output.pdf` في أي عارض PDF وجرب كتابة كلمة تظهر في الصور الممسوحة. إذا تم تمييز النص، فقد نجحت في **إنشاء PDF قابل للبحث**.

---

## مشكلات شائعة ونصائح احترافية

| المشكلة | لماذا تحدث | كيفية الإصلاح / التجنب |
|-------|----------------|--------------------|
| **GPU غير مكتشف** | عدم وجود أو عدم توافق برنامج تشغيل CUDA. | ثبّت نسخة برنامج التشغيل المذكورة في ملاحظات إصدار Aspose؛ اضبط `UseGpuAcceleration = false` كخيار احتياطي. |
| **اللغة غير صحيحة** | OCR يفرض اللغة الإنجليزية افتراضيًا؛ اللغات الأخرى تحتاج إلى تعيين صريح. | اضبط `Language = Language.Spanish` (أو أي تعداد مدعوم) قبل التحويل. |
| **PDF كبير يسبب OutOfMemory** | المحرك يحمل الصفحات بالكامل في الذاكرة. | عالج PDF على دفعات باستخدام `ocrEngine.PageRange = new PageRange(1, 5)` لكل مجموعة. |
| **ملف الإخراج تالف** | المجلد الوجهة يفتقر إلى صلاحيات الكتابة. | شغّل التطبيق بامتيازات مرتفعة أو اختر مسارًا قابلًا للكتابة. |
| **طبقة النص غير قابلة للبحث** | عارض PDF يخزن نسخة قديمة في الذاكرة المؤقتة. | حدّث عارض PDF أو أعد فتح الملف. |

**نصيحة احترافية:** عندما تتعامل مع مزيج من ملفات PDF الممسوحة والملفات الأصلية، تحقق من علم `HasText` لكل صفحة (`PdfPageInfo.HasText`) قبل تشغيل OCR. هذا يوفر دورات CPU ويتجنب تكرار OCR على الصفحات التي هي بالفعل قابلة للبحث.

---

## التحقق من النتيجة برمجيًا (اختياري)

إذا رغبت في أتمتة عملية التحقق، يمكن لـ Aspose.PDF استخراج النص المخفي:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the searchable PDF
Document doc = new Document(searchablePdfPath);
TextAbsorber absorber = new TextAbsorber();
doc.Pages.Accept(absorber);
string extracted = absorber.Text;

// Simple check – does the word "Invoice" appear?
if (extracted.Contains("Invoice"))
    Console.WriteLine("✅ OCR succeeded – 'Invoice' found.");
else
    Console.WriteLine("⚠️ OCR may have missed some text.");
```

هذا المقتطف يثبت أنك فعلاً **تحولت PDF إلى صيغة قابلة للبحث**، وليس مجرد وضع صورة فوقها.

---

## مثال صورة

![مثال ناتج PDF قابل للبحث](https://example.com/images/searchable-pdf.png "إنشاء PDF قابل للبحث باستخدام Aspose OCR")

*نص بديل:* مثال **إنشاء PDF قابل للبحث** يُظهر قبل (ممسوح) وبعد (قابل للبحث).

---

## الخطوات التالية والمواضيع ذات الصلة

- **معالجة دفعات:** ضع الحلقة من قسم “إضافة OCR إلى PDF” داخل خدمة Windows أو Azure Function للمهام الليلية.
- **دعم لغات متقدم:** استكشف `ocrEngine.Language = Language.Multilingual` للمستندات التي تحتوي على نصوص مختلطة.
- **تنظيف ما بعد OCR:** استخدم `TextFragmentAbsorber` من Aspose.PDF لتصحيح الأخطاء الشائعة في OCR (مثل “0” مقابل “O”).
- **الأمان**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}