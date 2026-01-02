---
date: 2026-01-02
description: تعلم كيفية استخدام Aspose OCR لـ .NET لاستخراج النص من الصور والحصول
  على نتيجة OCR بصيغة JSON. دليل خطوة بخطوة لتحويل الصورة إلى JSON باستخدام C#.
linktitle: How to Use Aspose OCR for JSON Result in Image Recognition
second_title: Aspose.OCR .NET API
title: كيفية استخدام Aspose OCR للحصول على نتيجة JSON في التعرف على الصور
url: /ar/net/text-recognition/get-result-as-json/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# الحصول على النتيجة بصيغة JSON في التعرف الضوئي على الأحرف (OCR)

## المقدمة

في التطبيقات الحديثة، **كيفية استخدام Aspose** OCR بفعالية يمكن أن تُسرّع بشكل كبير استخراج البيانات من المستندات الممسوحة ضوئياً، لقطات الشاشة، أو أي صورة تحتوي على نص. من خلال الاستفادة من Aspose.OCR لـ .NET يمكنك **extract text image C#**، recognize image aspose ocr، والحصول مباشرةً على **ocr result json** للمعالجة اللاحقة. يشرح هذا الدرس كل خطوة لتحويل صورة إلى مخرجات JSON بصيغة C#، بحيث يمكنك دمج النتيجة في واجهات برمجة التطبيقات، قواعد البيانات، أو خطوط التحليل.

## الإجابات السريعة
- **ماذا يغطي هذا الدرس؟** تحويل مخرجات OCR إلى JSON باستخدام Aspose OCR لـ .NET.  
- **ما اللغة المستخدمة؟** C# (.NET Framework أو .NET Core).  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية متاحة؛ الترخيص مطلوب للإنتاج.  
- **ما هو الناتج الأساسي؟** سلسلة JSON تحتوي على النص المعترف به وبيانات التخطيط.  
- **كم من الوقت تستغرق عملية التنفيذ؟** حوالي 10‑15 دقيقة لإعداد أساسي.

## ما هو Aspose OCR ولماذا نستخدمه؟

Aspose OCR هو مكتبة قوية متعددة المنصات تمكّن المطورين من **recognize image aspose ocr** دون الحاجة إلى خدمات خارجية. تعمل محلياً، تحترم خصوصية البيانات، وتعيد النتائج بصيغة JSON منظمة، مما يجعلها مثالية لتدفقات العمل المؤسسية لتحويل الصورة إلى نص.

## المتطلبات المسبقة

قبل البدء، تأكد من وجود ما يلي:

- **Visual Studio** (أي نسخة حديثة) مثبت على جهازك.  
- **Aspose.OCR for .NET** – قم بتنزيله من [توثيق Aspose.OCR for .NET](https://reference.aspose.com/ocr/net/).  
- صورة نموذجية (مثال: `sample.png`) موجودة في مجلد يمكنك الإشارة إليه من الكود.

## استيراد المساحات الاسمية

لبدء العمل، استورد المساحات الاسمية الأساسية:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## الخطوة 1: إعداد دليل المستندات الخاص بك

حدد المسار حيث توجد ملفات الصور الخاصة بك:

```csharp
string dataDir = "Your Document Directory";
```

## الخطوة 2: تهيئة Aspose.OCR

إنشاء مثال من محرك OCR:

```csharp
AsposeOcr api = new AsposeOcr();
```

## الخطوة 3: التعرف على الصورة

استدعِ طريقة `RecognizeImage` لمعالجة الصورة والحصول على كائن `RecognitionResult`:

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

## الخطوة 4: عرض نتيجة التعرف بصيغة JSON

إخراج نتيجة OCR كسلسلة JSON. هذه هي خطوة تحويل **image to json c#**:

```csharp
Console.WriteLine(result.GetJson());
```

تحتوي الـ JSON المطبوعة على النص المعترف به، درجات الثقة، ومعلومات التخطيط — مثالية لتغذيتها إلى خدمات أخرى.

## الخطوة 5: إنهاء التنفيذ

إشارة إلى إكمال التنفيذ بنجاح:

```csharp
Console.WriteLine("GetResultAsJson executed successfully");
```

## المشكلات الشائعة والنصائح

| المشكلة | الحل |
|---------|------|
| **إخراج JSON فارغ** | تأكد من صحة مسار الصورة وأن الملف قابل للوصول. |
| **درجات ثقة منخفضة** | قم بضبط `RecognitionSettings` (مثل اللغة، DPI) لتحسين الدقة. |
| **عنق زجاجة في الأداء** | أعد استخدام كائن `AsposeOcr` لعدة صور بدلاً من إنشائه في كل مرة. |

## الأسئلة المتكررة

**س: هل تتوفر نسخة تجريبية مجانية لـ Aspose.OCR for .NET؟**  
ج: نعم، يمكنك الوصول إلى نسخة تجريبية مجانية [هنا](https://releases.aspose.com/).

**س: أين يمكنني العثور على توثيق Aspose.OCR for .NET؟**  
ج: التوثيق متاح [هنا](https://reference.aspose.com/ocr/net/).

**س: كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.OCR for .NET؟**  
ج: زر [هذا الرابط](https://purchase.aspose.com/temporary-license/) للحصول على خيارات الترخيص المؤقت.

**س: أين يمكنني الحصول على دعم المجتمع لـ Aspose.OCR for .NET؟**  
ج: تفاعل مع المجتمع في [منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16).

**س: هل يمكنني شراء ترخيص لـ Aspose.OCR for .NET؟**  
ج: نعم، يمكنك شراء ترخيص [هنا](https://purchase.aspose.com/buy).

## الخلاصة

باتباع هذه الخطوات، أصبحت الآن تعرف **كيفية استخدام Aspose** OCR لـ **extract text image C#**، التعرف على الصور، وإنتاج **ocr result json** نظيف. يسهّل هذا النهج تدفقات العمل من الصورة إلى النص، يقلل الاعتماد على الخدمات الخارجية، ويمنحك تحكمًا كاملاً في تنسيق المخرجات.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**آخر تحديث:** 2026-01-02  
**تم الاختبار مع:** Aspose.OCR 24.11 for .NET  
**المؤلف:** Aspose  

---