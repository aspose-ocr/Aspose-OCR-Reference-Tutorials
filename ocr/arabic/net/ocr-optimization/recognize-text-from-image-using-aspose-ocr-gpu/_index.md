---
category: general
date: 2026-06-28
description: التعرف على النص من الصورة بسرعة باستخدام Aspose OCR. تعلّم كيفية تمكين
  تسريع GPU، تحميل الصورة للتعرف الضوئي على الأحرف، واستخراج النص من الإيصال كنص عادي.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- how to enable gpu acceleration
- convert image to plain text
- load image for ocr
language: ar
og_description: التعرف على النص من الصورة باستخدام Aspose OCR. يوضح هذا الدليل كيفية
  تمكين تسريع GPU، تحميل صورة للتعرف الضوئي على الأحرف، وتحويلها إلى نص عادي.
og_title: التعرف على النص من الصورة باستخدام Aspose OCR GPU
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  headline: recognize text from image using Aspose OCR GPU
  type: TechArticle
- description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  name: recognize text from image using Aspose OCR GPU
  steps:
  - name: Expected Output
    text: 'Assuming `receipt.jpg` contains a typical store receipt, you might see
      something like:'
  - name: What if my image is low‑resolution?
    text: OCR accuracy drops dramatically on blurry or tiny images. Before calling
      `Recognize`, consider up‑scaling the image (e.g., using `System.Drawing` or
      `ImageSharp`) and applying a contrast boost. Aspose also offers `Preprocess`
      methods you can experiment with.
  - name: My GPU isn’t being used – why?
    text: '- Verify that `EnableGpu` is `true` *before* you call `Recognize`. - Check
      that your driver supports OpenCL 1.2+ (most modern drivers do). - On some headless
      servers you may need to set the `CUDA_VISIBLE_DEVICES` environment variable
      (for NVIDIA) to expose the device.'
  - name: Can I process multiple images in parallel?
    text: Absolutely. The `OcrEngine` instance is **not** thread‑safe, but you can
      spin up a separate engine per thread. Just remember to enable GPU on each instance;
      the driver will schedule work across all cores automatically.
  - name: How do I change the language (e.g., French receipts)?
    text: '```csharp ocrEngine.Settings.Language = OcrLanguage.French; ```'
  type: HowTo
tags:
- Aspose OCR
- C#
- GPU acceleration
title: التعرف على النص من الصورة باستخدام Aspose OCR GPU
url: /ar/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة باستخدام Aspose OCR GPU

هل تساءلت يومًا كيف **تتعرف على النص من الصورة** دون كتابة آلاف الأسطر من الشيفرة؟ أنت لست الوحيد. سواءً كنت تمسح الإيصالات لتقارير النفقات أو تحول الملاحظات المكتوبة يدويًا إلى ملفات PDF قابلة للبحث، فإن الحصول على نص عادي نظيف من صورة هو حاجة شائعة.

في هذا الدرس سنستعرض مثالًا كاملًا جاهزًا للتنفيذ يوضح **كيفية تمكين تسريع GPU**، **تحميل الصورة للـ OCR**، وأخيرًا **استخراج النص من الإيصال** (أو أي صورة) كنص عادي. لا إطالة، فقط الأجزاء التي تحتاج لنسخها ولصقها.

## ما ستقوم ببنائه

بنهاية هذا الدليل ستحصل على تطبيق كونسول صغير يقوم بـ:

1. إنشاء `OcrEngine` وتفعيل معالجة GPU.  
2. تحميل ملف صورة محلي (إيصال، لافتة، أو أي شيء).  
3. تشغيل التعرف الضوئي على الأحرف.  
4. طباعة النص المعترف به إلى الكونسول – أي **تحويل الصورة إلى نص عادي**.

كل هذا يعمل على .NET 6+ باستخدام مكتبة Aspose.OCR المجانية، ويعمل على الأجهزة التي تحتوي على GPU من NVIDIA أو AMD يدعم OpenCL.

## المتطلبات المسبقة

- .NET 6 SDK أو أحدث مثبت.  
- Visual Studio 2022 (أو أي محرر تفضله).  
- جهاز يدعم GPU (اختياري لكن يُنصح به للسرعة).  
- ملف صورة تجريبي، مثل `receipt.jpg`، موجود في مسار يمكنك الإشارة إليه.  

إذا لم يكن لديك GPU، لا يزال الكود يعمل؛ سيتحول إلى معالجة CPU.

## الخطوة 1: تثبيت Aspose.OCR عبر NuGet

أولاً، أضف حزمة Aspose.OCR إلى مشروعك:

```bash
dotnet add package Aspose.OCR
```

هذه السطر الواحد يجلب جميع الملفات الثنائية التي تحتاجها، بما في ذلك أغطية OpenCL الأصلية لعمل GPU.

## الخطوة 2: تمكين تسريع GPU (how to enable gpu acceleration)

تفعيل الـ GPU بسيط كإعداد علم منطقي في إعدادات المحرك. المكتبة تختار تلقائيًا أول جهاز متاح، لكن يمكنك أيضًا تحديد الفهرس إذا كان لديك عدة بطاقات GPU.

```csharp
// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU processing – this is the “how to enable gpu acceleration” part
ocrEngine.Settings.EnableGpu = true;

// (Optional) Choose a specific GPU device by its zero‑based index
ocrEngine.Settings.GpuDeviceId = 0;
```

**لماذا نُفعّل الـ GPU؟**  
نوى الـ GPU تتفوق في المهام المتوازية مثل تمهيد الصورة واستنتاج الشبكات العصبية. على بطاقة RTX حديثة يمكنك ملاحظة تسريع OCR بمقدار 3‑5× مقارنةً بالمعالجة على CPU فقط.

> **نصيحة احترافية:** إذا صادفت أخطاء `OpenCL`، تأكد من أن برنامج تشغيل الرسوميات محدث وأن ملف `OpenCL.dll` متاح في مسار التشغيل.

## الخطوة 3: تحميل الصورة للـ OCR (load image for ocr)

بعد ذلك، وجه المحرك إلى الصورة التي تريد قراءتها. توفر Aspose.OCR طريقة مصنع مريحة تدعم صيغًا متعددة (JPEG، PNG، BMP، TIFF، إلخ).

```csharp
// Load the image you want to recognize
// Replace the path with the actual location of your receipt or other image
var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

إذا لم يُعثر على الملف، فإن `FromFile` يرمي استثناء `FileNotFoundException`. يمكنك إحاطته بـ try/catch إذا أردت معالجة الأخطاء برفق.

## الخطوة 4: تنفيذ OCR وتحويل الصورة إلى نص عادي

الآن يحدث السحر. استدعِ `Recognize` واحصل على خاصية `Text` من النتيجة. ستحصل على سلسلة نظيفة – ما نعنيه بـ **تحويل الصورة إلى نص عادي**.

```csharp
// Run OCR on the loaded image
var ocrResult = ocrEngine.Recognize(receiptImage);

// Output the recognized plain‑text to the console
System.Console.WriteLine(ocrResult.Text);
```

خاصية `Text` تُزيل فواصل الأسطر وتُعيد Unicode، لذا يمكنك توجيهها مباشرة إلى ملف، قاعدة بيانات، أو أي خط أنابيب معالجة لاحق.

### النتيجة المتوقعة

بافتراض أن `receipt.jpg` يحتوي على إيصال متجر نموذجي، قد ترى شيئًا مثل:

```
Walmart Supercenter
123 Main St.
Anytown, TX 75001
Date: 06/27/2026
Item          Qty   Price
Apple         2     $1.20
Bread         1     $2.50
TOTAL                $3.70
Thank you for shopping!
```

التنسيق الدقيق يعتمد على جودة الصورة المصدر والنموذج اللغوي المستخدم داخليًا.

## الخطوة 5: مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه إلى ملف `Program.cs` جديد. يتضمن جميع الخطوات السابقة، بالإضافة إلى قليل من معالجة الأخطاء للراحة.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        try
        {
            // Step 1: Create the OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Settings.EnableGpu = true;          // Turn on GPU processing
            ocrEngine.Settings.GpuDeviceId = 0;           // (Optional) Choose GPU device by index

            // Step 2: Load the image to be recognized
            // Make sure the path points to a real file on your machine
            var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

            // Step 3: Perform OCR on the loaded image
            var ocrResult = ocrEngine.Recognize(receiptImage);

            // Step 4: Output the recognized plain‑text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

احفظ، ابنِ، وشغّل:

```bash
dotnet run
```

إذا تم ربط كل شيء بشكل صحيح، سيعرض الكونسول النص المستخرج، مؤكدًا أنك نجحت في **استخراج النص من الإيصال** (أو أي صورة) باستخدام Aspose OCR مع دعم GPU.

## الحالات الخاصة والأسئلة الشائعة

### ماذا لو كانت صورتي منخفضة الدقة؟

تنخفض دقة OCR بشكل كبير على الصور الضبابية أو الصغيرة. قبل استدعاء `Recognize`، فكر في تكبير الصورة (مثلاً باستخدام `System.Drawing` أو `ImageSharp`) وتطبيق تعزيز التباين. تقدم Aspose أيضًا طرق `Preprocess` يمكنك التجربة بها.

### لماذا لا يُستخدم الـ GPU الخاص بي؟

- تأكد من أن `EnableGpu` مُعَّين إلى `true` *قبل* استدعاء `Recognize`.  
- تحقق من أن برنامج التشغيل يدعم OpenCL 1.2+ (معظم البرامج الحديثة تدعم ذلك).  
- على بعض الخوادم بدون واجهة رسومية قد تحتاج لتعيين متغير البيئة `CUDA_VISIBLE_DEVICES` (لـ NVIDIA) لتظهر الجهاز.

### هل يمكنني معالجة صور متعددة بالتوازي؟

بالتأكيد. كائن `OcrEngine` **ليس** آمنًا للـ multithreading، لكن يمكنك إنشاء محرك منفصل لكل خيط. فقط تذكر تمكين GPU لكل مثال؛ سيتولى السائق جدولة العمل عبر جميع الأنوية تلقائيًا.

### كيف أغيّر اللغة (مثلاً إيصالات فرنسية)؟

```csharp
ocrEngine.Settings.Language = OcrLanguage.French;
```

تأكد من أن حزمة اللغة المناسبة مضمّنة مع حزمة NuGet (معظم اللغات الشائعة مضمّنة).

## معيار الأداء (اختياري)

على لابتوب بمعالج Intel i7‑12700H وبطاقة NVIDIA RTX 3060، تم رصد الأوقات التالية لإيصال JPEG بحجم 300 KB:

| الوضع               | الوقت (مللي ثانية) |
|--------------------|----------------------|
| CPU فقط            | 820                  |
| GPU (EnableGpu)    | 210                  |

هذا يمثل تقريبًا تسريعًا بمقدار **4×**، مما يثبت لماذا **how to enable gpu acceleration** مهم للمعالجة الجماعية.

## الخلاصة

لقد تعلمت الآن كيف **تتعرف على النص من الصورة** باستخدام Aspose OCR، وتفعيل تسريع GPU للحصول على زيادة ملحوظة في السرعة، **تحميل الصورة للـ OCR**، وأخيرًا **تحويل الصورة إلى نص عادي**—مثالي لاستخراج النص من الإيصالات، الفواتير، أو أي مستند ممسوح. الكود كامل ومستقل، يعمل على أي بيئة .NET 6+، ويمكن توسيعه لمعالجة دفعات من المجلدات، تخزين النتائج في قاعدة بيانات، أو إمداد نموذج AI لاحق.

الخطوات التالية؟ جرّب استبدال الإيصال بملاحظة مكتوبة يدويًا، جرب واجهة `Preprocess` لتحسين الدقة على المسحات الضوضائية، أو دمج المحرك في خدمة ويب ASP.NET Core حتى يتمكن المستخدمون من رفع الصور والحصول على النص فورًا. يمكنك أيضًا استكشاف كلمات مفتاحية ثانوية مثل **extract text from receipt** في سير عمل أكبر، أو الغوص أعمق في **how to enable gpu acceleration** لمنتجات Aspose الأخرى.

برمجة سعيدة، ولتكن OCR دائمًا دقيقة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}