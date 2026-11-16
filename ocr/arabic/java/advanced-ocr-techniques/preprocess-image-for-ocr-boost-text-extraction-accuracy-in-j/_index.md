---
category: general
date: 2026-03-28
description: قم بتهيئة الصورة للتعرف الضوئي على الأحرف (OCR) وتعرف على النص من الصورة
  باستخدام Aspose OCR. تعلم كيفية استخراج النص من الصورة وتحسين دقة OCR من خلال خطوات
  تمهيدية خطوة بخطوة.
draft: false
keywords:
- preprocess image for OCR
- recognize text from image
- extract text from photo
- improve OCR accuracy preprocessing
- Aspose OCR Java
- image preprocessing pipeline
language: ar
og_description: قم بتهيئة الصورة مسبقًا للتعرف الضوئي على الأحرف واستخراج النص من
  الصورة باستخدام Aspose OCR Java. اتبع هذا الدليل لتحسين دقة التعرف الضوئي على الأحرف
  من خلال المعالجة المسبقة في بضع خطوات فقط.
og_title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف – دليل جافا الكامل
tags:
- OCR
- Java
- Image Processing
title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف – تحسين دقة استخراج النص في جافا
url: /ar/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-text-extraction-accuracy-in-j/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجـة الصورة مسبقًا للتعرف الضوئي على الأحرف – دليل Java كامل

هل حاولت يومًا **preprocess image for OCR** وما زلت تحصل على مخرجات مشوشة؟ لست وحدك. في العديد من المشاريع الواقعية، يحتوي المسح الخام أو صورة الهاتف الذكي على ميل، ضوضاء، أو تباين منخفض يفسد حتى أكثر محركات التعرف ذكاءً. الخبر السار؟ خط أنابيب معالجة مسبقة قصير — de‑skew، denoise، binarize — يمكنه تحسين **improve OCR accuracy preprocessing** بشكل كبير.

في هذا البرنامج التعليمي سنستعرض مثالًا عمليًا يوضح لك بالضبط كيفية **recognize text from image** باستخدام Aspose OCR for Java. في النهاية ستتمكن من **extract text from photo** للملفات مع أخطاء أقل بكثير، وستفهم لماذا كل خطوة معالجة مسبقة مهمة.

> **ما ستحصل عليه**  
> * برنامج Java قابل للتنفيذ بالكامل يقوم بتحميل صورة مائلة، يطبق ثلاثة فلاتر كلاسيكية، ويطبع نصًا نظيفًا.  
> * نظرة عميقة على “السبب” وراء de‑skew، denoise، و binarize.  
> * نصائح للتعامل مع الحالات الطرفية — ملفات كبيرة، صيغ صور مختلفة، وترتيب الفلاتر المخصص.

## المتطلبات المسبقة

- Java 8 أو أحدث مثبت (الكود يُجمّع مع JDK 11 أيضًا).  
- Maven أو Gradle لجلب مكتبة Aspose OCR.  
- صورة نموذجية (مثال: `angled-photo.jpg`) مائلة قليلًا وتحتوي على بعض الضوضاء البصرية.  
- إلمام أساسي بطريقة `main` في Java — لا تحتاج إلى خبرة عميقة في OCR.

إذا كنت تفتقد أيًا من هذه المتطلبات، فقط احصل على أحدث JDK من Oracle أو OpenJDK وأضف الاعتماد التالي لـ Maven إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Maven Central for the newest version -->
</dependency>
```

## الخطوة 1 – إنشاء كائن محرك OCR

أول شيء تحتاجه هو كائن `OcrEngine`. فكر فيه كالعقل الذي سيقرأ لاحقًا الصورة المعالجة.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:** المحرك يضم إعدادات التعرف، حزم اللغات،—والأهم بالنسبة لنا—خيارات المعالجة المسبقة. بدون ذلك، سيتعين عليك ربط مكتبات معالجة الصور يدويًا، مما يُفقد خط الأنابيب النظيف هدفه.

## الخطوة 2 – بناء خط أنابيب المعالجة المسبقة (de‑skew → denoise → binarize)

تأتي Aspose OCR مع فئة `PreprocessingOptions` مدمجة تسمح لك بترتيب الفلاتر بالترتيب الدقيق الذي تحتاجه. هنا نضيف ثلاثة فلاتر:

1. **DE_SKEW** – يسطّح النص المائل.  
2. **DENOISE** – ينعم البكسلات الحبيبية التي قد تُخطئ كحروف.  
3. **BINARIZE** – يحول الصورة إلى أبيض وأسود نقي، مما يسهل عمل محرك OCR.

```java
        // Step 2: Assemble the preprocessing pipeline
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);   // correct rotation
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);  // remove grain
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE); // high‑contrast B&W

        // Attach the pipeline to the OCR engine
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);
```

> **نصيحة احترافية:** ترتيب الفلاتر أمر حاسم. إذا قمت بعملية binarize *قبل* denoise، قد تتحول الضوضاء إلى بقع سوداء حادة تُربك المُعرّف. de‑skew أولاً يضمن أن خط أساس النص أفقي، مما يحسن نتائج كل من denoise و binarize.

## الخطوة 3 – تمرير الصورة إلى المحرك

الآن نوجه المحرك إلى الملف الذي نريد قراءته. يمكن أن يكون المسار مطلقًا أو نسبيًا لجذر مشروعك.

```java
        // Step 3: Run OCR on the target image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

> **ماذا لو كانت الصورة ضخمة؟** تقوم Aspose OCR تلقائيًا بتقليل حجم الصور التي يزيد طولها عن 2000 px على الجانب الأطول، لكن يمكنك تجاوز ذلك عبر `ocrEngine.getRecognitionSettings().setMaxImageDimension(1500)` إذا كان الذاكرة تشكل قلقًا.

## الخطوة 4 – إخراج النص المُعترف به

أخيرًا، نطبع السلسلة المستخرجة إلى وحدة التحكم. في تطبيق حقيقي قد تكتبها إلى قاعدة بيانات، ملف، أو تمررها إلى خط أنابيب NLP لاحق.

```java
        // Step 4: Print the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### النتيجة المتوقعة

إذا كان ملف `angled-photo.jpg` يحتوي على الجملة *“The quick brown fox jumps over the lazy dog.”* يجب أن ترى شيئًا مشابهًا:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

لاحظ كيف أن المخرجات نظيفة — لا رموز عشوائية، لا أسطر مكسورة. هذه هي قوة **preprocess image for OCR**.

## الخطوة 5 – التحقق والتعديل (اختياري)

حتى مع خط أنابيب قوي، قد تواجه حالات طرفية:

| الحالة | التعديل المقترح |
|-----------|-----------------|
| **تباين منخفض جدًا** (مثال: مستندات ممسوحة باهتة) | أضف فلتر `ContrastAdjustment` إضافي قبل binarization. |
| **خلفية ملونة** (مثال: إيصالات بطوابع ملونة) | أضف فلتر `BackgroundRemoval` أو حوّل إلى تدرج الرمادي يدويًا أولاً. |
| **ملفات PDF متعددة الصفحات** | كرّر عبر صورة كل صفحة وأعد استخدام نفس `preprocessingOptions`. |

يمكنك التجربة عبر استدعاء `preprocessingOptions.addFilter(PreprocessFilter.CONTRAST)` أو أي فلتر آخر مدرج في وثائق Aspose OCR API.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل، جاهز للنسخ واللصق في ملف باسم `PreprocessExample.java`. تأكد من حل اعتماد Maven قبل التجميع.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing: de‑skew → denoise → binarize
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE);
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);

        // 3️⃣ Perform OCR on the chosen image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // 4️⃣ Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

قم بالتجميع والتشغيل:

```bash
mvn compile exec:java -Dexec.mainClass=PreprocessExample
```

سترى النص النظيف يُطبع على وحدة التحكم، مما يؤكد أنك نجحت في **preprocess image for OCR** و **recognize text from image**.

## أسئلة شائعة وإجابات

**س1: هل يعمل هذا مع ملفات PNG أو TIFF؟**  
نعم — تدعم Aspose OCR صيغ JPEG، PNG، BMP، TIFF، والعديد من الصيغ الأخرى. يُطبق نفس خط أنابيب المعالجة المسبقة؛ المكتبة تكتشف الصيغة تلقائيًا.

**س2: ماذا لو احتجت لاستخراج النص من صورة تم التقاطها بالهاتف؟**  
غالبًا ما تعاني صور الهاتف من إضاءة غير متساوية. إضافة فلتر `LIGHTING_CORRECTION` قبل binarization يمكن أن يساعد. التغيير في الكود هو سطر واحد:

```java
preprocessingOptions.addFilter(PreprocessFilter.LIGHTING_CORRECTION);
```

**س3: هل يمكنني تغيير لغة OCR؟**  
بالطبع. بعد إنشاء المحرك، اضبط اللغة:

```java
ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.SPANISH);
```

**س4: كيف يُحسّن هذا من دقة OCR في المعالجة المسبقة؟**  
كل فلتر يقلل نوعًا معينًا من الضوضاء البصرية. de‑skew يضبط خطوط النص، denoise يزيل البقع العشوائية، و binarize يخلق صورة ذات تباين عالي. معًا يمنحان خوارزمية التعرف إشارة أنظف، مما يترجم إلى دقة أعلى على مستوى الأحرف — غالبًا زيادة بنسبة 15‑30 % على المدخلات الضوضائية.

## الخطوات التالية والمواضيع ذات الصلة

- **المعالجة الدفعية:** غلف المنطق الأساسي داخل حلقة للتعامل مع مجلدات كاملة من الصور.  
- **ترتيب الفلاتر المخصص:** جرّب `BINARIZE` قبل `DENOISE` للوثائق التي هي بالفعل ذات تباين عالي.  
- **تحسين الأداء:** استخدم `ocrEngine.getRecognitionSettings().setThreadCount(4)` لتوازي المعالجة على أجهزة متعددة الأنوية.  
- **مكتبات بديلة:** قارن بين Aspose OCR و Tesseract‑Java للسيناريوهات المفتوحة المصدر.  
- **ما بعد المعالجة:** طبّق تدقيق إملائي أو تنظيف regex على المخرجات الخام للحصول على نتائج أنظف.

من خلال إتقان سير عمل **preprocess image for OCR**، ستجد أن استخراج النص من مصادر الصور يصبح مهمة قابلة للتنبؤ وتكرارها بدلاً من تجربة عشوائية.

---

*هل أنت مستعد لتعزيز خط أنابيب OCR الخاص بك؟ احصل على الكود، عدّل الفلاتر، وشاهد الدقة ترتفع. إذا واجهت أي مشكلة، اترك تعليقًا أدناه — برمجة سعيدة!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}