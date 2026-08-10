---
category: general
date: 2026-02-19
description: دليل OCR بلغة C# – تعلم كيفية استخراج النص من الصورة، قراءة نص الصورة،
  تحويل الصورة إلى نص، والتعرف على نص الصورة باستخدام Aspose.OCR في دقائق.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- read image text
- convert image to text
- recognize image text
language: ar
og_description: دروس C# OCR تُظهر لك كيفية استخراج النص من الصورة، قراءة نص الصورة،
  تحويل الصورة إلى نص، والتعرف على نص الصورة باستخدام Aspose OCR.
og_title: دليل c# OCR – استخراج النص من الصور باستخدام Aspose OCR
tags:
- OCR
- C#
- Aspose
title: 'دليل OCR بلغة C#: استخراج النص من الصور باستخدام Aspose OCR'
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# ocr – استخراج النص من الصور باستخدام Aspose OCR

هل تساءلت يومًا كيف **استخراج النص من صورة** بينما تبقى داخل بيئة C# النقية؟ هذا هو بالضبط ما يحله **دليل c# ocr**. في بضع خطوات فقط ستتعلم قراءة نص الصورة، تحويل الصورة إلى نص، وحتى التعرف على نص الصورة بلغات مختلفة باستخدام مكتبة Aspose.OCR.

في هذا الدليل سنستعرض كل ما تحتاجه: من تثبيت حزمة NuGet إلى التعامل مع الترخيص، ضبط اللغة، وطباعة النتائج. في النهاية ستحصل على تطبيق كونسول جاهز للتشغيل يحول أي صورة—مثل فاتورة ممسوحة أو لقطة شاشة—إلى نص قابل للبحث.

## ما ستحتاجه

- .NET 6.0 SDK أو أحدث (الكود يعمل على .NET Framework 4.7+ أيضًا)  
- Visual Studio 2022 (أو أي محرر تفضله)  
- ملف ترخيص Aspose.OCR *اختياري* – المكتبة تعمل في وضع التقييم، لكن الترخيص يزيل العلامات المائية.  
- صورة عينة (مثال: `cyrillic_sample.jpg`) موجودة في مكان ما على القرص.

لا توجد أدوات طرف ثالث أخرى مطلوبة؛ Aspose.OCR يتولى كل المعالجة الثقيلة تحت الغطاء.

![صورة عينة من دليل c# ocr تظهر نصًا سيريليًا](/images/ocr-sample.jpg "دليل c# ocr – صورة عينة لـ OCR")

## دليل c# ocr – إعداد Aspose OCR

أولاً، أضف حزمة Aspose.OCR إلى مشروعك:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، يمكنك أيضًا النقر بزر الماوس الأيمن على المشروع → **Manage NuGet Packages** والبحث عن *Aspose.OCR*.

### لماذا الترخيص مهم

يعمل Aspose.OCR في وضع التقييم لمدة 30 يومًا بدون ترخيص. فئة `License` ببساطة تشير إلى ملف `.lic` الخاص بك؛ بمجرد ضبطه، يتوقف المحرك عن إدراج تذييلات التقييم في الناتج.

```csharp
// Optional: apply your Aspose.OCR license to unlock full features
// new License().SetLicense("Aspose.OCR.lic");
```

إذا تخطيت هذه السطر أثناء التطوير، سيظل OCR يعمل—فقط تذكر أن إشعار التقييم سيظهر في النص المستخرج.

## استخراج النص من الصورة – إنشاء محرك OCR

جوهر أي **دليل c# ocr** هو كائن `OcrEngine`. فهو يجمل كامل خط أنابيب التعرف.

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Step 1: (Optional) Apply your license – see above
        // new License().SetLicense("Aspose.OCR.lic");

        // Step 2: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 3: Choose the language you want to recognize
        // For this demo we use Cyrillic, but you can pick English, Arabic, etc.
        ocrEngine.Language = Language.Cyrillic;

        // Step 4: Run OCR on the target picture
        var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/cyrillic_sample.jpg");

        // Step 5: Output the recognized text to the console
        Console.WriteLine("Recognized text:");
        Console.WriteLine(result.Text);
    }
}
```

### ما الذي يفعله الكود فعليًا

- **إنشاء `OcrEngine`** ينشئ سياق معالجة جديد.  
- **ضبط `Language`** يخبر Aspose بمجموعة الأحرف المتوقعة؛ هذا يحسن الدقة بشكل كبير لأن المحرك يمكنه تطبيق خوارزميات خاصة باللغة.  
- **`RecognizeImage`** يحمل الملف، ينفذ سلسلة من خطوات ما قبل معالجة الصورة (تصحيح الميل، التثبيت الثنائي، إزالة الضوضاء) وأخيرًا يشغل مُعَرِّف الشبكة العصبية.  
- **`result.Text`** يحتوي على تمثيل النص العادي—مثالي لسيناريوهات **تحويل الصورة إلى نص**.

## قراءة نص الصورة – التعامل مع أنواع الملفات المختلفة

Aspose.OCR لا يقتصر على JPEGs. فهو يدعم PNG، BMP، TIFF، وحتى صفحات PDF (كصور). إذا كنت بحاجة لمعالجة دفعة، غلف الاستدعاء في حلقة بسيطة:

```csharp
string[] files = Directory.GetFiles(@"YOUR_DIRECTORY", "*.*", SearchOption.TopDirectoryOnly)
                          .Where(f => f.EndsWith(".jpg") || f.EndsWith(".png") || f.EndsWith(".tif"))
                          .ToArray();

foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(res.Text);
}
```

### حالة حافة: صور فارغة أو تالفة

إذا استلم `RecognizeImage` ملفًا فارغًا أو غير قابل للقراءة، فإنه يرمي `ArgumentException`. حارس سريع يحافظ على صلابة **دليل c# ocr** الخاص بك:

```csharp
if (!File.Exists(file))
{
    Console.WriteLine($"File not found: {file}");
    continue;
}
```

## التعرف على نص الصورة – تحسين الدقة

أحيانًا الإعدادات الافتراضية تفوت بعض الأحرف، خاصةً في المسحات منخفضة التباين. Aspose.OCR يتيح لك تعديل بعض الخيارات:

| الخاصية               | ما تفعله                              | حالة الاستخدام النموذجية |
|------------------------|-------------------------------------------|------------------|
| `ocrEngine.PreprocessingOptions.Deskew` | يدور الصورة لتصحيح الميل | المستندات الممسوحة |
| `ocrEngine.PreprocessingOptions.NoiseRemoval` | يزيل البقع | الصور القديمة |
| `ocrEngine.Language`   | نموذج اللغة (سيريلي، إنجليزي، إلخ) | OCR متعدد اللغات |

مثال على تمكين تصحيح الميل:

```csharp
ocrEngine.PreprocessingOptions.Deskew = true;
```

هذه التعديلات تساعدك على **استخراج النص من صورة** غير محاذاة تمامًا، مما يزيد من معدل نجاح عملية **قراءة نص الصورة**.

## النتيجة المتوقعة

تشغيل الكود العيني على `cyrillic_sample.jpg` (الذي يحتوي على العبارة “Привет мир”) ينتج شيء مشابه:

```
Recognized text:
Привет мир
```

إذا كنت في وضع التقييم، سترى أيضًا سطرًا إضافيًا:

```
--- Evaluation version. Use a licensed copy for production. ---
```

هذا السطر يختفي بمجرد توفير ملف ترخيص صالح.

## الأخطاء الشائعة وكيفية تجنبها

1. **إعداد لغة خاطئ** – استخدام `Language.English` على نص سيريلي سيعيد نصًا غير مفهوم. دائمًا طابق اللغة مع المصدر.  
2. **صور كبيرة** – معالجة صورة بدقة 10 MP قد تكون بطيئة. قلل حجم الصورة أولاً (`Bitmap.Resize`) إذا كانت السرعة أهم من الدقة المثالية.  
3. **اعتماديات مفقودة** – Aspose.OCR يأتي مع ملفات ثنائية أصلية؛ تأكد من أن مجلد الإخراج يحتوي على `Aspose.OCR.Native.dll` (NuGet يتولى ذلك، لكن خطوط بناء مخصصة قد تحتاج إلى خطوة نسخ).

## الخطوات التالية – ما بعد الأساسيات

- **تحويل دفعي**: دمج الحلقة الموضحة سابقًا مع `Task.Run` غير المتزامن لتسريع المعالجة في المجلدات الكبيرة.  
- **تصدير إلى PDF**: بعد **تحويل الصورة إلى نص**، مرر السلسلة إلى مولد PDF (مثل Aspose.PDF) لإنشاء ملفات PDF قابلة للبحث.  
- **دمج مع Azure Functions**: حول منطق OCR إلى نقطة نهاية خالية من الخوادم تعالج التحميلات مباشرة.

كل هذه الإضافات تستمر في موضوع **استخراج النص من صورة** و**قراءة نص الصورة** في تطبيقات العالم الحقيقي.

## الخلاصة

لقد أكملت للتو **دليل c# ocr** الذي يوضح كيفية قراءة نص الصورة، تحويل الصورة إلى نص، والتعرف على نص الصورة باستخدام Aspose.OCR. المثال الكامل القابل للتنفيذ أعلاه يوضح كل خطوة—من الترخيص إلى اختيار اللغة ومعالجة الأخطاء—حتى يمكنك إدراج هذا الكود في أي مشروع .NET والبدء في استخراج النص فورًا.

لا تتردد في تجربة لغات مختلفة، تعديل خيارات ما قبل المعالجة، أو ربط الناتج بقاعدة بيانات لأرشفة قابلة للبحث. إذا واجهت أي مشاكل، فإن وثائق Aspose مرجع قوي، لكن الكود هنا يجب أن يعمل مباشرة في معظم السيناريوهات.

برمجة سعيدة، ولتكن صورك دائمًا قابلة للقراءة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}