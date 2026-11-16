---
category: general
date: 2026-03-26
description: التعرف على النص من ملف PNG واستخراج بيانات الإيصال باستخدام Aspose OCR
  في C#. تحويل الصورة إلى JSON‑L ومعالجة الإيصال باستخدام OCR في مثال كامل.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: ar
og_description: التعرف على النص من ملفات PNG وتحويل الإيصالات إلى JSON‑L باستخدام
  Aspose OCR في C#. كود كامل خطوة بخطوة ونصائح.
og_title: التعرف على النص من PNG – دليل Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: التعرف على النص من PNG – دليل Aspose OCR C# JSON‑L
url: /ar/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من PNG – دليل Aspose OCR الكامل لـ C#

هل احتجت يومًا إلى **التعرف على النص من PNG** لكنك لم تكن متأكدًا أي مكتبة ستعطيك نتائج نظيفة سطرًا بسطر؟ لست وحدك. في العديد من تطبيقات الأعمال الصغيرة، تكون الإيصال صورة PNG، واستخراج المبلغ أو التاريخ أو اسم التاجر هو نقطة ألم يومية.  

الخبر السار؟ ببضع أسطر من C# ومكتبة **Aspose OCR** يمكنك **استخراج النص من الإيصال**، ثم **تحويل الصورة إلى jsonl** للتحليلات اللاحقة. في هذا الدرس سنستعرض كامل الخطوات — تحميل PNG، تشغيل OCR، وكتابة كل سطر إلى ملف JSON‑L — حتى تتمكن من **معالجة الإيصال باستخدام OCR** فورًا.

سنغطي كل ما تحتاجه: حزم NuGet المطلوبة، برنامج كامل قابل للتنفيذ، شرح لماذا كل خطوة مهمة، وبعض النصائح العملية التي ستقدّرها عندما تصبح الإيصالات فوضوية. لا تحتاج إلى وثائق خارجية؛ فقط انسخ‑الصق، شغّل، وعدّل حسب الحاجة.

---

## ما ستتعلمه

- كيف **تتعرف على النص من PNG** باستخدام `Aspose.OCR`.
- كيف **تستخرج النص من الإيصال** ككائنات سطر وتلتقط درجات الثقة.
- كيف **تحول الصورة إلى jsonl** بحيث يصبح كل سطر OCR كائن JSON منفصل.
- كيف **تعالج الإيصال باستخدام OCR** من البداية إلى النهاية، مع معالجة الحالات الخاصة مثل الصور الفارغة أو الأسطر ذات الثقة المنخفضة.
- نصائح لتصحيح الأخطاء الشائعة في OCR وتحسين الدقة.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا).
- Visual Studio 2022 أو أي بيئة تطوير تفضّلها.
- رخصة صالحة لـ Aspose OCR (يمكنك البدء برخصة مؤقتة مجانية من Aspose.com).
- عينة إيصال محفوظة باسم `receipt.png` في مجلد يمكنك التحكم فيه.

---

## الخطوة 1: التعرف على النص من PNG باستخدام Aspose OCR

أول شيء نحتاجه هو `OcrEngine` مهيّأ. هذا الكائن يحمل إعدادات محرك OCR (اللغة، وضع الكشف، إلخ). بشكل افتراضي يستخدم اللغة الإنجليزية ويكتشف تخطيط الصفحة تلقائيًا، وهو ما يناسب معظم الإيصالات.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**لماذا هذا مهم:**  
`OcrEngine` هو المكوّن الأساسي؛ إن إنشاؤه مرة واحدة وإعادة استخدامه عبر العديد من الصور يقلل من استهلاك الذاكرة. إذا كنت بحاجة إلى لغة مختلفة (مثلاً إيصالات إسبانية)، يمكنك تعيين `ocrEngine.Language = OcrLanguage.Spanish;` قبل استدعاء `Recognize`.

---

## الخطوة 2: استخراج النص من أسطر الإيصال

`OcrResult` يحتوي على مجموعة تسمى `Lines`. كل سطر يحمل النص الأصلي ودرجة الثقة (0‑100). استخراج هذه القيم يمنحك تحكمًا دقيقًا — يمكنك حذف الأسطر ذات الثقة المنخفضة أو وضع علامة عليها للمراجعة اليدوية.

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**لماذا نقوم بتهجير JSON:**  
نص الإيصال قد يحتوي على علامات اقتباس (`"`) أو شرطات مائلة عكسية (`\`) قد تُفسد سلسلة JSON بسيطة. طريقة `EscapeJson` تضمن سطر JSON صالح.

**ما يبدو عليه الناتج:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

كل سطر هو سجل منفصل، مثالي للبث إلى بحيرة بيانات أو لتغذية نموذج تعلم آلي.

---

## الخطوة 3: تحويل الصورة إلى JSONL – معالجة الحالات الخاصة

عند معالجة دفعة من الإيصالات، قد تكون بعض الصور فارغة، تالفة، أو ذات درجات ثقة منخفضة جدًا. دعنا نجعل خط الأنابيب أكثر صلابة.

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**لماذا نُفلتر:**  
الإيصالات المطبوعة على ورق باهت قد تُنتج أحرف عشوائية ذات ثقة منخفضة. حذف كل ما هو أقل من 80 % عادةً يزيل الضوضاء مع الحفاظ على البيانات المفيدة.

---

## الخطوة 4: معالجة الإيصال باستخدام OCR – مثال من البداية إلى النهاية

بدمج كل شيء معًا، إليك البرنامج **الكامل الجاهز للتنفيذ**. استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على ملف PNG الخاص بك.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**تشغيل الكود:**  
1. افتح طرفية في مجلد المشروع.  
2. `dotnet add package Aspose.OCR` – لتثبيت المكتبة.  
3. `dotnet run` – يجب أن ترى رسالة نجاح وملف `receipt.jsonl` يظهر.

**النتيجة المتوقعة:** ملف JSON مفصول بأسطر حيث كل سطر يعكس سطرًا من الإيصال، مع درجات الثقة. يمكنك الآن توجيه هذا الملف إلى Power BI أو Elastic أو أي أداة تحليل تدعم JSON‑L.

---

## المشكلات الشائعة & نصائح احترافية

| المشكلة | لماذا يحدث | الحل السريع |
|-------|----------------|-----------|
| **إخراج فارغ** | مسار الصورة غير صحيح أو الملف ليس PNG. | تحقق من المسار، واستخدم `File.Exists(imagePath)`. |
| **حروف غير مفهومة** | DPI منخفض أو PNG مضغوط بشدة. | استخدم مسحًا بدقة لا تقل عن 300 dpi؛ تجنّب ضغط JPEG القوي. |
| **عدد كبير من الأسطر منخفضة الثقة** | إيصال مطبوع على ورق حراري باهت. | زد عتبة `minConfidence` أو عالج الصورة مسبقًا (تباين/عتبة). |
| **أخطاء في تحليل JSON** | اقتباسات غير مُهجرة في نص الإيصال. | احتفظ بدالة `EscapeJson` أو انتقل إلى `System.Text.Json` لتسلسل أكثر صلابة. |

**نصيحة احترافية:** إذا كنت بحاجة لاستخراج حقول محددة (مثل المبلغ الإجمالي)، نفّذ تعبيرًا نمطيًا بسيطًا على كل `line.Text` بعد حصولك على ملف JSON‑L. هذا يبقي OCR منفصلًا عن منطق الأعمال ويسهّل عملية التصحيح.

---

## توسيع الحل

- **معالجة دفعات:** غلف منطق `Main` داخل حلقة `foreach` على جميع ملفات PNG في دليل.
- **دعم متعدد اللغات:** عيّن `ocrEngine.Language = OcrLanguage.Spanish;` (أو أي لغة مدعومة) قبل `Recognize`.
- **إخراج منظم:** بدلاً من JSON سطرًا بسطر، أنشئ كائن `Receipt` يحتوي على خصائص `Date` و `Merchant` و `Total`، ثم سَلّس مرة واحدة.

كل هذه التنويعات لا تزال **تحول الصورة إلى jsonl** في الجوهر، لذا يمكنك تبديل المستهلك اللاحق دون لمس جزء OCR.

---

## الخلاصة

لقد أظهرنا لك كيف **تتعرف على النص من PNG** باستخدام Aspose OCR، **تستخرج النص من الإيصال**، و**تحول الصورة إلى jsonl** لمعالجة سهلة لاحقة. البرنامج الكامل المستقل بـ C# يوضح سير العمل بالكامل — من تحميل PNG، معالجة الحالات الخاصة، إلى كتابة ملف JSON‑L نظيف — حتى تتمكن فورًا من **معالجة الإيصال باستخدام OCR** في مشاريعك.

جرّبه مع بعض الإيصالات التجريبية، عدّل عتبة الثقة، وسترى كيف يتحول كومة من الصور المشوشة إلى بيانات منظمة جاهزة للتحليل. عندما تشعر بالراحة، استكشف معالجة الدفعات أو أضف نموذج ML صغير لتصنيف فئات النفقات تلقائيًا.

هل لديك أسئلة أو اكتشفت تعديلًا ذكيًا؟ اترك تعليقًا أدناه — برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}