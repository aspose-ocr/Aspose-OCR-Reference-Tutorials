---
category: general
date: 2026-05-02
description: دليل C# OCR يوضح كيفية استخراج نص من صورة باستخدام C# والتعرف على نص
  PNG، ثم كتابة JSON منسق باستخدام JsonSerializer في C#. دليل خطوة بخطوة للمطورين.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: ar
og_description: دروس OCR بلغة C# توضح كيفية استخراج النص من صورة باستخدام C# والتعرف
  على نص PNG، ثم كتابة JSON منسق باستخدام JsonSerializer في C#. مثال كامل وقابل للتنفيذ.
og_title: دليل c# OCR – استخراج النص وتصديره كـ JSON منسق
tags:
- OCR
- C#
- Aspose
- JSON
title: دليل C# OCR – استخراج النص من الصور وتصديره كـ JSON منسق
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – استخراج النص من الصور وتصديره كـ JSON منسق

هل احتجت يومًا إلى **c# ocr tutorial** يتحول من صورة نص إلى ملف JSON منسق بشكل جميل؟ لست وحدك. في العديد من المشاريع – مثل مسح الفواتير، تحليل الإيصالات، أو حتى استخراج نص من الميمات – ينتهي بك الأمر بملف PNG وتتساءل كيف تستخرج الكلمات دون كتابة مُعرّف مخصص.  

هذا الدليل يقدّم لك حلًا عمليًا: سنقوم **باستخراج نص صورة c#** باستخدام Aspose.OCR، **وتعرف نص png**، ثم **كتابة json منسق** باستخدام `JsonSerializer` في C#. في النهاية ستحصل على تطبيق console مستقل يمكنك إدراجه في أي حل .NET. لا روابط غامضة “انظر الوثائق”، بل مثال كامل جاهز للنسخ واللصق.

## ما ستحتاجه

- **.NET 6** (أو أي نسخة حديثة من .NET). الإطارات الأقدم تعمل، لكن الصياغة المعروضة تستهدف .NET 6+.
- **Aspose.OCR for .NET** – تثبيت عبر NuGet: `dotnet add package Aspose.OCR`.
- صورة PNG تجريبية (`text.png`) تحتوي على نص واضح يمكن قراءته آليًا.
- بيئة تطوير أو محرر من اختيارك – Visual Studio، VS Code، Rider، إلخ.

> **نصيحة احترافية:** إذا كنت تخطط لمعالجة عدد كبير من الصور، فكر في إعادة استخدام كائن `OcrEngine` واحد بدلاً من إنشاء كائن جديد لكل ملف. هذا يقلل الحمل ويحسّن الأداء.

## الخطوة 1: إعداد مشروع c# ocr tutorial

أولاً، أنشئ مشروع console. الأوامر التالية تُنشئ الهيكلية وتضيف مكتبة OCR:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

الآن افتح الملف `Program.cs` الذي تم إنشاؤه. سنستبدل محتوياته بالمثال الكامل لاحقًا، لكن الآن تأكد من أن المشروع يبني بدون أخطاء:

```bash
dotnet build
```

إذا لم تظهر أي أخطاء، فأنت جاهز للمتابعة.

## الخطوة 2: تعرف على نص PNG من صورة

قلب أي **c# ocr tutorial** هو محرك OCR نفسه. Aspose.OCR يخفّف التفاصيل منخفضة المستوى ويقدّم لك فئة `OcrEngine` نظيفة. أدناه نقوم بإنشاء المحرك، ونشير إلى ملف PNG، ونطلب منه التعرف على النص.

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### لماذا يعمل هذا

- **`RecognizeImage`** يدعم صيغًا متعددة (PNG، JPEG، BMP). نحن نستخدم **recognize png text** لأن PNG يحافظ على التفاصيل بدون فقد، وهو مثالي للـ OCR.
- كائن `OcrResult` المرتجع يحتوي ليس فقط على النص العادي بل أيضًا على درجة الثقة لكل حرف، ما يفيد إذا أردت تصفية الأحرف ذات الثقة المنخفضة لاحقًا.

## الخطوة 3: كتابة JSON منسق باستخدام JsonSerializer c#

الآن بعد أن حصلنا على `ocrResult`، الخطوة المنطقية التالية في **c# ocr tutorial** هي تحويل هذا الكائن إلى JSON قابل للقراءة. المُسلسل المدمج `System.Text.Json` يقوم بالمهمة، وسنُعدّه لكتابة **write indented json** للوضوح.

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### استخدام `JsonSerializer` بشكل صحيح

- علم `WriteIndented` هو أبسط طريقة لـ **write indented json** دون الحاجة إلى مكتبات خارجية.
- إذا احتجت أسماء خصائص بصيغة camel‑case، أضف `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` إلى الخيارات.
- يمكن حفظ السلسلة `jsonOutput` باستخدام `File.WriteAllText("result.json", jsonOutput);` – تعديل مفيد لسلاسل المعالجة الواقعية.

## الخطوة 4: تشغيل البرنامج والتحقق من النتيجة

قم بترجمة وتشغيل البرنامج:

```bash
dotnet run
```

بافتراض أن `text.png` يحتوي على العبارة *“Hello, OCR World!”*، يجب أن ترى شيئًا مشابهًا لـ:

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

ذلك الـ JSON **منسق**، مما يجعله سهل القراءة في السجلات أو لتسليمه إلى الخدمات المت downstream.

### الحالات الخاصة والنصائح

| Situation | What to Do |
|-----------|------------|
| **Image is blurry** | Increase `ocrEngine.Config.Dpi` (e.g., `ocrEngine.Config.Dpi = 300`) before calling `RecognizeImage`. |
| **Non‑English language** | Set `ocrEngine.Config.Language = OcrLanguage.German` (or any supported language). |
| **Large batch of files** | Loop over a directory, reusing the same `OcrEngine` instance; store each JSON result with a unique filename. |
| **Need only high‑confidence text** | Filter `ocrResult.Lines` where `Confidence` ≥ 0.95 before serialization. |

## مثال كامل جاهز (نسخ‑لصق)

فيما يلي البرنامج *كاملًا*، جاهزًا للإدراج في `Program.cs`. يتضمن جميع الخطوات، ومعالجة الأخطاء، وتعليقات تجعل الكود سهل الفهم.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

شغّل الكود، افحص وحدة التحكم أو ملف الـ `.json` المُولد، وسترى النص المستخرج مع درجات الثقة، كل ذلك **منسق**.

## الخلاصة

أصبح لديك الآن **c# ocr tutorial** قوي يوضح كيفية **extract text image c#**، **recognize png text**، و**write indented json** باستخدام `JsonSerializer`. المثال كامل، قابل للتنفيذ، ويتضمن نصائح عملية للسيناريوهات الواقعية.  

ما الخطوة التالية؟ جرّب استبدال Aspose.OCR بمحرك آخر (مثل Tesseract) ولاحظ كيف يتغيّر شكل `OcrResult`، أو أرسل الـ JSON إلى API لاحق يخزن بيانات OCR في قاعدة بيانات. يمكنك أيضًا تجربة **use jsonserializer c#** مع محولات مخصصة لتنسيق التواريخ أو التعامل مع الـ enum.

برمجة سعيدة، ولتكن خطوط OCR الخاصة بك دقيقة دائمًا!  

---  

![دليل c# ocr diagram](image.png "مخطط يوضح تدفق OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}