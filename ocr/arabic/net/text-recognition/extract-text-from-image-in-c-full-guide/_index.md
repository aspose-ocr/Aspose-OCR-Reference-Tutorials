---
category: general
date: 2026-03-23
description: استخراج النص من الصورة باستخدام Aspose OCR في C# وتعلم كيفية إضافة مسجل
  وحدة التحكم لتوفير ملاحظات فورية.
draft: false
keywords:
- extract text from image
- add console logger
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR وإضافة مسجل وحدة التحكم
  لمراقبة العملية. دليل خطوة‑بخطوة بلغة C#.
og_title: استخراج النص من الصورة في C# – دليل برمجي كامل
tags:
- OCR
- C#
- logging
title: استخراج النص من الصورة في C# – دليل كامل
url: /ar/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة في C# – الدليل الكامل

هل تحتاج إلى **استخراج النص من الصورة** بسرعة وبشكل موثوق؟ مع Aspose OCR يمكنك فعل ذلك في بضع أسطر من C#.  
سنوضح لك أيضًا كيفية **إضافة مسجل وحدة التحكم** حتى تتمكن من مراقبة تقدم محرك OCR وهو يهمس مباشرة إلى الطرفية الخاصة بك.

تخيل أن لديك إيصالًا ممسوحًا ضوئيًا، أو ملاحظة مكتوبة بخط اليد، أو صفحة PDF محفوظة كملف PNG. تريد الأحرف الخام دون فتح واجهة مستخدم ضخمة. يشرح لك هذا الدليل خطوة بخطوة حلًا كاملًا يمكن نسخه ولصقه يعمل اليوم مع .NET 6+ وأحدث مكتبة Aspose OCR.

بحلول نهاية هذا الدليل ستتمكن من:

* تحميل ملف صورة وتشغيل OCR لاستخراج بيانات **استخراج النص من الصورة**.  
* ربط مسجل وحدة التحكم بـ Aspose AI لتتمكن من رؤية ما تفعله المكتبة خلف الكواليس.  
* تطبيق معالج ما بعد التصحيح الإملائي المدمج لتصحيح الأخطاء الإملائية في OCR.  

> **المتطلبات المسبقة** – بيئة تطوير .NET تعمل (Visual Studio 2022، VS Code، أو Rider)، .NET 6 SDK أو أحدث، ورخصة Aspose OCR (أو تجربة مجانية). لا توجد حزم طرف ثالث أخرى مطلوبة.

## ما ستحتاجه

| العنصر | لماذا يهم |
|------|----------------|
| **Aspose.OCR** NuGet package | يوفر فئة `OcrEngine` التي تقوم فعليًا بقراءة الصورة. |
| **Aspose.OCR.AI** NuGet package | يمنحك إطار عمل `AsposeAI` لمعالجة ما بعد التعرف، بما في ذلك تصحيح الإملاء. |
| **Microsoft.Extensions.Logging** (optional) | يوفر واجهة `ILogger` لخطوة **إضافة مسجل وحدة التحكم**. |
| **An input image** (`input.png`) | ملف المصدر الذي سنقوم منه **استخراج النص من الصورة**. |

يمكنك تثبيت الحزم عبر الطرفية:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

## الخطوة 1 – استخراج النص من الصورة باستخدام Aspose OCR

أول شيء نقوم به هو تمرير الصورة إلى محرك OCR. هذه الكتلة تقوم بالعمل الشاق وتعيد سلسلة نصية خام قد لا تزال تحتوي على أخطاء إملائية.

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**لماذا هذا يعمل:** `OcrEngine` يختصر جميع عمليات ما قبل معالجة الصورة منخفضة المستوى (التصنيف الثنائي، تصحيح الميل، إلخ). عندما تُعيد `Recognize()` القيمة `true`، تكون خاصية `Text` تحتوي بالفعل على أفضل تخمين للأحرف.  

> **نصيحة:** إذا كانت صورتك كبيرة، فكر في تغيير حجمها إلى ≤ 2000 px على الجانب الأطول قبل تمريرها إلى المحرك. هذا يسرّع المعالجة دون الإضرار بالدقة.

## الخطوة 2 – إضافة مسجل وحدة التحكم للحصول على رؤى في الوقت الحقيقي

الآن نضيف جزء **إضافة مسجل وحدة التحكم**. التسجيل ليس فقط للتصحيح؛ فهو يمنحك رؤية إلى تنزيلات النماذج، خطوات معالج AI، وأي تحذيرات قد تصدرها المكتبة.

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

يمكنك الآن توصيل هذا المسجل بـ Aspose AI:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

هذه هي ميزة **إضافة مسجل وحدة التحكم** – لن تتساءل أبدًا ما إذا كانت العملية الخلفية قد نجحت.

## الخطوة 3 – تكوين وتسجيل معالج ما بعد التصحيح الإملائي

تأتي Aspose AI مع معالج ما بعد التصحيح الإملائي المفيد الذي ينظف الأخطاء الشائعة في OCR (مثال: “rec0gn1ze” → “recognize”). سنقوم بتكوينه، وربما نخبر المكتبة بمكان تخزين النموذج، ثم نسجله.

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**لماذا قد ترغب في مسار مخصص:** في خطوط أنابيب CI/CD غالبًا ما تريد تخزين النماذج في دليل معروف لتجنب التنزيلات المتكررة. علم `AllowAutoDownload` يضمن تحميل النموذج في المرة الأولى التي تشغل فيها الكود.

## الخطوة 4 – تشغيل معالج ما بعد التعرف على نتيجة OCR

مع وجود نص OCR في المتناول ومعالج التصحيح الإملائي جاهز، نمرر السلسلة الخام إلى `AsposeAI`. يقوم المحرك بتشغيل النموذج، ويخزن المعالج النص المصحح داخليًا.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

بعد هذه الاستدعاء، يحتوي `spellProcessor` على مجموعة من كائنات `RecognitionResult`، كل منها يمتلك خاصية `RecognitionText` التي تحتوي على النسخة المنقحة.

## الخطوة 5 – استرجاع وعرض النص المصحح

أخيرًا نستخرج السلسلة المصححة من المعالج ونطبعها. هذه هي اللحظة التي ترى فيها الفائدة الحقيقية لكل من OCR و**إضافة مسجل وحدة التحكم**.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**المخرجات المتوقعة** (بافتراض أن الصورة تحتوي على العبارة “Aspose OCR demo” مع بعض الأخطاء في OCR):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

لاحظ كيف أخبرنا المسجل أن النموذج جاهز، وأن السطر المصحح يُقرأ بوضوح.

## الخطوة 6 – تنظيف الموارد

كلا من `AsposeAI` و `OcrEngine` ينفذان `IDisposable`. تحريرهما يفرغ الذاكرة الأصلية ومقابض الملفات، وهو أمر مهم خاصة في الخدمات التي تعمل لفترات طويلة.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد (`dotnet new console`). استبدل `"YOUR_DIRECTORY"` بمجلد فعلي على جهازك.

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}