---
title: عملية OCRO مع اختيار اللغة في التعرف على الصور OCR
linktitle: عملية OCRO مع اختيار اللغة في التعرف على الصور OCR
second_title: Aspose.OCR .NET API
description: أطلق العنان لقدرات التعرف الضوئي على الحروف (OCR) القوية باستخدام Aspose.OCR لـ .NET. استخراج النص من الصور بسلاسة.
type: docs
weight: 12
url: /ar/net/ocr-configuration/ocr-operation-with-language-selection/
---
## مقدمة

في عالم التعرف على الصور والتعرف البصري على الأحرف (OCR)، يبرز Aspose.OCR for .NET كأداة قوية للمطورين الذين يبحثون عن استخراج نص دقيق وفعال من الصور. سيرشدك هذا الدليل التفصيلي خطوة بخطوة خلال عملية التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR) باستخدام Aspose.OCR لـ .NET، مع التركيز على العملية مع اختيار اللغة.

## المتطلبات الأساسية

قبل أن نتعمق في البرنامج التعليمي، تأكد من توفر المتطلبات الأساسية التالية:

-  Aspose.OCR لـ .NET: تأكد من تثبيت مكتبة Aspose.OCR. يمكنك تنزيله من[صفحة تنزيل Aspose.OCR لـ .NET](https://releases.aspose.com/ocr/net/).

- بيئة التطوير: قم بإعداد بيئة عمل باستخدام تطبيق .NET. إذا لم تقم بذلك بعد، فارجع إلى[توثيق](https://reference.aspose.com/ocr/net/) للحصول على تعليمات مفصلة.

## استيراد مساحات الأسماء

في تطبيق .NET الخاص بك، ابدأ باستيراد مساحات الأسماء الضرورية:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## الخطوة 1: تهيئة Aspose.OCR

ابدأ بتهيئة مثيل لفئة Aspose.OCR. وهذا يمهد الطريق لاستخدام قدرات التعرف الضوئي على الحروف داخل التطبيق الخاص بك.

```csharp
// البداية:1
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory";

// تهيئة مثيل AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## الخطوة 2: تحديد مسار الصورة

بعد ذلك، حدد المسار إلى الصورة التي تريد إجراء التعرف الضوئي على الحروف عليها. تأكد من إمكانية الوصول إلى الصورة من التطبيق الخاص بك.

```csharp
//مسار الصورة
string fullPath = dataDir + "sample.png";
```

## الخطوة 3: التعرف على الصورة باستخدام اختيار اللغة

الآن تأتي عملية التعرف الضوئي على الحروف الأساسية. استخدم مكتبة Aspose.OCR للتعرف على النص من الصورة المحددة. ضبط إعدادات التعرف، بما في ذلك اختيار اللغة.

```csharp
// التعرف على الصورة
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // اختر اللغة: لا شيء، eng، deu، por، spa، fra، ita، cze، dan، dum، est، fin، lav، lit، nor، pol، rum، srp_hrv، slk، slv، swe، chi
});
```

## الخطوة 4: طباعة النتائج وعرضها

بعد عملية التعرف الضوئي على الحروف، قم بطباعة النتائج وعرضها، بما في ذلك النص الذي تم التعرف عليه والمناطق والتحذيرات وتمثيل JSON.

```csharp
// طباعة النتيجة
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// النهاية:1
```

## خاتمة

تهانينا! لقد نجحت في إجراء التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR) من خلال تحديد اللغة باستخدام Aspose.OCR لـ .NET. أظهر هذا البرنامج التعليمي الخطوات الأساسية لاستخراج النص من الصور وسلط الضوء على مرونة خيارات اللغة.

## الأسئلة الشائعة

### س1: هل Aspose.OCR مناسب للتعرف على النص متعدد اللغات؟

ج1: نعم، يدعم Aspose.OCR العديد من اللغات، مما يوفر المرونة لمهام التعرف الضوئي على الحروف متعددة اللغات.

### س2: هل يمكنني ضبط إعدادات التعرف الضوئي على الحروف لخصائص معينة للصورة؟

ج2: بالتأكيد! اضبط المعلمات مثل زاوية الانحراف والتعرف على الخط واكتشاف المنطقة لتحسين التعرف الضوئي على الحروف لسيناريوهات مختلفة.

### س3: أين يمكنني العثور على دعم إضافي أو مناقشات مجتمعية؟

 ج3: قم بزيارة[منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) للحصول على الدعم والمناقشات مع المجتمع.

### س4: هل هناك نسخة تجريبية مجانية متاحة؟

 ج4: نعم، اكتشف[تجربة مجانية](https://releases.aspose.com/) لتجربة قدرات Aspose.OCR.

### س5: كيف يمكنني شراء Aspose.OCR لـ .NET؟

 ج5: للشراء، قم بزيارة[صفحة الشراء](https://purchase.aspose.com/buy).
