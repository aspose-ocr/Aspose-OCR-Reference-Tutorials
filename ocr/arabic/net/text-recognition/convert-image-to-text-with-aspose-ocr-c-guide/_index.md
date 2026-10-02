---
category: general
date: 2026-02-14
description: تحويل الصورة إلى نص باستخدام Aspose OCR في C#. تعلم كيفية استخراج النص
  العربي من صورة، تحميل الصورة للتعرف الضوئي على الأحرف، والتعرف على العربية بكفاءة.
draft: false
keywords:
- convert image to text
- extract text from picture
- how to extract arabic text
- load image for ocr
- how to recognize arabic
language: ar
og_description: تحويل الصورة إلى نص باستخدام Aspose OCR في C#. يوضح هذا الدرس كيفية
  استخراج النص العربي من صورة، تحميل الصورة للتعرف الضوئي على الأحرف، والتعرف على
  اللغة العربية.
og_title: تحويل الصورة إلى نص باستخدام Aspose OCR – دليل C#
tags:
- OCR
- C#
- Aspose
title: تحويل الصورة إلى نص باستخدام Aspose OCR – دليل C#
url: /ar/net/text-recognition/convert-image-to-text-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى نص باستخدام Aspose OCR – دليل C#

هل تريد **تحويل الصورة إلى نص** في تطبيق C#؟ تحويل الصورة إلى نص مهمة شائعة، خاصة عندما تحتاج إلى **استخراج النص من صورة** تحتوي على نصوص غير لاتينية. في هذا الدرس سنستعرض مثالًا كاملاً جاهزًا للتنفيذ يوضح **كيفية استخراج النص العربي**، وكيفية **تحميل الصورة للـ OCR**، والخطوات الدقيقة التي تحتاجها **لتعرف الأحرف العربية** باستخدام مكتبة Aspose.OCR.

سنتناول كل شيء بدءًا من تثبيت حزمة NuGet وحتى التعامل مع الحالات الخاصة مثل الخطوط المفقودة أو المسحات منخفضة الدقة. في النهاية ستحصل على برنامج مستقل يطبع السلسلة العربية التي تم التعرف عليها في وحدة التحكم—بدون الحاجة إلى أدوات خارجية.

## ما ستتعلمه

- كيفية إضافة Aspose.OCR إلى مشروع .NET (أحدث نسخة حتى عام 2026)
- الشيفرة الدقيقة اللازمة **لتحويل الصورة إلى نص** ولماذا كل سطر مهم
- نصائح لتحسين الدقة عند التعامل مع الحروف العربية
- كيفية **تحميل الصورة للـ OCR** من مسار ملف أو من تدفق بيانات
- طرق استكشاف الأخطاء الشائعة (مثل إعداد اللغة الخاطئ، أو تنسيق الصورة غير المدعوم)

> **نصيحة احترافية:** إذا كنت تستهدف .NET 6 أو أحدث، يمكنك استخدام العبارات ذات المستوى الأعلى لجعل الشيفرة أقصر. المثال أدناه يظل يستخدم فئة `Program` الكلاسيكية لأقصى توافق.

## المتطلبات المسبقة

- .NET 6 SDK (أو أي نسخة حديثة من .NET)
- Visual Studio 2022 أو VS Code مع امتداد C#
- حزمة NuGet `Aspose.OCR` (تثبيت عبر `dotdot add package Aspose.OCR`)
- ملف صورة يحتوي على نص عربي (مثال: `arabic_sign.jpg`)

---

## تحويل الصورة إلى نص – تنفيذ خطوة بخطوة

فيما يلي ملف المصدر الكامل الذي يمكنك نسخه‑لصقه في مشروع وحدة تحكم جديد. يحتوي على **جميع توجيهات `using` الضرورية**، ودالة `Main`، وتعليقات داخلية تشرح *السبب* وراء كل عملية.

```csharp
// ------------------------------------------------------------
// Program.cs – Complete example to convert image to text
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine – this object holds the core logic.
            var ocrEngine = new Engine();

            // 2️⃣ Configure OCR options.
            //    We set the language to Arabic because the picture contains Arabic script.
            //    You can replace Language.Arabic with any other supported language.
            var ocrOptions = new OcrOptions
            {
                Language = Language.Arabic
            };

            // 3️⃣ Load the image you want to process.
            //    ImageStream.FromFile reads the file into a stream that Aspose can handle.
            //    If your image is in a different folder, adjust the path accordingly.
            var inputImage = ImageStream.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");

            // 4️⃣ Run OCR – the Recognize method returns an OcrResult object.
            var ocrResult = ocrEngine.Recognize(inputImage, ocrOptions);

            // 5️⃣ Output the recognized text to the console.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### النتيجة المتوقعة

إذا كان `arabic_sign.jpg` يحتوي على العبارة **"مطار دولي"**، فستظهر وحدة التحكم شيئًا مثل:

```
=== OCR Result ===
مطار دولي
```

قد يختلف التهجئة الدقيقة قليلًا حسب جودة الصورة، لكن يجب أن ترى الأحرف العربية بدلاً من الرموز غير المفهومة.

---

## كيفية استخراج النص العربي – ضبط اللغة

لماذا نحدد صراحةً `Language = Language.Arabic`؟ تدعم Aspose.OCR عشرات اللغات، لكنها الافتراضية هي الإنجليزية. العربية تستخدم كتابة من اليمين إلى اليسار وتشكيل حروف يعتمد على السياق. بإخبار المحرك باللغة الصحيحة، ستحصل على:

- **اكتشاف الحروف المتصلة** – الأحرف التي تتصل معًا (مثل “لا”)
- **ترتيب من اليمين إلى اليسار** – السلسلة الناتجة ستكون موجهة بشكل صحيح
- **تحسين فحص القاموس** – يستطيع المحرك الرجوع إلى قوائم الكلمات العربية لزيادة الدقة

إذا احتجت **استخراج النص من صورة** تحتوي على لغات متعددة، يمكنك تمرير مصفوفة من تعداد `Language` إلى `OcrOptions.Language` (مثال: `new[] { Language.Arabic, Language.English }`).

---

## تحميل الصورة للـ OCR – قراءة الصورة

السطر `ImageStream.FromFile(...)` هو أبسط طريقة **لتحميل الصورة للـ OCR**. ومع ذلك، قد تواجه سيناريوهات حيث:

- الصورة مخزنة في BLOB بقاعدة البيانات.
- تستقبل الصورة عبر طلب HTTP.
- الملف بتنسيق غير قياسي (مثل TIFF متعدد الصفحات).

في هذه الحالات، يمكنك إنشاء `ImageStream` من `MemoryStream`:

```csharp
byte[] bytes = System.IO.File.ReadAllBytes("path/to/image.png");
using var memStream = new System.IO.MemoryStream(bytes);
var inputImage = ImageStream.FromStream(memStream);
```

كلا الطريقتين تزودان المحرك بنفس التمثيل الداخلي، لذا لا تتأثر جودة الـ OCR.

---

## كيفية التعرف على العربية – تشغيل المحرك

عند استدعاء `ocrEngine.Recognize(inputImage, ocrOptions)`, يقوم المحرك بعدة مراحل داخلية:

1. **ما قبل المعالجة** – تقليل الضوضاء، التحويل إلى ثنائي، وتصحيح الميل.
2. **التقسيم** – تقسيم الصورة إلى أسطر، كلمات، وحروف.
3. **التصنيف** – مطابقة كل جزء مع حروف عربية معروفة.
4. **ما بعد المعالجة** – تطبيق قواعد اللغة وعوامل الثقة.

إذا لاحظت انخفاضًا في درجات الثقة، ففكّر في:

- **زيادة دقة الصورة** (الحد الأدنى 300 dpi موصى به للعربية).
- **ضبط التباين** قبل تمرير الصورة (استخدم مكتبة معالجة صور بسيطة مثل `System.Drawing` أو `ImageSharp`).
- **تمكين `ocrOptions.UseLanguageDictionary = true`** لفحص القاموس بشكل أكثر صرامة.

---

## المشكلات الشائعة وكيفية تجنّبها

| العرض | السبب المحتمل | الحل |
|---------|--------------|-----|
| مخرجات فارغة | مسار الملف خاطئ أو تنسيق غير مدعوم | تحقق من المسار، استخدم `File.Exists`، وتأكد أن الصورة بصيغة PNG/JPEG/BMP |
| أحرف مشوشة | اللغة غير مضبوطة على العربية | عيّن `Language = Language.Arabic` في `OcrOptions` |
| دقة منخفضة | الصورة غير واضحة أو دقة منخفضة | استخدم مصدرًا بدقة أعلى أو طبّق مرشحات تحسين |
| استثناء `ArgumentNullException` | `inputImage` فارغ | تأكد من وجود الملف وأن الـ stream مفتوح بشكل صحيح |

---

## مثال كامل يعمل (نسخة جاهزة للنسخ)

إذا كنت تفضّل ملفًا واحدًا بدون مساحات أسماء، إليك نسخة مختصرة لا تزال تتبع أفضل الممارسات:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class ConvertImageToText
{
    static void Main()
    {
        // Engine creation
        var engine = new Engine();

        // Set OCR options – Arabic language
        var options = new OcrOptions { Language = Language.Arabic };

        // Load image – change the path to your actual file
        var image = ImageStream.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");

        // Perform recognition
        var result = engine.Recognize(image, options);

        // Show result
        Console.WriteLine("=== Recognized Arabic Text ===");
        Console.WriteLine(result.Text);
    }
}
```

شغّل البرنامج باستخدام `dotnet run` وسترى النص العربي يُطبع في وحدة التحكم.

---

## ملخص بصري

فيما يلي لقطة شاشة توضيحية تُظهر مخرجات وحدة التحكم. **النص البديل** يحتوي على الكلمة المفتاحية الأساسية للامتثال لتحسين محركات البحث.

![مثال تحويل الصورة إلى نص – وحدة التحكم تعرض نتيجة OCR العربية](convert-image-to-text-example.png)

---

## الخاتمة

لقد استعرضنا كيفية **تحويل الصورة إلى نص** باستخدام Aspose OCR في C#. شمل الدرس كل شيء من تثبيت المكتبة، ضبط اللغة لاستخراج النص العربي، تحميل الصورة، وأخيرًا **كيفية التعرف على الأحرف العربية** باستدعاء طريقة واحدة.

مع هذه المعرفة، يمكنك الآن دمج OCR في أي مشروع .NET—سواء كان أداة سطح مكتب، واجهة ويب API، أو خدمة خلفية تعالج دفعات من المستندات الممسوحة.

### ما التالي؟

- جرّب لغات أخرى بتغيير `Language.Arabic` إلى `Language.French` أو `Language.ChineseSimplified` وغيرها.
- دمج OCR مع خطوط **استخراج النص من صورة** التي تخزن النتائج في قاعدة بيانات.
- استخدم الخاصية `ocrResult.Confidence` لتصفية الأسطر ذات الثقة المنخفضة قبل حفظها.

هل لديك أسئلة حول حالات خاصة أو تحسين الأداء؟ اترك تعليقًا أو شارك في موضوع النقاش. برمجة سعيدة، ولتُنتج صورك دائمًا نصًا نظيفًا وقابلًا للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}