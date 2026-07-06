---
category: general
date: 2026-02-22
description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. دليل خطوة بخطوة
  لاستخراج النص من PNG، تحويل الصورة إلى نص، وقراءة المورد المدمج في C# للتراخيص.
draft: false
keywords:
- recognize text from image
- extract text from png
- convert image to text
- read embedded resource c#
- perform ocr on image
language: ar
og_description: تعرف على النص من الصورة فورًا باستخدام Aspose OCR. تعلم استخراج النص
  من PNG، تحويل الصورة إلى نص، وقراءة المورد المدمج في C# للحصول على ترخيص سلس.
og_title: التعرف على النص من الصورة في C# – دليل Aspose OCR الكامل
tags:
- OCR
- C#
- Aspose
- Image Processing
title: التعرف على النص من الصورة في C# باستخدام Aspose OCR
url: /ar/net/text-recognition/recognize-text-from-image-in-c-with-aspose-ocr/
---

/products-backtop-button >}}

All preserved.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في C# باستخدام Aspose OCR

هل احتجت يومًا إلى **التعرف على النص من صورة** لكنك لم تكن متأكدًا من أين تبدأ في C#؟ لست وحدك—معظم المطورين يواجهون نفس الصعوبة عندما يلتقون بـ OCR لأول مرة. في هذا الدرس سنغوص مباشرةً في حل عملي يتيح لك **استخراج النص من png**، **تحويل الصورة إلى نص**، وحتى **قراءة المورد المدمج c#** للحصول على الترخيص دون عناء.  

سنغطي كل شيء من تحميل ترخيص Aspose OCR المدمج إلى طباعة السلسلة النهائية على وحدة التحكم. بحلول النهاية ستحصل على برنامج مستقل يمكنك إدراجه في أي مشروع .NET وتشغيله اليوم.

## ما ستحتاجه

- **.NET 6+** (الكود يُجمّع على .NET Framework أيضًا، لكن .NET 6 هو الإصدار طويل الدعم الحالي)
- **Aspose.OCR for .NET** حزمة NuGet (الإصدار 23.9 أو أحدث)
- صورة **PNG تجريبية** تحتوي على نص إنجليزي واضح ومطبوع
- ملف ترخيص **Aspose OCR** (`Aspose.OCR.lic`) مضاف إلى مشروعك كـ *Embedded Resource*  

إذا كان أي من هذه غير مألوف لك، لا تقلق—كل خطوة أدناه تشرح كيفية إعداده.

## الخطوة 1: قراءة ترخيص المورد المدمج C#  

قبل أن يعمل محرك OCR، يحتاج Aspose إلى ترخيص صالح. تخزين ملف `.lic` كمورد مدمج يبقيه خارج شجرة المصدر ويجعل النشر سهلًا.

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Load the embedded Aspose OCR license
        // ------------------------------------------------------------
        var assembly = Assembly.GetExecutingAssembly();

        // The resource name follows the folder hierarchy in the project.
        // Adjust "MyApp.Resources.Aspose.OCR.lic" if yours differs.
        using (var licenseStream = assembly.GetManifestResourceStream(
               "MyApp.Resources.Aspose.OCR.lic"))
        {
            if (licenseStream == null)
            {
                Console.Error.WriteLine(
                    "License file not found. Make sure it's marked as Embedded Resource.");
                return;
            }

            var license = new License();
            license.SetLicenseFromStream(licenseStream);
        }

        // Continue with OCR steps...
```

**لماذا هذا مهم:**  
إدماج الترخيص يمنع كشفه عن طريق الخطأ في التحكم بالمصدر ويضمن أن الملف ينتقل مع الـ DLL المجمّع. إذا كان الـ stream `null`، يتوقف البرنامج مبكرًا—هذا هو فحصنا الدفاعي الأول.

## الخطوة 2: تهيئة محرك OCR (إجراء OCR على الصورة)  

الآن بعد تحميل الترخيص، يمكننا إنشاء مثال `OcrEngine`. سنضبط اللغة إلى الإنجليزية لأن صورة PNG التجريبية تستخدمها.

```csharp
        // ------------------------------------------------------------
        // 2️⃣ Initialise the OCR engine – this is where we perform OCR on image
        // ------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // change to Language.French etc. if needed
        };
```

**نصيحة:** تعداد `Language` يدعم أكثر من 30 لغة. التبديل سهل مثل `Language.Spanish`. إذا احتجت إلى اكتشاف متعدد اللغات، أنشئ محركات منفصلة أو استخدم `ocrEngine.AutoDetectLanguage = true` (متاح في إصدارات Aspose الأحدث).

## الخطوة 3: تحميل صورة PNG (استخراج النص من PNG)  

Aspose OCR يعمل مع فئة `Image` الخاصة به، وليس `System.Drawing.Image`. وجهه إلى مسار ملف، أو زوده بـ `Stream` إذا فضلت.

```csharp
        // ------------------------------------------------------------
        // 3️⃣ Load the image – this is the step where we extract text from png
        // ------------------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/sample.png";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Image not found at {imagePath}");
            return;
        }

        var image = Image.Load(imagePath);
```

**حالة حافة:** إذا كانت صورة PNG تحتوي على قناة ألفا (خلفية شفافة)، قد يفسر Aspose الفراغات بشكل غير صحيح. إصلاح سريع هو معالجة الصورة مسبقًا باستخدام `ImageProcessor` لتسويتها، لكن بالنسبة لمعظم المستندات الممسوحة يعمل المحمل الافتراضي بشكل جيد.

## الخطوة 4: تشغيل التعرف (تحويل الصورة إلى نص)  

مع جاهزية المحرك والصورة، استدعاء OCR الفعلي هو سطر واحد. كائن النتيجة يمنحك السلسلة الخام ودرجة الثقة.

```csharp
        // ------------------------------------------------------------
        // 4️⃣ Recognise the image – this is where we convert image to text
        // ------------------------------------------------------------
        var ocrResult = ocrEngine.Recognize(image);

        // Optional: check confidence (0‑100)
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

**لماذا قد يهمك مستوى الثقة:**  
ثقة منخفضة (مثلاً < 70٪) عادةً تشير إلى مسح ضبابي أو خط غير مدعوم. في الإنتاج يمكنك الرجوع إلى محرك OCR مختلف أو طلب من المستخدم إعادة المسح.

## الخطوة 5: إخراج النص المُعترف به  

أخيرًا، اطبع السلسلة المستخرجة. في تطبيق حقيقي قد تكتبها إلى قاعدة بيانات، ملف JSON، أو تغذيها إلى فهرس بحث.

```csharp
        // ------------------------------------------------------------
        // 5️⃣ Output the recognised text – the final result of recognize text from image
        // ------------------------------------------------------------
        Console.WriteLine("\n--- Recognised Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### النتيجة المتوقعة في وحدة التحكم

```
Confidence: 96%
--- Recognised Text ---
Hello, world!
This is a sample PNG used for OCR testing.
```

إذا رأيت النص أعلاه (أو شيء مشابه)، مبروك—لقد نجحت في **التعرف على النص من صورة** باستخدام Aspose OCR!

## المشكلات الشائعة وكيفية تجنبها  

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| `License not set` exception | ملف الترخيص غير مدمج أو اسم المورد غير صحيح | تحقق من `Build Action = Embedded Resource` وتأكد من الاسم المؤهل بالكامل |
| إخراج فارغ | دقة الصورة (DPI) منخفضة جدًا (أقل من 150) | أعد تحجيم PNG إلى ما لا يقل عن 150 DPI قبل إرساله إلى Aspose |
| حروف مشوهة | اختيار لغة خاطئة | عيّن `ocrEngine.Language` إلى قيمة تعداد `Language` الصحيحة |
| `OutOfMemoryException` on large images | تحميل PNG كبير جدًا (أكثر من 10 ميغابايت) مباشرة | استخدم `Image.Load(stream, maxWidth: 2000, maxHeight: 2000)` لتقليل الحجم أثناء التحميل |

## نصيحة احترافية: المعالجة الدفعية  

إذا كنت بحاجة إلى **التعرف على النص من صورة** ملفات بشكل جماعي، غلف المنطق الأساسي داخل حلقة `foreach` وأعد استخدام نفس مثال `OcrEngine`. إعادة استخدام المحرك يوفر بضع مليثانية لكل ملف لأن المكتبات الأصلية تظل محملة.

```csharp
var images = System.IO.Directory.GetFiles("YOUR_DIRECTORY", "*.png");
foreach (var path in images)
{
    var img = Image.Load(path);
    var result = ocrEngine.Recognize(img);
    Console.WriteLine($"{path} → {result.Text.Trim()}");
}
```

## الخطوات التالية  

- **ضبط ما قبل المعالجة** – جرّب `ImageProcessor` لتحسين التباين أو إزالة الضوضاء.  
- **استكشاف صيغ إخراج أخرى** – `ocrResult.GetWords()` يمنحك الصناديق المحيطة، مفيد لتسليط الضوء على النص في واجهة المستخدم.  
- **دمج مع Azure Cognitive Services** إذا كنت تحتاج إلى دعم كتابة يدوية سحابي.  

جميع هذه الإضافات لا تزال تعتمد على النمط الأساسي نفسه: تحميل ترخيص، إنشاء محرك، إمداد صورة، وقراءة النص.

![لقطة شاشة لوحدة التحكم تُظهر النص المُعترف به من صورة](/images/ocr-result.png "recognize text from image result screenshot")

## الخاتمة  

لقد استعرضنا مثالًا كاملًا وجاهزًا للإنتاج يوضح كيفية **التعرف على النص من صورة** في C# باستخدام Aspose OCR. من قراءة مورد مدمج للحصول على الترخيص إلى تحميل PNG، إجراء OCR، وطباعة النتيجة، تم تغطية كل جزء.  

الآن يمكنك **استخراج النص من png**، **تحويل الصورة إلى نص**، وحتى **قراءة المورد المدمج c#** للحصول على الترخيص—كل ذلك في بضع عشرات من الأسطر البرمجية. لا تتردد في تجربة لغات مختلفة، دفعات صور أكبر، أو دمج النتيجة في خط أنابيب معالجة المستندات الخاص بك. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}