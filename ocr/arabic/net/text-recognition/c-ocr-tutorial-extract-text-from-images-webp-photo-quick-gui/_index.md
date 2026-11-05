---
category: general
date: 2026-03-17
description: دورة C# OCR – اكتشف كيفية استخراج النص من ملفات الصور، قراءة النص من
  صور WebP، وتحويل الصورة إلى نص باستخدام OcrEngine بسيط.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: ar
og_description: يُظهر لك درس C# OCR كيفية استخراج النص من ملفات الصور، قراءة النص
  من صور WebP، وتحويل الصورة إلى نص باستخدام بضع أسطر من الشيفرة.
og_title: دليل C# OCR – استخراج النص من الصور في دقائق
tags:
- C#
- OCR
- Image Processing
title: 'دليل سريع: برنامج تعليمي C# OCR: استخراج النص من الصور (WebP، صورة)'
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# OCR – استخراج النص من الصور (WebP، صورة)

هل احتجت يوماً إلى **استخراج النص من صورة** ولكنك لم تعرف من أين تبدأ في C#؟ ربما لديك لقطة شاشة بصيغة WebP، أو صورة JPEG لإيصال، أو صفحة PDF ممسوحة وتريد فقط الكلمات الموجودة بداخلها. في هذا **دليل c# OCR** سنستعرض مثالاً كاملاً جاهزاً للتنفيذ يقرأ النص من صورة، يدعم WebP وغيرها من الصيغ الحديثة، ويحول الصورة إلى نص عادي—كل ذلك في بضع أسطر فقط.

**ما الفائدة؟** ستتمكن من تحويل أي صورة تحتوي على نص إلى سلاسل قابلة للبحث، وإدخالها في قواعد البيانات، أو تمريرها إلى خطوط معالجة AI لاحقة. لا سحر، فقط محرك OCR قوي، وبعض واجهات .NET، وتوضيحات واضحة للـ “لماذا” وراء كل خطوة.

## ما الذي ستحتاجه

قبل أن نبدأ، تأكد من وجود التالي:

- **.NET 6 SDK** (أو أحدث). الكود أدناه يُترجم مع .NET 6+ ويعمل على Windows، Linux، أو macOS.
- **Visual Studio 2022** أو أي محرر تفضله (VS Code يعمل بشكل جيد).
- حزمة **`Microsoft.Windows.SDK.Contracts`** من NuGet (توفر `Windows.Media.Ocr`). ثبّتها باستخدام:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- ملف صورة تريد معالجته – في هذا الدليل سنستخدم صورة **WebP** باسم `photo.webp` موجودة في مجلد يسمى `YOUR_DIRECTORY`.

> نصيحة احترافية: إذا كنت على منصة غير Windows، يمكنك استبدال `OcrEngine` بمكتبة متعددة المنصات مثل **Tesseract**. يبقى الكود المحيط تقريباً كما هو.

## الخطوة 1: إعداد مشروع دليل C# OCR

أولاً، أنشئ تطبيق console جديد. افتح الطرفية ونفّذ:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

أضف الحزمة المطلوبة (كما هو موضح أعلاه) وافتح المشروع في بيئة التطوير الخاصة بك. هذا الإعداد يمنحنا قاعدة نظيفة لـ **دليل c# OCR**.

## الخطوة 2: استيراد المساحات الاسمية وتحضير الصورة

نحتاج إلى بعض توجيهات `using` حتى يعرف المترجم أين يجد `OcrEngine`، `SoftwareBitmap`، ومساعدي تحميل الصور.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **لماذا هذه المساحات الاسمية؟**  
> `Windows.Media.Ocr` يحتوي على الفئة `OcrEngine` التي تقوم فعلياً بعملية التعرف. `Windows.Graphics.Imaging` يتيح لنا فك ترميز الصورة (بما فيها WebP) إلى `SoftwareBitmap` يمكن للمحرك قراءتها. مساعدات `System.IO` و `Windows.Storage.Streams` تجعل تحميل الملفات سهلًا.

الآن، قم بتحميل الصورة. الفاكتر المدمج يستطيع التعامل مع WebP، HEIF، PNG، JPEG، وأكثر، لذا يمكنك **قراءة النص من WebP** دون إضافات خارجية.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **حالة خاصة:** إذا كانت صورتك بالفعل بالأبيض والأسود، يمكنك تخطي خطوة التحويل. تحويل الصورة إلى تدرج رمادي يمنح تحسينًا بسيطًا في الأداء وغالبًا ما يحسّن التعرف على الصور الضوضائية.

## الخطوة 3: تشغيل محرك OCR – التعرف على النص من الصورة

هذا هو جوهر **دليل c# OCR**. ننشئ مثالًا من `OcrEngine`، نمرره إلى الـ bitmap، ثم نستخرج النص المعترف به.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**ما الذي يحدث؟**  
- `TryCreateFromUserProfileLanguages()` يختار اللغة (اللغات) التي تم ضبطها في ملف تعريف مستخدم Windows، وهو عادةً ما يغطي الإنجليزية، الإسبانية، إلخ. إذا كنت بحاجة إلى لغة محددة، استخدم `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.  
- `RecognizeAsync` يقوم بالعمل الثقيل على خيط خلفي، ويعيد `OcrResult` يحتوي على السلسلة الخام، مربعات حدود الكلمات، ودرجات الثقة.  
- أخيرًا، نطبع `ocrResult.Text`، مما يمنحك نتيجة **تحويل الصورة إلى نص** التي يمكنك توجيهها إلى أي مكان آخر.

## الخطوة 4: مثال كامل قابل للتنفيذ

بدمج كل ما سبق، إليك برنامج مستقل يمكنك نسخه ولصقه في `Program.cs`. يترجم، ينفّذ، ويطبع النص المستخرج من `photo.webp`.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### النتيجة المتوقعة

إذا كان `photo.webp` يحتوي على الجملة “Hello, world! This is a test.” فستظهر لك نتيجة مشابهة:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

تختلف الفواصل السطرية الدقيقة حسب تخطيط الصورة الأصلية، لكن نتيجة **استخراج النص من الصورة** ستكون دائمًا سلسلة نصية عادية يمكنك معالجتها لاحقًا.

## أسئلة شائعة وحالات خاصة

### هل يعمل هذا مع صيغ صور أخرى؟

بالتأكيد. الفاكتر المستخدم (`BitmapDecoder`) يكتشف تلقائيًا JPEG، PNG، BMP، GIF، **WebP**، HEIF، وأكثر. لذا يمكنك **قراءة النص من WebP**، JPEG، أو حتى TIFF دون تعديل الكود.

### ماذا لو أعاد محرك OCR ثقة منخفضة؟

يمكنك فحص `ocrResult.Lines` وكل `OcrWord` للحصول على `ConfidenceScore`. إذا كان المعدل أقل من عتبة (مثلاً 0.6)، فكر في:

- معالجة مسبقة للصورة (زيادة التباين، تحسين الحدة، تصحيح الميل).
- استخدام صورة مصدر ذات دقة أعلى.
- التحول إلى مكتبة مخصصة مثل **Tesseract** لدعم متعدد اللغات.

### كيف أتعامل مع لغات متعددة في نفس الصورة؟

أنشئ مثيلات منفصلة من `OcrEngine` لكل لغة وشغّلها بالتتابع، أو استخدم مكتبة تدعم اكتشاف اللغات المختلطة. بالنسبة للمحرك المدمج، يمكنك تمرير كائن `Language`:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### هل يمكن تشغيل هذا على Linux/macOS؟

واجهة `Windows.Media.Ocr` مخصصة لنظام Windows فقط. على المنصات غير Windows، استبدل جزء OCR بـ **Tesseract** (من خلال `Tesseract.Net.SDK`). يظل كود التحميل والمعالجة المسبقة هو نفسه، لذا يبقى باقي **دليل c# OCR** صالحًا.

## نصائح احترافية لتحسين الدقة

- **تغيير الحجم**: قلل الصور الكبيرة إلى حد أقصى 2000 بكسل على الجانب الأطول – محركات OCR تعمل أسرع على الأحجام المتوسطة.  
- **إزالة الضوضاء** باستخدام تمويه غاوسي بسيط إذا كانت الصورة محببة.  
- **تصحيح الميل** للـ bitmap إذا لم يكن النص أفقيًا تمامًا؛ يمكن تدوير `SoftwareBitmap` قبل تمريره إلى `OcrEngine`.  
- **تخزين مؤقت** لكائن `OcrEngine` إذا كنت تعالج العديد من الصور دفعة واحدة؛ إنشاءه مرارًا يضيف عبئًا.

## مواضيع ذات صلة لاستكشافها

- **تحويل الصورة إلى نص** باستخدام **Tesseract** للمشاريع متعددة المنصات.  
- **استخراج النص من PDF** عن طريق تحويل كل صفحة إلى صورة أولاً.  
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}