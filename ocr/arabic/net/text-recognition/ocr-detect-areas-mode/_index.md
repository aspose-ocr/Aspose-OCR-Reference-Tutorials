---
date: 2026-01-02
description: عزز تطبيقات .NET الخاصة بك باستخدام Aspose.OCR للتعرف الفعال على نصوص
  الصور عبر وضع مستند OCR. تعلّم كيفية استخراج نص الجدول من الصورة من خلال هذا الدرس
  التعليمي لـ Aspose OCR بلغة C#.
linktitle: OCR Detect Areas Mode in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: وضع مستند OCR – وضع اكتشاف المناطق في التعرف على الصور عبر OCR
url: /ar/net/text-recognition/ocr-detect-areas-mode/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# وضع مستند OCR – وضع اكتشاف المناطق في التعرف على الصور OCR

## المقدمة

في تطوير .NET الحديث، **ocr document mode** هو النهج المفضل عندما تحتاج إلى تحكم دقيق في كيفية اكتشاف النص داخل الصور. تجعل Aspose.OCR for .NET من السهل التبديل بين استراتيجيات الكشف المختلفة، مما يتيح لك **extract table text image** من تخطيطات معقدة مثل الإيصالات، الفواتير، أو المستندات متعددة الأعمدة. سيوجهك هذا **aspose ocr tutorial c#** عبر ميزة Detect Areas Mode، يشرح متى تستخدم كل وضع، ويعرض لك مثال شفرة جاهز للتنفيذ.

## إجابات سريعة
- **ما هو وضع مستند OCR؟** مجموعة من استراتيجيات الكشف (PHOTO, DOCUMENT, COMBINE) التي تخبر Aspose.OCR كيفية تحديد مناطق النص.
- **أي وضع يعمل بشكل أفضل للجداول؟** وضع `PHOTO` يتفوق في استخراج جدول النص من الصورة والكتل النصية الصغيرة.
- **هل أحتاج إلى ترخيص للتطوير؟** ترخيص تجريبي مجاني يكفي للاختبار؛ يلزم ترخيص تجاري للإنتاج.
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+، .NET Core 3.1+، .NET 5/6 وما بعده.
- **كم يستغرق إعداد البيئة؟** عادةً أقل من 10 دقائق لتكامل وتشغيل شفرة العينة.

## ما هو وضع مستند OCR؟
`ocr document mode` يشير إلى التكوين الذي يخبر Aspose.OCR كيف يقسم الصورة قبل تنفيذ التعرف على النص. الأنماط الثلاثة المدمجة هي:

- **PHOTO** – مُحسّن للصور الفوتوغرافية، الإيصالات، الفواتير، ومناطق النص الصغيرة (مثالي لاستخراج جدول النص من الصورة).
- **DOCUMENT** – مناسب للصفحات المطبوعة متعددة الأعمدة والمستندات التي تحتوي على رسومات مدمجة.
- **COMBINE** – يجمع نتائج PHOTO و DOCUMENT للحصول على تغطية شاملة بأقصى قدر ممكن.

## لماذا نستخدم وضع اكتشاف المناطق؟
اختيار وضع الكشف المناسب يقلل من الإيجابيات الكاذبة، يسرّع المعالجة، ويحسّن الدقة—خاصةً عند التعامل مع بيانات منظمة مثل الجداول. من خلال تعديل الوضع وفقًا لنوع الصورة، يمكنك تحقيق نتائج OCR موثوقة دون الحاجة إلى معالجة لاحقة.

## المتطلبات المسبقة

قبل البدء، تأكد من وجود ما يلي:

- **Aspose.OCR for .NET** – قم بتحميل وتثبيت المكتبة من [Aspose.OCR for .NET documentation](https://reference.aspose.com/ocr/net/).
- **Document Directory** – مجلد على جهازك يحتوي على الصور التي تريد معالجتها (مثال: `table.png`).

## استيراد المساحات الاسمية

أولاً، استورد المساحات الاسمية المطلوبة للعمل مع Aspose.OCR في مشروع C# الخاص بك.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## الخطوة 1: تهيئة Aspose.OCR

أنشئ نسخة من محرك OCR ووجهها إلى مجلد البيانات الخاص بك.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## الخطوة 2: تحميل الصورة واختيار وضع اكتشاف المناطق

حمّل الصورة المستهدفة وحدد استراتيجية الكشف التي تتطابق مع سيناريوك.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "table.png", new RecognitionSettings
{
    // Choose the Detect Areas Mode
    DetectAreasMode = DetectAreasMode.PHOTO
    // Other options: NONE, DOCUMENT, COMBINE
});
```

## الخطوة 3: استرجاع وعرض النص المعترف به

بعد إكمال OCR، يمكنك الوصول إلى النص المستخرج—مثالي للمعالجة الإضافية أو التخزين في قاعدة بيانات.

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);

Console.WriteLine("OCRDetectAreasMode executed successfully");
```

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|--------|-----|
| **إخراج فارغ** | وضع `DetectAreasMode` غير مناسب لنوع الصورة | التحويل إلى `DOCUMENT` أو `COMBINE` حسب التخطيط |
| **حروف غير صالحة** | صورة منخفضة الدقة | توفير مصدر بدقة أعلى أو معالجة مسبقة بتحسين الصورة |
| **انتهاء المهلة على ملفات كبيرة** | نقص الذاكرة | استخدام `RecognitionSettings` لتحديد حجم المنطقة أو معالجة الصفحات على دفعات |

## الأسئلة المتكررة

**س: هل Aspose.OCR for .NET مناسب للتطبيقات على نطاق واسع؟**  
ج: نعم، تم تصميمه للتعامل مع أحجام OCR الكبيرة بأداء محسن.

**س: هل يمكنني استخدام Aspose.OCR for .NET للتعرف على النص المكتوب يدويًا؟**  
ج: تركز المكتبة على النص المطبوع؛ قد يتطلب التعرف على الخط اليدوي محركًا متخصصًا.

**س: ما صيغ الصور المدعومة؟**  
ج: الصيغ الشائعة مثل PNG، JPEG، BMP، و TIFF مدعومة بالكامل.

**س: كيف يمكنني الحصول على الدعم الفني؟**  
ج: زر [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) لطرح الأسئلة والتفاعل مع المجتمع.

**س: هل هناك نسخة تجريبية مجانية متاحة؟**  
ج: نعم، يمكنك استكشاف القدرات باستخدام [free trial license](https://releases.aspose.com/).

## الخلاصة

من خلال إتقان **ocr document mode** وخيارات وضع اكتشاف المناطق، يمكنك ضبط Aspose.OCR for .NET لاستخراج جدول النص من الصورة وغيرها من البيانات المنظمة بدقة عالية. دمج هذا النهج في تطبيقاتك يتيح أتمتة إدخال البيانات، معالجة الفواتير، أو أي سيناريو يتطلب تحويل الصور إلى نص قابل للبحث.

---

**آخر تحديث:** 2026-01-02  
**تم الاختبار مع:** Aspose.OCR 24.11 for .NET  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}