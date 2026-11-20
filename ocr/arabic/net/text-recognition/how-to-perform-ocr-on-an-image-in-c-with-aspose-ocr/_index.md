---
category: general
date: 2026-10-18
description: قم بتنفيذ التعرف الضوئي على الأحرف (OCR) على صورة في C# بسرعة. تعلم استخراج
  النص من JPG، تحويل الصورة إلى نص وقراءة النص من الصورة باستخدام Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- convert image to text
- read text from image
- load image for OCR
language: ar
lastmod: 2026-10-18
og_description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على صورة باستخدام C# مع Aspose.OCR.
  يوضح هذا الدليل كيفية استخراج النص من ملف JPG، تحويل الصورة إلى نص، وقراءة النص
  من الصورة في دقائق.
og_image_alt: Console output displaying recognized Cyrillic text after performing
  OCR on an image
og_title: إجراء التعرف الضوئي على الأحرف (OCR) على صورة في C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Perform OCR on an image in C# quickly. Learn to extract text from JPG,
    convert image to text and read text from image using Aspose.OCR.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
title: كيفية إجراء OCR على صورة في C# باستخدام Aspose.OCR
url: /ar/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR على صورة في C# باستخدام Aspose.OCR

إذا كنت بحاجة إلى **تنفيذ OCR على صورة** في تطبيق .NET، فإن هذا الدليل يوضح لك حلاً كاملاً جاهزًا للتنفيذ. ستتعرف على كيفية **تحميل الصورة لـ OCR**، التعرف على الأحرف السيريلية، و**استخراج النص من ملفات JPG** دون كتابة أي كود معالجة صورة منخفض المستوى.

في هذا البرنامج التعليمي ستقوم بـ:

* تثبيت حزمة Aspose.OCR عبر NuGet.  
* تحميل ملف صورة (JPG، PNG، BMP، إلخ).  
* تشغيل محرك OCR **لتحويل الصورة إلى نص**.  
* **قراءة النص من مخرجات الصورة** في وحدة التحكم.  

تعمل الخطوات مع أي صورة متوافقة مع .NET، لذا يمكنك تعديلها لتعمل مع ملفات PDF، الإيصالات الممسوحة، أو لقطات الشاشة.

## المتطلبات المسبقة

* .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+).  
* Visual Studio 2022 أو أي محرر C# تفضله.  
* اتصال بالإنترنت للتشغيل الأول – يقوم Aspose.OCR بتنزيل وحدة اللغة السيريلية تلقائيًا.  

> **نصيحة احترافية:** حافظ على تحديث حزمة NuGet؛ الإصدارات الأحدث تحسن دقة التعرف وتضيف حزم لغات جديدة.

## الخطوة 1: تثبيت Aspose.OCR

افتح الطرفية في مجلد المشروع وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

تحتوي الحزمة على الفئة `OcrEngine` المستخدمة **لتنفيذ OCR على ملفات الصورة**. بعد انتهاء الأمر، سيظهر مرجع الحزمة في ملف *.csproj* الخاص بك.

## الخطوة 2: إنشاء هيكل برنامج وحدة تحكم

أنشئ مشروع وحدة تحكم جديد إذا لم يكن لديك واحد بالفعل:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

استبدل ملف *Program.cs* المُولد بالكود الموضح في الأقسام التالية. يتضمن الهيكل التوجيهات `using` المطلوبة وطريقة `Main` التي تدير عملية OCR.

## الخطوة 3: تحميل الصورة لـ OCR

السطر الوظيفي الأول **يقوم بتحميل الصورة** التي تريد تحليلها. يقبل Aspose.OCR أي تدفق (Stream)، لذا يمكنك تحميل ملف من القرص، أو من عنوان ويب، أو من مورد مدمج.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 3: Load the image containing Cyrillic text
        // Replace the path with the location of your JPG file.
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);
```

*لماذا هذا مهم*: استخدام `ImageStream.FromFile` يُجردك من التعامل مع تنسيقات الملفات، مما يضمن أن محرك OCR يتلقى bitmap ثابت بغض النظر عن نوع الملف الأصلي. كما يتم تحرير التدفق تلقائيًا بفضل جملة `using`.

## الخطوة 4: تهيئة محرك OCR وتعيين اللغة (اختياري)

بشكل افتراضي يحاول Aspose.OCR اكتشاف اللغة تلقائيًا. للنص السيريليني يمكنك طلب وحدة `Language.Cyrillic` صراحةً، مما يسرّع عملية التنزيل الأولى.

```csharp
        // Step 4: Initialize the OCR engine
        var engine = new OcrEngine();

        // Optional: force Cyrillic language to avoid auto‑detection overhead
        engine.Language = Language.Cyrillic;
```

إذا حذفت تعيين اللغة، سيقوم المحرك بتنزيل الوحدة اللازمة في المرة الأولى التي تستدعي فيها `Recognize`. يتم التنزيل عبر HTTPS ويُخزن مؤقتًا محليًا للعمليات اللاحقة.

## الخطوة 5: تنفيذ OCR وتحويل الصورة إلى نص

الآن تقوم فعليًا **بتنفيذ OCR على الصورة** وتحصل على سلسلة نصية عادية. تقوم طريقة `Recognize` بكل الأعمال الثقيلة: المعالجة المسبقة، تحليل التخطيط، وتصنيف الأحرف.

```csharp
        // Step 5: Perform OCR – convert image to text
        engine.Image = image;
        string recognizedText = engine.Recognize();
```

السلسلة `recognizedText` المرتجعة تحتوي على فواصل أسطر تتطابق مع التخطيط الأصلي، مما يسهل معالجتها لاحقًا أو تخزينها في قاعدة بيانات.

## الخطوة 6: عرض النتيجة – قراءة النص من الصورة

أخيرًا، **اقرأ النص من الصورة** بكتابة النتيجة إلى وحدة التحكم. هذه الخطوة تتحقق من نجاح OCR وتظهر لك بالضبط ما تم استخراجها.

```csharp
        // Step 6: Display the recognized text – read text from image
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

عند تشغيل البرنامج (`dotnet run`)، يجب أن ترى مخرجات مشابهة لـ:

```
=== OCR Result ===
Пример текста на кириллице
```

> **ملاحظة:** تعتمد النتيجة الدقيقة على جودة ملف JPG الأصلي. الصور الواضحة وعالية الدقة تعطي أفضل النتائج.

## الكود الكامل القابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في *Program.cs* وتنفيذه دون تعديل (باستثناء مسار الصورة).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Load the image containing Cyrillic text
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);

        // Initialize the OCR engine
        var engine = new OcrEngine
        {
            // Force Cyrillic language; optional but speeds up first run
            Language = Language.Cyrillic,
            Image = image
        };

        // Recognize the text – this converts the image to text
        string recognizedText = engine.Recognize();

        // Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

تشغيل البرنامج يطبع الأحرف المستخرجة إلى وحدة التحكم، مما يثبت أنك نجحت في **استخراج النص من JPG** و**تحويل الصورة إلى نص**.

## معالجة الاختلافات الشائعة

| السيناريو | التعديل |
|----------|------------|
| **لغة مختلفة** | عيّن `engine.Language = Language.English;` أو أي تعداد مدعوم آخر. |
| **PDF متعدد الصفحات** | حوّل كل صفحة إلى صورة (مثلاً باستخدام `Aspose.PDF`) واستدعِ حلقة OCR لكل صورة. |
| **دفعة كبيرة** | غلف استدعاء OCR داخل حلقة `Parallel.ForEach`؛ أعد استخدام كائن `OcrEngine` واحد لتقليل استهلاك الذاكرة. |
| **صورة منخفضة الدقة** | عالج مسبقًا باستخدام `engine.Image = ImageProcessing.Filters.GaussianBlur(image, 1.5);` لتقليل الضوضاء قبل التعرف. |

تتيح لك هذه التعديلات **استخراج النص من JPG** لأي لغة، حجم أو جودة.

## نصائح الأداء

* **تخزين وحدات اللغة مؤقتًا** – قد يستغرق التنزيل الأول بضع ثوانٍ؛ التشغيلات اللاحقة تكون فورية. |
* **إعادة استخدام كائن `OcrEngine`** لعدة صور لتجنب تكاليف التهيئة المتكررة. |
* **تقليل حجم الصورة** – الصور الضخمة جدًا تستهلك ذاكرة أكبر. قلل العرض إلى أقصى 2000 px قبل تمريرها إلى المحرك.

## الخلاصة

أنت الآن تعرف كيف **تنفذ OCR على ملفات الصورة** في C# باستخدام Aspose.OCR. عبر تحميل صورة، ضبط المحرك، واستدعاء `Recognize`، يمكنك **استخراج النص من JPG**، **تحويل الصورة إلى نص**، و**قراءة النص من الصورة** ببضع أسطر من الكود.  

من هنا يمكنك استكشاف:

* تخزين نتائج OCR في قاعدة بيانات لأرشفة قابلة للبحث.  
* دمج سير العمل في واجهة ويب API تستقبل صورًا مرفوعة.  
* استخدام وحدات لغات أخرى (العربية، الهندية، إلخ) لتوسيع نطاق تطبيقك.

لا تتردد في تجربة صيغ صور مختلفة، لغات متعددة، واستراتيجيات معالجة دفعات. النمط الأساسي—**تحميل الصورة لـ OCR → التعرف → معالجة النص العادي**—يبقى هو نفسه، مما يمنحك أساسًا قويًا لأي مشروع استخراج نص.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف طرق تنفيذ بديلة في مشاريعك.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to extract text from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}