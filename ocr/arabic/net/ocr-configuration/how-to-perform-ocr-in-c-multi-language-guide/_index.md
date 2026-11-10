---
category: general
date: 2026-04-29
description: كيفية تنفيذ OCR في C# باستخدام Aspose OCR – استخراج النص الهندي، التعرف
  على النص من PNG، وتغيير لغة OCR في الوقت الفعلي.
draft: false
keywords:
- how to perform OCR
- extract Hindi text
- multi language OCR
- recognize text from PNG
- change OCR language
language: ar
og_description: كيفية تنفيذ OCR في C# باستخدام Aspose OCR. تعلم استخراج النص الهندي،
  التعرف على النص من ملفات PNG، وتغيير لغة OCR ديناميكيًا.
og_title: كيفية تنفيذ OCR في C# – دليل شامل متعدد اللغات
tags:
- OCR
- C#
- Aspose
title: كيفية تنفيذ OCR في C# – دليل متعدد اللغات
url: /ar/net/ocr-configuration/how-to-perform-ocr-in-c-multi-language-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في C# – دليل متعدد اللغات

هل تساءلت يومًا **كيف تقوم بتنفيذ OCR** على صور تحتوي على أكثر من لغة؟ ربما لديك إيصال روسي وكتيب هندي جنبًا إلى جنب، وتحتاج إلى النص من كليهما دون الحاجة إلى أدوات منفصلة. هذه مشكلة شائعة لأي شخص يتعامل مع مستندات دولية.  

في هذا الدرس سنعرض لك طريقة نظيفة وشاملة **لأداء OCR** باستخدام Aspose OCR، استخراج النص الهندي، التعرف على النص من ملفات PNG، وحتى **تغيير لغة OCR** أثناء التشغيل. في النهاية ستحصل على مقطع شفرة قابل لإعادة الاستخدام يعمل مع أي تركيبة من اللغات المدعومة.

## ما ستتعلمه

- كيفية إعداد محرك Aspose OCR في مشروع .NET.  
- الفرق بين تكوين لغة ثابتة وتبديل اللغات أثناء وقت التشغيل.  
- كيفية استخراج النص الهندي من صورة ولماذا يمكن للمكتبة تنزيل حزم اللغات تلقائيًا.  
- نصائح للتعامل مع ملفات PNG، ومعالجة وحدات اللغة المفقودة، وحل المشكلات الشائعة.

> **نصيحة احترافية:** إذا كنت تستخدم Aspose OCR بالفعل للغة واحدة، فكل ما عليك هو تعديل سطرين أو ثلاثة لتحويل هذا إلى حل **OCR متعدد اللغات**.

---

## المتطلبات المسبقة

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 or later (or .NET Framework 4.7+) | Aspose OCR يستهدف بيئات تشغيل حديثة؛ قد تفتقد الإصدارات القديمة دعم التنزيل التلقائي لحزم اللغات. |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | يوفر فئة `OcrEngine` وتعدادات اللغات. |
| Two sample PNG images (`russian.png` and `hindi.png`) placed in a known folder | يوضح **التعرف على النص من PNG** و**استخراج النص الهندي** في تشغيل واحد. |
| Internet connection (for the first time you request a new language) | المكتبة تقوم بسحب وحدة اللغة المطلوبة عند الطلب. |

لا تحتاج إلى أي ملفات تنفيذية إضافية لـ OCR أو أدوات خارجية—Aspose يتولى كل العمل الشاق.

---

## الخطوة 1 – تثبيت Aspose OCR وإنشاء المحرك

أولًا: أضف حزمة Aspose OCR إلى مشروعك. افتح وحدة تحكم مدير الحزم (Package Manager Console) وشغّل:

```powershell
Install-Package Aspose.OCR
```

الآن يمكننا إنشاء مثيل `OcrEngine`. فكر في المحرك كماسح ذكي يمكن إعادة تكوينه أثناء وقت التشغيل.

```csharp
using Aspose.OCR;
using System;

class MultiLanguageOcrDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

لماذا ننشئ المحرك مرة واحدة فقط؟ إعادة استخدام نفس المثيل يتجنب العبء الناتج عن تحميل مكتبات OCR الأصلية بشكل متكرر، وهو ما قد يكون ملحوظًا عند معالجة دفعات كبيرة.

---

## الخطوة 2 – التعرف على النص الروسي (اللغة الأولى)

قبل الانتقال إلى الهندية، دعنا نثبت أن المحرك يعمل مع لغة معروفة. نحدد اللغة إلى الروسية، نمرر ملف PNG، ونطبع النتيجة.

```csharp
        // Step 2: Configure the engine for Russian and recognize the image
        ocrEngine.Config.Language = OcrLanguage.Russian;
        var russianImagePath = @"YOUR_DIRECTORY/russian.png";
        var russianOcrResult = ocrEngine.Recognize(OcrEngine.LoadImage(russianImagePath));
        Console.WriteLine("Russian: " + russianOcrResult.Text);
```

**ما الذي يحدث في الخلفية؟**  
`OcrEngine.LoadImage` يقرأ ملف PNG إلى تنسيق bitmap الداخلي في Aspose. خاصية `Config.Language` تخبر محرك OCR أي قاموس ومجموعة أحرف يجب تطبيقها. عند استدعاء `Recognize`، يقوم المحرك بتشغيل نموذج شبكة عصبية مُضبط على الأحرف السيريالية ويعيد كائن `OcrResult` يحتوي على النص العادي.

> **الناتج المتوقع (مثال)**  
> `Russian: Привет, мир! Это тестовое изображение.`

إذا رأيت أحرفًا مشوشة، تحقق مرة أخرى من أن الصورة غير تالفة وأن وحدة اللغة الروسية موجودة (تأتي مع الحزمة الأساسية).

---

## الخطوة 3 – التحويل إلى الهندية – **تغيير لغة OCR** ديناميكيًا

الآن للجزء الممتع: تبديل اللغة دون إعادة إنشاء المحرك. Aspose OCR سيقوم بتنزيل وحدة اللغة الهندية في المرة الأولى التي تطلبها فيها، لذا تحتاج إلى اتصال إنترنت مرة واحدة فقط.

```csharp
        // Step 3: Switch the engine to Hindi (the language module will be downloaded automatically) and recognize the image
        ocrEngine.Config.Language = OcrLanguage.Hindi;
        var hindiImagePath = @"YOUR_DIRECTORY/hindi.png";
        var hindiOcrResult = ocrEngine.Recognize(OcrEngine.LoadImage(hindiImagePath));
        Console.WriteLine("Hindi: " + hindiOcrResult.Text);
    }
}
```

**لماذا يعمل هذا؟**  
مُحدد `Config.Language` يُفعل روتين التحميل الكسول. إذا لم تكن حزمة اللغة المطلوبة موجودة على القرص، يتواصل Aspose مع شبكة CDN الخاصة به، يُحمّل الوحدة المضغوطة، يُخزنها مؤقتًا، ثم يواصل عملية التعرف. يتيح لك هذا التصميم بناء خطوط معالجة **OCR متعدد اللغات** تتكيف مع المحتوى أثناء وقت التشغيل.

> **نموذج ناتج الهندية**  
> `Hindi: नमस्ते दुनिया! यह एक परीक्षण छवि है।`

لاحظ كيف يتعامل نفس كائن `ocrEngine` مع كل من النص السيريالي وخط الديفاناغاري بسلاسة. هذه هي قوة **تغيير لغة OCR** أثناء التشغيل.

---

## الخطوة 4 – التعامل مع ملفات PNG بكفاءة

كلا المثالين أعلاه يستخدمان صور PNG، وهو تنسيق شائع للقطات الشاشة والوثائق الممسوحة. PNG غير مضغوط، مما يعني أن بيانات البكسل تبقى نقية—مثالية لـ OCR. ومع ذلك، قد تستهلك ملفات PNG الكبيرة الذاكرة. إليك بعض النصائح السريعة:

1. **إعادة التحجيم إذا لزم الأمر** – إذا تجاوز عرض الصورة 2000 px، قلل حجمها باستخدام `System.Drawing.Image` قبل تمريره إلى Aspose.  
2. **تعيين DPI** – بعض محركات OCR تستفيد من DPI بقيمة 300. يمكنك تضمينه عبر نسخة `OcrEngine.LoadImage` التي تقبل `Bitmap` بدقة مخصصة.

```csharp
using System.Drawing;

// Example of downscaling a huge PNG
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/large.png");
int maxWidth = 2000;
if (original.Width > maxWidth)
{
    int newHeight = (int)((double)original.Height / original.Width * maxWidth);
    Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));
    original.Dispose(); // free original memory
    original = resized;
}
var result = ocrEngine.Recognize(OcrEngine.LoadImage(original));
```

هذه التعديلات تحافظ على انخفاض استهلاك الذاكرة وغالبًا ما تحسن الدقة لأن محرك OCR يعمل على شبكة بكسلات أكثر قابلية للإدارة.

---

## الخطوة 5 – تجميع كل شيء معًا – مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ والذي يوضح **كيفية تنفيذ OCR**، **استخراج النص الهندي**، **التعرف على النص من PNG**، و**تغيير لغة OCR** دون إعادة تشغيل المحرك.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class MultiLanguageOcrDemo
{
    static void Main()
    {
        // Create a single OCR engine instance (re‑use it for all languages)
        var ocrEngine = new OcrEngine();

        // ----------- Russian ----------
        ocrEngine.Config.Language = OcrLanguage.Russian;
        var russianPath = @"YOUR_DIRECTORY/russian.png";
        var russianResult = ocrEngine.Recognize(OcrEngine.LoadImage(russianPath));
        Console.WriteLine("Russian: " + russianResult.Text);

        // ----------- Hindi ------------
        // The first time this runs, the Hindi language pack will be downloaded automatically.
        ocrEngine.Config.Language = OcrLanguage.Hindi;
        var hindiPath = @"YOUR_DIRECTORY/hindi.png";
        var hindiResult = ocrEngine.Recognize(OcrEngine.LoadImage(hindiPath));
        Console.WriteLine("Hindi: " + hindiResult.Text);

        // ----------- Optional PNG optimization ----------
        // If you have very large PNGs, resize them before recognition (example shown earlier).
        // This block is optional and can be removed if your images are already sized appropriately.
    }
}
```

**تشغيل الكود** يطبع شيئًا مثل:

```
Russian: Привет, мир! Это тестовое изображение.
Hindi: नमस्ते दुनिया! यह एक परीक्षण छवि है।
```

إذا رأيت هذه السطور، مبروك—لقد نجحت في بناء حل **OCR متعدد اللغات** يمكنه **استخراج النص الهندي** و**التعرف على النص من ملفات PNG** باستخدام محرك واحد.

---

## الأسئلة المتكررة (FAQ)

| Question | Answer |
|----------|--------|
| *هل أحتاج إلى ترخيص لـ Aspose OCR؟* | مفتاح تقييم مجاني يعمل للاختبار، لكن الاستخدام في الإنتاج يتطلب ترخيصًا تجاريًا. |
| *هل يمكنني التعرف على أكثر من لغتين في صورة واحدة؟* | نعم. اضبط `Config.Language` إلى `OcrLanguage.Multiple` ومرّر قائمة مفصولة بفواصل (مثال: `Russian, Hindi`). |
| *ماذا لو فشل تحميل وحدة اللغة؟* | تحقق من إعدادات جدار الحماية أو الوكيل. يمكنك أيضًا تنزيل الوحدات مسبقًا من بوابة Aspose ووضعها في مجلد `Data`. |
| *هل PNG هو التنسيق الوحيد المدعوم؟* | لا. Aspose OCR يدعم أيضًا JPEG و BMP و TIFF و PDF (كصور). PNG مجرد خيار شائع للجودة غير المضغوطة. |

---

## الخطوات التالية والمواضيع ذات الصلة

- **معالجة دفعات** – تكرار عبر مجلد من ملفات PNG وتخزين النتائج في ملف CSV.  
- **استخراج PDF** – استخدم `OcrEngine.RecognizePdf` لاستخراج النص من ملفات PDF الممسوحة.  
- **قواميس مخصصة** – توسيع حزم اللغات المدمجة بقوائم كلمات يقدمها المستخدم لتناسب مفردات خاصة بالمجال.  
- **تحسين الأداء** – تنفيذ المكالمات بشكل متوازي باستخدام `Parallel.ForEach` عند العمل مع مجموعات صور كبيرة.  

استكشاف هذه المجالات سيعمق إتقانك لـ **كيفية تنفيذ OCR** عبر سيناريوهات متنوعة.

---

## الخلاصة

لقد تعلمت الآن **كيفية تنفيذ OCR** في C# باستخدام Aspose OCR، وتبديل اللغات أثناء التشغيل، واستخراج **النص الهندي** بنجاح من صورة PNG. الفكرة الأساسية هي أن مثيلًا واحدًا من `OcrEngine` يمكن أن يكون محركًا متعدد الاستخدامات و**OCR متعدد اللغات**—فقط اضبط `Config.Language` ودع المكتبة تتولى الباقي.

جرّب الكود، استبدل الصور النموذجية بأخرى خاصة بك، وجرب لغات إضافية. مرونة Aspose OCR تعني أنك تستطيع الانتقال من نموذج أولي سريع إلى خط معالجة مستندات جاهز للإنتاج مع تغييرات قليلة.

برمجة سعيدة، ولتكن مغامرات استخراج النص خالية من الأخطاء!

![how to perform OCR example](/images/ocr-demo.png "how to perform OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}