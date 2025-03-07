---
title: تصحيح النتيجة مع التدقيق الإملائي في التعرف على الصور OCR
linktitle: تصحيح النتيجة مع التدقيق الإملائي في التعرف على الصور OCR
second_title: Aspose.OCR .NET API
description: تعزيز دقة التعرف الضوئي على الحروف باستخدام Aspose.OCR لـ .NET. قم بتصحيح التهجئة وتخصيص القواميس وتحقيق التعرف على النص الخالي من الأخطاء دون عناء.
weight: 13
url: /ar/net/ocr-optimization/result-correction-with-spell-checking/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصحيح النتيجة مع التدقيق الإملائي في التعرف على الصور OCR

## مقدمة

في مجال التعرف البصري على الأحرف (OCR)، يعد تحقيق نتائج دقيقة أمرًا بالغ الأهمية لاستخراج معلومات ذات معنى من الصور. أحد التحديات الشائعة هو التعامل مع الكلمات التي بها أخطاء إملائية في عملية التعرف. ولحسن الحظ، يوفر Aspose.OCR for .NET حلاً قويًا لتحسين نتائج التعرف الضوئي على الحروف من خلال التدقيق الإملائي.

سيرشدك هذا البرنامج التعليمي خلال عملية تصحيح النتائج من خلال التدقيق الإملائي باستخدام Aspose.OCR لـ .NET. في النهاية، ستكون جاهزًا لتحسين دقة النص المشتق من تقنية التعرف الضوئي على الحروف، مما يضمن إخراجًا أكثر دقة وخاليًا من الأخطاء.

## المتطلبات الأساسية

قبل أن نتعمق في سحر التدقيق الإملائي، تأكد من توفر المتطلبات الأساسية التالية:

-  Aspose.OCR لمكتبة .NET: قم بتنزيل وتثبيت مكتبة Aspose.OCR من[صفحة الإصدار](https://releases.aspose.com/ocr/net/).

- دليل المستندات: تأكد من أن لديك دليلًا مخصصًا لمستنداتك. استبدل "دليل المستندات الخاص بك" في مقتطفات التعليمات البرمجية بالمسار الفعلي.

## استيراد مساحات الأسماء

لنبدأ باستيراد مساحات الأسماء الضرورية في مشروع .NET الخاص بك:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## الخطوة 1: تهيئة Aspose.OCR

قم بتهيئة مثيل Aspose.OCR لبدء عملية التعرف الضوئي على الحروف.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory";

// تهيئة مثيل AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## الخطوة 2: التعرف على الصورة

بعد ذلك، تعرف على النص الموجود في الصورة باستخدام Aspose.OCR. إليك مقتطف يوضح هذه العملية:

```csharp
// التعرف على الصورة
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## الخطوة 3: قبل التصحيح

قم باسترجاع نتيجة التعرف الضوئي على الحروف قبل التصحيح للمقارنة مع النسخة المصححة.

```csharp
// الحصول على النتيجة
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## الخطوة 4: بعد التصحيح

قم بتطبيق التدقيق الإملائي للحصول على النتيجة الصحيحة. يوضح مقتطف الكود التالي هذه الخطوة:

```csharp
// الحصول على النتيجة المصححة
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## الخطوة 5: الكلمات والاقتراحات التي بها أخطاء إملائية

احصل على قائمة بالكلمات التي بها أخطاء إملائية مع التصحيحات المقترحة باستخدام الكود التالي:

```csharp
// الحصول على قائمة الكلمات التي بها أخطاء إملائية مع الاقتراحات
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## الخطوة 6: تصحيح نص المستخدم

قم بتصحيح النص المحدد المقدم من المستخدم باستخدام مكتبة Aspose.OCR:

```csharp
// تصحيح نص المستخدم
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## الخطوة 7: التصحيح باستخدام قاموس المستخدم

تعزيز التصحيح بشكل أكبر من خلال دمج قاموس المستخدم المخصص:

```csharp
// الحصول على النتيجة المصححة مع قاموس المستخدم
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## خاتمة

تهانينا! لقد نجحت في التنقل بين إمكانيات التدقيق الإملائي لـ Aspose.OCR لـ .NET. تمكنك هذه الميزة من تحسين نتائج التعرف الضوئي على الحروف، مما يضمن الدقة والقضاء على الأخطاء.

## الأسئلة الشائعة

### س1: هل يمكنني استخدام Aspose.OCR للغات أخرى غير الإنجليزية؟

A1: نعم، يدعم Aspose.OCR لغات متعددة. اضبط إعدادات اللغة وفقًا لذلك.

### س٢: كيف يمكنني دمج Aspose.OCR في مشروع .NET الخاص بي؟

 ج2: راجع[توثيق](https://reference.aspose.com/ocr/net/) للحصول على خطوات التكامل التفصيلية.

### س3: هل هناك إصدار تجريبي متاح لـ Aspose.OCR؟

 ج3: نعم، يمكنك استكشاف الميزات باستخدام[نسخة تجريبية مجانية](https://releases.aspose.com/).

### س4: هل يمكنني تحميل قاموس مخصص للتدقيق الإملائي؟

ج4: بالتأكيد! يوضح البرنامج التعليمي كيفية تحسين التصحيح باستخدام القاموس المقدم من المستخدم.

### س5: أين يمكنني طلب الدعم لـ Aspose.OCR؟

 ج5: قم بزيارة[منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) لدعم المجتمع وتوجيهه.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
