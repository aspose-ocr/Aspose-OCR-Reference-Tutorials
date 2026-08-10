---
category: general
date: 2026-03-18
description: قم بتعيين جهاز GPU في Aspose OCR لاستخراج النص من الصورة بسرعة. تعلّم
  كيفية تحميل الصورة للتعرف الضوئي على الأحرف، وتعرّف على صورة الإيصال واحصل على نتائج
  دقيقة.
draft: false
keywords:
- set GPU device
- extract text from image
- how to extract text
- load image for OCR
- recognize receipt image
language: ar
og_description: قم بتعيين جهاز GPU في Aspose OCR لاستخراج النص من الصورة بسرعة. اتبع
  هذا الدليل خطوة بخطوة لتحميل الصورة للـ OCR والتعرف على صورة الإيصال.
og_title: تعيين جهاز GPU للتعرف الضوئي على الأحرف في C# – دليل برمجي كامل
tags:
- OCR
- C#
- GPU
- Aspose
title: تعيين جهاز GPU للتعرف الضوئي على الأحرف في C# – دليل برمجي كامل
url: /ar/net/ocr-configuration/set-gpu-device-for-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين جهاز GPU لمعالجة OCR في C# – دليل برمجي كامل

هل تحتاج إلى **تعيين جهاز GPU** للحصول على معالجة OCR أسرع؟ في هذا الدليل سنرشدك خطوة بخطوة إلى كيفية تعيين جهاز GPU باستخدام Aspose OCR، ثم استخراج النص من صورة إيصال في بضع أسطر من الشيفرة فقط.  

إذا كنت قد واجهت صعوبة في **load image for OCR** أو تساءلت *كيف تستخرج النص* من مسحات عالية الدقة، فأنت في المكان المناسب. في النهاية ستحصل على برنامج قابل للتنفيذ يتعرف على صورة إيصال، يطبع النص العادي، ويتحول بسلاسة إلى CPU إذا لم يتوفر GPU.

## ما يغطيه هذا الدرس

* تثبيت حزمة Aspose OCR NuGet (الاعتماد الخارجي الوحيد).  
* تعيين جهاز GPU (`set GPU device`) واختيار فهرس GPU مختلف اختياريًا.  
* تحميل ملف صورة للـ OCR – نعم، هذا يتضمن خطوة “load image for OCR” المزعجة التي تُربك الكثير من المبتدئين.  
* تشغيل محرك التعرف لت **recognize receipt image** المحتوى.  
* استخراج السلسلة الناتجة حتى تتمكن من **extract text from image** واستخدامها في تطبيقك.  

لا سحر، لا روابط مستندات مخفية – مجرد حل كامل ومستقل يمكنك نسخه‑لصقه في Visual Studio وتشغيله اليوم.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الشيفرة تعمل على .NET Core و .NET Framework أيضًا).  
* جهاز يدعم GPU مع تثبيت التعريفات المناسبة – وإلا سيتحول المكتبة تلقائيًا إلى وضع CPU.  
* صورة إيصال نموذجية (مثال: `receipt_highres.png`) موجودة في مكان يمكنك الإشارة إليه بمسار كامل.  

هذا كل شيء. إذا كنت تفتقد حزمة NuGet، شغّل `dotnet add package Aspose.OCR` في مجلد المشروع.

---

## الخطوة 1 – تعيين جهاز GPU في Aspose OCR

أول شيء عليك فعله هو **set GPU device** على محرك OCR. هذا يخبر Aspose بتحميل الأعمال الثقيلة إلى بطاقة الرسومات بدلاً من المعالج.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // Enable GPU processing – this is where we set the GPU device
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu;

        // (Optional) Choose a specific GPU if you have more than one.
        // The default is device 0, but you can set it to 1, 2, etc.
        ocrEngine.Settings.GpuDeviceId = 0;
```

**لماذا هذا مهم:**  
عندما يعمل المحرك في `ProcessingMode.Gpu`، يمكن لنوى CUDA الأساسية تسريع تجزئة الأحرف والاستدلال عبر الشبكات العصبية بشكل كبير. على بطاقة RTX 3080 الحديثة ستلاحظ انخفاض أوقات OCR من ثوانٍ إلى أقل من ثانية للوصلات عالية الدقة.

> **نصيحة احترافية:** إذا لم تكن متأكدًا من فهرس GPU الذي يجب استخدامه، استدعِ `OcrEngine.GetAvailableGpuDevices()` (متاح في الإصدارات الأحدث) واختر الجهاز الذي يمتلك أكبر مساحة ذاكرة حرة.

---

## الخطوة 2 – Load Image for OCR

الآن بعد أن تم تكوين المحرك، نحتاج إلى **load image for OCR**. توفر Aspose غلاف `ImageStream` مريح يُجرد عمليات I/O للملفات ويدعم التدفقات من الذاكرة أو الشبكة أو القرص.

```csharp
        // Load the receipt image you want to recognize
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        var imageStream = ImageStream.FromFile(imagePath);
```

**ما الذي قد يخطئ؟**  
إذا كان مسار الملف خاطئًا أو الصورة تالفة، سيُطلق `FromFile` استثناء `FileNotFoundException`. فحص سريع `File.Exists(imagePath)` قبل إنشاء التدفق يحفظك من تعطل غير مرغوب.

---

## الخطوة 3 – Recognize Receipt Image

مع الصورة في المتناول، نستدعي `Recognize`. هذه هي الخطوة التي **recognize receipt image** المحتوى باستخدام خط الأنابيب المسرّع بـ GPU الذي أعددناه مسبقًا.

```csharp
        // Perform OCR – this returns an OcrResult object
        var ocrResult = ocrEngine.Recognize(imageStream);
```

**خلف الكواليس:**  
يقوم المحرك أولاً بتحويل الصورة إلى bitmap رمادي موحد، ثم يشغّل نموذج تعلم عميق يتنبأ باحتمالات الأحرف. لأننا على GPU، يعالج النموذج الـ bitmap بالكامل بشكل متوازي، وهذا هو السبب في إكمال الفواتير الكبيرة بسرعة.

---

## الخطوة 4 – Extract Text from Image and Verify Output

أخيرًا، نستخرج النتيجة النصية العادية من `OcrResult` ونكتبها إلى وحدة التحكم. هذه هي اللحظة التي **extract text from image** فيها ويمكنك تمريرها إلى منطق لاحق (مثال: تحليل بنود الفاتورة).

```csharp
        // Output the recognized plain text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

**الناتج المتوقع:**  

```
=== OCR Result ===
Store Name
Date: 03/15/2026
Item A   $12.99
Item B   $5.49
Total    $18.48
==================
```

إذا كان النص مشوشًا، تحقق مرة أخرى من أن الصورة عالية الدقة وأن برنامج تشغيل GPU محدث. يمكنك أيضًا تبديل `ocrEngine.Settings.PreprocessMode` لتحسين التباين للوصلات ذات الإضاءة الضعيفة.

---

## الخطوة 5 – Fallback to CPU (Edge Case Handling)

ماذا لو لم يكن الجهاز المستهدف يحتوي على GPU متوافق؟ بدلاً من التعطل، يمكنك اكتشاف الحالة والتحول إلى معالجة CPU.

```csharp
        // Detect GPU availability – fallback if needed
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, falling back to CPU mode.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }
```

**لماذا نضيف هذا؟**  
في خطوط CI أو حاويات السحابة غالبًا ما تُشغل على خوادم بدون واجهة رسومية ولا GPU. يضمن الانحدار السلس أن الشيفرة نفسها تعمل في أي مكان.

---

## المشكلات الشائعة والنصائح العملية

| المشكلة | كيفية التجنب |
|---------|--------------|
| نسيان تعيين `ProcessingMode` قبل تحميل الصورة. | دائمًا قم بتهيئة المحرك أولًا (الخطوة 1). |
| استخدام فهرس GPU غير صحيح (`GpuDeviceId`). | استعلم عن الأجهزة المتاحة أو التزم بالافتراضي `0`. |
| تحميل صورة منخفضة الدقة، مما يقلل من دقة OCR. | استهدف على الأقل 300 DPI للإيصالات. |
| عدم تحرير `ImageStream` – يؤدي إلى قفل الملفات. | غلف الـ stream بكتلة `using` أو استدعِ `Dispose()` يدويًا. |
| تجاهل علم `IsGpuAvailable` على الأجهزة بدون CUDA. | أضف منطق الفallback من الخطوة 5. |

---

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي البرنامج بالكامل، جاهز للترجمة. احفظه باسم `Program.cs`، أضف حزمة Aspose OCR NuGet، وشغّله.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // ---------- Step 1: Set GPU device ----------
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu; // set GPU device
        ocrEngine.Settings.GpuDeviceId = 0; // use the first GPU (change if needed)

        // Optional: fallback if GPU isn't present
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, switching to CPU.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }

        // ---------- Step 2: Load image for OCR ----------
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }
        var imageStream = ImageStream.FromFile(imagePath);

        // ---------- Step 3: Recognize receipt image ----------
        var ocrResult = ocrEngine.Recognize(imageStream);

        // ---------- Step 4: Extract text from image ----------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

تشغيل البرنامج يطبع نص الإيصال المستخرج إلى وحدة التحكم، تمامًا كما هو موضح سابقًا. الآن يمكنك تمرير تلك السلسلة إلى محلل، قاعدة بيانات، أو أي منطق أعمال آخر تحتاجه.

---

## الخلاصة

أظهرنا لك كيف **set GPU device** في Aspose OCR، **load image for OCR**، و **recognize receipt image** حتى تتمكن من **extract text from image** بسرعة فائقة. المثال الكامل القابل للتنفيذ يوضح كلًا من “كيف” و“لماذا”، مما يمنحك أساسًا صلبًا لأي مشروع OCR بـ C# يحتاج تسريع GPU.

هل أنت مستعد للخطوة التالية؟ جرّب التجربة مع:

* معالجة صور متعددة بالتوازي باستخدام `Parallel.ForEach`.  
* تعديل `ocrEngine.Settings.PreprocessMode` لتحسين النتائج على المسحات منخفضة التباين.  
* تصدير مخرجات OCR إلى JSON للتحليلات اللاحقة.  

لا تتردد في ترك تعليق إذا واجهت أي صعوبات، ونتمنى لك برمجة سعيدة!

![مخطط يوضح كيفية تعيين جهاز GPU لمعالجة OCR](set-gpu-device.png "تعيين جهاز GPU")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}