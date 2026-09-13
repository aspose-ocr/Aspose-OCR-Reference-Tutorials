---
category: general
date: 2026-09-13
description: تعلم استخراج النص من ملفات JPG في C# عن طريق تحميل صورة للتعرف الضوئي
  على الأحرف، ضبط لغة OCR، وتشغيل Aspose OCR – دليل خطوة بخطوة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from jpg
- load image for ocr
- set ocr language
- c# ocr tutorial
language: ar
lastmod: 2026-09-13
og_description: استخراج النص من ملفات JPG في C# باستخدام هذا الدرس المختصر عن OCR.
  تعلم كيفية تحميل صورة للـ OCR، ضبط لغة الـ OCR، والحصول على نتائج دقيقة.
og_image_alt: Screenshot of C# console output showing extracted Ukrainian text from
  a JPG image
og_title: استخراج النص من JPG في C# – دليل OCR كامل
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn to extract text from JPG files in C# by loading an image for
    OCR, setting OCR language, and running Aspose OCR – a step‑by‑step guide.
  headline: How to extract text from JPG using a C# OCR tutorial
  type: TechArticle
- description: Learn to extract text from JPG files in C# by loading an image for
    OCR, setting OCR language, and running Aspose OCR – a step‑by‑step guide.
  name: How to extract text from JPG using a C# OCR tutorial
  steps:
  - name: Install the Aspose.OCR package
    text: 'Open a terminal in your project folder and run:'
  - name: Create a console application skeleton
    text: 'Create a new console project if you don’t already have one:'
  - name: Load an image for OCR
    text: The first operation after instantiating the engine is to provide the image
      you want to process. Aspose.OCR supports JPEG, PNG, BMP, GIF, and TIFF. In this
      tutorial we work with a JPEG file named **sample_ukrainian.jpg**.
  - name: Set OCR language
    text: OCR accuracy heavily depends on the language model. Aspose.OCR ships with
      data files for more than 30 languages. To recognize Ukrainian text, set the
      language code to `"ukr"`.
  - name: Perform OCR and extract text from JPG
    text: Calling `Recognize()` runs the recognition pipeline and returns the detected
      text as a plain string.
  - name: Run the program and verify the output
    text: 'Compile and execute the application:'
  - name: Loading images from memory or a web request
    text: 'Instead of `ImageStream.FromFile`, you can create a stream from a byte
      array:'
  - name: Processing multiple images in a batch
    text: 'Wrap the OCR logic in a method and iterate over a collection of file paths:'
  - name: Handling errors and edge cases
    text: 'OCR can fail if the image is corrupted or the language data cannot be downloaded.
      Catch exceptions to provide a graceful fallback:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: كيفية استخراج النص من JPG باستخدام دليل OCR بلغة C#
url: /ar/net/text-recognition/how-to-extract-text-from-jpg-using-a-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج النص من JPG باستخدام دليل OCR بلغة C#

إذا كنت بحاجة إلى استخراج النص من صور JPG في تطبيق .NET، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. ستقوم بتحميل صورة للـ OCR، وتعيين لغة الـ OCR، واسترجاع النص المعترف به باستخدام Aspose.OCR—كل ذلك في برنامج C# واحد مكتمل ومستقل.

يغطي الدليل كل ما يلزم لتشغيل الـ OCR على اللغة الأوكرانية أو الإنجليزية أو أي لغة مدعومة. لا تحتاج إلى أدوات خارجية بخلاف حزمة Aspose.OCR على NuGet، ويتبع الكود أفضل الممارسات لإدارة الموارد ومعالجة الأخطاء.

## ما ستحققه

بنهاية هذا الدليل ستتمكن من:

* تحميل صورة للـ OCR مباشرةً من نظام الملفات.  
* تعيين لغة الـ OCR لتطابق المستند الأصلي.  
* استخراج النص من ملف JPG وعرض النتيجة في وحدة التحكم.  
* فهم كيفية تعديل المثال لتعامل مع صيغ صور أخرى أو لغات مختلفة.

**المتطلبات المسبقة**  

* .NET 6.0 SDK أو أحدث مثبت.  
* Visual Studio 2022 (أو أي بيئة تطوير C#).  
* حزمة Aspose.OCR على NuGet (`dotnet add package Aspose.OCR`).  

لا يلزم أي خبرة سابقة في الـ OCR.

## كيفية استخراج النص من JPG باستخدام Aspose OCR في C#

الأقسام التالية تقسم العملية إلى خطوات واضحة. كل خطوة تتضمن مقتطف كود، شرح لأهميتها، ونصائح عملية يمكنك تطبيقها في مشاريعك الواقعية.

### الخطوة 1: تثبيت حزمة Aspose.OCR

افتح الطرفية في مجلد المشروع وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

تحتوي الحزمة على الفئة `OcrEngine`، ملفات بيانات اللغات، وأدوات مساعدة لتحميل الصور. تثبيتها مرة واحدة يجعل المكتبة متاحة لكل مشروع يشير إلى ملف `.csproj`.

### الخطوة 2: إنشاء هيكل تطبيق سطر الأوامر

أنشئ مشروعًا جديدًا لتطبيق سطر الأوامر إذا لم يكن لديك واحد بالفعل:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

استبدل ملف `Program.cs` الذي تم إنشاؤه تلقائيًا بالكود الموضح في الخطوات التالية. الحفاظ على المشروع بسيطًا يساعدك على التركيز على سير عمل الـ OCR.

### الخطوة 3: تحميل صورة للـ OCR

العملية الأولى بعد إنشاء مثيل المحرك هي توفير الصورة التي تريد معالجتها. يدعم Aspose.OCR صيغ JPEG, PNG, BMP, GIF, و TIFF. في هذا الدليل نعمل على ملف JPEG اسمه **sample_ukrainian.jpg**.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 3: Load the image to be processed
        // ImageStream.FromFile reads the file and creates a stream compatible with OcrEngine.
        var imagePath = "YOUR_DIRECTORY/sample_ukrainian.jpg";
        using (var engine = new OcrEngine())
        {
            engine.Image = ImageStream.FromFile(imagePath);
```

**لماذا هذا مهم** – تحميل الصورة إلى `ImageStream` يضمن أن المحرك يستطيع الوصول إلى بيانات البكسل دون قفل الملف الأصلي. هذا النهج يعمل أيضًا مع الصور المخزنة في الذاكرة أو المستلمة من واجهة برمجة تطبيقات ويب.

### الخطوة 4: تعيين لغة الـ OCR

تعتمد دقة الـ OCR بشكل كبير على نموذج اللغة. يأتي Aspose.OCR مع ملفات بيانات لأكثر من 30 لغة. للتعرف على النص الأوكراني، عيّن رمز اللغة إلى `"ukr"`.

```csharp
            // Step 4: Set the language for recognition (Ukrainian = "ukr")
            engine.Language = "ukr";
```

إذا كنت تحتاج إلى معالجة الإنجليزية، استخدم `"eng"`؛ وللإسبانية، `"spa"`. تتبع رموز اللغات معيار ISO 639‑2. عندما تحدد لغة لم تُحمَّل بعد، يقوم المحرك تلقائيًا بتنزيل البيانات المطلوبة في المرة الأولى التي تشغّل فيها الكود.

### الخطوة 5: تنفيذ الـ OCR واستخراج النص من JPG

استدعاء `Recognize()` يشغّل خط أنابيب التعرف ويعيد النص المكتشف كسلسلة نصية عادية.

```csharp
            // Step 5: Perform OCR – required language data will be downloaded automatically if missing
            string recognizedText = engine.Recognize();

            // Step 6: Output the recognized text
            Console.WriteLine("=== Extracted text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**شرح** – يضمن كتلة `using` أن كائن `OcrEngine` يتم التخلص منه بشكل صحيح، مما يحرّر الموارد غير المُدارة مثل مخازن الذاكرة الأصلية. التخلص من المحرك أمر حاسم في الخدمات طويلة التشغيل التي تعالج العديد من الصور.

### الخطوة 6: تشغيل البرنامج والتحقق من المخرجات

قم بترجمة وتنفيذ التطبيق:

```bash
dotnet run
```

يجب أن ترى مخرجات مشابهة لـ:

```
=== Extracted text ===
Привіт, це тестовий текст українською мовою.
```

إذا عرضت وحدة التحكم أحرفًا مشوشة، تأكد من أن الطرفية تستخدم ترميز UTF‑8 (`chcp 65001` على Windows) وأن الصورة المصدرية تحتوي على نص واضح وعالي التباين.

## تكييف دليل الـ OCR بلغة C# لسيناريوهات أخرى

### تحميل الصور من الذاكرة أو طلب ويب

بدلاً من `ImageStream.FromFile`، يمكنك إنشاء تدفق من مصفوفة بايت:

```csharp
byte[] imageBytes = await httpClient.GetByteArrayAsync(imageUrl);
engine.Image = ImageStream.FromBytes(imageBytes);
```

هذه التقنية مفيدة عند معالجة الصور التي يتم رفعها عبر نقطة نهاية API.

### معالجة صور متعددة على دفعات

ضع منطق الـ OCR داخل دالة وكررها على مجموعة من مسارات الملفات:

```csharp
static string ExtractText(string path, string language = "eng")
{
    using var engine = new OcrEngine();
    engine.Image = ImageStream.FromFile(path);
    engine.Language = language;
    return engine.Recognize();
}
```

تقلل المعالجة على دفعات من الحمل الزائد عبر إعادة استخدام نفس مثيل `OcrEngine` إذا نقلت عبارة `using` إلى خارج الحلقة.

### معالجة الأخطاء والحالات الحدية

يمكن أن يفشل الـ OCR إذا كانت الصورة تالفة أو لم يتمكن المحرك من تنزيل بيانات اللغة. امسك الاستثناءات لتوفير طريقة تعافي مرنة:

```csharp
try
{
    string text = ExtractText(imagePath, "ukr");
    Console.WriteLine(text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

يساعد تسجيل الاستثناء في تشخيص مشاكل الشبكة عندما تحتاج ملفات اللغة إلى التحميل.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه مباشرةً إلى `Program.cs`. يتضمن جميع توجيهات `using` المطلوبة، التعليقات، ومعالجة الأخطاء.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Path to the JPEG image you want to process.
        var imagePath = "YOUR_DIRECTORY/sample_ukrainian.jpg";

        // Ensure the file exists before attempting OCR.
        if (!System.IO.File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        try
        {
            // Create the OCR engine inside a using block to guarantee disposal.
            using var engine = new OcrEngine();

            // Load the image for OCR.
            engine.Image = ImageStream.FromFile(imagePath);

            // Set OCR language (Ukrainian = "ukr").
            engine.Language = "ukr";

            // Perform OCR and retrieve the recognized text.
            string recognizedText = engine.Recognize();

            // Output the extracted text.
            Console.WriteLine("=== Extracted text from JPG ===");
            Console.WriteLine(recognizedText);
        }
        catch (Exception ex)
        {
            // Handle any exceptions that occur during OCR.
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

تشغيل هذا الكود يستخرج النص من ملف JPG ويطبعه في وحدة التحكم. استبدل `imagePath` و `engine.Language` للعمل مع ملفات ولغات أخرى.

## الخلاصة

أنت الآن تعرف كيف تستخرج النص من صور JPG في C# عبر تحميل صورة للـ OCR، تعيين لغة الـ OCR، وتنفيذ دليل OCR مختصر. يوضح المثال أفضل الممارسات مثل التخلص السليم من `OcrEngine`، معالجة نقص بيانات اللغة، وتوفير رسائل خطأ واضحة.

من هنا يمكنك:

* تجربة رموز لغات مختلفة (`"eng"`, `"spa"`, `"fra"`).  
* دمج منطق الـ OCR في واجهات ASP.NET Core API للمعالجة الفورية للصور.  
* دمج مخرجات الـ OCR مع مكتبات معالجة اللغة الطبيعية لتحليل المحتوى المستخرج.

لا تتردد في تعديل الكود لمشاريعك الخاصة، ومشاركة نتائجك في التعليقات أو على وسائل التواصل الاجتماعي. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image in C# – Offline OCR with Aspose (Step‑by‑Step Guide)](/ocr/english/net/text-recognition/extract-text-from-image-in-c-offline-ocr-with-aspose-step-by/)
- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}