---
category: general
date: 2026-07-05
description: تعلم كيفية تنفيذ OCR في C# باستخدام Aspose.OCR، وضبط اللغة، وتحميل صورة
  OCR، وتحويل PNG إلى JSON في بضع خطوات سهلة.
draft: false
keywords:
- how to perform OCR
- how to set language
- convert png to json
- load image ocr
- set ocr language
language: ar
og_description: كيفية تنفيذ OCR في C# باستخدام Aspose.OCR، تعيين لغة OCR، تحميل صورة
  OCR، وتحويل PNG إلى JSON—كل ذلك في دليل مختصر واحد.
og_title: كيفية تنفيذ OCR باستخدام Aspose.OCR – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to perform OCR in C# using Aspose.OCR, set language, load
    image OCR, and convert PNG to JSON in a few easy steps.
  headline: How to Perform OCR with Aspose.OCR – Complete C# Guide
  type: TechArticle
- description: Learn how to perform OCR in C# using Aspose.OCR, set language, load
    image OCR, and convert PNG to JSON in a few easy steps.
  name: How to Perform OCR with Aspose.OCR – Complete C# Guide
  steps:
  - name: – Install the Aspose.OCR NuGet Package
    text: 'Before you can even think about **how to perform OCR**, the library has
      to be on your machine. Open a terminal in your project folder and run:'
  - name: – Load the Image for OCR (load image OCR)
    text: 'Now that the package is ready, you need to **load image OCR**. The engine
      expects an `ImageStream`, which you can create from a file path, a `MemoryStream`,
      or even a byte array. Here’s the simplest approach using a PNG file on disk:'
  - name: – Set the OCR Language (how to set language / set OCR language)
    text: Aspose.OCR supports over 60 languages, but it defaults to English. If your
      document is in another language, you must tell the engine which one to use.
      That’s where **how to set language** and **set OCR language** come into play.
  - name: – Perform OCR and Convert PNG to JSON
    text: 'With the image loaded and the language set, the final piece is to run the
      OCR engine and **convert PNG to JSON**. Aspose.OCR makes this a one‑liner:'
  - name: Full Working Example (All Steps Combined)
    text: 'Putting everything together, here’s a compact program you can compile and
      run instantly:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: كيفية تنفيذ OCR باستخدام Aspose.OCR – دليل C# الكامل
url: /ar/net/ocr-configuration/how-to-perform-ocr-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إجراء OCR باستخدام Aspose.OCR – دليل C# كامل

هل تساءلت يومًا **كيف تقوم بإجراء OCR** على فاتورة ممسوحة ضوئيًا دون كتابة الكثير من الشيفرة المتكررة؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى استخراج النص من الصور، خاصةً عندما يجب أن يكون التنسيق اللاحق JSON لتسهيل الاستهلاك.

في هذا الدرس ستتعرف بالضبط على **كيفية إجراء OCR** باستخدام مكتبة Aspose.OCR، وتتعلم **كيفية تعيين اللغة**، وتكتشف أفضل طريقة لـ **تحميل صورة OCR**، وتحصل على مقتطف جاهز للتنفيذ **يحوّل PNG إلى JSON**. في النهاية ستحصل على حل قوي وجاهز للإنتاج يمكنك دمجه في أي مشروع .NET.

---

![مخطط يوضح كيفية إجراء OCR باستخدام Aspose.OCR في C#](ocr-flow.png "كيفية إجراء OCR")

## ما ستتعلمه

- المتطلبات الدنيا لتشغيل Aspose.OCR.  
- شيفرة خطوة بخطوة **تحمّل صورة OCR**، تختار اللغة الصحيحة، وت **تحوّل PNG إلى JSON**.  
- لماذا يهم تعيين لغة OCR الصحيحة وكيفية القيام بذلك بأمان.  
- المشكلات الشائعة (ملفات كبيرة، لغات غير مدعومة) وكيفية تجنبها.  
- مثال كامل قابل للتنفيذ يمكنك نسخه ولصقه الآن.

---

## كيفية إجراء OCR باستخدام Aspose.OCR في C#

### الخطوة 1 – تثبيت حزمة Aspose.OCR NuGet

قبل أن تتمكن حتى من التفكير في **كيفية إجراء OCR**، يجب أن تكون المكتبة موجودة على جهازك. افتح طرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

هذا السطر الواحد يجلب أحدث نسخة مستقرة (اعتبارًا من يوليو 2026، الإصدار 23.10). لا ملفات DLL إضافية، لا إعداد يدوي—فقط إشارة حزمة نظيفة.

### الخطوة 2 – تحميل الصورة لـ OCR (load image OCR)

الآن بعد أن أصبحت الحزمة جاهزة، تحتاج إلى **load image OCR**. المحرك يتوقع `ImageStream`، ويمكنك إنشاؤه من مسار ملف، أو `MemoryStream`، أو حتى مصفوفة بايت. إليك أبسط طريقة باستخدام ملف PNG على القرص:

```csharp
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

// Create an OCR engine instance
var engine = new OcrEngine();

// Load the image you want to process
engine.Image = ImageStream.FromFile(@"C:\Invoices\invoice.png");

// Optional: verify that the image was loaded
if (engine.Image == null)
{
    throw new InvalidOperationException("Failed to load the image. Check the file path.");
}
```

> **لماذا هذا مهم:** تحميل الصورة بشكل صحيح هو أساس أي خط أنابيب OCR. إذا لم تُحمَّل الصورة، سيطرح المحرك استثناءً غامضًا `NullReferenceException`، وهو كابوس في عملية التصحيح.

### الخطوة 3 – تعيين لغة OCR (how to set language / set OCR language)

يدعم Aspose.OCR أكثر من 60 لغة، لكنه يفرض اللغة الإنجليزية افتراضيًا. إذا كان مستندك بلغة أخرى، يجب أن تخبر المحرك أي لغة يستخدمها. هنا يأتي دور **how to set language** و **set OCR language**.

```csharp
// Specify the language of the text in the image
engine.Language = OcrLanguage.English; // Change to OcrLanguage.Spanish, etc.

// You can also set multiple languages if needed
// engine.Language = OcrLanguage.English | OcrLanguage.French;
```

> **نصيحة:** عيّن اللغة صراحةً دائمًا. حتى إذا كان نصك بالإنجليزية، فإن تعيين `OcrLanguage.English` صراحةً يمكن أن يحسن الدقة لأن المحرك يتخطى خطوة اكتشاف اللغة.

### الخطوة 4 – تنفيذ OCR وتحويل PNG إلى JSON

مع تحميل الصورة وتعيين اللغة، الجزء الأخير هو تشغيل محرك OCR و **convert PNG to JSON**. تجعل Aspose.OCR ذلك في سطر واحد:

```csharp
// Perform OCR and save the recognized text as JSON
engine.Save(@"C:\Invoices\invoice.json", OcrOutputFormat.Json);
```

الناتج بصيغة JSON يبدو هكذا:

```json
{
  "Pages": [
    {
      "Text": "Invoice #12345\nDate: 2026-07-01\nTotal: $1,250.00\n..."
    }
  ]
}
```

هذه البنية مثالية لواجهات برمجة التطبيقات اللاحقة، أو إدخالات قاعدة البيانات، أو معاينات واجهة المستخدم السريعة.

### مثال كامل يعمل (جميع الخطوات مجمعة)

بدمج كل شيء معًا، إليك برنامجًا مختصرًا يمكنك تجميعه وتشغيله فورًا:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        var engine = new OcrEngine();

        // 2️⃣ Load the PNG image (load image OCR)
        string inputPath = @"C:\Invoices\invoice.png";
        engine.Image = ImageStream.FromFile(inputPath);
        if (engine.Image == null)
        {
            Console.WriteLine($"Unable to load image from {inputPath}");
            return;
        }

        // 3️⃣ Set the language (how to set language / set OCR language)
        engine.Language = OcrLanguage.English; // Adjust as needed

        // 4️⃣ Run OCR and write JSON (convert PNG to JSON)
        string outputPath = @"C:\Invoices\invoice.json";
        engine.Save(outputPath, OcrOutputFormat.Json);

        Console.WriteLine($"OCR complete! JSON saved to {outputPath}");
    }
}
```

**المخرجات المتوقعة على وحدة التحكم:**

```
OCR complete! JSON saved to C:\Invoices\invoice.json
```

افتح ملف JSON وسترى النص المستخرج جاهزًا لأي غرض تحتاجه بعد ذلك.

---

## الحالات الشائعة وكيفية التعامل معها

| الحالة | ما يجب مراقبته | الحل الموصى به |
|-----------|-------------------|-----------------|
| **PNG كبير (>10 MB)** | ارتفاع استهلاك الذاكرة، معالجة أبطأ | قلل حجم الصورة أولًا باستخدام `engine.Image = ImageStream.FromFile(...).Resize(1024, 0)` |
| **لغة غير مدعومة** | `ArgumentException` عند تعيين `engine.Language` | تحقق من قائمة اللغات المدعومة عبر `OcrLanguage.GetSupportedLanguages()` |
| **ملف صورة تالف** | `InvalidOperationException` عند التحميل | غلف عملية التحميل بـ `try/catch` وتحقق من وجود الملف باستخدام `File.Exists` |
| **الحاجة إلى نص عادي بدلاً من JSON** | تنسيق الإخراج غير صحيح | استخدم `engine.Save(outputPath, OcrOutputFormat.PlainText)` |

بتوقع هذه السيناريوهات ستتجنب المشكلات الشائعة مثل “لماذا فشل OCR لدي؟”.

---

## نصائح احترافية لتحسين الدقة

1. **معالجة مسبقة للصورة** – زد التباين أو حوّلها إلى تدرج رمادي قبل تمريرها إلى المحرك. يقدم Aspose.OCR الدالة `engine.Image = engine.Image.AdjustContrast(1.2f)` لتعديلات سريعة.  
2. **إزالة الميلان من المسحات المائلة** – استخدم `engine.Image = engine.Image.Deskew()` إذا لم يكن المستند محاذيًا تمامًا.  
3. **المعالجة الدفعية** – عند التعامل مع عشرات الفواتير، أعد استخدام نفس كائن `OcrEngine`؛ فهو يخزن نماذج اللغات في الذاكرة ويسرّع الاستدعاءات اللاحقة.  
4. **التحقق من صحة JSON** – بعد الحفظ، نفّذ فحص مخطط سريع لضمان توافق الإخراج مع العقود اللاحقة.

---

## ملخص: كيفية إجراء OCR من البداية إلى النهاية

- ثبّت Aspose.OCR عبر NuGet.  
- **Load image OCR** باستخدام `ImageStream.FromFile`.  
- **Set OCR language** (أو **how to set language**) باستخدام `engine.Language`.  
- استدعِ `engine.Save(..., OcrOutputFormat.Json)` لـ **convert PNG to JSON**.  

هذا هو سير العمل الكامل لـ **كيفية إجراء OCR** بطريقة نظيفة وقابلة للصيانة.

---

## ما التالي؟

- جرّب **set OCR language** للفواتير متعددة اللغات (مثلاً English | Spanish).  
- استبدل `OcrOutputFormat.Json` بـ `OcrOutputFormat.PlainText` إذا كنت تحتاج فقط سلاسل نصية خام.  
- دمج مخرجات JSON في Azure Function أو AWS Lambda للمعالجة بدون خادم.  

لا تتردد في تعديل المثال، إضافة سجلات الأخطاء، أو تغليفه في فئة خدمة قابلة لإعادة الاستخدام. السماء هي الحد عندما تتقن أساسيات **كيفية إجراء OCR** باستخدام Aspose.OCR.

برمجة سعيدة، ولتكن استخراج النصوص دائمًا دقيقة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}