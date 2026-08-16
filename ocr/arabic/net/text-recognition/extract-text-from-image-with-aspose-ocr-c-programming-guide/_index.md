---
category: general
date: 2026-03-13
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف، تشغيل OCR على الصورة، واستخراج النص السيريلي مع كود واضح
  خطوة بخطوة.
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- extract cyrillic text
- recognize cyrillic text
language: ar
og_description: استخراج النص من صورة باستخدام C# وAspose OCR. يوضح هذا الدرس كيفية
  تحميل الصورة للتعرف الضوئي على الأحرف، تشغيل OCR على الصورة، واستخراج النص السيريلي
  بكفاءة.
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل C#
tags:
- Aspose OCR
- C#
- Image Processing
title: استخراج النص من الصورة باستخدام Aspose OCR – دليل برمجة C#
url: /ar/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة باستخدام Aspose OCR – دليل برمجة C#

هل احتجت يومًا إلى **استخراج النص من صورة** لكنك لم تكن متأكدًا أي مكتبة ستتعامل مع الأحرف السيريلية دون مشاكل؟ لست وحدك. في العديد من المشاريع—مسح الفواتير، التحقق من جواز السفر، أو تدوين الملاحظات السريعة—الحصول على نص موثوق من صورة أمر أساسي.  

في هذا الدليل سنستعرض الخطوات الدقيقة لـ **تحميل الصورة للـ OCR**، ضبط Aspose OCR، **تشغيل OCR على الصورة**، وأخيرًا **استخراج النص السيريليني** ببضع أسطر من C#. في النهاية ستحصل على مقطع جاهز للتنفيذ يطبع النص المعترف به في وحدة التحكم.

## ما ستتعلمه

- كيفية تثبيت وإضافة مرجع حزمة NuGet الخاصة بـ Aspose OCR.  
- الطريقة الصحيحة لتوجيه المحرك إلى موارد حزم اللغات.  
- لماذا اختيار `Language.Cyrillic` مهم للخطوط غير اللاتينية.  
- المشكلات الشائعة (نقص الموارد، صيغ الصور غير المدعومة) وكيفية تجنبها.  
- مثال كامل قابل للتنفيذ يمكنك إدراجه في أي مشروع .NET.

لا يلزم خبرة سابقة في OCR، لكن إلمامًا أساسيًا بـ C# وVisual Studio سيسهل العملية.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود التالي:

1. **.NET 6.0** أو أحدث مثبت (الكود يعمل على .NET Core و .NET Framework).  
2. **Visual Studio 2022** (أو أي محرر يدعم C#).  
3. حزمة **Aspose.OCR** من NuGet. قم بتثبيتها عبر Package Manager Console:  

   ```powershell
   Install-Package Aspose.OCR
   ```

4. مجلد يحتوي على حزم لغات OCR (قابلة للتنزيل من موقع Aspose).  
5. ملف صورة (`cyrillic.png` في المثال) يحتوي على نص سيريليني تريد قراءته.

> **نصيحة محترف:** احتفظ بمجلد حزمة اللغة بجوار دليل `bin` الخاص بمشروعك؛ فهذا يبسط التعامل مع المسارات.

## الخطوة 1 – تحميل الصورة للـ OCR

أول ما عليك فعله هو إعطاء المحرك صورة bitmap للعمل عليها. Aspose OCR يقبل `ImageStream` يمكن إنشاؤه مباشرةً من مسار الملف.

```csharp
using Aspose.OCR;

// Step 1: Load the image you want to process
string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
ImageStream image = ImageStream.FromFile(imagePath);
```

*لماذا هذا مهم:* تحميل الصورة مبكرًا يتيح لك التحقق من وجود الملف وأنه بصيغة مدعومة (PNG، JPEG، BMP، إلخ). إذا كان الملف مفقودًا، ستطلق الدالة `FromFile` استثناءً واضحًا، مما يحفظك من أخطاء OCR غير المفهومة لاحقًا.

## الخطوة 2 – إعداد محرك OCR والموارد

بعد ذلك، أنشئ محرك OCR ووجهه إلى المجلد الذي يحتوي على حزم اللغات. بدون الموارد الصحيحة لن يتمكن المحرك من تفسير الحروف السيريلية.

```csharp
// Step 2: Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Tell Aspose where the language resources live
string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
ocrEngine.SetResourcesPath(resourcesPath);
```

*لماذا هذا مهم:* طريقة `SetResourcesPath` هي الجسر بين الكود وملفات البيانات التي تحتوي على أشكال الأحرف لكل لغة مدعومة. نسيان هذه الخطوة يؤدي عادةً إلى مخرجات مشوهة أو استثناء `ResourceNotFoundException`.

## الخطوة 3 – اختيار اللغة و **تشغيل OCR على الصورة**

الآن نحدد اللغة التي نتوقعها. بما أن المثال يتعامل مع السيريلية، نعين `Language.Cyrillic`. إذا احتجت إلى معالجة عدة خطوط يمكنك دمجها باستخدام عامل OR البتّي (`|`).

```csharp
// Step 3: Select the language you want to recognize
ocrEngine.Language = Language.Cyrillic;

// Assign the previously loaded image to the engine
ocrEngine.Image = image;

// Finally, perform the recognition
ocrEngine.Recognize();
```

*لماذا هذا مهم:* تحديد اللغة يقلل مساحة البحث لخوارزمية OCR، مما يحسن السرعة والدقة بشكل كبير. عندما **تشغل OCR على الصورة** مع علم اللغة الصحيح، ستلاحظ عددًا أقل من الأخطاء في التعرف.

## الخطوة 4 – استرجاع واستخدام النص السيريليني المستخرج

بعد انتهاء التعرف، يخزن المحرك النتيجة في الخاصية `Text`. يمكنك الآن عرضها، كتابتها إلى ملف، أو تمريرها إلى نظام آخر.

```csharp
// Step 4: Output the recognized text
string recognizedText = ocrEngine.Text;
Console.WriteLine("=== Extracted Cyrillic Text ===");
Console.WriteLine(recognizedText);
```

مخرجات وحدة التحكم النموذجية تكون كالتالي:

```
=== Extracted Cyrillic Text ===
Привет, мир! Это тестовое изображение.
```

إذا احتوت المخرجات على رموز غير متوقعة، تحقق مرة أخرى من أن حزم اللغات تتطابق مع نسخة Aspose OCR التي قمت بتثبيتها.

## مثال كامل يعمل – جميع الخطوات مجمعة

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد. استبدل `YOUR_DIRECTORY` بالمسارات الفعلية على جهازك.

```csharp
using System;
using Aspose.OCR;

namespace ExtractCyrillicDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the image you want to process
            string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // 2️⃣ Initialize OCR engine and point to language resources
            OcrEngine ocrEngine = new OcrEngine();
            string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
            ocrEngine.SetResourcesPath(resourcesPath);

            // 3️⃣ Choose Cyrillic language and run OCR on image
            ocrEngine.Language = Language.Cyrillic;
            ocrEngine.Image = image;
            ocrEngine.Recognize();

            // 4️⃣ Extract and display the text
            string result = ocrEngine.Text;
            Console.WriteLine("=== Extracted Cyrillic Text ===");
            Console.WriteLine(result);
        }
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يجب أن يطبع النص الدقيق الموجود في `cyrillic.png`. إذا كانت الصورة تحتوي على العبارة “Привет, мир!”، سترى هذا السطر في وحدة التحكم دون أي رموز إضافية.

## الحالات الخاصة & استكشاف الأخطاء وإصلاحها

| الحالة | ما الذي يجب التحقق منه | الحل المقترح |
|-----------|---------------|---------------|
| **نقص حزم اللغة** | هل `resourcesPath` يشير إلى مجلد يحتوي على ملفات `.dat`؟ | أعد تحميل الحزم من Aspose وضعها في المجلد المحدد. |
| **صيغة صورة غير مدعومة** | هل الملف PNG، JPEG، BMP، أو TIFF؟ | حوّل الصورة إلى إحدى الصيغ المدعومة قبل استدعاء `FromFile`. |
| **حروف غير مفهومة في المخرجات** | هل ضبطت `ocrEngine.Language` بشكل صحيح؟ | استخدم `Language.Cyrillic` (أو دمج العلامات للغات متعددة). |
| **بطء الأداء مع صور كبيرة** | دقة الصورة > 3000 px؟ | قلل حجم الصورة إلى حجم معقول (مثلاً عرض 1024 px) قبل تشغيل OCR. |

## مواضيع ذات صلة قد ترغب في استكشافها لاحقًا

- **استخراج النص من صورة** في ملفات PDF باستخدام Aspose PDF + OCR.  
- **تحميل صورة للـ OCR** من `Stream` (مفيد عندما تأتي الصور من واجهة برمجة تطبيقات ويب).  
- استخدام **تشغيل OCR على الصورة** بشكل متوازي لتسريع معالجة الدفعات.  
- **استخراج النص السيريليني** من الملاحظات المكتوبة يدويًا باستخدام وضع الكتابة اليدوية في Aspose OCR.  
- دمج النتيجة مع **التعرف على النص السيريليني** في قاعدة بيانات لفهرسة البحث.

## الخلاصة

لقد أظهرنا لك كيفية **استخراج النص من صورة** باستخدام Aspose OCR، بدءًا من تحميل الصورة وحتى طباعة الأحرف السيريلية المعترف بها. البرنامج القصير والمستقل يوضح الحد الأدنى من الكود المطلوب، بينما جدول استكشاف الأخطاء يوفر لك حلولًا لأكثر المشكلات شيوعًا.  

جرّبه على لقطاتك الخاصة، استبدل حزمة اللغة بالعربية أو الصينية، وشاهد كيف يعمل النمط نفسه في جميع أنحاء العالم. نتمنى لك برمجة سعيدة، وأن تكون نتائج OCR دائمًا واضحة كالكريستال! 

![مثال على استخراج النص من صورة](extract-text-from-image.png "مثال على استخراج النص من صورة")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}