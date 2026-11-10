---
category: general
date: 2026-05-28
description: تشغيل OCR على الصورة باستخدام C# لقراءة النص من الصورة واستخراج النص
  من الإيصال بسرعة. تعلم خيارات GPU وتقنيات التحميل.
draft: false
keywords:
- run ocr on image
- read text from image
- extract text from receipt
- load image for ocr
language: ar
og_description: تشغيل OCR على الصورة باستخدام C#. يوضح لك هذا الدليل كيفية قراءة النص
  من الصورة، استخراج النص من الفاتورة، وتحسين استخدام وحدة معالجة الرسومات.
og_title: تشغيل OCR على الصورة – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  headline: Run OCR on Image – Complete C# Guide
  type: TechArticle
- description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  name: Run OCR on Image – Complete C# Guide
  steps:
  - name: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
    text: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
  - name: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
    text: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
  - name: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
    text: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
  - name: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
    text: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Computer Vision
title: تشغيل OCR على الصورة – دليل C# الكامل
url: /ar/net/ocr-optimization/run-ocr-on-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على الصورة – دليل C# كامل

هل احتجت يوماً إلى **run OCR on image** للملفات لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك؛ العديد من المطورين يواجهون هذه المشكلة عندما يحاولون أول مرة قراءة النص من بيانات الصورة. الخبر السار هو أنه ببضع أسطر من C# يمكنك استخراج النص من مسح الفواتير، ملفات PDF، أو أي صورة تُلقِيها. في هذا الدليل سنستعرض مثالًا كاملاً جاهزًا للتنفيذ يوضح أيضًا كيفية **load image for OCR**، الاستفادة من تسريع GPU، وتحديد استخدام الذاكرة بأمان.

بحلول نهاية هذا الدرس ستتمكن من:

* تهيئة محرك OCR في C#
* **Load image for OCR** من القرص أو من تدفق
* **Read text from image** مع دعم GPU اختياري
* **Extract text from receipt** وإخراج النتيجة إلى وحدة التحكم

لا حاجة لخدمات خارجية — فقط مكتبة محلية وصورة عينة لفاتورة.

---

## ما ستحتاجه

| المتطلبات المسبقة | السبب |
|--------------|--------|
| .NET 6.0 SDK or later | بيئة تشغيل حديثة، تدعم أحدث ميزات اللغة |
| مكتبة OCR تُظهر فئة `OcrEngine` (مثل IronOCR، Tesseract .NET wrapper) | توفر طُرُق `Configuration` و `Recognize` المستخدمة أدناه |
| وحدة معالجة رسومية مدعومة بـ CUDA (اختياري) | تمكن علم `EnableGpu` لمعالجة أسرع |
| صورة عينة لفاتورة (`receipt.jpg`) | توضح خطوة **extract text from receipt** |
| أي بيئة تطوير C# (Visual Studio, Rider, VS Code) | للتجميع السريع وتصحيح الأخطاء |

إذا لم يكن لديك GPU، سيعود الكود ببساطة إلى وضع CPU — لا تقلق.

![مثال إخراج تشغيل OCR على الصورة](https://example.com/ocr-output.png "تشغيل OCR على الصورة – مثال إخراج وحدة التحكم")

*نص بديل: مثال إخراج تشغيل OCR على الصورة يُظهر النص المعترف به من الفاتورة.*

---

## الخطوة 1: تشغيل OCR على الصورة – إعداد المحرك

أولاً: أنشئ نسخة من محرك OCR. هذا الكائن هو قلب العملية؛ يحتفظ بجميع تفاصيل الإعداد ويقوم بالمعالجة الثقيلة.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

*لماذا هذا مهم:* فئة `OcrEngine` تغلف محرك OCR الأصلي (Tesseract، IronOCR، إلخ). إنشاء نسخة واحدة وإعادة استخدامها عبر صور متعددة يقلل من الحمل ويمنحك مكانًا واحدًا لضبط الإعدادات.

---

## الخطوة 2: تحميل الصورة لـ OCR

قبل أن يتمكن المحرك من القراءة، تحتاج إلى تزويده بصورة. خاصية `Image` في المكتبة تتوقع تدفقًا أو مسار ملف، حسب التنفيذ.

```csharp
// Step 2: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

*نصيحة:* إذا كنت تتعامل مع تحميلات المستخدمين، غلف ذلك بـ `try/catch` وتحقق من نوع الملف أولاً. الصيغ غير المدعومة ستطلق استثناء يمكن التعامل معه بسلاسة.

---

## الخطوة 3: تمكين تسريع GPU (اختياري)

إذا كان جهازك يحتوي على بيئة تشغيل CUDA أو OpenCL متوافقة، فإن تشغيل وضع GPU يمكن أن يوفر ثوانٍ في كل عملية التعرف.

```csharp
// Step 3: Enable GPU acceleration (requires CUDA/OpenCL runtime)
ocrEngine.Configuration.EnableGpu = true;
```

*نصيحة احترافية:* ليست كل بطاقات GPU متساوية. على البطاقات القديمة قد تلاحظ بطءً طفيفًا بسبب عبء التعريفات. اختبر كلا المسارين (`EnableGpu = true/false`) لتعرف ما هو الأنسب لمعداتك.

---

## الخطوة 4: تحديد استخدام ذاكرة GPU (اختياري)

أحيانًا لا تريد أن يستهلك عملية OCR كل ذاكرة GPU، خاصةً عندما تشارك الـ GPU مع أحمال عمل أخرى مثل استدلال التعلم العميق.

```csharp
// Step 4: (Optional) Limit the amount of GPU memory the engine can use (in MB)
ocrEngine.Configuration.GpuMemoryLimit = 1024; // 1 GB limit
```

*متى تستخدم:* إذا كنت تشغّل خدمة ويب تعالج العديد من الصور بشكل متزامن، فإن تحديد الذاكرة يمنع حدوث أعطال نفاد الذاكرة.

---

## الخطوة 5: التعرف على النص وقراءة النص من الصورة

الآن المحرك جاهز للقيام بمهمته. استدعاء `Recognize()` يشغل خط أنابيب OCR ويعيد السلسلة المستخرجة.

```csharp
// Step 5: Perform OCR and retrieve the recognized text
string recognizedText = ocrEngine.Recognize();
```

*لماذا هذا هو الجوهر:* هذا السطر الواحد يخفي سلسلة من عمليات ما قبل المعالجة (تث binarization، تصحيح الميل) والتصنيف الفعلي للأحرف. الـ `recognizedText` المُرجع هو نص Unicode عادي، جاهز للمعالجة الإضافية.

---

## الخطوة 6: استخراج النص من الفاتورة – الإخراج

أخيرًا، اكتب النتيجة إلى وحدة التحكم أو احفظها حيثما تحتاج. بالنسبة للفاتورة، قد تقوم لاحقًا بتحليل بنود السطر، الإجماليات، أو التواريخ.

```csharp
// Step 6: Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

**الإخراج المتوقع لوحدة التحكم (مقتطع للاختصار):**

```
=== OCR Result ===
Store Name
123 Main St.
Date: 04/27/2026
Item   Qty   Price
Apple   2    1.20
Bread   1    2.50
Total          3.70
Thank you!
```

إذا واجه OCR صعوبة مع تخطيط فاتورة معين، فكر في تعديل خيارات ما قبل المعالجة (مثال، `ocrEngine.Configuration.Deskew = true`) أو تزويده بصورة ذات دقة أعلى.

---

## حالات الحافة الشائعة وكيفية التعامل معها

| الموقف | الإصلاح المقترح |
|-----------|----------------|
| **Null image** – `ocrEngine.Image` is `null` | تحقق من مسار الملف قبل الإسناد؛ ألقِ استثناء `ArgumentException` واضح إذا كان مفقودًا. |
| **GPU not available** – `EnableGpu = true` throws `PlatformNotSupportedException` | غلف استدعاء تمكين GPU بـ `try/catch` وارجع إلى وضع CPU. |
| **Large receipts ( > 10 MB )** cause memory pressure | استخدم `GpuMemoryLimit` أو عالج الصورة على شكل بلاطات (`ocrEngine.Configuration.TileSize`). |
| **Incorrect language detection** – output contains gibberish | عيّن `ocrEngine.Configuration.Language = "eng"` (أو رمز ISO المناسب) لإجبار اللغة على الإنجليزية. |

---

## نصائح احترافية لـ OCR جاهز للإنتاج

1. **Batch processing:** أعد استخدام نسخة واحدة من `OcrEngine` لمجموعة من الصور؛ تقوم بتخزين نماذج اللغة وتقلل من زمن الاستجابة.
2. **Pre‑filtering:** طبّق تحويل بسيط إلى تدرج الرمادي وتعزيز التباين قبل تسليم الصورة إلى المحرك — العديد من المكتبات تكشف عن طريقة `Preprocess`.
3. **Error logging:** احصل على `ocrEngine.LastError` (إن كان متاحًا) بعد كل استدعاء لـ `Recognize()` لتشخيص الأخطاء دون تعطل خدمتك.
4. **Thread safety:** معظم محركات OCR **ليس** آمنة للمتعدد الخيوط. إذا كنت تحتاج إلى التوازي، أنشئ محركًا منفصلًا لكل خيط أو استخدم طابورًا متزامنًا.

---

## الخلاصة

لقد استعرضنا للتو سير عمل كامل لـ **run OCR on image** في C#. بدءًا من إنشاء المحرك، **loading image for OCR**، تفعيل تسريع GPU، وأخيرًا **extracting text from receipt**، لديك الآن أساس قوي لبناء خطوط معالجة مستندات أكثر تعقيدًا.

الخطوات التالية قد تشمل:

* تحليل نص الفاتورة إلى JSON منظم (باستخدام regex أو مكتبة لغة طبيعية) – مفيد لأتمتة **read text from image**.
* دمج خطوة OCR في واجهة برمجة تطبيقات ASP .NET Core بحيث يمكن للمستخدمين رفع الفواتير عبر HTTP.
* تجربة خلفيات OCR مختلفة (Tesseract مقابل SDKs تجارية) لمقارنة الدقة.

جرّب ذلك مع عدة تخطيطات مختلفة للفواتير، عدّل الإعدادات، وسترى مدى السرعة التي يمكنك بها تحويل صورة غير واضحة إلى بيانات قابلة للتنفيذ. برمجة سعيدة، ولتكن صورك دائمًا واضحة!

---

## دروس ذات صلة

- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)
- [كيفية استخراج النص من الصورة عن طريق إعداد المستطيلات في OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}