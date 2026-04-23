---
category: general
date: 2026-03-17
description: كيفية استخدام تقنية OCR لتحويل صورة إلى HTML بسرعة. تعلم استخراج النص
  من الصورة، التعرف على النص من ملف JPG، وإنشاء HTML باستخدام C# في دقائق.
draft: false
keywords:
- how to use OCR
- convert image to html
- extract text from image
- recognize text from jpg
- ocr image to html
language: ar
og_description: كيفية استخدام OCR لتحويل الصور إلى HTML مُصمم. يوضح لك هذا الدليل
  خطوة بخطوة كيفية استخراج النص من ملفات الصور وتوليد مخرجات HTML.
og_title: 'كيفية استخدام OCR: تحويل الصورة إلى HTML في C#'
tags:
- OCR
- C#
- Image Processing
title: 'كيفية استخدام OCR: تحويل الصورة إلى HTML في C#'
url: /ar/net/text-recognition/how-to-use-ocr-convert-image-to-html-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تستخدم OCR: تحويل الصورة إلى HTML في C#

هل تساءلت يومًا **كيف تستخدم OCR** لتحويل صورة قائمة طعام إلى HTML نظيف وقابل للبحث؟ لست وحدك—المطورون يحتاجون باستمرار إلى **استخراج النص من الصورة**، خاصةً عند التعامل مع الإيصالات، النشرات، أو ملفات PDF الممسوحة. الخبر السار؟ ببضع أسطر من C# يمكنك التعرف على النص من JPG، الحصول على السلاسل الخام، وكتابة صفحة HTML منسقة على الفور.

في هذا الدرس سنستعرض العملية بالكامل: من تحميل ملف JPEG، ضبط محرك OCR، إلى حفظ النتيجة كملف HTML. في النهاية ستعرف بالضبط **كيف تستخدم OCR**، وكيف **تحول الصورة إلى HTML**، ولماذا هذا الأسلوب يتفوق على النسخ واللصق اليدوي. لا خدمات خارجية، مجرد مكتبة صغيرة وقليل من الشيفرة.

> **ما ستحتاجه**  
> • .NET 6+ (أو .NET Framework 4.7 +).  
> • مكتبة OCR توفر `OcrEngine` (مثل Microsoft Azure Cognitive Services OCR، IronOCR، أو أي غلاف يطابق العينة).  
> • صورة تجريبية مثل `menu.jpg` موجودة في مجلد تملكه.  
> • محرر نصوص أو بيئة تطوير (Visual Studio Code تعمل جيدًا).

إذا كنت مهتمًا بـ **استخراج النص من الصورة** لصيغ أخرى لاحقًا، فإن النمط نفسه ينطبق—فقط غيّر مسار الملف وربما عدل تنسيق الإخراج.

---

![Diagram illustrating how to use OCR to convert image to HTML](/images/ocr-process.png){alt="مخطط يوضح كيفية استخدام OCR لتحويل الصورة إلى HTML"}

## الخطوة 1: إعداد المشروع وإضافة مكتبة OCR

قبل أن نتمكن من الإجابة على *كيف تستخدم OCR*، يجب أن نُشير إلى مكتبة تُنفّذ `OcrEngine`. لغرض هذا الدليل سنفترض وجود حزمة NuGet تسمى `Simple.Ocr` (استبدلها بالمزود الفعلي لديك).

```csharp
// Program.cs – top of the file
using System;
using System.IO;
using Simple.Ocr;          // <-- your OCR library
using Simple.Ocr.Models;   // optional, for OutputFormat enum
```

**لماذا هذا مهم:** استيراد المساحات الاسمية الصحيحة يمنحك الوصول إلى فئة `OcrEngine` وخيارات تكوينها. بدون ذلك سيظهر خطأ “type or namespace not found” من المترجم.

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن “Simple.Ocr” وقم بالتثبيت. نفس الأمر يعمل من سطر الأوامر: `dotnet add package Simple.Ocr`.

## الخطوة 2: تهيئة محرك OCR – جوهر *كيف تستخدم OCR*

الآن ننشئ مثيلًا، نخبره أننا نريد إخراجًا بصيغة HTML، ونحدده إلى الصورة التي نريد معالجتها.

```csharp
// Step 2: Initialise OCR engine
var ocrEngine = new OcrEngine();

// Choose HTML because it preserves basic styling (fonts, line breaks, etc.)
ocrEngine.Config.OutputFormat = OutputFormat.Html;

// Load the image (this is where we *recognize text from jpg*)
ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\menu.jpg");
```

**شرح:**  
- `OutputFormat.Html` يجعل المحرك يلف الكلمات المعترف بها بوسوم `<span>` مع خصائص النمط، وهو مثالي عندما تحتاج لاحقًا إلى **تحويل الصورة إلى HTML**.  
- `ImageStream.FromFile` يقرأ ملف JPEG إلى الذاكرة؛ يمكنك أيضًا تمرير `Stream` من طلب ويب إذا احتجت يومًا إلى **استخراج النص من الصورة** المستلمة عبر API.

## الخطوة 3: تشغيل عملية التعرف

مع تهيئة المحرك، يبدأ عمل OCR الفعلي. هذه هي اللحظة التي يقوم فيها المكتبة بمسح البكسلات، تطبيق نماذج التعلم الآلي، وإخراج النص.

```csharp
// Step 3: Perform OCR – this is the heart of *how to use OCR*
var ocrResult = ocrEngine.Recognize();

// The `Text` property contains the HTML string when OutputFormat.Html is set.
string htmlContent = ocrResult.Text;
```

**لماذا نخزن النتيجة:**  
كائن `ocrResult` غالبًا ما يحتوي على درجات الثقة ومربعات الحدود. بالنسبة لمعظم التحويلات البسيطة نحتاج فقط إلى `Text`، لكن يمكنك لاحقًا توسيعها لتسليط الضوء على الكلمات ذات الثقة المنخفضة أو إنشاء ملفات PDF قابلة للبحث.

## الخطوة 4: حفظ إخراج HTML

الآن بعد أن لدينا سلسلة HTML، نكتبها ببساطة إلى القرص. هذا يُكمل خط أنابيب **ocr image to html**.

```csharp
// Step 4: Save the HTML file
string outputPath = @"C:\MyImages\menu.html";
File.WriteAllText(outputPath, htmlContent);

Console.WriteLine($"✅ OCR complete! HTML saved to: {outputPath}");
```

**ما المتوقع:** افتح `menu.html` في المتصفح وسترى نص القائمة، مع الحفاظ على فواصل الأسطر وتنسيق الخط الأساسي. لا مزيد من النسخ واللصق اليدوي من لقطة الشاشة.

## مثال كامل جاهز للتنفيذ

بدمج كل ما سبق، إليك تطبيق console مستقل يمكنك وضعه في مشروع .NET جديد وتشغيله فورًا.

```csharp
// File: Program.cs
using System;
using System.IO;
using Simple.Ocr;
using Simple.Ocr.Models;

namespace OcrToHtmlDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialise OCR engine – the foundation of how to use OCR
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣  Choose HTML output – perfect for convert image to html scenarios
            // -------------------------------------------------
            ocrEngine.Config.OutputFormat = OutputFormat.Html;

            // -------------------------------------------------
            // 3️⃣  Load the source JPEG – this is where we recognize text from jpg
            // -------------------------------------------------
            string imagePath = @"C:\MyImages\menu.jpg";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 4️⃣  Run the OCR engine – the core of how to use OCR
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 5️⃣  Grab the HTML string – the final step of ocr image to html
            // -------------------------------------------------
            string html = ocrResult.Text;

            // -------------------------------------------------
            // 6️⃣  Write the HTML to disk
            // -------------------------------------------------
            string outputPath = @"C:\MyImages\menu.html";
            File.WriteAllText(outputPath, html);

            Console.WriteLine($"✅ Success! HTML saved at {outputPath}");
        }
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع:

```
✅ Success! HTML saved at C:\MyImages\menu.html
```

فتح `menu.html` يُظهر شيئًا مشابهًا لـ:

```html
<div style="font-family:Arial; font-size:12pt;">
  <p>Starters</p>
  <p>Bruschetta – $5.99</p>
  <p>Garlic Bread – $4.49</p>
  ...
</div>
```

العلامات الدقيقة تعتمد على مُسلسل HTML الخاص بمحرك OCR، لكن النقطة الأساسية هي أن **النص من JPG أصبح الآن HTML قابلًا للاستخدام**.

## الأسئلة المتكررة (FAQ)

**س: هل يمكنني تغيير الإخراج إلى نص عادي بدلاً من HTML؟**  
ج: بالتأكيد. استبدل `OutputFormat.Html` بـ `OutputFormat.Text`. هذا مفيد عندما تحتاج فقط إلى **استخراج النص من الصورة** للتحليلات.

**س: ماذا لو كانت صورتي بصيغة PNG أو BMP؟**  
ج: معظم مكتبات OCR تقبل أي صيغة نقطية. فقط غيّر امتداد الملف في `FromFile`. نفس خطوات **كيف تستخدم OCR** تنطبق.

**س: كيف أحسن الدقة للماسحات منخفضة الدقة؟**  
ج: عالج الصورة مسبقًا (زيادة التباين، تصحيح الميل، أو تكبير) قبل تمريرها إلى المحرك. بعض المكتبات توفر طريقة `Preprocess` يمكنك استدعاؤها على `ocrEngine.Image`.

**س: هل HTML الناتج آمن للإدراج مباشرة في صفحتي الويب؟**  
ج: عمومًا نعم، لكن قد ترغب في تنقيحه إذا كان مصدر الصورة قد يحتوي على سكريبتات خبيثة (نادر في مخرجات OCR، لكن الوقاية أفضل).

## الخاتمة

لقد غطينا الآن **كيف تستخدم OCR** لت **تحويل الصورة إلى HTML** في C#. من تهيئة المحرك، ضبطه لإخراج HTML، تحميل JPEG، تشغيل التعرف، إلى حفظ النتيجة—أصبح لديك حل كامل وقابل للتنفيذ ي **يستخرج النص من الصورة**، **يتعرف على النص من jpg**، ويُنتج ملف **ocr image to html** يمكنك تقديمه للمستخدمين أو تمريره إلى خطوط معالجة لاحقة.

هل تريد التعمق أكثر؟ جرّب:

* تصدير HTML إلى PDF باستخدام مكتبة مثل `iTextSharp`.  
* إضافة اكتشاف اللغة لتعيين حزم لغة OCR تلقائيًا.  
* دمج هذا الكود في API بـ ASP.NET Core بحيث يمكن للعملاء رفع الصور والحصول على HTML فورًا.

لا تتردد في التجربة، كسر الأشياء، وطرح الأسئلة في التعليقات. برمجة سعيدة، ولتكن مغامرات OCR دقيقة دائمًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}