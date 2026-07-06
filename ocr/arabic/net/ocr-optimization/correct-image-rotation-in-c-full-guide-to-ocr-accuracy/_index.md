---
category: general
date: 2026-03-04
description: تصحيح دوران الصورة وإزالة الضوضاء لاستخراج النص باستخدام Aspose OCR.
  تعلّم كيفية تحسين دقة OCR وتحميل OCR للصورة في C#.
draft: false
keywords:
- correct image rotation
- remove image noise
- extract text image
- improve ocr accuracy
- load image ocr
language: ar
og_description: صحح دوران الصورة بسرعة؛ أزل ضوضاء الصورة، استخرج النص من الصورة وحسّن
  دقة OCR باستخدام Aspose OCR في C#.
og_title: تصحيح دوران الصورة – تعزيز دقة OCR في C#
tags:
- OCR
- C#
- Image Processing
title: التدوير الصحيح للصورة في C# – دليل كامل لدقة OCR
url: /ar/net/ocr-optimization/correct-image-rotation-in-c-full-guide-to-ocr-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصحيح دوران الصورة – تحسين دقة OCR في C#

## ما ستتعلمه

- كيفية تثبيت وإضافة مرجع لمكتبة Aspose OCR.  
- لماذا تعتبر خط أنابيب الفلاتر المخصص مهمة لـ **تصحيح دوران الصورة**.  
- الكود الدقيق المطلوب لـ **load image OCR**، وتطبيق *DeskewFilter* و *DenoiseFilter*، واستدعاء `Recognize`.  
- نصائح للتعامل مع الحالات الحدية مثل الانحراف الشديد أو الضوضاء الكثيفة.  
- كيفية التحقق من النتيجة وضبط الإعدادات للحصول على **تحسين دقة OCR** أفضل.

## المتطلبات المسبقة

| المتطلب | السبب |
|-------------|--------|
| .NET 6.0 SDK (or later) | ميزات لغة حديثة وأداء أفضل |
| Visual Studio 2022 (or VS Code) | تصحيح سهل وIntelliSense مريح |
| Aspose.OCR NuGet package | محرك OCR الذي سنستخدمه |
| A sample image (e.g., `skewed_noisy.png`) | لإظهار **تصحيح دوران الصورة** و **إزالة ضوضاء الصورة** |

إذا كان لديك هذه بالفعل، رائع—لننتقل.

## الخطوة 1: تثبيت Aspose  OCR

Open a terminal in your project folder and run:

```bash
dotnet add package Aspose.OCR
```

هذا يجلب أحدث إصدار ثابت (اعتبارًا من مارس 2026، الإصدار 23.12). الحزمة تتضمن جميع فئات الفلاتر التي نحتاجها، لذا لا توجد تبعيات إضافية.

## الخطوة 2: تهيئة محرك OCR

Creating an engine instance is straightforward, but it’s worth understanding why we do it early.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();
```

`OcrEngine` هو المركز الرئيسي—فكر فيه كـ “العقل” الذي ينسق التحميل، المعالجة المسبقة، والتعرف. إنشاء نسخة واحدة وإعادة استخدامها عبر صور متعددة يمكن أن يوفر بضع مليثانية من كل استدعاء.

## الخطوة 3: بناء خط أنابيب فلاتر مخصص  

Here’s where the magic happens. By chaining filters we can **correct image rotation**, **remove image noise**, and *binarize* the picture for sharper text edges.

```csharp
            // Step 3: Build a custom filter pipeline to improve recognition
            ocrEngine.Filters = new FilterBuilder()
                .Add(new DeskewFilter { MaxAngle = 5 })                         // correct up‑to‑5° rotation
                .Add(new DenoiseFilter { Strength = DenoiseStrength.Medium }) // remove image noise
                .Add(new BinarizeFilter { Threshold = 127 })                  // convert to black‑and‑white
                .Build();
```

- **DeskewFilter**: يكتشف خط الأساس للنص ويعيد تدوير الصورة. نحدده عند 5° لأن ما بعد ذلك قد يفسر الخوارزمية اتجاه النص بشكل خاطئ.  
- **DenoiseFilter**: يطبق فلتر متوسط يزيل البقع دون تشويش الأحرف—ضروري لـ *تحسين دقة OCR*.  
- **BinarizeFilter**: يحول الصورة إلى أبيض وأسود نقي، وهو ما تفضله العديد من محركات OCR لتسريع مطابقة الأنماط.

> **نصيحة احترافية:** إذا كان بإمكان مستنداتك أن تُدوَّر بأكثر من 5°، زد `MaxAngle` إلى 10 أو 15، لكن راقب الأداء.

## الخطوة 4: تحميل الصورة لـ OCR  

Now we actually **load image OCR**. The `ImageInfo.Load` method reads the file into a format the engine understands.

```csharp
            // Step 4: Load the image that needs OCR processing
            string imagePath = @"YOUR_DIRECTORY/skewed_noisy.png";
            var imageInfo = ImageInfo.Load(imagePath);
```

تأكد من أن المسار يشير إلى ملف حقيقي؛ وإلا ستحصل على `FileNotFoundException`. إذا كنت تبني واجهة ويب API، يمكنك قبول `IFormFile` وإرسال تدفقه مباشرة إلى `ImageInfo.Load`.

## الخطوة 5: التعرف واستخراج النص

With the filters in place and the image loaded, we finally ask the engine to read the characters.

```csharp
            // Step 5: Perform OCR on the prepared image
            var ocrResult = ocrEngine.Recognize(imageInfo);

            // Step 6: Output the recognized text
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

استدعاء `Recognize` يُعيد كائن `OcrResult` يحتوي على النص الخام، درجات الثقة، وحتى إطارات الحدود إذا احتجتها لاحقًا. في معظم الحالات، `ocrResult.Text` هو كل ما يهمك.

### النتيجة المتوقعة

If `skewed_noisy.png` contains the sentence “Hello, World!” you should see something like:

```
=== OCR Output ===
Hello, World!
```

إذا كان الإخراج مشوشًا، حاول زيادة `DenoiseStrength` إلى `High` أو تعديل `Threshold` في `BinarizeFilter`. التعديلات الصغيرة غالبًا ما تُحدث قفزة ملحوظة في **تحسين دقة OCR**.

## الخطوة 6: الحالات الحدية وسيناريوهات ماذا‑لو  

### انحراف شديد (> 5°)

The default `MaxAngle = 5` works for most scanned receipts. For scanned legal documents that might be rotated 12°, set:

```csharp
.Add(new DeskewFilter { MaxAngle = 12 })
```

لكن تذكر: الزوايا الأكبر تزيد من وقت المعالجة وقد تُدخل تشوهات إذا كان خط أساس النص غير مستوي.

### خلفيات شديدة الضوضاء

If the image is a photo taken under poor lighting, add a second `DenoiseFilter` after binarization:

```csharp
.Add(new DenoiseFilter { Strength = DenoiseStrength.High })
```

إذا كانت الصورة فوتوغرافية مأخوذة بإضاءة ضعيفة، أضف `DenoiseFilter` ثانية بعد التثبيت الثنائي:

### مستندات متعددة اللغات

Aspose OCR auto‑detects language, but you can force it:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;
```

هذا يمكن أن يُحسّن **دقة OCR** أكثر عندما تواجه عملية الاكتشاف الافتراضية صعوبة.

## مثال كامل يعمل (جاهز للنسخ واللصق)

Below is the complete program, ready to compile and run. Replace `YOUR_DIRECTORY` with the actual folder containing your image.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Build filter pipeline: correct image rotation, remove image noise, binarize
            ocrEngine.Filters = new FilterBuilder()
                .Add(new DeskewFilter { MaxAngle = 5 })
                .Add(new DenoiseFilter { Strength = DenoiseStrength.Medium })
                .Add(new BinarizeFilter { Threshold = 127 })
                .Build();

            // Load the image you want to OCR
            string imagePath = @"YOUR_DIRECTORY/skewed_noisy.png";
            var imageInfo = ImageInfo.Load(imagePath);

            // Perform OCR
            var ocrResult = ocrEngine.Recognize(imageInfo);

            // Show the extracted text
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

شغّله باستخدام `dotnet run`. يجب أن ترى النص المنقح يُطبع على وحدة التحكم.

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات PDF؟**  
ج: نعم. حوّل كل صفحة PDF إلى صورة (مثلاً باستخدام `Aspose.PDF`) ومرّر الـ bitmap إلى `ImageInfo.Load`.

**س: ماذا لو كانت صورتي مستقيمة تمامًا؟**  
ج: سيكتشف `DeskewFilter` زاوية قريبة من الصفر ويترك الصورة دون تعديل—بدون تأثير على الأداء.

**س: هل يمكنني معالجة مجموعة من الصور؟**  
ج: بالتأكيد. ضع كود التعرف داخل حلقة `foreach`؛ أعد استخدام نفس نسخة `OcrEngine` للسرعة.

## الخاتمة

الآن لديك وصفة متكاملة من البداية للنهاية لـ **تصحيح دوران الصورة** التي تزيل أيضًا **ضوضاء الصورة**، مما يتيح لك *استخراج نص الصورة* بثقة. من خلال تكوين سلسلة فلاتر مخصصة ستحسن باستمرار **دقة OCR** وتجعل سير عمل *load image OCR* بأكمله سهلًا.

الخطوات التالية؟ جرب تجربة `DenoiseStrength` أعلى، العب مع عتبات التثبيت الثنائي المختلفة، أو دمج الكود في نقطة نهاية ASP.NET Core التي تقبل التحميلات. نفس المبادئ تنطبق سواء كنت تعالج فواتير، جوازات سفر، أو ملاحظات مكتوبة يدويًا.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالكريستال!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}