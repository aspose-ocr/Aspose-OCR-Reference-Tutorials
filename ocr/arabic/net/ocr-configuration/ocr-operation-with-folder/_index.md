---
title: عملية OCRO مع المجلد في التعرف على الصور OCR
linktitle: عملية OCRO مع المجلد في التعرف على الصور OCR
second_title: Aspose.OCR .NET API
description: أطلق العنان لقوة التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR) في .NET باستخدام Aspose.OCR. استخراج النص من الصور دون عناء.
weight: 11
url: /ar/net/ocr-configuration/ocr-operation-with-folder/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# عملية OCRO مع المجلد في التعرف على الصور OCR

## مقدمة

مرحبًا بك في عالم التعرف الضوئي على الحروف (OCR) باستخدام Aspose.OCR لـ .NET! إذا كنت تتطلع إلى استخراج النص من الصور بسلاسة داخل تطبيقات .NET، فأنت في المكان الصحيح. سيرشدك هذا البرنامج التعليمي خلال عملية التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR) باستخدام المجلدات، مع الاستفادة من الإمكانات القوية لـ Aspose.OCR.

## المتطلبات الأساسية

قبل الغوص في البرنامج التعليمي، تأكد من أن لديك المتطلبات الأساسية التالية:

- معرفة عملية بتطوير C# و.NET.
- تم تثبيت Visual Studio على جهازك.
-  Aspose.OCR لمكتبة .NET، والتي يمكنك تنزيلها[هنا](https://releases.aspose.com/ocr/net/).
- الفهم الأساسي لمفاهيم التعرف الضوئي على الحروف.

## استيراد مساحات الأسماء

في كود C# الخاص بك، تأكد من استيراد مساحات الأسماء اللازمة لاستخدام Aspose.OCR. قم بتضمين ما يلي في بداية البرنامج النصي الخاص بك:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## الخطوة 1: قم بتعيين دليل المستندات

```csharp
// البداية:1
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory";
```

تأكد من استبدال "دليل المستندات الخاص بك" بالمسار الفعلي حيث يتم تخزين الصور الخاصة بك.

## الخطوة 2: تهيئة Aspose.OCR

```csharp
// تهيئة مثيل AsposeOcr
AsposeOcr api = new AsposeOcr();
```

قم بإنشاء مثيل لفئة AsposeOcr للاستفادة من وظائفها.

## الخطوة 3: تحديد مسار الصورة

```csharp
//مسار الصورة
string fullPath = dataDir + "OCR";
```

قم بتسلسل مسار دليل المستند مع المجلد المحدد الذي يحتوي على صورك.

## الخطوة 4: التعرف على الصور

```csharp
// التعرف على الصورة
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //الافتراضي أو المخصص
});
```

استخدم طريقة RecognizeMultipleImages لإجراء التعرف الضوئي على الحروف على صور متعددة داخل المجلد المحدد.

## الخطوة 5: طباعة النتائج

```csharp
// طباعة النتيجة
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

قم بمراجعة النتائج وطباعة النص الذي تم التعرف عليه لكل صورة.

## الخطوة 6: الاستنتاج

```csharp
// النهاية:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

تأكد من الوصول إلى نهاية البرنامج النصي الخاص بك للإشارة إلى التنفيذ الناجح لعملية التعرف الضوئي على الحروف (OCR) مع المجلدات.

## خاتمة

تهانينا! لقد تعلمت بنجاح كيفية تنفيذ التعرف على الصور بتقنية التعرف الضوئي على الحروف (OCR) مع المجلدات باستخدام Aspose.OCR لـ .NET. تفتح هذه الأداة القوية عددًا لا يحصى من الإمكانيات لاستخراج النص من الصور في تطبيقات .NET الخاصة بك.

## الأسئلة الشائعة

### س1: هل يمكنني استخدام Aspose.OCR لـ .NET في المشاريع التجارية؟

 A1: نعم، Aspose.OCR لـ .NET هو منتج تجاري. للحصول على معلومات الترخيص، قم بزيارة[هنا](https://purchase.aspose.com/buy).

### س2:. هل هناك نسخة تجريبية مجانية متاحة؟

 ج2: نعم، يمكنك استكشاف النسخة التجريبية المجانية[هنا](https://releases.aspose.com/).

### س3: أين يمكنني العثور على الوثائق؟

 ج3: الوثائق متاحة[هنا](https://reference.aspose.com/ocr/net/).

### س4: كيف يمكنني الحصول على ترخيص مؤقت؟

 ج4: يمكن الحصول على تراخيص مؤقتة[هنا](https://purchase.aspose.com/temporary-license/).

### س5: هل تحتاج إلى دعم أو لديك أسئلة؟

 ج5: قم بزيارة[منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) لدعم المجتمع.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
