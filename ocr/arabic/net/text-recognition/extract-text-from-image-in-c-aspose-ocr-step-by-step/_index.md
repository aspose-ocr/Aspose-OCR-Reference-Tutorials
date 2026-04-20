---
category: general
date: 2026-03-05
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية قراءة ملف
  الصورة في C#، تحويل DJVU إلى نص، والحصول على نتائج OCR من الصورة إلى سلسلة بسرعة.
draft: false
keywords:
- extract text from image
- read image file c#
- convert djvu to text
- ocr image to string
- recognize text from djvu
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدليل
  كيفية قراءة ملف الصورة في C#، وتحويل DJVU إلى نص، ومعالجة صورة OCR إلى سلسلة بسهولة.
og_title: استخراج النص من صورة في C# – دليل Aspose OCR الكامل
tags:
- Aspose OCR
- C#
- Image Processing
title: استخراج النص من الصورة في C# – خطوة بخطوة باستخدام Aspose OCR
url: /ar/net/text-recognition/extract-text-from-image-in-c-aspose-ocr-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة في C# – دليل Aspose OCR الكامل

هل احتجت يومًا إلى **استخراج النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة ستعطيك نتائج موثوقة؟ ربما لديك مجموعة من مسحات DJVU وتريد النص العادي فقط دون العبث بأدوات الطرف الثالث. في هذا الدرس سنحل هذه المشكلة خلال دقائق قليلة باستخدام Aspose OCR لـ .NET.

سنستعرض كيفية قراءة ملف صورة في C#، وتحويل مستند DJVU إلى نص، وتحويل أي صورة OCR إلى سلسلة نظيفة. في النهاية ستحصل على تطبيق console جاهز للتشغيل يطبع النص المعترف به إلى وحدة التحكم. لا روابط غامضة مثل “انظر الوثائق”—فقط حل كامل يمكن نسخه ولصقه.

## ما ستحتاجه

- **.NET 6.0** أو أحدث (الكود يعمل على .NET Framework 4.6+ أيضًا).  
- حزمة NuGet **Aspose.OCR for .NET** (رخصة التجربة المجانية تعمل للاختبار).  
- ملف DJVU أو أي صورة مدعومة (PNG، JPEG، BMP، إلخ).  
- Visual Studio، Rider، أو محرّكك المفضّل.

إذا كنت تفتقد أيًا من هذه المتطلبات، فقط قم بتثبيت حزمة NuGet:

```bash
dotnet add package Aspose.OCR
```

هذا كل ما يلزم للإعداد. هيا نبدأ.

## الخطوة 1: تهيئة محرك OCR – استخراج النص من الصورة

أول شيء تقوم به هو إنشاء نسخة من `OcrEngine`. فكر فيه كالعقل الذي سيقرأ البكسلات ويحولها إلى أحرف.

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

لماذا ننشئ المحرك *قبل* تحميل الملف؟ تصميم Aspose يفصل بين الإعداد (مثل الترخيص) وبيانات الصورة الفعلية، بحيث يمكنك إعادة استخدام نفس المحرك لعدة ملفات دون إعادة إنشاء الكائنات—وهو تحسين بسيط في الأداء.

## الخطوة 2: تطبيق رخصة Aspose OCR الخاصة بك (اختياري لكن موصى به)

إذا كان لديك رخصة تجارية، قم بتعيينها الآن. تخطي هذه الخطوة يُجبر الوضع التجريبي، الذي يضيف علامة مائية إلى الناتج ويحدّ من عدد الصفحات.

```csharp
        // Apply license – remove this line if you’re using the free trial
        ocrEngine.SetLicense("Aspose.OCR.lic");
```

**نصيحة احترافية:** احفظ ملف الرخصة خارج نظام التحكم بالمصادر (مثلاً في متغيّر بيئي) لتجنب الالتزام العرضي.

## الخطوة 3: تحميل الصورة – قراءة ملف الصورة في C# بسهولة

يمكن لـ Aspose قراءة العديد من الصيغ، بما في ذلك صيغة DJVU النادرة. سنستخدم المساعد `ImageStream.FromFile` لتحميل الملف إلى المحرك.

```csharp
        // Load the image (DJVU, PNG, JPEG, etc.)
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.djvu");
```

إذا كنت تفضّل العمل مع `byte[]` (مثلاً عندما تأتي الصورة من قاعدة بيانات)، يمكنك استخدام `ImageStream.FromBytes(byteArray)` بدلاً من ذلك. هذه المرونة مفيدة عندما تحتاج إلى **قراءة ملف صورة C#** من تدفق بدلاً من القرص.

## الخطوة 4: تنفيذ OCR – تحويل صورة OCR إلى سلسلة في استدعاء واحد

الآن يحدث السحر. استدعاء `Recognize()` يشغّل محرك OCR ويعيد `RecognitionResult` يحتوي على النص المستخرج، درجات الثقة، وأكثر.

```csharp
        // Run OCR and get the result
        var result = ocrEngine.Recognize();

        // Extract plain text
        string recognizedText = result.Text;
```

لماذا لا نستدعي مباشرة `Recognize().Text`؟ تقسيم الاستدعاء يتيح لك فحص `result.Confidence` أو `result.Regions` إذا احتجت إلى بيانات أكثر تفصيلاً لاحقًا—مفيد للتصحيح أو بناء واجهة تُظهر الكلمات ذات الثقة المنخفضة.

## الخطوة 5: عرض النص المستخرج – النتيجة النهائية

أخيرًا، اكتب النص إلى وحدة التحكم. في تطبيق حقيقي قد تكتب إلى ملف، قاعدة بيانات، أو ترسله عبر API.

```csharp
        // Show the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

**الناتج المتوقع** (مقتطع للاختصار):

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

إذا لم يتمكن محرك OCR من التعرف على أي حرف، فإن `recognizedText` ستكون سلسلة فارغة. في هذه الحالة، تحقق مرة أخرى من جودة الصورة أو جرّب تعديل إعدادات لغة المحرك (مثلاً، `ocrEngine.Language = Language.English;`).

## تحويل DJVU إلى نص – التعرف على النص من DJVU دفعيًا

قد يكون لديك العشرات من ملفات DJVU للمعالجة. ضع المنطق السابق داخل حلقة:

```csharp
string[] files = Directory.GetFiles("YOUR_DIRECTORY", "*.djvu");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    string text = ocrEngine.Recognize().Text;
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), text);
    Console.WriteLine($"Converted {Path.GetFileName(file)} → {Path.GetFileNameWithoutExtension(file)}.txt");
}
```

هذا المقتطف **يحوّل DJVU إلى نص** تلقائيًا، وينشئ ملف `.txt` بجوار كل مصدر. إنها طريقة سريعة لبناء أرشيف قابل للبحث من المستندات الممسوحة ضوئيًا القديمة.

## معالجة الحالات الخاصة – ماذا لو كانت الصورة مشوشة؟

تنخفض دقة OCR عندما تكون الصورة غير واضحة، ذات تباين منخفض، أو تحتوي على خلفيات ملونة. يوفر Aspose OCR خيارات ما قبل المعالجة:

```csharp
// Example: Binarize the image to improve contrast
ocrEngine.Image = ImageProcessing.Binarize(ocrEngine.Image, threshold: 128);
```

بدلاً من ذلك، يمكنك ضبط المحرك لاكتشاف اللغة تلقائيًا:

```csharp
ocrEngine.Language = Language.Detect; // Detects language based on content
```

هذه التعديلات غالبًا ما تحول نتيجة بدقة 60 % إلى 95 %. جرّب أساليب `Threshold`، `Denoise`، أو `Deskew` إذا واجهت مشاكل.

## مثال كامل يعمل – نسخ، لصق، تشغيل

فيما يلي البرنامج الكامل، جاهز للتجميع. استبدل `"YOUR_DIRECTORY/input.djvu"` بالمسار إلى ملفك وتأكد من أن ملف الرخصة قابل للوصول.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Apply license (optional)
        // ocrEngine.SetLicense("Aspose.OCR.lic"); // Uncomment if you have a license

        // 3️⃣ Load the image (DJVU, PNG, JPEG, etc.)
        string imagePath = "YOUR_DIRECTORY/input.djvu";
        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 4️⃣ Perform OCR
        var result = ocrEngine.Recognize();
        string recognizedText = result.Text;

        // 5️⃣ Output the text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

شغّله باستخدام:

```bash
dotnet run
```

يجب أن ترى النص المستخرج يُطبع إلى وحدة التحكم، تمامًا كما هو موضح في المثال السابق.

## أسئلة شائعة وملاحظات

- **هل يعمل هذا مع ملفات PDF؟**  
  ليس مباشرة. يتعامل Aspose OCR مع الصور النقطية؛ بالنسبة للـ PDF يجب أولاً تحويل كل صفحة إلى صورة (مثلاً باستخدام Aspose.PDF) ثم تمرير تلك الصور إلى محرك OCR.

- **ماذا لو احتجت لمعالجة دفعة كبيرة على خادم؟**  
  أنشئ **محركًا واحدًا** `OcrEngine` وأعد استخدامه عبر الخيوط. المحرك آمن للقراءة المتعددة، لكن يجب تجنّب مشاركة نفس كائن `Image` في وقت واحد.

- **هل يمكنني استخراج نص منسق (خطوط، أحجام)؟**  
  يُعيد Aspose OCR نصًا عاديًا Unicode فقط. لاستخراج يحافظ على التخطيط تحتاج إلى حل أكثر تقدمًا مثل OCR‑ML أو مكتبة PDF تحتفظ بالتخطيط.

## الخطوات التالية – توسيع سير العمل

الآن بعد أن يمكنك **استخراج النص من الصورة** بثقة، فكر في:

- تخزين النتائج في Elasticsearch للبحث النصي الكامل.  
- إمداد النص إلى نموذج لغة للتلخيص.  
- إضافة واجهة مستخدم بسيطة باستخدام ASP.NET Core لتحميل الملفات وعرض نتائج OCR فورًا.

كل هذه تعتمد على نفس الكود الأساسي الذي غطيناه للتو، لذا أنت في موقع جيد لتوسيع الحل.

---

### ملخص سريع

- **قمنا بتهيئة** `OcrEngine` (قلب Aspose OCR).  
- تطبيق **رخصة** لفتح جميع الميزات.  
- **تحميل** ملف DJVU باستخدام `ImageStream.FromFile`.  
- استدعينا `Recognize()` للحصول على نتيجة **ocr image to string**.  
- طبعنا **النص المستخرج** إلى وحدة التحكم.  

هذه هي الوصفة الكاملة لتحويل أي صورة مدعومة—بما في ذلك DJVU—إلى نص قابل للبحث باستخدام C#.

لا تتردد في تجربة صيغ صور مختلفة، تعديل إعدادات ما قبل المعالجة، أو ربط هذا الكود مع مكتبات Aspose أخرى. إذا واجهت مشكلة، اترك تعليقًا أدناه—برمجة سعيدة!  

![extract text from image example](/images/ocr-example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}