---
category: general
date: 2026-02-14
description: حمّل ملف الصورة واستخرج النص من الإيصال باستخدام محرك Aspose OCR للمعالجة
  على وحدة معالجة الرسوميات. تعلّم كيفية ضبط الحد الأقصى لذاكرة وحدة معالجة الرسوميات،
  وتكوين الذاكرة، وتشغيل OCR على الصورة بكفاءة.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: ar
og_description: حمّل ملف الصورة واستخرج النص من الإيصال باستخدام محرك Aspose OCR GPU.
  يوضح هذا الدليل كيفية تعيين الحد الأقصى لذاكرة GPU وتشغيل OCR على الصورة في C#.
og_title: تحميل ملف الصورة واستخراج نص الإيصال باستخدام OCR على وحدة معالجة الرسومات
  في C#
tags:
- C#
- OCR
- Aspose
- GPU
title: تحميل ملف الصورة واستخراج نص الإيصال باستخدام OCR على وحدة معالجة الرسومات
  في C#
url: /ar/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحميل ملف الصورة واستخراج نص الإيصال باستخدام OCR على وحدة معالجة الرسومات (GPU) في C#

هل احتجت يوماً إلى **تحميل ملف الصورة** واستخراج النص الدقيق من إيصال ولكن شعرت بأنك عالق في خطوة الـ OCR؟ لست وحدك. في العديد من التطبيقات الواقعية—متتبعات النفقات، أنظمة الجرد، أو حتى الروبوتات البسيطة التي تمسح الإيصالات—يمكن أن تكون القدرة على قراءة صورة الإيصال بسرعة عاملاً مغيراً للعبة.  

الأخبار السارة؟ باستخدام محرك Aspose.OCR المسرّع بالـ GPU يمكنك **تحميل ملف الصورة**، **تحديد الحد الأقصى لذاكرة الـ GPU**، و**تشغيل OCR على الصورة** كل ذلك في بضع أسطر أنيقة من C#. أدناه سنستعرض العملية بالكامل، من ضبط الـ GPU إلى طباعة النص المستخرج.

## ما ستتعلمه

في هذا الدرس ستكتشف كيفية:

* **تحميل ملف الصورة** من القرص باستخدام `ImageStream` الخاص بـ Aspose.
* **تكوين ذاكرة الـ GPU** بحيث لا يستهلك المحرك أكثر من الذاكرة التي تسمح بها.
* **تشغيل OCR على الصورة** واستخراج كل حرف في الإيصال.
* التعامل مع المشكلات الشائعة—مثل أخطاء نفاد الذاكرة أو الصور الضبابية.
* التحقق من النتيجة وضبط الإعدادات للحصول على دقة أفضل.

لا خدمات خارجية، لا حيل غامضة—فقط كود C# نقي يمكنك إدراجه في أي مشروع .NET 6+.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود التالي:

* .NET 6 SDK أو أحدث مثبت.
* ترخيص صالح لـ Aspose.OCR (أو يمكنك استخدام وضع التقييم المجاني).
* حزم NuGet `Aspose.OCR` و `Aspose.OCR.Gpu` مضافة إلى مشروعك.
* صورة إيصال تجريبية (`receipt.png`) جاهزة على القرص.

إذا كان أي من ذلك غير مألوف لك، توقف لحظة وقم بتثبيت الحزم:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

هذا كل شيء—لا تحتاج إلى مكتبات أصلية إضافية لأن دعم الـ GPU مدمج مباشرة في حزمة NuGet.

---

## تحميل ملف الصورة وإعداد محرك الـ GPU

أول شيء يجب القيام به هو **تحميل ملف الصورة** إلى كائن `ImageStream`. هذا الكائن يخفّف تفاصيل نظام الملفات ويعطي محرك OCR تمثيلاً نظيفاً في الذاكرة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**لماذا هذا مهم:**  
*تحميل ملف الصورة* عبر `ImageStream.FromFile` يضمن أن المحرك يرى بيانات البكسل الدقيقة، مع الحفاظ على DPI وعمق اللون. تخطي هذه الخطوة أو تمرير تدفق تالف سيؤدي إلى فقدان الأحرف أو رمي استثناءات.

> **نصيحة محترف:** إذا كنت تتعامل مع ملفات يرفعها المستخدمون، احط استدعاء `FromFile` بكتلة `try‑catch` وتحقق من حجم الملف أولاً. الصور الكبيرة قد تستهلك ذاكرة الـ GPU إذا لم تقم **بتكوين ذاكرة الـ GPU** بشكل صحيح.

---

## تحديد الحد الأقصى لذاكرة الـ GPU لأداء مثالي

موارد الـ GPU ثمينة، خاصةً على الخوادم المشتركة أو الحواسيب المحمولة ذات الذاكرة المحدودة. خاصية `MaxDeviceMemory` تخبر Aspose بكمية الذاكرة التي يمكنه تخصيصها بأمان على الـ GPU.

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

عند **تحديد الحد الأقصى لذاكرة الـ GPU**، سيعود المحرك تلقائياً إلى المعالجة على الـ CPU إذا لم يتمكن من تلبية الطلب—مما يمنع حدوث تعطل. هذه هي الطريقة الأكثر أماناً **لتكوين ذاكرة الـ GPU** دون كتابة حدود ثابتة خاصة بجهاز معين.

**متى يجب تعديل الإعداد:**  
* إذا لاحظت `OutOfMemoryException` أثناء معالجة دفعات كبيرة، قلل الحد.  
* إذا كانت إيصالاتك عالية الدقة (300 DPI+)، زد الحد إلى 2 GB للحفاظ على السرعة.

---

## تشغيل OCR على الصورة لاستخراج نص الإيصال

الجزء الممتع الآن—**تشغيل OCR على الصورة** واستخراج نص الإيصال. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على خاصية `Text` التي تحمل النص الصافي.

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

ستظهر وحدة التحكم شيئاً مشابهًا لـ:

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**لماذا هذا يعمل:**  
محرك الـ GPU يشغّل نموذج تعلم عميق تم تدريبه على مجموعة متنوعة من تخطيطات المستندات. من خلال تزويده بصورة نظيفة ومحمّلة بشكل صحيح، تمنح النموذج أفضل فرصة **لاستخراج النص من الإيصال** بدقة.

---

## التحقق من النتيجة والمشكلات الشائعة

حتى مع محرك قوي، OCR ليس سحراً. إليك بعض الأمور التي يجب الانتباه إليها:

| المشكلة | السبب | الحل |
|-------|-------|-----|
| أحرف مشوشة | انخفاض التباين أو صورة ضبابية | **معالجة مسبقة** باستخدام `ImageProcessor` من Aspose لزيادة التباين |
| سطور مفقودة | قص الصورة بشكل ضيق جدًا | تأكد من أن الإيصال يملأ كامل حدود الصورة |
| أخطاء نفاد الذاكرة | `MaxDeviceMemory` منخفض جدًا بالنسبة لحجم الصورة | زد `MaxDeviceMemory` أو قلل أبعاد الصورة أولاً |
| لغة غير صحيحة | الإيصال يحتوي على نص غير إنجليزي | اضبط `gpuEngine.Language = OcrLanguage.Spanish;` (أو اللغة المناسبة) |

إذا واجهت أيًا من هذه المشكلات، فإن الحل السريع هو تغيير حجم الصورة لتكون أقل من 2000 بكسل على الجانب الأطول—هذا يقلل ضغط الـ GPU بشكل كبير دون التضحية بقراءة معظم الإيصالات.

---

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي البرنامج الكامل، جاهز للترجمة. استبدل مسار الملف بموقع إيصالك الخاص.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**الناتج المتوقع في وحدة التحكم** (سيختلف حسب إيصالك بالطبع):

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

شغّل البرنامج باستخدام `dotnet run`. إذا رأيت النص مطبوعًا، تهانينا—لقد نجحت في **تحميل ملف الصورة**، **تحديد الحد الأقصى لذاكرة الـ GPU**، و**تشغيل OCR على الصورة** لاستخراج **نص الإيصال**.

---

## الأسئلة المتكررة

**س: هل يعمل هذا على أجهزة لا تحتوي على GPU مخصص؟**  
ج: نعم. سيعود Aspose.OCR تلقائيًا إلى وضع الـ CPU إذا لم يتم اكتشاف GPU متوافق. لا يزال بإمكانك **تحميل ملف الصورة** و**تشغيل OCR على الصورة**، لكن السرعة ستكون أبطأ قليلاً.

**س: هل يمكنني معالجة عدة إيصالات دفعة واحدة؟**  
ج: بالتأكيد. ضع كود التعرف داخل حلقة `foreach`، لكن تذكر إعادة استخدام نفس كائن `GpuEngine`—هذا يتجنب إعادة تهيئة موارد الـ GPU لكل ملف.

**س: ماذا لو كان إيصالى بلغة غير الإنجليزية؟**  
ج: اضبط اللغة قبل استدعاء `Recognize`:

```csharp
gpuEngine.Language = OcrLanguage.French;
```

سيتعامل المحرك بعد ذلك مع مجموعة الأحرف المناسبة.

---

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن أتقنت الأساسيات، فكر في استكشاف:

* **تحسين دقة OCR** – جرّب `gpuEngine.RecognitionOptions` مثل `EnableDeskew` أو `ContrastEnhancement`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}