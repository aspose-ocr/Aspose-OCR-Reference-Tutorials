---
category: general
date: 2026-02-11
description: تعلم كيفية تشغيل تقنية OCR على ملف TIFF متعدد الصفحات باستخدام C# و Aspose
  OCR. قم بتحويل TIFF إلى نص، استخراج النص من TIFF، وتعرف على النص من الصورة بسرعة.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: ar
og_description: كيفية تشغيل OCR على ملف TIFF متعدد الصفحات باستخدام Aspose OCR في
  C#. دليل خطوة بخطوة لتحويل TIFF إلى نص، استخراج النص من TIFF، والتعرف على النص من
  الصورة.
og_title: كيفية تشغيل OCR على صور TIFF متعددة الصفحات – دليل C# الكامل
tags:
- OCR
- C#
- Aspose
- TIFF
title: كيفية تشغيل OCR على صور TIFF متعددة الصفحات باستخدام Aspose OCR – دليل C#
url: /ar/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

text. Keep markdown syntax.

We need to translate all text, including bullet points, paragraphs, etc. Keep code block placeholders unchanged.

Also need to preserve links, but there are none except maybe in the tip "Manage NuGet Packages". That's not a link. So fine.

We must keep images none.

Let's produce Arabic translation.

We need to translate the introductory paragraph, steps, etc.

Make sure to keep code block placeholders as is.

Also keep the shortcodes unchanged.

Let's craft.

Note: For RTL, we can just write Arabic text; markdown will render.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR على صور TIFF متعددة الصفحات باستخدام Aspose OCR

هل تساءلت يومًا **كيف تشغّل OCR** على ملف TIFF ممسوح ضوئيًا يحتوي على عدة صفحات؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يحتاجون لاستخراج نص قابل للبحث من مستندات قديمة. الخبر السار؟ باستخدام Aspose OCR يمكنك التعرف على النص من ملفات الصور ببضع أسطر من كود C# فقط، وستحصل على نص عادي متسلسل جاهز للفهرسة أو المعالجة الإضافية.

في هذا الدرس سنستعرض سير العمل بالكامل: من تثبيت حزمة Aspose OCR، تحميل صورة TIFF متعددة الصفحات، إلى تحويل TIFF إلى نص وأخيرًا عرض المحتوى المستخرج. بنهاية الدرس ستكون قادرًا على **استخراج النص من ملفات TIFF**، **التعرف على النص من صورة**، وحتى أتمتة العملية لمئات الملفات في مهمة دفعة. لا سحر، فقط خطوات واضحة وعملية.

## ما ستتعلمه

- كيفية إعداد محرك Aspose OCR للتعرف على اللغة الإنجليزية.  
- الكود الدقيق اللازم **لتحويل TIFF إلى نص** باستخدام الفئة `OcrEngine`.  
- نصائح للتعامل مع الصور متعددة الصفحات وضمان فصل كل صفحة بشكل صحيح.  
- الأخطاء الشائعة (مثل فقدان الاعتمادات الأصلية) وكيفية تجنبها.  

**المتطلبات المسبقة** – ستحتاج إلى .NET 6 أو أحدث، Visual Studio (أو أي محرر C#)، واتصال بالإنترنت لميزة تنزيل الموارد تلقائيًا. هذا كل ما تحتاجه؛ لا مكتبات أصلية إضافية للتعامل معها.

---

## الخطوة 1 – تثبيت حزمة Aspose OCR عبر NuGet

قبل أن تتمكن من **إجراء OCR على ملفات الصورة** يجب إضافة المكتبة إلى مشروعك.

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تعمل داخل Visual Studio، يمكنك أيضًا النقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → البحث عن “Aspose.OCR” ثم النقر على *Install*.

الحزمة تتضمن كل ما تحتاجه، ومع `AutomaticResourceDownload = true` سيقوم المحرك بتنزيل حزم اللغات تلقائيًا عند الحاجة.

---

## الخطوة 2 – تهيئة محرك OCR (كيفية تشغيل OCR)

الآن بعد أن أصبحت الحزمة موجودة، نقوم بإنشاء وتكوين كائن `OcrEngine`. هذا هو قلب **كيفية تشغيل OCR** في سيناريونا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**لماذا هذا مهم:** ضبط `Language` يخبر المحرك بمجموعة الأحرف المتوقعة، بينما `AutomaticResourceDownload` يوفر عليك وضع ملفات اللغة يدويًا على الخادم. `OutputFormat` كـ `Text` يمنحنا سلسلة نصية بسيطة—مثالية لخطوط **تحويل TIFF إلى نص**.

---

## الخطوة 3 – تحميل صورة TIFF متعددة الصفحات (التعرف على النص من صورة)

يمكن أن يحتوي ملف TIFF على عدة إطارات، كل إطار يمثل صفحة. فئة `System.Drawing.Image` تج abstracts ذلك لنا.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **ماذا لو لم يكن الملف في نفس المجلد؟** قدم مسارًا مطلقًا كاملاً أو استخدم `Path.Combine` مع `AppContext.BaseDirectory`.  
> **ماذا عن استهلاك الذاكرة؟** جملة `using` تُفرغ الصورة بعد المعالجة، مما يمنع التسرب—وهو أمر حاسم عند معالجة عشرات ملفات TIFF الكبيرة على دفعة.

نداء `Recognize` يت iterates تلقائيًا على كل صفحة في TIFF، ويجمع النتائج مع فواصل أسطر. لهذا السبب سترى كل صفحة مفصولة عند طباعة `ocrResult.Text`.

---

## الخطوة 4 – مثال كامل يعمل (جميع الخطوات في ملف واحد)

فيما يلي تطبيق console كامل جاهز للتنفيذ. انسخه والصقه في مشروع .NET console جديد واضغط **F5**.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**الناتج المتوقع** (مقتطع للاختصار):

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

كل صفحة تظهر في سطر منفصل لأن `OcrOutputFormat.Text` يضيف فاصل سطر بين الإطارات. إذا احتجت فاصلًا مختلفًا، يمكنك معالجة `result.Text` لاحقًا باستخدام `String.Replace`.

---

## الخطوة 5 – معالجة الحالات الشائعة

### 5.1 ملفات TIFF الكبيرة  
عند التعامل مع ملفات TIFF بحجم جيجابايت، قد يكون تحميل الملف بالكامل في الذاكرة مشكلة. حل بديل هو معالجة كل إطار على حدة:

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. مستندات غير إنجليزية  
إذا كنت بحاجة إلى **التعرف على النص من صورة** بالإسبانية أو الفرنسية، فقط غير خاصية `Language`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

ستقوم Aspose بتنزيل موارد اللغة المناسبة تلقائيًا.

### 5. حفظ الناتج  
غالبًا ما تريد **تحويل TIFF إلى نص** وتخزين النتيجة في ملف `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

يمكنك أيضًا تقسيم الناتج حسب الصفحة باستخدام `String.Split(Environment.NewLine)` وكتابة كل جزء إلى ملف منفصل.

---

## نصائح احترافية وملاحظات

- **AutomaticResourceDownload** يعمل في المرة الأولى التي تشغل فيها التطبيق؛ التشغيلات اللاحقة تكون دون اتصال.  
- إذا رأيت أحرفًا مشوشة، تحقق من إعداد `Language`؛ حزم اللغة غير المتطابقة تسبب أخطاء في التعرف.  
- بالنسبة لملفات PDF التي تم تحويلها إلى TIFF، قد ترغب في زيادة `ocrEngine.Dpi` (القيمة الافتراضية 300) للحصول على دقة أعلى.  
- احرص دائمًا على وضع `Image.FromFile` داخل كتلة `using`؛ وإلا ستبقى الملف مقفولًا ولن تتمكن من حذفه أو نقله لاحقًا.

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات TIFF ذات صفحة واحدة؟**  
ج: بالتأكيد. يعامل المحرك ملف TIFF ذو إطار واحد بنفس الطريقة؛ ستحصل على سطر نص واحد فقط.

**س: هل يمكنني معالجة ملفات PNG أو JPEG بنفس الطريقة؟**  
ج: نعم—فقط غيّر امتداد الملف. طريقة `Recognize` تقبل أي تنسيق `System.Drawing.Image`.

**س: ماذا لو أردت الحصول على نتيجة OCR كملف PDF بدلاً من نص عادي؟**  
ج: اضبط `OutputFormat = OcrOutputFormat.Pdf` وستحتوي `ocrResult` على مصفوفة بايتات PDF يمكنك كتابتها إلى القرص.

---

## الخلاصة

أصبح لديك الآن حل شامل من البداية إلى النهاية **لتشغيل OCR** على ملفات TIFF متعددة الصفحات باستخدام Aspose OCR في C#. من خلال تكوين المحرك، تحميل الصورة، واستدعاء `Recognize`، يمكنك **استخراج النص من TIFF**، **تحويل TIFF إلى نص**، و**التعرف على النص من صورة** ببضع أسطر من الكود فقط. لا تتردد في تعديل اللغة، تنسيق الإخراج، أو المعالجة إطارًا بإطار لتناسب احتياجاتك في المعالجة الدفعية.

هل أنت مستعد للخطوة التالية؟ جرّب دمج هذا النهج مع خدمة مراقبة مجلد لتقوم تلقائيًا **بإجراء OCR على ملفات الصورة** عندما تصل إلى مجلد الإدخال، أو دمج الناتج في فهرس بحث للحصول على بحث نص كامل فوري. الاحتمالات لا حصر لها، والكود الذي رأيته الآن هو أساس قوي.

إذا واجهت أي صعوبات، اترك تعليقًا أدناه أو تواصل معي عبر GitHub. برمجة سعيدة، واستمتع بتحويل ملفات TIFF العنيدة إلى نص قابل للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}