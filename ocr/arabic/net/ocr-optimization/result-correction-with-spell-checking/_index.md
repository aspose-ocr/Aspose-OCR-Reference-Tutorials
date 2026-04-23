---
date: 2026-04-23
description: حسّن دقة التعرف الضوئي على الأحرف باستخدام Aspose OCR لـ .NET، مستفيدًا
  من التدقيق الإملائي، ودعم حزم لغات OCR، والقواميس المخصصة لتعزيز جودة OCR للمستندات
  الممسوحة ضوئيًا.
keywords:
- improve ocr accuracy
- ocr language pack
- process scanned documents
- boost ocr quality
- ocr spell checking
linktitle: تحسين دقة التعرف الضوئي على الأحرف باستخدام التدقيق الإملائي في الصور
second_title: Aspose.OCR .NET API
title: تحسين دقة التعرف الضوئي على الأحرف باستخدام التدقيق الإملائي في الصور
url: /ar/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحسين دقة OCR باستخدام التدقيق الإملائي في الصور

عند العمل مع تقنية التعرف الضوئي على الأحرف (OCR)، الهدف النهائي هو **تحسين دقة OCR** بحيث يتطابق النص المستخرج مع الصورة الأصلية تمامًا. الكلمات المكتوبة بشكل خاطئ، الخلفيات الصاخبة، والخطوط غير المعتادة هي من الأسباب الشائعة التي تقلل من جودة النتيجة. من خلال دمج محرك التدقيق الإملائي المدمج في Aspose.OCR مع حزمة اللغات الواسعة الخاصة به، يمكنك **رفع جودة OCR** بشكل كبير لأي مستند ممسوح ضوئيًا.

## كيفية تحسين دقة OCR باستخدام التدقيق الإملائي

في هذا القسم سنستعرض سير العمل الكامل — من تحميل الصورة إلى تطبيق التدقيق الإملائي وأخيرًا صقل النتيجة باستخدام قاموس مستخدم مخصص. ستشاهد أمثلة واقعية قبل وبعد، وتتعرف على أهمية ذلك في معالجة المستندات الممسوحة، وتكتشف نصائح للحصول على أقصى استفادة من ميزة التدقيق الإملائي في OCR.

## إجابات سريعة
- **ما الذي يفعله التدقيق الإملائي لـ OCR؟** يكتشف تلقائيًا الكلمات المكتوبة بشكل خاطئ في ناتج OCR ويستبدلها بأكثر البدائل صحة المحتملة.  
- **أي مكتبة توفر هذه الميزة؟** Aspose.OCR for .NET تشمل واجهة برمجة تطبيقات جاهزة للتدقيق الإملائي.  
- **هل أحتاج إلى اتصال بالإنترنت؟** لا، يعمل محرك التدقيق الإملائي بالكامل دون اتصال.  
- **هل يمكنني إضافة مصطلحاتي الخاصة؟** نعم، يمكنك تزويد القاموس المستخدم المخصص للتعامل مع الكلمات الخاصة بالمجال.  
- **ما اللغات المدعومة؟** راجع قسم “aspose ocr language support” للحصول على التفاصيل.

## ما هو التدقيق الإملائي في OCR؟

يقوم التدقيق الإملائي بفحص النص الخام الذي يُرجعه محرك OCR، ويحدد الرموز التي لا تتطابق مع الكلمات المعروفة في القاموس اللغوي المختار، ثم يقترح أو يطبق التصحيحات. هذه الخطوة أساسية **لتحسين دقة OCR**، خاصةً عند معالجة المستندات الممسوحة، الإيصالات، أو النماذج التي قد يخطئ OCR في تفسير الأحرف فيها.

## لماذا تستخدم حزمة لغة Aspose OCR؟

تأتي Aspose.OCR مع حزم لغات شاملة وتسمح لك بإضافة قواميس إضافية. الاستفادة من **aspose ocr language support** يعني أنك تستطيع التعامل مع مستندات متعددة اللغات دون كتابة محللات مخصصة، وتستفيد من قواعد خاصة بكل لغة تُحسّن جودة التعرف أكثر.

## المتطلبات المسبقة

قبل الغوص في سحر التدقيق الإملائي، تأكد من توفر المتطلبات التالية:

- Aspose.OCR for .NET Library: قم بتحميل وتثبيت مكتبة Aspose.OCR من [صفحة الإصدار](https://releases.aspose.com/ocr/net/).

- Document Directory: تأكد من وجود دليل مخصص لمستنداتك. استبدل `"Your Document Directory"` في مقتطفات الشيفرة بالمسار الفعلي.

## استيراد مساحات الأسماء

لنبدأ باستيراد مساحات الأسماء الضرورية في مشروع .NET الخاص بك:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## الخطوة 1: تهيئة Aspose.OCR

تهيئة كائن Aspose.OCR لبدء عملية OCR.

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

استرجع ناتج OCR قبل التصحيح للمقارنة مع النسخة المصححة.

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

## الخطوة 5: الكلمات غير الصحيحة واقتراحات التصحيح

احصل على قائمة بالكلمات غير الصحيحة مع الاقتراحات باستخدام الشيفرة التالية:

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

صحح نصًا محددًا قدمه المستخدم باستخدام مكتبة Aspose.OCR:

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

## نصائح لتعزيز جودة OCR

- **اختر حزمة لغة OCR الصحيحة** التي تتطابق مع المستند الأصلي. استخدام `Language.Eng` على مستند فرنسي سيقلل الدقة بشكل كبير.  
- **قم بتهيئة الصور مسبقًا** (إزالة الميل، إزالة الضوضاء، زيادة التباين) قبل تمريرها إلى محرك OCR؛ الصور النقية تنتج أخطاء إملائية أقل.  
- **حافظ على قواميس المستخدم مختصرة** — كلمة واحدة في كل سطر — حتى يتمكن المدقق الإملائي من العثور على المصطلحات المخصصة بسرعة دون إبطاء المعالجة على دفعات كبيرة.  
- **عالج الصفحات على دفعات** عند التعامل مع ملفات PDF متعددة الصفحات؛ هذا يقلل من استهلاك الذاكرة ويسرّع مرحلة التدقيق الإملائي.

## المشكلات الشائعة والحلول

| المشكلة | السبب | طريقة الحل |
|-------|----------------|------------|
| لا توجد اقتراحات مسترجعة | لم يتم تحميل حزمة اللغة أو النص قصير جدًا. | تأكد من أن `RecognitionSettings(Language.Eng)` يتطابق مع لغة الصورة المصدر وأن ناتج OCR يحتوي على عدد كافٍ من الأحرف. |
| القاموس المخصص غير مطبق | مسار غير صحيح أو تنسيق ملف غير مدعوم. | تحقق من وجود `dictionary.txt` في الموقع المحدد وأنه يستخدم كلمة واحدة في كل سطر. |
| المدقق الإملائي يبطئ المستندات الكبيرة | معالجة كل كلمة على حدة يضيف عبئًا. | عالج الصفحات على دفعات أو زد من تخصيص الذاكرة إذا كنت تستخدم .NET Core. |

## الأسئلة المتكررة

### س1: هل يمكنني استخدام Aspose.OCR للغات غير الإنجليزية؟

نعم، يدعم Aspose.OCR عدة لغات. قم بضبط إعدادات اللغة وفقًا لذلك.

### س2: كيف أدمج Aspose.OCR في مشروع .NET الخاص بي؟

راجع [التوثيق](https://reference.aspose.com/ocr/net/) للحصول على خطوات التكامل التفصيلية.

### س3: هل هناك نسخة تجريبية متاحة لـ Aspose.OCR؟

نعم، يمكنك استكشاف الميزات عبر [نسخة التجربة المجانية](https://releases.aspose.com/).

### س4: هل يمكنني رفع قاموس مخصص للتدقيق الإملائي؟

بالطبع! يوضح البرنامج التعليمي كيفية تحسين التصحيح باستخدام قاموس يقدمه المستخدم.

### س5: أين يمكنني الحصول على الدعم لـ Aspose.OCR؟

زر [منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) للحصول على دعم المجتمع والإرشادات.

---

**آخر تحديث:** 2026-04-23  
**تم الاختبار مع:** Aspose.OCR for .NET أحدث إصدار  
**المؤلف:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}