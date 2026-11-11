---
category: general
date: 2026-10-08
description: تعلم كيفية تنفيذ تقنية التعرف الضوئي على الحروف (OCR) في C# باستخدام
  Aspose.OCR لاستخراج النص من ملفات الصور. يوضح لك هذا الدليل كيفية تحويل الصورة إلى
  نص والتعرف على النص من ملفات JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- recognize text from jpeg
- c# ocr example
language: ar
lastmod: 2026-10-08
og_description: كيفية تنفيذ تقنية التعرف الضوئي على الأحرف (OCR) في C# باستخدام Aspose.OCR.
  اتبع هذا الدليل خطوة بخطوة لاستخراج النص من ملفات الصور، تحويل الصورة إلى نص، والتعرف
  على النص من ملفات JPEG.
og_image_alt: Console output displaying Cyrillic text recognized from a JPEG image
  by a C# OCR program
og_title: كيفية تنفيذ OCR في C# – استخراج النص من الصور
schemas:
- author: Aspose
  dateModified: '2026-10-08'
  description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  headline: How to perform OCR in C# – extract text from images
  type: TechArticle
- description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  name: How to perform OCR in C# – extract text from images
  steps:
  - name: Why each line matters
    text: '* **`OcrEngine ocrEngine = new OcrEngine();`** – Instantiates the engine
      that orchestrates the whole OCR pipeline. * **`ocrEngine.Language = Language.Cyrillic;`**
      – Selects the language model. Choosing the correct language dramatically improves
      accuracy when you **extract text from image** files tha'
  - name: 4.1 Recognizing English or multilingual text
    text: 'Replace the language assignment with the appropriate enum:'
  - name: 4.2 Processing images from a stream instead of a file
    text: 'If your image arrives via an HTTP response or a database blob, use a `MemoryStream`:'
  - name: 4.3 Handling large or low‑resolution images
    text: 'Large images increase memory consumption. You can downscale before OCR:'
  - name: 4.4 Error handling
    text: 'Wrap the recognition call in a try‑catch block to catch network or file‑access
      errors:'
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
- Image Processing
title: كيفية تنفيذ OCR في C# – استخراج النص من الصور
url: /ar/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في C# – استخراج النص من الصور

إذا كنت بحاجة إلى **كيفية تنفيذ OCR** في تطبيق .NET، فإن هذا الدليل يقدم لك حلاً كاملاً وجاهزًا للتنفيذ. باستخدام Aspose.OCR يمكنك **استخراج النص من صورة**، **تحويل الصورة إلى نص**، و**التعرف على النص من JPEG** ببضع أسطر من الشيفرة.

سترى سير العمل بالكامل — من تثبيت المكتبة إلى طباعة السلسلة التي تم التعرف عليها — بحيث يمكنك نسخ المثال إلى مشروعك والبدء في معالجة الصور فورًا.

## ما ستتعلمه

* كيفية إعداد مشروع C# لمهام OCR.  
* كيفية تحميل ملف JPEG (أو أي صورة مدعومة) وتشغيل عملية التعرف.  
* كيفية استرجاع النص الناتج واستخدامه في تطبيقك.  

المتطلب الوحيد هو وجود .NET SDK حديث (≥ .NET 6) واتصال بالإنترنت لتحميل نموذج اللغة الأول.

## الخطوة 1: إعداد المشروع وتثبيت Aspose.OCR

1. أنشئ مشروع وحدة تحكم جديد:

   ```bash
   dotnet new console -n OcrDemo
   cd OcrDemo
   ```

2. أضف حزمة NuGet الخاصة بـ Aspose.OCR:

   ```bash
   dotnet add package Aspose.OCR
   ```

   تحتوي الحزمة على محرك OCR، نماذج اللغات، وأدوات معالجة الصور اللازمة لـ **تحويل الصورة إلى نص**.

> **نصيحة احترافية:** إذا كنت تخطط لتشغيل OCR على عدة صور، فكر في إضافة الحزمة إلى مكتبة مشتركة حتى تتمكن من إعادة استخدام نفس نسخة المحرك.

## الخطوة 2: كتابة مثال OCR بلغة C#

أنشئ أو استبدل ملف `Program.cs` بالكود التالي. يوضح مثال **c# ocr example** يعمل مع أي صيغة صورة يدعمها Aspose.OCR (JPEG، PNG، BMP، إلخ).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // ---------------------------------------------------------
        // Step 2.1: Create an OCR engine instance
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // Step 2.2: Choose the language model.
        // The example uses Cyrillic; replace with Language.English,
        // Language.French, etc., to match your source image.
        // ---------------------------------------------------------
        ocrEngine.Language = Language.Cyrillic; // <-- change as needed

        // ---------------------------------------------------------
        // Step 2.3: Load the image you want to process.
        // ImageStream.FromFile automatically reads JPEG, PNG, BMP…
        // ---------------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile("sample_cyrillic.jpg");

        // ---------------------------------------------------------
        // Step 2.4: Run the recognition process.
        // This call downloads the required language model the first
        // time it is used, then performs the OCR.
        // ---------------------------------------------------------
        ocrEngine.Recognize();

        // ---------------------------------------------------------
        // Step 2.5: Retrieve the recognized text.
        // The Text property holds the result of the OCR engine.
        // ---------------------------------------------------------
        string recognizedText = ocrEngine.Text;

        // ---------------------------------------------------------
        // Step 2.6: Display the output.
        // This is where you can further process the string,
        // e.g., save to a database, feed to a search index, etc.
        // ---------------------------------------------------------
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### لماذا كل سطر مهم

* **`OcrEngine ocrEngine = new OcrEngine();`** – ينشئ المحرك الذي يدير كامل خط أنابيب OCR.  
* **`ocrEngine.Language = Language.Cyrillic;`** – يحدد نموذج اللغة. اختيار اللغة الصحيحة يحسن الدقة بشكل كبير عند **استخراج النص من صورة** التي تحتوي على أحرف غير لاتينية.  
* **`ocrEngine.Image = ImageStream.FromFile(...);`** – يحمل ملف JPEG المصدر (أو أي صورة مدعومة أخرى). هذه الخطوة أساسية لـ **التعرف على النص من jpeg**.  
* **`ocrEngine.Recognize();`** – ينفذ خوارزمية OCR الأساسية. الطريقة تحجب التنفيذ حتى ينتهي المحرك من المعالجة.  
* **`ocrEngine.Text;`** – تُعيد النتيجة كنص عادي، والذي يمكنك الآن **تحويل الصورة إلى نص** لاستخدامه في منطق التطبيق اللاحق.

## الخطوة 3: تشغيل البرنامج والتحقق من النتيجة

قم بالترجمة والتنفيذ:

```bash
dotnet run
```

إذا كانت الصورة `sample_cyrillic.jpg` تحتوي على العبارة السلافية “Привет мир”، فستظهر في وحدة التحكم:

```
=== Recognized Text ===
Привет мир
```

تثبت هذه النتيجة أنك نجحت في تعلم **كيفية تنفيذ OCR** و**استخراج النص من صورة** باستخدام C#.

## الخطوة 4: التغييرات الشائعة والحالات الخاصة

### 4.1 التعرف على النص الإنجليزي أو متعدد اللغات

استبدل تعيين اللغة بالعدد المناسب:

```csharp
ocrEngine.Language = Language.English;           // English only
ocrEngine.Language = Language.Multilingual;      // Detects many languages automatically
```

### 4.2 معالجة الصور من تدفق بدلاً من ملف

إذا كانت الصورة تصل عبر استجابة HTTP أو كـ BLOB في قاعدة بيانات، استخدم `MemoryStream`:

```csharp
using (var ms = new MemoryStream(imageBytes))
{
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
}
```

### 4.3 التعامل مع الصور الكبيرة أو منخفضة الدقة

الصور الكبيرة تستهلك ذاكرة أكبر. يمكنك تقليل الحجم قبل تشغيل OCR:

```csharp
ocrEngine.Config.ImagePreprocessOptions.ScaleFactor = 0.5; // Reduce size by 50%
```

### 4.4 معالجة الأخطاء

غلف استدعاء التعرف داخل كتلة try‑catch لالتقاط أخطاء الشبكة أو الوصول إلى الملفات:

```csharp
try
{
    ocrEngine.Recognize();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

## الخطوة 5: الخطوات التالية – توسيع سير عمل OCR الخاص بك

* **المعالجة الدفعية:** كرر عبر الملفات في دليل لتطبيق **تحويل الصورة إلى نص** على كل JPEG.  
* **ما بعد المعالجة:** استخدم تعبيرات نمطية لتنظيف السلسلة التي تم التعرف عليها، مفيد عندما تحتاج إلى **استخراج النص من صورة** للنماذج أو الفواتير.  
* **التكامل مع Azure Cognitive Services:** قارن نتائج Aspose.OCR مع OCR السحابي للحصول على دقة أعلى في التخطيطات المعقدة.  
* **تخزين النتائج:** أدخل النص المستخرج في قاعدة بيانات SQL أو فهرس ElasticSearch لتوفير مستندات قابلة للبحث.

---

## الخلاصة

أنت الآن تعرف **كيفية تنفيذ OCR** في C# باستخدام Aspose.OCR، من تثبيت الحزمة إلى عرض السلسلة التي تم التعرف عليها. يتيح لك هذا **c# ocr example** الكامل **استخراج النص من صورة**، **تحويل الصورة إلى نص**، و**التعرف على النص من JPEG** ببضع أسطر من الشيفرة فقط. جرّب نماذج لغات مختلفة، مصادر صور متنوعة، وتقنيات ما بعد المعالجة لتناسب حالتك الخاصة.

---


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Use OCR in C# – Extract Text from Image Files](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-files/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Perform OCR in C# – Extract Text and Write JSON](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}