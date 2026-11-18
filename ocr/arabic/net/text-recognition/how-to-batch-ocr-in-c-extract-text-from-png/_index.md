---
category: general
date: 2026-03-26
description: كيفية تنفيذ التعرف الضوئي على الحروف (OCR) دفعيًا في C# يجعل استخراج
  النص من ملفات PNG سهلًا. اتبع هذا الدليل خطوة بخطوة للتعرف الضوئي على الحروف في
  C# لاستخراج النص دفعيًا باستخدام Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: ar
og_description: كيفية تنفيذ OCR دفعيًا في C# يتيح لك استخراج النص بسرعة من ملفات PNG.
  يوضح هذا الدليل خطوة بخطوة كيفية إجراء استخراج النص دفعيًا باستخدام C#.
og_title: كيفية تنفيذ OCR دفعيًا في C# – استخراج النص من PNG
tags:
- OCR
- C#
- Aspose
title: كيفية تنفيذ OCR دفعيًا في C# – استخراج النص من PNG
url: /ar/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعيًا في C# – استخراج النص من PNG

هل تساءلت يومًا **كيف تقوم بـ OCR دفعي** لمجموعة من لقطات الشاشة دون كتابة برنامج منفصل لكل ملف؟ لست وحدك. في العديد من المشاريع ننتهي بمجموعة من عشرات ملفات PNG التي تحتاج إلى استخراج نصها، والقيام بذلك ملفًا بملف أمر مرهق.  

الأخبار السارة؟ مع Aspose OCR يمكنك إنشاء تطبيق وحدة تحكم صغير بلغة C# يعالج جميع هذه الصور بشكل متوازي، مما يمنحك **استخراج نص دفعي** سريع ومجموعة نتائج نظيفة. في هذا الدليل سنستعرض **دروس OCR بلغة C#** كاملة، نشرح لماذا كل جزء مهم، ونظهر لك بالضبط كيف يبدو الناتج.

بحلول نهاية هذا المقال ستتمكن من:

* تحميل قائمة بملفات PNG (أو أي صورة مدعومة) دفعة واحدة.  
* تكوين `OcrEngine` مشترك بحيث تبقى الإعدادات متسقة عبر الدفعة.  
* تشغيل طابور التعرف مع ما يصل إلى أربعة عمال متوازيين.  
* الحصول على النص المعترف به لكل صفحة وطباعةه إلى وحدة التحكم.

لا سحر، فقط كود ثابت يمكنك إدراجه في مشروعك اليوم.

## ما ستحتاجه

قبل أن نغوص في التفاصيل، تأكد من أن لديك:

* .NET 6 SDK (أو أي نسخة حديثة من .NET).  
* ترخيص Aspose OCR صالح أو مفتاح تقييم مؤقت.  
* مجلد يحتوي على ملفات PNG التي تريد معالجتها.  
* Visual Studio 2022 أو محررك المفضل.

هذا كل شيء—لا حزم NuGet إضافية بخلاف `Aspose.OCR` و`System.Collections.Generic` القياسية.

## كيفية إعداد مشروع OCR دفعي – إعداد المشروع

أولاً، أنشئ مشروع وحدة تحكم جديد واستورد مكتبة Aspose OCR.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

بعد انتهاء الاستعادة، افتح **Program.cs** (أو أنشئ ملفًا جديدًا) وأضف توجيهات `using` المعتادة:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

هذا الإعداد البسيط يمنحنا الوصول إلى `OcrEngine` و`RecognitionQueue` والفئات المساعدة التي سنحتاجها لاحقًا.

## استخراج النص من PNG – إعداد قائمة الصور

الآن نحتاج إلى إخبار البرنامج **بأي PNGs** يجب تشغيل OCR عليها. أبسط طريقة هي بناء `List<string>` يحتوي على مسارات مطلقة أو نسبية.

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

استبدل `YOUR_DIRECTORY` بالمسار الفعلي للمجلد. إذا كان لديك مجموعة ديناميكية، يمكنك أيضًا استخدام `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` وإدخال النتيجة في القائمة. النقطة الأساسية هي أن **استخراج النص من PNG** هو مجرد إمداد الطابور بأسماء الملفات الصحيحة.

![مخطط سير عمل OCR دفعي](https://example.com/placeholder.png "مخطط يوضح كيفية تنفيذ OCR دفعيًا لمجموعة من ملفات PNG")

*نص بديل للصورة: مخطط سير عمل OCR دفعي*

## درس OCR بلغة C# – تكوين طابور التعرف

قلب عملية الدفعة هو `RecognitionQueue`. فكر فيه كحزام ناقل يسلّم كل صورة إلى `OcrEngine` المشترك. بمشاركة المحرك نحافظ على انخفاض استهلاك الذاكرة ونضمن إعدادات متطابقة لكل صفحة.

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

لماذا نضبط `MaxDegreeOfParallelism` إلى 4؟ على جهاز محمول رباعي النواة يعطيك أفضل معدل نقل دون إهمال نظام التشغيل. إذا كنت تعمل على خادم بعدد أكبر من الأنوية، قم بزيادة الرقم وفقًا لذلك.

### نصيحة احترافية

إذا كنت بحاجة إلى حزم لغات مخصصة أو إعدادات DPI أو قص منطقة اهتمام، قم بذلك **مرة واحدة** على `Engine` المشترك قبل إدراج أي صور. مثال:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

جميع عمليات التعرف اللاحقة ترث هذه الخيارات تلقائيًا—هذه هي جوهر **كيفية إنشاء خطوط أنابيب OCR** التي تظل متسقة.

## استخراج النص دفعيًا – إدراج الصور وتشغيل الطابور

مع جاهزية الطابور، الخطوة التالية هي دفع كل صورة إليه. طريقة `Enqueue` تقبل كائن `OcrImage`، والذي ننشئه من مسار ملف.

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

بمجرد إدراج كل ملف في الطابور، نطلق عملية المعالجة:

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` تحجب التنفيذ حتى تنتهي كل صورة، ثم تُعيد قائمة حيث يتطابق كل عنصر مع ترتيب الإدخال. هذا يضمن أن نتيجة الصفحة 1 تكون في الفهرس 0، والصفحة 2 في الفهرس 1، وهكذا—مفيد عندما تحتاج إلى ربط النتائج بالملفات المصدر.

## كيفية إنشاء OCR – عرض النتائج

أخيرًا، لنطبع النص المعترف به إلى وحدة التحكم. هنا ستشاهد **استخراج النص دفعيًا** يعمل فعليًا.

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

عند تشغيل البرنامج (`dotnet run`)، يجب أن ترى شيئًا مثل:

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

إذا فشلت أي صورة (مثلاً ملف تالف)، سيحمل `OcrResult` المقابل خاصية `Text` فارغة ويمكنك فحص `ocrResults[i].Exception` للتشخيص.

## كيفية إنشاء OCR – نصائح، حالات حافة، وأفضل الممارسات

### معالجة دفعات كبيرة

معالجة مئات ملفات PNG قد تستهلك الذاكرة إذا أبقيت جميع كائنات `OcrResult` حية. في مثل هذه الحالات، قم ببث الإخراج إلى ملف أو قاعدة بيانات فور وصول كل نتيجة:

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### التعامل مع صيغ غير PNG

Aspose OCR يدعم أيضًا JPEG وBMP وTIFF مباشرة. فقط غيّر امتداد الملف في القائمة أو استخدم بحثًا بالوايلدكارد. نفس خطوات **دروس OCR بلغة C#** تنطبق—لا حاجة لتغيير الكود.

### تخطي الصفحات الفارغة

إذا كان لديك ملفات PDF ممسوحة تحتوي أحيانًا على صفحات فارغة، يمكنك تصفية النتائج:

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### اعتبارات الترخيص

نسخة التقييم تضع علامة مائية على كل صفحة. للاستخدام الإنتاجي، تأكد من تضمين ملف الترخيص في بداية `Main`:

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### ضبط التوازي

`MaxDegreeOfParallelism` يساوي افتراضيًا `Environment.ProcessorCount`. إذا لاحظت استهلاكًا عاليًا للمعالج أو ضغطًا على الذاكرة، قلل القيمة. وعلى العكس، في جهاز افتراضي سحابي بعدد كبير من الأنوية، زدها لاستغلال العتاد بالكامل.

## الخلاصة

أصبح لديك الآن حل **كيفية تنفيذ OCR دفعي** كامل في C# يمكنه **استخراج النص من PNG**، تشغيله بشكل متوازي، وتزويدك بنتائج نظيفة ومرتبة. بمشاركة `OcrEngine` واحد تعلمت **كيفية إنشاء خطوط أنابيب OCR** التي تكون فعّالة في الذاكرة وسهلة الصيانة. هذا **دروس OCR بلغة C#** يوضح أيضًا كيفية التوسع إلى **استخراج نص دفعي** لمئات الصور ببضع أسطر إضافية فقط.

---

### ما التالي؟

* جرّب إضافة اكتشاف اللغة (`Engine.Language = Language.AutoDetect`).  
* جرب صيغ إخراج مختلفة—اكتب النتائج إلى JSON أو CSV للتحليلات اللاحقة.  
* اجمع هذا OCR الدفعي مع خطوة تحويل PDF إلى صورة لمعالجة المستندات الممسوحة بالكامل.

لا تتردد في تعديل التوازي، أو استبدال مصادر الصور الخاصة بك، أو ربط النتائج بفهرس بحث. السماء هي الحد عندما تتقن **كيفية تنفيذ OCR دفعي** في C#.

برمجة سعيدة، ولتكن عمليات OCR سريعة وخالية من الأخطاء!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}