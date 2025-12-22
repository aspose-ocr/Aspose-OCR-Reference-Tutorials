---
date: 2025-12-22
description: تعلم كيفية استخراج النص من الصورة باستخدام Aspose.OCR لـ .NET. يوضح لك
  هذا الدليل كيفية إعداد المستطيلات للتعرف على النص في الصورة باستخدام OCR وتعزيز
  الدقة.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: كيفية استخراج النص من الصورة عن طريق إعداد المستطيلات في OCR
url: /ar/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحضير المستطيلات في التعرف على النصوص من الصور (OCR)

## المقدمة

التعرف الضوئي على الأحرف (OCR) ضروري لتحويل المحتوى البصري إلى نص قابل للبحث والتحرير. في هذا الدرس ستقوم **باستخراج النص من الصورة** عن طريق تحضير مستطيلات مخصصة تركّز محرك OCR على مناطق محددة. باستخدام Aspose.OCR for .NET، سنستعرض كل خطوة — من إعداد مشروعك إلى استرجاع النص المعترف به — لتتمكن من دمج وظيفة قوية لتحويل الصورة إلى نص في تطبيقات .NET الخاصة بك.

## إجابات سريعة
- **ماذا يعني “استخراج النص من الصورة”؟** يعني تحويل الأحرف البصرية في الصورة إلى سلاسل قابلة للقراءة آليًا.  
- **ما المكتبة التي تساعد في ذلك في .NET؟** Aspose.OCR for .NET.  
- **هل أحتاج إلى ترخيص للتطوير؟** النسخة التجريبية المجانية تكفي للاختبار؛ الترخيص مطلوب للإنتاج.  
- **هل يمكنني استهداف مناطق محددة؟** نعم، عن طريق تعريف مستطيلات تحدد نطاق OCR.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+، .NET Core 3.1+، .NET 5/6/7.

## ما هو “استخراج النص من الصورة” باستخدام المستطيلات؟
عند تعريف مناطق مستطيلة على الصورة، يقوم محرك OCR بمعالجة تلك المناطق فقط. هذا يحسن الدقة، يقلل من زمن المعالجة، ويسمح لك بتجاهل الخلفيات المزعجة أو الأقسام غير ذات الصلة.

## لماذا تحضير المستطيلات قبل OCR؟
- **التركيز على المحتوى ذي الصلة:** تخطي العناوين، التذييلات، أو الرسومات الزخرفية.  
- **تحسين الأداء:** المناطق الأصغر تعني التعرف أسرع.  
- **تحسين الدقة:** القليل من الضوضاء البصرية يؤدي إلى نتائج أنظف.

## المتطلبات المسبقة

- الإلمام بـ C# وتطوير .NET.  
- مكتبة Aspose.OCR for .NET مثبتة – يمكنك تحميلها **[هنا](https://releases.aspose.com/ocr/net/)**.  
- صورة نموذجية (مثال: `sample.png`) تحتوي على النص الذي تريد استخراجَه.

## استيراد مساحات الأسماء

أولاً، استدعِ مساحات الأسماء المطلوبة:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## الخطوة 1: إعداد دليل المستندات الخاص بك

حدد مكان وجود ملفات الصور وأنشئ نسخة من محرك OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## كيفية استخراج النص من الصورة باستخدام مستطيلات متعددة

### الخطوة 2: التعرف على الصورة باستخدام مستطيلات متعددة

#### 2.1 تعريف المستطيلات

أنشئ قائمة من كائنات `Rectangle` التي تحدد المناطق التي تريد أن يقوم محرك OCR بمسحها.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 تنفيذ التعرف الضوئي على الأحرف

مرّر مسار الصورة وقائمة المستطيلات إلى `RecognizeImage`. تُعيد الطريقة مجموعة من السلاسل — كل عنصر يُطابق مستطيلًا واحدًا.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### الخطوة 3: التعرف على الصورة باستخدام إعدادات التعرف (نهج بديل)

إذا كنت تفضّل استخدام `RecognitionSettings`، يمكنك تحقيق نفس النتيجة باستدعاء API مختلف قليلًا.

#### 3.1 تعريف إعدادات التعرف

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 عرض النص المعترف به

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## المشكلات الشائعة والنصائح

- **إحداثيات المستطيل غير صحيحة:** تأكد من أن قيم `X` و `Y` و `Width` و `Height` تمثل المنطقة المطلوبة بدقة.  
- **جودة الصورة:** قد تؤدي الصور منخفضة الدقة إلى نتائج OCR ضعيفة؛ فكر في المعالجة المسبقة (مثل التحويل إلى ثنائي).  
- **نتائج فارغة:** تحقق من أن المستطيلات تحتوي فعليًا على نص؛ وإلا سيعيد المحرك سلاسل فارغة.

## الخلاصة

لقد تعلمت الآن كيفية **استخراج النص من الصورة** عن طريق تحضير مستطيلات مخصصة باستخدام Aspose.OCR for .NET. تمنحك هذه التقنية تحكمًا دقيقًا في معالجة OCR، مما يساعدك على بناء ميزات استخراج نص أسرع وأكثر دقة في تطبيقاتك.

## الأسئلة المتكررة

**س:** هل يمكنني استخدام Aspose.OCR for .NET مع أطر .NET أخرى؟  
**ج:** نعم، Aspose.OCR for .NET متوافق مع أطر .NET المختلفة.

**س:** هل هناك نسخة تجريبية مجانية متاحة لـ Aspose.OCR for .NET؟  
**ج:** بالتأكيد! يمكنك الوصول إلى النسخة التجريبية **[هنا](https://releases.aspose.com/)**.

**س:** كيف أحصل على الدعم لـ Aspose.OCR for .NET؟  
**ج:** زر **[منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16)** للحصول على الدعم المتخصص.

**س:** هل يمكنني الحصول على ترخيص مؤقت لأغراض الاختبار؟  
**ج:** نعم، يمكنك الحصول على ترخيص مؤقت **[هنا](https://purchase.aspose.com/temporary-license/)**.

**س:** أين يمكنني العثور على وثائق Aspose.OCR for .NET؟  
**ج:** الوثائق متاحة **[هنا](https://reference.aspose.com/ocr/net/)**.

---

**آخر تحديث:** 2025-12-22  
**تم الاختبار مع:** Aspose.OCR 24.11 for .NET  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}