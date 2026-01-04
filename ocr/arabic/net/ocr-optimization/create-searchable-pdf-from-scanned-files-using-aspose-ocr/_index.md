---
category: general
date: 2026-01-04
description: أنشئ ملف PDF قابل للبحث من ملف PDF ممسوح ضوئياً بسرعة. تعلّم كيفية تحويل
  PDF الممسوح، إضافة OCR إلى PDF، وضبط جودة الصورة باستخدام Aspose OCR في C#.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- add ocr to pdf
- adjust image quality
- how to use ocr
language: ar
og_description: أنشئ ملف PDF قابل للبحث من ملف PDF ممسوح ضوئياً بسرعة. اتبع هذا الدليل
  خطوة بخطوة لتحويل ملف PDF الممسوح، وإضافة OCR إلى PDF، وضبط جودة الصورة.
og_title: إنشاء ملف PDF قابل للبحث من الملفات الممسوحة ضوئياً باستخدام Aspose OCR
tags:
- Aspose OCR
- C#
- PDF processing
title: إنشاء ملف PDF قابل للبحث من ملفات ممسوحة ضوئيًا باستخدام Aspose OCR
url: /ar/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث من ملفات ممسوحة ضوئياً باستخدام Aspose OCR

هل احتجت يوماً إلى **create searchable PDF** من مجموعة من المستندات الممسوحة ضوئياً لكنك لم تعرف من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند بناء خطوط معالجة المستندات. الخبر السار؟ باستخدام Aspose OCR يمكنك **convert scanned PDF**، إضافة OCR، وضبط جودة الصورة ببضع أسطر من C# فقط.

في هذا الدرس سنستعرض العملية بالكامل، من تحميل ملف PDF الممسوح إلى حفظ نسخة قابلة للبحث بالكامل. في النهاية ستعرف بالضبط **how to use OCR** مع Aspose، لماذا كل إعداد مهم، وما الذي يجب تعديله عندما لا تسير الأمور كما هو مخطط. لا مراجع غامضة—فقط مثال كامل قابل للتنفيذ يمكنك إدراجه في مشروعك اليوم.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضاً)
- رخصة Aspose OCR صالحة (الإصدار التجريبي المجاني يكفي للاختبار)
- ملف PDF إدخال يُدعى `input.pdf` موجود في مجلد يمكنك التحكم فيه
- Visual Studio 2022 أو أي محرر C# تفضله

هذا كل ما تحتاجه. إذا كان أي من هذه غير مألوف لك، توقف وقم بتثبيت العنصر المفقود—لا شيء آخر مطلوب.

## الخطوة 1: تهيئة محرك OCR وتحميل ملف PDF الممسوح  
**(هنا نضيف OCR إلى PDF للمرة الأولى.)**

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Load the scanned PDF from disk
ocrEngine.LoadPdf(@"C:\Docs\input.pdf");
```

*لماذا هذه الخطوة؟*  
`OcrEngine` هو قلب Aspose OCR. تحميل الـ PDF يخبر المحرك أين يبحث عن الصور النقطية التي سيحللها لاحقاً. إذا تخطيت هذه الخطوة، لن يكون هناك ما يتحول، وستظهر استثناءات في الخطوات التالية.

> **نصيحة احترافية:** إذا كان ملف PDF محمياً بكلمة مرور، استخدم `ocrEngine.LoadPdf(path, password)` لتجنب خطأ وقت التشغيل.

## الخطوة 2: تعيين اللغة الأساسية واللغات الإضافية  
**(سنقوم **convert scanned PDF** بالإنجليزية، الفرنسية، والألمانية.)**

```csharp
// Primary language – the most common language in the document
ocrEngine.Config.Language = Language.English;

// Add extra languages if the document contains multilingual text
ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };
```

*لماذا اللغة مهمة؟*  
دقة OCR تعتمد على مجموعة الأحرف التي يتوقعها. بإعلان الإنجليزية كلغة أساسية وإضافة الفرنسية/الألمانية، يستطيع المحرك تفسير الأحرف ذات اللكنات والرموز الخاصة بشكل صحيح. نسيان هذا غالباً ما يؤدي إلى نص مشوش.

## الخطوة 3: ضبط جودة الصورة – تحسين مخرجات PDF  
**(هنا نُعد **adjust image quality** لتحقيق توازن بين حجم الملف وقابلية القراءة.)**

```csharp
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    ImageQuality = 90,          // JPEG quality for embedded images (0‑100)
    Compress = true,            // Enable PDF compression to shrink file size
    PreserveOriginalLayout = true // Keep the scanned layout intact
};
```

*لماذا نضبط `ImageQuality`؟*  
القيمة الأعلى (90‑100) تحافظ على الوضوح، وهو أمر حاسم لدقة OCR، لكنها تزيد من حجم الملف. إذا كنت تقوم بأرشفة ملايين الصفحات، خفضها إلى 70‑80 للحصول على PDF أصغر دون التضحية كثيراً بقراءة النص.

## الخطوة 4: حفظ النتيجة كملف PDF قابل للبحث  
**(الآن نُنشئ **create searchable PDF** الذي يمكنك فهرسته.)**

```csharp
// Export the OCR result as a searchable PDF
ocrEngine.SaveAsSearchablePdf(@"C:\Docs\output.pdf", pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created at C:\\Docs\\output.pdf");
```

*ماذا يحدث فعلياً؟*  
Aspose OCR يستخرج طبقة النص من كل صفحة ويضمّنها خلف الصورة الأصلية. يظل الـ PDF بصرياً كما هو، لكن يمكنك الآن تحديد النص، نسخه، والبحث فيه—وذلك يُعد فوزاً كبيراً لسير العمل اللاحق.

## الخطوة 5: التحقق من النتيجة (اختياري لكن موصى به)  
من السهل الافتراض أن كل شيء نجح، لكن فحص سريع يوفر عليك المتاعب لاحقاً.

```csharp
using System.Diagnostics;

// Open the generated PDF automatically (Windows only)
Process.Start(new ProcessStartInfo
{
    FileName = @"C:\Docs\output.pdf",
    UseShellExecute = true
});
```

افتح الملف، حاول تحديد كلمة، أو اضغط `Ctrl+F` واكتب عبارة تعرف أنها موجودة في المسح الأصلي. إذا كان النص قابلًا للتحديد، فقد نجحت في **create searchable PDF**.

## حالات الحافة الشائعة وكيفية التعامل معها  

| الحالة | لماذا يحدث | الحل السريع |
|-----------|----------------|-----------|
| **صفحات ذات دقة مختلطة** (بعضها 150 dpi، والبعض الآخر 300 dpi) | جودة OCR تختلف من صفحة لأخرى، مما يؤدي إلى عدم تجانس قابلية البحث. | اضبط `ocrEngine.Config.Dpi = 300;` قبل التحميل لإجبار الرفع، أو عالج مسبقاً باستخدام `ImageProcessor` لتوحيد الـ DPI. |
| **PDF مشفر** | Aspose OCR لا يستطيع القراءة بدون كلمة المرور. | مرّر كلمة المرور إلى `LoadPdf` كما هو موضح أعلاه. |
| **PDF كبير (>500 MB)** | استهلاك الذاكرة يرتفع، مما يسبب `OutOfMemoryException`. | عالج المستند على دفعات: `ocrEngine.SplitPdfIntoPages();` ثم نفّذ OCR على كل صفحة على حدة وادمج النتائج. |
| **حروف غير لاتينية** (مثل السيريالية) | اللغة غير مضافة، فتتحول الأحرف إلى “?” | أضف `Language.Russian` (أو أي لغة تحتاجها) إلى `AdditionalLanguages`. |
| **جودة صورة منخفضة جداً** | يصبح النص غير واضح، ويفشل OCR. | زد `ImageQuality` أو استخدم `pdfOptions.Dpi = 300;` لتضمين صور ذات دقة أعلى. |

## مثال كامل وجاهز للتنفيذ  

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق Console جديد. يتضمن جميع الخطوات، معالجة الأخطاء، وتعليقات لتوضيح كل جزء.

```csharp
using System;
using System.Diagnostics;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\Docs\input.pdf";
            string outputPath = @"C:\Docs\output.pdf";

            try
            {
                // 1️⃣ Initialize OCR engine and load scanned PDF
                OcrEngine ocrEngine = new OcrEngine();
                ocrEngine.LoadPdf(inputPath);

                // 2️⃣ Configure languages (primary + additional)
                ocrEngine.Config.Language = Language.English;
                ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };

                // 3️⃣ Set PDF save options – adjust image quality as needed
                PdfSaveOptions pdfOptions = new PdfSaveOptions
                {
                    ImageQuality = 90,
                    Compress = true,
                    PreserveOriginalLayout = true
                };

                // 4️⃣ Save as searchable PDF
                ocrEngine.SaveAsSearchablePdf(outputPath, pdfOptions);
                Console.WriteLine($"✅ Searchable PDF created at {outputPath}");

                // 5️⃣ Optional: open the file to verify
                Process.Start(new ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            catch (Exception ex)
            {
                // Friendly error message – helps during debugging
                Console.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
                // For real‑world apps, consider logging the stack trace
            }
        }
    }
}
```

**الناتج المتوقع:**  
```
✅ Searchable PDF created at C:\Docs\output.pdf
```

عند فتح `output.pdf`، يجب أن تكون قادرًا على تحديد والبحث عن أي نص كان موجودًا في المسح الأصلي.

---

## الأسئلة المتكررة (FAQs)

**س: هل يعمل هذا مع ملفات PDF تحتوي على صور ممسوحة ونص أصلي؟**  
ج: بالتأكيد. Aspose OCR يضيف طبقة نص مخفية فقط حيث يلزم، ويترك النص الموجود دون تعديل.

**س: هل يمكنني معالجة مجموعة من ملفات PDF دفعة واحدة؟**  
ج: نعم. ضع الكود أعلاه داخل حلقة `foreach (var file in Directory.GetFiles(folder, "*.pdf"))` وعدّل مسار الإخراج وفقًا لذلك.

**س: كيف يمكنني تقليل حجم PDF النهائي أكثر؟**  
ج: خفض `ImageQuality` إلى 70‑80، فعّل `Compress`، أو استخدم `pdfOptions.Dpi = 150` لتقليل دقة الصور قبل تضمينها.

**س: هل هناك طريقة لاستخراج نص OCR دون إنشاء PDF؟**  
ج: استدعِ `ocrEngine.ExtractText();` بعد تحميل الـ PDF. سيعيد ذلك سلسلة نصية عادية يمكنك تخزينها أو فهرستها.

---

## الخلاصة  

لقد غطينا **how to use OCR** مع Aspose لإنشاء **create searchable PDF** من مستند ممسوح، وأظهرنا لك كيفية **convert scanned PDF**، و**add OCR to PDF**، وشرحنا كيفية **adjust image quality** للحصول على أفضل النتائج. الكود الكامل جاهز للتنفيذ، وجدول استكشاف الأخطاء سيساعدك على الاستمرار عندما تظهر مفاجآت غير متوقعة.

ما الخطوة التالية؟ جرّب ما يلي:

- حزم لغات مختلفة لأرشيفات متعددة اللغات
- معالجة صور مخصصة (تصحيح الميل، إزالة البقع) عبر `ImageProcessor`
- دمج PDF القابل للبحث في خط أنابيب SharePoint أو ElasticSearch

لا تتردد في ترك تعليق إذا واجهت مشكلة أو اكتشفت تعديلًا ذكيًا. نتمنى لك برمجة سعيدة، واستمتع بملفات PDF القابلة للبحث فورًا! 

![Create searchable PDF flowchart showing OCR engine → language config → PDF save options → searchable PDF output](create-searchable-pdf-flow.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}