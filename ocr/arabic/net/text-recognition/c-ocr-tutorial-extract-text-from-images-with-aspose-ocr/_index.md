---
category: general
date: 2026-02-24
description: دليل C# OCR يوضح كيفية استخراج النص من الصورة باستخدام Aspose OCR – دليل
  كامل خطوة بخطوة لمطوري .NET.
draft: false
keywords:
- c# ocr tutorial
- how to extract text from image
- Aspose OCR C#
- OCR region of interest
- image text extraction C#
language: ar
og_description: دليل C# OCR يوضح كيفية استخراج النص من الصورة باستخدام Aspose OCR
  – دليل كامل خطوة بخطوة لمطوري .NET.
og_title: 'دليل C# OCR: استخراج النص من الصور باستخدام Aspose OCR'
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 'دليل C# OCR: استخراج النص من الصور باستخدام Aspose OCR'
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# OCR – استخراج النص من الصور باستخدام Aspose OCR

هل تساءلت يومًا كيف تستخرج النص من ملفات الصور في تطبيق C#؟ لست وحدك. في العديد من المشاريع الواقعية—مثل ماسحات جوازات السفر، معالجات الفواتير، أو حتى قارئات الإيصالات البسيطة—الحصول على نتائج OCR موثوقة يمثل تحديًا يوميًا.  

هذا **c# ocr tutorial** يشرح لك حلاً عمليًا باستخدام Aspose OCR، موضحًا بالضبط **كيفية استخراج النص من الصورة**، وتحديد نطاق المسح إلى منطقة اهتمام، وعرض النتيجة—كل ذلك في بضع أسطر من الشيفرة.  

سنغطي كل ما تحتاجه: حزمة NuGet، عبارات `using` المطلوبة، إعداد ROI، تكوين الخيارات، وفحص سريع للنتيجة. في النهاية، ستحصل على تطبيق console قابل للتنفيذ يقرأ الاسم من مسح جواز السفر (أو أي صورة أخرى تشير إليها). لا حشو، مجرد إجابة واضحة ومتكاملة يمكنك نسخها ولصقها وتشغيلها.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6+ SDK (أو .NET Framework 4.7+ إذا كنت تفضّل runtime الأقدم)
- Visual Studio 2022 أو أي محرر يدعم C#
- اتصال بالإنترنت لجلب حزمة **Aspose.OCR** من NuGet
- ملف صورة (مثال: `passport_scan.png`) يحتوي على نص قابل للقراءة

> **نصيحة احترافية:** إذا كنت تجرب محليًا، ضع ملف PNG أو JPEG صغير في مجلد اسمه `Images` داخل مشروعك – سيجعل المسار قصيرًا والشيفرة منظمة.

## الخطوة 1: تثبيت Aspose OCR وإضافة المساحات الاسمية

أولًا، نحتاج إلى مكتبة OCR. افتح الطرفية (أو Package Manager Console) وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

بعد تثبيت الحزمة، أضف توجيهات `using` المطلوبة في أعلى ملف `Program.cs`:

```csharp
using Aspose.OCR;          // Core OCR engine
using System.Drawing;     // Rectangle struct for ROI
```

هاتان السطران يمنحانك الوصول إلى `OcrEngine` و`OcrOptions` ونوع `Rectangle` الذي سنستخدمه لتحديد مساحة المسح.

## الخطوة 2: إنشاء كائن OCR Engine

المحرك هو قلب العملية. فكر فيه كـ “العقل” الذي يقرأ البكسلات ويحولها إلى أحرف. تهيئته بسيطة:

```csharp
// Step 2: Instantiate the OCR engine – this object does the heavy lifting.
OcrEngine ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:** يمكن إعادة استخدام كائن `OcrEngine` لعدة صور، مما يوفر الذاكرة ويجنبك فحص الترخيص المتكرر.

## الخطوة 3: تعريف منطقة الاهتمام (ROI)

مسح الصورة عالية الدقة بالكامل قد يكون مضيعة للموارد، خاصةً عندما تعرف بالضبط أين يقع النص (مثلاً حقل الاسم في جواز السفر). بتحديد **منطقة الاهتمام**، تخبر المحرك بتجاهل كل ما خارج المستطيل.

```csharp
// Step 3: Set the ROI – adjust X, Y, Width, Height to match your image layout.
Rectangle regionOfInterest = new Rectangle(150, 300, 800, 200);
```

- **X** و **Y** يمثلان الزاوية العلوية اليسرى للمستطيل.
- **Width** و **Height** يحددان حجم الصندوق.

إذا لم تكن متأكدًا من القيم الدقيقة، يمكنك إجراء اختبار بصري سريع باستخدام أي محرر صور (مثل Paint.NET) لتحديد الإحداثيات.

## الخطوة 4: تكوين خيارات OCR وربط ROI

الآن نربط ROI بكائن `OcrOptions`. يتيح لك هذا الكائن أيضًا تعديل اللغة، سرعة الكشف، وأكثر، لكن في هذا الدرس سنبقيه بسيطًا.

```csharp
// Step 4: Prepare OCR options and assign the ROI we just defined.
OcrOptions ocrOptions = new OcrOptions { Roi = regionOfInterest };
```

> **حالة حافة:** إذا حذفت ROI، سيقوم Aspose OCR بمسح الصورة بالكامل، مما قد يزيد من زمن المعالجة وقد ينتج ضوضاء إضافية في النتيجة.

## الخطوة 5: تشغيل OCR Engine على صورتك

بعد ربط كل شيء، حان الوقت لتعرف النص فعليًا. قدم مسار الصورة والخيارات التي أنشأناها للتو.

```csharp
// Step 5: Perform OCR on the target image using the configured options.
OcrResult ocrResult = ocrEngine.RecognizeImage(
    "Images/passport_scan.png", // Adjust this path to your file location
    ocrOptions);
```

تُعيد الطريقة كائن `OcrResult` يحتوي على السلسلة المستخرجة، درجات الثقة، وحتى المربعات المحيطة بكل كلمة (إذا احتجت إليها لاحقًا).

## الخطوة 6: إخراج النص المستخرج

أخيرًا، اعرض النتيجة. في تطبيق حقيقي قد تخزنها في قاعدة بيانات، لكن في هذا الدرس يكفي إخراجها إلى الـ console.

```csharp
// Step 6: Show the extracted text in the console.
Console.WriteLine("Extracted name: " + ocrResult.Text);
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
Extracted name: JOHN DOE
```

إذا كان الإخراج فارغًا أو مشوشًا، تحقق مرة أخرى من إحداثيات ROI وتأكد من وضوح الصورة المصدر (تباين عالي، تشويش قليل).

## مثال كامل يعمل

فيما يلي ملف `Program.cs` كامل جاهز للترجمة. احفظه في مشروع console، ضع صورتك في مجلد `Images`، ثم اضغط **F5**.

```csharp
using Aspose.OCR;
using System.Drawing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2: Define the region of interest (ROI) where the text is expected
            // (x, y, width, height) – adjust these values for your own image
            Rectangle regionOfInterest = new Rectangle(150, 300, 800, 200);

            // Step 3: Prepare OCR options and assign the ROI
            OcrOptions ocrOptions = new OcrOptions { Roi = regionOfInterest };

            // Step 4: Perform OCR on the target image using the configured options
            OcrResult ocrResult = ocrEngine.RecognizeImage(
                "Images/passport_scan.png",
                ocrOptions);

            // Step 5: Display the extracted text
            Console.WriteLine("Extracted name: " + ocrResult.Text);
        }
    }
}
```

> **الإخراج المتوقع:**  
> `Extracted name: JOHN DOE` (أو أي نص موجود في ROI المحددة).

## أسئلة شائعة وحالات حافة

### ماذا لو كانت صوري بصيغة مختلفة؟

يدعم Aspose OCR PNG، JPEG، BMP، TIFF، وحتى PDF. فقط غير امتداد الملف في المسار؛ سيكتشف المحرك الصيغة تلقائيًا.

### هل يمكن معالجة عدة صور داخل حلقة؟

بالطبع. يمكن إعادة استخدام `OcrEngine`:

```csharp
foreach (var file in Directory.GetFiles("Images", "*.png"))
{
    var result = ocrEngine.RecognizeImage(file, ocrOptions);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text}");
}
```

### كيف أحسن الدقة للغات غير اللاتينية؟

حدد خاصية اللغة في `OcrOptions`:

```csharp
ocrOptions.Language = Language.English; // or Language.Russian, Language.ChineseSimplified, etc.
```

### ماذا لو كان ROI غير صحيح وفقدت النص؟

يمكنك إما تكبير المستطيل أو حذف ROI تمامًا لتمكين المحرك من مسح الصورة بالكامل. ضع في اعتبارك أن مسح الصورة الكاملة قد يزيد من زمن المعالجة.

## نصائح احترافية لتجربة سلسة

- **احتفظ بالمحرك في الذاكرة:** إنشاء `OcrEngine` جديد لكل صورة يضيف عبئًا. حافظ على كائن واحد طوال مدة تشغيل التطبيق.
- **معالجة مسبقة للصورة:** خطوات بسيطة مثل تحويلها إلى تدرج رمادي أو زيادة التباين يمكن أن تعزز معدلات التعرف بشكل كبير.
- **التعامل مع النتائج الفارغة:** دائمًا افحص `ocrResult?.Text` قبل استخدامها لتجنب `NullReferenceException`.
- **الترخيص مهم:** النسخة المجانية تضيف علامة مائية بعد أول 200 حرف. سجّل ترخيص تجريبي أو تجاري إذا كنت تحتاج مخرجات جاهزة للإنتاج.

## الخطوات التالية

الآن بعد أن أتقنت أساسيات **c# ocr tutorial**، فكر في استكشاف:

- **كيفية استخراج النص من الصور** دفعةً واحدة (معالجة دفعات)
- استخدام **Aspose OCR** لاكتشاف الجداول أو البيانات المهيكلة
- دمج نتيجة OCR مع قاعدة بيانات أو واجهة برمجة تطبيقات ويب
- الجمع بين OCR ومكتبات **معالجة الصور** مثل `OpenCvSharp`

كل من هذه المواضيع يبني على الأساس الذي أنشأته، مما يتيح لك تحويل المسحات الخام إلى بيانات قابلة للبحث والعمل.

---

*هل أنت مستعد لنشر هذا في بيئة الإنتاج؟ احصل على الشيفرة الكاملة من مستودعي على GitHub، عدّل ROI لتناسب مستنداتك، وشاهد النص يظهر كالسحر.*  

برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}