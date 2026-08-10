---
category: general
date: 2026-02-13
description: تعلم كيفية استخدام OCR في C# لاستخراج النص من ملفات الصور، وتمكين معالجة
  GPU، وتحويل المسحات الضوئية إلى نص بسرعة.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: ar
og_description: كيف تستخدم OCR في C#؟ يوضح لك هذا الدليل كيفية استخراج النص من ملفات
  الصور، وتمكين معالجة GPU، وتحويل المسحات الضوئية إلى نص.
og_title: كيفية استخدام OCR في C# – استخراج النص من الصور باستخدام وحدة معالجة الرسومات
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: كيفية استخدام OCR في C# – استخراج النص من الصور باستخدام وحدة معالجة الرسومات
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – استخراج النص من الصور باستخدام GPU

هل تساءلت يومًا **كيفية استخدام OCR** لاستخراج النص من مستند ممسوح ضوئيًا دون عناء؟ لست وحدك—المطورون يسألون باستمرار: “كيف يمكنني استخراج النص من ملفات الصور بكفاءة؟” الخبر السار هو أنه باستخدام Aspose.OCR يمكنك فعل ذلك بالضبط، ويمكنك أيضًا **تمكين معالجة GPU** للحصول على تسريع ملحوظ على الأجهزة المدعومة.

في هذا البرنامج التعليمي سنستعرض مثالًا كاملًا من البداية إلى النهاية يوضح لك **كيفية استخدام OCR**، وكيفية **استخراج النص من الصورة**، وكيفية **تحويل الماسح الضوئي إلى نص**، وماذا تفعل إذا لم يكن GPU متاحًا. في النهاية ستحصل على تطبيق كونسول C# جاهز للتشغيل يطبع النص المعترف به ويخبرك ما إذا تم استخدام GPU فعليًا.

## ما ستحتاجه

- .NET 6 SDK أو أحدث (الكود يعمل مع .NET Core أيضًا)  
- Visual Studio 2022 أو أي محرر تفضله  
- حزمة Aspose.OCR لـ .NET (متاحة عبر NuGet)  
- ملف صورة عالية الدقة (مثال: `highres_scan.tif`) للاختبار  

لا حاجة لإعدادات معقدة—فقط بضع أوامر NuGet وستكون جاهزًا.

## الخطوة 1: تثبيت Aspose.OCR وتحضير المشروع

أولاً وقبل كل شيء. عليك إضافة مكتبة OCR إلى مشروعك. افتح طرفية في مجلد الحل الخاص بك وشغّل:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

هذا ينشئ مشروع كونسول جديد باسم **OcrDemo** ويضيف حزمة NuGet `Aspose.OCR`. المكتبة تحتوي على الفئة `OcrEngine` التي سنستخدمها.

> **نصيحة احترافية:** إذا كنت تستخدم جهازًا يحتوي على GPU مخصص، تأكد من تثبيت أحدث برنامج تشغيل للرسومات؛ وإلا ستعود المكتبة تلقائيًا إلى وضع CPU.

## الخطوة 2: كتابة كود OCR الكامل

الآن افتح `Program.cs` واستبدل محتواه بما يلي. كل سطر مُعلّق لتتمكن من رؤية *سبب* ما نقوم به.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### لماذا يعمل هذا

- **ProcessingMode = Gpu** يُخبر المحرك بمحاولة استخدام GPU أولاً. المكتبة تُجرد استدعاءات CUDA/OpenCL منخفضة المستوى، لذا لا تحتاج إلى إدارة سياقات الجهاز بنفسك.  
- **IsGpuEnabled** هو قيمة منطقية تؤكد ما إذا كان مسار GPU قد نجح. إذا رأيت `false`، فإن المحرك سيتراجع تلقائيًا إلى CPU—لا داعي للذعر.  
- **RecognizeImage** يقوم بكل العمل الشاق: يحمل الصورة، يشغّل نموذج OCR، ويعيد النتيجة كنص عادي. لا حاجة لمعالجة البت ماب يدويًا إلا إذا كان لديك متطلبات خاصة (مثل تصحيح الميل).

## الخطوة 3: تشغيل التطبيق والتحقق من المخرجات

قم بالترجمة والتنفيذ:

```bash
dotnet run
```

إذا تم إعداد كل شيء بشكل صحيح، سترى شيئًا مثل:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

إذا لم يكن GPU متاحًا، سيظهر السطر الأول كـ `GPU used: False`، لكن النص المستخرج سيظهر ما زال—بفضل التراجع السلس.

> **سؤال شائع:** *ماذا لو كانت صورتي JPEG بدلاً من TIFF؟*  
> طريقة `RecognizeImage` تقبل أي تنسيق يدعمه .NET عبر `System.Drawing` (JPEG، PNG، BMP، إلخ). فقط غيّر امتداد الملف في `imagePath`.

## الخطوة 4: اختياري – تعديل الإعدادات للحصول على دقة أفضل

تقدم Aspose.OCR بعض الخيارات التي يمكنك تعديلها:

| الإعداد | ما يفعله | متى يستخدم |
|---------|----------|------------|
| `ocrEngine.Language` | يفرض لغة محددة (مثال: `OcrLanguage.English`) | إذا كنت تعرف لغة المستند |
| `ocrEngine.PageSegMode` | يتحكم في طريقة تقسيم المحرك للصفحات إلى كتل | لتصاميم متعددة الأعمدة |
| `ocrEngine.DetectOrientation` | يدور النص تلقائيًا إذا لم يكن موجهًا بشكل صحيح | مسحات قد تكون مقلوبة |

يمكنك ضبط هذه الخصائص قبل استدعاء `RecognizeImage`. على سبيل المثال:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## الخطوة 5: تصور التدفق (صورة مع نص بديل)

فيما يلي مخطط بسيط يوضح **كيفية استخدام OCR** مع تسريع GPU اختياري. ليس ضروريًا لتشغيل الكود، لكنه يساعدك على رؤية الصورة الكبيرة.

![مخطط يوضح كيفية استخدام OCR مع معالجة GPU](/images/ocr-gpu-flow.png)

*نص بديل:* *مخطط يوضح كيفية استخدام OCR مع معالجة GPU، مع إبراز التراجع إلى CPU عند الحاجة.*

## الحالات الخاصة & استكشاف الأخطاء وإصلاحها

1. **نفاد الذاكرة على GPU** – قد تتجاوز الصور الكبيرة جدًا سعة ذاكرة GPU. في هذه الحالة، ستعود المكتبة تلقائيًا إلى CPU. يمكنك تصغير حجم الصورة مسبقًا للحفاظ على استهلاك الذاكرة منخفضًا.  
2. **تنسيق صورة غير مدعوم** – إذا أطلقت `RecognizeImage` استثناء *NotSupportedException*، تحقق من امتداد الملف وتأكد من أن الصورة غير تالفة. التحويل إلى PNG غالبًا ما يحل المشكلة.  
3. **درجات ثقة منخفضة** – عندما يحتوي ناتج OCR على العديد من الأحرف غير القابلة للقراءة، فكر في المعالجة المسبقة (تحويل إلى ثنائي، إزالة الضوضاء) أو التحويل إلى مسح بدقة أعلى.  

## الخلاصة: ما أنجزناه

لقد غطينا للتو **كيفية استخدام OCR** في تطبيق كونسول C#، وأظهرنا كيفية **استخراج النص من ملفات الصورة**، وأوضحنا لك كيفية **تمكين معالجة GPU** للحصول على نتائج أسرع. الآن تعرف كيف **تحول الماسح الضوئي إلى نص**، وتتحقق مما إذا تم استخدام GPU فعليًا، وتضبط بعض الإعدادات لحالات الحافة.

### الخطوات التالية

- جرّب إدخال الناتج في **فهرس بحث** (مثال: Elasticsearch) حتى تصبح ملفات PDF الممسوحة قابلة للبحث.  
- جرب **المعالجة الدفعية**—التكرار على مجلد من الصور وكتابة كل نتيجة إلى ملف `.txt`.  
- دمج OCR مع **واجهات برمجة تطبيقات الترجمة** لترجمة المستندات الممسوحة بلغات أجنبية تلقائيًا.  

هل لديك المزيد من الأسئلة؟ اترك تعليقًا، وتمنياتنا لك بالبرمجة السعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}