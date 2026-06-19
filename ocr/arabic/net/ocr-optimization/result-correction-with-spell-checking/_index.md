---
date: 2026-04-29
description: حسّن دقة التعرف الضوئي على الأحرف وتعلّم كيفية التعرف على النص من الصورة
  باستخدام Aspose OCR لـ .NET، مستفيدًا من التدقيق الإملائي ودعم اللغات لتصحيح الأخطاء
  الإملائية وتخصيص القواميس.
keywords:
- improve ocr accuracy
- recognize text from image
- Aspose OCR spell checking
- custom OCR dictionary
linktitle: تحسين دقة التعرف الضوئي على الأحرف باستخدام التدقيق الإملائي في الصور
second_title: Aspose.OCR .NET API
title: تحسين دقة التعرف الضوئي على الأحرف باستخدام التدقيق الإملائي في الصور
url: /ar/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحسين دقة OCR مع التدقيق الإملائي في الصور

عند العمل مع التعرف الضوئي على الأحرف (OCR)، الهدف النهائي هو **تحسين دقة OCR** بحيث يتطابق النص المستخرج مع الصورة الأصلية تمامًا. الكلمات المكتوبة بشكل خاطئ هي مصدر شائع للأخطاء، خاصة عندما تكون الصورة المصدر مشوشة أو تحتوي على خطوط غير عادية. تقدم Aspose.OCR لـ .NET قدرات تدقيق إملائي مدمجة لا تصحح هذه الأخطاء فحسب، بل تتيح لك أيضًا توسيع المحرك بقواميس مخصصة. في هذا البرنامج التعليمي ستتعلم كيفية استخدام التدقيق الإملائي لتعزيز نتائج OCR، وسترى المخرجات قبل وبعد، وتكتشف كيفية تخصيص عملية التصحيح وفقًا لاحتياجات لغتك المحددة.

## إجابات سريعة
- **ماذا يفعل التدقيق الإملائي لـ OCR؟** يكتشف تلقائيًا الكلمات المكتوبة بشكل خاطئ في مخرجات OCR ويستبدلها بالبدائل الصحيحة الأكثر احتمالًا.  
- **أي مكتبة توفر هذه الميزة؟** Aspose.OCR for .NET يتضمن واجهة برمجة تطبيقات تدقيق إملائي جاهزة للاستخدام.  
- **هل أحتاج إلى اتصال بالإنترنت؟** لا، يعمل محرك التدقيق الإملائي بالكامل دون اتصال.  
- **هل يمكنني إضافة مصطلحاتي الخاصة؟** نعم، يمكنك توفير قاموس مستخدم مخصص للتعامل مع الكلمات الخاصة بالمجال.  
- **كيف يساعدني ذلك في التعرف على النص من الصورة؟** من خلال تصحيح الأخطاء التي يولدها OCR، يصبح النص النهائي نظيفًا وجاهزًا للمعالجة اللاحقة.

## ما هو التدقيق الإملائي في OCR؟
يفحص التدقيق الإملائي النص الخام الذي تُعيده محرك OCR، يحدد الرموز التي لا تتطابق مع الكلمات المعروفة في القاموس اللغوي المختار، ويقترح أو يطبق التصحيحات. هذه الخطوة أساسية لـ **تحسين دقة OCR**، خاصةً عند معالجة المستندات الممسوحة ضوئيًا أو الإيصالات أو النماذج التي قد يفسر فيها OCR الأحرف بشكل خاطئ.

## لماذا تستخدم دعم لغة Aspose OCR؟
يأتي Aspose.OCR مع حزم لغات شاملة ويسمح لك بإضافة قواميس إضافية. الاستفادة من **دعم لغة Aspose OCR** يعني أنك تستطيع التعامل مع مستندات متعددة اللغات دون كتابة محللات مخصصة، وتتمكن من الوصول إلى قواعد خاصة باللغات تُحسن جودة التعرف بشكل إضافي.

## متى تكون تحسين دقة OCR مهمًا أكثر؟
- **المستندات القانونية ومتطلبات الامتثال** حيث يمكن لخطأ إملائي واحد أن يغير المعنى.  
- **خطوط استخراج البيانات** التي تغذي نتائج OCR إلى التحليلات أو نماذج الذكاء الاصطناعي.  
- **التطبيقات الموجهة للعملاء** مثل الماسحات الضوئية المحمولة التي يجب أن تُعيد نصًا قابلاً للقراءة فورًا.  

## المتطلبات المسبقة

قبل أن نغوص في سحر التدقيق الإملائي، تأكد من أن لديك المتطلبات المسبقة التالية جاهزة:

- Aspose.OCR for .NET Library: قم بتنزيل وتثبيت مكتبة Aspose.OCR من [صفحة الإصدار](https://releases.aspose.com/ocr/net/).
- Document Directory: تأكد من وجود دليل مخصص لمستنداتك. استبدل `"Your Document Directory"` في مقتطفات الشيفرة بالمسار الفعلي.

## استيراد مساحات الأسماء

لنبدأ باستيراد مساحات الأسماء الضرورية في مشروع .NET الخاص بك:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## الخطوة 1: تهيئة Aspose.OCR

قم بتهيئة كائن Aspose.OCR لبدء عملية OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## الخطوة 2: التعرف على الصورة

بعد ذلك، تعرف على النص في صورة باستخدام Aspose.OCR. إليك مقتطف يوضح هذه العملية:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## الخطوة 3: قبل التصحيح

احصل على نتيجة OCR قبل التصحيح للمقارنة مع النسخة المصححة.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## الخطوة 4: بعد التصحيح

طبق التدقيق الإملائي للحصول على النتيجة المصححة. يوضح مقتطف الشيفرة التالي هذه الخطوة:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## الخطوة 5: الكلمات المكتوبة خطأ والاقتراحات

احصل على قائمة بالكلمات المكتوبة خطأ مع الاقتراحات التصحيحية باستخدام الشيفرة التالية:

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

## المشكلات الشائعة والحلول

| المشكلة | سبب حدوثه | كيفية الإصلاح |
|-------|----------------|------------|
| لم يتم إرجاع اقتراحات | حزمة اللغة غير محملة أو النص قصير جدًا. | تأكد من أن `RecognitionSettings(Language.Eng)` يتطابق مع لغة الصورة المصدر وأن نتيجة OCR تحتوي على عدد كافٍ من الأحرف. |
| القاموس المخصص غير مُطبق | مسار غير صحيح أو تنسيق ملف غير صحيح. | تحقق من وجود `dictionary.txt` في الموقع المحدد وأنه يستخدم كلمة واحدة في كل سطر. |
| التدقيق الإملائي يبطئ المستندات الكبيرة | معالجة كل كلمة على حدة يضيف عبءً إضافيًا. | عالج الصفحات على دفعات أو زد تخصيص الذاكرة إذا كنت تعمل على .NET Core. |

## الأسئلة المتكررة

**Q1: هل يمكنني استخدام Aspose.OCR للغات غير الإنجليزية؟**  
A1: نعم، يدعم Aspose.OCR عدة لغات. اضبط إعدادات اللغة وفقًا لذلك.

**Q2: كيف يمكنني دمج Aspose.OCR في مشروع .NET الخاص بي؟**  
A2: ارجع إلى [documentation](https://reference.aspose.com/ocr/net/) للحصول على خطوات التكامل التفصيلية.

**Q3: هل هناك نسخة تجريبية متاحة لـ Aspose.OCR؟**  
A3: نعم، يمكنك استكشاف الميزات من خلال [نسخة تجريبية مجانية](https://releases.aspose.com/).

**Q4: هل يمكنني رفع قاموس مخصص للتدقيق الإملائي؟**  
A4: بالطبع! يوضح البرنامج التعليمي كيفية تحسين التصحيح باستخدام قاموس يقدمه المستخدم.

**Q5: أين يمكنني طلب الدعم لـ Aspose.OCR؟**  
A5: زر [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) للحصول على دعم المجتمع والإرشاد.

---

**آخر تحديث:** 2026-04-29  
**تم الاختبار مع:** Aspose.OCR for .NET latest version  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}