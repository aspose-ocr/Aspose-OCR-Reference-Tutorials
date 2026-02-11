---
date: 2025-12-21
description: تعرّف على كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) واستخراج النص من
  الصورة باستخدام Aspose.OCR لـ .NET. يوضح هذا الدليل خطوة بخطوة التعرف على النص متعدد
  اللغات واختيار اللغة.
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: كيفية تنفيذ التعرف الضوئي على الأحرف مع اختيار اللغة في Aspose.OCR
url: /ar/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR مع اختيار اللغة في Aspose.OCR

## المقدمة

إذا كنت بحاجة إلى **كيفية تنفيذ OCR** على الصور واستخراج النص من ملفات الصور في تطبيق .NET، فإن Aspose.OCR لـ .NET يقدم حلاً سريعًا ودقيقًا وواعٍ للغة. في هذا البرنامج التعليمي سنستعرض مثالًا واقعيًا يوضح التعرف على الصور باستخدام OCR مع اختيار اللغة، بحيث يمكنك استخراج نص متعدد اللغات من الصور ببضع أسطر من الشيفرة فقط.

## إجابات سريعة
- **ماذا يفعل Aspose.OCR؟** يتعرف على النص المطبوع والمكتوب يدويًا في الصور ويعيد النص المستخرج.  
- **هل يمكنني اختيار اللغة؟** نعم – يمكنك تحديد أي لغة مدعومة مثل الإنجليزية أو الألمانية أو الإسبانية أو الصينية، إلخ.  
- **هل أحتاج إلى ترخيص للتطوير؟** النسخة التجريبية المجانية تكفي للتقييم؛ الترخيص مطلوب للاستخدام في بيئة الإنتاج.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+، .NET Core 3.1+، .NET 5/6+.  
- **هل تصحيح الميل تلقائي؟** يمكنك تمكين `AutoSkew` وضبط إعداد `SkewAngle` يدويًا.

## لماذا تختار Aspose.OCR لمهام OCR؟

- **دقة عالية** عبر خطوط متعددة وجودات صور مختلفة.  
- **اختيار اللغة مدمج** يلغي الحاجة إلى حزم لغات خارجية.  
- **واجهة برمجة تطبيقات بسيطة** تتكامل بسهولة مع مشاريع C# الحالية.  
- **لا توجد تبعيات خارجية** – كل شيء يعمل محليًا، مما يحافظ على أمان بياناتك.

## المتطلبات المسبقة

قبل الغوص في الشيفرة، تأكد من توفر المتطلبات التالية:

- Aspose.OCR لـ .NET: تأكد من تثبيت مكتبة Aspose.OCR. يمكنك تنزيلها من [صفحة تنزيل Aspose.OCR لـ .NET](https://releases.aspose.com/ocr/net/).
- بيئة التطوير: قم بإعداد بيئة عمل لتطبيق .NET. إذا لم تقم بذلك بعد، راجع [الوثائق](https://reference.aspose.com/ocr/net/) للحصول على تعليمات مفصلة.

## استيراد المساحات الاسمية

في تطبيق .NET الخاص بك، ابدأ باستيراد المساحات الاسمية الضرورية:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## الخطوة 1: تهيئة Aspose.OCR

ابدأ بتهيئة كائن من فئة Aspose.OCR. هذا يهيئ البيئة لاستخدام إمكانيات OCR داخل تطبيقك.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## الخطوة 2: تحديد مسار الصورة

بعد ذلك، عرّف المسار إلى الصورة التي تريد تنفيذ OCR عليها. تأكد من أن الصورة متاحة لتطبيقك.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## الخطوة 3: التعرف على الصورة مع اختيار اللغة

الآن يأتي الجزء الأساسي من عملية OCR. استخدم مكتبة Aspose.OCR للتعرف على النص من الصورة المحددة. اضبط إعدادات التعرف، بما في ذلك اختيار اللغة.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## الخطوة 4: طباعة وعرض النتائج

بعد عملية OCR، اطبع واعرض النتائج، بما في ذلك النص المعترف به، المناطق، التحذيرات، وتمثيل JSON.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## المشكلات الشائعة والنصائح

- **اختيار لغة غير صحيح** – إذا كان الناتج مشوشًا، تحقق مرة أخرى من أن خاصية `Language` تتطابق مع لغة الصورة المصدر.  
- **صور مائلة** – فعّل `AutoSkew` أو اضبط `SkewAngle` يدويًا للحصول على دقة أفضل في المسحات المائلة.  
- **ملفات كبيرة** – عالج الصور الكبيرة على دفعات أو قلل الدقة قبل تمريرها إلى `RecognizeImage` لتقليل استهلاك الذاكرة.

## الخاتمة

تهانينا! لقد تعلمت **كيفية تنفيذ OCR** مع اختيار اللغة باستخدام Aspose.OCR لـ .NET. أظهر لك هذا البرنامج التعليمي كيفية استخراج النص من ملفات الصور، تخصيص إعدادات التعرف، والتعامل مع المحتوى متعدد اللغات بسهولة.

## الأسئلة المتكررة

### س1: هل Aspose.OCR مناسب للتعرف على النص متعدد اللغات؟

ج1: نعم، يدعم Aspose.OCR عدة لغات، مما يوفر مرونة لمهام OCR متعددة اللغات.

### س2: هل يمكنني ضبط إعدادات OCR لتناسب خصائص صورة معينة؟

ج2: بالتأكيد! اضبط معلمات مثل زاوية الميل، التعرف على الخطوط، واكتشاف المناطق لتحسين OCR في سيناريوهات مختلفة.

### س3: أين يمكنني العثور على دعم إضافي أو مناقشات المجتمع؟

ج3: زر [منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) للحصول على الدعم والمناقشات مع المجتمع.

### س4: هل تتوفر نسخة تجريبية مجانية؟

ج4: نعم، استكشف [النسخة التجريبية المجانية](https://releases.aspose.com/) لتجربة إمكانيات Aspose.OCR.

### س5: كيف يمكنني شراء Aspose.OCR لـ .NET؟

ج5: للشراء، زر [صفحة الشراء](https://purchase.aspose.com/buy).

---

**آخر تحديث:** 2025-12-21  
**تم الاختبار مع:** Aspose.OCR 24.11 لـ .NET  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}