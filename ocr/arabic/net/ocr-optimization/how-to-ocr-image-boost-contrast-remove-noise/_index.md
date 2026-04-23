---
category: general
date: 2026-02-22
description: كيفية التعرف الضوئي على الحروف في الصورة باستخدام Aspose OCR – إزالة
  ضوضاء الصورة، تعزيز تباين الصورة، واستخراج النص من الصورة في C# بسرعة.
draft: false
keywords:
- how to ocr image
- remove image noise
- boost image contrast
- extract text image
- recognize image text
language: ar
og_description: تعلم كيفية إجراء OCR للصور باستخدام Aspose OCR، وإزالة الضوضاء، وتعزيز
  التباين، واستخراج النص من الصورة في C# مع مثال كامل وجاهز للتنفيذ.
og_title: كيفية التعرف الضوئي على الأحرف في الصورة – زيادة التباين وإزالة الضوضاء
tags:
- OCR
- C#
- Image Processing
title: 'كيفية التعرف الضوئي على الصورة: تعزيز التباين، إزالة الضوضاء'
url: /ar/net/ocr-optimization/how-to-ocr-image-boost-contrast-remove-noise/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إجراء OCR على الصورة – تعزيز التباين وإزالة الضوضاء في C#

هل تساءلت يومًا **كيف تقوم بعمل OCR للصور** التي تكون مائلة، مليئة بالضوضاء، أو صعب قراءتها؟ لست وحدك. في العديد من المشاريع الواقعية — فكر في مسح الإيصالات أو رقمنة المستندات القديمة — الصورة الأصلية نادراً ما تكون مثالية. الخبر السار؟ باستخدام بضع سطور من C# و Aspose OCR يمكنك **إزالة ضوضاء الصورة**، **تعزيز تباين الصورة**، وأخيرًا **استخراج نص الصورة** دون عناء.

في هذا الدرس سنستعرض حلًا كاملاً من البداية إلى النهاية. في النهاية ستعرف بالضبط كيف تُهيئ محرك OCR، وتنظف صورةً مليئةً بالضوضاء، وتُـ**تعرّف نص الصورة** بحيث يمكنك توجيه النتيجة إلى أي مكان تحتاجه. لا مراجع غامضة، فقط عينة كود قابلة للتنفيذ والمنطق وراء كل اختيار.

## ما ستحتاجه

- .NET 6+ (أو .NET Core 3.1+ – الـ API هو نفسه)
- حزمة Aspose.OCR عبر NuGet (`Install-Package Aspose.OCR`)
- صورة نموذجية مائلة ومليئة بالضوضاء (مثال: `skewed_noisy.jpg`)
- أي بيئة تطوير تفضّلها – Visual Studio أو Rider أو VS Code ستكفي

هذا كل شيء. إذا كان لديك هذه المتطلبات، يمكننا القفز مباشرة إلى الكود.

![how to ocr image example](/images/ocr-demo.png){alt="مثال على كيفية إجراء OCR على الصورة"}

## الخطوة 1: تهيئة محرك OCR – كيفية إجراء OCR على الصورة بشكل صحيح  

أول شيء يجب القيام به هو إنشاء كائن `OcrEngine` وتحديد اللغة المتوقعة. الإنجليزية هي الأكثر شيوعًا، لكن Aspose يدعم عشرات اللغات مباشرةً.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Create the OCR engine and set the language to English.
        var ocrEngine = new OcrEngine { Language = Language.English };
```

**لماذا هذا مهم:** يحتاج المحرك إلى معرفة مجموعة الأحرف؛ وإلا سيهدر الوقت في التخمين وستنخفض دقّته. ضبط اللغة مسبقًا يقلل أيضًا من استهلاك الذاكرة لأن المحرك يحمل فقط بيانات اللغة المطلوبة.

## الخطوة 2: تحميل الصورة والبدء في إزالة ضوضاء الصورة  

بعد ذلك نقوم بقراءة الصورة من القرص. في معظم الحالات يكون الملف JPEG أو PNG يحتوي على الكثير من الحبوب. تحميله إلى كائن `Image` يمنحنا مقبضًا يمكننا تمريره عبر الفلاتر.

```csharp
        // Load the input image (skewed and noisy)
        var inputImage = Image.Load(@"YOUR_DIRECTORY/skewed_noisy.jpg");
```

**نصيحة احترافية:** إذا كانت صورتك مخزنة في سحابة، يمكنك بثها مباشرةً باستخدام `Image.Load(Stream)`. بهذه الطريقة تتجنب إنشاء ملف مؤقت.

## الخطوة 3: تطبيق سلسلة من الفلاتر – تعزيز تباين الصورة وتنظيف الضوضاء  

Aspose OCR يأتي مع خط أنابيب فلاتر مفيد. هنا نربط ثلاثة فلاتر:

1. **DeskewFilter** – يُصحّح الدوران بحيث يكون النص أفقيًا.  
2. **DenoiseFilter** – يزيل الحبوب دون تمويه الحروف.  
3. **ContrastFilter** – يضاعف الفرق بين الخلفية والمقدمة، مما يجعل الأحرف الباهتة تبرز.

```csharp
        // Pre‑process the image with a chain of filters
        var processedImage = inputImage
            .Apply(new DeskewFilter())          // correct rotation
            .Apply(new DenoiseFilter())         // reduce grain
            .Apply(new ContrastFilter(1.5f));   // boost contrast
```

**لماذا هذه الفلاتر؟**  
- **Deskew** ضروري للحصول على OCR دقيق؛ حتى بضع درجات من الانحراف قد تقلّف معدل التعرف إلى النصف.  
- **Denoise** يتعامل مع مشكلة “إزالة ضوضاء الصورة” التي نراها كثيرًا في مسحات الكاميرا الهاتفية.  
- **Contrast** هو السر للوثائق منخفضة التباين — فكر في الإيصالات الباهتة.  

يمكنك تعديل معامل `ContrastFilter` (القيمة الافتراضية `1.0f`). القيم فوق `1.5f` قد تُفرط في إضاءة الصورة، لذا جرّب عدة مرات.

## الخطوة 4: التعرف على نص الصورة – جوهر كيفية إجراء OCR على الصورة  

الآن بعد أن أصبحت الصورة نظيفة، نمرّرها إلى محرك OCR.

```csharp
        // Recognize text from the processed image
        var ocrResult = ocrEngine.Recognize(processedImage);
```

طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على السلسلة المستخرجة، درجات الثقة، وحتى إطارات التحديد إذا احتجت إليها لتسليط الضوء.

**حالة خاصة:** إذا كانت الصورة تحتوي على لغات متعددة، يمكنك ضبط `ocrEngine.Language = Language.English | Language.Spanish;`. سيحاول المحرك كلا القاموسين.

## الخطوة 5: العرض والتحقق – استخراج نص الصورة لتطبيقك  

أخيرًا، نطبع النص على وحدة التحكم. في تطبيق حقيقي قد تكتب النتيجة إلى قاعدة بيانات، ملف، أو تمرّرها إلى خط أنابيب NLP لاحق.

```csharp
        // Display the extracted text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**الناتج المتوقع:**  

```
=== OCR Result ===
Invoice #12345
Date: 2024‑01‑15
Total: $256.78
Thank you for your business!
```

إذا رأيت أحرفًا مشوشة، عد إلى الخطوة 3 وعدّل معلمات الفلاتر. غالبًا ما يساعد رفع معامل التباين أو إضافة `SharpenFilter` إضافي.

## أسئلة شائعة ونصائح  

### ماذا لو كانت صورتي بالفعل بالأبيض والأسود؟  
يمكنك تخطي `ContrastFilter` واستخدام `DenoiseFilter` فقط. زيادة التباين على صورة ثنائية قد تُنشئ تشوهات.

### كيف أتعامل مع ملفات كبيرة جدًا (>10 MB)؟  
حمّل الصورة بدقة أقل (`Image.Load(path, new LoadOptions { DesiredWidth = 2000 })`) قبل الفلترة. يعمل محرك OCR جيدًا مع النسخ المصغرة طالما ظل النص مقروءًا.

### هل يمكن تشغيل هذا في واجهة برمجة تطبيقات ويب؟  
بالطبع. غلف المنطق نفسه في متحكم ASP.NET Core، استقبل `IFormFile`، وأرجع نتيجة OCR كـ JSON. تذكّر تحرير كائنات `Image` لت

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}