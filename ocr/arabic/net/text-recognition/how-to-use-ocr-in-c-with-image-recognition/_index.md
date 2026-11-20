---
category: general
date: 2026-11-20
description: كيفية استخدام OCR في C# للتعرف على النص من صورة. تعلّم كيفية تحميل صورة
  OCR، تعيين لغة OCR، واستخراج النص من ملفات JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text image
- load image OCR
- recognize text JPEG
- set OCR language
language: ar
lastmod: 2026-11-20
og_description: كيفية استخدام OCR في C# لاستخراج النص من الصور. يوضح هذا الدليل تحميل
  صورة، ضبط لغة OCR، والتعرف على النص من ملفات JPEG.
og_image_alt: Screenshot of C# code demonstrating how to use OCR to recognize text
  from an image
og_title: كيفية استخدام OCR في C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to use OCR in C# to recognize text from an image. Learn to load
    image OCR, set OCR language, and extract text from JPEG files.
  headline: How to use OCR in C# with image recognition
  type: TechArticle
tags:
- OCR
- C#
- Image processing
- Text extraction
title: كيفية استخدام OCR في C# مع التعرف على الصور
url: /ar/net/text-recognition/how-to-use-ocr-in-c-with-image-recognition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# مع التعرف على الصور

إذا كنت بحاجة إلى **كيفية استخدام OCR** في تطبيق C#، فإن هذا الدليل يشرح لك العملية بالكامل. سواءً كنت تقوم برقمنة العقود الممسوحة ضوئياً أو استخراج المعلومات من الصور، ستتعلم كيفية **التعرف على نص الصورة** بسرعة وموثوقية.

يغطي الدرس تحميل الصورة، تكوين محرك OCR، واسترجاع النص المعترف به من ملفات JPEG. في النهاية ستحصل على مثال مكتمل يمكن تشغيله وإدراجه في أي مشروع .NET.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 (أو أحدث) مثبت.
* وصول إلى مكتبة OCR توفر `OcrEngine`، `ImageStream`، ووحدات اللغة (مثلاً **Leadtools**، **Aspose.OCR**، أو أي حزمة متوافقة).
* صورة نموذجية باسم `sample.jpg` في مسار معروف.

لا توجد خدمات خارجية إضافية مطلوبة—محرك OCR سيقوم بتحميل حزم اللغة المفقودة تلقائيًا.

## الخطوة 1: تحميل الصورة لـ OCR

تحميل الصورة هو الخطوة الأولى في أي سير عمل OCR. الشيفرة أدناه تنشئ `ImageStream` من ملف JPEG موجود على القرص.

```csharp
// Step 1: Load the image to be recognized
var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
var image = ImageStream.FromFile(imagePath);
```

*لماذا هذا مهم:* كائن `ImageStream` يج abstracts التعامل مع الملفات ويوفر بيانات البكسل التي يستهلكها محرك OCR. إذا لم يُعثر على الملف، فإن `FromFile` يرمي استثناء واضح، مما يجعل عملية التصحيح سهلة.

## الخطوة 2: إنشاء مثيل محرك OCR (مع التخلص التلقائي)

استخدام كتلة `using` يضمن تحرير الموارد غير المدارة فور انتهاء عمل OCR.

```csharp
// Step 2: Create an OCR engine instance (automatically disposes when done)
using var ocrEngine = new OcrEngine();
```

*نصيحة محترف:* يفضل استخدام جملة `using` على استدعاءات `Dispose()` اليدوية لأنها تُزيل خطر نسيان تحرير الذاكرة الأصلية، مما قد يسبب تسربات ذاكرة في الخدمات طويلة التشغيل.

## الخطوة 3: تعيين لغة OCR (اختياري لكن موصى به)

إذا كنت تعرف لغة المستند الأصلي، فإن تعيينها يحسن الدقة ويسرّع المعالجة. المثال يحدد اللغة إلى السيريالية؛ يمكنك استبدالها بأي قيمة enum للغة مدعومة.

```csharp
// Step 3 (optional): Specify the language module, e.g., Cyrillic
// The required language pack will be downloaded automatically if missing
ocrEngine.Language = OcrLanguage.Cyrillic;
```

*لماذا نحدد اللغة؟* تحتوي محركات OCR على نماذج أحرف مخصصة لكل لغة. باختيار النموذج الصحيح، تقلل الإيجابيات الزائفة وتتفادى استبدالات الأحرف غير الضرورية.

## الخطوة 4: تنفيذ OCR على الصورة المحملة

الآن يقوم المحرك بمعالجة الـ bitmap ويعيد النص المعترف به كسلسلة نصية.

```csharp
// Step 4: Perform OCR on the loaded image
string recognizedText = ocrEngine.Recognize(image);
```

*حالة حافة:* إذا كانت الصورة منخفضة الدقة أو مضغوطة بشدة، قد يُعيد المحرك نتائج جزئية. فكر في ما قبل المعالجة (مثل التثنيم) للحصول على نتائج أفضل.

## الخطوة 5: إخراج النص المعترف به

أخيرًا، اعرض النص المستخرج في وحدة التحكم أو مرره إلى مكوّن آخر.

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

**الناتج المتوقع**

```
=== Recognized Text ===
Пример текста, полученного из изображения.
```

المحتوى الدقيق يعتمد على الصورة المصدر، لكن وحدة التحكم ستظهر السلسلة الكاملة التي اكتشفها محرك OCR.

## مثال كامل قابل للتنفيذ

جمع جميع الخطوات معًا ينتج برنامجًا مختصرًا يمكنك تجميعه وتشغيله فورًا.

```csharp
using System;
using System.IO;

// Ensure you reference the OCR library that provides these types
// e.g., using Leadtools.OCR;

class Program
{
    static void Main()
    {
        // Load the image to be recognized
        var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
        var image = ImageStream.FromFile(imagePath);

        // Create an OCR engine instance (auto‑dispose)
        using var ocrEngine = new OcrEngine();

        // Optional: set the language (Cyrillic in this case)
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // Perform OCR
        string recognizedText = ocrEngine.Recognize(image);

        // Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

انسخ الشيفرة إلى مشروع وحدة تحكم جديد، استبدل `YOUR_DIRECTORY` بالمسار إلى صورتك، ثم نفّذ `dotnet run`. سيطبع البرنامج النص المعترف به إلى وحدة التحكم.

## أسئلة شائعة واستكشاف الأخطاء

| السؤال | الجواب |
|----------|--------|
| **ماذا يحدث إذا لم يتم تحميل حزمة اللغة؟** | ستحاول مكتبة OCR جلبها تلقائيًا. تأكد من أن الجهاز متصل بالإنترنت، أو قم بتثبيت حزمة اللغة مسبقًا وفقًا لتوثيق المكتبة. |
| **هل يمكنني التعرف على نص من ملفات PNG أو BMP؟** | نعم. `ImageStream.FromFile` يعمل مع أي صيغة تدعمها مكتبة الصور الأساسية. فقط غيّر امتداد الملف. |
| **كيف أحسن الدقة للماسحات الضوضائية؟** | عالج الصورة مسبقًا (ضبط التباين، إزالة الضوضاء) قبل تمريرها إلى `Recognize`. العديد من المكتبات توفر فئات `ImageProcessor` لهذا الغرض. |
| **هل من الآمن تشغيل OCR على ملفات يرفعها المستخدمون؟** | تحقق من حجم الملف ونوعه، وشغّل OCR في بيئة معزولة لتجنب تحميل شيفرات خبيثة. |

## الخلاصة

أنت الآن تعرف **كيفية استخدام OCR** في C# لت **التعرف على نص الصورة**، **تحميل صورة OCR**، **تعيين لغة OCR**، و **التعرف على نص JPEG** بشكل موثوق. المثال الكامل يوضح سير عمل نظيف يمكن التخلص منه، ويمكنك توسيعه بإضافة معالجة مسبقة، دعم متعدد اللغات، أو دمجه في خطوط معالجة مستندات أكبر.

### الخطوات التالية

* استكشف المعالجة الدفعية عبر التكرار على مجلد من ملفات JPEG.  
* اجمع OCR مع معالجة اللغة الطبيعية (NLP) لاستخراج بيانات منظمة.  
* جرّب وحدات لغة أخرى مثل `OcrLanguage.English` أو `OcrLanguage.Arabic`.  

لا تتردد في تعديل الشيفرة لتناسب حالتك الخاصة، ونتمنى لك برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Use Windows.Media.Ocr to recognize text image in C# – Full OCR Guide](/ocr/english/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/)
- [How to Use OCR in C# – Extract Text from Image Asynchronously](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/)
- [How to Use OCR in C# – Extract Text from Image with Aspose OCR](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}