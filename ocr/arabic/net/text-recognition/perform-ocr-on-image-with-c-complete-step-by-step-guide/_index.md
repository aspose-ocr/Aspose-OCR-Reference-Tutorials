---
category: general
date: 2026-05-21
description: تنفيذ التعرف الضوئي على الحروف (OCR) على صورة باستخدام C#. تعلّم كيفية
  تحميل الصورة للتعرف الضوئي على الحروف، استخراج النص من ملف PNG، والتعرف على النص
  من الصورة باستخدام عينة شفرة صغيرة.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: ar
og_description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على صورة في C# بسرعة. يوضح
  هذا الدليل كيفية تحميل الصورة للتعرف الضوئي على الأحرف، استخراج النص من PNG، والتعرف
  على النص من الصورة مع إخراج HTML يدرك التخطيط.
og_title: إجراء التعرف الضوئي على الحروف في الصورة باستخدام C# – دليل برمجة كامل
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: إجراء التعرف الضوئي على الحروف (OCR) في الصورة باستخدام C# – دليل كامل خطوة
  بخطوة
url: /ar/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنفيذ OCR على صورة باستخدام C# – دليل خطوة‑بخطوة كامل

هل تساءلت يوماً كيف **تنفّذ OCR على ملفات الصورة** دون الحاجة إلى واجهات رسومية ثقيلة؟ لست وحدك. سواءً كنت تقوم برقمنة الإيصالات، استخراج البيانات من النماذج الممسوحة، أو مجرد تحويل PNG إلى نص قابل للبحث، بضع أسطر من C# يمكنها إنجاز المهمة.

في هذا البرنامج التعليمي سنستعرض تحميل صورة لـ OCR، التعرف على النص من الصورة، وأخيراً استخراج النص من PNG كـ HTML نظيف. في النهاية ستحصل على تطبيق وحدة تحكم جاهز للتنفيذ **ينفّذ OCR على ملفات الصورة** ويحافظ على التخطيط الأصلي.

## ما ستبنيه

- برنامج وحدة تحكم بسيط يقرأ PNG (أو أي صورة مدعومة)  
- يستخدم محرك OCR **للتعرف على النص من الصورة**  
- يحفظ النتيجة كـ HTML مع الحفاظ على التخطيط، مدمجاً الصورة الأصلية  
- يوضح كيف **تحمّل صورة لـ OCR**، **استخراج النص من PNG**، وكيفية التعامل مع الحالات الشائعة  

> **المتطلبات المسبقة**  
> - .NET 6.0 SDK أو أحدث (يمكنك أيضاً استهداف .NET Framework 4.7+)  
> - مكتبة OCR متوافقة مع NuGet – المثال يستخدم *Aspose.OCR* لكن أي مكتبة ذات API مشابهة ستعمل  
> - معرفة أساسية بـ C# (لا شيء معقّد)  

هل لديك كل ذلك؟ رائع—هيا نبدأ.

## تنفيذ OCR على صورة – استعراض كامل للكود

فيما يلي البرنامج **الكامل القابل للتنفيذ**. انسخه والصقه في مشروع وحدة تحكم جديد (`dotnet new console`) ثم اضغط **F5**.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **المخرجات المتوقعة**  
> ```
> HTML with layout saved.
> ```  
> بعد التشغيل ستجد `form.html` بجوار ملف PNG الخاص بك. افتحه في المتصفح وسترى نفس التخطيط، لكن الآن النص قابل للتحديد والبحث.

### تحميل صورة لـ OCR

السطر `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` هو المكان الذي **نحمّل فيه صورة لـ OCR**. أداة `ImageStream` تُجرد تفاصيل تنسيق الملف، لذا يمكنك إمداد JPEG أو BMP أو TIFF دون تعديل الكود.  

**لماذا لا نمرّر `Bitmap` مباشرة؟**  
لأن العديد من SDKs الخاصة بـ OCR تتوقع تدفقًا (stream) يحمل أيضًا بيانات DPI. استخدام محمل المكتبة المدمج يضمن أن المحرك يرى الصورة تمامًا كما تظهر على الشاشة، مما يحسّن الدقة.

#### نصيحة احترافية
إذا كنت تعالج دفعة من الملفات، غلف خطوة التحميل داخل `try/catch` وسجّل أي `FileNotFoundException`. هذا يمنع تعطل الدفعة بالكامل بسبب ملف مفقود واحد.

### استخراج النص من PNG

بعد انتهاء `engine.Recognize()`، يحتفظ محرك OCR بالنص المُعترف به داخليًا. يمكنك سحب النص كسلسلة إذا كنت تحتاج فقط النص الخام:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

هذه أسرع طريقة **لاستخراج النص من PNG** عندما لا يهمك التخطيط. لمعظم وظائف إدخال البيانات، النص العادي يكفي—فقط تذكّر إزالة فواصل الأسطر إذا كنت تخطط لاستيراده إلى CSV.

### التعرف على النص من الصورة

استدعاء `Recognize()` هو ما يقوم بالعمل الشاق. تحت الغطاء، يقوم المحرك بـ:

1. تطبيع الصورة (إزالة الميل، إزالة الضوضاء)  
2. تقسيمها إلى أسطر وكلمات  
3. تشغيل مصنف شبكة عصبية مدربة على ملايين الرموز  

لأننا عيّنّا `Language = OcrLanguage.English`، يستخدم المحرك قواميس خاصة بالإنجليزية، مما يقلل الأخطاء بشكل كبير. إذا كنت تحتاج دعمًا متعدد اللغات، ما عليك سوى تمرير مصفوفة من اللغات:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### معالجة إخراج HTML مع الحفاظ على التخطيط

معظم المطورين يتوقفون عند النص العادي، لكن `HtmlSaveOptions` التي استخدمناها تتيح لك **تنفيذ OCR على صورة** مع الحفاظ على البنية البصرية. هناك علامتان مهمتان:

- `PreserveLayout = true` – يحافظ على الأعمدة والجداول والمسافات.  
- `EmbedImages = true` – يدرج PNG الأصلي كعنصر `<img>` مشفر بـ Base64، بحيث يكون HTML مستقلًا.

إذا كنت تفضّل ملفًا أخف، عيّن `EmbedImages = false` وسيشير HTML إلى PNG الأصلي على القرص بدلاً من ذلك.

#### حالة خاصة: ملفات كبيرة

للصور التي يزيد حجمها عن 5 ميغابايت، قد يؤدي تضمين الصورة إلى تضخم حجم HTML. في مثل هذه الحالات، استخدم مراجع صور خارجية وفكّر في ضغط PNG مسبقًا باستخدام `ImageProcessor.Compress`.

## مشاكل شائعة ونصائح احترافية

| العرض | السبب المحتمل | الحل |
|--------|--------------|-----|
| أحرف مشوشة | تعيين لغة خاطئة أو نقص حزمة اللغة | ثبّت ملفات بيانات اللغة المناسبة وعين `engine.Language` بشكل صحيح |
| لا نص في الإخراج | الصورة مظلمة جدًا أو منخفضة الدقة | عالج مسبقًا بـ `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` |
| التخطيط مكسور في HTML | ترك `PreserveLayout` على القيمة الافتراضية `false` | عيّن `PreserveLayout = true` في `HtmlSaveOptions` |
| معالجة بطيئة لعدد كبير من الصفحات | إعادة تهيئة المحرك لكل ملف | أعد استخدام نفس كائن `OcrEngine` وغيّر فقط `engine.Image` في كل حلقة |

### التوسع لمعالجة ملفات متعددة

إذا كنت تحتاج إلى **تنفيذ OCR على صورة** لملفات داخل مجلد، غلف المنطق الأساسي في حلقة بسيطة:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

لاحظ أننا **نحمّل صورة لـ OCR** داخل الحلقة، لكننا نحتفظ بنفس كائنات `engine` و `htmlOptions`. هذا يقلل من استهلاك الذاكرة ويسرّع وظائف الدفعات.

## ما بعد ذلك: التصدير إلى PDF أو DOCX

يمكن لنفس `engine` حفظ النتائج بصيغ أخرى:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

إذا كان نظامك النهائي يتطلب ملفات PDF قابلة للبحث، فهذا تعديل سطر واحد—لا حاجة لخط أنابيب تحويل منفصل.

## الخلاصة

لقد أظهرنا لك كيف **تنفّذ OCR على صورة** باستخدام C#، من تحميل الصورة إلى **استخراج النص من PNG** وأخيرًا **التعرف على النص من الصورة** وحفظه كملف HTML مع الحفاظ على التخطيط. المثال الكامل جاهز للتنفيذ، والآن تفهم لماذا كل خطوة مهمة، وكيفية تعديلها للغات مختلفة، وما هي الأخطاء التي يجب الانتباه لها.

الخطوة التالية: جرّب استبدال اللغة الإنجليزية بلغة أخرى، جرب `PreserveLayout = false` للحصول على HTML أخف، أو صلّ إخراج النص العادي بقاعدة بيانات لأرشفة قابلة للبحث. السماء هي الحد عندما تجمع محرك OCR قوي مع بضع أسطر من C#.

هل لديك أسئلة حول معالجة ملفات TIFF متعددة الصفحات، أو تريد معرفة كيفية دمج هذا في API بـ ASP.NET Core؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

## دروس ذات صلة

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}