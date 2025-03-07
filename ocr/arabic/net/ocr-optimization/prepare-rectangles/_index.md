---
title: تحضير المستطيلات في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR).
linktitle: تحضير المستطيلات في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR).
second_title: Aspose.OCR .NET API
description: أطلق العنان لإمكانات Aspose.OCR لـ .NET من خلال دليلنا الشامل. تعلم خطوة بخطوة كيفية تحضير المستطيلات للتعرف على الصور. ارفع مستوى تطبيقات .NET الخاصة بك من خلال تكامل التعرف الضوئي على الحروف (OCR) بسلاسة.
weight: 11
url: /ar/net/ocr-optimization/prepare-rectangles/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحضير المستطيلات في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR).

## مقدمة

في عالم التكنولوجيا المتطور باستمرار، يلعب التعرف الضوئي على الحروف (OCR) دورًا محوريًا في تحويل الصور إلى نص يمكن قراءته آليًا. يبرز Aspose.OCR for .NET كحل قوي للمطورين الذين يسعون إلى التكامل السلس لإمكانيات التعرف الضوئي على الحروف في تطبيقات .NET الخاصة بهم. في هذا الدليل الشامل، سنستكشف عملية إعداد المستطيلات في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR) باستخدام Aspose.OCR for .NET.

## المتطلبات الأساسية

قبل الغوص في البرنامج التعليمي، تأكد من توفر المتطلبات الأساسية التالية:

- معرفة عملية بتطوير .NET.
-  تم تثبيت Aspose.OCR لمكتبة .NET. يمكنك تنزيله[هنا](https://releases.aspose.com/ocr/net/).
- فهم أساسي لمفاهيم التعرف على الصور.

## استيراد مساحات الأسماء

لنبدأ باستيراد مساحات الأسماء الضرورية لبدء رحلة التعرف الضوئي على الحروف:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## الخطوة 1: قم بإعداد دليل المستندات الخاص بك

 ابدأ بتحديد الدليل الذي تم تخزين مستنداتك فيه. يستبدل`"Your Document Directory"` مع المسار الفعلي إلى المستندات الخاصة بك.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory";

// تهيئة مثيل AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## الخطوة 2: التعرف على الصورة ذات المستطيلات المتعددة

في هذه الخطوة، سنوضح كيفية التعرف على النص من الصورة باستخدام مستطيلات متعددة. اتبع هذه الخطوات الفرعية:

### 2.1 تحديد المستطيلات

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 2.2 إجراء التعرف الضوئي على الحروف

```csharp
// الحالة الأولى
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// عرض النص الذي تم التعرف عليه
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## الخطوة 3: التعرف على الصورة باستخدام إعدادات التعرف

في هذه الخطوة، سنعرض طريقة بديلة باستخدام إعدادات التعرف للتعرف على الصور:

### 3.1 تحديد إعدادات التعرف

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 3.2 عرض النص الذي تم التعرف عليه

```csharp
// عرض النص الذي تم التعرف عليه
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## خاتمة

تهانينا! لقد نجحت في اجتياز عملية إعداد المستطيلات في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR) باستخدام Aspose.OCR لـ .NET. يمكّنك هذا الدليل من دمج تقنية التعرف الضوئي على الحروف (OCR) بسلاسة في تطبيقات .NET الخاصة بك، مما يعزز قدرات التعرف على النص الخاصة بها.

### الأسئلة الشائعة

### س١: هل يمكنني استخدام Aspose.OCR لـ .NET مع أطر عمل .NET الأخرى؟

A1: نعم، Aspose.OCR لـ .NET متوافق مع أطر عمل .NET المختلفة.

### س2: هل تتوفر نسخة تجريبية مجانية من Aspose.OCR لـ .NET؟

 ج2: بالتأكيد! يمكنك الوصول إلى النسخة التجريبية المجانية[هنا](https://releases.aspose.com/).

### س٣: كيف يمكنني الحصول على دعم Aspose.OCR لـ .NET؟

 ج3: قم بزيارة[منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) للحصول على الدعم المخصص.

### س4: هل يمكنني الحصول على ترخيص مؤقت لأغراض الاختبار؟

 ج4: نعم، يمكنك الحصول على ترخيص مؤقت[هنا](https://purchase.aspose.com/temporary-license/).

### س5: أين يمكنني العثور على الوثائق الخاصة بـ Aspose.OCR لـ .NET؟

 ج5: الوثائق متاحة[هنا](https://reference.aspose.com/ocr/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
