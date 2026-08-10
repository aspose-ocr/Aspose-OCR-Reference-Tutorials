---
category: general
date: 2026-04-26
description: كيفية تحسين OCR من خلال معالجة الصور مسبقًا. تعلم استخراج النص من الصورة،
  إزالة ضوضاء الصورة، تعزيز تباين الصورة، ومعالجة الصورة مسبقًا لـ OCR باستخدام Aspose.OCR.
draft: false
keywords:
- how to improve OCR
- extract text from image
- remove image noise
- boost image contrast
- preprocess image for OCR
language: ar
og_description: تحسين تقنية التعرف الضوئي على الأحرف يبدأ بالمعالجة المسبقة الذكية.
  يوضح لك هذا الدليل كيفية استخراج النص من الصورة، وإزالة الضوضاء من الصورة، وتعزيز
  تباين الصورة باستخدام Aspose.OCR.
og_title: كيفية تحسين دقة التعرف الضوئي على الأحرف في C# – دليل كامل
tags:
- OCR
- C#
- Image Processing
title: كيفية تحسين دقة التعرف الضوئي على الأحرف في C# – دليل كامل
url: /ar/net/ocr-optimization/how-to-improve-ocr-accuracy-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحسين دقة OCR في C# – دليل كامل

هل تساءلت يومًا **كيف تحسن OCR** عندما يكون النص الذي تحتاجه غير واضح، مائل، أو مجرد ضوضائي؟ لست وحدك. في المشاريع الواقعية، غالبًا ما تؤدي صورة مرتجفة لإيصال أو عقد ممسوح ضوئيًا إلى أحرف مشوشة ما لم تتخذ بعض الخطوات الإضافية.  

الخبر السار؟ من خلال **معالجة الصورة مسبقًا**—إزالة ضوضاء الصورة، تعزيز تباين الصورة، وتصحيح الدوران—يمكنك زيادة موثوقية محرك OCR بشكل كبير. في هذا الدرس سنستعرض مثالًا عمليًا باستخدام **Aspose.OCR** لـ *استخراج النص من ملفات الصورة*، وسنشرح **لماذا** كل تعديل مهم، وليس فقط **ماذا** تكتب.

> **ما ستحصل عليه:** برنامج C# قابل للتنفيذ بالكامل يقوم بتحميل صورة JPEG مائلة ومشوَّشة، يطبق ثلاثة فلاتر، يجري التعرف، ويطبع نصًا نظيفًا إلى وحدة التحكم. لا سكريبتات خارجية، ولا أجزاء مفقودة.

---

## ما ستحتاجه

| المتطلبات المسبقة | السبب |
|--------------|--------|
| .NET 6+ (or .NET Framework 4.6+) | Aspose.OCR تُوزَّع كمكتبة .NET؛ إصدارات التشغيل الأحدث توفر أداءً أفضل. |
| Aspose.OCR NuGet package (`Aspose.OCR`) | توفر `OcrEngine`، الفلاتر، ومساعدي الصور. |
| صورة عينة (مثال: `skewed_noise.jpg`) | سنوضح *إزالة ضوضاء الصورة* و*تعزيز تباين الصورة* على هذا الملف. |
| بيئة تطوير متكاملة (Visual Studio، Rider، أو VS Code) | تسهل عملية تصحيح الأخطاء، لكن أي محرر يمكن استخدامه. |

يمكنك تثبيت المكتبة عبر سطر الأوامر:

```bash
dotnet add package Aspose.OCR
```

## الخطوة 1 – تهيئة محرك OCR (كيفية تحسين OCR من الأساس)

أول شيء يجب القيام به عندما تريد **تحسين OCR** هو إنشاء مثيل `OcrEngine` وإبلاغه باللغة التي تتوقعها. ضبط اللغة يحد من مجموعة الأحرف ويسرّع عملية التعرف.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine to expect Latin characters (English, French, etc.)
ocrEngine.Language = Language.Latin;
```

> **لماذا؟**  
> يمكن للمحرك تخطي الرموز غير ذات الصلة (مثل السيريلي) وتطبيق خوارزميات خاصة باللغة، وهذا جزء أساسي من *تحسين دقة OCR*.

## الخطوة 2 – معالجة الصورة مسبقًا (إزالة ضوضاء الصورة وتعزيز تباين الصورة)

قبل تمرير الصورة إلى أداة التعرف، نضيف ثلاثة فلاتر:

1. **DeskewFilter** – يقوم بتصحيح النص المائل.  
2. **NoiseRemovalFilter** – يزيل البقع التي قد تُقرأ كحروف.  
3. **ContrastBoostFilter** – يجعل الخطوط الخفيفة بارزة.

```csharp
// Clear any default filters
ocrEngine.Options.Preprocessing.Filters.Clear();

// Correct image rotation
ocrEngine.Options.Preprocessing.Filters.Add(new DeskewFilter());

// Remove random speckles and grain
ocrEngine.Options.Preprocessing.Filters.Add(new NoiseRemovalFilter());

// Enhance the contrast so dark text becomes darker and light background stays light
ocrEngine.Options.Preprocessing.Filters.Add(new ContrastBoostFilter());
```

> **لماذا هذه الفلاتر؟**  
> *إزالة ضوضاء الصورة* أمر أساسي عند مسح مستندات منخفضة الدقة؛ غالبًا ما تتحول البكسلات العشوائية إلى إيجابيات كاذبة. *تعزيز تباين الصورة* يساعد محرك OCR على التمييز بين المقدمة والخلفية، خاصةً في المطبوعات الباهتة. معًا تشكل أساسًا قويًا لـ **تحسين نتائج OCR**.

## الخطوة 3 – تحميل الصورة التي تريد معالجتها (استخراج النص من الصورة)

الآن نوجه المحرك إلى الملف الذي نرغب بقراءته. يساعد `ImageStream.FromFile` على تحميل الصورة إلى صيغة يفهمها محرك OCR.

```csharp
// Replace the path with your actual image location
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noise.jpg");
```

> **نصيحة:** إذا كانت صورتك موجودة على عنوان ويب، يمكنك تنزيلها إلى `MemoryStream` أولاً ثم استدعاء `ImageStream.FromStream`.

## الخطوة 4 – تشغيل محرك التعرف (جوهر استخراج النص من الصورة)

مع تكوين المحرك وتحميل الصورة، خطوة OCR الفعلية هي استدعاء طريقة واحدة.

```csharp
// Perform OCR and capture the result
RecognitionResult recognitionResult = ocrEngine.Recognize();
```

> **ماذا يحدث خلف الكواليس؟**  
> يطبق المحرك الفلاتر الثلاثة للمعالجة المسبقة بالترتيب الذي أضيفت به، ثم يشغل مصنفًا يعتمد على الشبكة العصبية على كل كتلة نصية مكتشفة. هذه هي اللحظة التي يثمر فيها كل العمل السابق على **تحسين OCR**.

## الخطوة 5 – عرض النص المعترف به (تحقق من الاستخراج الخاص بك)

أخيرًا، نطبع السلسلة المعترف بها. في مشروع حقيقي قد تقوم بكتابتها إلى قاعدة بيانات، ملف، أو تمريرها إلى خط أنابيب معالجة اللغة الطبيعية اللاحق.

```csharp
// Print the extracted text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(recognitionResult.Text);
```

**الناتج المتوقع** (بافتراض أن الصورة العينة تحتوي على “Invoice #12345 – Total $250.00”):

```
=== OCR RESULT ===
Invoice #12345 – Total $250.00
```

إذا رأيت أحرفًا مشوشة، تحقق مرة أخرى من ترتيب الفلاتر أو جرّب خيارات إضافية مثل `ocrEngine.Options.Preprocessing.Binarization`.

## إضافات – تحسين الضبط والحالات الخاصة

### 1. عندما تكون الصورة داكنة جدًا

أضف `BrightnessAdjustmentFilter` قبل تعزيز التباين:

```csharp
ocrEngine.Options.Preprocessing.Filters.Add(new BrightnessAdjustmentFilter(20)); // raises brightness by 20%
```

### 2. مستندات متعددة اللغات

يمكنك تعيين `ocrEngine.Language = Language.Mixed;` ثم توفير قائمة باللغات الاحتياطية عبر `ocrEngine.Options.LanguageHints`.

### 3. ملفات PDF الكبيرة أو TIFF متعددة الصفحات

قم بالتكرار عبر كل صفحة، عيّن `ocrEngine.Image` داخل الحلقة، واجمع النتائج في `StringBuilder`. هذا النمط *يستخرج النص من مجموعة صور* بكفاءة.

### 4. نصيحة للأداء

إذا كنت تعالج مئات الصور، أعد استخدام نفس مثيل `OcrEngine` بدلاً من إنشاء جديد في كل مرة. يبقى النموذج الداخلي محملاً، مما يقلل وقت المعالجة بحوالي 30 %.

## الخلاصة

أصبح لديك الآن مثال عملي من البداية إلى النهاية يوضح **كيفية تحسين OCR** عبر *معالجة الصورة مسبقًا لـ OCR*، *إزالة ضوضاء الصورة*، و*تعزيز تباين الصورة* قبل أن *تستخرج النص من الصورة* باستخدام Aspose.OCR. النقاط الرئيسية هي:

* حدد اللغة الصحيحة مبكرًا.  
* طبق فلاتر Deskew وإزالة الضوضاء وتعزيز التباين بهذا الترتيب.  
* تحقق من المخرجات وكرر باستخدام فلاتر إضافية إذا لزم الأمر.

من هنا يمكنك استكشاف مواضيع أكثر تقدمًا مثل القواميس المخصصة، المعالجة الدفعية، أو دمج خط أنابيب OCR في دالة سحابية. لا تتردد في التجربة—ربما تجرب مجموعة فلاتر مختلفة أو تستبدل Aspose بمكتبة أخرى لترى كيف تختلف النتائج.

**برمجة سعيدة، ولتقرأ OCR دائمًا بنص نظيف!**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}