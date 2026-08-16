---
category: general
date: 2026-03-29
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم التعرف الضوئي
  على الأحرف مع التدوير التلقائي وكيفية تصحيح ميل الصورة الممسوحة للحصول على نتائج
  مثالية.
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR. يوضح هذا الدليل خاصية
  التدوير التلقائي للـ OCR وكيفية تصحيح ميل الصورة الممسوحة ضوئيًا في C#.
og_title: استخراج النص من صورة في C# – OCR مع تدوير تلقائي وتصحيح الميل
tags:
- C#
- OCR
- Aspose
- Image Processing
title: استخراج النص من الصورة في C# – دليل OCR مع التدوير التلقائي وتصحيح الميل
url: /ar/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة في C# – دليل OCR مع التدوير التلقائي وتصحيح الميل

هل احتجت يوماً إلى **extract text from image** لكن الملف جاء بزاوية غريبة؟ هذه مشكلة شائعة—خاصةً عندما تتعامل مع فواتير ممسوحة ضوئياً، إيصالات مُصوَّرة، أو ملفات PDF مائلة. الخبر السار هو أنك لا تحتاج إلى كتابة خوارزمية تدوير مخصصة بنفسك. باستخدام ميزة *auto rotate OCR* المدمجة في Aspose OCR يمكنك السماح للمحرك بتصحيح الصورة ثم **extract text from image** في خطوة واحدة سلسة.

في هذا الدرس سنستعرض برنامج C# كامل جاهز للتنفيذ يقوم بـ:

* تهيئة محرك OCR مع التدوير التلقائي وتصحيح الميل،
* التعرف على صورة مائلة أو مائلة قليلاً،
* إرجاع كل من زاوية الدوران المكتشفة والنص المستخرج.

بدون خدمات خارجية، بدون حسابات رياضية معقدة—فقط بضع أسطر من الشيفرة وتوضيح واضح لـ *how to deskew scanned image* عند الحاجة.

## ما الذي ستحتاجه

| المتطلب المسبق | لماذا يهم |
|----------------|-----------|
| .NET 6.0 أو أحدث (أو .NET Framework 4.6+) | Aspose OCR يُوزَّع كحزمة NuGet تستهدف هذه البيئات. |
| Visual Studio 2022 (أو أي محرر C#) | يسهل إضافة حزم NuGet وتشغيل تطبيق الكونسول. |
| صورة نموذجية (`rotated_document.jpg`) | يجب أن تكون الصورة بصيغة JPEG أو PNG أو BMP أو TIFF وليست موجهة تماماً. |
| حزمة NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | توفر الفئات `OcrEngine`، `PreprocessingFilters`، وغيرها. |

إذا كان كل ما سبق متوفرًا، فأنت جاهز للبدء. وإلا، قم بتحميل أحدث نسخة من Aspose OCR عبر NuGet—التثبيت بنقرة واحدة.

---

## الخطوة 1 – تهيئة محرك OCR (الكلمة المفتاحية الأساسية في التنفيذ)

أول ما نقوم به هو إنشاء كائن `OcrEngine` وإخبارها بـ **auto rotate OCR** و **deskew** لأي صورة واردة. يتم دمج هذين العلمين باستخدام عملية OR البتية (`|`) لأن `PreprocessingFilters` هو تعداد يحمل صفة `[Flags]`.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **لماذا هذا مهم:**  
> *Auto‑rotate OCR* يفحص خط أساس النص في الصورة، يخمن الاتجاه الصحيح، ويقوم بتدويره داخلياً قبل التعرف. *Auto‑deskew* يفعل الشيء نفسه للانحرافات الطفيفة التي تظهر غالباً في المستندات الممسوحة. بتمكينهما معاً، تضمن أفضل نتائج **extract text from image** دون تعديل يدوي للصورة.

---

## الخطوة 2 – التعرف على الصورة واسترجاع النتيجة

الآن نمرّر مسار الملف إلى المحرك. تُعيد الدالة `RecognizeImage` كائن `OcrResult` يحتوي على زاوية الدوران المكتشفة، درجات الثقة، والنص الناتج.

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **نصيحة:** إذا كنت تتعامل مع تدفق (مثلاً ملف تم رفعه)، استخدم `ocrEngine.RecognizeImage(Stream)` بدلاً من ذلك. تُطبق نفس أعلام المعالجة المسبقة، لذا ستحصل على فوائد **auto rotate OCR**.

---

## الخطوة 3 – عرض زاوية الدوران والنص المستخرج

أخيراً، نطبع معلومتين إلى الكونسول: الزاوية التي يعتقد المحرك أن الصورة تحتاج إلى تدويرها، والنص الفعلي الذي استخرجه.

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**الناتج المتوقع** (ستختلف أرقامك بناءً على الصورة المدخلة):

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

إذا كانت الصورة موجهة أصلاً، ستكون زاوية الدوران `0°`، وستظل تحصل على نص نظيف بفضل خوارزمية *auto‑deskew*.

---

## الخطوة 4 – فهم كيفية تصحيح الميل في الصور الممسوحة (غوص عميق في الكلمة المفتاحية الثانوية)

قد تتساءل *how to deskew scanned image* عندما يُظهر محرك OCR زاوية غير صفرية. في الخلفية، يستخدم Aspose OCR **تحويل هوغ** لاكتشاف اتجاه الخط النصي السائد. ثم يدور البت ماب بالزاوية المعاكسة، مما يُعيد النص إلى وضعه المستقيم.

**متى يكون ذلك مهماً؟**  
* الماسحات التي تُدخل الورق بزاوية طفيفة (شائع في بيئات المكاتب).  
* الصور التي تُلتقط بالهواتف الذكية يدويًا—الأفق نادراً ما يكون مثالياً.  

**معالجة الحالات الحدية:**  
إذا كانت قيمة `RotationAngle` في النتيجة كبيرة بشكل غير عادي (مثلاً > 45°)، قد يكون المحرك قد فسر الصورة خطأً (ربما يكون شعارًا أو رسمًا غير نصي). في هذه الحالة يمكنك:

1. تدوير الصورة يدويًا باستخدام `System.Drawing` قبل تمريرها إلى المحرك، أو  
2. تعطيل `AutoRotate` والاحتفاظ بـ `AutoDeskew` فقط إذا كنت تعلم أن المستند موجه أصلاً.

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## الخطوة 5 – الأخطاء الشائعة والنصائح الاحترافية (E‑E‑A‑T في التنفيذ)

| الخطأ | السبب | الحل |
|-------|--------|------|
| **صور ضبابية أو منخفضة الدقة** | دقة OCR تنخفض بشكل كبير؛ قد يفشل اكتشاف الدوران. | استخدم مسحات بدقة لا تقل عن 300 dpi؛ طبّق مرشح شحذ قبل OCR. |
| **لغات مختلطة** | المحرك يفرض الإنجليزية افتراضيًا؛ الأحرف الأجنبية تصبح مشوهة. | عيّن `Language = Language.English | Language.Spanish` (أو أي تركيبة مناسبة). |
| **ملفات كبيرة (> 10 MB)** | الضغط على الذاكرة قد يسبب استثناء `OutOfMemoryException`. | قلل أبعاد الصورة أولاً، أو عالجها على أجزاء باستخدام `OcrEngine.RecognizeRegion`. |
| **مسار ملف غير صحيح** | استثناء `FileNotFoundException` يوقف البرنامج. | استخدم `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` للموثوقية. |

> **نصيحة احترافية:** دوّن دائمًا `ocrResult.RotationAngle` و `ocrResult.Confidence` (إن توفرت). تساعدك هذه المقاييس في اتخاذ قرار ما إذا كان من المفيد إعادة المحاولة بإعدادات معالجة مسبقة مختلفة.

---

## الخطوة 6 – توسيع المثال (ما التالي؟)

الآن بعد أن أصبحت قادرًا على **extract text from image** مع التدوير التلقائي وتصحيح الميل، فكر في الخطوات التالية:

* **معالجة دفعات** – كرّر عبر مجلد من الصور، خزن كل نتيجة في قاعدة بيانات، وضع علامة على أي صورة ذات `RotationAngle > 5°` للمراجعة اليدوية.  
* **تحويل إلى PDF** – دمج النص المستخرج مع الصورة الأصلية لإنشاء PDF قابل للبحث باستخدام Aspose.PDF.  
* **اكتشاف اللغة** – استخدم علم `AutoDetectLanguage` في Aspose.OCR لتمكين المحرك من اختيار اللغة الأنسب تلقائيًا.  

كل هذه الأفكار تعتمد على المبدأ الأساسي نفسه: دع المكتبة تتعامل مع الاتجاه، وركز أنت على منطق العمل.

---

## مثال كامل جاهز للتنفيذ (انسخه‑ألصقه)

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

احفظ الملف باسم `Program.cs`، نفّذ `dotnet add package Aspose.OCR`، ثم `dotnet run`. يجب أن ترى الزاوية والنص النظيف يُطبعان في الكونسول.

---

## الخلاصة

لقد استعرضنا كيفية **extract text from image** في C# مع السماح لـ Aspose OCR بالاعتناء بـ *auto rotate OCR* ومشكلة *how to deskew scanned image* الصعبة. بتمكين علمي المعالجة المسبقة، يقوم المحرك تلقائيًا بتصحيح الصور المائلة، يحدد الاتجاه الصحيح، ويُنتج نصًا دقيقًا—دون الحاجة لتعديل يدوي للصورة.

لا تتردد في تجربة دفعات أكبر، لغات مختلفة، أو دمج الناتج في PDF قابل للبحث. السماء هي الحد عندما يتولى محرك OCR الجزء الأكبر من العمل.

**هل أنت مستعد للارتقاء بسلسلة معالجة المستندات لديك؟** احصل على الشيفرة، وجهها إلى مسحاتك الخاصة، وشاهد زوايا الدوران تختفي. إذا واجهت أي صعوبات، اترك تعليقًا أدناه—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}