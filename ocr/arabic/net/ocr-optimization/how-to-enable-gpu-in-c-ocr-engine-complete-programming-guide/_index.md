---
category: general
date: 2026-06-06
description: كيفية تمكين وحدة معالجة الرسومات (GPU) في محرك OCR بلغة C# والتعرف بسرعة
  على النص من الصورة. تعلم كيفية إجراء OCR، تحميل الصورة للـ OCR، واستخدام محرك OCR
  بلغة C# في دقائق.
draft: false
keywords:
- how to enable gpu
- how to perform ocr
- recognize text from image
- load image for ocr
- use ocr engine c#
language: ar
og_description: كيفية تمكين وحدة معالجة الرسومات (GPU) في محرك OCR بلغة C#. يوضح هذا
  الدليل كيفية إجراء OCR، تحميل الصورة لـ OCR، والتعرف على النص من الصورة باستخدام
  محرك OCR بلغة C#.
og_title: كيفية تمكين وحدة معالجة الرسومات (GPU) في محرك OCR بلغة C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to enable GPU in a C# OCR engine and quickly recognize text from
    image. Learn how to perform OCR, load image for OCR, and use OCR engine C# in
    minutes.
  headline: How to Enable GPU in C# OCR Engine – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- C#
- GPU
title: كيفية تمكين وحدة معالجة الرسومات في محرك OCR بلغة C# – دليل برمجي شامل
url: /ar/net/ocr-optimization/how-to-enable-gpu-in-c-ocr-engine-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين وحدة معالجة الرسومات (GPU) في محرك OCR بلغة C# – دليل برمجي كامل

هل تساءلت يومًا **عن كيفية تمكين GPU** عندما تقوم بتشغيل عبء عمل OCR في C#؟ لست وحدك—المطورون يواجهون باستمرار بطء المعالجة على الـ CPU فقط، خاصةً مع المسحات عالية الدقة.  

الخبر السار؟ تشغيل تسريع GPU سهل للغاية، ومتى ما تم تشغيله يمكنك **إجراء OCR**، **تحميل صورة للـ OCR**، و**التعرف على النص من الصورة** في لحظات. في هذا الدليل سنستعرض كل خطوة، من تثبيت الحزم المناسبة إلى طباعة النص النهائي، مع الحفاظ على شفرة نظيفة وقابلة للتنفيذ.

سنناقش أيضًا بعض السيناريوهات “ماذا لو”: ماذا لو كان لديك عدة وحدات GPU؟ ماذا لو كان تنسيق الصورة غير مدعوم؟ بنهاية الدليل ستحصل على مقتطف جاهز للإنتاج يوضح بالضبط **كيفية تمكين GPU** والحصول على نتائج يمكنك الاعتماد عليها.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (العينة تستخدم عبارات المستوى الأعلى للتبسيط)
- مكتبة OCR تدعم GPU (مثال: *MyOcrLib* – استبدلها بمساحة الاسم الخاصة بموردك)
- وحدة GPU متوافقة مع CUDA مع تثبيت التعريفات
- صورة تجريبية (JPEG/PNG) موجودة في مجلد يمكنك الإشارة إليه

إذا كان أي من هذه غير متوفر، احصل على أحدث تعريف NVIDIA وأضف حزمة NuGet:

```bash
dotnet add package MyOcrLib --version 2.3.1
```

الآن، لنبدأ.

## الخطوة 1: كيفية تمكين GPU في محرك OCR بلغة C#

أول شيء تحتاجه هو تشغيل مفتاح GPU في كائن تكوين المحرك. معظم SDKs الحديثة للـ OCR تعرض خاصية `Config` حيث يمكنك تعيين `GpuEnabled`، `GpuDeviceId`، وربما وضع الدقة لزيادة السرعة.

```csharp
// Create the OCR engine instance
var ocrEngine = new MyOcrLib.OcrEngine();

// Enable GPU acceleration
ocrEngine.Config.GpuEnabled = true;                     // Turn on GPU mode
ocrEngine.Config.GpuDeviceId = 0;                       // Choose the first GPU (0‑based index)
ocrEngine.Config.GpuPrecision = GpuPrecision.Float16; // Optional: lower precision for less memory usage
```

**لماذا هذا مهم:** تسريع GPU ينقل حسابات المصفوفات الثقيلة من الـ CPU، مما يسمح لمعالج الرسومات بمعالجة آلاف البكسلات بالتوازي. على بطاقة RTX 3060 متوسطة يمكنك ملاحظة زيادة سرعة 3‑5× مقارنةً بوضع CPU فقط.

> **نصيحة احترافية:** إذا كان لديك أكثر من وحدة GPU، جرّب `GpuDeviceId = 1` (أو أعلى) لتوزيع الحمل بين البطاقات.

## الخطوة 2: تحميل صورة للـ OCR في C#

قبل أن يتمكن المحرك من القراءة، عليك تزويده بتدفق صورة. عادةً ما يوفر SDK مساعدًا مثل `ImageStream.FromFile`. تأكد من صحة المسار وإمكانية الوصول إلى الملف.

```csharp
// Load the image you want to process
ocrEngine.Image = MyOcrLib.ImageStream.FromFile(@"C:\OCRSamples\sample1.jpg");

// Quick sanity check – ensure the image was loaded
if (ocrEngine.Image == null)
{
    Console.WriteLine("Failed to load image. Check the file path and format.");
    return;
}
```

**حالة حافة:** بعض المكتبات تتعطل مع صور JPEG بنظام ألوان CMYK. إذا واجهت استثناءً، حوّل الصورة إلى RGB أولًا باستخدام `System.Drawing` أو `ImageSharp`.

## الخطوة 3: تعيين اللغة وإجراء OCR

معظم محركات OCR تحتاج إلى معرفة نموذج اللغة الذي سيُستخدم. الإنجليزية هي الافتراضية في العديد من الحزم، لكن يمكنك التبديل إلى الفرنسية أو الإسبانية وغيرها بتغيير قيمة enum واحدة.

```csharp
// Choose the language for recognition
ocrEngine.Language = OcrLanguage.English; // Change to OcrLanguage.Spanish for Spanish text
```

الآن نقوم بتشغيل خط أنابيب التعرف. هذه هي اللحظة التي يتحول فيها **كيفية إجراء OCR** إلى استدعاء ملموس.

```csharp
// Run the OCR process – this will automatically use the GPU because we enabled it earlier
var ocrResult = ocrEngine.Recognize();
```

إذا أعاد الاستدعاء `null` أو رمى استثناءً، تحقق مرة أخرى من أن تعريفات GPU محدثة وأن ملفات النموذج موجودة في الدليل المتوقع.

## الخطوة 4: التعرف على النص من الصورة وإخراج النتيجة

طريقة `Recognize` تُعيد كائنًا يحتوي عادةً على خاصية `Text`، بالإضافة إلى درجات الثقة لكل سطر. لنطبع النص الصافي إلى وحدة التحكم.

```csharp
// Output the recognized text
if (ocrResult?.Text != null)
{
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
else
{
    Console.WriteLine("OCR failed to produce any text.");
}
```

**ما ستراه:** بالنسبة لصفحة ممسوحة بوضوح، يجب أن يكون الإخراج شبه مثالي. إذا لاحظت أحرفًا مشوشة، فكر في زيادة DPI الصورة (300 dpi هو القيمة المثالية) أو عُد إلى `GpuPrecision` بـ `Float32` للحصول على دقة أعلى.

### ناتج وحدة التحكم المتوقع (عينة)

```
=== OCR Output ===
The quick brown fox jumps over the lazy dog.
```

## الخطوة 5: المشكلات الشائعة وتعديلات الأداء

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| **GPU غير مُستخدم** (ارتفاع استهلاك CPU) | ترك `GpuEnabled` على `false` أو عدم وجود تعريف | تحقق من أن `ocrEngine.Config.GpuEnabled` يساوي `true` وشغّل `nvidia-smi` لرؤية العملية |
| **خطأ نفاد الذاكرة** | استخدام `Float16` على صورة كبيرة جدًا | انتقل إلى `GpuPrecision.Float32` أو قلل أبعاد الصورة قبل تمريرها |
| **دقة منخفضة** | نموذج لغة خاطئ أو DPI منخفض | عيّن `ocrEngine.Language` بشكل صحيح وتأكد من أن DPI الصورة ≥300 |
| **تعطل عند ملفات PDF متعددة الصفحات** | المحرك يتوقع صورة واحدة | كرّر العملية لكل صفحة، وأنشئ `ImageStream` جديد لكل تكرار |

**نصيحة إضافية:** غلف استدعاء OCR داخل `Task.Run` إذا كنت بحاجة لإبقاء الواجهة مستجيبة. عمل الـ GPU يتم على خيط منفصل، لكن مجموعة خيوط .NET لا تزال محجوزة ما لم تُفرغها.

```csharp
var ocrResult = await Task.Run(() => ocrEngine.Recognize());
```

## الخطوة 6: مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي برنامج مستقل يمكنك وضعه في تطبيق Console. يتضمن توجيهات `using`، معالجة الأخطاء، و`Console.ReadKey()` نهائيًا لتتمكن من رؤية النتيجة قبل إغلاق النافذة.

```csharp
using System;
using MyOcrLib;               // Replace with the actual namespace of your OCR library
using MyOcrLib.Enums;        // For GpuPrecision and OcrLanguage

// ------------------------------------------------------------
// How to Enable GPU, Load Image, Perform OCR, and Get Text
// ------------------------------------------------------------
var ocrEngine = new OcrEngine();

// 1️⃣ Enable GPU acceleration
ocrEngine.Config.GpuEnabled = true;
ocrEngine.Config.GpuDeviceId = 0;                 // First GPU
ocrEngine.Config.GpuPrecision = GpuPrecision.Float16;

// 2️⃣ Load the image for OCR
string imagePath = @"C:\OCRSamples\sample1.jpg";
ocrEngine.Image = ImageStream.FromFile(imagePath);

if (ocrEngine.Image == null)
{
    Console.WriteLine("❌ Unable to load image. Check the path.");
    return;
}

// 3️⃣ Set language (how to perform OCR)
ocrEngine.Language = OcrLanguage.English;

// 4️⃣ Run OCR – this uses the GPU because we enabled it
var ocrResult = ocrEngine.Recognize();

if (ocrResult?.Text != null)
{
    Console.WriteLine("\n=== Recognized Text ===");
    Console.WriteLine(ocrResult.Text);
}
else
{
    Console.WriteLine("\n⚠️ OCR returned no text.");
}

// Keep console open
Console.WriteLine("\nPress any key to exit...");
Console.ReadKey();
```

شغّل البرنامج باستخدام `dotnet run` وسترى النص المستخرج يُطبع في وحدة التحكم. إذا غيرت `imagePath` إلى ملف آخر، سيعمل نفس الخط الأنابيب—فقط تذكّر تعديل اللغة إذا لزم الأمر.

## الخاتمة

غطّينا **كيفية تمكين GPU** في محرك OCR بلغة C#، وأظهرنا لك **كيفية تحميل صورة للـ OCR**، وشرحنا **كيفية إجراء OCR**، وأظهرنا أبسط طريقة **للتعرف على النص من الصورة** باستخدام واجهة برمجة `OCR engine C#`. المثال الكامل في النهاية يجمع كل شيء، بحيث يمكنك النسخ، اللصق، ومشاهدة تسارع الـ GPU لاستخراج النص فورًا.

هل أنت مستعد للخطوة التالية؟ جرّب معالجة دفعة من الصور عبر حلقة `Parallel.ForEach`، أو جرب إعدادات `GpuPrecision` مختلفة، أو انتقل إلى نموذج متعدد اللغات لتوسيع قدرات تطبيقك.  

إذا واجهت أي صعوبات أو لديك أفكار للتحسين، اترك تعليقًا—برمجة سعيدة!  

![how to enable gpu in OCR engine](/images/ocr-gpu-setup.png "Diagram showing GPU‑enabled OCR pipeline – how to enable gpu")

---


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}