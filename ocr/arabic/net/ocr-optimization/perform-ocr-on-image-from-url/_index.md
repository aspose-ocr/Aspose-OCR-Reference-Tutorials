---
date: 2026-02-25
description: تعلم كيفية تحويل الصورة إلى نص باستخدام Aspose.OCR لـ .NET، واستخراج
  النص من الصورة بإعدادات التعرف الضوئي على الأحرف الدقيقة.
linktitle: convert image to text – Perform OCR on Image from URL
second_title: Aspose.OCR .NET API
title: تحويل الصورة إلى نص – إجراء التعرف الضوئي على الحروف (OCR) على صورة من عنوان
  URL
url: /ar/net/ocr-optimization/perform-ocr-on-image-from-url/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى نص – تنفيذ OCR على الصورة من URL

## المقدمة

إذا كنت بحاجة إلى **تحويل الصورة إلى نص** في تطبيق .NET، فإن Aspose.OCR for .NET يوفّر لك طريقة موثوقة لاستخراج النص من الصور المستضافة في أي مكان على الويب. في هذا الدرس ستتعلم كيفية التعرف على النص من صورة موجودة على URL عام، وتكوين إعدادات التعرف على OCR، ومعالجة النتيجة—كل ذلك في بضع دقائق فقط.

## إجابات سريعة
- **ما الذي يغطيه هذا الدرس؟** تحويل الصورة إلى نص من URL عام باستخدام Aspose.OCR for .NET.  
- **ما هي الكلمة المفتاحية الأساسية المستهدفة؟** *convert image to text*  
- **هل أحتاج إلى ترخيص؟** يتوفر نسخة تجريبية، لكن الترخيص التجاري مطلوب للاستخدام في الإنتاج.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+، .NET Core 3.1+، .NET 5/6+.  
- **كم يستغرق التنفيذ؟** عادةً أقل من 10 دقائق لإعداد أساسي.

## ما هو “تحويل الصورة إلى نص”؟
تحويل الصورة إلى نص يعني تحويل التمثيل البصري للأحرف إلى سلاسل قابلة للتحرير والبحث. هذه العملية—المعروفة أيضًا بـ **extract text from image**—تدعم رقمنة المستندات، وأتمتة إدخال البيانات، وحلول الوصول.

## لماذا نستخدم Aspose.OCR for .NET لتحويل الصورة إلى نص؟
- **دقة عالية** مع دعم مدمج للغات وإضافات **OCR language pack** اختيارية.  
- **إعدادات التعرف على OCR دقيقة** مثل تصحيح الانحراف التلقائي، اكتشاف المناطق، ومعالجة النص متعدد الأسطر.  
- **API بسيطة** تعمل مع كل من .NET Framework و .NET Core دون تبعيات خارجية.  
- **دعم مباشر للـ URL** – يمكنك **recognize text from URL** دون تنزيل الصورة أولاً، ومع ذلك لديك الخيار أيضًا لـ **download image for OCR** إذا لزم الأمر.

## المتطلبات المسبقة

قبل المتابعة، تأكد من وجود ما يلي:

- تثبيت Aspose.OCR for .NET. احصل على أحدث مكتبة من [صفحة الإصدار](https://releases.aspose.com/ocr/net/).  
- بيئة تطوير .NET (Visual Studio، VS Code، أو أي IDE تفضله).  
- اتصال بالإنترنت لجلب الصورة التي **تريد معالجتها**.

## استيراد المساحات الاسمية

أضف المساحات الاسمية المطلوبة لتتمكن من العمل مع فئات Aspose.OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## دليل خطوة بخطوة لتحويل الصورة إلى نص من URL

### الخطوة 1: إعداد دليل المستندات الخاص بك
حدد المكان الذي ستخزن فيه أي ملفات مؤقتة أو نتائج.

```csharp
string dataDir = "Your Document Directory";
```

### الخطوة 2: توفير URL الصورة
قدّم URL يمكن الوصول إليه علنًا. إذا كانت الصورة تتطلب مصادقة، ستحتاج أولاً إلى **download image for OCR** ثم استخدام تدفق بدلاً من ذلك.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

### الخطوة 3: تهيئة محرك AsposeOcr
أنشئ مثيلًا لمحرك OCR.

```csharp
AsposeOcr api = new AsposeOcr();
```

### الخطوة 4: تكوين إعدادات التعرف على OCR
قم بضبط كيفية معالجة المحرك للصورة. هنا نقوم بتمكين اكتشاف المناطق، وتصحيح الانحراف التلقائي، وتحديد مستطيلين مخصصين كمثال على **ocr recognition settings**.

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

> **نصيحة احترافية:** إذا لم تكن بحاجة إلى مناطق مخصصة، عيّن `DetectAreas = false` ودع المحرك يحدد كتل النص تلقائيًا.

### الخطوة 5: إخراج نتيجة OCR
اطبع النص المعترف به، والمناطق المكتشفة، وأي تحذيرات، وحمولة JSON الكاملة للتصحيح.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

### الخطوة 6: تأكيد نجاح التنفيذ
رسالة تأكيد بسيطة تخبرك بأن العملية انتهت دون استثناءات.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## المشكلات الشائعة والحلول

- **الصورة غير متاحة للجمهور** – تحقق من أن الـ URL يعمل في المتصفح. للصور المحمية، قم بتنزيلها أولاً واستدعِ `RecognizeImageFromStream`.  
- **المناطق المكتشفة غير صحيحة** – عدل قيم `Rectangle` أو عطل `DetectAreas` لتمكين الاكتشاف التلقائي.  
- **اللغة غير معروفة** – ثبّت **OCR language pack** المناسب وعين `Language = "eng"` (أو أي رمز ISO آخر) في `RecognitionSettings`.  

## الأسئلة المتكررة

### س1: هل Aspose.OCR مناسب للتعامل مع لغات متعددة؟
**ج:** نعم. بإضافة **ocr language pack** المناسب، يمكنك التعرف على النص بعدة لغات.

### س2: هل يمكنني استخدام Aspose.OCR لاستخراج نص أحادي السطر ومتعدد الأسطر؟
**ج:** بالتأكيد. قم بتبديل `RecognizeSingleLine` في `RecognitionSettings` وفقًا لاحتياجاتك.

### س3: هل هناك خيارات ترخيص للمشاريع التجارية؟
**ج:** نعم، يمكنك استكشاف خيارات الترخيص وشراء ترخيص كامل عبر [متجر Aspose](https://purchase.aspose.com/buy).

### س4: هل تتوفر نسخة تجريبية مجانية؟
**ج:** نعم، نسخة تجريبية متاحة للتحميل من [صفحة الإصدارات](https://releases.aspose.com/).

### س5: أين يمكنني العثور على دعم المجتمع؟
**ج:** زر منتدى [Aspose.OCR](https://forum.aspose.com/c/ocr/16) المخصص للحصول على المساعدة والنقاشات.

## الخاتمة

مع Aspose.OCR for .NET، يصبح تحويل الصورة إلى نص من URL بعيد أمرًا بسيطًا وقابلًا للتخصيص بدرجة عالية. باتباع الخطوات أعلاه يمكنك دمج قدرات OCR قوية في أي تطبيق .NET، سواء كنت تحتاج إلى وظيفة **extract text from image** بسيطة أو إلى **ocr recognition settings** متقدمة للمستندات المعقدة.

---

**آخر تحديث:** 2026-02-25  
**تم الاختبار مع:** Aspose.OCR 24.11 for .NET  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}