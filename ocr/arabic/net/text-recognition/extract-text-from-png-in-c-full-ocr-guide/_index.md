---
category: general
date: 2026-03-07
description: استخراج النص من ملفات PNG باستخدام C#. تعلم كيفية تحويل الصورة إلى نص
  باستخدام C# وقراءة النص من الصور الممسوحة ضوئياً بسرعة.
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: ar
og_description: استخراج النص من ملفات PNG باستخدام C#. يوضح هذا الدليل كيفية تحويل
  الصورة إلى نص باستخدام C# وقراءة النص من الصور الممسوحة ضوئياً باستخدام Aspose OCR.
og_title: استخراج النص من PNG في C# – دليل OCR كامل
tags:
- OCR
- C#
- Aspose
- Image Processing
title: استخراج النص من PNG في C# – دليل OCR كامل
url: /ar/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من PNG باستخدام C# – دليل OCR كامل

هل احتجت يومًا إلى **استخراج النص من PNG** لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—معظم المطورين يواجهون هذا التحدي عندما يصادفون رسومات ممسوحة ضوئيًا أو لقطات شاشة تحتاج إلى أن تصبح نصًا قابلاً للبحث. الخبر السار؟ ببضع أسطر من C# و Aspose OCR يمكنك تحويل أي PNG إلى سلاسل قابلة للتحرير في لحظة.

في هذا الدرس سنستعرض العملية بالكامل: من العثور على ملفات PNG على القرص، إلى تشغيل مهام OCR بشكل متوازي، ثم عرض معاينة مرتبة لكل نتيجة. بنهاية الدرس ستعرف كيف **تحويل الصورة إلى نص C#**، وستتمكن من **قراءة النص من الصور الممسوحة ضوئيًا** بكفاءة، وسترى أيضًا أفضل طريقة لـ **تشغيل OCR على الصور** دون إبطاء خيط واجهة المستخدم.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل على .NET Core و .NET Framework أيضًا)  
- حزمة NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- مجلد يحتوي على ملفات *.png* التي تريد معالجتها  
- أي بيئة تطوير تفضلها (Visual Studio، VS Code، Rider…)

لا يلزم أي إعداد إضافي؛ المكتبة تأتي مع كل ما يلزم لفك ترميز PNGs، JPEGs، TIFFs، وما إلى ذلك.

## الخطوة 1: تحديد جميع ملفات PNG – بدء **استخراج النص من PNG**

أولاً علينا العثور على كل ملف PNG نعتزم تشغيل OCR عليه. استخدام `Directory.GetFiles` سريع وموثوق.

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*لماذا هذا مهم:* فحص الدليل مرة واحدة يبقي بقية سير العمل بسيطًا، والفحص المبكر يمنع حالة “لا مخرجات” صامتة قد يصعب تتبعها لاحقًا.

## الخطوة 2: تشغيل مهام OCR متوازية – تشغيل **OCR على الصور** بكفاءة

تشغيل OCR بشكل متسلسل مناسب لعدد قليل من الملفات، لكن المشاريع الواقعية غالبًا ما تتعامل مع العشرات أو المئات. بإطلاق `Task` لكل صورة نحافظ على إشغال المعالج بينما تقوم المكتبة بالعمل الثقيل.

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*نصيحة محترف:* `Task.Run` يرسل العمل إلى مجموعة الخيوط، مما يعني أن واجهة المستخدم (إن وجدت) تظل سريعة الاستجابة. إذا كنت على خادم، فإن النمط نفسه يتوسع بشكل جيد عبر الأنوية.

## الخطوة 3: انتظار جميع المهام – جمع النتائج

الآن ننتظر انتهاء كل عملية OCR. `Task.WhenAll` تُعيد مصفوفة تتطابق مع ترتيب الملفات الأصلي، مما يسهل ربط النتائج بأسماء الملفات.

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*ملاحظة حالة حافة:* إذا أطلقت أي صورة استثناء (ملف تالف، تنسيق غير مدعوم) فإن `WhenAll` بالكامل سيُعيد الاستثناء. يمكنك تغليف `Task.Run` الداخلي داخل try/catch وإرجاع سلسلة فارغة أو رسالة تشخيصية إذا كنت تحتاج إلى تحمل الأخطاء.

## الخطوة 4: عرض معاينة – التحقق من مخرجات **تحويل الصورة إلى نص C#**

معاينة سريعة تساعدك على التأكد من أن OCR نجح قبل أن تبدأ بحفظ البيانات في مكان آخر.

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

مخرجات وحدة التحكم النموذجية تبدو هكذا:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

إذا أظهرت المعاينة نصًا غير مفهوم، تحقق مرة أخرى من جودة الصورة أو فكر في المعالجة المسبقة (مثل التحويل إلى ثنائي) – لكن بالنسبة لمعظم PNGs النظيفة، Aspose OCR ينجح من المحاولة الأولى.

## اختياري: حفظ النتائج إلى CSV – حالة استخدام واقعية

معظم المشاريع تحتاج النص المستخرج بصيغة منظمة. أدناه أداة صغيرة تكتب اسم الملف والنص الكامل من OCR إلى ملف CSV.

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

الآن يمكنك استيراد CSV إلى Excel أو Power BI أو أي نظام لاحق يتوقع **قراءة النص من الصور الممسوحة ضوئيًا**.

## الأسئلة المتكررة

**ماذا لو كانت ملفات PNG كبيرة جدًا (أكثر من 5 ميغابايت)؟**  
Aspose OCR يقلل حجم الصور الكبيرة تلقائيًا للحفاظ على استهلاك الذاكرة معقولًا، ولكن يمكنك تغيير الحجم يدويًا باستخدام `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` لتحديد العرض بحد أقصى 2000 بكسل مع الحفاظ على نسبة الأبعاد.

**هل يمكن تشغيل هذا على Linux؟**  
نعم. Aspose OCR متعدد المنصات؛ فقط تأكد من تثبيت الاعتمادات الأصلية (`libgdiplus` على بعض التوزيعات).

**هل لغة OCR مضبوطة على الإنجليزية افتراضيًا؟**  
صحيح. إذا كنت بحاجة إلى لغة أخرى، اضبط `engine.Language = OcrLanguage.French;` (أو أي تعداد مدعوم) قبل استدعاء `Recognize()`.

**كيف أتعامل مع ملفات PDF المحمية بكلمة مرور وتحتوي على PNGs؟**  
حوّل صفحات PDF إلى صور أولاً (باستخدام Aspose PDF أو مكتبة أخرى)، ثم أدخل تلك PNGs إلى نفس خط الأنابيب. مبدأ **كيفية تشغيل OCR على الصور** يبقى دون تغيير.

## مثال كامل يعمل (Async Main)

فيما يلي برنامج مستقل يمكنك نسخه ولصقه في مشروع وحدة تحكم. يتضمن جميع الأجزاء السابقة، بالإضافة إلى أداة صغيرة للتحقق من صحة مجلد الإدخال.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**المخرجات المتوقعة** (عينة لملفين PNG):

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## الخلاصة

لقد غطينا الآن كل ما تحتاجه **لاستخراج النص من PNG** باستخدام C#. من تحديد الملفات، تشغيل مهام OCR المتوازية، معاينة السلاسل، إلى حفظها في CSV—هذا الدليل يزودك بنمط جاهز للإنتاج لسيناريوهات **تحويل الصورة إلى نص C#**.  

إذا كنت مستعدًا للخطوة التالية، جرّب تمرير ملفات JPEG أو TIFF عبر نفس خط الأنابيب، جرب لغات OCR مختلفة، أو اربط النتائج بفهرس بحث لتتمكن من **قراءة النص من الصور الممسوحة ضوئيًا** فورًا.  

هل لديك أسئلة حول حالات الحافة، تحسين الأداء، أو الترخيص؟ اترك تعليقًا أو تواصل مع مجتمع Aspose—برمجة سعيدة!  

![مثال على استخراج النص من PNG](extract-text-png.png "استخراج النص من PNG باستخدام Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}