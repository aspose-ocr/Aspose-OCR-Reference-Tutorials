---
category: general
date: 2026-01-02
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية تحويل الصورة
  إلى تنسيق JSONL بسرعة وبشكل موثوق.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR وتحويله إلى تنسيق JSONL.
  دليل كامل خطوة بخطوة بلغة C# للمطورين.
og_title: استخراج النص من الصورة – تحويل إلى JSONL باستخدام C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: استخراج النص من الصورة وتحويله إلى JSONL – دليل C#
url: /ar/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة وتحويله إلى JSONL – دليل C# الكامل

هل احتجت يومًا إلى **استخراج النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة ستعطيك ناتجًا نظيفًا ومنظمًا؟ لست وحدك. في العديد من مشاريع معالجة الإيصالات أو رقمنة المستندات، تكون العقبة هي تحويل صورة bitmap إلى نص قابل للبحث *و* إلى تنسيق يمكن للآلة قراءته.

الخبر السار؟ باستخدام Aspose OCR يمكنك **استخراج النص من الصورة** ومع بضع أسطر من الشيفرة، **تحويل الصورة إلى JSONL** للتحليلات اللاحقة. يشرح هذا الدليل العملية بالكامل، بدءًا من تحميل ملف PNG إلى كتابة ملف JSON‑Lines يمكن بثه في خط أنابيب البيانات.

> **تلميح:** إذا كنت تستخدم .NET 6 أو أحدث، فإن نفس الشيفرة تعمل دون أي إعداد إضافي.

## المتطلبات المسبقة — ما ستحتاجه

- **.NET 6 SDK** (أو أي نسخة حديثة من .NET)
- **Aspose.OCR** حزمة NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** للتسلسل  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- صورة نموذجية (مثال: `receipt.png`) موجودة في مجلد يمكنك الإشارة إليه.
- بيئة تطوير أو محرر من اختيارك—Visual Studio، VS Code، Rider، إلخ.

لا إعدادات معقدة، لا خدمات خارجية، فقط عدد قليل من حزم NuGet.

![استخراج النص من الصورة باستخدام C# مع Aspose OCR](https://example.com/assets/ocr-sample.png)

*Alt text: استخراج النص من الصورة باستخدام C# مع Aspose OCR*

## الخطوة 1: تحميل الصورة التي تريد معالجتها  

الأول الذي تقوم به عندما تريد **استخراج النص من الصورة** هو إعطاء محرك OCR صورة bitmap. استخدام `System.Drawing.Bitmap` سهل ويعمل مع معظم صيغ الرسوم النقطية.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **لماذا هذا مهم:** تحميل الصورة كـ `Bitmap` يمنح محرك OCR وصولًا مباشرًا إلى البكسلات، مما يحسن سرعة ودقة التعرف مقارنةً ببث البايتات الخام.

## الخطوة 2: ضبط Aspose OCR لإخراج JSON‑Lines  

Aspose OCR يتيح لك تحديد اللغة، تنسيق الإخراج، وبعض تحسينات الأداء. هنا نطلب **JSON‑Lines** (كائن JSON واحد في كل سطر) لأنه مثالي للمعالجة سطرًا بسطر لاحقًا.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **نصيحة احترافية:** إذا كنت تحتاج إلى إيصالات متعددة اللغات، عيّن `Language = Language.Multilingual` أو مرّر مصفوفة من قيم `Language`.

## الخطوة 3: تشغيل OCR والتقاط النتيجة  

الآن نقوم فعليًا **باستخراج النص من الصورة**. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على مجموعة من كائنات `OcrLine`، كل منها يمثل سطرًا من النص المعترف به مع صندوق الحدود الخاص به.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

في هذه المرحلة `ocrResult.Lines` يحتوي على كل ما تحتاجه—النص الخام، درجات الثقة، والإحداثيات.

## الخطوة 4: تسلسل السطور إلى JSON‑Lines  

سنحوّل المجموعة إلى سلسلة JSON مُنسقة بشكل جميل. رغم أن JSON‑Lines عادةً ما تكون مضغوطة، فإن إضافة المسافات تجعل الملف أسهل للفحص أثناء التطوير.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

المتغير الناتج `jsonLines` يبدو تقريبًا هكذا (مقتطع للوضوح):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

كل سطر ينتهي بحرف سطر جديد، مما يمنحك ملف **JSONL** (JSON‑Lines) حقيقي.

## الخطوة 5: كتابة JSON‑Lines إلى القرص  

أخيرًا، نقوم بحفظ الناتج حتى تتمكن الخدمات الأخرى—مثل Spark، Logstash، أو سكريبت Bash بسيط—من استهلاكه سطرًا بسطر.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

عند فتح `receipt.jsonl` سترى كائن JSON واحد في كل سطر، جاهز للبث.

## الخطوة 6: التحقق من التصدير  

فحص سريع للمنطقية يوفر لك ساعات من تصحيح الأخطاء لاحقًا. لنقرأ أول few سطور مرة أخرى ونطبعها على وحدة التحكم.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

مخرجات وحدة التحكم النموذجية:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

إذا رأيت شيئًا مشابهًا، تهانينا—لقد نجحت في **استخراج النص من الصورة** و**تحويل الصورة إلى JSONL**.

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| **إخراج فارغ** | مسار الصورة غير صحيح أو الملف غير قابل للقراءة. | استخدم `File.Exists(imagePath)` قبل إنشاء الـ bitmap. |
| **درجات ثقة منخفضة** | الصورة غير واضحة أو ذات تباين منخفض. | قم بمعالجة مسبقة للصورة (مثل `Bitmap.RotateFlip`، `Graphics.Clear`) أو زيادة DPI. |
| **لغة غير صحيحة** | OCR يفرض اللغة الإنجليزية افتراضيًا لكن الإيصال بلغة أخرى. | عيّن `options.Language = Language.Spanish` (أو التعداد المناسب). |
| **JSONL يظهر كمصفوفة JSON واحدة** | استخدمت `Formatting.None` دون معالجة السطر الجديد. | تأكد من أن كل كائن مسلسل ينتهي بـ `Environment.NewLine`. |

## مثال كامل يعمل  

فيما يلي البرنامج الكامل الجاهز للتنفيذ. الصقه في مشروع Console واضغط **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**النتيجة المتوقعة:** ملف `receipt.jsonl` يحتوي على كائن JSON واحد في كل سطر، كل منها يحتوي على حقول `Text`، `Confidence`، و`BoundingBox`. يمكنك الآن تغذية هذا الملف في أي خط أنابيب تحليلي يستهلك JSONL.

## الخطوات التالية – ما بعد OCR الأساسي  

- **معالجة دفعات:** غلف المنطق أعلاه داخل حلقة `foreach` لمعالجة مجلد كامل من الإيصالات.  
- **التوازي:** استخدم `Parallel.ForEach` لتسريع المعالجة على عدة نوى عند التعامل مع آلاف الصور.  
- **معالجة لاحقة:** احذف السطور ذات الثقة المنخفضة (`Confidence < 0.9`) قبل التخزين.  
- **التكامل:** ادفع JSONL مباشرة إلى Azure Blob Storage أو AWS S3 باستخدام SDK المناسب.  
- **تنسيقات بديلة:** غيّر `OutputFormat` إلى `PlainText` أو `Xml` إذا كان نظامك اللاحق يفضلهما.  

## الخلاصة  

أصبح لديك الآن حل شامل من البداية إلى النهاية لـ **استخراج النص من الصورة** و**تحويل الصورة إلى JSONL** باستخدام Aspose OCR في C#. يغطي الدليل كل شيء من تحميل الـ bitmap إلى التحقق من الناتج، بالإضافة إلى مجموعة من النصائح العملية للحفاظ على استقرار خط الأنابيب الخاص بك.

جرّبه مع إيصالاتك، فواتيرك، أو نماذجك الممسوحة ضوئيًا—راقب محرك OCR يحول البكسلات إلى بيانات قابلة للبحث ومهيكلة سطرًا بسطر في ثوانٍ. إذا صادفت حالات حافة (مثل المسح المائل أو النص متعدد اللغات)، عد إلى قسم *RecognitionOptions* وعدّل اللغة أو خطوات المعالجة المسبقة.

برمجة سعيدة، ولتكن خطوط أنابيب البيانات دائمًا نظيفة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}