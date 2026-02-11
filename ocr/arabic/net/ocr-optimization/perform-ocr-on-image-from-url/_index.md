---
date: 2025-12-22
description: تعلم كيفية التعرف على النص من الصورة باستخدام Aspose.OCR لـ .NET، وتحويل
  الصورة إلى نص باستخدام إعدادات التعرف الضوئي على الحروف الدقيقة.
linktitle: recognize text from image – Perform OCR on Image from URL
second_title: Aspose.OCR .NET API
title: التعرف على النص من الصورة – إجراء OCR على صورة من عنوان URL
url: /ar/net/ocr-optimization/perform-ocr-on-image-from-url/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على صورة من URL في التعرف على الصور باستخدام OCR

## المقدمة

في مجال التعرف الضوئي على الحروف (OCR)، يتيح لك Aspose.OCR for .NET **recognize text from image** بدقة، مما يمكّن المطورين من استخراج المحتوى من الصور بسهولة. إذا كنت ترغب في دمج قدرات OCR في تطبيق .NET الخاص بك وإجراء التعرف على النص من مصدر بعيد، سيوضح لك هذا الدليل خطوة بخطوة عملية تنفيذ OCR على صورة من URL.

## إجابات سريعة
- **ما الذي يغطيه هذا الدرس؟** التعرف على النص من صورة موجودة على URL عام باستخدام Aspose.OCR for .NET.  
- **ما هي الكلمة المفتاحية الأساسية المستهدفة؟** *recognize text from image*  
- **هل أحتاج إلى ترخيص؟** يتوفر إصدار تجريبي، لكن الترخيص التجاري مطلوب للاستخدام في الإنتاج.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **كم من الوقت تستغرق عملية التنفيذ؟** عادةً أقل من 10 دقيقة للإعداد الأساسي.

## ما هو “recognize text from image”؟
يعني التعرف على النص من صورة تحويل التمثيل البصري للأحرف إلى نص قابل للتحرير والبحث. غالبًا ما يُشار إلى هذه العملية باسم **convert image to text** أو **extract text from image**، وتُستخدم في سيناريوهات مثل رقمنة المستندات، أتمتة إدخال البيانات، وتحسين إمكانية الوصول.

## لماذا تستخدم Aspose.OCR for .NET؟
- **دقة عالية** مع دعم مدمج للغات.  
- **إعدادات OCR دقيقة** (مثل auto‑skew، اكتشاف المنطقة).  
- **API بسيط** يعمل مع كل من .NET Framework و .NET Core.  
- **بدون تبعيات خارجية** – كل شيء يعمل محليًا.

## المتطلبات المسبقة

قبل الخوض في الدرس، تأكد من توفر المتطلبات التالية:

- Aspose.OCR for .NET: تأكد من دمج مكتبة Aspose.OCR في مشروع .NET الخاص بك. يمكنك تنزيلها من [صفحة الإصدار](https://releases.aspose.com/ocr/net/).

- بيئة التطوير: احرص على وجود بيئة تطوير .NET تعمل على جهازك.

## استيراد مساحات الأسماء

في مشروع .NET الخاص بك، أضف مساحات الأسماء اللازمة للوصول إلى وظائف Aspose.OCR. أدرج الشيفرة التالية في مشروعك:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## كيفية التعرف على النص من صورة باستخدام URL؟

### الخطوة 1: إعداد دليل المستندات الخاص بك

ابدأ بتحديد الدليل الذي تُخزن فيه مستنداتك. استبدل `"Your Document Directory"` بالمسار الفعلي لمستنداتك.

```csharp
string dataDir = "Your Document Directory";
```

### الخطوة 2: الحصول على الصورة للتعرف

قدّم URL الصورة التي تريد إجراء OCR عليها. تأكد من أن الصورة متاحة للجمهور.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

### الخطوة 3: تهيئة AsposeOcr

أنشئ كائنًا من فئة AsposeOcr للوصول إلى وظائف OCR.

```csharp
AsposeOcr api = new AsposeOcr();
```

### الخطوة 4: التعرف على الصورة

استخدم مكتبة Aspose.OCR للتعرف على النص من URL الصورة المحدد. اضبط إعدادات التعرف وفقًا لمتطلباتك.

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

### الخطوة 5: طباعة النتيجة

اعرض نتيجة التعرف، بما في ذلك النص المستخرج، المناطق، وأية تحذيرات.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

### الخطوة 6: التنفيذ والتحقق

شغّل تطبيقك، وإذا تم الإعداد بشكل صحيح، سترى عملية OCR تُنفّذ بنجاح.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## المشكلات الشائعة والحلول

- **الصورة غير متاحة للجمهور** – تحقق من عمل URL في المتصفح. إذا كانت الصورة تتطلب مصادقة، قم بتنزيلها أولاً واستخدم `RecognizeImageFromStream`.  
- **مناطق التعرف غير صحيحة** – اضبط قيم `Rectangle` أو عيّن `DetectAreas = false` للسماح للمحرك بالكشف التلقائي.  
- **اللغة غير معروفة** – تأكد من تثبيت حزمة اللغة المناسبة أو عيّن `Language = "eng"` (أو أي رمز ISO آخر) في `RecognitionSettings`.

## الأسئلة المتكررة

### س1: هل Aspose.OCR مناسب للتعامل مع لغات متعددة؟
ج1: نعم، يدعم Aspose.OCR التعرف على النص بعدة لغات، مما يجعله مرنًا للتطبيقات الدولية.

### س2: هل يمكنني استخدام Aspose.OCR لكل من التعرف على النص أحادي السطر ومتعدد الأسطر؟
ج2: بالتأكيد! يوفر Aspose.OCR مرونة للتعرف على النص أحادي السطر ومتعدد الأسطر، وفقًا لحالتك الخاصة.

### س3: هل هناك خيارات ترخيص متاحة لـ Aspose.OCR؟
ج3: نعم، يمكنك استكشاف خيارات الترخيص والشراء من [متجر Aspose](https://purchase.aspose.com/buy).

### س4: هل يتوفر تجربة مجانية لـ Aspose.OCR؟
ج4: نعم، يمكنك تجربة Aspose.OCR مجانًا بزيارة [صفحة الإصدارات](https://releases.aspose.com/).

### س5: أين يمكنني العثور على الدعم أو مناقشات المجتمع المتعلقة بـ Aspose.OCR؟
ج5: زر [منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) للحصول على الدعم والتفاعل مع المجتمع.

## الخاتمة

مع Aspose.OCR for .NET، يصبح دمج قدرات OCR في تطبيقات .NET تجربة سلسة. لقد أرشدك هذا الدرس إلى عملية **recognize text from image** باستخدام URL، موفرًا أساسًا قويًا لاستغلال استخراج النص في مشاريعك.

---

**Last Updated:** 2025-12-22  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}