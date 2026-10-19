---
category: general
date: 2026-04-26
description: استخراج النص من الصورة باستخدام C# و Aspose.OCR وتعلم كيفية تحويل الصورة
  إلى صيغ JSON و XML في دقائق.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: ar
og_description: استخراج النص من الصورة في C# باستخدام Aspose.OCR. تعلم خطوة بخطوة
  كيفية تحويل النتيجة إلى JSON و XML فورًا.
og_title: استخراج النص من الصورة في C# – التحويل إلى JSON و XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: استخراج النص من الصورة في C# – التحويل إلى JSON و XML
url: /ar/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة في C# – التحويل إلى JSON & XML

هل احتجت يوماً إلى **استخراج النص من الصورة** في مشروع .NET لكن شعرت بالحيرة حول “كيف أحصل على البيانات فعلياً؟” لست وحدك. في العديد من التطبيقات الواقعية—مثل معالجة الفواتير، مسح الإيصالات، أو التحقق من البطاقات—استخراج الأحرف الخام من صورة هو الخطوة الأولى والحاسمة.  

الأخبار السارة؟ مع Aspose.OCR يمكنك القيام بذلك ببضع أسطر، ثم تحويل الصورة فوراً إلى **JSON** أو **XML** للأنظمة اللاحقة. في هذا الدليل سنستعرض الكود الكامل الجاهز للتنفيذ، نشرح لماذا كل جزء مهم، ونظهر لك بعض الحيل لتجنب المشكلات الشائعة.

---

## ما ستحتاجه

- **.NET 6+** (أي مجموعة تطوير حديثة تعمل؛ العينة تستهدف .NET 6)
- **Aspose.OCR for .NET** حزمة NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- ملف صورة (PNG, JPG, إلخ) يحتوي على نص قابل للطباعة؛ سنستخدم `invoice.png` كمثال.
- محرر كود—Visual Studio، VS Code، أو Rider—أيًا كان ما تفضله.

هذا كل شيء. لا محركات OCR إضافية، لا خدمات خارجية، فقط حزمة NuGet واحدة.

---

## الخطوة 1: إعداد محرك OCR – كيفية استخراج النص من الصورة

أولاً نقوم بإنشاء كائن `OcrEngine` ونشير به إلى ملف الصورة. هذه الخطوة هي الأساس؛ بدون تحميل الصورة بشكل صحيح لا يستطيع المحرك التعرف على أي شيء.

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**لماذا هذا مهم:**  
- `OcrEngine` يضم جميع عمليات ما قبل معالجة الصورة منخفضة المستوى (التثبيت الثنائي، تصحيح الميل).  
- تحميل الصورة عبر `ImageStream.FromFile` يضمن أن المحرك يقرأ البايتات الدقيقة، مع الحفاظ على DPI وعمق اللون—كلاهما يمكن أن يؤثر على دقة التعرف.  

> **نصيحة احترافية:** إذا كانت صور المصدر في تدفق (مثلاً، تم تحميلها عبر واجهة ويب API)، استخدم `ImageStream.FromStream(yourStream)` بدلاً من `FromFile`.

---

## الخطوة 2: إخبار المحرك باللغة المتوقعة – استخراج النص من الصورة بدقة

يدعم Aspose.OCR العديد من الأبجديات. تحديد اللغة الصحيحة يحد من مجموعة الأحرف ويزيد الدقة.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**لماذا:**  
عند تعيين `Language.Latin`، يتجاهل محرك OCR الحروف السيريالية أو الآسيوية، مما يقلل الإيجابيات الزائفة. إذا احتجت لاحقًا معالجة مستندات متعددة اللغات، يمكنك التحويل إلى `Language.Multilingual` أو دمج لغات.

---

## الخطوة 3: تشغيل عملية التعرف – استخراج النص من الصورة في مكالمة واحدة

الآن نقوم فعليًا بالتعرف على النص. طريقة `Recognize` تُعيد كائن `RecognitionResult` الذي يحتوي على النص الخام، درجات الثقة، وحتى بيانات التخطيط.

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**لماذا:**  
استدعاء `Recognize` مرة واحدة يكفي لأن المحرك يقوم داخليًا بعمليات ما قبل المعالجة، التجزئة، وتصنيف الأحرف. خاصية `Text` تعطيك تمثيل نصي بسيط، مثالي للتسجيل أو التحقق السريع.

---

## الخطوة 4: تحويل النتيجة إلى JSON – تحويل الصورة إلى JSON بسهولة

العديد من الخدمات الحديثة تفضل حمولات JSON. يوفر Aspose.OCR طريقة `ToJson` المريحة التي تسلسل كامل `RecognitionResult`، بما في ذلك قيم الثقة ومربعات الحدود.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**لماذا قد ترغب في JSON:**  
- **قابلية التفاعل:** تطبيقات الواجهة الأمامية (React, Angular) يمكنها استهلاك JSON مباشرة.  
- **التصحيح:** يتضمن JSON ثقة لكل حرف، مما يتيح لك وضع علامة على الكلمات ذات الثقة المنخفضة للمراجعة اليدوية.  

> **حالة خاصة:** إذا كان نظامك اللاحق يحتاج فقط النص العادي، يمكنك استخراج `recognitionResult.Text` وتغليفه في كائن JSON مخصص بدلاً من الحمولة الكاملة لـ Aspose.

---

## الخطوة 5: تحويل النتيجة إلى XML – تحويل الصورة إلى XML للأنظمة القديمة

لا تزال بعض المؤسسات تعتمد على مخططات XML لتبادل البيانات. طريقة `ToXml` تعكس `ToJson` لكنها تُنتج XML.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**لماذا XML:**  
- **تحقق المخطط:** يمكنك تعريف XSD يطابق البنية التي ينتجها Aspose، مما يضمن الالتزام بالعقد.  
- **التكامل:** غالبًا ما تقوم أنظمة ERP أو إدارة المستندات القديمة بتحليل XML مباشرةً.

---

## مثال كامل يعمل – كود شامل

فيما يلي البرنامج الكامل الذي يجمع كل شيء معًا. انسخه والصقه في مشروع وحدة تحكم جديد (`dotnet new console`) وشغّله.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**المخرجات المتوقعة (وحدة التحكم):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

ستحتوي ملفات JSON و XML على بنية أغنى، على سبيل المثال:

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت الصورة غير واضحة أو مائلة؟

يقوم Aspose.OCR تلقائيًا بتصحيح ميل معظم الصور، ولكن في الحالات القصوى قد ترغب في ما قبل المعالجة باستخدام `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)`. إضافة تعزيز بسيط للتباين (`ImageProcessor.AdjustContrast`) يمكن أيضًا تحسين درجة الثقة.

### هل يمكنني استخراج النص من ملفات PDF؟

نعم—قم بتحويل كل صفحة PDF إلى صورة أولاً (مثلاً باستخدام Aspose.PDF أو مكتبة مجانية مثل PDFium) ثم أدخل تلك الصور في نفس تدفق OCR.

### كيف أتعامل مع لغات متعددة في مستند واحد؟

عيّن `ocrEngine.Language = Language.Multilingual;` أو دمج لغات محددة:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

كن على علم أن مجموعات اللغات الأوسع قد

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}