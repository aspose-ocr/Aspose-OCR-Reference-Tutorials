---
category: general
date: 2026-02-28
description: حوّل ملفات Djvu إلى نص بسرعة باستخدام Aspose OCR C#. تعلّم كيفية التعرف
  على النص من الصورة واستخراج النص من ملفات Djvu في بضع خطوات سهلة.
draft: false
keywords:
- convert djvu to text
- recognize text from image
- extract text from djvu
- aspose ocr c# tutorial
language: ar
og_description: تحويل Djvu إلى نص باستخدام Aspose OCR C#. اتبع هذا الدليل خطوة بخطوة
  للتعرف على النص من الصورة واستخراج النص من ملفات Djvu.
og_title: تحويل Djvu إلى نص في C# – دليل Aspose OCR الكامل
tags:
- Aspose OCR
- C#
- DjVu
- Text Extraction
title: تحويل Djvu إلى نص في C# باستخدام Aspose OCR – دليل كامل
url: /ar/net/text-recognition/convert-djvu-to-text-in-c-with-aspose-ocr-complete-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل Djvu إلى نص في C# باستخدام Aspose OCR – دليل كامل

هل احتجت يومًا إلى **تحويل Djvu إلى نص** لكن لم تكن متأكدًا أي مكتبة يمكنها التعامل مع ذلك؟ لست وحدك. يواجه العديد من المطورين هذا العائق عندما يحاولون استخراج سلاسل قابلة للبحث من مستندات DjVu الممسوحة ضوئيًا. الخبر السار؟ تجعل Aspose OCR العملية بأكملها سهلة للغاية، مما يتيح لك **التعرف على النص من صورة** للملفات—بما في ذلك DjVu—دون الحاجة إلى التعامل مع معالجة البكسل منخفضة المستوى.

في هذا الدليل سنستعرض مثالًا واقعيًا يوضح لك بالضبط كيفية **استخراج النص من Djvu** باستخدام C#. في النهاية ستحصل على برنامج قابل للتنفيذ، وفهم واضح لأسباب أهمية كل سطر، ومجموعة من النصائح التي تحميك من المشكلات الشائعة. لا حاجة لمراجع خارجية—فقط كود جاهز للنسخ واللصق.

## ما الذي ستحتاجه

* .NET 6.0 SDK أو أحدث (تعمل الواجهة البرمجية مع .NET Core و .NET Framework على حد سواء)
* رخصة Aspose.OCR for .NET سارية (الإصدار التجريبي المجاني يُستخدم للاختبار)
* ملف DjVu تريد معالجته (ضعه في مجلد يمكنك الإشارة إليه)
* Visual Studio 2022 أو أي محرر C# تفضله

هذا كل شيء—لا شيء معقد. إذا كان لديك هذه الأساسيات، فأنت جاهز للبدء في **تحويل Djvu إلى نص**.

![convert djvu to text example](image-placeholder.png "Screenshot showing Aspose OCR extracting text from a DjVu file")

## الخطوة 1: تثبيت حزمة Aspose.OCR عبر NuGet

أولاً، أضف مكتبة Aspose OCR إلى مشروعك. افتح طرفية في مجلد الحل الخاص بك وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** استخدام NuGet CLI يضمن حصولك على أحدث نسخة مستقرة، والتي في وقت كتابة هذا الدليل هي `23.10`. الحفاظ على تحديث الحزمة يقلل من احتمال مواجهة أخطاء تم إصلاحها بالفعل.

## الخطوة 2: تهيئة محرك OCR

إنشاء نسخة من `OcrEngine` هو نقطة الدخول لأي عملية **التعرف على النص من صورة**. فكر في المحرك كالعقل الذي يفسر بيانات البكسل ويحولها إلى أحرف.

```csharp
using Aspose.OCR;
using System.Drawing;

class DjvuDemo
{
    static void Main()
    {
        // Step 2: Create an OCR engine instance – this object holds all the settings.
        OcrEngine ocrEngine = new OcrEngine();
```

لماذا ننشئ المحرك مرة واحدة؟ إعادة استخدام نفس `OcrEngine` عبر ملفات متعددة يتجنب عبء تحميل بيانات اللغة بشكل متكرر، مما يمكن أن يحسن الأداء عندما يكون لديك دفعة من ملفات DjVu.

## الخطوة 3: تحميل صورة DjVu

تعامل Aspose OCR ملفات DjVu كصور، لذا يمكنك تحميلها مباشرة باستخدام `Image.Load`. يضمن بيان `using` تحرير الصورة بشكل صحيح، مما يمنع تسرب الذاكرة.

```csharp
        // Step 3: Load the DjVu image you want to process.
        // Replace the path with the actual location of your .djvu file.
        using var djvuImage = Image.Load(@"C:\Docs\input.djvu");
```

> **Edge case:** بعض ملفات DjVu تحتوي على صفحات متعددة. `Image.Load` سيحمّل الصفحة الأولى افتراضيًا. إذا كنت بحاجة لمعالجة كل صفحة، استخدم `Image.LoadMultiple` وتكرّر عبر المجموعة الناتجة.

## الخطوة 4: تنفيذ التعرف الضوئي على الأحرف (OCR)

الآن يأتي السحر. تقوم طريقة `Recognize` بمسح الـ bitmap وتعيد كائن `OcrResult` يحتوي على النص المستخرج، درجات الثقة، وأكثر.

```csharp
        // Step 4: Perform OCR recognition on the loaded image.
        var ocrResult = ocrEngine.Recognize(djvuImage);
```

قد تتساءل: *ماذا لو كان DjVu يحتوي على مسح منخفض الدقة؟* تعديل خاصية `Resolution` للمحرك قبل استدعاء `Recognize` يمكن أن يعزز الدقة:

```csharp
        // Optional: improve accuracy for low‑dpi images.
        ocrEngine.RecognitionSettings.Resolution = 300; // DPI
```

## الخطوة 5: إخراج النص المعترف به

أخيرًا، اكتب السلسلة المستخرجة إلى وحدة التحكم—أو إلى ملف إذا فضلت ذلك. هذه هي اللحظة التي تقوم فيها فعليًا **تحويل Djvu إلى نص**.

```csharp
        // Step 5: Output the recognized text to the console.
        System.Console.WriteLine("=== Extracted Text ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

عند تشغيل البرنامج (`dotnet run`)، يجب أن ترى شيئًا مشابهًا لـ:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

إذا كان الإخراج مشوشًا، تحقق مرة أخرى من جودة DjVu المصدر، إعدادات اللغة، وما إذا كنت بحاجة لتفعيل حزمة لغة معينة عبر `ocrEngine.Language = OcrLanguage.English;`.

## التعرف على النص من صورة باستخدام Aspose OCR – الإعدادات المتقدمة

بينما يعمل التدفق الأساسي لمعظم الحالات، تقدم Aspose OCR مجموعة غنية من الخيارات التي تتيح لك ضبط خطوة **التعرف على النص من صورة** بدقة:

| الإعداد | ما يفعله | متى يُستخدم |
|---------|----------|--------------|
| `ocrEngine.RecognitionSettings.DetectOrientation` | يدور الصفحات المائلة تلقائيًا | المستندات الممسوحة التي ليست محاذاة تمامًا |
| `ocrEngine.RecognitionSettings.Language` | يفرض نموذج لغة محدد | ملفات PDF متعددة اللغات حيث يفشل نموذج اللغة الإنجليزية الافتراضي |
| `ocrEngine.RecognitionSettings.UsePreProcessing` | يطبق فلاتر (إزالة الضوضاء، تحويل إلى ثنائي) قبل OCR | مسحات DjVu منخفضة التباين أو صاخبة |
| `ocrEngine.RecognitionSettings.OutputFormat` | يعيد نصًا عاديًا، hOCR، أو PDF | تحتاج إلى ملفات PDF قابلة للبحث بدلاً من النص الخام |

جرّب هذه العلامات بمجرد أن يعمل الخط الأساسي. يمكن للتعديلات الصغيرة رفع دقتك من 85 % إلى أكثر من 95 % على المستندات الصعبة.

## استخراج النص من ملفات Djvu – معالجة الصفحات المتعددة

إذا كان DjVu الخاص بك يحتوي على عدة صفحات، فستحتاج إلى التكرار عبر كل صفحة وربط النتائج معًا. إليك نسخة مختصرة:

```csharp
using Aspose.OCR;
using System.Drawing;

class DjvuMultiPageDemo
{
    static void Main()
    {
        OcrEngine engine = new OcrEngine();
        var images = Image.LoadMultiple(@"C:\Docs\book.djvu");

        foreach (var page in images)
        {
            var result = engine.Recognize(page);
            System.Console.WriteLine($"--- Page {page.PageNumber} ---");
            System.Console.WriteLine(result.Text);
        }
    }
}
```

لاحظ استخدام `LoadMultiple`؛ كل كائن `page` يعرف `PageNumber` الخاص به، مما يجعل من السهل تسمية الإخراج. هذا النمط شائع عند **استخراج النص من Djvu** للفهرسة أو البحث النصي الكامل.

## دليل Aspose OCR C# – الأخطاء الشائعة وكيفية تجنبها

1. **نسيت ضبط الترخيص** – بدون ترخيص صالح تعمل المكتبة في وضع التقييم، وتضيف علامة مائية إلى الإخراج. استدعِ `License license = new License(); license.SetLicense("Aspose.OCR.lic");` في بداية `Main`.
2. **استخدام تنسيق صورة غير صحيح** – DjVu ليس صورة bitmap أصلية؛ تمرير تدفق تالف سيسبب استثناء `ArgumentException`. احمِل دائمًا عبر `Image.Load` أو `LoadMultiple`.
3. **تجاهل تحرير الموارد** – ملفات DjVu الكبيرة يمكن أن تستهلك عدة جيجابايت من الذاكرة. يضمن نمط `using` الموضح سابقًا تحرير الموارد الأصلية بسرعة.
4. **إعدادات اللغة غير المتطابقة** – إذا كان مستندك بالفرنسية، اضبط `engine.RecognitionSettings.Language = OcrLanguage.French;` لتجنب الأحرف المشوشة.

## اختبار تنفيذك

للتحقق من أن التحويل يعمل كما هو متوقع:

1. شغّل البرنامج باستخدام ملف DjVu معروف (مثلاً صفحة ممسوحة من كتاب ضمن الملكية العامة).
2. قارن مخرجات وحدة التحكم مع النص الأصلي باستخدام أداة diff.
3. اضبط `Resolution` و `UsePreProcessing` حتى يصبح الفرق أقل من الحد المقبول.

إذا كنت بحاجة إلى اختبار آلي، غلف استدعاء OCR في طريقة تُعيد سلسلة نصية، ثم اكتب اختبارات وحدة مع سلاسل فرعية متوقعة.

## ملخص وخطوات مستقبلية

لقد استعرضنا للتو سير عمل كامل لـ **تحويل Djvu إلى نص** باستخدام Aspose OCR في C#. الخطوات الأساسية—تثبيت الحزمة، تهيئة `OcrEngine`، تحميل DjVu، التعرف على المحتوى، وإخراج النتيجة—مغطاة جميعًا مع كود يمكنك نسخه مباشرة إلى مشروعك.

من هنا قد ترغب في:

* **معالجة دفعة** لمجلد كامل من ملفات DjVu وكتابة كل نتيجة إلى ملف `.txt`.
* **إنشاء ملفات PDF قابلة للبحث** عن طريق إرجاع نص OCR إلى Aspose.PDF.
* **دمج مع Azure Functions** لتوفير OCR عند الطلب في السحابة.
* استكشاف **اكتشاف اللغة** لتبديل حزم لغة OCR تلقائيًا.

الحدود لا توجد لها بمجرد أن تتقن أساسيات **التعرف على النص من صورة** و **استخراج النص من Djvu** باستخدام Aspose OCR.

---

*برمجة سعيدة! إذا واجهت أي مشاكل، اترك تعليقًا أدناه—دعنا نحلها معًا.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}