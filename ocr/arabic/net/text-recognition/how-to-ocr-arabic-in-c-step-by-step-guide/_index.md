---
category: general
date: 2026-03-26
description: كيفية التعرف الضوئي على الأحرف العربية في C# باستخدام Aspose OCR – تعلم
  استخراج النص العربي، التعرف على النص من الصورة، وتحويل الصورة إلى نص بسرعة.
draft: false
keywords:
- how to ocr arabic
- extract arabic text
- recognize text from image
- convert image to text
- load image for ocr
language: ar
og_description: كيف تقوم بعملية OCR للغة العربية في C#؟ اتبع هذا الدليل لاستخراج النص
  العربي، والتعرف على النص من الصورة، وتحويل الصورة إلى نص باستخدام Aspose OCR.
og_title: كيفية إجراء OCR للغة العربية في C# – دليل برمجة شامل
tags:
- OCR
- C#
- Aspose
- Arabic
title: كيفية إجراء OCR للغة العربية في C# – دليل خطوة بخطوة
url: /ar/net/text-recognition/how-to-ocr-arabic-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على الأحرف العربية في C# – دليل برمجة كامل

هل تساءلت يومًا **كيف تقوم بالتعرف الضوئي على الأحرف العربية** في تطبيق .NET؟ في هذا الدرس سنستعرض الخطوات الدقيقة **لاستخراج النص العربي** من صورة باستخدام Aspose OCR. سواء كنت تبني ماسحًا متعدد اللغات أو تحتاج فقط إلى سحب لافتات عربية إلى قاعدة بيانات، فإن العملية بسيطة جدًا بمجرد توفر المكونات اللازمة.

الأمر هو أن معظم مكتبات OCR تكون مهيأة للإنجليزية افتراضيًا، لذا عليك إخبار المحرك باللغة التي تتوقعها. سنغطي **كيفية تحميل الصورة للتعرف الضوئي**، ضبط اللغة، وأخيرًا **التعرف على النص من الصورة** لتتمكن من **تحويل الصورة إلى نص** ببضع أسطر من C#. في النهاية ستحصل على تطبيق console يعمل ويطبع اللغة المكتشفة والسلسلة العربية المستخرجة.

## ما الذي ستحتاجه

- **.NET 6+** (أو أي نسخة حديثة من .NET؛ الواجهة البرمجية تعمل بنفس الطريقة)
- حزمة NuGet **Aspose.OCR for .NET** – ثبّتها باستخدام `dotnet add package Aspose.OCR`
- ملف صورة يحتوي على أحرف عربية، مثل `arabic_sign.jpg`
- محرر كود – Visual Studio أو VS Code أو Rider يكفي

لا ملفات إعدادات إضافية، لا خدمات خارجية، ولا سحر مخفي. مجرد تطبيق console نظيف ومستقل.

## الخطوة 1: تهيئة محرك OCR – كيفية التعرف الضوئي على الأحرف العربية

أولًا، أنشئ كائنًا من `OcrEngine`. هذا الكائن هو قلب المكتبة؛ فهو يحمل جميع الإعدادات التي تؤثر على عملية التعرف.

```csharp
using System;
using Aspose.OCR;

class LanguageExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:** إنشاء المحرك يخصّص موارد OCR الأصلية. إذا تخطيت هذه الخطوة، لن يكون هناك ما يخبر المكتبة اللغة المتوقعة، وستحصل على مخرجات مشوشة.

## الخطوة 2: إخبار المحرك أي لغة يجب التعرف عليها

الآن نضبط خاصية `Language`. للغة العربية نستخدم `OcrLanguage.Arabic`. يمكنك التبديل إلى لغات أخرى (Cyrillic، Korean، إلخ) بتغيير هذه السطر الوحيد.

```csharp
        // Step 2: Specify the language to recognize (Arabic in this case)
        ocrEngine.Language = OcrLanguage.Arabic;   // alternatives: OcrLanguage.CyrillicExtended, OcrLanguage.Korean
```

> **نصيحة احترافية:** إذا كانت صورك تحتوي على لغات مختلطة، يمكنك تفعيل `OcrLanguage.Multilingual` والسماح للمحرك بالتخمين، لكن الأداء قد يتراجع قليلًا. الالتزام بلغة واحدة—مثل العربية—يبقي العملية سريعة ودقيقة.

## الخطوة 3: تحميل الصورة للتعرف الضوئي

الخطوة التالية هي إمداد المحرك بصورة. `OcrImage.FromFile` يقرأ الملف من القرص ويحوّله إلى bitmap داخلي يمكن لـ Aspose معالجته.

```csharp
        // Step 3: Load the image that contains the text
        OcrImage inputImage = OcrImage.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");
```

> **ماذا لو لم يُعثر على الملف؟** ضع الاستدعاء داخل `try/catch` واعرض رسالة مفيدة. وإلا سيُطلق المحرك استثناء `FileNotFoundException`.

```csharp
        // Optional: graceful error handling
        try
        {
            OcrImage inputImage = OcrImage.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not load image: {ex.Message}");
            return;
        }
```

## الخطوة 4: التعرف على النص من الصورة وتحويل الصورة إلى نص

بعد تهيئة المحرك وتحميل الصورة، نُجري عملية التعرف. تُعيد طريقة `Recognize` كائن `OcrResult` يحتوي على السلسلة المستخرجة وبعض مقاييس الثقة.

```csharp
        // Step 4: Run the recognition process
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);
```

> **لماذا يعمل هذا:** محرك OCR من Aspose يُجري سلسلة من خطوات ما قبل المعالجة—التنقيط، تصحيح الميل، تجزئة الأحرف—قبل تمرير البيانات إلى شبكة عصبية مدربة على أشكال الأحرف العربية. النتيجة عادةً موثوقة للطباعة ذات التباين العالي.

## الخطوة 5: عرض اللغة المكتشفة والنص المستخرج

أخيرًا، نطبع ما حصلنا عليه. لا تزال خاصية `Language` تحتفظ بالقيمة التي ضبطناها، لتأكيد أن المحرك كان يستخدم العربية. خاصية `Text` في `OcrResult` تحمل ناتج **تحويل الصورة إلى نص**.

```csharp
        // Step 5: Display the detected language and the extracted text
        Console.WriteLine($"Detected language: {ocrEngine.Language}");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### النتيجة المتوقعة

```
Detected language: Arabic
مرحبا بكم في عالم البرمجة
```

إذا كانت الصورة غير واضحة أو الخط مزخرف، قد تلاحظ فقدان أحرف أو انخفاض في الثقة. في هذه الحالة، جرّب زيادة دقة الصورة أو تطبيق مرشح ما قبل المعالجة (مثل الشحذ) قبل تمريرها إلى `OcrEngine`.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع console جديد. لا تنس استبدال `YOUR_DIRECTORY/arabic_sign.jpg` بالمسار الفعلي لصورتك العربية.

```csharp
using System;
using Aspose.OCR;

class LanguageExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Specify the language to recognize (Arabic in this case)
        ocrEngine.Language = OcrLanguage.Arabic;   // alternatives: OcrLanguage.CyrillicExtended, OcrLanguage.Korean

        // Step 3: Load the image that contains the text
        OcrImage inputImage;
        try
        {
            inputImage = OcrImage.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not load image: {ex.Message}");
            return;
        }

        // Step 4: Run the recognition process
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // Step 5: Display the detected language and the extracted text
        Console.WriteLine($"Detected language: {ocrEngine.Language}");
        Console.WriteLine(ocrResult.Text);
    }
}
```

شغّل المشروع باستخدام `dotnet run`. إذا تم إعداد كل شيء بشكل صحيح، سترى السلسلة العربية مطبوعة في الـ console.

## أسئلة شائعة وحالات خاصة

### ماذا لو أردت **التعرف على النص من ملفات صورة** بصيغ غير JPEG؟

يدعم Aspose OCR صيغ PNG، BMP، TIFF، وحتى صفحات PDF. فقط غيّر امتداد الملف في `FromFile`. بالنسبة للـ PDF يمكنك أيضًا تمرير رقم الصفحة: `OcrImage.FromPdf("file.pdf", pageNumber: 1)`.

### كيف أحسّن الدقة عندما تكون الصورة منخفضة التباين؟

قم بتهيئة الصورة مسبقًا باستخدام `System.Drawing` أو `ImageSharp` لزيادة التباين، تحويلها إلى تدرج الرمادي، أو تطبيق مرشح شحذ قبل إنشاء `OcrImage`. مثال:

```csharp
using SixLabors.ImageSharp;
using SixLabors.ImageSharp.Processing;

// Load, enhance, then feed to Aspose
using var img = Image.Load("low_contrast.jpg");
img.Mutate(x => x.Contrast(1.5f).Sharpen());
img.Save("enhanced.png");
OcrImage enhanced = OcrImage.FromFile("enhanced.png");
```

### هل يمكنني **استخراج النص العربي** من عدة صور دفعة واحدة؟

بالتأكيد. ضع منطق التعرف داخل حلقة `foreach` على مجلد يحتوي على الملفات. فقط تذكّر تحرير كل `OcrImage` بعد الاستخدام لتحرير الذاكرة الأصلية:

```csharp
foreach (var file in Directory.GetFiles("images", "*.jpg"))
{
    using var img = OcrImage.FromFile(file);
    var result = ocrEngine.Recognize(img);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text}");
}
```

## الخطوات التالية

الآن بعد أن أتقنت **كيفية التعرف الضوئي على الأحرف العربية** باستخدام Aspose، قد ترغب في:

- **استخراج النص العربي** من ملفات PDF (استخدم `OcrImage.FromPdf`).
- تخزين النتائج في قاعدة بيانات لأرشفة قابلة للبحث.
- دمج OCR مع واجهات برمجة تطبيقات الترجمة للترجمة الآلية من العربية إلى الإنجليزية.
- تجربة لغات أخرى—فقط استبدل `OcrLanguage.Arabic` بـ `OcrLanguage.Korean` أو `OcrLanguage.CyrillicExtended`.

كل هذه المواضيع تعتمد على نفس المفاهيم الأساسية: **تحميل الصورة للتعرف الضوئي**، **التعرف على النص من الصورة**، و**تحويل الصورة إلى نص**، لذا فأنت الآن مستعد لاستكشافها.

---

*برمجة سعيدة! إذا واجهت أي مشكلة، اترك تعليقًا أدناه أو راجع وثائق Aspose.OCR للمزيد من خيارات التكوين المتقدمة.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}