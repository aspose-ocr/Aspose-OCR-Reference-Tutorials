---
date: 2025-12-25
description: حسّن دقة التعرف الضوئي على الأحرف باستخدام Aspose OCR لـ .NET، مستفيدًا
  من تدقيق الإملاء ودعم اللغات لتصحيح الأخطاء الإملائية وتخصيص القواميس لضمان التعرف
  على النص دون أخطاء.
linktitle: Improve OCR Accuracy with Spell Checking in Images
second_title: Aspose.OCR .NET API
title: تحسين دقة التعرف الضوئي على الحروف باستخدام التدقيق الإملائي في الصور
url: /ar/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحسين دقة OCR باستخدام التدقيق الإملائي في الصور

## المقدمة

عند العمل مع تقنية التعرف الضوئي على الأحرف (OCR)، الهدف النهائي هو **تحسين دقة OCR** بحيث يتطابق النص المستخرج مع الصورة الأصلية تمامًا. الكلمات المكتوبة بشكل خاطئ هي مصدر شائع للأخطاء، خاصةً عندما تكون الصورة المصدر ذات ضوضاء أو تحتوي على خطوط غير معتادة. تقدم Aspose.OCR لـ .NET قدرات تدقيق إملائي مدمجة لا تصحح هذه الأخطاء فحسب، بل تسمح لك أيضًا بتمديد المحرك باستخدام قواميس مخصصة. في هذا الدرس ستتعلم كيفية استخدام التدقيق الإملائي لتعزيز نتائج OCR، ومشاهدة النتيجة قبل وبعد، واكتشاف كيفية تخصيص عملية التصحيح وفقًا لاحتياجات لغتك المحددة.

## إجابات سريعة
- **ما الذي يفعله التدقيق الإملائي لـ OCR؟** يكتشف تلقائيًا الكلمات المكتوبة بشكل خاطئ في ناتج OCR ويستبدلها بالبدائل الأكثر احتمالًا.  
- **أي مكتبة توفر هذه الميزة؟** Aspose.OCR for .NET تتضمن واجهة برمجة تطبيقات تدقيق إملائي جاهزة للاستخدام.  
- **هل أحتاج إلى اتصال بالإنترنت؟** لا، يعمل محرك التدقيق الإملائي بالكامل دون اتصال.  
- **هل يمكنني إضافة مصطلحاتي الخاصة؟** نعم، يمكنك توفير قاموس مستخدم مخصص للتعامل مع الكلمات الخاصة بالمجال.  
- **ما اللغات المدعومة؟** راجع قسم “aspose ocr language support” للحصول على التفاصيل.

## ما هو التدقيق الإملائي في OCR؟

يقوم التدقيق الإملائي بفحص النص الخام الذي يُعيده محرك OCR، ويحدد الرموز التي لا تتطابق مع الكلمات المعروفة في القاموس اللغوي المختار، ويقترح أو يطبق التصحيحات. هذه الخطوة أساسية لـ **تحسين دقة OCR**، خاصةً عند معالجة المستندات الممسوحة ضوئيًا أو الإيصالات أو النماذج التي قد يفسر OCR فيها الأحرف بشكل غير صحيح.

## لماذا تستخدم دعم لغات Aspose OCR؟

تأتي Aspose.OCR مع حزم لغات واسعة وتسمح لك بإضافة قواميس إضافية. الاستفادة من **aspose ocr language support** يعني أنك تستطيع التعامل مع مستندات متعددة اللغات دون الحاجة إلى كتابة محللات مخصصة، وتتمكن من الوصول إلى قواعد خاصة باللغات تُحسن جودة التعرف بشكل إضافي.

## المتطلبات المسبقة

قبل أن نغوص في سحر التدقيق الإملائي، تأكد من توفر المتطلبات التالية:

- مكتبة Aspose.OCR لـ .NET: قم بتنزيل وتثبيت مكتبة Aspose.OCR من [صفحة الإصدار](https://releases.aspose.com/ocr/net/).
- دليل المستندات: تأكد من وجود دليل مخصص لمستنداتك. استبدل `"Your Document Directory"` في مقتطفات الشيفرة بالمسار الفعلي.

## استيراد مساحات الأسماء

لنبدأ باستيراد مساحات الأسماء الضرورية في مشروع .NET الخاص بك:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## الخطوة 1: تهيئة Aspose.OCR

قم بتهيئة مثيل من Aspose.OCR لبدء عملية OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## الخطوة 2: التعرف على الصورة

بعد ذلك، قم بالتعرف على النص في صورة باستخدام Aspose.OCR. إليك مقتطف يوضح هذه العملية:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## الخطوة 3: قبل التصحيح

استرجع نتيجة OCR قبل التصحيح للمقارنة مع النسخة المصححة.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## الخطوة 4: بعد التصحيح

طبق التدقيق الإملائي للحصول على النتيجة المصححة. يوضح المقتطف التالي هذه الخطوة:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## الخطوة 5: الكلمات المكتوبة خطأ والاقتراحات

احصل على قائمة بالكلمات المكتوبة بشكل خاطئ مع الاقتراحات التصحيحية باستخدام الشيفرة التالية:

```csharp
// Get list of misspelled words with suggestions
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

قم بتصحيح نص معين مقدم من المستخدم باستخدام مكتبة Aspose.OCR:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## الخطوة 7: التصحيح باستخدام قاموس المستخدم

عزز عملية التصحيح أكثر بدمج قاموس مستخدم مخصص:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## المشكلات الشائعة والحلول

| المشكلة | لماذا يحدث | كيفية الإصلاح |
|---------|------------|----------------|
| لم يتم إرجاع اقتراحات | حزمة اللغة غير محملة أو النص قصير جدًا. | تأكد من أن `RecognitionSettings(Language.Eng)` يتطابق مع لغة الصورة المصدر وأن نتيجة OCR تحتوي على عدد كافٍ من الأحرف. |
| لم يتم تطبيق القاموس المخصص | مسار غير صحيح أو تنسيق ملف غير صحيح. | تحقق من وجود `dictionary.txt` في الموقع المحدد وأنه يستخدم كلمة واحدة في كل سطر. |
| التدقيق الإملائي يبطئ المستندات الكبيرة | معالجة كل كلمة على حدة يضيف عبءً إضافيًا. | قم بمعالجة الصفحات على دفعات أو زد تخصيص الذاكرة إذا كنت تعمل على .NET Core. |

## الأسئلة المتكررة

### س1: هل يمكنني استخدام Aspose.OCR للغات غير الإنجليزية؟

ج1: نعم، يدعم Aspose.OCR عدة لغات. قم بضبط إعدادات اللغة وفقًا لذلك.

### س2: كيف يمكنني دمج Aspose.OCR في مشروع .NET الخاص بي؟

ج2: راجع [التوثيق](https://reference.aspose.com/ocr/net/) للحصول على خطوات التكامل التفصيلية.

### س3: هل هناك نسخة تجريبية متاحة لـ Aspose.OCR؟

ج3: نعم، يمكنك استكشاف الميزات من خلال [نسخة التجربة المجانية](https://releases.aspose.com/).

### س4: هل يمكنني رفع قاموس مخصص للتدقيق الإملائي؟

ج4: بالتأكيد! يوضح الدرس كيفية تحسين التصحيح باستخدام قاموس يقدمه المستخدم.

### س5: أين يمكنني الحصول على الدعم لـ Aspose.OCR؟

ج5: زر [منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) للحصول على دعم المجتمع والإرشاد.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**آخر تحديث:** 2025-12-25  
**تم الاختبار مع:** Aspose.OCR for .NET أحدث إصدار  
**المؤلف:** Aspose