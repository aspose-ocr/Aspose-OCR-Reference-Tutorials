---
category: general
date: 2026-10-21
description: تعلم كيفية إجراء التعرف الضوئي على الأحرف (OCR) على ملف JPG، استخراج
  النص من الصورة وتحميل الصورة للتعرف الضوئي على الأحرف باستخدام Aspose.OCR في C#.
  دليل كامل خطوة بخطوة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from jpg
- load image for OCR
- perform OCR on image
language: ar
lastmod: 2026-10-21
og_description: كيفية تنفيذ OCR على صورة في C# باستخدام Aspose.OCR. اتبع هذا الدليل
  لتحميل الصورة للـ OCR، التعرف على النص من ملف JPG واستخراج النص من الصورة.
og_image_alt: Screenshot showing how to perform OCR on a Cyrillic image in C#
og_title: كيفية تنفيذ OCR على صورة في C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to perform OCR on a JPG, extract text from image and load
    image for OCR using Aspose.OCR in C#. Complete step‑by‑step guide.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
- Image processing
- Text extraction
title: كيفية إجراء OCR على صورة في C# باستخدام Aspose.OCR
url: /ar/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR على صورة في C# باستخدام Aspose.OCR

إذا كنت بحاجة إلى **كيفية تنفيذ OCR** على صورة، فإن هذا الدليل يوضح لك حلاً كاملاً جاهزًا للتنفيذ. ستتعلم كيفية تحميل صورة للـ OCR، التعرف على النص من ملفات JPG، واستخراج النص من الصورة باستخدام مكتبة Aspose.OCR.

يغطي الدليل كل شيء بدءًا من تثبيت حزمة NuGet إلى التعامل مع نماذج اللغة وطباعة النتيجة المعترف بها. في النهاية ستكون قادرًا على دمج OCR في أي مشروع .NET ومعالجة النصوص السيريالية أو أي لغات أخرى دون مغادرة بيئة التطوير المتكاملة.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+)
- Visual Studio 2022 (أو أي محرر C#)
- اتصال بالإنترنت للتشغيل الأول (Aspose.OCR يقوم بتحميل نموذج اللغة تلقائيًا)
- صورة نموذجية، مثال: `cyrillic_sample.jpg`، موجودة في مجلد يمكنك الإشارة إليه من الكود

## الخطوة 1: تثبيت Aspose.OCR

افتح مدير حزم NuGet وأضف **Aspose.OCR** إلى مشروعك:

```bash
dotnet add package Aspose.OCR
```

تحتوي الحزمة على محرك OCR، نماذج اللغة، والفئات المساعدة اللازمة لمعالجة الصور. لا توجد DLLs إضافية مطلوبة.

## الخطوة 2: إنشاء محرك OCR – كيفية تنفيذ OCR

المهمة الحقيقية الأولى في **كيفية تنفيذ OCR** هي إنشاء كائن المحرك. هذا الكائن يدير كامل خط أنابيب التعرف.

```csharp
using Aspose.OCR;

// Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

`OcrEngine` خفيف الوزن؛ يمكنك إعادة استخدام نفس المثيل لعدة صور، مما يحسن الأداء عند معالجة دفعات من الصور.

## الخطوة 3: تحميل الصورة للـ OCR

قبل عملية التعرف يجب توفير بيانات الصورة. خطوة **تحميل الصورة للـ OCR** تقبل صيغًا متعددة، لكن هذا المثال يركز على ملف JPEG.

```csharp
// Load the image you want to process
engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

`OcrImage.FromFile` يقرأ الملف إلى الذاكرة ويجهزه للمحرك. إذا كان مسار الملف غير صالح، سيتم إلقاء `ArgumentException`، لذا تأكد من صحة المسار.

## الخطوة 4: اختيار اللغة المناسبة (اختياري لكن يُنصح به)

إذا كانت صورتك تحتوي على أحرف سيريالية، اضبط اللغة إلى `Cyrillic`. النموذج المطلوب يتم تحميله تلقائيًا في التشغيل الأول.

```csharp
// Choose the language model
engine.Language = OcrLanguage.Cyrillic;
```

يمكنك التبديل إلى لغات أخرى (مثل `OcrLanguage.English`) بتغيير هذه الخاصية. المكتبة تدعم أكثر من 60 لغة.

## الخطوة 5: التعرف على النص من JPG – كيفية تنفيذ OCR على JPEG

الآن استدعِ طريقة `Recognize`. هذه هي جوهر **كيفية تنفيذ OCR** وتحوّل البت ماب إلى نص Unicode.

```csharp
// Perform the recognition
engine.Recognize();
```

الطريقة تحجب التنفيذ حتى ينتهي عملية OCR. للصور الكبيرة قد ترغب في تشغيلها على خيط خلفي للحفاظ على استجابة واجهة المستخدم.

## الخطوة 6: استخراج النص من الصورة

بعد التعرف، يخزن المحرك النتيجة في الخاصية `Text`. هذا يُكمل خطوة **استخراج النص من الصورة**.

```csharp
// Retrieve the extracted text
string extractedText = engine.Text;

// Output the recognized text to the console
Console.WriteLine(extractedText);
```

سيحتوي الناتج على الأحرف الدقيقة الموجودة في الصورة، مع الحفاظ على فواصل الأسطر وعلامات الترقيم.

## مثال كامل قابل للتنفيذ

جمع جميع الخطوات معًا يمنحك برنامجًا واحدًا يمكنك نسخه ولصقه وتشغيله:

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image for OCR
        engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");

        // Step 3: Choose the language model (Cyrillic in this case)
        engine.Language = OcrLanguage.Cyrillic;

        // Step 4: Perform OCR on the image
        engine.Recognize();

        // Step 5: Extract text from image
        string extractedText = engine.Text;

        // Step 6: Output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

### النتيجة المتوقعة

إذا كان ملف `cyrillic_sample.jpg` يحتوي على العبارة “Привет мир” (Hello world)، سيظهر في وحدة التحكم:

```
=== OCR Result ===
Привет мир
```

قد تؤثر الخطوط المختلفة أو جودة الصورة على الدقة، لكن Aspose.OCR عادةً ما يحقق أكثر من 95 % دقة على الطبعات الواضحة.

## المشكلات الشائعة والنصائح العملية

- **جودة الصورة مهمة** – JPEG منخفض الدقة أو المشوش يقلل من الدقة. عالج الصورة مسبقًا (مثلاً، زيادة التباين) باستخدام `engine.Image.AdjustContrast()` إذا لزم الأمر.
- **تحميل نموذج اللغة** – التنفيذ الأول يحمل النموذج إلى `%USERPROFILE%\.Aspose\OCR`. تأكد من أن العملية لديها صلاحية كتابة.
- **معالجة الدفعات** – أعد استخدام نفس مثيل `OcrEngine` وغيّر فقط `engine.Image` بين الملفات. هذا يتجنب تحميل النموذج مرارًا.
- **استهلاك الذاكرة** – الصور الكبيرة تستهلك RAM أكثر. استدعِ `engine.Image.Dispose()` بعد كل عملية إذا كنت تعالج ملفات متعددة في حلقة.
- **سلامة الخيوط** – `OcrEngine` غير آمن للاستخدام المتعدد الخيوط. أنشئ مثيلًا منفصلًا لكل خيط عند التوازي.

## الخلاصة

أنت الآن تعرف **كيفية تنفيذ OCR** على JPEG، **تحميل صورة للـ OCR**، و**استخراج النص من الصورة** باستخدام Aspose.OCR في C#. يوضح الحل الكامل ضبط اللغة، التعرف على النص من JPG، وطباعة النتيجة، مما يمنحك أساسًا قويًا لأي مشروع استخراج نص.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **تنفيذ OCR على دفعات من الصور**، دمج OCR مع واجهات ASP.NET Core APIs، أو تحويل النص المستخرج إلى ملفات PDF قابلة للبحث. جرّب لغات وصور مختلفة لتحسين جودة التعرف.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Perform OCR in C# – Convert Image to Text with Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-text-with-aspose-oc/)
- [How to Perform OCR in C# – Recognize Text from Image](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/)
- [How to extract text from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}