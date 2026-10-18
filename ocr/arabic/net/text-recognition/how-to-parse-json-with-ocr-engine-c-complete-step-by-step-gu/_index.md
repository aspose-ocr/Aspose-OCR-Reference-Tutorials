---
category: general
date: 2026-03-17
description: تعلم كيفية تحليل JSON من نتائج OCR في C#. يغطي هذا الدرس كيفية استخراج
  النص، تحميل الصورة للتعرف الضوئي على الأحرف، تشغيل التعرف الضوئي على الأحرف، واستخدام
  محرك OCR في C# بكفاءة.
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: ar
og_description: كيفية تحليل JSON من مخرجات OCR في C#. اتبع دليلنا لاستخراج النص، وتحميل
  الصورة للتعرف الضوئي على الأحرف، وتشغيل التعرف الضوئي على الأحرف، واستخدام محرك
  OCR في C#.
og_title: كيفية تحليل JSON باستخدام محرك OCR في C# – دليل كامل
tags:
- C#
- OCR
- JSON
- Image Processing
title: كيفية تحليل JSON باستخدام محرك OCR في C# – دليل خطوة بخطوة كامل
url: /ar/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحليل JSON باستخدام محرك OCR C# – دليل خطوة بخطوة كامل

هل تساءلت يومًا **how to parse json** التي تأتي مباشرةً من محرك OCR؟ لست وحدك. يواجه معظم المطورين نفس المشكلة — الحصول على JSON الخام، ثم معرفة أفضل طريقة لاستخراج الأجزاء المفيدة مثل درجات الثقة أو النص الفعلي. في هذا الدليل سنستعرض تحميل صورة لـ OCR، تشغيل التعرف على النص، وأخيرًا **how to parse json** بطريقة نظيفة وقابلة للصيانة.

بنهاية البرنامج التعليمي ستتمكن من:

* تحميل صورة لـ OCR ببضع أسطر من الشيفرة فقط.  
* تشغيل التعرف على النص باستخدام محرك OCR مكتوب بـ C#.  
* **How to extract text** وغيرها من البيانات الوصفية من حمولة JSON.  
* معالجة الحالات الشاذة الشائعة (حقول مفقودة، صيغ غير متوقعة) دون حدوث تعطل.

لا حاجة إلى وثائق خارجية — كل ما تحتاجه موجود هنا.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

* .NET 6.0 أو أحدث (الشيفرة تُجمّع أيضًا على .NET Framework 4.7+).  
* إشارة إلى مكتبة OCR التي تستخدمها (المثال يستخدم فئة `OcrEngine` افتراضية).  
* حزمة NuGet `Newtonsoft.Json` لمعالجة JSON (`Install-Package Newtonsoft.Json`).  
* ملف صورة (مثال: `passport.png`) موجود في مكان يمكن لتطبيقك قراءته.

> **نصيحة احترافية:** إذا كنت تستخدم SDK تجاريًا لـ OCR، تحقق من تمكين صيغة إخراج JSON — معظم البائعين يتيحون ذلك عبر خاصية إعداد مثل `ocrEngine.Config.OutputFormat`.

## الخطوة 1 – إنشاء وتكوين محرك OCR (الكلمة المفتاحية الأساسية في العمل)

أول شيء تحتاج إلى القيام به هو إنشاء نسخة من محرك OCR وإخبارها بإرجاع JSON. هنا تظهر عبارة **how to parse json** لأول مرة في شيفرتنا، لأن المحرك سيعطينا سلسلة JSON سنقوم بتحليلها لاحقًا.

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**لماذا هذا مهم:** ضبط `OutputFormat` إلى `Json` يضمن أن الاستجابة تحتوي على النص المعترف به **وأيضًا** البيانات الوصفية المفيدة مثل درجات الثقة. إذا نسيت هذه الخطوة ستحصل على نص عادي بدلاً من ذلك، وتصبح **how to parse json** مسألة غير ذات صلة.

## الخطوة 2 – تحميل صورة لـ OCR

الآن نقوم بتحميل الصورة التي نريد تحليلها. هذه هي النقطة التي يبرز فيها الكلمة المفتاحية الثانوية **load image for OCR**.

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **ماذا لو الملف غير موجود؟** احطِ الاستدعاء بـ `try/catch` واظهر رسالة ودية — لن يتعطل تطبيقك وسيتعرف المستخدم على ما حدث.

## الخطوة 3 – تشغيل التعرف على النص

مع جاهزية المحرك وتحميل الصورة، الخطوة المنطقية التالية هي تشغيل عملية التعرف فعليًا. هذا يحقق الكلمة المفتاحية الثانوية **run OCR recognition**.

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

خاصية `ocrResult.Text` الآن تحتوي على سلسلة JSON. إذا طبعتها إلى وحدة التحكم سترى شيئًا مثل:

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## الخطوة 4 – كيفية استخراج النص (وحقول أخرى) من JSON

هذا هو جوهر البرنامج التعليمي: **how to parse json** و **how to extract text** من حمولة OCR. سنستخدم `Newtonsoft.Json.Linq.JObject` لمرونته.

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**لماذا نستخدم `JObject`؟** يسمح لك بالتنقل بأمان في شجرة JSON دون تعريف فئة نموذج C# كاملة. عوامل الشرطية `?.` تحميك من `NullReferenceException` إذا ما حذف محرك OCR حقلًا ما.

### معالجة الحالات الشاذة

* **الحقول المفقودة:** نمط `?.Value<T>() ?? default` يعيد قيمة احتياطية منطقية.  
* **صفحات متعددة:** كرّر عبر `jsonObject["Pages"]` إذا كنت تتوقع أكثر من صفحة واحدة.  
* **ثقة غير رقمية:** استخدم `double.TryParse` إذا كان الـ SDK أحيانًا يُعيد قيمة نصية.

## الخطوة 5 – تجميع كل شيء في طريقة قابلة لإعادة الاستخدام

لتجنب نسخ ولصق الكود المتكرر، احزم التدفق بالكامل في طريقة مساعدة. هذا أيضًا يوضح **use OCR engine C#** بطريقة نظيفة وقابلة لإعادة الاستخدام.

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

الآن يمكنك استدعاء `RunOcrAndParseJson(@"C:\Images\passport.png");` من `Main` أو أي جزء آخر من تطبيقك.

## مثال كامل يعمل

فيما يلي برنامج كونسول كامل، مستقل، يمكنك نسخه ولصقه في مشروع `.csproj` جديد. يتضمن جميع الأجزاء التي ناقشناها، بالإضافة إلى قليل من معالجة الأخطاء.

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**الناتج المتوقع** (بافتراض نجاح OCR):

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

إذا تعذّر قراءة الصورة، سيُطلق الـ SDK استثناءً نلتقطه في `Main`، ونطبع رسالة خطأ ودية بدلاً من التعطل.

## الأسئلة المتكررة (FAQs)

**س: ماذا لو أعاد محرك OCR مصفوفة من الصفحات؟**  
ج: كرّر عبر `json["Pages"]` وادمج كل قيمة `["Text"]`، أو عالجها بشكل منفصل حسب حالتك.

**س: هل يمكنني تحويل JSON إلى فئة C# ذات نوع محدد؟**  
ج: بالتأكيد. عرّف بنية فئة تتطابق مع مخطط JSON واستخدم `JsonConvert.DeserializeObject<YourRootClass>(result.Text)`. يمنحك ذلك أمانًا في وقت التجميع لكنه يتطلب إبقاء النموذج متزامنًا مع مخرجات الـ SDK.

**س: هل يعمل هذا مع واجهات OCR غير المتزامنة (async)؟**  
ج: نعم. استبدل `engine.Recognize()` بـ `await engine.RecognizeAsync()` واجعل `RunOcrAndParseJson` من النوع `async Task`. يبقى جزء تحليل JSON كما هو.

**س: كيف أحفظ JSON في ملف للتحليل لاحقًا؟**  
ج: بعد استرجاع `result.Text`، استدعِ `File.WriteAllText(@"output.json", result.Text);`. يمكنك بعدها إعادة تحميله باستخدام `JObject.Parse(File.ReadAllText(...))`.

## التالي

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}