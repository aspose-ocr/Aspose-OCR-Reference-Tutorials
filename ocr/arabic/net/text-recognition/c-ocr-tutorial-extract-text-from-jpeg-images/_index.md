---
category: general
date: 2026-01-04
description: دروس OCR بلغة C# توضح كيفية استخراج النص من JPEG، وإجراء OCR على الصورة،
  والتعرف على النص من الفاتورة باستخدام تسريع GPU.
draft: false
keywords:
- c# OCR tutorial
- extract text from JPEG
- perform OCR on image
- load image for OCR
- recognize text from receipt
language: ar
og_description: دروس C# OCR ترشدك خلال تحميل صورة للتعرف الضوئي على الأحرف، استخراج
  النص من JPEG، والتعرف على النص من الفاتورة بدعم وحدة معالجة الرسومات.
og_title: دورة C# OCR – استخراج النص من صور JPEG
tags:
- C#
- OCR
- Image Processing
title: دروس OCR بلغة C# – استخراج النص من صور JPEG
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-jpeg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# OCR – استخراج النص من صور JPEG

هل احتجت يوماً إلى **c# OCR tutorial** لاستخراج النص من إيصال ممسوح ضوئياً أو صورة لوثيقة؟ لست وحدك. في العديد من التطبيقات الواقعية—متتبعات المصاريف، إدخال البيانات الآلي، أو حتى أداة ملاحظات سريعة—ستجد نفسك بحاجة إلى **extract text from JPEG** في الوقت الفعلي.

في هذا الدليل سنقدم لك حلاً كاملاً وجاهزاً للتنفيذ. ستتعلم كيف **load image for OCR**، **perform OCR on image**، وأخيراً **recognize text from receipt** باستخدام محرك مدعوم بتسريع GPU. لا اختصارات “انظر الوثائق” الغامضة—فقط الشيفرة الكاملة، شرح لماذا كل سطر مهم، ونصائح لتجنب الأخطاء الشائعة.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يستخدم صsyntax C# الحديثة).  
- مكتبة OCR تُوفر فئة `OcrEngine` مع كائن `Config`—معظم SDKs التجارية تتبع هذا النمط.  
- بطاقة رسومية متوافقة مع CUDA إذا أردت التسريع الاختياري (إلا فإن fallback على CPU يعمل بشكل جيد).  
- صورة JPEG تجريبية، مثل `receipt.jpg`، موجودة في مجلد يمكنك الإشارة إليه.

هذا كل شيء. إذا كان لديك Visual Studio، افتح مشروع كونسول جديد وستكون جاهزاً للنسخ‑اللصق.

![c# OCR tutorial example showing a receipt image being processed](https://example.com/placeholder.jpg "c# OCR tutorial example")

*(نص بديل: دليل c# OCR – لقطة شاشة لمحرك OCR يعالج صورة إيصال)*

## الخطوة 1 – إنشاء وتكوين محرك OCR (أساس دليل c# OCR tutorial)

أولاً نقوم بإنشاء المحرك وتفعيل وضع GPU. تفعيل GPU يمكن أن يقلل ثوانٍ من زمن التعرف على دفعات كبيرة، لكنه اختياري.

```csharp
using System;

// Assume the OCR SDK namespace is OcrSdk
using OcrSdk;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration (requires a CUDA‑compatible GPU)
        ocrEngine.Config.EnableGPU = true;   // Turn on GPU mode
        ocrEngine.Config.GpuDeviceId = 0;    // Optional: select GPU index (0 = first GPU)

        // The rest of the steps follow...
```

**لماذا هذا مهم:** المحرك يحمل كل منطق المعالجة الثقيلة—نماذج اللغة، تمهيد الصورة، وخط أنابيب الاستدلال. تفعيل `EnableGPU` يخبر الـ SDK بتحميل هذه الحسابات إلى بطاقة الرسوميات، وهو مفيد خصوصاً عندما تعالج JPEGs عالية الدقة أو عشرات الإيصالات دفعة واحدة.

## الخطوة 2 – تحميل الصورة لـ OCR (خطوة “load image for OCR”)

بعد ذلك نشير بالمحرك إلى الملف الذي نريد قراءته. يمكن أن يكون المسار مطلقاً أو نسبياً؛ فقط تأكد من وجود الملف.

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.LoadImage(imagePath);
```

**نصيحة احترافية:** إذا كنت تتعامل مع ملفات يرفعها المستخدم، تحقق من الامتداد والحجم قبل استدعاء `LoadImage`. عادةً ما يتوقع محرك OCR صورة bitmap في الذاكرة، لذا تمرير JPEG تالف سيسبب استثناءً.

## الخطوة 3 – تنفيذ OCR على الصورة (الإجراء الأساسي “perform OCR on image”)

الآن يقوم المحرك بالعمل الثقيل. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على النص العادي، وربما درجات الثقة.

```csharp
        // Step 3: Perform the recognition and retrieve the text
        OcrResult ocrResult = ocrEngine.Recognize();
```

**ما الذي يحدث خلف الكواليس؟** عادةً ما يمر الـ SDK بسلسلة من المراحل:  
1. **Pre‑processing** – تصحيح الميل، تحويل إلى ثنائي، إزالة الضوضاء.  
2. **Text line detection** – يحدد أين تبدأ الكلمات وتنتهي.  
3. **Character classification** – الشبكة العصبية تتنبأ بكل حرف.  

فهم هذا التدفق يساعدك على استكشاف الأخطاء—إذا ظهر ناتج مشوش، تحقق من جودة الصورة قبل تعديل إعدادات المحرك.

## الخطوة 4 – استخراج النص من JPEG (عرض النتيجة)

أخيراً نطبع السلسلة المستخرجة إلى وحدة التحكم. في تطبيق حقيقي قد تخزنها في قاعدة بيانات، ترسلها إلى API، أو تمررها إلى خط أنابيب NLP آخر.

```csharp
        // Step 4: Display the recognized text
        Console.WriteLine("Recognized Text:");
        Console.WriteLine(ocrResult.Text);

        // Keep the console window open (useful when running from VS)
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**الناتج المتوقع:**  
إذا كان `receipt.jpg` يحتوي على إيصال بقالة نموذجي، سترى شيئاً مثل:

```
Recognized Text:
WALMART
123 Main St.
Date: 01/03/2026
Item   Qty   Price
Milk    2    $4.58
Bread   1    $2.99
Total          $7.57
```

لاحظ كيف تم الحفاظ على فواصل الأسطر والمسافات—معظم SDKs OCR تحاول الحفاظ على التخطيط، وهو مفيد عندما تقوم لاحقاً باستخراج حقول مثل “Total”.

## الخطوة 5 – حالات الحافة الشائعة والنصائح (تحسين دليل c# OCR tutorial)

- **JPEGs منخفضة الدقة:** إذا كانت الصورة أقل من 300 dpi، فكر في تكبيرها بفلتر bicubic قبل استدعاء `LoadImage`.  
- **لغات متعددة:** بعض المحركات تسمح لك بتعيين `ocrEngine.Config.Language = "en,es";`. هذا مفيد عندما يحتوي الإيصال على نص بالإنجليزية والإسبانية معاً.  
- **معالجة دفعات:** ضع الخطوات داخل حلقة `foreach` على قائمة مسارات الملفات. تذكر إعادة استخدام نفس كائن `OcrEngine` لتجنب عبء إعادة تهيئة سياق GPU.  
- **معالجة الأخطاء:** احط استدعاء التعرف بـ `try…catch (OcrException ex)` لالتقاط مشاكل مثل “GPU not available” أو “unsupported image format”.  

```csharp
        try
        {
            OcrResult result = ocrEngine.Recognize();
            Console.WriteLine(result.Text);
        }
        catch (OcrException ex)
        {
            Console.Error.WriteLine($"OCR failed: {ex.Message}");
        }
```

## ملخص – ما أنجزناه

أصبح لديك الآن **c# OCR tutorial** يمر بك عبر كل مرحلة من استخراج النص من إيصال JPEG: إنشاء المحرك، تحميل الصورة، تنفيذ OCR، وأخيراً استرجاع النتيجة النصية. المثال يوضح كيفية **perform OCR on image** بفعالية مع تسريع GPU اختياري، ويظهر سير العمل النموذجي لسيناريوهات **recognize text from receipt**.

## الخطوات التالية والمواضيع ذات الصلة

- **ضبط التمهيد المسبق** – جرب `ocrEngine.Config.DenoiseLevel` أو بنية ثنائية مخصصة لزيادة الدقة على المسحات الضوضائية.  
- **الدمج مع قاعدة بيانات** – خزن `ocrResult.Text` جنباً إلى جنب مع بيانات مثل `imagePath` ووقت المعالجة.  
- **استكشاف الكلمات المفتاحية الثانوية** – جرّب “extract text from JPEG” في سياق خدمة ويب، أو أنشئ API صغير يقبل صورة مرفوعة ويعيد النص المستخرج.  
- **التحول إلى مزود OCR مختلف** – معظم SDKs التجارية توفر فئات مشابهة (`Engine`, `Config`, `Result`)، لذا النمط الذي تعلمته ينتقل بسهولة.

جرّبه، عدّل الإعدادات، وسترى كيف يمكن أن يصبح OCR جزءاً موثوقاً من صندوق أدوات C# الخاص بك. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}