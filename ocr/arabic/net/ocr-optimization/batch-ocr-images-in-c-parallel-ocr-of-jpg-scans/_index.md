---
category: general
date: 2026-04-29
description: قم بمعالجة صور OCR دفعيًا بسرعة باستخدام Aspose OCR في C#. تعلم كيفية
  استخراج النص من ملفات jpg، قراءة النص من المسحات الضوئية، ومعالجة قائمة الصور بشكل
  متوازي.
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: ar
og_description: قم بمعالجة صور OCR على دفعات بسرعة باستخدام Aspose OCR. يوضح هذا الدليل
  كيفية استخراج النص من ملفات JPG، قراءة النص من المسحات الضوئية، ومعالجة قائمة الصور
  بشكل متوازي.
og_title: معالجة دفعة من صور OCR في C# – OCR متوازي لملفات JPG الممسوحة
tags:
- C#
- OCR
- Aspose
- Image Processing
title: معالجة OCR دفعية للصور في C# – OCR متوازي لملفات JPG الممسوحة.
url: /ar/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة دفعة صور OCR في C# – OCR متوازي لملفات JPG

هل احتجت يوماً إلى **معالجة دفعة صور OCR** لكنك لم تكن متأكدًا من كيفية توسيع العمل عبر ملفات متعددة؟ لست وحدك—غالبًا ما يواجه المطورون عقبة عندما يحاولون قراءة النص من المسحات واحدةً تلو الأخرى. الخبر السار هو أنه باستخدام Aspose OCR يمكنك **استخراج النص من jpg**، **قراءة النص من المسحات**، و**معالجة قائمة الصور** بشكل متوازي ببضع أسطر من C# فقط.

في هذا الدرس سنستعرض مثالًا كاملًا جاهزًا للتنفيذ يوضح بالضبط كيفية القيام بذلك. في النهاية ستحصل على تطبيق console مستقل يتعرف على مجلد من مسحات JPEG، يطبع نص كل صفحة، ويخبرك بالمدة التي استغرقها كل عملية. لا مستندات خارجية لتتبعها، ولا مقتطفات شفرة نصف مكتملة—فقط حل كامل يمكنك وضعه في Visual Studio وتشغيله.

## ما الذي ستحتاجه

- **.NET 6.0** أو أحدث (الكود يُجمّع أيضًا على .NET Framework 4.6+)
- حزمة NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`)
- مجموعة من ملفات JPG أو صور مسح ضوئي تريد معالجتها
- أي بيئة تطوير تفضلها؛ أستخدم Visual Studio 2022، لكن VS Code يعمل أيضًا بشكل جيد

هذا كل شيء. إذا كان لديك حزمة NuGet بالفعل، فأنت جاهز للبدء.

## الخطوة 1 – تهيئة محرك OCR (إعداد دفعة صور OCR)

أول شيء نقوم به هو إنشاء مثيل `OcrEngine` وتحديد اللغة التي نريد البحث عنها. في معظم الحالات تكون الإنجليزية كافية، لكن يمكنك استبدال `OcrLanguage.English` بأي لغة مدعومة.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*لماذا هذا مهم:* تهيئة المحرك مرة واحدة وإعادة استخدامه عبر جميع الصور أكثر كفاءة بكثير من إنشاء مثيل جديد لكل ملف. كما يسمح ذلك لـ Aspose بمشاركة الموارد الداخلية، وهو أمر أساسي لـ **معالجة OCR المتوازية**.

## الخطوة 2 – بناء قائمة الصور (معالجة قائمة الصور)

بعد ذلك نحدد مجموعة مسارات الملفات التي نريد تمريرها إلى المعالج الدفعي. يمكنك توليد هذه القائمة ديناميكيًا باستخدام `Directory.GetFiles`، لكن للتوضيح سنقوم بكتابة بعض الإدخالات يدويًا.

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*نصيحة:* إذا كان لديك آلاف المسحات، فكر في استخدام `Directory.EnumerateFiles` مع مرشح مثل `*.jpg` لتجنب تحميل القائمة بالكامل في الذاكرة مرة واحدة.

## الخطوة 3 – تشغيل التعرف الدفعي (معالجة OCR المتوازية)

الآن يأتي جوهر الموضوع: استدعاء `BatchRecognize`. تقبل الطريقة معامل `maxDegreeOfParallelism`، الذي يتحكم في عدد الخيوط التي سيُنشئها Aspose. بشكل افتراضي يستخدم أربعة خيوط، لكن يمكنك زيادة ذلك إذا كان معالجك يحتوي على نوى أكثر.

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*ما الذي يحدث خلف الكواليس؟* يقوم Aspose بتقسيم مجموعة `imagePaths` إلى أجزاء، يسلّم كل جزء إلى خيط منفصل، ثم يجمع النتائج. هذه هي الطريقة الأكثر كفاءة لـ **استخراج النص من jpg** عندما يكون لديك **قائمة معالجة الصور** يمكن التعامل معها بشكل متزامن.

## الخطوة 4 – عرض النتائج (قراءة النص من المسحات)

أخيرًا نمر عبر مجموعة `recognitionResults` ونطبع نص كل ملف ووقت المعالجة. كما يوفر كائن `OcrResult` اسم الملف الأصلي، مما يساعد عندما تحتاج إلى تسجيل أو تخزين المخرجات.

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**الناتج المتوقع (مثال):**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

لاحظ كيف أن كل كتلة تُظهر اسم الملف، ومدة تنفيذ OCR، والنص المستخرج. هذا بالضبط ما تحتاجه عندما تقوم **بقراءة النص من المسحات** في خط إنتاج.

## معالجة الحالات الشائعة

| الحالة | ما الذي يجب مراقبته | حل سريع |
|-----------|-------------------|-----------|
| **ملف مفقود** | استثناء `FileNotFoundException` يُرمى داخل `BatchRecognize` | تحقق من المسارات باستخدام `File.Exists` قبل إضافتها إلى `imagePaths`. |
| **صيغة غير مدعومة** | Aspose يدعم فقط الصور النقطية (JPG, PNG, BMP, TIFF). | حوّل ملفات PDF إلى صور أولًا (استخدم Aspose.PDF) أو تخطّ تلك الملفات. |
| **ضغط الذاكرة** | الصور الكبيرة جدًا قد تستهلك الذاكرة عندما تعمل عدة خيوط. | قلل `maxDegreeOfParallelism` أو قلّص حجم الصور قبل OCR. |
| **نص غير إنجليزي** | ضبط اللغة على الإنجليزية سيتجاهل النصوص الأخرى. | غيّر `Language = OcrLanguage.French` (أو مجموعة لغات متعددة). |

هذه النصائح تجعل مهمة الدفعة أكثر صلابة، خاصة عندما تقوم **بمعالجة قائمة صور** تأتي من تحميلات المستخدم أو أرشيف ممسوح.

## نصيحة احترافية – ضبط التوازي

إذا شغّلت هذا على جهاز بثمانية نوى، زد التوازي إلى 6 أو 8 وستلاحظ تحسنًا في السرعة. ومع ذلك، تذكر أن كل خيط يستهلك أيضًا ذاكرة للـ bitmap. قاعدة جيدة لتطبيقها:

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

استخدم المتغيّر `maxThreads` داخل `BatchRecognize` لتكوين إعداد ديناميكي يتوافق مع مواصفات الجهاز.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل، جاهزًا للترجمة. ما عليك سوى استبدال `YOUR_DIRECTORY` بالمسار الذي يحتوي على مسحات JPG الخاصة بك.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **ملاحظة:** سطر `using System.IO;` ضروري لمساعد `Directory`. يطبع الكود رسالة ودية إذا لم يُعثر على أي JPGs، مما يمنع فشل صامت.

## الخلاصة

لقد عرضنا للتو سير عمل **دفعة صور OCR** نظيفًا ي **استخراج النص من jpg**، **يقرأ النص من المسحات**، ويعالج **قائمة الصور** بفعالية باستخدام **معالجة OCR المتوازية**. المثال القابل للتنفيذ يوضح بالضبط كيفية إعداد المحرك، إمداده بمجموعة من الملفات، والتعامل مع النتائج—كل ذلك مع الحفاظ على استهلاك الذاكرة وعدد الخيوط تحت السيطرة.

هل أنت مستعد للخطوة التالية؟ جرّب تغيير اللغة إلى الفرنسية، أضف تحويل PDF إلى صورة، أو خزن نص OCR في قاعدة بيانات. النمط يبقى نفسه: تهيئة مرة واحدة، إمداد القائمة، ودع Aspose يتولى العمل الشاق بشكل متوازي.

هل لديك أسئلة أو تريد مشاركة تعديلاتك؟ اترك تعليقًا أدناه، وبرمجة سعيدة! 

![معالجة دفعة صور OCR](https://example.com/placeholder.png "مخطط يوضح سير عمل دفعة صور OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}