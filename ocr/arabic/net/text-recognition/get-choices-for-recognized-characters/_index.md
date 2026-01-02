---
date: 2026-01-02
description: تعلم كيفية الحصول على خيارات الأحرف في تقنية OCR باستخدام Aspose.OCR
  لـ .NET. يوضح هذا الدليل خطوة بخطوة كيفية استرجاع بدائل الأحرف في التعرف على الصور.
linktitle: Get Choices for Recognized Characters in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: كيفية الحصول على خيارات الأحرف في OCR للأحرف المعترف بها في التعرف على الصور
url: /ar/net/text-recognition/get-choices-for-recognized-characters/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# الحصول على خيارات الأحرف المعترف بها في التعرف على الصور باستخدام OCR

## المقدمة

اكتشف قوة تقنية التعرف الضوئي على الأحرف (OCR) في تطبيقات .NET الحديثة، وتعلم **كيفية الحصول على خيارات أحرف OCR** لكل رمز تم التعرف عليه. تجعل مكتبة Aspose.OCR لـ .NET هذه العملية بسيطة، حيث لا تحصل فقط على النص الأكثر احتمالًا بل أيضًا على الأحرف البديلة التي نظر فيها المحرك. بنهاية هذا الدرس ستتمكن من دمج هذه الميزة في أي مشروع C# وتحسين التعامل مع الأحرف غير الواضحة.

## إجابات سريعة
- **ماذا يعني “الحصول على خيارات أحرف OCR”؟** يُعيد قائمة بالأحرف البديلة لكل حرف تم التعرف عليه.  
- **لماذا نستخدم خيارات الأحرف؟** للتعامل مع التعرف غير المؤكد، إجراء ما بعد المعالجة، أو تنفيذ تحقق مخصص.  
- **ماذا أحتاج مسبقًا؟** بيئة تطوير .NET، Visual Studio، ومكتبة Aspose.OCR لـ .NET.  
- **هل يلزم ترخيص؟** نسخة تجريبية مجانية تكفي للاختبار؛ يلزم الحصول على ترخيص تجاري للإنتاج.  
- **هل يمكن تشغيلها على .NET Core / .NET 6؟** نعم، تدعم Aspose.OCR جميع إصدارات .NET الحديثة.

## ما هو “الحصول على خيارات أحرف OCR”؟
عند تحليل محرك OCR لصورة، قد يتطابق نمط البكسل مع عدة أحرف محتملة. تُظهر واجهة برمجة التطبيقات **get OCR character choices** هذه البدائل، مما يتيح للمطورين اختيار الحرف الأنسب حسب السياق.

## لماذا نستخدم Aspose.OCR لـ .NET؟
- **دقة عالية** عبر العديد من اللغات والخطوط.  
- **تكامل سهل** من خلال واجهة برمجة تطبيقات C# بسيطة.  
- **الوصول إلى بدائل الأحرف** عبر `RecognitionCharactersList`.  
- **بدون تبعيات خارجية** – يعمل مباشرة على Windows وLinux وmacOS.

## المتطلبات المسبقة

قبل الخوض في الدرس، تأكد من توفر المتطلبات التالية:

- معرفة أساسية بـ C# وتطوير .NET.  
- تثبيت Visual Studio على جهازك.  
- مكتبة Aspose.OCR لـ .NET، والتي يمكنك تحميلها من [هنا](https://releases.aspose.com/ocr/net/).

## استيراد المساحات الاسمية

في مشروع C# الخاص بك، ابدأ باستيراد المساحات الاسمية الضرورية:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## الخطوة 1: تهيئة Aspose.OCR

ابدأ بتهيئة كائن Aspose.OCR:

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## الخطوة 2: تحديد مسار الصورة

عيّن المسار الخاص بالصورة التي تريد تحليلها:

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## الخطوة 3: التعرف على الصورة

نفّذ عملية التعرف على الصورة:

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    // Default or custom settings
});
```

## نظرة عامة على الحصول على خيارات أحرف OCR

الآن بعد أن تم التعرف على الصورة، يمكنك استرجاع قائمة بدائل الأحرف التي نظر فيها محرك OCR لكل موضع.

## الخطوة 4: الحصول على خيارات الأحرف المعترف بها

استرجع الخيارات للأحرف المعترف بها:

```csharp
List<char[]> resultWithChoices = result.RecognitionCharactersList;
```

## الخطوة 5: طباعة النتائج

اعرض نص التعرف والخيارات:

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Choices:");
resultWithChoices.ForEach(a => Console.WriteLine($"character: {a[0]} . Choices: {a[1]} {a[2]} {a[3]} {a[4]}"));

Console.WriteLine("GetChoiceForRecognizedCharacters executed successfully");
```

كرر هذه الخطوات، مع تخصيصها وفقًا لمتطلبات تطبيقك.

## المشكلات الشائعة والحلول

- **قائمة `RecognitionCharactersList` فارغة** – تأكد من أن الصورة ذات دقة وتباين كافيين.  
- **أحرف غير متوقعة** – اضبط `RecognitionSettings` (مثل اللغة أو القاموس) لتحسين الدقة.  
- **مشكلات الأداء** – عالج الصور بشكل غير متزامن أو اجمع عدة صور في دفعة واحدة للحفاظ على استجابة الواجهة.

## الأسئلة المتكررة

### س1: هل Aspose.OCR لـ .NET مناسب لمعالجة المستندات على نطاق واسع؟

ج1: بالتأكيد! تم تصميم Aspose.OCR لـ .NET للتعامل مع كميات كبيرة من المستندات بكفاءة ودقة.

### س2: هل يمكنني استخدام Aspose.OCR لـ .NET في تطبيق ويب؟

ج2: نعم، يمكنك دمج Aspose.OCR لـ .NET في تطبيقات الويب، مما يجعله مرنًا لمختلف سيناريوهات التطوير.

### س3: هل هناك خيارات ترخيص متاحة لـ Aspose.OCR لـ .NET؟

ج3: نعم، يمكنك استكشاف خيارات الترخيص وإجراء الشراء من [هنا](https://purchase.aspose.com/buy).

### س4: كيف يمكنني الحصول على الدعم أو طرح أسئلة حول Aspose.OCR لـ .NET؟

ج4: زر منتدى [Aspose.OCR](https://forum.aspose.com/c/ocr/16) للحصول على الدعم، طرح الأسئلة، والتواصل مع المجتمع.

### س5: هل تتوفر نسخة تجريبية مجانية لـ Aspose.OCR لـ .NET؟

ج5: نعم، يمكنك الوصول إلى نسخة تجريبية مجانية من [هنا](https://releases.aspose.com/) لتجربة إمكانيات Aspose.OCR لـ .NET.

## الخاتمة

في هذا الدرس، استعرضنا كيفية **الحصول على خيارات أحرف OCR** باستخدام Aspose.OCR لـ .NET. تضيف هذه الميزة بُعدًا جديدًا لإمكانات OCR الخاصة بك، مما يتيح معالجة أذكى للأحرف غير الواضحة ومنطق ما بعد المعالجة الأكثر غنى.

---

**آخر تحديث:** 2026-01-02  
**تم الاختبار مع:** Aspose.OCR 24.11 لـ .NET  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}