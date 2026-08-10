---
category: general
date: 2026-06-19
description: 'التعرف على النص من الصورة باستخدام Aspose OCR في C#: دليل خطوة بخطوة
  لتحويل الصورة إلى نص واستخراج النص من ملفات JPG.'
draft: false
keywords:
- recognize text from image
- extract text from jpg
- convert image to text
- perform ocr on image
- set ocr language
language: ar
og_description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية ضبط
  لغة OCR، استخراج النص من ملف JPG، وتحويل الصورة إلى نص في دقائق.
og_title: التعرف على النص من الصورة في C# – تحويل الصورة إلى نص
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  headline: recognize text from image in C# – Convert Image to Text
  type: TechArticle
- description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  name: recognize text from image in C# – Convert Image to Text
  steps:
  - name: 5.1 Low‑Resolution Images
    text: OCR accuracy drops sharply below 100 dpi. If you notice garbled output,
      try pre‑processing the image (increase contrast, resize, or apply a sharpening
      filter) before feeding it to Aspose OCR.
  - name: 5.2 Multi‑Page Documents
    text: "Even though Community mode caps at 100 pages, you can still process PDFs
      or multi‑page TIFFs. The engine will return concatenated text, preserving page
      breaks with `\f`."
  - name: 5.3 Non‑English Languages
    text: 'Switch the `Language` enum to another supported value:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: التعرف على النص من الصورة في C# – تحويل الصورة إلى نص
url: /ar/net/text-recognition/recognize-text-from-image-in-c-convert-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في C# – تحويل الصورة إلى نص

هل احتجت يومًا إلى **التعرف على النص من صورة** لكنك لم تكن متأكدًا أي مكتبة ستتيح لك ذلك دون رسوم ترخيص باهظة؟ لست وحدك. في هذا الدرس سنستعرض استخدام وضع المجتمع المجاني لـ Aspose OCR **لتحويل الصورة إلى نص**، استخراج النص من ملفات jpg، وحتى **تعيين لغة OCR** للسيناريوهات متعددة اللغات.

سنغطي كل شيء من تثبيت حزمة NuGet إلى معالجة الحالات الخاصة مثل ملفات PDF متعددة الصفحات أو الصور منخفضة الدقة. في النهاية ستحصل على تطبيق كونسول قابل للتنفيذ يمكنه **إجراء OCR على الصور** في لمح البصر.

## ما ستحتاجه

- .NET 6 SDK أو أحدث (الكود يعمل مع .NET Core 3.1+ أيضًا)  
- Visual Studio 2022 أو أي محرر تفضله  
- ملف صورة (JPG, PNG, BMP…) يحتوي على نص قابل للقراءة  
- اتصال بالإنترنت لجلب حزمة NuGet `Aspose.OCR`  

هذا كل شيء—لا ملفات DLL إضافية، لا خدمات خارجية، فقط C# نقي.

![مثال على التعرف على النص من صورة](https://example.com/ocr-screenshot.png "مثال على التعرف على النص من صورة")

*(تظهر لقطة الشاشة مخرجات الكونسول بعد التعرف على صورة JPG تجريبية.)*

## الخطوة 1: تثبيت Aspose  OCR عبر NuGet

أولاً، أضف مكتبة Aspose  OCR إلى مشروعك. افتح طرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

تأتي الحزمة مع **وضع المجتمع** الذي يحدّ من المعالجة إلى 100 صفحة لكل تشغيل، وهو مثالي للتجارب الصغيرة. إذا احتجت إلى حدود أعلى في المستقبل، يمكنك الترقية إلى ترخيص مدفوع لاحقًا—دون الحاجة لتغييرات في الكود.

## الخطوة 2: تكوين محرك OCR (تعيين لغة OCR)

قبل أن تتمكن من **إجراء OCR على صورة**، يجب إبلاغ المحرك باللغة المتوقعة. اللغة الافتراضية هي الإنجليزية، لكن يمكنك التبديل إلى الإسبانية أو الفرنسية أو حتى الصينية بسطر واحد.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;

// Choose the language you need – here we stick with English.
var ocrConfig = new OcrEngineConfig
{
    Language = Language.English,      // set ocr language
    MaxPagesPerRun = 100              // enforced limit in Community mode
};
```

لماذا اللغة مهمة؟ نماذج OCR مدربة على مجموعات أحرف معينة؛ إمداد نموذج إنجليزي بوثيقة فرنسية سيفقده العلامات والربط. ضبط اللغة الصحيحة يحسّن الدقة بشكل كبير.

## الخطوة 3: إنشاء محرك OCR والتعرف على الصورة

مع إعداد التكوين جاهزًا، أنشئ المحرك داخل كتلة `using` حتى يتم تحرير الموارد تلقائيًا. ثم استدعِ `RecognizeImage` مع مسار ملف JPG الخاص بك (أو أي صيغة مدعومة).

```csharp
// Step 3: Create the OCR engine and recognize the image
using var ocrEngine = new OcrEngine(ocrConfig);

// Replace with the actual path to your image file.
string imagePath = @"YOUR_DIRECTORY/sample.jpg";

// Perform OCR – this will **recognize text from image**.
var ocrResult = ocrEngine.RecognizeImage(imagePath);
```

بعض النقاط التي يجب ملاحظتها:

- **سلامة الخيوط:** كائن `OcrEngine` غير آمن للاستخدام المتعدد الخيوط. إذا كنت تخطط لمعالجة العديد من الصور بشكل متزامن، أنشئ محركًا منفصلًا لكل خيط.
- **الصيغ المدعومة:** بخلاف JPG، يمكنك إمداد PNG، BMP، TIFF، وحتى PDF. نفس الطريقة تعمل، لذا يمكنك **استخراج النص من jpg** أو أي صورة نقطية أخرى.

## الخطوة 4: إخراج النص المتعرف عليه (تحويل الصورة إلى نص)

الآن بعد أن أنجز محرك OCR مهمته، يتم تخزين النتيجة في كائن `OcrResult`. خاصية `Text` تحتوي على تمثيل النص العادي لكل ما استطاع المحرك قراءته.

```csharp
// Step 4: Write the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

إذا شغّلت البرنامج مع لقطة شاشة واضحة لإيصال، سترى شيئًا مثل:

```
=== OCR Output ===
Item        Qty   Price
Apple       2     $1.20
Banana      5     $0.75
Total               $5.55
```

هذه هي جوهر **تحويل الصورة إلى نص**—الصورة الآن تمثل سلسلة نصية يمكنك تخزينها، البحث فيها، أو تمريرها إلى نظام آخر.

## الخطوة 5: معالجة الحالات الخاصة الشائعة

### 5.1 صور منخفضة الدقة

تنخفض دقة OCR بشكل حاد تحت 100 dpi. إذا لاحظت مخرجات مشوشة، حاول معالجة الصورة مسبقًا (زيادة التباين، تغيير الحجم، أو تطبيق مرشح تعزيز) قبل إمدادها إلى Aspose OCR.

```csharp
// Example: Resize a low‑dpi image to improve accuracy
using var bitmap = new Bitmap(imagePath);
var highRes = new Bitmap(bitmap, new Size(bitmap.Width * 2, bitmap.Height * 2));
highRes.Save("highres_sample.jpg");
var highResResult = ocrEngine.RecognizeImage("highres_sample.jpg");
```

### 5.2 مستندات متعددة الصفحات

على الرغم من أن وضع المجتمع يحدّ من 100 صفحة، يمكنك ما زال معالجة ملفات PDF أو TIFF متعددة الصفحات. سيعيد المحرك نصًا متسلسلًا، مع الحفاظ على فواصل الصفحات باستخدام `\f`.

```csharp
var multiPageResult = ocrEngine.RecognizeImage("multi_page.pdf");
Console.WriteLine(multiPageResult.Text); // contains form‑feed characters between pages
```

### 5.3 لغات غير إنجليزية

غيّر تعداد `Language` إلى قيمة مدعومة أخرى:

```csharp
ocrConfig.Language = Language.French; // now the engine expects French characters
```

تذكر تثبيت حزم اللغات المناسبة إذا تجاوزت المجموعة الافتراضية؛ Aspose توفرها كحزم NuGet منفصلة.

## الخطوة 6: مثال كامل يعمل

بجمع كل شيء معًا، إليك تطبيق كونسول كامل جاهز للنسخ واللصق يقوم بـ **التعرف على النص من صورة**، **استخراج النص من jpg**، و **تعيين لغة OCR** حسب الحاجة.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Configuration;

class OcrDemo
{
    static void Main()
    {
        // 1️⃣ Configure OCR – change Language to match your source.
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.English,   // set ocr language
            MaxPagesPerRun = 100
        };

        // 2️⃣ Create the engine inside a using block.
        using var ocrEngine = new OcrEngine(ocrConfig);

        // 3️⃣ Path to the image you want to process.
        string imagePath = @"YOUR_DIRECTORY/sample.jpg";

        // 4️⃣ Perform OCR – this **recognize text from image**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 5️⃣ Output – now you have **convert image to text** results.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**المخرجات المتوقعة** (بافتراض أن الصورة التجريبية تحتوي على النص “Hello World!”):

```
=== OCR Output ===
Hello World!
```

شغّل البرنامج باستخدام `dotnet run` وسترى الكونسول يعرض السلسلة المستخرجة.

## نصائح احترافية ومخاطر شائعة

- **نصيحة احترافية:** غلف استدعاء OCR بكتلة `try/catch` للتعامل مع الملفات التالفة بشكل سلس.  
- **احذر من:** الصور التي تحتوي على علامات مائية أو ضوضاء خلفية قوية؛ غالبًا ما تُربك المحرك.  
- **نصيحة:** إذا كنت بحاجة لمعالجة دفعة من الملفات، قم بالتكرار عبر مدخلات الدليل وأعد استخدام نفس كائن `OcrEngine`—فقط تذكر إعادة ضبط أي إعدادات خاصة بكل صورة.  
- **تذكر:** حد 100 صفحة في وضع المجتمع هو لكل تشغيل، وليس لكل ملف. قسّم ملفات PDF الكبيرة إذا وصلت إلى الحد.

## الخلاصة

أصبح لديك الآن مقتطف قوي جاهز للإنتاج ي **يتعرف على النص من صورة** باستخدام Aspose OCR في C#. من تثبيت حزمة NuGet إلى **تعيين لغة OCR**، ومعالجة الصور منخفضة الدقة، وأخيرًا **تحويل الصورة إلى نص**، تم تغطية كل خطوة. لا تتردد في التجربة—غيّر اللغة، استخدم PNGs، أو اربط المخرجات مع فهرس بحث لاحق.

بعد ذلك، قد تستكشف **استخراج النص من jpg** على نطاق واسع بدمج هذا الكود في Azure Function، أو تغوص أعمق في ميزات Aspose OCR المتقدمة مثل تحليل التخطيط والتعرف على الخط اليدوي. الاحتمالات لا حصر لها، والأساس الذي بنيته اليوم سيجعل هذه الإضافات سهلة.

برمجة سعيدة، ولتكن صورك دائمًا قابلة للقراءة!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [التعرف على نص الصورة باستخدام Aspose OCR لعدة لغات](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}