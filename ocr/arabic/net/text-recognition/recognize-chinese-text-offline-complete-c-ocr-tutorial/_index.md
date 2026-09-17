---
category: general
date: 2026-01-02
description: تعلم كيفية التعرف على النص الصيني واستخراج النص من ملفات PNG باستخدام
  التعرف على النصوص دون اتصال عبر Aspose.OCR. لا حاجة للإنترنت – قم بإجراء OCR على
  الصورة في بضع خطوات فقط.
draft: false
keywords:
- recognize chinese text
- extract text from png
- offline text recognition
- perform OCR on image
language: ar
og_description: التعرف على النص الصيني دون الإنترنت. يوضح هذا الدرس كيفية استخراج
  النص من ملف PNG باستخدام التعرف على النص دون اتصال وإجراء OCR على الصورة في C#.
og_title: التعرف على النص الصيني دون اتصال – دليل C# خطوة بخطوة
tags:
- OCR
- C#
- Aspose
title: التعرف على النص الصيني دون اتصال – دليل OCR كامل بلغة C#
url: /ar/net/text-recognition/recognize-chinese-text-offline-complete-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص الصيني دون اتصال – دليل OCR كامل بلغة C#

هل احتجت يومًا إلى **التعرف على النص الصيني** من صورة PNG ممسوحة ضوئيًا لكن تطبيقك يعمل على جهاز بدون إنترنت؟ لست وحدك. في العديد من سيناريوهات الشركات—مثل الخوادم المعزولة أو الأجهزة الميدانية—الاعتماد على خدمات السحابة ليس خيارًا.

في هذا الدليل سنستعرض حلًا ذاتيًا يتيح لك **استخراج النص من ملفات png**، تشغيل **التعرف على النص دون اتصال**، و**إجراء OCR على ملفات الصور** باستخدام Aspose.OCR. في النهاية ستحصل على برنامج C# Console جاهز للتشغيل يطبع الأحرف الصينية مباشرةً في وحدة التحكم.

## المتطلبات المسبقة

- .NET 6 SDK (أو أي نسخة حديثة من .NET) مثبت محليًا.  
- Visual Studio 2022 أو VS Code – حسب ما تفضله.  
- نسخة من حزمة NuGet Aspose.OCR لـ .NET (`Aspose.OCR`).  
- ملفات موارد اللغة للإنجليزية والصينية المبسطة (الدليل يوضح كيفية تنزيلها تلقائيًا).  
- صورة باسم `chinese_doc.png` موجودة في مجلد يمكنك الإشارة إليه (عنصر نائب `YOUR_DIRECTORY`).

لا توجد خدمات إضافية، ولا مفاتيح API—فقط مكتبة DLL محلية وقليل من ملفات الموارد.

---

## الخطوة 1 – تنزيل موارد اللغة المطلوبة (مرة واحدة)

Aspose.OCR يخزن حزم اللغات على القرص. في المرة الأولى التي تشغل فيها التطبيق تحتاج إلى سحبها. استدعاء `ResourceManager.DownloadResources` يقوم بذلك بالضبط، وبما أننا نمرر كلًا من الإنجليزية والصينية المبسطة، يمكن للمحرك التبديل بينهما لاحقًا دون أي حركة مرور شبكة إضافية.

```csharp
using Aspose.OCR;

// Download English and Simplified Chinese language packs (run once)
ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);
```

> **نصيحة احترافية:** احتفظ بالمجلد الذي تم تنزيله (`Aspose.OCR.Resources`) تحت نظام التحكم في الإصدارات إذا كنت تحتاج إلى بنى قابلة لإعادة الإنتاج على عدة أجهزة.

## الخطوة 2 – تهيئة محرك OCR في وضع عدم الاتصال

ضبط `OfflineMode = true` يخبر المكتبة بتجنب أي استدعاءات HTTP. هذا هو المفتاح للحصول على **التعرف على النص دون اتصال** حقيقي.

```csharp
// Initialise the OCR engine for offline use
var ocrEngine = new OcrEngine()
{
    OfflineMode = true   // Guarantees no network traffic
};
```

> **لماذا هذا مهم:** بعض مكتبات OCR تلجأ إلى خدمات السحابة عندما تكون حزمة اللغة مفقودة. بفرض وضع عدم الاتصال نضمن أداءً حتميًا والامتثال لسياسات خصوصية البيانات.

## الخطوة 3 – تحميل ملف PNG الذي تريد معالجته

سنستخدم `System.Drawing.Bitmap` لقراءة الصورة. إذا كان مشروعك يستهدف .NET 6+ على منصات غير Windows، فكر في `SkiaSharp` كبديل، لكن بالنسبة لمعظم عمليات النشر التي تركز على Windows يعمل `Bitmap` بشكل جيد.

```csharp
using System.Drawing;

// Load the PNG that contains Chinese characters
var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
var image = new Bitmap(imagePath);
```

> **حالة حافة:** إذا كان ملف PNG كبيرًا جدًا (أكثر من 5 MP) قد ترغب في تقليص حجمه أولًا لتسريع التعرف وتقليل استهلاك الذاكرة:

```csharp
// Optional downscale for huge images
if (image.Width * image.Height > 5_000_000)
{
    var scaled = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
    image.Dispose();
    image = scaled;
}
```

## الخطوة 4 – تشغيل التعرف باستخدام اللغة الصينية المبسطة

هنا نخبر المحرك بالضبط أي لغة يجب استخدامها. كائن `RecognitionOptions` يتيح لك أيضًا تعديل خيارات مثل `DetectOrientation` أو `PreserveFormatting`، لكن الإعدادات الافتراضية تعمل جيدًا لمعظم المستندات المطبوعة.

```csharp
using Aspose.OCR;

// Perform OCR using Simplified Chinese language pack
var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
{
    Language = Language.ChineseSimplified
});
```

## الخطوة 5 – عرض (أو معالجة) النص المستخرج

خاصية `OcrResult.Text` تحتفظ بالتمثيل النصي العادي. يمكنك كتابتها إلى وحدة التحكم، ملف، أو تمريرها إلى خط أنابيب NLP لاحق.

```csharp
// Output the recognized Chinese text to the console
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

### النتيجة المتوقعة

إذا كان `chinese_doc.png` يحتوي على العبارة “你好，世界！”، ستظهر وحدة التحكم:

```
=== Recognized Chinese Text ===
你好，世界！
```

> **ملاحظة:** دقة OCR تعتمد على جودة الصورة، وضوح الخط، والتباين. للحصول على أفضل النتائج، استخدم مسحات عالية الدقة (300 dpi أو أعلى) وتأكد من أن النص غير مائل.

---

## مثال عملي كامل

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق. احفظه باسم `Program.cs` داخل مشروع Console جديد وشغّل `dotnet run`. جميع الخطوات مدمجة معًا، لذا يمكنك رؤية التدفق من تنزيل الموارد إلى الإخراج النهائي.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;

class OfflineExample
{
    static void Main()
    {
        // 1️⃣ Download language resources (only needed once)
        ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);

        // 2️⃣ Initialise OCR engine in offline mode
        var ocrEngine = new OcrEngine()
        {
            OfflineMode = true
        };

        // 3️⃣ Load the PNG image
        var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
        using var image = new Bitmap(imagePath);

        // 4️⃣ Recognise Simplified Chinese text
        var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
        {
            Language = Language.ChineseSimplified
        });

        // 5️⃣ Print the result
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **نصيحة:** غلف استدعاء `ResourceManager.DownloadResources` داخل كتلة `try/catch` إذا أردت معالجة مرنة عندما يكون الإنترنت غير متاح فعليًا. ستقوم الطريقة بإلقاء استثناء `NetworkException` خلاف ذلك.

---

## الأسئلة المتكررة (FAQ)

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني التعرف على الصينية التقليدية؟** | نعم—استبدل `Language.ChineseSimplified` بـ `Language.ChineseTraditional` ونزل الحزمة المقابلة. |
| **ماذا لو أردت استخراج النص من JPEG بدلاً من PNG؟** | نفس الكود يعمل؛ فقط غيّر امتداد الملف. `Bitmap` يدعم معظم صيغ الصور النقطية الشائعة. |
| **هل هناك طريقة للحصول على إطارات حدودية لكل حرف؟** | اضبط `RecognitionOptions.DetectRegions = true`. سيحتوي `OcrResult` بعد ذلك على كائنات `Region` مع الإحداثيات. |
| **كيف أشغل هذا على Linux؟** | استخدم حزمة `System.Drawing.Common` (الإصدار 1.0+). على Linux بدون واجهة قد تحتاج إلى الاعتماد الأصلي `libgdiplus`. |
| **هل يمكنني معالجة مجموعة من الصور دفعة واحدة؟** | بالتأكيد—غلف منطق التعرف داخل حلقة `foreach (var file in Directory.GetFiles(folder, "*.png"))`. |

---

## الخطوات التالية والمواضيع ذات الصلة

- **تحسين الدقة**: جرّب `RecognitionOptions.PreprocessImage = true` للسماح للمحرك بتحسين التباين تلقائيًا.  
- **دمج اللغات**: يمكنك تمرير مصفوفة من اللغات إلى `ResourceManager.DownloadResources` والسماح للمحرك بالكشف التلقائي.  
- **دمج مع واجهة مستخدم**: انقل كود الـ console إلى تطبيق WinForms أو WPF وعرض نتيجة OCR في مربع نص.  
- **استكشاف مكتبات Aspose الأخرى**: `Aspose.PDF` لإنشاء ملفات PDF، `Aspose.Slides` لأتمتة العروض التقديمية، إلخ.  

إذا كنت مهتمًا باستخراج النص من صيغ صور أخرى، فإن النمط نفسه ينطبق—فقط استبدل مسار الملف وقم بتعديل خيارات ما قبل المعالجة إذا لزم الأمر. برمجة سعيدة!

---

![recognize chinese text example](/images/recognize-chinese-text.png "Screenshot showing recognize chinese text output in console")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}