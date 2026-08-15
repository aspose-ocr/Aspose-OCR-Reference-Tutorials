---
category: general
date: 2026-04-17
description: تعلم مثال Aspose OCR لقراءة ملف صورة C#، استخراج نص الصورة C# وكتابة
  ملف JSON C#. دليل OCR كامل خطوة بخطوة بلغة C#.
draft: false
keywords:
- aspose ocr example
- write json file c#
- read image file c#
- extract text image c#
- c# ocr tutorial
language: ar
og_description: اتقن مثال Aspose OCR لقراءة صورة، استخراج النص، وكتابة ملف JSON باستخدام
  C#. اتبع هذا الدرس المختصر لـ OCR بلغة C#.
og_title: مثال Aspose OCR – تحويل نص الصورة إلى JSON في C#
tags:
- Aspose
- OCR
- C#
- JSON
title: مثال Aspose OCR – تحويل نص الصورة إلى JSON في C#
url: /ar/net/text-recognition/aspose-ocr-example-convert-image-text-to-json-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# مثال Aspose OCR – تحويل نص الصورة إلى JSON في C#

هل احتجت يومًا إلى **مثال Aspose OCR** لا يقرأ الصورة فحسب بل ينتج JSON منظم للمعالجة اللاحقة؟ لست وحدك. في العديد من المشاريع—أتمتة الفواتير، مسح الإيصالات، أو حتى أرشفة المستندات البسيطة—يواجه المطورون نفس المشكلة: “كيف أحصل على نتيجة OCR بصيغة يحبها API الخاص بي؟”

الأخبار السارة؟ باستخدام Aspose.OCR يمكنك فعل ذلك ببضع أسطر فقط، وسأوضح لك بالضبط كيف. بنهاية هذا الدليل ستعرف كيف **قراءة ملف صورة C#**، **استخراج نص من صورة C#**، و **كتابة ملف JSON C#**—كل ذلك ضمن دليل OCR C# نظيف وقابل لإعادة الاستخدام.

## ما الذي ستحتاجه

- .NET 6.0 أو أحدث (الكود يُجمّع مع .NET Core أيضًا)  
- حزمة NuGet لـ Aspose.OCR for .NET (`Install-Package Aspose.OCR`)  
- صورة (`input.jpg`) تحتوي على نص واضح قابل للقراءة آليًا  
- محرر نصوص أو Visual Studio (أي بيئة تطوير متكاملة ستكفي)

لا ملفات إعداد إضافية، ولا سحر مخفي—فقط الـ SDK وصورة واحدة.

## الخطوة 1 – قراءة ملف صورة C# باستخدام Aspose.OCR

أولًا وقبل كل شيء: عليك تزويد محرك OCR بصورة صالحة. Aspose.OCR يتوقع كائن `OcrImage`، يمكنك إنشاؤه مباشرةً من مسار ملف.

```csharp
using Aspose.OCR;
using System.IO;

// Path to the source picture
string imagePath = @"C:\MyProject\Images\input.jpg";

// Load the image – this is the “read image file C#” part
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

*لماذا هذا مهم:* تحميل الصورة مبكرًا يتيح لك التحقق من وجود الملف واكتشاف مشاكل الصيغة قبل أن يبدأ المحرك في معالجة البكسلات. إذا كان الملف مفقودًا، فإن `FromFile` يرمي استثناء واضح يمكنك التعامل معه لاحقًا.

## الخطوة 2 – تهيئة محرك Aspose OCR

إنشاء المحرك بسيط، لكن يجب أن تغلفه بعبارة `using` حتى يتم تحرير الموارد بسرعة.

```csharp
// Create the OCR engine – it holds all the recognition settings
using var ocrEngine = new OcrEngine();
```

*نصيحة احترافية:* المحرك الافتراضي يعمل جيدًا لمعظم النصوص اللاتينية. إذا كنت تحتاج لغة مختلفة، يمكنك تعيين `ocrEngine.Language = Language.YourLanguage;` قبل استدعاء `Recognize`.

## الخطوة 3 – استخراج نص الصورة C# – تنفيذ التعرف

الآن يبدأ العمل الشاق. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على النص الخام، درجات الثقة، ومربعات الإحاطة لكل كلمة.

```csharp
// Run OCR – this is the “extract text image C#” step
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

ستلاحظ أن `ocrResult.Text` يحتوي على السلسلة النصية العادية، بينما `ocrResult.Regions` يزودك ببيانات الموقع إذا احتجت لتسليط الضوء على الكلمات في واجهة المستخدم.

## الخطوة 4 – كتابة ملف JSON C# – تسلسل النتيجة

تحويل النتيجة إلى JSON سهل باستخدام `System.Text.Json`. سنطبع النتيجة بشكل منسق لتكون قابلة للقراءة البشرية.

```csharp
using System.Text.Json;

// Convert the OCR result to nicely formatted JSON
string json = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true });
```

*لماذا نستخدم `System.Text.Json`*: فهو مدمج في .NET، سريع، ولا يتطلب تبعيات إضافية. إذا كنت تفضل Newtonsoft، سيتغير الكود بضع أسطر فقط.

## الخطوة 5 – حفظ JSON على القرص

أخيرًا، اكتب السلسلة إلى ملف. هذا يُكمل جزء **write json file c#**.

```csharp
// Destination path for the JSON output
string jsonOutputPath = @"C:\MyProject\Output\ocrResult.json";

// Save the JSON – now you have a portable data file
File.WriteAllText(jsonOutputPath, json);

Console.WriteLine("OCR data saved as JSON.");
```

### النتيجة المتوقعة بصيغة JSON (عينة)

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑01\nTotal: $1,234.56",
  "Regions": [
    {
      "BoundingBox": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Confidence": 0.98,
      "Text": "Invoice #12345"
    },
    {
      "BoundingBox": { "X": 10, "Y": 60, "Width": 150, "Height": 30 },
      "Confidence": 0.96,
      "Text": "Date: 2024‑03‑01"
    },
    {
      "BoundingBox": { "X": 10, "Y": 100, "Width": 180, "Height": 30 },
      "Confidence": 0.99,
      "Text": "Total: $1,234.56"
    }
  ]
}
```

*ملاحظة:* الأرقام الدقيقة ستختلف بناءً على صورتك، لكن الهيكل يبقى نفسه—مثالي لتغذيته إلى APIs، قواعد البيانات، أو أدوات العرض في الواجهة الأمامية.

## دليل OCR كامل بـ C# – جميع الخطوات مجمعة

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق الذي يجمع كل شيء معًا. لا أجزاء مفقودة، ولا اختصارات “انظر الوثائق”.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\MyProject\Images\input.jpg";
        var ocrImage = OcrImage.FromFile(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine();
        // Example: ocrEngine.Language = Language.English; // optional

        // -------------------------------------------------
        // Step 3: Perform OCR recognition
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // -------------------------------------------------
        // Step 4: Serialize the result to indented JSON
        // -------------------------------------------------
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // -------------------------------------------------
        // Step 5: Write the JSON to a file
        // -------------------------------------------------
        string jsonOutputPath = @"C:\MyProject\Output\output.json";
        File.WriteAllText(jsonOutputPath, json);

        // -------------------------------------------------
        // Step 6: Let the user know we’re done
        // -------------------------------------------------
        Console.WriteLine("OCR data saved as JSON.");
    }
}
```

### تشغيل الكود

1. استبدل مساري `@"C:\MyProject\…"` بالمسارات الفعلية لديك.  
2. ابنِ المشروع (`dotnet build`) وشغّله (`dotnet run`).  
3. افتح `output.json`—يجب أن ترى تمثيلًا منسقًا بشكل جيد لنص الصورة.

## أسئلة شائعة وحالات خاصة

**ماذا لو كانت صورتي غير واضحة؟**  
Aspose.OCR يقدم خيارات ما قبل المعالجة مثل `ocrEngine.ImagePreprocessOptions.Deskew = true;`. فعّلها قبل استدعاء `Recognize` لتحسين الدقة.

**هل يمكنني حصر الناتج على النص العادي فقط؟**  
بالطبع—قم بتسلسل `ocrResult.Text` بدلاً من الكائن بالكامل:

```csharp
string plainJson = JsonSerializer.Serialize(
    new { Text = ocrResult.Text },
    new JsonSerializerOptions { WriteIndented = true });
```

**هل أحتاج إلى معالجة ملفات PDF متعددة الصفحات؟**  
المثال يركز على صورة واحدة، لكن يمكنك التكرار عبر كل صورة صفحة، تنفيذ نفس الخطوات، وتجميع النتائج في مصفوفة JSON.

## نصائح احترافية وملاحظات

- **مسارات الملفات:** استخدم `Path.Combine` لتجنب كتابة الشرطات المائلة يدوياً، خاصة إذا انتقلت إلى Linux.  
- **الذاكرة:** للدفعات الضخمة، أعد استخدام نسخة واحدة من `OcrEngine` بدلاً من إنشاء نسخة جديدة لكل صورة.  
- **حجم JSON:** إذا كنت تحتاج النص فقط، احذف خاصية `Regions` لتقليل حجم الحمولة.  
- **التحقق من الإصدار:** تم اختبار هذا الدليل مع Aspose.OCR 23.9.0؛ الإصدارات الأحدث تحتفظ بنفس واجهة API، لكن دائمًا راجع ملاحظات الإصدار لأي تغييرات كسرية.

![عينة إخراج JSON من OCR – مثال Aspose OCR](https://example.com/sample-ocr-json.png "معاينة JSON لمثال Aspose OCR")

## الخلاصة

لقد استعرضنا مثال **Aspose OCR** كامل يقرأ صورة، يستخرج نصها، ويكتب النتيجة في ملف JSON باستخدام C# فقط. الحل مستقل، جاهز للإنتاج، وسهل التوسيع—سواء أردت إضافة دعم لغات، تعديل عتبات الثقة، أو تغذية JSON إلى خدمة لاحقة.

إذا كنت تبحث عن الخطوة التالية، جرّب ربط هذا الدليل مع **دليل OCR بـ C#** يرفع JSON إلى Azure Cognitive Search، أو جرب استخراج الجداول من الفواتير. السماء هي الحد عندما تكون لديك JSON بين يديك.

هل لديك تعديل ترغب في مشاركته؟ اترك تعليقًا، استنسخ المستودع، أو راسلني على GitHub. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}