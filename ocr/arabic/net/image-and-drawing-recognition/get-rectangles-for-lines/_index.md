---
date: 2026-02-22
description: تعلم كيفية تنفيذ تحليل تخطيط OCR من خلال التعرف على سطور النص في صورة
  واستخراج مستطيلات السطر باستخدام Aspose.OCR لـ .NET.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: تحليل تخطيط OCR – استخراج مستطيلات السطور من الصور
url: /ar/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحليل تخطيط OCR – الحصول على مستطيلات السطر من الصور

## Introduction

في هذا الدرس ستكتشف **كيفية الحصول على مستطيلات سطر OCR** باستخدام Aspose.OCR لـ .NET. بنهاية الدليل ستتمكن من **التعرف على سطور النص في صورة** و **استخراج إحداثيات السطر** لكل سطر مكتشف — مثالي للمعالجة اللاحقة مثل **تحليل تخطيط OCR**، استخراج البيانات، أو العرض المخصص.

## Quick Answers
- **ماذا يعني “الحصول على مستطيلات سطر OCR”?** يُعيد صناديق الإحاطة لكل سطر نصي يتم اكتشافه في صورة.  
- **ما هي طريقة API المستخدمة؟** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تعمل للتطوير؛ يلزم ترخيص تجاري للإنتاج.  
- **ما صيغ الصور المدعومة؟** PNG، JPEG، BMP، TIFF، وأكثر.  
- **هل يمكن تشغيله على .NET Core؟** نعم، Aspose.OCR يدعم بالكامل .NET Core و .NET 5/6.

## Prerequisites

قبل الغوص في الدرس، تأكد من توفر المتطلبات التالية:

- معرفة أساسية بـ C# وتطوير .NET.  
- بيئة تطوير متكاملة (IDE) مثل Visual Studio.  
- مكتبة Aspose.OCR لـ .NET مثبتة. يمكنك تنزيلها [هنا](https://releases.aspose.com/ocr/net/).  
- صورة نموذجية تحتوي على نص للتعرف الضوئي على الأحرف.

## Import Namespaces

تأكد من استيراد المساحات الاسمية اللازمة إلى مشروعك. أضف السطور التالية إلى أعلى ملف C# الخاص بك:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

الآن، دعنا نفصل عملية الحصول على المستطيلات للسطر في التعرف الضوئي على الأحرف إلى خطوات سهلة المتابعة.

## layout analysis ocr – دليل خطوة بخطوة

### Step 1: Set Up Your Document Directory

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

استبدل `"Your Document Directory"` بالمسار الفعلي للمجلد الذي يحتوي على صورتك النموذجية.

### Step 2: Initialize Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

أنشئ مثيلاً من الفئة `AsposeOcr` للوصول إلى وظائف OCR.

### Step 3: Specify Image Path

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

حدد المسار الكامل للصورة التي تريد تنفيذ OCR عليها.

### Step 4: Recognize Image and Get Rectangles

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

طريقة `GetRectangles` تُعيد قائمة من كائنات `Rectangle`، كل منها يمثل إحداثيات سطر نص مكتشف. هذا هو جوهر **الحصول على مستطيلات سطر OCR** ويمكّن **تحليل تخطيط OCR**.

### Step 5: Print Result

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

اطبع إحداثيات المناطق المكتشفة إلى وحدة التحكم. ستظهر لك القيم التي يمكنك لاحقًا استخدامها **لاستخراج إحداثيات السطر** للمعالجة المخصصة.

## Why Use Aspose.OCR for Line Rectangles?

- **دقة عالية** – الخوارزميات المتقدمة تكتشف السطور حتى في الصور الضوضائية أو المائلة.  
- **متعدد المنصات** – يعمل على .NET Framework، .NET Core، و .NET 5/6.  
- **بدون تبعيات خارجية** – مكتبة .NET صافية، لا تحتاج إلى ملفات DLL أصلية.  
- **مخرجات غنية** – بالإضافة إلى مستطيلات السطر يمكنك أيضًا استرجاع الكلمات، الأحرف، ودرجات الثقة.

## Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| **لم يتم إرجاع أي مستطيلات** | تأكد من أن الصورة تحتوي على نص واضح وأفقي وأن `AreasType.LINES` محدد. |
| **إحداثيات غير صحيحة** | تحقق من DPI الصورة؛ قد تتسبب الصور منخفضة الدقة في حدود غير دقيقة. |
| **عنق زجاجة في الأداء مع الصور الكبيرة** | غيّر حجم الصورة إلى دقة معقولة قبل استدعاء `GetRectangles`. |
| **استثناء الترخيص** | استخدم ترخيص تجريبي للاختبار؛ طبق ترخيص كامل للإنتاج لتجنب حدود التقييم. |

## Frequently Asked Questions

**س: هل يمكنني استخراج كلمات فردية بدلاً من السطور الكاملة؟**  
ج: نعم، استخدم `AreasType.WORDS` مع نفس طريقة `GetRectangles` للحصول على صناديق إحاطة على مستوى الكلمات.

**س: هل تدعم API ملفات PDF متعددة الصفحات؟**  
ج: حوّل كل صفحة PDF إلى صورة أولاً، ثم استدعِ `GetRectangles` على كل صورة.

**س: كيف أتعامل مع النص المدوّر؟**  
ج: فعّل خيار التدوير التلقائي في إعدادات OCR أو قم بتدوير الصورة مسبقًا قبل المعالجة.

**س: هل هناك طريقة للحصول على درجات الثقة لكل سطر؟**  
ج: بعد الحصول على المستطيلات، استدعِ `api.RecognizeImage(...).Lines` للوصول إلى كائنات السطر التي تشمل قيم الثقة.

**س: ما إصدارات .NET المتوافقة؟**  
ج: المكتبة تعمل مع .NET Framework 4.5+، .NET Core 3.1+، و .NET 5/6.

## Real‑World Use Cases

- **تحليل تخطيط المستند OCR** – أدخل مستطيلات السطر إلى محرك تخطيط لإعادة بناء هياكل الأعمدة.  
- **استخراج البيانات تلقائيًا** – استخدم الإحداثيات لقص السطور الفردية لخطوط معالجة اللغة الطبيعية اللاحقة.  
- **عرض مخصص** – ضع صناديق الإحاطة فوق الصورة الأصلية للتحقق البصري أو لتراكب واجهة المستخدم.

## Conclusion

تهانينا! لقد نجحت في **الحصول على مستطيلات سطر OCR** لصورة باستخدام Aspose.OCR لـ .NET. مع وجود صناديق الإحاطة، يمكنك الآن إدخال إحداثيات السطر في سير عمل لاحق مثل العرض المخصص، استخراج البيانات، أو **تحليل تخطيط OCR**.

---

**Last Updated:** 2026-02-22  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}