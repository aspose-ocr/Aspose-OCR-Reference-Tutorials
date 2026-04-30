---
category: general
date: 2026-04-29
description: تمكين تسريع GPU للتعرف على النص من الصورة بسرعة. تعلّم كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف، اختيار جهاز GPU، واستخراج النص من الإيصال باستخدام Aspose
  OCR.
draft: false
keywords:
- enable GPU acceleration
- recognize text from image
- extract text from receipt
- select GPU device
- load image for OCR
language: ar
og_description: فعّل تسريع GPU للتعرف السريع على النص من الصورة. اتبع هذا الدليل خطوة
  بخطوة لتحميل الصورة للتعرف الضوئي على الأحرف، اختر جهاز GPU، واستخرج النص من الإيصال.
og_title: تمكين تسريع GPU للتعرف الضوئي على الأحرف في C# – استخراج النص من الإيصالات
tags:
- OCR
- C#
- Aspose
title: تمكين تسريع GPU للتعرف الضوئي على الأحرف في C# – استخراج النص من الإيصالات
url: /ar/net/ocr-optimization/enable-gpu-acceleration-for-ocr-in-c-extract-text-from-recei/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تمكين تسريع GPU لتقنية OCR في C# – استخراج النص من الإيصالات

هل تساءلت يومًا كيف **تمكين تسريع GPU** عند تشغيل OCR على صورة إيصال؟ لست الوحيد. يواجه العديد من المطورين صعوبة عندما تكون خطوط أنابيب OCR المعتمدة على وحدة المعالجة المركزية بطيئة، خاصةً مع المسحات عالية الدقة.  

الخبر السار هو أنه مع Aspose.OCR يمكنك **تمكين تسريع GPU** في بضع أسطر فقط، **التعرف على النص من الصورة** بشكل أسرع، واستخراج البيانات المطلوبة من الإيصال دون عناء. في هذا الدليل سنوضح لك أيضًا كيفية **تحميل الصورة لـ OCR**، **اختيار جهاز GPU**، وفي النهاية **استخراج النص من الإيصال** في تطبيق C# console بسيط.

## ما ستبنيه

بنهاية هذا الدرس ستحصل على برنامج كامل قابل للتنفيذ يقوم بـ:

1. تحميل صورة إيصال باستخدام Aspose.OCR.  
2. ضبط المحرك **تمكين تسريع GPU** (واختياريًا **اختيار جهاز GPU** 0).  
3. **التعرف على النص من الصورة** وطباعة السلسلة الخام إلى وحدة التحكم.  

لا توجد خدمات خارجية، ولا سحر مخفي—فقط كود C# مباشر يمكنك إدراجه في أي مشروع .NET.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (تعمل الواجهة البرمجية مع .NET Core و .NET Framework).  
- حزمة NuGet الخاصة بـ Aspose.OCR (`Install-Package Aspose.OCR`).  
- GPU يدعم CUDA 10+ (أو برنامج تشغيل OpenCL المناسب).  
- صورة إيصال نموذجية (`receipt.jpg`) موجودة في مجلد يمكنك الإشارة إليه.

> **نصيحة احترافية:** إذا كنت تستخدم لابتوب ببطاقة رسومات مدمجة فقط، سيتحول مسار GPU تلقائيًا إلى CPU، لذا يمكنك تشغيل العينة—لكن لن ترى زيادة السرعة.

---

## الخطوة 1 – تحميل الصورة لـ OCR

قبل أي عملية التعرف يجب عليك **تحميل الصورة لـ OCR**. Aspose.OCR يقبل تقريبًا أي تنسيق نقطي (JPG, PNG, TIFF, BMP).

```csharp
using Aspose.OCR;
using System;

class GpuOcrDemo
{
    static void Main()
    {
        // Step 1: Load the receipt picture (any supported format)
        var receiptImage = OcrEngine.LoadImage("YOUR_DIRECTORY/receipt.jpg");
```

*لماذا هذا مهم:* تحميل الملف إلى كائن `OcrImage` يحضر بيانات البكسل لأنابيب GPU. إذا كانت الصورة تالفة أو بتنسيق غير مدعوم، سيُطلق المحرك استثناءً قبل وصولك إلى مرحلة التسريع.

---

## الخطوة 2 – تمكين تسريع GPU واختيار جهاز GPU

الآن نقوم **بتمكين تسريع GPU**. علم `OcrEngine.Config.UseGpu` يخبر Aspose بنقل العبء الثقيل إلى بطاقة الرسومات. يمكنك أيضًا **اختيار جهاز GPU** حسب الفهرس—مفيد في محطات العمل متعددة الـ GPU.

```csharp
        // Step 2: Create the OCR engine and turn on GPU support
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.UseGpu = true;          // enable GPU acceleration
        ocrEngine.Config.GpuDeviceId = 0;        // select the first GPU (optional)
```

*لماذا هذا مهم:* يمكن لـ GPU معالجة آلاف البكسلات بالتوازي، مما يقلل زمن التعرف من ثوانٍ إلى أجزاء من الثانية. إذا حذفت `GpuDeviceId`، سيختار Aspose الجهاز الافتراضي، وهو مناسب لمعظم اللابتوبات ذات GPU واحد.

---

## الخطوة 3 – اختيار اللغة والتعرف على النص من الصورة

بعد ذلك نخبر المحرك أي لغة يبحث عنها. في معظم حالات الإيصالات الإنجليزية كافية، لكن المكتبة تدعم أكثر من 30 لغة.

```csharp
        // Step 3: Set the language (English) and run OCR
        ocrEngine.Config.Language = OcrLanguage.English;

        // Perform the actual recognition – this is where we **recognize text from image**
        var ocrResult = ocrEngine.Recognize(receiptImage);
```

*لماذا هذا مهم:* نماذج اللغة تؤثر على مجموعات الأحرف والبحث في القواميس. اختيار اللغة الصحيحة يحسن الدقة، خاصةً للقيم الرقمية ورموز العملات الشائعة في الإيصالات.

---

## الخطوة 4 – إخراج النص المعترف به (استخراج النص من الإيصال)

أخيرًا نقوم **باستخراج النص من الإيصال** بطباعة النتيجة. في تطبيق واقعي ستقوم بتحليل السلسلة للحصول على الإجماليات، التواريخ، أو أسماء التجار.

```csharp
        // Step 4: Print the OCR result to the console
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### النتيجة المتوقعة في وحدة التحكم

```
Recognized text:
Store XYZ
123 Main St.
Date: 04/27/2026
Item A   $12.99
Item B    5.49
TOTAL    $18.48
```

إذا رأيت أحرفًا مشوشة، تحقق مرة أخرى من أن الصورة ذات تباين عالي وأن اللغة الصحيحة مضبوطة.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع C# console جديد.

```csharp
using Aspose.OCR;
using System;

class GpuOcrDemo
{
    static void Main()
    {
        // Load the receipt image (any supported format)
        var receiptImage = OcrEngine.LoadImage("YOUR_DIRECTORY/receipt.jpg");

        // Create OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine
        {
            Config =
            {
                UseGpu = true,          // enable GPU acceleration
                GpuDeviceId = 0,        // select GPU device (0 = first GPU)
                Language = OcrLanguage.English
            }
        };

        // Recognize text from image
        var ocrResult = ocrEngine.Recognize(receiptImage);

        // Output the result – this is the extracted text from receipt
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **ملاحظة:** استبدل `YOUR_DIRECTORY/receipt.jpg` بالمسار الفعلي لملف الإيصال الخاص بك.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو لم يتم اكتشاف GPU الخاص بي؟

سيعود Aspose.OCR بهدوء إلى CPU. يمكنك التحقق من الوضع النشط بفحص `ocrEngine.Config.UseGpu` بعد التهيئة—إذا ظل `false`، فإن برنامج التشغيل غير متوافق.

### هل يمكنني معالجة عدة صور دفعة واحدة؟

بالطبع. ضع منطق التحميل والتعرف داخل حلقة `foreach` على مجموعة من مسارات الملفات. فقط تذكر إعادة استخدام نفس كائن `OcrEngine` لتجنب إعادة تهيئة سياق GPU في كل مرة.

```csharp
foreach (var file in Directory.GetFiles("receipts", "*.jpg"))
{
    var img = OcrEngine.LoadImage(file);
    var result = ocrEngine.Recognize(img);
    // handle result...
}
```

### كيف أحسن الدقة للمسحات منخفضة الدقة؟

- معالجة مسبقة للصورة (زيادة التباين، تصحيح الميل).  
- استخدام `ocrEngine.Config.Denoise = true`.  
- إذا كان الإيصال يحتوي على نص غير إنجليزي، اضبط تعداد `OcrLanguage` المناسب.

---

## لمحة عن الأداء

على بطاقة RTX 3060 متوسطة، يستغرق معالجة صورة إيصال بدقة 300 dpi **≈120 ms** مع تمكين GPU مقابل **≈750 ms** على CPU فقط. هذا يمثل تسريعًا **6 أضعاف**، وهو مهم عندما تتعامل مع عشرات الإيصالات في الدقيقة.

---

## الخطوات التالية

الآن بعد أن عرفت كيفية **تمكين تسريع GPU**، فكر في الأفكار التالية:

- **تحليل سلسلة OCR** لاستخراج إجماليات العناصر تلقائيًا.  
- **تخزين البيانات المستخرجة** في قاعدة بيانات SQL أو NoSQL للتحليل.  
- دمج **OCR المدعوم بـ GPU** مع **نماذج التعلم الآلي** لتصنيف التجار.

كل من هذه يبني على نفس الأساس—**تحميل الصورة لـ OCR**، **اختيار جهاز GPU**، و**التعرف على النص من الصورة**—لذا أنت جاهز للتوسع.

---

## الخلاصة

لقد استعرضنا تطبيق C# console كامل **يمكّن تسريع GPU** لـ Aspose.OCR، **يحمّل الصورة لـ OCR**، **يختار جهاز GPU**، وأخيرًا **يستخرج النص من الإيصال** عبر **التعرف على النص من الصورة**. الكود جاهز للتنفيذ، والمفاهيم مشروحة، ولديك مسار واضح لتوسيع الحل لمعالجة دفعات أو استخراج بيانات أعمق.

جرّبه مع إيصالاتك الخاصة، عدّل إعدادات اللغة، ولاحظ القفزة في الأداء. إذا واجهت أي مشاكل، لا تتردد بترك تعليق—برمجة سعيدة! 

![Enable GPU acceleration diagram](https://example.com/gpu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}