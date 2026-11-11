---
category: general
date: 2026-05-31
description: قم بمعالجة الصورة مسبقًا للتعرف الضوئي على الأحرف لتحسين دقة التعرف بشكل
  كبير باستخدام المعالجة المسبقة مع Aspose OCR Java. اتبع دليلًا كاملاً خطوة بخطوة.
draft: false
keywords:
- preprocess image for OCR
- improve OCR accuracy with preprocessing
language: ar
og_description: قم بتهيئة الصورة مسبقًا للتعرف الضوئي على الأحرف وتعلم كيفية تحسين
  دقة التعرف الضوئي على الأحرف من خلال المعالجة المسبقة في جافا باستخدام Aspose OCR.
og_title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف – تعزيز الدقة من خلال المعالجة
  المسبقة
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  headline: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  type: TechArticle
- description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  name: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  steps:
  - name: Loads the original PNG.
    text: Loads the original PNG.
  - name: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
    text: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
  - name: Runs the recognizer on the cleaned bitmap.
    text: Runs the recognizer on the cleaned bitmap.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف – تعزيز الدقة بالمعالجة المسبقة
url: /ar/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-accuracy-with-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preprocess Image for OCR – تعزيز الدقة باستخدام المعالجة المسبقة

هل تساءلت يومًا لماذا تبدو نتائج الـ OCR لديك فوضى مشوشة رغم أن الصورة المصدر تبدو جيدة؟ في معظم الحالات يكون السبب مخفيًا داخل الصورة — الانحراف، الضوضاء، انخفاض التباين — أشياء تُربك حتى أذكى محرك تعرّف. **Preprocess image for OCR** وستلاحظ قفزة دراماتيكية في الجودة.  

في هذا الدرس لن نُظهر لك فقط كيفية **preprocess image for OCR**، بل سنشرح أيضًا **how to improve OCR accuracy with preprocessing** من خلال بناء خط أنابيب صغير لكنه قوي باستخدام Aspose OCR for Java. في النهاية ستحصل على برنامج جاهز للتنفيذ يحوّل صورة PNG مشوشة ومائلة إلى نص نظيف وقابل للقراءة.

## ما ستتعلمه

- لماذا المعالجة المسبقة مهمة لمحركات OCR  
- كيفية إعداد Aspose OCR في مشروع Java  
- كود خطوة بخطوة **preprocess image for OCR** باستخدام فلاتر تصحيح الانحراف، إزالة الضوضاء، وتعديل التباين  
- نصائح لتعديل خط الأنابيب **improve OCR accuracy with preprocessing** على مجموعات البيانات الخاصة بك  

بدون حشو، مجرد مثال كامل قابل للتنفيذ وتفسير لكل سطر.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

| المتطلب | السبب |
|-------------|--------|
| Java 8 أو أحدث | مكتبة Aspose OCR Java تستهدف Java 8+ |
| Maven أو Gradle (اختياري) | يبسط إضافة تبعية Aspose OCR |
| ملف ترخيص Aspose OCR for Java (`Aspose.OCR.Java.lic`) | مطلوب لفتح جميع الوظائف |
| صورة نموذجية (مثال: `noisy_skewed.png`) | الصورة التي ستقوم بـ *preprocess image for OCR* عليها |

إذا كان أي من هذه غير متوفر، توقف الآن واحصل عليه—محاولة تشغيل الكود بدون ترخيص ستؤدي إلى استثناء.

## الخطوة 1: تطبيق ترخيص Aspose OCR

أولًا وقبل كل شيء. محرك OCR لن يقوم بأي شيء مفيد بدون ترخيص صالح. هذه الخطوة **preprocesses image for OCR** بشكل غير مباشر عبر فتح مجموعة الفلاتر الكاملة.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

> **نصيحة احترافية:** احفظ ملف الترخيص خارج نظام التحكم بالإصدار. استخدم متغيرات البيئة أو مخزن آمن في بيئة الإنتاج.

## الخطوة 2: تهيئة محرك OCR وتحميل الصورة المصدر

الآن ننشئ المحرك، نحدّد اللغة المتوقعة، ونشير إلى الملف الذي نريد *preprocess image for OCR* عليه.

```java
        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Set the language – English works for most demos
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);

        // Load the source image (the one that needs preprocessing)
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));
```

لماذا نحدد اللغة؟ لأن المحرك يمكنه تطبيق خوارزميات خاصة باللغة، مما **improve OCR accuracy with preprocessing** قبل حتى أن نلمس الفلاتر.

## الخطوة 3: بناء خط أنابيب المعالجة المسبقة

هذا هو قلب الدرس. هنا **preprocess image for OCR** عن طريق ربط ثلاثة فلاتر:

| الفلتر | ما يفعله | لماذا يهم للدقة |
|--------|--------------|-----------------------------|
| `AutoDeskew` | يكتشف ويصحّح الانحراف | خطوط النص المائلة تُربك تجزئة الأحرف |
| `DenoiseMedian(3)` | تقليل الضوضاء بفلتر متوسط (kernel = 3) | يزيل البقع التي تشبه الأحرف العشوائية |
| `ContrastStretch` | يمدّ الهستوجرام لزيادة التباين | الخلفيات الداكنة تصبح قابلة للقراءة، والنص الفاتح يبرز |

```java
        // Access the preprocessor
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();

        // 1️⃣ Correct image skew
        preprocessor.addFilter(new AutoDeskew());

        // 2️⃣ Reduce noise with a median filter (kernel size = 3)
        preprocessor.addFilter(new DenoiseMedian(3));

        // 3️⃣ Enhance contrast for sharper edges
        preprocessor.addFilter(new ContrastStretch());
```

لاحظ أننا لا نحتاج لكتابة أي كود معالجة صورة من الصفر—Aspose يوفر فلاتر جاهزة. هذا **improves OCR accuracy with preprocessing** بشكل كبير مع الحفاظ على تنفيذ مختصر.

## الخطوة 4: تشغيل OCR على الصورة المعالجة مسبقًا

مع وجود خط الأنابيب، يطبق المحرك الفلاتر تلقائيًا قبل التعرف. كل ما تحتاجه هو استدعاء واحد:

```java
        // Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();
```

خلف الكواليس يقوم المحرك بـ:

1. تحميل ملف PNG الأصلي.  
2. تمريره عبر `AutoDeskew`، `DenoiseMedian`، و `ContrastStretch`.  
3. تشغيل المتعرّف على البت ماب المنقّاة.  

هذا هو سحر **preprocess image for OCR**—العمل الشاق مُجرد خلفية.

## الخطوة 5: إخراج النص المتعرّف عليه

أخيرًا، اطبع النتيجة على الشاشة أو احفظها في ملف. لأغراض العرض، يكفي `System.out.println`.

```java
        // Show the extracted text
        System.out.println(extractedText);
    }
}
```

إذا سارت الأمور بسلاسة، سترى جملًا نظيفة وقابلة للقراءة بدلًا من فوضى مشوشة. يختلف الإخراج الدقيق حسب الصورة المصدر، لكنك ستلاحظ تحسنًا واضحًا مقارنةً بتشغيل OCR على الملف الخام.

### النتيجة المتوقعة (مثال)

```
The quick brown fox jumps over the lazy dog.
This is a sample text line for OCR testing.
```

إذا ما زلت تحصل على أحرف غريبة، تحقق من ترتيب الفلاتر—أحيانًا تطبيق `ContrastStretch` *قبل* `DenoiseMedian` يعطي نتائج أفضل على المسحات المتدهورة بشدة.

## تصور خط الأنابيب (اختياري)

فيما يلي مخطط يوضح تدفق الصورة عبر كل فلتر. يمكن أن يساعدك في شرح العملية للزملاء أو تضمينه في الوثائق.

![preprocess image for OCR pipeline diagram](pipeline.png "Diagram showing AutoDeskew → DenoiseMedian → ContrastStretch stages for preprocess image for OCR")

*نص بديل:* *مخطط preprocess image for OCR يوضح الفلاتر الثلاثة المطبقة قبل التعرف.*

## المشكلات الشائعة وكيفية إصلاحها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| النص لا يزال غير واضح بعد المعالجة | فلتر التباين غير كافٍ | زد عامل التمدد أو جرّب `HistogramEqualization` |
| OCR يرمي `NullPointerException` | مسار ملف الترخيص غير صحيح | تحقق من المسار وتأكد من إمكانية قراءة الملف |
| الانحراف لا يزال موجودًا | دوران الصورة > 15° (حد AutoDeskew) | قم بالدوران يدويًا باستخدام `AffineTransform` قبل خط الأنابيب |
| الكثير من الإيجابيات الزائفة | مستوى الضوضاء عالي، حجم kernel منخفض | زد حجم kernel للمتوسط (مثال: `new DenoiseMedian(5)`) |

بتوقع هذه القضايا ستحقق **improve OCR accuracy with preprocessing** حتى على أصعب المسحات.

## توسيع خط الأنابيب

هل تريد مزيدًا من التحكم؟ Aspose OCR يتيح لك إضافة فلاتر مخصصة أو إعادة ترتيب الموجودة. إليك بعض الأفكار:

- **Binarization**: `preprocessor.addFilter(new BinarizeOtsu());` – يفرض أبيض وأسود نقي، مفيد للمستندات المطبوعة.  
- **Resize**: `preprocessor.addFilter(new Scale(2.0));` – يرفع دقة الصور منخفضة الوضوح، غالبًا ما يعزز الدقة.  
- **Sharpen**: `preprocessor.addFilter(new Sharpen());` – يبرز الحواف للخطوط الصغيرة.

تذكر أن كل فلتر إضافي يزيد من زمن المعالجة، لذا قم بالاختبار على الأجهزة المستهدفة.

## الكود الكامل (جاهز للنسخ واللصق)

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create the OCR engine and configure language & source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));

        // Step 3: Build a preprocessing pipeline to improve OCR accuracy with preprocessing
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();
        preprocessor.addFilter(new AutoDeskew());               // Correct image skew
        preprocessor.addFilter(new DenoiseMedian(3));           // Reduce noise (kernel size = 3)
        preprocessor.addFilter(new ContrastStretch());         // Enhance contrast

        // Step 4: Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println(extractedText);
    }
}
```

احفظه كـ `PreprocessDemo.java`، أضف JAR الخاص بـ Aspose OCR إلى مسار الـ classpath (أو أعلن عنه في Maven)، ثم شغّله:



## ما الذي يجب أن تتعلمه بعد ذلك؟

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [How to calculate skew angle java using Aspose.OCR](/ocr/english/java/ocr-basics/calculate-skew-angle/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}