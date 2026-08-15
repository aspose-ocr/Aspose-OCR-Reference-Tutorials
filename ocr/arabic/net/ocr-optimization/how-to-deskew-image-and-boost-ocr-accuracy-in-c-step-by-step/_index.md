---
category: general
date: 2026-04-17
description: كيفية تصحيح انحراف الصورة بسرعة باستخدام Aspose.OCR – تعلّم تحميل صورة
  OCR، ومعالجة الصورة مسبقًا باستخدام OCR، والتعرف على نص الصورة بدقة عالية.
draft: false
keywords:
- how to deskew image
- recognize text image
- improve ocr accuracy
- load image ocr
- preprocess image ocr
language: ar
og_description: كيفية تصحيح انحراف الصورة وتحسين دقة OCR في C#. تعلم كيفية تحميل صورة
  OCR، ومعالجة الصورة مسبقًا للـ OCR، والتعرف على نص الصورة باستخدام Aspose.OCR.
og_title: كيفية تصحيح انحراف الصورة – دليل OCR كامل بلغة C#
tags:
- Aspose.OCR
- C#
- Image Processing
title: كيفية تصحيح ميل الصورة وزيادة دقة OCR في C# – دليل خطوة بخطوة
url: /ar/net/ocr-optimization/how-to-deskew-image-and-boost-ocr-accuracy-in-c-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح إمالة الصورة وزيادة دقة OCR في C#

**كيفية تصحيح إمالة الصورة** هي عقبة شائعة كلما احتجت لاستخراج النص من صورة غير محاذاة تمامًا. في هذا الدليل سنستعرض تحميل الصورة، معالجتها مسبقًا، وأخيرًا **التعرف على نص الصورة** باستخدام سلسلة الفلاتر القوية في Aspose.OCR.

إذا سبق لك أن وجهت كاميرا هاتفك إلى إيصال أو علامة أو نموذج ممسوح وانتهى بك الأمر بنصوص مشوهة وغير قابلة للقراءة، فأنت تعرف مدى الإحباط. الخبر السار؟ بضع أسطر من كود C# يمكنها أن تُستقيم الصورة، تُنظف الضوضاء، وتُعطيك سلسلة نظيفة يمكنك استخدامها فعليًا. سنتطرق أيضًا إلى كيفية **تحسين دقة OCR** عبر تعديل خطوات المعالجة المسبقة.

## ما الذي ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Core)  
- رخصة أو نسخة تجريبية من **Aspose.OCR** (متوفرة عبر NuGet)  
- ملف صورة به إمالة بسيطة أو ضوضاء (مثال: `skewed_photo.png`)  

لا تحتاج إلى أدوات طرف ثالث معقدة—فقط مكتبة Aspose.OCR وقليل من معرفة C#.

![مثال على كيفية تصحيح إمالة الصورة](/images/deskew-demo.png "كيفية تصحيح إمالة الصورة – الأصلية مقابل المصححة")

---

## الخطوة 1 – تحميل صورة OCR: تجهيز ملف المصدر

قبل أن نتمكن من استقامة أي شيء، نحتاج إلى جلب الصورة إلى الذاكرة. طريقة `OcrImage.FromFile` تقوم بذلك بالضبط.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the image you want to process
var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");
```

> **لماذا هذا مهم:** تحميل الصورة كـ `OcrImage` يمنح محرك OCR وصولًا مباشرًا إلى بيانات البكسل، وهو أمر أساسي لخطوات **معالجة صورة OCR** اللاحقة. إذا كان مسار الملف غير صحيح، ستحصل على استثناء `FileNotFoundException`، لذا تحقق من الموقع جيدًا.

## الخطوة 2 – معالجة صورة OCR: بناء سلسلة فلاتر تصحيح الإمالة

الآن يأتي جوهر **كيفية تصحيح إمالة الصورة**. يأتي Aspose.OCR مع مجموعة من الفلاتر التي يمكنك ترتيبها بأي تسلسل. لمعظم الصور الواقعية ستحتاج إلى:

1. **Deskew** – تصحيح الإمالة  
2. **Denoise** – إزالة بقع الملح والفلفل  
3. **ContrastEnhance** – إبراز الأحرف الباهتة

```csharp
// Create a chain of preprocessing filters
var filterChain = new ImageFilterCollection
{
    new DeskewFilter(),          // Detects and corrects rotation
    new DenoiseFilter(),        // Reduces noise
    new ContrastEnhanceFilter() // Boosts contrast for faint text
};

// Apply the filter chain to obtain a cleaned image
var filteredImage = filterChain.Apply(ocrImage);
```

> **نصيحة محترف:** إذا كانت صورتك مضاءة جيدًا بالفعل، يمكنك حذف `ContrastEnhanceFilter`. تقليل المعالجة يعني تنفيذًا أسرع.

### حالات خاصة

- **إمالة شديدة (>45°):** يعمل `DeskewFilter` بأفضل شكل حتى حوالي 30°. للزوايا الأكبر قد تحتاج إلى تدوير الصورة يدويًا أولًا (`filteredImage.Rotate(…)`).
- **خلفيات ملونة:** حوّل إلى تدرج الرمادي قبل إزالة الضوضاء للحصول على نتائج أفضل (`filteredImage = filteredImage.ToGrayscale();`).

## الخطوة 3 – التعرف على نص الصورة: تشغيل محرك OCR

مع صورة bitmap نظيفة ومستقيمة في يدك، حان وقت استخراج الأحرف.

```csharp
// Create an OCR engine instance
using var ocrEngine = new OcrEngine();

// Recognize text from the filtered image
var ocrResult = ocrEngine.Recognize(filteredImage);

// Display the recognized text
Console.WriteLine(ocrResult.Text);
```

> **ما الذي يحدث في الخلفية؟** `OcrEngine` يشغل مُعرّفًا يعتمد على الشبكات العصبية يتوقع صورة شبه عمودية وعالية التباين. لهذا السبب خطوة **معالجة صورة OCR** السابقة حاسمة لـ **تحسين دقة OCR**.

### النتيجة المتوقعة

إذا احتوت الصورة الأصلية على السطر “Invoice #12345 – Total $89.99”، سيطبع الطرفية شيءً مشابهًا:

```
Invoice #12345 – Total $89.99
```

إذا رأيت أحرفًا مشوشة، راجع سلسلة الفلاتر—ربما تحتاج الصورة إلى شحذ إضافي (`new SharpenFilter()`).

## الخطوة 4 – ضبط دقيق لتحسين دقة OCR

حتى بعد تصحيح الإمالة، قد يتعثر OCR مع بعض الخطوط أو المسحات منخفضة الدقة. إليك بعض التعديلات السريعة:

| المشكلة | الحل |
|-------|-----|
| حجم الخط صغير (<10 pt) | تكبير الصورة (`filteredImage = filteredImage.Resize(2.0);`) |
| نص رمادي فاتح على خلفية بيضاء | زيادة التباين أكثر (`new ContrastEnhanceFilter(1.5)`) |
| نص متعدد اللغات | تعيين `ocrEngine.Language = OcrLanguage.Multilingual;` |

هذه التعديلات **تحسن دقة OCR** مباشرةً دون تغيير بنية الكود الأساسية.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ الذي يدمج جميع الخطوات السابقة. انسخه إلى مشروع وحدة تحكم جديد واضغط **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 1: Load the image you want to process
        var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");

        // Step 2: Build a chain of preprocessing filters
        var filterChain = new ImageFilterCollection
        {
            new DeskewFilter(),          // Detects and corrects rotation
            new DenoiseFilter(),        // Reduces salt‑and‑pepper noise
            new ContrastEnhanceFilter() // Improves faint characters
        };

        // Step 3: Apply the filter chain to obtain a cleaned image
        var filteredImage = filterChain.Apply(ocrImage);

        // Step 4: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Optional: set language or other engine options here
        // ocrEngine.Language = OcrLanguage.English;

        // Step 5: Recognize text from the filtered image
        var ocrResult = ocrEngine.Recognize(filteredImage);

        // Step 6: Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

شغّل البرنامج، وسترى النص المنظف والمستقيم يُطبع في الطرفية.

## أسئلة شائعة وإجابات

**س: هل يعمل هذا مع ملفات PDF؟**  
ج: نعم. حوّل كل صفحة PDF إلى صورة (مثلاً باستخدام `Aspose.PDF`) ومرّر الـ bitmap الناتج إلى نفس سلسلة الفلاتر.

**س: ماذا لو كانت صورتي محاذاة تمامًا؟**  
ج: سيكتشف `DeskewFilter` زاوية قريبة من الصفر ويترك الصورة دون تعديل—لا ضرر يحدث.

**س: هل يمكنني معالجة عدة صور دفعة واحدة؟**  
ج: بالتأكيد. غلف الكود داخل حلقة `foreach (var path in Directory.GetFiles(...))` واحفظ كل `ocrResult.Text` في قائمة أو ملف.

---

## الخلاصة

أظهرنا **كيفية تصحيح إمالة الصورة** برمجيًا، استعرضنا خطوة **تحميل صورة OCR**، طبقنا خط أنابيب **معالجة صورة OCR** قوي، وأخيرًا **تعرفنا على نص الصورة** باستخدام Aspose.OCR. عبر تعديل الفلاتر وربما تكبير أو شحذ الصورة، يمكنك **تحسين دقة OCR** لمجموعة واسعة من السيناريوهات الواقعية.

هل أنت مستعد للتحدي التالي؟ جرّب دمج هذه السلسلة في واجهة ويب API، أو جرب التعرف على الملاحظات المكتوبة يدويًا بإضافة `new BinarizationFilter()` قبل تصحيح الإمالة. الاحتمالات لا حصر لها—برمجة سعيدة!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}