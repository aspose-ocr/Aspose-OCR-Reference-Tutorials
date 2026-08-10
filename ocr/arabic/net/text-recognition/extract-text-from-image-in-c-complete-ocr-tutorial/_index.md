---
category: general
date: 2026-06-06
description: استخراج النص من الصورة باستخدام OCR في C#. تعلم كيفية تحميل الصورة للتعرف
  الضوئي على الأحرف، التعرف على المستند الممسوح ضوئياً، والحصول على نتائج دقيقة في
  دقائق.
draft: false
keywords:
- extract text from image
- load image for OCR
- recognize scanned document
- c# OCR tutorial
language: ar
og_description: استخراج النص من الصورة باستخدام C#. يوضح هذا الدرس كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف (OCR)، التعرف على المستند الممسوح، وإتقان درس OCR بلغة
  C# خطوة بخطوة.
og_title: استخراج النص من الصورة في C# – دليل OCR كامل
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image using C# OCR. Learn how to load image for OCR,
    recognize scanned document, and get accurate results in minutes.
  headline: Extract Text from Image in C# – Complete OCR Tutorial
  type: TechArticle
- description: Extract text from image using C# OCR. Learn how to load image for OCR,
    recognize scanned document, and get accurate results in minutes.
  name: Extract Text from Image in C# – Complete OCR Tutorial
  steps:
  - name: Save the code as `Program.cs` inside a new console project.
    text: Save the code as `Program.cs` inside a new console project.
  - name: Open a terminal at the project root.
    text: Open a terminal at the project root.
  - name: Run `dotnet add package Aspose.OCR` (if you haven’t already).
    text: Run `dotnet add package Aspose.OCR` (if you haven’t already).
  - name: 'Build and execute:'
    text: 'Build and execute:'
  type: HowTo
- questions:
  - answer: Yes—most OCR libraries let you load a PDF page as an image stream or expose
      a `PdfDocument` API. Convert each page to an image first, then follow the same
      steps.
    question: Can I process PDFs directly?
  - answer: The `ImageStream.FromFile` method supports JPEG, PNG, BMP, and TIFF out
      of the box. No extra conversion required.
    question: What if my image is in PNG format?
  - answer: Handwriting is a tougher nut to crack. Look for a library that offers
      a “handwriting” model, or pre‑process the image with binarization and noise
      removal before feeding it to the engine.
    question: How do I improve accuracy for handwritten notes?
  - answer: 'Absolutely. Most engines expose a `Rect` or `Region` property where you
      can limit OCR to a bounding box—great for forms with fixed fields. --- ## Next
      Steps & Related Topics Now that you’ve mastered the basics of **extract text
      from image** with a **c# OCR tutorial**, consider exploring: - **Batch p'
    question: Is there a way to extract text in a specific region?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: استخراج النص من الصورة في C# – دليل OCR كامل
url: /ar/net/text-recognition/extract-text-from-image-in-c-complete-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة باستخدام C# – دليل OCR كامل

هل تساءلت يومًا كيف **استخراج النص من الصورة** باستخدام بضع أسطر فقط من C#؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى استخراج الكلمات من مسح ضوضائي ومائل، والحيل التقليدية “نسخ‑لصق” لا تنجح غالبًا.  

في هذا الدليل سنستعرض **دورة تعليمية C# OCR** عملية تُظهر لك كيفية **تحميل الصورة لـ OCR**، تمكين المعالجة المسبقة الذكية، وأخيرًا **التعرف على محتوى المستند الممسوح** بدقة واضحة. في النهاية ستحصل على برنامج قابل للتنفيذ يمكنك إدراجه في أي مشروع .NET.

## ما يغطيه هذا الدليل

- تثبيت حزمة NuGet Aspose.OCR (أو ما يعادلها)  
- إنشاء وتكوين كائن محرك OCR  
- **تحميل الصورة لـ OCR** – التعامل مع مسارات الملفات، التدفقات، والمشكلات الشائعة  
- تمكين المعالجة المسبقة التلقائية لإصلاح الميل، إزالة الضوضاء، ومشكلات التباين  
- **التعرف على المستند الممسوح** – استخراج النتيجة كنص عادي  
- الشيفرة الكاملة التي يمكنك نسخها ولصقها وتشغيلها فورًا  

لا تحتاج إلى خبرة سابقة في OCR؛ فقط فهم أساسي لـ C# وVisual Studio (أو أي بيئة تطوير تفضّلها).  

> **لماذا يهم؟** أتمتة استخراج النص تفتح أبوابًا لمعالجة الفواتير، إنشاء ملفات PDF قابلة للبحث، تقليل إدخال البيانات يدويًا، وحتى إعداد مجموعات بيانات جاهزة للذكاء الاصطناعي.  

![استخراج النص من صورة باستخدام OCR في C#](/images/extract-text-from-image-csharp.png "استخراج النص من صورة")

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.8)  
- Visual Studio 2022 (الإصدار Community يكفي)  
- حزمة NuGet `Aspose.OCR` (أو أي مكتبة توفر `OcrEngine`، `OcrResult`، إلخ)  

إذا لم تقم بتثبيت الحزمة بعد، نفّذ الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

هذا الأمر الواحد يجلب جميع الثنائيات الأصلية التي تحتاجها لأداء OCR عالي السرعة.

---

## الخطوة 1: إنشاء كائن محرك OCR

أول ما تقوم به هو تشغيل المحرك الذي سيتولى الجزء الأكبر من العمل. فكر في `OcrEngine` كالعقل المدبر للعملية—بمجرد أن يصبح نشطًا، يمكنك تزويده بالصور وطلب النص.

```csharp
using Aspose.OCR;          // Namespace for OCR classes
using Aspose.OCR.Image;    // For ImageStream helper

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **نصيحة محترف:** احتفظ بالمحرك ككائن Singleton إذا كنت تعالج العديد من الصور دفعة واحدة؛ فهو يعيد استخدام الموارد الداخلية ويسرّع العملية.

## الخطوة 2: تمكين المعالجة المسبقة التلقائية

المسحات الواقعية نادرًا ما تكون مثالية. قد تكون مائلة، مليئة بالضوضاء، أو ذات تباين ضعيف. تمكين `AutoPreprocess` يخبر المحرك بأن يقوم تلقائيًا بتصحيح الميل، إزالة الضوضاء، وضبط التباين قبل أن ينظر إلى الأحرف.

```csharp
// Step 2: Enable automatic preprocessing (deskew, denoise, contrast adjustment)
ocrEngine.Config.AutoPreprocess = true;
```

لماذا هذا مهم؟ بدون المعالجة المسبقة، قد يخطئ محرك OCR في قراءة “8” كـ “B” أو يتخطى سطرًا بالكامل. الخطوة التلقائية تحافظ عليك من كتابة كود مخصص لتنظيف الصورة.

## الخطوة 3: تحديد لغة التعرف

معظم مكتبات OCR تأتي مع حزم لغات. هنا نحدد الإنجليزية، لكن يمكنك التبديل إلى `OcrLanguage.French`، `OcrLanguage.Spanish`، إلخ، حسب المستند.

```csharp
// Step 3: Set the language for recognition
ocrEngine.Language = OcrLanguage.English;
```

إذا كان المستند الممسوح يحتوي على لغات مختلطة، يمكنك إما تشغيل المحرك مرتين أو استخدام نموذج متعدد اللغات—موضوع يمكن استكشافه لاحقًا.

## الخطوة 4: تحميل الصورة لـ OCR

الآن ن **حمّل الصورة لـ OCR**. المساعد `ImageStream.FromFile` يقرأ الملف إلى صيغة يفهمها المحرك. تأكد من أن المسار يشير إلى ملف فعلي؛ المسارات النسبية تعمل عندما تشغّل البرنامج من مجلد المشروع.

```csharp
// Step 4: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **خطأ شائع:** استخدام مسار يحتوي على مسافات دون وضعه بين علامات اقتباس قد يسبب استثناء `FileNotFoundException`. دائمًا تحقق من وجود الملف باستخدام `File.Exists` قبل تمريره إلى المحرك.

## الخطوة 5: تنفيذ التعرف OCR

بعد تكوين كل شيء، ن finally **نتعرف على محتوى المستند الممسوح**. طريقة `Recognize` تقوم بالعمل الشاق وتعيد كائن `OcrResult` يحتوي على النص المستخرج ومستويات الثقة.

```csharp
// Step 5: Perform OCR recognition
OcrResult ocrResult = ocrEngine.Recognize();
```

إذا احتجت مستوى الثقة لكل سطر، يمكنك فحص `ocrResult.Confidence` (قيمة عائمة بين 0 و 1). ثقة منخفضة؟ فكر في تعديل إعدادات المعالجة المسبقة أو توفير صورة ذات دقة أعلى.

## الخطوة 6: إخراج النص المتعرف عليه

أسهل طريقة للتحقق من النجاح هي طباعة النص إلى وحدة التحكم. في تطبيق حقيقي ربما تكتب النص إلى ملف، قاعدة بيانات، أو تمريره إلى خدمة أخرى.

```csharp
// Step 6: Output the recognized text
Console.WriteLine(ocrResult.Text);
```

تشغيل البرنامج يجب أن يطبع شيئًا مثل:

```
The quick brown fox jumps over the lazy dog.
```

حتى وإن كانت الصورة الأصلية مائلة قليلًا أو مليئة بالضوضاء، يجب أن تكون المعالجة المسبقة التلقائية قد نظفتها بما يكفي للحصول على ناتج نظيف.

---

## الشيفرة الكاملة – مثال جاهز للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه إلى مشروع Console جديد (`dotnet new console`). يتضمن جميع الخطوات السابقة، بالإضافة إلى قليل من معالجة الأخطاء لجعل الدليل أكثر صلابة.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace ExtractTextFromImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate input argument
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image-path>");
                return;
            }

            string imagePath = args[0];

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found at '{imagePath}'");
                return;
            }

            try
            {
                // Step 1: Create OCR engine
                OcrEngine ocrEngine = new OcrEngine();

                // Step 2: Enable auto‑preprocess (deskew, denoise, contrast)
                ocrEngine.Config.AutoPreprocess = true;

                // Step 3: Choose language (English in this case)
                ocrEngine.Language = OcrLanguage.English;

                // Step 4: Load image for OCR
                ocrEngine.Image = ImageStream.FromFile(imagePath);

                // Step 5: Recognize scanned document
                OcrResult result = ocrEngine.Recognize();

                // Step 6: Output the extracted text
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
                Console.WriteLine("\n--- End of Output ---\n");

                // Optional: Show confidence if you need it
                Console.WriteLine($"Overall confidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### كيفية التشغيل

1. احفظ الشيفرة كملف `Program.cs` داخل مشروع Console جديد.  
2. افتح طرفية في جذر المشروع.  
3. نفّذ `dotnet add package Aspose.OCR` (إذا لم تقم بذلك مسبقًا).  
4. ابنِ البرنامج ونفّذه:  

   ```bash
   dotnet run "C:\Images\invoice_scanned.jpg"
   ```

يجب أن ترى النص المستخرج يُطبع على وحدة التحكم، مع نسبة الثقة الإجمالية.

---

## الأسئلة المتكررة (FAQs)

**س: هل يمكنني معالجة ملفات PDF مباشرة؟**  
ج: نعم—معظم مكتبات OCR تسمح لك بتحميل صفحة PDF كـ stream صورة أو توفر API `PdfDocument`. حوّل كل صفحة إلى صورة أولًا، ثم اتبع نفس الخطوات.

**س: ماذا لو كانت صورتي بصيغة PNG؟**  
ج: طريقة `ImageStream.FromFile` تدعم JPEG، PNG، BMP، وTIFF مباشرةً. لا حاجة لتحويل إضافي.

**س: كيف أحسن الدقة للملفات المكتوبة يدويًا؟**  
ج: الخط اليدوي أصعب في المعالجة. ابحث عن مكتبة توفر نموذج “handwriting”، أو قم بمعالجة الصورة مسبقًا باستخدام التثنيم وإزالة الضوضاء قبل تمريرها إلى المحرك.

**س: هل يمكن استخراج النص من منطقة محددة؟**  
ج: بالتأكيد. معظم المحركات توفر خاصية `Rect` أو `Region` لتحديد صندوق حدودي يقتصر عليه OCR—مفيد للنماذج ذات الحقول الثابتة.

---

## الخطوات التالية والمواضيع ذات الصلة

بعد أن أتقنت أساسيات **استخراج النص من صورة** عبر **دورة OCR في C#**، يمكنك استكشاف:

- **المعالجة الدفعية** – تكرار عبر مجلد من الصور وكتابة كل نتيجة إلى ملف CSV.  
- **إنشاء PDF** – دمج النص المستخرج مع مكتبة PDF لإنشاء ملفات قابلة للبحث.  
- **معالجة ما بعد التعلم الآلي** – استخدام مدققات إملائية أو نماذج لغة لتنقية أخطاء OCR.  

كل هذه تبني على المفاهيم الأساسية التي غطيناها: تحميل الصورة لـ OCR، تكوين المحرك، والتعرف على المستند الممسوح.

---

## الخلاصة

لقد استعرضنا مثالًا كاملاً من البداية إلى النهاية يوضح كيفية **استخراج النص من صورة** باستخدام C#. من إنشاء `OcrEngine` إلى إخراج السلسلة النهائية، كل سطر من الشيفرة مشروح وجاهز للتنفيذ.  

إذا اتبعت الخطوات، ستتمكن من تحويل المسحات الضوضائية، الإيصالات، أو الملاحظات المكتوبة يدويًا إلى نص قابل للبحث والتحرير في ثوانٍ. استمر في التجربة—عدّل إعدادات المعالجة المسبقة، غيّر اللغات، أو عالج دفعة من الملفات. عالم معالجة المستندات الآلية بانتظارك.

هل لديك أسئلة إضافية أو حالة استخدام مميزة تريد مشاركتها؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شرح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}