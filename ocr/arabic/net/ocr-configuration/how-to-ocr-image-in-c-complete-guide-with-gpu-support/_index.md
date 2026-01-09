---
category: general
date: 2026-01-09
description: تعلم كيفية التعرف الضوئي على الأحرف (OCR) للصورة واستخراج النص من الصورة
  باستخدام Aspose.OCR. يتضمن خطوات تحويل المستند الممسوح ضوئياً، تمكين وحدة معالجة
  الرسومات، وقراءة الصورة باستخدام OCR.
draft: false
keywords:
- how to ocr image
- extract image text
- convert scanned document
- how to enable gpu
- read image with ocr
language: ar
og_description: كيفية التعرف الضوئي على الحروف (OCR) للصورة بسرعة باستخدام Aspose.OCR.
  اتبع هذا الدليل خطوة بخطوة لاستخراج نص الصورة، تحويل المستند الممسوح ضوئياً، وتمكين
  وحدة معالجة الرسومات (GPU).
og_title: كيفية التعرف الضوئي على الأحرف في الصورة باستخدام C# – دليل معزز بالـ GPU
tags:
- OCR
- C#
- Aspose
- Image Processing
title: كيفية إجراء OCR على صورة في C# – دليل شامل مع دعم GPU
url: /ar/net/ocr-configuration/how-to-ocr-image-in-c-complete-guide-with-gpu-support/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على الأحرف (OCR) للصور في C# – دليل كامل مع دعم GPU

هل تساءلت يومًا **how to OCR image** مباشرةً من تطبيق .NET الخاص بك؟ لست وحدك—المطورون يحتاجون باستمرار إلى استخراج النص من ملفات PDF وTIFF والصور، خاصةً عند التعامل مع مستندات ممسوحة ضوئيًا كبيرة. الخبر السار؟ باستخدام Aspose.OCR يمكنك **extract image text** ببضع أسطر فقط، ويمكنك أيضًا **enable GPU** لتسريع المعالجة.

في هذا البرنامج التعليمي سنستعرض كل ما تحتاج معرفته: من تثبيت المكتبة، إلى تهيئة محرك OCR مع دعم fallback للـ GPU، ثم **reading image with OCR** وعرض النتيجة. في النهاية ستكون قادرًا على **convert scanned document** إلى سلاسل قابلة للتحرير—بدون الحاجة إلى خدمات خارجية.

---

## ما ستحتاجه

قبل أن نبدأ، تأكد من توفر ما يلي:

- **.NET 6.0** أو أحدث (الكود يعمل على .NET Core و .NET Framework أيضًا).
- **رخصة** لـ Aspose.OCR أو مفتاح تقييم مؤقت (الإصدار التجريبي المجاني يكفي للاختبار).
- ملف صورة تريد معالجته—يفضل أن يكون TIFF أو PNG عالي الدقة.
- (اختياري) جهاز يدعم GPU إذا أردت رؤية تحسين السرعة؛ وإلا سيتراجع المحرك تلقائيًا إلى CPU.

تغطية هذه المتطلبات يعني أنك ستتمكن من التركيز على سير عمل OCR الفعلي دون مواجهة عوائق لاحقًا.

---

## الخطوة 1: تثبيت حزمة NuGet الخاصة بـ Aspose.OCR

أولًا، أضف مكتبة Aspose.OCR إلى مشروعك. افتح الطرفية في مجلد الحل وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

أو، إذا كنت تستخدم واجهة NuGet في Visual Studio، ابحث عن **Aspose.OCR** واضغط تثبيت. هذا الأمر الواحد يجلب جميع ملفات DLL الضرورية، بما في ذلك الثنائيات الأصلية للـ GPU عندما تكون متوفرة.

> **نصيحة احترافية:** حافظ على تحديث الحزمة. الإصدارات الجديدة غالبًا ما تتضمن تحسينات في نماذج اللغة ودعم GPU أفضل.

---

## الخطوة 2: استيراد المساحات الاسمية المطلوبة  

بعد تثبيت الحزمة، استدعِ المساحات الاسمية ذات الصلة. هذه الخطوة هي حيث نبدأ **how to OCR image** في الكود.

```csharp
// Step 2: Import required namespaces
using Aspose.OCR;
using Aspose.OCR.Settings;
```

هاتان السطران يمنحانك الوصول إلى الفئة `OcrEngine` وكائن الإعدادات الذي يتيح لك تفعيل استخدام GPU. بدونهما، لن يعرف المترجم ما معنى `OcrEngine`.

---

## الخطوة 3: تهيئة محرك OCR وتفعيل GPU  

إذا تساءلت يومًا **how to enable GPU** لـ OCR، فهذه هي الإجابة. ننشئ كائن `OcrEngineSettings`، نضبط علم `UseGpu`، ثم نمرره إلى مُنشئ المحرك. يكتشف المحرك تلقائيًا ما إذا كان هناك GPU متوافق؛ إذا لم يكن موجودًا، يتراجع إلى CPU—وبالتالي لا تحتاج إلى معالجة أخطاء إضافية.

```csharp
// Step 3: Initialize the OCR engine with GPU support (falls back to CPU if unavailable)
var ocrSettings = new OcrEngineSettings { UseGpu = true };
var ocrEngine   = new OcrEngine(ocrSettings);
```

لماذا نفعّل GPU أصلاً؟ بالنسبة للصور الكبيرة—مثل ملفات TIFF متعددة الصفحات أو المسحات عالية الدقة—يمكن أن ينخفض وقت المعالجة من عدة ثوانٍ إلى جزء من الثانية. إذا كنت تبني خط أنابيب معالجة دفعات، فإن هذا التحسين يضيف قيمة كبيرة.

---

## الخطوة 4: تنفيذ OCR على الصورة المستهدفة  

هنا نصل إلى **read image with OCR** فعليًا. قدم مسار الملف إلى المحرك، وسيعيد النص المعترف به كسلسلة. يعمل هذا مع أي تنسيق نقطي يدعمه Aspose (PNG، JPEG، TIFF، BMP، إلخ).

```csharp
// Step 4: Perform OCR on the target image file
string imagePath = @"C:\Images\large-document.tif";
string recognizedText = ocrEngine.RecognizeImage(imagePath);
```

إذا كنت تحتاج إلى **convert scanned document** صفحةً بصفحة، ما عليك سوى التكرار على أسماء الملفات واستدعاء `RecognizeImage` لكل منها. الطريقة آمنة للاستخدام عبر الخيوط، لذا يمكنك حتى موازنة الحمل على معالج متعدد الأنوية.

---

## الخطوة 5: عرض النص المستخرج أو حفظه  

أخيرًا، نطبع النتيجة. في تطبيق Console، يكفي `Console.WriteLine`. في سيناريو واقعي قد تكتب النص إلى قاعدة بيانات، ملف JSON، أو تدخله في فهرس بحث.

```csharp
// Step 5: Display the extracted text
Console.WriteLine(recognizedText);
```

السطر أعلاه يطبع ناتج OCR الخام. ستلاحظ فواصل أسطر، وبعض الأخطاء البسيطة، وربما بعض الأحرف العشوائية—هذا طبيعي في OCR. يمكن للمعالجة اللاحقة (مثل تنظيف regex) تحسين النتيجة إذا لزم الأمر.

> **ملاحظة:** يدعم Aspose.OCR قواميس خاصة باللغات. إذا كنت تعالج نصوصًا غير إنجليزية، اضبط `ocrEngine.Settings.Language` وفقًا لذلك قبل استدعاء `RecognizeImage`.

---

## مثال كامل يعمل  

لنجمع كل ما سبق في برنامج مستقل يمكنك نسخه ولصقه في مشروع Console جديد:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // Initialize OCR engine with GPU support
        var ocrSettings = new OcrEngineSettings { UseGpu = true };
        var ocrEngine   = new OcrEngine(ocrSettings);

        // Path to the image you want to process
        string imagePath = @"C:\Images\large-document.tif";

        // Perform OCR
        string recognizedText = ocrEngine.RecognizeImage(imagePath);

        // Output the result
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**الناتج المتوقع** (مقتطع لل brevity):

```
=== OCR Result ===
This is a sample scanned document.
It contains several lines of text that have been
converted from image to editable characters.
...
```

شغّل البرنامج، وسترى النص المستخرج يظهر في نافذة الـ Console. إذا كان الـ GPU متاحًا، سيكون وقت المعالجة أقصر بكثير مقارنةً بالأجهزة التي تعتمد على CPU فقط.

---

## المشكلات الشائعة وكيفية تجنّبها  

| المشكلة | السبب | الحل |
|-------|----------------|-----|
| **حروف غير مفهومة** | مصدر منخفض الدقة أو خلفية مشوشة. | عالج الصورة مسبقًا (زيادة DPI، تطبيق التث_binization) قبل OCR. |
| **GPU غير مستخدم** | لا يوجد برنامج تشغيل CUDA متوافق. | تحقق من نسخة البرنامج، أو اضبط `UseGpu = false` لإجبار الاستخدام على CPU. |
| **نفاد الذاكرة على TIFFs الكبيرة** | تحميل الملف بالكامل مرة واحدة. | استخدم `OcrEngineSettings.MaxMemoryUsage` لتقليل الاستهلاك، أو عالج الصفحات بشكل فردي. |
| **كشف لغة غير صحيح** | اللغة الافتراضية هي الإنجليزية. | اضبط `ocrEngine.Settings.Language = Language.YourLanguage;` قبل استدعاء `RecognizeImage`. |

معالجة هذه الحالات تضمن بقاء تنفيذ **how to OCR image** قويًا عبر بيئات مختلفة.

---

## توسيع الحل  

الآن بعد أن أصبحت قادرًا على **extract image text**، قد ترغب في:

- **convert scanned document** إلى ملفات PDF قابلة للبحث عبر دمج طبقة OCR.
- تخزين النتائج في فهرس **Azure Cognitive Search** لاسترجاع سريع.
- ربط ناتج OCR بواجهة **translation API** إذا احتجت دعمًا متعدد اللغات.
- استخدام طريقة **GetBoundingBoxes** في Aspose.OCR لتحديد موقع كل كلمة على الصورة—مفيد لأدوات التمويه.

جميع هذه الامتدادات تبنى على المبدأ الأساسي الذي غطيناه: تهيئة المحرك، إمداده بصورة، وقراءة النص.

---

## الخلاصة  

استعرضنا مثالًا كاملاً من البداية إلى النهاية حول **how to OCR image** باستخدام Aspose.OCR في C#. من خلال تثبيت حزمة NuGet، استيراد المساحات الاسمية المناسبة، تفعيل GPU (أو الاعتماد على CPU)، واستدعاء `RecognizeImage`، يمكنك استخراج نص الصور بثقة، **convert scanned document**، و**read image with OCR** في أي تطبيق .NET.

جرّبه على مجموعة من مسحاتك—جرب صيغ صور مختلفة، غيّر علم الـ GPU، ولاحظ الفرق في الأداء. عندما تكون جاهزًا، استكشف الميزات المتقدمة مثل قواميس اللغة أو استخراج إطارات الكلمات لجعل حلك أكثر ذكاءً.

برمجة سعيدة، ولتكن خطوط OCR الخاصة بك سريعة، دقيقة، وخالية من المتاعب!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}