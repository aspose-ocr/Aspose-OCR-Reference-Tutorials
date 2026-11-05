---
category: general
date: 2026-04-06
description: التعرف على نص الصورة باستخدام Aspose OCR في C#. تعلم كيفية استخراج النص،
  تحميل ملف الصورة في C#، وكتابة JSON في C# مع مثال بسيط خطوة بخطوة.
draft: false
keywords:
- recognize image text
- how to extract text
- write json in c#
- load image file c#
language: ar
og_description: التعرف على نص الصورة باستخدام Aspose OCR في C#. يوضح هذا الدليل كيفية
  استخراج النص، تحميل ملف الصورة في C#، وكتابة JSON في C# بسرعة.
og_title: التعرف على نص الصورة في C# – دليل خطوة بخطوة كامل
tags:
- OCR
- C#
- Aspose
title: التعرف على نص الصورة في C# – دليل كامل مع تصدير JSON
url: /ar/net/text-recognition/recognize-image-text-in-c-full-guide-with-json-export/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على نص الصورة في C# – دليل خطوة بخطوة كامل

هل احتجت يومًا إلى **التعرف على نص الصورة** من إيصال ممسوح ضوئيًا لكنك لم تكن متأكدًا أي مكتبة تختار؟ لست وحدك. في العديد من التطبيقات الواقعية—متتبعات النفقات، معالجات الفواتير، وحتى أدوات الوصول—استخراج الكلمات من صورة هو العائق الأول.  

في هذا البرنامج التعليمي سنستعرض حلًا عمليًا **يتعرف على نص الصورة** باستخدام مكتبة Aspose OCR، يوضح **كيفية استخراج النص**، يبين **كيفية تحميل ملف الصورة c#** بشكل صحيح، وأخيرًا **كتابة json في c#** حتى تتمكن من تخزين أو نقل النتائج. في النهاية ستحصل على تطبيق كونسول جاهز للتشغيل يحول أي صورة PNG إلى حمولة JSON منظمة.

---

## ما ستحتاجه

- **.NET 6+** (الكود يعمل أيضًا مع .NET Framework 4.8، لكن .NET 6 هو الخيار المثالي).
- **Aspose.OCR for .NET** حزمة NuGet. قم بتثبيتها باستخدام `dotnet add package Aspose.OCR`.
- صورة نموذجية (`input.png`) موجودة في مكان يمكن لتطبيقك قراءته.  
- Visual Studio 2022 أو أي محرر تفضله—لا تحتاج إلى حيل IDE متقدمة.

> نصيحة احترافية: احفظ ملفات الصور في مجلد يسمى `Resources` داخل المشروع؛ فهذا يحافظ على نظافة المسارات ويتجنب مشاكل “الملف غير موجود”.

---

## الخطوة 1: التعرف على نص الصورة – تحميل ملف الصورة

قبل أن يتمكن محرك OCR من أداء سحره، عليك **تحميل ملف الصورة c#** بأمان. طريقة `Image.FromFile` تُطلق استثناءً إذا كان المسار غير صحيح أو إذا كان الملف غير مدعوم، لذا سنحمي من ذلك.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // Verify the image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // Load the image – this is the “load image file c#” step
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // Continue to OCR...
        }
    }
}
```

*لماذا هذا مهم*: تحميل الصورة داخل كتلة `using` يضمن تحرير موارد GDI+ غير المُدارة بسرعة، مما يمنع تسرب الذاكرة في الخدمات طويلة التشغيل.

---

## الخطوة 2: كيفية استخراج النص باستخدام Aspose OCR

الآن بعد أن أصبحت الـ bitmap في الذاكرة، نقوم بتمريرها إلى محرك **التعرف على نص الصورة**. `OcrEngine` من Aspose بسيط: إنشاء كائن، استدعاء `Recognize`, وستحصل على كائن `OcrResult` يحتوي على النص الخام، درجات الثقة، وحتى المربعات المحيطة.

```csharp
// Inside the using block from Step 1
var ocrEngine = new OcrEngine();

// Perform OCR – this is the core “how to extract text” operation
OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

// Quick sanity check
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("⚠️ No text detected. Try a clearer image.");
    return;
}
Console.WriteLine("✅ OCR succeeded. Extracted text:");
Console.WriteLine(ocrResult.Text);
```

*شرح*: طريقة `Recognize` تشغل الشبكة العصبية المدمجة. تعمل بأفضل شكل مع صور ذات تباين عالي ودقة 300 DPI. إذا قدمت صورة غير واضحة، ستنخفض درجة الثقة—فكر في ما قبل المعالجة (إزالة الميل، تحويل إلى ثنائي) للشفرة الإنتاجية.

---

## الخطوة 3: كتابة JSON في C# – تصدير نتيجة OCR

معظم واجهات برمجة التطبيقات تتوقع JSON، لذا سنقوم **بكتابة json في c#** باستخدام `JsonExport` من Aspose. المكتبة تسلسل كامل كائن `OcrResult`، مع الحفاظ على معلومات السطر وقيم الثقة.

```csharp
// Still inside the same using block
string jsonResult = JsonExport.ToJson(ocrResult);

// Persist the JSON to disk
File.WriteAllText(outputPath, jsonResult);
Console.WriteLine($"💾 JSON written to {outputPath}");
```

### مخرجات JSON المتوقعة

```json
{
  "Text": "Total: $12.34\r\nDate: 2026-04-01\r\n...",
  "Words": [
    { "Text": "Total", "Confidence": 0.98, "Rectangle": { "X": 10, "Y": 15, "Width": 50, "Height": 12 } },
    { "Text": "$12.34", "Confidence": 0.96, "Rectangle": { "X": 70, "Y": 15, "Width": 45, "Height": 12 } }
    // … more words …
  ]
}
```

*لماذا JSON؟* إنه مستقل عن اللغة، سهل التفكيك، ويحافظ على بيانات OCR التفصيلية التي قد تحتاجها للتحقق في المراحل اللاحقة.

---

## الخطوة 4: برنامج كامل قابل للتنفيذ

بجمع الأجزاء معًا، إليك تطبيق الكونسول الكامل. انسخ‑الصق، استعد حزم NuGet، واضغط **F5**.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Configuration – adjust these paths as needed
        // -------------------------------------------------
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // -------------------------------------------------
        // Validate input file
        // -------------------------------------------------
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // -------------------------------------------------
        // Load image (load image file c#)
        // -------------------------------------------------
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // -------------------------------------------------
            // Initialize OCR engine and recognize text
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("⚠️ No text detected. Try a clearer image.");
                return;
            }

            Console.WriteLine("✅ OCR succeeded. Sample output:");
            Console.WriteLine(ocrResult.Text.Substring(0, Math.Min(100, ocrResult.Text.Length)) + "...");

            // -------------------------------------------------
            // Convert result to JSON (write json in c#)
            // -------------------------------------------------
            string jsonResult = JsonExport.ToJson(ocrResult);
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"💾 JSON written to {outputPath}");
        }
    }
}
```

شغّل البرنامج وافتح `Resources/output.json`—سترى تمثيل JSON منظم جيدًا لكل ما تعرفه المحرك.

---

## التعامل مع الحالات الشائعة

| الحالة | ما الذي يجب فعله | السبب |
|-----------|------------|-----|
| **الصورة فارغة أو تالفة** | غلف `Image.FromFile` بكتلة try/catch وسجّل الاستثناء. | يمنع تعطل التطبيق ويعطيك رسالة خطأ واضحة. |
| **درجات الثقة منخفضة** | تحقق من `ocrResult.Words[i].Confidence`. إذا كانت أقل من 0.75، فكر في ما قبل المعالجة (زيادة DPI، تحسين الحدة). | يحسن الاعتمادية للعمليات اللاحقة مثل استخراج المبالغ. |
| **ملفات كبيرة (>10 ميغابايت)** | قلل أبعاد الصورة قبل OCR (`receiptImage = new Bitmap(receiptImage, new Size(width/2, height/2))`). | يقلل من ضغط الذاكرة ويسرّع التعرف. |
| **مستندات متعددة اللغات** | عيّن `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` | يتيح للمحرك اكتشاف الأحرف من اللغتين. |

---

## إضافي: تصور نتيجة OCR (اختياري)

إذا أردت رؤية موضع كل كلمة على الصورة، يمكنك رسم المربعات المحيطة:

```csharp
using (Graphics g = Graphics.FromImage(receiptImage))
{
    foreach (var word in ocrResult.Words)
    {
        var rect = new Rectangle(word.Rectangle.X, word.Rectangle.Y,
                                 word.Rectangle.Width, word.Rectangle.Height);
        g.DrawRectangle(Pens.Red, rect);
    }
    receiptImage.Save(Path.Combine("Resources", "annotated.png"));
}
```

الصورة الناتجة `annotated.png` ستظهر مستطيلات حمراء حول كل كلمة تم التعرف عليها—مفيد للتصحيح.

---

## الخلاصة

لقد قمنا للتو **بالتعرف على نص الصورة** في C# من البداية إلى النهاية: تحميل ملف الصورة، استدعاء Aspose OCR **لاستخراج النص**، وأخيرًا **كتابة json في c#** حتى يمكن للبيانات الانتقال إلى أي مكان. المثال الكامل يعمل مباشرة، والنصائح الإضافية تساعدك على التعامل مع الإيصالات غير الواضحة، الملفات الضخمة، أو المسحات متعددة اللغات.

ما التالي؟ جرّب استبدال Aspose بمحرك آخر (Tesseract، Microsoft OCR) وقارن درجات الثقة، أو أدخل JSON إلى قاعدة بيانات لتقارير النفقات. يمكنك أيضًا توسيع تطبيق الكونسول إلى واجهة ويب ASP .NET Core API تستقبل تحميلات الصور وتعيد JSON فورًا.

هل لديك أسئلة حول التحجيم، معالجة الأخطاء، أو التكامل مع Azure Functions؟ اترك تعليقًا أو راسلني على GitHub. برمجة سعيدة، ولتكن OCR دائمًا واضحة!

---

![لقطة شاشة لمخرجات JSON الخاصة بـ OCR – مثال التعرف على نص الصورة](https://example.com/ocr-example.png "مثال التعرف على نص الصورة")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}