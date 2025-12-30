---
date: 2025-12-30
description: تعلم كيفية تحويل الصور إلى PDF باستخدام C# و Aspose.OCR، حفظ نتائج OCR
  متعددة الصفحات كمستندات، واستخراج النص من الصور باستخدام C#.
linktitle: Convert Images to PDF C# – Save Multipage OCR Result
second_title: Aspose.OCR .NET API
title: تحويل الصور إلى PDF C# – حفظ نتيجة OCR متعددة الصفحات
url: /ar/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصور إلى PDF C# – حفظ نتيجة OCR متعددة الصفحات

## المقدمة

في هذا البرنامج التعليمي ستكتشف كيفية **تحويل الصور إلى PDF C#** باستخدام Aspose.OCR لـ .NET وحفظ ناتج OCR متعدد الصفحات كوثيقة. سواء كنت بحاجة إلى **تحويل الصور الممسوحة ضوئياً إلى PDF** للأرشفة أو **استخراج النص من الصور C#** لمعالجة البيانات، فإن هذا الدليل يشرح لك كل خطوة — مع أمثلة واقعية ونصائح لأفضل الممارسات.

## إجابات سريعة
- **ما الذي يغطيه هذا البرنامج التعليمي؟** تحويل صور متعددة إلى PDF/Docx/Txt/Pdf/Xlsx باستخدام Aspose.OCR في C#.
- **ما الصيغ المدعومة؟** Docx، Text، Pdf، و Xlsx (يمكنك أيضًا إخراج PDF مباشرة).
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تكفي للتقييم؛ يلزم ترخيص دائم للإنتاج.
- **ما إصدارات .NET المتوافقة؟** .NET Framework 4.5+، .NET Core 3.1+، .NET 5/6/7.
- **هل يمكنني استخراج النص أثناء التحويل؟** نعم — استخدم نتائج OCR لاستخراج النص قبل الحفظ.

## ما هو “تحويل الصور إلى PDF C#”؟

تحويل الصور إلى PDF في C# يعني برمجياً أخذ ملف أو أكثر من ملفات البت ماب (PNG، JPEG، TIFF، إلخ) وإنشاء مستند PDF يحافظ على التخطيط البصري مع إمكانية تضمين نص قابل للبحث عبر OCR. تجعل Aspose.OCR هذه العملية بسيطة وقابلة للتخصيص بشكل كبير.

## لماذا نستخدم Aspose.OCR لهذه المهمة؟

- **دقة عالية** محرك OCR يعمل مع العديد من اللغات.
- **دعم متعدد الصفحات** – معالجة دفعات من الصور في استدعاء واحد.
- **حفظ مباشر** إلى صيغ مكتبية شائعة دون خطوات تحويل إضافية.
- **تكامل كامل مع .NET** – لا توجد تبعيات أصلية أو أدوات خارجية.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من توفر ما يلي:

1. تثبيت Aspose.OCR لـ .NET. يمكنك تنزيله [هنا](https://releases.aspose.com/ocr/net/).
2. الحصول على نسخة تجريبية مجانية أو ترخيص مُشتَرٍ – احصل على نسخة تجريبية [هنا](https://releases.aspose.com/) أو اشترِ واحدة [هنا](https://purchase.aspose.com/buy).
3. مراجعة [الوثائق](https://reference.aspose.com/ocr/net/) الرسمية للتعرف على واجهة برمجة التطبيقات.
4. الانضمام إلى المجتمع عبر [منتديات الدعم](https://forum.aspose.com/c/ocr/16) للحصول على مساعدة في أي عقبة.

الآن بعد أن كل شيء جاهز، لنبدأ بالبرمجة.

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

## الخطوة 1: تعيين دليل المستند الخاص بك

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

استبدل `"Your Document Directory"` بالمسار المطلق أو النسبي حيث توجد صور المصدر الخاصة بك وأين تريد حفظ ملفات الإخراج.

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

طريقة `RecognizeMultipleImages` تعالج كل ملف في القائمة وتعيد مجموعة من `RecognitionResult`. يمكنك تمرير أي عدد من الصور، وهو مثالي لسيناريوهات **تحويل الصور الممسوحة ضوئياً إلى PDF**.

## الخطوة 4: حفظ النتائج بالتنسيقات المفضلة

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

اختر التنسيق الذي يناسب سير عملك اللاحق:

- **Docx** – مستند Word قابل للتحرير مع نص قابل للبحث.
- **Text** – استخراج نص عادي للبحث السريع عن البيانات (**استخراج النص من الصور C#**).
- **Pdf** – مخرجات PDF الكلاسيكية، مثالية للأرشفة.
- **Xlsx** – تمثيل جدول بيانات للبيانات الجدولية.

## حالات الاستخدام الشائعة

- **الأرشفة الرقمية:** تحويل العقود الورقية الممسوحة ضوئياً إلى ملفات PDF قابلة للبحث.
- **أتمتة إدخال البيانات:** استخراج النص من الإيصالات أو الفواتير وإدخاله في قاعدة بيانات.
- **المعالجة الدفعة:** معالجة آلاف الصور في مهمة واحدة بأقل قدر من الشيفرة.

## استكشاف الأخطاء وإصلاحها والنصائح

- **مجموعات الصور الكبيرة:** معالجة الصور على دفعات أصغر لتجنب ارتفاع الذاكرة.
- **جودة الصورة:** تأكد من أن الصور بدقة لا تقل عن 300 dpi للحصول على أفضل دقة OCR.
- **أخطاء الترخيص:** تحقق من تحميل ملف الترخيص بشكل صحيح قبل استدعاء طرق OCR.

## الأسئلة المتكررة (الأصلية)

### س1: هل تتوفر رخصة مؤقتة لأغراض الاختبار؟

A1: نعم، يمكنك الحصول على رخصة مؤقتة [هنا](https://purchase.aspose.com/temporary-license/) لاختبار Aspose.OCR.

### س2: هل يمكنني التعرف على النص من الصور بصيغ مختلفة؟

A2: بالتأكيد! يدعم Aspose.OCR صيغ صور متعددة، مما يضمن مرونة في مهام OCR الخاصة بك.

### س3: هل هناك أي قيود على عدد الصور للتعرف؟

A3: عدد الصور التي يمكنك معالجتها يعتمد على الترخيص الخاص بك. راجع الوثائق للتفاصيل.

### س4: كيف يمكنني التعامل مع الأخطاء أثناء التعرف على OCR؟

A4: راجع الوثائق للحصول على أفضل ممارسات التعامل مع الأخطاء أو اطلب المساعدة في منتديات الدعم.

### س5: هل يدعم Aspose.OCR لغات غير الإنجليزية؟

A5: نعم، يدعم Aspose.OCR عدة لغات. استكشف الوثائق للحصول على تفاصيل دعم اللغات.

## أسئلة متكررة إضافية

**س: هل يمكنني تحويل الصور إلى PDF C# دون استخدام OCR؟**  
ج: نعم، يمكنك استخدام Aspose.PDF أو مكتبات أخرى للتحويل الصرف من صورة إلى PDF، لكن OCR يضيف نصًا قابلًا للبحث.

**س: كيف أستخرج النص من الصور C# بعد التحويل؟**  
ج: قائمة `result` التي تُرجعها `RecognizeMultipleImages` تحتوي على خصائص `Text` يمكنك كتابتها إلى ملف `.txt` أو معالجتها مباشرة.

**س: هل يمكن ضبط هوامش الصفحة أو الاتجاه مخصصًا؟**  
ج: عند الحفظ إلى PDF أو Docx، يمكنك تعديل تخطيط المستند عبر واجهات Aspose.Words أو Aspose.PDF قبل استدعاء `SaveMultipageDocument`.

**س: ماذا يحدث إذا تعذر قراءة صورة؟**  
ج: يُرجع محرك OCR `RecognitionResult` فارغًا لتلك الصفحة؛ يمكنك فحص `result[i].Text` للتحقق من قيم null أو السلاسل الفارغة ومعالجتها وفقًا لذلك.

**س: هل يدعم الـ API النشر السحابي؟**  
ج: نعم، تعمل المكتبة على أي بيئة تشغيل .NET، بما في ذلك Azure Functions و AWS Lambda، طالما أن بيئة التشغيل تلبي متطلبات الإصدار.

---

**آخر تحديث:** 2025-12-30  
**تم الاختبار مع:** Aspose.OCR 24.11 لـ .NET  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}