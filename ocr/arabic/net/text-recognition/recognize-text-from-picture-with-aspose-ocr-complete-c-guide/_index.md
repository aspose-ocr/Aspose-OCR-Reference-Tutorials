---
category: general
date: 2026-03-05
description: تعلم كيفية التعرف على النص من الصورة باستخدام Aspose OCR في C#. يتضمن
  خطوات استخراج النص من ملف JPEG، تحويل الصورة إلى نص، وتحميل الصورة للتعرف الضوئي
  على الأحرف.
draft: false
keywords:
- recognize text from picture
- extract text from jpeg
- convert image to text
- load image for ocr
- recognize hindi text image
language: ar
og_description: التعرف على النص من الصورة في C# باستخدام Aspose OCR. دليل خطوة بخطوة
  لاستخراج النص من JPEG، تحويل الصورة إلى نص، وتحميل الصورة للتعرف الضوئي على الأحرف.
og_title: التعرف على النص من الصورة – دليل Aspose OCR الكامل بلغة C#
tags:
- OCR
- C#
- Aspose
title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/recognize-text-from-picture-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة – دليل كامل C# Aspose OCR

هل احتجت يومًا إلى التعرف على النص من صورة لكنك لم تعرف أي مكتبة ستقوم بالعمل الشاق فعليًا؟ لست وحدك. في العديد من التطبيقات الواقعية—مثل ماسحات الفواتير، قارئات الإيصالات، أو أدوات ترجمة اللافتات متعددة اللغات—تُعد القدرة على استخراج الأحرف من ملف JPEG أو PNG أمرًا حيويًا للغاية.  

في هذا الدليل سنوضح لك **بالضبط** كيفية التعرف على النص من صورة باستخدام Aspose OCR لـ .NET. بنهاية القراءة ستكون قادرًا على استخراج النص من ملفات JPEG، تحويل الصورة إلى نص، وحتى التعرف على صورة نصية باللغة الهندية ببضع أسطر من الشيفرة. لا إشارات غامضة، بل مثال كامل قابل للتنفيذ يمكنك نسخه ولصقه في Visual Studio الآن.

## ما ستتعلمه

- كيفية **تحميل الصورة للتعرف الضوئي على الأحرف (OCR)** باستخدام تدفق يعمل مع أي نوع ملف.  
- الفرق بين **استخراج النص من JPEG** وتحويل الصورة العام، ولماذا تتعامل المكتبة مع كليهما بسلاسة.  
- كيفية **تحويل الصورة إلى نص** في استدعاء طريقة واحد، ثم عرض النتيجة.  
- خطوات محددة لـ **التعرف على صورة نصية باللغة الهندية**—بما في ذلك تنزيل بيانات اللغة تلقائيًا.  
- المشكلات الشائعة (مكان الترخيص، تسرب الذاكرة) ونصائح احترافية توفر عليك وقت تصحيح الأخطاء.

> **المتطلبات المسبقة** – .NET 6+ (أو .NET Framework 4.7.2)، Visual Studio 2022، وملف ترخيص Aspose OCR (`Aspose.OCR.lic`). إذا لم يكن لديك ترخيص بعد، يمكنك طلب مفتاح مؤقت مجاني من موقع Aspose.

---

## الخطوة 1 – التعرف على النص من الصورة: تهيئة محرك OCR

قبل أن نتمكن من القيام بأي شيء، نحتاج إلى كائن `OcrEngine` وترخيص صالح. المحرك هو الكائن الأساسي الذي يدير تحليل الصورة، واكتشاف اللغة، واستخراج النص.

```csharp
using Aspose.OCR;          // Core OCR namespace
using System;              // For Console
using Aspose.OCR.Models;   // For language enums

// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Apply your license – replace the path with the actual location of Aspose.OCR.lic
ocrEngine.SetLicense("Aspose.OCR.lic");

// Optional: Verify that the license was applied (helps during debugging)
if (ocrEngine.IsLicensed)
    Console.WriteLine("License applied successfully.");
else
    Console.WriteLine("Warning: Running in evaluation mode.");
```

**لماذا هذا مهم:** بدون ترخيص صحيح يعود المحرك إلى نسخة تجريبية مدتها 30 يومًا تُضيف علامة مائية على المخرجات وتحد من الدقة. تطبيق الترخيص مسبقًا يُجنبك أيضًا عقوبة أداء صامتة لاحقًا.

---

## الخطوة 2 – تحميل الصورة للتعرف الضوئي على الأحرف (استخراج النص من JPEG أو PNG)

الآن نحتاج إلى تزويد المحرك بصورة. يعمل Aspose OCR مع التدفقات، مما يعني أنه يمكنك تحميل ملف من القرص، أو استجابة شبكة، أو حتى صورة bitmap في الذاكرة. إليك أبسط حالة—قراءة ملف JPEG من مجلد المشروع الخاص بك.

```csharp
// Path to the picture you want to process
string imagePath = @"YOUR_DIRECTORY\hindi_sample.jpg";

// Open a stream that the OCR engine can consume
using (var imageStream = ImageStream.FromFile(imagePath))
{
    // Assign the stream to the engine
    ocrEngine.Image = imageStream;

    Console.WriteLine($"Loaded image: {imagePath}");
    // The using block ensures the stream is disposed automatically.
}
```

> **نصيحة:** إذا كنت تخطط لمعالجة العديد من الصور في حلقة، حافظ على بقاء كائن `OcrEngine` حيًا واستبدل فقط `ocrEngine.Image` في كل تكرار. هذا يعيد استخدام المخازن الداخلية ويسرّع معالجة الدفعات.

---

## الخطوة 3 – اختيار اللغة الهندية (التعرف على صورة نصية باللغة الهندية)

يدعم Aspose OCR أكثر من 130 لغة، وسيقوم بتنزيل حزمة اللغة المطلوبة في المرة الأولى التي تطلبها فيها. بما أن مثالنا يحتوي على نص ديڤاناجاري، نضبط اللغة إلى الهندية.

```csharp
// Tell the engine which language to look for
ocrEngine.Language = OcrLanguage.Hindi;   // Supports 130+ languages

Console.WriteLine("Language set to Hindi. If the data isn’t cached, it will be downloaded now.");
```

**ماذا يحدث خلف الكواليس؟** تتحقق المكتبة من مجلد التخزين المؤقت المحلي (`%AppData%\Aspose\OCR\`) للعثور على نموذج اللغة الهندية. إذا لم يكن موجودًا، يتم جلب ملف صغير (~5 ميغابايت) من شبكة توزيع المحتوى (CDN) الخاصة بـ Aspose. عملية التنزيل شفافة—لا تحتاج إلى أي شيفرة إضافية.

---

## الخطوة 4 – تنفيذ التحويل: تحويل الصورة إلى نص

مع جاهزية المحرك وتحميل الصورة، عملية OCR الفعلية هي استدعاء طريقة واحدة. يحتوي كائن النتيجة على النص العادي، درجات الثقة، وحتى إحداثيات الصناديق المحيطة إذا احتجت إليها.

```csharp
// Run the recognition process
OcrResult ocrResult = ocrEngine.Recognize();

// The Text property holds the plain string
string extractedText = ocrResult.Text;

// Show the output in the console
Console.WriteLine("\n--- Recognized Text ---");
Console.WriteLine(extractedText);
Console.WriteLine("--- End of Output ---\n");
```

**الناتج المتوقع** (بافتراض أن الصورة النموذجية تحتوي على العبارة “नमस्ते दुनिया”):

```
--- Recognized Text ---
नमस्ते दुनिया
--- End of Output ---
```

إذا كانت الصورة JPEG مختلفة، سترى الأحرف التي استطاع المحرك فك شفرتها. كما يُظهر `OcrResult` قيمة `Confidence` (0‑100) لكل سطر إذا كنت بحاجة إلى تصفية الجودة.

---

## الخطوة 5 – استخراج النص من JPEG ومعالجة الحالات الخاصة

يجب على حل جاهز للإنتاج أن يتوقع المشكلات الشائعة:

| الموقف | كيفية التعامل معه |
|-----------|------------------|
| **ملف تالف أو غير مدعوم** | غلف `Recognize()` داخل `try/catch` وسجّل `OcrException`. |
| **صورة منخفضة الدقة** | قم بالمعالجة المسبقة باستخدام `ImageProcessor` لزيادة DPI (مثال: `ocrEngine.Image = ImageProcessor.IncreaseResolution(ocrEngine.Image, 300);`). |
| **لغات متعددة في صورة واحدة** | اضبط `ocrEngine.Language = OcrLanguage.Multilingual;` ويمكنك اختيارياً توفير قائمة أولوية للغات. |
| **دفعة كبيرة** | أعد استخدام نفس كائن `OcrEngine`، واستبدل فقط `ocrEngine.Image` في كل حلقة. حرّر المحرك بعد انتهاء الدفعة. |

إليك غلاف دفاعي سريع يمكنك إضافته إلى مشروعك:

```csharp
static string RecognizePicture(string filePath, OcrLanguage lang = OcrLanguage.Hindi)
{
    try
    {
        using var stream = ImageStream.FromFile(filePath);
        OcrEngine engine = new OcrEngine();
        engine.SetLicense("Aspose.OCR.lic");
        engine.Language = lang;
        engine.Image = stream;

        var result = engine.Recognize();
        return result.Text;
    }
    catch (OcrException ex)
    {
        Console.Error.WriteLine($"OCR failed: {ex.Message}");
        return string.Empty;
    }
}
```

استدعِه هكذا:

```csharp
string text = RecognizePicture(@"YOUR_DIRECTORY\hindi_sample.jpg");
Console.WriteLine(text);
```

الآن لديك طريقة **قابلة لإعادة الاستخدام** تقوم **باستخراج النص من JPEG**، **تحويل الصورة إلى نص**، وتتعامل بأناقة مع الأخطاء.

---

## إضافي: تصور نتيجة OCR (اختياري)

إذا كنت فضوليًا حول موقع كل حرف على الصورة، يمكنك رسم صناديق محيطة باستخدام `System.Drawing`. هذا ليس مطلوبًا لاستخراج النص الأساسي، لكنه طريقة رائعة للتحقق من أن المحرك يقرأ المنطقة الصحيحة.

```csharp
using System.Drawing; // Add System.Drawing.Common NuGet for .NET Core

// After recognition...
Bitmap bmp = new Bitmap(imagePath);
using (Graphics g = Graphics.FromImage(bmp))
{
    Pen pen = new Pen(Color.Red, 2);
    foreach (var line in ocrResult.Lines)
    {
        g.DrawRectangle(pen, line.Bounds);
    }
}

// Save a copy with overlays
bmp.Save("hindi_sample_annotated.png");
Console.WriteLine("Annotated image saved as hindi_sample_annotated.png");
```

ستظهر صورة PNG الناتجة مستطيلات حمراء حول كل سطر مكتشف—مثالية لتصحيح مستندات متعددة الأسطر.

---

## الخلاصة

أصبح لديك الآن وصفة كاملة من البداية إلى النهاية لـ **التعرف على النص من الصورة** باستخدام Aspose OCR في C#. لقد غطينا كل شيء من تحميل الصورة (حتى تتمكن من **تحميل الصورة للتعرف الضوئي على الأحرف**) إلى اختيار اللغة الهندية كلغة هدف (وبالتالي **التعرف على صورة نصية باللغة الهندية**)، وتنفيذ عملية **تحويل الصورة إلى نص** الفعلية، وأخيرًا **استخراج النص من JPEG** مع معالجة أخطاء قوية.

> **الخطوات التالية** – جرّب استبدال `OcrLanguage.Hindi` بـ `OcrLanguage.Multilingual` للتعامل مع المستندات متعددة النصوص، أو دمج الطريقة في واجهة برمجة تطبيقات ASP.NET Core بحيث يمكن للمستخدمين رفع الصور مباشرة. يمكنك أيضًا استكشاف بيانات `OcrResult` الوصفية لإنشاء ملفات PDF قابلة للبحث أو إمداد النص إلى خدمة ترجمة.

إذا واجهت أي شذوذ، اترك تعليقًا أدناه أو تحقق من منتديات Aspose OCR. برمجة سعيدة، ولتكون صورك دائمًا واضحة كالكريستال!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}