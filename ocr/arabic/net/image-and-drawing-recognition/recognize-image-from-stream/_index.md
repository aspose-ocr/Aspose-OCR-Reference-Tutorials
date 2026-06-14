---
date: 2026-04-12
description: تعلم كيفية استخراج النص من الصور من خلال التدفقات باستخدام Aspose OCR
  لـ .NET. يوضح هذا المثال خطوة بخطوة استخراج النص بسهولة باستخدام OCR.
keywords:
- image text extraction
- image to memorystream
- ocr png file
- image stream ocr
- read image stream c#
linktitle: التعرف على الصورة من التدفق في التعرف الضوئي على الأحرف
second_title: Aspose.OCR .NET API
title: كيفية استخراج النص من صورة من تدفق باستخدام Aspose OCR
url: /ar/net/image-and-drawing-recognition/recognize-image-from-stream/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج نص الصورة من تدفق باستخدام Aspose OCR

مرحبًا بك في عالم **استخراج نص الصورة** مع **Aspose.OCR for .NET**. في هذا البرنامج التعليمي ستتعرف على كيفية قراءة تدفق صورة، تشغيل OCR على ملف PNG، واستخراج النص المعترف به إلى تطبيق C# الخاص بك. سواء كنت تبني خط أنابيب معالجة مستندات، أو أداة أتمتة إدخال بيانات، أو مجرد تجربة OCR، فإن الخطوات أدناه ستحول الصورة الخام إلى نص قابل للبحث في دقائق.

## إجابات سريعة
- **ما الذي يوضح هذا البرنامج التعليمي؟** استخراج النص من صورة مقدمة كتيار باستخدام Aspose OCR.  
- **ما هي الكلمة المفتاحية الأساسية المستهدفة؟** *image text extraction* (مستخدمة طوال الدليل).  
- **هل أحتاج إلى ترخيص للتطوير؟** الإصدار التجريبي المجاني يعمل للاختبار؛ الترخيص التجاري مطلوب للاستخدام في الإنتاج.  
- **هل يمكنني معالجة ملفات PNG مباشرةً؟** نعم – Aspose OCR يتعامل مع صيغ **ocr png file** دون تحويل إضافي.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## ما هو استخراج نص الصورة؟
استخراج نص الصورة (المعروف أيضًا باسم OCR) يحول الأحرف البصرية في الصورة إلى نص قابل للتحرير والبحث. مع Aspose OCR يمكنك تمرير `MemoryStream` يحتوي على أي صورة مدعومة (PNG، JPEG، BMP، إلخ) وتلقي السلسلة المعترف بها في استدعاء واحد.

## لماذا تختار Aspose OCR لاستخراج نص الصورة؟
- **دعم واسع للغات** – يعمل مع عشرات اللغات مباشرةً.  
- **واجهة برمجة تطبيقات بسيطة** – بضع أسطر من C# تحول **image to memorystream** إلى نص قابل للقراءة.  
- **دقة عالية** – الخوارزميات المتقدمة تتعامل مع المسحات الضوضائية وملفات PNG منخفضة الدقة.  
- **متعدد المنصات** – يعمل على Windows وLinux وmacOS مع .NET Core.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أنك تمتلك:

- تثبيت Aspose.OCR for .NET (قم بالتنزيل من [Aspose.OCR for .NET Documentation](https://reference.aspose.com/ocr/net/)).  
- ملف صورة تجريبي (مثال: **sample.png**) موجود في مجلد يمكنك الإشارة إليه من الكود.

## استيراد مساحات الأسماء

أضف مساحات الأسماء المطلوبة إلى ملف C# الخاص بك:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## دليل خطوة بخطوة

### الخطوة 1: تعيين دليل المستند
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```
استبدل **"Your Document Directory"** بالمجلد الفعلي الذي يحتوي على *sample.png*.

### الخطوة 2: تهيئة محرك Aspose OCR
```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```
إنشاء كائن `AsposeOcr` يمنحك الوصول إلى جميع طرق OCR.

### الخطوة 3: قراءة تدفق الصورة والتعرف على النص
```csharp
// Recognize image
using (MemoryStream ms = new MemoryStream())
using (FileStream file = new FileStream(dataDir + "sample.png", FileMode.Open, FileAccess.Read))
{
    file.CopyTo(ms);
    result = api.RecognizeImage(ms);
}
```
هنا نفتح **sample.png**، ننسخ بايتاته إلى `MemoryStream`، ونمرر هذا التدفق إلى `RecognizeImage`. هذا يوضح **image stream ocr** ونمط **read image stream c#** في تدفق واحد.

### الخطوة 4: عرض النص المعترف به
```csharp
// Display the recognized text
Console.WriteLine(result);
```
يتم طباعة نتيجة OCR إلى وحدة التحكم؛ يمكنك أيضًا تخزينها في قاعدة بيانات أو ملف.

### الخطوة 5: تأكيد التنفيذ الناجح
```csharp
Console.WriteLine("RecognizeImageFromStream executed successfully");
```
تأكيد بسيط يخبرك بأن العملية انتهت دون استثناءات.

## المشكلات الشائعة والحلول

| المشكلة | الحل |
|-------|----------|
| *النتيجة فارغة* | تحقق من مسار الصورة، تأكد من أن الملف قابل للقراءة، وتأكد من أن الصورة تحتوي على نص واضح وعالي التباين. |
| *تنسيق صورة غير مدعوم* | حوّل المصدر إلى PNG أو JPEG قبل استدعاء `RecognizeImage`. |
| *استثناء الترخيص* | طبق ترخيصًا مؤقتًا أثناء التطوير أو اشترِ ترخيصًا كاملاً للإنتاج (انظر أدناه). |

## الأسئلة المتكررة

**س: هل يمكن لـ Aspose.OCR التعامل مع لغات متعددة؟**  
ج: نعم، يدعم Aspose.OCR مجموعة واسعة من اللغات، مما يجعله مناسبًا لمشاريع OCR العالمية.

**س: هل هناك نسخة تجريبية يمكنني استخدامها؟**  
ج: بالتأكيد! يمكنك تجربة Aspose.OCR for .NET بنسخة تجريبية مجانية [هنا](https://releases.aspose.com/).

**س: أين يمكنني الحصول على مساعدة إذا واجهت مشاكل؟**  
ج: زر [منتدى Aspose.OCR](https://forum.aspose.com/c/ocr/16) للحصول على دعم المجتمع والخبراء.

**س: كيف أحصل على ترخيص مؤقت للاختبار؟**  
ج: ترخيص مؤقت متاح [هنا](https://purchase.aspose.com/temporary-license/) لأغراض التقييم.

**س: أين يمكنني شراء ترخيص دائم؟**  
ج: لإضافة Aspose.OCR إلى مجموعة أدوات الإنتاج الخاصة بك، انتقل إلى [صفحة الشراء](https://purchase.aspose.com/buy).

## الخاتمة

لقد أصبحت الآن متمكنًا من **استخراج نص الصورة** من تدفق باستخدام Aspose OCR for .NET. تتيح لك واجهة برمجة التطبيقات المختصرة تحويل أي صورة مدعومة—مثل **ocr png file**—إلى نص قابل للبحث ببضع أسطر من الشيفرة فقط. جرّب مصادر صور مختلفة، حزم لغات، وإعدادات متقدمة لضبط مخرجات OCR وفقًا لسيناريوك الخاص.

---

**آخر تحديث:** 2026-04-12  
**تم الاختبار مع:** Aspose.OCR 24.12 for .NET  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}