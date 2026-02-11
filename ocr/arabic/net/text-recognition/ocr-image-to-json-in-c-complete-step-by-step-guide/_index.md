---
category: general
date: 2026-02-11
description: تحويل صورة OCR إلى JSON في C#. تعلم استخراج النص من الصورة، قراءة ملف
  الصورة في C#، تنسيق مخرجات JSON وطباعة JSON بشكل جميل في C# باستخدام Aspose.OCR.
draft: false
keywords:
- ocr image to json
- extract text from image
- read image file c#
- format json output
- pretty print json c#
language: ar
og_description: تحويل صورة OCR إلى JSON في C#. يوضح هذا الدليل كيفية استخراج النص
  من الصورة، قراءة ملف الصورة في C#، تنسيق مخرجات JSON وطباعة JSON بشكل جميل في C#
  باستخدام Aspose.OCR.
og_title: تحويل صورة OCR إلى JSON في C# – دليل كامل خطوة بخطوة
tags:
- OCR
- C#
- JSON
title: تحويل صورة OCR إلى JSON في C# – دليل كامل خطوة بخطوة
url: /ar/net/text-recognition/ocr-image-to-json-in-c-complete-step-by-step-guide/
---

unchanged.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل صورة إلى JSON في C# – دليل خطوة‑بخطوة كامل

هل احتجت يوماً إلى **ocr image to json** لكن لم تكن متأكدًا من المكتبة التي تختارها أو كيف تحصل على نتيجة منسقة بشكل جميل؟ لست وحدك. في العديد من التطبيقات الواقعية—مسح الفواتير، التحقق من الهوية، أو أرشفة المستندات البسيطة—ستحتاج إلى استخراج النص من صورة والحصول على حمولة JSON نظيفة يمكن للخدمات اللاحقة استهلاكها.

في هذا الدرس سنستعرض كامل سير العمل: من قراءة ملف الصورة في C# إلى استخراج النص باستخدام Aspose.OCR، ثم طلب إخراج JSON منظم، وأخيرًا تنسيق هذا الـ JSON ليصبح مقروءًا للإنسان. في النهاية ستحصل على مقتطف جاهز للإنتاج يمكنك إدراجه في أي مشروع .NET.

سنناقش أيضًا بعض المشكلات الشائعة (مثل حزم اللغات المفقودة) ونظهر بعض التغييرات السريعة—مثلاً التحويل إلى إخراج XML أو معالجة ملفات PDF متعددة الصفحات. لا تحتاج إلى وثائق خارجية؛ كل ما تحتاجه موجود هنا.

## ما ستحتاجه

- **.NET 6+** (الكود يعمل أيضًا مع .NET Framework 4.7+)
- **Aspose.OCR for .NET** – تثبيت عبر NuGet (`Install-Package Aspose.OCR`)
- صورة نموذجية (مثال: `receipt.png`) موجودة في مكان يمكنك الإشارة إليه
- إلمام أساسي بصيغة C# (إذا كتبت برنامج “Hello World” من قبل، فأنت جاهز)

> *نصيحة احترافية:* إذا كنت تعمل على خادم CI، اضبط `AutomaticResourceDownload = true` حتى يقوم Aspose بتحميل بيانات اللغة تلقائيًا—دون الحاجة إلى التعامل اليدوي مع ملفات DLL.

## الخطوة 1: قراءة ملف الصورة C# وإنشاء محرك OCR  

أول شيء نقوم به هو تحميل الصورة من القرص. استخدام `System.Drawing.Image` يجعل الكود مختصرًا ويعمل مع PNG، JPEG، BMP، وحتى ملفات TIFF متعددة الصفحات (المحرك سيختار الصفحة الأولى افتراضيًا).

```csharp
using System.Drawing;          // For Image
using Aspose.OCR;              // Core OCR classes
using Aspose.OCR.Models;       // Language and output enums
using System.Text.Json;        // JSON parsing & pretty‑print

// 1️⃣ Configure the OCR engine – this is where we tell Aspose what language we expect
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // extract text from image in English
    AutomaticResourceDownload = true,        // auto‑download language packs if missing
    OutputFormat = OcrOutputFormat.Json      // ask for JSON rather than plain text
};
```

**لماذا هذا مهم:**  
- `AutomaticResourceDownload` يمنع حدوث أعطال وقت التشغيل عندما لا يكون ملف اللغة الإنجليزية موجودًا محليًا.  
- ضبط `OutputFormat` إلى `Json` يعني أن المحرك يقوم بالفعل بتحويل نتائج OCR الخام إلى كائن منظم—دون الحاجة إلى تحليل السلاسل يدويًا.

## الخطوة 2: تشغيل OCR والحصول على إخراج JSON  

الآن نمرر الـ bitmap المحمل إلى المحرك. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على خاصية `Text` التي تحمل سلسلة الـ JSON.

```csharp
// 2️⃣ Load the image you want to process
using (var receiptImage = Image.FromFile(@"C:\Images\receipt.png"))
{
    // 3️⃣ Perform OCR – this call blocks until the engine finishes
    var ocrResult = ocrEngine.Recognize(receiptImage);

    // 4️⃣ The OCR engine gave us JSON straight away
    string rawJson = ocrResult.Text;
    
    // Optional: write the raw JSON to a file for debugging
    System.IO.File.WriteAllText(@"C:\Temp\ocr_raw.json", rawJson);
}
```

**حالة حافة:** إذا كانت الصورة تالفة أو المسار غير صحيح، فإن `Image.FromFile` يطرح استثناء `FileNotFoundException`. احwrap الكود داخل `try/catch` إذا كنت تتوقع مدخلات غير موثوقة.

## الخطوة 3: تحليل وتنسيق الـ JSON – طباعة JSON بشكل جميل في C#  

الـ JSON الخام من محرك OCR يكون مضغوطًا وصعب القراءة. باستخدام `System.Text.Json` يمكننا تحويله إلى `JsonDocument`، ثم إعادة تسلسله مع إضافة مسافات.

```csharp
// 5️⃣ Parse the JSON string into a DOM-like structure
using var jsonDoc = JsonDocument.Parse(rawJson);

// 6️⃣ Pretty‑print with indentation (2 spaces by default)
string prettyJson = JsonSerializer.Serialize(
    jsonDoc.RootElement,
    new JsonSerializerOptions { WriteIndented = true });

// 7️⃣ Output to console – you could also send this to an API or a file
Console.WriteLine(prettyJson);

// 8️⃣ Save the pretty JSON for later use
System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
```

**ما ستراه:**  

```json
{
  "Lines": [
    {
      "Text": "Store Name",
      "BoundingBox": { "X": 12, "Y": 5, "Width": 150, "Height": 20 }
    },
    {
      "Text": "Total: $23.45",
      "BoundingBox": { "X": 12, "Y": 200, "Width": 100, "Height": 20 }
    }
  ],
  "Language": "English",
  "Confidence": 0.96
}
```

الـ JSON الآن يتضمن النص سطرًا بسطر، الصناديق المحيطة، اللغة المكتشفة، ودرجة الثقة—مثالي لتغذيته إلى تحليلات لاحقة أو مكوّن واجهة مستخدم.

## الخطوة 4: إضافية – تغيير صيغة الإخراج أو اللغة  

إذا احتجت يومًا إلى **format json output** كـ XML أو تريد OCR لفاتورة إسبانية، فقط عدل إعدادات المحرك:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;          // extract text from image in Spanish
ocrEngine.OutputFormat = OcrOutputFormat.Xml;     // ask for XML instead of JSON
```

بقية الكود تبقى كما هي؛ فقط تغير خطوة التحويل (استخدم `XmlDocument` للـ XML).

## مثال كامل يعمل  

بدمج كل ما سبق، إليك ملف واحد يمكنك نسخه ولصقه في تطبيق Console:

```csharp
// ---------------------------------------------------------------
// ocr_image_to_json_demo.cs
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Text.Json;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Configure OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            AutomaticResourceDownload = true,
            OutputFormat = OcrOutputFormat.Json
        };

        // Path to your image – adjust as needed
        string imagePath = @"C:\Images\receipt.png";

        try
        {
            using (var receiptImage = Image.FromFile(imagePath))
            {
                var ocrResult = ocrEngine.Recognize(receiptImage);
                string rawJson = ocrResult.Text;

                // Parse & pretty‑print
                using var jsonDoc = JsonDocument.Parse(rawJson);
                string prettyJson = JsonSerializer.Serialize(
                    jsonDoc.RootElement,
                    new JsonSerializerOptions { WriteIndented = true });

                Console.WriteLine("=== Pretty‑Printed OCR JSON ===");
                Console.WriteLine(prettyJson);

                // Optional: write to file
                System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Error processing image: {ex.Message}");
        }
    }
}
```

تشغيل هذا البرنامج يطبع حمولة JSON منسقة بشكل جميل إلى وحدة التحكم ويحفظها في `C:\Temp\ocr_pretty.json`. يضمن بلوك `try/catch` أنه حتى لو تعذرت قراءة الصورة، ستحصل على رسالة خطأ واضحة بدلاً من تعطل صامت.

## أسئلة شائعة ومشكلات محتملة  

- **ماذا لو أعاد OCR نصًا فارغًا؟**  
  عادةً ما يعني ذلك أن الصورة مشوشة جدًا أو أن اللغة غير متطابقة. جرّب زيادة التباين في الصورة أو تغيير `Language` إلى `AutoDetect`.  

- **هل يمكنني معالجة صور متعددة داخل حلقة؟**  
  بالتأكيد. ضع بلوك `using (var img = Image.FromFile(...))` داخل حلقة `foreach (var file in Directory.GetFiles(...))` واجمع كل `prettyJson` في قائمة أو احفظها في ملفات منفصلة.  

- **هل مخطط JSON ثابت؟**  
  Aspose يضمن التوافق العكسي لصيغة الإخراج `Json`، لكن تحقق دائمًا من خاصية `Version` في الاستجابة إذا كنت تستهدف نسخة API محددة.  

- **هل أحتاج إلى ترخيص لـ Aspose.OCR؟**  
  مفتاح تقييم مجاني يعمل حتى 100 صفحة. للإنتاج، اشترِ ترخيصًا واضبطه باستخدام `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.  

## الخلاصة  

أنت الآن تمتلك **حلًا كاملًا ومستقلاً لتحويل صورة إلى JSON في C#**. من خلال قراءة ملف الصورة، ضبط محرك OCR، طلب إخراج JSON، وتنسيقه بشكل جميل، يمكنك دمج استخراج النص في أي خدمة .NET دون الحاجة إلى حيل السلاسل النصية.  

من هنا يمكنك استكشاف **extract text from image** لأنواع ملفات أخرى (PDF، TIFF متعدد الصفحات)، تجربة لغات مختلفة، أو تمرير الـ JSON إلى مخزن NoSQL للتحليلات. السماء هي الحد—فقط تذكر التعامل مع الأخطاء بلطف ومراقبة الترخيص إذا توسعت في الاستخدام.

برمجة سعيدة، ولتكن خطوط OCR الخاصة بك دقيقة دائمًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}