---
category: general
date: 2026-09-22
description: استخراج النص من الصورة باستخدام Aspose.OCR في C#. تعلم كيفية تحويل الصورة
  إلى نص، تحميل الصورة للتعرف الضوئي على الأحرف، والتعرف على النص السيريلي بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for OCR
- recognize text image
- recognize Cyrillic text
language: ar
lastmod: 2026-09-22
og_description: استخراج النص من الصورة باستخدام Aspose.OCR في C#. يوضح هذا الدرس كيفية
  تحويل الصورة إلى نص، وتحميل الصورة للتعرف الضوئي على الأحرف، والتعرف على النص السيريلي
  في بضع أسطر من الشيفرة فقط.
og_image_alt: Diagram showing extract text from image workflow using Aspose.OCR
og_title: استخراج النص من الصورة باستخدام Aspose.OCR – دليل خطوة بخطوة بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Extract text from image with Aspose.OCR in C#. Learn how to convert
    image to text, load image for OCR, and recognize Cyrillic text efficiently.
  headline: How to extract text from image using Aspose.OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose.OCR in C#. Learn how to convert
    image to text, load image for OCR, and recognize Cyrillic text efficiently.
  name: How to extract text from image using Aspose.OCR in C#
  steps:
  - name: Install the Aspose.OCR package
    text: 'Open a terminal in your solution folder and run:'
  - name: Create the OCR engine instance
    text: '```csharp using Aspose.OCR; using System.Drawing; // Required for Image
      handling'
  - name: Choose the language to recognize
    text: '```csharp // Step 3: Select Cyrillic as the target language engine.Language
      = OcrLanguage.Cyrillic; ```'
  - name: Load image for OCR
    text: '```csharp // Step 4: Load the image that contains the text engine.Image
      = Image.FromFile(@"YOUR_DIRECTORY\sample_cyrillic.png"); ```'
  - name: Perform the recognition and get the result
    text: '```csharp // Step 5: Run the recognition process string recognizedText
      = engine.Recognize(); ```'
  - name: Output the extracted text
    text: '```csharp // Step 6: Display the extracted text Console.WriteLine("Recognized
      text:"); Console.WriteLine(recognizedText); ```'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image processing
title: كيفية استخراج النص من الصورة باستخدام Aspose.OCR في C#
url: /ar/net/text-recognition/how-to-extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج النص من صورة باستخدام Aspose.OCR في C#

إذا كنت بحاجة إلى **استخراج النص من صورة** في تطبيق .NET، فإن هذا الدليل يوضح لك حلًا كاملًا وجاهزًا للتنفيذ. ستتعرف على كيفية **تحويل الصورة إلى نص**، تحميل الصورة للـ OCR، ومعالجة الأحرف السيريلية دون أي إعدادات إضافية.

يغطي الدليل كل ما تحتاجه: حزم NuGet المطلوبة، عينة شفرة كاملة، شرح لكل خطوة، ونصائح لتجنب المشكلات الشائعة. في النهاية يمكنك نسخ بضع أسطر إلى مشروعك والبدء في التعرف على النص فورًا.

## ما ستحتاجه

قبل أن تبدأ، تأكد من وجود ما يلي:

- .NET 6.0 SDK أو أحدث (تعمل الشفرة أيضًا مع .NET Framework 4.7+)
- Visual Studio 2022 أو أي بيئة تطوير تدعم C#
- حزمة Aspose.OCR من NuGet (`Aspose.OCR`) مثبتة في مشروعك
- صورة نموذجية تحتوي على نص سيريل (مثال: `sample_cyrillic.png`)

> **نصيحة محترف:** في المرة الأولى التي تطلب فيها لغة غير مدمجة، يقوم Aspose.OCR تلقائيًا بتحميل الوحدة المطلوبة. هذا السلوك هو ما يتيح **التعرف على النص السيريلي** بسلاسة.

## استخراج النص من صورة باستخدام Aspose.OCR

جوهر الحل هو إنشاء `OcrEngine`، ضبط اللغة، تحميل الصورة، ثم استدعاء `Recognize()`. الأقسام التالية توضح كل خطوة.

### الخطوة 1: تثبيت حزمة Aspose.OCR

افتح نافذة الأوامر في مجلد الحل الخاص بك وشغّل:

```bash
dotnet add package Aspose.OCR
```

يضيف هذا الأمر أحدث نسخة مستقرة من Aspose.OCR إلى ملف المشروع، مما يضمن توفر محرك OCR ووحدات اللغة وقت التشغيل.

### الخطوة 2: إنشاء كائن محرك OCR

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image handling

// ...

// Step 2: Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

`OcrEngine` هو نقطة الدخول لجميع عمليات OCR. إنشاءه يخصص الموارد الداخلية اللازمة لتحليل الصورة.

### الخطوة 3: اختيار اللغة للتعرف عليها

```csharp
// Step 3: Select Cyrillic as the target language
engine.Language = OcrLanguage.Cyrillic;
```

ضبط `engine.Language` يخبر Aspose.OCR مجموعة الأحرف التي يجب البحث عنها. **التعرف على النص السيريلي** يؤدي إلى تحميل تلقائي لحزمة اللغة السيريالية إذا لم تكن موجودة على الجهاز.

### الخطوة 4: تحميل الصورة للـ OCR

```csharp
// Step 4: Load the image that contains the text
engine.Image = Image.FromFile(@"YOUR_DIRECTORY\sample_cyrillic.png");
```

هذا السطر **يقوم بتحميل الصورة للـ OCR** باستخدام `System.Drawing.Image`. استبدل `YOUR_DIRECTORY` بالمسار الفعلي لملف PNG أو JPEG الخاص بك. الآن يحتفظ المحرك ببيتماب جاهز للتحليل.

### الخطوة 5: إجراء التعرف والحصول على النتيجة

```csharp
// Step 5: Run the recognition process
string recognizedText = engine.Recognize();
```

`Recognize()` يمسح البيتماب، يطبق نماذج خاصة باللغة، ويعيد السلسلة المستخرجة. إذا كانت الصورة واضحة وتم ضبط اللغة بشكل صحيح، ستعيد الطريقة نتيجة عالية الدقة.

### الخطوة 6: إخراج النص المستخرج

```csharp
// Step 6: Display the extracted text
Console.WriteLine("Recognized text:");
Console.WriteLine(recognizedText);
```

طباعة النتيجة إلى وحدة التحكم تتيح لك التحقق من أن **استخراج النص من صورة** يعمل كما هو متوقع. يمكنك أيضًا كتابة النص إلى ملف، قاعدة بيانات، أو تمريره إلى خدمة أخرى.

## مثال كامل قابل للتنفيذ

فيما يلي برنامج مستقل يتضمن جميع الخطوات السابقة. انسخ الشفرة إلى مشروع وحدة تحكم جديد (`dotnet new console`) وشغّله.

```csharp
using System;
using System.Drawing;          // Provides Image class
using Aspose.OCR;              // Aspose OCR namespace

namespace ImageToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            OcrEngine engine = new OcrEngine();

            // Select the language – Cyrillic triggers module download if needed
            engine.Language = OcrLanguage.Cyrillic;

            // Load the image file (adjust the path to your environment)
            string imagePath = @"YOUR_DIRECTORY\sample_cyrillic.png";
            engine.Image = Image.FromFile(imagePath);

            // Perform recognition
            string recognizedText = engine.Recognize();

            // Output the result
            Console.WriteLine("Recognized text:");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**الناتج المتوقع**

```
Recognized text:
Пример текста на кириллице
```

إذا كانت الصورة النموذجية تحتوي على العبارة “Пример текста на кириллице”، ستظهر في وحدة التحكم كما هو موضح. قد تؤثر اختلافات الخط أو الحجم أو الضوضاء على الدقة، لكن المعالجة المسبقة المدمجة في Aspose.OCR تتعامل مع معظم الحالات الشائعة.

## معالجة الحالات الشائعة

| السيناريو | ما الذي يجب فعله | لماذا يهم |
|----------|----------------|-----------|
| عدم العثور على الصورة | غلف `Image.FromFile` بكتلة `try / catch (FileNotFoundException)` وعرض رسالة ودية. | يمنع تعطل التطبيق ويساعد المستخدم على تحديد الملف الصحيح. |
| صورة منخفضة التباين | اضبط `engine.ImagePreprocessingOptions` إلى `ImagePreprocessingOptions.Auto` أو عدّل السطوع/التباين يدويًا قبل التعرف. | يحسن دقة OCR عندما تكون الصورة الأصلية باهتة. |
| الحاجة إلى التعرف على لغات متعددة | عيّن `engine.Language = OcrLanguage.Multilingual;` وأضف اختياريًا `engine.AdditionalLanguages.Add(OcrLanguage.English);`. | يتيح اكتشاف المستندات ذات النصوص المختلطة (مثل السيريلي مع اللاتيني). |
| دفعة كبيرة من الصور | أعد استخدام كائن `OcrEngine` واحد واستدعِ `engine.Recognize()` داخل حلقة. حرّر المحرك بعد الانتهاء. | يقلل من تخصيص الذاكرة ويسرّع المعالجة. |

## أفضل الممارسات للحصول على OCR موثوق

- **استخدم صيغ صور غير مضغوطة** (PNG أو TIFF) قدر الإمكان؛ ضغط JPEG قد يضيف تشويهات تُربك المحرك.
- **حافظ على دقة الصورة** عند 300 dpi أو أعلى للنص المطبوع؛ الدقة الأقل قد تفقد الأحرف الصغيرة.
- **قم بقص الهوامش غير الضرورية** قبل تحميل الصورة؛ المساحات الفارغة تزيد من وقت المعالجة دون فائدة.
- **تحقق من صحة المخرجات** بالبحث عن سلاسل فارغة أو أحرف غير متوقعة، خاصةً عند معالجة مستندات ممسوحة ضوضاؤها.

## الخطوات التالية

الآن بعد أن أصبحت قادرًا على **استخراج النص من صورة**، فكر في توسيع الحل:

- **تحويل الصور إلى نص بشكل جماعي**: قراءة مجلد من الصور، معالجة كل ملف، وكتابة النتائج إلى ملف CSV.
- **التكامل مع التخزين السحابي**: سحب الصور من Azure Blob Storage أو Amazon S3، تشغيل OCR، وتخزين النص المستخرج مرة أخرى في السحابة.
- **دمج مع واجهات ترجمة**: بعد التعرف على النص السيريلي، استدعِ Azure Translator أو Google Cloud Translation لإنتاج ترجمة إنجليزية.
- **استكشاف تحليل التخطيط المتقدم**: يوفر Aspose.OCR كائنات `OcrPage` التي تكشف إحداثيات النص، مفيدة لإعادة إنشاء ملفات PDF أو مستندات قابلة للبحث.

باتباع الخطوات في هذا الدليل، ستحصل على أساس قوي لأي مشروع يحتاج إلى **تحويل الصورة إلى نص** أو **التعرف على نص الصورة** عبر لغات متعددة.

---


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image with Aspose OCR – C# Quickstart](/ocr/english/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-quickstart/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}