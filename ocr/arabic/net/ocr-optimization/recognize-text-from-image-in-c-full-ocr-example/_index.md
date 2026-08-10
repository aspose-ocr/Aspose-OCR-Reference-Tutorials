---
category: general
date: 2026-06-22
description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. تعلّم كيفية تصحيح
  الميل تلقائيًا للصورة، ومعالجة الصورة مسبقًا للتعرف الضوئي على الأحرف، وتفعيل التصحيح
  التلقائي للميل في مثال مختصر للتعرف الضوئي على الأحرف باستخدام C#.
draft: false
keywords:
- recognize text from image
- auto deskew image
- preprocess image for ocr
- c# ocr example
- enable auto deskew
language: ar
og_description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدليل
  كيفية تصحيح الميل تلقائيًا للصورة، ومعالجة الصورة مسبقًا للتعرف الضوئي على الأحرف،
  وتمكين تصحيح الميل التلقائي في مثال عملي للتعرف الضوئي على الأحرف باستخدام C#.
og_title: التعرف على النص من الصورة في C# – مثال كامل على OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  headline: Recognize Text from Image in C# – Full OCR Example
  type: TechArticle
- description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  name: Recognize Text from Image in C# – Full OCR Example
  steps:
  - name: 1. Low Contrast or Dark Backgrounds
    text: 'Aspose.OCR offers an extra flag `PreprocessingOptions.ContrastEnhancement`.
      Add it to the `Preprocessing` line:'
  - name: 2. Non‑English Documents
    text: Swap `OcrLanguage.English` for `OcrLanguage.Spanish`, `OcrLanguage.French`,
      etc. The engine auto‑loads the appropriate language model.
  - name: 3. Large Images
    text: 'Processing a 5 MP photo can be memory‑hungry. Scale it down first:'
  - name: 4. Getting Bounding Boxes
    text: 'If you need the exact location of each word (e.g., for a UI overlay), iterate
      over `result.Regions`:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: التعرف على النص من الصورة في C# – مثال كامل على OCR
url: /ar/net/ocr-optimization/recognize-text-from-image-in-c-full-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في C# – مثال كامل للـ OCR

هل تساءلت يومًا كيف **تتعرف على النص من صورة** في تطبيق C# دون أن تشعر بالإحباط بسبب الصور الضبابية؟ لست وحدك. سواءً كنت تقوم برقمنة الإيصالات، استخراج البيانات من النماذج، أو مجرد تجربة حيل الصور المدعومة بالذكاء الاصطناعي، فإن الحصول على نتائج OCR نظيفة يعتمد على المعالجة المسبقة الصحيحة—فكر في تعديل الميل تلقائيًا وتقليل الضوضاء.  

في هذا الدرس سنستعرض **c# ocr example** يستخدم مكتبة Aspose.OCR لتفعيل **auto deskew**، تعديل الصور المائلة تلقائيًا، و**preprocess image for OCR** ببضع أسطر من الشيفرة فقط. في النهاية ستحصل على برنامج قابل للتنفيذ يطبع النص المستخرج مباشرةً إلى وحدة التحكم.

## ما ستتعلمه

- كيفية تثبيت وإضافة مرجع حزمة Aspose.OCR عبر NuGet.  
- إعداد `OcrEngine` بدعم اللغة الإنجليزية.  
- تفعيل **auto deskew image** وخيارات المعالجة المسبقة الأخرى في خطوة واحدة.  
- تشغيل المحرك على صورة واقعية ومعالجة الناتج.  
- نصائح للتعامل مع الحالات الخاصة مثل الصور المدارة بشدة أو المسحات منخفضة التباين.

> **المتطلبات المسبقة** – تحتاج إلى .NET 6 (أو أحدث) وفهم أساسي للغة C#. لا يلزم خبرة سابقة في OCR.

---

## ## التعرف على النص من صورة – تثبيت حزمة Aspose.OCR

قبل كتابة أي شيفرة، يجب إضافة المكتبة إلى المشروع. افتح الطرفية في مجلد الحل الخاص بك وشغّل:

```bash
dotnet add package Aspose.OCR
```

هذا الأمر يجلب أحدث نسخة مستقرة من Aspose.OCR، التي تتضمن محرك OCR، حزم اللغات، وأدوات المعالجة المسبقة التي سنحتاجها.  

*نصيحة احترافية:* إذا كنت تستهدف .NET Framework بدلاً من .NET Core، استخدم واجهة مدير الحزم NuGet في Visual Studio—ابحث عن “Aspose.OCR” وانقر **Install**.

---

## ## التعرف على النص من صورة – تهيئة محرك OCR

الآن بعد أن أصبحت الحزمة جاهزة، يمكننا إنشاء المحرك. الخطوة الأولى هي إخبار المحرك أي لغة يتوقعها. في معظم الحالات تكون الإنجليزية كافية، لكن المكتبة تدعم عشرات اللغات جاهزة للاستخدام.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine and set the language to English
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,

            // Step 2: Enable preprocessing to automatically deskew and denoise the image
            Preprocessing = PreprocessingOptions.AutoDeskew | PreprocessingOptions.Denoise
        };
```

**لماذا هذا مهم:**  
- `Language = OcrLanguage.English` يخبر المحرك بمجموعة الأحرف التي يجب استخدامها، مما يحسن الدقة بشكل كبير.  
- خاصية `Preprocessing` تجمع بين علمتين—`AutoDeskew` و `Denoise`. خطوة **auto deskew image** هذه تدور الصورة لتعود إلى خط أفقي، بينما `Denoise` يزيل الضوضاء التي قد تربك محرك OCR.  

إذا تخطيت خطوة المعالجة المسبقة، غالبًا ما ستحصل على مخرجات مشوشة عند مسح الإيصالات أو الصور الملتقطة بزاوية.

---

## ## التعرف على النص من صورة – تمرير الصورة إلى المحرك

مع تحضير المحرك، الخطوة التالية هي تزويده بملف صورة. Aspose.OCR تقبل مسارًا أو `Stream`، لذا يمكنك العمل مع ملفات محلية، موارد مدمجة، أو حتى صور تم تحميلها من الويب.

```csharp
        // Step 3: Recognize text from the input image
        var result = engine.RecognizeImage(@"YOUR_DIRECTORY/skewed_photo.jpg");
```

**ملاحظة حول الحالات الخاصة:**  
- إذا كانت الصورة **مُدارة بشدة** (> 45°)، سيحاول `AutoDeskew` تصحيحها قدر المستطاع، لكن قد تحتاج إلى تدويرها يدويًا باستخدام `System.Drawing` أو `ImageSharp` قبل تمريرها إلى المحرك.  
- بالنسبة لـ **ملفات PDF متعددة الصفحات**، استخدم `engine.RecognizePdf` بدلاً من ذلك؛ نفس علمات المعالجة المسبقة تنطبق.

---

## ## التعرف على النص من صورة – إظهار النتيجة

أخيرًا، نعرض النص المستخرج. كائن `result` يحتوي على أكثر من مجرد نص عادي—فهو يقدم أيضًا درجات الثقة، الصناديق المحيطة، والصورة الأصلية مع المناطق المظللة. للعرض السريع، طباعة `result.Text` تكفي.

```csharp
        // Step 4: Output the recognized text to the console
        System.Console.WriteLine(result.Text);
    }
}
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!
```

إذا كان الناتج مشوشًا، تحقق مرة أخرى من وضوح الصورة الأصلية، إضاءتها الجيدة، وأن **preprocess image for OCR** مفعلة فعلاً (علمات `Preprocessing` أعلاه).  

---

## ## التعرف على النص من صورة – معالجة المشكلات الشائعة

### 1. انخفاض التباين أو الخلفيات الداكنة
Aspose.OCR توفر علمًا إضافيًا `PreprocessingOptions.ContrastEnhancement`. أضفه إلى سطر `Preprocessing`:

```csharp
Preprocessing = PreprocessingOptions.AutoDeskew |
                PreprocessingOptions.Denoise |
                PreprocessingOptions.ContrastEnhancement
```

### 2. مستندات غير إنجليزية
استبدل `OcrLanguage.English` بـ `OcrLanguage.Spanish` أو `OcrLanguage.French` وغيرها. المحرك يحمل نموذج اللغة المناسب تلقائيًا.

### 3. صور كبيرة
معالجة صورة بدقة 5 MP قد تستهلك الكثير من الذاكرة. قلل حجمها أولًا:

```csharp
engine.Image = ImageProcessor.Resize(@"YOUR_DIRECTORY/skewed_photo.jpg", 1024, 768);
```

### 4. الحصول على الصناديق المحيطة
إذا كنت بحاجة إلى الموقع الدقيق لكل كلمة (مثلاً لتراكب واجهة المستخدم)، تكرّر عبر `result.Regions`:

```csharp
foreach (var region in result.Regions)
{
    System.Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

---

## ## التعرف على النص من صورة – مثال كامل يعمل

فيما يلي البرنامج **الكامل القابل للنسخ واللصق** الذي يدمج جميع النصائح السابقة. احفظه باسم `Program.cs`، استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على صورة الاختبار، ثم شغّل `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,
            // Enable auto deskew, denoise, and contrast enhancement
            Preprocessing = PreprocessingOptions.AutoDeskew |
                            PreprocessingOptions.Denoise |
                            PreprocessingOptions.ContrastEnhancement
        };

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/skewed_photo.jpg";

        // Recognize the image
        var result = engine.RecognizeImage(imagePath);

        // Output plain text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // Optional: print bounding boxes for each detected region
        Console.WriteLine("=== Detected Regions ===");
        foreach (var region in result.Regions)
        {
            Console.WriteLine($"{region.Text}  -->  {region.Bounds}");
        }
    }
}
```

**الناتج المتوقع في وحدة التحكم** (بافتراض أن الصورة تحتوي على إيصال بسيط):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!

=== Detected Regions ===
Invoice #12345  -->  {X=12,Y=34,Width=250,Height=20}
Date: 2026-06-01  -->  {X=12,Y=60,Width=200,Height=18}
Total: $256.78  -->  {X=12,Y=86,Width=180,Height=18}
Thank you for your business!  -->  {X=12,Y=112,Width=300,Height=22}
```

إذا رأيت النص مطبوعًا بوضوح، مبروك—لقد نجحت في **recognize text from image** مع تعديل الميل تلقائيًا ومعالجة مسبقة!

---

## ## التعرف على النص من صورة – الخطوات التالية والمواضيع ذات الصلة

- **معالجة دفعات:** ضع استدعاء المحرك داخل حلقة `foreach` لمعالجة العشرات من الصور مرة واحدة.  
- **تحويل PDF:** استخدم `engine.RecognizePdf` للمستندات متعددة الصفحات، ثم دمج النتائج.  
- **قواميس مخصصة:** زوّد `engine.CustomWords` بقائمة كلمات لتحسين الدقة في المصطلحات المتخصصة (مثل رموز طبية).  
- **تحسين الأداء:** خزن كائن `OcrEngine` في الذاكرة إذا كنت تعالج الكثير من الصور؛ إنشاء المحرك هو أغلى خطوة من حيث الأداء.  

هذه الإضافات تعتمد بطبيعتها على نفس المفاهيم—**preprocess image for OCR**، **enable auto deskew**، و**recognize text from image**—وبالتالي يمكنك إعادة استخدام أنماط الشيفرة التي تعلمتها الآن.

---

## الخلاصة

لقد استعرضنا **c# ocr example** يوضح كيفية **recognize text from image** باستخدام Aspose.OCR، مع تعديل الميل تلقائيًا وإزالة الضوضاء من الصورة. عبر تفعيل `AutoDeskew` (ميزة **auto deskew image**) وإضافة بعض علمات المعالجة المسبقة، تعزز موثوقية OCR بشكل كبير دون الحاجة لكتابة سطر واحد من شيفرة معالجة الصور بنفسك.

الآن يمكنك أخذ هذا القالب، إدخال صورك الخاصة، والبدء باستخراج البيانات من الفواتير، بطاقات الهوية، أو أي نوع آخر من المستندات الورقية. هل لديك مسح صعب؟ جرّب خيارات المعالجة المسبقة الإضافية التي ذكرناها، أو جرب حزم لغات مخصصة. السماء هي الحد.

إذا ساعدك هذا الدليل على تخطي العقبة، اترك تعليقًا، شارك نتائجك، أو راسلني على GitHub—برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}