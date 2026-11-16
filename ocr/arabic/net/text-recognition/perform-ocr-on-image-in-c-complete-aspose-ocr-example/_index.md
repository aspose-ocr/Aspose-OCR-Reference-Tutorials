---
category: general
date: 2026-06-25
description: تنفيذ التعرف الضوئي على الحروف (OCR) على صورة باستخدام C# و Aspose OCR،
  ثم كتابة ملف JSON وحفظه باستخدام C# مع مثال واضح خطوة بخطوة.
draft: false
keywords:
- perform ocr on image
- c# write json file
- save json file c#
- aspose ocr example
- load image for ocr
language: ar
og_description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على صورة باستخدام C# و Aspose
  OCR، ثم احفظ النتيجة كملف JSON. دليل كامل وقابل للتنفيذ للمطورين.
og_title: إجراء OCR على صورة في C# – مثال كامل على Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on image using C# and Aspose OCR, then c# write json file
    and save json file c# with a clear, step‑by‑step example.
  headline: Perform OCR on Image in C# – Complete Aspose OCR Example
  type: TechArticle
- questions:
  - answer: It builds a platform‑independent path, preventing “file not found” errors
      on Windows vs. Linux.
    question: Why use `Path.Combine`?
  - answer: The engine scans the bitmap, applies language‑specific classifiers, and
      builds a hierarchical result object containing pages, blocks, lines, and words.
    question: What happens under the hood?
  - answer: Human‑readable output makes debugging easier, especially when you later
      feed the JSON into other services.
    question: Why pretty‑print?
  - answer: Wrap the write in a try/catch and surface a clear message—this helps in
      Docker containers where the working directory may be mounted read‑only.
    question: What if the folder is read‑only?
  type: FAQPage
tags:
- C#
- Aspose OCR
- JSON
- Image Processing
title: تنفيذ التعرف الضوئي على الأحرف (OCR) على صورة في C# – مثال كامل لاستخدام Aspose
  OCR
url: /ar/net/text-recognition/perform-ocr-on-image-in-c-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنفيذ OCR على صورة في C# – مثال كامل باستخدام Aspose OCR

هل احتجت يوماً إلى **تنفيذ OCR على ملفات الصور** من تطبيق C# console ولم تعرف كيف تستخرج النص وتخزنه بطريقة منظمة؟ لست وحدك. في العديد من خطوط الأتمتة—مثل رقمنة الفواتير أو أرشفة المستندات متعددة اللغات—القدرة على تحويل صورة إلى نص قابل للبحث ثم **c# write json file** تُعد دفعة إنتاجية حقيقية.

في هذا الدرس سنستعرض مثالًا **aspose ocr example** من البداية إلى النهاية يقوم بتحميل صورة، استخراج الأحرف، تنسيق النتيجة كـ JSON منسق، وأخيرًا **save json file c#** إلى القرص. بنهاية الشرح ستحصل على برنامج مستقل يمكنك إدراجه في أي مشروع .NET.

![مثال تنفيذ OCR على صورة](perform-ocr-on-image.png "لقطة شاشة تُظهر نتيجة OCR – تنفيذ OCR على صورة")

## ما ستحققه

- **تحميل صورة للـ OCR** باستخدام `OcrImage.FromFile` من Aspose.OCR.
- **تنفيذ OCR على الصورة** باستدعاء طريقة واحدة.
- تحويل نتيجة التعرف إلى سلسلة JSON منسقة بشكل جميل.
- **حفظ ملف JSON C#** باستخدام `File.WriteAllText`.
- فهم المشكلات الشائعة (حزمة NuGet مفقودة، صيغ صور غير مدعومة، معالجة Unicode).

بدون خدمات خارجية، بدون مفاتيح سحابة—فقط كود C# يعمل محليًا.

---

## الخطوة 1: إعداد المشروع وإضافة Aspose.OCR

قبل أن نتمكن من **تنفيذ OCR على صورة**، نحتاج إلى المكتبات المناسبة.

1. افتح Visual Studio (أو بيئتك المفضلة) وأنشئ تطبيق **Console App (.NET 6 أو أحدث)**.  
2. افتح مدير حزم NuGet وقم بتثبيت `Aspose.OCR`:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستهدف .NET Framework، فإن الحزمة نفسها تعمل، لكن تأكد من وجود .NET 4.6.2 على الأقل.

> **لماذا هذا مهم:** Aspose.OCR يتضمن حزم لغات ومحرك عالي الأداء، لذا لا تحتاج إلى شحن ملفات OCR منفصلة.

---

## الخطوة 2: تحميل الصورة للـ OCR

المحرك يحتاج إلى كائن `OcrImage`. هنا يأتي دور **load image for OCR**.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Create the OCR engine
        var ocrEngine = new OcrEngine();

        // 👉 Load the image you want to recognize
        var imagePath = Path.Combine(Environment.CurrentDirectory, "multi_lang.png");
        var image = OcrImage.FromFile(imagePath);

        // Continue with recognition...
```

- **لماذا نستخدم `Path.Combine`؟** لأنه يبني مسارًا مستقلاً عن النظام، مما يمنع أخطاء “الملف غير موجود” على Windows مقابل Linux.
- **الصيغ المدعومة:** PNG، JPEG، BMP، TIFF. إذا قمت بتمرير PDF، سيُطلق Aspose.OCR استثناء `NotSupportedException`.

---

## الخطوة 3: تنفيذ OCR على الصورة

الآن العملية الأساسية. سطر واحد يقوم بالعمل الشاق.

```csharp
        // Perform OCR recognition on the image
        var ocrResult = ocrEngine.Recognize(image);
```

- **ماذا يحدث خلف الكواليس؟** يقوم المحرك بمسح البت ماب، تطبيق مصنفات خاصة باللغات، وإنشاء كائن نتيجة هرمي يحتوي على الصفحات، الكتل، الأسطر، والكلمات.
- **حالة حافة:** إذا كانت الصورة فارغة أو صاخبة جدًا، قد يحتوي `ocrResult` على حقل `Text` فارغ. يمكنك فحص `ocrResult.IsEmpty` لتجنب ذلك.

---

## الخطوة 4: تحويل النتيجة إلى JSON (c# write json file)

كائن `OcrResult` في Aspose.OCR يعرف كيف يسلسل نفسه. سنطلب منه سلسلة JSON *منسقة*.

```csharp
        // Convert the recognition result to a nicely formatted JSON string
        string jsonResult = ocrResult.ToJson(prettyPrint: true);
```

- **لماذا التنسيق المنسق؟** لأن الإخراج القابل للقراءة البشرية يسهل عملية التصحيح، خاصةً عندما تستخدم JSON لاحقًا في خدمات أخرى.
- **بديل:** إذا كنت تحتاج حمولة مضغوطة للنقل عبر الشبكة، عيّن `prettyPrint: false`.

---

## الخطوة 5: حفظ ملف JSON C# – تخزين النتيجة

أخيرًا، نكتب الـ JSON إلى القرص. هذه هي خطوة **save json file c#** في الدرس.

```csharp
        // Define where the JSON will be saved
        var jsonPath = Path.Combine(Environment.CurrentDirectory, "result.json");

        // Write the JSON string to the file system
        File.WriteAllText(jsonPath, jsonResult);

        // Inform the user
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

- **ملاحظة الترميز:** `WriteAllText` يستخدم UTF‑8 افتراضيًا، مما يحافظ على أي أحرف Unicode مستخرجة من صور متعددة اللغات.
- **ماذا لو كان المجلد للقراءة فقط؟** ضع عملية الكتابة داخل `try/catch` واطلق رسالة واضحة—هذا يساعد في حاويات Docker حيث قد يكون دليل العمل مركبًا للقراءة فقط.

---

## مثال كامل يعمل

بتجميع كل ما سبق، إليك البرنامج الكامل الذي يمكنك نسخه‑ولصقه في `Program.cs` وتشغيله فورًا (مع افتراض وجود `multi_lang.png` بجوار الملف التنفيذي).

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Step 1: Create OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        var imagePath = Path.Combine(Environment.CurrentDirectory, "multi_lang.png");
        var image = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR on image
        var ocrResult = ocrEngine.Recognize(image);

        // Optional: guard against empty results
        if (ocrResult == null || ocrResult.IsEmpty)
        {
            Console.WriteLine("No text recognized. Check the image quality.");
            return;
        }

        // Step 4: Convert result to pretty‑printed JSON
        string jsonResult = ocrResult.ToJson(prettyPrint: true);

        // Step 5: Save JSON file C#
        var jsonPath = Path.Combine(Environment.CurrentDirectory, "result.json");
        File.WriteAllText(jsonPath, jsonResult);

        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
JSON saved to C:\Projects\OcrDemo\result.json
```

فتح `result.json` يكشف عن مستند منظم:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Lines": [
            {
              "Words": [
                { "Text": "Hello", "Confidence": 0.98 },
                { "Text": "World", "Confidence": 0.97 }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

المحتوى الفعلي يختلف بناءً على الصورة المصدر، لكن مخطط JSON يبقى ثابتًا—مثالي للمعالجة اللاحقة (مثل إرساله إلى ElasticSearch أو مخزن NoSQL).

---

## أسئلة شائعة ومشكلات محتملة

| السؤال | الجواب |
|----------|--------|
| **هل أحتاج إلى ترخيص؟** | يعمل Aspose.OCR في وضع التقييم حتى 20 صفحة. للإنتاج ستحتاج إلى ملف ترخيص (`Aspose.OCR.lic`). |
| **ما اللغات المدعومة؟** | الإنجليزية، الفرنسية، الألمانية، الإسبانية، الصينية، اليابانية، العربية، والعديد غيرها. اضبط `ocrEngine.Language = Language.English;` لتحديد لغة أو `ocrEngine.Language = Language.All;` للكشف التلقائي. |
| **هل يمكنني معالجة ملفات PDF مباشرة؟** | ليس مع Aspose.OCR وحده. استخدم Aspose.PDF لتحويل الصفحات إلى صور أولاً. |
| **لماذا JSON فارغ؟** | عادةً بسبب صورة منخفضة التباين. جرّب زيادة التباين أو استخدم `ocrEngine.Config.PreprocessOptions` لتحسين البت ماب. |
| **هل مخطط JSON ثابت؟** | نعم، تضمن Aspose التوافق العكسي لإخراج `ToJson` عبر الإصدارات الثانوية. |

---

## توسيع المثال

الآن بعد أن عرفت كيف **تنفيذ OCR على صورة** و **حفظ ملف JSON c#**، قد ترغب في:

- **معالجة دفعات** من الصور في مجلد (`Directory.GetFiles(..., "*.png")`).
- **رفع الـ JSON** إلى API REST باستخدام `HttpClient`.
- **إدخال النص** في قاعدة بيانات لأرشفة قابلة للبحث.
- **إضافة معالجة مسبقة للصور** (تصحيح الميل، ثنائيات) عبر `ocrEngine.Config.PreprocessOptions`.

جميع هذه الخطوات تتبع النمط نفسه: تحميل → التعرف → التسلسل → التخزين.

---

## الخلاصة

لقد أنجزنا مثالًا مختصرًا **aspose ocr example** يوضح كيفية **تنفيذ OCR على صورة**، تحويل النتيجة إلى **JSON منسق**، و**حفظ ملف JSON C#** ببضع أسطر فقط. النهج بسيط، لا يتطلب خدمات خارجية، ويمكن توسيعه ليتناسب مع أي سير عمل إنتاجي.

جرّبه، عدّل إعدادات اللغة، وشاهد تحسين دقة OCR. إذا واجهت أي صعوبات، راجع وثائق Aspose.OCR أو اترك تعليقًا أدناه—برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف طرق تنفيذ بديلة في مشاريعك.

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}