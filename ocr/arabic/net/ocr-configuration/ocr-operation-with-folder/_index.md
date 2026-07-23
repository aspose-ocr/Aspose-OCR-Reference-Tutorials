---
date: 2026-07-23
description: تعلم كيفية استخراج النص من الصور باستخدام Aspose.OCR لـ .NET، مما يتيح
  التعرف على الصور عبر OCR القائم على المجلدات.
keywords:
- extract text from images
- convert images to text
- ocr multiple images
lastmod: 2026-07-23
linktitle: عملية OCR مع المجلد في التعرف على الصور باستخدام OCR
og_description: استخراج النص من الصور باستخدام Aspose.OCR لـ .NET. تعلم OCR القائم
  على المجلدات، المعالجة الدفعية، وأفضل الممارسات في C# في بضع خطوات فقط.
og_image_alt: Guide showing C# code extracting text from image files using Aspose.OCR
og_title: استخراج النص من الصور باستخدام عملية OCR على المجلدات – دليل Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from images using Aspose.OCR for .NET, enabling
    folder‑based OCR image recognition.
  headline: Extract Text from Images Using OCR Operation on Folders
  type: TechArticle
- description: Learn how to extract text from images using Aspose.OCR for .NET, enabling
    folder‑based OCR image recognition.
  name: Extract Text from Images Using OCR Operation on Folders
  steps:
  - name: Set Document Directory
    text: Define the folder that holds the images you want to process. > **Pro tip:**
      Use an absolute path or `Path.Combine` to avoid path‑separator issues on different
      OSes.
  - name: Initialize Aspose.OCR
    text: Create an instance of the OCR engine.
  - name: Specify Image Path
    text: Point the API to the specific sub‑folder that contains your image files.
      > **Why this matters:** The `RecognizeMultipleImages` method expects a folder
      path, not a single file.
  - name: Recognize Images
    text: Run OCR on every image inside the folder. You can customize `RecognitionSettings`
      if you need language hints or specific preprocessing. `RecognitionResult` contains
      the extracted text and confidence information for a processed image.
  - name: Print Results
    text: Iterate through the returned `RecognitionResult` array and output the extracted
      text. > **Common pitfall:** Forgetting to check `result.Length` can cause an
      `IndexOutOfRangeException` when the folder is empty. Always validate the folder
      content first.
  - name: Completion Message
    text: Signal successful execution.
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR for .NET is a commercial product. For licensing information,
      visit [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for .NET in commercial projects?
  - answer: Yes, you can explore a free trial [here](https://releases.aspose.com/).
    question: Is there a free trial available?
  - answer: The documentation is available [here](https://reference.aspose.com/ocr/net/).
    question: Where can I find the documentation?
  - answer: Temporary licenses can be obtained [here](https://purchase.aspose.com/temporary-license/).
    question: How can I obtain a temporary license for evaluation?
  - answer: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) for community
      support.
    question: Need support or have questions?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- extract text from images
- Aspose.OCR
- C# OCR library
title: استخراج النص من الصور باستخدام عملية OCR على المجلدات
url: /ar/net/ocr-configuration/ocr-operation-with-folder/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصور باستخدام عملية OCR على المجلدات

## مقدمة

مرحبًا بك في عالم التعرف الضوئي على الأحرف (OCR) مع **Aspose.OCR for .NET**! إذا كنت بحاجة إلى **استخراج النص من الصور** بكميات كبيرة—مثلاً مجلد كامل من المستندات الممسوحة ضوئيًا—ستقودك هذه الدورة التعليمية عبر حل عملي وواقعي. سنغطي كل شيء من إعداد المشروع إلى طباعة النص المعترف به، حتى تتمكن من دمج OCR القائم على المجلدات بسرعة في تطبيقات C# الخاصة بك. في النهاية، سترى أيضًا كيف يتيح لك هذا النهج **تحويل الصور إلى نص**، **استخراج النص من المستندات الممسوحة**، و**قراءة نص الصورة في C#** ببضع أسطر من الشيفرة.

## إجابات سريعة
- **ما الذي تعلمه هذه الدورة التعليمية؟** كيفية استخراج النص من الصور المخزنة في مجلد باستخدام Aspose.OCR.  
- **ما اللغة والمنصة؟** C# مع .NET (Framework أو .NET Core).  
- **المتطلب الأساسي؟** مكتبة Aspose.OCR for .NET – قم بتنزيلها [هنا](https://releases.aspose.com/ocr/net/).  
- **كم عدد مقتطفات الشيفرة؟** سبعة نُسخ مختصرة توضح كل خطوة.  
- **هل يمكنني تحويل الصور إلى نص؟** بالتأكيد—هذا المثال يُظهر التحويل من البداية إلى النهاية.

## ما هو “استخراج النص من الصور”؟
يستخدم استخراج النص من الصور تقنية OCR لتحويل الأحرف في الصور أو ملفات PDF أو المسحات الضوئية إلى سلاسل قابلة للتحرير والبحث. توفر Aspose.OCR محركًا قويًا يدعم العديد من صيغ الصور واللغات. تمكّن هذه التقنية المطورين من تحويل المحتوى البصري إلى نص يمكن قراءته آليًا، مما يسهل عمليات الفهرسة والبحث واستخراج البيانات عبر مجموعة واسعة من التطبيقات.

## لماذا تستخدم Aspose.OCR لـ OCR القائم على المجلدات؟
حمّل المجلد بالكامل باستخدام استدعاء API واحد ودع Aspose.OCR يتولى اكتشاف اللغة، تحليل التخطيط، والمعالجة الدفعية. يدعم المحرك **أكثر من 70 صيغة صورة** (بما في ذلك PNG و JPEG و TIFF و BMP و WebP) ويمكنه معالجة ملفات تصل إلى **2 جيجابايت** دون تحميل المستند بالكامل في الذاكرة، مما يوفر نتائج عالية الدقة لأكثر من **30 لغة**.

## حالات الاستخدام الشائعة
- رقمنة مكتبة من الفواتير أو الإيصالات الممسوحة ضوئيًا.  
- تحويل ملفات PNG/JPEG المؤرشفة إلى نص قابل للبحث للفهرسة.  
- أتمتة إدخال البيانات عبر قراءة النص من صور ملصقات المنتجات.  
- بناء ميزة بحث في المستندات تحتاج إلى **استخراج النص من المستندات الممسوحة** في الوقت الفعلي.

## المتطلبات المسبقة
- إتقان أساسي للغة C# وتطوير .NET.  
- Visual Studio (أي نسخة حديثة).  
- مكتبة **Aspose.OCR for .NET** – قم بتنزيلها [هنا](https://releases.aspose.com/ocr/net/).  
- فهم لمفاهيم OCR (اختياري لكنه مفيد).

## استيراد مساحات الأسماء

أضف توجيهات `using` المطلوبة في أعلى ملف C# الخاص بك حتى يعرف المترجم مكان العثور على فئات OCR.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## كيفية استخراج النص من الصور باستخدام OCR على المجلدات؟

حمّل مسار المجلد، أنشئ محرك OCR، استدعِ `RecognizeMultipleImages`، وتكرّر عبر النتائج لطباعة نص كل صفحة. هذا التدفق من البداية إلى النهاية يعمل في أقل من ثانية لمجموعة نموذجية من 20 صورة على محطة عمل حديثة.

طريقة `RecognizeMultipleImages` تعالج جميع ملفات الصور المدعومة في دليل وتعيد مصفوفة من كائنات `RecognitionResult`.  
تتيح لك `RecognitionSettings` تحديد اللغة، المعالجة المسبقة، وغيرها من خيارات OCR.

### دليل خطوة بخطوة

### الخطوة 1: تعيين دليل المستند
حدد المجلد الذي يحتوي على الصور التي تريد معالجتها.

```csharp
// ExStart:1   
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

> **نصيحة احترافية:** استخدم مسارًا مطلقًا أو `Path.Combine` لتجنب مشاكل فواصل المسار على أنظمة تشغيل مختلفة.

### الخطوة 2: تهيئة Aspose.OCR
أنشئ نسخة من محرك OCR.

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### الخطوة 3: تحديد مسار الصورة
وجّه الـ API إلى المجلد الفرعي المحدد الذي يحتوي على ملفات الصور الخاصة بك.

```csharp
// Image Path
string fullPath = dataDir + "OCR";
```

> **لماذا هذا مهم:** طريقة `RecognizeMultipleImages` تتوقع مسار مجلد، وليس ملفًا واحدًا.

### الخطوة 4: التعرف على الصور
نفّذ OCR على كل صورة داخل المجلد. يمكنك تخصيص `RecognitionSettings` إذا كنت بحاجة إلى تلميحات لغة أو معالجة مسبقة محددة.

```csharp
// Recognize image           
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //default or custom
});
```

`RecognitionResult` يحتوي على النص المستخرج ومعلومات الثقة لصورة معالجة.  

### الخطوة 5: طباعة النتائج
تكرّر عبر مصفوفة `RecognitionResult` المُرجعة واطبع النص المستخرج.

```csharp
// Print result
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

> **مشكلة شائعة:** نسيان التحقق من `result.Length` قد يسبب `IndexOutOfRangeException` عندما يكون المجلد فارغًا. تحقق دائمًا من محتوى المجلد أولاً.

### الخطوة 6: رسالة الانتهاء
أظهر إشارة إلى نجاح التنفيذ.

```csharp
// ExEnd:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

## نصائح وأفضل الممارسات
- **حجم الدفعة:** إذا كنت تعالج آلاف الملفات، قسّم المجلد إلى دفعات أصغر (مثلاً 500 صورة لكل دفعة) للحفاظ على استهلاك الذاكرة بشكل متوقع.  
- **تلميحات اللغة:** توفير رمز اللغة الصحيح في `RecognitionSettings` يحسن الدقة بشكل كبير، خاصةً للخطوط غير اللاتينية.  
- **المعالجة غير المتزامنة:** غلف استدعاء OCR داخل `Task.Run` أو استخدم async/await للحفاظ على استجابة خيوط واجهة المستخدم.  
- **التحقق من الملفات:** قبل استدعاء `RecognizeMultipleImages`، صَفِّ الدليل للامتدادات المدعومة (`.png`, `.jpg`, `.jpeg`, `.tif`, `.tiff`).  
- **مراقبة الأداء:** استخدم `Stopwatch` لتسجيل الوقت المستغرق لكل دفعة؛ على معالج رباعي النوى ستلاحظ ~0.8 ثانية لكل 100 صورة.

## المشكلات الشائعة والحلول
| المشكلة | السبب | الحل |
|-------|-------|-----|
| لا يتم إرجاع أي ناتج | مسار المجلد غير صحيح أو فارغ | تحقق من أن `fullPath` يشير إلى الدليل الصحيح ويحتوي على صيغ صور مدعومة (PNG, JPEG, TIFF). |
| أحرف مشوشة | إعدادات لغة غير صحيحة | مرّر `RecognitionSettings` مكوَّنة مع `Language` المحدد إلى رمز ISO المناسب. |
| بطء الأداء مع العديد من الصور | المعالجة تسلسليًا على خيط واجهة المستخدم | نفّذ OCR على خيط خلفي أو استخدم نمط async للحفاظ على استجابة واجهة المستخدم. |

## الأسئلة المتكررة

**س: هل يمكنني استخدام Aspose.OCR for .NET في المشاريع التجارية؟**  
ج: نعم، Aspose.OCR for .NET هو منتج تجاري. للحصول على معلومات الترخيص، زر [هنا](https://purchase.aspose.com/buy).

**س: هل هناك نسخة تجريبية مجانية متاحة؟**  
ج: نعم، يمكنك تجربة نسخة تجريبية مجانية [هنا](https://releases.aspose.com/).

**س: أين يمكنني العثور على الوثائق؟**  
ج: الوثائق متاحة [هنا](https://reference.aspose.com/ocr/net/).

**س: كيف يمكنني الحصول على ترخيص مؤقت للتقييم؟**  
ج: يمكن الحصول على تراخيص مؤقتة [هنا](https://purchase.aspose.com/temporary-license/).

**س: هل تحتاج إلى دعم أو لديك أسئلة؟**  
ج: زر [منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) للحصول على دعم المجتمع.

---
**آخر تحديث:** 2026-07-23  
**تم الاختبار مع:** Aspose.OCR 24.11 for .NET  
**المؤلف:** Aspose

## دروس ذات صلة
- [كيفية معالجة مجموعة من الصور باستخدام OCR مع List في Aspose.OCR for .NET](/ocr/net/ocr-configuration/ocr-operation-with-list/)
- [كيفية استخراج النص من أرشيفات ZIP باستخدام Aspose.OCR for .NET](/ocr/net/ocr-configuration/ocr-operation-with-archive/)
- [استخراج النص من الصور – إعدادات OCR مع Aspose.OCR](/ocr/net/ocr-settings/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-wrap-class >}}