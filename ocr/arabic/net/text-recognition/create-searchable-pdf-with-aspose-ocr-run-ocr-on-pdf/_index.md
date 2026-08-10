---
category: general
date: 2026-05-28
description: إنشاء ملف PDF قابل للبحث باستخدام Aspose OCR في C#. تعلّم كيفية تشغيل
  OCR على ملفات PDF، التعرف على نص PDF، وتحويل ملف PDF الممسوح ضوئياً باستخدام OCR
  إلى ملف PDF قابل للبحث.
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: ar
og_description: إنشاء ملف PDF قابل للبحث باستخدام Aspose OCR في C#. اتبع هذا الدليل
  خطوة بخطوة لتشغيل OCR على PDF، والتعرف على نص PDF، ومعالجة ملفات PDF الممسوحة ضوئياً
  باستخدام OCR.
og_title: إنشاء PDF قابل للبحث باستخدام Aspose OCR – تشغيل OCR على PDF
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: إنشاء ملف PDF قابل للبحث باستخدام Aspose OCR – تشغيل OCR على PDF
url: /ar/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث باستخدام Aspose OCR – تشغيل OCR على PDF

هل احتجت يوماً إلى **إنشاء ملفات PDF قابلة للبحث** من مجموعة من المستندات الممسوحة ضوئياً؟ لست وحدك. في العديد من سير عمل المكاتب، الشيء الوحيد الذي يمنعك من أرشيف كامل القابل للبحث هو بضع أسطر من الشيفرة التي تُجري OCR على صفحات PDF.  

في هذا الدرس سنستعرض مثالاً كاملاً جاهزاً للتنفيذ يوضح لك بالضبط كيفية **إنشاء ملفات PDF قابلة للبحث** باستخدام مكتبة Aspose OCR for .NET. في النهاية ستعرف كيف *تشغل OCR على PDF*، *تتعرف على نص ملفات PDF*، وتحوّل *PDF ممسوح ضوئياً باستخدام OCR* إلى نسخة قابلة للبحث دون أي خدمات طرف ثالث.

> **المتطلبات المسبقة** – .NET SDK حديث (يفضل 6.0+)، رخصة صالحة لـ Aspose.OCR for .NET (أو مفتاح تقييم مؤقت)، وملف PDF ترغب في معالجته.

![Create searchable PDF diagram](alt="Diagram illustrating the create searchable pdf workflow using Aspose OCR")  

---

## ما يغطيه هذا الدليل

- إعداد مكتبة Aspose OCR في مشروع C#.  
- تحميل ملف PDF المصدر (أي عدد من الصفحات).  
- تكوين المحرك لإنتاج **PDF قابل للبحث**.  
- تشغيل عملية OCR وحفظ النتيجة.  
- نصائح للتعامل مع المستندات متعددة الصفحات، اختيار اللغة، والمشكلات الشائعة.  

إذا اتبعت كل خطوة، ستحصل على ملف يمكنك فتحه في Adobe Reader، الضغط على **Ctrl + F**، والبحث فوراً عن أي كلمة ظهرت في المسح الأصلي.

---

## الخطوة 1: تثبيت Aspose OCR for .NET

قبل كتابة أي كود، أضف حزمة NuGet إلى مشروعك:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة محترف:** استخدم علامة `--version` لتثبيت أحدث إصدار ثابت (مثال: `Aspose.OCR 23.10`). هذا يضمن التوافق مع .NET 6 وما بعده.

---

## الخطوة 2: إنشاء كائن محرك OCR

قلب العملية هو `OcrEngine`. فكر فيه كالعقل الذي يقرأ الصور ويُخرج النص. تهيئته بسيطة:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

كائن `OcrEngine` سيحمل كل من تدفق صورة الإدخال والتكوين الذي يخبر Aspose بما تريد في المخرجات.

---

## الخطوة 3: تحميل ملف PDF المصدر (تشغيل OCR على PDF)

يمكن لـ Aspose OCR استيعاب PDF مباشرةً؛ فهو يستخرج كل صفحة كصورة داخلياً. استبدل مسار العنصر النائب بموقع المستند الممسوح ضوئياً الخاص بك:

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **لماذا يعمل هذا:** طريقة `ImageStream.FromFile` تكتشف تلقائياً تنسيق PDF وتُعد تمثيلاً نقطياً (Raster) للـ OCR. لا حاجة لخطوة تحويل إضافية.

---

## الخطوة 4: تكوين تنسيق الإخراج واللغة

هنا نخبر Aspose بما نريد استرجاعه. ضبط `OutputFormat` إلى `SearchablePdf` يوجه المحرك لإدراج النص المُتعرف عليه خلف صور الصفحات الأصلية، مما ينتج **PDF قابل للبحث**. يمكنك أيضاً اختيار اللغة لتحسين الدقة—الإنجليزية هي الافتراضية، لكن يمكنك التبديل إلى الفرنسية أو الألمانية وغيرها.

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

إذا كنت بحاجة لمعالجة مستند ثنائي اللغة، يمكنك دمج اللغات باستخدام أعلام تعداد `Language`.

---

## الخطوة 5: تشغيل عملية OCR – التعرف على نص PDF

الآن يحدث العمل الشاق. طريقة `Recognize` تمسح كل صفحة، تستخرج الحروف، وتبني تدفق PDF داخلي يحتوي على الصورة الأصلية وطبقة نصية غير مرئية. هذه هي الخطوة التي *نتعرف فيها على نص PDF*.

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **سؤال شائع:** *ماذا لو كان PDF يحتوي على 200 صفحة؟*  
> المعالج يعالج الصفحات تسلسلياً ويُرسل النتائج كتيار، لذا يبقى استهلاك الذاكرة معتدلاً. ومع ذلك، للملفات الكبيرة جداً قد ترغب في زيادة إعداد `MemoryLimit` في `ocrEngine.Configuration`.

---

## الخطوة 6: حفظ PDF القابل للبحث

أخيراً، اكتب النتيجة إلى القرص. طريقة `Save` تكتب التيار الداخلي إلى ملف جديد يمكنك فتحه بأي عارض PDF.

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

شغّل البرنامج (`dotnet run`) وسترى رسالة في وحدة التحكم تؤكد إنشاء الملف. افتح `handbook_searchable.pdf` وجرب البحث عن كلمة تعرف أنها موجودة في المسح الأصلي – يجب أن تظهر النتائج فوراً.

---

## معالجة الحالات الخاصة والسيناريوهات المتقدمة

### لغات متعددة (PDF ممسوح ضوئياً باستخدام OCR)

إذا كان PDF المصدر يحتوي على نص إنجليزي وإسباني، دمج اللغات:

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

سيتبدل Aspose OCR القواميس أثناء التشغيل، مما يعزز الدقة للمستندات المختلطة اللغات.

### ملفات PDF محمية بكلمة مرور

عند التعامل مع PDF مؤمن، قدم كلمة المرور قبل استدعاء `Recognize`:

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

إذا كانت كلمة المرور خاطئة، تُطلق `Recognize` استثناء `InvalidPasswordException`؛ التقاطه يتيح لك طلب كلمة مرور صحيحة من المستخدم.

### التحكم في جودة الصورة

كلما ارتفعت DPI زادت جودة نتائج OCR لكن يزداد استهلاك الذاكرة. عدّل DPI إذا لاحظت تشويش الأحرف:

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### الترخيص مقابل وضع التقييم

في وضع التقييم يظهر علامة مائية على كل صفحة. لإزالتها، طبّق رخصتك قبل أي استدعاء OCR:

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

---

## نصائح محترف للاستخدام في الإنتاج

- **المعالجة الدفعية:** ضع المنطق الأساسي داخل حلقة `foreach` تتنقل عبر قائمة من ملفات PDF. حرّر `OcrEngine` بعد كل ملف لتحرير الموارد الأصلية.  
- **التسجيل (Logging):** استخدم `ocrEngine.Configuration.Logger` لالتقاط إحصائيات OCR التفصيلية (مثل عدد الأحرف المُعترف بها في الثانية). هذا لا يقدر بثمن عند استكشاف الأخطاء المتعلقة بالدقة المنخفضة.  
- **تحسين الأداء:** للخوادم متعددة النوى، أنشئ كائنات `OcrEngine` منفصلة لكل خيط؛ المكتبة آمنة للخطوط عندما يكون كل مثال معزولاً.  
- **معالجة الأخطاء:** احط دائمًا `Recognize` و `Save` بكتل `try/catch`. الاستثناءات الشائعة تشمل `FileNotFoundException`، `OutOfMemoryException`، و `UnsupportedFormatException`.

---

## مثال كامل جاهز للنسخ واللصق

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**المخرجات المتوقعة** (وحدة التحكم):

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

افتح الملف الناتج، اضغط **Ctrl + F**، وستتمكن من العثور على أي كلمة ظهرت في الصفحات الممسوحة الأصلية. هذه هي سحر تحويل *PDF ممسوح ضوئياً باستخدام OCR* إلى **PDF قابل للبحث**.

---

## الخلاصة

لقد أظهرنا للتو كيفية **إنشاء ملفات PDF قابلة للبحث** باستخدام Aspose OCR for .NET، مع تغطية كل شيء من تثبيت الحزمة إلى التعامل مع ملفات PDF متعددة اللغات ومحميّة بكلمة مرور. باتباع هذه الخطوات يمكنك تشغيل OCR على مستندات PDF، *التعرف على نص PDF*، وتحويل أي *PDF ممسوح ضوئياً باستخدام OCR* إلى أصل قابل للبحث بالكامل.

### ما التالي؟

- استكشف المزيد من واجهة **aspose ocr pdf**: استخراج النص العادي، التصدير إلى DOCX، أو إنشاء ملفات PDF قابلة للبحث بالجملة.  
- دمج مخرجات PDF القابلة للبحث مع Aspose.PDF لإضافة فواصل مرجعية أو علامات مائية.  
- جرّب إعدادات DPI مختلفة أو قواميس OCR مخصصة للخطوط المتخصصة.

لا تتردد في تعديل العينة، دمجها في خط أنابيب إدارة المستندات الخاص بك، أو طرح الأسئلة في التعليقات. ترميز سعيد، واستمتع بتحويل تلك المسحات غير القابلة للقراءة إلى ذهب قابل للبحث!

## دروس ذات صلة

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cómo hacer OCR a PDF en .NET con Aspose.OCR](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [كيفية إجراء OCR لملف PDF في .NET باستخدام Aspose.OCR](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}