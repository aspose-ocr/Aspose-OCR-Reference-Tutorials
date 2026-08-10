---
category: general
date: 2026-02-14
description: كيفية استخدام OCR في C# لاستخراج النص من ملفات PNG بسرعة. تعلم معالجة
  صور OCR على دفعات، معالجة صور متعددة، واستخدام Aspose OCR C# في دليل واحد.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: ar
og_description: كيفية استخدام OCR في C# مع Aspose OCR C#. يوضح هذا الدرس كيفية استخراج
  النص من ملفات PNG، ومعالجة مجموعة من الصور باستخدام OCR، ومعالجة عدة صور بكفاءة.
og_title: كيفية استخدام OCR في C# – استخراج النص من ملفات PNG دفعيًا
tags:
- OCR
- C#
- Aspose
- Image Processing
title: كيفية استخدام OCR في C# – معالجة دفعة من صور PNG باستخدام Aspose OCR
url: /ar/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – معالجة دفعة من صور PNG باستخدام Aspose OCR

هل تساءلت يومًا **كيف تستخدم OCR** لاستخراج النص من مجموعة من ملفات PNG دون كتابة روتين منفصل لكل ملف؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى **استخراج نص PNG** على نطاق واسع، خاصة عندما تكون الصور موجودة في مجلد وتحتاج إلى تشغيل محرك OCR لكل ملف.  

في هذا الدليل سنستعرض حلًا كاملاً جاهزًا للتنفيذ يقوم بـ **معالجة دفعة من صور OCR**، **معالجة صور متعددة** بالتوازي، ويستفيد من مكتبة **Aspose OCR C#** القوية. في النهاية ستحصل على ملف تنفيذي واحد يقرأ أي عدد من ملفات PNG، يستخرج نصها، ويطبع النتائج إلى وحدة التحكم—كل ذلك ببضع أسطر من الشيفرة فقط.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (تعمل الشيفرة مع .NET Core و .NET Framework أيضًا)  
- رخصة صالحة لـ Aspose.OCR for .NET (أو النسخة التجريبية) – يمكنك الحصول عليها من موقع Aspose.  
- مجلد يحتوي على ملفات PNG التي تريد قراءتها.  
- Visual Studio 2022 (أو أي بيئة تطوير متوافقة مع C#).  

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.OCR`.

## الخطوة 1: كيفية استخدام OCR – تهيئة محرك Aspose OCR

الشيء الأول الذي تحتاجه هو نسخة من الفئة `Engine`. هذا الكائن ي抽象 التقنية الأساسية لـ OCR ويمكنه العمل على CPU أو GPU، حسب العتاد والرخصة لديك.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*لماذا هذا مهم:* تهيئة المحرك مرة واحدة وإعادة استخدامه عبر الخيوط يوفر الذاكرة ويتجنب العبء المتكرر لتحميل نماذج OCR. كما يضمن إعدادات متسقة لجميع الصور.

## الخطوة 2: استخراج نص PNG – جمع مسارات الصور

بعد ذلك، نحتاج إلى مجموعة من مسارات الملفات. في مشروع حقيقي قد تقرأ الدليل ديناميكيًا، لكن للتوضيح سنذكر بعض الملفات النموذجية.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*نصيحة:* استبدل `YOUR_DIRECTORY` بالمسار المطلق أو النسبي للصور الخاصة بك. إذا كان لديك عشرات الملفات، يمكنك استبدال القائمة اليدوية بـ `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`.

## الخطوة 3: معالجة دفعة من صور OCR – تشغيل التعرف بالتوازي

معالجة الصور واحدة تلو الأخرى بسيطة لكنها بطيئة. باستخدام `Parallel.ForEach` يمكننا **معالجة صور متعددة** في نفس الوقت، مستفيدين من المعالجات متعددة النوى.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*لماذا التوازي؟* كل استدعاء OCR يستهلك CPU لكنه مستقل، لذا تشغيلها متزامنًا يمكن أن يقلل زمن التنفيذ بشكل كبير، خاصة على جهاز بأربع نوى أو أكثر.

## الخطوة 4: معالجة صور متعددة – عرض النص المستخرج

الآن بعد أن لدينا مجموعة من كائنات `OcrResult`، يمكننا التكرار عليها وطباعة النص المعترف به. هنا عادةً ما تقوم بتخزين النتيجة في قاعدة بيانات أو كتابة ملفات، لكن إخراج وحدة التحكم يبقي المثال مختصرًا.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**نموذج لإخراج وحدة التحكم (عينة):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

إذا فشل تحميل أي صورة، ستطرح Aspose استثناءً؛ يمكنك وضع استدعاء `engine.Recognize` داخل كتلة `try/catch` لتسجيل الأخطاء دون إيقاف الدفعة بأكملها.

## الخطوة 5: مثال كامل يعمل – كل الأجزاء معًا

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع C# جديد من نوع Console. يتضمن كل شيء من عبارات `using` إلى حلقة الإخراج النهائية.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### تشغيل العينة

1. أنشئ مشروع **Console App** جديد في Visual Studio.  
2. أضف حزمة NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`).  
3. استبدل `YOUR_DIRECTORY` بالمسار الذي يحتوي على ملفات PNG الخاصة بك.  
4. ابنِ المشروع وشغّله – يجب أن ترى النص المستخرج مطبوعًا في وحدة التحكم.

## نصائح احترافية وحالات خاصة

- **تسريع GPU:** إذا كان لديك GPU متوافق ورخصة Aspose OCR، فعّل التسريع عبر `EngineSettings` قبل إنشاء المحرك. هذا يمكن أن يقلل الثواني المستهلكة لكل صورة.  
- **الملفات الكبيرة:** للصور التي يزيد حجمها عن 10 ميغابايت، فكر في تقليل أبعادها أولًا لتقليل الضغط على الذاكرة.  
- **دعم اللغات:** افتراضيًا يفترض المحرك اللغة الإنجليزية. اضبط `engine.Language = Language.French;` (أو أي لغة مدعومة) لتحسين الدقة للنص غير الإنجليزي.  
- **معالجة الأخطاء:** يضمن `try/catch` داخل حلقة التوازي أن ملفًا فاسدًا لا يوقف الدفعة بأكملها. يمكنك أيضًا تسجيل الفشل إلى ملف للمراجعة لاحقًا.  
- **تخزين النتائج:** بدلاً من الطباعة، يمكنك كتابة `result.Text` إلى ملف `.txt` باستخدام `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## الخلاصة

أنت الآن تعرف **كيف تستخدم OCR** في C# **لاستخراج نص PNG**، **معالجة دفعة من صور OCR**، و**معالجة صور متعددة** بكفاءة باستخدام Aspose OCR C#. الحل مكتمل ذاتيًا، يعمل بالتوازي، ويمكن توسيعه للتعامل مع مئات أو آلاف الملفات مع تغييرات قليلة فقط.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال إخراج وحدة التحكم بتقرير CSV، أو جرب تسريع GPU، أو أدخل نص OCR في فهرس بحث. الاحتمالات لا حصر لها، والنمط الأساسي—تهيئة مرة واحدة، تشغيل بالتوازي، معالجة الأخطاء برفق—سيساعدك في أي خط أنابيب لمعالجة الصور.

برمجة سعيدة، ولتكن وظائف OCR سريعة وخالية من الأخطاء!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}