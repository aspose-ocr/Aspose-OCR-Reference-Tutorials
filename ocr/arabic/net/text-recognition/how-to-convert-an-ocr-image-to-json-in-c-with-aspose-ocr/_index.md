---
category: general
date: 2026-09-06
description: تحويل صورة OCR إلى JSON في C# باستخدام Aspose.OCR – دليل خطوة بخطوة لاستخراج
  النص من الصورة والحصول على مخرجات JSON.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: ar
lastmod: 2026-09-06
og_description: تحويل صورة OCR إلى JSON في C# باستخدام Aspose.OCR. تعلم كيفية تحميل
  صورة للتعرف الضوئي على الأحرف، واستخراج النص من الصورة، وتحويل النتيجة إلى JSON.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: تحويل صورة OCR إلى JSON في C# – دليل Aspose.OCR الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: كيفية تحويل صورة OCR إلى JSON في C# باستخدام Aspose.OCR
url: /ar/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحويل صورة OCR إلى JSON في C# باستخدام Aspose.OCR

إذا كنت بحاجة إلى **ocr image to json** في تطبيق .NET، يوضح لك هذا الدليل كيفية القيام بذلك باستخدام Aspose.OCR. سنستعرض تحميل صورة للـ OCR، التعرف على النص من الصورة، وتحويل النتيجة إلى JSON حتى تتمكن من استهلاك البيانات في الـ APIs أو قواعد البيانات.

استخراج النص من ملفات الصور هو طلب شائع لمعالجة الفواتير، مسح الإيصالات، ومشاريع الأرشفة. بنهاية هذا الدرس ستتمكن من **convert image to text**، الحصول على النتيجة كنص عادي، وإنشاء حمولة JSON منظمة تحافظ على معلومات التخطيط.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

- .NET 6.0 SDK أو أحدث مثبت  
- Visual Studio 2022 (أو أي محرر يدعم .NET)  
- حزمة Aspose.OCR NuGet (`Aspose.OCR`) مضافة إلى مشروعك  
- صورة نموذجية (`input.jpg`) موجودة في مجلد يمكنك الإشارة إليه من الشيفرة  

لا تحتاج إلى أي محركات OCR إضافية؛ Aspose.OCR يتولى كل العمل داخليًا.

## الخطوة 1: تثبيت حزمة Aspose.OCR NuGet

افتح طرفية في مجلد مشروعك وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

تتضمن الحزمة الفئة `Aspose.OCR.OcrEngine`، التي توفر طرقًا لـ **load image for ocr**، اختيار اللغة، وتصدير النتيجة.

## الخطوة 2: إنشاء مشروع C# Console جديد

إذا لم يكن لديك مشروع بعد، أنشئ واحدًا:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

أضف توجيهات `using` التي ستحتاجها:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## الخطوة 3: تحميل الصورة وتكوين محرك OCR

الشيفرة التالية توضح كيفية **load image for ocr**، ضبط اللغة، وتحضير المحرك للمعالجة. في هذا المثال نستخدم السيريليكية، لكن يمكنك التبديل إلى `OcrLanguage.English`، `OcrLanguage.French`، إلخ، حسب لغة المصدر.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **لماذا هذا مهم:** ضبط اللغة الصحيحة يحسن الدقة بشكل كبير عندما تقوم بـ **recognize text from photo**. يستخدم المحرك قواميس ومجموعات أحرف مخصصة لكل لغة.

## الخطوة 4: تشغيل عملية OCR واسترجاع النتائج

الآن شغّل محرك OCR. إذا نجحت العملية، يمكنك **extract text from image** كنص عادي، HTML، أو JSON. توفر Aspose.OCR طريقة `SaveJson` التي تكتب النتيجة المنظمة إلى ملف.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### بنية JSON المتوقعة

ملف `output.json` النموذجي يبدو هكذا (منسق للقراءة):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

تحتوي حمولة JSON على نص كل سطر، درجة الثقة، والمستطيل الذي يحيط بالسطر في الصورة الأصلية. هذا يجعل من السهل ربط نتيجة OCR بعناصر الواجهة أو حقول قاعدة البيانات.

## الخطوة 5: الشيفرة الكاملة للعرض التجريبي

فيما يلي البرنامج الكامل الجاهز للتنفيذ الذي يقوم بعملية **ocr image to json**. انسخه إلى `Program.cs` وشغّل `dotnet run`.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### تشغيل المثال

1. ضع صورة باسم `input.jpg` في جذر المشروع.  
2. نفّذ الأمر `dotnet run`.  
3. راقب مخرجات الكونسول وافتح `output.json` لرؤية البيانات المنظمة.

## نصائح احترافية ومشكلات شائعة

| الحالة | التوصية |
|-----------|----------------|
| **صور منخفضة الدقة** | زد الـ DPI قبل المعالجة أو استخدم `ocrEngine.Image = ImageStream.FromFile(path, 300)` لفرض 300 DPI. |
| **لغات مختلطة** | اضبط `ocrEngine.Language = OcrLanguage.Multilingual` ويمكنك إمداد قائمة لغات عبر `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }`. |
| **مستندات كبيرة** | عالج صفحة واحدة في كل مرة لتقليل استهلاك الذاكرة؛ يدعم المحرك ملفات TIFF متعددة الصفحات. |
| **أحرف غير صحيحة** | تحقق من اختيار `OcrLanguage` الصحيح؛ اختيار لغة غير مناسبة يقلل الدقة عند **convert image to text**. |
| **JSON يفتقد حقولًا** | تأكد من أنك تستخدم Aspose.OCR الإصدار 23.6 أو أحدث؛ الإصدارات القديمة لم تكن توفر طريقة `SaveJson`. |

## الأسئلة المتكررة

**س: هل يمكن الحصول على نتيجة OCR كمصفوفة بايت بدلاً من ملف؟**  
ج: نعم. استخدم `ocrEngine.SaveJson(Stream)` للكتابة مباشرة إلى `MemoryStream`، ثم استدعِ `stream.ToArray()`.

**س: هل يدعم المحرك إدخال PDF؟**  
ج: يمكن لـ Aspose.OCR قبول صفحات PDF محوّلة إلى صور عبر Aspose.PDF، لكن محرك OCR نفسه يعمل على الصور النقطية. حوّل ملفات PDF إلى صور أولاً، ثم **load image for ocr**.

**س: كيف أتعامل مع النصوص من اليمين إلى اليسار مثل العربية؟**  
ج: اضبط `ocrEngine.Language = OcrLanguage.Arabic`. يتضمن JSON اتجاه النص الصحيح، ويمكنك عرضه في أطر UI تدعم RTL.

## الخلاصة

الآن لديك حل كامل لـ **ocr image to json** في C#. من خلال تحميل صورة، ضبط اللغة، تشغيل محرك OCR، وتصدير النتيجة كـ JSON، يمكنك **extract text from image**، **convert image to text**، و**recognize text from photo** في سير عمل موحد وسلس.

من هنا يمكنك استكشاف:

- دمج مخرجات JSON مع Web API (`ASP.NET Core`)  
- تخزين النتيجة في قاعدة NoSQL مثل MongoDB  
- إضافة معالجة لاحقة لتصحيح أخطاء OCR الشائعة  

لا تتردد في تجربة لغات، صيغ صور، وخيارات إخراج مختلفة لتناسب احتياجات مشروعك. Happy coding!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن شيفرات عمل كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [recognize text from image in C# – Complete Guide to OCR and JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}