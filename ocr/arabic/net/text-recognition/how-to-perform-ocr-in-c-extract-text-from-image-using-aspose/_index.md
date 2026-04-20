---
category: general
date: 2026-02-16
description: كيفية تنفيذ OCR في C# بسرعة – تعلم استخراج النص من الصورة باستخدام مكتبة
  Aspose OCR في بضع خطوات بسيطة.
draft: false
keywords:
- how to perform OCR
- extract text from image
- Aspose OCR C#
- OCR JSON output
- image text extraction
language: ar
og_description: كيف تقوم بتنفيذ OCR في C#؟ اتبع هذا الدليل خطوة بخطوة لاستخراج النص
  من الصورة باستخدام Aspose OCR والحصول على نتائج بصيغة JSON.
og_title: كيفية تنفيذ OCR في C# – دليل سريع
tags:
- OCR
- C#
- Aspose
- Image Processing
title: كيفية تنفيذ OCR في C# – استخراج النص من الصورة باستخدام Aspose OCR
url: /ar/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في C# – استخراج النص من الصورة باستخدام Aspose OCR

هل تساءلت يومًا **كيف تقوم بتنفيذ OCR** في C# دون أن تشعر بالإحباط؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى استخراج النص من النماذج الممسوحة ضوئيًا أو الإيصالات أو الملاحظات المكتوبة يدويًا. الخبر السار؟ مع Aspose OCR يمكنك **استخراج النص من الصورة** في بضع أسطر من الشيفرة فقط.

في هذا الدرس سنستعرض مثالًا كاملاً جاهزًا للتنفيذ يوضح لك بالضبط كيفية تحميل نموذج اللغة، إمداد الصورة، تشغيل محرك التعرف، وتحويل النتيجة إلى JSON. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع .NET، بالإضافة إلى بعض النصائح العملية للسيناريوهات الواقعية.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل على .NET Framework أيضًا، لكن يُفضَّل .NET 6+)
- حزمة NuGet صالحة لـ Aspose.OCR (`Install-Package Aspose.OCR`)
- ملف صورة (JPEG, PNG, BMP, إلخ) يحتوي على النص الذي تريد قراءته
- بيئة تطوير C# أساسية (Visual Studio, Rider, أو VS Code)

هذا كل ما تحتاجه—لا محركات OCR إضافية، لا ملفات DLL أصلية، مجرد مكتبة مُدارة نظيفة.

## الخطوة 1: إنشاء كائن محرك OCR – كيفية تنفيذ OCR

الأول الذي تحتاجه هو كائن `OcrEngine`. فكر فيه كالعقل الذي سيتولى الأعمال الثقيلة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **لماذا هذه الخطوة مهمة:** الـ `OcrEngine` يضم جميع خيارات التكوين. بدون هذا الكائن لا يمكنك إخبار المكتبة أي لغة تستخدم أو أين تجد الصورة.

## الخطوة 2: تحميل نموذج اللغة – استخراج النص من الصورة

تأتي Aspose OCR مع عدة حزم لغات. بالنسبة لمعظم المستندات الإنجليزية ستحمّل النموذج المدمج للغة الإنجليزية.

```csharp
// Load the English language model
ocrEngine.LoadLanguage(LanguageModel.English);
```

> **نصيحة احترافية:** إذا كنت بحاجة إلى التعرف على الفرنسية أو الألمانية أو لغة مخصصة، استبدل `LanguageModel.English` بالقيمة المناسبة من الـ enum أو حمّل ملف نموذج مخصص.

## الخطوة 3: توفير الصورة للمعالجة – كيفية تنفيذ OCR

الآن وجه المحرك إلى الملف الذي تريد قراءته. المساعد `ImageStream.FromFile` يقرأ الصورة إلى صيغة يفهمها محرك OCR.

```csharp
// Supply the image (replace the path with your own file location)
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.jpg");
```

> **حالة حافة:** الصور الكبيرة (>5 ميغابايت) قد تُبطئ المعالجة. فكر في تغيير حجمها أو ضغطها قبل إمدادها للمحرك.

## الخطوة 4: تشغيل التعرف – استخراج النص من الصورة

بعد إعداد كل شيء، يمكنك أخيرًا تشغيل عملية OCR. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على النص، الصناديق المحيطة، ودرجات الثقة.

```csharp
// Perform OCR and capture the result
OcrResult ocrResult = ocrEngine.Recognize();
```

> **ما الذي يحدث خلف الكواليس؟** يعمل المحرك على شبكة عصبية تم تدريبها على ملايين الأحرف، ثم يطابق كل حرف مكتشف مع نص Unicode.

## الخطوة 5: تحويل النتيجة إلى JSON – كيفية تنفيذ OCR

معظم واجهات برمجة التطبيقات الحديثة تتوقع JSON، لذا لنقوم بتسلسل النتيجة. طريقة الامتداد `ToJson` تعطيك سلسلة منسقة بشكل جميل.

```csharp
// Serialize the OCR result to JSON
string jsonResult = ocrResult.ToJson();
```

مثال على حمولة JSON شائعة يبدو هكذا (مقتطع للوضوح):

```json
{
  "Text": "Invoice #12345\nDate: 01/02/2026\nTotal: $250.00",
  "Words": [
    {
      "Value": "Invoice",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 80, "Height": 20 },
      "Confidence": 0.98
    },
    // ... more words ...
  ]
}
```

> **لماذا JSON؟** إنه مستقل عن اللغة، سهل التسجيل، ومثالي لإرساله إلى خدمات لاحقة مثل Elasticsearch أو واجهة REST.

## الخطوة 6: إخراج JSON – استخراج النص من الصورة

أخيرًا، اكتب الـ JSON إلى وحدة التحكم (أو ملف، أو قاعدة بيانات—اختيارك).

```csharp
// Print the JSON result to the console
Console.WriteLine(jsonResult);
```

تشغيل البرنامج يجب أن يعرض بنية JSON الكاملة، مؤكدًا أنك نجحت في **استخراج النص من الصورة**.

## مثال كامل يعمل

فيما يلي الشيفرة الكاملة التي يمكنك نسخها ولصقها في مشروع وحدة تحكم جديد. لا توجد أجزاء مفقودة—كل ما تحتاجه موجود هنا.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2: Load the English language model for recognition
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Step 3: Provide the image to be processed
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.jpg");

            // Step 4: Perform OCR on the image
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 5: Convert the recognition result to JSON (includes text, bounding boxes, confidence scores)
            string jsonResult = ocrResult.ToJson();

            // Step 6: Output the JSON result
            Console.WriteLine(jsonResult);
        }
    }
}
```

> **الإخراج المتوقع:** سلسلة JSON تحتوي على النص المعترف به، صندوق كل كلمة، وقيم الثقة. إذا كانت الصورة واضحة ونموذج اللغة متطابق، عادةً ما تكون درجات الثقة فوق 0.90.

## أسئلة شائعة ومشكلات محتملة

- **ماذا لو كانت الصورة مائلة؟**  
  يمكن لـ Aspose OCR اكتشاف الاتجاه تلقائيًا، لكن للحصول على أفضل النتائج قد تحتاج إلى تدوير الصورة مسبقًا باستخدام `System.Drawing` أو `ImageSharp` قبل تمريرها إلى المحرك.

- **هل يمكنني معالجة ملفات PDF مباشرة؟**  
  ليس مباشرة. حوّل كل صفحة PDF إلى صورة (مثلاً باستخدام Aspose.PDF) ثم مرّر تلك الصور إلى محرك OCR.

- **كيف أتعامل مع النماذج متعددة الصفحات؟**  
  كرّر العملية لكل صورة صفحة، شغّل نفس الخطوات، واجمع نتائج JSON في مجموعة واحدة.

- **هل هناك طريقة لتقليل الإخراج إلى نص عادي فقط؟**  
  نعم—استخدم الخاصية `ocrResult.Text` بدلاً من `ToJson()` إذا كنت تحتاج السلسلة المتصلة فقط.

## نصائح احترافية لـ OCR جاهز للإنتاج

1. **تخزين نماذج اللغة مؤقتًا** – تحميل النموذج رخيص، لكن إذا كنت تعالج مئات الصور في الثانية، احتفظ بمثيل واحد من `OcrEngine` حيًا بدلاً من إنشائه في كل مرة.
2. **ضبط عتبات الثقة** – استبعد الكلمات التي قيمتها `Confidence < 0.80` لتقليل الضوضاء.
3. **المعالجة الدفعية** – للأحمال الكبيرة، فكر في وضع مسارات الصور في طابور ومعالجتها بشكل غير متزامن باستخدام `Task.Run`.
4. **التسجيل** – احفظ الـ JSON الخام جنبًا إلى جنب مع الصورة الأصلية لأغراض التدقيق؛ فهو لا يقدر بثمن عند تصحيح الأخطاء في التعرف.

## الخلاصة

أصبح لديك الآن حل واضح من البداية إلى النهاية لـ **كيفية تنفيذ OCR** في C# و**استخراج النص من الصورة** باستخدام مكتبة Aspose OCR. يوضح المثال إنشاء المحرك، تحميل اللغة، إمداد الصورة، التعرف، تسلسل JSON، والإخراج—كل ذلك في برنامج واحد قابل للتنفيذ.

ما الخطوة التالية؟ جرّب استبدال نموذج الإنجليزية بنموذج لغة آخر، جرب صيغ صور مختلفة، أو دمج حمولة JSON في فهرس بحث. السماء هي الحد، ومع هذه اللبنات الأساسية أنت جاهز لمواجهة أي تحدٍ لاستخراج النصوص.

برمجة سعيدة، ولتكن نتائج OCR دقيقة دائمًا! 

![Diagram illustrating how to perform OCR in C# with Aspose OCR library](https://example.com/ocr-diagram.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}