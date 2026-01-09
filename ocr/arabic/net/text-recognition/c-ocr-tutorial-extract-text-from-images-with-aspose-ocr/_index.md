---
category: general
date: 2026-01-09
description: دروس C# OCR تُظهر كيفية استخراج النص من ملفات الصور، التعرف على النص
  من PNG، تحويل الصورة إلى سلسلة نصية، واكتشاف اللغة تلقائيًا باستخدام Aspose.OCR.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from png
- convert image to string
- detect language automatically
language: ar
og_description: دليل C# OCR يشرح لك كيفية استخراج النص من الصور، التعرف على النص من
  ملفات PNG، تحويل الصور إلى سلاسل نصية، واكتشاف اللغة تلقائيًا باستخدام Aspose OCR.
og_title: دليل c# OCR – استخراج النص من الصور
tags:
- C#
- OCR
- Aspose
- Image Processing
title: دورة C# OCR – استخراج النص من الصور باستخدام Aspose OCR
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# ocr – استخراج النص من الصور باستخدام Aspose OCR

هل احتجت إلى **دليل c# ocr** يعمل فعليًا على ملف PNG حقيقي؟ ربما تقوم بإنشاء ماسح فواتير، أو معالج نماذج متعدد اللغات، أو مجرد فضول حول كيفية تحويل صورة نص إلى سلسلة قابلة للبحث. مهما كان السبب، فأنت في المكان الصحيح.

في هذا الدليل سنوضح لك خطوة بخطوة كيفية **استخراج النص من ملف صورة**، **التعرف على النص من png**، **تحويل الصورة إلى سلسلة**، وحتى **اكتشاف اللغة تلقائيًا** — كل ذلك باستخدام مكتبة Aspose.OCR. لا مراجع غامضة، مجرد مثال كامل قابل للتنفيذ يمكنك نسخه ولصقه في Visual Studio.

## ما الذي ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا)  
- إشارة NuGet إلى `Aspose.OCR` (الإصدار 23.9 أو أحدث)  
- ملف صورة (`mixed‑script.png` في هذا المثال) موجود في مكان يمكن للتطبيق قراءته  
- فهم أساسي للغة C# (إذا كتبت برنامج "Hello World"، فأنت جاهز)

> **نصيحة محترف:** إذا لم يكن لديك ترخيص بعد، تقدم Aspose ترخيصًا مؤقتًا مجانيًا للاختبار. ما عليك سوى وضع ملف `.lic` بجوار الملف التنفيذي.

## الخطوة 1 – تثبيت حزمة Aspose.OCR عبر NuGet

أولاً، أضف المكتبة إلى مشروعك. افتح Package Manager Console وشغّل:

```powershell
Install-Package Aspose.OCR
```

أو، إذا كنت تفضّل الواجهة الرسومية، انقر بزر الماوس الأيمن على *Dependencies → Manage NuGet Packages* وابحث عن **Aspose.OCR**.

## الخطوة 2 – إعداد محرك OCR (c# ocr tutorial core)

الآن سننشئ كائن `OcrEngine`، نحدده لاكتشاف اللغة تلقائيًا، ونشير به إلى ملف PNG الخاص بنا.

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Step 2.1: Initialise the OCR engine – this is the heart of the c# ocr tutorial
        var ocrEngine = new OcrEngine();

        // Step 2.2: Let the engine decide which language(s) are present.
        // AutoDetect is the default, but we set it explicitly for clarity.
        ocrEngine.Language = OcrLanguage.AutoDetect;

        // Step 2.3: Path to the image you want to process.
        // Replace with your own path if needed.
        string imagePath = @"C:\Images\mixed-script.png";

        // Step 2.4: Run the recognition.
        string recognizedText = ocrEngine.RecognizeImage(imagePath);

        // Step 2.5: Output the result – this is where we **convert image to string**.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### لماذا نعيّن `Language = OcrLanguage.AutoDetect`

اكتشاف اللغة تلقائيًا يحفظك من التخمين ما إذا كانت الصورة تحتوي على الإنجليزية، الروسية، العربية، أو مزيج منها. إنه الخيار الأكثر مرونة لسيناريو **detect language automatically**، ويعمل مباشرةً لمعظم النصوص التي تدعمها Aspose.

## الخطوة 3 – تشغيل التطبيق والتحقق من المخرجات

قم بترجمة البرنامج وتشغيله (`dotnet run` أو اضغط **F5** في Visual Studio). إذا تم ربط كل شيء بشكل صحيح، سترى شيئًا مشابهًا لـ:

```
=== Recognized Text ===
Hello World!
Привет мир!
مرحبا بالعالم!
```

تثبت هذه النتيجة أننا نجحنا في **استخراج النص من الصورة**، **التعرف على النص من png**، و**تحويل الصورة إلى سلسلة** — كل ذلك في مقتطف واحد مختصر.

## الخطوة 4 – تنويعات شائعة وحالات حافة

### معالجة صور متعددة

إذا كنت بحاجة لمعالجة مجلد يحتوي على PNGs، غلف استدعاء التعرف داخل حلقة `foreach`:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Images", "*.png"))
{
    string text = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"[{Path.GetFileName(file)}] => {text}");
}
```

### تحديد لغة ثابتة

أحيانًا تعرف اللغة مسبقًا (مثلاً الإنجليزية فقط). يمكنك استبدال `AutoDetect` بـ `OcrLanguage.English` لتسريع المعالجة:

```csharp
ocrEngine.Language = OcrLanguage.English;
```

### التعامل مع مسحات منخفضة الجودة

توفر Aspose.OCR خيارات ما قبل المعالجة (تقليل الضوضاء، تصحيح الميل). لتصحيح سريع:

```csharp
ocrEngine.ImagePreprocessingOptions.Deskew = true;
ocrEngine.ImagePreprocessingOptions.RemoveNoise = true;
```

### حفظ النتيجة إلى ملف

بدلاً من الطباعة على وحدة التحكم، قد ترغب في كتابة النص المستخرج إلى ملف `.txt`:

```csharp
File.WriteAllText(@"C:\Output\recognized.txt", recognizedText);
```

## الخطوة 5 – مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي **البرنامج الكامل** بما في ذلك المعالجة المسبقة الاختيارية ومنطق حفظ الملف. لا تتردد في تعديل المسارات.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class OcrDemo
{
    static void Main()
    {
        // Initialise engine
        var ocrEngine = new OcrEngine
        {
            // Auto‑detect language (detect language automatically)
            Language = OcrLanguage.AutoDetect,

            // Optional: improve accuracy on noisy scans
            ImagePreprocessingOptions = {
                Deskew = true,
                RemoveNoise = true
            }
        };

        // Input image – change to your own file
        string inputPath = @"C:\Images\mixed-script.png";

        // Perform OCR
        string extractedText = ocrEngine.RecognizeImage(inputPath);

        // Display on console (convert image to string)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);

        // Save to a text file for later use
        string outputPath = Path.ChangeExtension(inputPath, ".txt");
        File.WriteAllText(outputPath, extractedText);
        Console.WriteLine($"\nText saved to: {outputPath}");
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج على PNG يحتوي على الإنجليزية، الروسية، والعربية ينتج:

```
=== OCR Result ===
Hello World!
Привет мир!
مرحبا بالعالم!

Text saved to: C:\Images\mixed-script.txt
```

إذا كانت الصورة فارغة أو غير قابلة للقراءة، يُعيد المحرك سلسلة فارغة — عالج هذه الحالة بالتحقق من `string.IsNullOrWhiteSpace(extractedText)` قبل المتابعة.

## الأسئلة المتكررة (FAQs)

**س: هل يدعم Aspose.OCR النص المكتوب بخط اليد؟**  
ج: يركز على OCR المطبع. للكتابة اليدوية تحتاج نموذج ML مخصص أو خدمة مثل Azure Computer Vision.

**س: هل يمكن تشغيله على Linux/macOS؟**  
ج: بالتأكيد. Aspose.OCR متعدد المنصات؛ فقط قم بتثبيت .NET runtime لنظامك.

**س: ماذا لو أردت معالجة ملفات PDF بدلاً من PNGs؟**  
ج: حوّل كل صفحة PDF إلى صورة أولًا (مثلاً باستخدام `Aspose.PDF`) ثم مرّر الصورة إلى محرك OCR.

## الخلاصة

لقد أتممنا الآن **دليل c# ocr** الذي يشرح لك **استخراج النص من ملفات الصورة**، **التعرف على النص من png**، **تحويل الصورة إلى سلسلة**، و**اكتشاف اللغة تلقائيًا** باستخدام Aspose.OCR. الكود قصير، المفاهيم واضحة، ويمكنك توسيعه لمعالجة دفعات، إعدادات لغة مخصصة، أو دمجه في واجهة برمجة تطبيقات ويب.

ما الخطوة التالية؟ جرّب إمداد مخرجات OCR إلى فهرس بحث، أو إلى خدمة ترجمة، أو دمجها مع Azure Cognitive Services للحصول على خطوط بيانات أكثر غنى. السماء هي الحد بمجرد إتقانك أساسيات تحويل الصورة إلى نص في C#.

برمجة سعيدة، ولا تنس تجربة جودة صور مختلفة — محرك OCR سيشكرك! 

![دليل c# ocr – مثال على ناتج OCR على PNG متعدد النصوص](placeholder-image.png "دليل c# ocr – لقطة شاشة لنتيجة OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}