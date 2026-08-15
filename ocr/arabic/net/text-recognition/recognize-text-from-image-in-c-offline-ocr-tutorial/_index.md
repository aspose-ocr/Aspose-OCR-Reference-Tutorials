---
category: general
date: 2026-04-29
description: تعلم كيفية التعرف على النص من الصورة دون اتصال باستخدام Aspose OCR. يتضمن
  خطوات استخراج النص من ملف PNG وتحميل الصورة للتعرف الضوئي على الأحرف في تطبيق C#
  واحد.
draft: false
keywords:
- recognize text from image
- extract text from png
- load image for ocr
- Aspose OCR offline
- C# OCR example
language: ar
og_description: التعرف على النص من الصورة دون اتصال باستخدام Aspose OCR في C#. دليل
  خطوة بخطوة لاستخراج النص من ملف PNG وتحميل الصورة للتعرف الضوئي على الأحرف.
og_title: التعرف على النص من الصورة – دليل OCR الكامل دون اتصال
tags:
- OCR
- C#
- Aspose
- Image Processing
title: التعرف على النص من الصورة في C# – دليل OCR دون اتصال
url: /ar/net/text-recognition/recognize-text-from-image-in-c-offline-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة – دليل OCR كامل دون اتصال

هل احتجت يومًا إلى **التعرف على النص من صورة** بينما يعمل تطبيقك على جهاز لا يتوفر فيه اتصال بالإنترنت؟ ربما تقوم بإنشاء ماسح جهاز ميداني، أو كشك آمن، أو تريد فقط تجنب زمن الانتظار في الخدمات السحابية. في هذا الدرس سنستعرض برنامج C# مستقل **يتعرف على النص من صورة** باستخدام Aspose OCR، وسنوضح لك أيضًا كيفية **استخراج النص من png** و**تحميل الصورة لـ OCR** بشكل صحيح عندما تكون الموارد مخزنة على القرص.

سنغطي كل ما تحتاجه: حزمة NuGet الدقيقة، هيكل المجلدات للملفات المسبقة التحميل لوحدات OCR، وبعض النصائح التي تجعل كودك قويًا عندما تواجه مشاكل. في النهاية ستحصل على تطبيق console يعمل ويطبع النص المتعرف عليه في وحدة التحكم—بدون أي استدعاءات شبكة.

## المتطلبات المسبقة

- .NET 6 (أو أي نسخة حديثة من .NET) مثبتة محليًا.  
- Visual Studio 2022 أو VS Code—أي بيئة تطوير تفضلها.  
- حزمة NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
- ملفات موارد OCR غير المتصلة بالإنترنت التي تم تنزيلها من بوابة Aspose (حجمها بضع ميغابايت فقط).  
- صورة PNG (`offline_test.png`) تريد معالجتها.

> **نصيحة احترافية:** احفظ مجلد الموارد بجوار الملف التنفيذي؛ سيسهل ذلك حل المسارات النسبية بشكل كبير.

## الخطوة 1 – إنشاء كائن محرك OCR

أول شيء نفعله هو إنشاء كائن `OcrEngine`. فكر فيه كالعقل الذي سيحلل البكسلات لاحقًا.

```csharp
using Aspose.OCR;
using System;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

لماذا ننشئ كائنًا جديدًا في كل تشغيل؟ يضمن ذلك حالة نظيفة، خاصةً عندما تقوم بتبديل خيارات مثل تنزيل الموارد تلقائيًا. في خدمة طويلة التشغيل قد تعيد استخدام المحرك، لكن لهذا العرض البسيط هذه الطريقة هي الأكثر أمانًا.

## الخطوة 2 – توجيه المحرك إلى مواردك غير المتصلة

عادةً ما يقوم Aspose OCR بجلب حزم اللغات من السحابة. بما أننا نريد **التعرف على النص من صورة** دون اتصال، يجب إخبار المحرك بمكان وجود الملفات.

```csharp
        // Step 2: Point the engine to the folder containing the pre‑downloaded OCR modules
        ocrEngine.Config.ResourcesPath = @"YOUR_DIRECTORY";
```

استبدل `YOUR_DIRECTORY` بالمسار المطلق أو النسبي الذي يحتوي على مجلد `ocrdata` الذي استخرجته من تحميل Aspose. إذا كان المسار غير صحيح، سيطرح المحرك استثناء `FileNotFoundException`—لذا تأكد من صحة الكتابة.

## الخطوة 3 – إيقاف تنزيل الموارد تلقائيًا

بشكل افتراضي يحاول Aspose تنزيل الوحدات المفقودة عند الحاجة. في سيناريو غير متصل نحتاج إلى تعطيل هذه الميزة صراحةً.

```csharp
        // Step 3: Disable automatic resource download to enforce offline operation
        ocrEngine.Config.AllowAutomaticResourceDownload = false;
```

إذا نسيت إضافة هذا السطر، سيحاول المحرك إجراء اتصال شبكة، وهو ما سيفشل بصمت في العديد من جدران الحماية المؤسسية ويتركك بنتيجة فارغة. إيقافه يسرّع أيضًا عملية التعرف الأولى لأن المحرك يتخطى فحص التنزيل.

## الخطوة 4 – تحميل الصورة وتشغيل OCR

الآن نأتي إلى **تحميل الصورة لـ OCR**. المساعد الثابت `LoadImage` يقبل مسار الملف ويعيد كائن `Image` يمكن للمحرك استهلاكه.

```csharp
        // Step 4: Load the image to be processed and run OCR
        var ocrResult = ocrEngine.Recognize(
            OcrEngine.LoadImage(@"YOUR_DIRECTORY/offline_test.png"));
```

لاحظ أننا نستخدم ملف PNG—مثالي لاستخراج النص بدون فقدان. إذا كان لديك JPEG، فإن نفس الاستدعاء يعمل، لكن PNG عادةً ما يعطي نتائج أنظف لأنه لا يحتوي على تشوهات ضغط.

## الخطوة 5 – عرض النص المتعرف عليه

طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على خاصية `Text`. نكتبها ببساطة إلى وحدة التحكم.

```csharp
        // Step 5: Display the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مثل:

```
Hello, Aspose OCR!
This is an offline test.
```

إذا كان الإخراج فارغًا، تحقق مرة أخرى من `ResourcesPath` وتأكد من وجود وحدة اللغة (مثل `English`).

![التعرف على النص من صورة باستخدام Aspose OCR](/images/offline_ocr_demo.png "التعرف على النص من صورة")

*الصورة أعلاه تُظهر مخرجات وحدة التحكم بعد استخراج النص من png.*

## الحالات الشائعة وكيفية التعامل معها

### 1. الصورة كبيرة جدًا

ملفات PNG ذات الدقة العالية قد تضع ضغطًا على الذاكرة. قلل حجم الصورة قبل تمريرها إلى المحرك:

```csharp
using System.Drawing;

// Load, resize, then pass to OCR
var original = (Bitmap)Image.FromFile(@"YOUR_DIRECTORY/offline_test.png");
var resized = new Bitmap(original, new Size(original.Width / 2, original.Height / 2));
var tempPath = Path.Combine(Path.GetTempPath(), "temp_resized.png");
resized.Save(tempPath);
var ocrResult = ocrEngine.Recognize(OcrEngine.LoadImage(tempPath));
```

### 2. عدم اكتشاف اللغة

إذا كنت تحاول **استخراج النص من png** يحتوي على لغة غير الإنجليزية، عيّن اللغة صراحةً:

```csharp
ocrEngine.Config.Language = Language.French; // or Language.Spanish, etc.
```

تأكد من وجود حزمة اللغة المقابلة في مجلد الموارد غير المتصل.

### 3. صور فارغة أو منخفضة التباين

يواجه OCR صعوبة مع التباين المنخفض. عالج الصورة بعتبة بسيطة:

```csharp
using System.Drawing.Imaging;

var bitmap = new Bitmap(@"YOUR_DIRECTORY/offline_test.png");
for (int y = 0; y < bitmap.Height; y++)
{
    for (int x = 0; x < bitmap.Width; x++)
    {
        var pixel = bitmap.GetPixel(x, y);
        var gray = (pixel.R + pixel.G + pixel.B) / 3;
        var bw = gray > 128 ? Color.White : Color.Black;
        bitmap.SetPixel(x, y, bw);
    }
}
bitmap.Save(@"YOUR_DIRECTORY/processed.png");
```

ثم وجه محرك OCR إلى `processed.png`. هذه اللمسة الصغيرة غالبًا ما تحول معدل نجاح 30 % إلى استخراج شبه كامل.

## مثال كامل يعمل

فيما يلي البرنامج *كاملًا* يمكنك نسخه ولصقه في `Program.cs`. لا تنس استبدال `YOUR_DIRECTORY` بالمسار الفعلي على جهازك.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set offline resources folder
        ocrEngine.Config.ResourcesPath = @"C:\OCRResources";

        // 3️⃣ Prevent any network calls
        ocrEngine.Config.AllowAutomaticResourceDownload = false;

        // 4️⃣ Load PNG and recognize
        string imagePath = @"C:\OCRResources\offline_test.png";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        var ocrResult = ocrEngine.Recognize(OcrEngine.LoadImage(imagePath));

        // 5️⃣ Output the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**الإخراج المتوقع** (با افتراض أن PNG يحتوي على النص “Hello World!”):

```
=== OCR Output ===
Hello World!
```

شغّله باستخدام `dotnet run` من مجلد المشروع وسترى وحدة التحكم تطبع السلسلة المستخرجة.

## ملخص – ما أنجزناه

- **التعرف على النص من صورة** بالكامل دون اتصال باستخدام Aspose OCR.  
- عرضنا كيفية **استخراج النص من png** دون أي خدمة خارجية.  
- أظهرنا الطريقة الصحيحة لـ **تحميل الصورة لـ OCR** وتكوين المحرك للعمل دون اتصال.  

كل ذلك في تطبيق C# console واحد مستقل.

## الخطوات التالية والمواضيع ذات الصلة

- **المعالجة الدفعية** – تكرار عبر مجلد PNGs وكتابة كل نتيجة إلى ملف `.txt`.  
- **صيغ ملفات مختلفة** – جرّب `LoadImage` مع TIFF أو BMP للحصول على مسح أعلى دقة.  
- **تحسين الأداء** – فعّل التعرف متعدد الخيوط إذا كان لديك عدة نوى.  
- **التكامل مع ASP.NET Core** – أنشئ نقطة API تستقبل صورة مرفوعة وتعيد نتيجة OCR، مع البقاء في وضع عدم الاتصال.

إذا كنت مهتمًا بالتعامل مع ملفات PDF، اطلع على دليلنا “التعرف على النص من PDF باستخدام Aspose PDF”. لمزيد من معالجة الصور المتقدمة، راجع ربطات OpenCV لـ C#.

---

*برمجة سعيدة! إذا واجهت أي صعوبة، لا تتردد بترك تعليق أدناه—سأحاول مساعدتك في استخراج النص من أي صورة، مهما كانت عنيدة.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}