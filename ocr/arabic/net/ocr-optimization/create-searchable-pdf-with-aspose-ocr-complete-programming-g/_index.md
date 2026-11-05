---
category: general
date: 2026-05-21
description: إنشاء ملف PDF قابل للبحث باستخدام Aspose OCR مع تحسين دقة OCR وتعلم كيفية
  تحميل الصورة للـ OCR في C#. دليل خطوة بخطوة.
draft: false
keywords:
- create searchable PDF
- improve OCR accuracy
- load image for OCR
- Aspose OCR C#
- PDF output with OCR
language: ar
og_description: إنشاء ملف PDF قابل للبحث باستخدام Aspose OCR. تعلّم كيفية تحسين دقة
  OCR وتحميل الصورة للـ OCR في مثال واحد قابل للتنفيذ.
og_title: إنشاء ملف PDF قابل للبحث باستخدام Aspose OCR – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF using Aspose OCR while you improve OCR accuracy
    and learn how to load image for OCR in C#. Step‑by‑step tutorial.
  headline: Create Searchable PDF with Aspose OCR – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- Aspose
- PDF
- C#
title: إنشاء ملف PDF قابل للبحث باستخدام Aspose OCR – دليل برمجي شامل
url: /ar/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث باستخدام Aspose OCR – دليل برمجة كامل

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من صورة ممسوحة ضوئياً لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يبدؤون أول مشروع OCR. الخبر السار هو أن Aspose OCR يجعل سير العمل بالكامل—تحميل الصورة، تحسين الصورة للحصول على نتائج أفضل، وأخيرًا حفظ PDF قابل للبحث—سهلًا للغاية.

في هذا الدليل سنستعرض مثالًا كاملاً من البداية إلى النهاية يوضح لك ليس فقط كيفية **إنشاء PDF قابل للبحث**، بل أيضًا كيفية **تحسين دقة OCR** والطريقة الصحيحة **لتحميل الصورة لـ OCR**. في النهاية ستحصل على تطبيق C# Console جاهز للتنفيذ ينتج PDF قابل للبحث مع تضمين الصورة الأصلية.

## ما ستتعلمه

- إعداد Aspose OCR (بما في ذلك تسريع GPU الاختياري)  
- تكوين المحرك للغة الفرنسية (أو أي لغة) **لتحسين دقة OCR**  
- **تحميل الصورة لـ OCR** بشكل صحيح باستخدام `ImageStream`  
- بناء خط أنابيب للفلتر لتنظيف الصورة قبل التعرف  
- حفظ النتيجة كملف PDF قابل للبحث مع تضمين الصورة المصدر  

لا توجد تبعيات خارجية بخلاف Aspose OCR، والكود يعمل على .NET 6+ (أو .NET Framework 4.6+). لنبدأ.

---

![مثال على PDF قابل للبحث تم إنشاؤه بواسطة Aspose OCR – مثال إنشاء PDF قابل للبحث](images/searchable-pdf-sample.png "مثال إنشاء PDF قابل للبحث")

## الخطوة 1: إنشاء PDF قابل للبحث – تفعيل GPU وتحديد مسار الموارد  

إذا كان لديك GPU متوافق، فإن تفعيله يمكن أن يسرّع عملية التعرف بشكل كبير. حتى إذا تخطيت هذه الخطوة، سيعمل باقي الكود بشكل جيد.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// Enable GPU acceleration (optional)
OcrEngine.EnableGpu(true);

// Tell Aspose where to find language data files (offline mode)
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");
```

**لماذا هذا مهم:** تسريع GPU يقلل من زمن الاستجابة عند معالجة دفعات كبيرة، وتحديد مسار الموارد يضمن أن المحرك يستطيع العمل بدون اتصال بالإنترنت—مثالي لخطوط CI أو البيئات المعزولة.

> **نصيحة احترافية:** إذا كنت تعمل على خادم بدون واجهة رسومية، تأكد من أن تعريفات CUDA تتطابق مع الإصدار المدمج مع Aspose OCR؛ الإصدارات غير المتطابقة قد تتسبب في فشل صامت.

## الخطوة 2: تحسين دقة OCR – اختيار اللغة الصحيحة  

اختيار نموذج اللغة المناسب هو فوز سريع للدقة. هنا نختار الفرنسية، لكن يمكنك استبدال `OcrLanguage.French` بأي لغة مدعومة.

```csharp
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.French   // improves OCR accuracy for French documents
};
```

**لماذا هذا مهم:** القواميس الخاصة بكل لغة تساعد المحرك على حل الأحرف المتشابهة (مثل “œ” مقابل “oe”). إذا تخطيت هذه الخطوة، سيستخدم المحرك اللغة الإنجليزية افتراضيًا، مما قد يقلل بشكل كبير من **تحسين دقة OCR** للنصوص غير الإنجليزية.

## الخطوة 3: تحميل الصورة لـ OCR – باستخدام ImageStream  

الآن نقوم **بتحميل الصورة لـ OCR**. المساعد `ImageStream.FromFile` يخفف عنك التعامل مع الـ Bitmap الخام ويعمل مع معظم الصيغ الشائعة (JPG، PNG، TIFF).

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

**لماذا هذا مهم:** تحميل الصورة بهذه الطريقة يضمن أن Aspose يتلقى الصورة بصيغة يمكنه معالجتها بكفاءة. إذا حاولت تمرير `Bitmap` مباشرة، قد تواجه مشاكل في إدارة الذاكرة مع الملفات الكبيرة.

## الخطوة 4: بناء خط أنابيب فلتر الصورة لتعزيز الدقة  

الصورة النظيفة هي نصف المعركة. الخط الأنابيب أدناه يقوم بتصحيح الميل وإزالة الضوضاء الخلفية—اثنان من أهم العوامل التي تعيق **تحسين دقة OCR**.

```csharp
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());   // corrects rotation
filterPipeline.Add(new DenoiseFilter()); // reduces grainy artifacts

// Apply the pipeline and replace the original image
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);
```

**لماذا هذا مهم:** تصحيح الميل يضمن أن خطوط النص أفقية، بينما إزالة الضوضاء تقلل من البقع الخاطئة. يمكنك إضافة فلاتر أخرى (مثل `ContrastFilter`) إذا كانت مسحاتك الأصلية سيئة جدًا.

## الخطوة 5: تنفيذ التعرف على النصوص  

بعد معالجة الصورة، نترك المحرك يقوم بسحره.

```csharp
ocrEngine.Recognize();
```

هذا السطر الواحد يُشغّل نموذج التعلم العميق خلف Aspose OCR. يملأ `ocrEngine.Text` بالنص العادي ويجهّز أيضًا مخرجات PDF.

> **ماذا لو ظهر النص مشوّهًا؟** تأكد من إعداد اللغة في الخطوة 2 وفكّر في إضافة `BinarizeFilter` إلى خط الأنابيب.

## الخطوة 6: حفظ النتيجة كملف PDF قابل للبحث  

الخطوة الأخيرة هي حفظ **PDF قابل للبحث** حيث يكون النص المستخرج خلف الصورة الأصلية—بالضبط ما تحتاجه للمستندات القانونية أو الأرشفة.

```csharp
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });
```

**لماذا هذا مهم:** `EmbedOriginalImage = true` يحافظ على جودة الصورة الأصلية مع السماح بالبحث النصي. إذا ضبطتها على `false`، سيحتوي PDF على النص المستخرج فقط، وهو ما قد يكون مفيدًا للأرشفة الخفيفة.

### اختياري: طباعة النص المستخرج وJSON  

إذا رغبت في فحص المخرجات الخام، هذه الأسطر تُظهر النص العادي وبيانات JSON منظمة.

```csharp
Console.WriteLine(ocrEngine.Text);               // plain text
Console.WriteLine(ocrEngine.GetResultAsJson());  // JSON with layout info
```

**الناتج المتوقع:** بعد تشغيل البرنامج، سترى الجملة (الجمل) الفرنسية مطبوعة في وحدة التحكم، تليها كائن JSON يحتوي على إطارات الحدود، درجات الثقة، وبيانات اللغة.

---

## مثال كامل جاهز للنسخ واللصق

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// 1️⃣ Enable GPU (optional) and set resources path
OcrEngine.EnableGpu(true);
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");

// 2️⃣ Create and configure the OCR engine (improve OCR accuracy)
var ocrEngine = new OcrEngine { Language = OcrLanguage.French };

// 3️⃣ Load the source image (load image for OCR)
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");

// 4️⃣ Build filter pipeline (deskew + denoise)
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());
filterPipeline.Add(new DenoiseFilter());
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);

// 5️⃣ Recognize text
ocrEngine.Recognize();

// 6️⃣ Save as searchable PDF (create searchable PDF)
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });

// Optional: output text and JSON
Console.WriteLine(ocrEngine.Text);
Console.WriteLine(ocrEngine.GetResultAsJson());
```

شغّل البرنامج، وجه `YOUR_DIRECTORY` إلى المجلد الذي يحتوي على `input.jpg` وموارد Aspose OCR، وستحصل على `output.pdf` بجواره مباشرة.

---

## الخلاصة

أصبح لديك الآن وصفة جاهزة للإنتاج **لإنشاء PDF قابل للبحث** باستخدام Aspose OCR، مع تعلم كيفية **تحسين دقة OCR** و**تحميل الصورة لـ OCR** بشكل صحيح. يغطي خط الأنابيب—GPU (اختياري) → اختيار اللغة → تحميل الصورة → سلسلة الفلاتر → التعرف → حفظ PDF—كل خطوة حاسمة، ويمكنك تعديلها للغات أخرى، دفعات أكبر، أو صيغ إخراج مختلفة.

ما الخطوة التالية؟ جرّب استبدال `PdfSaveOptions` بـ `DocxSaveOptions` لإنشاء مستندات Word قابلة للبحث، أو جرب فلاتر إضافية مثل `ContrastFilter`، أو دمج هذا الكود في API ASP.NET Core لتوليد PDF في الوقت الفعلي. الاحتمالات لا حصر لها، ومع الأساس الذي وضعناه هنا، أنت مجهّز جيدًا لمواجهة أي تحدٍ متعلق بـ OCR.

هل لديك أسئلة أو واجهت مشكلة؟ اترك تعليقًا، وتمنياتنا لك ببرمجة سعيدة!

## دروس ذات صلة

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}