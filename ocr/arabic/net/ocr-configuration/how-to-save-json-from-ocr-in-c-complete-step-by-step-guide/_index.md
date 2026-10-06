---
category: general
date: 2026-03-02
description: تعلم كيفية حفظ JSON أثناء استخراج النص من الصورة باستخدام Aspose OCR.
  يتضمن كود كتابة ملف JSON، ونصائح تحميل صورة bitmap، ومثال كامل بلغة C#.
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: ar
og_description: اكتشف كيفية حفظ JSON أثناء استخراج النص من الصورة باستخدام Aspose
  OCR. كود C# كامل، خطوات كتابة ملف JSON، ونصائح عملية.
og_title: كيفية حفظ JSON من OCR في C# – دليل برمجي كامل
tags:
- C#
- OCR
- Aspose
- JSON
title: كيفية حفظ JSON من OCR في C# – دليل خطوة بخطوة كامل
url: /ar/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ JSON من OCR في C# – دليل خطوة بخطوة كامل

هل تساءلت يومًا **كيفية حفظ JSON** الذي يحتوي على النص الذي استخرجته للتو من صورة؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى *استخراج النص من صورة* ثم حفظ تلك المعلومات كملف JSON منسق بشكل أنيق. الخبر السار؟ الحل بسيط إلى حد كبير بمجرد أن تكون لديك الأدوات المناسبة.

في هذا الدرس سنستعرض سيناريو واقعي: استخدام Aspose.OCR **لاستخراج النص من صورة**، ثم **كتابة ملف JSON**، وأخيرًا **كيفية حفظ JSON** على القرص. على طول الطريق سنظهر لك أيضًا **كيفية تحميل صورة bitmap** بشكل صحيح، وسنغطي بعض الحالات الخاصة التي قد تواجهها. في النهاية ستحصل على تطبيق C# Console مستقل يقوم بكل شيء من تحميل الصورة إلى إنتاج وثيقة JSON جاهزة للاستخدام.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا)
- Aspose.OCR for .NET (يمكنك الحصول على حزمة تجريبية مجانية عبر NuGet)
- صورة PNG أو JPG تجريبية تحتوي على نص إنجليزي
- Visual Studio أو VS Code أو أي بيئة تطوير متوافقة مع C#

لا توجد مكتبات إضافية مطلوبة—فقط مساحة الاسم القياسية `System.Drawing` لمعالجة الـ bitmap و `System.Text.Json` للتسلسل.

---

## الخطوة 1 – تحميل صورة الـ Bitmap (جزء “load bitmap image”)

قبل أن يتم أي OCR، يجب جلب الصورة إلى الذاكرة ككائن `Bitmap`. فكر في ذلك كفتح كتاب قبل أن تبدأ بقراءة صفحاته.

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **نصيحة احترافية:** إذا كانت الصورة كبيرة، فكر في تغيير حجمها أولاً لتحسين الأداء. يعمل محرك OCR أسرع على الصور التي يقل حجمها عن 2 ميغابايت.

---

## الخطوة 2 – تكوين محرك Aspose OCR

الآن بعد أن أصبحت الـ bitmap جاهزة، نحتاج إلى `OcrEngine`. هذا الكائن يعرف **كيفية استخراج النص من صورة** ويمكنه أيضًا تزويدنا ببيانات هندسية مثل الصناديق المحيطة.

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

لماذا نفعّل `ExportBoundingBoxes`؟ إذا احتجت يومًا لتسليط الضوء على الكلمات في واجهة المستخدم، فإن هذه الإحداثيات ثمينة. إذا لم تكن بحاجة إليها، يمكنك ضبط العلامة على `false` وسيصبح الـ JSON أصغر قليلًا.

---

## الخطوة 3 – تنفيذ OCR والحصول على نتيجة منظمة

مع تكوين المحرك، الخطوة التالية هي عملية **كيفية استخراج النص** الفعلية. تُعيد طريقة `RecognizeToOcrResult` كائنًا غنيًا يحتوي على النص المعترف به، درجات الثقة، وبيانات التخطيط الاختيارية.

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

المتغير `ocrResult` الآن يحمل كل ما تحتاجه. إذا فحصته في المصحح، ستلاحظ تسلسل هرمي لكائنات `Page` و `Paragraph` و `Line` و `Word`، كل منها يمتلك خاصية `Text` الخاصة به.

---

## الخطوة 4 – تسلسل النتيجة إلى سلسلة JSON منسقة

هنا يبدأ سحر **كيفية حفظ json** حقًا. سنستخدم `System.Text.Json` لأنه مدمج، سريع، ويدعم التنسيق الجميل مباشرةً.

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

إذا كنت تحتاج إلى نمط تسمية مختلف (مثلاً camelCase)، فقط أضف `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` إلى الخيارات.

---

## الخطوة 5 – كتابة JSON إلى القرص (خطوة “write json file”)

أخيرًا، نحن فعليًا **نكتب ملف JSON** إلى نظام الملفات. هذا هو الجواب الملموس على **كيفية حفظ json** في بيئة C#.

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

بعد تنفيذ هذا السطر، ستجد ملف `sample-page.json` منسقًا بشكل جميل بجوار الصورة الأصلية. افتحه بأي محرر نصوص أو مرره إلى خدمة أخرى—بيانات OCR الآن قابلة للنقل.

---

## الخطوة 6 – التحقق من النتيجة (ماذا يجب أن ترى؟)

تشغيل البرنامج يجب أن يطبع تأكيدًا قصيرًا في وحدة التحكم:

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

افتح ملف JSON المُولد وسترى شيئًا مثل:

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

إذا كانت العلامة `ExportBoundingBoxes` مفعلة، سيتضمن كل كلمة إحداثيات `Rectangle`. هذا مفيد للعمل على واجهات المستخدم اللاحقة.

---

## أسئلة شائعة وحالات حافة

### ماذا لو كان مسار الصورة غير صالح؟

غلف تحميل الـ bitmap داخل كتلة `try/catch` واعرض خطأ واضح:

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### كيف أتعامل مع اللغات غير الإنجليزية؟

فقط غير خاصية `Language`:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

تدعم Aspose أكثر من 50 لغة، لذا اختر اللغة التي تتطابق مع مصدر النص الخاص بك.

### هل يجب علي تحرير كائنات `Bitmap`؟

نعم. `Bitmap` يطبق `IDisposable`، لذا غلفه بعبارة `using` لتحرير الموارد الأصلية فورًا.

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### ماذا لو أردت JSON مضغوط بدون تنسيق؟

بدّل `JsonSerializerOptions`:

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

هذا يقلل من حجم الملف—مفيد في السيناريوهات ذات النطاق الترددي المحدود.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يجمع جميع الخطوات، معالجة الأخطاء، ونصائح أفضل الممارسات التي نوقشت أعلاه. احفظه باسم `Program.cs` وشغّله من سطر الأوامر أو بيئة التطوير الخاصة بك.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**ما يفعله هذا البرنامج:**  
1. يتحقق من وجود الصورة.  
2. يحملها بأمان داخل كتلة `using`.  
3. ينفّذ OCR **لاستخراج النص من صورة**.  
4. يسلسل النتيجة إلى سلسلة JSON منسقة بشكل جميل.  
5. يحفظ تلك السلسلة على القرص، مجيبًا على السؤال الأساسي **كيفية حفظ json**.

شغّل `dotnet run` (أو اضغط F5 في Visual Studio) وسترى رسالة التأكيد بمجرد كتابة الملف.

---

## الخاتمة

أصبح لديك الآن وصفة كاملة وجاهزة للإنتاج لـ **كيفية حفظ JSON** الناتج عن استخراج النص باستخدام OCR. من تحميل صورة bitmap إلى كتابة ملف JSON نظيف، كل خطوة موضحة مع “السبب” وراء الكود، حتى تتمكن من تعديل الحل ليتناسب مع مشاريعك الخاصة.

إذا كنت فضوليًا بشأن الخطوة التالية، فكر في:

- **كيفية استخراج النص** من ملفات PDF عبر تحويل كل صفحة إلى صورة أولًا.  
- استخدام بيانات الصناديق المحيطة لتسليط الضوء على الكلمات في واجهة WPF أو WinForms.  
- بث الـ JSON مباشرة إلى واجهة ويب API بدلاً من كتابة ملف (استخدم `HttpClient`).

جرّبه، عدّل الخيارات، ودع بيانات OCR تغذي أي تطبيق تبنيه. هل لديك أسئلة؟ اترك تعليقًا، وتمنياتنا لك بالبرمجة السعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}