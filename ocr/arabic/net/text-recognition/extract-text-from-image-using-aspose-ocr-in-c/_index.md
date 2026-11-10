---
category: general
date: 2026-08-09
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف، ضبط لغة OCR، معالجة الصورة باستخدام OCR، وتحويل الصورة
  إلى نص بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: ar
lastmod: 2026-08-09
og_description: استخراج النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدرس كيفية
  تحميل الصورة للتعرف الضوئي على الأحرف، تعيين لغة OCR، معالجة الصورة باستخدام OCR،
  وتحويل الصورة إلى نص في بضع أسطر من الشيفرة.
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل C#
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: استخراج النص من الصورة باستخدام Aspose OCR في C#
url: /ar/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام Aspose OCR في C#

إذا كنت بحاجة إلى **استخراج النص من الصورة** في تطبيق .NET، فإن هذا الدليل يشرح لك حلاً كاملاً وجاهزًا للتنفيذ. سترى كيف **تحمّل صورة للتعرف الضوئي على الأحرف (OCR)**، وتختار وحدة اللغة المناسبة، وتشغل محرك OCR، وأخيرًا **تحوّل الصورة إلى نص** ببضع أسطر من C#.

يغطي الدليل كل ما يلزم للحصول على نتائج موثوقة باستخدام Aspose.OCR، بما في ذلك المشكلات الشائعة مثل صيغ الصور غير المدعومة وفروق اللغات. في النهاية، ستحصل على برنامج مستقل يطبع النص المُعترف به إلى وحدة التحكم.

## ما ستحققه

* تحميل ملف صورة إلى محرك Aspose OCR.  
* **تحديد لغة OCR** (السيريلية في المثال، لكن أي لغة مدعومة تعمل).  
* **معالجة صورة OCR** والحصول على التمثيل النصي.  
* **تحويل الصورة إلى نص** وعرضه، جاهز للمعالجة أو التخزين الإضافي.  

**المتطلبات المسبقة**

* .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.6+).  
* Visual Studio 2022 (أو أي بيئة تطوير تدعم C#).  
* حزمة Aspose.OCR عبر NuGet (`Install-Package Aspose.OCR`).  

---

## استخراج النص من الصورة – شرح كامل للكود

فيما يلي البرنامج الكامل القابل للتنفيذ. انسخه في مشروع وحدة تحكم جديد واستبدل `YOUR_DIRECTORY/sample_cyrillic.jpg` بمسار صورتك الخاصة.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### لماذا كل خطوة مهمة

1. **إنشاء مثيل لمحرك OCR** – الـ `OcrEngine` يضم جميع وظائف OCR. تحريره (Dispose) بسرعة يحرّر الموارد الأصلية، وهو أمر حاسم للخدمات طويلة التشغيل.  
2. **تحديد لغة OCR** – اختيار وحدة اللغة الصحيحة يحسّن الدقة بشكل كبير. توفر Aspose أكثر من 30 حزمة لغة؛ اللغة الافتراضية هي الإنجليزية. يستخدم المثال السيريلية لتوضيح نص غير لاتيني.  
3. **تحميل صورة للتعرف الضوئي (OCR)** – يعمل المحرك مع `ImageStream`. توفير صورة عالية الدقة (≥300 dpi) يقلل من الأخطاء، خصوصًا للخطوط المعقدة.  
4. **معالجة صورة OCR** – هنا يتم تنفيذ العملية الثقيلة. تُعيد الطريقة كائن `OcrResult` يحتوي على النص المستخرج، درجات الثقة، وبيانات تخطيطية اختيارية.  
5. **تحويل الصورة إلى نص** – `result.Text` هو سلسلة `string` عادية. يمكنك كتابتها إلى ملف، أو إدخالها في فهرس بحث، أو تمريرها إلى خطوط معالجة اللغة الطبيعية اللاحقة.  

---

## تحميل صورة للتعرف الضوئي (OCR)

طريقة `ImageStream.FromFile` تدعم صيغ الرسوم النقطية الشائعة. إذا استلمت صورًا كمصفوفات بايت (مثلاً من واجهة ويب API)، استخدم `ImageStream.FromBytes(byte[])` بدلاً من ذلك:

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**نصيحة احترافية:** تأكد دائمًا من أن الصورة غير تالفة قبل تمريرها إلى المحرك. فحص سريع بـ `try { Image.FromFile(...); } catch { ... }` يمنع استثناءات وقت التشغيل.

---

## تحديد لغة OCR

تأتي Aspose.OCR مع حزم لغات يمكنك تمكينها أثناء التشغيل. لسرد جميع اللغات المتاحة:

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

إذا كنت بحاجة إلى التعرف على عدة لغات في نفس المستند، اجمعها باستخدام عامل OR الثنائي:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**حالة خاصة:** خلط اللغات من اليمين إلى اليسار (RTL) (مثل العربية) مع النصوص من اليسار إلى اليمين قد يتطلب معالجة تخطيط إضافية. تقوم Aspose بالكشف تلقائيًا عن الاتجاه، لكن يمكنك ضبطه عبر `engine.PageSegmentationMode`.

---

## معالجة صورة OCR

استدعاء `Process` متزامن ويمنع الاستمرار حتى ينتهي المحرك. للدفعات الكبيرة أو تطبيقات الواجهة، فكر في النسخة غير المتزامنة:

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**مشكلة شائعة:** نسيان تعيين `engine.Image` قبل استدعاء `Process` يسبب استثناء `InvalidOperationException`. احرص دائمًا على تعيين الصورة أولاً.

---

## تحويل الصورة إلى نص

يمكن معالجة السلسلة المستخرجة مثل أي `string` أخرى في .NET. على سبيل المثال، لكتابة النتيجة إلى ملف:

```csharp
File.WriteAllText("output.txt", result.Text);
```

إذا كنت بحاجة إلى الحفاظ على فواصل الأسطر كما هي في الصورة، استخدم `result.Text` مباشرة. للمعالجة اللاحقة (مثل إزالة الفراغات الزائدة)، استخدم طرق السلاسل القياسية:

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## ملخص المثال الكامل

بجمع كل شيء معًا، البرنامج:

1. ينشئ مثيلًا من `OcrEngine`.  
2. **يحدد لغة OCR** إلى السيريلية (أو أي لغة تختارها).  
3. **يحمل صورة للتعرف الضوئي** من القرص.  
4. **يعالج صورة OCR** للحصول على النتيجة النصية.  
5. **يحوّل الصورة إلى نص** ويطبعها.

تشغيل العينة مع صورة سيريلية واضحة ينتج مخرجات مشابهة لـ:

```
=== Recognized Text ===
Пример текста на кириллице
```

إذا كانت الصورة تحتوي على نص إنجليزي، فقط غيّر `engine.Language = OcrLanguage.English;` وسيقوم نفس الكود **باستخراج النص من الصورة** بشكل صحيح.

---

## الخلاصة

أنت الآن تعرف كيف **استخراج النص من الصورة** باستخدام Aspose OCR في C#. غطى الدليل تحميل الصورة، اختيار اللغة المناسبة، تشغيل عملية OCR، و**تحويل الصورة إلى نص** للاستخدام اللاحق.

من هنا يمكنك:

* تجربة لغات أخرى (`load image for OCR` → `set OCR language` → `process image OCR`).  
* دمج خطوة OCR في خط أنابيب أكبر (مثل استيعاب المستندات، ملفات PDF قابلة للبحث).  
* تحسين الأداء عن طريق تجميع الصور أو استخدام واجهة API غير المتزامنة.

لا تتردد في استكشاف وثائق Aspose.OCR للميزات المتقدمة مثل القواميس المخصصة، أوضاع تقسيم الصفحات، وضبط دقة OCR. برمجة سعيدة!

## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)
- [كيفية استخراج نص الصورة من تدفق باستخدام Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}