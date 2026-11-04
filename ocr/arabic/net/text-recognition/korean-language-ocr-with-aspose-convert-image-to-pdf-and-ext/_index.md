---
category: general
date: 2026-05-28
description: دروس التعرف الضوئي على الحروف للغة الكورية باستخدام Aspose في C#. تعلم
  كيفية تحميل الصورة من تدفق، استخراج النص العادي، تحويل الصورة إلى PDF وتصدير PDF
  قابل للبحث.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: ar
og_description: التعرف الضوئي على الأحرف للغة الكورية في C# باستخدام Aspose. دليل
  خطوة بخطوة لتحميل الصورة من التدفق، استخراج النص العادي، تحويل الصورة إلى PDF وتصدير
  PDF قابل للبحث.
og_title: التعرف الضوئي على الأحرف للغة الكورية – تحويل الصورة إلى PDF واستخراج النص
  (دليل C#)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'التعرف الضوئي على الأحرف للغة الكورية باستخدام Aspose: تحويل الصورة إلى PDF
  واستخراج النص في C#'
url: /ar/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف الضوئي على الأحرف (OCR) للغة الكورية باستخدام Aspose: تحويل الصورة إلى PDF واستخراج النص في C#

هل تساءلت يومًا كيف تشغّل **Korean Language OCR** على صورة دون إرسال أي شيء إلى السحابة؟ لست وحدك. سواءً كنت تقوم برقمنة لافتات الشوارع، أو معالجة الإيصالات، أو بناء فهرس بحث متعدد اللغات، فإن القدرة على التعرف على الأحرف الكورية محليًا يمكن أن توفر لك الوقت والمال وتجنب مشاكل الخصوصية.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح لك كيفية **load image from stream**، **extract plain text**، **convert image to PDF**، وأخيرًا **export searchable PDF**—كل ذلك باستخدام Aspose.OCR وبضع أسطر من C#. لا خدمات خارجية، لا سحر مخفي—فقط شفرة .NET صافية يمكنك وضعها في أي تطبيق كونسول.

## ما ستحصل عليه بعد الانتهاء

- برنامج كونسول يعمل يقرأ ملف JPEG عبر تدفق ملف.  
- نص كوري مستخرج كسلاسل Unicode عادية.  
- تقرير JSON مفصل عن عملية OCR للتصحيح أو التحليل.  
- ملف PDF قابل للبحث يمكنك فتحه في أي قارئ PDF وتحديد الكلمات الكورية فيه.  

**المتطلبات المسبقة**  
- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).  
- حزمة Aspose.OCR for .NET عبر NuGet مثبتة (`Install-Package Aspose.OCR`).  
- مجلد يحتوي على `korean_sign.jpg` وموقع قابل للكتابة لحفظ ملفات الإخراج.  

إذا كان لديك كل هذه العناصر جاهزة، رائع—لنبدأ بالعمل.

## الخطوة 1: تهيئة محرك OCR للغة الكورية

الأول الذي تحتاجه هو كائن `OcrEngine`. تمكين الـ GPU (إذا كان متوفرًا) يسرّع التعرف بشكل كبير، وتعطيل تحميل الموارد تلقائيًا يجبر المكتبة على استخدام حزم اللغة غير المتصلة التي تزودها.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **لماذا هذا مهم:**  
> *GPU acceleration* يمكنه تقليل زمن المعالجة من ثوانٍ إلى مللي ثانية للدفعات الكبيرة. ضبط `AutomaticResourceDownload` إلى `false` يضمن أن العرض التجريبي يعمل دون اتصال—وهو مطلب حاسم للعديد من بيئات المؤسسات.

## الخطوة 2: تحميل الصورة عبر تدفق (Stream)

قراءة الصورة عبر تدفق يمنحك مرونة: يمكنك سحب الملفات من القرص، أو مشاركات الشبكة، أو حتى كتل الذاكرة المؤقتة. هنا نفتح ملف JPEG محلي، لكن النمط نفسه يعمل مع أي `Stream`.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **نصيحة احترافية:** إذا احتجت يومًا لمعالجة صور تُرفع عبر واجهة ويب API، استبدل `File.OpenRead` بـ `IFormFile.OpenReadStream()` الوارد—وبقية الشيفرة تبقى كما هي.

## الخطوة 3: اختيار اللغة الكورية وتطبيق مرشحات ما قبل المعالجة

Aspose.OCR يدعم عددًا قليلًا من خطوات ما قبل المعالجة التي تنظف الصورة قبل التعرف. بالنسبة لللافتات الكورية، عادةً ما تكون عملية تصحيح الميل (deskew) وإزالة الضوضاء (denoise) كافية.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **ما الذي يحدث في الخلفية؟**  
> مرشح `Deskew` يُعيد النص المائل إلى وضعه الصحيح، بينما `Denoise` يزيل الحبيبات التي قد تُربك المصنف. تخطي هذه الخطوات غالبًا ما يؤدي إلى مخرجات مشوشة، خاصةً في الصور منخفضة الدقة.

## الخطوة 4: استخراج النص العادي بشكل غير متزامن (Asynchronously)

الآن يأتي لحظة الحقيقة—طلب المحرك التعرف على الأحرف وإعطائنا سلسلة نظيفة. استخدام `RecognizeAsync` يحافظ على استجابة الواجهة إذا دمجتها في تطبيق سطح مكتب أو ويب.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
OCR complete. Extracted text:
서울시청
```

> **لماذا غير متزامن؟**  
> OCR يمكن أن يكون مكثفًا على وحدة المعالجة. التنفيذ غير المتزامن يمنع حظر الخيط الخاص بك، وهو مفيد بشكل خاص في ASP.NET Core حيث نقص الخيوط مشكلة حقيقية.

## الخطوة 5: الحصول على نتيجة تفصيلية وحفظها كملف JSON

أحيانًا تحتاج إلى أكثر من السلسلة الخام—ربما تريد درجات الثقة، أو الصناديق المحيطة، أو بيانات الصورة الأصلية. طريقة `RecognizeDetailed` تُعيد كائن `RecognitionResult` يمكن تسلسله إلى JSON للتحليل لاحقًا.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

فتح `korean_ocr.json` سيظهر بنية مشابهة لـ:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **متى تستخدم هذا؟**  
> إذا كنت تبني فهرس بحث، قيم الثقة تسمح لك بتصفية النتائج ذات الجودة المنخفضة. إذا كنت تحتاج لتسليط الضوء على النص في واجهة المستخدم، فإن الصناديق المحيطة هي خريطتك.

## الخطوة 6: تحويل الصورة إلى PDF وتصدير PDF قابل للبحث

Aspose يجعل الانتقال من الرستر إلى الفكتور سهلًا. بتعيين `OutputFormat` إلى `SearchablePdf`، تُدمج المكتبة الصورة الأصلية وتضيف طبقة نص غير مرئية تحتوي على ناتج OCR. يمكن البحث في ملف PDF الناتج، نسخه، وفهرسته كما أي PDF أصلي.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

افتح `korean_searchable.pdf` في Adobe Reader أو أي عارض PDF، اضغط **Ctrl+F**، اكتب كلمة كورية، وستنتقل مباشرة إلى الموضع الصحيح في الصفحة. هذه هي قوة PDF القابل للبحث.

> **نصيحة إضافية:** إذا كنت تحتاج فقط إلى PDF بصري دون طبقة النص المخفي، غيّر `OutputFormat` إلى `Pdf` بدلاً من ذلك.

## مثال كامل يعمل

فيما يلي البرنامج الكامل—انسخه، الصقه، استبدل `YOUR_DIRECTORY` بمسار فعلي، ثم اضغط **F5**.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### ناتج الكونسول المتوقع

```
OCR complete. Extracted text:
서울시청
```

وستجد ثلاثة ملفات جديدة بجوار صورة المصدر:

- `korean_ocr.json` – بيانات التعرف الكاملة.  
- `korean_searchable.pdf` – PDF يمكنك **البحث** فيه.  
- (اختياري) أي سجلات وسيطة تختار إضافتها.

## أسئلة شائعة وحالات خاصة

**ماذا لو لم يكن لدي GPU؟**  
اضبط `EnableGpu = false`؛ fallback إلى CPU يكفي تمامًا للدفعات الصغيرة.

**هل يمكنني معالجة عدة صور في تشغيل واحد؟**  
بالطبع. غلف المنطق الأساسي داخل حلقة `foreach (var file in Directory.GetFiles(...))` وأعد تعيين `ocrEngine.Image` في كل تكرار.

**كيف أتعامل مع لغات أخرى إلى جانب الكورية؟**  
Aspose.OCR يسمح لك بتعيين `Language = Language.AutoDetect` أو دمج اللغات باستخدام عامل OR الثنائي (مثال: `Language.Korean | Language.English`).

**ماذا لو كانت ثقة OCR منخفضة؟**  
افحص `detailedResult.Pages[0].Words` وصّفّ entries التي قيمتها `Confidence < 0.7`. يمكنك أيضًا تعديل مرشحات ما قبل المعالجة—جرّب إضافة `PreprocessFilter.ContrastEnhancement`.

## الخلاصة

لقد رأيت الآن كيف تُجري **Korean Language OCR** من البداية إلى النهاية، بدءًا من **loading image from stream** إلى **extract plain text**، ثم **convert image to PDF** وأخيرًا **export searchable PDF**. النهج معيّن، لذا يمكنك استبدال مصدر الصورة، تغيير صيغة الإخراج، أو توصيل JSON بأي خط أنابيب لاحق.

ما التالي

## دروس ذات صلة

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}