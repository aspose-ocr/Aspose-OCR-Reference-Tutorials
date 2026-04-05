---
category: general
date: 2026-04-04
description: كيفية تمكين وحدة معالجة الرسومات (GPU) في Aspose OCR بسرعة. تعلم استخراج
  النص من الصورة، تحميل الصورة للتعرف الضوئي على الأحرف (OCR) والتعرف على النص باستخدام
  C#.
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: ar
og_description: كيفية تمكين وحدة معالجة الرسومات (GPU) في Aspose OCR بسرعة. اتبع هذا
  البرنامج التعليمي لاستخراج النص من الصورة، وتحميل الصورة للتعرف الضوئي على الأحرف،
  والتعرف على النص باستخدام C#.
og_title: كيفية تمكين GPU للتعرف الضوئي على الأحرف (OCR) في C# – دليل كامل
tags:
- Aspose OCR
- C#
- GPU acceleration
title: كيفية تمكين وحدة معالجة الرسومات (GPU) للتعرف الضوئي على الأحرف (OCR) في C#
  – دليل خطوة بخطوة
url: /ar/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين وحدة معالجة الرسومات لـ OCR في C# – دليل شامل

هل تساءلت يومًا **كيف يتم تمكين وحدة معالجة الرسومات** عند استخدام Aspose OCR؟ ربما واجهت عائقًا في الأداء أثناء معالجة مئات الإيصالات، ولا يستطيع المعالج المركزي مواكبة السرعة. الخبر السار هو أن تشغيل تسريع GPU سهل للغاية، وبمجرد تشغيله ستلاحظ أن محرك OCR يمر عبر الصور بسرعة فائقة.

في هذا الدرس لن نكتفي فقط بتشغيل مفتاح GPU، بل سنوضح لك أيضًا **كيفية تحميل صورة لـ OCR**، **كيفية التعرف على النص**، وأخيرًا **كيفية استخراج النص من الصورة** باستخدام مثال C# نظيف. في النهاية ستحصل على برنامج جاهز للتنفيذ يستخرج النص العادي من أي صورة مدعومة—بدون الحاجة إلى خدمات خارجية.

## ما ستحتاجه

- .NET 6+ (أو .NET Framework 4.7.2 وما بعده).  
- Aspose.OCR for .NET، الإصدار 24.2.0 أو أحدث (تم إضافة علم GPU في هذا الإصدار).  
- جهاز يدعم GPU مع التعريفات المناسبة (NVIDIA CUDA 11+ يعمل بشكل ممتاز).  
- ملف صورة تريد معالجته—مثل إيصال ممسوح ضوئيًا، فاتورة مُصوَّرة، أو ملاحظة مكتوبة بخط اليد.

إذا كان لديك كل ذلك، رائع—لنبدأ.

## الخطوة 1: كيفية تمكين وحدة معالجة الرسومات – تكوين محرك OCR

أول شيء عليك فعله هو إخبار Aspose OCR باستخدام GPU. يتم ذلك عن طريق ضبط الخاصية `UseGpu` في كائن `OcrEngine`. القيمة الافتراضية للخاصية هي `false`، لذا نقوم بتفعيلها صراحةً.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**لماذا هذا مهم:** عندما تكون `UseGpu` مساوية لـ `true`، تقوم المكتبة بتحميل حسابات المصفوفات الثقيلة إلى معالج الرسومات. على بطاقة RTX 3060 متوسطة ستلاحظ انخفاض زمن الاستجابة من عدة ثوانٍ لكل صورة إلى جزء من الثانية.

> **نصيحة احترافية:** إذا كنت تعمل في بيئة CI بدون واجهة رسومية، تأكد من تثبيت تعريف GPU وأن حساب الخدمة لديه صلاحية الوصول إلى الجهاز. وإلا سيتراجع المحرك صامتًا إلى وضع CPU.

## الخطوة 2: تحميل صورة لـ OCR – توجيه المحرك إلى ملفك

الخطوة التالية هي **تحميل صورة لـ OCR**. يدعم Aspose OCR أي صيغة صورة يدعمها System.Drawing (PNG، JPEG، BMP، TIFF، إلخ). الدالة المساعدة `ImageStream.FromFile` تغلف الملف في كائن الـ stream المطلوب.

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

إذا كنت تفضّل التحميل من `byte[]` (مثلاً عندما تأتي الصورة من قاعدة بيانات)، يمكنك استخدام `ImageStream.FromBytes(byteArray)` بدلاً من ذلك—نفس النتيجة، مجرد مصدر مختلف.

## الخطوة 3: كيفية التعرف على النص – تشغيل عملية OCR

الآن بعد أن تم تكوين المحرك وتحميل الصورة، حان الوقت لـ **التعرف على النص**. تقوم طريقة `Recognize` بكل العمل الشاق وتعيد كائن `OcrResult` يحتوي على النص العادي، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها لاحقًا.

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

يمكنك أيضًا تغيير اللغة عن طريق ضبط `ocrEngine.Language = OcrLanguage.French;` قبل استدعاء `Recognize()`. يعمل تسريع GPU بغض النظر عن حزمة اللغة التي تقوم بتحميلها.

## الخطوة 4: كيفية استخراج النص من الصورة – إخراج النتيجة

أخيرًا نقوم **باستخراج النص من الصورة** بقراءة الخاصية `Text` لكائن النتيجة. لأغراض العرض سنطبعها على وحدة التحكم، لكن يمكنك كتابتها إلى ملف، قاعدة بيانات، أو تمريرها إلى خدمة أخرى.

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**الناتج المتوقع** (النص الفعلي سيختلف بناءً على الصورة):

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

إذا كنت بحاجة إلى قيم الثقة الخام يمكنك تكرار `ocrResult.Regions` وفحص كل `Region.Confidence`.

## مثال كامل يعمل – ملف واحد جاهز للتنفيذ

فيما يلي البرنامج الكامل. انسخه والصقه في مشروع Console جديد، استعد حزمة NuGet الخاصة بـ Aspose.OCR، ثم اضغط **F5**.

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **ملاحظة:** استبدل `YOUR_DIRECTORY/receipt.jpg` بالمسار الفعلي لصورتك. إذا ألقى البرنامج استثناء `FileNotFoundException`، تحقق مرة أخرى من المسار وصلاحيات الملف.

## أسئلة شائعة وحالات خاصة

### ماذا لو لم يتم اكتشاف GPU؟

سيعود Aspose OCR تلقائيًا إلى وضع CPU ويسجل تحذيرًا. للتحقق من الوضع النشط، افحص `ocrEngine.IsGpuEnabled` بعد الإنشاء—ستعيد `true` فقط عندما يتم تحميل تعريف GPU بنجاح.

### هل يمكنني معالجة عدة صور داخل حلقة؟

بالطبع. فقط انقل سطر `ocrEngine.Image = …` داخل حلقة `foreach (var file in files)`. احتفظ بنفس كائن `OcrEngine`؛ إعادة استخدامه يجنبك عبء تخصيص موارد GPU مرارًا وتكرارًا.

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### كيف أتعامل مع اللغات غير الإنجليزية؟

اضبط اللغة قبل استدعاء `Recognize()`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

يعمل تسريع GPU بنفس الطريقة؛ فقط نموذج اللغة يتغير.

### ماذا عن الصور الكبيرة وعالية الدقة؟

إذا صادفت أخطاء نفاد الذاكرة، قلل أبعاد الصورة أولًا. يوفر Aspose OCR الدالة `ImageHelper.Resize`—طريقة سريعة لتصغير الصورة دون فقدان الكثير من التفاصيل.

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## الخلاصة

لقد غطينا **كيفية تمكين وحدة معالجة الرسومات** لـ Aspose OCR، وأظهرنا لك **كيفية تحميل صورة لـ OCR**، وتعرفنا على **كيفية التعرف على النص**، وأظهرنا **كيفية استخراج النص من الصورة** باستخدام برنامج C# مختصر وجاهز للإنتاج. بتبديل علم `UseGpu` تحصل على زيادة ملحوظة في السرعة، خاصةً عند معالجة دفعات من الإيصالات، الفواتير، أو أي تدفق مستندات عالي الحجم.

هل أنت مستعد للخطوة التالية؟ جرّب ربط خط أنابيب OCR هذا بقاعدة بيانات لتخزين الإيصالات المستخرجة، أو مرّر النص العادي إلى نموذج معالجة لغة طبيعية لتصنيف المصاريف. يمكنك أيضًا استكشاف مجموعة `OcrResult.Regions` للحصول على إحداثيات إطارات الحدود وبناء واجهة مستخدم تبرز كل كلمة على الصورة الأصلية.

برمجة سعيدة، واستمتع بالقوة الإضافية التي يجلبها تسريع GPU إلى أحمال عمل OCR الخاصة بك! 

---

![كيفية تمكين وحدة معالجة الرسومات](gpu-ocr-diagram.png "كيفية تمكين وحدة معالجة الرسومات")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}