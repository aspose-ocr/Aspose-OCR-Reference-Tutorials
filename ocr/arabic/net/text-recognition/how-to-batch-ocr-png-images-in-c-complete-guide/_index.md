---
category: general
date: 2026-04-26
description: كيفية إجراء التعرف الضوئي على الحروف (OCR) لصور PNG دفعة واحدة بسرعة.
  تعلّم استخراج النص من PNG، تحويل الصور إلى نص، كتابة النص المُعترف به، وقراءة دليل
  PNG باستخدام Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: ar
og_description: كيفية إجراء التعرف الضوئي على الأحرف (OCR) لصور PNG دفعيًا في C# باستخدام
  Aspose OCR. يوضح هذا الدليل كيفية استخراج النص من PNG، تحويل الصور إلى نص، وكتابة
  النص المعترف به بكفاءة.
og_title: كيفية تنفيذ OCR دفعي لصور PNG في C# – خطوة بخطوة
tags:
- OCR
- C#
- Aspose
title: كيفية تنفيذ OCR لصور PNG دفعةً في C# – دليل شامل
url: /ar/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعي لصور PNG في C# – دليل كامل

هل تساءلت يومًا **كيف تقوم بعمل OCR دفعي** لمجلد كامل من ملفات PNG دون كتابة برنامج منفصل لكل صورة؟ لست الوحيد الذي يتعامل مع العشرات من لقطات الشاشة، الإيصالات الممسوحة ضوئيًا، أو الرسومات التي تحتاج إلى تحويلها إلى نص قابل للبحث. في هذا الدرس سنستعرض حلًا عمليًا **يستخرج النص من PNG**، **يحول الصور إلى نص**، و**يكتب النص المُعترف به** إلى ملفات منفصلة—كل ذلك أثناء قراءة دليل PNG تلقائيًا.

بنهاية هذا الدليل ستحصل على تطبيق C# Console جاهز للتشغيل يعالج أي عدد من الصور دفعة واحدة. لا سكريبتات إضافية، لا نسخ‑لصق يدوي—فقط كود نقي يقوم بالعمل الشاق نيابة عنك.

## ما ستحتاجه

- **.NET 6.0** أو أحدث (الكود يعمل جيدًا على .NET Framework أيضًا).  
- حزمة **Aspose.OCR for .NET** عبر NuGet (الإصدار التجريبي المجاني يعمل للاختبار).  
- مجلد يحتوي على عدد قليل من ملفات *.png* التي تريد إجراء OCR لها.  
- Visual Studio 2022 أو أي بيئة تطوير C# تفضلها.

إذا كان لديك هذه المتطلبات، يمكننا القفز مباشرة إلى التنفيذ.

## الخطوة 1 – إعداد مجلدات الإدخال والإخراج *(قراءة دليل PNG)*

أول شيء نفعله هو توجيه البرنامج إلى المجلد الذي يحتوي على الصور وتحديد المكان الذي ستُحفظ فيه ملفات *.txt* الناتجة. استخدام `Directory.GetFiles` يمنحنا مجموعة قابلة للتعداد من جميع ملفات PNG في الدليل.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**لماذا هذا مهم:**  
- استخدام حرف البدل (`*.png`) يضمن أننا نعالج ملفات الصور فقط، متجاهلين أي مستندات عشوائية.  
- إنشاء مجلد الإخراج تلقائيًا يمنع حدوث `DirectoryNotFoundException` لاحقًا.

> **نصيحة احترافية:** إذا كنت بحاجة لدعم صيغ أخرى (JPEG, BMP)، فقط قم بتوسيع نمط البحث أو استدعِ `Directory.EnumerateFiles` مع امتدادات متعددة.

## الخطوة 2 – تهيئة محرك OCR *(تحويل الصور إلى نص)*

تأتي Aspose.OCR مع نوعين من المحركات: `OcrEngine` المعتمد على وحدة المعالجة المركزية CPU و`GpuOcrEngine` المعجل بوحدة معالجة الرسوميات GPU. بالنسبة لمعظم وظائف الدفعات، محرك الـ CPU كافٍ تمامًا، لكن يمكنك استبدال اسم الصنف إذا كان لديك GPU قوي.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**لماذا هذا مهم:**  
- تحديد اللغة يحسن الدقة بشكل كبير لأن المحرك يعرف مجموعة الأحرف المتوقعة.  
- التحويل إلى `GpuOcrEngine` هو تعديل سطر واحد إذا واجهت عنق زجاجة في الأداء عند دفعات كبيرة.

## الخطوة 3 – إنشاء Batch Recogniser

توفر Aspose صنف `BatchRecognizer` المريح الذي يقبل مجموعة من مسارات الملفات ويُعيد النتائج واحدة تلو الأخرى. هذا يتجنب تحميل جميع الصور في الذاكرة مرة واحدة—وهي تفاصيل حاسمة للمجلدات الكبيرة.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**لماذا هذا مهم:**  
- مُعرّف الـ batch recogniser ي encapsulates منطق الحلقة، مما يسمح لنا بالتركيز على ما يجب فعله مع كل نتيجة بدلاً من كيفية التكرار بأمان.

## الخطوة 4 – تشغيل OCR على جميع الصور وكتابة الناتج *(كتابة النص المُعترف به)*

الآن نقوم فعليًا بتنفيذ OCR. تُعيد طريقة `Recognize` كائنًا من النوع `IEnumerable<RecognitionResult>` حيث يحتوي كل نتيجة على النص المستخرج وبيانات وصفية أخرى.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**لماذا هذا مهم:**  
- استخدام `File.WriteAllText` يضمن حفظ النص بترميز UTF‑8 افتراضيًا، مما يحافظ على الأحرف الخاصة.  
- التسمية المتزايدة (`out_0.txt`, `out_1.txt`) تتطابق مع ترتيب المعالجة، وهو مفيد لتصحيح الأخطاء.

> **حالة خاصة:** إذا فشل أي صورة في الـ OCR (مثلاً ملف تالف)، سيكون `RecognitionResult.Text` فارغًا. يمكنك إضافة فحص بسيط داخل الحلقة لتسجيل الفشل:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## الخطوة 5 – جمع كل شيء معًا – مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في مشروع Console جديد. يتضمن توجيهات `using`، والتحقق من صحة المجلد، وواجهة Console صغيرة لتعرف متى تنتهي الدفعة.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**الإخراج المتوقع:**  
تشغيل البرنامج يطبع شيئًا مثل:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

## أسئلة شائعة ونصائح

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني إجراء OCR للمجلدات الفرعية أيضًا؟* | نعم—استبدل `Directory.GetFiles` بـ `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *ماذا لو احتجت لغة مختلفة؟* | قم بتعيين `ocrEngine.Language = Language.Spanish;` (أو أي قيمة enum مدعومة). |
| *كيف أتعامل مع دفعات ضخمة (آلاف الملفات)؟* | فكر في المعالجة على دفعات أو استخدم `Parallel.ForEach` مع درجة توازي محدودة لتجنب استنزاف الذاكرة. |
| *هل يكون الإخراج دائمًا UTF‑8؟* | `File.WriteAllText` يستخدم UTF‑8 بدون BOM افتراضيًا، وهو يعمل لمعظم اللغات اللاتينية. بالنسبة للخطوط الآسيوية قد تحتاج إلى تعيين `Encoding.UTF8` صراحةً. |
| *هل يمكنني الحصول على درجات الثقة؟* | `RecognitionResult` يوفّر الخاصية `Confidence`—يمكنك تسجيلها مع النص للتحكم في الجودة. |

## نظرة بصرية *(كيفية OCR دفعي – مخطط)*

![مخطط سير عمل OCR دفعي يُظهر مجلد الإدخال → OCR engine → batch recogniser → ملفات txt الناتجة](https://example.com/diagram-how-to-batch-ocr.png "كيفية OCR دفعي")

*نص alt يحتوي على الكلمة المفتاحية الأساسية، مما يلبي متطلبات تحسين محركات البحث للصور.*

## الخاتمة

لقد غطينا للتو **كيفية تنفيذ OCR دفعي** لدليل يحتوي على ملفات PNG باستخدام Aspose.OCR، بدءًا من قراءة دليل PNG وحتى كتابة كل ملف نص مُعترف به. الحل مكتمل ذاتيًا، يعمل على أي بيئة تشغيل .NET حديثة، ويمكن توسيعه لتسريع GPU، دعم متعدد اللغات، أو المعالجة المتوازية.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال `Language.Latin` بلغة أخرى، أو دمج الناتج في فهرس بحث لتصبح مستنداتك قابلة للبحث فورًا. السماء هي الحد عندما تتقن OCR الدفعي.

برمجة سعيدة، وأخبرني في التعليقات إذا واجهت أي مشاكل!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}