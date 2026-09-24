---
category: general
date: 2026-02-09
description: استخرج نص الصور بسرعة باستخدام C# عن طريق ضبط الحد الأقصى للتوازي في
  التعرف الضوئي على الحروف للدفعات – تعلم كيفية تحويل الصفحات الممسوحة ضوئياً، ومعالجة
  التعرف الضوئي على الحروف لعدة صور، وقراءة نص PNG بفعالية.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: ar
og_description: استخراج النص من الصور في C# عن طريق تعيين الحد الأقصى للتوازي. يوضح
  هذا الدرس كيفية تحويل الصفحات الممسوحة ضوئياً، تشغيل OCR على عدة صور، وقراءة نص
  PNG باستخدام Aspose OCR.
og_title: استخراج النصوص من صور PNG باستخدام C# – دليل OCR كامل للدفعات
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: استخراج النص من الصور بصيغة PNG باستخدام C# – التعرف الضوئي على الأحرف دفعيًا
  باستخدام Aspose OCR
url: /ar/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صور PNG باستخدام C# – OCR دفعي باستخدام Aspose OCR

هل احتجت يوماً إلى **استخراج النص من الصور** في مجلد يحتوي على ملفات PNG ممسوحة ضوئياً لكن شعرت بالتعثر عند سؤال “كيف أجعل العملية سريعة؟”؟ لست وحدك. في العديد من المشاريع الواقعية، يحتاج المطورون إلى **تحديد الحد الأقصى للتوازي** بحيث يتم معالجة عشرات الصفحات في ثوانٍ بدلاً من دقائق.  

في هذا الدليل سنستعرض مثالاً كاملاً قابلاً للتنفيذ ي **يحوّل الصفحات الممسوحة**، ويجري **OCR على صور متعددة**، وأخيراً **يقرأ نص PNG** دون عناء. لا روابط “انظر الوثائق” غامضة—فقط كود يمكنك نسخه‑لصقه، وتفسيرات لماذا كل سطر مهم، ونصائح لتجنب المشكلات الشائعة.

> **نصيحة احترافية:** إذا كنت تستخدم Aspose OCR في مكان آخر، ستلاحظ ظهور فئة `OcrEngine` نفسها هنا، لكننا سنضبط إعداداتها للمعالجة المتوازية الفعلية.

---

## ما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.6+). تعمل الواجهة البرمجية بنفس الطريقة، لكن أوقات التشغيل الأحدث تعطي تحكمًا أفضل في الخيوط.  
- **Aspose.OCR for .NET** – تثبيت عبر NuGet: `Install-Package Aspose.OCR`.  
- مجلد يحتوي على بعض ملفات PNG الممسوحة (`page1.png`, `page2.png`, …).  
- بيئة تطوير أو محرر تشعر بالراحة معه (Visual Studio, Rider, VS Code…).

هذا كل ما تحتاجه. لا خدمات إضافية، لا مفاتيح سحابة، مجرد معالجة محلية بحتة.

---

## استخراج النص من الصور – ضبط الحد الأقصى للتوازي لـ OCR الدفعي

عند تشغيل OCR على عدة ملفات، يستخدم المحرك، بشكل افتراضي، خيطًا واحدًا. هذا آمن لكنه بطيء جدًا. من خلال ضبط `MaxDegreeOfParallelism` تخبر المحرك بعدد الخيوط التي يمكنه تشغيلها في آنٍ واحد.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**لماذا 4؟**  
العدد أربعة هو نقطة مثالية لمعظم الحواسيب المحمولة الحديثة—عدد كافٍ من الأنوية لإبقاء المعالج مشغولًا، لكن ليس كثيرًا لدرجة أن يطغى على العمليات الأخرى. إذا كنت تشغل هذا على خادم به 16 نواة، يمكنك رفع العدد إلى 12 أو 14 لتحقيق تسريع ملحوظ.

---

## تحويل الصفحات الممسوحة – بناء مجموعة تدفقات الصور

تتوقع Aspose كل صورة كـ `ImageStream`. تساعد الدالة `FromFile` في قراءة الملف، إبقائه في الذاكرة، وتسليمه إلى محرك OCR. يمكنك أيضًا تمرير `MemoryStream` إذا كانت صورك تأتي من قاعدة بيانات أو استجابة HTTP.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**حالة حافة:** إذا كان أي ملف مفقودًا أو تالفًا، ستطرح `FromFile` استثناءً من نوع `FileNotFoundException`. اح.wrap الإنشاء داخل `try/catch` إذا كنت تتوقع مدخلات غير موثوقة.

---

## OCR على صور متعددة – تنفيذ OCR دفعي

الآن يبدأ العمل الجاد. `RecognizeBatch` يطلق عدد الخيوط التي حددتها مسبقًا، يعالج كل صورة، ويعيد قائمة من كائنات `OcrResult`.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

خلف الكواليس، كل خيط يحمل صورته، يشغّل الشبكة العصبية، ويستخرج النص العادي. ترتيب النتائج يطابق ترتيب قائمة الإدخال، لذا يمكنك بأمان ربط الصفحة 1 → النتيجة 0، وهكذا.

---

## قراءة نص PNG – عرض المحتوى المستخرج

أخيرًا نمر على النتائج ونطبع النص العادي إلى وحدة التحكم. هنا يمكنك توجيه المخرجات إلى ملف، قاعدة بيانات، أو حتى خدمة معالجة لغة طبيعية لاحقة.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### ناتج وحدة التحكم المتوقع

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

إذا رأيت أقسامًا فارغة، تأكد من أن ملفات PNG ليست صورًا بيضاء بالكامل—OCR يحتاج إلى تباين مرئي.

---

## نصائح عملية ومشكلات شائعة

| الموقف | ما يجب فعله |
|-----------|------------|
| **ضغط الذاكرة** عند دفعات كبيرة | عالج الصور على دفعات من 10‑20 ملفًا، ثم استدعِ `GC.Collect()` إذا لاحظت ارتفاعًا مفاجئًا. |
| **كشف لغة غير صحيح** | اضبط `ocrEngine.Configuration.Language = OcrLanguage.English;` (أو اللغة المستهدفة) قبل استدعاء `RecognizeBatch`. |
| **أداء بطيء رغم التوازي** | تحقق من أن SSD لا يحد من عمليات الإدخال/الإخراج؛ اقرأ جميع الملفات إلى الذاكرة أولًا (كما نفعل مع `ImageStream.FromFile`). |
| **حروف مفقودة** | زد `ocrEngine.Configuration.DPI = 300;` لمعالجة بدقة أعلى. |

---

## توسيع المثال – من PNG إلى PDF أو DOCX

إذا احتجت في المستقبل إلى **تحويل الصفحات الممسوحة** إلى ملفات PDF قابلة للبحث، ما عليك سوى تمرير `ocrResults[i].PlainText` إلى مكتبة PDF (مثل Aspose.PDF) وتراكب النص كطبقة غير مرئية. نفس حيلة التوازي تعمل هناك أيضًا.

---

## الكود الكامل (جاهز للنسخ‑اللصق)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

احفظه باسم `BatchExample.cs`، شغّله بالأمر `dotnet run`، وسترى وحدة التحكم تمتلئ بالنص الذي كان مخفيًا داخل ملفات PNG تلك.

---

## ملخص بصري

![extract text images example](images/ocr-batch.png){alt="مثال استخراج النص من الصور"}

المخطط يوضح التدفق: **ملفات PNG → مجموعة ImageStream → OcrEngine (الحد الأقصى للتوازي) → نتائج OCR → وحدة التحكم / تخزين لاحق**.

---

## الخلاصة

أصبح لديك الآن وصفة شاملة من البداية للنهاية حول كيفية **استخراج النص من الصور** في C# مع **تحديد الحد الأقصى للتوازي**، **تحويل الصفحات الممسوحة**، معالجة **OCR على صور متعددة**، و**قراءة نص PNG** بكفاءة. الكود مكتمل، الشروحات تغطي “كيف” و “لماذا”، والنصائح تحافظ عليك من المتاعب الشائعة.

ما الخطوة التالية؟ جرّب استبدال قائمة PNG بحلقة `Directory.GetFiles` ديناميكية، جرب أعداد خيوط مختلفة، أو وجه المخرجات إلى PDF قابل للبحث. النمط نفسه يتوسع لمئات الصفحات مع سطر برمجي إضافي قليل جدًا.

لديك أسئلة أو حالة حافة معقدة؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}