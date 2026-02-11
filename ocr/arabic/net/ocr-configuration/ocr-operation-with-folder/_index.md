---
date: 2025-12-21
description: تعلم كيفية استخراج النص من الصور باستخدام Aspose.OCR لـ .NET، مما يتيح
  التعرف الضوئي على النص في الصور على أساس المجلدات.
linktitle: OCROperation with Folder in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: استخراج النص من الصور باستخدام عملية OCR على المجلدات
url: /ar/net/ocr-configuration/ocr-operation-with-folder/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصور باستخدام عملية OCR على المجلدات

## المقدمة

مرحبًا بك في عالم التعرف الضوئي على الحروف (OCR) مع **Aspose.OCR for .NET**! إذا كنت بحاجة إلى **استخراج النص من الصور** بشكل جماعي—مثلاً، مجلد كامل من المستندات الممسوحة ضوئيًا—ستقودك هذه الدورة التعليمية عبر حل عملي وواقعي. سنغطي كل شيء من إعداد المشروع إلى طباعة النص المُعترف به، حتى تتمكن من دمج OCR القائم على المجلدات بسرعة في تطبيقات C# الخاصة بك.

## إجابات سريعة
- **ماذا تعلمنا في هذه الدورة؟** كيفية استخراج النص من الصور المخزنة في مجلد باستخدام Aspose.OCR.  
- **ما اللغة والمنصة؟** C# مع .NET (Framework أو .NET Core).  
- **المتطلب الأساسي؟** مكتبة Aspose.OCR for .NET (رابط التحميل أدناه).  
- **كم عدد أسطر الشيفرة؟** سبعة كتل شيفرة مختصرة فقط.  
- **هل يمكنني تحويل الصور إلى نص؟** نعم—هذا المثال يوضح ذلك بالضبط.

## ما هو “استخراج النص من الصور”؟
استخراج النص من الصور يعني استخدام تقنية OCR لقراءة الأحرف المدمجة في الصور أو ملفات PDF أو المستندات الممسوحة ضوئيًا وتحويلها إلى سلاسل قابلة للتحرير والبحث. توفر Aspose.OCR محركًا قويًا يدعم صيغ صور متعددة ولغات مختلفة.

## لماذا نستخدم Aspose.OCR لعملية OCR على المجلدات؟
- **دقة عالية** مع اكتشاف اللغة المدمج.  
- **معالجة دفعات** عبر `RecognizeMultipleImages`، مثالية للمجلدات.  
- **واجهة برمجة تطبيقات بسيطة** تتكامل بسلاسة مع مشاريع C#.  
- **قابلة للتوسع** – تعمل على كل من بيئات سطح المكتب والخوادم.

## المتطلبات المسبقة

- إتقان أساسي للغة C# وتطوير .NET.  
- Visual Studio (أي إصدار حديث).  
- مكتبة **Aspose.OCR for .NET** – حمّلها [هنا](https://releases.aspose.com/ocr/net/).  
- فهم لمفاهيم OCR (اختياري لكنه مفيد).

## استيراد المساحات الاسمية

أضف توجيهات `using` المطلوبة في أعلى ملف C# الخاص بك حتى يعرف المترجم أين يجد فئات OCR.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## دليل خطوة بخطوة

### الخطوة 1: تعيين دليل المستند
حدد المجلد الذي يحتوي على الصور التي تريد معالجتها.

```csharp
// ExStart:1   
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

> **نصيحة احترافية:** استخدم مسارًا مطلقًا أو `Path.Combine` لتجنب مشاكل فواصل المسار على أنظمة تشغيل مختلفة.

### الخطوة 2: تهيئة Aspose.OCR
أنشئ نسخة من محرك OCR.

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### الخطوة 3: تحديد مسار الصورة
وجه الـ API إلى المجلد الفرعي المحدد الذي يحتوي على ملفات الصور.

```csharp
// Image Path
string fullPath = dataDir + "OCR";
```

> **لماذا هذا مهم:** طريقة `RecognizeMultipleImages` تتوقع مسار مجلد، وليس ملفًا واحدًا.

### الخطوة 4: التعرف على الصور
نفّذ OCR على كل صورة داخل المجلد. يمكنك تخصيص `RecognitionSettings` إذا احتجت إلى تلميحات لغة أو معالجة مسبقة معينة.

```csharp
// Recognize image           
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //default or custom
});
```

### الخطوة 5: طباعة النتائج
تجول في مصفوفة `RecognitionResult` المسترجعة واطبع النص المستخرج.

```csharp
// Print result
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

> **خطأ شائع:** نسيان التحقق من `result.Length` قد يسبب استثناء `IndexOutOfRangeException` عندما يكون المجلد فارغًا. احرص دائمًا على التحقق من محتوى المجلد أولًا.

### الخطوة 6: رسالة الانتهاء
أظهر رسالة تشير إلى نجاح التنفيذ.

```csharp
// ExEnd:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|-------|-----|
| لا يوجد إخراج | مسار المجلد غير صحيح أو فارغ | تحقق من أن `fullPath` يشير إلى الدليل الصحيح ويحتوي على صيغ الصور المدعومة (PNG, JPEG, TIFF). |
| حروف غير مفهومة | إعدادات اللغة غير صحيحة | مرّر `RecognitionSettings` مكوّنة مع تعيين `Language` إلى رمز ISO المناسب. |
| بطء الأداء عند وجود العديد من الصور | المعالجة المتسلسلة على خيط واجهة المستخدم | شغّل OCR على خيط خلفي أو استخدم نمط غير متزامن للحفاظ على استجابة واجهة المستخدم. |

## الأسئلة المتكررة

**س: هل يمكنني استخدام Aspose.OCR لـ .NET في المشاريع التجارية؟**  
ج: نعم، Aspose.OCR لـ .NET هو منتج تجاري. للحصول على معلومات الترخيص، زر [here](https://purchase.aspose.com/buy).

**س: هل هناك نسخة تجريبية مجانية متاحة؟**  
ج: نعم، يمكنك تجربة نسخة تجريبية مجانية [here](https://releases.aspose.com/).

**س: أين يمكنني العثور على الوثائق؟**  
ج: الوثائق متاحة [here](https://reference.aspose.com/ocr/net/).

**س: كيف يمكنني الحصول على ترخيص مؤقت؟**  
ج: يمكن الحصول على تراخيص مؤقتة [here](https://purchase.aspose.com/temporary-license/).

**س: هل تحتاج إلى دعم أو لديك أسئلة؟**  
ج: زر منتدى [Aspose.OCR](https://forum.aspose.com/c/ocr/16) للحصول على دعم المجتمع.

---

**آخر تحديث:** 2025-12-21  
**تم الاختبار مع:** Aspose.OCR 24.11 for .NET  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}