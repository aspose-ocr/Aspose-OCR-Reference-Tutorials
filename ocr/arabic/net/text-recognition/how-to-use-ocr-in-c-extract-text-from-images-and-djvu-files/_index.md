---
category: general
date: 2026-04-04
description: كيفية استخدام OCR بسرعة وأمان. تعلم استخراج النص من الصورة، تحويل DJVU
  إلى نص، وتحميل الصورة لـ OCR باستخدام Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert djvu to text
- load image for OCR
- extract text from djvu
language: ar
og_description: كيفية استخدام OCR في C# لاستخراج النص من ملفات الصور ومستندات DJVU.
  دليل خطوة بخطوة مع الكود الكامل.
og_title: كيفية استخدام OCR في C# – دليل كامل
tags:
- OCR
- C#
- Aspose
title: كيفية استخدام OCR في C# – استخراج النص من الصور وملفات DJVU
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تستخدم OCR في C# – استخراج النص من الصور وملفات DJVU

هل تساءلت يومًا **كيف تستخدم OCR** لاستخراج الكلمات من صفحة ممسوحة ضوئيًا دون الحاجة للكتابة يدويًا؟ لست وحدك. في العديد من المشاريع—سواءً كنت تقوم برقمنة الكتب القديمة أو استخراج البيانات من الإيصالات—الحصول على النص من صورة هو نقطة ألم يومية. الخبر السار؟ مع Aspose.OCR يمكنك القيام بذلك ببضع أسطر فقط، حتى عندما يكون المصدر ملف DJVU.

في هذا الدليل سنستعرض كل ما تحتاجه **لاستخراج النص من ملفات الصورة**، **تحميل الصورة لـ OCR**، وحتى **تحويل DJVU إلى نص** باستخدام C#. في النهاية ستحصل على تطبيق Console جاهز للتنفيذ يطبع النص المعترف به مباشرةً في وحدة التحكم. لا أسرار، لا تبعيات إضافية، فقط C# صافي و Aspose.

## ما ستتعلمه

- كيفية تثبيت وإضافة مرجع لمكتبة Aspose.OCR.
- الكود الدقيق المطلوب **لتحميل الصورة لـ OCR**، سواء كانت PNG أو JPEG أو صفحة DJVU.
- كيفية استدعاء المحرك واسترجاع النتيجة.
- نصائح للتعامل مع المستندات الكبيرة والمشكلات الشائعة.
- مثال كامل قابل للتنفيذ يمكنك نسخه‑لصقه في Visual Studio.

> **المتطلبات المسبقة:** .NET 6.0 أو أحدث ورخصة صالحة لـ Aspose.OCR (أو نسخة تجريبية مجانية). إذا لم تكن تمتلك المكتبة بعد، احصل عليها من NuGet باستخدام `dotnet add package Aspose.OCR`.

---

## كيفية استخدام OCR مع Aspose في C#

هذه هي الخطوة الأساسية التي نجيب فيها على سؤال **كيف تستخدم OCR** في مشروع C#. الكود أدناه برنامج كامل؛ يمكنك وضعه في تطبيق Console جديد والضغط على F5.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance.
            var ocrEngine = new OcrEngine();

            // Step 2: Load the image (or DJVU page) you want to analyze.
            // Replace the path with your own file location.
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book-page.djvu");

            // Step 3: Run the recognition process.
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 4: Output the extracted text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**لماذا يعمل هذا:**  
- `OcrEngine` هو نقطة الدخول؛ فهو يختصر الجهد الثقيل لمعالجة الصورة، واكتشاف اللغة، وتصنيف الأحرف.  
- `ImageStream.FromFile` يمكنه التعامل مع العديد من الصيغ، بما في ذلك DJVU، مما يعني أنه يمكنك **تحويل DJVU إلى نص** دون خطوة تحويل إضافية.  
- `Recognize()` يعيد كائن `OcrResult` يحتوي على النص العادي، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها لاحقًا.

تشغيل البرنامج يطبع شيئًا مشابهًا لـ:

```
=== OCR Result ===
In the beginning God created the heavens and the earth.
```

هذا كل شيء—أول عملية **استخراج نص من DJVU** ناجحة لك.

![مثال على كيفية استخدام OCR](/images/ocr-demo.png "لقطة شاشة توضح كيفية استخدام OCR في تطبيق Console بلغة C#")

*النص البديل: “كيفية استخدام OCR” لقطة شاشة لمخرجات وحدة التحكم.*

---

## تحميل الصورة لـ OCR

قبل أن يتمكن المحرك من القراءة، يجب عليك **تحميل الصورة لـ OCR** بشكل صحيح. تدعم Aspose معظم صيغ الصور النقطية مباشرة، لكن بعض النصائح يمكن أن تجعل التعرف أكثر سلاسة:

- **تغيير حجم الصور الكبيرة** إلى حد أقصى 2000 بكسل على الجانب الأطول. الملفات الضخمة تزيد من استهلاك الذاكرة وقد تبطئ المحرك.  
- **تحويل الصور الملونة إلى تدرج الرمادي** إذا لاحظت خلفيات مشوشة. استخدم `ocrEngine.Image = ImageStream.FromFile(path).ConvertToGrayscale();`.  
- **تعيين DPI يدويًا** للماسحات منخفضة الدقة (`ocrEngine.Image.DpiX = 300; ocrEngine.Image.DpiY = 300;`).

هذه التعديلات اختيارية لكنها غالبًا ما تحسن الدقة عند **استخراج النص من صورة** مثل الإيصالات الممسوحة.

---

## استخراج النص من الصورة – أفضل الممارسات

عند التعامل مع صيغ الصور الشائعة (PNG، JPEG، BMP)، تظل الخطوات نفسها، لكن يمكنك تحسين المحرك:

```csharp
ocrEngine.Image = ImageStream.FromFile("sample.png");

// Optional: enable language packs for better accuracy.
ocrEngine.Language = Language.English;

// Optional: set recognition mode to auto.
ocrEngine.RecognitionMode = RecognitionMode.Auto;
```

- **اختيار اللغة** مهم. إذا كنت تعالج مستندات متعددة اللغات، عيّن `ocrEngine.Language = Language.Multilingual;`.  
- **RecognitionMode** يمكن أن تكون `Auto` أو `Fast` أو `Accurate`. `Accurate` تعطي جودة أعلى على حساب السرعة—استخدمها للمهام الأرشيفية.

---

## تحويل DJVU إلى نص – التعامل مع الملفات متعددة الصفحات

غالبًا ما تحتوي ملفات DJVU على عدة صفحات. تتعامل Aspose مع كل صفحة كتيار صورة منفصل، لذا يمكنك التكرار عبرها:

```csharp
using Aspose.OCR;
using System.Collections.Generic;

var ocrEngine = new OcrEngine();
List<string> allPagesText = new List<string>();

int pageCount = ImageStream.GetPageCount("book.djvu");
for (int i = 1; i <= pageCount; i++)
{
    ocrEngine.Image = ImageStream.FromFile("book.djvu", i); // Load page i
    OcrResult result = ocrEngine.Recognize();
    allPagesText.Add(result.Text);
}

// Combine all pages into a single string.
string fullText = string.Join("\n--- Page Break ---\n", allPagesText);
Console.WriteLine(fullText);
```

**لماذا التكرار؟**  
ملفات DJVU هي في الأساس مجموعة من الصور. من خلال التكرار على كل صفحة، **تستخرج النص من DJVU** بترتيبها، مع الحفاظ على تدفق المستند الأصلي.

---

## المشكلات الشائعة ونصائح الخبراء

| المشكلة | السبب | الحل |
|------|----------------|-----|
| **حروف غير مفهومة** | DPI منخفض أو ضغط عالي | تكبير الصورة، تعيين `ocrEngine.Image.DpiX/Y = 300` |
| **معالجة بطيئة** | استخدام وضع `Accurate` على ملفات ضخمة | التحول إلى وضع `Fast` للمهام الضخمة |
| **غياب دعم اللغة** | اللغة الافتراضية هي الإنجليزية فقط | تحميل حزم لغات إضافية (`ocrEngine.Language = Language.Spanish;`) |
| **أخطاء نفاد الذاكرة** | تحميل العديد من الصفحات عالية الدقة دفعة واحدة | معالجة الصفحات واحدة‑واحدة وإطلاق الموارد (`ocrEngine.Dispose();`) |

نصيحة سريعة **للمحترفين**: دائمًا استدعِ `ocrEngine.Dispose()` بعد الانتهاء من صفحة. هذا يحرر الموارد الأصلية ويمنع تسرب الذاكرة الخفي الذي قد يسبب تعطل الخدمات طويلة الأمد.

---

## اختبار خط أنابيب OCR الخاص بك

للتحقق من أن كل شيء يعمل، جرّب الفحوصات البسيطة التالية:

1. **طباعة طول** السلسلة المعترف بها: `Console.WriteLine($"Characters recognized: {ocrResult.Text.Length}");`  
2. **المقارنة مع نص معروف** باستخدام مكتبة diff بسيطة إذا كان لديك نص مرجعي.  
3. **تسجيل درجات الثقة** (`ocrResult.Confidence`) لتحديد الصفحات ذات الجودة المنخفضة تلقائيًا.

إذا كانت درجة الثقة باستمرار أقل من 0.7، عد إلى خطوات معالجة الصورة المذكورة سابقًا.

---

## الخطوات التالية

الآن بعد أن عرفت **كيف تستخدم OCR**، فكر في توسيع سير العمل الخاص بك:

- **معالجة دفعات**: غلف الحلقة داخل `Parallel.ForEach` لتسريع المجموعات الكبيرة.  
- **تصدير إلى PDF**: استخدم Aspose.PDF لإدراج النص المعترف به كطبقة مخفية لإنشاء ملفات PDF قابلة للبحث.  
- **الدمج مع الذكاء الاصطناعي**: مرّر السلاسل المستخرجة إلى نموذج لغة لتلخيصها أو استخراج الكيانات.

كل هذه الخطوات تبني على الأساس نفسه الذي أنشأته الآن، وتستفيد من نفس مبادئ **استخراج النص من صورة** التي غطيناها.

---

## الخلاصة

لقد غطينا بعمق **كيفية استخدام OCR** في C# مع Aspose، بدءًا من تحميل الصورة، **استخراج النص من صورة**، التعامل مع ملفات **DJVU**، وتجاوز المشكلات الشائعة. المثال الكامل القابل للتنفيذ أعلاه يمنحك نقطة انطلاق قوية، والنصائح المتناثرة ستساعدك على تكييف الحل مع مشاريع العالم الحقيقي.  

جرّبه، عدّل الإعدادات لتناسب مستنداتك، وستحول الصفحات الممسوحة إلى نص قابل للبحث في لمح البصر. هل لديك أسئلة أو ملف صعب يرفض التعاون؟ اترك تعليقًا—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}