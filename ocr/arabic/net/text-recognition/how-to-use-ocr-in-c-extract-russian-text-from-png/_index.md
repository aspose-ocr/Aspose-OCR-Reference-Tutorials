---
category: general
date: 2026-02-20
description: كيفية استخدام OCR في C# لقراءة النص من صور PNG – تعلم تحويل الصورة إلى
  نص واستخراج النص الروسي بسرعة.
draft: false
keywords:
- how to use ocr
- read text from png
- convert image to text
- recognize image text
- extract russian text
language: ar
og_description: كيفية استخدام OCR في C# موضحة في الجملة الأولى – دليل خطوة بخطوة لقراءة
  النص من PNG، تحويل الصورة إلى نص، واستخراج النص الروسي.
og_title: كيفية استخدام OCR في C# – دليل شامل
tags:
- OCR
- C#
- Aspose
title: كيفية استخدام OCR في C# – استخراج النص الروسي من PNG
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-russian-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – استخراج النص الروسي من PNG

هل تساءلت يومًا **كيف تستخدم OCR** في مشروع .NET دون قضاء أسابيع في البحث عن المكتبة المناسبة؟ لست وحدك. في العديد من التطبيقات الواقعية نحتاج إلى **قراءة النص من ملفات PNG**، تحويل تلك الصور إلى سلاسل قابلة للبحث، وأحيانًا استخراج الأحرف السيريلية لمعالجة اللغة الروسية.

في هذا الدرس سنستعرض مثالًا عمليًا يوضح لك بالضبط **كيفية تحويل الصورة إلى نص** باستخدام Aspose.OCR، ثم **التعرف على نص الصورة** المكتوب بالروسية. بنهاية الدرس ستحصل على برنامج كونسول جاهز للتنفيذ **يستخرج النص الروسي** من ملف PNG، بالإضافة إلى مجموعة من النصائح للحالات الخاصة التي قد تواجهها لاحقًا.

---

## ما ستحتاجه

- .NET 6 SDK أو أحدث (الكود يعمل أيضًا على .NET Core 3.1+)  
- Visual Studio 2022 أو أي محرر تفضله (VS Code يعمل جيدًا)  
- حزمة **Aspose.OCR** من NuGet (`Install-Package Aspose.OCR`)  
- صورة PNG تجريبية تحتوي على أحرف روسية (سنسمّيها `sample_russian.png`)

هذا كل شيء—لا مكتبات DLL أصلية إضافية، لا خدمات خارجية، ولا ملفات إعدادات معقدة. جاهز؟ لنبدأ.

---

## الخطوة 1 – تهيئة محرك OCR (how to use ocr)

أول شيء عليك فعله عندما تريد **استخدام OCR** هو إنشاء كائن محرك. تقوم Aspose بالعمل الشاق نيابةً عنك، بما في ذلك تنزيل حزمة اللغة السيريلية في المرة الأولى التي تطلبها.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;

// Create the OCR engine – this also triggers a one‑time download of language data
OcrEngine ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:** المحرك يحتفظ بجميع الحالات الداخلية (مثل نماذج اللغة) ويوفر طريقة `Recognize` التي ستستدعيها لاحقًا. إنشاءه مرة واحدة وإعادة استخدامه عبر صور متعددة أكثر كفاءة من إنشاء كائن جديد لكل ملف.

---

## الخطوة 2 – تحميل صورة PNG (read text from png)

الآن بعد أن أصبح المحرك جاهزًا، تحتاج إلى صورة لتغذيتها. خطوة **قراءة النص من PNG** بسيطة، لكن هناك بعض النقاط التي يجب الانتباه لها:

1. **مسار الملف** – تأكد من أن المسار مطلق أو نسبي إلى دليل العمل للملف التنفيذي.  
2. **التصريف** – `Image` تُطبق `IDisposable`؛ لذا احرص على وضعها داخل كتلة `using` لتجنب تسرب الذاكرة.

```csharp
string imagePath = @"YOUR_DIRECTORY\sample_russian.png";

using (Image russianImage = Image.FromFile(imagePath))
{
    // The image is now loaded and will be disposed automatically
}
```

> **نصيحة احترافية:** إذا كنت تتعامل مع تدفقات (مثلاً ملفات تم رفعها)، استخدم `Image.FromStream(stream)` بدلاً من `FromFile`.

---

## الخطوة 3 – اختيار حزمة اللغة السيريلية (extract russian text)

تأتي Aspose مع العديد من حزم اللغات، لكن الافتراضية هي الإنجليزية. بما أن هدفنا هو **استخراج النص الروسي**، يجب أن نخبر المحرك صراحةً باستخدام نموذج اللغة السيريلية.

```csharp
ocrEngine.Language = Language.Cyrillic;   // Switches the OCR engine to Cyrillic
```

> **لماذا هذا ضروري:** بدون ضبط `Language.Cyrillic`، سيحاول المحرك تفسير الأحرف كحروف لاتينية، مما يؤدي إلى مخرجات مشوشة. قد تستغرق المكالمة الأولى بضع ثوانٍ أثناء تنزيل بيانات اللغة—بعد ذلك تُخزن محليًا في الذاكرة المؤقتة.

---

## الخطوة 4 – التعرف وتحويل الصورة إلى نص (convert image to text)

هذا هو جوهر الدرس: تحويل الصورة إلى سلسلة نصية عادية. طريقة `Recognize` تقوم بذلك بالضبط.

```csharp
using (Image russianImage = Image.FromFile(imagePath))
{
    // Perform OCR – this returns the detected text as a string
    string recognizedText = ocrEngine.Recognize(russianImage);

    // Show the result in the console
    Console.WriteLine("=== Recognized Russian Text ===");
    Console.WriteLine(recognizedText);
}
```

**الناتج المتوقع في الكونسول** (النص الفعلي سيختلف حسب محتوى PNG):

```
=== Recognized Russian Text ===
Привет, мир! Это пример текста на русском языке.
```

إذا رأيت علامات استفهام أو رموز عشوائية، تحقق من أن الصورة ذات دقة عالية وأنك ضبطت `Language.Cyrillic` بشكل صحيح.

---

## الخطوة 5 – عرض النص المتعرف عليه والتحقق منه (recognize image text)

في تطبيق حقيقي ربما تقوم بحفظ النتيجة في قاعدة بيانات، أو تمريرها إلى فهرس بحث، أو إرساله إلى واجهة برمجة تطبيقات ترجمة. لهذا الدرس، يكفي `Console.WriteLine` لإثبات أننا نستطيع **التعرف على نص الصورة** بثقة.

```csharp
Console.WriteLine("\nDone! The OCR engine has extracted the Russian text.");
```

> **حالة خاصة:** إذا كانت PNG لا تحتوي على نص (أو النص غير واضح)، فإن `Recognize` تُعيد سلسلة فارغة. احرص دائمًا على التحقق من ذلك:

```csharp
if (string.IsNullOrWhiteSpace(recognizedText))
{
    Console.WriteLine("No readable text found – try a clearer image or adjust DPI.");
}
```

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في مشروع كونسول جديد (`dotnet new console`). يتضمن جميع توجيهات `using`، التصريف الصحيح، وقليل من معالجة الأخطاء.

```csharp
// ------------------------------------------------------------
// Full OCR example – extract Russian text from a PNG file
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine (downloads Cyrillic pack on first run)
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Path to the PNG that contains Russian text
        string imagePath = @"YOUR_DIRECTORY\sample_russian.png";

        // 3️⃣ Tell the engine to use Cyrillic (necessary for Russian)
        ocrEngine.Language = Language.Cyrillic;

        // 4️⃣ Load the image and run OCR
        using (Image russianImage = Image.FromFile(imagePath))
        {
            string recognizedText = ocrEngine.Recognize(russianImage);

            // 5️⃣ Output the result
            Console.WriteLine("=== Recognized Russian Text ===");
            Console.WriteLine(recognizedText);

            // Simple validation
            if (string.IsNullOrWhiteSpace(recognizedText))
            {
                Console.WriteLine("\n⚠️ No text detected – check image quality or language settings.");
            }
            else
            {
                Console.WriteLine("\n✅ OCR succeeded!");
            }
        }
    }
}
```

احفظ الملف، شغّل `dotnet run`، وشاهد الكونسول يطبع الجملة الروسية المدمجة في PNG الخاص بك. 🎉

---

## نصائح عملية ومشكلات شائعة

| الحالة | ما يجب فعله |
|-----------|------------|
| **الصورة منخفضة الدقة** | زد الـ DPI قبل OCR (`new Bitmap(image, new Size(width*2, height*2))`). |
| **النص مائل** | استخدم `ocrEngine.RotateImage` أو عالج مسبقًا باستخدام `System.Drawing` لتصحيح الميل. |
| **عدة لغات في صورة واحدة** | اضبط `ocrEngine.Language = Language.Cyrillic \| Language.English;` لتمكين الكشف المختلط. |
| **دفعة كبيرة من الملفات** | أعد استخدام كائن `OcrEngine` واحد؛ فقط كائنات `Image` تحتاج إلى تصريف في كل دورة. |
| **التشغيل على لينكس** | تأكد من تثبيت `libgdiplus` (`apt-get install -y libgdiplus`) لأن `System.Drawing.Common` يعتمد عليه. |

---

## ملخص بصري

![كيفية استخدام OCR في C# – مخرجات الكونسول تظهر النص الروسي المستخرج](ocr_console_output.png "كيفية استخدام OCR في C# – مثال على المخرجات")

*الصورة أعلاه توضح نافذة الكونسول بعد انتهاء البرنامج، مؤكدةً أننا نجحنا في **قراءة النص من PNG** و**تحويل الصورة إلى نص**.*

---

## الخلاصة

غطّينا **كيفية استخدام OCR** في C# من البداية حتى النهاية: تهيئة المحرك، تحميل PNG، التحويل إلى حزمة اللغة السيريلية، إجراء التعرف، وأخيرًا عرض الجملة الروسية المستخرجة. البرنامج الصغير يوضح سير عمل **تحويل الصورة إلى نص** بالكامل ويظهر لك كيف **تتعرف على نص الصورة** بثبات.

ما الخطوات التالية؟  
- جرّب استخراج النص من ملفات PDF متعددة الصفحات (Aspose.OCR يدعم ذلك أيضًا).  
- جرب حزم لغات أخرى (`Language.Arabic`, `Language.ChineseSimplified`, إلخ).  
- اربط الناتج بخدمة ترجمة أو فهرس بحث لتجعل تطبيقك متعدد اللغات فعليًا.

هل لديك أسئلة حول معالجة المسحات الضوضائية أو دمج OCR في واجهة برمجة تطبيقات ويب؟ اترك تعليقًا، ونتمنى لك برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}