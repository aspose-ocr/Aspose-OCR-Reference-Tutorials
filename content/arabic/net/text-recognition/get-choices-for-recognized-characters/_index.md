---
title: احصل على خيارات للأحرف التي تم التعرف عليها في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR).
linktitle: احصل على خيارات للأحرف التي تم التعرف عليها في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR).
second_title: Aspose.OCR .NET API
description: قم بتحسين تطبيقات .NET الخاصة بك باستخدام Aspose.OCR للتعرف الدقيق على الأحرف. اتبع دليلنا خطوة بخطوة لاسترداد اختيارات الأحرف التي تم التعرف عليها في التعرف على الصور.
type: docs
weight: 10
url: /ar/net/text-recognition/get-choices-for-recognized-characters/
---
## مقدمة

يعد إطلاق العنان لقوة التعرف الضوئي على الأحرف (OCR) أمرًا بالغ الأهمية في العصر الرقمي الحالي، ويبرز Aspose.OCR for .NET كحل قوي للتعرف الدقيق على الأحرف. في هذا البرنامج التعليمي، سوف نتعمق في ميزة محددة: الحصول على اختيارات للشخصيات التي تم التعرف عليها. وبنهاية هذا الدليل، ستتمكن من دمج هذه الوظيفة بسلاسة في تطبيقات .NET الخاصة بك.

## المتطلبات الأساسية

قبل الغوص في البرنامج التعليمي، تأكد من أن لديك المتطلبات الأساسية التالية:

- المعرفة الأساسية بتطوير C# و.NET.
- تم تثبيت Visual Studio على جهازك.
-  Aspose.OCR لمكتبة .NET، والتي يمكنك تنزيلها[هنا](https://releases.aspose.com/ocr/net/).

## استيراد مساحات الأسماء

في مشروع C# الخاص بك، ابدأ باستيراد مساحات الأسماء الضرورية:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## الخطوة 1: تهيئة Aspose.OCR

ابدأ بتهيئة مثيل Aspose.OCR:

```csharp
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory";

// تهيئة مثيل AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## الخطوة 2: تحديد مسار الصورة

قم بتعيين المسار للصورة التي تريد تحليلها:

```csharp
//مسار الصورة
string fullPath = dataDir + "sample.png";
```

## الخطوة 3: التعرف على الصورة

تنفيذ عملية التعرف على الصور:

```csharp
// التعرف على الصورة
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    // الإعدادات الافتراضية أو المخصصة
});
```

## الخطوة 4: احصل على خيارات الشخصيات المعترف بها

استرداد الاختيارات للأحرف التي تم التعرف عليها:

```csharp
List<char[]> resultWithChoices = result.RecognitionCharactersList;
```

## الخطوة 5: طباعة النتائج

عرض نص التعرف والاختيارات:

```csharp
// طباعة النتيجة
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Choices:");
resultWithChoices.ForEach(a => Console.WriteLine($"character: {a[0]} . Choices: {a[1]} {a[2]} {a[3]} {a[4]}"));

Console.WriteLine("GetChoiceForRecognizedCharacters executed successfully");
```

كرر هذه الخطوات، وقم بتخصيصها وفقًا لمتطلبات التطبيق الخاص بك.

## خاتمة

في هذا البرنامج التعليمي، اكتشفنا كيفية الاستفادة من Aspose.OCR لـ .NET للحصول على خيارات للأحرف المعترف بها في التعرف على الصور. تضيف هذه الميزة بُعدًا جديدًا لقدرات التعرف الضوئي على الحروف لديك، مما يعزز تنوع تطبيقاتك.

## الأسئلة الشائعة

### س١: هل Aspose.OCR for .NET مناسب لمعالجة المستندات على نطاق واسع؟

ج1: بالتأكيد! تم تصميم Aspose.OCR for .NET للتعامل مع كميات كبيرة من المستندات بكفاءة ودقة.

### س2: هل يمكنني استخدام Aspose.OCR لـ .NET في تطبيق ويب؟

ج2: نعم، يمكنك دمج Aspose.OCR لـ .NET في تطبيقات الويب، مما يجعله متعدد الاستخدامات لسيناريوهات التطوير المختلفة.

### س3: هل هناك أي خيارات ترخيص متاحة لـ Aspose.OCR لـ .NET؟

 ج3: نعم، يمكنك استكشاف خيارات الترخيص وإجراء عملية شراء[هنا](https://purchase.aspose.com/buy).

### س4: كيف يمكنني الحصول على الدعم أو طرح أسئلة حول Aspose.OCR لـ .NET؟

 ج4: قم بزيارة[منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) للحصول على الدعم وطرح الأسئلة والتواصل مع المجتمع.

### س5: هل تتوفر نسخة تجريبية مجانية من Aspose.OCR لـ .NET؟

 ج5: نعم، يمكنك الوصول إلى النسخة التجريبية المجانية[هنا](https://releases.aspose.com/) لتجربة إمكانيات Aspose.OCR لـ .NET.