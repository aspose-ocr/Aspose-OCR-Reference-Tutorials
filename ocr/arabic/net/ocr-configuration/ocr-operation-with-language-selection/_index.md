---
date: 2026-02-25
description: تعلم كيفية استخراج نص الصورة باستخدام C# و Aspose.OCR لـ .NET. يوضح هذا
  الدليل خطوة بخطوة التعرف الضوئي على الأحرف متعدد اللغات، اختيار اللغة، ونصائح عملية.
linktitle: Extract image text C# with language selection using Aspose.OCR
second_title: Aspose.OCR .NET API
title: استخراج نص الصورة في C# مع اختيار اللغة باستخدام Aspose.OCR
url: /ar/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

Let's translate.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR

## المقدمة

إذا كنت بحاجة إلى **استخراج نص الصورة C#** من الصور وملفات PDF في تطبيق .NET، فإن Aspose.OCR لـ .NET يقدم حلاً سريعًا ودقيقًا ومراعيًا للغات. في هذا الدرس سنستعرض مثالًا واقعيًا يوضح التعرف الضوئي على الأحرف (OCR) مع اختيار اللغة، بحيث يمكنك استخراج النص متعدد اللغات من الصور ببضع أسطر من الشيفرة فقط. في النهاية ستدرك مدى سهولة دمج OCR في مشاريع C# الخاصة بك ولماذا يُعد هذا النهج خيارًا قويًا لأحمال العمل الإنتاجية.

## إجابات سريعة
- **ماذا يفعل Aspose.OCR؟** يتعرف على النص المطبوع والمكتوب يدويًا في الصور ويعيد النص المستخرج.  
- **هل يمكنني اختيار اللغة؟** نعم – يمكنك تحديد أي لغة مدعومة مثل الإنجليزية، الألمانية، الإسبانية، الصينية، إلخ.  
- **هل أحتاج إلى ترخيص للتطوير؟** النسخة التجريبية المجانية تكفي للتقييم؛ الترخيص مطلوب للاستخدام الإنتاجي.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+، .NET Core 3.1+، .NET 5/6+.  
- **هل تصحيح الميل تلقائي؟** يمكنك تفعيل `AutoSkew` وضبط إعداد `SkewAngle` يدويًا.  

## ما هو “استخراج نص الصورة C#”؟

استخراج نص الصورة في C# يعني استخدام مكتبة لقراءة المحتوى البصري لصورة (PNG، JPEG، TIFF، إلخ) وتحويله إلى نص قابل للبحث والتحرير. توفر Aspose.OCR هذه القدرة محليًا، دون إرسال البيانات إلى خدمات خارجية، مما يحافظ على أمان سير العمل والامتثال للمعايير.

## لماذا تختار Aspose.OCR لمهام OCR؟

- **دقة عالية** عبر خطوط متعددة وجودات صور مختلفة.  
- **اختيار لغة مدمج** يلغي الحاجة إلى حزم لغات خارجية.  
- **واجهة برمجة تطبيقات بسيطة** تتكامل بسلاسة مع مشاريع C# الحالية، مما يجعل **استخراج نص الصورة C#** أمرًا سهلًا.  
- **لا توجد تبعيات خارجية** – كل شيء يعمل محليًا، مما يحافظ على أمان بياناتك.  

## المتطلبات المسبقة

قبل الغوص في الشيفرة، تأكد من توفر المتطلبات التالية:

- Aspose.OCR لـ .NET: تأكد من تثبيت مكتبة Aspose.OCR. يمكنك تنزيلها من [صفحة تنزيل Aspose.OCR لـ .NET](https://releases.aspose.com/ocr/net/).

- بيئة التطوير: إعداد بيئة عمل لتطبيق .NET. إذا لم تقم بذلك بعد، راجع [الوثائق](https://reference.aspose.com/ocr/net/) للحصول على تعليمات مفصلة.

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

ابدأ بتهيئة كائن من فئة Aspose.OCR. هذا يهيئ البيئة لاستخدام قدرات OCR داخل تطبيقك.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## الخطوة 2: تحديد مسار الصورة

بعد ذلك، عرّف المسار إلى الصورة التي تريد إجراء OCR عليها. تأكد من أن الصورة قابلة للوصول من تطبيقك.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## الخطوة 3: التعرف على الصورة مع اختيار اللغة

الآن يأتي الجزء الأساسي من عملية OCR. استخدم مكتبة Aspose.OCR للتعرف على النص من الصورة المحددة. اضبط إعدادات التعرف، بما في ذلك اختيار اللغة، لتخصيص عملية **استخراج نص الصورة C#**.

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

- **اختيار لغة غير صحيح** – إذا كان الناتج مشوشًا، تحقق من أن خاصية `Language` تتطابق مع لغة الصورة المصدر.  
- **صور مائلة** – فعّل `AutoSkew` أو اضبط `SkewAngle` يدويًا للحصول على دقة أفضل في المسحات المائلة.  
- **ملفات كبيرة** – عالج الصور الكبيرة على دفعات أو قلل الدقة قبل تمريرها إلى `RecognizeImage` لتوفير الذاكرة.  

## الأسئلة المتكررة

**س: هل Aspose.OCR مناسب للتعرف على النص متعدد اللغات؟**  
ج: نعم، يدعم Aspose.OCR عدة لغات، مما يوفر مرونة لمهام OCR متعددة اللغات.

**س: هل يمكنني ضبط إعدادات OCR لتناسب خصائص صورة معينة؟**  
ج: بالتأكيد! يمكنك تعديل معلمات مثل زاوية الميل، التعرف على الخطوط، واكتشاف المناطق لتحسين OCR في سيناريوهات مختلفة.

**س: أين يمكنني العثور على دعم إضافي أو مناقشات المجتمع؟**  
ج: زر [منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) للحصول على الدعم والمناقشات مع المجتمع.

**س: هل هناك نسخة تجريبية مجانية؟**  
ج: نعم، استكشف [النسخة التجريبية المجانية](https://releases.aspose.com/) لتجربة إمكانيات Aspose.OCR.

**س: كيف يمكنني شراء Aspose.OCR لـ .NET؟**  
ج: للشراء، زر [صفحة الشراء](https://purchase.aspose.com/buy).

## الخاتمة

تهانينا! لقد تعلمت **كيفية استخراج نص الصورة C#** مع اختيار اللغة باستخدام Aspose.OCR لـ .NET. أظهر لك هذا الدرس كيفية تكوين محرك OCR، اختيار اللغة المناسبة، ومعالجة النتائج، مما يمنحك أساسًا قويًا لبناء ميزات استخراج نص متعدد اللغات في تطبيقاتك.

---

**آخر تحديث:** 2026-02-25  
**تم الاختبار مع:** Aspose.OCR 24.11 لـ .NET  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}