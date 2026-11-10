---
category: general
date: 2026-02-16
description: قم بتشغيل OCR على ملفات PNG بسرعة باستخدام Aspose OCR في C#. تعلّم كيفية
  استخراج النص، قراءة نص PNG، والتعرف على نص PNG من خلال دليل خطوة بخطوة.
draft: false
keywords:
- run OCR on PNG
- how to extract text
- read text png
- recognize text png
- ocr tutorial c#
language: ar
og_description: تشغيل OCR على PNG باستخدام Aspose OCR في C#. يوضح لك هذا الدرس كيفية
  استخراج النص، قراءة نص PNG، والتعرف على نص PNG خطوة بخطوة.
og_title: تشغيل OCR على PNG في C# – دليل كامل
tags:
- OCR
- C#
- Aspose
- Image Processing
title: تشغيل OCR على PNG في C# – دليل كامل مع Aspose
url: /ar/net/text-recognition/run-ocr-on-png-in-c-complete-guide-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على PNG في C# – دليل كامل مع Aspose

هل احتجت يومًا إلى **run OCR on PNG** للملفات لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—المطورون يسألون باستمرار *how to extract text* من لقطات الشاشة عالية الدقة، الفواتير، أو المخططات الممسوحة. في هذا الدرس سنستعرض حلًا عمليًا من البداية إلى النهاية يتيح لك **run OCR on PNG** باستخدام مكتبة Aspose.OCR، كل ذلك بلغة C# العادية.

سنغطي كل شيء من تثبيت حزمة NuGet إلى تمكين تسريع GPU، تحميل نموذج اللغة الإنجليزية، وأخيرًا طباعة السلسلة المعترف بها إلى وحدة التحكم. في النهاية ستعرف بالضبط **how to extract text** من أي PNG، وكيفية **read text PNG** بفعالية، وستحصل على مقتطف **OCR tutorial C#** قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع.

## ما ستتعلمه

- تثبيت وتكوين Aspose.OCR لـ .NET.
- تمكين تسريع الأجهزة لتسريع المعالجة.
- تحميل نماذج اللغة وإدخال صورة PNG إلى المحرك.
- التقاط وعرض الناتج، مع معالجة المشكلات الشائعة.
- توسيع المثال إلى لغات أو صيغ صور أخرى.

**المتطلبات المسبقة:** .NET 6 أو أحدث، Visual Studio 2022 (أو بيئتك المتكاملة المفضلة)، ومعالج رسومي متوافق إذا كنت تريد التسريع الاختياري. لا حاجة لخبرة سابقة في OCR.

---

## تشغيل OCR على PNG – إعداد البيئة

قبل أن نغوص في الشيفرة، دعنا نتأكد من أن بيئة التطوير جاهزة. هذه الخطوة حاسمة؛ فقدان حزمة أو عدم توافق وقت التشغيل سيتسبب في فشل الدرس بأكمله.

1. **Create a new console project**  
   ```bash
   dotnet new console -n OcrPngDemo
   cd OcrPngDemo
   ```

2. **Add the Aspose.OCR NuGet package**  
   ```bash
   dotnet add package Aspose.OCR
   ```

3. **(Optional) Verify GPU support** – إذا كان لديك معالج رسومي NVIDIA أو AMD يدعم CUDA/OpenCL، قم بتثبيت التعريفات المناسبة. المكتبة ستكتشف العتاد تلقائيًا عندما تقوم بتعيين `HardwareAcceleration.Gpu`.

هذا كل شيء. مشروع جديد مع مكتبة OCR الآن جاهز لـ **run OCR on PNG**.

## كيفية استخراج النص – تهيئة محرك OCR

السطر الأول الحقيقي من الشيفرة ينشئ مثيلًا من `OcrEngine`. فكر في المحرك كالعقل وراء العملية؛ فهو يحتفظ بالإعدادات، نماذج اللغة، وإعدادات العتاد.

```csharp
using Aspose.OCR;

// Step 1: Initialize the OCR engine (default CPU mode)
OcrEngine ocrEngine = new OcrEngine();
```

لماذا نقوم بإنشائه يدويًا بدلاً من استخدام مساعد ثابت؟  
لأن ذلك يمنحنا تحكمًا كاملاً في **how to extract text**—يمكننا تبديل GPU، تغيير اللغة، أو استبدال مصدر الصورة في الوقت الفعلي. في التطبيقات الكبيرة قد تحتفظ بمحرك singleton لتجنب إعادة تحميل النماذج بشكل متكرر.

## قراءة نص PNG مع تسريع GPU

إذا كنت تعالج لقطات شاشة عالية الدقة، قد يكون OCR على المعالج فقط بطيئًا. تمكين تسريع GPU يقلل الثواني من كل تشغيل.

```csharp
// Step 2: Enable GPU acceleration for faster processing (requires compatible GPU)
ocrEngine.HardwareAcceleration = HardwareAcceleration.Gpu;
```

*نصيحة احترافية:* إذا كان جهازك يفتقر إلى GPU متوافق، فإن السطر أعلاه سيتحول بسلاسة إلى وضع CPU. لا يتم إلقاء استثناء، لذا يمكنك إبقاء الشيفرة دون تغيير عبر البيئات.

## تحميل نموذج اللغة – مثال “English”

Aspose يأتي مع نموذج إنجليزي جاهز، لكن يمكنك تحميل نماذج أخرى (French، German، إلخ) باستدعاء واحد. تحميل النموذج هو شرط مسبق لـ **recognize text PNG**؛ بدون ذلك لن يعرف المحرك مجموعة الأحرف المتوقعة.

```csharp
// Step 3: Load the language model you need (English is included by default)
ocrEngine.LoadLanguage(LanguageModel.English);
```

إذا احتجت يومًا إلى **read text PNG** بلغة أخرى، استبدل `LanguageModel.English` بالقيمة المناسبة من الـ enum.

## توفير الصورة – من ملف إلى تدفق

الآن نمرر ملف PNG إلى المحرك. المساعد `ImageStream.FromFile` يقرأ الملف إلى الذاكرة ويدعم صيغًا متعددة، لكن PNG هو ما نركز عليه.

```csharp
// Step 4: Provide the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/high_res_image.png");
```

تأكد من أن المسار يشير إلى PNG حقيقي؛ وإلا ستحصل على `FileNotFoundException`. للاختبار السريع، ضع لقطة شاشة لفاتورة مطبوعة في المجلد وأشر إليها هنا.

## التعرف على نص PNG – تشغيل عملية OCR

مع كل شيء موصول، استدعاء OCR الفعلي هو طريقة واحدة. الطريقة تُرجع سلسلة تحتوي على جميع الأحرف المستخرجة، مع الحفاظ على فواصل الأسطر حيثما أمكن.

```csharp
// Step 5: Run the OCR operation and capture the recognized text
string recognizedText = ocrEngine.Recognize();
```

لماذا تعمل هذه الاستدعاءة الواحدة؟  
خلف الكواليس، يقوم المحرك بسلسلة من المراحل: المعالجة المسبقة (إزالة الضوضاء، التثنائي)، التجزئة (تقسيم إلى أسطر وحروف)، وأخيرًا التصنيف باستخدام نموذج deep‑learning. كل هذه الخطوات الثقيلة مخفية عنك، وهذا ما يجعل الـ API يبدو خفيفًا.

## عرض النتيجة – التحقق من المخرجات

أخيرًا، نطبع النتيجة إلى وحدة التحكم. في تطبيق حقيقي قد تكتب إلى قاعدة بيانات، تغذي فهرس بحث، أو تمرر السلسلة إلى خدمة أخرى.

```csharp
// Step 6: Display the OCR result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

عند تشغيل البرنامج يجب أن ترى شيئًا مثل:

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

إذا كان الإخراج مشوشًا، تحقق مرة أخرى من جودة الصورة (التباين، الاتجاه) وفكر في تمكين `ocrEngine.PreprocessOptions` لمزيد من التعديلات.

## مثال كامل لتعليم OCR C# – مثال عملي كامل

فيما يلي الشيفرة **complete, runnable** التي تجمع كل الأجزاء معًا. انسخ‑الصقها في `Program.cs`، استبدل مسار الصورة، واضغط **F5**.

```csharp
using System;
using Aspose.OCR;

namespace OcrPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize the OCR engine (CPU by default)
            OcrEngine ocrEngine = new OcrEngine();

            // Enable GPU acceleration if a compatible GPU is present
            ocrEngine.HardwareAcceleration = HardwareAcceleration.Gpu;

            // Load the English language model (default)
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Specify the PNG image to process
            string imagePath = "YOUR_DIRECTORY/high_res_image.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR and retrieve the recognized text
            string recognizedText = ocrEngine.Recognize();

            // Output the result to the console
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**Expected output:** وحدة التحكم تطبع الأحرف الدقيقة الموجودة في PNG، مع الحفاظ على فواصل الأسطر. إذا كانت الصورة تحتوي على أرقام فقط، سترى سلسلة من الأرقام؛ إذا كانت تحتوي على لغات مختلطة، ستحصل على الأحرف Unicode المناسبة.

> **Note:** البرنامج أعلاه يعمل مع أي PNG أو JPEG أو BMP طالما أن مسار الملف صحيح. لـ **read text PNG** من تدفق (مثلاً من واجهة ويب API)، استبدل `ImageStream.FromFile` بـ `ImageStream.FromBytes(byteArray)`.

---

## أسئلة شائعة وحالات حافة

### ماذا لو كان PNG مائلًا؟

Aspose.OCR يمكنه تدوير الصور تلقائيًا. أضف:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath);
ocrEngine.ImageOrientation = ImageOrientation.AutoDetect;
```

### كيف أتعامل مع دفعات كبيرة؟

ضع المحرك داخل كتلة `using` وأعد استخدامه عبر الملفات:

```csharp
using (var engine = new OcrEngine())
{
    engine.LoadLanguage(LanguageModel.English);
    foreach (var file in Directory.GetFiles(folder, "*.png"))
    {
        engine.Image = ImageStream.FromFile(file);
        string text = engine.Recognize();
        // Process text...
    }
}
```

### هل يمكنني استخراج النص من صورة منخفضة التباين؟

فعّل المعالجة المسبقة:

```csharp
ocrEngine.PreprocessOptions = PreprocessOptions.EnhanceContrast | PreprocessOptions.Denoise;
```

### هل هناك طريقة للحصول على درجات الثقة؟

نعم—`ocrEngine.RecognizeWithDetails()` تُرجع مجموعة من كائنات `OcrResult`، كل منها يحتوي على خاصية `Confidence`.

## مثال بصري

<img src="https://example.com/ocr-output.png" alt="مثال تشغيل OCR على PNG يوضح النص المستخرج من الفاتورة">

*نص alt يتضمن الكلمة المفتاحية الأساسية، لتلبية متطلبات SEO.*

## الخلاصة

أنت الآن تمتلك سير عمل ثابتًا لـ **run OCR on PNG** يعمل مباشرةً مع Aspose.OCR. باتباع هذا **OCR tutorial C#**، يمكنك **how to extract text**، **read text PNG**، و**recognize text PNG** في بضع أسطر من الشيفرة فقط. دعم GPU للمحرك، تحميل اللغات، وواجهة API البسيطة تجعل منه الحل المثالي لأي مطور .NET يحتاج إلى تحويل الصور إلى نص قابل للبحث.

ما التالي؟ جرّب استبدال `LanguageModel.English` بلغة أخرى، جرب `PreprocessOptions` للصور الضوضائية، أو دمج النتيجة في فهرس بحث نص كامل. الاحتمالات لا حصر لها، والشيفرة التي كتبتها الآن هي أساس قابل لإعادة الاستخدام لكل هذه المغامرات.

إذا واجهت أي مشاكل، اترك تعليقًا أدناه أو راجع وثائق Aspose للحصول على خيارات تكوين أعمق. برمجة سعيدة، واستمتع بتحويل تلك PNG العنيدة إلى نص قابل للتحرير!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}