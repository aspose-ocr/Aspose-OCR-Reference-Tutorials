---
category: general
date: 2026-07-05
description: إجراء التعرف الضوئي على الأحرف (OCR) على صورة باستخدام Aspose.OCR في
  C#. تعلم كيفية تحميل الصورة للتعرف الضوئي على الأحرف، ومعالجة الصورة مسبقًا قبل
  التعرف، واستخراج النص من الإيصال مع تحسين دقة التعرف.
draft: false
keywords:
- perform OCR on image
- extract text from receipt
- improve OCR accuracy
- load image for OCR
- preprocess image before OCR
language: ar
og_description: إجراء التعرف الضوئي على الأحرف (OCR) على صورة باستخدام C# و Aspose.OCR.
  يوضح هذا الدليل كيفية تحميل الصورة للتعرف الضوئي على الأحرف، ومعالجة الصورة مسبقًا
  قبل التعرف الضوئي على الأحرف، واستخراج النص من الفاتورة مع تحسين دقة التعرف الضوئي
  على الأحرف.
og_title: إجراء OCR على صورة باستخدام Aspose – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Aspose.OCR in C#. Learn how to load image
    for OCR, preprocess image before OCR, and extract text from receipt while improving
    OCR accuracy.
  headline: Perform OCR on Image with Aspose – Complete C# Guide
  type: TechArticle
- description: Perform OCR on image using Aspose.OCR in C#. Learn how to load image
    for OCR, preprocess image before OCR, and extract text from receipt while improving
    OCR accuracy.
  name: Perform OCR on Image with Aspose – Complete C# Guide
  steps:
  - name: '**Load** the picture file into memory.'
    text: '**Load** the picture file into memory.'
  - name: '**Preprocess** it: deskew, denoise, and boost contrast.'
    text: '**Preprocess** it: deskew, denoise, and boost contrast.'
  - name: '**Run** the OCR engine.'
    text: '**Run** the OCR engine.'
  - name: '**Read** the resulting text.'
    text: '**Read** the resulting text.'
  type: HowTo
- questions:
  - answer: Aspose.OCR works best with printed text. For cursive or mixed fonts you
      may need a specialized handwriting model or a different library.
    question: What if the receipt is handwritten?
  - answer: Yes—convert each PDF page to an image (`Aspose.PDF` can help) and feed
      those images into the same pipeline.
    question: Can I process PDFs directly?
  - answer: Wrap the core logic inside a `foreach` loop that iterates over a folder
      of images. Remember to dispose of the `OcrEngine` after each file to free memory.
    question: Is there a way to batch‑process many receipts?
  - answer: Aspose offers a free evaluation with a watermark. For production use,
      purchase a license to remove the watermark and unlock full performance.
    question: Do I need a license?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- Image Processing
title: إجراء OCR على الصورة باستخدام Aspose – دليل C# الكامل
url: /ar/net/ocr-optimization/perform-ocr-on-image-with-aspose-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنفيذ OCR على الصورة باستخدام Aspose – دليل C# كامل

هل احتجت يومًا إلى **perform OCR on image** للملفات لكن النتائج كانت غير واضحة، أو فقدت أحرفًا، أو كانت خاطئة تمامًا؟ لست وحدك—مسح الإيصالات، الفواتير، أو الملاحظات المكتوبة بخط اليد غالبًا ما يتحول إلى لعبة تخمين. في هذا الدليل سنستعرض طريقة عملية لـ **load image for OCR**، تنظيفها، وأخيرًا **extract text from receipt** مع تحسين ملحوظ في **improve OCR accuracy**.

الأمر هو أن مكتبة Aspose.OCR توفر لك API منظمة تتيح لك تجميع فلاتر ما قبل المعالجة بالضبط كما تحتاجها. بنهاية هذا الدليل ستحصل على تطبيق C# Console جاهز للتنفيذ يقرأ إيصالًا مائلًا، يصححه، يزيل الضوضاء من الخلفية، يعزز التباين، ويطبع النص المنقح على وحدة التحكم. لا غموض، فقط كود خطوة بخطوة يمكنك نسخه ولصقه.

## ما ستتعلمه

- كيفية **load image for OCR** باستخدام `ImageStream` من Aspose.
- ما هي فلاتر **preprocess image before OCR** الأكثر فعالية للإيصالات.
- تقنيات **improve OCR accuracy** دون شراء خدمات طرف ثالث مكلفة.
- الأوامر الدقيقة لـ **extract text from receipt** والتحقق من النتيجة.
- مثال كامل قابل للتنفيذ يمكنك إدراجه في Visual Studio الآن.

### المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا مع .NET Core).
- حزمة NuGet صالحة لـ Aspose.OCR (`Aspose.OCR` 23.9 أو أحدث).
- صورة إيصال نموذجية (مثال: `skewed_receipt.jpg`) موجودة في مجلد يمكنك الإشارة إليه.
- إلمام أساسي بتطبيقات C# Console.

إذا كان لديك هذه المتطلبات، فلنبدأ—بدون إطالة، فقط الجوهر.

---

## تنفيذ OCR على الصورة – نظرة عامة خطوة بخطوة

قبل أن نبدأ بكتابة الكود، تخيل خط الأنابيب:

1. **Load** ملف الصورة إلى الذاكرة.  
2. **Preprocess** الصورة: تصحيح الميل، إزالة الضوضاء، وتعزيز التباين.  
3. **Run** محرك OCR.  
4. **Read** النص الناتج.

كل من هذه المراحل هي قطعة صغيرة من اللغز، ومعًا هم **perform OCR on image** للملفات التي ستكون غير قابلة للقراءة بخلاف ذلك. الأقسام التالية تفصل كل قطعة.

---

## تحميل الصورة لـ OCR

أول شيء يحتاجه أي سير عمل OCR هو صورة bitmap للعمل عليها. Aspose تُجرد التعامل مع الملفات خلف `ImageStream`، مما يعني أنك لست مضطرًا للتعامل مع `System.Drawing` إلا إذا أردت.

```csharp
using Aspose.OCR;
using System;

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Load the image you want to recognize
// Replace the path with the actual location of your receipt image
ocrEngine.Image = ImageStream.FromFile(@"C:\OCRDemo\skewed_receipt.jpg");

// Quick sanity check – make sure the image was loaded
if (ocrEngine.Image == null)
{
    Console.WriteLine("Failed to load image. Verify the file path.");
    return;
}
```

> **لماذا هذا مهم:** تحميل الصورة بشكل صحيح هو الأساس. إذا كان المسار خاطئًا، كل فلتر لاحق سيعمل بصمت على مرجع فارغ، وستحصل على نتيجة فارغة. الفحص أعلاه يحفظك من هذه المشكلة.

---

## ما قبل معالجة الصورة قبل OCR

صور الإيصالات معروفة بثلاث مشاكل: الدوران، البقع العشوائية، وانخفاض التباين. Aspose يأتي بثلاث فلاتر مدمجة تعالج هذه المشكلات مباشرة. الترتيب مهم—أولًا تصحيح الميل، ثم إزالة الضوضاء، وأخيرًا تعزيز التباين.

```csharp
// Step 3: Add preprocessing filters in the desired order
ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Deskew);          // Corrects image rotation
ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Denoise);        // Reduces noise
ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.ContrastBoost); // Enhances contrast
```

> **نصيحة احترافية:** إذا كنت تعالج دفعة من الإيصالات التي تم مسحها جميعًا بدقة 300 dpi، يمكنك تخطي `ContrastBoost` لأن الماسح يوفر بالفعل تباينًا كافيًا. التجربة هي المفتاح لـ **improve OCR accuracy** لمجموعة البيانات الخاصة بك.

---

## تحسين دقة OCR باستخدام الفلاتر

الآن بعد أن تم معالجة الصورة مسبقًا، يمكن لمحرك OCR أن يقوم بسحره. استدعاء `Recognize()` يشغل أداة التعرف القائمة على الشبكة العصبية على الـ bitmap المنقح.

```csharp
// Step 4: Perform OCR recognition
ocrEngine.Recognize();
```

خلف الكواليس، Aspose يطبق نماذج مخصصة للغة، تقسيم الأحرف، وخوارزميات ما بعد المعالجة. من خلال تزويده بصورة مصححة الميل، منقاة، وعالية التباين، فأنت في الواقع تقدم له صفحة بجودة كتاب دراسي—وهذا يفسر **improve OCR accuracy** التي تسعى إليها.

---

## استخراج النص من الإيصال

أخيرًا، استخرج السلسلة التي تم التعرف عليها من المحرك. خاصية `Text` تحتوي على النتيجة الخام بصيغة Unicode، والتي يمكنك كتابتها إلى وحدة التحكم، ملف، أو قاعدة بيانات.

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Receipt Text ===");
Console.WriteLine(ocrEngine.Text);
```

مخرجات الإيصال النموذجية تبدو هكذا:

```
=== Recognized Receipt Text ===
Store: QuickMart
Date: 2024-06-15
Item 1  $2.99
Item 2  $5.49
Total   $8.48
Thank you!
```

إذا لاحظت أرقامًا مفقودة أو أحرفًا مشوهة، عد إلى خطوة ما قبل المعالجة—ربما تحتاج الصورة إلى مستوى `Denoise` أقوى أو فلتر مخصص. الخبر السار هو أنه يمكنك تجميع عدة نسخ من نفس الفلتر إذا لزم الأمر.

---

## مثال كامل يعمل

فيما يلي البرنامج كاملًا جاهزًا للنسخ واللصق. احفظه باسم `Program.cs`، استعد حزمة NuGet، وشغّله. ستعرض وحدة التحكم النص المستخرج من الإيصال.

```csharp
using Aspose.OCR;
using System;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create the OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣  Load the image you want to process
            // -------------------------------------------------
            // Change the path to point at your own receipt file
            string imagePath = @"C:\OCRDemo\skewed_receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image from '{imagePath}'. Check the path and try again.");
                return;
            }

            // -------------------------------------------------
            // 3️⃣  Preprocess the image – this is where we
            //     actually **improve OCR accuracy**
            // -------------------------------------------------
            ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Deskew);
            ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Denoise);
            ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.ContrastBoost);

            // -------------------------------------------------
            // 4️⃣  Run the OCR engine – **perform OCR on image**
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // 5️⃣  Extract and display the text – **extract text from receipt**
            // -------------------------------------------------
            Console.WriteLine("\n=== Recognized Receipt Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### النتيجة المتوقعة

تشغيل البرنامج على إيصال واضح ومصحح الميل يجب أن يطبع شيئًا مشابهًا للمقتطف المعروض سابقًا. إذا حصلت على سلسلة فارغة، تحقق مرة أخرى من ترتيب ما قبل المعالجة أو حاول زيادة DPI لصورة المصدر.

---

## أسئلة شائعة ومشكلات محتملة

- **ماذا لو كان الإيصال مكتوبًا بخط اليد؟**  
  Aspose.OCR يعمل بشكل أفضل مع النص المطبوع. للخطوط المتصلة أو المختلطة قد تحتاج إلى نموذج كتابة يد متخصص أو مكتبة مختلفة.

- **هل يمكنني معالجة ملفات PDF مباشرةً؟**  
  نعم—حوّل كل صفحة PDF إلى صورة (`Aspose.PDF` يمكن أن يساعد) ومرّر تلك الصور إلى نفس خط الأنابيب.

- **هل هناك طريقة لمعالجة دفعات متعددة من الإيصالات؟**  
  ضع المنطق الأساسي داخل حلقة `foreach` التي تت iterates over مجلد من الصور. تذكر تحرير `OcrEngine` بعد كل ملف لتحرير الذاكرة.

- **هل أحتاج إلى ترخيص؟**  
  Aspose يقدم تقييمًا مجانيًا مع علامة مائية. للاستخدام الإنتاجي، اشترِ ترخيصًا لإزالة العلامة المائية وإطلاق الأداء الكامل.

---

## الخاتمة

لقد استعرضنا للتو كيفية **perform OCR on image** للملفات باستخدام Aspose.OCR، من **load image for OCR** إلى **preprocess image before OCR**، وأخيرًا **extract text from receipt**. من خلال ترتيب فلاتر تصحيح الميل، إزالة الضوضاء، وتعزيز التباين، ستلاحظ عادةً **improve OCR accuracy** ملحوظة—خاصةً في مسح الإيصالات منخفض الجودة.

ما التالي؟ جرّب إضافة تلميح اللغة (`ocrEngine.Language = Language.English;`) أو جرب فلاتر مخصصة لعكس الألوان. يمكنك أيضًا تمرير النص المستخرج إلى محلل بسيط يستخرج بنود الفاتورة والإجماليات تلقائيًا.

إذا ساعدك هذا الدليل على تجاوز العقبات المعتادة في OCR، أعطه نجمة على GitHub أو اترك تعليقًا أدناه. برمجة سعيدة، ولتكن إيصالاتك دائمًا قابلة للقراءة!

![مخطط يوضح خط أنابيب ما قبل معالجة OCR الذي يساعدك على تنفيذ OCR على الصورة] 

---

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة قابلة للتنفيذ مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)
- [كيفية استخدام AspOCR: فلاتر ما قبل معالجة صورة OCR لـ .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}