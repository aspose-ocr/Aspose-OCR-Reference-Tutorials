---
date: 2026-04-23
description: تعرّف على كيفية تحويل الصور إلى PDF باستخدام C# و Aspose.OCR، وحفظ نتائج
  OCR متعددة الصفحات كوثائق، واستخراج النص من الصور.
keywords:
- extract text from images
- batch image to pdf
- convert scanned images pdf
linktitle: تحويل الصور إلى PDF باستخدام C# – حفظ نتيجة OCR متعددة الصفحات
second_title: Aspose.OCR .NET API
title: استخراج النص من الصور – تحويل الصور إلى PDF C#
url: /ar/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصور – تحويل الصور إلى PDF C#

## المقدمة

في هذا الدرس ستتعرف على كيفية **استخراج النص من الصور** أثناء **تحويل الصور إلى PDF C#** باستخدام Aspose.OCR لـ .NET، ثم حفظ نتيجة الـ OCR متعددة الصفحات كمستند. سواء كنت بحاجة إلى **تحويل دفعة من الصور إلى PDF** للأرشفة، أو **تحويل الصور الممسوحة ضوئياً إلى PDF** للامتثال، أو ببساطة سحب نص قابل للبحث من الصور، سنستعرض كل خطوة مع شروحات واضحة، ونصائح عملية، وتوصيات لأفضل الممارسات.

## الإجابات السريعة
- **ما الذي يغطيه هذا الدرس؟** تحويل عدة صور إلى PDF/Docx/Txt/Xlsx واستخراج النص من الصور باستخدام Aspose.OCR في C#.
- **ما هي صيغ الإخراج المدعومة؟** Docx، Text، Pdf، و Xlsx (يمكنك أيضاً إخراج PDF مباشرة).
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للتقييم؛ الترخيص الدائم مطلوب للإنتاج.
- **ما إصدارات .NET المتوافقة؟** .NET Framework 4.5+، .NET Core 3.1+، .NET 5/6/7.
- **هل يمكن استخراج النص أثناء التحويل؟** نعم—استخدم نتائج OCR لسحب النص قبل الحفظ.

## ما هو “استخراج النص من الصور” ولماذا دمجه مع تحويل PDF؟

استخراج النص من الصور يعني استخدام OCR (التعرف الضوئي على الأحرف) لتحويل الأحرف المرئية إلى سلاسل نصية قابلة للبحث والتحرير. عندما **تحول الصور إلى PDF C#**، تقوم بدمج هذه السلاسل داخل ملف PDF بحيث يصبح المستند قابلاً للبحث والفهرسة—مثالي للأرشفة الرقمية واستخراج البيانات.

## لماذا نستخدم Aspose.OCR لهذه المهمة؟

- **دقة عالية** عبر عشرات اللغات.  
- **دعم الصفحات المتعددة** – معالجة دفعات من الصور في استدعاء واحد (مثالي لسيناريوهات **تحويل دفعة من الصور إلى PDF**).  
- **حفظ مباشر** إلى صيغ مكتبية شائعة دون خطوات تحويل إضافية.  
- **تكامل كامل مع .NET** – لا يعتمد على مكونات أصلية، يعمل على Windows، Linux، وبيئات السحابة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود التالي:

1. تثبيت Aspose.OCR لـ .NET. يمكنك تنزيله [هنا](https://releases.aspose.com/ocr/net/).  
2. الحصول على نسخة تجريبية مجانية أو ترخيص مُشتَرٍ – احصل على نسخة تجريبية [هنا](https://releases.aspose.com/) أو اشترِ واحدة [هنا](https://purchase.aspose.com/buy).  
3. مراجعة الوثائق الرسمية [هنا](https://reference.aspose.com/ocr/net/) لتتعرف على واجهة البرمجة (API).  
4. الانضمام إلى المجتمع عبر [منتديات الدعم](https://forum.aspose.com/c/ocr/16) للحصول على المساعدة في أي عوائق.  

الآن بعد أن أصبح كل شيء جاهزًا، لنبدأ بالبرمجة.

## استيراد المساحات الاسمية

ابدأ بإضافة المساحات الاسمية المطلوبة إلى ملف C# الخاص بك:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

تمنحك هذه الاستيرادات الوصول إلى المجموعات، معالجة الملفات، LINQ، وفئات Aspose OCR.

## الخطوة 1: تحديد مسار دليل المستندات

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

استبدل `"Your Document Directory"` بالمسار المطلق أو النسبي حيث توجد صور المصدر وأين تريد حفظ ملفات الإخراج.

## الخطوة 2: تهيئة Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

إنشاء كائن `AsposeOcr` يمنحك الوصول إلى جميع عمليات OCR، بما في ذلك سير عمل **تحويل الصور إلى PDF C#**.

## الخطوة 3: التعرف على الصور

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

طريقة `RecognizeMultipleImages` تعالج كل ملف في القائمة وتعيد مجموعة من `RecognitionResult`. يمكنك تمرير أي عدد من الصور، وهو ما يناسب سيناريوهات **تحويل الصور الممسوحة ضوئياً إلى PDF**.

## الخطوة 4: حفظ النتائج بالصيغ المفضلة

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

اختر الصيغة التي تتناسب مع سير عملك اللاحق:

- **Docx** – مستند Word قابل للتحرير مع نص قابل للبحث.  
- **Text** – استخراج نص عادي للبحث السريع عن البيانات (**استخراج النص من الصور**).  
- **Pdf** – إخراج PDF الكلاسيكي، مثالي للأرشفة.  
- **Xlsx** – تمثيل جدول بيانات للبيانات الجدولية.

## حالات الاستخدام الشائعة

- **الأرشفة الرقمية:** تحويل العقود الورقية الممسوحة إلى ملفات PDF قابلة للبحث.  
- **أتمتة إدخال البيانات:** استخراج النص من الإيصالات أو الفواتير وإدخاله في قاعدة بيانات.  
- **المعالجة الدفعية:** معالجة آلاف الصور في مهمة واحدة مع كود بسيط—مثالي لاحتياجات **تحويل دفعة من الصور إلى PDF**.

## استكشاف الأخطاء وإصلاحها والنصائح

- **مجموعات الصور الكبيرة:** عالج الصور على دفعات أصغر لتجنب ارتفاع استهلاك الذاكرة.  
- **جودة الصورة:** تأكد من أن الصور بدقة لا تقل عن 300 dpi للحصول على أقصى دقة OCR.  
- **أخطاء الترخيص:** تحقق من تحميل ملف الترخيص بشكل صحيح قبل استدعاء طرق OCR.  
- **نتائج فارغة:** محرك OCR يُرجع `RecognitionResult` فارغ للصفحات غير القابلة للقراءة؛ افحص `result[i].Text` للتحقق من قيم null أو فارغة وتعامل معها وفقًا لذلك.

## الأسئلة المتكررة

**س: هل يمكنني تحويل الصور إلى PDF C# دون استخدام OCR؟**  
ج: نعم، يمكنك استخدام Aspose.PDF أو مكتبات أخرى للتحويل الصرف من صورة إلى PDF، لكن OCR يضيف نصًا قابلًا للبحث.

**س: كيف يمكن استخراج النص من الصور في C# بعد التحويل؟**  
ج: قائمة `result` التي تُرجعها `RecognizeMultipleImages` تحتوي على خاصية `Text` يمكنك كتابتها إلى ملف `.txt` أو معالجتها مباشرة.

**س: هل يمكن ضبط هوامش الصفحة أو الاتجاه بشكل مخصص؟**  
ج: عند الحفظ إلى PDF أو Docx، يمكنك تعديل تخطيط المستند عبر واجهات Aspose.Words أو Aspose.PDF قبل استدعاء `SaveMultipageDocument`.

**س: ماذا يحدث إذا تعذرت قراءة صورة ما؟**  
ج: محرك OCR يُرجع `RecognitionResult` فارغ لتلك الصفحة؛ يمكنك فحص `result[i].Text` للتحقق من قيم null أو فارغة ومعالجتها وفقًا لذلك.

**س: هل يدعم الـ API النشر على السحابة؟**  
ج: نعم، المكتبة تعمل على أي بيئة تشغيل .NET، بما في ذلك Azure Functions وAWS Lambda، طالما أن بيئة التشغيل تلبي متطلبات الإصدار.

---

**آخر تحديث:** 2026-04-23  
**تم الاختبار مع:** Aspose.OCR 24.11 لـ .NET  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}