---
date: 2025-12-27
description: تعلم كيفية استخدام تحويل الصورة إلى نص باستخدام Aspose.OCR لـ .NET، مع
  تحديد الأحرف المسموح بها وضبط إعدادات التعرف على النص بدقة. يتضمن كودًا للتعرف على
  صورة الأرقام.
linktitle: 'ocr image to text: Specify Allowed Characters in OCR'
second_title: Aspose.OCR .NET API
title: 'تحويل صورة إلى نص باستخدام OCR: تحديد الأحرف المسموح بها في OCR'
url: /ar/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل صورة إلى نص: تحديد الأحرف المسموح بها في OCR

## مقدمة

في المشهد المتطور باستمرار للتكنولوجيا، أصبح التعرف الضوئي على الأحرف (OCR) – أو تحويل **ocr image to text** – أداة تحويلية، تمكّن الآلات من فهم النص من الصور. تبرز Aspose.OCR لـ .NET كحل قوي، يوفر دمجًا سلسًا للمطورين الذين يبحثون عن قدرات OCR قوية في تطبيقاتهم على .NET.

## إجابات سريعة
- **ما الذي يفعله “Specify Allowed Characters”؟** يقيد مخرجات OCR إلى مجموعة محددة من الرموز، مثل الأرقام فقط.  
- **ما الطريقة التي تستخرج سطرًا واحدًا من النص؟** `RecognizeLine` returns the first line it detects.  
- **هل يمكنني تغيير إعدادات التعرف على OCR أثناء التشغيل؟** نعم – استخدم `RecognitionSettings` لضبط الخيارات مثل `AllowedCharacters`.  
- **هل تتوفر نسخة تجريبية؟** بالطبع، قم بتحميل النسخة التجريبية المجانية من موقع Aspose.  
- **ما إصدارات .NET المدعومة؟** جميع إصدارات .NET Framework الحديثة و .NET Core/5/6.

## المتطلبات المسبقة

قبل الغوص في البرنامج التعليمي، تأكد من توفر المتطلبات التالية:

- معرفة عملية بتطوير .NET.  
- مكتبة Aspose.OCR لـ .NET. يمكنك تحميلها [هنا](https://releases.aspose.com/ocr/net/).  
- الإلمام بـ Visual Studio أو أي بيئة تطوير .NET مفضلة أخرى.

## استيراد مساحات الأسماء

في مشروع .NET الخاص بك، استورد مساحات الأسماء اللازمة للاستفادة من وظائف Aspose.OCR لـ .NET بفعالية:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

الآن، لنقسم البرنامج التعليمي إلى سلسلة من الخطوات الشاملة:

## الخطوة 1: تحديد الأحرف المسموح بها في ocr image to text

للبدء، قم بإعداد المسار إلى دليل المستندات الخاص بك:

```csharp
string dataDir = "Your Document Directory";
```

## الخطوة 2: تهيئة Aspose.OCR بالرموز المسموح بها (التعرف على صورة أرقام)

أنشئ مثيلًا من `AsposeOcr`، محددًا الرموز المسموح بها. في هذه الحالة، نسمح بالأرقام (0‑9) فقط:

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## الخطوة 3: التعرف على الصورة

استخدم مثيل `AsposeOcr` للتعرف على النص من صورة:

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## الخطوة 4: عرض النص المعترف به

اطبع النص المعترف به إلى وحدة التحكم:

```csharp
Console.WriteLine(result);
```

## الخطوة 5: الحالة الثانية – التعرف على صورة بإعدادات OCR المحددة

تهيئة مثيل آخر من `AsposeOcr`، هذه المرة بإعدادات أكثر تحديدًا توضح استخدام **ocr recognition settings**:

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## الخطوة 6: عرض النص المعترف به في الحالة الثانية

اطبع النص المعترف به من الحالة الثانية إلى وحدة التحكم:

```csharp
Console.WriteLine(result2.RecognitionText);
```

## الخطوة 7: تنفيذ ناجح

أخيرًا، أكد التنفيذ الناجح للبرنامج التعليمي **SpecifyAllowedCharacters**:

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

باتباعك هذه الخطوات، لقد فتحت القدرة على **specify allowed characters** في التعرف على الصور باستخدام OCR باستخدام Aspose.OCR لـ .NET، مما يتيح تحويلًا دقيقًا من **ocr image to text** للسيناريوهات التي تقتصر على الأرقام فقط.

## لماذا نستخدم تصفية الأحرف المسموح بها؟

- **دقة أعلى:** تقييد مجموعة الأحرف يقلل من التعرف الخاطئ، خاصةً في الصور الضوضائية.  
- **تحسين الأداء:** يتخطى محرك OCR الرموز غير ذات الصلة، مما يسرّع المعالجة.  
- **الامتثال:** يفرض تنسيقات البيانات (مثل أرقام الفواتير، الرموز التسلسلية) مباشرةً في مرحلة OCR.

## المشكلات الشائعة والنصائح

- **المشكلة:** توفير سلسلة فارغة للأحرف المسموح بها يعطل التصفية.  
  **النصيحة:** دائمًا مرّر سلسلة غير فارغة أو استخدم تعداد `CharactersAllowedType`.  
- **المشكلة:** استخدام `RecognizeLine` على مستندات متعددة الأسطر قد يفوت البيانات.  
  **النصيحة:** انتقل إلى `RecognizeImage` مع `RecognizeSingleLine = false` لاستخراج الصفحة بالكامل.  
- **المشكلة:** نسيان دمج مسار الدليل بشكل صحيح قد يسبب `FileNotFoundException`.  
  **النصيحة:** استخدم `Path.Combine(dataDir, "file.jpg")` لمسارات مستقلة عن النظام.

## الأسئلة المتكررة

**س: هل Aspose.OCR لـ .NET مناسب لكل من المبتدئين والمطورين ذوي الخبرة؟**  
ج: بالطبع! الـ API بديهية للمبتدئين وتوفر إعدادات متقدمة للمستخدمين المتقدمين.

**س: هل يمكنني استخدام Aspose.OCR لـ .NET للتعرف على الأحرف بعدة لغات؟**  
ج: نعم، يدعم Aspose.OCR مجموعة واسعة من اللغات؛ يمكنك أيضًا دمج حزم اللغات للمشاريع متعددة اللغات.

**س: كم مرة يتم تحديث Aspose.OCR لـ .NET؟**  
ج: يتم إصدار التحديثات بانتظام لمواكبة إصدارات .NET الجديدة وتحسينات OCR. راجع [documentation](https://reference.aspose.com/ocr/net/) للحصول على أحدث نسخة.

**س: هل تتوفر نسخة تجريبية مجانية لـ Aspose.OCR لـ .NET؟**  
ج: نعم، يمكنك استكشاف القدرات بتحميل [free trial](https://releases.aspose.com/).

**س: أين يمكنني طلب المساعدة أو التواصل مع المجتمع للحصول على الدعم؟**  
ج: زر [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) للتفاعل مع الخبراء والمطورين الآخرين.

---

**آخر تحديث:** 2025-12-27  
**تم الاختبار مع:** Aspose.OCR 24.11 for .NET  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}