---
category: general
date: 2026-03-18
description: كيفية تصحيح إمالة الصورة وتقليل الضوضاء في الملفات الممسوحة ضوئياً. تعلم
  كيفية تحميل الصورة من ملف، استخراج النص من ملف TIFF، والتعرف على النص من الصورة
  باستخدام Aspose OCR.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: ar
og_description: كيفية تصحيح انحراف الصورة بسرعة باستخدام Aspose OCR. يوضح هذا الدليل
  كيفية تقليل الضوضاء، وتحميل الصورة من ملف، واستخراج النص من ملف TIFF باستخدام C#.
og_title: كيفية تصحيح ميل الصورة – دليل كامل لتقنية OCR بلغة C#
tags:
- OCR
- C#
- Image Processing
title: كيفية تصحيح إمالة الصورة وتنظيف المسحات الضوئية – دليل C# الكامل
url: /ar/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح ميل الصورة – دليل OCR كامل بلغة C#

هل تساءلت يومًا **كيفية تصحيح ميل الصورة** للملفات التي تبدو كأنها مأخوذة من ماسح ضوئي غير ثابت؟ لست وحدك. يواجه معظم المطورين هذه المشكلة عندما يكون ملف TIFF الأصلي مائلًا قليلًا، وتصبح نتائج OCR فوضى. الخبر السار؟ ببضع أسطر من C# يمكنك تسوية الصورة، القضاء على الخلفية المحببة، واستخراج نص نظيف قابل للبحث مباشرة من الملف.

في هذا الدليل سنستعرض **كيفية تقليل الضوضاء**، **تحميل الصورة من ملف**، وأخيرًا **التعرف على النص من الصورة** باستخدام Aspose OCR. في النهاية ستتمكن من **استخراج النص من ملفات tiff** دون عناء.

> **نصيحة احترافية:** إذا كنت تستخدم Aspose OCR بالفعل في مشاريع أخرى، يمكنك إضافة هذه الفلاتر دون أي مشاكل ترخيص إضافية.

---

## ما ستحتاجه

- .NET 6 أو أحدث (الكود يعمل على .NET Core أيضًا)  
- حزمة NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- ملف TIFF ممسوح ضوئيًا مائل قليلًا أو يحتوي على ضوضاء (سنستخدم `skewed_scanned_doc.tif` كمثال)  
- محرر نصوص أو بيئة تطوير (Visual Studio, VS Code, Rider – اختر ما يناسبك)

لا توجد مكتبات إضافية مطلوبة؛ الفلاتر التي سنستخدمها مدمجة في Aspose OCR.

---

## الخطوة 1 – إنشاء محرك OCR (كيفية تصحيح ميل الصورة)

الخطوة الأولى هي إنشاء كائن `OcrEngine`. فكر فيه كالعقل الذي سيقرأ الأحرف لاحقًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

لماذا ننشئ المحرك مسبقًا؟ لأنه يتيح لك مكانًا واحدًا لإرفاق فلاتر ما قبل المعالجة، حزم اللغات، وخيارات الإخراج. إذا تخطيت هذه الخطوة واستدعيت `OcrEngine.Recognize` مباشرة، ستفقد فرصة تنظيف الصورة أولًا، وهذا هو السبب الرئيسي لاهتمامنا بتصحيح الميل.

---

## الخطوة 2 – إضافة فلاتر تصحيح الميل وتقليل الضوضاء (كيفية تقليل الضوضاء)

الآن نرفق فلتريْن:

| الفلتر | ما يفعله | لماذا يهم |
|--------|----------|-----------|
| `AutoDeskewFilter` | يكتشف ويصحح الدوران | يُسطّح خطوط النص بحيث يستطيع محرك OCR قراءتها بشكل صحيح |
| `NoiseReductionFilterV2` | يزيل البقع والحبوب الخلفية | البكسلات الأنظف تعني أخطاء أقل في التعرف |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

يمكنك استبدال `NoiseReductionFilterV2` بالإصدار الأقدم، لكن خوارزمية v2 تتعامل مع الماسحات الحديثة بشكل أفضل. إذا كان مستندك مسطحًا تمامًا، فإن فلتر تصحيح الميل سيتخطى الصورة دون تعديل—بدون أي ضرر.

---

## الخطوة 3 – تحميل الصورة من ملف (تحميل الصورة من ملف)

توفر Aspose أداة مساعدة `ImageStream.FromFile` التي تقرأ مجموعة متنوعة من الصيغ، بما في ذلك TIFF, JPEG, PNG, و BMP. إليك كيفية جلب الملف إلى الذاكرة:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

استبدل `YOUR_DIRECTORY` بالمسار الفعلي على جهازك. إذا كنت تستخدم مسارًا نسبيًا، تأكد من أن الملف موجود بجوار الملف التنفيذي أو اضبط دليل العمل وفقًا لذلك.

---

## الخطوة 4 – تشغيل OCR على الصورة المعالجة مسبقًا (التعرف على النص من الصورة)

مع الفلاتر في مكانها والصورة محمَّلة، نطلب من Aspose أخيرًا قراءة الأحرف:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

في الخلفية، يقوم المحرك بتشغيل خوارزمية تصحيح الميل، تنعيم الضوضاء، ثم تشغيل مُعرّف يعتمد على الشبكات العصبية. النتيجة تُغلف في كائن `OcrResult` يزودك بالنص الخام، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها لاحقًا.

---

## الخطوة 5 – عرض أو حفظ النص المستخرج (استخراج النص من TIFF)

للتجربة السريعة نطبع النص على وحدة التحكم، لكن يمكنك كتابته إلى ملف، قاعدة بيانات، أو تمريره إلى سير عمل لاحق.

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**الناتج المتوقع** (مثال، سيتفاوت حسب مستندك):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

إذا كان الناتج لا يزال يحتوي على أحرف غير مفهومة، تحقق من أن ملف TIFF الأصلي ليس منخفض الدقة جدًا (الحد الأدنى الموصى به 300 dpi) وأن اللغة مضبوطة بشكل صحيح في `ocrEngine.Settings.Language`.

---

## مثال كامل يعمل (جميع الخطوات في مكان واحد)

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد وتشغيله فورًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

احفظ الملف باسم `Program.cs`، نفّذ `dotnet run`، وسترى النص المنقح يظهر في الطرفية.

---

## الأسئلة المتكررة والحالات الخاصة

### ماذا لو كان ملف TIFF يحتوي على صفحات متعددة؟
يمكن لـ Aspose OCR معالجة الصور متعددة الصفحات عبر حلقة `image.GetPages()` (أو باستخدام `image.Pages`). كل صفحة تُعيد كائن `OcrResult` خاص بها. اجمع النتائج باستخدام `StringBuilder` إذا كنت تحتاج إلى نص موحد.

### هل يعمل فلتر تصحيح الميل على الصور المائلة بشدة؟
يتعامل مع دوران يصل إلى حوالي ±15°. إذا تجاوز ذلك، قد تحتاج إلى تدوير الصورة يدويًا مسبقًا باستخدام مكتبة رسومية (مثل `System.Drawing` أو `SkiaSharp`) قبل تمريرها إلى Aspose.

### كيف يمكن تحسين الدقة للنص غير الإنجليزي؟
حدد اللغة صراحةً:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

يمكنك أيضًا تحميل حزم لغات مخصصة إذا لم تغطِ الحزم المدمجة أبجديتك.

### هل يمكن تشغيل هذا على لينكس؟
بالطبع. Aspose OCR متعدد المنصات؛ فقط تأكد من وجود الاعتمادات الأصلية (عادة لا توجد لأي نسخة .NET صافية). استخدم `dotnet publish -r linux-x64` للحصول على ملف تنفيذي مستقل.

---

## إضافي: تصور الصورة المصححة

إذا أردت رؤية الصورة المصححة قبل OCR، يمكنك حفظها مرة أخرى على القرص:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![مثال على تصحيح ميل الصورة](https://example.com/deskew-demo.png "مثال على تصحيح ميل الصورة")

*نص بديل للصورة:* **مثال على تصحيح ميل الصورة** – يُظهر قبل/بعد لملف TIFF مائل تم تصحيحه بواسطة AutoDeskewFilter.

---

## الخلاصة

غطّينا **كيفية تصحيح ميل الصورة** للملفات، **كيفية تقليل الضوضاء**، والمسار الكامل لـ **التعرف على النص من الصورة**، **تحميل الصورة من ملف**، و**استخراج النص من TIFF** باستخدام Aspose OCR بلغة C#. الفكرة الأساسية؟ إضافة فلتريْن فقط قبل المعالجة يمكن أن يحوّل مسحًا غير مستقر ومحبب إلى مستند واضح وقابل للبحث دون أدوات خارجية.

مستعد للخطوة التالية؟ جرّب استبدال `AutoDeskewFilter` بـ `AutoRotateFilter` إذا كانت مستنداتك مقلوبة، أو جرب `ContrastEnhancementFilter` للطبعات الباهتة. النمط نفسه—المحرك → الفلاتر → التحميل → التعرف—ينطبق على جميع سيناريوهات Aspose OCR، لذا يمكنك إعادة استخدام هذا الهيكل للـ PDFs، PNGs، أو حتى صور الكاميرا.

برمجة سعيدة، ولتكن OCR دائمًا دقيقة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}