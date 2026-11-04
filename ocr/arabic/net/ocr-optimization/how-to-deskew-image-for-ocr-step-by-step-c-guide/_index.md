---
category: general
date: 2026-03-04
description: تعرّف على كيفية تصحيح انحراف الصورة والتعرف على النص منها مع ضبط التباين
  لتحسين دقة التعرف الضوئي على الأحرف وتعزيز الصورة للتعرف الضوئي على الأحرف.
draft: false
keywords:
- how to deskew image
- recognize text from image
- how to apply contrast
- improve OCR accuracy
- enhance image for OCR
language: ar
og_description: كيفية تصحيح انحراف الصورة وتعزيز نتائج OCR. تعلم تطبيق التباين، تحسين
  دقة OCR، والتعرف على النص من الصورة باستخدام خطوط معالجة قابلة لإعادة الاستخدام.
og_title: كيفية تصحيح انحراف الصورة – دليل OCR كامل بلغة C#
tags:
- OCR
- C#
- image‑processing
title: كيفية تصحيح ميل الصورة للتعرف الضوئي على الأحرف – دليل خطوة بخطوة بلغة C#
url: /ar/net/ocr-optimization/how-to-deskew-image-for-ocr-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح إمالة الصورة – دليل C# OCR كامل

هل تساءلت يومًا **how to deskew image** حتى يقرأ محرك OCR الخاص بك النص فعليًا؟ لست وحدك. في العديد من المشاريع الواقعية—الإيصالات الممسوحة، العقود المصورة، أو الإيصالات الضبابية من كاميرا الهاتف—الصورة ليست مائلة بشكل مثالي. الصفحة المائلة تشوش على مُعرّف الأحرف، والنتيجة تكون عبارة عن خليط من الهراء.

الأخبار السارة؟ من خلال تصحيح إمالة الصورة **and** تعديل التباين يمكنك تحسين **improve OCR accuracy** بشكل كبير. في هذا الدليل سنستعرض مثالًا كاملًا بلغة C# يوضح لك بالضبط كيفية **recognize text from image** بعد تطبيق مرشح تصحيح الإمالة وتعزيز التباين. سنشرح أيضًا **how to apply contrast** بطريقة صحيحة، نناقش الحالات الخاصة، ونزودك بخط أنابيب قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع.

## ما ستحصل عليه من هذا الدليل

- شرح واضح لماذا تصحيح الإمالة والتباين مهمان لـ OCR.
- عينة كود C# جاهزة للتنفيذ تُنشئ خط أنابيب للمرشحات، وتربطه بمحرك OCR، وتقرأ عدة صور.
- نصائح لإعادة استخدام نفس خط الأنابيب لعدة ملفات، ومعالجة حالات الفشل، وقياس تحسين الدقة.
- روابط لمواضيع ذات صلة مثل تحويل الصورة إلى ثنائية، إزالة الضوضاء، و OCR متعدد اللغات (كل ذلك دون مغادرة الصفحة).

**المتطلبات المسبقة** – تحتاج إلى بيئة .NET 6+، ومكتبة OCR تدعم خط أنابيب للمرشحات (مثل Tesseract‑.NET، IronOCR، أو أي SDK تجاري)، وبعض ملفات PNG كعينة. لا حاجة لخدمات خارجية.

---

## الخطوة 1 – لماذا يعتبر تصحيح الإمالة أول شيء يجب القيام به

عندما يتم تدوير صفحة ممسوحة حتى بضع درجات، يرى محرك OCR خط الأساس لكل سطر بزاوية. معظم المُعرّفات تفترض نصًا أفقيًا؛ أي انحراف يقلل من درجات الثقة ويُدخل أخطاء استبدال.

> **نصيحة احترافية:** إذا أمكن، التقط الصورة على سطح مستوٍ وإضاءة جيدة؛ لا يمكن لإصلاحات البرمجيات أن تعوض تمامًا عن البيانات الجيدة.

في مصطلحات البرمجة، “how to deskew image” عادةً ما يعني اكتشاف اتجاه خط النص السائد وتدوير الصورة النقطية (bitmap) مرة أخرى إلى 0°. معظم SDKs الخاصة بـ OCR توفر `DeskewFilter` الذي يقوم بذلك تلقائيًا.

```csharp
// Create a deskew filter – it analyses the image and rotates it back.
var deskew = new DeskewFilter();
```

يفترض المرشح أن الصفحة تحتوي على نص أكثر من الخلفية، وهو ما ينطبق على معظم المستندات. إذا كان لديك صورة تحتوي على الكثير من المساحات الفارغة، قد تحتاج إلى خوارزمية احتياطية—لكن بالنسبة لمعظم ملفات PDF الممسوحة، الإعداد الافتراضي يعمل بشكل جيد.

---

## الخطوة 2 – تعزيز التباين لجعل الأحرف بارزة

التباين هو الفرق بين أغمق وأفتح البكسلات. المسحات ذات التباين المنخفض تبدو باهتة، ولا يستطيع محرك OCR تحديد مكان بدء أو انتهاء الحرف. بزيادة التباين نُحسّن “حدة” الفاصل البصري، مما **improves OCR accuracy**.

```csharp
// Set the contrast level – 1.0 is neutral, >1.0 brightens the darks and whites.
var contrast = new ContrastFilter { Level = 1.2 };
```

لماذا 1.2؟ عمليًا زيادة معتدلة (10‑30 %) تكفي. إذا دفعتها بعيدًا جدًا ستفقد التفاصيل الدقيقة، خاصةً في الخطوط الرفيعة. لا تتردد في التجربة؛ خط الأنابيب الذي سنبنيه لاحقًا يتيح لك تعديل المستوى دون إعادة تجميع التطبيق بالكامل.

---

## الخطوة 3 – بناء خط أنابيب مرشح قابل لإعادة الاستخدام

الآن نجمع المرشحين في خط أنابيب واحد. بهذه الطريقة يمكنك **recognize text from image** بنفس التحضير المسبق في كل مرة، مما يضمن نتائج متسقة.

```csharp
using YourOcrLibrary;          // Replace with the actual namespace of your OCR SDK
using YourOcrLibrary.Filters; // Namespace where DeskewFilter & ContrastFilter live

// Step 3: Build a filter pipeline that deskews the image and enhances contrast
var filterPipeline = new FilterBuilder()
    .Add(new DeskewFilter())                 // First: straighten the page
    .Add(new ContrastFilter { Level = 1.2 }) // Then: make the text pop
    .Build();
```

**لماذا خط أنابيب؟**  
- **قابلية التعديل:** إضافة أو إزالة المرشحات دون تعديل استدعاء OCR.  
- **الأداء:** يمكن للمكتبة تجميع العمليات، مما يقلل استهلاك الذاكرة.  
- **إعادة الاستخدام:** ربط نفس خط الأنابيب بعدة استدعاءات `engine.Recognize`.

---

## الخطوة 4 – ربط خط الأنابيب بمحرك OCR

معظم محركات OCR تعرض خاصية `Filters` أو طريقة `SetFilters`. من خلال تعيين خط الأنابيب هنا، تمر كل صورة لاحقة عبر تصحيح الإمالة + التباين قبل بدء تحليل الأحرف الفعلي.

```csharp
// Step 4: Attach the pipeline to the OCR engine so it processes images using these filters
var engine = new OcrEngine(); // Instantiate your OCR engine (configure language, etc.)
engine.Filters = filterPipeline;
```

إذا احتجت لتغيير نموذج اللغة (مثلاً English → Spanish) يمكنك القيام بذلك **قبل** ربط المرشحات؛ فالترتيب لا يهم لمرحلة التحضير المسبق.

---

## الخطوة 5 – التعرف على النص من الصورة الأولى

دعنا نضع خط الأنابيب قيد التنفيذ. سنحمّل ملف PNG، نشغّل OCR، ونطبع النتيجة. لاحظ أننا نستخدم نفس مثيل `engine`—لا حاجة لإعادة بناء المرشحات.

```csharp
// Step 5: Recognize text from the first image using the configured engine
var firstImagePath = @"C:\Images\doc1.png";
var firstResult = engine.Recognize(ImageInfo.Load(firstImagePath));

Console.WriteLine("=== First Document ===");
Console.WriteLine(firstResult.Text);
```

**ما يجب أن تراه:** نص نظيف وموجه بشكل صحيح مع عدد أقل بكثير من الأحرف المشوشة مقارنةً بالمسح الخام. إذا لاحظت أخطاءً ما زالت، فكر في إضافة `BinarizeFilter` (تحويل إلى أبيض وأسود نقي) بعد خطوة التباين.

---

## الخطوة 6 – إعادة استخدام نفس خط الأنابيب للملفات الإضافية

إحدى أكبر مزايا خط الأنابيب هو إمكانية إعادة استخدامه عبر العشرات من الملفات دون أي عبء إضافي.

```csharp
// Step 6: Recognize text from a second image to demonstrate reuse of the same pipeline
var secondImagePath = @"C:\Images\doc2.png";
var secondResult = engine.Recognize(ImageInfo.Load(secondImagePath));

Console.WriteLine("\n=== Second Document ===");
Console.WriteLine(secondResult.Text);
```

إذا كان لديك مجلد مليء بملفات PDF الممسوحة، فقط قم بالتكرار عبر `Directory.GetFiles(...)` واستدعِ `engine.Recognize` في كل مرة. تبقى خطوات تصحيح الإمالة والتباين ثابتة، وهو ما يُعد مفتاحًا لـ **enhance image for OCR** في وظائف الدفعات.

---

## مثال كامل يعمل – جمع كل شيء معًا

فيما يلي البرنامج الكامل المستقل. انسخه والصقه في مشروع وحدة تحكم جديد، أضف حزمة NuGet المناسبة لـ OCR SDK الخاص بك، وشغّله. سيظهر النص المُعترف به لصورتين عينة.

```csharp
// ------------------------------------------------------------
// Complete C# OCR Example – Deskew + Contrast Pipeline
// ------------------------------------------------------------
using System;
using System.IO;
using YourOcrLibrary;          // e.g., IronOcr, Tesseract.NET, etc.
using YourOcrLibrary.Filters; // Filters live here

class Program
{
    static void Main()
    {
        // 1️⃣ Build the filter pipeline (deskew + contrast)
        var filterPipeline = new FilterBuilder()
            .Add(new DeskewFilter())                 // Straighten the page
            .Add(new ContrastFilter { Level = 1.2 }) // Boost contrast a bit
            .Build();

        // 2️⃣ Create and configure the OCR engine
        var engine = new OcrEngine
        {
            // Example: set language to English (adjust as needed)
            Language = OcrLanguage.English,
            Filters = filterPipeline
        };

        // 3️⃣ Define image paths (replace with your own)
        string[] imagePaths = {
            @"C:\Images\doc1.png",
            @"C:\Images\doc2.png"
        };

        // 4️⃣ Process each image
        foreach (var path in imagePaths)
        {
            if (!File.Exists(path))
            {
                Console.WriteLine($"⚠️ File not found: {path}");
                continue;
            }

            var result = engine.Recognize(ImageInfo.Load(path));

            Console.WriteLine($"\n=== {Path.GetFileName(path)} ===");
            Console.WriteLine(result.Text);
        }

        Console.WriteLine("\n✅ All done – you have successfully deskewed and enhanced contrast for OCR!");
    }
}
```

### النتيجة المتوقعة

```
=== doc1.png ===
Invoice #12345
Date: 2024‑02‑15
Total: $1,250.00
...

=== doc2.png ===
Meeting Minutes
1. Project kickoff...
2. Budget approval...
...
```

إذا قارنت هذه النتيجة مع تشغيل **بدون** خط الأنابيب، ستلاحظ على الأرجح أحرفًا مفقودة، أرقامًا في غير موضعها، أو أسطر مشوشة تمامًا. هذا هو الأثر القابل للقياس لتعلم **how to deskew image** و **how to apply contrast** بشكل صحيح.

---

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كانت الصورة بالفعل موجهة بشكل صحيح؟* | يكشف `DeskewFilter` عن دوران 0° ويعيد الصورة النقطية الأصلية، لذا لا يوجد عبء تقريبًا. |
| *هل يمكنني استخدام هذا مع ملفات PDF؟* | نعم. معظم SDKs الخاصة بـ OCR تسمح بتحميل صفحة PDF كـ `ImageInfo`. يعمل نفس خط الأنابيب لأن الصورة النقطية الأساسية تُعالج بنفس الطريقة. |
| *وثائقي تحتوي على نص ملون—هل سيؤدي التباين إلى إتلاف الألوان؟* | يعمل مرشح التباين على الإضاءة (luminance)، لذا تُحافظ على الألوان ولكن تصبح أكثر وضوحًا. إذا كنت بحاجة إلى أبيض وأسود نقي، أضف `BinarizeFilter` بعد خطوة التباين. |
| *كيف أقيس تحسين الدقة؟* | شغّل OCR على مجموعة اختبار قبل وبعد خط الأنابيب، ثم احسب معدل خطأ الأحرف (CER) أو معدل خطأ الكلمات (WER). عادةً ما ستلاحظ انخفاضًا بنسبة 10‑30 % في الأخطاء. |
| *هل هناك تأثير على الأداء؟* | يضيف تصحيح الإمالة تكلفة CPU صغيرة (عادةً < 100 ms لكل صفحة). التباين عملية بسيطة على مستوى البكسل، لذا الأثر الكلي ضئيل مقارنةً بمرحلة OCR نفسها. |

---

## الخطوات التالية – ارتقِ بـ OCR إلى المستوى التالي

الآن بعد أن عرفت **how to deskew image**، **how to apply contrast**، وكيفية **recognize text from image** باستخدام خط أنابيب قابل لإعادة الاستخدام، فكر في استكشاف هذه المواضيع ذات الصلة:

- **تقليل الضوضاء** – أضف `MedianFilter` قبل تصحيح الإمالة لتنظيف البقع.
- **تحويل إلى ثنائي** – تحويل إلى أبيض وأسود نقي للغات ذات النصوص المعقدة.
- **معالجة متعددة الصفحات** – التكرار عبر صفحات PDF وتخزين النتائج في فهرس قابل للبحث.
- **نماذج اللغة** – التبديل بين `OcrLanguage.English` و `OcrLanguage.French` في الوقت الفعلي.
- **معالجة ما بعد** – استخدم التدقيق الإملائي أو regex لتصحيح الأخطاء الشائعة في OCR (مثلاً “0” مقابل “O”).

يمكن إدراج كل من هذه في سلسلة `FilterBuilder` نفسها، مما يمنحك حلاً قابلاً للتعديل وسهل الصيانة يُـ **enhances image for OCR** في أي خط إنتاج.

---

## الخلاصة

لقد غطينا كل ما تحتاج معرفته حول **how to deskew image** لـ OCR، ولماذا تعديل التباين طريقة رخيصة yet powerful لت **improve OCR accuracy**، وكيفية **recognize text from image** باستخدام نهج نظيف وقابل لإعادة الاستخدام

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}