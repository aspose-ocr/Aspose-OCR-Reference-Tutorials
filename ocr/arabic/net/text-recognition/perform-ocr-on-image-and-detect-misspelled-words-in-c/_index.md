---
category: general
date: 2026-06-03
description: قم بإجراء التعرف الضوئي على الحروف (OCR) على الصورة واستخراج النص منها
  باستخدام Aspose.OCR. تعلّم كيفية اكتشاف الكلمات المكتوبة بشكل خاطئ والحصول على اقتراحات
  إملائية في عرض توضيحي واحد بلغة C#.
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: ar
og_description: قم بإجراء OCR على الصورة لاستخراج النص منها، ثم اكتشف الكلمات المكتوبة
  بشكل خاطئ واحصل على اقتراحات إملائية باستخدام Aspose.OCR في C#.
og_title: إجراء التعرف الضوئي على الأحرف في الصورة واكتشاف الكلمات المكتوبة بشكل خاطئ
  في C#
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: إجراء التعرف الضوئي على الأحرف في الصورة واكتشاف الكلمات المكتوبة بشكل خاطئ
  في C#
url: /ar/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على الصورة واكتشاف الكلمات المكتوبة بشكل خاطئ في C#

هل تساءلت يومًا كيف تقوم **perform OCR on image** للملفات دون أن تمزق شعرك؟ لست وحدك. سواءً كنت تقوم برقمنة رسائل قديمة، أو مسح الفواتير، أو بناء سير عمل مستندات ذكي، فإن استخراج نص نظيف من الصور هو العقبة الأولى. الخبر السار؟ مع Aspose.OCR يمكنك إنشاء حل خلال دقائق، والمكافأة هي أنك يمكنك أيضًا **detect misspelled words** و **get spelling suggestions** في نفس العملية.

في هذا الدرس سنستعرض تطبيقًا كاملًا وجاهزًا للتنفيذ في وحدة تحكم C# يقوم **extracts text from image**، ويشغل مدقق إملائي للإنجليزية، ويطبع كل خطأ مع اقتراحات تصحيح مفيدة. بنهاية الدرس ستعرف بالضبط **how to extract text**، وكيفية ربط API المدقق الإملائي، وما هو شكل مخرجات وحدة التحكم المتوقعة.

## ما ستبنيه

- تحميل صورة bitmap (أو PNG) تحتوي على أخطاء إملائية.  
- تشغيل Aspose.OCR لـ **perform OCR on image** والحصول على بيانات نصية خام.  
- تهيئة مدقق الإملاء الإنجليزي المدمج.  
- **Detect misspelled words** و **get spelling suggestions** لكل كلمة.  
- طباعة تقرير منسق إلى وحدة التحكم.

بدون خدمات خارجية، ولا مكالمات HTTP معقدة—فقط حزمة NuGet واحدة وقليل من أسطر الشيفرة.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).  
- Visual Studio 2022 (أو أي محرر تفضله).  
- حزمة NuGet Aspose.OCR لـ .NET (`Aspose.OCR`).  
- ملف صورة (`letter_with_typos.png`) موجود في مكان يمكنك الإشارة إليه من المشروع.

إذا لم تستخدم Aspose من قبل، لا تقلق—تثبيت الحزمة سهل كتشغيل:

```bash
dotnet add package Aspose.OCR
```

الآن دعنا نغوص في التنفيذ.

## الخطوة 1: إعداد المشروع وتثبيت Aspose.OCR

أنشئ مشروع وحدة تحكم جديد وأدرج مكتبة OCR:

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

بعد انتهاء الاستعادة، افتح `Program.cs`. سنستبدل المحتوى الافتراضي بكود العرض الكامل لاحقًا، ولكن أولاً دعنا نتحدث عن سبب أهمية كل مساحة أسماء.

- `Aspose.OCR` – محرك OCR الأساسي ومعالجة الصور.  
- `Aspose.OCR.SpellCheck` – أدوات التدقيق الإملائي المرفقة بالمكتبة.  
- `System` – فئات .NET الأساسية القياسية (مثل `Console`).

## الخطوة 2: تحميل الصورة وإجراء OCR على الصورة

العمل الحقيقي الأول هو تمرير الصورة إلى محرك OCR. Aspose.OCR يقرأ العديد من الصيغ (PNG، JPEG، TIFF). إليك المقتطف الذي يقوم بالعمل الشاق:

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **لماذا هذا مهم:** `OcrImage.FromFile` يخفّف تفاصيل مستوى البكسل، بينما `OcrEngine.Recognize` يشغّل النموذج العصبي المدرب الذي يترجم الرموز البصرية إلى أحرف Unicode. خاصية `ocrResult.Text` الآن تحتوي على السلسلة الخام—بالضبط ما تحتاجه لـ **extract text from image**.  
> **نصيحة احترافية:** إذا كانت صورتك تحتوي على لغات متعددة، يمكنك تعيين `ocrEngine.Language = OcrLanguage.Multilingual;` قبل استدعاء `Recognize`.

## الخطوة 3: تهيئة مدقق الإملاء الإنجليزي

Aspose.OCR يأتي مع محرك تدقيق إملائي مدمج يفهم الإنجليزية مباشرةً. تهيئته سطر واحد:

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **لماذا هذه الخطوة حاسمة:** قد يتضمن ناتج OCR أحرفًا تم التعرف عليها بشكل خاطئ (مثل “l” مقابل “1”) أو أخطاء إملائية حقيقية من المستند الأصلي. سيقوم مدقق الإملاء بمسح السلسلة، وتحديد الرموز المشكوك فيها، واقتراح بدائل.

## الخطوة 4: اكتشاف الكلمات المكتوبة بشكل خاطئ والحصول على اقتراحات إملائية

الآن نقوم بتمرير نص OCR إلى المدقق:

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings` هي مجموعة حيث يحتوي كل إدخال على الكلمة الخاطئة ومصفوفة من التصحيحات المحتملة.

## الخطوة 5: إخراج النتائج

أخيرًا، نقوم بالتكرار عبر المجموعة وطباعة تقرير قابل للقراءة للإنسان:

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### مخرجات وحدة التحكم المتوقعة

بافتراض أن `letter_with_typos.png` يحتوي على الجملة:

```
Ths is an exampel of a lettter with som misspelled wrds.
```

تشغيل العرض سيولد شيئًا مشابهًا لـ:

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

لاحظ كيف يتم إقران كل خطأ إملائي بمجموعة من التصحيحات المحتملة—بالضبط ما تحتاجه عند بناء واجهة تصحيح صديقة للمستخدم.

## مثال كامل يعمل

فيما يلي البرنامج **complete, copy‑paste‑ready**. استبدل `YOUR_DIRECTORY` بالمسار الفعلي لملف الصورة الخاص بك.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **حالات الحافة التي يجب مراعاتها**  
> - **Empty Image:** إذا أعاد محرك OCR سلسلة فارغة، فإن `spellChecker.Check` سيعيد ببساطة مجموعة فارغة—بدون تعطل.  
> - **Non‑English Text:** استبدل `OcrLanguage.English` بـ `OcrLanguage.French` (أو أي لغة مدعومة) لـ **detect misspelled words** في لغات أخرى.  
> - **Large Documents:** بالنسبة لملفات PDF متعددة الصفحات، ستقوم بالتكرار على كل صفحة، إجراء OCR، ثم تجميع النتائج قبل التدقيق الإملائي.

## نظرة بصرية (نص بديل للصورة)

![مخطط يوضح تدفق إجراء OCR على الصورة، استخراج النص من الصورة، ثم اكتشاف الكلمات المكتوبة بشكل خاطئ مع اقتراحات إملائية](perform-ocr-on-image-flow.png)

*المخطط أعلاه يوضح خط الأنابيب من البداية إلى النهاية: صورة → محرك OCR → نص خام → مدقق إملائي → اقتراحات.*

## أسئلة شائعة ونصائح احترافية

| السؤال | الجواب |
|----------|--------|
| **هل أحتاج إلى اتصال بالإنترنت؟** | لا. Aspose.OCR يعمل بالكامل محليًا؛ مثالي للبيئات غير المتصلة أو الآمنة. |
| **ما مدى دقة مدقق الإملاء؟** | يستخدم قاموسًا يضم حوالي 150 ألف كلمة إنجليزية وتقنية المطابقة الضبابية، لذا يتم التقاط معظم الأخطاء الشائعة. |
| **هل يمكنني تخصيص القاموس؟** | نعم. `SpellChecker.AddUserDictionary("custom.txt")` يتيح لك تحميل مصطلحات خاصة بالمجال (مثل أسماء المنتجات). |
| **ماذا لو كانت الصورة مائلة؟** | محرك OCR يكتشف الاتجاه تلقائيًا، ولكن يمكنك استدعاء `ocrEngine.ImagePreprocessing.Rotate(angle)` يدويًا في الحالات الصعبة. |
| **هل هناك طريقة لتسليط الضوء على الاقتراحات في واجهة المستخدم؟** | بعد الحصول على مجموعة `misspellings`، يمكنك ربط كل `entry.Word` بموقعه في `ocrResult.Text` وتسطيره في RichTextBox أو عرض ويب. |

## الخلاصة

لقد أظهرنا لك الآن **how to perform OCR on image**، **extract text from image**، ثم **detect misspelled words** مع **getting spelling suggestions**—كل ذلك باستخدام تطبيق وحدة تحكم C# مختصر. الفكرة الأساسية بسيطة: دع Aspose.OCR يتولى الجزء الثقيل من التعرف على الأحرف، ثم دع مدقق الإملاء المدمج ينظف الناتج. من هنا يمكنك توسيع العرض إلى خدمة معالجة مستندات كاملة، دمجه مع API ويب، أو ربطه بمحرر سطح مكتب.

هل أنت مستعد للخطوة التالية؟ جرّب تبديل اللغة إلى الإسبانية، أو معالجة PDF متعدد الصفحات، أو بناء واجهة WPF صغيرة تسمح للمستخدمين بالنقر على كلمة لقبول اقتراح. اللبنات الأساسية موجودة بالفعل—استمر في التجربة.

إذا واجهت أي مشاكل أو كان لديك أفكار لتوسعات، اترك تعليقًا أدناه. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [استخراج النص من الصورة باستخدام Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}