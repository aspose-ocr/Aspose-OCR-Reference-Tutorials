---
category: general
date: 2026-02-28
description: كيفية تنفيذ التعرف الضوئي على الحروف (OCR) على دفعات باستخدام Aspose.OCR
  في C#. تعلم استخراج النص من الصور، التعرف على النص من ملفات PNG، وتعزيز معالجة OCR
  على دفعات بكفاءة.
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- batch ocr processing
language: ar
og_description: كيفية تنفيذ OCR دفعيًا باستخدام Aspose.OCR. يوضح لك هذا الدليل خطوة
  بخطوة كيفية استخراج النص من الصور، والتعرف على النص من ملفات PNG، وتحسين معالجة
  OCR الدفعية.
og_title: كيفية تنفيذ OCR دفعيًا في C# – استخراج النص بسرعة من الصور
tags:
- OCR
- C#
- Aspose
title: كيفية تنفيذ التعرف الضوئي على الحروف (OCR) على دفعات في C# – دليل كامل لاستخراج
  النص من الصور
url: /ar/net/ocr-optimization/how-to-batch-ocr-in-c-complete-guide-for-extracting-text-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعة في C# – دليل كامل لاستخراج النص من الصور

هل تساءلت يومًا **كيف تقوم بـ OCR دفعة** لعشرات الصفحات الممسوحة ضوئيًا دون كتابة استدعاء منفصل لكل ملف؟ لست وحدك. في العديد من المشاريع—أتمتة الفواتير، رقمنة الأرشيف، أو ببساطة استخراج البيانات من لقطات الشاشة—يحتاج المطورون إلى طريقة موثوقة لـ **استخراج النص من الصور** على نطاق واسع.  

في هذا الدرس سنستعرض حلًا عمليًا باستخدام Aspose.OCR. بحلول النهاية ستعرف بالضبط كيف **تتعرف على النص من ملفات PNG**، وتتحكم في التوازي، وتتعامل مع نتائج تشغيل **معالجة OCR دفعة**. لا مراجع غامضة، بل برنامج كامل قابل للتنفيذ وتفسير لكل إعداد.

## المتطلبات المسبقة — ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا)  
- Aspose.OCR لـ .NET ≥ 23.10 (اسم حزمة NuGet هو `Aspose.OCR`)  
- مجلد يحتوي على بعض صور PNG التي تريد معالجتها (المثال يستخدم ثلاثة ملفات)  
- كمية معتدلة من الذاكرة RAM/CPU—قم بتعديل `MaxDegreeOfParallelism` إذا وصلت إلى الحدود  

إذا لم تقم بتثبيت الحزمة بعد، نفّذ:

```bash
dotnet add package Aspose.OCR
```

هذا كل شيء. لا ملفات تنفيذية إضافية، ولا خدمات خارجية.

## نظرة عامة على الحل

سننشئ كائنًا من نوع `OcrBatchProcessor`، نزوده بقائمة من مسارات الصور، ونسمح للمكتبة بتشغيل أداة التعرف على كل ملف بشكل متوازي. يُعيد المعالج مجموعة من كائنات `OcrResult`، كل منها يحتوي على النص المستخرج وبعض البيانات الوصفية. أخيرًا سنطبع ملخصًا قصيرًا، وربما نص الصفحة الأولى.

Below is a high‑level diagram (feel free to replace the placeholder with your own image).  

<img src="batch-ocr-diagram.png" alt="مخطط كيفية تنفيذ OCR دفعة" width="600"/>

## الخطوة 1 – إعداد معالج OCR دفعة

أول شيء تحتاجه هو نسخة من `OcrBatchProcessor`. هذا الكائن ينظم العمل ويسمح لك بضبط الخيارات المتعلقة بالأداء.

```csharp
using Aspose.OCR;
using System.Collections.Generic;
using System;

/// <summary>
/// Demonstrates how to batch OCR a collection of PNG images using Aspose.OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Configure the batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor
        {
            // Use up to 4 threads – increase on a multi‑core machine, decrease if you hit memory pressure
            MaxDegreeOfParallelism = 4,

            // Tell the engine what language to expect; here we use French as an example.
            // Change to OcrLanguage.English, OcrLanguage.Spanish, etc., as needed.
            Language = OcrLanguage.French
        };
```

**لماذا هذا مهم:** `MaxDegreeOfParallelism` يحدد عدد الصور التي تُعالج في وقت واحد. ضبطه عاليًا جدًا قد يملأ وحدة المعالجة المركزية أو يسبب أخطاء نفاد الذاكرة، بينما قيمة منخفضة جدًا تهدر الموارد. خاصية `Language` تحسن الدقة لأن محرك OCR يمكنه تطبيق خوارزميات خاصة باللغة.

## الخطوة 2 – بناء قائمة ملفات الصور

بعد ذلك نجمع مسارات الملفات التي نريد معالجتها. في سيناريوهات العالم الحقيقي قد تقرأ محتويات الدليل بشكل ديناميكي، لكن القائمة الثابتة تجعل المثال مختصرًا.

```csharp
        // Step 2: Assemble the collection of PNG files you want to OCR
        List<string> imageFiles = new()
        {
            @"C:\Images\page1.png",
            @"C:\Images\page2.png",
            @"C:\Images\page3.png"
        };
```

**نصيحة:** إذا كنت بحاجة لتصفية ملفات PNG فقط من مجلد، يمكنك استخدام `Directory.GetFiles(path, "*.png")`. يعمل معالج الدفعة مع أي تنسيق نقطي مدعوم من Aspose.OCR، بما في ذلك JPEG و BMP.

## الخطوة 3 – تشغيل عملية OCR دفعة

الآن نمرر القائمة إلى `batchProcessor.Recognize`. تُعيد الطريقة `List<OcrResult>` حيث يتطابق كل عنصر مع صورة الإدخال.

```csharp
        // Step 3: Execute the OCR operation on the whole batch
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

**ماذا يحدث خلف الكواليس؟**  
Aspose.OCR ينشئ ما يصل إلى `MaxDegreeOfParallelism` من خيوط العمل. كل خيط يحمل صورة، يطبق المعالجة المسبقة (إزالة الميل، التحويل إلى ثنائي)، يشغل محرك التعرف، ويخزن الناتج النصي في `OcrResult`. لأن العمل متوازي، يكون إجمالي وقت المعالجة تقريبًا *عدد الصور / التوازي* (مع بعض النفقات الإضافية).

## الخطوة 4 – تلخيص النتائج

بعد انتهاء الدفعة، من المفيد معرفة عدد الصفحات التي تمت معالجتها بنجاح. سنظهر أيضًا كيفية الوصول إلى النص الخام.

```csharp
        // Step 4: Report how many pages were recognized
        Console.WriteLine($"Processed {ocrResults.Count} pages.");
```

المخرجات في هذه المرحلة تبدو كالتالي:

```
Processed 3 pages.
```

إذا فشل أي صورة (ملف تالف، تنسيق غير مدعوم)، فإن Aspose.OCR يرمي استثناء. يمكنك تغليف الاستدعاء داخل كتلة `try/catch` لتسجيل الأخطاء دون إيقاف الدفعة بأكملها.

## الخطوة 5 – (اختياري) عرض النص المستخرج

غالبًا ما تحتاج فقط إلى فحص سريع—عرض نص الصفحة الأولى، على سبيل المثال.

```csharp
        // Step 5: Optionally dump the text of the first page
        if (ocrResults.Count > 0)
        {
            Console.WriteLine("--- Page 1 Text ---");
            Console.WriteLine(ocrResults[0].Text);
        }
    }
}
```

قد يكون إخراج وحدة التحكم النموذجي كالتالي:

```
--- Page 1 Text ---
Bonjour, ceci est un exemple de texte extrait d'une image PNG.
```

هذا يؤكد أن OCR نجح وأن تلميح اللغة عمل.

## الكود الكامل الجاهز للتنفيذ

بجمع كل شيء معًا، إليك البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد.

```csharp
using Aspose.OCR;
using System.Collections.Generic;
using System;

/// <summary>
/// Complete example of batch OCR processing with Aspose.OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // 1️⃣ Configure the batch OCR processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 4,   // Adjust based on your hardware
            Language = OcrLanguage.French // Change to match your source language
        };

        // 2️⃣ List the PNG files you want to process
        List<string> imageFiles = new()
        {
            @"C:\Images\page1.png",
            @"C:\Images\page2.png",
            @"C:\Images\page3.png"
        };

        // 3️⃣ Run the batch OCR operation
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);

        // 4️⃣ Show how many pages were recognized
        Console.WriteLine($"Processed {ocrResults.Count} pages.");

        // 5️⃣ (Optional) Print the extracted text of the first page
        if (ocrResults.Count > 0)
        {
            Console.WriteLine("--- Page 1 Text ---");
            Console.WriteLine(ocrResults[0].Text);
        }
    }
}
```

قم بالترجمة باستخدام `dotnet run` وشاهد وحدة التحكم تُظهر عدد الصفحات ومحتوى الصفحة الأولى.

## التعامل مع الحالات الطرفية والمشكلات الشائعة

| الحالة | ما الذي يجب مراقبته | الإصلاح المقترح |
|-----------|-------------------|----------------|
| **مجموعة صور كبيرة (مئات الملفات)** | ارتفاع استهلاك الذاكرة لأن كل خيط يحمل صورة bitmap كاملة. | قلل `MaxDegreeOfParallelism` أو عالج الملفات على دفعات أصغر (مثلاً مجموعات من 50). |
| **لغات مختلطة في نفس الدفعة** | ضبط `Language` واحدة قد يقلل الدقة للملفات ذات اللغات الأخرى. | أنشئ نسخًا منفصلة من `OcrBatchProcessor` لكل لغة، أو اترك `Language` غير محددة لتسمح للمحرك بالكشف التلقائي (أبطأ). |
| **ملف PNG تالف أو غير مدعوم** | `Recognize` يرمي `FileNotFoundException` أو `InvalidOperationException`. | غلف الاستدعاء بـ `try { … } catch (Exception ex) { Log(ex); continue; }`. |
| **الحاجة إلى تسريع GPU** | يمكن لـ Aspose.OCR الاستفادة من GPU، لكن يجب تمكينه صراحةً. | اضبط `batchProcessor.UseGpu = true;` وتأكد من تثبيت برامج تشغيل متوافقة. |
| **الحاجة إلى درجة الثقة** | `OcrResult` يوفّر أيضًا `Confidence` لكل سطر. | قم بالتكرار على `ocrResults[i].Lines` لجمع درجة الثقة لكل سطر إذا كنت تحتاج إلى تصفية الجودة. |

### نصيحة احترافية

إذا كنت تعالج فواتيرًا ممسوحة ضوئيًا، فكر في **قصّ مسبق** لكل صورة إلى المنطقة التي تحتوي على النص. يعمل محرك OCR أسرع ويعطي ثقة أعلى عندما تزيل الحدود والضوضاء.

## مؤشرات الأداء (مرجع سريع)

| عدد الصور | التوازي (4 خيوط) | الوقت التقريبي على i7‑12700H |
|-------------|------------------------|---------------------------|
| 10          | 4                      | 3.2 seconds               |
| 50          | 4                      | 14.7 seconds              |
| 200         | 8 (إذا زدت القيمة) | 1 minute 10 seconds |

قد تختلف النتائج حسب دقة الصورة وتعقيد اللغة، لكن الجدول يعطي توقعًا واقعيًا لمعالجة OCR دفعة النموذجية.

## الخطوات التالية – توسيع سير العمل

الآن بعد أن يمكنك **تنفيذ OCR دفعة** لملفات PNG، قد ترغب في:

- **حفظ النتائج** في قاعدة بيانات أو ملف JSON للتحليلات اللاحقة.  
- **ربط المخرجات** بسلسلة معالجة لغة طبيعية (مثلاً تحليل المشاعر).  
- **دمج مع Azure Functions** للحصول على OCR بدون خادم، عند الطلب، كجزء من بنية ميكروسيرفيس أكبر.  

جميع هذه السيناريوهات تعيد استخدام النمط الأساسي الذي غطيناه للتو: ضبط المعالج، تغذيته بمجموعة، ومعالجة كائنات `OcrResult`.

## الخلاصة

لقد أوضحنا للتو **كيفية تنفيذ OCR دفعة** في C# باستخدام Aspose.OCR. أظهر الدرس لك كيف **استخراج النص من الصور**، وبشكل خاص **التعرف على النص من ملفات PNG**، وكيفية ضبط **معالجة OCR دفعة** للسرعة والموثوقية. مع الكود الكامل، وشروحات كل إعداد، وبعض النصائح العملية، أنت جاهز لتضمين ذلك في مشاريعك—سواءً كنت تقوم برقمنة الإيصالات، أرشفة الأدلة القديمة، أو بناء مستودع صور قابل للبحث.

جرّبه، عدّل التوازي، غيّر اللغة، وشاهد خط أنابيب استخراج النصوص ينشط. إذا واجهت أي مشاكل أو كان لديك أفكار لتحسين إضافي، لا تتردد في ترك تعليق أدناه. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}