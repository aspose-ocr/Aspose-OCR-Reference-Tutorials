---
title: احصل على مستطيلات للخطوط في التعرف الضوئي على الحروف (OCR).
linktitle: احصل على مستطيلات للخطوط في التعرف الضوئي على الحروف (OCR).
second_title: Aspose.OCR .NET API
description: استكشف Aspose.OCR for .NET، وهو مفتاحك للتعرف الدقيق على صور OCR. أطلق العنان لقوة استخراج النص دون عناء.
weight: 10
url: /ar/net/image-and-drawing-recognition/get-rectangles-for-lines/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# احصل على مستطيلات للخطوط في التعرف الضوئي على الحروف (OCR).

## مقدمة

مرحبًا بك في عالم Aspose.OCR لـ .NET، وهي أداة قوية تتيح لك الاستفادة من إمكانات التعرف الضوئي على الأحرف (OCR) في تطبيقات .NET الخاصة بك. سواء كنت مطورًا متمرسًا أو متحمسًا فضوليًا، سيرشدك هذا الدليل خلال عملية الحصول على مستطيلات للخطوط في التعرف الضوئي على الحروف باستخدام Aspose.OCR.

## المتطلبات الأساسية

قبل الغوص في البرنامج التعليمي، تأكد من توفر المتطلبات الأساسية التالية:

- المعرفة الأساسية بتطوير C# و.NET.
- بيئة تطوير متكاملة (IDE) مثل Visual Studio.
-  تم تثبيت Aspose.OCR لمكتبة .NET. يمكنك تنزيله[هنا](https://releases.aspose.com/ocr/net/).
- صورة نموذجية تحتوي على نص للتعرف الضوئي على الحروف.

## استيراد مساحات الأسماء

تأكد من أن لديك مساحات الأسماء الضرورية المستوردة إلى مشروعك. أضف الأسطر التالية إلى أعلى ملف C# الخاص بك:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

الآن، دعونا نقسم عملية الحصول على مستطيلات للخطوط في التعرف الضوئي على الحروف إلى خطوات سهلة المتابعة.

## الخطوة 1: قم بإعداد دليل المستندات الخاص بك

```csharp
// البداية:3
string dataDir = "Your Document Directory";
// النهاية:3
```

 يستبدل`"Your Document Directory"` بالمسار الفعلي إلى دليل المستندات الخاص بك.

## الخطوة 2: تهيئة Aspose.OCR

```csharp
// البداية:4
AsposeOcr api = new AsposeOcr();
// النهاية:4
```

 إنشاء مثيل لـ`AsposeOcr` فئة للوصول إلى وظيفة التعرف الضوئي على الحروف.

## الخطوة 3: تحديد مسار الصورة

```csharp
// البداية:5
string fullPath = dataDir + "sample.png";
// النهاية:5
```

حدد المسار الكامل للصورة التي تريد إجراء التعرف الضوئي على الحروف عليها.

## الخطوة 4: التعرف على الصورة والحصول على المستطيلات

```csharp
// البداية:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// النهاية:6
```

 الاستفادة من`GetRectangles` طريقة لاسترداد المستطيلات للخطوط في الصورة المحددة.

## الخطوة 5: طباعة النتيجة

```csharp
// البداية:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// النهاية:7
```

طباعة إحداثيات المناطق المكتشفة على لوحة التحكم.

## خاتمة

تهانينا! لقد نجحت في الحصول على مستطيلات للخطوط في التعرف الضوئي على الصور باستخدام Aspose.OCR لـ .NET. تفتح هذه الأداة متعددة الاستخدامات عالمًا من الإمكانيات لاستخراج النص في تطبيقاتك.

## الأسئلة الشائعة

### س1: هل يمكنني استخدام Aspose.OCR لـ .NET مع أي نوع من الصور؟

ج1: يدعم Aspose.OCR نطاقًا واسعًا من تنسيقات الصور، مما يضمن المرونة في تطبيقات التعرف الضوئي على الحروف (OCR).

### س2: ما مدى دقة التعرف الضوئي على الحروف (OCR)؟

ج2: يعمل Aspose.OCR على تعزيز الخوارزميات المتقدمة للحصول على دقة عالية، مما يجعله مناسبًا لمختلف سيناريوهات التعرف على النص.

### س3: هل هناك نسخة تجريبية متاحة؟

 ج3: نعم، يمكنك استكشاف إمكانيات Aspose.OCR لـ .NET باستخدام[تجربة مجانية](https://releases.aspose.com/).

### س4: أين يمكنني العثور على وثائق شاملة؟

 ج4: راجع[توثيق](https://reference.aspose.com/ocr/net/) للحصول على معلومات مفصلة وإرشادات الاستخدام.

### س5: هل تحتاج إلى مساعدة أو لديك أسئلة محددة؟

 ج5: قم بزيارة[منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) لدعم المجتمع والمناقشات.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
