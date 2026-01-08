---
category: general
date: 2026-01-07
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية التعرف على
  النص من الصورة، تحسين دقة OCR، تحميل الصورة للـ OCR وتحديد لغة OCR.
draft: false
keywords:
- extract text from image
- recognize text from photo
- improve ocr accuracy
- load image for ocr
- set ocr language
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR. يوضح هذا الدليل كيفية
  التعرف على النص من الصورة، تحسين دقة OCR، تحميل الصورة لـ OCR وتعيين لغة OCR.
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل C#
tags:
- Aspose OCR
- C#
- Image Processing
title: استخراج النص من الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة – تنفيذ كامل بلغة C# باستخدام Aspose OCR

هل احتجت يومًا إلى **استخراج النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة ستعطيك نتائج موثوقة؟ لست وحدك. في العديد من التطبيقات الواقعية—ماسحات الفواتير، أدوات التحقق من الهوية، أو مجرد أداة سريعة لتدوين الملاحظات—يعد **التعرف على النص من الصورة** ميزة لا غنى عنها.

في هذا الدرس سنستعرض مثالًا كاملًا جاهزًا للتنفيذ يوضح لك كيفية **تحميل الصورة للتعرف الضوئي على الأحرف (OCR)**، ضبط المحرك لتحديد **لغة OCR**، وتطبيق بعض حيل ما قبل المعالجة لتحسين **دقة OCR**. في النهاية ستحصل على ملف C# واحد يطبع النص المستخرج على وحدة التحكم، وستفهم لماذا كل إعداد مهم.

> **نصيحة:** يعمل الكود مع Aspose.OCR ≥ 23.5، .NET 6+ وأي بيئة Windows أو Linux أو macOS يمكنها تشغيل .NET Core.

## المتطلبات المسبقة

- .NET 6 SDK (أو أحدث) مثبت  
- Visual Studio 2022، VS Code، أو أي محرر تفضله  
- حزمة NuGet `Aspose.OCR` (تثبيت عبر `dotnet add package Aspose.OCR`)  
- ملف صورة (JPEG/PNG) يحتوي على نص مطبوع أو مكتوب بوضوح  

إذا كان لديك كل ذلك، فلنبدأ.

![مثال لاستخراج النص من الصورة](/images/ocr-example.png "استخراج النص من الصورة – مخرجات Aspose OCR")

## الخطوة 1: إنشاء وإغلاق محرك OCR – نواة “استخراج النص من الصورة”

أول ما تحتاجه هو نسخة من `OcrEngine`. تغليفها داخل كتلة `using` يضمن تحرير الموارد الأصلية بشكل صحيح.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

/// <summary>
/// Demonstrates how to extract text from image using Aspose OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Step 1 – Initialize the OCR engine (the heart of the process)
        using (var ocrEngine = new OcrEngine())
        {
            // The rest of the workflow lives inside this block.
```

**لماذا هذا مهم:** `OcrEngine` يحتفظ بذاكرة غير مُدارة لمكتبات OCR الأصلية. إغلاقها بسرعة يمنع تسرب الذاكرة، خاصةً عند معالجة العديد من الصور دفعة واحدة.

## الخطوة 2: تعريف إعدادات التعرف – تحسين دقة OCR

بعد ذلك ننشئ كائن `RecognitionSettings`. هنا نـ **حدد لغة OCR** ونضيف فلاتر ما قبل المعالجة التي غالبًا ما تُحدث الفارق بين نص مشوش ونص نظيف.

```csharp
            // Step 2 – Configure recognition settings
            var recognitionSettings = new RecognitionSettings
            {
                // Set the language to English; other languages are available via Language enum.
                Language = Language.English,

                // PreprocessFilters help the engine deal with real‑world photo issues.
                PreprocessFilters = new[]
                {
                    PreprocessFilter.Deskew,          // Corrects slight rotation
                    PreprocessFilter.Denoise,         // Reduces grainy noise
                    PreprocessFilter.ContrastEnhance // Boosts text visibility
                }
            };
```

**لماذا هذه الفلاتر؟**  
- **Deskew** يصلح المشكلة الشائعة للصور الملتقطة بالهاتف التي تكون مائلة بضع درجات.  
- **Denoise** يزيل البقع التي قد تُفسَّر كحروف.  
- **ContrastEnhance** يجعل الحبر الخفيف يبرز، وهو أمر أساسي **لتحسين دقة OCR**.

## الخطوة 3: تحميل الصورة – تحميل الصورة للتعرف الضوئي على الأحرف بكفاءة

توفر Aspose الدالة `ImageStream.FromFile` للتحميل السريع. يمكنك أيضًا تمرير `MemoryStream` إذا كانت الصورة تأتي من طلب ويب أو قاعدة بيانات.

```csharp
            // Step 3 – Load the image you want to analyze
            var imagePath = @"YOUR_DIRECTORY/phone_photo.jpg";
            var imageStream = ImageStream.FromFile(imagePath);
```

**خطأ شائع:** إعطاء مسار يحتوي على شرطات مائلة للأمام على Windows يعمل، لكن استخدام `Path.Combine` أكثر أمانًا للمشاريع متعددة المنصات.

## الخطوة 4: إجراء التعرف – التعرف على النص من الصورة

الآن نستدعي `Recognize`، مع تمرير كل من تدفق الصورة وإعداداتنا. تُعيد الدالة سلسلة نصية عادية تحتوي على النص المستخرج.

```csharp
            // Step 4 – Run OCR and capture the result
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

إذا احتوت الصورة على عدة كتل نصية، تقوم Aspose بدمجها مع فواصل أسطر، محافظًا على التخطيط الأصلي قدر الإمكان.

## الخطوة 5: إخراج النتيجة – التحقق من الاستخراج

أخيرًا، نكتب النتيجة إلى وحدة التحكم. في تطبيق حقيقي قد تخزنها في قاعدة بيانات، ترسلها إلى خدمة أخرى، أو تعرضها في واجهة المستخدم.

```csharp
            // Step 5 – Show the extracted text
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(recognizedText);
            Console.WriteLine("=== Extracted Text End ===");
        } // End of using block – OcrEngine disposed
    }
}
```

### النتيجة المتوقعة على وحدة التحكم

```
=== Extracted Text Start ===
This is a sample receipt.
Total: $23.45
Thank you for shopping!
=== Extracted Text End ===
```

إذا رأيت أحرفًا مشوشة، تحقق من وضوح الصورة، وتطابق اللغة مع النص، وأن فلاتر ما قبل المعالجة مناسبة.

## الخطوة 6: تعديلات اختيارية – تحسينات لحالات الطرفية

### أ. تبديل اللغات

```csharp
recognitionSettings.Language = Language.Spanish; // For Spanish receipts
```

### ب. إضافة فلاتر مخصصة

توفر Aspose أيضًا `PreprocessFilter.Sharpen` أو `PreprocessFilter.Binarize`. جربها عندما لا تكون الثلاثة الافتراضية كافية.

### ج. معالجة الصور الكبيرة

للصور ذات الدقة العالية جدًا، قلل الحجم أولًا لتقليل استهلاك الذاكرة:

```csharp
var resizedStream = ImageProcessor.Resize(imageStream, 1024, 768);
string text = ocrEngine.Recognize(resizedStream, recognitionSettings);
```

## الأسئلة المتكررة

**س: هل يعمل هذا مع الملاحظات المكتوبة بخط اليد؟**  
ج: تم ضبط Aspose OCR للنص المطبوع. التعرف على الخط اليدوي يتطلب محركًا مختلفًا (مثل Aspose.OCR للخط اليدوي أو نموذج تعلم آلي).

**س: هل يمكنني معالجة عدة صور داخل حلقة؟**  
ج: بالتأكيد. فقط انقل كتلة `using (var ocrEngine = new OcrEngine())` خارج الحلقة وأعد استخدام المحرك لتحسين الأداء.

**س: ماذا لو كانت الصورة صفحة PDF؟**  
ج: حوّل صفحة PDF إلى صورة أولًا (Aspose.PDF يمكنه تحويل الصفحات إلى PNG/JPEG)، ثم مرّرها إلى محرك OCR.

## ملخص – ما أنجزناه

- **استخراج النص من الصورة** باستخدام برنامج C# واحد مكتمل ومستقل.  
- عرضنا كيفية **التعرف على النص من الصورة** مع ما قبل المعالجة التي **تحسن دقة OCR**.  
- أظهرنا الطريقة الصحيحة **لتحميل الصورة للتعرف الضوئي على الأحرف** و**تحديد لغة OCR** للسيناريوهات متعددة اللغات.  

## الخطوات التالية والمواضيع ذات الصلة

- **المعالجة الدفعية:** دمج هذا المقتطف مع `Directory.GetFiles` لتطبيق OCR على مجلد كامل.  
- **ما بعد المعالجة:** استخدم التعبيرات النمطية لتنظيف التواريخ أو المبالغ أو المعرفات بعد الاستخراج.  
- **التكاملات:** ربط النص المستخرج بـ Azure Cognitive Search أو Elastic لإنشاء مستندات قابلة للبحث.  

لا تتردد في تجربة تركيبات فلاتر مختلفة، لغات متعددة، ومصادر صور متنوعة. النمط الأساسي يبقى نفسه: أنشئ المحرك، اضبط الإعدادات، حمّل الصورة، قم بالتعرف، وأخرج النتيجة. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}