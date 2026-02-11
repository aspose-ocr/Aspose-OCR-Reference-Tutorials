---
category: general
date: 2026-02-11
description: كيفية تصحيح إمالة الصورة في C# وإزالة الضوضاء من الصورة قبل استخراج النص.
  تعلم كيفية تحميل الصورة من ملف ومعالجة الصورة مسبقًا للتعرف الضوئي على الأحرف في
  دقائق.
draft: false
keywords:
- how to deskew image
- remove noise from image
- extract text from image
- preprocess image for ocr
- load image from file
language: ar
og_description: كيفية تصحيح ميل الصورة في C# وإزالة الضوضاء من الصورة قبل استخراج
  النص. اتبع هذا الدليل خطوة بخطوة لمعالجة الصورة مسبقًا للتعرف الضوئي على الأحرف.
og_title: كيفية تصحيح انحراف الصورة في C# – دليل شامل لمعالجة ما قبل OCR
tags:
- C#
- OCR
- Image Processing
title: كيفية تصحيح انحراف الصورة في C# – دليل كامل لمعالجة ما قبل OCR
url: /ar/net/ocr-optimization/how-to-deskew-image-in-c-full-ocr-pre-processing-guide/
---

."

Translate.

Continue.

List "What You’ll Need" etc.

Translate bullet points.

Code block placeholders remain.

Image alt and title.

Step headings.

Blockquote translations.

Table translation.

At the end.

Make sure to keep markdown formatting.

Let's craft Arabic translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح إمالة الصورة في C# – دليل كامل لمعالجة ما قبل OCR

هل تساءلت يوماً **كيف تصحّح إمالة الصورة** التي تبدو كأنها مأخوذة من كاميرا مهتزة؟ ربما حاولت إدخال مسح مائل إلى محرك OCR فحصلت على ناتج مشوّش. هذه مشكلة شائعة—خاصة عندما تكون الصورة الأصلية مائلة *ومليئة* بالضوضاء.  

في هذا الدرس سنستعرض كيفية تحميل صورة من ملف، تصحيح إمالتها، تنظيف البقع، وأخيراً استخراج النص من الصورة باستخدام Aspose.OCR. في النهاية ستحصل على تطبيق Console بلغة C# جاهز للتنفيذ يقوم بكل ما يلزم. لا أسرار، فقط كود واضح وشرح لأهمية كل خطوة.

---

## ما ستحتاجه

- **.NET 6+** (أو أي نسخة حديثة من .NET)  
- حزمة **Aspose.OCR for .NET** عبر NuGet (الإصدار التجريبي المجاني يكفي للعرض)  
- صورة نموذجية مائلة ومليئة بالضوضاء (مثال: `skewed_noisy.jpg`)  
- Visual Studio، VS Code، أو أي بيئة تطوير تفضّلها  

هذا كل شيء. إذا كان لديك مشروع .NET بالفعل، فقط أضف حزمة Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

---

![مثال على تصحيح إمالة الصورة](/images/deskew-example.png "كيفية تصحيح إمالة الصورة")

*نص بديل: كيفية تصحيح إمالة الصورة – قبل وبعد المعالجة*

---

## الخطوة 1 – تحميل الصورة من الملف

قبل أن نتمكن من أي سحر، يجب قراءة الصورة إلى الذاكرة. استخدام `System.Drawing.Image.FromFile` سهل، لكنه يقفل الملف حتى تقوم بتفريغ كائن `Image`، لذا سنغلفه داخل كتلة `using`.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the source file – this satisfies the “load image from file” requirement.
using (Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg"))
{
    // The rest of the pipeline will go here.
}
```

> **نصيحة محترف:** احتفظ بالمسار مطلقاً أثناء الاختبار، ثم انتقل إلى مسار نسبي أو إعدادات تكوين في بيئة الإنتاج.

---

## الخطوة 2 – تهيئة محرك OCR (وتفعيل تحميل الموارد تلقائيًا)

يمكن لـ Aspose.OCR جلب بيانات اللغة تلقائيًا. تفعيل `AutomaticResourceDownload` يوفر عليك نسخ حزم اللغة يدويًا.

```csharp
// Step 2: Set up the OCR engine.
OcrEngine ocrEngine = new OcrEngine
{
    AutomaticResourceDownload = true,
    Language = OcrLanguage.English // you can change this to French, Spanish, etc.
};
```

لماذا نحدد اللغة صراحةً؟ يستخدم المحرك قواميس خاصة بكل لغة لتحسين الدقة، خاصة عندما تحتوي الصورة على علامات ترقيم أو أحرف خاصة.

---

## الخطوة 3 – تصحيح إمالة الصورة (How to Deskew Image)

المسح المائل يربك معظم خوارزميات OCR لأن الأحرف لم تعد على خط الأساس. `OcrPreprocessor.Deskew` يحلل خطوط النص، يحسب الزاوية، ويُدوّر البت ماب إلى الوضع الأفقي.

```csharp
// Step 3: Correct orientation – this is the core “how to deskew image” operation.
Image deskewedImage = OcrPreprocessor.Deskew(sourceImage);
```

> **ماذا لو كانت الصورة مستقيمة بالفعل؟** الطريقة تكتشف زاوية قريبة من الصفر وتعيد نسخة، لذا يمكنك استدعاؤها بأمان دون شرط.

---

## الخطوة 4 – إزالة الضوضاء من الصورة

المسحات من المستندات القديمة غالبًا ما تحتوي على بقع، تشوهات ضغط، أو أنماط خلفية خفيفة. تلك البقع الصغيرة قد تجعل محرك OCR يخطئ في التعرف على الأحرف. `OcrPreprocessor.Denoise` يطبق مرشحًا متوسطًا يحافظ على الحواف بينما يمحو البكسلات المعزولة.

```csharp
// Step 4: Clean up the deskewed picture – this fulfills “remove noise from image”.
Image cleanedImage = OcrPreprocessor.Denoise(deskewedImage);
```

إذا احتجت إلى تنظيف أكثر شدة، توفر Aspose فلاتر إضافية مثل `GaussianBlur` أو `ContrastAdjustment`. في معظم الحالات، يعمل الفلتر الافتراضي بشكل ممتاز.

---

## الخطوة 5 – تنفيذ OCR واستخراج النص من الصورة

الآن بعد أن أصبحت الصورة مستقيمة وهادئة، نمررها إلى محرك OCR. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على النص العادي، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها لاحقًا.

```csharp
// Step 5: Run OCR – this is where we “extract text from image”.
OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);
```

قد تتساءل: *هل يجب تفريغ الصور الوسيطة؟* بالتأكيد. غلف كل صورة بكتلة `using` خاصة أو استدعِ `Dispose()` يدويًا. في هذا المثال المختصر نعتمد على الـ `using` الخارجي لـ `sourceImage` ونترك الـ GC يتولى البقية، لكن في الكود الإنتاجي يُفضَّل التفريغ الصريح.

---

## الخطوة 6 – عرض النص المستخرج

أخيرًا، نطبع النتيجة على وحدة التحكم. في تطبيق حقيقي يمكنك كتابة النص إلى ملف، قاعدة بيانات، أو تمريره إلى خط أنابيب NLP لاحق.

```csharp
// Step 6: Output the recognized text.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**الناتج المتوقع** (بافتراض أن الصورة النموذجية تحتوي على العبارة “Hello World”):

```
=== OCR Output ===
Hello World
```

إذا ظهر النص مشوّشًا، راجع الخطوات السابقة: ربما تحتاج إلى تنقية أقوى أو ضبط إعداد اللغة.

---

## مثال كامل يعمل

بدمج كل ما سبق، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Initialize OCR engine with automatic resource download.
        OcrEngine ocrEngine = new OcrEngine
        {
            AutomaticResourceDownload = true,
            Language = OcrLanguage.English
        };

        // Load the source image from file.
        using (Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg"))
        {
            // Deskew – core “how to deskew image” step.
            Image deskewedImage = OcrPreprocessor.Deskew(sourceImage);

            // Denoise – fulfills “remove noise from image”.
            Image cleanedImage = OcrPreprocessor.Denoise(deskewedImage);

            // Perform OCR – “extract text from image”.
            OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);

            // Show the result.
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

احفظ الملف باسم `Program.cs`، شغّله بالأمر `dotnet run`، وستظهر مخرجات OCR. بسيط، أليس كذلك؟  

---

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| **ماذا لو كانت الصورة صفحة PDF؟** | حوّل الـ PDF إلى صورة أولًا (مثلاً باستخدام `Aspose.PDF`)، ثم مرّر البت ماب إلى نفس السلسلة. |
| **هل يمكن معالجة عدة صفحات في حلقة؟** | بالتأكيد. ضع الكتلة بالكامل داخل حلقة `foreach (var path in imagePaths)` واجمع النتائج في قائمة. |
| **ماذا عن الأداء عند معالجة دفعات كبيرة؟** | أعد استخدام كائن `OcrEngine` واحد؛ فهو يخزن بيانات اللغة مؤقتًا، مما يقلل زمن التهيئة بشكل كبير. |
| **نصيّتي تحتوي على أحرف غير لاتينية – هل سيعمل؟** | عيّن `ocrEngine.Language` إلى قيمة `OcrLanguage` المناسبة (مثال: `OcrLanguage.ChineseSimplified`). |
| **الناتج لا يزال يحتوي على أحرف غريبة – أي نصائح؟** | جرّب زيادة قوة التنقية (`OcrPreprocessor.Denoise(sourceImage, strength: 2)`) أو طبّق مرشح تباين (`OcrPreprocessor.Binarize`). |

---

## الخطوات التالية

بعد أن أتقنت **كيفية تصحيح إمالة الصورة** و**إزالة الضوضاء من الصورة** قبل تشغيل OCR، يمكنك استكشاف:

- **المعالجة الدفعية** – قراءة مجلد من المستندات الممسوحة وإخراج ملف نصي موحد.  
- **استخراج إطارات الحدود** – استخدم `ocrResult.Regions` لتحديد موضع كل كلمة، مفيد لتصحيح PDF.  
- **اكتشاف اللغة** – دمج Aspose.OCR مع مكتبة لتحديد اللغة لتغيير `ocrEngine.Language` تلقائيًا.  

كل هذه تبني مباشرةً على أساس **معالجة الصورة قبل OCR** الذي أنشأته الآن.

---

## TL;DR

غطينا حلًا كاملًا بلغة C# يوضح **كيفية تصحيح إمالة الصورة**، **إزالة الضوضاء من الصورة**، **تحميل الصورة من الملف**، وأخيرًا **استخراج النص من الصورة** باستخدام Aspose.OCR. الكود مستقل، يحتوي على تعليقات، ويشرح “السبب” وراء كل عملية—مما يجعله صديقًا لمحركات البحث ومفيدًا للمساعدين الذكائيين.

جرّبه، عدّل الفلاتر، ودع محرك OCR يقوم بالعمل الشاق. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}