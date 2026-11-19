---
category: general
date: 2026-04-08
description: تعلم كيفية إجراء التعرف الضوئي على الحروف (OCR) على صورة وكتابة ملف JSON
  باستخدام C# وAspose OCR. يوضح هذا الدرس التعليمي لـ Aspose OCR بلغة C# تحويل صورة
  OCR إلى JSON مع قيم الثقة.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: ar
og_description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على الصورة وتصدير النتائج
  إلى ملف JSON باستخدام C#. يغطي هذا الدرس كامل سير عمل Aspose OCR بلغة C#، بما في
  ذلك درجات الثقة.
og_title: تنفيذ التعرف الضوئي على الأحرف (OCR) من الصورة إلى JSON في C# – دليل Aspose
  OCR
tags:
- Aspose
- OCR
- C#
- JSON
title: إجراء OCR على صورة وتحويلها إلى JSON في C# باستخدام Aspose
url: /ar/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على صورة وتحويلها إلى JSON باستخدام C# و Aspose

هل احتجت يومًا إلى **perform OCR on image** للملفات لكنك لم تكن متأكدًا من كيفية الحصول على النتائج بصيغة منظمة؟ لست وحدك—المطورون يسألون باستمرار، “كيف أحول صورة ممسوحة ضوئيًا إلى بيانات قابلة للاستخدام؟” الخبر السار هو أن Aspose.OCR يجعل ذلك سهلًا للغاية، ويمكنك حتى **write JSON file C#**‑style مع تضمين درجات الثقة.

في هذا الدليل سنستعرض **aspose OCR C# tutorial** كامل يغطي كل شيء من تحميل الصورة إلى تصدير النص المُعترف به كـ JSON. في النهاية ستحصل على تطبيق console قابل للتنفيذ يقوم **performs OCR on image**، يحول الناتج إلى JSON (بما في ذلك قيم الثقة)، ويحفظه بسطر واحد من الشيفرة. لا خطوات مخفية، لا سكريبتات خارجية—فقط C# نقي.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0 SDK أو أحدث (الشيفرة تعمل مع .NET Core و .NET Framework أيضًا)
- Visual Studio 2022 (أو أي محرر تفضله)
- رخصة صالحة لـ **Aspose.OCR for .NET** أو رخصة تجريبية مجانية (الإصدار التجريبي المجاني يكفي للاختبار)
- ملف صورة (`input.png`) تريد معالجته (أي صيغة شائعة—PNG، JPG، BMP—ستكفي)

هذا كل شيء. إذا كان أيٌ من هذه غير متوفر، احصل عليه الآن؛ باقي الدليل يفترض أن كل شيء جاهز.

## الخطوة 1: تثبيت حزمة NuGet الخاصة بـ Aspose.OCR

أولًا، أضف المكتبة إلى مشروعك. افتح الطرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

هذا سيجلب أحدث نسخة (اعتبارًا من أبريل 2026 هي 23.12) ويضيف ملفات DLL الضرورية إلى مجلد `bin`. لا حاجة لأي إعدادات إضافية.

## الخطوة 2: تهيئة محرك OCR (Perform OCR on Image)

الآن ننشئ كائن `OcrEngine` ونحدد اللغة التي سيستخدمها. اللغة الإنجليزية (`"en"`) هي الأكثر شيوعًا، لكن يمكنك استبدالها بـ `"fr"` أو `"de"` أو أي لغة مدعومة.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**لماذا نهيئه هنا:** `OcrEngine` يحمل كل الإعدادات اللازمة لعملية التعرف. تحديد اللغة مسبقًا يضمن أن المحرك يستخدم مجموعة الأحرف الصحيحة، مما يحسن الدقة بشكل كبير.

## الخطوة 3: التعرف على الصورة وتسجيل درجة الثقة

مع جاهزية المحرك، نمرر له ملف الصورة. تُعيد طريقة `RecognizeImage` كائن `OcrResult` يحتوي على النص المستخرج ودرجة الثقة لكل كلمة.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**ما الذي يحدث في الخلفية؟** تقوم Aspose بتشغيل مُعرّف يعتمد على الشبكات العصبية يحلل كل كتلة بكسل، يطابقها مع نموذج اللغة الخاص به، ويُرفق قيمة ثقة (0‑100) تُظهر مدى تأكده من كل كلمة.

## الخطوة 4: تحويل النتيجة إلى JSON (OCR Image to JSON)

تُسهل Aspose عملية التحويل. بتمرير `includeConfidence: true` نحصل على حمولة JSON تبدو هكذا:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

وهنا الشيفرة التي تُنتج سلسلة JSON:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**لماذا نضيف درجة الثقة؟** إذا كنت تخطط لإرسال البيانات إلى عمليات لاحقة (مثل التحقق، أو تمييز النص في الواجهة)، معرفة الكلمات غير المؤكدة يتيح لك اتخاذ قرار بطلب تأكيد من المستخدم.

## الخطوة 5: كتابة ملف JSON بأسلوب C#‑Style

الآن نكتب **JSON file C#** فعليًا. طريقة `File.WriteAllText` ذرية وتعمل عبر الأنظمة، مما يجعلها مثالية لتطبيقات console.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

هذا هو سير العمل بالكامل—خمسة خطوات مختصرة تقوم **performs OCR on image**، تحول الناتج إلى JSON، وتخزنه.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في `Program.cs`. تأكد من أن `input.png` موجود في نفس مجلد الملف التنفيذي أو عدّل المسارات وفقًا لذلك.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج (`dotnet run`)، ستظهر لك مخرجات مشابهة لـ:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

وسيحتوي `output.json` على الـ JSON المنظم المعروض سابقًا، مع نسب الثقة لكل كلمة.

## نصائح احترافية وحالات خاصة

- **معالجة ملفات مفقودة:** غلف استدعاء `RecognizeImage` بكتلة `try/catch` للـ `FileNotFoundException` إذا كنت تتعامل مع مسارات ديناميكية.
- **لغات مختلفة:** عيّن `ocrEngine.Language = "fr"` للفرنسية، أو حمّل حزمة لغة مخصصة عبر `ocrEngine.LoadLanguage("custom.lang")`.
- **مستندات كبيرة:** للملفات PDF متعددة الصفحات، حوّل كل صفحة إلى صورة أولًا (مثلاً باستخدام `Aspose.PDF`) ثم كرّر خطوات OCR.
- **تحسين الأداء:** إذا كنت تحتاج نتائج سريعة فقط، غيّر إلى `RecognitionMode.Fast`—ستفقد قليلًا من الدقة لكن ستحصل على سرعة أعلى.
- **تنسيق JSON:** تريد JSON منسقًا؟ استخدم `JsonConvert.SerializeObject` من Newtonsoft مع `Formatting.Indented` بعد تحويل سلسلة JSON الخاصة بـ Aspose إلى كائن.

## الأسئلة المتكررة

**س: هل يعمل هذا مع .NET Framework؟**  
ج: بالتأكيد. نفس حزمة NuGet تستهدف .NET Standard 2.0، لذا يمكنك الإشارة إليها من .NET Framework 4.6.1 وما فوق.

**س: ماذا لو أردت درجة الثقة للمستند بأكمله وليس لكل كلمة؟**  
ج: `OcrResult` يوفر أيضًا `OverallConfidence`. يمكنك إضافتها يدويًا إلى الـ JSON:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**س: هل يمكنني بث الـ JSON مباشرة إلى واجهة ويب؟**  
ج: نعم. استبدل `File.WriteAllText` بطلب `POST` باستخدام `HttpClient` يرسل `jsonResult`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}