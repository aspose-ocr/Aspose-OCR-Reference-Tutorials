---
category: general
date: 2026-05-28
description: التعرف على النص من ملفات PNG باستخدام Aspose OCR في C#. تعلم كيفية استخراج
  النص من الصفحات الممسوحة ضوئياً وإجراء OCR على الصور بكفاءة.
draft: false
keywords:
- recognize text from png
- extract text from scanned pages
- perform ocr on images
- Aspose OCR C#
- OCR image processing
language: ar
og_description: التعرف على النص من ملفات PNG باستخدام Aspose OCR في C#. تعلم كيفية
  استخراج النص من الصفحات الممسوحة ضوئياً وإجراء OCR على الصور في دقائق.
og_title: التعرف على النص من PNG باستخدام Aspose OCR – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: recognize text from png using Aspose OCR in C#. Learn how to extract
    text from scanned pages and perform OCR on images efficiently.
  headline: recognize text from png with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: recognize text from png using Aspose OCR in C#. Learn how to extract
    text from scanned pages and perform OCR on images efficiently.
  name: recognize text from png with Aspose OCR – Complete C# Guide
  steps:
  - name: '**Engine initialization** – The `OcrEngine` class is the entry point; it
      holds all configuration and state.'
    text: '**Engine initialization** – The `OcrEngine` class is the entry point; it
      holds all configuration and state.'
  - name: '**Evaluation‑mode guard** – If you’re using a trial license, Aspose caps
      the number of pages you can process. Setting `MaxPagesInEvaluation` prevents
      the library from throwing a *LicenseException* halfway through.'
    text: '**Evaluation‑mode guard** – If you’re using a trial license, Aspose caps
      the number of pages you can process. Setting `MaxPagesInEvaluation` prevents
      the library from throwing a *LicenseException* halfway through.'
  - name: '**Image loading** – `ImageStream.FromFile` abstracts away the `System.Drawing`
      dependency, letting you feed any supported format (PNG, JPEG, BMP) directly.'
    text: '**Image loading** – `ImageStream.FromFile` abstracts away the `System.Drawing`
      dependency, letting you feed any supported format (PNG, JPEG, BMP) directly.'
  - name: '**Recognition loop** – By iterating, you can **perform OCR on images**
      in bulk, which is exactly what most real‑world scanning pipelines need.'
    text: '**Recognition loop** – By iterating, you can **perform OCR on images**
      in bulk, which is exactly what most real‑world scanning pipelines need.'
  - name: '**Disposal** – The engine holds unmanaged resources; disposing releases
      memory promptly, especially important when processing many high‑resolution PNGs.'
    text: '**Disposal** – The engine holds unmanaged resources; disposing releases
      memory promptly, especially important when processing many high‑resolution PNGs.'
  - name: Install the NuGet package.
    text: Install the NuGet package.
  - name: Initialise `OcrEngine`.
    text: Initialise `OcrEngine`.
  - name: (Optional) Set a page limit for evaluation mode.
    text: (Optional) Set a page limit for evaluation mode.
  - name: Load each PNG with `ImageStream.FromFile`.
    text: Load each PNG with `ImageStream.FromFile`.
  - name: Call `Recognize()` and output the result.
    text: Call `Recognize()` and output the result.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: التعرف على النص من ملف PNG باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/recognize-text-from-png-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من PNG باستخدام Aspose OCR – دليل C# كامل

هل احتجت يوماً إلى **التعرف على النص من PNG** في تطبيق .NET؟ باستخدام Aspose OCR يمكنك بسرعة **استخراج النص من الصفحات الممسوحة** و**إجراء OCR على الصور** دون الحاجة إلى معالجة الصور منخفضة المستوى. في هذا الدرس سنستعرض مثالًا جاهزًا للتنفيذ بلغة C#، نشرح لماذا كل سطر مهم، ونظهر لك كيفية تكييفه للمشاريع الواقعية.

إذا كنت تتساءل ما إذا كان هذا يعمل على مسحات متعددة الصفحات، أو كيف يمكنك تحديد وضع التقييم، أو كيفية التعامل مع ملفات صور ضخمة—تابع معنا. في النهاية ستحصل على مقتطف جاهز للإنتاج يمكنك نسخه ولصقه في حلّك الخاص.

---

## ما ستحتاجه

قبل أن نبدأ، تأكد من توفر ما يلي:

| المتطلب المسبق | لماذا هو مهم |
|----------------|--------------|
| **.NET 6.0 أو أحدث** (أو .NET Framework 4.6+) | تستهدف Aspose.OCR بيئات تشغيل حديثة وتوفر أحدث تحسينات الأداء. |
| **Visual Studio 2022** (أو أي بيئة تطوير تفضّلها) | محرر مريح يجعل اختبار الكود أسهل. |
| **حزمة NuGet Aspose.OCR** | هذه هي المكتبة التي تقوم بالعمل الفعلي. |
| مجلد يحتوي على مجموعة من **صور PNG** التي تريد قراءتها | يفترض الدرس وجود ملفات مسماة `page1.png`، `page2.png`، … |

إذا كان أي من هذه غير مألوف لك، فقط قم بتثبيت حزمة NuGet وأنشئ مشروع console بسيط—لا حاجة لإعدادات إضافية.

---

## الخطوة 1: تثبيت Aspose.OCR عبر NuGet

افتح الطرفية (أو Package Manager Console) وشغّل الأمر:

```bash
dotnet add package Aspose.OCR
```

أو، إذا كنت تفضّل الواجهة الرسومية، انقر بزر الماوس الأيمن على **Dependencies → Manage NuGet Packages**، ابحث عن *Aspose.OCR*، ثم اضغط **Install**. سيقوم ذلك بجلب كل ما تحتاجه، بما في ذلك فئة المساعدة `ImageStream` المستخدمة لاحقًا.

> **نصيحة احترافية:** استخدم أحدث نسخة مستقرة (حتى مايو 2026 النسخة هي 23.10). الإصدارات الجديدة غالبًا ما تحتوي على إصلاحات لأخطاء تنسيقات الصور المعقدة.

---

## الخطوة 2: إنشاء تطبيق Console بسيط

أنشئ مشروع console جديد إذا لم تقم بذلك بعد:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

استبدل محتوى `Program.cs` بالمثال الكامل أدناه. لاحظ كيف حافظنا على الكود **مستقلاً**—بدون ملفات إعدادات خارجية، بدون سحر مخفي.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine
            // -------------------------------------------------
            var engine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣  Optional: limit pages when running in evaluation mode
            // -------------------------------------------------
            // Evaluation licenses only allow a few pages; set this to avoid runtime errors.
            engine.Configuration.MaxPagesInEvaluation = 5;

            // -------------------------------------------------
            // 3️⃣  Define where your PNG files live
            // -------------------------------------------------
            string basePath = @"YOUR_DIRECTORY"; // <-- change this to your real folder

            // -------------------------------------------------
            // 4️⃣  Loop through the images you want to process
            // -------------------------------------------------
            for (int i = 0; i < 5; i++) // adjust the loop count to match your file count
            {
                // Load the current page image
                engine.Image = ImageStream.FromFile($"{basePath}/page{i + 1}.png");

                // -------------------------------------------------
                // 5️⃣  Perform OCR and display the result
                // -------------------------------------------------
                Console.WriteLine($"--- Page {i + 1} ---");
                string recognizedText = engine.Recognize();

                // Show the extracted text; you could also write it to a file.
                Console.WriteLine(recognizedText);
                Console.WriteLine(); // blank line for readability
            }

            // -------------------------------------------------
            // 6️⃣  Clean up (optional but good practice)
            // -------------------------------------------------
            engine.Dispose();
        }
    }
}
```

### لماذا يعمل هذا الهيكل

1. **تهيئة المحرك** – فئة `OcrEngine` هي نقطة الدخول؛ تحتفظ بكل الإعدادات والحالة.
2. **حارس وضع التقييم** – إذا كنت تستخدم ترخيص تجريبي، تقوم Aspose بتحديد عدد الصفحات التي يمكن معالجتها. ضبط `MaxPagesInEvaluation` يمنع المكتبة من رمي *LicenseException* في منتصف العملية.
3. **تحميل الصورة** – `ImageStream.FromFile` يزيل الاعتماد على `System.Drawing`، مما يتيح لك تمرير أي تنسيق مدعوم (PNG، JPEG، BMP) مباشرة.
4. **حلقة التعرف** – من خلال التكرار، يمكنك **إجراء OCR على الصور** دفعةً واحدة، وهو ما تحتاجه معظم خطوط معالجة المسحات في العالم الحقيقي.
5. **التفريغ** – يحتفظ المحرك بموارد غير مُدارة؛ التفريغ يحرّر الذاكرة فورًا، وهو أمر مهم عند معالجة عدد كبير من PNG عالية الدقة.

---

## الخطوة 3: تشغيل التطبيق والتحقق من النتيجة

ابنِ المشروع وشغّله:

```bash
dotnet run
```

بافتراض أنك وضعت خمس ملفات PNG مسماة `page1.png` … `page5.png` في المجلد المحدد، يجب أن ترى شيئًا مشابهًا لـ:

```
--- Page 1 ---
Invoice #12345
Date: 2026-05-01
Total: $1,250.00

--- Page 2 ---
Thank you for your purchase!
...

```

إذا حصلت على سلسلة فارغة، تأكد من أن الصور تحتوي على **نص قابل للتعرف** (تباين واضح، ليست صورة ضبابية لعلامة). يعمل Aspose OCR بأفضل شكل مع مسحات عالية الجودة—يفضل 300 dpi أو أعلى.

> **مثال صورة**  
> ![مثال إخراج التعرف على النص من PNG](https://example.com/ocr-output.png "إخراج التعرف على النص من PNG – مخرجات وحدة التحكم")

---

## الخطوة 4: المشكلات الشائعة عند **استخراج النص من الصفحات الممسوحة**

| العَرَض | السبب المحتمل | الحل |
|--------|---------------|------|
| إخراج فارغ | الصورة منخفضة التباين أو مشوشة | عالج مسبقًا باستخدام Aspose.Imaging (تثبيت الثنائيات، تصحيح الميل). |
| أحرف مشوهة | اللغة غير مضبوطة (الافتراضية هي الإنجليزية) | `engine.Configuration.Language = Language.English;` أو اضبطها إلى `Language.French`، إلخ. |
| استثناء *“File not found”* | مسار المجلد غير صحيح أو امتداد الملف مفقود | استخدم `Path.Combine(basePath, $"page{i+1}.png")` للسلامة. |
| خطأ ترخيص بعد عدة صفحات | استخدام ترخيص تجريبي بدون `MaxPagesInEvaluation` | إما شراء ترخيص أو الإبقاء على سطر `MaxPagesInEvaluation`. |

هذه النصائح تحافظ على سلاسة سير عمل **استخراج النص من الصفحات الممسوحة** حتى عندما لا تكون المادة المصدرية مثالية.

---

## الخطوة 5: متقدم – توسيع النطاق لمئات الصور

إذا كنت تحتاج إلى **إجراء OCR على الصور** المخزنة في قاعدة بيانات أو دلو سحابي، استبدل حلقة `for` بـ `foreach` على مجموعة من مسارات الملفات:

```csharp
string[] pngFiles = Directory.GetFiles(basePath, "*.png");
foreach (var file in pngFiles)
{
    engine.Image = ImageStream.FromFile(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(engine.Recognize());
}
```

يمكنك أيضًا تمكين **المعالجة المتعددة الخيوط** (Aspose OCR آمن للاستخدام المتعدد الخيوط) لتسريع المعالجة على الأجهزة متعددة النوى:

```csharp
Parallel.ForEach(pngFiles, file =>
{
    var localEngine = new OcrEngine(); // each thread gets its own engine
    localEngine.Image = ImageStream.FromFile(file);
    string text = localEngine.Recognize();
    lock (Console.Out) // avoid garbled console output
    {
        Console.WriteLine($"--- {Path.GetFileName(file)} ---");
        Console.WriteLine(text);
    }
    localEngine.Dispose();
});
```

تذكر تفريغ كل نسخة من المحرك؛ وإلا ستسرب الذاكرة الأصلية.

---

## الخطوة 6: ما بعد PNG – صيغ أخرى وملفات PDF

Aspose OCR لا يقتصر على PNG. يمكنك تمرير JPEG، BMP، TIFF، أو حتى **صفحات PDF** (عن طريق تحويلها إلى صور أولًا). بالنسبة للـ PDF، اجمع بين Aspose.PDF وAspose.OCR:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;

// Load PDF, render each page to a PNG stream, then OCR
Document pdf = new Document("sample.pdf");
for (int pageNum = 1; pageNum <= pdf.Pages.Count; pageNum++)
{
    using var imgStream = new MemoryStream();
    var rasterizer = new PngDevice();
    rasterizer.Process(pdf.Pages[pageNum], imgStream);
    imgStream.Position = 0;

    engine.Image = ImageStream.FromStream(imgStream);
    Console.WriteLine($"--- PDF Page {pageNum} ---");
    Console.WriteLine(engine.Recognize());
}
```

هذا المقتطف يوضح كيف يمكنك **استخراج النص من الصفحات الممسوحة** التي تأتي كملفات PDF—سيناريو شائع في خطوط معالجة الفواتير.

---

## ملخص وخطوات تالية

غطّينا دورة الحياة الكاملة لـ **التعرف على النص من PNG** باستخدام Aspose OCR:

1. تثبيت حزمة NuGet.  
2. تهيئة `OcrEngine`.  
3. (اختياري) ضبط حد الصفحات لوضع التقييم.  
4. تحميل كل PNG عبر `ImageStream.FromFile`.  
5. استدعاء `Recognize()` وعرض النتيجة.

## دروس ذات صلة

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}