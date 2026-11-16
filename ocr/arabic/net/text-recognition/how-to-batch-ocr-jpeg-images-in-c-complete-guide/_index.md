---
category: general
date: 2026-02-22
description: كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) للصور JPEG دفعيًا في C# باستخدام
  Aspose.OCR. تعلم استخراج النص من ملفات jpg، تحويل jpg إلى txt، ومعالجة الصور دفعيًا
  بكفاءة.
draft: false
keywords:
- how to batch ocr
- extract text from jpg
- convert jpg to txt
- batch process images
- c# ocr example
language: ar
og_description: كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) لصور JPEG دفعيًا في C#
  باستخدام Aspose.OCR. يوضح هذا الدرس كيفية استخراج النص من ملفات JPG، تحويل JPG إلى
  TXT، ومعالجة الصور دفعيًا في دقائق.
og_title: كيفية تنفيذ OCR دفعي لصور JPEG في C# – دليل شامل
tags:
- OCR
- C#
- Aspose
- Image Processing
title: كيفية تنفيذ OCR لصور JPEG دفعة واحدة في C# – دليل كامل
url: /ar/net/text-recognition/how-to-batch-ocr-jpeg-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعي لصور JPEG في C# – دليل كامل

هل تساءلت يومًا **كيف تقوم بعمل OCR دفعي** لمجلد مليء بالصور دون كتابة برنامج منفصل لكل ملف؟ في هذا الدليل سنوضح لك بالضبط **كيف تقوم بعمل OCR دفعي** لملفات JPEG باستخدام Aspose.OCR، بحيث يمكنك **استخراج النص من jpg** و**تحويل jpg إلى txt** ببضع أسطر من الشيفرة.  

إذا كنت قد حدقت يومًا في دليل يحتوي على فواتير ممسوحة ضوئيًا وفكرت، “يجب أن تكون هناك طريقة أسرع”، فأنت في المكان المناسب. سنستعرض كل خطوة، نشرح لماذا كل جزء مهم، ونضيف بعض النصائح الاحترافية للتعامل مع دفعات كبيرة.

## ما ستبنيه

بحلول نهاية هذا الدرس ستحصل على تطبيق console صغير يقوم بـ:

* يفحص دليلًا محددًا للبحث عن ملفات `*.jpg`.  
* يرسل كل صورة عبر محرك Aspose OCR (مع تسريع GPU إذا كان لديك بطاقة مناسبة).  
* يكتب النص المعترف به إلى ملف `.txt` يقع بجوار الصورة الأصلية.  

بدون خدمات خارجية، بدون نسخ‑لصق يدوي—فقط C# نقي ومكتبة OCR موثوقة.

### المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل على .NET Framework 4.8 أيضًا).  
* Visual Studio 2022 أو أي محرر يدعم C#.  
* حزمة Aspose.OCR NuGet (الإصدار التجريبي المجاني يعمل للاختبار).  

إذا كنت تفتقد أيًا من هذه المتطلبات، توقف الآن وقم بتثبيتها؛ باقي الدليل يفترض أنها موجودة بالفعل.

![How to batch OCR example](/images/how-to-batch-ocr.png "how to batch ocr diagram")

## الخطوة 1: تثبيت حزمة Aspose.OCR NuGet

أولاً وقبل كل شيء—مشروعك يحتاج مكتبة OCR. افتح طرفية في مجلد الحل وشغّل:

```bash
dotnet add package Aspose.OCR
```

أو استخدم واجهة مدير الحزم NuGet في Visual Studio. هذا سيجلب كل ما تحتاجه، بما في ذلك الثنائيات المدعومة بـ GPU إذا كان جهازك يدعمها.

> **نصيحة احترافية:** إذا كنت تخطط لتشغيل هذا على خادم بدون GPU، عيّن `UseGpu = false` لاحقًا؛ سيعود المحرك إلى استخدام CPU تلقائيًا.

## الخطوة 2: تكوين محرك OCR

إنشاء وتكوين `OcrEngine` هو المكان الذي يبدأ فيه السحر. ستخبر المحرك بأي لغة يتوقعها، ما إذا كان سيستخدم GPU، وما هو تنسيق الإخراج المطلوب.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 2: Initialize and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most documents; change if you need another language.
    Language = Language.English,

    // Enable GPU for faster processing on supported hardware.
    UseGpu = true,

    // We only need plain text for our .txt files.
    OutputFormat = OutputFormat.Text
};
```

**لماذا هذا مهم:** ضبط `Language` يحسن الدقة لأن المحرك يمكنه تضييق مجموعة الأحرف. تمكين `UseGpu` يمكن أن يقلل وقت المعالجة إلى النصف على بطاقة رسومية حديثة، وهو فوز حقيقي عندما تقوم **بمعالجة دفعات من الصور**.

## الخطوة 3: التعرف على جميع ملفات JPEG في مجلد

الآن نترك Aspose يقوم بالعمل الشاق. الطريقة الساكنة `BatchProcessor.RecognizeFolder` تتجول في الدليل، تشغل OCR على كل ملف مطابق، وتعيد مجموعة من النتائج.

```csharp
using System.Collections.Generic;

// ...

// Step 3: Run OCR on every *.jpg in the target directory
IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
    ocrEngine,
    @"C:\Images\Invoices",   // <-- replace with your folder path
    searchPattern: "*.jpg"); // Only JPEG files are processed
```

**معالجة الحالات الطرفية:** إذا كان المجلد يحتوي على مجلدات فرعية، يمكنك إضافة تحميل `SearchOption.AllDirectories` (أو التكرار يدويًا) لضمان عدم تفويت أي ملف.

## الخطوة 4: كتابة كل نتيجة إلى ملف `.txt` مطابق

كائنات `OcrResult` تحتوي على مسار الملف الأصلي والنص المعترف به. قم بالتكرار عليها، غيّر الامتداد، واكتب النتيجة.

```csharp
using System.IO;

// ...

// Step 4: Persist OCR results as .txt files next to the source images
foreach (var result in ocrResults)
{
    // Change "image.jpg" → "image.txt"
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");

    // Save the extracted text
    File.WriteAllText(txtFilePath, result.Text);
}
```

هذا كل شيء—كل صورة JPEG الآن لديها ملف نصي شقيق يمكنك تمريره إلى عمليات ما بعد المعالجة، فهارس البحث، أو ببساطة أرشفته.

## الخطوة 5: تشغيل التطبيق والتحقق من المخرجات

قم بترجمة البرنامج وتشغيله:

```bash
dotnet run
```

بافتراض أن المجلد يحتوي على `invoice1.jpg` و `receipt2.jpg`، يجب أن ترى `invoice1.txt` و `receipt2.txt` يظهران بجانبهما. افتح أي من ملفات `.txt`؛ ستجد ناتج OCR الخام، على سبيل المثال:

```
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

إذا كان النص مشوشًا، تحقق مرة أخرى من أن الصور المصدرية ذات تباين عالي وأن خاصية `Language` تتطابق مع لغة المستند.

## الخطوة 6: تعديلات متقدمة (اختياري)

### أ) معالجة المسحات منخفضة الجودة

أحيانًا تكون ملفات JPEG صاخبة. يمكنك معالجة الصور مسبقًا باستخدام Aspose.Imaging أو أي مكتبة أخرى:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

// Example: increase contrast before OCR
using (var image = Image.Load(result.SourceFilePath))
{
    image.Contrast = 30; // boost contrast
    image.Save(result.SourceFilePath); // overwrite or save to temp file
}
```

### ب) تشغيل الدفعة بالتوازي

إذا كان لديك العديد من الملفات ومعالج متعدد النوى، غلف الحلقة بـ `Parallel.ForEach`:

```csharp
Parallel.ForEach(ocrResults, result =>
{
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
    File.WriteAllText(txtFilePath, result.Text);
});
```

كن على علم بأن محرك Aspose OCR نفسه غير آمن للاستخدام المتعدد الخيوط؛ ستحتاج إلى إنشاء نسخة `OcrEngine` منفصلة لكل خيط أو استخدام طابور متزامن.

### ج) التسجيل ومعالجة الأخطاء

حل قوي يسجل الفشل حتى تتمكن من إعادة المحاولة لاحقًا:

```csharp
try
{
    // OCR and write logic here
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {result.SourceFilePath}: {ex.Message}");
    // Optionally write to a log file
}
```

## مثال عملي كامل

بدمج كل ما سبق، إليك البرنامج الكامل الذي يمكنك نسخه‑ولصقه في تطبيق Console جديد:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = Language.English,
            UseGpu = true,
            OutputFormat = OutputFormat.Text
        };

        // 2️⃣ Recognize all JPEG images in the target folder
        IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
            ocrEngine,
            @"C:\Images\Invoices",   // <-- change to your directory
            searchPattern: "*.jpg");

        // 3️⃣ Write each OCR result to a matching .txt file
        foreach (var result in ocrResults)
        {
            string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
            File.WriteAllText(txtFilePath, result.Text);
        }

        Console.WriteLine("Batch OCR complete. Check the folder for .txt files.");
    }
}
```

شغّله، راقب مخرجات الـ console، ثم افتح بعض ملفات `.txt` لتؤكد أن خطوة **استخراج النص من jpg** نجحت.  

---

## الخاتمة

لقد غطينا للتو **كيفية تنفيذ OCR دفعي** لمجموعة من صور JPEG في C# باستخدام Aspose.OCR، محولين كل صورة إلى ملف `.txt` قابل للبحث. الحل مدمج، يدعم GPU، وسهل التوسيع لمعالجة الأخطاء، معالجة الصور مسبقًا، أو التنفيذ المتوازي.  

إذا كنت مستعدًا للمزيد، فكر في الخطوات التالية:

* **معالجة دفعة من الصور** بصيغ أخرى (`*.png`, `*.tif`) عن طريق تعديل `searchPattern`.  
* دمج المخرجات مع محرك بحث نص كامل مثل Lucene.NET للبحث الفوري عن المستندات.  
* استكشاف ميزات تحويل PDF في Aspose لإنشاء ملفات PDF قابلة للبحث مباشرة من نتائج OCR.  

لا تتردد في التجربة—غيّر اللغة، أوقف تشغيل GPU، أو صل النص بقاعدة بيانات. النمط الأساسي يبقى هو نفسه، والآن لديك أساس صلب للبناء عليه.

برمجة سعيدة، ولتكن خطوط أنابيب OCR لديك سريعة ودقيقة دائمًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}