---
category: general
date: 2026-04-03
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية تحويل الصورة
  الممسوحة ضوئياً، تحميل ملف الصورة في C#، والتعرف على النص من ملف TIF بشكل غير متزامن.
draft: false
keywords:
- extract text from image
- convert scanned image
- how to ocr image
- load image file c#
- recognize text from tif
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدليل
  كيفية تحويل الصورة الممسوحة ضوئياً، تحميل ملف الصورة في C#، والتعرف على النص من
  ملف TIF باستخدام استدعاءات غير متزامنة.
og_title: استخراج النص من صورة في C# – دليل OCR غير المتزامن
tags:
- OCR
- C#
- Aspose
- Async
title: استخراج النص من الصورة في C# – دليل OCR غير المتزامن
url: /ar/net/text-recognition/extract-text-from-image-in-c-async-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة في C# – دليل OCR غير المتزامن

هل تحتاج إلى **استخراج النص من الصورة** بسرعة؟ باستخدام Aspose OCR يمكنك القيام بذلك في C# باستخدام استدعاءات غير متزامنة، وتكتمل العملية بأكملها قبل أن تنتهي من فنجان القهوة الخاص بك.  
إذا كنت تتساءل أيضًا عن كيفية **تحويل صورة ممسوحة ضوئيًا** أو تحميل ملف صورة في C# دون عناء، فأنت في المكان الصحيح.

في هذا الدليل سنستعرض كل خطوة — من سحب ملف TIF من القرص إلى الحصول على نص نظيف وقابل للبحث. في النهاية ستتمكن من **التعرف على النص من ملفات TIF**، وفهم تفاصيل تحميل صيغ الصور المختلفة، وستحصل على نمط غير متزامن قوي يمكنك إعادة استخدامه في أي مشروع .NET.

## ما ستتعلمه

* كيفية إعداد محرك Aspose OCR للاستخدام غير المتزامن.  
* الكود الدقيق الذي تحتاجه **لتحميل ملف صورة C#**‑style، بما في ذلك معالجة الأخطاء للملفات المفقودة.  
* طرق **تحويل صورة ممسوحة ضوئيًا** من ملفات PDF أو TIFF إلى صورة bitmap يمكن لـ Aspose قراءتها.  
* لماذا OCR غير المتزامن (`RecognizeAsync`) أسرع وأكثر قابلية للتوسع مقارنةً بنظيره المتزامن.  
* الناتج المتوقع في وحدة التحكم وكيفية التحقق من أن النص المستخرج يطابق المصدر.

> **نصيحة احترافية:** إذا كنت تعالج عشرات الصفحات، حافظ على بقاء محرك OCR فعالًا عبر الاستدعاءات — إنشاء نسخة جديدة في كل مرة يضيف عبئًا غير ضروري.

## استخراج النص من الصورة بشكل غير متزامن

تكمن جوهر الحل في طريقة `Main` غير المتزامنة. استخدام `await` يبقي خيط واجهة المستخدم حرًا (أو، في تطبيق وحدة تحكم، يحرر مجموعة الخيوط) بينما يقوم محرك OCR بالعمل الشاق.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.Threading.Tasks;

class AsyncDemo
{
    static async Task Main()
    {
        // 1️⃣ Create an instance of the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        Image inputImage = Image.FromFile(@"YOUR_DIRECTORY/input.tif");

        // 3️⃣ Run asynchronous OCR recognition (returns a Task<string>)
        string recognizedText = await ocrEngine.RecognizeAsync(inputImage);

        // 4️⃣ Display the OCR result
        Console.WriteLine("Async OCR result:");
        Console.WriteLine(recognizedText);
    }
}
```

**لماذا غير متزامن؟** قد تتضمن عملية OCR إدخال/إخراج شبكة (إذا كان المحرك يستخدم خدمات سحابية) أو عمل مكثف على وحدة المعالجة المركزية. `RecognizeAsync` يحرر الخيط المستدعي، مما يسمح بمتابعة أعمال أخرى — مثل معالجة ملفات إضافية.

### الناتج المتوقع

```
Async OCR result:
The quick brown fox jumps over the lazy dog.
```

إذا كانت الصورة تحتوي على عدة أسطر، سيظهر كل سطر مفصولًا بأحرف سطر جديد. يمكنك توجيه النتيجة إلى ملف باستخدام `File.WriteAllText("output.txt", recognizedText);` إذا كنت تحتاج إلى تخزين دائم.

## تحويل الصورة الممسوحة ضوئيًا إلى صيغة قابلة للاستخدام

أحيانًا تستلم ملف PDF ممسوح ضوئيًا أو TIFF متعدد الصفحات. يعمل Aspose OCR بأفضل شكل مع `System.Drawing.Image`، لذا قد تحتاج إلى التحويل أولاً.

```csharp
using Aspose.OCR;
using System.Drawing;
using System.Drawing.Imaging;

// Load a multi‑page TIFF and pick the first frame
Image tiff = Image.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
tiff.SelectActiveFrame(FrameDimension.Page, 0); // Grab page 0

// Optionally, change DPI for better accuracy
var bitmap = new Bitmap(tiff);
bitmap.SetResolution(300, 300); // 300 DPI is a sweet spot for OCR
```

> **لماذا تغيير DPI؟** الدقة الأعلى تعطي محرك OCR مزيدًا من التفاصيل، مما يقلل من الأخطاء في التعرف على الصور الضبابية. فقط لا تتجاوز 600 DPI — معظم المحركات لن تحصل على دقة إضافية ولكنها ستستهلك المزيد من الذاكرة.

## تحميل ملف صورة C# — التعامل مع الصيغ المختلفة

قد تميل إلى كتابة مسار `.tif` صلبًا، لكن الأداة القوية يجب أن تقبل **أي** نوع صورة (`.png`, `.jpg`, `.bmp`). إليك أداة مساعدة صغيرة تجريد منطق التحميل:

```csharp
static Image LoadImage(string path)
{
    if (!File.Exists(path))
        throw new FileNotFoundException($"Image not found: {path}");

    // Let .NET decide the correct decoder based on file header
    using (var stream = File.OpenRead(path))
    {
        return Image.FromStream(stream);
    }
}
```

استخدمها هكذا:

```csharp
Image img = LoadImage(@"YOUR_DIRECTORY/input.tif");
string text = await ocrEngine.RecognizeAsync(img);
```

الآن غطيت سيناريو **تحميل ملف صورة C#** دون القلق بشأن الامتداد الدقيق.

## التعرف على النص من TIF — ما تحتاج معرفته

غالبًا ما تخزن ملفات TIF عدة صفحات أو تستخدم ضغطًا يربك بعض المكتبات. هناك شيئين يساعدانك على الحصول على نتائج موثوقة:

1. **اختر الإطار الصحيح** — كما هو موضح سابقًا باستخدام `SelectActiveFrame`.  
2. **تطبيع الألوان** — تحويل إلى صورة bitmap 24‑bit RGB يمكن أن يقضي على لوحات ألوان غريبة.

```csharp
static Image PrepareTif(string tifPath, int pageIndex = 0)
{
    Image tif = Image.FromFile(tifPath);
    tif.SelectActiveFrame(FrameDimension.Page, pageIndex);
    // Convert to 24‑bit RGB to avoid palette issues
    Bitmap rgb = new Bitmap(tif.Width, tif.Height, PixelFormat.Format24bppRgb);
    using (Graphics g = Graphics.FromImage(rgb))
    {
        g.DrawImage(tif, 0, 0, tif.Width, tif.Height);
    }
    return rgb;
}
```

مرر الـ `Image` المعاد مباشرة إلى `RecognizeAsync` وستتمكن من **التعرف على النص من TIF** بثقة حتى عندما يستخدم المصدر ضغط CCITT Group 4.

## مثال كامل من البداية إلى النهاية

جمع كل شيء معًا يمنحك ملفًا واحدًا يمكنك وضعه في مشروع وحدة تحكم وتشغيله.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        try
        {
            // Step 1 – Initialize OCR engine (reuse if processing many files)
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2 – Load and prepare the image (handles TIF, PNG, JPG, etc.)
            Image img = PrepareImage(@"YOUR_DIRECTORY/input.tif");

            // Step 3 – Run async recognition
            string result = await ocrEngine.RecognizeAsync(img);

            // Step 4 – Output the result
            Console.WriteLine("Async OCR result:");
            Console.WriteLine(result);

            // Optional: Save to a text file
            File.WriteAllText("ocr-output.txt", result);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // Helper that decides how to load based on extension
    static Image PrepareImage(string path)
    {
        string ext = Path.GetExtension(path).ToLowerInvariant();
        return ext switch
        {
            ".tif" or ".tiff" => PrepareTif(path),
            _ => LoadImage(path)
        };
    }

    static Image LoadImage(string path)
    {
        if (!File.Exists(path))
            throw new FileNotFoundException($"Image not found: {path}");

        using var stream = File.OpenRead(path);
        return Image.FromStream(stream);
    }

    static Image PrepareTif(string tifPath, int page = 0)
    {
        Image tif = Image.FromFile(tifPath);
        tif.SelectActiveFrame(FrameDimension.Page, page);
        Bitmap rgb = new Bitmap(tif.Width, tif.Height, PixelFormat.Format24bppRgb);
        using var g = Graphics.FromImage(rgb);
        g.DrawImage(tif, 0, 0, tif.Width, tif.Height);
        return rgb;
    }
}
```

**ما يجب أن تراه:** تقوم وحدة التحكم بطباعة النص المستخرج، ويظهر ملف باسم `ocr-output.txt` بجوار الملف التنفيذي يحتوي على نفس السلسلة.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني إجراء OCR لملف PDF مباشرة؟* | يعمل Aspose OCR على الصور، لذا تحتاج أولاً إلى تحويل كل صفحة PDF إلى صورة (مثلاً باستخدام Aspose.PDF أو `PdfRenderer`). |
| *ماذا لو كانت الصورة ضخمة؟* | قلل الحجم إلى حد أقصى 2500 px للعرض/الارتفاع قبل OCR؛ سيقوم Aspose بإعادة التحجيم داخليًا تلقائيًا، لكنك ستوفر الذاكرة. |
| *هل الطريقة غير المتزامنة آمنة من حيث الخيوط؟* | نعم، لكن أعد استخدام نفس كائن `OcrEngine` فقط إذا لم تكن تستدعي `RecognizeAsync` بشكل متزامن. للمعالجة المتوازية، أنشئ محركات منفصلة لكل مهمة. |
| *هل أحتاج إلى ترخيص؟* | يوفر Aspose OCR تقييمًا مجانيًا مع علامات مائية. للإنتاج، اشترِ ترخيصًا واضبطه عبر `License license = new License(); license.SetLicense("Aspose.OCR.lic");`. |

## الخلاصة

أنت الآن تعرف كيف **استخراج النص من ملفات الصورة** في C# باستخدام واجهة Aspose OCR غير المتزامنة. من خلال معالجة تحميل الصور، التحويل الاختياري للصور الممسوحة ضوئيًا، وخصوصيات ملفات TIF، فإن الحل قوي وجاهز للإنتاج.  

من هنا قد ترغب في:

* **تحويل ملفات PDF الممسوحة ضوئيًا** إلى PNG قبل OCR للحصول على دقة أفضل.  
* استكشف **كيفية OCR الصورة** من تدفقات مباشرة عبر واجهة ويب API، مما يلغي الحاجة إلى ملفات مؤقتة.  
* معالجة دفعات من عشرات الملفات بإعادة استخدام كائن `OcrEngine` داخل حلقة `Parallel.ForEach`.  

جرّب هذه الأنواع، وسترى بسرعة لماذا OCR غير المتزامن يُغيّر قواعد اللعبة للتطبيقات التي تتعامل مع مستندات كثيرة. برمجة سعيدة، ولا تتردد في ترك تعليق إذا واجهت أي صعوبات!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}