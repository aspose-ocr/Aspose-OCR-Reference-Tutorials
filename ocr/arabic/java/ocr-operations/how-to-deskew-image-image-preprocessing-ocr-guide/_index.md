---
category: general
date: 2026-06-22
description: 'كيفية تصحيح إمالة الصورة للتعرف الضوئي على الأحرف: تعلم خطوات ما قبل
  معالجة الصورة للتعرف الضوئي على الأحرف، إزالة ضوضاء الملح والفلفل، وتعزيز الدقة.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: ar
og_description: كيفية تصحيح انحراف الصورة للتعرف الضوئي على الأحرف، إزالة ضوضاء الملح
  والفلفل، وتطبيق تقنيات ما قبل معالجة الصور للتعرف الضوئي على الأحرف في مثال Java
  كامل.
og_title: كيفية تصحيح إمالة الصورة – دليل معالجة الصور المسبق للتعرف الضوئي على الأحرف
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: كيفية تصحيح ميل الصورة – دليل معالجة الصور المسبق لتقنية OCR
url: /ar/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح إمالة الصورة – دليل معالجة الصور المسبقة لـ OCR

هل تساءلت يومًا **how to deskew image** لكي يقرأ محرك OCR الخاص بك النص فعليًا؟ لست وحدك. يمكن للمسح المائل أن يحول مستندًا مثاليًا إلى فوضى مشوهة، وغالبًا ما يواجه معظم المطورين هذه المشكلة مرة واحدة على الأقل.

في هذا الدرس سنستعرض خط أنابيب كامل لـ **image preprocessing OCR** لا يصحح الدوران فحسب، بل يزيل أيضًا عيوب **remove[s] salt pepper** ويعزز التباين — باختصار كل ما تحتاجه لـ **preprocess images OCR**‑style قبل إمداده إلى المحرك. في النهاية ستحصل على مقتطف Java جاهز للتنفيذ ونموذج ذهني واضح لأهمية كل خطوة.

## كيفية تصحيح إمالة الصورة – بناء خط أنابيب المعالجة المسبقة

قلب أي سير عمل صديق لـ OCR هو كائن **preprocess options** الذي يربط سلسلة من الفلاتر. فكر فيه كحزام ناقل: كل فلتر يقوم بمهمة واحدة، ثم يمرر الصورة إلى التالي. أدناه مثال بسيط لكنه كامل باستخدام مكتبة OCR افتراضية تتضمن `DeskewFilter` و `DenoiseFilter` و `ContrastBoostFilter`.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### لماذا هذا يعمل

* **DeskewFilter** يحلل خطوط النص السائدة في الصورة، يقدّر الزاوية، ويُدوّر البت ماب إلى الوضع الأفقي. معظم المكتبات تقيد التصحيح عند ±15° لأن الزوايا الأكبر عادةً تشير إلى صفحة ممسوحة سيئًا تحتاج إلى تدخل يدوي.
* **DenoiseFilter** يستهدف نمط *salt‑and‑pepper* الكلاسيكي — تلك البكسلات السوداء أو البيضاء المعزولة التي تشبه التشويش على شاشة التلفاز. إزالتها تمنع محرك OCR من الخلط بين الضوضاء والحروف.
* **ContrastBoostFilter** يمدّد المدرج التكراري، مما يجعل الخطوط الخفيفة بارزة. مضاعف `1.5f` هو قيمة افتراضية آمنة؛ يمكنك رفعه إذا كانت مسحاتك باهتة جدًا.

> **نصيحة احترافية:** إذا كنت تعلم أن مستنداتك لا تتجاوز إمالة 10°، مرّر هذا الحد الأصغر إلى `DeskewFilter` — سيعمل الخوارزم أسرع وأقل احتمالًا لتصحيح مفرط.

## معالجة الصور المسبقة لـ OCR: إضافة الفلاتر بالترتيب الصحيح

الترتيب مهم. تخيّل أنك تقوم بإزالة الضوضاء *قبل* تصحيح الإمالة؛ قد تُربك الضوضاء اكتشاف الزاوية، مما يؤدي إلى نتيجة غير محاذاة. وعلى العكس، تطبيق تعزيز التباين *بعد* التصحيح يضمن أن الدوران لا يُدخل عيوبًا جديدة.

أدناه قائمة مراجعة سريعة يمكنك نسخها‑لصقها في أي مشروع:

| الخطوة | الفلتر | السبب |
|------|--------|--------|
| 1 | `DeskewFilter` | يوازن خط أساس النص |
| 2 | `DenoiseFilter` | يزيل الضوضاء البكسلية المعزولة |
| 3 | `ContrastBoostFilter` | يعزز وضوح النص لـ OCR |

إذا احتجت لإدراج خطوات إضافية — مثل فلتر **binarization** لـ OCR الثنائي — فستضعه **بعد** تعزيز التباين، لأن الصورة النظيفة ذات التباين العالي تُصبح ثنائية بدقة أكبر.

## إزالة ضوضاء الملح والفلفل باستخدام DenoiseFilter

ضوضاء *salt‑and‑pepper* مشهورة في المسحات منخفضة الجودة، خاصةً تلك الملتقطة بهواتف رخيصة. `DenoiseFilter` في مكتبتنا يطبق نواة مرشح متوسط، الذي يستبدل كل بكسل بمتوسط جيرانه. النتيجة؟ تختفي تلك البقع دون تمويه الأحرف الفعلية.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*متى يجب زيادة حجم النواة؟* إذا كانت صورك المصدر مليئة بالبقع الكبيرة، فإن نواة أكبر ستنظفها، لكن احذر: إذا كانت كبيرة جدًا قد تبدأ في محو الخطوط الدقيقة في الخطوط الصغيرة.

## معالجة الصور المسبقة لـ OCR – تطبيق خط الأنابيب

بمجرد تجميع سلسلة الفلاتر، ربطها بالمحرك يصبح سطرًا واحدًا (`engine.setPreprocessOptions`). من تلك اللحظة، كل استدعاء لـ `recognizeText` يمر تلقائيًا عبر خط الأنابيب. لا حاجة لاستدعاء كل فلتر يدويًا — يبقى كودك منظمًا، وأي تغييرات مستقبلية (إضافة فلتر جديد، تعديل المعلمات) تكون مركزة.

إليك ما يبدو عليه تشغيل ناجح مع مسح تجريبي كان في الأصل يميل 12° ويحتوي على ضوضاء ملحية ملحوظة:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

لاحظ كيف أن النص نظيف، موجه بشكل صحيح، وخالٍ من الأحرف العشوائية التي كانت ستظهر كـ “I n v o i c e” أو “$‑‑‑”.

## الحالات الحدية والمشكلات الشائعة

| الحالة | ما الذي يجب مراقبته | الحل المقترح |
|-----------|-------------------|---------------|
| Rotation > 15° | قد يتوقف DeskewFilter | قم بالدوران المسبق يدويًا أو استخدم فلتر نطاق أعلى |
| دقة منخفضة جدًا ( < 100 dpi ) | لا يستطيع تعزيز التباين استعادة التفاصيل | أعد تحجيم الصورة أولاً (مثال: `ResampleFilter`) |
| ضوضاء مختلطة (Gaussian + salt‑pepper) | DenoiseFilter وحده غير كافٍ | ربط `GaussianBlurFilter` قبل `DenoiseFilter` |
| مسحات ملونة بنص ملون | الحاجة إلى تحويل إلى تدرج الرمادي | أدخل `GrayscaleFilter` قبل تعزيز التباين |

من خلال توقع هذه السيناريوهات ستحفظ نفسك ساعات من تصحيح الأخطاء لاحقًا.

## مثال كامل يعمل (الكل‑في‑واحد)

أدناه فئة Java مستقلة يمكنك وضعها في أي مشروع Maven أو Gradle يتضمن تبعية `com.example.ocr`. تُظهر **how to deskew image**، **remove salt pepper**، و**preprocess images OCR**‑style.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**الناتج المتوقع** (بافتراض أن `scanned-document.png` يحتوي على فاتورة واضحة):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

إذا استبدلت الصورة بأخرى مُحاذاة تمامًا، ستلاحظ أن خط الأنابيب لا يزال يعمل — لا شيء يتعطل، وتظل دقة OCR عالية.

## الخاتمة

أنت الآن تمتلك فهماً قويًا لـ **how to deskew image** ولماذا كل خطوة من خطوات المعالجة المسبقة — **image preprocessing OCR**, **remove salt pepper**, و**preprocess images OCR** — تلعب دورًا حيويًا في تقديم نص نظيف وقابل للبحث. المثال أعلاه هو مثال كامل،

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية استخدام AspOCR: فلاتر معالجة صورة OCR لـ .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [حساب زاوية الإمالة لمعالجة صورة OCR](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [كيفية ضبط قيمة العتبة في التعرف على صورة OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}