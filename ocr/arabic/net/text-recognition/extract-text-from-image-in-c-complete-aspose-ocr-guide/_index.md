---
category: general
date: 2026-01-10
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية تحويل نص
  المستند الممسوح ضوئياً باستخدام المعالجة الدفعية وحفظ النتائج.
draft: false
keywords:
- extract text from image
- convert scanned document text
- batch OCR processing
- Aspose OCR
- C# OCR tutorial
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدرس كيفية
  تحويل نص المستند الممسوح ضوئياً باستخدام المعالجة الدفعية.
og_title: استخراج النص من الصورة في C# – دليل Aspose OCR الكامل
tags:
- OCR
- C#
- Aspose
- Image Processing
title: استخراج النص من الصورة في C# – دليل Aspose OCR الكامل
url: /ar/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة – دليل Aspose OCR الكامل

هل احتجت يومًا إلى **استخراج النص من الصورة** لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك؛ العديد من المطورين يواجهون هذه المشكلة عند التعامل مع ملفات PDF الممسوحة ضوئيًا، أو ملفات TIFF متعددة الصفحات، أو الإيصالات المستندة إلى الصور. الخبر السار هو أنه باستخدام Aspose OCR يمكنك **تحويل نص المستند الممسوح ضوئيًا** في بضع أسطر فقط من C#.

في هذا الدرس سنستعرض سيناريو واقعي: أخذ ملف TIFF متعدد الصفحات، تشغيل OCR دفعي على كل صفحة، وكتابة ملف نصي واحد يحتوي على محتوى كل صفحة. بنهاية الدرس ستحصل على تطبيق كونسول جاهز للتنفيذ، وتفهم لماذا كل خطوة مهمة، وتعرف كيف تعدل التدفق لحالات الحافة مثل الصور المحمية بكلمة مرور أو حزم اللغات المخصصة.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا)  
- Visual Studio 2022 (أو أي محرر تفضله)  
- ملف ترخيص Aspose OCR (أو يمكنك استخدام وضع التقييم المجاني)  
- ملف صورة متعدد الصفحات (مثال: `multipage.tif`) موجود في مجلد يمكنك الإشارة إليه  

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.OCR`؛ سنقوم بتثبيتها في الخطوة الأولى.

## الخطوة 1 – تثبيت Aspose  OCR وإعداد المشروع

للبدء، أنشئ مشروع كونسول جديد وأضف مكتبة Aspose OCR.

```bash
dotnet new console -n ImageTextExtractor
cd ImageTextExtractor
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كان لديك ملف ترخيص (`Aspose.OCR.lic`)، انسخه إلى جذر المشروع. ستقوم المكتبة تلقائيًا بتحميله أثناء التشغيل.

لماذا هذه الخطوة؟ تثبيت الحزمة يمنحك الوصول إلى `BatchProcessor` و `OcrEngine` وفئات مفيدة أخرى تُجردك من التعامل مع الصور على مستوى منخفض. كما يضمن أنك تستخدم أحدث خوارزميات OCR التي تقدمها Aspose.

## الخطوة 2 – تحميل صورة متعددة الصفحات باستخدام BatchProcessor

`BatchProcessor` صُمم لهذا السيناريو بالضبط: التكرار على كل صفحة من صورة متعددة الصفحات دون الحاجة إلى تقسيم الملفات يدويًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System.Text;

// Step 2: Initialize the batch processor with the path to your TIFF
var batchProcessor = new BatchProcessor(@"YOUR_DIRECTORY\multipage.tif");

// Verify that pages were loaded
if (batchProcessor.Pages.Count == 0)
{
    Console.WriteLine("No pages found – double‑check the file path.");
    return;
}
```

يقوم `BatchProcessor` بقراءة جميع الصفحات إلى الذاكرة، ويُتيح الوصول إليها عبر `batchProcessor.Pages`. كل كائن صفحة يعرف رقمه (`ocrPage.Number`) والذي سنستخدمه لاحقًا لعناوين واضحة.

## الخطوة 3 – إعداد StringBuilder لتجميع النتائج

نريد ملف نصي واحد يحتوي على مخرجات OCR لكل صفحة، مفصولة بعناوين. `StringBuilder` هو أكثر طريقة كفاءة لدمج السلاسل داخل حلقة.

```csharp
// Step 3: Create a StringBuilder to collect OCR results
var extractedText = new StringBuilder();
```

لماذا `StringBuilder`؟ دمج السلاسل باستخدام `+` داخل حلقة سيؤدي إلى إنشاء سلسلة جديدة في كل تكرار، مما يضر بالأداء—خاصةً مع المستندات الكبيرة.

## الخطوة 4 – التكرار على كل صفحة، تشغيل OCR، وإضافة النتائج

الآن نصل إلى جوهر الدرس: التكرار على كل صفحة، التعرف على النص، وتخزينه مع علامة صفحة.

```csharp
// Step 4: Process each page individually
foreach (var ocrPage in batchProcessor.Pages)
{
    // Create a fresh OcrEngine for every page – this isolates settings
    var ocrEngine = new OcrEngine
    {
        Image = ocrPage
    };

    // Perform recognition
    ocrEngine.Recognize();

    // Append a clear header and the recognized text
    extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
    extractedText.AppendLine(ocrEngine.Text);
}
```

**لماذا إنشاء `OcrEngine` جديد لكل صفحة؟** بعض المطورين يعيدون استخدام محرك واحد ويغيرون خاصية `Image`، لكن ذلك قد يحتفظ بإعدادات اللغة أو النتائج السابقة، مما يسبب أخطاء دقيقة. إنشاء محرك جديد يضمن بداية نظيفة.

### التعامل مع الحالات الشائعة

- **صفحات فارغة:** إذا كانت الصفحة لا تحتوي على نص يمكن التعرف عليه، سيكون `ocrEngine.Text` سلسلة فارغة. قد ترغب في إدراج عنصر نائب مثل “(No text detected)”.
- **اختيار اللغة:** بشكل افتراضي يستخدم Aspose OCR اللغة الإنجليزية. لمعالجة الألمانية أو الفرنسية، اضبط `ocrEngine.Language = Language.German;` قبل استدعاء `Recognize()`.
- **نصيحة أداء:** بالنسبة لملفات TIFF الضخمة، يمكنك تمكين `ocrEngine.UseParallelProcessing = true;` لاستغلال الأنوية المتعددة.

## الخطوة 5 – كتابة المخرجات المجمعة إلى ملف نصي

أخيرًا، احفظ السلسلة المتجمعة على القرص.

```csharp
// Step 5: Save the result to a .txt file
string outputPath = @"YOUR_DIRECTORY\multipage_result.txt";
File.WriteAllText(outputPath, extractedText.ToString());

Console.WriteLine($"OCR complete! Results saved to {outputPath}");
```

سيظهر ملف `multipage_result.txt` الناتج بالشكل التالي:

```
--- Page 1 ---
This is the first page of the scanned document.
It contains a title and some introductory text.

--- Page 2 ---
Continuation of the report.
Data tables and figures follow.
```

الآن لديك **استخراج النص من الصورة** و**تحويل نص المستند الممسوح ضوئيًا** إلى صيغة قابلة للبحث والتحرير.

## إضافي – نظرة بصرية (نص بديل للصورة)

فيما يلي مخطط تدفق بسيط يوضح العملية.  
*النص البديل:* “مخطط يوضح كيفية استخراج النص من الصورة باستخدام معالجة دفعة Aspose OCR في C#”.

![OCR Flow Diagram](placeholder-image-url.png)

*(إذا كنت تنشر هذا الدرس على موقع ثابت، استبدل العنصر النائب بملف SVG أو PNG فعلي.)*

## الأسئلة المتكررة

**هل يعمل هذا مع ملفات PDF؟**  
نعم، يمكن لـ Aspose OCR قراءة صفحات PDF كصور. عليك فقط تحويل PDF إلى صور أولًا، أو استخدام `PdfDocument` من `Aspose.PDF` وتغذية كل صورة صفحة إلى `OcrEngine`.

**ماذا لو كان ملف TIFF محميًا بكلمة مرور؟**  
`BatchProcessor` لا يتعامل مع التشفير مباشرة. فك تشفير الملف باستخدام مكتبة مثل `Aspose.Imaging` قبل تمريره إلى خط أنابيب OCR.

**هل يمكنني إخراج JSON بدلاً من النص العادي؟**  
بالطبع. استبدل منطق `StringBuilder` بمسلسل JSON (مثل `System.Text.Json`) وخزن نص كل صفحة تحت مفتاح `pageNumber`.

## مثال كامل يعمل

إليك البرنامج الكامل الذي يمكنك نسخه ولصقه في `Program.cs`. يتضمن جميع توجيهات using، معالجة الأخطاء، وتعليقات.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Text;

namespace ImageTextExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            string inputImagePath = @"YOUR_DIRECTORY\multipage.tif";
            string outputTextPath = @"YOUR_DIRECTORY\multipage_result.txt";

            // 1️⃣ Load the multi‑page image
            var batchProcessor = new BatchProcessor(inputImagePath);
            if (batchProcessor.Pages.Count == 0)
            {
                Console.WriteLine("No pages detected – verify the file path.");
                return;
            }

            // 2️⃣ Prepare a StringBuilder for the final output
            var extractedText = new StringBuilder();

            // 3️⃣ Process each page
            foreach (var ocrPage in batchProcessor.Pages)
            {
                var ocrEngine = new OcrEngine
                {
                    Image = ocrPage,
                    // Uncomment to change language:
                    // Language = Language.German,
                    // UseParallelProcessing = true
                };

                // Run OCR
                ocrEngine.Recognize();

                // Append header and text
                extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
                // Guard against empty results
                string pageText = string.IsNullOrWhiteSpace(ocrEngine.Text)
                    ? "(No text detected on this page)"
                    : ocrEngine.Text;
                extractedText.AppendLine(pageText);
            }

            // 4️⃣ Write to file
            File.WriteAllText(outputTextPath, extractedText.ToString());

            Console.WriteLine($"✅ Extraction complete. File saved at: {outputTextPath}");
        }
    }
}
```

شغّل البرنامج باستخدام:

```bash
dotnet run
```

سترى رسالة في الكونسول تؤكد النجاح، وسيحتوي ملف الإخراج على نتائج OCR المدمجة.

## الخلاصة

لقد عرضنا طريقة عملية **لاستخراج النص من الصورة** باستخدام Aspose OCR، وتحويل أي ملف ممسوح ضوئيًا متعدد الصفحات إلى نص عادي قابل للبحث. من خلال الاستفادة من `BatchProcessor` وإعداد `OcrEngine` نظيف لكل صفحة، يمكنك **تحويل نص المستند الممسوح ضوئيًا** بشكل موثوق مع الحفاظ على بساطة وصيانة الكود.

لا تتردد في التجربة: جرّب لغات مختلفة، غيّر الإخراج إلى JSON، أو دمج هذه المنطق في واجهة ويب API تعالج التحميلات فورًا. النمط الأساسي يبقى نفسه—تحميل، التعرف، التجميع، والحفظ.

هل لديك المزيد من الأسئلة حول OCR، تراخيص Aspose، أو معالجة دفعات المستندات الضخمة؟ اترك تعليقًا أدناه أو راجع الوثائق الرسمية لـ Aspose لمزيد من التفاصيل. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}