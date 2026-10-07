---
category: general
date: 2026-02-28
description: كيفية تشغيل OCR في C# باستخدام Aspose OCR – تعلم كيفية استخراج النص من
  الصورة، وتحويل الصورة إلى JSON أو XML في بضع خطوات فقط.
draft: false
keywords:
- how to run OCR
- extract text from image
- convert image to json
- convert image to xml
- how to extract text
language: ar
og_description: كيفية تشغيل OCR في C# باستخدام Aspose OCR – اكتشف كيفية استخراج النص
  من الصورة وتحويل الصورة إلى JSON أو XML مع مثال جاهز للتنفيذ.
og_title: كيفية تشغيل OCR باستخدام Aspose OCR في C# – دليل كامل
tags:
- OCR
- C#
- Aspose
- Image Processing
title: كيفية تشغيل OCR باستخدام Aspose OCR في C# – دليل شامل
url: /ar/net/text-recognition/how-to-run-ocr-with-aspose-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR باستخدام Aspose OCR في C# – دليل كامل

إذا كنت تتساءل **كيف تشغّل OCR** على صورة إيصال باستخدام C#، فقد وصلت إلى المكان الصحيح. في هذا الدرس سنستعرض **استخراج النص من الصورة** ثم **تحويل الصورة إلى JSON** أو **تحويل الصورة إلى XML** باستخدام Aspose OCR—كل ذلك في برنامج واحد مكتمل ومستقل.

تخيل أنك تبني تطبيقًا لتتبع النفقات وتحتاج إلى استخراج بنود الفاتورة من إيصالات مصوَّرة. كتابة كل إدخال يدويًا أمر مزعج، أليس كذلك؟ بنهاية هذا الدليل ستحصل على مقتطف قابل لإعادة الاستخدام يقرأ أي صورة، يُعيد نصًا مُنظمًا، ويعطيك تمثيلات JSON وXML جاهزة للمعالجة اللاحقة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا على .NET Framework 4.8)
- Visual Studio 2022 (أو أي محرر تفضله)
- حزمة **Aspose.OCR** NuGet نشطة (`Install-Package Aspose.OCR`)
- صورة نموذجية (مثال: `receipt.png`) موجودة في مجلد يمكنك الإشارة إليه

لا تحتاج إلى أي إعدادات إضافية؛ المكتبة تُضمّن جميع نماذج OCR اللازمة.

![Receipt image for OCR processing – how to run OCR](receipt.png)

> *نص بديل: صورة إيصال لمعالجة OCR – كيفية تشغيل OCR*

## التنفيذ خطوة بخطوة

نقسم الحل إلى أجزاء منطقية. كل خطوة تشرح **لماذا** نقوم بها، وليس فقط **ماذا** يبدو عليه الكود.

### 1️⃣ تهيئة محرك OCR – الأساس لـ **كيفية تشغيل OCR**

الفئة `OcrEngine` هي نقطة الدخول. إنشاء كائن منها يحمل نماذج اللغة الداخلية ويجهّز المحرك للتعرف.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        // This object holds the OCR model and settings.
        var ocrEngine = new OcrEngine();
```

> **نصيحة محترف:** إعادة استخدام نفس `OcrEngine` عبر صور متعددة يقلل من استهلاك الذاكرة ويسرّع المعالجة الدفعية.

### 2️⃣ تحميل الصورة – جوهر **استخراج النص من الصورة**

Aspose OCR يعمل مع غلاف `Image` الخاص به. استخدام جملة `using` يضمن تحرير مقبض الملف بسرعة.

```csharp
        // Step 2: Load the image you want to analyze
        // Replace YOUR_DIRECTORY with the actual path on your machine.
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");
```

إذا كانت الصورة بصيغة مختلفة (BMP، TIFF، PDF)، فإن طريقة `Load` نفسها تتعامل معها—دون الحاجة إلى تحويل إضافي.

### 3️⃣ تشغيل التعرف على OCR – قلب **كيفية تشغيل OCR**

استدعاء `Recognize` يقوم بالعمل الشاق: تحليل التخطيط، تجزئة الأحرف، وتصنيف اللغة المحددة.

```csharp
        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);
```

الكائن `OcrResult` المرتجع يحتوي على النص الخام، درجات الثقة، وشجرة تخطيط مفصلة يمكن تسلسلها.

### 4️⃣ تحويل الصورة إلى JSON – الطريقة المبسطة لـ **تحويل الصورة إلى json**

JSON مثالي لواجهات الويب أو قواعد NoSQL. طريقة `ToJson` تعطيك سلسلة منسقة بشكل جميل، ما يجعل عملية تصحيح الأخطاء سهلة.

```csharp
        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);
```

مثال على مخرجات JSON (مقتطع للوضوح):

```json
{
  "Text": "Total 12.34",
  "Blocks": [
    {
      "Text": "Total",
      "Confidence": 0.98,
      "Bounds": { "X": 10, "Y": 150, "Width": 45, "Height": 15 }
    },
    {
      "Text": "12.34",
      "Confidence": 0.97,
      "Bounds": { "X": 60, "Y": 150, "Width": 30, "Height": 15 }
    }
  ]
}
```

يمكنك الآن تمرير هذا الـ JSON مباشرةً إلى نقطة نهاية REST أو تخزينه في Azure Cosmos DB.

### 5️⃣ تحويل الصورة إلى XML – عندما يكون **تحويل الصورة إلى xml** مطلوبًا

بعض الأنظمة القديمة لا تزال تستهلك XML. توفر Aspose طريقة `ToXml` لتمثيل نظيف ومتوافق مع المخطط.

```csharp
        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

مقتطف XML نموذجي:

```xml
<OcrResult>
  <Text>Total 12.34</Text>
  <Blocks>
    <Block>
      <Text>Total</Text>
      <Confidence>0.98</Confidence>
      <Bounds X="10" Y="150" Width="45" Height="15" />
    </Block>
    <Block>
      <Text>12.34</Text>
      <Confidence>0.97</Confidence>
      <Bounds X="60" Y="150" Width="30" Height="15" />
    </Block>
  </Blocks>
</OcrResult>
```

كلا التنسيقين يحافظان على نفس البيانات الهرمية، لذا يمكنك اختيار ما يناسب خط أنابيبك اللاحق.

## المشكلات الشائعة وكيفية استخراج النص بثقة

حتى مع مكتبة قوية، الصور الواقعية قد تواجهك بمشكلات غير متوقعة. إليك ثلاث قضايا قد تصادفها والحلول المقترحة.

### 📏 صور منخفضة الدقة

**لماذا يهم:** الخطوط الصغيرة تندمج، مما يقلل من درجات الثقة.  
**الحل:** عالج الصورة مسبقًا—قم بتكبيرها باستخدام `Image.Resize` أو طبّق مرشح شحذ قبل تمريرها إلى `Recognize`.

```csharp
using var highRes = image.Resize(2.0, InterpolationMode.HighQualityBicubic);
var result = ocrEngine.Recognize(highRes);
```

### 🌈 تباين ضعيف

**لماذا يهم:** النص الفاتح على خلفية داكنة يربك خوارزمية التجزئة.  
**الحل:** عكس الألوان أو تعديل السطوع/التباين عبر `Image.AdjustBrightnessContrast`.

```csharp
image.AdjustBrightnessContrast(brightness: 30, contrast: 40);
```

### 📄 مستندات متعددة اللغات

**لماذا يهم:** النموذج اللغوي الافتراضي هو الإنجليزية؛ اللغات المختلطة تؤدي إلى ناتج غير مفهوم.  
**الحل:** عيّن `ocrEngine.Language = OcrLanguage.Multilingual;` قبل عملية التعرف.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

معالجة هذه الحالات الطرفية تضمن أن **كيفية استخراج النص** من أي صورة تصبح روتينًا موثوقًا وليس مجرد حظ.

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي البرنامج الكامل، جاهز للترجمة والتنفيذ. ما عليك سوى استبدال `YOUR_DIRECTORY` بمسار الصورة ثم الضغط على F5.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Optional: improve accuracy for low‑contrast images
        // ocrEngine.Language = OcrLanguage.Multilingual;

        // Step 2: Load the image you want to analyze
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");

        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);

        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

**الناتج المتوقع في وحدة التحكم** (منسق للقراءة) يعرض هياكل JSON وXML التي تحتوي على النص المستخرج ومربعات الحدود.

## ملخص – ما تم تغطيته

- **كيفية تشغيل OCR** باستخدام Aspose OCR في C#
- العملية خطوة بخطوة لـ **استخراج النص من الصورة**
- خيارا التسلسل: **تحويل الصورة إلى json** و **تحويل الصورة إلى xml**
- نصائح للتعامل مع الصور منخفضة الدقة، منخفضة التباين، والسيناريوهات متعددة اللغات
- عينة كود كاملة جاهزة للنسخ واللصق يمكنك إدراجها في أي مشروع .NET

## ما الخطوة التالية؟

الآن بعد أن أصبحت قادرًا على **استخراج النص** والحصول على بيانات منظمة، فكر في الأفكار التالية:

- إرسال الـ JSON إلى Azure Function يخزن الإيصالات في Cosmos DB.
- استخدام مخرجات XML لتعبئة نظام محاسبة قائم على SOAP.
- دمج Aspose OCR مع نموذج تعلم آلي لتصنيف أنواع النفقات تلقائيًا.

لا تتردد في التجربة—استبدل `receipt.png` بفواتير، بطاقات عمل، أو ملاحظات مكتوبة يدويًا. النمط نفسه يعمل عبر

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}