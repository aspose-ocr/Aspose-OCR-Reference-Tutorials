---
category: general
date: 2026-05-06
description: تعلم كيفية تصحيح إمالة الصورة واستخراج النص من الصورة باستخدام Aspose
  OCR – دليل خطوة بخطوة لتحسين دقة OCR وكيفية إزالة الضوضاء من الصورة.
draft: false
keywords:
- how to deskew image
- extract text from image
- how to use OCR
- improve OCR accuracy
- how to denoise image
language: ar
og_description: تعلم كيفية تصحيح انحراف الصورة واستخراج النص من الصورة باستخدام Aspose
  OCR. يوضح هذا الدرس كيفية إزالة الضوضاء من الصورة وتحسين دقة OCR.
og_title: كيفية تصحيح انحراف الصورة في C# – دليل OCR الكامل
tags:
- OCR
- C#
- Image Processing
title: كيفية تصحيح ميل الصورة في C# – دليل OCR الكامل
url: /ar/net/ocr-optimization/how-to-deskew-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح إمالة الصورة في C# – دليل OCR كامل

هل احتجت يومًا إلى **كيفية تصحيح إمالة الصورة** قبل تشغيل OCR، لكنك لم تكن متأكدًا من الفلاتر التي يجب تطبيقها؟ لست وحدك—العديد من المطورين يواجهون نفس المشكلة عندما تكون الصورة المصدر مائلة قليلًا أو مشوشة. الخبر السار؟ ببضع أسطر من C# و Aspose.OCR يمكنك تعديل الصورة، تنظيفها، وأخيرًا استخراج النص منها بدقة مذهلة.

في هذا الدرس سنستعرض كل ما تحتاجه: تحميل صورة مائلة، تطبيق فلاتر تصحيح الإمالة وإزالة الضوضاء، تعزيز التباين، وأخيرًا استخراج النص. بنهاية الدرس ستفهم **كيفية استخدام OCR**، وتعرف **كيفية تحسين دقة OCR**، وستحصل على عينة كود جاهزة للتنفيذ يمكنك إدراجها في أي مشروع .NET.

## ما ستحتاجه

- .NET 6 أو أحدث (API يعمل مع .NET Core و .NET Framework)
- Aspose.OCR for .NET (نسخة تجريبية مجانية أو مرخصة) – يمكنك الحصول عليها من NuGet باستخدام `Install-Package Aspose.OCR`
- صورة مثال مائلة ومشوشة قليلًا (مثال: `skewed_noisy.jpg`)
- Visual Studio، VS Code، أو أي محرر تفضله

لا توجد مكتبات أصلية إضافية مطلوبة؛ Aspose يتولى كل شيء داخليًا.

## الخطوة 1: إعداد المشروع وتثبيت Aspose.OCR

### إنشاء تطبيق Console جديد

```bash
dotnet new console -n DeskewOcrDemo
cd DeskewOcrDemo
```

### إضافة حزمة Aspose.OCR

```bash
dotnet add package Aspose.OCR
```

هذا كل شيء—المشروع الآن يملك مرجعًا إلى محرك OCR والفلاتر المدمجة التي سنحتاجها.

## الخطوة 2: تحميل الصورة التي تريد معالجتها

سنبدأ بإنشاء كائن `OcrEngine` وتوجيهه إلى الملف الذي نريد تنظيفه.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 2: Load the image you want to process
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // The rest of the pipeline will be added next…
    }
}
```

> **لماذا هذا مهم:** تحميل الصورة هو الخطوة الأولى لأي مرشح لاحق. إذا كان المسار خاطئًا، سيفشل خط الأنابيب بأكمله بصمت، لذا تحقق مرة أخرى من الموقع.

## الخطوة 3: بناء خط أنابيب المعالجة – تصحيح الإمالة، إزالة الضوضاء، ثم تعزيز التباين

هنا يحدث السحر. سنضيف ثلاثة فلاتر بالترتيب الدقيق الذي يحقق أفضل نتائج OCR:

1. **DeskewFilter** – يصحح إمالة الصورة.
2. **MedianDenoiseFilter** – يزيل البقع العشوائية دون تشويش الحواف.
3. **ContrastStretchFilter** – يعزز الفارق بين النص والخلفية.

```csharp
        // Step 3: Build a processing pipeline – deskew, denoise, then enhance contrast
        ocrEngine.Filters.Add(new DeskewFilter());               // how to deskew image
        ocrEngine.Filters.Add(new MedianDenoiseFilter());        // how to denoise image
        ocrEngine.Filters.Add(new ContrastStretchFilter());      // improve OCR accuracy
```

> **نصيحة محترف:** الترتيب مهم جدًا. يجب تصحيح الإمالة أولًا، لأن الصورة المائلة قد تشتت مرشح إزالة الضوضاء. بعد أن تصبح الصورة مستقيمة، يمكن للفلتر المتوسط تنظيف الحبوب، وأخيرًا يعزز تمدد التباين الحروف لتبرز بوضوح.

## الخطوة 4: تشغيل التعرف على النص OCR

الآن نترك Aspose يقوم بالعمل الشاق. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على السلسلة المستخرجة وبعض مقاييس الثقة.

```csharp
        // Step 4: Run the OCR recognition
        var ocrResult = ocrEngine.Recognize();

        // Optional: check confidence (0‑100). Higher means more reliable.
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

> **كيفية استخدام OCR:** استدعاء `Recognize` يطبق داخليًا جميع الفلاتر التي أضفناها، ثم يشغل محرك OCR. لا تحتاج إلى استدعاء كل فلتر يدويًا؛ خط الأنابيب يقوم بذلك نيابةً عنك.

## الخطوة 5: إخراج النص المستخرج

أخيرًا، نطبع النص إلى وحدة التحكم. في التطبيقات الحقيقية قد تكتب النص إلى ملف، قاعدة بيانات، أو تمرره إلى خدمة أخرى.

```csharp
        // Step 5: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### مثال كامل قابل للتنفيذ

بجمع كل ما سبق، إليك البرنامج الكامل الذي يمكنك نسخه ولصقه في `Program.cs`:

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to process
        ocrEngine.SetImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 3️⃣ Build a processing pipeline – deskew, denoise, then enhance contrast
        ocrEngine.Filters.Add(new DeskewFilter());               // how to deskew image
        ocrEngine.Filters.Add(new MedianDenoiseFilter());        // how to denoise image
        ocrEngine.Filters.Add(new ContrastStretchFilter());      // improve OCR accuracy

        // 4️⃣ Run the OCR recognition
        var ocrResult = ocrEngine.Recognize();

        // 5️⃣ Show confidence and extracted text
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

شغّله باستخدام:

```bash
dotnet run
```

ستظهر لك قيمة الثقة متبوعةً بالنص العادي لما كان موجودًا في الصورة الأصلية.

## التحقق من النتيجة – ما الذي تتوقعه

إذا كانت الصورة المصدر تحتوي، على سبيل المثال، على سطر فاتورة مطبوع:

```
Invoice #12345
Total: $1,250.00
Date: 2024‑04‑30
```

بعد تشغيل خط الأنابيب، ستظهر وحدة التحكم شيئًا مشابهًا لـ:

```
Confidence: 96%
=== Extracted Text ===
Invoice #12345
Total: $1,250.00
Date: 2024-04-30
```

قيمة ثقة عالية (عادةً فوق 90٪) تشير إلى أن خطوات **how to deskew image** و **how to denoise image** ساعدت محرك OCR على رؤية الأحرف بوضوح.

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت الصورة مائلة بأكثر من 45 درجة؟

`DeskewFilter` يكتشف الزاوية تلقائيًا حتى ±45°. للميل الأكبر، قم ب pre‑rotate الصورة باستخدام `ocrEngine.Filters.Add(new RotateFilter(angle))` قبل تصحيح الإمالة.

### ثقتي منخفضة—ماذا يمكنني تجربة أخرى؟

- أضف **BinarizationFilter** لإجبار التحويل إلى أبيض وأسود.
- زد نصف قطر **MedianDenoiseFilter**: `new MedianDenoiseFilter(3)`.
- استخدم صورة مصدر ذات دقة أعلى (300 dpi أو أكثر).

### هل يمكنني معالجة عدة صور داخل حلقة؟

بالطبع. فقط انقل إنشاء المحرك خارج الحلقة، استدعِ `SetImage` لكل ملف، وأعد استخدام مجموعة الفلاتر نفسها.

```csharp
foreach (var file in Directory.GetFiles("images", "*.jpg"))
{
    ocrEngine.SetImage(file);
    var result = ocrEngine.Recognize();
    // handle result...
}
```

### هل يعمل هذا مع ملفات PDF؟

Aspose.OCR يمكنه قراءة صفحات PDF كصور، لكنك ستحتاج إلى مكتبة Aspose.PDF لاستخراج كل صفحة كصورة bitmap أولًا.

## نصائح لتعزيز دقة OCR

1. **قم بقص الحدود غير الضرورية** – المساحات الفارغة الزائدة قد تشوش محرك OCR.
2. **استخدم خلفية موحدة** – الأبيض النقي أو الرمادي الفاتح هو الأنسب.
3. **تجنّب الإضاءة القوية** – الظلال تُنشئ حواف زائفة قد لا يزيلها فلتر إزالة الضوضاء بالكامل.
4. **اختبر على عينات واقعية** – البيانات الاصطناعية تبدو نظيفة؛ الصور في الإنتاج غالبًا ما تحتوي على عيوب.

## الخلاصة

لقد غطينا للتو **how to deskew image**، **how to denoise image**، والمسار الكامل لـ **how to use OCR** مع Aspose لاستخراج **text from image** مع **improving OCR accuracy**. الكود المثال كامل، قابل للتنفيذ، وجاهز لتعديله لمعالجة دفعات، دمجه في واجهة مستخدم، أو خدمات سحابية.

ما الخطوة التالية؟ جرّب استبدال `MedianDenoiseFilter` بـ `GaussianDenoiseFilter` وقارن قيم الثقة، أو مرّر النص المستخرج إلى محلل لغة طبيعية لملء النماذج تلقائيًا. السماء هي الحد عندما تتقن خط أنابيب ما قبل المعالجة.

برمجة سعيدة، ولتكن نتائج OCR واضحة كالكريستال! 

--- 

![how to deskew image example](/images/deskew-example.png "how to deskew image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}