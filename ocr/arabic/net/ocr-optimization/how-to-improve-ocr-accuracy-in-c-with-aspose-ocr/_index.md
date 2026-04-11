---
category: general
date: 2026-04-11
description: تعلم كيفية تحسين تقنية التعرف الضوئي على الأحرف (OCR) في C# من خلال التعرف
  على النص من ملفات JPG، وتصحيح انحراف الصور، وإزالة الضوضاء باستخدام Aspose OCR.
draft: false
keywords:
- how to improve OCR
- recognize text from jpg
- extract text from image
- how to deskew image
- how to remove noise
language: ar
og_description: اكتشف كيفية تحسين OCR من خلال التعرف على النص من ملفات JPG، وتصحيح
  انحراف الصور، وإزالة الضوضاء—دليل C# كامل.
og_title: كيفية تحسين دقة OCR في C# باستخدام Aspose OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: كيفية تحسين دقة OCR في C# باستخدام Aspose OCR
url: /ar/net/ocr-optimization/how-to-improve-ocr-accuracy-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحسين دقة OCR في C# باستخدام Aspose OCR

هل تساءلت يومًا **how to improve OCR** عندما تبدو مسحاتك أكثر كفن تجريدي من نص قابل للقراءة؟ لست وحدك. في العديد من المشاريع الواقعية—فكر في الفواتير، الإيصالات، أو الملاحظات المكتوبة يدويًا—غالبًا ما تكون الصور المصدرية مائلة، ذات حبيبات، أو مجرد ضوضاء صاخبة. الخبر السار؟ Aspose OCR يزودك بمجموعة من إعدادات ما قبل المعالجة التي يمكنها تحويل تلك الفوضى إلى أحرف نظيفة قابلة للقراءة آليًا. في هذا الدرس سنستعرض مثالًا كاملاً قابلًا للتنفيذ يُظهر **how to improve OCR** عبر **recognizing text from JPG**، وتصحيح ميل الصورة، وإزالة الضوضاء غير المرغوب فيها.

> *نصيحة احترافية:* إذا تخطيت مرحلة ما قبل المعالجة، فمن المحتمل أن تحصل على مخرجات مشوشة تشبه أحجية الكلمات المتقاطعة الغامضة. دعنا نتجنب ذلك.

![كيفية تحسين OCR مع معالجة Aspose OCR المسبقة](https://example.com/ocr-preprocess.png "كيفية تحسين OCR مع Aspose OCR")

## ما ستتعلمه

1. كيفية إعداد محرك Aspose OCR للحصول على أقصى دقة.  
2. الكود الدقيق اللازم لـ **recognize text from JPG** الملفات.  
3. لماذا يهم تمكين *AutoDeskew* و *RemoveNoise* وكيفية ضبطهما.  
4. كيفية **extract text from image** الملفات دون كتابة مرشح مخصص.  
5. المشكلات الشائعة (ملف مفقود، تنسيق غير مدعوم) والحلول السريعة.

بنهاية الدرس ستحصل على تطبيق وحدة تحكم C# واحد يمكنه أخذ أي JPG، تنظيفه، وإخراج السلسلة المستخرجة—جاهزة للمعالجة اللاحقة أو التخزين.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (المثال يستخدم عبارات المستوى الأعلى للتبسيط).  
- حزمة NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
- صورة JPG نموذجية (اسمها `input.jpg`) موجودة في نفس مجلد الملف التنفيذي.  
- إلمام أساسي بـ C#—لا حاجة لمفاهيم متقدمة.

إذا كان لديك مشروع بالفعل، فقط الصق الكود فيه؛ وإلا أنشئ تطبيق وحدة تحكم جديد:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

الآن دعنا نغوص في الكود.

## كيفية تحسين OCR: نظرة عامة على إعدادات ما قبل المعالجة

جوهر **how to improve OCR** يكمن في كائن `PreprocessSettings`. فكر فيه كمحرر صور صغير يعمل *قبل* تشغيل محرك التعرف على الأحرف الفعلي. أدناه نظرة سريعة على أكثر العلامات تأثيرًا:

| Setting                | ما يفعله                                            | حالة الاستخدام النموذجية |
|------------------------|-----------------------------------------------------|--------------------------|
| `AutoDeskew`           | يطبق خوارزمية تصحيح الميل باستخدام التعلم العميق.   | صفحات ممسوحة مائلة قليلاً. |
| `AdaptiveThreshold`    | يعزز التباين في الصور ذات الإضاءة المنخفضة أو الباهتة. | إيصالات قديمة بحبر باهت. |
| `RemoveNoise`          | يطبق مرشح تمويه غاوسي لتقليل البقع.               | صور مأخوذة بفلاش الهاتف الذكي. |
| `NoiseRemovalStrength` | يتحكم في شدة المعالجة (1 = منخفض، 3 = عال).       | ضبط دقيق بناءً على مدى حبيبية المصدر. |

تفعيل هذه الخيارات هو في الأساس “السر الخفي” لـ **how to improve OCR** على المدخلات غير المثالية.

## التعرف على النص من JPG باستخدام Aspose OCR

فيما يلي البرنامج الكامل القابل للتنفيذ. كل سطر مشروح حتى ترى *لماذا* وجود كل جزء، وليس فقط *ماذا* يفعل.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class PreprocessDemo
{
    static void Main()
    {
        // ------------------------------------------------------------
        // Step 1: Create an OCR engine instance.
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ------------------------------------------------------------
        // Step 2: Fine‑tune preprocessing to improve accuracy.
        // ------------------------------------------------------------
        ocrEngine.Settings.Preprocess = new PreprocessSettings
        {
            AutoDeskew = true,               // How to deskew image automatically.
            AdaptiveThreshold = true,        // Improves contrast for better recognition.
            RemoveNoise = true,              // How to remove noise before OCR.
            NoiseRemovalStrength = 2         // Medium strength; adjust 1‑3 as needed.
        };

        // ------------------------------------------------------------
        // Step 3: Load the JPG image you want to process.
        // ------------------------------------------------------------
        // If the file is missing, Aspose will throw a FileNotFoundException.
        // Wrap it in a try/catch if you need graceful fallback.
        ImageStream image;
        try
        {
            image = ImageStream.FromFile("input.jpg");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading image: {ex.Message}");
            return;
        }

        // ------------------------------------------------------------
        // Step 4: Run the OCR engine on the preprocessed image.
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ------------------------------------------------------------
        // Step 5: Display the extracted text.
        // ------------------------------------------------------------
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### النتيجة المتوقعة

إذا كان `input.jpg` يحتوي على العبارة “Invoice #12345 – Total: $256.78”، سيطبع وحدة التحكم:

```
=== Extracted Text ===
Invoice #12345 – Total: $256.78
```

لاحظ كيف أن المخرجات نظيفة، مع الحفاظ على الشرطة وعلامة الدولار—تمامًا ما تتوقعه عند **extracting text from image** الملفات.

## كيفية تصحيح ميل الصورة باستخدام إعدادات ما قبل المعالجة

لماذا يعتبر تصحيح الميل مهمًا؟ حتى ميل بمقدار درجتين يمكن أن يربك مرحلة تجزئة الأحرف، مما يؤدي إلى أخطاء في التعرف على الحروف. علامة `AutoDeskew` تشغل شبكة عصبية تلافيفية تحت الغطاء تكتشف الزاوية السائدة وتدوير الصورة إلى الوضع الأصلي.

إذا كنت تحتاج إلى مزيد من التحكم، يمكنك ضبط الزاوية يدويًا:

```csharp
ocrEngine.Settings.Preprocess = new PreprocessSettings
{
    AutoDeskew = false,          // Turn off automatic detection.
    // Manually specify a rotation angle (in degrees):
    DeskewAngle = -1.8           // Positive = clockwise, negative = counter‑clockwise.
};
```

> **متى تستخدم تصحيح الميل اليدوي:** إذا كنت تعلم أن الكاميرا تميل الصور دائمًا بكمية ثابتة (مثلاً، ماسح مثبت)، فإن ترميز الزاوية يدويًا يوفر قليلًا من وقت المعالجة.

## كيفية إزالة الضوضاء للحصول على استخراج أنظف

تظهر الضوضاء على شكل بقع عشوائية أو حبيبات، خاصة في الصور ذات الإضاءة المنخفضة. علامة `RemoveNoise` تطبق مرشح ثنائي الجانب ينعّم الخلفية مع الحفاظ على الحواف (الأحرف الفعلية). خاصية `NoiseRemovalStrength` تتيح لك ضبط شدة المعالجة:

| القوة | التأثير |
|-------|----------|
| 1     | تنعيم خفيف—مناسب للصور ذات الحبيبات الخفيفة. |
| 2     | متوازن—يعمل مع معظم لقطات الهواتف الذكية. |
| 3     | تنعيم قوي—استخدم عندما تكون الصورة شديدة الضوضاء، لكن احذر من طمس الخطوط الرفيعة. |

إذا واجهت حالة يصبح فيها الخط الصغير غير قابل للقراءة بعد التنعيم القوي، قلل ببساطة من القوة أو عطل الفلتر تمامًا.

## استخراج النص من الصورة: ما وراء JPG

بينما يركز عرضنا التجريبي على JPG، يدعم Aspose OCR صيغ PNG، BMP، TIFF، وحتى صفحات PDF. لاستخراج النص من صورة (**extract text from image**) بصيغ غير JPG، فقط غير امتداد الملف في `ImageStream.FromFile`. بالنسبة لملفات TIFF متعددة الصفحات يمكنك التكرار عبر كل صفحة:

```csharp
for (int i = 0; i < tiffPageCount; i++)
{
    ImageStream page = ImageStream.FromFile($"input_{i}.tiff");
    OcrResult result = ocrEngine.Recognize(page);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(result.Text);
}
```

هذا المقتطف يوضح كيف يمكنك توسيع سير عمل **how to improve OCR** نفسه لمعالجة دفعة من مجموعة كاملة من المستندات الممسوحة.

## المشكلات الشائعة وكيفية إصلاحها

| العَرَض | السبب المحتمل | الحل السريع |
|---------|----------------|-------------|
| مخرجات فارغة | الصورة بيضاء تمامًا بعد المعالجة (عَتَبة مفرطة) | قلل `NoiseRemovalStrength` أو اضبط `AdaptiveThreshold = false`. |
| حروف مشوشة | نموذج لغة غير صحيح (الافتراضي هو الإنجليزية) | اضبط `ocrEngine.Settings.Language = Language.English;` أو حمّل حزمة لغة مخصصة. |
| تحطم عند ملفات كبيرة | نفاد الذاكرة بسبب صورة عالية الدقة | قلل الحجم باستخدام `ocrEngine.Settings.ImageResizeFactor = 0.5;` قبل التعرف. |
| لا توجد مخرجات للمسحات المائلة | `AutoDeskew` تم تعطيله عن غير قصد | فعّل `AutoDeskew = true` أو قدّم `DeskewAngle` الصحيح. |

مراعاة هذه النقاط سيوفر لك ساعات من تصحيح الأخطاء عندما تحاول **how to improve OCR** في خطوط الإنتاج.

## إضافي: تعديل السرعة مقابل الدقة

إذا كنت تعالج آلاف الإيصالات يوميًا، قد تفضّل السرعة. عطل `AdaptiveThreshold` واضبط `NoiseRemovalStrength = 1`. وعلى العكس، بالنسبة للوثائق القانونية حيث يمكن أن يكون حرف واحد مفقودًا مكلفًا، احتفظ بجميع العلامات مفعلة وفكّر في رفع `NoiseRemovalStrength` إلى 3.

## الخلاصة

لقد غطينا الرحلة الكاملة لـ **how to improve OCR** في C# باستخدام Aspose OCR: من إنشاء المحرك، تكوين ما قبل المعالجة (الركيزة الأساسية لـ *how to deskew image* و *how to remove noise*), تحميل JPG، التعرف على النص، ومعالجة الحالات الخاصة. الكود مستقل، يعمل مباشرةً، ويظهر الخطوات الدقيقة التي تحتاجها لـ **recognize text from jpg** و **extract text from image** الملفات.

### ما التالي؟

- جرّب صيغ صور أخرى (PNG، TIFF) لترى كيف تتصرف الإعدادات نفسها.  
- دمج مخرجات OCR في قاعدة بيانات أو

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}