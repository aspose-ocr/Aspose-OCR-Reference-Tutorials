---
category: general
date: 2026-01-06
description: التعرف على النص متعدد اللغات في C# باستخدام Aspose OCR – تعلم كيفية استخراج
  النص من الصورة، تحميل الصورة للتعرف الضوئي على الأحرف، والتعرف على الأحرف السيريالية.
draft: false
keywords:
- multilingual text recognition
- extract text from image
- load image for OCR
- run OCR recognition
- recognize Cyrillic characters
language: ar
og_description: التعرف على النص متعدد اللغات في C# باستخدام Aspose OCR. تعلم خطوة
  بخطوة كيفية استخراج النص من الصورة، تحميل الصورة للتعرف الضوئي على الأحرف، تشغيل
  التعرف الضوئي على الأحرف، والتعرف على الأحرف السيريالية.
og_title: التعرف على النص متعدد اللغات في C# – دليل Aspose OCR الكامل
tags:
- Aspose OCR
- C#
- Image Processing
title: التعرف على النص متعدد اللغات في C# باستخدام Aspose OCR – دليل كامل
url: /ar/net/text-recognition/multilingual-text-recognition-in-c-with-aspose-ocr-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص متعدد اللغات في C# باستخدام Aspose OCR – دليل كامل

هل احتجت يومًا إلى **multilingual text recognition** في تطبيق .NET لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—المطورون يسألون باستمرار عن كيفية *extract text from image* التي تحتوي على كل من النص اللاتيني والسيريلي. في هذا الدرس سنستعرض حلًا عمليًا باستخدام Aspose OCR، يغطي كل شيء من **load image for OCR** إلى **run OCR recognition** وأخيرًا **recognize Cyrillic characters** بشكل موثوق.

سنركز على الجانب العملي: عينة كود واحدة قابلة للتنفيذ، شروحات *لماذا* كل سطر مهم، ونصائح لسيناريوهات العالم الحقيقي مثل الملفات الكبيرة أو محدودية عرض النطاق الترددي. بنهاية الدرس ستحصل على مقطع شفرة مستقل يمكنك إدراجه في أي مشروع C# والبدء في استخراج النص متعدد اللغات فورًا.

---

## ما يغطيه هذا الدرس

- إعداد محرك Aspose OCR للغات English + Cyrillic.  
- تحميل صورة من القرص (أو من تدفق) بطريقة تعمل مع كل من حاويات Windows وLinux.  
- تنفيذ **run OCR recognition** ومعالجة النجاح أو الفشل برشاقة.  
- ما بعد المعالجة للنتيجة لتقوم بـ *extract text from image* بشكل نظيف، بما في ذلك فواصل الأسطر وإزالة الفراغات.  
- المشكلات الشائعة عند محاولة **recognize Cyrillic characters** وكيفية تجنبها.  

بدون خدمات خارجية، بدون ملفات تكوين مخفية—فقط شفرة C# صافية وحزمة Aspose OCR NuGet.

---

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يُترجم على .NET Core و .NET Framework أيضًا).  
- Visual Studio 2022 أو أي محرر تفضله.  
- رخصة Aspose OCR (أو يمكنك التشغيل في وضع التجربة؛ المكتبة ستطلب مفتاح الترخيص).  
- صورة نموذجية تحتوي على كل من النص الإنجليزي والسيريلي (سنطلق عليها `multilingual.png`).  

إذا كنت تفتقد أيًا من هذه المتطلبات، احصل على حزمة Aspose OCR NuGet الآن:

```bash
dotnet add package Aspose.OCR
```

هذا كل شيء—لا توجد تبعيات أخرى مطلوبة.

---

## التعرف على النص متعدد اللغات – تهيئة المحرك

أول شيء تحتاجه هو نسخة من `OcrEngine`. فكر فيها كالعقل الذي سيفسر البكسلات في صورتك. إن إنشاؤها سهل، لكن يجب أن تكون على علم بالإعدادات الافتراضية: يبدأ المحرك بدون حزم لغات محملة، مما يعني أن المرة الأولى التي تطلب فيها منه التعرف على لغة سيقوم بتحميل الموارد المطلوبة تلقائيًا.

```csharp
using Aspose.OCR;
using System;

// Create the OCR engine – this object holds all configuration.
OcrEngine ocrEngine = new OcrEngine();

// OPTIONAL: Set a timeout for language‑pack downloads (seconds).
ocrEngine.ResourceDownloadTimeout = 60; // 1 minute; adjust for slow networks.
```

> **نصيحة احترافية:** إذا كنت تعلم أن بيئة النشر الخاصة بك لن تتوفر فيها اتصال بالإنترنت، قم بتحميل حزم اللغات مسبقًا على جهاز التطوير وضمّها مع تطبيقك. عندها سيصبح `ResourceDownloadTimeout` غير مهم.

---

## تحميل صورة للـ OCR وتحديد اللغات

الآن نخبر المحرك *ماذا* يقرأ. خاصية `Image` تقبل `ImageStream`، والتي يمكن إنشاؤها من مسار ملف، أو مصفوفة بايت، أو حتى تدفق شبكة. استخدام `ImageStream.FromFile` هو أبسط طريقة لعرض محلي.

```csharp
// Point to the image that contains both English and Cyrillic text.
string imagePath = @"YOUR_DIRECTORY/multilingual.png";
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

بعد ذلك، فعّل اللغات التي تحتاجها. يستخدم Aspose OCR تعدادًا بنظام القناع الثنائي (`OcrLanguage`) بحيث يمكنك دمج عدة حزم باستخدام العامل `|`.

```csharp
// Enable English and Cyrillic language packs.
// The first call will trigger an automatic download if the packs are missing.
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

> **لماذا هذا مهم:** إذا فعلت الإنجليزية فقط، ستظهر الأحرف السيريليّة كرموز مشوشة أو تُحذف تمامًا. بإضافة `OcrLanguage.Cyrillic` صراحةً تضمن أن المحرك يحمل النماذج العصبية اللازمة للتعرف الدقيق.

---

## تنفيذ التعرف على OCR ومعالجة النتائج

مع تحميل الصورة وتحديد اللغات، يمكنك أخيرًا طلب من المحرك تنفيذ مهمته. طريقة `Recognize()` تُعيد قيمة Boolean تُشير إلى النجاح، والنص المُتعرف عليه يُخزن في خاصية `Text`.

```csharp
if (ocrEngine.Recognize())
{
    // Success! Grab the recognized string.
    string recognizedText = ocrEngine.Text;

    // OPTIONAL: Clean up line breaks and extra whitespace.
    string cleaned = recognizedText
        .Replace("\r\n", "\n")   // Normalize Windows line endings.
        .Trim();                // Remove leading/trailing spaces.

    Console.WriteLine("=== Recognized Multilingual Text ===");
    Console.WriteLine(cleaned);
}
else
{
    // Something went wrong – print the error for debugging.
    Console.WriteLine($"Recognition failed: {ocrEngine.ErrorMessage}");
}
```

### النتيجة المتوقعة

إذا كانت `multilingual.png` تحتوي على الجملة:

> "Hello мир! This is a test."

يجب أن ترى:

```
=== Recognized Multilingual Text ===
Hello мир! This is a test.
```

لاحظ كيف تظهر كلمة **мир** السيريليّة بشكل صحيح إلى جانب النص الإنجليزي—هذا هو قوة الدعم المتعدد اللغات الصحيح.

---

## استخراج النص من الصورة – نصائح ما بعد المعالجة

حتى بعد تشغيل ناجح، قد تحتاج إلى تنقية الناتج الخام قبل استخدامه لاحقًا:

| المشكلة | الحل |
|-------|----------|
| **فواصل أسطر زائدة** | استخدم `String.Replace("\r\n", "\n")` ثم قسّم على `\n` فقط حيث يلزم. |
| **مسافات زائدة في النهاية** | استدعِ `.Trim()` على كل سطر أو على السلسلة بأكملها. |
| **تباينات حالة الأحرف** | طبق `.ToUpperInvariant()` أو `.ToLowerInvariant()` إذا كان منطقك اللاحق حساسًا لحالة الأحرف. |
| **حروف غير قابلة للطباعة** | قم بالترشيح باستخدام `char.IsControl(c) ? ' ' : c`. |

تحول هذه الخطوات مخرجات OCR الخام إلى نص نظيف وقابل للبحث—مثالي للفهرسة أو لتغذيته إلى واجهة برمجة تطبيقات الترجمة.

---

## التعرف على الأحرف السيريليّة – المشكلات الشائعة

عند التعامل مع السيريليّة، يواجه المطورون غالبًا مشكلتين خفيتين:

1. **Missing language pack** – إذا نسيت تضمين `OcrLanguage.Cyrillic`، سيعود المحرك إلى النموذج الافتراضي (Latin) وينتج `????` أو سلاسل فارغة. تأكد دائمًا من قناع اللغة قبل استدعاء `Recognize()`.
2. **Incorrect image DPI** – دقة OCR تنخفض بشكل كبير تحت 150 dpi. إذا كانت صورتك المصدر لقط شاشة أو PDF ممسوح، فكر في إعادة تحجيمها:

```csharp
// Example: upscale a low‑dpi image before OCR.
using (var bitmap = new Bitmap(imagePath))
{
    var highRes = new Bitmap(bitmap, new Size(bitmap.Width * 2, bitmap.Height * 2));
    ocrEngine.Image = ImageStream.FromBitmap(highRes);
}
```

إعادة التحجيم تضيف عبءً حسابيًا لكن غالبًا ما تعطي تحسينًا ملحوظًا في التعرف على الحروف السيريليّة.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ والذي يدمج كل ما ناقشنا. فقط استبدل `YOUR_DIRECTORY` بالمجلد الفعلي الذي يحتوي على `multilingual.png`.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine with a reasonable download timeout.
        OcrEngine ocrEngine = new OcrEngine
        {
            ResourceDownloadTimeout = 60 // seconds
        };

        // 2️⃣ Load the image – you can also use a MemoryStream here.
        string imagePath = @"YOUR_DIRECTORY/multilingual.png";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Enable English and Cyrillic language packs.
        ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;

        // 4️⃣ Run recognition.
        if (ocrEngine.Recognize())
        {
            // 5️⃣ Retrieve and clean the text.
            string raw = ocrEngine.Text;
            string cleaned = raw
                .Replace("\r\n", "\n")
                .Trim();

            Console.WriteLine("=== Recognized Multilingual Text ===");
            Console.WriteLine(cleaned);
        }
        else
        {
            // 6️⃣ Handle errors gracefully.
            Console.WriteLine($"Recognition failed: {ocrEngine.ErrorMessage}");
        }
    }
}
```

احفظ الملف باسم `Program.cs`، ثم ابنِه وشغّله. إذا تم إعداد كل شيء بشكل صحيح، سترى المحتوى متعدد اللغات يُطبع على وحدة التحكم.

---

## الخلاصة

لقد غطينا **multilingual text recognition** من البداية إلى النهاية: تهيئة محرك Aspose OCR، **load image for OCR**، تمكين English + Cyrillic، **run OCR recognition**، وأخيرًا **extract text from image** مع معالجة الحالات الحدية. باتباع هذا الدليل يمكنك بشكل موثوق **recognize Cyrillic characters** إلى جانب النص اللاتيني، مما يفتح الباب أمام معالجة المستندات عالميًا، وإدخال البيانات تلقائيًا، والمزيد.

ما التالي؟ جرّب تغيير قناع اللغة لتضمين حزم إضافية مثل `OcrLanguage.Greek` أو `OcrLanguage.Arabic`. جرب المعالجة الدفعية—تكرار عبر مجلد من الصور وكتابة كل نتيجة إلى ملف CSV. وإذا واجهت أي صعوبات، فإن منتديات مجتمع Aspose مكان رائع لطرح الأسئلة.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالبلور!

![مخطط يوضح تدفق التعرف على النص متعدد اللغات – تحميل الصورة، تحديد اللغات، تشغيل OCR، الحصول على النص](/images/multilingual-ocr-flow.png "مخطط تدفق التعرف على النص متعدد اللغات")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}