---
title: حفظ النتيجة كمستند في التعرف على الصور OCR
linktitle: حفظ النتيجة كمستند في التعرف على الصور OCR
second_title: Aspose.OCR .NET API
description: أطلق العنان لإمكانات Aspose.OCR لـ .NET. يمكنك التعرف بسهولة على النص الموجود في الصور وحفظ النتائج بتنسيقات المستندات المختلفة.
type: docs
weight: 10
url: /ar/net/ocr-settings/save-result-as-document/
---
## مقدمة

مرحبًا بك في عالم التعرف البصري على الأحرف (OCR) المثير باستخدام Aspose.OCR لـ .NET! في هذا البرنامج التعليمي الشامل، سوف نتعمق في تعقيدات استخدام Aspose.OCR للتعرف على النص في الصور وإظهار كيفية حفظ النتائج بتنسيقات مستندات مختلفة.

## المتطلبات الأساسية

قبل الشروع في رحلة التعرف الضوئي على الحروف، تأكد من توفر المتطلبات الأساسية التالية:

-  Aspose.OCR لـ .NET. تأكد من تثبيت مكتبة Aspose.OCR. يمكنك تنزيله[هنا](https://releases.aspose.com/ocr/net/).

-  دليل المستندات: قم بإعداد دليل مخصص لمستنداتك، وقم بتحديث ملف`dataDir` متغير في الكود المقدم وفقًا لذلك.

## استيراد مساحات الأسماء

ابدأ باستيراد مساحات الأسماء الضرورية. هذه هي العناصر الأساسية التي ستمكن التعليمات البرمجية الخاصة بك من خلال إمكانيات التعرف الضوئي على الحروف.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

الآن، دعونا نقسم المثال إلى عدة خطوات:

## الخطوة 1: تهيئة Aspose.OCR

```csharp
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory";

// تهيئة مثيل AsposeOcr
AsposeOcr api = new AsposeOcr();
```

تمهد هذه الخطوة الطريق من خلال تهيئة Aspose.OCR API.

## الخطوة 2: التعرف على الصورة

```csharp
// التعرف على الصورة
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

هنا، نستخدم Aspose.OCR للتعرف على النص داخل الصورة المحددة (استبدل "sample.png" بملف الصورة الخاص بك).

## الخطوة 3: حفظ النتيجة بتنسيقات مختلفة

```csharp
// احفظ النتيجة بالتنسيق المفضل لديك
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

قم بتخصيص هذه الخطوة بناءً على احتياجاتك. يتيح لك Aspose.OCR حفظ النص الذي تم التعرف عليه بتنسيقات المستندات المختلفة مثل DOCX وTXT وPDF وXLSX.

## الخطوة 4: عرض رسالة النجاح

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

رسالة تأكيد بسيطة لإعلامك بأن العملية قد اكتملت دون أي عوائق.

باتباع هذه الخطوات، تكون قد نجحت في استغلال قوة Aspose.OCR لـ .NET في التعرف على النص داخل الصور وحفظ النتائج بتنسيقات مستندات مختلفة.

## خاتمة

في الختام، يفتح Aspose.OCR for .NET عالمًا من الإمكانيات للتعرف على النص في الصور. سواء كنت تستخرج بيانات أو تنشئ مستندات قابلة للبحث، فإن Aspose.OCR يبسط العملية من خلال واجهة برمجة التطبيقات البديهية الخاصة به.

## الأسئلة الشائعة

### س1. هل Aspose.OCR متوافق مع تنسيقات الصور المختلفة؟

ج1: نعم، يدعم Aspose.OCR نطاقًا واسعًا من تنسيقات الصور، مما يضمن المرونة في مهام التعرف الضوئي على الحروف (OCR).

### س2: هل يمكنني تخصيص إعدادات التعرف للحصول على دقة أفضل؟

ج2: بالتأكيد! يوفر Aspose.OCR إعدادات التعرف لضبط عملية التعرف الضوئي على الحروف وفقًا لمتطلباتك المحددة.

### س3: هل هناك نسخة تجريبية مجانية متاحة؟

 ج3: نعم، يمكنك البدء بالتجربة المجانية[هنا](https://releases.aspose.com/).

### س4: كيف يمكنني الحصول على تراخيص مؤقتة لـ Aspose.OCR؟

 ج4: يمكن الحصول على تراخيص مؤقتة[هنا](https://purchase.aspose.com/temporary-license/).

### س5: أين يمكنني طلب المساعدة أو التواصل مع المجتمع؟

 ج5: انضم إلى مجتمع Aspose.OCR على[منتدى أسبوز](https://forum.aspose.com/c/ocr/16) للدعم والمناقشات.