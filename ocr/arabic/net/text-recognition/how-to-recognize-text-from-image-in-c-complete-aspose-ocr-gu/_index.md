---
category: general
date: 2026-07-05
description: تعلم كيفية التعرف على النص من الصورة باستخدام Aspose OCR مع تسريع GPU
  وكيفية تحميل الصورة للتعرف الضوئي على الأحرف في بضع خطوات فقط.
draft: false
keywords:
- how to recognize text from image
- load image for OCR
language: ar
og_description: كيف تتعرف على النص من صورة باستخدام Aspose OCR؟ اتبع هذا الدليل لتحميل
  الصورة للتعرف الضوئي على الأحرف، وتمكين وحدة معالجة الرسومات، والحصول على النتائج
  بسرعة.
og_title: كيفية التعرف على النص من الصورة – Aspose OCR باستخدام وحدة معالجة الرسومات
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to recognize text from image using Aspose OCR with GPU acceleration
    and how to load image for OCR in just a few steps.
  headline: How to Recognize Text from Image in C# – Complete Aspose OCR Guide
  type: TechArticle
tags:
- Aspose OCR
- C#
- GPU acceleration
title: كيفية التعرف على النص من الصورة في C# – دليل Aspose OCR الكامل
url: /ar/net/text-recognition/how-to-recognize-text-from-image-in-c-complete-aspose-ocr-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف على النص من صورة – دليل Aspose OCR الكامل

هل تساءلت يومًا **كيف تتعرف على النص من صورة** عندما يكون الملف ضخمًا ويشعر معالجك وكأنه عالق في زحمة المرور؟ لست الوحيد. في العديد من المشاريع الواقعية—مثل مسح الفواتير أو أرشفة المستندات على دفعات—عادةً ما تكون خطوة OCR هي عنق الزجاجة، وليس باقي خط الأنابيب.

الأخبار السارة؟ مع Aspose.OCR يمكنك تشغيل محرك مدعوم بـ GPU، وتوجيهه إلى ملف TIFF أو PNG، والسماح للمكتبة بالقيام بالعمل الشاق. أدناه سترى بالضبط **كيف تتعرف على النص من صورة**، وبنفس الأهمية، **كيف تقوم بتحميل الصورة لـ OCR** دون الوقوع في حدود الذاكرة.

> **ما ستحصل عليه**  
> تطبيق C# Console قابل للتنفيذ بالكامل يقرأ صورة كبيرة، يشغل OCR مدعومًا بـ GPU، يطبع وقت المعالجة، ويتعامل مع المشكلات الشائعة مثل ضبط حجم الدفعة.

---

## المتطلبات المسبقة

* **.NET 6.0** (أو أي نسخة حديثة من .NET) مثبتة.  
* حزمة NuGet **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`).  
* **GPU** يدعم CUDA 10+ (اختياري لكنه موصى به بشدة للسرعة).  
* ملف صورة—`large_batch.tif` يعمل بشكل ممتاز لاختبار معالجة الدفعات.

لا تحتاج إلى أي مكتبات أصلية إضافية؛ Aspose.OCR يضم كل شيء.

---

## الخطوة 1: إعداد محرك OCR – وضع GPU

أول شيء تحتاج إلى القيام به هو إنشاء مثيل `OcrEngine` يعمل على الـ GPU. هنا يبدأ سحر **كيفية التعرف على النص من صورة**.

```csharp
using Aspose.OCR;

// Create an OCR engine that uses the GPU
OcrEngine ocrEngine = new OcrEngine(OcrEngineMode.Gpu);
```

*لماذا GPU؟*  
نوى الـ GPU تتفوق في معالجة الصور بشكل متوازي. عندما تزودها بملف TIFF عالي الدقة، يستطيع الـ GPU مسح آلاف البكسلات في آن واحد، مما يقلل الدقائق من مهمة قد تستغرق ساعات على نواة CPU واحدة.

---

## الخطوة 2: اختيار اللغة – الإنجليزية في هذا المثال

تحديد اللغة يخبر المحرك مجموعة الأحرف المتوقعة. الإنجليزية هي الافتراضية لمعظم العروض، لكن Aspose يدعم أكثر من 100 لغة.

```csharp
ocrEngine.Language = OcrLanguage.English;
```

إذا احتجت يومًا إلى التبديل إلى، مثلاً، الفرنسية، فقط استبدل `OcrLanguage.English` بـ `OcrLanguage.French`. نفس السطر يعمل مع أي لغة مدعومة.

---

## الخطوة 3: تحميل الصورة لـ OCR – الخطوة الحرجة

الآن نجيب مباشرة على الكلمة المفتاحية الثانية: **كيف تقوم بتحميل الصورة لـ OCR**. Aspose.OCR توفر أداة مساعدة `ImageStream` المريحة التي تُجرد تفاصيل نظام الملفات.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/large_batch.tif");
```

> **نصيحة احترافية:** استخدم المسارات المطلقة في بيئة الإنتاج لتجنب مفاجآت “الملف غير موجود”، خاصةً عندما يعمل تطبيقك كخدمة Windows.

إذا كانت صورتك موجودة في مصفوفة بايت (مثلاً، تم تنزيلها من واجهة ويب API)، يمكنك استخدام `ImageStream.FromBytes(byteArray)` بدلاً من ذلك—بدون الحاجة إلى كود إضافي.

---

## الخطوة 4: (اختياري) ضبط ذاكرة GPU بحجم الدفعة

ملفات TIFF الكبيرة يمكن أن تستهلك الكثير من ذاكرة الـ GPU. Aspose يتيح لك تقسيم العمل إلى دفعات، وهو مفيد عندما تقوم بمعالجة مجلد كامل مرة واحدة.

```csharp
// Adjust GPU batch size – 8 works well for most modern cards
ocrEngine.GpuSettings.BatchSize = 8;
```

*متى يجب تغييره؟*  
- **GPU صغير (2‑4 GB):** قلل حجم الدفعة إلى 4 أو حتى 2.  
- **GPU كبير (8 GB+):** لا تتردد في رفعه إلى 16 للحصول على تدفق أسرع.

---

## الخطوة 5: تشغيل محرك التعرف

تم الانتهاء من جميع التحضيرات؛ الآن نقوم أخيرًا بتنفيذ OCR. هذه الدعوة الواحدة تقوم بكل شيء—المعالجة المسبقة، تجزئة الأحرف، واستخراج النص.

```csharp
// Perform the OCR recognition
ocrEngine.Recognize();
```

بعد انتهاء `Recognize()`، يمكنك جلب النتيجة عبر `ocrEngine.Text`. للتحقق السريع من الصحة، دعنا نطبع أول 200 حرف.

```csharp
string result = ocrEngine.Text;
Console.WriteLine("Extracted text (first 200 chars):");
Console.WriteLine(result.Substring(0, Math.Min(200, result.Length)));
```

---

## الخطوة 6: قياس الأداء – ما مدى السرعة؟

إحدى أكبر الأسئلة عندما تسأل **كيف تتعرف على النص من صورة** هي “كم من الوقت سيستغرق؟” Aspose.OCR يسجل وقت المعالجة تلقائيًا.

```csharp
// Display the time taken for processing
Console.WriteLine($"Time: {ocrEngine.ProcessingTime.TotalSeconds}s");
```

على بطاقة RTX 3060 متوسطة المستوى، عادةً ما ينتهي العينة `large_batch.tif` (≈30 MB) في أقل من **3 ثوانٍ**. عند تشغيله على CPU فقط، توقع 10‑15 ثانية لنفس الملف.

---

## مثال كامل يعمل

جمع كل الأجزاء معًا يمنحك برنامجًا جاهزًا للتشغيل. انسخ الكود إلى مشروع Console جديد واضغط **F5**.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize GPU‑accelerated OCR engine
            OcrEngine ocrEngine = new OcrEngine(OcrEngineMode.Gpu);

            // Step 2: Set language to English
            ocrEngine.Language = OcrLanguage.English;

            // Step 3: Load the image for OCR
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/large_batch.tif");

            // Step 4: Optional – tune batch size for GPU memory
            ocrEngine.GpuSettings.BatchSize = 8;

            // Step 5: Run recognition
            ocrEngine.Recognize();

            // Step 6: Output results and timing
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrEngine.Text);
            Console.WriteLine($"Processing time: {ocrEngine.ProcessingTime.TotalSeconds}s");
        }
    }
}
```

**الناتج المتوقع** (مقتطع للختصر):

```
=== OCR Result ===
Invoice #12345
Date: 2026-07-01
Total: $1,234.56
...
Processing time: 2.87s
```

إذا طبع الـ console سلسلة فارغة، تحقق مرة أخرى من وجود ملف الصورة وأن تعريفات الـ GPU محدثة.

---

## المشكلات الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| `ProcessingTime` is **0** | لم يتم التعرف على تعريف GPU؛ عاد المحرك إلى CPU | تأكد من تثبيت بيئة تشغيل CUDA وأن الـ GPU مرئي عبر `nvidia-smi`. |
| `ocrEngine.Text` is **null** | تنسيق الصورة غير مدعوم أو معطوب | حوّل الملف إلى تنسيق مدعوم (TIFF, PNG, JPEG) قبل التحميل. |
| Out‑of‑memory exception | حجم الدفعة كبير جدًا بالنسبة للـ GPU | قلل `GpuSettings.BatchSize` حتى يختفي الخطأ. |
| Poor accuracy on handwritten text | نموذج اللغة الافتراضي مخصص للنص المطبوع | قم بالتبديل إلى `OcrLanguage.EnglishHandwritten` إذا كان متاحًا، أو عالج الصورة مسبقًا (تحويل إلى ثنائي، إزالة الضوضاء). |

---

## توسيع الحل

الآن بعد أن عرفت **كيف تتعرف على النص من صورة** و**كيف تقوم بتحميل الصورة لـ OCR**، يمكنك:

* **معالجة مجلد** – تكرار عبر `Directory.GetFiles(...)` وإعادة استخدام نفس مثيل `OcrEngine` للسرعة.  
* **تصدير إلى PDF** – تمرير `ocrEngine.Text` إلى مولد PDF مثل Aspose.PDF.  
* **دمج مع Azure Functions** – تحويل المقتطف إلى نقطة نهاية بدون خادم لتشغيل OCR حسب الطلب.

كل من هذه الإضافات يتبع النمط نفسه: التهيئة مرة واحدة، تحديد اللغة، تحميل الصورة، التعرف، ومعالجة الناتج.

---

## الخلاصة

لقد استعرضنا كل خطوة مطلوبة للإجابة على **كيف تتعرف على النص من صورة** باستخدام وضع GPU في Aspose.OCR، وأظهرنا بالضبط **كيف تقوم بتحميل الصورة لـ OCR** بطريقة نظيفة وقابلة لإعادة الاستخدام. المثال الكامل يعمل في ثوانٍ، ويتوسع مع حجم الدفعة، ويمنحك تحكمًا كاملًا في اللغة والأداء.

جرّبه، عدّل حجم الدفعة، وشاهد زيادة إنتاجية OCR. عندما تكون جاهزًا، استكشف المواضيع ذات الصلة مثل *معالجة الصورة مسبقًا لـ OCR* أو *معالجة الدفعات باستخدام Azure Batch*—الحدود لا توجد.

هل لديك أسئلة أو صورة صعبة ترفض التعاون؟ اترك تعليقًا أدناه، ولنحل المشكلة معًا. برمجة سعيدة!

![how to recognize text from image using Aspose OCR GPU](ocr_gpu_example.png)

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية التعرف على نص الصورة باستخدام اللغة مع Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [كيفية استخراج النص من صورة عبر URL باستخدام Aspose.OCR للـ Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)
- [كيفية استخدام Aspose OCR للحصول على نتيجة JSON في التعرف على الصور](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}