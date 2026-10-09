---
category: general
date: 2026-03-07
description: مثال Aspose OCR يوضح كيفية تمكين التدقيق الإملائي، إضافة قاموس مخصص،
  تحميل OCR للصور وإصلاح أخطاء OCR بسرعة.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: ar
og_description: مثال Aspose OCR يوضح لك كيفية تمكين التدقيق الإملائي، إضافة قاموس
  مخصص، تحميل صورة للـ OCR وإصلاح الأخطاء الشائعة في الـ OCR.
og_title: مثال Aspose OCR – تمكين التدقيق الإملائي وإصلاح الأخطاء
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: مثال Aspose OCR – تمكين التدقيق الإملائي وإصلاح الأخطاء في C#
url: /ar/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# مثال Aspose OCR – تمكين التدقيق الإملائي وإصلاح الأخطاء في C#

هل احتجت يومًا إلى **مثال Aspose OCR** لا يقرأ النص من صورة فحسب، بل ينظف أيضًا تلك الأخطاء الإملائية المزعجة؟ لست وحدك. في العديد من المشاريع الواقعية يكون ناتج OCR الخام مليئًا بالأخطاء، خاصة عندما تحتوي الصورة المصدر على خطوط منخفضة التباين أو ملاحظات مكتوبة بخط اليد.  

الأخبار السارة؟ مع Aspose.OCR يمكنك **تمكين التدقيق الإملائي**، وإضافة القاموس الخاص بك، والحصول على سلسلة منقحة في بضع أسطر من الشيفرة فقط. أدناه سترى بالضبط **كيفية تمكين التدقيق الإملائي**، **كيفية إضافة قاموس**، و**كيفية تحميل صورة OCR** حتى تتمكن أخيرًا من **إصلاح أخطاء OCR** دون أن تشد شعر رأسك.

في هذا الشرح سنغطي كل ما تحتاجه — من تثبيت NuGet إلى برنامج كامل قابل للتنفيذ يطبع النص المصحح. في النهاية ستحصل على **مثال Aspose OCR** قوي يمكنك إدراجه مباشرة في أي مشروع .NET.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الشيفرة تعمل مع .NET Core و .NET Framework أيضًا)
- Visual Studio 2022 أو أي بيئة تطوير متوافقة مع C#
- ملف صورة (`typed_text.png`) يحتوي على نص إنجليزي واضح ومكتوب
- اتصال بالإنترنت لجلب حزمة Aspose.OCR من NuGet

لا توجد مكتبات طرف ثالث أخرى مطلوبة.

---

## الخطوة 1 – تثبيت حزمة Aspose.OCR من NuGet (Load Image OCR)

قبل أن نتمكن من كتابة أي شيفرة، نحتاج إلى المكتبة التي تشغل محرك OCR.

```bash
dotnet add package Aspose.OCR
```

> **نصيحة:** إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن **Aspose.OCR** واضغط *Install*.  

تثبيت الحزمة يمنحك الوصول إلى `OcrEngine` و `ImageStream` وأدوات التدقيق الإملائي المدمجة التي سنستخدمها لاحقًا. بمجرد وجود الحزمة، ستكون جاهزًا لـ **load image OCR**.

## الخطوة 2 – إنشاء مثيل محرك OCR

إنشاء المحرك هو الخطوة الملموسة الأولى في أي **مثال Aspose OCR**. فكر في `OcrEngine` كالعقل الذي سيحلل الصورة النقطية ويستخرج النص.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

مُنشئ `OcrEngine` لا يتطلب أي معلمات، مما يجعله بسيطًا ومنظمًا للنماذج الأولية السريعة.

## الخطوة 3 – كيفية تمكين التدقيق الإملائي (ولماذا هو مهم)

غالبًا ما يحتوي ناتج OCR الخام على كلمات تم التعرف عليها خطأً مثل “teh” بدلاً من “the”. تمكين المدقق الإملائي المدمج يسمح لـ Aspose باستبدال تلك الأخطاء تلقائيًا بأكثر تهجئة صحيحة محتملة.

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **لماذا تمكين التدقيق الإملائي؟**  
> - **الدقة:** يمكن لتدقيق إملائي بعد المعالجة أن يزيد من دقة النص الإجمالية بنسبة 10‑15 % للمستندات المطبوعة.  
> - **تجربة المستخدم:** النص النظيف يعني تقليل التنظيف اللاحق عندما تُدخل النتيجة إلى فهارس البحث أو خطوط أنابيب التحليل.

## الخطوة 4 – كيفية إضافة قاموس (كلمات مخصصة)

أحيانًا لا يعرف القاموس الافتراضي أسماء علامتك التجارية أو رموز المنتجات أو المصطلحات المتخصصة في المجال. هنا يأتي دور **كيفية إضافة القاموس**.

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

يمكنك تمرير مصفوفة أو قائمة، أو حتى القراءة من ملف إذا كان لديك مفردات مخصصة كبيرة. سيعامل المدقق الإملائي الآن تلك الإدخالات كصحيحة، مما يمنع التصحيحات الخاطئة.

## الخطوة 5 – تحميل الصورة لـ OCR (Load Image OCR)

الآن بعد تكوين المحرك، نحتاج إلى توجيهه إلى الصورة التي نريد قراءتها. يساعد `ImageStream.FromFile` في إخفاء تفاصيل قراءة الملف.

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **نصيحة:** إذا كانت صورتك موجودة في مجلد فرعي داخل المشروع، اضبط خاصية *Copy to Output Directory* إلى *Copy always* حتى يتم حل المسار أثناء التشغيل.

## الخطوة 6 – تنفيذ التعرف وإصلاح أخطاء OCR

مع إعداد كل شيء، استدعاء واحد لـ `Recognize()` يشغل خط أنابيب OCR، يطبق التدقيق الإملائي، ويخزن النتيجة المنقحة في `ocrEngine.Text`.

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### النتيجة المتوقعة

بافتراض أن `typed_text.png` يحتوي على الجملة `The quick brown fox jumps over teh lazy dog`، سيظهر في وحدة التحكم:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

لاحظ كيف تم تصحيح “teh” تلقائيًا إلى “the”. إذا كنت قد أضفت “OCRify” إلى القاموس المخصص وكانت الصورة تحتوي على تلك الكلمة، فإن المحرك سيتركها دون تعديل.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يمكنك إدراجه في مشروع وحدة تحكم جديد. يتضمن جميع الخطوات السابقة، بالإضافة إلى بعض التعليقات للتوضيح.

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

احفظ هذا كـ `Program.cs`، شغّل `dotnet run`، ويجب أن ترى الجملة المصححة مطبوعة في وحدة التحكم.

---

## الأسئلة المتكررة وحالات الحافة

| السؤال | الإجابة |
|----------|--------|
| **ماذا لو كانت الصورة ملف PDF متعدد الصفحات؟** | يمكن لـ Aspose.OCR معالجة صفحات PDF كصور. استخدم `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` وكرر عبر الصفحات. |
| **هل يمكنني تغيير اللغة إلى غير الإنجليزية؟** | بالطبع. اضبط `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (أو أي لغة مدعومة). |
| **قاموسي المخصص ضخم — هل سيؤثر ذلك على الأداء؟** | إضافة آلاف الكلمات يتطلب تكلفة أولية صغيرة، لكن البحث يكون O(1) بفضل مجموعة التجزئة (hash‑set) في الخلفية. بالنسبة للمفردات الضخمة، فكر في تحميلها مرة واحدة عند بدء التطبيق. |
| **ماذا لو ألقى محرك OCR استثناءً عند صورة تالفة؟** | ضع `Recognize()` داخل كتلة try‑catch وتفقد `ocrEngine.LastError`. يمكنك أيضًا التحقق مسبقًا من أبعاد الصورة باستخدام `ocrEngine.Image.Width` و `Height`. |
| **هل أحتاج إلى ترخيص للاستخدام في الإنتاج؟** | التقييم المجاني يعمل للاختبار، لكن الترخيص التجاري يزيل علامة التقييم المائية ويفتح الأداء الكامل. |

## الخلاصة

أصبح لديك الآن **مثال Aspose OCR كامل** يوضح **كيفية تمكين التدقيق الإملائي**، **كيفية إضافة قاموس**، **تحميل صورة OCR**، و**كيفية إصلاح أخطاء OCR** بطريقة نظيفة وجاهزة للإنتاج. من خلال تكوين المدقق الإملائي وإدخال قائمة كلمات مخصصة، تحسن جودة النص المستخرج بشكل كبير دون الحاجة إلى كتابة أي منطق ما بعد المعالجة بنفسك.

هل أنت مستعد للخطوة التالية؟ جرّب تبديل اللغة إلى الإسبانية، أو معالجة PDF متعدد الصفحات، أو دمج النتيجة في فهرس Azure Cognitive Search القابل للبحث. النمط نفسه ينطبق — فقط عدل علم اللغة وربما وسّع القاموس المخصص.

إذا وجدت هذا الدليل مفيدًا، امنحه نجمة على GitHub، شاركه مع زملائك، أو اترك تعليقًا أدناه. برمجة سعيدة، ولتكن نتائج OCR دائمًا خالية من الأخطاء!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}