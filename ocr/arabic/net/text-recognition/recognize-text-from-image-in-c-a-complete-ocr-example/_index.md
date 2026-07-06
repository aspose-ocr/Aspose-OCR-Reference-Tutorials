---
category: general
date: 2026-06-19
description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. اتبع مثال OCR بلغة
  C# لاستخراج النص من ملفات JPG وتعلم كيفية ضبط لغة OCR بسرعة.
draft: false
keywords:
- recognize text from image
- extract text from jpg
- c# ocr example
- read text from image file
- set OCR language
language: ar
og_description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدليل
  مثالًا كاملاً لاستخدام OCR في C#، ويغطي كيفية تعيين لغة OCR واستخراج النص من ملفات
  JPG.
og_title: التعرف على النص من الصورة في C# – مثال كامل على OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: recognize text from image using Aspose OCR in C#. Follow this c# ocr
    example to extract text from jpg files and learn how to set ocr language quickly.
  headline: recognize text from image in C# – a complete OCR example
  type: TechArticle
- questions:
  - answer: Absolutely. Wrap the recognition call in a `foreach (var file in Directory.GetFiles(folder,
      "*.jpg"))` loop. Remember to reuse the same `engine` instance for speed.
    question: Can I process a folder of JPG files automatically?
  - answer: The default models focus on printed text. For handwritten recognition
      you’d need a specialized model—Aspose currently offers a separate Handwriting
      OCR package.
    question: Does Aspose.OCR support handwritten text?
  - answer: 'Convert the PDF page to an image first (e.g., using Aspose.PDF) and then
      feed that image to the OCR engine. --- ## Conclusion We’ve just **recognize
      text from image** using a concise **c# OCR example** that shows how to **set
      OCR language**, trigger automatic resource download, and **extract text fr'
    question: What if I need to extract text from a PDF page instead of a JPG?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: التعرف على النص من صورة في C# – مثال كامل على OCR
url: /ar/net/text-recognition/recognize-text-from-image-in-c-a-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في C# – مثال كامل على OCR

هل احتجت يوماً إلى **التعرف على النص من صورة** لكن لم تكن متأكدًا من المكتبة التي تختارها؟ لست وحدك. في العديد من المشاريع—مسح الفواتير، التحقق من الهوية، أو مجرد استخراج التعليقات من الصور—تُعد القدرة على قراءة النص من ملف صورة معززة حقيقية للإنتاجية.

في هذا الدرس سنستعرض **مثال C# OCR** يستخدم Aspose.OCR **لاستخراج النص من ملفات jpg**. بنهاية الدرس ستعرف بالضبط كيف **تضبط لغة OCR**، وتتعامل مع تحميل النماذج تلقائيًا، وتطبع السلسلة المتعرف عليها—كل ذلك ببضع أسطر من الشيفرة فقط.

## ما ستتعلمه

- كيفية ضبط محرك OCR للغة معينة (مثل الإنجليزية، العربية، الهندية).  
- كيفية استدعاء المحرك بحيث يقوم التحميل الأولي للموارد تلقائيًا.  
- كيفية إمداد صورة JPEG واسترجاع نص نظيف وقابل للقراءة.  
- نصائح لتجاوز المشكلات الشائعة مثل الخطوط المفقودة أو الصيغ غير المدعومة.  

**المتطلبات المسبقة**: .NET 6+ (أو .NET Core 3.1)، نسخة حديثة من Visual Studio أو VS Code، وحزمة Aspose.OCR عبر NuGet. لا تحتاج إلى خبرة سابقة في OCR.

---

![مخطط يوضح سير عمل التعرف على النص من صورة باستخدام Aspose OCR في C#](/images/ocr-workflow.png "مخطط سير عمل التعرف على النص من صورة")

## الخطوة 1: تثبيت حزمة Aspose.OCR عبر NuGet

قبل كتابة أي شيفرة، نحتاج إلى المكتبة. افتح الطرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن “Aspose.OCR” ثم اضغط *Install*. الحزمة تتضمن المحرك الأساسي وفئات الإعداد التي سنستخدمها لاحقًا.

## الخطوة 2: ضبط محرك OCR – **set OCR language**

أول شيء يجب فعله هو إخبار المحرك أي لغة يبحث عنها. هنا يبرز دور كلمة المفتاح **set OCR language**. كائن `OcrEngineConfig` يحتوي على جميع الإعدادات التي تحتاجها.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;

// Choose the language you want to recognize.
// Language.English is the default, but you can switch to Arabic, Hindi, etc.
var config = new OcrEngineConfig
{
    Language = Language.English,          // <-- set OCR language here
    AutoDownloadResources = true         // downloads the model on first use
};
```

لماذا نحتاج `AutoDownloadResources`؟ في المرة الأولى التي تشغّل فيها البرنامج، سيقوم Aspose بتحميل النموذج المناسب من السحابة. هذا يعني أنك لا تحتاج إلى شحن ملفات نماذج ضخمة مع تطبيقك—فائدة كبيرة لحجم النشر.

## الخطوة 3: إنشاء محرك OCR

الآن بعد أن لدينا إعدادًا، يمكننا إنشاء المثيل. استخدام جملة `using` يضمن تحرير المحرك بشكل صحيح، مما يحرّر الموارد الأصلية.

```csharp
// The engine respects the configuration we just defined.
using var engine = new OcrEngine(config);
```

إذا احتجت لتغيير اللغة أثناء التشغيل، يمكنك ببساطة تعيين قيمة `Language` جديدة إلى `engine.Config.Language` قبل استدعاء `RecognizeImage`.

## الخطوة 4: التعرف على النص من صورة – **c# OCR example** الأساسي

هذه هي لحظة الحقيقة: نمرر ملف JPEG ونطلب من المحرك تنفيذ السحر. الاستدعاء الأول سيُطلق تحميل النموذج تلقائيًا إذا لم يحدث ذلك بعد.

```csharp
// Replace the path with the location of your test image.
string imagePath = Path.Combine(Environment.CurrentDirectory, "sample_english.jpg");

// RecognizeImage returns an OcrResult containing the extracted string.
OcrResult result = engine.RecognizeImage(imagePath);
```

> **ماذا لو كانت الصورة PNG أو BMP؟**  
> طريقة `RecognizeImage` تقبل أي صيغة يدعمها System.Drawing، لذا يمكنك تمرير PNG أو BMP أو حتى TIFF دون تعديل.

## الخطوة 5: إخراج النص المتعرف عليه – **read text from image file**

أخيرًا، نكتب النتيجة إلى وحدة التحكم. في تطبيق واقعي قد تخزنها في قاعدة بيانات أو تمرّرها إلى خدمة أخرى.

```csharp
// The Text property holds the plain‑text representation of the image.
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(result.Text);
```

### النتيجة المتوقعة

إذا كان `sample_english.jpg` يحتوي على العبارة “Hello, Aspose OCR!”، ستظهر وحدة التحكم:

```
=== Recognized Text ===
Hello, Aspose OCR!
```

لاحظ نظافة الإخراج—لا فواصل أسطر إضافية أو بقايا OCR. Aspose يقوم بعمل جيد في تطبيع الفراغات مباشرةً.

## التعامل مع الحالات الشائعة

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **فشل تحميل النموذج** | تأكد من أن الجهاز متصل بالإنترنت. يمكنك أيضًا تحميل النموذج مسبقًا عبر استدعاء `engine.DownloadResources()` يدويًا. |
| **اكتشاف لغة غير صحيح** | اضبط `config.Language` صراحةً إلى القيمة الصحيحة (مثال: `Language.Arabic`). |
| **صورة منخفضة الدقة** | قم بزيادة حجم الصورة أو تطبيق فلتر تحسين قبل استدعاء `RecognizeImage`. |
| **معالجة دفعات كبيرة** | أعد استخدام نفس كائن `OcrEngine` عبر عدة استدعاءات لتجنب تحميل النموذج المتكرر. |

## مثال كامل جاهز للنسخ واللصق

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Configuration;

class Program
{
    static void Main()
    {
        // Step 1: Configure the OCR engine – select the language and enable auto‑download
        var config = new OcrEngineConfig
        {
            Language = Language.English,          // e.g., Language.Arabic, Language.Hindi, etc.
            AutoDownloadResources = true         // downloads the required model on first use
        };

        // Step 2: Create the OCR engine with the specified configuration
        using var engine = new OcrEngine(config);

        // Step 3: Recognize text from an image (the first call triggers the model download if needed)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "sample_english.jpg");
        OcrResult result = engine.RecognizeImage(imagePath);

        // Step 4: Output the recognized text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
```

شغّل البرنامج باستخدام `dotnet run`. إذا تم إعداد كل شيء بشكل صحيح، سترى السلسلة المستخرجة مطبوعة في وحدة التحكم.

---

## الأسئلة المتكررة

**س: هل يمكنني معالجة مجلد من ملفات JPG تلقائيًا؟**  
ج: بالتأكيد. ضع استدعاء التعرف داخل حلقة `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`. تذكر إعادة استخدام نفس كائن `engine` للسرعة.

**س: هل يدعم Aspose.OCR النص المكتوب يدويًا؟**  
ج: النماذج الافتراضية تركز على النص المطبوع. للتعرف على النص اليدوي تحتاج إلى نموذج متخصص—Aspose يقدم حزمة Handwriting OCR منفصلة.

**س: ماذا لو أردت استخراج النص من صفحة PDF بدلاً من JPG؟**  
ج: حوّل صفحة PDF إلى صورة أولًا (مثال باستخدام Aspose.PDF) ثم مرّر تلك الصورة إلى محرك OCR.

---

## الخلاصة

لقد تعلمنا الآن **التعرف على النص من صورة** باستخدام مثال **c# OCR** مختصر يوضح كيفية **set OCR language**، تشغيل التحميل التلقائي للموارد، و**استخراج النص من jpg** بحد أدنى من الشيفرة. تدفق العمل الكامل—من تثبيت حزمة NuGet إلى طباعة النتيجة—يُحَاط بوسيلة واحدة، ما يجعل دمجه في تطبيقات أكبر سهلًا.

ما الخطوة التالية؟ جرّب استبدال `Language.English` بـ `Language.French` أو `Language.Hindi` ولاحظ كيف يتكيف المحرك. جرب صيغ صور مختلفة، أو عالج دفعة من الملفات لتقييم الأداء. API الخاص بـ Aspose.OCR مرن بما يكفي للنماذج السريعة والخدمات الإنتاجية.

إذا وجدت هذا الدليل مفيدًا، أعطه نجمة على GitHub، شاركه مع زملائك، أو اترك تعليقًا أدناه حول تجاربك مع OCR. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي عرضناها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}