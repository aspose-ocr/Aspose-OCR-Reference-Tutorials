---
category: general
date: 2026-04-01
description: دروس C# OCR تُظهر كيفية استخراج النص العربي، ومعالجة الصورة مسبقًا للتعرف
  الضوئي على الأحرف، والتعرف على النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة.
draft: false
keywords:
- c# ocr tutorial
- extract arabic text
- preprocess image for ocr
- recognize text from image
- aspose ocr c# example
language: ar
og_description: دليل C# OCR يشرح لك استخراج النص العربي، ومعالجة الصورة مسبقًا، والتعرف
  على النص من الصورة باستخدام Aspose OCR في C#.
og_title: دورة OCR بلغة C# – استخراج النص العربي باستخدام Aspose OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: دليل OCR بلغة C# – استخراج النص العربي باستخدام Aspose OCR
url: /ar/net/text-recognition/c-ocr-tutorial-extract-arabic-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# OCR – استخراج النص العربي باستخدام Aspose OCR

هل احتجت يومًا إلى **c# ocr tutorial** ينجح فعلاً في استخراج العلامات العربية من صورة دون أن يسبب لك صداعًا؟ لست وحدك. في كثير من المشاريع العائق الأكبر ليس المكتبة—بل الحصول على صورة نظيفة بما يكفي لتتمكن المحرك من قراءة النص من اليمين إلى اليسار. يقدم هذا الدليل حلاً جاهزًا للتنفيذ، يوضح لماذا كل إعداد مهم، ويظهر لك كيفية **extract arabic text** بشكل موثوق.

سنمرّ عبر تثبيت حزمة Aspose OCR، ومعالجة الصورة مسبقًا لزيادة الدقة، وأخيرًا **recognize text from image**. في النهاية ستحصل على برنامج مستقل يطبع الأحرف العربية في وحدة التحكم، وستفهم المقايضات وراء كل خيار. لا حاجة إلى وثائق خارجية—كل ما تحتاجه هنا.

## ما ستحتاجه

- **.NET 6.0** (أو أي نسخة من .NET Core / .NET Framework تدعم NuGet)
- Visual Studio 2022 أو VS Code مع امتداد C#
- صورة تحتوي على نص عربي (مثال: `arabic_sign.jpg`)
- ترخيص Aspose OCR فعال (إصدار تجريبي مجاني يكفي للتطوير)

إذا كان لديك كل ذلك، يمكننا القفز مباشرة إلى الكود.

## الخطوة 1 – تثبيت Aspose OCR لـ .NET  

الخطوة الأولى هي سحب المكتبة من NuGet. افتح الطرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

أو، إذا كنت تفضّل واجهة Visual Studio، انقر بزر الماوس الأيمن على **Dependencies → Manage NuGet Packages**، ابحث عن **Aspose.OCR**، ثم اضغط **Install**. سيضيف ذلك تجميع `Aspose.OCR` وجميع تبعياته المتسلسلة.

> **نصيحة احترافية:** استخدم أحدث نسخة ثابتة (حتى أبريل 2026 هي 23.9). الإصدارات الجديدة غالبًا ما تحتوي على تحسينات خاصة باللغات العربية.

## الخطوة 2 – معالجة الصورة مسبقًا للـ OCR  

الخط العربي حساس للانحراف والضوضاء. صورة نظيفة يمكن أن ترفع معدل التعرف من 70 % إلى أكثر من 95 %. يأتي Aspose OCR مع كائن `PreprocessOptions` يتيح لك تشغيل **auto‑deskew** وإزالة الضوضاء.

```csharp
using Aspose.OCR;
using System;

class ArabicDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine and tell it we’re dealing with Arabic
        OcrEngine ocrEngine = new OcrEngine { Language = Language.Arabic };

        // 2️⃣ Turn on preprocessing – auto‑deskew + low‑level denoise
        ocrEngine.PreprocessOptions = new PreprocessOptions
        {
            AutoDeskew = true,                // Straightens rotated text
            DenoiseLevel = DenoiseLevel.Low   // Removes speckles without blurring characters
        };
```

**لماذا هذا مهم:**  
- **AutoDeskew**: كثير من اللقطات تكون مائلة بضع درجات. يكتشف الخوارزم خط أساس النص ويُدوّر البت ماب، مما يمنع الـ OCR من قراءة الأحرف بشكل خاطئ كشرطات أو نقاط.  
- **Low Denoise**: تحتوي الحروف العربية على الكثير من النقاط؛ إزالة الضوضاء بقوة قد تمحوها، فتتحول “ب” إلى “ن”. إعداد `Low` يوازن بين النظافة والدقة.

إذا كنت تتعامل مع مسح ضوئي شديد الضوضاء، يمكنك رفع `DenoiseLevel` إلى `Medium` أو `High`، لكن راقب الناتج—الإزالة الزائدة قد تمحو العلامات التشكيلية.

## الخطوة 3 – التعرف على النص العربي من الصورة  

الآن نمرّر الصورة المعالجة إلى المحرك. تُعيد طريقة `Recognize` كائن `OcrResult` يحتوي على السلسلة المستخرجة ودرجات الثقة.

```csharp
        // 3️⃣ Run OCR on the target image file
        // Replace the path with the actual location of your Arabic sign picture
        string imagePath = @"YOUR_DIRECTORY/arabic_sign.jpg";
        OcrResult ocrResult = ocrEngine.Recognize(imagePath);
```

بعض الأمور التي يجب مراقبتها:

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| الصورة **بالدرجات الرمادية** لكنها مظلمة | عيّن `ocrEngine.ImageProcessingOptions.IsGrayScale = true` قبل استدعاء `Recognize`. |
| النص **مائل > 15°** | فكر في تدوير البت ماب يدويًا أولًا؛ الـ auto‑deskew يعمل بأفضلية تحت ~10°. |
| تحتاج إلى **ثقة** لكل سطر | استخدم مجموعة `ocrResult.Regions`؛ كل منطقة لها خاصية `Confidence`. |

## الخطوة 4 – عرض والتحقق من النص العربي المستخرج  

أخيرًا، اطبع النتيجة. الإخراج إلى وحدة التحكم يكفي للعرض التجريبي، لكن في الإنتاج قد تخزن السلسلة في قاعدة بيانات أو تمرّرها إلى خدمة ترجمة.

```csharp
        // 4️⃣ Show the recognized Arabic text in the console
        Console.WriteLine("Detected Arabic text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### النتيجة المتوقعة

إذا كان `arabic_sign.jpg` يحتوي على العبارة “مكتبة المدينة”، يجب أن تطبع وحدة التحكم:

```
Detected Arabic text:
مكتبة المدينة
```

لاحظ أن ترتيب النص من اليمين إلى اليسار محفوظ—Aspose OCR يتعامل تلقائيًا مع النصوص ثنائية الاتجاه.

## المشكلات الشائعة والنصائح  

### 1. توافق الخطوط  
بعض محركات OCR تواجه صعوبة مع الخطوط العربية المزخرفة. استخدم خطوطًا شائعة مثل **Tahoma**، **Arial**، أو **Traditional Arabic** للحصول على أفضل النتائج. إذا كنت تتحكم في الصورة المصدر (مثلاً توليدها برمجيًا)، اختر خطًا نظيفًا وعالي التباين.

### 2. دقة الصورة  
يوصى بدقة **300 dpi** أو أعلى. أقل من ذلك قد يخطئ المحرك في تفسير العلامات التشكيلية. يمكنك تكبير صورة منخفضة الدقة باستخدام `System.Drawing` قبل تمريرها إلى Aspose:

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;

Bitmap Upscale(Bitmap src, int scaleFactor = 2)
{
    int newWidth = src.Width * scaleFactor;
    int newHeight = src.Height * scaleFactor;
    Bitmap bmp = new Bitmap(newWidth, newHeight);
    using (Graphics g = Graphics.FromImage(bmp))
    {
        g.InterpolationMode = InterpolationMode.HighQualityBicubic;
        g.DrawImage(src, 0, 0, newWidth, newHeight);
    }
    return bmp;
}
```

### 3. وضع الترخيص  
إذا كنت تستخدم نسخة تجريبية، سيظهر سطر **watermark** في الناتج. ضع ملف الترخيص (`Aspose.Total.lic`) في مجلد التنفيذ أو أدخله عبر `License license = new License(); license.SetLicense("Aspose.Total.lic");` قبل إنشاء `OcrEngine`.

### 4. المستندات متعددة اللغات  
عند خلط العربية والإنجليزية في صفحة واحدة، عيّن `ocrEngine.Language = Language.Multilingual;` ويمكنك أيضًا توفير قائمة تلميحات لغوية. سيكتشف المحرك كل كتلة تلقائيًا.

## مثال عملي كامل  

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد (`dotnet new console`). لا تنسَ استبدال `YOUR_DIRECTORY/arabic_sign.jpg` بالمسار الفعلي لصورتك.

```csharp
using Aspose.OCR;
using System;

class ArabicDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine for Arabic
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.Arabic
        };

        // -------------------------------------------------
        // 2️⃣ Enable preprocessing (auto‑deskew + low denoise)
        // -------------------------------------------------
        ocrEngine.PreprocessOptions = new PreprocessOptions
        {
            AutoDeskew = true,
            DenoiseLevel = DenoiseLevel.Low
        };

        // -------------------------------------------------
        // 3️⃣ Recognize the image
        // -------------------------------------------------
        string imagePath = @"YOUR_DIRECTORY/arabic_sign.jpg";
        OcrResult ocrResult = ocrEngine.Recognize(imagePath);

        // -------------------------------------------------
        // 4️⃣ Output the result
        // -------------------------------------------------
        Console.WriteLine("Detected Arabic text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

شغّله باستخدام `dotnet run` وسترى السلسلة العربية مطبوعة في الطرفية.

## توسيع العرض التجريبي  

- **معالجة دفعات** – تكرار عبر مجلد، جمع النتائج في ملف CSV.  
- **التكامل مع Azure Blob Storage** – جلب الصور من السحابة، تشغيل OCR، وتخزين النص مرة أخرى.  
- **معالجة ما بعد** – استخدم `System.Globalization.StringInfo` لتطبيع الروابط العربية أو إزالة الأحرف التحكمية غير المرغوب فيها.

كل هذه خطوات طبيعية بعد إتقان أساسيات **c# ocr tutorial** و **aspose ocr c# example**.

## الخلاصة  

أصبح لديك الآن **c# ocr tutorial** متكامل يوضح كيفية **extract arabic text** عبر **preprocess image for ocr** ثم **recognize text from image** باستخدام مكتبة Aspose OCR. الكود كامل، وتم شرح السبب وراء كل إعداد، ورأيت نصائح عملية لتجنب المشكلات الشائعة.

لا تتردد في التجربة: جرّب مستويات إزالة الضوضاء المختلفة، استخدم مسحات عالية الدقة، أو اجمع ذلك مع واجهة برمجة تطبيقات ترجمة. النمط الأساسي—التهيئة، المعالجة المسبقة، التعرف، العرض—يبقى ثابتًا مهما كانت اللغة أو المصدر.

هل لديك أسئلة حول التعامل مع مستندات مختلطة اللغات، أو تحتاج نصيحة حول الترخيص؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}