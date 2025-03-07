---
title: الحصول على مستطيلات للفقرات في التعرف على الصور OCR
linktitle: الحصول على مستطيلات للفقرات في التعرف على الصور OCR
second_title: Aspose.OCR .NET API
description: أطلق العنان لقدرات التعرف الضوئي على الحروف المتقدمة باستخدام Aspose.OCR لـ .NET. استخراج مستطيلات الفقرة دون عناء.
weight: 11
url: /ar/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# الحصول على مستطيلات للفقرات في التعرف على الصور OCR

## مقدمة

مرحبًا بك في دليلنا الشامل حول الاستفادة من Aspose.OCR لـ .NET لاستخراج مستطيلات الفقرات في التعرف على الصور باستخدام OCR. إذا كنت تتطلع إلى تحسين قدرات معالجة المستندات لديك والاستفادة من قوة التعرف الضوئي على الحروف (OCR) في تطبيقات .NET الخاصة بك، فأنت في المكان الصحيح.

## المتطلبات الأساسية

قبل أن نتعمق في البرنامج التعليمي، تأكد من توفر المتطلبات الأساسية التالية:

- المعرفة الأساسية بتطوير C# و.NET.
-  تم إعداد بيئة التطوير باستخدام Aspose.OCR لـ .NET. إذا لم تكن قد قمت بذلك بالفعل، يمكنك تنزيله[هنا](https://releases.aspose.com/ocr/net/).
- فهم مفاهيم معالجة الصور وأهمية التعرف الضوئي على الحروف (OCR) في استخراج النص من الصور.

## استيراد مساحات الأسماء

في كود C# الخاص بك، تأكد من استيراد مساحات الأسماء اللازمة لاستخدام Aspose.OCR بكفاءة. قم بتضمين ما يلي في أعلى ملفك:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## الخطوة 1: قم بإعداد دليل المستندات الخاص بك

ابدأ بتهيئة المسار إلى دليل المستندات الخاص بك حيث يتم تخزين الصور لمعالجة التعرف الضوئي على الحروف:

```csharp
string dataDir = "Your Document Directory";
```

## الخطوة 2: تهيئة مثيل AsposeOcr

قم بإنشاء مثيل لفئة AsposeOcr للوصول إلى وظائف التعرف الضوئي على الحروف:

```csharp
AsposeOcr api = new AsposeOcr();
```

## الخطوة 3: تحديد مسار الصورة

حدد المسار الكامل للصورة التي تريد معالجتها:

```csharp
string fullPath = dataDir + "sample.png";
```

## الخطوة 4: التعرف على الصورة والحصول على مستطيلات الفقرة

 استدعاء`GetRectangles` طريقة للحصول على مستطيلات للفقرات في صورة التعرف الضوئي على الحروف (OCR). تعيين`detect_areas` ل`true` إذا كنت تريد استخراج الفقرات:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## الخطوة 5: طباعة النتائج

طباعة إحداثيات المناطق المحددة:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## الخطوة 6: الاستنتاج

تهانينا! لقد قمت بنجاح بتنفيذ عملية التعرف على الصور OCR للحصول على مستطيلات للفقرات باستخدام Aspose.OCR لـ .NET.

## خاتمة

في هذا البرنامج التعليمي، اكتشفنا الخطوات الأساسية لدمج Aspose.OCR لـ .NET في تطبيقاتك، مما يسمح لك باستخراج مستطيلات الفقرة من الصور التي تمت معالجتها بواسطة OCR. يعمل Aspose.OCR على تبسيط تنفيذ التعرف الضوئي على الحروف، مما يجعله أداة قيمة لمعالجة المستندات واستخراج النص.

## الأسئلة الشائعة

### س1: هل Aspose.OCR متوافق مع تنسيقات الصور المختلفة؟

A1: نعم، يدعم Aspose.OCR تنسيقات الصور المختلفة، بما في ذلك PNG وJPEG وTIFF.

### س2: هل يمكنني استخدام Aspose.OCR للمعالجة المجمعة لصور متعددة؟

ج2: بالتأكيد! يسهل Aspose.OCR معالجة الدُفعات للتعامل مع صور متعددة بسلاسة.

### س3: هل تتوفر نسخة تجريبية مجانية من Aspose.OCR لـ .NET؟

 ج3: نعم، يمكنك استكشاف النسخة التجريبية المجانية[هنا](https://releases.aspose.com/).

### س4: كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.OCR؟

 ج4: يمكنك الحصول على ترخيص مؤقت[هنا](https://purchase.aspose.com/temporary-license/).

### س5: أين يمكنني العثور على دعم إضافي ومناقشات متعلقة بـ Aspose.OCR؟

 ج5: توجه إلى[منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) لدعم المجتمع والمناقشات.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
