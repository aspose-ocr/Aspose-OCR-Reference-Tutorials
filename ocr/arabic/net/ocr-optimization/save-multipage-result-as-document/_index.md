---
title: حفظ نتيجة الصفحات المتعددة كمستند في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR).
linktitle: حفظ نتيجة الصفحات المتعددة كمستند في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR).
second_title: Aspose.OCR .NET API
description: أطلق العنان لإمكانات Aspose.OCR لـ .NET. احفظ نتائج التعرف الضوئي على الحروف (OCR) متعددة الصفحات بسهولة كمستندات باستخدام هذا الدليل الشامل خطوة بخطوة.
weight: 14
url: /ar/net/ocr-optimization/save-multipage-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حفظ نتيجة الصفحات المتعددة كمستند في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR).

## مقدمة

مرحبًا بك في العالم الرائع للتعرف البصري على الأحرف (OCR) باستخدام Aspose.OCR لـ .NET! في هذا البرنامج التعليمي، سنستكشف كيفية تسخير إمكانات Aspose.OCR لحفظ نتائج التعرف الضوئي على الحروف (OCR) متعددة الصفحات كمستندات. سواء كنت مطورًا متمرسًا أو بدأت للتو في استخدام تقنية التعرف الضوئي على الحروف (OCR)، سيرشدك هذا الدليل خلال كل خطوة، مما يضمن تحقيق أقصى استفادة من هذه الأداة القوية.

## المتطلبات الأساسية

قبل أن نتعمق في البرنامج التعليمي، دعونا نتأكد من إعداد كل شيء:

1.  تثبيت Aspose.OCR لـ .NET: ابدأ بتنزيل Aspose.OCR لـ .NET وتثبيته. يمكنك العثور على الملفات الضرورية[هنا](https://releases.aspose.com/ocr/net/).

2.  احصل على النسخة التجريبية المجانية أو الترخيص: إذا لم تكن قد قمت بذلك بالفعل، فيمكنك الحصول على نسخة تجريبية مجانية[هنا](https://releases.aspose.com/) أو شراء ترخيص[هنا](https://purchase.aspose.com/buy).

3.  استكشاف الوثائق: تعرف على[توثيق](https://reference.aspose.com/ocr/net/)لـ Aspose.OCR لـ .NET. إنه مصدرك المفضل للحصول على معلومات مفصلة.

4.  الوصول إلى منتديات الدعم: إذا واجهت أية مشكلات أو كانت لديك أسئلة، فإن[منتديات الدعم](https://forum.aspose.com/c/ocr/16) هي مورد مجتمعي قيم.

الآن بعد أن انتهيت من كل شيء، دعنا ننتقل إلى الدليل خطوة بخطوة.

## استيراد مساحات الأسماء

ابدأ مشروعك عن طريق استيراد مساحات الأسماء الضرورية:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

## الخطوة 1: قم بتعيين دليل المستندات الخاص بك

```csharp
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory";
```

 تأكد من الاستبدال`"Your Document Directory"` بالمسار الفعلي إلى دليل المستندات الخاص بك.

## الخطوة 2: تهيئة Aspose.OCR

```csharp
// تهيئة مثيل AsposeOcr
AsposeOcr api = new AsposeOcr();
```

 إنشاء مثيل ل`AsposeOcr` للوصول إلى وظائف التعرف الضوئي على الحروف.

## الخطوة 3: التعرف على الصور

```csharp
// التعرف على الصورة
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

استخدم Aspose.OCR للتعرف على النص من صور متعددة. اضبط مسارات الملفات وفقًا لملفات الصور الخاصة بك.

## الخطوة 4: حفظ النتائج بالتنسيقات المفضلة

```csharp
// احفظ النتيجة بالتنسيق المفضل لديك
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

اختر التنسيق الذي تريده (Docx أو Text أو Pdf أو Xlsx) واحفظ نتائج التعرف الضوئي على الحروف كمستند متعدد الصفحات.

## خاتمة

تهانينا! لقد تعلمت بنجاح كيفية حفظ نتائج التعرف الضوئي على الحروف (OCR) متعددة الصفحات كمستندات باستخدام Aspose.OCR لـ .NET. تفتح هذه الأداة متعددة الاستخدامات عالمًا من الإمكانيات للتعرف على النص في مشاريعك.

## الأسئلة الشائعة

### س1: هل الترخيص المؤقت متاح لأغراض الاختبار؟

 ج1: نعم، يمكنك الحصول على ترخيص مؤقت[هنا](https://purchase.aspose.com/temporary-license/) لاختبار Aspose.OCR.

### س2: هل يمكنني التعرف على النص من الصور بتنسيقات مختلفة؟

ج2: بالتأكيد! يدعم Aspose.OCR تنسيقات الصور المختلفة، مما يضمن المرونة في مهام التعرف الضوئي على الحروف (OCR).

### س3: هل هناك أي قيود على عدد الصور للتعرف عليها؟

ج3: يعتمد عدد الصور التي يمكنك معالجتها على الترخيص الخاص بك. تحقق من الوثائق للحصول على التفاصيل.

### س 4: كيف يمكنني معالجة الأخطاء أثناء التعرف على الحروف (OCR)؟

ج4: راجع الوثائق للتعرف على أفضل ممارسات معالجة الأخطاء أو اطلب المساعدة في منتديات الدعم.

### س5: هل يدعم Aspose.OCR لغات أخرى غير الإنجليزية؟

ج5: نعم، يدعم Aspose.OCR لغات متعددة. استكشف الوثائق للحصول على تفاصيل دعم اللغة.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
