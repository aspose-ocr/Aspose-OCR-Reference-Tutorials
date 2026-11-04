---
category: general
date: 2026-02-09
description: تعلم كيفية تنفيذ OCR في C# لاستخراج النص من الصورة، والتعرف على النص
  من PNG، وكتابة ملف JSON في C# بسرعة.
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: ar
og_description: كيف تُجري OCR في C#؟ اتبع هذا الدليل خطوة بخطوة لاستخراج النص من الصورة،
  التعرف على النص من PNG، وكتابة ملف JSON في C# بكفاءة.
og_title: كيفية تنفيذ OCR في C# – استخراج النص وكتابة JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: كيفية تنفيذ OCR في C# – استخراج النص وكتابة JSON
url: /ar/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في C# – دليل كامل

تنفيذ OCR في C# هو عائق شائع عندما تحتاج إلى **استخراج النص من صورة**. في هذا الدليل سنستعرض التعرف على النص من PNG، وتصدير النتيجة التفصيلية إلى سلسلة JSON، وأخيرًا **كتابة ملف JSON C#**. هل سبق لك أن حدقت في نموذج ممسوح وتساءلت كيف تحول تلك الخطوط المتعرجة إلى نص قابل للبحث؟ لست وحدك؛ كثير من المطورين يواجهون هذه المشكلة في البداية.

سنستخدم مكتبة Aspose.OCR لأنها توفر ثقة لكل رمز مباشرةً وتعمل بسلاسة مع مشاريع .NET 6+. بنهاية هذا الشرح ستحصل على تطبيق كونسول جاهز للتشغيل يقوم بتحميل PNG، واستخراج كل حرف، وحفظ ملف JSON منظم يمكنك إرساله إلى قاعدة بيانات أو نموذج ذكاء اصطناعي. لا اختصارات غامضة مثل “انظر إلى الوثائق” — مجرد حل مستقل.

## ما ستحتاجه

- **.NET 6 SDK** (أو أحدث) – الإصدار LTS الحالي وقت كتابة هذا الدليل.
- **Aspose.OCR for .NET** حزمة NuGet – `Install-Package Aspose.OCR`.
- صورة PNG تريد مسحها (مثال: `form.png`).  
- بيئة تطوير أو محرر – Visual Studio، VS Code، Rider – أيًا كان ما ترتاح له.

هذا كل شيء. إذا كان لديك هذه المكونات، فأنت جاهز للبدء.

![كيفية تنفيذ OCR مثال](ocr-example.png "كيفية تنفيذ OCR في C#")

*نص بديل للصورة: توضيح لكيفية تنفيذ OCR يظهر تطبيق كونسول C# يعالج صورة PNG.*

## الخطوة 1: إعداد المشروع وإضافة الاعتمادات

أولاً، أنشئ مشروع كونسول جديد واستورد مكتبة Aspose OCR.

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** استخدم العلامة `--framework net6.0` إذا أردت تثبيت إطار العمل الهدف بشكل صريح.

لماذا هذه الخطوة مهمة: حزمة NuGet تحتوي على الفئات `OcrEngine` و `ImageStream` و `JsonExporter` التي سنعتمد عليها. بدونها، لن يعرف المترجم ما معنى “OCR” أصلاً.

## الخطوة 2: كتابة منطق OCR الأساسي

افتح `Program.cs` (أو أنشئ ملفًا جديدًا) واستبدل محتوياته بما يلي. كل قسم مُعلّق حتى تتمكن من معرفة سبب وجوده.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### لماذا كل جزء مهم

- **OcrEngine**: فكر فيه كعقل العملية. يقوم بتحميل نماذج اللغة وإعداد خط أنابيب الاستدلال.
- **ImageStream.FromFile**: يتعامل مع أي PNG أو JPEG أو BMP، إلخ. يُجرد تعقيدات إدخال/إخراج الملفات.
- **RecognitionResult**: يحتفظ بالنص الخام بالإضافة إلى درجات الثقة. هنا تحصل على البيانات الدقيقة التي تحتاجها للتحقق اللاحق.
- **JsonExporter**: يحول `RecognitionResult` الغني إلى حمولة JSON نظيفة، مثالية للواجهات البرمجية (APIs).
- **File.WriteAllText**: الطريقة المباشرة في .NET لـ **كتابة ملف JSON C#** دون اعتماديات إضافية.

## الخطوة 3: تشغيل التطبيق والتحقق من المخرجات

قم بترجمة البرنامج وتنفيذه:

```bash
dotnet run
```

يجب أن ترى رسالة كونسول مشابهة لـ:

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

افتح `form.json` – ستجد شيئًا مثل:

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

نجحت خطوة **استخراج النص من صورة**، والآن لديك تمثيل JSON قابل للقراءة آليًا لكل حرف.

## الخطوة 4: معالجة الحالات الطرفية الشائعة

### ملفات مفقودة أو تالفة

إذا كان مسار PNG غير صحيح، فإن `ImageStream.FromFile` يطرح استثناء `FileNotFoundException`. احطّ كود التحميل بكتلة try‑catch:

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### درجات ثقة منخفضة

أحيانًا تُعيد OCR درجات ثقة منخفضة للمسحات الضوضائية. يمكنك تصفية الرموز قبل التصدير:

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

هذا يضمن أن يحتوي JSON فقط على أحرف موثوقة إلى حد ما — مفيد عندما تُدخل البيانات في خطوط تحقق لاحقة.

### ملفات كبيرة والذاكرة

معالجة PNG متعددة الميجابايت قد ترفع استهلاك الذاكرة. فكر في بث الصورة على دفعات أو استخدام `OcrEngine.RecognizeAsync` (متاح في إصدارات Aspose الأحدث) للحفاظ على استجابة واجهة المستخدم.

## الخطوة 5: توسيع الحل (اختياري)

- **معالجة دفعات**: تكرار عبر مجلد من PNGs وإنشاء JSON مطابق لكل ملف.
- **تخزين في قاعدة البيانات**: إدراج JSON في عمود SQL `NVARCHAR(MAX)` للتحليلات لاحقًا.
- **اختيار اللغة**: اضبط `ocrEngine.Language = OcrLanguage.Spanish;` إذا كنت بحاجة إلى دعم غير الإنجليزية.

جميع هذه الإضافات تتبع نفس نمط **كيفية تنفيذ OCR** الذي أنشأناه — التهيئة، التعرف، التصدير، والحفظ.

## الأسئلة المتكررة

**س: هل يعمل هذا مع JPG أو TIFF؟**  
ج: بالتأكيد. `ImageStream.FromFile` يكتشف الصيغة تلقائيًا، لذا يمكنك استبدال PNG بأي صورة نقطية مدعومة.

**س: ماذا لو احتجت لاستخراج النص من PDF؟**  
ج: حوّل كل صفحة PDF إلى صورة أولاً (مثلاً باستخدام `Aspose.PDF`) ثم أدخل PNG في تدفق OCR الموضح هنا.

**س: هل يمكن الحصول على نتيجة OCR كـ XML بدلاً من JSON؟**  
ج: نعم. Aspose.OCR يتضمن أيضًا `XmlExporter`. استبدل `JsonExporter` بـ `XmlExporter` وعدّل امتداد الملف.

## الخلاصة

لقد استعرضنا **كيفية تنفيذ OCR** في C# من البداية إلى النهاية، موضحين لك كيفية **استخراج النص من صورة**، **التعرف على النص من PNG**، و**كتابة ملف JSON C#** دون أي مشاكل. المثال الكامل القابل للتنفيذ موجود في مقتطفات الشيفرة أعلاه، والآن تفهم سبب كل خطوة — تهيئة المحرك، معالجة الحالات الطرفية، وحفظ النتائج.

بعد ذلك، قد تستكشف خطوط OCR الدفعية، أو دمج مخرجات JSON مع Azure Cognitive Search، أو تجربة نماذج لغة مخصصة. السماء هي الحد عندما تتقن أساسيات OCR في C#.

إذا واجهت أي صعوبات أو لديك أفكار لتوسعات إضافية، اترك تعليقًا أدناه. ترميز سعيد، واستمتع بتحويل تلك المسحات البكسلية إلى بيانات نظيفة وقابلة للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}