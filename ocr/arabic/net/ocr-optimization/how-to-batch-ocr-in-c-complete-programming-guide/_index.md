---
category: general
date: 2026-05-31
description: كيفية تنفيذ التعرف الضوئي على الحروف (OCR) على دفعات في C# باستخدام Aspose
  OCR. تعلم تحويل الصور إلى نص، استخراج النص من الصور، ومعالجة ملفات متعددة بكفاءة.
draft: false
keywords:
- how to batch OCR
- convert images to text
- extract text from images
- OCR multiple files
- batch OCR processing
language: ar
og_description: كيفية تنفيذ OCR على دفعات في C# باستخدام Aspose OCR. تحويل الصور إلى
  نص، استخراج النص من الصور، ومعالجة ملفات OCR المتعددة بسهولة.
og_title: كيفية تنفيذ OCR دفعيًا في C# – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  headline: How to Batch OCR in C# – Complete Programming Guide
  type: TechArticle
- description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  name: How to Batch OCR in C# – Complete Programming Guide
  steps:
  - name: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
    text: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
  - name: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
    text: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
  - name: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
    text: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- batch-processing
title: كيفية تنفيذ OCR دفعةً في C# – دليل برمجة شامل
url: /ar/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعيًا في C# – دليل برمجة شامل

هل تساءلت يومًا **كيف تقوم بعمل OCR دفعي** لمجلد كامل من الصور الممسوحة ضوئيًا دون فتح كل ملف يدويًا؟ لست وحدك. في العديد من المشاريع الواقعية—فكر في أتمتة الفواتير أو أرشفة الصور التاريخية—تحتاج إلى **تحويل الصور إلى نص** على نطاق واسع، والقيام بذلك ملفًا بملف هو مضيعة ضخمة للوقت.

في هذا الدرس سنستعرض تطبيقًا جاهزًا لتشغيله في وحدة تحكم C# يأخذ كل ملفات PNG أو JPG أو TIFF في دليل المصدر، يشغل Aspose OCR على كلٍ منها، ويضع ملف *.txt* مطابق في مجلد الإخراج. بنهاية الدرس ستكون قادرًا على **استخراج النص من الصور**، ومعالجة **OCR لملفات متعددة**، وستمتلك قاعدة صلبة لأي **معالجة OCR دفعية** قد تحتاجها لاحقًا.

## ما ستتعلمه

- إعداد مشروع .NET مع حزمة NuGet الخاصة بـ Aspose OCR.  
- تعريف مجلدات المصدر والوجهة لتشغيل **OCR دفعي**.  
- تعداد أنواع الصور المدعومة وإرسالها إلى محرك OCR.  
- كتابة النص المستخرج إلى ملفات *.txt* منفصلة، مما يحقق **تحويل الصور إلى نص**.  
- التعامل مع المشكلات الشائعة مثل المجلدات المفقودة، الصيغ غير المدعومة، وتحسينات الأداء.

لا تحتاج إلى خبرة سابقة مع Aspose؛ فقط فهم أساسي لـ C# وVisual Studio سيكفيك.

---

![مخطط يوضح تدفق معالجة OCR الدفعي من مجلد الصور إلى مخرجات النص – كيفية تنفيذ OCR دفعيًا](/images/batch-ocr-flow.png){alt="مخطط تدفق كيفية تنفيذ OCR دفعيًا"}

## كيفية تنفيذ OCR دفعي – إعداد المشروع

قبل أن نغوص في الكود، تأكد من وجود ما يلي:

1. **.NET 6 SDK** (أو أحدث) مثبت – أحدث نسخة من وقت التشغيل تمنحك أداءً أفضل ودعمًا أصليًا للـ async I/O.  
2. **Visual Studio 2022** (الإصدار المجتمعي يعمل جيدًا) أو أي محرر تفضله.  
3. حزمة **Aspose.OCR** من NuGet. قم بتثبيتها عبر وحدة التحكم الخاصة بمدير الحزم:

   ```powershell
   Install-Package Aspose.OCR
   ```

هذا كل شيء. باقي الدرس يفترض أن الحزمة مضافة بشكل صحيح إلى المشروع.

## الخطوة 2: إعداد مجلدات المصدر والوجهة (تحويل الصور إلى نص)

أولاً، نحتاج إلى مجلدين: أحدهما يحتوي على الصور الأصلية والآخر حيث ستُحفظ ملفات *.txt* المُولدة. الكود أدناه ينشئ مجلد الوجهة إذا لم يكن موجودًا مسبقًا—دون أي خطوات يدوية.

```csharp
// Define where the images live and where the text files will go
string sourceFolder = @"C:\OCR\Batch";
string outputFolder = @"C:\OCR\BatchTxt";

// Ensure the output directory exists; CreateDirectory is idempotent
Directory.CreateDirectory(outputFolder);
```

> **لماذا هذا مهم:** إذا تخطيت استدعاء `CreateDirectory`، سيتسبب البرنامج في رمي استثناء `DirectoryNotFoundException` في اللحظة التي يحاول فيها كتابة أول ملف نصي. بمعالجة ذلك مسبقًا، تجعل عملية OCR الدفعي أكثر موثوقية.

## الخطوة 3: تعداد ملفات الصور لمعالجة OCR لملفات متعددة

بعد ذلك، نجمع كل ملف يطابق الصيغ التي ندعمها. استخدام LINQ يبقي الكود مختصرًا مع الحفاظ على قابليته للقراءة.

```csharp
// Grab all PNG, JPG, and TIFF files from the source folder (non‑recursive)
var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
    .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));
```

> **نصيحة:** إذا احتجت لاحقًا إلى معالجة ملفات PDF أو BMP، ما عليك سوى توسيع شرط `Where`. إبقاء الفلتر في مكان واحد يجعل التعديلات المستقبلية سهلة.

## الخطوة 4: تشغيل محرك OCR على كل صورة (كيفية تنفيذ OCR دفعي)

الآن نصل إلى جوهر العملية: تمرير كل صورة إلى Aspose OCR واستخراج النص المعترف به. الحلقة أدناه تنشئ كائن `OcrEngine` جديد لكل ملف—هذا يضمن تحرير الذاكرة المستخدمة من الصورة السابقة قبل بدء معالجة التالية.

```csharp
foreach (var imagePath in imageFiles)
{
    // Initialize the OCR engine with the current image
    OcrEngine ocrEngine = new OcrEngine
    {
        Image = ImageStream.FromFile(imagePath)
    };

    // Perform recognition; Recognize() returns an OcrResult object
    OcrResult ocrResult = ocrEngine.Recognize();

    // Build the output .txt file path (same base name, .txt extension)
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    // Persist the extracted text
    File.WriteAllText(textFilePath, ocrResult.Text);

    Console.WriteLine($"Processed {Path.GetFileName(imagePath)} → {Path.GetFileName(textFilePath)}");
}
```

**ما الذي يحدث؟**  

- `ImageStream.FromFile` يحمل الصورة إلى تدفق يمكن لـ Aspose قراءته.  
- `ocrEngine.Recognize()` ينفّذ خوارزمية OCR الفعلية، ويعيد سلسلة نصية في `ocrResult.Text`.  
- `File.WriteAllText` يكتب تلك السلسلة إلى القرص، مما يحقق **استخراج النص من الصور**.

### معالجة الحالات الخاصة

- **الصور التالفة** – غلف استدعاء التعرف داخل `try/catch` وسجّل الفشل، ثم استمر في الملف التالي.  
- **دفعات كبيرة** – فكر في معالجة الملفات بشكل غير متزامن باستخدام `Parallel.ForEach` إذا كان لديك جهاز متعدد النوى.  
- **لغات مختلفة** – اضبط `ocrEngine.Language = Language.English;` أو أي لغة مدعومة أخرى قبل استدعاء `Recognize()`.

## الخطوة 5: حفظ النص المستخرج (استخراج النص من الصور)

المقتطف السابق بالفعل يحفظ ناتج OCR، لكن دعنا نفصل تلك المنطق في طريقة مساعدة. هذا يجعل الحلقة الرئيسية أنظف ويشجع على إعادة الاستخدام.

```csharp
static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
{
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    File.WriteAllText(textFilePath, recognizedText);
}
```

بعد ذلك استبدل استدعاء `File.WriteAllText` المضمن بـ:

```csharp
SaveOcrResult(outputFolder, imagePath, ocrResult.Text);
```

> **لماذا نفصل هذا في طريقة؟** لأنه يفصل بين المسؤوليات—التعرف مقابل الحفظ—ويمنحك مكانًا واحدًا لإضافة معالجة لاحقة (مثل قص الفراغات أو إلحاق الطوابع الزمنية).

## مثال كامل يعمل – معالجة OCR دفعي في C#

بدمج جميع الأجزاء، إليك برنامج مستقل يمكنك نسخه ولصقه في مشروع تطبيق وحدة تحكم جديد وتشغيله فورًا.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Define source & destination folders
            string sourceFolder = @"C:\OCR\Batch";
            string outputFolder = @"C:\OCR\BatchTxt";

            // 2️⃣ Make sure the output folder exists
            Directory.CreateDirectory(outputFolder);

            // 3️⃣ Get all supported image files (convert images to text)
            var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
                .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));

            // 4️⃣ Process each image (how to batch OCR)
            foreach (var imagePath in imageFiles)
            {
                try
                {
                    // Initialise OCR engine for the current file
                    OcrEngine ocrEngine = new OcrEngine
                    {
                        Image = ImageStream.FromFile(imagePath)
                    };

                    // Run OCR – this extracts text from images
                    OcrResult result = ocrEngine.Recognize();

                    // 5️⃣ Save the result (extract text from images)
                    SaveOcrResult(outputFolder, imagePath, result.Text);

                    Console.WriteLine($"✅ {Path.GetFileName(imagePath)} processed.");
                }
                catch (Exception ex)
                {
                    // Gracefully handle problematic files
                    Console.WriteLine($"⚠️ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }

            Console.WriteLine("🎉 Batch OCR processing complete!");
        }

        // Helper to write the OCR output to a .txt file
        static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
        {
            string textFilePath = Path.Combine(outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, recognizedText);
        }
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج، ستظهر سطور في وحدة التحكم مشابهة لـ:

```
✅ invoice001.png processed.
✅ receipt123.jpg processed.
✅ map.tif processed.
🎉 Batch OCR processing complete!
```

في الوقت نفسه، سيحتوي المجلد `C:\OCR\BatchTxt` على:

- `invoice001.txt`
- `receipt123.txt`
- `map.txt`

كل ملف يحمل تمثيل النص العادي لصورته الأصلية، جاهز للفهرسة أو البحث أو التحليلات اللاحقة.

## نصائح احترافية ومشكلات شائعة (معالجة OCR دفعي)

- **إدارة الذاكرة:** Aspose OCR يحرّر مخازن الصور بعد كل استدعاء `Recognize()`، لكن إذا عالجت آلاف الملفات، فكر في استدعاء `GC.Collect()` بشكل مقتصد للحفاظ على حجم الذاكرة منخفضًا.  
- **زيادة السرعة:** استخدم `OcrEngine.RecognizeAsync()` في .NET 6+ وأطلق مهامًا متعددة باستخدام `Task

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

- [كيفية تنفيذ OCR دفعي للصور باستخدام List في Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [استخراج النص من الصور باستخدام عملية OCR على المجلدات](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [كيفية تنفيذ OCR على صور الأرشيف باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}