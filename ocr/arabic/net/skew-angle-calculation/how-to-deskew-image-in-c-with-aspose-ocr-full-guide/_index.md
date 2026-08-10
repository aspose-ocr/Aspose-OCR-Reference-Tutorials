---
category: general
date: 2026-03-23
description: كيفية تصحيح انحراف الصورة باستخدام Aspose OCR في C#. تعلم كيفية إزالة
  الضوضاء، تصحيح دوران الصورة، والتعرف على النص من الصورة في دقائق.
draft: false
keywords:
- how to deskew image
- how to remove noise
- recognize text from image
- remove salt pepper noise
- correct image rotation
language: ar
og_description: كيفية تصحيح انحراف الصورة بسرعة باستخدام Aspose OCR. يوضح هذا الدليل
  أيضًا كيفية إزالة الضوضاء، وتصحيح دوران الصورة، والتعرف على النص من الصورة.
og_title: كيفية تصحيح انحراف الصورة في C# – دليل Aspose OCR الكامل
tags:
- OCR
- C#
- Image Preprocessing
title: كيفية تصحيح ميل الصورة في C# باستخدام Aspose OCR – دليل كامل
url: /ar/net/skew-angle-calculation/how-to-deskew-image-in-c-with-aspose-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح انحراف الصورة في C# – دليل Aspose OCR الكامل

هل تساءلت يومًا **كيفية تصحيح انحراف الصورة** التي تأتي من ماسح ضوئي غير مستوي قليلًا؟ لست وحدك. في العديد من المشاريع الواقعية تكون الصورة الأصلية مائلة بضع درجات، مليئة بضوضاء من نوع الملح والفلفل، ولا يزال يلزم قراءتها كنص عادي.  

الخبر السار؟ باستخدام Aspose OCR يمكنك تصحيح الدوران، وإزالة الضوضاء، ثم **التعرف على النص من الصورة**—كل ذلك في بضع أسطر فقط. في هذا الدليل سنستعرض كامل سير العمل، نشرح لماذا كل مرشح مهم، ونزودك ببرنامج C# جاهز للتنفيذ.

> *نصيحة احترافية:* إذا لم تستخدم Aspose OCR من قبل، احصل على نسخة تجريبية مجانية من موقع Aspose؛ الـ API يعمل جاهزًا مع .NET 6+.

---

## ما ستحتاجه

- **.NET 6 SDK** (أو أي نسخة .NET حديثة) – يتم تجميع الكود باستخدام Visual Studio أو Rider أو سطر الأوامر `dotnet`.  
- **حزمة Aspose.OCR NuGet** – تثبيت باستخدام `dotnet add package Aspose.OCR`.  
- **صورة نموذجية** مائلة قليلًا وتحتوي على ضوضاء (مثال: `skewed.png`).  
- معرفة أساسية بـ C# – لا تحتاج أن تكون خبيرًا، فقط أن تكون مرتاحًا مع عبارات `using` ووحدة التحكم.

هذا كل ما تحتاجه. لا محركات OCR إضافية، لا ملفات DLL أصلية، مجرد مرجع NuGet واحد.

## كيفية تصحيح انحراف الصورة – نظرة عامة خطوة بخطوة

فيما يلي نقسم العملية إلى خطوات منطقية. كل خطوة لها عنوان واضح، مقتطف شفرة، وفقرة قصيرة توضح “السبب” حتى تفهم المنطق وراء الاستدعاء.

![مثال على تصحيح انحراف الصورة](https://example.com/deskew-demo.png "مثال على تصحيح انحراف الصورة")

### الخطوة 1: إعداد محرك OCR

أولًا نقوم بإنشاء كائن `OcrEngine`. يضمن كتلة `using` التخلص السليم، مما يحرر الموارد الأصلية فور الانتهاء.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Preprocess
{
    static void Main()
    {
        // Step 1 – instantiate the OCR engine
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // The rest of the pipeline goes here...
        }
    }
}
```

*لماذا هذا مهم:* `OcrEngine` هو قلب Aspose OCR. يحتفظ بالصورة، وسلسلة المرشحات، وإعدادات التعرف. تغليفه داخل `using` يمنع تسرب الذاكرة، خاصةً عند معالجة عشرات الصفحات في مهمة دفعة.

### الخطوة 2: تحميل الصورة الممسوحة

نحمّل الملف باستخدام `ImageStream.FromFile`. يمكن أن يكون المسار مطلقًا أو نسبيًا إلى دليل العمل الخاص بالملف التنفيذي.

```csharp
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed.png");
```

*لماذا هذا مهم:* يعمل المحرك على تدفق صورة في الذاكرة. توفير المسار الصحيح هو المكان الوحيد الذي قد يحدث فيه `FileNotFoundException`، لذا تحقق من بنية المجلدات قبل التشغيل.

### الخطوة 3: إضافة مرشحات ما قبل المعالجة

هنا نجيب على **كيفية إزالة الضوضاء** و**تصحيح دوران الصورة**. مرشحان مدمجان يقومان بالعمل الشاق:

```csharp
// DeskewFilter corrects small rotation (usually up to ±5°)
ocrEngine.Filters.Add(new DeskewFilter());

// DenoiseFilter removes salt‑and‑pepper noise
ocrEngine.Filters.Add(new DenoiseFilter());
```

*لماذا هذه المرشحات؟*  
- **DeskewFilter** يحلل خطوط النص الأساسية، يحسب زاوية الانحراف، ويعيد تدوير الصورة إلى الوضع الأفقي. بدونه قد يخطئ محرك OCR في تفسير الأحرف (مثل “l” مقابل “i”).  
- **DenoiseFilter** يطبق خوارزمية قائمة على الوسيط تُنقّح البكسلات السوداء/البيضاء المنعزلة—وهو ما يعنيه “إزالة ضوضاء الملح والفلفل” في مصطلحات معالجة الصور. هذا يحسّن درجات الثقة بشكل كبير.

إذا كان لديك مسح ضبابي بشكل كبير، يمكنك أيضًا إضافة `SharpenFilter` في البداية، لكن ذلك تعديل اختياري.

### الخطوة 4: تشغيل التعرف على OCR

الآن نطلب من Aspose OCR أداء مهمته. تُعيد طريقة `Recognize` قيمة منطقية تشير إلى النجاح.

```csharp
if (ocrEngine.Recognize())
{
    // Step 5 – output the cleaned text
    Console.WriteLine("Cleaned text:\n" + ocrEngine.Text);
}
else
{
    Console.Error.WriteLine("OCR failed – check the image and filter configuration.");
}
```

*لماذا نتحقق من النتيجة:* أحيانًا لا يستطيع المحرك العثور على أي نص (مثلاً صفحة فارغة). معالجة الحالة `false` تمنع فشل صامت يصعب تتبعه لاحقًا.

### الخطوة 5: التحقق من النتيجة

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
Cleaned text:
The quick brown fox jumps over the lazy dog.
```

إذا ما زال النص مشوشًا، فكر في:

- **زيادة تحمل تصحيح الانحراف** – `new DeskewFilter(0.1)` يسمح للمرشح بقبول زوايا أكبر.  
- **إضافة `BinarizeFilter`** قبل إزالة الضوضاء لتحويل الصورة إلى أبيض وأسود نقي.  
- **التحقق من DPI** – عادةً ما تحتاج المسحات منخفضة الدقة (< 150 dpi) إلى تكبير قبل OCR.

## كيفية إزالة الضوضاء – خيارات متقدمة

`DenoiseFilter` الأساسي يعمل جيدًا مع البقع النموذجية للماسحات، لكن أحيانًا قد تواجه **إزالة ضوضاء الملح والفلفل** في مسحات أفلام قديمة. في تلك الحالات:

```csharp
// Apply a stronger median filter (kernel size 3x3)
ocrEngine.Filters.Add(new DenoiseFilter { KernelSize = 3 });
```

أو ربط **GaussianBlurFilter** قبل إزالة الضوضاء:

```csharp
ocrEngine.Filters.Add(new GaussianBlurFilter { Sigma = 0.8 });
ocrEngine.Filters.Add(new DenoiseFilter());
```

هذه التعديلات تضحي بقليل من الحدة للحصول على صورة ثنائية أنظف، مما يرفع عادةً درجة ثقة OCR بنسبة 5‑10 %.

## التعرف على النص من الصورة – نصائح ما بعد المعالجة

بعد حصولك على `ocrEngine.Text`، قد ترغب في:

- **إزالة الفراغات الزائدة** – `ocrEngine.Text = ocrEngine.Text.Trim();`  
- **تطبيع نهايات الأسطر** – `ocrEngine.Text = ocrEngine.Text.Replace("\r\n", "\n");`  
- **تشغيل مدقق إملائي** باستخدام `System.Globalization` أو مكتبة طرف ثالث إذا لم تكن لغة المصدر الإنجليزية.

جميع هذه الخطوات تجعل السلسلة المستخرجة جاهزة للمعالجة اللاحقة، مثل إدخالها في فهرس بحث أو نموذج إدخال بيانات.

## الحالات الخاصة والمشكلات الشائعة

| الحالة | ما الذي يجب مراقبته | الحل المقترح |
|-----------|-------------------|---------------|
| الصورة مائلة > 10° | `DeskewFilter` يتوقف عند الحد الافتراضي | مرّر زاوية قصوى مخصصة: `new DeskewFilter { MaxAngle = 15 }` |
| خلفية داكنة جدًا | قد تفسر المرشحات الخلفية على أنها نص | أضف `InvertColorsFilter` في البداية أو زد التباين |
| PDF متعدد الصفحات | `OcrEngine` يعمل على صورة واحدة في كل مرة | كرر عبر كل صفحة، أنشئ `OcrEngine` جديد لكل تكرار |
| نص غير لاتيني | اللغة الافتراضية هي الإنجليزية | عيّن `ocrEngine.Language = OcrLanguage.Thai;` (أو أي لغة مدعومة أخرى) |

مراعاة هذه النقاط سيوفر عليك الوقوع في كابوس “لماذا ناتج OCR فارغ؟” الشائع.

## مثال كامل يعمل

انسخ الشفرة أدناه إلى مشروع وحدة تحكم جديد (`dotnet new console -n OcrDemo`). استعد حزمة Aspose OCR، استبدل `YOUR_DIRECTORY/skewed.png` بالمسار إلى صورة الاختبار الخاصة بك، ثم شغّل البرنامج.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Preprocess
{
    static void Main()
    {
        // Initialize OCR engine
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // Load the image that may be slightly rotated
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed.png");

            // Add preprocessing filters
            //   - DeskewFilter corrects small rotation
            //   - DenoiseFilter removes salt‑and‑pepper noise
            ocrEngine.Filters.Add(new DeskewFilter());
            ocrEngine.Filters.Add(new DenoiseFilter());

            // Perform OCR recognition
            if (ocrEngine.Recognize())
            {
                // Output the cleaned text
                Console.WriteLine("Cleaned text:\n" + ocrEngine.Text);
            }
            else
            {
                Console.Error.WriteLine("Recognition failed – verify the image and filters.");
            }
        }
    }
}
```

تشغيل هذا البرنامج يطبع النص المنظف والمصحح إلى وحدة التحكم. هذه هي كامل عملية **كيفية تصحيح انحراف الصورة** مُختصرة في أقل من 50 سطرًا من الشفرة.

## الخلاصة

لقد غطينا للتو **كيفية تصحيح انحراف الصورة** باستخدام Aspose OCR، وأظهرنا **كيفية إزالة الضوضاء**، وشرحنا **تصحيح دوران الصورة**، وبيّنّا طريقة موثوقة لـ **التعرف على النص من الصورة**. بربط `DeskewFilter` و `DenoiseFilter` ستحصل على صورة نقطية واضحة ومستقيمة يمكن لمحرك OCR قراءتها بثقة عالية.  

من هنا قد ترغب في استكشاف:

- معالجة دفعات من عشرات المسحات بالتوازي.  
- تصدير نتيجة OCR إلى PDF/A للأرشفة.  
- دمج كشف اللغة للمستندات متعددة اللغات.

جرّب هذه الأفكار، ولا تتردد في تعديل معلمات المرشحات لتناسب مسحاتك الخاصة. برمجة سعيدة، ولتكون صورك دائمًا مستقيمة تمامًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}