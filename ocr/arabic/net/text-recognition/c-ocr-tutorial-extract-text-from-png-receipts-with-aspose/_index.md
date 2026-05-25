---
category: general
date: 2026-05-25
description: دروس OCR بلغة C# تُظهر كيفية تحميل ملف صورة C# والتعرف على نص PNG من
  إيصال باستخدام Aspose OCR – دليل خطوة بخطوة.
draft: false
keywords:
- c# OCR tutorial
- load image file c#
- recognize png text
- read receipt OCR
- perform OCR image
language: ar
og_description: دروس OCR بلغة C# التي ترشدك خلال تحميل ملف صورة C# والتعرف على نص
  PNG من إيصال باستخدام Aspose OCR.
og_title: دورة OCR بلغة C# – استخراج النص من إيصالات PNG
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: c# OCR tutorial that shows how to load image file c# and recognize
    png text from a receipt using Aspose OCR – step‑by‑step guide.
  headline: 'c# OCR tutorial: Extract Text from PNG Receipts with Aspose'
  type: TechArticle
- description: c# OCR tutorial that shows how to load image file c# and recognize
    png text from a receipt using Aspose OCR – step‑by‑step guide.
  name: 'c# OCR tutorial: Extract Text from PNG Receipts with Aspose'
  steps:
  - name: Why Aspose?
    text: Aspose OCR supports over 30 languages, works offline, and returns a rich
      `OcrResult` object—perfect for **perform OCR image** tasks where you need more
      than just plain text.
  - name: Handling Common Edge Cases
    text: '| Situation | What to do | |-----------|------------| | **Image is blurry**
      | Pre‑process with `System.Drawing` to sharpen or increase DPI. | | **Receipt
      contains multiple languages** | Set `ocrEngine.Language = OcrLanguage.English
      | OcrLanguage.Spanish;` | | **Large batch processing** | Reuse a sin'
  - name: What’s Next?
    text: '- Experiment with **load image file c#** using `SkiaSharp` for true cross‑platform
      support. - Dive deeper into `OcrResult.Words` to extract line items, prices,
      and dates—perfect for expense‑tracking apps. - Combine this tutorial with Azure
      Functions or AWS Lambda to build a serverless receipt‑proces'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: 'دورة OCR بلغة C#: استخراج النص من إيصالات PNG باستخدام Aspose'
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-png-receipts-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# OCR – استخراج النص من إيصالات PNG باستخدام Aspose

هل احتجت إلى **دليل c# OCR** ينجز المهمة فعلاً دون الحاجة للبحث المستمر على جوجل؟ أنت في المكان الصحيح. في هذا الدليل سنقوم بـ **تحميل ملف صورة c#**، **التعرف على نص PNG**، و **قراءة نتائج OCR للإيصال**، كل ذلك مع إظهار كيفية **أداء معالجة صورة OCR** باستخدام Aspose OCR.

سنبدأ بتثبيت حزمة NuGet المطلوبة، نتناول كل سطر من الشيفرة، وننتهي بتفريغ JSON مرتب يمكنك تمريره مباشرة إلى خط أنابيب البيانات التالي. لا إطالة، مجرد حل عملي جاهز للتنفيذ.

## ما ستتعلمه

- كيفية إعداد Aspose OCR في مشروع .NET 6 (أو أحدث).  
- الخطوات الدقيقة لـ **تحميل ملف صورة c#** وتمريره إلى المحرك.  
- كيفية **التعرف على نص PNG** من صورة إيصال والتقاط النتيجة.  
- طرق **قراءة OCR للإيصال** كـ JSON منسق بشكل جميل.  
- نصائح لـ **أداء معالجة صورة OCR** على أنواع ملفات مختلفة ومعالجة المشكلات الشائعة.

**المتطلبات المسبقة**  
- Visual Studio 2022 (أو أي بيئة تطوير تفضلها).  
- .NET 6 SDK أو أحدث.  
- صورة إيصال بصيغة PNG جاهزة (سنسميها `receipt.png`).  

إذا كان لديك هذه المتطلبات، لنبدأ.

![c# OCR tutorial screenshot](ocr-demo.png "c# OCR tutorial result showing JSON output")

## دليل c# OCR – إعداد محرك Aspose OCR

أولاً، نحتاج إلى مكتبة Aspose OCR. افتح الطرفية في مجلد الحل وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

هذا الأمر الواحد يجلب كل ما يلزم، بما في ذلك الثنائيات الأصلية لفك ترميز الصور. بعد التثبيت، أنشئ مشروع console جديد أو أضف الشيفرة إلى مشروع موجود.

### لماذا Aspose؟

Aspose OCR يدعم أكثر من 30 لغة، يعمل دون اتصال بالإنترنت، ويعيد كائن `OcrResult` غني—مثالي لمهام **أداء معالجة صورة OCR** حيث تحتاج إلى أكثر من مجرد نص عادي.

## تحميل ملف صورة c# وتحضير الإيصال

الآن بعد أن أصبحت المكتبة جاهزة، لنقم بـ **تحميل ملف صورة c#**. فئة `System.Drawing.Image` تقوم بالعمل الشاق، لكن يمكنك أيضاً استخدام `SkiaSharp` إذا كنت تفضل بديلًا متعدد المنصات.

```csharp
using System;
using System.Drawing;               // For Image loading
using Aspose.OCR;                  // OCR engine
using System.Text.Json;            // JSON serialization

// Step 1: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most receipts; change as needed
    Language = OcrLanguage.English
};

// Step 2: Load the image to be processed
// Replace the path with the actual location of your receipt PNG
string imagePath = @"C:\Receipts\receipt.png";
if (!File.Exists(imagePath))
{
    Console.WriteLine($"File not found: {imagePath}");
    return;
}
using Image receiptImage = Image.FromFile(imagePath);
```

> **نصيحة احترافية:** ضع الـ `Image` داخل عبارة `using` (كما هو موضح) لتحرير الموارد الأصلية بسرعة—وهذا مهم خاصةً عندما تقوم بـ **أداء معالجة صورة OCR** على العديد من الملفات داخل حلقة.

## التعرف على نص PNG باستخدام Aspose

مع الصورة في الذاكرة، يمكن للمحرك الآن **التعرف على نص PNG**. Aspose يعيد كائن `OcrResult` يحتوي على السلسلة الخام وبيانات مفصلة عن كل كلمة تم التعرف عليها.

```csharp
// Step 3: Perform OCR and obtain the result object
OcrResult ocrResult = ocrEngine.RecognizeWithResult(receiptImage);

// Quick sanity check – was anything recognized?
if (string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("No text detected. Verify image quality or language settings.");
    return;
}
```

لماذا نستدعي `RecognizeWithResult` بدلاً من `Recognize` الأبسط؟ الأول يمنحك إمكانية الوصول إلى درجات الثقة، الصناديق المحيطة، وفواصل الأسطر—مفيد إذا احتجت لاحقًا إلى **قراءة OCR للإيصال** لاستخراج بنود الفاتورة.

## قراءة نتيجة OCR للإيصال كـ JSON

معظم الأنظمة المت downstream تفضل JSON، لذا لنقوم بتسلسل `OcrResult`. مُسلسل `System.Text.Json` يتعامل مع الكائنات المعقدة بسلاسة، وسنُفعّل المسافات البادئة للقراءة السهلة.

```csharp
// Step 4: Convert the OCR result to a readable JSON string (indented)
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

الناتج JSON يبدو تقريبًا هكذا (مقتطع للاختصار):

```json
{
  "Text": "Walmart\n123 Main St\nTotal $12.34",
  "Words": [
    {
      "Text": "Walmart",
      "Confidence": 0.98,
      "Rectangle": { "X": 10, "Y": 20, "Width": 150, "Height": 30 }
    },
    {
      "Text": "Total",
      "Confidence": 0.95,
      "Rectangle": { "X": 10, "Y": 150, "Width": 80, "Height": 25 }
    }
  ]
}
```

يمكنك الآن تمرير `jsonResult` إلى قاعدة بيانات، طابور رسائل، أو ببساطة تسجيله للتصحيح.

## أداء معالجة صورة OCR وعرض النتيجة

أخيرًا، نطبع الـ JSON على وحدة التحكم. في تطبيق واقعي قد تكتبها إلى ملف أو ترسلها عبر HTTP، لكن وحدة التحكم تجعل من السهل التحقق من أن كل شيء يعمل.

```csharp
// Step 5: Output the JSON to the console
Console.WriteLine("=== OCR Result (JSON) ===");
Console.WriteLine(jsonResult);
```

شغّل البرنامج (`dotnet run`) وسترى الـ JSON المنسق يُطبع. إذا كانت صورة الإيصال واضحة، سيكون النص دقيقًا؛ إذا لم يكن كذلك، فكر في زيادة دقة الصورة أو تطبيق فلتر تمهيدي (مثل تحويل إلى تدرج رمادي، تعزيز التباين) قبل إرساله إلى المحرك.

### التعامل مع الحالات الشائعة

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **الصورة غير واضحة** | قم بتمهيدها باستخدام `System.Drawing` لتوضيحها أو زيادة DPI. |
| **الإيصال يحتوي على لغات متعددة** | عيّن `ocrEngine.Language = OcrLanguage.English \| OcrLanguage.Spanish;` |
| **معالجة دفعات كبيرة** | أعد استخدام كائن `OcrEngine` واحد؛ غير الـ `Image` فقط في كل دورة. |
| **ضغط الذاكرة** | حرّر كائنات `Image` فورًا وفكّر في استخدام `await Task.Run` للخطوط غير المتزامنة. |

هذه التعديلات تحافظ على سير عمل **أداء معالجة صورة OCR** قوي حتى عندما لا تكون المدخلات مثالية.

## الخلاصة

تهانينا—لقد أكملت **دليل c# OCR** الذي يحمل صورة، **يتعرف على نص PNG**، و **يقرأ نتيجة OCR للإيصال** كـ JSON نظيف. الخطوات الأساسية (إعداد المحرك، تحميل الصورة، تنفيذ OCR، التسلسل، والعرض) تشكل أساسًا صلبًا يمكنك توسيعه لتشمل الفواتير، جوازات السفر، أو أي مستند ممسوح ضوئيًا آخر.

### ما التالي؟

- جرّب **تحميل ملف صورة c#** باستخدام `SkiaSharp` لدعم متعدد المنصات حقيقي.  
- تعمق في `OcrResult.Words` لاستخراج بنود الفاتورة، الأسعار، والتواريخ—مثالي لتطبيقات تتبع النفقات.  
- اجمع هذا الدليل مع Azure Functions أو AWS Lambda لبناء API لمعالجة الإيصالات بدون خادم.  

لا تتردد في تعديل الشيفرة، إضافة المزيد من الصور، أو حتى تغيير حزمة اللغة. عالم OCR مليء بالمفاجآت، والآن لديك الأدوات لاستكشافها.

برمجة سعيدة، ولتظل إيصالاتك دائمًا قابلة للقراءة!

## دروس ذات صلة

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use OCR - Recognize Image without Text Area Detection](/ocr/english/net/image-and-drawing-recognition/recognize-image-without-text-area-detection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}