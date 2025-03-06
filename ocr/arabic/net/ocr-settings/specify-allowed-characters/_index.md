---
title: حدد الأحرف المسموح بها في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR).
linktitle: حدد الأحرف المسموح بها في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR).
second_title: Aspose.OCR .NET API
description: افتح تقنية التعرف الضوئي على الحروف (OCR) بدقة في .NET باستخدام Aspose.OCR. التعرف على النص من الصور دون عناء. قم بالتنزيل الآن للحصول على تجربة تطوير تحويلية.
weight: 13
url: /ar/net/ocr-settings/specify-allowed-characters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حدد الأحرف المسموح بها في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR).

## مقدمة

في مشهد التكنولوجيا المتطور باستمرار، برز التعرف الضوئي على الحروف (OCR) كأداة تحويلية، تمكن الآلات من فهم النص من الصور. يبرز Aspose.OCR for .NET كحل قوي، حيث يوفر تكاملًا سلسًا للمطورين الذين يبحثون عن إمكانات OCR قوية في تطبيقات .NET الخاصة بهم.

## المتطلبات الأساسية

قبل الغوص في البرنامج التعليمي، تأكد من توفر المتطلبات الأساسية التالية:

- معرفة عملية بتطوير .NET.
-  Aspose.OCR لمكتبة .NET. يمكنك تنزيله[هنا](https://releases.aspose.com/ocr/net/).
- الإلمام بـ Visual Studio أو أي بيئة تطوير NET مفضلة أخرى.

## استيراد مساحات الأسماء

في مشروع .NET الخاص بك، قم باستيراد مساحات الأسماء الضرورية للاستفادة من وظائف Aspose.OCR لـ .NET بشكل فعال:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

الآن، دعونا نقسم البرنامج التعليمي إلى سلسلة من الخطوات الشاملة:

## الخطوة 1: تحديد الأحرف المسموح بها في التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR).

للبدء، قم بإعداد المسار إلى دليل المستندات الخاص بك:

```csharp
string dataDir = "Your Document Directory";
```

## الخطوة 2: تهيئة Aspose.OCR بالرموز المسموح بها

قم بإنشاء مثيل AsposeOcr، مع تحديد الرموز المسموح بها. في هذه الحالة، نسمح بالأرقام (0-9):

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## الخطوة 3: التعرف على الصورة

استخدم مثيل AsposeOcr للتعرف على النص من الصورة:

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## الخطوة 4: عرض النص الذي تم التعرف عليه

اطبع النص الذي تم التعرف عليه على وحدة التحكم:

```csharp
Console.WriteLine(result);
```

## الخطوة 5: الحالة الثانية - التعرف على الصورة باستخدام إعدادات محددة

قم بتهيئة مثيل AsposeOcr آخر، هذه المرة بإعدادات أكثر تحديدًا:

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## الخطوة 6: عرض النص الذي تم التعرف على الحالة الثانية

اطبع النص الذي تم التعرف عليه من الحالة الثانية إلى وحدة التحكم:

```csharp
Console.WriteLine(result2.RecognitionText);
```

## الخطوة 7: التنفيذ الناجح

وأخيرًا، أكد التنفيذ الناجح للبرنامج التعليمي SpecifyAllowedCharacters:

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

باتباع هذه الخطوات، قمت بإلغاء تأمين القدرة على تحديد الأحرف المسموح بها في التعرف على الصور بتقنية OCR باستخدام Aspose.OCR لـ .NET.

## خاتمة

يعمل Aspose.OCR for .NET على تمكين المطورين من دمج إمكانات التعرف الضوئي على الحروف في تطبيقاتهم بسلاسة، مما يفتح الأبواب أمام حلول مبتكرة في مجالات مختلفة. احتضن قوة التعرف الضوئي على الحروف (OCR) وعزز مشروعاتك من خلال التعرف الدقيق على النص.

## الأسئلة الشائعة

### س1: هل Aspose.OCR for .NET مناسب لكل من المطورين المبتدئين وذوي الخبرة؟

ج1: بالتأكيد! يلبي Aspose.OCR for .NET احتياجات المطورين من جميع مستويات المهارات، ويوفر وظائف بديهية للتكامل السلس.

### س2: هل يمكنني استخدام Aspose.OCR لـ .NET للتعرف على الأحرف بلغات متعددة؟

ج2: نعم، يدعم Aspose.OCR التعرف على اللغات المختلفة، مما يجعله متعدد الاستخدامات لتطبيقات متنوعة.

### س 3: كم مرة يتم تحديث Aspose.OCR لـ .NET؟

 ج3: يتم إصدار التحديثات بانتظام لضمان التوافق مع أحدث التقنيات ومعالجة أية مشكلات محتملة. افحص ال[توثيق](https://reference.aspose.com/ocr/net/) للحصول على أحدث المعلومات.

### س4: هل تتوفر نسخة تجريبية مجانية من Aspose.OCR لـ .NET؟

 ج4: نعم، يمكنك استكشاف إمكانيات Aspose.OCR عن طريق تنزيل ملف[تجربة مجانية](https://releases.aspose.com/).

### س5: أين يمكنني طلب المساعدة أو التواصل مع المجتمع للحصول على الدعم؟

 ج5: قم بزيارة[منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) للتواصل مع المجتمع والحصول على مساعدة الخبراء.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
