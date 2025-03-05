---
title: قم بإجراء التعرف الضوئي على الحروف (OCR) على الصورة من عنوان URL في التعرف على الصور (OCR).
linktitle: قم بإجراء التعرف الضوئي على الحروف (OCR) على الصورة من عنوان URL في التعرف على الصور (OCR).
second_title: Aspose.OCR .NET API
description: اكتشف تكامل التعرف الضوئي على الحروف (OCR) السلس مع Aspose.OCR لـ .NET. التعرف على النص من الصور بدقة.
type: docs
weight: 10
url: /ar/net/ocr-optimization/perform-ocr-on-image-from-url/
---
## مقدمة

في مجال التعرف البصري على الأحرف (OCR)، يبرز Aspose.OCR for .NET كأداة قوية تمكن المطورين من استخراج محتوى النص من الصور بدقة. إذا كنت تتطلع إلى دمج إمكانات التعرف الضوئي على الحروف (OCR) في تطبيق .NET الخاص بك وإجراء التعرف على النص بسهولة، فسيرشدك هذا الدليل خطوة بخطوة خلال عملية إجراء التعرف الضوئي على الحروف (OCR) على صورة من عنوان URL.

## المتطلبات الأساسية

قبل الخوض في البرنامج التعليمي، تأكد من توفر المتطلبات الأساسية التالية:

-  Aspose.OCR لـ .NET: تأكد من دمج مكتبة Aspose.OCR في مشروع .NET الخاص بك. يمكنك تنزيله من[صفحة الإصدار](https://releases.aspose.com/ocr/net/).

- بيئة التطوير: قم بإعداد بيئة تطوير .NET عاملة على جهازك.

## استيراد مساحات الأسماء

في مشروع .NET الخاص بك، قم بتضمين مساحات الأسماء الضرورية للوصول إلى وظائف Aspose.OCR. أضف مقتطف الكود التالي إلى مشروعك:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## الخطوة 1: قم بإعداد دليل المستندات الخاص بك

 ابدأ بتحديد الدليل الذي تم تخزين مستنداتك فيه. يستبدل`"Your Document Directory"` مع المسار الفعلي إلى المستندات الخاصة بك.

```csharp
string dataDir = "Your Document Directory";
```

## الخطوة 2: احصل على الصورة للتعرف عليها

قم بتوفير عنوان URL للصورة التي تريد إجراء التعرف الضوئي على الحروف عليها. تأكد من أن الصورة متاحة للعامة.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

## الخطوة 3: تهيئة AsposeOcr

قم بإنشاء مثيل لفئة AsposeOcr للوصول إلى وظائف التعرف الضوئي على الحروف.

```csharp
AsposeOcr api = new AsposeOcr();
```

## الخطوة 4: التعرف على الصورة

استخدم مكتبة Aspose.OCR للتعرف على النص من عنوان URL للصورة المحددة. اضبط إعدادات التعرف بناءً على متطلباتك.

```csharp
RecognitionResult result = api.RecognizeImageFromUri(uri, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    RecognitionAreas = new List<Rectangle>()
    {
        new Rectangle(1,3,390,70),
        new Rectangle(1,72,390,70)
    }
});
```

## الخطوة 5: طباعة النتيجة

قم بعرض نتيجة التعرف، بما في ذلك النص والمناطق التي تم التعرف عليها وأي تحذيرات.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

## الخطوة 6: التنفيذ والتحقق

قم بتشغيل التطبيق الخاص بك، وإذا تم إعداد كل شيء بشكل صحيح، فيجب أن ترى عملية التعرف الضوئي على الحروف (OCR) قد تم تنفيذها بنجاح.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## خاتمة

مع Aspose.OCR for .NET، يصبح دمج إمكانات OCR في تطبيقات .NET الخاصة بك تجربة سلسة. يرشدك هذا البرنامج التعليمي خلال عملية إجراء التعرف الضوئي على الحروف على صورة من عنوان URL، مما يوفر لك أساسًا للاستفادة من قوة التعرف على النص في مشاريعك.

## الأسئلة الشائعة

### س1: هل Aspose.OCR مناسب للتعامل مع لغات متعددة؟

ج1: نعم، يدعم Aspose.OCR التعرف على النص بلغات مختلفة، مما يجعله متعدد الاستخدامات للتطبيقات الدولية.

### س٢: هل يمكنني استخدام Aspose.OCR للتعرف على النص أحادي السطر ومتعدد الأسطر؟

ج2: بالتأكيد! يوفر Aspose.OCR المرونة للتعرف على النص أحادي السطر ومتعدد الأسطر، والتكيف مع حالة الاستخدام المحددة الخاصة بك.

### س3: هل هناك أي خيارات ترخيص متاحة لـ Aspose.OCR؟

 ج3: نعم، يمكنك استكشاف خيارات الترخيص وإجراء عمليات الشراء على[متجر أسبوز](https://purchase.aspose.com/buy).

### س4: هل هناك نسخة تجريبية مجانية متاحة لـ Aspose.OCR؟

 ج4: نعم، يمكنك تجربة Aspose.OCR مجانًا من خلال زيارة الموقع[صفحة الإصدارات](https://releases.aspose.com/).

### س5: أين يمكنني العثور على الدعم أو مناقشات المجتمع المتعلقة بـ Aspose.OCR؟

 ج5: قم بزيارة[منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) من أجل الدعم والتفاعل مع المجتمع.