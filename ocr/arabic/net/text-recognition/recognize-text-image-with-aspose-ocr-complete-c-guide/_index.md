---
category: general
date: 2026-06-22
description: تعلم كيفية التعرف على صورة النص واستخراج النص من الفواتير عالية الدقة
  باستخدام Aspose OCR. يتضمن تعيين لغة OCR وتسريع GPU.
draft: false
keywords:
- recognize text image
- extract text image
- high resolution ocr
- process invoice ocr
- set ocr language
language: ar
og_description: التعرف على النص في الصورة باستخدام Aspose OCR في C#. يوضح هذا الدرس
  كيفية استخراج النص من صور الفواتير عالية الدقة، وتعيين لغة OCR، وتعزيز الأداء.
og_title: التعرف على نص الصورة باستخدام Aspose OCR – دليل كامل بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to recognize text image and extract text image from high
    resolution OCR invoices using Aspose OCR. Includes set OCR language and GPU acceleration.
  headline: recognize text image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Learn how to recognize text image and extract text image from high
    resolution OCR invoices using Aspose OCR. Includes set OCR language and GPU acceleration.
  name: recognize text image with Aspose OCR – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code also works on .NET Framework 4.7+). -
      A valid Aspose.OCR NuGet package (free trial works fine). - A high‑resolution
      image of an invoice (e.g., `high_res_invoice.png`). - Basic familiarity with
      C# and Visual Studio or your favorite IDE.'
  - name: 1. Image Quality Matters
    text: Even the fastest GPU can’t fix a blurry scan. Aim for at least **300 dpi**
      for invoices; lower resolutions cause missed characters. If you can’t control
      the source, consider pre‑processing with a sharpening filter before sending
      the image to Aspose.
  - name: 2. Memory Consumption on Very Large Files
    text: A 5000 × 7000 pixel PNG can consume several hundred megabytes of RAM. If
      you hit `OutOfMemoryException`, split the invoice into pages or downscale slightly
      (e.g., to 250 dpi) before OCR.
  - name: 3. Fallback to CPU When GPU Fails
    text: If the GPU driver crashes, Aspose will silently revert to CPU. To ensure
      you’re always using the GPU, check `ocrEngine.ProcessingMode` after initialization
      and log a warning if it isn’t `ProcessingMode.Gpu`.
  - name: 4. Multi‑Language Documents
    text: 'When an invoice contains both English and Spanish, you can enable **multiple
      languages**:'
  type: HowTo
tags:
- Aspose OCR
- C#
- Image Processing
title: التعرف على النص في الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/recognize-text-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# recognize text image with Aspose OCR – دليل C# الكامل

هل احتجت يوماً إلى **recognize text image** لكن النتائج كانت غير واضحة أو بطيئة بشكل مؤلم؟ لست وحدك. سواءً كنت تمسح فاتورة عالية الدقة أو تستخرج بيانات من عقد ممسوح، الحصول على مخرجات نظيفة وموثوقة أمر حاسم. في هذا الدرس سنستعرض مثالاً كاملاً جاهزاً للتنفيذ يقوم بـ **recognize text image** من ملف عالي الدقة، **extract text image**، وحتى **set OCR language** للحصول على أفضل دقة—كل ذلك مع الاستفادة من تسريع الـ GPU.

سنضيف أيضاً بعض الحيل الإضافية: كيفية **process invoice OCR** بفعالية، لماذا قد تحتاج إلى **high resolution OCR**، وماذا تفعل عندما لا يتوفر الـ GPU. في النهاية ستحصل على برنامج C# واحد يحول صورة PNG ضبابية إلى نص قابل للبحث في لحظة.

## ما ستتعلمه

- كيفية إنشاء مثيل `OcrEngine` باستخدام Aspose OCR.
- تفعيل **GPU acceleration** للحصول على **high resolution OCR** سريع كالصاعقة.
- استخدام **set OCR language** لاستهداف الإنجليزية (أو أي لغة مدعومة أخرى).
- **Extract text image** من ملف فاتورة عالي الدقة.
- قياس زمن المعالجة لتثبت الفوائد الأداء.
- التعامل مع سيناريوهات fallback عندما لا يكون الـ GPU موجوداً.

### المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل أيضاً على .NET Framework 4.7+).
- حزمة Aspose.OCR NuGet صالحة (الإصدار التجريبي المجاني يكفي).
- صورة عالية الدقة لفاتورة (مثال: `high_res_invoice.png`).
- إلمام أساسي بـ C# وVisual Studio أو أي بيئة تطوير تفضّلها.

---

## الخطوة 1: تثبيت Aspose.OCR وتحضير المشروع

أولاً—أضف مكتبة Aspose OCR إلى مشروعك. افتح الطرفية في مجلد الحل وشغّل:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة محترف:** حافظ على تحديث الحزمة؛ الإصدارات الأحدث تحسّن دعم الـ GPU ونماذج اللغات.

أنشئ تطبيق console جديد إذا لم يكن لديك واحد بالفعل:

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
```

الآن لديك بيئة نظيفة للـ **recognize text image**.

## الخطوة 2: تهيئة محرك OCR (تمكين GPU)

القلب النابض للعملية هو `OcrEngine`. بشكل افتراضي يعمل على الـ CPU، لكن لـ **high resolution OCR** على مسح الفواتير الكبيرة يمكن للـ GPU أن يختصر الثواني من زمن التنفيذ.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // Enable GPU processing – dramatically speeds up high‑resolution OCR
    ProcessingMode = ProcessingMode.Gpu
};
```

> **لماذا GPU؟** الصورة عالية الدقة قد تحتوي على ملايين البكسلات. الـ GPU يعالجها بالتوازي، محوّلاً مهمة تستغرق 5 ثوانٍ على الـ CPU إلى عملية تحت الثانية على معظم بطاقات الرسوميات الحديثة.

إذا كان الجهاز المستهدف لا يملك GPU متوافق، سيعود Aspose تلقائياً إلى وضع الـ CPU. يمكنك اكتشاف هذا الـ fallback هكذا:

```csharp
if (ocrEngine.ProcessingMode != ProcessingMode.Gpu)
{
    Console.WriteLine("GPU not available – using CPU fallback.");
}
```

## الخطوة 3: **set OCR language** – اختيار القاموس المناسب

Aspose OCR يأتي مع لغات أساسية؛ الإنجليزية هي الافتراضية، لكن يمكنك تعيينها صراحة. هذا مهم لأن نموذج اللغة يؤثر على تجزئة الأحرف والبحث في القاموس.

```csharp
// Step 3: Explicitly set the language to English (core language)
ocrEngine.Language = OcrLanguage.English;
```

> **حالة خاصة:** إذا احتجت قراءة فاتورة فرنسية، استبدل `OcrLanguage.English` بـ `OcrLanguage.French`. نفس استدعاء **set OCR language** يعمل مع أي لغة مدعومة.

## الخطوة 4: **recognize text image** – معالجة فاتورة عالية الدقة

الآن نبدأ فعلياً بـ **recognize text image**. وجه المحرك إلى ملف PNG (أو TIFF) عالي الدقة ترغب في معالجته. يمكن أن يكون المسار مطلقاً أو نسبياً؛ فقط تأكد من وجود الملف.

```csharp
// Step 4: Recognize the image and capture the result
string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);
```

كائن `OcrResult` يحتوي على النص المستخرج ومعلومات الوقت، وسنعرضهما لاحقاً.

## الخطوة 5: **extract text image** – عرض النتائج وزمن المعالجة

أخيراً، اطبع نص الـ OCR والمدة التي استغرقها. هذه هي اللحظة التي يمكنك فيها التأكد من أن **process invoice OCR** نفّذ كما هو متوقع.

```csharp
// Step 5: Output processing time and extracted text
Console.WriteLine($"GPU OCR time: {ocrResult.ProcessingTimeMs} ms");
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("=== Extracted Text End ===");
```

تشغيل البرنامج يجب أن ينتج شيئاً مثل:

```
GPU OCR time: 312 ms
=== Extracted Text Start ===
Invoice #12345
Date: 2024‑04‑15
Total: $1,250.00
...
=== Extracted Text End ===
```

وهكذا—انتهى سير عمل **extract text image** الخاص بك.

---

## إضافات: التعامل مع المشكلات الشائعة

### 1. جودة الصورة مهمة

حتى أسرع GPU لا يمكنه إصلاح مسح ضبابي. استهدف على الأقل **300 dpi** للفواتير؛ الدقة الأقل تؤدي إلى فقدان الأحرف. إذا لم تستطع التحكم بالمصدر، فكر في معالجة مسبقة بفلتر تحسين قبل إرسال الصورة إلى Aspose.

### 2. استهلاك الذاكرة للملفات الضخمة

صورة PNG بحجم 5000 × 7000 بكسل قد تستهلك مئات الميجابايت من الذاكرة. إذا واجهت `OutOfMemoryException`، قسّم الفاتورة إلى صفحات أو قلل الدقة قليلاً (مثلاً إلى 250 dpi) قبل الـ OCR.

### 3. الرجوع إلى CPU عندما يفشل GPU

إذا تعطل برنامج تشغيل الـ GPU، سيعود Aspose صامتاً إلى الـ CPU. لضمان أنك تستخدم الـ GPU دائماً، تحقق من `ocrEngine.ProcessingMode` بعد التهيئة وسجّل تحذيراً إذا لم يكن `ProcessingMode.Gpu`.

### 4. مستندات متعددة اللغات

عندما تحتوي الفاتورة على الإنجليزية والإسبانية معاً، يمكنك تمكين **multiple languages**:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

سوف يحاول المحرك التعرف على الأحرف من أي من مجموعتي اللغات.

---

## مثال كامل يعمل

فيما يلي البرنامج **الكامل القابل للتنفيذ** الذي يدمج كل خطوة تم مناقشتها. انسخه إلى `Program.cs`، عدّل مسار الصورة، واضغط **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 2: Create an OCR engine instance and enable GPU acceleration
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu // Fast high‑resolution OCR
        };

        // Verify GPU availability (optional but helpful)
        if (ocrEngine.ProcessingMode != ProcessingMode.Gpu)
        {
            Console.WriteLine("GPU not detected – falling back to CPU processing.");
        }

        // Step 3: Set the OCR language (set OCR language for better accuracy)
        ocrEngine.Language = OcrLanguage.English; // Change as needed

        // Step 4: Recognize text from a high‑resolution invoice image
        string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // Step 5: Display processing time and the extracted text
        Console.WriteLine($"GPU OCR time: {ocrResult.ProcessingTimeMs} ms");
        Console.WriteLine("=== Extracted Text Start ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("=== Extracted Text End ===");
    }
}
```

**الناتج المتوقع** (الأوقات ستختلف حسب العتاد):

```
GPU OCR time: 287 ms
=== Extracted Text Start ===
Invoice #98765
Date: 2024‑03‑22
Amount Due: $2,340.00
...
=== Extracted Text End ===
```

جرّبه على عدة فواتير مختلفة لترى كيف يبقى زمن المعالجة أقل من نصف ثانية على GPU متوسط.

---

## الخلاصة

لقد تعلمت الآن كيفية **recognize text image** باستخدام Aspose OCR، **extract text image** من فاتورة عالية الدقة، و**set OCR language** للحصول على أفضل النتائج—كل ذلك مع الاستفادة من تسريع الـ GPU لـ **high resolution OCR**. الكود المعروض جاهز للإنتاج، يتضمن منطق fallback، ويمكن توسيعه لمعالجة ملفات PDF متعددة الصفحات، لغات مختلفة، أو حتى تدفقات كاميرا في الوقت الفعلي.

الخطوات التالية؟ جرّب:

- تحويل النص المستخرج إلى كائن JSON منظم للفاتورة.
- إضافة معالجة مسبقة للصورة (تصحيح الميل، التحويل إلى ثنائي) لتحسين الدقة على المسحات منخفضة الجودة.
- دمج استدعاء OCR في API بـ ASP.NET Core حتى يتمكن خدمتك الويب من معالجة الفواتير عند الطلب.

هل لديك أسئلة حول **process invoice OCR** أو تحتاج مساعدة في تعديل حزم اللغة؟ اترك تعليقاً أدناه، وبرمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}