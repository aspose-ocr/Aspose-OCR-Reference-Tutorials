---
category: general
date: 2026-01-06
description: تعلم كيفية تصحيح انحراف الصورة، وإزالة الضوضاء، واستخراج النص باستخدام
  Aspose OCR. الدليل خطوة بخطوة يوضح أيضًا كيفية تحميل الصورة للتعرف الضوئي على الأحرف.
draft: false
keywords:
- how to deskew image
- how to extract text
- how to remove noise
- recognize text from image
- load image for ocr
language: ar
og_description: تعلم كيفية تصحيح انحراف الصورة، وإزالة الضوضاء، واستخراج النص باستخدام
  Aspose OCR. يوضح الدليل خطوة بخطوة أيضًا كيفية تحميل الصورة للتعرف الضوئي على الأحرف.
og_title: كيفية تصحيح انحراف الصورة للتعرف الضوئي على الأحرف – دليل C# الكامل
tags:
- OCR
- C#
- Image Processing
title: كيفية تصحيح ميل الصورة للتعرف الضوئي على الأحرف – دليل C# الكامل
url: /ar/net/skew-angle-calculation/how-to-deskew-image-for-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح إمالة الصورة للتعرف الضوئي على الأحرف – دليل C# كامل

هل تساءلت يومًا **how to deskew image** للملفات قبل تمريرها إلى محرك OCR؟ لست وحدك—معظم المطورين يواجهون نفس المشكلة عندما تكون الصورة الممسوحة مائلة قليلًا، أو مليئة بالضوضاء، أو صعبة القراءة. الخبر السار؟ باستخدام Aspose OCR يمكنك تصحيح الإمالة، وتنظيف الصورة، ثم استخراج النص ببضع أسطر من C#.

في هذا الدرس سنستعرض **how to extract text**، **how to remove noise**، وبالطبع **how to deskew image** حتى تكون نتائج OCR دقيقة تمامًا. بحلول النهاية ستعرف أيضًا **how to load image for OCR** وستحصل على سلاسل نصية نظيفة وقابلة للبحث جاهزة لتطبيقك.

---

## ما ستحتاجه

- **Aspose.OCR for .NET** (v23.12 أو أحدث). حزمة NuGet هي `Aspose.OCR`.
- .NET 6+ (أي بيئة تشغيل حديثة).
- صورة نموذجية مائلة أو مليئة بالبقع، مثل `skewed_photo.jpg`.
- Visual Studio أو Rider أو محرّكك المفضّل.

لا توجد مكتبات أصلية إضافية—Aspose يتعامل مع كل شيء داخل العملية.

## الخطوة 1 – إعداد محرك OCR (التعرف على النص من الصورة)

قبل أن نتمكن من **load image for OCR**، نحتاج إلى نسخة من المحرك واللغة التي نريد قراءتها.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine and tell it we’re reading English text.
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

**لماذا هذا مهم:** الـ `OcrEngine` هو قلب العملية. ضبط `Language` مبكرًا يضمن أن خوارزمية التعرف تستخدم مجموعة الأحرف الصحيحة، مما يحسن الدقة بشكل كبير.

## الخطوة 2 – تحميل صورتك (Load Image for OCR)

الآن نوجه المحرك إلى الملف على القرص. هذه هي اللحظة التي تتوقف عندها العديد من الدروس، لكننا سنناقش أيضًا الأخطاء الشائعة.

```csharp
// Load the image you want to process.
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");
```

> **نصيحة احترافية:** استخدم مسارًا مطلقًا أثناء الاختبار، ثم انتقل إلى مسار نسبي أو مورد مدمج للإنتاج. أيضًا، تأكد من أن الصورة بتنسيق مدعوم (JPEG, PNG, BMP, TIFF). إذا حصلت على خطأ “Unsupported format”، تحقق مرة أخرى من امتداد الملف ونوع MIME.

## الخطوة 3 – ما قبل المعالجة: تصحيح الإمالة وإزالة البقع (How to Deskew Image & How to Remove Noise)

وثيقة مائلة هي كابوس كلاسيكي للـ OCR. تقدم Aspose فلتر `DeskewFilter` الذي يكتشف الدوران تلقائيًا حتى زاوية قابلة للتكوين. اجمعه مع `DespeckleFilter` لتنظيف ضوضاء الملح والفلفل.

```csharp
// 1️⃣ Deskew – correct rotation up to 15° (adjust as needed)
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

// 2️⃣ Despeckle – reduce noise; Strength 1‑5 (3 is moderate)
ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });
```

### كيف يعمل فلتر Deskew

يقوم الفلتر بمسح الصورة للعثور على خطوط النص السائدة، يحسب زاوية الإمالة، وي rotates البت ماب وفقًا لذلك. إذا كانت الصورة مستوية بالفعل، لا يفعل الفلتر شيئًا—وبالتالي يمكنك إضافته بأمان إلى أي سلسلة معالجة.

### كيف يساعد فلتر Despeckle

غالبًا ما تظهر الضوضاء كبيكسلات داكنة أو ساطعة منفصلة. خوارزمية despeckle تطبق فلتر متوسط، تحافظ على الحواف (مثل خطوط الأحرف) بينما تنعم البقع. قوة عالية جدًا قد تشوش التفاصيل الدقيقة، لذا ابدأ بـ `Strength = 3` واضبطها بناءً على المادة المصدر.

> **ملاحظة جانبية:** إذا كانت صورك ذات دوران شديد (>15°)، زد `MaxAngle`. بالنسبة للوثائق الممسوحة مقلوبة، قد تحتاج إلى خطوة دوران مخصصة قبل فلتر deskew.

## الخطوة 4 – تشغيل التعرف (Recognize Text from Image)

مع وجود ما قبل المعالجة، نطلب من المحرك أخيرًا قراءة النص.

```csharp
if (ocrEngine.Recognize())
{
    // The recognized text is now stored in ocrEngine.Text
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(ocrEngine.Text);
}
else
{
    Console.WriteLine("Recognition failed – check the image quality.");
}
```

### ماذا يحدث خلف الكواليس؟

1. **Binarization:** يحول الصورة إلى أبيض وأسود، مع تعزيز التباين.
2. **Segmentation:** يقسم البت ماب إلى أسطر وكلمات وأحرف.
3. **Classification:** يطابق كل حرف مع نموذج مدرب (الأبجدية الإنجليزية، الأرقام، علامات الترقيم).
4. **Post‑processing:** يطبق قواعد اللغة (مثل التدقيق الإملائي) لتحسين قابلية القراءة.

نظرًا لأننا قد **deskewed the image** و **removed noise** بالفعل، فإن كل مرحلة تتلقى بيانات أنظف، مما يؤدي إلى تقليل الأخطاء في التعرف.

## الخطوة 5 – التحقق وتنظيف المخرجات (How to Extract Text Effectively)

قد يحتوي النص الخام على فواصل أسطر عشوائية أو مسافات إضافية. تنظيف سريع يجعل البيانات جاهزة للمعالجة اللاحقة.

```csharp
string raw = ocrEngine.Text;

// Trim leading/trailing whitespace and collapse multiple newlines.
string cleaned = System.Text.RegularExpressions.Regex
    .Replace(raw, @"\s+", " ")
    .Trim();

Console.WriteLine("\n=== Cleaned Text ===");
Console.WriteLine(cleaned);
```

**لماذا تنظيفه؟** العديد من مكتبات OCR تحافظ على التخطيط الأصلي، وهو مفيد للـ PDFs لكنه مزعج لسلاسل النص العادية. توحيد المسافات يضمن إمكانية تخزين النتيجة في قاعدة بيانات أو تمريرها إلى فهرس بحث دون جهد إضافي.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق الذي يجمع كل شيء معًا. احفظه باسم `Program.cs`، أضف حزمة Aspose.OCR من NuGet، وشغّله.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to process
        //    (this demonstrates how to load image for OCR)
        ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");

        // 3️⃣ Add preprocessing filters
        //    - Deskew up to 15° (how to deskew image)
        //    - Despeckle with moderate strength (how to remove noise)
        ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
        ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });

        // 4️⃣ Perform recognition (recognize text from image)
        if (ocrEngine.Recognize())
        {
            // 5️⃣ Output raw and cleaned text (how to extract text)
            Console.WriteLine("=== Raw OCR Output ===");
            Console.WriteLine(ocrEngine.Text);

            string cleaned = System.Text.RegularExpressions.Regex
                .Replace(ocrEngine.Text, @"\s+", " ")
                .Trim();

            Console.WriteLine("\n=== Cleaned OCR Output ===");
            Console.WriteLine(cleaned);
        }
        else
        {
            Console.WriteLine("OCR failed – verify the image path and quality.");
        }
    }
}
```

**الناتج المتوقع** (بافتراض أن الصورة النموذجية تحتوي على العبارة “Hello World”):

```
=== Raw OCR Output ===
Hello World

=== Cleaned OCR Output ===
Hello World
```

إذا كانت الصورة مائلة بشدة، ستلاحظ أن الناتج الخام يحتوي على أحرف مشوشة قبل إضافة `DeskewFilter`. بعد الفلتر، يصبح النص مقروءًا—تمامًا ما كنا نسعى لتحقيقه.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كانت صورتي مدارة بأكثر من 15°؟* | زيادة `MaxAngle` في `DeskewFilter`. القيم حتى 45° آمنة، لكن الزوايا الشديدة قد تحتاج إلى دوران يدوي أولاً (`Image.Rotate(angle)`). |
| *ما زال OCR يفوت حروفًا بعد إزالة البقع.* | جرب `Strength` أعلى (4‑5) أو أضف `ContrastFilter` قبل عملية إزالة البقع. |
| *هل يمكنني معالجة ملفات PDF مباشرة؟* | نعم—استخدم `PdfDocument` لتحويل كل صفحة إلى صورة، ثم مرّر كل بت ماب إلى نفس سلسلة المعالجة. |
| *هل المحرك آمن للاستخدام عبر خيوط متعددة؟* | أنشئ نسخة منفصلة من `OcrEngine` لكل خيط؛ الفئة نفسها لا تضمن الأمان عبر الخيوط. |
| *كيف أتعامل مع مستندات متعددة اللغات؟* | اضبط `ocrEngine.Language = OcrLanguage.Multilingual` أو غيّر اللغة لكل صفحة. |

## نصائح لـ OCR جاهز للإنتاج

- **معالجة دفعات:** كرّر عبر مجلد من الصور، مع إعادة استخدام نفس نسخة `OcrEngine` لتقليل الحمل.
- **التسجيل:** احصل على `ocrEngine.LastError` عندما تُعيد `Recognize()` قيمة false؛ غالبًا ما يشير إلى تنسيقات غير مدعومة أو ملفات تالفة.
- **الأداء:** خطوة تصحيح الإمالة هي الأكثر استهلاكًا للمعالج. إذا كنت تعلم أن صورك مستوية بالفعل، يمكنك تخطي إضافة الفلتر.
- **إدارة الذاكرة:** حرّر كائنات `ImageStream` بعد الاستخدام (`ocrEngine.Image.Dispose()`) لتجنب تسرب الذاكرة في الخدمات طويلة الأمد.

## الخلاصة

لقد غطينا **how to deskew image**، **how to remove noise**، **how to load image for OCR**، و **how to extract text** باستخدام Aspose OCR في C#. من خلال ما قبل المعالجة باستخدام `DeskewFilter` و `DespeckleFilter`، تحسن بشكل كبير فرص أن تُعيد `Recognize()` سلاسل نصية نظيفة وقابلة للبحث.

من أول سطر كود إلى النتيجة النهائية المنقحة، الخطوات بسيطة، لكنها قوية بما يكفي للسيناريوهات الواقعية—سواء كنت تبني خدمة أرشفة مستندات، أو تطبيقًا محمولًا لمسح الفواتير، أو خلفية معالجة دفعات.

هل أنت مستعد للتحدي التالي؟ جرّب إضافة خطوة **language detection**، أو جرب **custom OCR dictionaries** لزيادة الدقة في المفردات الخاصة بالصناعات. السماء هي الحد، والآن لديك أساس قوي للبناء عليه.

برمجة سعيدة، ولتكن صورك دائمًا مستقيمة تمامًا!

![توضيح لمستند مصحح بعد تصحيح الإمالة](deskewed_example.png "كيفية تصحيح إمالة الصورة")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}