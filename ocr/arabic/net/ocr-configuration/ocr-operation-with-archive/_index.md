---
date: 2025-12-19
description: تعلم كيفية إجراء التعرف الضوئي على الحروف (OCR) على صور الأرشيف، وتحويل
  الصور إلى نص، واستخراج النص من ملفات الأرشيف باستخدام Aspose.OCR لـ .NET.
linktitle: How to Perform OCR on Archive Images with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: كيفية إجراء OCR على صور الأرشيف باستخدام Aspose.OCR لـ .NET
url: /ar/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إجراء OCR على صور الأرشيف باستخدام Aspose.OCR لـ .NET

## مقدمة

في هذا الدرس الشامل ستكتشف **كيفية إجراء OCR** على ملفات الصور المؤرشفة باستخدام مكتبة Aspose.OCR لـ .NET. سواء كنت بحاجة إلى **تحويل الصور إلى نص** أو **استخراج النص من الأرشيف**، سيوجهك الدليل خطوة بخطوة أدناه عبر كل شيء—من إعداد بيئة التطوير إلى استرجاع النص المعترف به من كل صورة داخل أرشيف ZIP.

## إجابات سريعة
- **ما الذي يغطيه الدرس؟** إجراء OCR على صور الأرشيف (ZIP) باستخدام Aspose.OCR لـ .NET.  
- **ما هي الكلمة المفتاحية الأساسية المستهدفة؟** *how to perform ocr*.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تكفي للتقييم؛ يلزم الحصول على ترخيص تجاري للإنتاج.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+، .NET Core 3.1+، .NET 5/6+.  
- **هل يمكنني تخصيص إعدادات التعرف؟** نعم—استخدم `RecognitionSettings` لضبط الدقة.

## ما هو OCR ولماذا نستخدمه على الأرشيفات؟

يحوّل التعرف الضوئي على الأحرف (OCR) الصور الممسوحة أو ملفات PDF إلى نص قابل للبحث والتحرير. عندما تُجمع الصور داخل أرشيف (مثل ملف ZIP)، فإن استخراج كل صورة والتعرف عليها دفعة واحدة يوفر الوقت ويقلل تعقيد الشيفرة. طريقة `RecognizeMultipleImages` في Aspose.OCR تجعل هذه العملية مباشرة.

## المتطلبات المسبقة

- Visual Studio 2019 أو أحدث (أو أي بيئة تطوير متوافقة مع .NET).  
- .NET Framework 4.5 + أو .NET Core 3.1 + مثبتة.  
- الوصول إلى مكتبة Aspose.OCR لـ .NET (رابط التحميل أدناه).  
- ترخيص Aspose.OCR صالح للاستخدام في الإنتاج (يتوفر نسخة تجريبية).

## استيراد مساحات الأسماء

في مشروع .NET الخاص بك، تأكد من استيراد مساحات الأسماء اللازمة للوصول إلى الوظائف التي توفرها Aspose.OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## تنزيل وتثبيت Aspose.OCR لـ .NET

احصل على أحدث حزمة من صفحة الإصدار **[هنا](https://releases.aspose.com/ocr/net/)** واتبع خطوات التثبيت القياسية عبر NuGet أو يدويًا.

## الحصول على ترخيص

احصل على ترخيص من **[صفحة الشراء](https://purchase.aspose.com/buy)** أو جرّب **[النسخة التجريبية المجانية](https://releases.aspose.com/)**. ضع ملف الترخيص في جذر المشروع وحمّله أثناء التشغيل كما هو موضح في وثائق Aspose.

## الخطوة 1: إعداد دليل المستندات الخاص بك

ابدأ بتهيئة المسار إلى دليل المستندات الخاص بك:

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **نصيحة محترف:** استخدم `Path.Combine` لمعالجة المسارات عبر الأنظمة.

## الخطوة 2: تهيئة Aspose.OCR

أنشئ مثالًا من فئة Aspose.OCR لبدء عمليات OCR:

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## الخطوة 3: تحديد مسار الصورة

حدد المسار الكامل إلى صورة الأرشيف الخاصة بك (ملف ZIP الذي يحتوي على الصور التي تريد قراءتها):

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## الخطوة 4: التعرف على الصورة

نفّذ عملية التعرف الضوئي على الأحرف على الأرشيف المحدد باستخدام الإعدادات الافتراضية أو المخصصة. هذه الدالة تستخرج كل صورة من ملف ZIP تلقائيًا وتجرى عليها OCR:

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> يمكنك تعديل `RecognitionSettings` لتحسين الدقة للغات أو جودة صور معينة.

## الخطوة 5: طباعة النتائج

قم بالتكرار عبر النتائج واطبع النص المعترف به لكل صورة داخل الأرشيف:

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

يعرض الناتج فهرس كل صورة متبوعًا بالسلسلة المستخرجة، مما يحول **الصور إلى نص** و**يستخرج النص من الأرشيف** بفعالية.

## المشكلات الشائعة & استكشاف الأخطاء وإصلاحها

| المشكلة | السبب | الحل |
|-------|-------|----------|
| لا يتم إرجاع نص | جودة الصورة منخفضة جدًا | قم بتمهيد الصور (مثل التحويل إلى ثنائي) أو اضبط `RecognitionSettings.Dpi` |
| استثناء عند قراءة ZIP | مسار الأرشيف غير صالح | تحقق من أن `fullPath` يشير إلى ملف `.zip` صالح وأن التطبيق يملك أذونات القراءة |
| الترخيص غير مُطبق | ملف الترخيص مفقود أو لم يُحمَّل | استدعِ `License license = new License(); license.SetLicense("Aspose.OCR.lic");` قبل إنشاء كائن `AsposeOcr` |

## الأسئلة المتكررة

**س: هل يمكنني استخدام Aspose.OCR لـ .NET بدون ترخيص؟**  
ج: نعم، تتوفر نسخة تجريبية مجانية للتقييم، لكن النسخة المرخصة مطلوبة للنشر في بيئات الإنتاج.

**س: هل تدعم المكتبة أرشيفات ZIP المحمية بكلمة مرور؟**  
ج: حاليًا، تعمل `RecognizeMultipleImages` مع ملفات ZIP القياسية. بالنسبة للأرشيفات المشفرة، يجب استخراج الصور أولاً باستخدام مكتبة طرف ثالث، ثم تمرير مصفوفة الصور إلى محرك OCR.

**س: كيف يمكنني تحسين الدقة للنص المكتوب يدويًا؟**  
ج: فعّل العلم `RecognitionSettings.EnableHandwritingRecognition` وامنح إعداد DPI أعلى (مثلاً 300).

**س: هل هناك طريقة للحصول على درجات الثقة لكل سطر مُعترف به؟**  
ج: كل `RecognitionResult` يحتوي على خاصية `Confidence` يمكنك تسجيلها أو استخدامها لتصفية النتائج ذات الثقة المنخفضة.

## الخلاصة

الآن لديك سير عمل كامل وجاهز للإنتاج **لإجراء OCR على صور الأرشيف**، **تحويل الصور إلى نص**، و**استخراج النص من الأرشيف** باستخدام Aspose.OCR لـ .NET. دمج هذا في تطبيقاتك يتيح مستودعات مستندات قابلة للبحث، إدخال بيانات آلي، أو أي سيناريو يتطلب استخراج نص من مجموعة كبيرة من الصور.

## موارد إضافية

- **منتدى Aspose.OCR:** للحصول على دعم المجتمع والسيناريوهات المتقدمة، زر [منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16).  
- **ترخيص مؤقت:** إذا كنت بحاجة إلى تقييم قصير الأمد، اطلب [ترخيصًا مؤقتًا](https://purchase.aspose.com/temporary-license/).  
- **الوثائق الرسمية:** ابقَ محدثًا بأحدث تغييرات API عبر مراجعة [الوثائق](https://reference.aspose.com/ocr/net/).

---

**آخر تحديث:** 2025-12-19  
**تم الاختبار مع:** Aspose.OCR 24.11 لـ .NET  
**المؤلف:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
