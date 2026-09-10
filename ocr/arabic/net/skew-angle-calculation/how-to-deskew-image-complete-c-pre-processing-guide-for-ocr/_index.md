---
category: general
date: 2026-01-13
description: كيفية تصحيح انحراف الصورة وإزالة الضوضاء منها في C# – تعلم زيادة تباين
  الصورة، ومعالجة الصورة مسبقًا للتعرف الضوئي على الأحرف (OCR)، وتطبيق فلاتر متعددة
  على الصورة.
draft: false
keywords:
- how to deskew image
- remove image noise
- increase image contrast
- preprocess image ocr
- multiple image filters
language: ar
og_description: كيفية تصحيح انحراف الصورة وإزالة الضوضاء منها في C# – تعلم زيادة تباين
  الصورة، ومعالجة الصورة مسبقًا لتقنية OCR، وتطبيق فلاتر متعددة على الصورة.
og_title: كيفية تصحيح انحراف الصورة – دليل شامل لمعالجة ما قبل C# للتعرف الضوئي على
  الأحرف
tags:
- OCR
- C#
- Image Processing
title: كيفية تصحيح ميل الصورة – دليل شامل لمعالجة ما قبل C# للتعرف الضوئي على الأحرف
url: /ar/net/skew-angle-calculation/how-to-deskew-image-complete-c-pre-processing-guide-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تُصحح انحراف الصورة – دليل شامل لمعالجة ما قبل الـ OCR بلغة C#

هل تساءلت يومًا **كيف تُصحح انحراف الصورة** قبل تمريرها إلى محرك OCR؟ لست وحدك. في العديد من السيناريوهات الواقعية—العقود الممسوحة، الإيصالات، أو النسخ القديمة—النص يكون مائلًا قليلًا، الصورة تبدو مشوشة، والتباين غير متساوٍ. الخبر السار؟ بضع أسطر من كود C# يمكنها أن تُعيد الصورة إلى وضعها المستقيم، تُزيل الضوضاء، وتزيد التباين، لتمنح الـ OCR أساسًا قويًا.

في هذا الدرس سنستعرض **مثالًا كاملاً قابلاً للتنفيذ** يوضح لك بالضبط كيفية تصحيح انحراف الصورة، إزالة الضوضاء، زيادة التباين، ثم تشغيل OCR باستخدام Aspose.OCR. في النهاية ستحصل على خط أنابيب قابل لإعادة الاستخدام يطبق **عدة فلاتر للصور** في استدعاء واحد سلس—بدون تخمين.

## ما الذي ستحتاجه

- **.NET 6+** (أو أي نسخة حديثة من .NET؛ الواجهة البرمجية تعمل بنفس الطريقة)
- حزمة NuGet **Aspose.OCR for .NET** (`Aspose.OCR` و `Aspose.OCR.Filters`)
- صورة ممسوحة ضوئيًا تجريبية (مثال: `skewed_noisy.png`) تحتوي على انحراف، ضوضاء، وتباين منخفض
- بيئة التطوير المفضلة لديك (Visual Studio، Rider، VS Code—اختر ما يناسبك)

إذا كان لديك مشروع جاهز، فقط أضف مرجع NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Filters
```

> **نصيحة احترافية:** Aspose تقدم نسخة تجريبية مجانية بعدد صفحات محدود—مثالية لتجربة الكود أدناه.

## الخطوة 1: إنشاء كائن محرك OCR

أول ما نقوم به هو إنشاء `OcrEngine`. فكر فيه كالعقل الذي سيقرأ النص لاحقًا. لا شيء معقد هنا، لكنه الأساس لكل ما سيأتي بعده.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:** تهيئة المحرك مرة واحدة وإعادة استخدامه لعدة صور يُجنبك تحميل بيانات اللغة مرارًا وتكرارًا.

## الخطوة 2: تحميل الصورة الممسوحة الخام

بعد ذلك نقوم بقراءة الصورة من القرص. طريقة `OcrImage.FromFile` تقرأ الملف إلى صيغة يمكن لـ Aspose معالجتها.

```csharp
        // Step 2: Load the raw scanned image (skewed, noisy, low‑contrast)
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");
```

> **حالة خاصة:** إذا كانت صورتك بصيغة غير قياسية (TIFF، BMP)، لا يزال Aspose يتعامل معها، لكن قد ترغب في تحويلها إلى PNG أولًا للاتساق.

## الخطوة 3: بناء خط أنابيب المعالجة المسبقة (تصحيح → إزالة الضوضاء → تحسين التباين)

هنا نجيب على السؤال الأساسي **كيف تُصحح انحراف الصورة** مع **إزالة ضوضاء الصورة** و**زيادة تباين الصورة**. تسمح لك الواجهة السلسة لـ Aspose بربط الفلاتر معًا، لتصبح الشيفرة كجملة.

```csharp
        // Step 3: Apply Deskew, Denoise, and Contrast filters in one pipeline
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())      // Corrects rotation
            .ApplyFilter(new DenoiseFilter())     // Reduces grainy artifacts
            .ApplyFilter(new ContrastFilter());   // Boosts foreground/background separation
```

### ما يقوم به كل فلتر

| الفلتر | الغرض | التأثير النموذجي |
|--------|-------|-------------------|
| **DeskewFilter** | يكتشف زاوية خطوط النص ويُدوّر الصورة لجعلها أفقية. | يزيل الميل الذي يربك الـ OCR، غالبًا ما يقلل معدلات الأخطاء بنسبة 30‑50 ٪. |
| **DenoiseFilter** | يطبق خوارزمية تمهيد تحافظ على الحواف وتزيل الضوضاء العشوائية. | ينظف الإيصالات الممسوحة أو الصور ذات الإضاءة الضعيفة، مما يجعل الأحرف أكثر وضوحًا. |
| **ContrastFilter** | يمدد المدرج التكراري بحيث تصبح المناطق الداكنة أغمق والفاتحة أفتح. | يحسّن التباين بين النص والخلفية، مفيد جدًا للوثائق الباهتة. |

> **لماذا نربطهم معًا؟** تصحيح الانحراف أولًا يضمن أن يعمل مرشح إزالة الضوضاء على صورة موجهة بشكل صحيح؛ وزيادة التباين في النهاية تجعل النص المنقّى يبرز للـ OCR.

## الخطوة 4: تنفيذ OCR على الصورة المعالجة

الآن بعد أن أصبحت الصورة مستقيمة، نظيفة، وعالية التباين، نمررها إلى محرك OCR. سنستخدم بيانات اللغة الإنجليزية، لكن Aspose يدعم أكثر من 150 لغة.

```csharp
        // Step 4: Recognize text using the English language pack
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);
```

إذا احتجت لغة أخرى، استبدل `OcrLanguage.English` بالقيمة المناسبة من الـ enum (مثال: `OcrLanguage.Spanish`).

## الخطوة 5: إخراج النص المُعرَّف

أخيرًا، نطبع النتيجة على وحدة التحكم. في تطبيق حقيقي قد تكتبها إلى ملف، قاعدة بيانات، أو تمرر النص إلى خطوط معالجة لغوية لاحقة.

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج الكامل على إيصال مائل نموذجي ينتج شيء مشابه لـ:

```
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
Thank you for your business!
```

إذا كان الإخراج غير واضح، تحقق من الصورة الأصلية—الطمس الزائد أو الظلام الشديد قد يتطلب معالجة إضافية (مثل `SharpenFilter`).

![مثال على تصحيح انحراف الصورة](images/deskewed_example.png "كيف تُصحح انحراف الصورة – قبل وبعد المعالجة")

*الصورة أعلاه تُظهر المسح المائل الأصلي على اليسار والإصدار المصحح، المنظف، وعالي التباين على اليمين.*

## نصائح إضافية ومخاطر شائعة

### 1. عندما تكون زاوية الانحراف شديدة

إذا كان المستند مائلًا بأكثر من 30°، قد يواجه `DeskewFilter` صعوبة. في هذه الحالة، قم بتدوير الصورة يدويًا مسبقًا:

```csharp
var manuallyRotated = rawImage.Rotate(45); // rotates 45 degrees clockwise
var processed = manuallyRotated.ApplyFilter(new DeskewFilter());
```

### 2. التعامل مع الصور الملونة

الفلاتر تعمل على التدرج الرمادي داخليًا، لكن يمكنك فرض التحويل:

```csharp
var grayImage = rawImage.ConvertToGrayscale();
var processed = grayImage.ApplyFilter(new DeskewFilter());
```

### 3. ضبط قوة إزالة الضوضاء

`DenoiseFilter` يقبل معاملًا اختياريًا `strength` (0‑100). القيم الأعلى تزيل المزيد من الضوضاء لكن قد تُطمس التفاصيل الدقيقة.

```csharp
.ApplyFilter(new DenoiseFilter(strength: 70))
```

### 4. استخدام فلاتر صور متعددة تتجاوز الأساسيات

Aspose يضم العديد من الفلاتر الأخرى: `SharpenFilter`، `BinarizeFilter`، `ResizeFilter`، إلخ. يمكنك دمجها لإنشاء خط أنابيب مخصص يناسب نوع المستند الخاص بك.

```csharp
var processed = rawImage
    .ApplyFilter(new DeskewFilter())
    .ApplyFilter(new DenoiseFilter())
    .ApplyFilter(new BinarizeFilter())
    .ApplyFilter(new SharpenFilter());
```

## مثال كامل جاهز للتنفيذ (انسخه‑الصقه)

فيما يلي البرنامج بالكامل، جاهز للإدراج في مشروع وحدة تحكم.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load the original scanned image
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // Build preprocessing pipeline: Deskew → Denoise → Contrast
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())
            .ApplyFilter(new DenoiseFilter())
            .ApplyFilter(new ContrastFilter());

        // Run OCR using English language
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);

        // Output recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

شغّل البرنامج باستخدام `dotnet run`. إذا تم الإعداد بشكل صحيح، ستظهر النصوص النظيفة والقابلة للقراءة في وحدة التحكم من الصورة المائلة والضوضائية الأصلية.

## الخلاصة

لقد استعرضنا **كيفية تصحيح انحراف الصورة** باستخدام C# مع **إزالة ضوضاء الصورة**، **زيادة تباين الصورة**، ومعالجة ما قبل OCR عبر سلسلة من **فلاتر الصور المتعددة**. الفكرة الأساسية هي أن خط أنابيب معالجة مسبقة منظم جيدًا يمكنه تحسين دقة OCR بشكل كبير—غالبًا ما يحول مسحًا شبه غير قابل للقراءة إلى نص واضح تمامًا.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال `ContrastFilter` بـ `BinarizeFilter` لتلاحظ كيف يؤثر التحويل إلى أبيض‑أسود على النتائج، أو جرب `ResizeFilter` لتزويد المحرك بصورة ذات دقة أعلى. النمط نفسه ينطبق بغض النظر عن الفلاتر التي تختارها، لذا لديك أساس مرن لجميع مشاريع OCR المستقبلية.

هل لديك أسئلة حول معالجة ملفات PDF، OCR متعدد اللغات، أو دمج هذا في API بـ ASP.NET؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}