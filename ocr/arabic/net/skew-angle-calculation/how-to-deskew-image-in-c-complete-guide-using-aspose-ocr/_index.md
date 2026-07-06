---
category: general
date: 2026-03-21
description: تعلم كيفية تصحيح إمالة ملفات الصور والتعرف على النص في الصورة باستخدام
  Aspose OCR. حوّل ملفات JPG إلى نص وصحّح دوران الصورة ببضع أسطر من كود C#.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: ar
og_description: كيفية تصحيح انحراف الصورة واستخراج النص من ملفات JPEG باستخدام Aspose
  OCR. اتبع هذا الدليل خطوة بخطوة لتحويل JPG إلى نص وتصحيح دوران الصورة.
og_title: كيفية تصحيح انحراف الصورة في C# – دليل Aspose OCR السريع
tags:
- OCR
- C#
- Aspose
title: كيفية تصحيح انحراف الصورة في C# – دليل كامل باستخدام Aspose OCR
url: /ar/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح إمالة الصورة في C# – دليل كامل باستخدام Aspose OCR

هل تساءلت يومًا **كيف تصحح إمالة الصورة** للملفات التي خرجت من الماسح الضوئي مائلة بزاوية غريبة؟ لست وحدك—فالعديد من المطورين يواجهون هذه المشكلة عندما يحاولون استخراج النص من الإيصالات، الفواتير، أو الملاحظات المكتوبة يدويًا. الخبر السار هو أنه باستخدام Aspose OCR يمكنك تصحيح دوران الصورة واستخراج نص نظيف قابل للبحث ببضع أسطر فقط.

في هذا الدرس سنستعرض العملية بالكامل: من تثبيت المكتبة، تمكين التصحيح التلقائي للإمالة، إلى التعرف على نص الصورة وأخيرًا تحويل JPG إلى نص. في النهاية ستحصل على تطبيق كونسول جاهز للتشغيل يمكنه **التعرف على نص jpg** دون الحاجة إلى تدويرها يدويًا أولاً.

## ما ستحتاجه

- **.NET 6.0** أو أحدث (الكود يعمل على .NET Core و .NET Framework على حد سواء)  
- حزمة **Aspose.OCR for .NET** عبر NuGet – يفضَّل الإصدار 23.12 أو أحدث  
- صورة **JPEG مائلة** تجريبية (مثال: `skewed_receipt.jpg`) موجودة في مكان يمكن للتطبيق قراءته  
- Visual Studio، VS Code، أو أي محرر C# تفضله  

لا توجد أدوات طرف ثالث أخرى مطلوبة. المكتبة تتعامل مع تصحيح الإمالة، OCR، وحتى اكتشاف اللغة داخليًا.

![مثال على كيفية تصحيح إمالة الصورة](/images/deskew-example.png "كيفية تصحيح إمالة الصورة باستخدام Aspose OCR")

## الخطوة 1: إعداد المشروع وتثبيت Aspose.OCR

للحفاظ على التنظيم، ابدأ مشروع كونسول جديد:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

سطر `dotnet add package` يجلب ملفات **Aspose.OCR** الثنائية بالإضافة إلى جميع الاعتمادات الأصلية. إذا كنت على Windows ستحصل على ملفات DLL الأصلية تلقائيًا؛ على Linux/macOS قد تحتاج إلى حزمة `libgdiplus`، لكنها تثبيت مرة واحدة.

## الخطوة 2: تمكين التصحيح التلقائي للإمالة (تصحيح دوران الصورة)

الآن افتح `Program.cs` واستبدل محتوياته بالكود أدناه. السطر الرئيسي هنا هو `ocrEngine.Settings.Deskew = true;` – هذا هو العلم الذي يخبر المحرك **كيف يصحح إمالة الصورة** تلقائيًا.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### لماذا تمكين التصحيح التلقائي للإمالة؟

عندما يمر الماسح الضوئي بصفحة بزاوية، يكون خط أساس النص مائلًا. محركات OCR التقليدية تقرأ كل حرف كنسخة مائلة، مما يقلل الدقة بشكل كبير. من خلال ضبط `Deskew = true`، يقوم Aspose OCR بتنفيذ تحويل Hough سريع في الخلفية، يدور الصورة إلى الوضع الأفقي، ثم يجري التعرف. النتيجة هي نفسها كما لو أنك قمت يدويًا بتدوير الصورة في Photoshop—لكن بسرعة أكبر وبشكل آلي بالكامل.

## الخطوة 3: التعرف على نص الصورة وتحويل JPG إلى نص

استدعاء `Recognize` يقوم بعملين في آن واحد:

1. **يصصح إمالة** الصورة (لأننا فعلنا العلم).  
2. **يستخرج** المحتوى النصي، ويعيده في كائن `OcrResult`.

يمكنك التعامل مع `ocrResult.Text` كسلسلة نصية عادية، كتابةها إلى ملف، أو تمريرها إلى خطوط معالجة لاحقة. إذا كنت بحاجة إلى درجات الثقة الخام لكل كلمة، فإن `ocrResult.Words` يوفر لك مجموعة تحتوي على قيم `Confidence`.

### مثال على المخرجات

بافتراض أن `skewed_receipt.jpg` يحتوي على إيصال بسيط، قد ترى شيئًا مثل:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

لاحظ كيف أن الأرقام تصطف بشكل جميل رغم أن الصورة الأصلية كانت مائلة بحوالي 7°. هذه هي سحر **تصحيح دوران الصورة** المدمج في المكتبة.

## الخطوة 4: تشغيل المثال والتحقق من النتائج

قم بالترجمة والتشغيل:

```bash
dotnet run
```

إذا تم ربط كل شيء بشكل صحيح سترى النص المستخرج يُطبع في الكونسول. إذا حصلت على استثناء مثل `FileNotFoundException`، تحقق مرة أخرى من مسار ملف JPEG وتأكد من أن الملف قابل للقراءة.

### الأخطاء الشائعة والنصائح الاحترافية

- **الصور الكبيرة** – استهلاك الذاكرة في OCR يزداد مع أبعاد الصورة. قم بإعادة تحجيم الملفات الضخمة جدًا (مثال: عرض > 3000 بكسل) قبل تمريرها إلى المحرك.  
- **الخطوط غير اللاتينية** – بشكل افتراضي يفترض المحرك اللغة الإنجليزية. اضبط `ocrEngine.Settings.Language = OcrLanguage.French;` (أو أي لغة مدعومة) إذا كنت بحاجة إلى **التعرف على نص الصورة** بأبجديات أخرى.  
- **المعالجة الدفعية** – للعديد من الملفات، أعد استخدام نفس كائن `OcrEngine`؛ إنشاء محرك جديد لكل ملف يضيف عبءً غير ضروري.  
- **فحص الجودة** – بعد تصحيح الإمالة يمكنك تصدير الصورة المصححة عبر `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` للتحقق بصريًا من إصلاح الدوران.

## مثال كامل يعمل (الكل معًا)

فيما يلي البرنامج الكامل المستقل الذي يمكنك نسخه ولصقه في `Program.cs`. يتضمن تعليقات، معالجة أخطاء، وخطوة اختيارية لحفظ الصورة المصححة.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

تشغيل البرنامج سيقوم **بالتعرف على نص jpg** للملفات، وتصحيح أي إمالة تلقائيًا، وطباعة نص نظيف قابل للبحث في الكونسول.

## الخلاصة

أصبح لديك الآن مقتطف قوي وجاهز للإنتاج يوضح **كيفية تصحيح إمالة الصورة** للملفات واستخراج محتواها باستخدام Aspose OCR. النهج يعمل مع الإيصالات، الفواتير، العقود الممسوحة، أو أي ملف JPEG حيث النص ليس أفقيًا تمامًا.

الخطوات التالية التي قد تستكشفها:

- **المعالجة الدفعية** لمجلد من ملفات JPEG وكتابة كل نتيجة إلى ملف `.txt` (يرتبط بـ *تحويل jpg إلى نص*).  
- دمج خطوة OCR في API مبني على ASP.NET Core بحيث يمكن للعملاء رفع الصور والحصول على نص بصيغة JSON.  
- تجربة إعدادات OCR مختلفة مثل `ocrEngine.Settings.Language` أو `ocrEngine.Settings.RecognitionMode` لتحسين الدقة للوثائق غير الإنجليزية.

جرّبه، عدّل الإعدادات، ودع المحرك يقوم بالعمل الشاق. كما هو الحال دائمًا، إذا واجهت مشكلة أو لديك تحسين ذكي لتشاركه، اترك تعليقًا أدناه. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}