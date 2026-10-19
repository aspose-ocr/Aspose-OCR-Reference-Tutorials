---
category: general
date: 2026-01-09
description: التعرف على النص في ملفات JPG بسرعة باستخدام Aspose OCR في C#. تعلم كيفية
  استخراج النص من الصورة، وتحويل الصورة إلى JSON و EPUB في دليل واحد.
draft: false
keywords:
- recognize text in jpg
- extract text from image
- convert image to json
- convert image to epub
- create epub from image
language: ar
og_description: التعرف على النص في ملف JPG باستخدام Aspose OCR. يوضح هذا الدليل كيفية
  استخراج النص من الصورة، وتحويل الصورة إلى JSON و EPUB، وإنشاء ملف ePub من صورة.
og_title: التعرف على النص في ملف JPG – دليل C# الكامل
tags:
- Aspose OCR
- C#
- Image Processing
title: التعرف على النص في ملفات JPG باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/recognize-text-in-jpg-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص في JPG – دليل C# كامل

هل احتجت يومًا إلى **التعرف على النص في ملفات JPG** لكن لم تكن متأكدًا أي مكتبة تختار؟ لست وحدك. يواجه العديد من المطورين نفس المشكلة عندما يحاولون استخراج الكلمات من صورة فوتوغرافية أو مستند ممسوح ضوئيًا للمرة الأولى.  

الخبر السار؟ مع Aspose OCR يمكنك **استخراج النص من صورة** ببضع أسطر من كود C#، ثم **تحويل الصورة إلى JSON** أو حتى **تحويل الصورة إلى EPUB**—كل ذلك دون مغادرة بيئة التطوير المتكاملة الخاصة بك.

في هذا الدرس سنستعرض سير العمل بالكامل: من تثبيت حزم NuGet المناسبة، مرورًا بالتعرف على النص في JPG، إلى حفظ النتيجة كملف JSON منظم وكمستند ePub. في النهاية ستتمكن من **إنشاء ePub من صورة** برمجيًا، وهو خدعة مفيدة لمنصات التعلم الإلكتروني، المكتبات الرقمية، أو أي تطبيق يحتاج إلى كتب إلكترونية قابلة للبحث.

---

## ما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.6+). يعمل الكود على أي بيئة تشغيل حديثة.
- حزمة NuGet **Aspose.OCR** – محرك OCR الأساسي.
- حزمة NuGet **Aspose.Publishing** – مطلوبة لتنسيق الإخراج ePub.
- ملف صورة باسم `input.jpg` موجود في مكان ما على قرصك (استبدل المسار بمسارك الخاص).
- محرر نصوص أو بيئة تطوير (Visual Studio، VS Code، Rider—اختر ما يناسبك).

هذا كل ما تحتاجه. لا خدمات إضافية، لا واجهات برمجة تطبيقات خارجية، فقط مكتبتان وملف JPG.

---

## الخطوة 1: إعداد المشروع **للتعرف على النص في JPG**

أولًا، أنشئ تطبيقًا جديدًا من نوع console (أو أضف إلى مشروع موجود). ثم أضف الحزمتين Aspose عبر مدير حزم NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.Publishing
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن *Aspose.OCR* و*Aspose.Publishing*، ثم اضغط **Install**.

هذه الحزم تجلب لك كل ما تحتاجه **لاستخراج النص من صورة** وإنتاج ملف ePub لاحقًا.

---

## الخطوة 2: **استخراج النص من صورة** باستخدام Aspose OCR

الآن سنكتب الكود الذي يقرأ ملف JPG ويستخرج الأحرف منه.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ImageToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // 2️⃣ Recognize text from the JPG file
            // Replace the path with the location of your own image
            string inputPath = @"YOUR_DIRECTORY\input.jpg";
            var ocrResult = ocrEngine.RecognizeImage(inputPath);

            // 3️⃣ Show the recognized text in the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**لماذا يعمل هذا:** `OcrEngine` ي abstract كل عمليات ما قبل معالجة الصورة، واكتشاف اللغة، وتقسيم الأحرف. كل ما عليك هو توجيهه إلى ملف وستحصل على كائن `OcrResult` يحتوي على النص العادي (`ocrResult.Text`) ومجموعة غنية من البيانات الوصفية.

---

## الخطوة 3: **تحويل الصورة إلى JSON** – تصدير نتيجة OCR

إذا كنت بحاجة لتخزين مخرجات OCR بتنسيق منظم (لـ APIs، قواعد البيانات، أو المعالجة اللاحقة)، تجعل لك Aspose عملية تسلسل النتيجة إلى JSON أمرًا سهلًا.

```csharp
// 4️⃣ Convert the OCR result to JSON
string jsonContent = ocrResult.ToJson();

// 5️⃣ Save the JSON to disk
string jsonPath = @"YOUR_DIRECTORY\output.json";
File.WriteAllText(jsonPath, jsonContent);

Console.WriteLine($"JSON saved to: {jsonPath}");
```

الـ JSON الناتج يبدو تقريبًا هكذا (مقتطع للتبسيط):

```json
{
  "Text": "Hello world!",
  "Confidence": 0.98,
  "PageCount": 1,
  "Words": [
    { "Value": "Hello", "Confidence": 0.99 },
    { "Value": "world!", "Confidence": 0.97 }
  ]
}
```

**متى تستخدمه:** JSON مثالي إذا كنت تُرسل بيانات OCR إلى خدمة ويب، تخزنها في قاعدة NoSQL، أو تحتاج إلى تمثيل قابل للنقل يمكن تحليله بأي لغة برمجة.

---

## الخطوة 4: **تحويل الصورة إلى EPUB** – حفظها ككتاب إلكتروني

تضيف Aspose Publishing دعمًا لعدة تنسيقات كتب إلكترونية، بما في ذلك EPUB. عبر استدعاء `Save` على كائن `OcrResult` يمكنك توليد ملف ePub متوافق بالكامل يحتوي على النص المستخرج، وربما الصورة الأصلية.

```csharp
// 6️⃣ Save the OCR result as an ePub document
string epubPath = @"YOUR_DIRECTORY\output.epub";
ocrResult.Save(epubPath, OcrOutputFormat.Epub);

Console.WriteLine($"EPUB created at: {epubPath}");
```

**ما ستحصل عليه:** ePub يمكنك فتحه بأي قارئ (Calibre، Apple Books، Adobe Digital Editions). الملف يتضمن النص المستخرج كمحتوى قابل للبحث، بالإضافة إلى الصورة الأصلية كطبقة خلفية—مثالي لإنشاء خطوط **إنشاء ePub من صورة**.

---

## الخطوة 5: مثال كامل يعمل – من JPG إلى JSON & EPUB

بجمع كل ما سبق، إليك البرنامج الكامل الجاهز للتنفيذ. انسخه إلى `Program.cs`، عدل مسارات الملفات، ثم اضغط **F5**.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ImageToEpubDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // Path to the input JPG
            string inputPath = @"YOUR_DIRECTORY\input.jpg";

            // Recognize text
            var ocrResult = ocrEngine.RecognizeImage(inputPath);

            // Output recognized text to console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine();

            // Export to JSON
            string jsonPath = @"YOUR_DIRECTORY\output.json";
            File.WriteAllText(jsonPath, ocrResult.ToJson());
            Console.WriteLine($"JSON saved to: {jsonPath}");

            // Export to EPUB
            string epubPath = @"YOUR_DIRECTORY\output.epub";
            ocrResult.Save(epubPath, OcrOutputFormat.Epub);
            Console.WriteLine($"EPUB created at: {epubPath}");
        }
    }
}
```

شغّل البرنامج وسترى ثلاثة أشياء:

1. النص المستخرج يُطبع في وحدة التحكم.
2. ملف `output.json` يحتوي على بيانات OCR المنظمة.
3. ملف `output.epub` يمكنك فتحه بأي قارئ كتب إلكترونية.

---

## أسئلة شائعة وحالات خاصة

- **ماذا لو كانت الصورة PNG أو BMP؟**  
  يدعم Aspose OCR معظم صيغ الصور النقطية (PNG، BMP، TIFF، GIF). فقط غيّر امتداد الملف في `inputPath`؛ سيعمل الكود نفسه.

- **هل يمكن تحديد لغة غير الإنجليزية؟**  
  نعم. عيّن `ocrEngine.Language = OcrLanguage.French;` (أو أي لغة مدعومة) قبل استدعاء `RecognizeImage`.

- **ماذا عن ملفات PDF متعددة الصفحات؟**  
  بالنسبة للـ PDFs، يجب أولًا تحويل كل صفحة إلى صورة (يمكن لـ Aspose.PDF القيام بذلك) ثم تمرير كل صورة إلى `RecognizeImage`. يمكن دمج كائنات `OcrResult` الناتجة قبل تصديرها إلى JSON أو EPUB.

- **أحصل على درجات ثقة منخفضة. كيف أحسن الدقة؟**  
  عالج الصورة مسبقًا: زد التباين، أصلح الانحراف، أو حوّلها إلى تدرج رمادي. يوفر Aspose OCR أيضًا `PreprocessOptions` يمكنك تعديلها.

---

## الخلاصة

أصبح لديك الآن وصفة شاملة من الطرف إلى الطرف **للتعرف على النص في ملفات JPG** باستخدام Aspose OCR، ثم **تحويل الصورة إلى JSON** لسلاسل البيانات و**تحويل الصورة إلى EPUB** لإنشاء كتب إلكترونية قابلة للبحث. النهج خفيف الوزن، يتطلب حزمتين فقط من NuGet، ويعمل على جميع بيئات .NET الحديثة.

من هنا يمكنك:

- دمج مخرجات JSON في فهرس بحث (Azure Cognitive Search، Elastic).
- معالجة مجموعة من الصور دفعيًا وإنشاء مكتبة من كتب ePub.
- توسيع سير العمل بواجهات ترجمة لإنشاء كتب متعددة اللغات تلقائيًا.

جرّبه، واختبر جودة الصور المختلفة، ودع محرك OCR يقوم بالعمل الشاق. برمجة سعيدة!

---

![لقطة شاشة لإخراج التعرف على النص في JPG](placeholder-image.png "مثال على التعرف على النص في JPG")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}