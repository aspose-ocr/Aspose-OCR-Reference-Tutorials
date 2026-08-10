---
category: general
date: 2026-06-06
description: التعرف على النص في الصورة باستخدام C# OCR – مثال خطوة بخطوة لـ OCR باستخدام
  C# يستخراج النص من المسحات الضوئية ويحوّل المسح إلى نص في دقائق.
draft: false
keywords:
- recognize text image
- c# ocr example
- extract text scan
- convert scan to text
- image to text c#
language: ar
og_description: التعرف على نص الصورة باستخدام C# OCR. تعلم مثال عملي لـ C# OCR يستخراج
  النص من المسح الضوئي، يحول المسح إلى نص، ويتعامل مع الصور الواقعية.
og_title: التعرف على صورة النص في C# – دليل OCR كامل
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text image using C# OCR – a step‑by‑step c# ocr example that
    extracts text from scans and convert scan to text in minutes.
  headline: recognize text image in C# – Full OCR Guide
  type: TechArticle
- questions:
  - answer: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d
      swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize`
      method, so the surrounding code stays virtually unchanged.
    question: Does this work on .NET Core on Linux?
  - answer: Handwriting recognition is still experimental. For best results, stick
      to printed fonts or consider a cloud service like Azure Cognitive Services if
      you need high accuracy.
    question: How accurate is the built‑in OCR for handwritten notes?
  - answer: 'Not out of the box. Convert each PDF page to an image first (using `PdfSharp`
      or `Ghostscript`) and then feed the bitmap to the OCR engine. --- ## Conclusion
      You now have a complete, production‑ready **c# ocr example** that can **recognize
      text image** files, **extract text scan** contents, and **co'
    question: Can I process PDFs directly?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: التعرف على صورة النص في C# – دليل OCR الكامل
url: /ar/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص في الصورة باستخدام C# – دليل OCR كامل

هل تساءلت يومًا كيف **تتعرف على نص الصورة** مباشرةً من صورة ممسوحة ضوئيًا باستخدام C#؟ لست وحدك. سواءً كنت تقوم برقمنة إيصالات قديمة، أو استخراج بيانات من بطاقة عمل، أو مجرد تحويل مسح منخفض الدقة إلى نص قابل للتحرير، فإن القدرة على استخراج النص من صورة هي حيلة مفيدة يجب أن يمتلكها كل مطور في صندوق أدواته.

في هذا الدليل سنستعرض **مثال c# ocr** يقوم بتحميل صورة، تشغيل التعرف الضوئي على الأحرف، وطباعة النتيجة إلى وحدة التحكم. بنهاية الدليل ستتمكن من **استخراج نص من مسح**، **تحويل المسح إلى نص**، وحتى تعديل العملية للصور ذات الضوضاء. لا تحتاج إلى خدمات طرف ثالث باهظة—فقط API المدمج Windows.Media.Ocr (أو أي OcrEngine متوافق) وعدد قليل من أسطر الكود.

## ما ستتعلمه

* كيفية إعداد مشروع C# لتقنية OCR.
* الكود الدقيق المطلوب **لتعرف على نص الصورة**.
* نصائح للتعامل مع المسحات منخفضة الدقة والوثائق متعددة الصفحات.
* طرق لتوسيع المثال إلى مكتبة قابلة لإعادة الاستخدام لتطبيقاتك.

### المتطلبات المسبقة

* .NET 6.0 أو أحدث (API يعمل أيضًا على .NET 5+).
* Visual Studio 2022 (الإصدار المجتمعي يكفي) أو أي بيئة تطوير تفضلها.
* صورة نموذجية مثل `lowres_scan.jpg` موجودة في مجلد يمكنك الإشارة إليه.
* إلمام أساسي بـ async/await—استدعاءات OCR غير متزامنة في API الخاص بـ Windows.

> **نصيحة احترافية:** إذا كنت تعمل على منصة غير Windows، استبدل مساحة الأسماء `Windows.Media.Ocr` بمكتبة متعددة المنصات مثل TesseractSharp؛ يبقى المنطق المحيط كما هو.

---

## الخطوة 1: إعداد **التعرف على نص الصورة** باستخدام محرك OCR

أولاً، نحتاج إلى إنشاء نسخة من محرك OCR. فئة `OcrEngine` هي نقطة الدخول لأي عملية **تحويل صورة إلى نص c#**.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Create the OCR engine – default language is English.
        OcrEngine engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));
        if (engine == null)
        {
            Console.WriteLine("Failed to create OcrEngine. Make sure you are on Windows 10 version 1809 or later.");
            return;
        }

        // Continue with the rest of the pipeline...
```

**لماذا هذا مهم:** المحرك يختصر الجهد الثقيل للتعرف على الأنماط. بإنشائه صراحةً نحصل على تحكم في إعدادات اللغة، وهو أمر أساسي عندما تريد لاحقًا **استخراج نص من مسح** مستندات بلغات أخرى.

## الخطوة 2: تحميل ملف الصورة – جوهر **تحويل المسح إلى نص**

بعد ذلك، نقرأ الصورة من القرص ونحولها إلى `SoftwareBitmap`، وهو الشكل الذي يتوقعه محرك OCR.

```csharp
        // Load the image file into a SoftwareBitmap.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "lowres_scan.jpg");
        using (FileStream fs = new FileStream(imagePath, FileMode.Open, FileAccess.Read))
        {
            // Decode the image (supports JPEG, PNG, BMP, etc.).
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Optional: upscale low‑resolution images for better accuracy.
            SoftwareBitmap upscaled = SoftwareBitmap.Convert(bitmap, bitmap.BitmapPixelFormat, bitmap.BitmapAlphaMode);
            // Pass the bitmap to OCR.
            await RecognizeAsync(engine, upscaled);
        }
    }
```

**سبب القيام بذلك:** تمرير تدفق ملف خام مباشرةً إلى OCR غالبًا ما ينتج عنه نتائج ضعيفة، خاصةً مع المسحات منخفضة الدقة. التحويل إلى `SoftwareBitmap` يتيح لنا تعديل DPI، عمق اللون، وحتى تطبيق فلاتر قبل عملية التعرف.

## الخطوة 3: تنفيذ عملية **التعرف على نص الصورة**

الآن نستدعي أخيرًا طريقة `RecognizeAsync` الخاصة بالمحرك. هنا يحدث السحر.

```csharp
    private static async Task RecognizeAsync(OcrEngine engine, SoftwareBitmap bitmap)
    {
        // Run OCR – this returns an OcrResult object.
        OcrResult result = await engine.RecognizeAsync(bitmap);

        // The Result contains a collection of lines and words.
        Console.WriteLine("=== OCR Output ===");
        foreach (var line in result.Lines)
        {
            Console.WriteLine(line.Text);
        }

        // For a quick **image to text c#** check, also output the raw string.
        Console.WriteLine("\nFull Text:\n" + result.Text);
    }
}
```

**ما ستراه:** إذا كانت الصورة `lowres_scan.jpg` تحتوي على العبارة “Hello World”، ستطبع وحدة التحكم:

```
=== OCR Output ===
Hello World

Full Text:
Hello World
```

هذا هو **مثال c# ocr** بالكامل في عمله—أربع خطوات منطقية فقط، لكنه يغطي كل شيء من تحميل الملف إلى الإخراج النهائي.

## الخطوة 4: معالجة الحالات الخاصة – عندما لا يكون المسح مثالياً

الصور الواقعية ليست دائمًا واضحة. إليك بعض التعديلات التي يمكنك إجراؤها دون الحاجة لإعادة كتابة البرنامج بالكامل:

| المشكلة | الحل السريع |
|-------|-----------|
| **DPI منخفض جدًا (≤ 72)** | قم بتكبير الـ bitmap باستخدام `BitmapTransform` قبل التعرف. |
| **نص مائل** | طبّق تحويل دوران (`SoftwareBitmap.Rotate`) لتصحيح الصفحة. |
| **لغات متعددة** | أنشئ `OcrEngine.TryCreateFromLanguage(new OcrLanguage("en-fr"))` واضبط `engine.Language` وفقًا لذلك. |
| **ملفات كبيرة** | عالج الصورة على شكل قطع (`engine.RecognizeAsync(tileBitmap)`) ثم اجمع النتائج. |

هذه التعديلات تضمن بقاء روتين **استخراج نص من مسح** موثوقًا حتى عند التعامل مع إيصالات مليئة بالضوضاء أو صور مأخوذة بزاوية.

## الخطوة 5: تحويل المثال إلى أداة مساعدة قابلة لإعادة الاستخدام (اختياري)

إذا كنت تخطط لـ **تحويل المسح إلى نص** في عدة أجزاء من التطبيق، غلف المنطق داخل فئة مساعدة صغيرة:

```csharp
public static class OcrHelper
{
    private static readonly OcrEngine _engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));

    public static async Task<string> ImageToTextAsync(string filePath)
    {
        using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        var decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
        var bitmap = await decoder.GetSoftwareBitmapAsync();

        var result = await _engine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

الآن يمكنك استدعاؤها ببساطة:

```csharp
string text = await OcrHelper.ImageToTextAsync("YOUR_DIRECTORY/lowres_scan.jpg");
Console.WriteLine(text);
```

**لماذا ستحب ذلك:** الأداة تعزل تفاصيل OCR، مما يتيح لك التركيز على منطق الأعمال—مثالي لـ **مثال c# ocr** سيُعاد استخدامه عبر مشاريع متعددة.

---

![مثال على التعرف على نص الصورة](https://example.com/ocr-demo.png "لقطة شاشة لإخراج وحدة التحكم في OCR تُظهر نتيجة التعرف على نص الصورة")

*نص بديل:* **إخراج التعرف على نص الصورة** من تطبيق وحدة تحكم OCR مكتوب بـ C#.

---

## الأسئلة المتكررة

**س: هل يعمل هذا على .NET Core على لينكس؟**  
ج: مساحة الأسماء `Windows.Media.Ocr` مخصصة لنظام Windows فقط. على لينكس أو macOS تستبدلها بـ TesseractSharp أو IronOcr—كلاهما يوفر طريقة `Engine.Recognize` مشابهة، لذا يبقى الكود المحيط دون تغيير جوهري.

**س: ما مدى دقة OCR المدمج للخطوط اليدوية؟**  
ج: التعرف على الخط اليدوي لا يزال تجريبيًا. للحصول على أفضل النتائج، استخدم خطوطًا مطبوعة أو فكر في خدمة سحابية مثل Azure Cognitive Services إذا كنت تحتاج إلى دقة عالية.

**س: هل يمكنني معالجة ملفات PDF مباشرة؟**  
ج: ليس مباشرة. يجب تحويل كل صفحة PDF إلى صورة أولًا (باستخدام `PdfSharp` أو `Ghostscript`) ثم تمرير الـ bitmap إلى محرك OCR.

---

## الخلاصة

أصبح لديك الآن **مثال c# ocr** كامل وجاهز للإنتاج يمكنه **التعرف على نص الصورة**، **استخراج نص من مسح**، و**تحويل المسح إلى نص** ببضع أسطر من الكود. بفهمك لتسلسل الخطوات—إنشاء المحرك، تحميل الصورة، التعرف غير المتزامن، ومعالجة النتيجة—يمكنك تعديل النمط لأي مشروع C# يحتاج إلى تحويل الصور إلى سلاسل قابلة للبحث.

هل أنت مستعد للخطوة التالية؟ جرّب إضافة واجهة مستخدم بسيطة باستخدام WinForms أو WPF، جرب لغات مختلفة، أو اربط الإخراج بقاعدة بيانات لأرشفة قابلة للبحث. السماء هي الحد عندما تتقن تقنيات **تحويل صورة إلى نص c#**.

برمجة سعيدة، ولتكن مسحاتك دائمًا واضحة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [تحويل الصورة إلى نص – تنفيذ OCR على صورة من URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [كيفية استخراج النص من الصورة عبر إعداد المستطيلات في OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}