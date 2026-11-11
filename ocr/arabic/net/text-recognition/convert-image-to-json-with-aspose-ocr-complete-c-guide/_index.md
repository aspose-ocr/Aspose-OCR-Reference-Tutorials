---
category: general
date: 2026-05-06
description: تعلم كيفية تحويل الصورة إلى JSON باستخدام Aspose OCR في C#. يغطي هذا
  الدليل خطوة بخطوة أيضًا كيفية إجراء OCR على الصورة، استخراج النص من الصورة وتحميل
  الصورة للـ OCR.
draft: false
keywords:
- convert image to json
- how to ocr image
- extract text from image
- how to extract text
- load image for ocr
language: ar
og_description: تحويل الصورة إلى JSON باستخدام Aspose OCR في C#. اتبع هذا الدليل لتعلم
  كيفية التعرف الضوئي على الأحرف في الصورة، استخراج النص من الصورة وحفظ النتائج مع
  بيانات الثقة.
og_title: تحويل الصورة إلى JSON باستخدام Aspose OCR – دليل C# الكامل
tags:
- Aspose OCR
- C#
- JSON
title: تحويل الصورة إلى JSON باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/convert-image-to-json-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى JSON باستخدام Aspose OCR – دليل C# كامل

هل تساءلت يومًا كيف **convert image to JSON** دون كتابة محلل مخصص؟ لست وحدك. يحتاج العديد من المطورين إلى استخراج النص من الصور ثم تمرير تلك البيانات مباشرة إلى الخدمات المت downstream التي تتوقع حمولة JSON. الخبر السار؟ باستخدام Aspose OCR يمكنك القيام بذلك ببضع أسطر فقط من C#.

في هذا الدرس سنستعرض العملية بالكامل: من تحميل صورة لـ OCR، إلى تشغيل محرك التعرف، وأخيرًا حفظ النص المعترف به (مع درجات الثقة) كملف JSON نظيف. في النهاية ستتمكن من **how to OCR image** الملفات، **extract text from image** الأصول، وحتى الإجابة على السؤال القديم “**how to extract text**?” بطريقة جاهزة للإنتاج.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core أيضًا)  
- حزمة NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- ملف صورة (JPEG, PNG, BMP…) يحتوي على نص قابل للقراءة  
- بيئة تطوير مفضلة – Visual Studio, Rider، أو حتى VS Code كافية  

لا تحتاج إلى مكتبات إضافية؛ Aspose يتولى الجزء الصعب خلف الكواليس.

![مثال تحويل الصورة إلى JSON](https://via.placeholder.com/600x300.png?text=Convert+Image+to+JSON+with+Aspose+OCR "مثال تحويل الصورة إلى JSON")

## الخطوة 1 – تثبيت وإشارة Aspose OCR

قبل أن تتمكن من **load image for OCR**، تحتاج إلى المكتبة التي تتواصل فعليًا مع محرك OCR.

```csharp
// Using the .NET CLI
dotnet add package Aspose.OCR
```

أو، إذا كنت تفضّل وحدة تحكم مدير الحزم:

```powershell
Install-Package Aspose.OCR
```

> **نصيحة احترافية:** استهدف أحدث نسخة مستقرة (اعتبارًا من مايو 2026 هي 23.9) للحصول على أحدث حزم اللغات وتحسينات الأداء.

## الخطوة 2 – إنشاء كائن محرك OCR

المحرك هو قلب العملية. إنشاء نسخة واحدة يتيح لك إعادة استخدام الإعدادات نفسها لعدة صور إذا احتجت إلى معالجة دفعات.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

لماذا هذه الخطوة مهمة: بدون كائن `OcrEngine` لا يوجد سياق لعملية OCR، وستضطر إلى إدارة معالجة الصورة على مستوى منخفض يدويًا – صداع غير ضروري.

## الخطوة 3 – تحميل الصورة التي تريد التعرف عليها

هنا نقوم بـ **load image for OCR**. طريقة `SetImage` تقبل مسار ملف، أو تدفق، أو حتى مصفوفة بايت.

```csharp
// Path to the source picture
string inputPath = @"C:\Images\sample-photo.jpg";

// Load the image into the engine
ocrEngine.SetImage(inputPath);
```

إذا كانت الصورة موجودة في الذاكرة (مثلاً، تم رفعها عبر API)، يمكنك تمرير `MemoryStream` بدلاً من ذلك:

```csharp
using System.IO;

// Assume `uploadedBytes` contains the image data
using var ms = new MemoryStream(uploadedBytes);
ocrEngine.SetImage(ms);
```

تحميل الصورة بشكل صحيح يضمن أن محرك OCR يرى بيانات البكسل الدقيقة التي يحتاجها لتفسير الأحرف.

## الخطوة 4 – تنفيذ OCR والحصول على مخرجات JSON

الآن نجيب أخيرًا على **how to OCR image** و **how to extract text** في خطوة واحدة. توفر Aspose طريقة `RecognizeToJson` المريحة التي تُعيد النص المعترف به *و* قيم الثقة في سلسلة JSON جاهزة للاستخدام.

```csharp
// Run OCR and receive a JSON string
string ocrResultJson = ocrEngine.RecognizeToJson();
```

يظهر JSON تقريبًا هكذا:

```json
{
  "Text": "Hello World",
  "Confidence": 0.98,
  "Blocks": [
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": [10,20,80,30]
    },
    {
      "Text": "World",
      "Confidence": 0.97,
      "BoundingBox": [90,20,150,30]
    }
  ]
}
```

لماذا صيغة JSON؟ لأنها تسمح بتمرير النتيجة مباشرة إلى APIs، قواعد البيانات، أو أدوات العرض الأمامية دون تحويل إضافي—مثالية لتدفق **convert image to JSON**.

## الخطوة 5 – حفظ JSON على القرص (أو في أي مكان تريد)

حفظ المخرجات سهل للغاية، بسطر واحد من الكود.

```csharp
string outputPath = @"C:\Images\ocr-result.json";
File.WriteAllText(outputPath, ocrResultJson);
Console.WriteLine($"OCR result saved to {outputPath}");
```

إذا كنت تبني خدمة ويب، يمكنك إرجاع السلسلة مباشرة في استجابة HTTP بدلاً من كتابة ملف.

## مثال كامل يعمل

بتجميع كل ذلك، إليك تطبيق console مستقل يمكنك نسخه ولصقه في مشروع C# جديد وتشغيله فورًا.

```csharp
using System;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        string inputPath = @"C:\Images\input.jpg"; // <-- change to your file
        ocrEngine.SetImage(inputPath);

        // 3️⃣ Perform OCR and obtain JSON with confidence data
        string ocrResultJson = ocrEngine.RecognizeToJson();

        // 4️⃣ Save the JSON output to a file
        string outputPath = @"C:\Images\result.json";
        File.WriteAllText(outputPath, ocrResultJson);

        // 5️⃣ Inform the user
        Console.WriteLine($"OCR result saved to {outputPath} with confidence data.");
    }
}
```

### مخرجات Console المتوقعة

```
OCR result saved to C:\Images\result.json with confidence data.
```

وعند فتح `result.json` سيظهر حمولة JSON منظمة بشكل جيد جاهزة للمعالجة المت downstream.

## أسئلة شائعة وحالات خاصة

### ماذا لو احتوت الصورة على لغات متعددة؟

Aspose OCR يكتشف النص تلقائيًا، لكن يمكنك فرض لغة للحصول على دقة أفضل:

```csharp
ocrEngine.Language = OcrLanguage.English; // or OcrLanguage.French, etc.
```

### كيف تتعامل مع الصور الكبيرة التي تسبب ضغطًا على الذاكرة؟

قم بتغيير حجم الصورة أو تقليل دقتها قبل تمريرها إلى المحرك:

```csharp
using System.Drawing;

// Load, resize, then set
using var bmp = new Bitmap(inputPath);
using var resized = new Bitmap(bmp, new Size(bmp.Width / 2, bmp.Height / 2));
ocrEngine.SetImage(resized);
```

### هل يمكن الحصول على النص العادي فقط دون غلاف JSON؟

بالتأكيد—استخدم `Recognize` بدلاً من `RecognizeToJson`:

```csharp
string plainText = ocrEngine.Recognize();
```

ولكن إذا كنت تحتاج إلى درجات الثقة أو إحداثيات الكتل، فإن مسار JSON هو الطريقة لـ **convert image to JSON**.

## الخلاصة

أصبح لديك الآن وصفة كاملة وجاهزة للإنتاج لـ **convert image to JSON** باستخدام Aspose OCR في C#. غطى الدرس **how to OCR image**، وأظهر **extract text from image**، وأجاب على **how to extract text** مع بيانات الثقة، وأظهر الطريقة الصحيحة لـ **load image for OCR**.

الخطوات التالية قد تشمل:

- التكرار على مجلد من الصور لمعالجة عشرات الملفات دفعة واحدة.  
- إرسال حمولة JSON إلى Azure Function أو AWS Lambda للتحليل في الوقت الحقيقي.  
- دمج مخرجات OCR مع API ترجمة لبناء خطوط أنابيب متعددة اللغات.

لا تتردد في التجربة—استبدل تنسيق الإدخال، عدّل إعدادات اللغة، أو مرر JSON مباشرة إلى بحيرة البيانات الخاصة بك. إذا واجهت مشكلة، اترك تعليقًا أدناه وسنحلها معًا. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}