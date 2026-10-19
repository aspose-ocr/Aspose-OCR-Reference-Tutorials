---
category: general
date: 2026-04-26
description: استخراج النص من ملفات PNG بسرعة باستخدام C#. تعلّم كيفية تحويل الصور
  إلى نص، قراءة ملفات PNG، التكرار عبر الصور ومعالجة OCR للصور دفعةً في دقائق.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: ar
og_description: استخراج النص من ملفات PNG بسرعة باستخدام C#. يوضح هذا الدليل كيفية
  تحويل الصور إلى نص، قراءة ملفات PNG، التكرار عبر الصور ومعالجة OCR للصور دفعةً.
og_title: استخراج النص من PNG – دليل OCR دفعي كامل بلغة C#
tags:
- C#
- OCR
- Aspose
title: استخراج النص من PNG – دليل OCR كامل للمعالجة الدفعية بلغة C#
url: /ar/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من PNG – دليل OCR دفعي كامل بلغة C#

هل احتجت يوماً إلى **استخراج النص من ملفات PNG** لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—الكثير من المطورين يواجهون هذه المشكلة عندما يجربون OCR لأول مرة على مجلد من لقطات الشاشة. الخبر السار هو أنه ببضع أسطر من C# و Aspose OCR يمكنك تحويل الصور إلى نص، قراءة ملفات PNG، التكرار عبر الصور، ومعالجة كل ذلك دفعة واحدة.

في هذا الدليل سنستعرض تطبيقًا جاهزًا من نوع console يقوم بذلك بالضبط. في النهاية ستحصل على حل مستقل يقتطف النص من كل ملف PNG في دليل ما ويضع ملف `.txt` مطابق بجانب كل صورة. لا سكربتات إضافية، لا نسخ‑لصق يدوي—فقط كود نقي.

## ما الذي ستحتاجه

- **.NET 6 SDK** (أو أي نسخة أحدث من .NET). إنه مجاني، سريع، ويعمل في كل مكان.  
- **Aspose.OCR for .NET** (حزمة NuGet). المكتبة تشمل تسريع GPU إذا كان لديك GPU متوافق، لكنها تعود تلقائيًا إلى CPU إذا لم يتوفر.  
- مجلد يحتوي على مجموعة من **صور PNG** التي تريد معالجتها.  
- محرر نصوص أو بيئة تطوير—Visual Studio، VS Code، Rider—أيا كان تفضله.

هذا كل شيء. إذا كان لديك هذه المتطلبات، فأنت جاهز للبدء.

![extract text from png example](image.png "لقطة شاشة توضيحية لاستخراج النص من PNG")

*نص بديل للصورة: “استخراج النص من PNG باستخدام C# OCR دفعي”*

## الخطوة 1 – إعداد المشروع وتثبيت Aspose.OCR

أولاً، أنشئ مشروع console جديد وأضف حزمة Aspose OCR.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

لماذا نستخدم تطبيق console؟ لأنه أبسط بيئة لتشغيل مهام الدفعات، ويمكن تشغيله من سطر الأوامر أو جدولته باستخدام أداة جدولة. إذا احتجت لاحقًا إلى واجهة مستخدم، يمكنك نقل المنطق الأساسي إلى مكتبة فئات.

## الخطوة 2 – تهيئة محرك OCR مسرّع بـ GPU (أو fallback إلى CPU)

توفر Aspose محرك `GpuOcrEngine` الذي يكتشف تلقائيًا GPU مدعوم. إذا لم يُعثر على أي GPU، يعود إلى محرك CPU العادي—بدون الحاجة إلى كتابة كود إضافي.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**نصيحة محترف:** إذا كنت تعمل على خادم بدون شاشة ولا يحتوي على GPU، يمكنك استبدال `GpuOcrEngine` بـ `OcrEngine` وسيعمل الكود بنفس الطريقة.

## الخطوة 3 – التكرار عبر الصور في الدليل المستهدف

نحتاج إلى **التكرار عبر الصور** واختيار ملفات PNG فقط. طريقة `Directory.GetFiles` تقوم بالعمل الشاق، وسنضيف فحصًا لتجنب المجلد الفارغ.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

لاحظ استخدام `SearchOption.TopDirectoryOnly`. إذا احتجت لاحقًا إلى التعمق داخل المجلدات الفرعية، ما عليك سوى التحويل إلى `AllDirectories`. هذا التغيير الصغير يتيح لك **تحويل الصور إلى نص** عبر شجرة كاملة بسطر واحد.

## الخطوة 4 – تنفيذ OCR وحفظ النتيجة

الآن يأتي الجزء الأساسي من سير عمل **معالجة OCR دفعيًا للصور**. نقوم بتحميل كل PNG، تشغيل `Recognize()`، ثم كتابة النص المستخرج إلى ملف `.txt` يحمل نفس الاسم الأساسي.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**لماذا نغلفه بـ try/catch؟** مجموعات الصور الواقعية غالبًا ما تحتوي على ملف تالف أو PNG يستخدم ملف تعريف ألوان غير شائع. التقاط الاستثناء يمنع تعطل العملية بالكامل ويسمح بالاستمرار في معالجة باقي الملفات.

## الخطوة 5 – تشغيل التطبيق والتحقق من المخرجات

قم ببناء وتشغيل التطبيق:

```bash
dotnet run
```

يجب أن ترى سجل console مشابهًا لـ:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

افتح أي من ملفات `.txt` التي تم إنشاؤها—ستجد النص المستخرج. إذا كان الملف فارغًا، تحقق من جودة الصورة؛ OCR يعمل بأفضل شكل مع نص واضح وعالي التباين.

### سكربت تحقق سريع (اختياري)

إذا أردت التأكد من أن كل PNG حصل على ملف نصي مطابق، شغّل سطر PowerShell الصغير التالي:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## حالات شائعة وتحديات خاصة

| الحالة | ما الذي يجب تغييره |
|-----------|----------------|
| **لغات غير لاتينية** (مثل السيريالية) | اضبط `ocrEngine.Language = Language.Cyrillic;` |
| **مجموعة صور كبيرة (>10 000 ملف)** | استخدم `Parallel.ForEach` لتسريع المعالجة، لكن راقب استهلاك ذاكرة GPU. |
| **الحاجة للحفاظ على ترتيب الصور الأصلي** | رتب `pngFiles` قبل حلقة `foreach` (`Array.Sort(pngFiles);`). |
| **التشغيل على خادم CI بدون GPU** | استبدل `GpuOcrEngine` بـ `OcrEngine` لتجنب أخطاء تهيئة GPU. |
| **تريد معالجة الملفات التي تحتوي على كلمة مفتاحية معينة فقط** | بعد الحصول على `result.Text`، تحقق من `result.Text.Contains("Invoice")` قبل كتابة الملف. |

هذه التعديلات تسمح لك بتكييف **تحويل الصور إلى نص** لتناسب أي سيناريو قد تواجهه.

## الشيفرة الكاملة (جاهزة للنسخ واللصق)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

احفظها باسم `Program.cs`، شغّل `dotnet run`، وشاهد السحر يحدث.

## الخلاصة

الآن لديك **طريقة كاملة وجاهزة للإنتاج لاستخراج النص من ملفات PNG** باستخدام C#. غطى الدليل كل شيء—من إعداد المشروع، تهيئة محرك OCR مسرّع بـ GPU، **التكرار عبر الصور**، إلى **معالجة OCR دفعيًا للصور** وحفظ النتائج كنص عادي.

إذا كنت ترغب في الخطوات التالية، جرّب:

- **تحويل الصور إلى نص** لصيغ أخرى (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}