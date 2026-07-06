---
category: general
date: 2026-03-20
description: دروس C# OCR توضح كيفية استخراج النص من ملفات الصور مثل JPG باستخدام محرك
  OCR بسيط. تعلم كيفية تحويل الصورة إلى نص بسرعة.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- recognize text from jpg
- convert image to text
- read image text c#
language: ar
og_description: دورة OCR بلغة C# التي ترشدك لاستخراج النص من صورة JPG وتحويله إلى
  نص عادي باستخدام C#.
og_title: دليل C# للتعرف الضوئي على الحروف – استخراج النص من صور JPG
tags:
- OCR
- C#
- Image Processing
title: 'دورة OCR بلغة C#: استخراج النص من صور JPG'
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-jpg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# OCR – تحويل الصور إلى نص قابل للتحرير

هل احتجت يومًا إلى **c# OCR tutorial** لإثبات مفهوم سريع، لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك. سواء كنت تبني ماسحًا للإيصالات، أو أرشيفًا للوثائق، أو مجرد تجربة تحويل الصورة إلى نص، فإن القدرة على *استخراج النص من ملفات الصورة* مهارة مفيدة لأي مطور .NET.

في هذا الدليل سنظهر لك كيفية **recognize text from jpg**، تحويل النتيجة إلى سلسلة، وطباعةها على وحدة التحكم. بنهاية الدليل ستحصل على مثال مستقل وقابل للتنفيذ يتيح لك *read image text c#* دون الحاجة للبحث في وثائق متفرقة. لا إطالة—حل واضح خطوة بخطوة يعمل اليوم.

## ما ستحتاجه

- **.NET 6** أو أحدث (الكود يستهدف .NET 6، لكن أي بيئة تشغيل حديثة ستكفي)
- مكتبة OCR صغيرة – لأغراض المثال سنستخدم حزمة NuGet الخيالية `SimpleOcr` التي توفر `OcrEngine` وتعداد `Language`. (إذا فضلت Tesseract، فقط استبدل توقيعات الاستدعاءات.)
- ملف صورة باسم `sample.jpg` موجود في مجلد يمكنك الإشارة إليه من مشروعك.
- Visual Studio، VS Code، أو أي محرر تفضله.

هذا كل شيء. لا تبعيات ثقيلة، لا خدمات خارجية، وبالتأكيد لا ملفات إعدادات غامضة.

![مخطط دليل c# OCR](ocr-diagram.png "مخطط دليل c# OCR")

## الخطوة 1: تثبيت حزمة OCR

أولًا، أضف مكتبة OCR إلى مشروعك. افتح طرفية في مجلد الحل وشغّل:

```bash
dotnet add package SimpleOcr --version 1.2.0
```

الحزمة تجلب الثنائيات الأصلية المطلوبة للـ OCR، وهي صغيرة بما يكفي لتبقي عملية البناء سريعة.  
*نصيحة محترف:* إذا كنت تستخدم خط أنابيب CI، قم بتثبيت نسخة محددة (كما فعلنا) لتجنب تغييرات مفاجئة قد تكسر التطبيق لاحقًا.

## الخطوة 2: إعداد هيكل المشروع

أنشئ تطبيقًا سطحيًا جديدًا (أو استخدم مشروعًا موجودًا) وأضف توجيهات `using` اللازمة:

```csharp
using System;
using SimpleOcr;   // The namespace that contains OcrEngine and Language
```

الآن سنكتب الفئة الكاملة `Program`. لاحظ كيف أن كل سطر مُعلّق لشرح *السبب* وراءه—هذا يساعدك على فهم التدفق، لا مجرد النسخ واللصق.

```csharp
namespace ImageToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Define the image file path – adjust the folder as needed.
            string imagePath = @"YOUR_DIRECTORY\sample.jpg";

            // 2️⃣ Choose the language for OCR. English works for most demos.
            Language ocrLanguage = Language.English;

            // 3️⃣ Run the OCR engine – this is where we *extract text from image*.
            string extractedText = OcrEngine.RecognizeText(imagePath, ocrLanguage);

            // 4️⃣ Output the result so you can verify the *convert image to text* step.
            Console.WriteLine("----- OCR RESULT START -----");
            Console.WriteLine(extractedText);
            Console.WriteLine("------ OCR RESULT END ------");
        }
    }
}
```

### لماذا هذه الخطوات مهمة

- **تحديد مسار الصورة** يخبر المحرك أين يبحث. إذا كان المسار خاطئًا، ستطرح استدعاءة OCR استثناء `FileNotFoundException`.  
- **اختيار اللغة** يحسن الدقة؛ المحرك يحمل نماذج خاصة باللغة في الخلفية.  
- **استدعاء `RecognizeText`** يقوم بالعمل الشاق—هذا هو جوهر أي *c# OCR tutorial*.  
- **الطباعة إلى وحدة التحكم** تتيح لك التحقق فورًا من إمكانية *read image text c#* دون بناء واجهة مستخدم أولًا.

## الخطوة 3: تشغيل التطبيق والتحقق من المخرجات

قم بالترجمة والتشغيل:

```bash
dotnet run
```

إذا تم ربط كل شيء بشكل صحيح، سترى شيئًا مشابهًا لـ:

```
----- OCR RESULT START -----
Hello, world!
This is a sample image containing text.
----- OCR RESULT END -----
```

المخرجات الدقيقة تعتمد على محتوى `sample.jpg`. إذا ظهر النص مشوشًا، تحقق من وضوح الصورة، وضبط اللغة بشكل صحيح، وأن مكتبة OCR تدعم النص الذي تستخدمه.

### حالات شائعة

| الحالة | ما الذي يجب التحقق منه | الإصلاح |
|-----------|------------------------|----------|
| **صورة فارغة أو صاخبة** | تباين الصورة، الدقة | معالجة مسبقة باستخدام فلتر تدرج رمادي بسيط أو تغيير الحجم إلى 300 dpi |
| **حروف غير إنجليزية** | تعداد اللغة | استخدم `Language.Spanish`، `Language.French`، إلخ، أو حمّل حزمة لغة مخصصة |
| **مسار الملف يحتوي على مسافات** | سلسلة المسار | استخدم سلسلة حرفية (`@"C:\My Folder\sample.jpg"`) أو هروب الأحرف |
| **مشكلات الأداء** | دفعة كبيرة من الصور | نفّذ OCR بالتوازي (`Parallel.ForEach`) أو خزن نماذج اللغة مؤقتًا |

## الخطوة 4: توسيع المثال – *Convert Image to Text* في واجهة برمجة تطبيقات ويب

إذا رغبت في إتاحة هذه الوظيفة عبر HTTP لاحقًا، يمكنك تغليف المنطق نفسه في متحكم ASP.NET Core:

```csharp
[ApiController]
[Route("api/[controller]")]
public class OcrController : ControllerBase
{
    [HttpPost("extract")]
    public IActionResult Extract([FromForm] IFormFile file)
    {
        // Save the uploaded file to a temporary location
        var tempPath = Path.GetTempFileName();
        using (var stream = System.IO.File.Create(tempPath))
        {
            file.CopyTo(stream);
        }

        // Run OCR – reuse the same code as in the console app
        string text = OcrEngine.RecognizeText(tempPath, Language.English);

        // Clean up the temp file
        System.IO.File.Delete(tempPath);

        return Ok(new { extractedText = text });
    }
}
```

الآن لديك نقطة نهاية **read image text c#** يمكن استدعاؤها من أي عميل—محمول، ويب، أو سطح مكتب.

## ملخص – ما تم تغطيته

- **c# OCR tutorial** يرشّحك لتثبيت مكتبة OCR خفيفة.  
- كيفية **extract text from image** عبر تحديد مسار وصيغة لغة.  
- الكود الدقيق لـ **recognize text from jpg** وطباعة النتيجة، محققًا حالة الاستخدام *convert image to text*.  
- نصائح للتعامل مع المشكلات الشائعة ونظرة سريعة على تحويل منطق وحدة التحكم إلى واجهة **read image text c#** API.

كل ما قدمناه هنا مستقل؛ يمكنك نسخ المقاطع، لصقها في مشروع جديد، ومشاهدة OCR يعمل فورًا.

## ما التالي؟

- جرّب **صيغ صور مختلفة** (PNG, BMP) – نفس الـ API يعمل، فقط غيّر امتداد الملف.  
- جرّب **معالجة دفعات** لتسريع *extract text from image* لمجموعات متعددة.  
- استكشف **إعدادات OCR متقدمة** مثل عتبات الثقة أو قوائم الأحرف المسموح بها.  
- دمج ناتج OCR مع **معالجة اللغة الطبيعية** لتصنيف المستندات تلقائيًا أو ملء قواعد البيانات.

هل لديك سؤال حول سيناريو معين، أو تريد مشاركة تعديلك على الخط الأنابيب؟ اترك تعليقًا أدناه—سعيد بمساعدتك على الاستفادة القصوى من رحلة *c# OCR tutorial* الخاصة بك!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}