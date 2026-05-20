---
category: general
date: 2026-05-02
description: التعرف على نص الصورة باستخدام Aspose OCR C#. تعلم كيفية معالجة صورة OCR
  مسبقًا، وزيادة الدقة، واستخراج نص نظيف في بضع خطوات فقط.
draft: false
keywords:
- recognize text image
- aspose ocr c#
- preprocess image ocr
- ocr preprocessing
- deskew denoise binarization
language: ar
og_description: تعرّف على النص في الصورة بسرعة باستخدام Aspose OCR C#. يوضح لك هذا
  الدليل كيفية معالجة صورة OCR مسبقًا للحصول على أفضل النتائج.
og_title: التعرف على صورة النص باستخدام Aspose OCR C# – دليل كامل للمعالجة المسبقة
tags:
- OCR
- C#
- Image Processing
title: التعرف على صورة النص باستخدام Aspose OCR C# – دليل المعالجة المسبقة الكامل
url: /ar/net/ocr-optimization/recognize-text-image-with-aspose-ocr-c-complete-preprocess-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على نص الصورة باستخدام Aspose OCR C# – دليل المعالجة المسبقة الكامل

هل احتجت يوماً إلى **التعرف على نص الصورة** لكن النتائج بدت كأنها مجرد رموز غير مفهومة بدلاً من جمل قابلة للقراءة؟ لست وحدك—المسحات الضوضائية، الإيصالات المائلة، أو لقطات الشاشة ذات التباين المنخفض يمكن أن تحول OCR إلى لعبة تخمين. الخبر السار؟ باستخدام Aspose OCR C# يمكنك تنظيف تلك الصور المشكلة قبل أن ينظر المحرك إليها، وستصبح النتيجة أوضح بكثير.

في هذا الدرس سنستعرض حلًا **خطوة بخطوة** لا يوضح لك فقط كيفية التعرف على نص الصورة، بل أيضًا كيفية *معالجة صورة OCR* مسبقًا باستخدام تصحيح الميل، إزالة الضوضاء، والتحويل إلى ثنائي. في النهاية ستحصل على برنامج C# جاهز للتنفيذ، وفهم قوي لأسباب أهمية كل خيار من خيارات المعالجة المسبقة، ومجموعة من النصائح التي يمكنك تطبيقها على أي مشروع OCR.

## ما ستحتاجه

- **.NET 6** أو أحدث (الكود يعمل مع .NET Core و .NET Framework على حد سواء)  
- حزمة NuGet **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`)  
- صورة نموذجية مائلة أو ضوضائية أو ذات تباين منخفض (مثال: `skewed_noisy.jpg`)  
- Visual Studio 2022 أو أي بيئة تطوير C# تفضلها  

لا مكتبات أصلية إضافية، ولا خدمات خارجية—فقط كود مُدار بالكامل.

---

## الخطوة 1: تثبيت Aspose OCR C# وإضافة المساحات الاسمية

أولاً وقبل كل شيء. احصل على مكتبة Aspose OCR من NuGet وأدرج المساحات الاسمية المطلوبة. هذا يضمن أن المترجم يعرف مكان وجود `OcrEngine` و `PreprocessOptions` وغيرها من الفئات.

```csharp
// Install via NuGet Package Manager Console:
// PM> Install-Package Aspose.OCR

using Aspose.OCR;
using Aspose.OCR.Settings;
```

> **نصيحة احترافية:** إذا كنت تستخدم .NET CLI، نفّذ `dotnet add package Aspose.OCR` بدلاً من ذلك. الحفاظ على حزمك محدثة (الإصدار الحالي 23.8) يساعدك على الاستفادة من أحدث خوارزميات المعالجة المسبقة.

---

## الخطوة 2: إنشاء محرك OCR وتمكين المعالجة المسبقة

قلب الحل هو `OcrEngine`. بشكل افتراضي سيحاول قراءة البت ماب الخام، مما يؤدي غالبًا إلى فقدان الأحرف في المسح الضوضائي. لذلك نقوم بتمكين ثلاث علامات معالجة مسبقة:

- **Deskew** – يُصحّح خطوط النص المائلة.  
- **Denoise** – يُزيل البقع والضوضاء الناتجة عن الضغط.  
- **Binarization** – يحول الصورة إلى أبيض‑أسود، مما يعزز التباين.

```csharp
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Configure preprocessing options
ocrEngine.Settings.PreprocessOptions = new PreprocessOptions
{
    EnableDeskew = true,          // Auto‑detect and correct rotation
    EnableDenoise = true,         // Reduce random noise
    EnableBinarization = true,    // Force black‑white conversion
    BinarizationThreshold = 120   // Tune based on your image brightness
};
```

**لماذا هذه الخيارات؟**  
`Deskew` يُصلح مشكلة الزاوية التي تجعل الأحرف مائلة، وهو ما تكافح معظم خوارزميات OCR معه. `Denoise` يزيل البكسلات العشوائية التي قد تُفسَّر كعلامات ترقيم. `Binarization` يُحسّن الفصل بين الخلفية والواجهة، وهو عامل أساسي لتجزئة الأحرف بدقة.

---

## الخطوة 3: توجيه المحرك إلى صورتك

الآن نخبر المحرك بأي ملف يجب معالجته. استخدم مسارًا مطلقًا أو مسارًا نسبيًا من مجلد إخراج المشروع. إذا كنت تجرب، انسخ بعض صور الاختبار إلى مجلد `Resources`.

```csharp
// Step 3: Specify the input image
string imagePath = @"Resources/skewed_noisy.jpg";

// Optional: Verify the file exists before proceeding
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"Image not found: {imagePath}");
    return;
}
```

> **حالة حدية:** إذا كانت صورتك بتنسيق غير مدعوم أصلاً (مثل TIFF متعدد الصفحات)، حوّلها إلى PNG أو JPEG أولاً، أو استخدم `Aspose.Imaging` لاستخراج الصفحة المطلوبة.

---

## الخطوة 4: تشغيل OCR على الصورة المعالجة مسبقًا

بعد تكوين المحرك وتحديد موقع الصورة، استدعِ `RecognizeImage`. تُعيد الطريقة كائن `OcrResult` يحتوي على النص المستخرج، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها لاحقًا.

```csharp
// Step 4: Perform OCR
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

// Check if any text was found
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("No recognizable text found.");
    return;
}
```

**ماذا يحدث خلف الكواليس؟**  
Aspose OCR أولاً يُنفّذ خط أنابيب المعالجة المسبقة الذي حددته في الخطوة 2، ثم يمرر البت ماب المنظف إلى مُعرّف الشبكة العصبية الخاص به. النتيجة عادةً ما تكون قفزة دراماتيكية في الدقة—غالبًا من 60 % إلى أكثر من 95 % على المسحات الصعبة.

---

## الخطوة 5: عرض أو تخزين النص المُعترف به

أخيرًا، أظهر السلسلة المُعترف بها في وحدة التحكم، أو احفظها في ملف، أو أرسلها إلى أي خدمة لاحقة. للعرض السريع، وحدة التحكم تكفي.

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("======================");

// Optional: Save to a .txt file
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

المخرجات المتوقعة تكون نصًا نظيفًا مفصولًا بأسطر—بدون رموز عشوائية أو كلمات مكسورة.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في تطبيق وحدة تحكم. يتضمن جميع الخطوات، معالجة الأخطاء، وتعليقات توضيحية لتبدأ فورًا.

```csharp
// ------------------------------------------------------------
// Full Example: Recognize Text Image with Aspose OCR C#
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class PreprocessExample
{
    public static void Run()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable preprocessing – deskew, denoise, binarization
        ocrEngine.Settings.PreprocessOptions = new PreprocessOptions
        {
            EnableDeskew = true,
            EnableDenoise = true,
            EnableBinarization = true,
            BinarizationThreshold = 120 // Adjust for your images
        };

        // 3️⃣ Specify the input image
        string imagePath = @"Resources/skewed_noisy.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        // 4️⃣ Run OCR on the preprocessed image
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found.");
            return;
        }

        // 5️⃣ Display the recognized text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Save to a file for later use
        System.IO.File.WriteAllText("output.txt", ocrResult.Text);
    }

    // Entry point for quick testing
    static void Main()
    {
        Run();
    }
}
```

**المخرجات المتوقعة في وحدة التحكم (مثال):**

```
=== Recognized Text ===
Invoice #12345
Date: 2024-04-30
Total: $1,250.00
Thank you for your business!
======================
```

إذا شغّلت نفس الكود دون المعالجة المسبقة، من المحتمل أن ترى أحرفًا مشوشة مثل “Ivn0i#12?5” بدلاً من “Invoice #12345”.

---

## الأسئلة المتكررة (FAQs)

### هل يعمل هذا مع **Aspose OCR C#** على .NET Core؟
بالتأكيد. المكتبة **غير مرتبطة بمنصة**؛ فقط أضف حزمة NuGet وستكون جاهزًا.

### ماذا لو كانت الصورة ذات تباين عالي بالفعل—هل يجب أن أُفعّل التحويل إلى ثنائي؟
عادةً نعم. التحويل إلى ثنائي مع عتبة معقولة (120 تعمل مع معظم المستندات الممسوحة) لا يضر الصورة النقية، ويضمن أن المحرك يتعامل مع بت ماب ثنائي، وهو الشكل الأمثل للمدخلات.

### هل يمكن تعديل زاوية الـ deskew يدويًا؟
نعم، عبر الوصول إلى `ocrEngine.Settings.PreprocessOptions.DeskewAngle`. ومع ذلك، خوارزمية الاكتشاف التلقائي موثوقة للزوايا بين –15° و +15°. للدوارات الشديدة، قم بلف الصورة مسبقًا باستخدام مكتبة معالجة صور أخرى.

### كيف أتعامل مع ملفات PDF متعددة الصفحات؟
حوّل كل صفحة إلى صورة (مثلاً باستخدام `Aspose.PDF`)، ثم كرّر عبر الصفحات مستدعيًا `RecognizeImage` لكل واحدة. احفظ النتائج في قائمة وادمجها إذا لزم الأمر.

---

## نصائح احترافية ومخاطر شائعة

- **ضبط العتبة:** إذا لاحظت أن الأحرف الخفيفة تُحذف، اخفض `BinarizationThreshold` إلى 90؛ إذا ظهرت الكثير من البقع السوداء، ارفعها إلى 150.  
- **إدارة الذاكرة:** للدفعات الكبيرة، أعد استخدام كائن `OcrEngine` واحد بدلاً من إنشاء جديد لكل صورة—هذا يقلل من ضغط الـ GC.  
- **دعم اللغات:** Aspose OCR يدعم عدة لغات مباشرة. عيّن `ocrEngine.Language = Language.English` (أو غيرها) قبل استدعاء `RecognizeImage` للحصول على دقة أعلى للنص غير الإنجليزي.  
- **التسجيل (Logging):** فعّل `ocrEngine.Settings.LogLevel = LogLevel.Debug` إذا احتجت لتتبع سبب فشل صورة معينة.

---

## الخلاصة

لقد أظهرنا لك كيفية **التعرف على نص الصورة** بثقة باستخدام Aspose OCR C# مع تطبيق تقنيات *معالجة صورة OCR* الأساسية. بتمكين deskew، denoise، وbinarization، يحصل المحرك على بت ماب نظيف، ما يترجم إلى درجات ثقة أعلى وأخطاء نسخ أقل بكثير.

خذ هذا الكود، ووجّهّه إلى مسحاتك الخاصة، واضبط العتبات، وستلاحظ نفس الارتفاع في الدقة عبر الفواتير، الإيصالات، أو الملاحظات المكتوبة يدويًا. بعد ذلك، يمكنك استكشاف ميزات **aspose ocr c#** المتقدمة مثل القواميس المخصصة، OCR القائم على المناطق، أو التكامل مع Azure Blob لتدفقات عمل واسعة النطاق.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالكريستال!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}