---
category: general
date: 2026-03-18
description: إنشاء ملف PDF قابل للبحث باستخدام Aspose OCR في C#. تحويل الصورة إلى
  PDF، إضافة طبقة نص OCR، وكتابة بايتات PDF إلى ملف في بضع خطوات سهلة.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- add ocr text layer
- write pdf bytes to file
language: ar
og_description: أنشئ ملف PDF قابل للبحث بسرعة باستخدام Aspose OCR في C#. تعلّم كيفية
  تحويل الصورة إلى PDF، وإضافة طبقة نص OCR، وكتابة بايتات PDF إلى ملف.
og_title: إنشاء ملف PDF قابل للبحث من صورة – دليل OCR سريع بلغة C#
tags:
- OCR
- PDF
- C#
- Aspose
title: إنشاء ملف PDF قابل للبحث من صورة باستخدام OCR – دليل C#
url: /ar/net/text-recognition/create-searchable-pdf-from-image-with-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث من صورة باستخدام OCR – دليل C#

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من صورة ممسوحة ضوئياً؟ مع Aspose OCR يمكنك القيام بذلك ببضع أسطر فقط، دون الحاجة إلى مكتبات ثقيلة. في هذا الدرس سنقوم **بتحويل الصورة إلى PDF**، وإضافة **طبقة نص OCR** فوقها، وأخيراً **كتابة بايتات PDF إلى ملف** لتنتج وثيقة PDF/A‑2b متوافقة مع المعايير يمكن للمستخدمين البحث فيها.

إذا كنت تتساءل لماذا تحتاج إلى PDF قابل للبحث بدلاً من ملف صورة فقط، ففكر في تجربة المستخدم: PDF القابل للبحث يتيح للناس نسخ النص، تحديده، وفهرسته—مفيد للأرشيفات، المستندات القانونية، أو أي سير عمل يحتاج إلى استخراج النص لاحقاً. هيا نبدأ.

## ما ستحتاجه

- .NET 6 أو أحدث (الكود يعمل أيضاً على .NET Framework 4.7+)
- حزمة NuGet الخاصة بـ Aspose.OCR (`Aspose.OCR` الإصدار 23.10 أو أحدث)
- صورة نقطية (`.png`، `.jpg`، إلخ) تريد تحويلها إلى PDF قابل للبحث
- قليل من المعرفة بـ C#—ليس شيئاً معقداً، فقط الأساسيات

هذا كل شيء. لا أدوات خارجية، لا محولات إضافية. كل ما يلزم يتم التعامل معه بواسطة محرك Aspose OCR.

## إنشاء PDF قابل للبحث – نظرة عامة

قبل الغوص في الكود، لنستعرض العملية:

1. **Instantiate** محرك OCR – هذا الكائن يعرف كيفية قراءة النص من الصور.  
2. **Load** صورة المصدر – سنزود المحرك بـ `ImageStream`.  
3. **Configure** خيارات حفظ PDF/A‑2b – هذا يخبر Aspose بدمج النص المُعترف به كطبقة مخفية.  
4. **Run** الـ OCR و **capture** بايتات PDF الناتجة.  
5. **Write** تلك البايتات إلى القرص، لإنتاج ملف PDF قابل للبحث النهائي.

كل خطوة من هذه الخطوات تقابل سطر أو سطرين من C#، مما يجعل سير العمل بأكمله يبدو كبرنامج نصي صغير بدلاً من مشروع ضخم.

## الخطوة 1: تحويل الصورة إلى PDF – تحميل الصورة

أولاً: نحتاج إلى إعطاء محرك OCR شيئًا ليقرأه. المساعد `ImageStream.FromFile` يحمل الملف إلى تدفق يمكن لـ Aspose معالجته.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

// 1️⃣ Load the source image you want to turn into a searchable PDF
ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
```

> **نصيحة احترافية:** حافظ على دقة صورتك 300 dpi أو أعلى؛ دقة OCR تنخفض بشكل كبير في المسحات منخفضة الدقة.

## الخطوة 2: التعرف على النص من الصورة وإضافة طبقة نص OCR

الآن ننشئ محرك OCR ونخبره بالتعرف على النص. السحر يحدث عندما نربط نتيجة التعرف مع `PdfSaveOptions` التي تحتوي على `IncludeTextLayer = true`. هذه العلامة تجبر Aspose على تضمين الأحرف المستخرجة كطبقة نصية غير مرئية، وهذا ما يجعل PDF قابلًا للبحث.

```csharp
// 2️⃣ Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// 3️⃣ Set up PDF/A‑2b save options – includes the hidden text layer
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
{
    PdfCompliance = PdfCompliance.PdfA2b, // ensures PDF/A‑2b compliance
    IncludeTextLayer = true               // this is the key for searchable PDFs
};
```

لماذا PDF/A‑2b؟ إنه تنسيق أرشيفي معيار ISO يضمن الحفظ طويل الأمد، والأهم بالنسبة لنا، يجبر PDF على احتواء طبقة نصية قابلة للبحث. إذا لم تكن بحاجة إلى الامتثال للأرشفة، يمكنك حذف `PdfCompliance` تمامًا، لكن الاحتفاظ به لا يكلفك شيئًا.

## الخطوة 3: كتابة بايتات PDF إلى ملف – حفظ النتيجة

مع المحرك جاهزًا والخيارات مضبوطة، نقوم بتشغيل التعرف ونطلب فورًا من Aspose أن يعطينا الـ PDF كـ `byte[]`. ثم نكتب تلك البايتات إلى القرص باستخدام `File.WriteAllBytes`. بسيط، لكنه قوي.

```csharp
// 4️⃣ Perform OCR on the image and get the PDF bytes
byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

// 5️⃣ Write the PDF/A‑2b file to the output location
System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
Console.WriteLine("PDF/A‑2b file created – you now have a searchable PDF!");
```

سطر `Console.WriteLine` اختياري، لكنه يمنحك تغذية راجعة فورية عندما تشغل البرنامج من الطرفية.

## مثال كامل يعمل

نجمع كل شيء معًا، إليك البرنامج الكامل الجاهز للتنفيذ. انسخه إلى مشروع وحدة تحكم جديد، استبدل `YOUR_DIRECTORY` بمسار فعلي، ثم اضغط **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

class PdfA2bDemo
{
    static void Main()
    {
        // Step 1: Load the source image
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");

        // Step 2: Create OCR engine and configure PDF/A‑2b options
        OcrEngine ocrEngine = new OcrEngine();
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
        {
            PdfCompliance = PdfCompliance.PdfA2b,
            IncludeTextLayer = true
        };

        // Step 3: Recognize and save as PDF bytes
        byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

        // Step 4: Write the bytes to a searchable PDF file
        System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
        Console.WriteLine("PDF/A‑2b file created.");
    }
}
```

### النتيجة المتوقعة

- يظهر ملف باسم `output.pdf` في المجلد الذي حددته.  
- افتحه في Adobe Acrobat Reader أو أي عارض PDF وحاول تحديد النص—إذا استطعت نسخ الكلمات، فقد نجحت في **إنشاء PDF قابل للبحث**.  
- الوثيقة ستمر أيضًا أدوات التحقق من PDF/A‑2b لأنها استخدمت العلامة الصحيحة للامتثال.

## أسئلة شائعة وحالات خاصة

**ماذا لو كانت صورتي تحتوي على عدة صفحات؟**  
قم بلف كل صفحة في `ImageStream` خاص بها ومررها تسلسليًا إلى `OcrEngine`. سيقوم Aspose بدمج الصفحات تلقائيًا في PDF واحد.

**هل يمكنني تغيير لغة OCR؟**  
بالطبع. اضبط `ocrEngine.Language = Language.English;` (أو أي لغة مدعومة) قبل استدعاء `Recognize`.

**ماذا عن استهلاك الذاكرة للملفات الضخمة؟**  
إذا كنت تعالج مسحات بحجم جيجابايت، فكر في بث النتيجة مباشرة إلى `FileStream` بدلاً من الاحتفاظ بـ `byte[]` بالكامل في الذاكرة:

```csharp
using (var file = new FileStream("output.pdf", FileMode.Create))
{
    ocrEngine.Recognize(image).Save(pdfSaveOptions, file);
}
```

**هل أحتاج إلى رخصة؟**  
Aspose تقدم نسخة تجريبية مجانية بدون علامة مائية. للاستخدام الإنتاجي، اشترِ رخصة لإزالة بانر التقييم وفتح جميع المميزات.

## نصائح لتحسين دقة OCR

- **Pre‑process** الصورة: تصحيح الميل، إزالة البقع، وزيادة التباين.  
- **Use lossless formats** مثل PNG؛ قد تشوش عيوب ضغط JPEG على المحرك.  
- **Avoid colored backgrounds**؛ الخلفية البيضاء البسيطة تعطي أفضل النتائج.

## الخطوات التالية

الآن بعد أن يمكنك **إنشاء PDF قابل للبحث**، قد ترغب في:

- **Batch process** مجلد من الصور باستخدام `Directory.GetFiles`.  
- **Extract the hidden text** لاحقاً باستخدام واجهات `PdfDocument` للفهرسة.  
- **Combine OCR with digital signatures** لإنشاء أرشيفات مقاومة للعبث.  

جميع هذه الأفكار تبنى على النمط الأساسي الذي غطيناه: تحميل، التعرف، التكوين، الحفظ.

*هل أنت مستعد لتحويل أرشيفاتك الممسوحة إلى PDF قابلة للبحث؟ احصل على الكود، وجهه إلى صورك، ودع Aspose يتولى العمل الشاق. برمجة سعيدة!*

![مثال على إنشاء PDF قابل للبحث](/images/create-searchable-pdf.png "توضيح PDF قابل للبحث تم إنشاؤه من صورة")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}