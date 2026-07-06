---
category: general
date: 2026-04-03
description: تعلم كيفية تنفيذ تقنية التعرف الضوئي على الحروف (OCR) في C# واستخراج
  النص من الصورة باستخدام Aspose OCR، مع تدقيق إملائي للغة الروسية.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- how to spell check
- ocr russian language
language: ar
og_description: تعلم كيفية تنفيذ التعرف الضوئي على الحروف (OCR) في C# واستخراج النص
  من الصورة باستخدام Aspose OCR، مع تدقيق إملائي للغة الروسية.
og_title: كيفية تنفيذ OCR في C# – استخراج النص من الصورة
tags:
- OCR
- C#
- Aspose
- SpellCheck
title: كيفية تنفيذ OCR في C# – استخراج النص من الصورة
url: /ar/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في C# – استخراج النص من الصورة

هل تساءلت يومًا **كيفية تنفيذ OCR** على صورة لملاحظة مكتوبة يدويًا؟ ربما لديك إيصال ممسوح ضوئيًا، أو لوحة بلغة أجنبية، أو صفحة PDF ترفض النسخ واللصق. الخبر السار؟ ببضع أسطر من C# ومكتبة Aspose OCR يمكنك تحويل تلك الصورة إلى نص قابل للتحرير في لحظة.  

في هذا الدليل لن نُظهر لك فقط **كيفية تنفيذ OCR**، بل سنستعرض أيضًا **استخراج النص من الصورة**، **تحويل الصورة إلى نص**، وحتى **كيفية التدقيق الإملائي** للنتيجة عندما تتعامل مع مستندات باللغة الروسية. يبدو كثيرًا؟ ابقَ معنا – سنقسم كل شيء خطوة بخطوة.

## ما ستتعلمه

* إعداد Aspose OCR لدعم اللغة الروسية.  
* تحميل ملف صورة وتشغيل التعرف الضوئي على الحروف لاستخراج النص من الصورة.  
* استخدام المدقق الإملائي المدمج لتصحيح الكلمات المكتوبة خطأ تلقائيًا – الجواب المثالي على سؤال “**كيفية التدقيق الإملائي**” لمخرجات OCR.  
* طباعة السلسلة المنقحة إلى وحدة التحكم، جاهزة لمزيد من المعالجة أو التخزين.

**المتطلبات المسبقة** – ستحتاج إلى:

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.8).  
* رخصة Aspose OCR صالحة أو مفتاح تقييم مؤقت.  
* ملف صورة يحتوي على نص روسي (للتجربة سنسميه `russian_note.jpg`).  

إذا كان أي من ذلك غير مألوف، لا تقلق. الخطوات أدناه تتضمن أمر NuGet الدقيق لجلب Aspose OCR، والكود مكتمل ذاتيًا.

![مثال على تنفيذ OCR](/images/ocr-demo.png "مثال على تنفيذ OCR في C#")

## الخطوة 1 – تثبيت Aspose OCR وإضافة المساحات الاسمية

أولاً، تحتاج إلى المكتبة. افتح طرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

هذا الأمر يجلب أحدث نسخة مستقرة (اعتبارًا من أبريل 2026 الإصدار 22.9). بعد استعادة الحزمة، أضف توجيهات `using` المطلوبة في أعلى ملف C# الخاص بك:

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;
```

*نصيحة احترافية:* إذا كنت تستخدم Visual Studio، سيقترح IDE إضافة هذه تلقائيًا بمجرد كتابة اسم الصنف الأول.

## الخطوة 2 – تهيئة محرك OCR للغة الروسية

جزء **كيفية تنفيذ OCR** يبدأ بإنشاء نسخة من `OcrEngine`. من خلال تحديد `OcrLanguage.Russian` نخبر المحرك بتحميل مجموعة الأحرف السيريالية والheuristics الخاصة باللغة.

```csharp
// Step 2: Initialise OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Russian   // Enables Russian language support
};
```

لماذا هذا مهم؟ بدون ضبط اللغة، ي默认 المحرك اللغة الإنجليزية وسيُفسّر العديد من الأحرف السيريالية بشكل خاطئ، مما يؤدي إلى مخرجات مشوشة. ضبط اللغة صراحةً يحسن الدقة بشكل كبير.

## الخطوة 3 – تحميل الصورة و **تحويل الصورة إلى نص**

الآن نقوم بتحميل الصورة إلى الذاكرة. طريقة `Image.FromFile` تعمل مع معظم الصيغ الشائعة (JPG, PNG, BMP). بعد التحميل، نستدعي `Recognize` لـ **تحويل الصورة إلى نص**.

```csharp
// Step 3: Load the image that contains Russian text
Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

// Step 4: Perform OCR – this is the core “how to perform OCR” call
string rawText = ocrEngine.Recognize(sourceImage);
```

المتغير `rawText` الآن يحتوي على مخرجات OCR الخام، والتي قد لا تزال تحتوي على أخطاء إملائية أو أحرف تم التعرف عليها بشكل خاطئ. يمكنك طباعتها لرؤية ما التقطه المحرك:

```csharp
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

## الخطوة 4 – **كيفية التدقيق الإملائي** لنتيجة OCR

يمكن أن يكون OCR للغة الروسية صاخبًا، خاصةً مع المسحات منخفضة الدقة. توفر Aspose فئة `SpellChecker` التي تفهم القواميس الروسية جاهزة للاستخدام. إليك كيفية استدعائها:

```csharp
// Step 5: Initialise the spell checker
SpellChecker spellChecker = new SpellChecker();

// Step 6: Correct spelling mistakes in the recognized text
string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);
```

طريقة `CheckAndCorrect` تُعيد سلسلة جديدة حيث تُستبدل الكلمات المكتوبة خطأ بأكثر البدائل صحة احتمالًا. كما تحترم علامات الترقيم، لذا لن تحصل على جدار من النص.

*حالة خاصة:* إذا كان مخرج OCR فارغًا (مثلاً الصورة بيضاء تمامًا)، فإن `CheckAndCorrect` سيعيد ببساطة سلسلة فارغة. من الجيد الحماية من ذلك إذا كنت تخطط لكتابة النتيجة إلى ملف.

## الخطوة 5 – عرض النتيجة المنقحة

أخيرًا، نطبع السلسلة المصححة. في تطبيق واقعي قد تكتبها إلى قاعدة بيانات، أو واجهة JSON API، أو مستند Word. لهذا العرض التجريبي، طباعة إلى وحدة التحكم تكفي:

```csharp
// Step 7: Show the corrected result
Console.WriteLine("\nCorrected text:");
Console.WriteLine(correctedText);
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مثل:

```
Raw OCR output:
Привeт мир! Этo тeкcт c русcкoй оcнoвнoй.

Corrected text:
Привет мир! Это текст с русской основой.
```

لاحظ كيف حوّل المدقق الإملائي “Привeт” (حرف لاتيني ‘e’ مختلط) إلى السيريالي الصحيح “Привет”. هذه هي سحر **كيفية التدقيق الإملائي** لمخرجات OCR.

## مثال كامل يعمل

فيما يلي البرنامج الكامل القابل للتنفيذ الذي يجمع جميع الخطوات معًا. انسخه والصقه في مشروع وحدة تحكم جديد واضغط **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine configured for Russian language
        OcrEngine ocrEngine = new OcrEngine { Language = OcrLanguage.Russian };

        // Step 2: Load the image that contains the text to be recognized
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

        // Step 3: Perform OCR to extract raw text from the image
        string rawText = ocrEngine.Recognize(sourceImage);

        // Optional: Show raw OCR output
        System.Console.WriteLine("Raw OCR output:");
        System.Console.WriteLine(rawText);

        // Step 4: Initialise the spell checker
        SpellChecker spellChecker = new SpellChecker();

        // Step 5: Correct spelling mistakes in the recognized text
        string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);

        // Step 6: Display the corrected result
        System.Console.WriteLine("\nCorrected text:");
        System.Console.WriteLine(correctedText);
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج مع صورة واضحة وعالية الدقة للكتابة اليدوية الروسية عادةً ما ينتج جملة نظيفة وقابلة للقراءة من قبل الإنسان. إذا كانت الصورة غير واضحة، قد تحصل على كلمات جزئيًا صحيحة، لكن المدقق الإملائي سيصقل معظم الأخطاء الواضحة.

## المشكلات الشائعة والنصائح

| المشكلة | لماذا يحدث | كيفية الإصلاح / التجنب |
|-------|----------------|--------------------|
| **حروف غير مفهومة** | DPI منخفض أو خلفية مشوشة | قم بمعالجة الصورة مسبقًا (زيادة التباين، تغيير الحجم إلى ≥300 dpi) قبل تمريرها إلى `Recognize`. |
| **مخرج فارغ** | مسار ملف خاطئ أو صيغة غير مدعومة | تحقق من المسار، واستخدم `Image.FromFile` داخل كتلة `try/catch` لعرض الأخطاء. |
| **المدقق الإملائي يفوت الأخطاء** | كلمات نادرة غير موجودة في القاموس | وسّع القاموس بتحميل قائمة كلمات مخصصة عبر `spellChecker.AddUserDictionary("mywords.txt")`. |
| **تأخر الأداء عند دفعات كبيرة** | OCR يستهلك موارد المعالج | شغّل OCR في خيط خلفي أو استخدم `Parallel.ForEach` للصور المتعددة. |
| **استثناء الترخيص** | استخدام نسخة تجريبية بعد انتهاء الفترة التجريبية | اشترِ رخصة واستدعِ `License license = new License(); license.SetLicense("Aspose.Total.lic");` قبل إنشاء `OcrEngine`. |

## الخطوات التالية – تجاوز OCR البسيط

الآن بعد أن أتقنت **كيفية تنفيذ OCR**، فكر في هذه الإضافات:

* **معالجة دفعات** – تكرار عبر مجلد من الصور وكتابة كل نص مصحح إلى ملف `.txt`.  
* **تحويل PDF** – استخدم Aspose PDF لتضمين النص المستخرج مرة أخرى في PDF قابل للبحث.  
* **اكتشاف اللغة** – إذا كنت بحاجة للتعامل مع لغات متعددة، افحص نتيجة OCR أولاً وغيّر `OcrLanguage` وفقًا لذلك.  
* **التكامل مع Azure Cognitive Services** – قارن نتائج Aspose مع واجهة OCR من Microsoft للحصول على نهج هجين.

جميع هذه المواضيع بطبيعتها تشمل الكلمات المفتاحية الثانوية **استخراج النص من الصورة**، **تحويل الصورة إلى نص**، و **كيفية التدقيق الإملائي**، لذا

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}