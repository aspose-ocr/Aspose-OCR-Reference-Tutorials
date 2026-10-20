---
category: general
date: 2026-03-28
description: تعلم كيفية التعرف على النص من الصورة واستخراج النص من المسح الضوئي في
  C# باستخدام Aspose OCR مع تسريع GPU. دليل OCR سريع ودقيق.
draft: false
keywords:
- recognize text from image
- extract text from scan
- c# read image file
- aspose ocr tutorial c#
language: ar
og_description: تعلم كيفية التعرف على النص من الصورة واستخراج النص من المسح الضوئي
  في C# باستخدام Aspose OCR مع تسريع GPU. دليل OCR سريع ودقيق.
og_title: التعرف على النص من الصورة في C# – دليل Aspose OCR الكامل
tags:
- Aspose OCR
- C#
- GPU acceleration
title: التعرف على النص من الصورة في C# – دليل Aspose OCR الكامل
url: /ar/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في C# – دليل Aspose OCR الكامل

هل احتجت يومًا إلى **التعرف على النص من صورة** لكنك لم تكن متأكدًا أي مكتبة ستمنحك السرعة والدقة معًا؟ لست وحدك—المطورون يسألون باستمرار: “كيف يمكنني استخراج النص من مسح ضوئي دون كتابة شبكة عصبية مخصصة؟” الخبر السار هو أن Aspose OCR يقوم بالعمل الشاق، ومع امتداد الـ GPU يمكنك تسريع العملية بشكل كبير.

في هذا الدليل سنستعرض كل ما تحتاجه لتبدأ العمل: من تثبيت حزم NuGet المناسبة، إلى تحميل ملف TIFF أو JPEG، وتمكين دعم الـ GPU، وأخيرًا استخراج السلسلة المتعرف عليها من الملف. في النهاية ستتمكن من **c# read image file** وتحويل أي مستند ممسوح ضوئيًا إلى نص قابل للبحث ببضع أسطر من الشيفرة فقط.

> **ما ستحصل عليه**  
> * تطبيق كونسول C# يعمل على التعرف على النص من ملفات الصور.  
> * فهم لماذا تسريع الـ GPU مهم للمسحات الكبيرة.  
> * نصائح للتعامل مع المشكلات الشائعة عند **extract text from scan**.

---

## المتطلبات المسبقة – ما تحتاجه قبل البدء

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| .NET 6.0 SDK (أو أحدث) | Aspose OCR يستهدف .NET Standard 2.0+، لذا فإن أطر التشغيل الحديثة تضمن التوافق. |
| Visual Studio 2022 (أو أي بيئة تطوير تفضلها) | تجعل عملية التصحيح وإدارة الحزم سهلة وسلسة. |
| حزم NuGet **Aspose.OCR** و **Aspose.OCR.GPU** | محرك OCR الأساسي موجود في `Aspose.OCR`؛ وواجهات برمجة التطبيقات الخاصة بالـ GPU في `Aspose.OCR.GPU`. |
| صورة نموذجية (مثال: `large_scan.tif`) | سنستخدم مثالًا على ملف TIFF متعدد الميغابايت لتوضيح تحسين الأداء. |

يمكنك تثبيت الحزم باستخدام سطر أوامر NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.GPU
```

> **نصيحة احترافية:** إذا كنت على Windows وتفضل الواجهة الرسومية، افتح **NuGet Package Manager** في Visual Studio وابحث عن “Aspose OCR”.

---

## الخطوة 1 – تحميل ملف الصورة (c# read image file)

أول شيء هو قراءة الصورة إلى الذاكرة. Aspose OCR يعمل مع `System.Drawing.Image`، لذا ستحتاج إلى إشارة إلى `System.Drawing.Common` إذا كنت تستخدم .NET Core.

```csharp
using System;
using System.Drawing;               // For Image class
using Aspose.OCR;
using Aspose.OCR.GPU;                // GPU extension namespace

class GpuExample
{
    static void Main()
    {
        // 👉 Load the image you want to recognize (any supported format)
        var imagePath = @"YOUR_DIRECTORY\large_scan.tif";
        Image image = Image.FromFile(imagePath);
```

> **لماذا هذه الخطوة؟**  
> تحميل الملف يمنح محرك OCR صورة bitmap يمكنه تحليلها. استخدام `Image.FromFile` يضمن فك ترميز الصورة بالكامل، وهو أمر أساسي لتقسيم الأحرف بدقة.

---

## الخطوة 2 – تهيئة محرك OCR وتمكين الـ GPU

الآن بعد أن أصبحت الـ bitmap في يدك، أنشئ كائن `OcrEngine`. بشكل افتراضي يعمل المحرك على الـ CPU، وهذا يكفي للقطات الشاشة الصغيرة. بالنسبة للمسحات الضخمة—مثل ملفات PDF بدقة 300 dpi—تشغيل الـ GPU يقلل وقت المعالجة بشكل كبير.

```csharp
        // 👉 Create the OCR engine and enable GPU acceleration for better performance
        var ocrEngine = new OcrEngine();

        // The UseGpu method toggles GPU mode. Pass true to enable.
        ocrEngine.UseGpu(true);
```

> **ما الذي يحدث خلف الكواليس؟**  
> عندما يتم استدعاء `UseGpu(true)`، يقوم Aspose بتحميل نوى CUDA (إذا كان هناك GPU متوافق). ثم تُنفّذ خطوط أنابيب OCR—المعالجة المسبقة، التقسيم، التصنيف—على بطاقة الرسوميات، مستفيدًا من آلاف الأنوية بدلاً من عدد قليل من خيوط الـ CPU.  
> 
> **حالة خاصة:** إذا لم يتمكن وقت التشغيل من العثور على GPU مناسب، فإن `UseGpu(true)` يعود صامتًا إلى وضع الـ CPU. يمكنك التحقق من الوضع الفعلي باستخدام `ocrEngine.IsGpuEnabled`.

---

## الخطوة 3 – التعرف على النص من الصورة

مع تهيئة المحرك، يصبح التعرف الفعلي استدعاء طريقة واحدة فقط. النتيجة هي سلسلة نصية عادية يمكنك تسجيلها، حفظها، أو تمريرها إلى فهرس بحث.

```csharp
        // 👉 Run the recognition and capture the extracted text
        string recognizedText = ocrEngine.Recognize(image);

        // Display the output
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

**الناتج المتوقع** (مقتطع للسهولة):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total Amount: $1,250.00
...
```

إذا كان المسح يحتوي على لغات متعددة، يمكنك ضبط `ocrEngine.Language` قبل استدعاء `Recognize`. بشكل افتراضي يتم الكشف التلقائي عن اللغة الإنجليزية.

---

## الخطوة 4 – التحقق من النتائج ومعالجة المشكلات الشائعة

التعرف نادرًا ما يكون مثاليًا، خاصةً مع المسحات الضوضائية. إليك بعض الفحوصات السريعة التي يمكنك إضافتها:

```csharp
        // Simple validation: ensure we got something non‑empty
        if (string.IsNullOrWhiteSpace(recognizedText))
        {
            Console.WriteLine("⚠️ No text was detected. Check image quality or try disabling GPU.");
        }
        else
        {
            // Optional: write to a .txt file for later processing
            System.IO.File.WriteAllText("output.txt", recognizedText);
        }
```

**لماذا نضيف هذا؟**  
قد تتخطى خطوط أنابيب المعالجة المسرّعة بالـ GPU بعض خطوات المعالجة المسبقة التي تساعد في تحسين الصور منخفضة التباين. الرجوع إلى الـ CPU (`ocrEngine.UseGpu(false)`) قد يحسن الدقة للملفات التي تواجه مشاكل.

---

## الخطوة 5 – مثال كامل جاهز للنسخ واللصق

فيما يلي البرنامج الكامل، جاهز للترجمة. ما عليك سوى استبدال `YOUR_DIRECTORY` بمسار المجلد الذي يحتوي على صورتك.

```csharp
using System;
using System.Drawing;               // System.Drawing.Common for .NET Core
using Aspose.OCR;
using Aspose.OCR.GPU;                // GPU extension namespace

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Load the image (c# read image file)
        var imagePath = @"YOUR_DIRECTORY\large_scan.tif";
        Image image = Image.FromFile(imagePath);

        // 2️⃣ Initialise OCR engine and enable GPU
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpu(true);               // Turn on GPU acceleration

        // 3️⃣ Recognise text from image
        string recognizedText = ocrEngine.Recognize(image);

        // 4️⃣ Output and simple validation
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);

        if (string.IsNullOrWhiteSpace(recognizedText))
        {
            Console.WriteLine("⚠️ No text detected – consider checking image quality or disabling GPU.");
        }
        else
        {
            System.IO.File.WriteAllText("output.txt", recognizedText);
        }
    }
}
```

احفظه كـ `Program.cs`، شغّله باستخدام `dotnet run`، وسترى النص المستخرج يُطبع على وحدة التحكم ويُحفظ في `output.txt`.

---

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا على Linux؟**  
ج: نعم. Aspose OCR متعدد المنصات، لكنك تحتاج إلى حزمة `libgdiplus` لدعم `System.Drawing` على Linux. ثبّتها عبر `apt-get install libgdiplus`.

**س: الـ GPU الخاص بي غير مُعترف به—ماذا أفعل الآن؟**  
ج: تأكد من تثبيت برنامج تشغيل NVIDIA وأدوات CUDA. يمكنك أيضًا استدعاء `ocrEngine.IsGpuSupported` للكشف البرمجي عن الدعم.

**س: هل يمكنني استخراج النص من ملف PDF متعدد الصفحات؟**  
ج: حوّل كل صفحة إلى صورة أولًا (`Aspose.PDF` أو `PdfSharp` يمكن أن يساعدا)، ثم مرّر كل صورة إلى حلقة OCR الموضحة أعلاه.

**س: ما مدى دقة Aspose OCR مقارنةً بـ Tesseract؟**  
ج: في معظم الاختبارات، يوازي Aspose OCR أو يتفوق على دقة Tesseract، خاصةً في المسحات منخفضة الدقة، مع توفير واجهة برمجة أبسط وتسريع مدمج بالـ GPU.

---

## الخاتمة

أصبح لديك الآن **مثال كامل وقابل للتنفيذ** يوضح كيفية **التعرف على النص من صورة** باستخدام Aspose OCR مع تسريع الـ GPU. باتباع الخطوات أعلاه يمكنك استخراج النص من المستندات الممسوحة ضوئيًا بثقة، دمجه في قواعد البيانات، أو إرساله إلى خطوط أنابيب AI لاحقة.

هل أنت مستعد للتحدي التالي؟ جرّب معالجة دفعة من الصور بالتوازي، جرب حزم اللغات، أو اجمع مخرجات OCR مع معالجة اللغة الطبيعية لتصنيف الفواتير تلقائيًا. السماء هي الحد—برمجة سعيدة!

---

![recognize text from image](/images/ocr-sample.png "recognize text from image example")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}