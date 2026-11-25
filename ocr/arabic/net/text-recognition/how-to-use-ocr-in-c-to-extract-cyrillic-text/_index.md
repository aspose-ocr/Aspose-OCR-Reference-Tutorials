---
category: general
date: 2026-09-10
description: كيفية استخدام OCR في C# لاستخراج النص السيريلي، ومعالجة الصور مسبقًا،
  وتحويلها إلى ملفات PDF أو HTML في مثال واحد قابل للتنفيذ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- preprocess image for OCR
- convert image to PDF
- convert image to HTML
- extract Cyrillic text
language: ar
lastmod: 2026-09-10
og_description: كيفية استخدام OCR في C# لاستخراج النص السيريلي، ومعالجة الصور مسبقًا،
  وتصدير النتائج كملف PDF أو HTML. اتبع هذا الدليل خطوة بخطوة.
og_image_alt: Diagram illustrating how to use OCR to extract Cyrillic text and convert
  images
og_title: كيفية استخدام OCR في C# – استخراج النص السيريلي وتحويل الصور
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to use OCR in C# to extract Cyrillic text, preprocess images, and
    convert them to PDF or HTML files in a single, runnable example.
  headline: How to use OCR in C# to extract Cyrillic text
  type: TechArticle
tags:
- OCR
- C#
- Cyrillic
- Image processing
- PDF conversion
title: كيفية استخدام OCR في C# لاستخراج النص السيريلي
url: /ar/net/text-recognition/how-to-use-ocr-in-c-to-extract-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# لاستخراج النص السيريلي

إذا كنت بحاجة إلى **كيفية استخدام OCR** في C# لاستخراج النص السيريلي من المستندات الممسوحة ضوئياً، فإن هذا الدليل يوضح لك حلاً كاملاً وجاهزًا للتنفيذ. ستتعلم أيضًا كيفية **معالجة الصورة مسبقًا لـ OCR**، وكيفية **تحويل الصورة إلى PDF** أو **تحويل الصورة إلى HTML** بمجرد التعرف على النص.

غالبًا ما تواجه مشاريع رقمنة المستندات مشكلتين: المسحات منخفضة الجودة والحاجة إلى تخزين النتائج بأكثر من تنسيق. يحل هذا الدرس كلا المشكلتين باستخدام مكتبة Aspose.OCR، التي تقوم تلقائيًا بتنزيل حزم اللغات المفقودة، وتوفر أدوات معالجة صور مدمجة، ويمكنها تصدير نتيجة OCR إلى PDF أو HTML بنقرة واحدة.

## المتطلبات المسبقة

* .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+).
* Visual Studio 2022 أو أي محرر يدعم مشاريع C#.
* حزمة **Aspose.OCR** NuGet. قم بتثبيتها باستخدام:

```bash
dotnet add package Aspose.OCR
```

* ملف صورة يحتوي على أحرف سيريلي (مثال: `sample_cyrillic.jpg`).  
  ضع الملف في مجلد يمكنك الإشارة إليه كـ `YOUR_DIRECTORY`.

ستقوم المكتبة بتنزيل حزمة اللغة السيريليّة في المرة الأولى التي تقوم فيها بتعيين `ocrEngine.Language = Language.Cyrillic;`، لذا لا يلزم تنزيل يدوي.

## الخطوة 1 – تهيئة محرك OCR (كيفية استخدام OCR)

إنشاء نسخة من `OcrEngine` يجهّز المحرك لجميع العمليات اللاحقة.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine – the first step in how to use OCR with Aspose
        var ocrEngine = new OcrEngine();
```

**لماذا هذا مهم:** يحتفظ المحرك بالإعدادات مثل اللغة، وإعدادات معالجة الصورة، وخيارات الإخراج. تهيئته مرة واحدة يحافظ على نظافة باقي الكود ويجعلها آمنة للخطوط المتعددة.

## الخطوة 2 – اختيار اللغة السيريليّة (استخراج النص السيريلي)

```csharp
        // Select Cyrillic language; the pack is fetched automatically if missing
        ocrEngine.Language = Language.Cyrillic;
```

**لماذا هذا مهم:** تعتمد دقة OCR بشكل كبير على نموذج اللغة الصحيح. باختيار `Language.Cyrillic` صراحةً، يطبق المحرك جداول تردد الأحرف المناسبة للروسية، الأوكرانية، البلغارية، وغيرها.

## الخطوة 3 – معالجة الصورة مسبقًا لـ OCR

المسحات منخفضة الجودة قد تحتوي على ميل، أو بقع، أو إضاءة غير متساوية. يمكن لـ `ImageProcessor` المدمج تحسين معدلات التعرف من خلال ندوتين فقط.

```csharp
        // Optional but strongly recommended: deskew and despeckle the image
        ocrEngine.ImageProcessor.Deskew();      // Aligns rotated text
        ocrEngine.ImageProcessor.Despeckle();  // Removes isolated noise pixels
```

**لماذا هذا مهم:** تقلل المعالجة المسبقة من الأخطاء في الأحرف وتزيد من درجة الثقة. النص المائل غالبًا ما ينتج مخرجات مشوشة؛ تصحيح الميل يجعله مستقيمًا. إزالة البقع تقضي على القطع الصغيرة التي قد يفسرها محرك OCR كحروف.

> **نصيحة احترافية:** إذا كانت الصور المصدرية نظيفة بالفعل، يمكنك تخطي هذه النداءات. بالنسبة للمسحات المتدهورة بشدة، فكر في خطوات إضافية مثل `Binarize()` أو `ContrastStretch()`.

## الخطوة 4 – تنفيذ OCR على صورة الإدخال

```csharp
        // The image path can be absolute or relative to the executable
        string inputPath = Path.Combine("YOUR_DIRECTORY", "sample_cyrillic.jpg");
        ocrEngine.Process(inputPath);
```

**لماذا هذا مهم:** `Process` تشغل خط أنابيب التعرف على الصورة المقدمة. لا تُعيد قيمة (`void`); يصبح النص المُعترف به متاحًا عبر الخاصية `Text`.

## الخطوة 5 – استرجاع النص المُعترف به وحفظه إلى ملف

```csharp
        // Access the recognized string
        string recognizedText = ocrEngine.Text;

        // Save the plain‑text result
        string txtOutput = Path.Combine("YOUR_DIRECTORY", "result.txt");
        File.WriteAllText(txtOutput, recognizedText);
        Console.WriteLine("Text saved to: " + txtOutput);
```

**لماذا هذا مهم:** تخزين النص الأصلي يتيح معالجة لاحقة مثل البحث، الفهرسة، أو إرساله إلى خدمات الترجمة.

## الخطوة 6 – تصدير نتيجة OCR إلى صيغ أخرى (تحويل الصورة إلى PDF وتحويل الصورة إلى HTML)

```csharp
        // Export as PDF – useful for archival or sharing with non‑technical users
        string pdfOutput = Path.Combine("YOUR_DIRECTORY", "result.pdf");
        ocrEngine.SaveResultAsPdf(pdfOutput);
        Console.WriteLine("PDF saved to: " + pdfOutput);

        // Export as HTML – retains basic layout and can be displayed in browsers
        string htmlOutput = Path.Combine("YOUR_DIRECTORY", "result.html");
        ocrEngine.SaveResultAsHtml(htmlOutput);
        Console.WriteLine("HTML saved to: " + htmlOutput);
    }
}
```

**لماذا هذا مهم:** تحويل نتيجة OCR إلى PDF أو HTML يتيح لك الحفاظ على السياق البصري للصورة الأصلية مع توفير نص قابل للبحث. هذا ذو قيمة خاصة في عمليات العمل القانونية أو الأرشيفية.

### النتيجة المتوقعة

تشغيل البرنامج مع مسح سيريلي واضح ينتج ثلاثة ملفات:

* `result.txt` – نص Unicode عادي، مثال: `Пример текста на кириллице`.
* `result.pdf` – ملف PDF يحتوي على الصورة مع طبقة نص غير مرئية للبحث.
* `result.html` – صفحة HTML تعرض الصورة والنص القابل للتحديد.

افتح أيًا من الملفات للتحقق من أن الأحرف السيريليّة قد تم استخراجها بشكل صحيح.

## أسئلة شائعة وحالات خاصة

| السؤال | الإجابة |
|----------|--------|
| **ماذا لو فشل تحميل حزمة اللغة؟** | تأكد من أن الجهاز لديه اتصال بالإنترنت. يمكنك أيضًا تنزيل الحزمة مسبقًا من موقع Aspose ووضعها في مجلد `bin`. |
| **هل يمكنني التعرف على أبجديات أخرى في نفس التشغيل؟** | نعم. استدعِ `ocrEngine.Language = Language.English;` (أو أي تعداد مدعوم) قبل `Process`. قد تحتاج إلى تشغيل `Process` بشكل منفصل لكل لغة إذا كانت الصورة تحتوي على نصوص مختلطة. |
| **صورة TIFF متعددة الصفحات – هل يعمل هذا؟** | `OcrEngine` يعالج صورة bitmap واحدة في كل مرة. حمّل كل صفحة إلى `Bitmap` واستدعِ `Process` داخل حلقة، مع دمج النتائج. |
| **كيف يمكنني زيادة الأداء للدفعات الكبيرة؟** | أعد استخدام نسخة واحدة من `OcrEngine` واضبط `ocrEngine.OptimizeMemory = true;`. كما يمكنك التفكير في المعالجة المتوازية باستخدام نسخ منفصلة من المحرك لكل خيط. |

## الخلاصة

أنت الآن تعرف **كيفية استخدام OCR** في C# **لاستخراج النص السيريلي**، **معالجة الصورة مسبقًا لـ OCR**، و**تحويل الصورة إلى PDF** أو **تحويل الصورة إلى HTML** في بضع خطوات مختصرة. المثال الكامل يوضح تطبيقًا إنتاجيًا‑

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة من الشيفرة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية استخدام AspOCR: مرشحات معالجة صورة OCR لـ .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [كيفية استخراج نص OCR في C# – دليل خطوة بخطوة كامل](/ocr/english/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/)
- [كيفية استخدام Aspose OCR للحصول على نتيجة JSON في التعرف على الصور](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}