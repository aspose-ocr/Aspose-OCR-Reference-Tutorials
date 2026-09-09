---
date: 2026-04-29
description: تعلم كيفية تحويل الصور إلى PDF باستخدام C# و Aspose.OCR، حفظ نتائج OCR
  متعددة الصفحات كوثائق، واستخراج النص من الصور باستخدام C#.
keywords:
- convert images to pdf
- extract text from images
- c# ocr library
- convert images to xlsx
- generate pdf from tiff
linktitle: تحويل الصور إلى PDF C# – حفظ نتيجة OCR متعددة الصفحات
second_title: Aspose.OCR .NET API
title: تحويل الصور إلى PDF باستخدام C# – حفظ نتيجة OCR متعددة الصفحات
url: /ar/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصور إلى PDF C# – حفظ نتيجة OCR متعددة الصفحات

## مقدمة

في هذا الدرس ستكتشف كيفية **تحويل الصور إلى PDF C#** باستخدام مكتبة **Aspose.OCR** القوية لـ .NET. سواء كنت بحاجة إلى **تحويل ملفات TIFF الممسوحة ضوئياً إلى ملفات PDF قابلة للبحث**، أو استخراج النص من الصور لتعدين البيانات، أو إنشاء مصنف Excel من مجموعة من الصور، فإن هذا الدليل يمرّ بك عبر كل خطوة مع شروحات واضحة، ونصائح عملية، وتوصيات لأفضل الممارسات.

## إجابات سريعة
- **ما الذي يغطيه هذا الدرس؟** تحويل صور متعددة إلى PDF، Docx، Text، و Xlsx باستخدام Aspose.OCR في C# وحفظ نتيجة OCR كمستند متعدد الصفحات.  
- **ما صيغ الإخراج المدعومة؟** Docx، Text، Pdf، و Xlsx (يمكنك أيضاً إخراج PDF مباشرة).  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تكفي للتقييم؛ الترخيص الدائم مطلوب للإنتاج.  
- **ما إصدارات .NET المتوافقة؟** .NET Framework 4.5+، .NET Core 3.1+، .NET 5/6/7.  
- **هل يمكن استخراج النص أثناء التحويل؟** نعم—استخدم نتائج OCR لاستخراج نص قابل للبحث قبل الحفظ.

## ما هو “convert images to PDF C#”؟

تحويل الصور إلى PDF في C# يعني أخذ ملف أو أكثر من ملفات البت ماب (PNG، JPEG، TIFF، إلخ) برمجياً وإنشاء مستند PDF يحافظ على التخطيط البصري مع إمكانية تضمين نص قابل للبحث عبر OCR. توفر Aspose.OCR **c# ocr library** التي تتعامل مع هذه العملية من البداية إلى النهاية، بما في ذلك دعم الصفحات المتعددة والحفظ المباشر إلى صيغ مكتبية شائعة.

## لماذا نستخدم Aspose.OCR لهذه المهمة؟

- **OCR عالي الدقة** يدعم عشرات اللغات.  
- **معالجة متعددة الصفحات** – قم بتمرير مجلد كامل من الصور واحصل على PDF واحد قابل للبحث.  
- **تصدير مباشر** إلى Docx، Text، Pdf، و Xlsx دون الحاجة إلى خطوة تحويل ثانية.  
- **نقي .NET** – لا يعتمد على مكتبات أصلية، يعمل على Windows، Linux، وبيئات السحابة.

## المتطلبات المسبقة

1. قم بتثبيت Aspose.OCR لـ .NET. يمكنك تنزيله [هنا](https://releases.aspose.com/ocr/net/).  
2. احصل على نسخة تجريبية مجانية أو ترخيص مدفوع – احصل على التجربة [هنا](https://releases.aspose.com/) أو اشترِ واحدة [هنا](https://purchase.aspose.com/buy).  
3. راجع الـ [documentation](https://reference.aspose.com/ocr/net/) الرسمي لتتعرف على واجهة البرمجة (API).  
4. انضم إلى المجتمع عبر [support forums](https://forum.aspose.com/c/ocr/16) للحصول على المساعدة في أي عقبة.

الآن بعد أن أصبح كل شيء جاهزاً، لنبدأ بالبرمجة.

## استيراد المساحات الاسمية

ابدأ بإضافة المساحات الاسمية المطلوبة إلى ملف C# الخاص بك:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

هذه الاستيرادات تمنحك الوصول إلى المجموعات، التعامل مع الملفات، LINQ، وفئات Aspose OCR.

## الخطوة 1: تعيين دليل المستندات الخاص بك

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

استبدل `"Your Document Directory"` بالمسار المطلق أو النسبي حيث توجد الصور المصدرية وأين تريد حفظ ملفات الإخراج.

## الخطوة 2: تهيئة Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

إنشاء كائن `AsposeOcr` يمنحك إمكانية الوصول إلى جميع عمليات OCR، بما في ذلك سير عمل **convert images to PDF C#**.

## الخطوة 3: التعرف على الصور

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

طريقة `RecognizeMultipleImages` تعالج كل ملف في القائمة وتعيد مجموعة من `RecognitionResult`. يمكنك تمرير أي عدد من الصور، وهو مثالي لسيناريوهات **convert scanned images to PDF**.

## الخطوة 4: حفظ النتائج بالصيغ المفضلة

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

اختر الصيغة التي تناسب سير عملك:

- **Docx** – مستند Word قابل للتحرير مع نص قابل للبحث.  
- **Text** – استخراج نص عادي لتعدين البيانات السريع (**extract text from images**).  
- **Pdf** – إخراج PDF الكلاسيكي، مثالي للأرشفة.  
- **Xlsx** – تمثيل جدول بيانات للبيانات الجدولية (**convert images to xlsx**).

## كيفية تحويل الصور إلى PDF C# – ملخص خطوة بخطوة

1. **جهّز المجلد** الذي يحتوي على الصور التي تريد تحويلها.  
2. **أنشئ كائن `AsposeOcr`** للوصول إلى وظائف OCR.  
3. **استدعِ `RecognizeMultipleImages`** للحصول على نتائج OCR لكل ملف.  
4. **احفظ النتيجة متعددة الصفحات** باستخدام `SaveMultipageDocument` بالصيغ التي تحتاجها.

## حالات الاستخدام الشائعة

- **الأرشفة الرقمية:** تحويل العقود الورقية الممسوحة إلى ملفات PDF قابلة للبحث.  
- **أتمتة إدخال البيانات:** استخراج النص من الإيصالات أو الفواتير وإدخاله في قاعدة بيانات.  
- **المعالجة الدفعة:** التعامل مع آلاف الصور في مهمة واحدة مع أقل قدر من الشيفرة.  
- **إنشاء PDF من TIFF:** مثالي للمستندات الممسوحة عالية الدقة التي تحتاج إلى الحفاظ على الدقة الأصلية.

## استكشاف الأخطاء وإصلاحها & نصائح

- **مجموعات الصور الكبيرة:** عالج الصور على دفعات أصغر لتجنب ارتفاع استهلاك الذاكرة.  
- **جودة الصورة:** تأكد من أن الصور لا تقل عن 300 dpi للحصول على أفضل دقة OCR.  
- **أخطاء الترخيص:** تحقق من تحميل ملف الترخيص بشكل صحيح قبل استدعاء طرق OCR.  
- **نتائج فارغة:** إذا تعذر قراءة صورة ما، سيحتوي `RecognitionResult` المقابل على خاصية `Text` فارغة—تحقق من القيم null أو السلاسل الفارغة قبل الحفظ.  

## الأسئلة المتكررة

**س: هل يمكنني تحويل الصور إلى PDF C# دون استخدام OCR؟**  
ج: نعم، يمكنك استخدام Aspose.PDF أو مكتبات أخرى للتحويل الصرف من صورة إلى PDF، لكن OCR يضيف نصًا قابلاً للبحث يجعل الـ PDF أكثر فائدة.

**س: كيف يمكنني استخراج النص من الصور C# بعد التحويل؟**  
ج: قائمة `result` التي تُرجعها `RecognizeMultipleImages` تحتوي على خاصية `Text` لكل صفحة. يمكنك كتابة هذه السلاسل إلى ملف `.txt` أو معالجتها مباشرة في تطبيقك.

**س: هل يمكن ضبط هوامش الصفحة أو الاتجاه؟**  
ج: عند الحفظ إلى PDF أو Docx، يمكنك تعديل تخطيط المستند عبر واجهات Aspose.Words أو Aspose.PDF قبل استدعاء `SaveMultipageDocument`.

**س: ماذا يحدث إذا تعذر قراءة صورة ما؟**  
ج: محرك OCR يُرجع `RecognitionResult` فارغ لتلك الصفحة؛ يمكنك اكتشاف ذلك وتخطي الملف أو تسجيله كخطأ.

**س: هل تدعم الواجهة البرمجية النشر على السحابة؟**  
ج: نعم، تعمل المكتبة على أي بيئة تشغيل .NET، بما في ذلك Azure Functions و AWS Lambda، طالما أن البيئة تلبي متطلبات الإصدار.

## الخاتمة

أصبح لديك الآن سير عمل كامل وجاهز للإنتاج **لتحويل الصور إلى PDF C#**، استخراج النص القابل للبحث، وحتى إنشاء ملفات Word، نص عادي، أو Excel من دفعة من الصور. لا تتردد في تجربة صيغ إخراج مختلفة، ضبط إعدادات OCR للغات معينة، أو دمج الشيفرة في خطوط معالجة مستندات أكبر.

---

**Last Updated:** 2026-04-29  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}