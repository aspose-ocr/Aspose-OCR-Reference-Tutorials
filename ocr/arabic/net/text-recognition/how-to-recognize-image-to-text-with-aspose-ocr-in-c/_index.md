---
category: general
date: 2026-11-14
description: تعلم كيفية تحويل الصورة إلى نص باستخدام Aspose OCR في C#. يغطي هذا الدليل
  خطوة بخطوة أيضًا كيفية استخراج النص من ملفات JPG وتحويل الصورة إلى نص بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize image to text
- extract text from jpg
- perform OCR on image
- convert image to text
- recognize text from image
language: ar
lastmod: 2026-11-14
og_description: تحويل الصورة إلى نص باستخدام Aspose OCR في C#. اتبع هذا الدليل الكامل
  لاستخراج النص من ملف JPG، وإجراء التعرف الضوئي على الأحرف على الصورة، وتحويل الصورة
  إلى نص.
og_image_alt: Screenshot of C# code that recognize image to text using Aspose OCR
og_title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل C#
schemas:
- author: Aspose
  dateModified: '2026-11-14'
  description: Learn how to recognize image to text using Aspose OCR in C#. This step‑by‑step
    guide also covers how to extract text from jpg and convert image to text efficiently.
  headline: How to recognize image to text with Aspose OCR in C#
  type: TechArticle
- description: Learn how to recognize image to text using Aspose OCR in C#. This step‑by‑step
    guide also covers how to extract text from jpg and convert image to text efficiently.
  name: How to recognize image to text with Aspose OCR in C#
  steps:
  - name: Large images
    text: Large files increase memory usage and processing time. Resize the image
      to a maximum of 2000 px on the longest side before calling `RecognizeImage`.
  - name: Missing language model
    text: If the required language pack cannot be downloaded (e.g., offline environment),
      the engine throws `IOException`. Wrap the call in a try‑catch block and provide
      a fallback language.
  - name: Asynchronous processing
    text: For UI applications, avoid blocking the UI thread. Wrap the recognition
      call in `Task.Run`.
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: كيفية تحويل الصورة إلى نص باستخدام Aspose OCR في C#
url: /ar/net/text-recognition/how-to-recognize-image-to-text-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف على النص من الصورة باستخدام Aspose OCR في C#

إذا كنت بحاجة إلى التعرف على النص من الصورة في تطبيق .NET، يوضح هذا الدليل الخطوات الدقيقة المطلوبة. ستتعرف على كيفية استخراج النص من ملفات jpg، وإجراء OCR على بيانات الصورة، وتحويل الصورة إلى نص بأقل قدر من الشيفرة.

يغطي الدليل كل شيء بدءًا من تثبيت حزمة Aspose.OCR عبر NuGet وحتى التعامل مع نتيجة OCR بأمان. لا توجد خدمات خارجية مطلوبة، وتعمل الشيفرة على .NET 6 أو أحدث.

## تثبيت حزمة Aspose OCR

قبل كتابة أي شيفرة، أضف مكتبة Aspose.OCR إلى مشروعك. تتضمن الحزمة جميع نماذج اللغات وتقوم بتحميل الملفات المطلوبة تلقائيًا أثناء التشغيل.

```bash
dotnet add package Aspose.OCR
```

الأمر يضيف أحدث نسخة مستقرة من **Aspose.OCR** إلى ملف `csproj` الخاص بك. تضمن هذه الخطوة إمكانية استدعاء `OcrEngine` دون الحاجة لإدارة ملفات DLL يدويًا.

## إنشاء وتكوين محرك OCR

إنشاء محرك OCR هو أول إجراء برمجي يجب اتخاذه. يدير المحرك تحميل الصورة، اختيار اللغة، والتعرف.

```csharp
using Aspose.OCR;

// Step 1: Instantiate the OCR engine (required modules are downloaded automatically)
OcrEngine ocrEngine = new OcrEngine();
```

`OcrEngine` هو الفئة الأساسية التي تقوم بالعمل الشاق. إنشاء نسخة منه يطلق عملية تهيئة خفيفة؛ تقوم المكتبة بتحميل حزم اللغات فقط عندما تختار لغة معينة.

## اختيار نموذج اللغة (استخراج النص من jpg)

اختيار نموذج اللغة الصحيح يؤثر على الدقة. للنص السيريلي، عيّن `OcrLanguage.Cyrillic`. في المرة الأولى التي تحدد فيها لغة غير مخزنة محليًا، يقوم Aspose بتحميل النموذج في الخلفية.

```csharp
// Step 2: Choose the language model – triggers download if needed
ocrEngine.Language = OcrLanguage.Cyrillic;
```

إذا كنت تتعامل مع نصوص لاتينية، استبدل `Cyrillic` بـ `English` أو قيمة أخرى من الـ enum. يتبع نفس مسار الشيفرة **perform OCR on image** بغض النظر عن اللغة.

## التعرف على النص من ملف JPG (تحويل الصورة إلى نص)

الآن يمكنك تمرير ملف صورة إلى المحرك. طريقة `RecognizeImage` تقبل مسار ملف، تدفق، أو `Bitmap`. نستخدم هنا JPEG لأنه تنسيق شائع للمستندات الممسوحة.

```csharp
// Step 3: Recognize text from the image file
OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/cyrillic-sample.jpg");
```

تُعيد الطريقة كائن `OcrResult` يحتوي على السلسلة الخام، درجات الثقة، ومعلومات تخطيطية اختيارية. هذا الاستدعاء **recognize text from image** في سطر واحد.

## عرض نتيجة OCR (استخراج النص من jpg)

بعد التعرف، قم بطباعة النص المكتشف إلى وحدة التحكم أو مرره إلى مكوّن آخر.

```csharp
// Step 4: Display the recognized text
Console.WriteLine(ocrResult.Text);
```

مثال على مخرجات وحدة التحكم النموذجية:

```
Пример текста на кириллице
```

إذا كانت الصورة لا تحتوي على أحرف قابلة للقراءة، سيكون `ocrResult.Text` سلسلة فارغة. تحقق دائمًا من هذا الشرط قبل أي معالجة إضافية.

## معالجة الحالات الشائعة

### الصور الكبيرة

الملفات الكبيرة تزيد من استهلاك الذاكرة ووقت المعالجة. قم بتغيير حجم الصورة إلى حد أقصى 2000 px على الجانب الأطول قبل استدعاء `RecognizeImage`.

```csharp
using System.Drawing;

// Load, resize, then recognize
using (Bitmap original = new Bitmap("YOUR_DIRECTORY/large-sample.jpg"))
{
    int maxDim = 2000;
    int width = original.Width;
    int height = original.Height;

    if (width > maxDim || height > maxDim)
    {
        float scale = Math.Min((float)maxDim / width, (float)maxDim / height);
        int newWidth = (int)(width * scale);
        int newHeight = (int)(height * scale);
        using (Bitmap resized = new Bitmap(original, newWidth, newHeight))
        {
            OcrResult result = ocrEngine.RecognizeImage(resized);
            Console.WriteLine(result.Text);
        }
    }
    else
    {
        OcrResult result = ocrEngine.RecognizeImage(original);
        Console.WriteLine(result.Text);
    }
}
```

### عدم وجود نموذج اللغة

إذا تعذر تحميل حزمة اللغة المطلوبة (مثلاً في بيئة غير متصلة)، يرمي المحرك استثناء `IOException`. اح.wrap الاستدعاء داخل كتلة try‑catch وقدم لغة بديلة.

```csharp
try
{
    ocrEngine.Language = OcrLanguage.Cyrillic;
    OcrResult result = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(result.Text);
}
catch (IOException ex)
{
    Console.WriteLine($"Language model download failed: {ex.Message}");
    // Fallback to English
    ocrEngine.Language = OcrLanguage.English;
    OcrResult fallback = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(fallback.Text);
}
```

### المعالجة غير المتزامنة

في تطبيقات الواجهة الرسومية، تجنّب حجز خيط UI. غلف استدعاء التعرف داخل `Task.Run`.

```csharp
await Task.Run(() =>
{
    OcrResult asyncResult = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(asyncResult.Text);
});
```

## نصائح عملية للحصول على OCR موثوق

- **معالجة مسبقة للصور**: طبّق تحويل إلى تدرج الرمادي وتعزيز التباين لتحسين الدقة عندما **perform OCR on image** في إضاءة ضعيفة.
- **اختيار اللغة المناسبة**: عيّن دائمًا `ocrEngine.Language` قبل عملية التعرف. اللغة الافتراضية هي الإنجليزية، مما يؤدي إلى دقة منخفضة للنصوص السيريالية أو الآسيوية.
- **التحقق من المخرجات**: استخدم تعبيرات عادية للتأكد من أن النص المعترف به يطابق الأنماط المتوقعة (مثل التواريخ، المعرفات) قبل تخزينه.
- **تخزين حزم اللغة مؤقتًا**: قد يستغرق التحميل الأول عدة ثوانٍ. انشر الحزم المطلوبة مع تطبيقك إذا كنت بحاجة إلى بدء فوري.

## مثال كامل

فيما يلي برنامج مستقل يوضح سير العمل بالكامل—من تثبيت الحزمة إلى عرض نتيجة OCR.

```csharp
// -----------------------------------------------------------
// Recognize image to text with Aspose OCR – complete example
// -----------------------------------------------------------
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1. Create the OCR engine (modules are downloaded automatically)
        OcrEngine ocrEngine = new OcrEngine();

        // 2. Select the language model – triggers download if missing
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 3. Recognize text from a JPG file (convert image to text)
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/cyrillic-sample.jpg");

        // 4. Output the recognized string (extract text from jpg)
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**مخرجات وحدة التحكم المتوقعة**

```
Recognized text:
Пример текста на кириллице
```

تشغيل البرنامج على صورة مختلفة (مثل فاتورة إنجليزية) يتطلب فقط تغيير قيمة الـ enum `Language` ومسار الملف. نفس الشيفرة **recognize text from image** دون تعديل.

## الخلاصة

أنت الآن تعرف كيف تتعرف على النص من الصورة باستخدام Aspose OCR في C#. غطى الدليل تثبيت المكتبة، إنشاء وتكوين محرك OCR، تحويل الصورة إلى نص، ومعالجة الحالات الشائعة. مع هذه الأساسيات يمكنك **extract text from jpg**, **perform OCR on image** لأي حجم صورة، ودمج النتيجة في تدفقات عمل .NET أكبر.

الخطوات التالية لاستكشاف ميزات متقدمة مثل:

- **OCR لملفات PDF متعددة الصفحات** (استخدم `PdfInput` بدلاً من JPG)
- **قائمة حروف مخصصة** لتحسين الدقة للأكواد الرقمية
- **حفظ نتائج OCR كملفات PDF قابلة للبحث** باستخدام `OcrEngine.Save`.

جرّب نماذج لغات مختلفة وتقنيات معالجة الصور لتحقيق أعلى معدل تعرف يناسب مجالك. Happy coding!

## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [recognize text from image in C# – step‑by‑step Aspose OCR guide](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-step-by-step-aspose-ocr-guide/)
- [recognize text from image with Aspose OCR – Complete C# Async Guide](/ocr/english/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-async-g/)
- [recognize text from image in C# – Complete Aspose OCR Tutorial](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}