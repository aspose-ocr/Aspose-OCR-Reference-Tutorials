---
category: general
date: 2026-10-05
description: يظهر دليل تحويل الصورة إلى PDF باستخدام OCR كيفية تحميل الصورة للـ OCR،
  وتطبيق خطوات ما قبل المعالجة، واستخراج النص السيريلي من الصورة باستخدام مثال Aspose
  OCR بلغة C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- image to pdf OCR
- load image for OCR
- ocr image preprocessing steps
- aspose OCR C# example
- extract Cyrillic text image
language: ar
lastmod: 2026-10-05
og_description: دليل تحويل الصورة إلى PDF باستخدام OCR يشرح لك كيفية تحميل صورة للـ
  OCR، وتطبيق خطوات ما قبل المعالجة، واستخراج نص سيريلي من الصورة باستخدام مثال Aspose
  OCR بلغة C#.
og_image_alt: Developer view of OCR converting an image to PDF with Aspose OCR in
  C#
og_title: تحويل الصورة إلى PDF باستخدام OCR من Aspose في C# – مثال كامل
schemas:
- author: Aspose
  dateModified: '2026-10-05'
  description: Image to PDF OCR tutorial shows how to load image for OCR, apply preprocessing
    steps, and extract Cyrillic text image using an Aspose OCR C# example.
  headline: 'Image to PDF OCR with Aspose OCR in C#: step‑by‑step guide'
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- PDF
- Image processing
title: 'تحويل الصورة إلى PDF باستخدام OCR من Aspose في C#: دليل خطوة بخطوة'
url: /ar/net/ocr-optimization/image-to-pdf-ocr-with-aspose-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى PDF باستخدام OCR من Aspose OCR في C#: دليل خطوة بخطوة

إذا كنت بحاجة إلى **تحويل الصورة إلى PDF باستخدام OCR** في تطبيق .NET، يوضح لك هذا الدليل بالضبط كيفية تحميل صورة للـ OCR، ومعالجتها مسبقًا، وتصدير النص المُعترف به كملف PDF قابل للبحث. سترى مثالًا كاملًا *Aspose OCR C#* يستخراج النص السيريلي من صورة ويحفظ النتيجة كملف PDF.

تحويل المستندات الممسوحة ضوئيًا إلى ملفات PDF قابلة للبحث هو طلب شائع لأغراض الأرشفة، والامتثال، أو خطوط استخراج البيانات. بنهاية هذا الشرح ستحصل على مشروع جاهز للتنفيذ يقوم بتنفيذ سير عمل OCR كامل، من تحميل الصورة إلى إنشاء PDF، مع معالجة الأحرف السيريليّة بشكل صحيح.

## ما ستتعلمه

- كيفية تثبيت وإضافة مرجع مكتبة **Aspose.OCR** في مشروع C#.  
- الطريقة الصحيحة **لتحميل صورة للـ OCR** باستخدام طريقة `Image.Load` الخاصة بـ Aspose.  
- خطوات **معالجة الصورة قبل OCR** الأساسية (الدوران وتصحيح الميل) التي تحسن دقة التعرف.  
- كيفية تكوين المحرك **لاستخراج النص السيريلي من الصورة** وإنتاج PDF قابل للبحث.  
- نصائح لتجاوز المشكلات الشائعة مثل نقص وحدات اللغة.

### المتطلبات المسبقة

| المتطلب | السبب |
|-------------|--------|
| .NET 6.0 SDK أو أحدث | يوفر بيئة التشغيل لميزات C# 10 المستخدمة في المثال. |
| Visual Studio 2022 (أو أي بيئة تطوير تدعم .NET) | يجعل إنشاء المشروع وتصحيح الأخطاء أسهل. |
| اتصال بالإنترنت (للتشغيل الأول) | يسمح لمحرك OCR بتحميل وحدة اللغة السيريليّة تلقائيًا. |
| صورة عينة تحتوي على نص سيريلي (مثل `sample_cyrillic.jpg`) | توضح سيناريو *استخراج النص السيريلي من الصورة*. |

> **نصيحة احترافية:** إذا كنت تعمل خلف بروكسي مؤسسي، قم بتكوين الخاصية `Resources.AutoDownload` لاستخدام إعدادات البروكسي قبل التشغيل الأول.

## الخطوة 1: تثبيت حزمة Aspose.OCR من NuGet

افتح الطرفية في مجلد الحل الخاص بك وشغّل:

```bash
dotnet add package Aspose.OCR
```

تحتوي الحزمة على مساحة الاسم `Aspose.Ocr`، محرك OCR، وموارد اللغة اللازمة للتعرف متعدد اللغات.

## الخطوة 2: تحميل صورة للـ OCR

الخطوة الوظيفية الأولى هي قراءة الملف المصدر إلى كائن `Aspose.Ocr.Image`. استخدام المسار الكامل يضمن أن المحرك يستطيع العثور على الملف بغض النظر عن دليل العمل الحالي.

```csharp
// Load the source image that contains Cyrillic text
var inputImage = Aspose.Ocr.Image.Load(@"C:\OCR\sample_cyrillic.jpg");
```

> **لماذا هذا مهم:** تحميل الصورة مبكرًا يمنحك إمكانية الوصول إلى بيانات البكسل الخاصة بها، وهو ما يلزم لمرحلة المعالجة المسبقة. طريقة `Image.Load` تتحقق أيضًا من تنسيق الملف، وتطرح استثناء واضح إذا كانت الصورة غير مدعومة.

## الخطوة 3: تكوين محرك OCR لاستخراج السيريليّة

يدعم Aspose OCR العديد من اللغات، لكن عليك تحديد اللغة المتوقعة صراحة. للنص السيريلي، استخدم قيمة التعداد `Language.Cyrillic`. تمكين `Resources.AutoDownload` يضمن جلب وحدة اللغة المطلوبة تلقائيًا في أول تشغيل للكود.

```csharp
using (var ocrEngine = new Aspose.Ocr.OcrEngine())
{
    // Select Cyrillic language to correctly recognize Russian, Ukrainian, etc.
    ocrEngine.Language = Aspose.Ocr.Language.Cyrillic;

    // Automatically download missing language modules (required on first run)
    ocrEngine.Resources.AutoDownload = true;
```

> **لماذا هذا مهم:** بدون تحديد اللغة، ي默认 المحرك اللغة الإنجليزية، مما يقلل الدقة بشكل كبير بالنسبة للأحرف السيريليّة.

## الخطوة 4: تطبيق خطوات معالجة الصورة قبل OCR

تحسين جودة OCR يتم عبر تصحيح المشكلات الشائعة في الصورة. يستخدم المثال خيارين من أكثر الخيارات فعالية:

- **Rotate** – يضبط الصفحة إذا تم مسحها بزاوية.  
- **Deskew** – يزيل الميل الطفيف الذي قد يربك تجزئة الأحرف.

```csharp
    // Preprocess the image: rotate to correct orientation and deskew to flatten text lines
    ocrEngine.PreprocessImage(
        inputImage,
        Aspose.Ocr.PreprocessOptions.Rotate |
        Aspose.Ocr.PreprocessOptions.Deskew);
```

> **كيف يعمل:** `PreprocessImage` ينشئ صورة bitmap داخلية يستهلكها محرك OCR. عملية الـ OR الثنائية تجمع عدة خيارات، مما يسمح بربط الخطوات دون كتابة كود إضافي.

## الخطوة 5: التعرف على النص وتحويله إلى PDF (تحويل الصورة إلى PDF باستخدام OCR)

الآن بعد معالجة الصورة وتحديد اللغة، استدعِ `Recognize`. تُعيد الطريقة كائن `OcrResult` يمكن حفظه مباشرة كملف PDF. يحتوي PDF الناتج على طبقة نص مخفية، مما يجعله قابلًا للبحث.

```csharp
    // Perform OCR and ask for PDF output format
    var ocrResult = ocrEngine.Recognize(inputImage, Aspose.Ocr.OutputFormat.Pdf);
```

> **النتيجة:** يتضمن PDF الصورة النقطية الأصلية بالإضافة إلى طبقة نصية تتطابق مع الأحرف السيريليّة التي تم التعرف عليها. يمكن لمحركات البحث فهرسة هذا النص، ويمكن للمستخدمين نسخه ولصقه.

## الخطوة 6: حفظ PDF القابل للبحث

أخيرًا، اكتب ملف PDF إلى القرص. اختر مسارًا يملك التطبيق صلاحية الكتابة فيه.

```csharp
    // Save the searchable PDF to the desired location
    ocrResult.Save(@"C:\OCR\result.pdf");
}
```

### النتيجة المتوقعة

عند فتح `result.pdf` في أي عارض PDF، ستظهر الصورة الأصلية وستتمكن من تحديد النص السيريلي المُعترف به. بحث سريع عن كلمة موجودة في الصورة المصدر يجب أن يبرز الموقع المقابل في PDF.

![OCR conversion result](/images/ocr-conversion.png){alt="لقطة شاشة تُظهر تحويل OCR من صورة إلى PDF باستخدام Aspose OCR في C#"}

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه إلى تطبيق Console. يتضمن جميع توجيهات `using` الضرورية ومعالجة الأخطاء لتطبيق جاهز للإنتاج.

```csharp
// ------------------------------------------------------------
// Image to PDF OCR – Aspose OCR C# example
// ------------------------------------------------------------
using System;
using Aspose.Ocr;

namespace ImageToPdfOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the image that contains Cyrillic text
            const string inputPath = @"C:\OCR\sample_cyrillic.jpg";
            // Destination PDF file
            const string outputPath = @"C:\OCR\result.pdf";

            try
            {
                // Step 1: Load the image for OCR
                var inputImage = Image.Load(inputPath);

                // Step 2: Create and configure the OCR engine
                using (var ocrEngine = new OcrEngine())
                {
                    // Choose Cyrillic language
                    ocrEngine.Language = Language.Cyrillic;
                    // Enable automatic download of language resources
                    ocrEngine.Resources.AutoDownload = true;

                    // Step 3: Apply preprocessing (rotate + deskew)
                    ocrEngine.PreprocessImage(
                        inputImage,
                        PreprocessOptions.Rotate |
                        PreprocessOptions.Deskew);

                    // Step 4: Recognize and export as PDF (image to PDF OCR)
                    var ocrResult = ocrEngine.Recognize(
                        inputImage,
                        OutputFormat.Pdf);

                    // Step 5: Save the searchable PDF
                    ocrResult.Save(outputPath);
                }

                Console.WriteLine($"✅ OCR completed. PDF saved to: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ An error occurred: {ex.Message}");
                // In a real application, consider logging the stack trace.
            }
        }
    }
}
```

شغّل البرنامج (`dotnet run`) وتأكد من ظهور `result.pdf` في `C:\OCR`. سيؤكد الطرفية إكمال العملية بنجاح.

## المشكلات الشائعة وكيفية تجنّبها

| العَرَض | السبب | الحل |
|---------|-------|-----|
| **عدم ظهور أحرف سيريليّة في PDF** | لم يتم ضبط اللغة إلى السيريليّة. | تأكد من `ocrEngine.Language = Language.Cyrillic;`. |
| **ملف PDF فارغ** | تم تعطيل `Resources.AutoDownload` ووحدة اللغة مفقودة. | أبقِ `ocrEngine.Resources.AutoDownload = true;` أو نزّل وحدة السيريليّة يدويًا من موقع Aspose. |
| **ضعف التعرف على مسحات مائلة** | تم إغفال خطوة المعالجة المسبقة. | أضف `PreprocessOptions.Rotate` (و`Deskew` عند الحاجة). |
| **استثناء `FileNotFoundException` عند تحميل الصورة** | مسار الصورة غير صحيح أو الملف مفقود. | استخدم مسارًا مطلقًا أو تحقق من وجود الملف قبل التحميل. |
| **نفاد الذاكرة على صور كبيرة** | تحميل صورة عالية الدقة دون تصغير. | قلّص حجم الصورة قبل OCR (`Image.Resize`)، أو زد حد الذاكرة للعملية. |

## توسيع المثال

- **عدة لغات:** اضبط `ocrEngine.Language = Language.Cyrillic | Language.English;` للتعرف على نصوص مختلطة.  
- **صيغ إخراج مختلفة:** استبدل `OutputFormat.Pdf` بـ `OutputFormat.Txt` أو `OutputFormat.Docx` للحصول على نص عادي أو مستند Word.  
- **معالجة دفعات:** غلف منطق OCR داخل حلقة `foreach` التي  

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [كيفية تنفيذ OCR في C# – استخراج النص من الصورة باستخدام Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/)
- [كيفية استخراج النص من الصورة باستخدام Aspose.OCR لـ .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}