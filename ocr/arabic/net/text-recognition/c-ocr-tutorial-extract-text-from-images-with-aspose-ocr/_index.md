---
category: general
date: 2026-02-20
description: دورة C# OCR تُظهر لك كيفية استخراج النص من الصورة، التعرف على النص من
  ملف PNG، وتحويل الصورة إلى نص في بضع أسطر من الشيفرة فقط.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from png
- convert image to text
- how to extract text
language: ar
og_description: دليل C# OCR يشرح لك كيفية استخراج النص من ملفات الصور، والتعرف على
  النص من ملفات PNG، وتحويل الصور إلى نص باستخدام Aspose.OCR.
og_title: دورة C# OCR – دليل سريع لاستخراج النص من الصور
tags:
- OCR
- C#
- Aspose
title: دورة C# OCR – استخراج النص من الصور باستخدام Aspose.OCR
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# OCR – استخراج النص من الصور باستخدام Aspose.OCR

هل احتجت يوماً إلى **c# ocr tutorial** يعمل فعلياً على ملف PNG حقيقي؟ لست وحدك. في العديد من المشاريع—مثل مسح الفواتير، أرشفة الإيصالات، أو تحليل لقطات الشاشة البسيطة—يواجه المطورون صعوبة عندما يحاولون **extract text from image** دون مكتبة موثوقة.  

الخبر السار هو أن Aspose.OCR يجعل العملية بأكملها سهلة للغاية. في هذا الدليل سنستعرض مثالاً كاملاً قابلًا للتنفيذ يوضح **how to extract text** من ملف PNG، ويشرح *why* كل سطر مهم، ويتطرق أيضاً إلى حالات الحافة مثل الترخيص ومعالجة الصور مسبقًا. في النهاية ستتمكن من **recognize text from png** و **convert image to text** باستخدام بضع جمل C# فقط.

## ما يغطيه هذا الدرس

- إعداد محرك Aspose.OCR في تطبيق .NET Console.  
- تحميل PNG (أو أي صورة bitmap مدعومة) من القرص.  
- تشغيل OCR وطباعة النتيجة إلى وحدة التحكم.  
- الترخيص الاختياري، معالجة الأخطاء، ونصائح الأداء.  

لا خدمات خارجية، لا سحر مخفي—فقط كود C# نقي يمكنك نسخه ولصقه وتشغيله. إذا تساءلت يوماً عن **how to extract text** من مستند ممسوح ضوئياً، ابق معنا؛ سنجيب على ذلك وبعض أسئلة “ماذا لو” على طول الطريق.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل أيضاً على .NET Framework 4.7+).  
- Visual Studio 2022 (أو أي محرر تفضله).  
- حزمة NuGet مجانية أو مدفوعة لـ Aspose.OCR for .NET.  
- ملف صورة باسم `sample.png` موجود في مجلد يمكنك الإشارة إليه.  

هذا كل شيء—لا تحتاج إلى أدوات طرف ثالث أخرى.

## دليل c# OCR: إعداد Aspose.OCR

أولاً وقبل كل شيء: تحتاج إلى مكتبة Aspose.OCR. افتح الطرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

هذا يقوم بجلب أحدث نسخة مستقرة ويضيف مراجع DLL الضرورية. إذا كان لديك ملف ترخيص (`Aspose.OCR.lic`)، احتفظ به قريبًا؛ وإلا سيعمل الإصدار التجريبي المجاني، لكن مع علامات مائية على نتيجة OCR.

### لماذا الترخيص مهم

بدون ترخيص يعمل المحرك في وضع التقييم، مما يضيف سطر “Powered by Aspose” إلى الناتج لبعض اللغات. في كود الإنتاج ستحتاج إلى استدعاء `SetLicense` مبكرًا، كما هو موضح في الكود أدناه. هو استدعاء سطر واحد، لكنه يزيل العلامة المائية ويفتح المعالجة بأقصى سرعة.

## استخراج النص من الصورة باستخدام Aspose.OCR

الآن دعنا نتعمق في كود OCR الفعلي. أدناه برنامج **complete, self‑contained** يمكنك تجميعه وتشغيله فورًا.

```csharp
using System;
using System.Drawing;          // Needed for Image class
using Aspose.OCR;               // Core OCR namespace
using Aspose.OCR.Models;       // For OCR settings (optional)

class LicenseCheck
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2 (Optional): Apply your Aspose.OCR license
        // -------------------------------------------------
        // Uncomment and set the correct path if you have a license file.
        // ocrEngine.SetLicense(@"C:\MyLicenses\Aspose.OCR.lic");

        // -------------------------------------------------
        // Step 3: Load the image you want to process
        // -------------------------------------------------
        // You can use any supported format (png, jpg, bmp, tiff, etc.)
        string imagePath = @"C:\Images\sample.png";
        Image inputImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // Step 4: Recognize text from the loaded image
        // -------------------------------------------------
        // The Recognize method returns a plain string.
        string recognizedText = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 5: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**ما الذي يحدث هنا؟**  

1. **Engine creation** – `OcrEngine` هو نقطة الدخول الرئيسية؛ يقوم بتحميل بيانات اللغة داخليًا.  
2. **License loading** – اختياري لكن يُنصح به؛ ببساطة تشير إلى ملف `.lic` الخاص بك.  
3. **Image loading** – `Image.FromFile` يعمل مع أي صيغة bitmap؛ نستخدم PNG لأنه يحافظ على الجودة غير المضغوطة، وهو أمر حاسم لدقة OCR.  
4. **Recognition** – `ocrEngine.Recognize` يقوم بكل المعالجة الثقيلة، ويعيد سلسلة تحتوي على الأحرف المكتشفة.  
5. **Output** – نكتب النتيجة إلى وحدة التحكم، لكن يمكنك بسهولة إرسالها إلى ملف أو قاعدة بيانات أو عنصر واجهة مستخدم.  

### النتيجة المتوقعة

إذا كان `sample.png` يحتوي على النص “Hello World”، ستظهر وحدة التحكم:

```
=== OCR Result ===
Hello World
```

إذا كانت الصورة غير واضحة أو تحتوي على أحرف غير لاتينية، قد تتضمن النتيجة رموزًا مشوشة. هنا يأتي دور المعالجة المسبقة (ضبط التباين، التحويل إلى ثنائي) — وهو ما سيتم تغطيته في القسم التالي.

## التعرف على النص من ملفات PNG – نصائح وحيل

PNG هو تنسيق شائع لأنه يخزن البكسلات دون تشويهات ضغط. ومع ذلك، ليست كل ملفات PNG متساوية. إليك بعض النصائح العملية التي قد تجدها مفيدة:

- **Resolution matters** – استهدف على الأقل 300 dpi. أي قيمة أقل قد تتسبب في فقدان الأحرف.  
- **Color vs. Grayscale** – تحويل PNG ملون إلى تدرج رمادي قبل OCR يمكن أن يحسن السرعة دون الإضرار بالدقة.  
- **Noise removal** – البقع الصغيرة غالبًا ما تربك المحرك؛ يمكن لمرشح متوسط بسيط أن يساعد.

أدناه مقتطف سريع يوضح كيفية معالجة صورة مسبقًا قبل تمريرها إلى Aspose.OCR:

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
Bitmap grayBitmap = new Bitmap(inputImage.Width, inputImage.Height);
using (Graphics g = Graphics.FromImage(grayBitmap))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}});
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(inputImage, new Rectangle(0,0,grayBitmap.Width,grayBitmap.Height),
                0,0,inputImage.Width,inputImage.Height, GraphicsUnit.Pixel, attributes);
}

// Optional: Apply a simple binary threshold
Bitmap binBitmap = new Bitmap(grayBitmap.Width, grayBitmap.Height);
for (int y = 0; y < grayBitmap.Height; y++)
{
    for (int x = 0; x < grayBitmap.Width; x++)
    {
        Color pixel = grayBitmap.GetPixel(x, y);
        int bw = pixel.R < 128 ? 0 : 255; // threshold at 128
        binBitmap.SetPixel(x, y, Color.FromArgb(bw, bw, bw));
    }
}

// Now run OCR on the cleaned bitmap
string cleanedText = ocrEngine.Recognize(binBitmap);
Console.WriteLine(cleanedText);
```

**نصيحة احترافية:** إذا كنت تعالج عشرات الصور، أنشئ نسخة واحدة من `OcrEngine` وأعد استخدامها. إنشاء محرك جديد لكل صورة يضيف عبئًا غير ضروري.

## تحويل الصورة إلى نص – خيارات متقدمة

Aspose.OCR لا يقتصر على استخراج النص العادي. يمكنك طلب إرجاع **structured data** (مثل إطارات الكلمات) أو ضبط **language hints** لتحسين الدقة في المستندات متعددة اللغات.

```csharp
// Set language to English + Spanish (ISO codes)
ocrEngine.Language = Language.English | Language.Spanish;

// Request detailed OCR result
OcrResult result = ocrEngine.RecognizeImage(inputImage, OcrOptions.DetectTextBlocks);

// Iterate over detected words
foreach (var word in result.Words)
{
    Console.WriteLine($"{word.Text} (x:{word.Bounds.X}, y:{word.Bounds.Y})");
}
```

كائن `OcrResult` يزودك بإحداثيات كل كلمة، وهو مفيد لتظليل النص في واجهة المستخدم أو للمعالجة اللاحقة (مثلاً إخفاء المعلومات الحساسة).

## كيفية استخراج النص في سيناريوهات العالم الحقيقي

دعونا نجيب على بعض أسئلة “ماذا لو” التي تظهر كثيرًا في بيئات الإنتاج.

### ماذا لو كانت الصورة صفحة PDF؟

يمكن لـ Aspose.OCR قراءة ملفات PDF مباشرة، لكن ستحتاج إلى مكتبة Aspose.PDF لتحويل كل صفحة إلى صورة أولاً. سير العمل هو:

1. تحميل PDF باستخدام `Aspose.Pdf.Document`.  
2. تحويل صفحة إلى bitmap (`PdfConverter`).  
3. تمرير الـ bitmap إلى `OcrEngine.Recognize`.

### ماذا لو كانت نتيجة OCR تحتوي على رموز غير مفهومة؟

الأسباب الشائعة هي انخفاض الدقة، الضوضاء الزائدة، أو خطوط غير مدعومة. جرّب:

- تكبير الصورة (`Bitmap` إعادة التحجيم).  
- تطبيق مرشح شحذ.  
- تحديد اللغة الصحيحة (كما هو موضح أعلاه).

### ماذا لو احتجت لمعالجة الصور بالتوازي؟

نظرًا لأن `OcrEngine` غير آمن للاستخدام عبر الخيوط، أنشئ **separate instance per thread** أو استخدم مجموعة محلية لكل خيط. مثال باستخدام `Parallel.ForEach`:

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine(); // each thread gets its own engine
    var img = Image.FromFile(path);
    string text = engine.Recognize(img);
    // Store or log 'text' as needed
});
```

## مثال عملي كامل

بدمج كل شيء معًا، إليك نسخة مختصرة يمكنك وضعها في مشروع Console جديد:

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialize OCR engine (single instance for this demo)
        OcrEngine engine = new OcrEngine();

        // Uncomment if you have a license file
        // engine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Path to the PNG you want to read
        string file = @"C:\Images\sample.png";

        // Load, optionally preprocess, then recognize
        using (Image img = Image.FromFile(file))
        {
            string text = engine.Recognize(img);
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(text);
        }
    }
}
```

Compile with `dotnet run` and watch the console print the extracted text. Simple, right? That’s the beauty of a well‑des

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}