---
date: 2026-07-23
description: تعرف على كيفية استخراج مكتبة OCR لـ .net نص الصورة C# باستخدام Aspose.OCR.
  يغطي هذا الدليل OCR متعدد اللغات، اختيار اللغة، ونصائح عملية.
keywords:
- ocr library for .net
- extract image text c#
- Aspose.OCR
- multilingual OCR
lastmod: 2026-07-23
linktitle: استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR
og_description: تمكن مكتبة OCR لـ .net من استخراج نص الصورة C# باستخدام Aspose.OCR.
  احصل على OCR متعدد اللغات، اختيار اللغة، وأمثلة شفرة خطوة بخطوة.
og_image_alt: 'Guide: Extract image text C# using Aspose.OCR OCR library for .NET'
og_title: مكتبة OCR لـ .net – استخراج نص الصورة C#
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how the ocr library for .net extracts image text C# using Aspose.OCR.
    This guide covers multilingual OCR, language selection, and practical tips.
  headline: ocr library for .net – Extract image text C#
  type: TechArticle
- questions:
  - answer: Yes, Aspose.OCR supports over 30 languages, providing flexibility for
      multilingual OCR tasks.
    question: Is Aspose.OCR suitable for multilingual text recognition?
  - answer: Absolutely! Adjust parameters like `AutoSkew`, `SkewAngle`, and `LineDetectionMode`
      to optimise results for different scenarios.
    question: Can I fine‑tune OCR settings for specific image characteristics?
  - answer: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) for support
      and discussions with the community.
    question: Where can I find additional support or community discussions?
  - answer: Yes, explore the [free trial](https://releases.aspose.com/) to experience
      the capabilities of Aspose.OCR.
    question: Is there a free trial available?
  - answer: To purchase, visit the [purchase page](https://purchase.aspose.com/buy).
    question: How can I purchase Aspose.OCR for .NET?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr library
- Aspose.OCR
- C# OCR
- image text extraction
title: مكتبة OCR لـ .net – استخراج نص الصورة C#
url: /ar/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR

## مقدمة

إذا كنت بحاجة إلى **استخراج نص الصورة C#** من الصور أو ملفات PDF في تطبيق .NET، فإن Aspose.OCR هي مكتبة **ocr library for .net** قوية توفر التعرف السريع والدقيق والواعي باللغات. في هذا الدرس سنستعرض مثالًا واقعيًا يوضح التعرف على الصور باستخدام OCR مع اختيار اللغة، بحيث يمكنك استخراج النص متعدد اللغات من الصور ببضع أسطر من الشيفرة فقط. في النهاية ستدرك لماذا يُعد هذا النهج خيارًا قويًا لأعباء العمل الإنتاجية ومدى سهولة دمج OCR في مشاريع C# الخاصة بك.

## إجابات سريعة
- **ما الذي يفعله Aspose.OCR؟** إنه يتعرف على النص المطبوع والمكتوب يدويًا في الصور ويعيد النص المستخرج.  
- **هل يمكنني اختيار اللغة؟** نعم – يمكنك تحديد أي لغة مدعومة مثل English، German، Spanish، Chinese، إلخ.  
- **هل أحتاج إلى ترخيص للتطوير؟** تجربة مجانية تعمل للتقييم؛ الترخيص مطلوب للاستخدام الإنتاجي.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **هل تصحيح الميل تلقائي؟** يمكنك تمكين `AutoSkew` وضبط إعداد `SkewAngle` بدقة.  

`AutoSkew` يكتشف تلقائيًا ويصحح ميل الصورة. `SkewAngle` يسمح بضبط يدوي لزاوية الدوران.

## ما هو “extract image text C#”؟

استخراج نص الصورة في C# يعني استخدام مكتبة لقراءة المحتوى البصري للصورة (PNG، JPEG، TIFF، إلخ) وتحويله إلى نص قابل للبحث والتحرير. **ocr library for .net** تقوم Aspose.OCR بإجراء هذا التحويل محليًا، مع الحفاظ على البيانات داخل المؤسسة وتجنب استدعاءات الخدمات الخارجية.

## لماذا تختار Aspose.OCR لمهام OCR؟

توفر Aspose.OCR **دقة تزيد عن 95 %** على الخطوط المطبوعة القياسية ويمكنها معالجة **ما يصل إلى 300 صفحة في الدقيقة** على خادم عادي بسرعة 2.5 GHz، مما يجعلها واحدة من أسرع حلول **ocr library for .net**. كما أنها تتضمن حزم لغات مدمجة، لذا لن تحتاج أبدًا إلى موارد طرف ثالث، وتعمل بالكامل دون اتصال لضمان أقصى درجات الأمان.

## المتطلبات المسبقة

قبل أن نغوص في الشيفرة، تأكد من توفر المتطلبات المسبقة التالية:

- Aspose.OCR for .NET: تأكد من تثبيت مكتبة Aspose.OCR. يمكنك تنزيلها من صفحة [Aspose.OCR for .NET download page](https://releases.aspose.com/ocr/net/).
- بيئة التطوير: قم بإعداد بيئة عمل مع تطبيق .NET. إذا لم تقم بذلك بعد، راجع [documentation](https://reference.aspose.com/ocr/net/) للحصول على تعليمات مفصلة.

## استيراد مساحات الأسماء

في تطبيق .NET الخاص بك، ابدأ باستيراد مساحات الأسماء الضرورية:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## الخطوة 1: تهيئة Aspose.OCR

`OcrEngine` هي الفئة الأساسية في Aspose.OCR التي تقوم بالتعرف الضوئي على الأحرف في الصور. ابدأ بإنشاء مثال من هذه الفئة؛ هذا يهيئ الأساس لجميع عمليات OCR اللاحقة.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## الخطوة 2: تحديد مسار الصورة

حدد المسار المطلق أو النسبي للصورة التي تريد معالجتها. يجب أن يشير المسار إلى ملف قابل للقراءة؛ وإلا سيطلق المحرك استثناءً.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## الخطوة 3: التعرف على الصورة مع اختيار اللغة

`RecognizeImage` هي الطريقة التي تمسح البت ماب المزوَّدة، وتطبق نماذج اللغة، وتعيد كائن `RecognitionResult` يحتوي على النص المستخرج. من خلال ضبط خاصية `Language` تخبر المحرك بأي قواعد لغوية يجب تطبيقها، مما يحسن الدقة بشكل كبير للمحتوى غير الإنجليزي.

خاصية `Language` تختار نموذج لغة OCR الذي سيتم استخدامه.

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

بعد عملية OCR، يمكنك الوصول إلى النص المعترف به، ومربعات الحدود لكل كلمة، وأي تحذيرات، وحتى تفريغ JSON للمعالجة اللاحقة.

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

## كيف تستخرج نص الصورة C# مع اختيار اللغة؟

حمّل صورتك باستخدام `new OcrEngine()` واضبط `engine.Language = Language.English` (أو أي لغة مدعومة) قبل استدعاء `engine.RecognizeImage(imagePath)`. تُعيد الطريقة النص الكامل كسلسلة واحدة، يمكنك بعد ذلك طباعته أو تخزينه أو إرساله إلى خدمات أخرى. هذا النمط ذو الخطوتين يعمل مع جميع اللغات المدعومة ولا يتطلب أي تبعيات خارجية.

## المشكلات الشائعة والنصائح

- **اختيار لغة غير صحيح** – إذا كان الناتج مشوشًا، تحقق مرة أخرى من أن خاصية `Language` تتطابق مع لغة الصورة المصدر.  
- **صور مائلة** – فعّل `AutoSkew` أو اضبط `SkewAngle` يدويًا للحصول على دقة أفضل في المسحات المائلة.  
- **ملفات كبيرة** – عالج الصور الكبيرة على دفعات أو قلل الدقة قبل تمريرها إلى `RecognizeImage` لتوفير الذاكرة.  

## الأسئلة المتكررة

**س: هل Aspose.OCR مناسب للتعرف على النص متعدد اللغات؟**  
ج: نعم، يدعم Aspose.OCR أكثر من 30 لغة، مما يوفر مرونة لمهام OCR متعددة اللغات.

**س: هل يمكنني ضبط إعدادات OCR خصيصًا لخصائص صورة معينة؟**  
ج: بالطبع! اضبط معلمات مثل `AutoSkew`، `SkewAngle`، و`LineDetectionMode` لتحسين النتائج في سيناريوهات مختلفة.

**س: أين يمكنني العثور على دعم إضافي أو مناقشات المجتمع؟**  
ج: زر [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) للحصول على الدعم والمناقشات مع المجتمع.

**س: هل هناك نسخة تجريبية مجانية متاحة؟**  
ج: نعم، استكشف [free trial](https://releases.aspose.com/) لتجربة قدرات Aspose.OCR.

**س: كيف يمكنني شراء Aspose.OCR لـ .NET؟**  
ج: للشراء، زر [purchase page](https://purchase.aspose.com/buy).

## الخاتمة

تهانينا! لقد تعلمت **كيفية استخراج نص الصورة C#** مع اختيار اللغة باستخدام Aspose.OCR لـ .NET. قدم لك هذا الدرس كيفية تكوين محرك OCR، اختيار اللغة المناسبة، ومعالجة النتائج، مما يمنحك أساسًا قويًا لبناء ميزات استخراج النص متعدد اللغات في تطبيقاتك.

---

**آخر تحديث:** 2026-07-23  
**تم الاختبار مع:** Aspose.OCR 24.11 for .NET  
**المؤلف:** Aspose  

{{< blocks/products/products-backtop-button >}}

## دروس ذات صلة

- [التعرف على نص الصورة باستخدام Aspose OCR لعدة لغات](/ocr/net/ocr-settings/working-with-different-languages/)
- [استخراج النص من الصور – إعدادات OCR مع Aspose.OCR](/ocr/net/ocr-settings/)
- [كيفية استخراج النص من الصورة باستخدام Aspose.OCR لـ .NET](/ocr/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}