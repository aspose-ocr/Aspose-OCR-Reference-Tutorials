---
category: general
date: 2026-03-17
description: استخراج النص من ملف PNG باستخدام Aspose OCR في C#. تعلم كيفية قراءة النص
  من الصورة، ومعالجة OCR للإيصالات، وإنشاء محرك OCR مع تسريع GPU.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: ar
og_description: استخراج النص من PNG باستخدام Aspose OCR. يوضح هذا الدليل كيفية قراءة
  النص من الصورة، ومعالجة OCR للإيصالات، وإنشاء محرك OCR بكفاءة.
og_title: استخراج النص من PNG – قراءة النص من الصورة باستخدام OCR
tags:
- OCR
- CSharp
- Aspose
title: استخراج النص من PNG – قراءة النص من الصورة باستخدام OCR
url: /ar/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

from png example" should be translated? The alt text is part of markdown; we should translate visible text but keep URL. So alt text becomes Arabic: "مثال استخراج النص من png". Title also translate.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من PNG – قراءة النص من الصورة باستخدام OCR

هل احتجت يومًا إلى **استخراج النص من PNG** لكن لم تكن متأكدًا أي مكتبة ستعطيك نتائج موثوقة؟ لست وحدك—المطورون يسألون باستمرار، “كيف يمكنني قراءة النص من ملفات الصور مثل الإيصالات دون كتابة شبكة عصبية مخصصة؟” الخبر السار هو أن Aspose OCR يقوم بالعمل الشاق نيابةً عنك، ويمكنك حتى تشغيل وحدة معالجة الرسومات (GPU) للحصول على تسريع في السرعة.

في هذا الدرس سنستعرض كل ما تحتاجه **لمعالجة OCR للإيصالات**، بدءًا من تثبيت حزمة NuGet وحتى إنشاء محرك OCR يفهم ملف PNG الخاص بك. في النهاية ستحصل على تطبيق console مستقل يقرأ صورة إيصال، يطبع النص المُعرَّف، ويُظهر لك كيفية تعديل المحرك لسيناريوهات مختلفة. لا مستندات خارجية، فقط شفرة صافية وشروحات واضحة.

## المتطلبات المسبقة

- .NET 6.0 SDK (أو أي نسخة حديثة من .NET)  
- Visual Studio 2022 أو VS Code مع امتدادات C#  
- بطاقة NVIDIA مدعومة مع أحدث برنامج تشغيل (اختياري، لكن يُنصح به لتفعيل وضع GPU)  
- حزمة **Aspose.OCR** من NuGet (`dotnet add package Aspose.OCR`)  

إذا لم يكن لديك GPU، يمكنك تشغيل المثال في وضع CPU—فقط تخطّ سطر إعدادات GPU.

## الخطوة 1: تثبيت Aspose.OCR وإعداد المشروع

أولًا، أنشئ مشروع console جديد وأضف مكتبة Aspose OCR.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

لماذا هذا مهم: حزمة `Aspose.OCR` تتضمن محرك OCR، محملات الصور، ودعم GPU اختياري. إضافتها عبر NuGet يضمن حصولك على أحدث نسخة مستقرة (حتى مارس 2026 الإصدار 23.10).

## الخطوة 2: استيراد المساحات الاسمية وإنشاء محرك OCR

الآن افتح **Program.cs** وأضف توجيهات `using` المطلوبة. ثم أنشئ المحرك.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**نصيحة احترافية:** إذا واجهت استثناء `System.DllNotFoundException` على أجهزة لا تحتوي على GPU، ما عليك سوى تعليق السطرين اللذين يحددان `EngineMode` و `GpuDeviceId`. سيعود المحرك تلقائيًا إلى وضع CPU.

## الخطوة 3: تحميل صورة PNG التي تريد استخراج النص منها

يمكن لـ Aspose OCR قراءة الصور مباشرةً من مسار ملف، أو تدفق، أو حتى مصفوفة بايت. في هذا العرض سنحمّل صورة إيصال محلية.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

لاحظ كيف نتحقق من وجود الملف. في التطبيقات الواقعية قد تُظهر رسالة واجهة مستخدم ودية بدلاً من الخروج الفوري.

## الخطوة 4: تنفيذ التعرف الضوئي على الحروف (OCR)

استخراج النص الفعلي يتم باستدعاء طريقة واحدة. يُعيد المحرك كائن `OcrResult` يحتوي على السلسلة الخام، درجات الثقة، ومعلومات التخطيط.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

لماذا نتحقق من `ocrResult.Text`؟ أحيانًا تُنتج PNG منخفض الجودة سلسلة فارغة، ومن الأفضل إبلاغ المستخدم بدلاً من عدم إظهار أي شيء صامتًا.

## الخطوة 5: إخراج النص المُعرَّف

أخيرًا، اطبع السلسلة المستخرجة إلى الـ console. يمكنك أيضًا كتابتها إلى ملف، قاعدة بيانات، أو تمريرها إلى خدمة أخرى.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

عند تشغيل البرنامج (`dotnet run`)، يجب أن ترى شيئًا مشابهًا لـ:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

هذا هو **الحل الكامل لاستخراج النص من ملفات PNG** باستخدام Aspose OCR، وقد تعلمت الآن كيف **تقرأ النص من ملفات الصور** التي تشبه الإيصالات.

## اختياري: تحسين محرك OCR (متقدم)

إذا احتجت إلى دقة أعلى لخطوط معينة أو خلفيات صاخبة، ففكّر في تعديل الإعدادات التالية:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

هذه التعديلات مفيدة خصوصًا عندما **تُعالج OCR للإيصالات** في وظائف دفعات حيث تكون بعض المسحات غير مثالية.

## الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | السبب | الحل |
|-------|----------------|-----|
| **غياب برنامج تشغيل GPU** | يحاول المحرك تحميل CUDA لكنه لا يجد الـ DLL. | ثبّت أحدث برنامج تشغيل NVIDIA أو انتقل إلى وضع CPU بإزالة سطر `EngineMode.Gpu`. |
| **مسار الصورة غير صحيح** | `ImageStream.FromFile` يرمي استثناء إذا لم يُعثر على الملف. | تحقق دائمًا من صحة المسار (انظر الخطوة 3) أو استخدم `Path.Combine` للسلامة عبر الأنظمة. |
| **ثقة منخفضة على الإيصالات الضبابية** | لا يستطيع محرك OCR تمييز الأحرف. | فعّل `EnableImagePreprocessing` وزد DPI الصورة قبل تمريرها للمحرك. |
| **تسرب الذاكرة في الخدمات طويلة التشغيل** | كل `OcrEngine` يحتفظ بموارد غير مُدارة. | حرّر المحرك بعد الاستخدام: `using var ocrEngine = new OcrEngine();` |

## مثال كامل جاهز (انسخه‑الصقه)

فيما يلي **البرنامج بالكامل** يمكنك وضعه في `Program.cs`. يتضمن جميع التعديلات الاختيارية مُعَلَّقَة لتفعيلها بسهولة.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

احفظ الملف، شغّـل `dotnet run`، وسترى محتوى الإيصال يُطبع على الـ console.

![مثال استخراج النص من png](receipt.png "مثال استخراج النص من png")

*الصورة أعلاه تُظهر إيصال PNG نموذجي يمكن للشفرة معالجته.*

## ملخص

غطّينا كيفية **استخراج النص من ملفات PNG** باستخدام Aspose OCR، وأظهرنا كيفية **قراءة النص من ملفات الصور**، وتعمقنا في خط أنابيب **معالجة OCR للإيصالات** الكامل مع دعم تسريع GPU اختياري. بإنشاء محرك OCR بنفسك، تحصل على تحكم كامل في الإعدادات، الأداء، ومعالجة الأخطاء.

## ما الذي يمكنك استكشافه لاحقًا؟

- **المعالجة الدفعية**: كرّر العملية على مجلد من إيصالات PNG واكتب كل نتيجة إلى ملف CSV.  
- **التكامل مع Azure Functions**: حوّل هذا التطبيق console إلى نقطة نهاية serverless تقبل تحميلات الصور.  
- **دعم متعدد اللغات**: استبدل `Language.English` بـ `Language.Spanish` أو أضف قواميس مخصصة.  
- **ما بعد المعالجة**: استخدم تعبيرات regex لاستخراج حقول مثل المبلغ الإجمالي، التاريخ، أو رقم الضريبة من النص الخام.  

لا تتردد في التجربة—OCR أداة مرنة بشكل مدهش بمجرد معرفة المفاتيح الصحيحة. إذا واجهت أي صعوبات، اترك تعليقًا أدناه أو راجع مرجع Aspose OCR API لمزيد من التفاصيل.

برمجة سعيدة، واستمتع بتحويل تلك إيصالات PNG العنيدة إلى نص قابل للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}