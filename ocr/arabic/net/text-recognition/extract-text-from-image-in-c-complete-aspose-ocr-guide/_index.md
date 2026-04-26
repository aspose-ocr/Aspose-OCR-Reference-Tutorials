---
category: general
date: 2026-04-26
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية التعرف على
  النص من ملف JPG، تحويل JPG إلى نص، وتحميل الصورة للتعرف الضوئي على الأحرف في دقائق.
draft: false
keywords:
- extract text from image
- recognize text from jpg
- convert jpg to text
- how to recognize text
- load image for ocr
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR. يوضح هذا الدرس كيفية التعرف
  على النص من ملف JPG، تحويل JPG إلى نص، وتحميل الصورة للتعرف الضوئي على الأحرف.
og_title: استخراج النص من الصورة في C# – دليل Aspose OCR الكامل
tags:
- C#
- OCR
- Aspose
- Image Processing
title: استخراج النص من الصورة في C# – دليل Aspose OCR الكامل
url: /ar/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة في C# – دليل Aspose OCR الكامل

هل احتجت يوماً إلى **استخراج النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة ستتيح لك ذلك دون إعدادات معقدة؟ لست وحدك. في كثير من المشاريع نحصل على مجموعة من لقطات JPG والخطوة التالية هي تحويل تلك البكسلات إلى سلاسل قابلة للبحث.  

في هذا الدرس سنستعرض مثالًا عمليًا يوضح **كيفية التعرف على النص** من ملف JPG، **تحويل JPG إلى نص**، و**تحميل الصورة للـ OCR** باستخدام واجهة Aspose OCR البسيطة في C#. في النهاية ستحصل على برنامج جاهز للتنفيذ يطبع النص المستخرج على وحدة التحكم.

## ما ستتعلمه

- كيفية تثبيت وإضافة مرجع حزمة Aspose OCR عبر NuGet.  
- التسلسل الدقيق للنداءات المطلوبة **لاستخراج النص من ملفات الصورة**.  
- لماذا من المهم ضبط المحرك على وضع التقييم للتجارب السريعة.  
- الأخطاء الشائعة (مثل صيغ الصور غير المدعومة) وكيفية تجنبها.  
- كيفية التحقق من أن نتيجة الـ OCR تطابق الصورة الأصلية.

لا تحتاج إلى خبرة سابقة في الـ OCR—فقط خلفية أساسية في C# و .NET 6 أو أحدث مثبتة على جهازك.

## المتطلبات المسبقة

| المتطلب | السبب |
|-------------|--------|
| .NET 6 SDK (أو أحدث) | يوفر بيئة التشغيل لتطبيق وحدة التحكم C#. |
| Visual Studio 2022 (أو VS Code) | يجعل تحرير الكود وتصحيح الأخطاء سهلًا. |
| حزمة Aspose.OCR NuGet | المكتبة التي تقوم فعليًا بعملية الـ OCR. |
| صورة JPG تجريبية (`sample1.jpg`) | الملف الذي سنمرره إلى المحرك. |

إذا كان لديك هذه المتطلبات، رائع—لنبدأ مباشرة.

## الخطوة 1 – إعداد محرك Aspose OCR **لاستخراج النص من الصورة**

أولاً نحتاج إلى إنشاء كائن `OcrEngine`. هذا الكائن هو قلب المكتبة؛ فهو يحمل الإعدادات ويقوم بالمعالجة الثقيلة.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable evaluation mode – no license file needed for this demo
        ocrEngine.SetEvaluationMode();

        // Choose the language (Latin works for most English/Japanese‑Romanized texts)
        ocrEngine.Language = Language.Latin;
```

**لماذا هذا مهم:**  
إنشاء المحرك أمر بسيط، لكن نسيان استدعاء `SetEvaluationMode()` سيتسبب في استثناء وقت تشغيل ما لم تكن قد اشتريت ترخيصًا. ضبط اللغة يحد من مجموعة الأحرف، مما يحسن الدقة ويسرّع المعالجة.

## الخطوة 2 – **تحميل الصورة للـ OCR** – **التعرف على النص من JPG**

الآن نوجه المحرك إلى الملف الذي نريد قراءته. المساعد `ImageStream.FromFile` يلغي الحاجة إلى فتح `FileStream` يدويًا.

```csharp
        // Step 2: Load the image you want to process
        // Replace YOUR_DIRECTORY with the actual folder path
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\sample1.jpg");
```

**نصيحة للحالات الحدية:**  
إذا كانت صورتك بصيغة PNG أو BMP، فإن `FromFile` لا يزال يعمل، لكن جودة الـ OCR قد تختلف. للحصول على أفضل النتائج، استخدم صور JPG عالية الدقة (300 dpi أو أعلى).  

## الخطوة 3 – تنفيذ الـ OCR و**تحويل JPG إلى نص**

بعد تحميل الصورة، نداء واحد لـ `Recognize()` يقوم بالباقي. تُعيد الطريقة كائن `RecognitionResult` يحتوي على السلسلة المستخرجة ودرجات الثقة.

```csharp
        // Step 3: Run the OCR engine
        RecognitionResult recognitionResult = ocrEngine.Recognize();

        // Step 4: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognitionResult.Text);
    }
}
```

**ماذا يحدث في الخلفية؟**  
`Recognize()` يجري سلسلة من خطوات ما قبل المعالجة—التنقيط، تصحيح الميل، التجزئة—قبل إمداد البيانات إلى شبكة عصبية مدربة على الأحرف اللاتينية. الخاصية `Text` المُرجعة مُشفرة بالفعل بـ Unicode، لذا يمكنك كتابتها إلى ملف، قاعدة بيانات، أو تمريرها إلى خدمة أخرى.

## النتيجة المتوقعة

إذا كان `sample1.jpg` يحتوي على العبارة “Hello World”، ستظهر وحدة التحكم:

```
=== OCR Output ===
Hello World
```

إذا كانت الصورة غير واضحة، قد ترى أحرفًا إضافية أو ثقة أقل. في هذه الحالة، فكر في زيادة DPI للصورة المصدر أو تطبيق مرشح تعزيز الحدة قبل تحميلها.

## نصائح احترافية وأخطاء شائعة

- **نصيحة احترافية:** ضع نداء الـ OCR داخل كتلة `try…catch` للتعامل بلطف مع الملفات التالفة.  
- **خطأ شائع:** نسيان ضبط اللغة قد يجعل المحرك يستخدم مجموعة عامة، مما قد يخطئ في التعرف على الأحرف ذات اللكنات.  
- **نصيحة أداء:** أعد استخدام نفس كائن `OcrEngine` لعدة صور؛ إنشاء محرك جديد في كل مرة يضيف عبئًا.  
- **ماذا لو أردت معالجة PDF؟** يمكن لـ Aspose OCR قبول صفحات PDF كصور عبر `ImageStream.FromPdf`، لكنك ستحتاج أيضًا إلى مكتبة Aspose.PDF.

## الخطوة 4 – التحقق من الاستخراج والخطوات التالية

بعد طباعة ناتج الـ OCR، ربما ترغب في مقارنته بالصورة الأصلية يدويًا أو عبر فحص بسيط. إليك طريقة سريعة لكتابة النتيجة إلى ملف نصي للمراجعة لاحقًا:

```csharp
        // Optional: Save the OCR result to a .txt file
        System.IO.File.WriteAllText(@"YOUR_DIRECTORY\sample1_ocr.txt", recognitionResult.Text);
        Console.WriteLine("Result saved to sample1_ocr.txt");
```

الآن لديك سير عمل قابل لإعادة الاستخدام **يستخرج النص من الصورة**، **يتعرف على النص من jpg**، و**يحول jpg إلى نص** تلقائيًا.

## الأسئلة المتكررة

**س: هل يعمل هذا على لينكس؟**  
ج: بالتأكيد. Aspose OCR متعدد المنصات؛ فقط قم بتثبيت بيئة تشغيل .NET للينكس وسيعمل الكود نفسه دون تعديل.

**س: هل يمكنني التعرف على نصوص غير لاتينية؟**  
ج: نعم—Aspose OCR يدعم السيريلية، العربية، وعدة أبجديات آسيوية. غيّر `ocrEngine.Language` إلى القيمة المناسبة من الـ enum.

**س: ماذا لو أردت معالجة مئات الملفات؟**  
ج: ضع المنطق داخل حلقة `foreach` وفكّر في تنفيذ التوازي باستخدام `Parallel.ForEach` مع إعادة استخدام كائن المحرك.

## الخلاصة

أصبح لديك الآن مقطع شفرة كامل وجاهز للإنتاج **يستخرج النص من ملفات الصورة** باستخدام Aspose OCR، يتيح لك **التعرف على النص من jpg**، ويظهر لك **كيفية تحويل jpg إلى نص** ببضع أسطر من C#. الخطوات الأساسية—إنشاء المحرك، تحميل الصورة، تشغيل `Recognize()`، ومعالجة النتيجة—مغطاة جميعًا، وقد رأيت نصائح عملية للحفاظ على سلاسة العملية.

من هنا يمكنك استكشاف:

- إمداد ناتج الـ OCR إلى فهرس بحث (مثل Elasticsearch).  
- إضافة كشف اللغة لاختيار الـ `Language` المناسب تلقائيًا.  
- دمج الكود في واجهة API بـ ASP.NET Core حتى تتمكن الخدمات الأخرى من طلب الـ OCR عند الحاجة.

جرّبه، عدّل جودة الصورة، وشاهد النص يظهر على وحدة التحكم. برمجة سعيدة!  

![مثال استخراج النص من الصورة](/images/ocr-sample.png "لقطة شاشة تُظهر ناتج OCR – استخراج النص من الصورة")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}