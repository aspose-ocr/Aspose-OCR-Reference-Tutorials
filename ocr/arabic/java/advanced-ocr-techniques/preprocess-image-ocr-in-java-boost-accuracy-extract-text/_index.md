---
category: general
date: 2026-01-07
description: معالجة صورة OCR مسبقًا لتحسين دقة OCR واستخراج النص من الصورة باستخدام
  Aspose OCR – دليل خطوة بخطوة للمطورين.
draft: false
keywords:
- preprocess image OCR
- extract text image
- improve OCR accuracy
- how to preprocess OCR
language: ar
og_description: معالجة مسبقة لصورة OCR لتحسين دقة OCR واستخراج نص الصورة باستخدام
  Aspose OCR. دليل Java كامل مع الكود.
og_title: معالجة مسبقة لتقنية OCR للصور في جافا – زيادة الدقة
tags:
- OCR
- Java
- Image Processing
title: معالجة مسبقة لتقنية OCR للصور في جافا – تحسين الدقة واستخراج النص
url: /ar/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة صورة OCR في جافا – دليل شامل

هل واجهت صعوبة في **معالجة صورة OCR** لأن مسحاتك تبدو كفوضى من البقع والنص المائل؟ لست وحدك. معظم المطورين يصطدمون بالحائط عندما تكون الصورة الخام مليئة بالضوضاء أو مائلة أو ذات تباين منخفض، وتنتج محرك OCR نصًا غير مفهوم بدلاً من الجمل المتوقعة.  

الخبر السار هو أن بعض خطوات ما قبل المعالجة يمكنها تحسين **دقة OCR** بشكل كبير، وتحويل لقطة غير مستقرة إلى نص نظيف يمكن للآلة قراءته. في هذا الدرس سنستعرض بالضبط **كيفية معالجة OCR** باستخدام Aspose OCR لجافا، وسترى كيف يمكنك **استخراج نص الصورة** بشكل موثوق.

سنغطي كل ما تحتاجه: المكتبات المطلوبة، كود خطوة بخطوة، لماذا كل خيار مهم، ونصائح للحالات الخاصة التي قد تواجهها. في النهاية ستحصل على برنامج جاهز للتنفيذ يأخذ صورة JPEG مشوشة، ينظفها، ويطبع النص المستخرج على وحدة التحكم.

---

## ما الذي ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

- مجموعة تطوير جافا (JDK) 8 أو أحدث مثبتة.
- Maven أو Gradle لإدارة التبعيات (سنظهر مقتطف Maven).
- رخصة Aspose OCR لجافا (الإصدار التجريبي المجاني يكفي للاختبار).
- صورة نموذجية، مثلاً `skewed-noisy.jpg`، موجودة في دليل معروف.

هذا كل شيء—لا تحتاج إلى مكتبات معالجة صورة إضافية لأن Aspose OCR يأتي مع قدرات ما قبل المعالجة مدمجة.

---

## الخطوة 1: إعداد Aspose OCR في مشروعك

أولاً، أضف تبعية Aspose OCR إلى ملف `pom.xml`. سيؤدي ذلك إلى جلب محرك الأساس ومساعدي معالجة الصورة الذين سنستخدمهم لاحقًا.

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- use the latest version available -->
</dependency>
```

إذا كنت تفضل Gradle، فالمكافئ هو:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **نصيحة احترافية:** حافظ على تحديث تبعياتك؛ الإصدارات الأحدث غالبًا ما تتضمن خوارزميات تصحيح الميل (deskew) أكثر ذكاءً تُحسّن **دقة OCR**.

---

## معالجة صورة OCR – الخطوة 2: تحميل الصورة

الآن بعد أن أصبحت المكتبة جاهزة، يمكننا إنشاء كائن `OcrEngine` وتوجيهه إلى الصورة التي تريد تنظيفها.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to preprocess
        // Replace "YOUR_DIRECTORY" with the actual folder path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/skewed-noisy.jpg"));
```

لماذا ننشئ المحرك أولاً؟ لأن Aspose OCR يربط خط أنابيب ما قبل المعالجة مباشرة بالمحرك، لذا أي خيار تضبطه لاحقًا سيؤثر على نفس تدفق الصورة. هذا يضمن أن عملية **استخراج نص الصورة** تعمل على النسخة المنقحة، وليس على الملف الخام.

---

## تحسين دقة OCR – الخطوة 3: ضبط خيارات ما قبل المعالجة

السحر يحدث في `ImageProcessingOptions`. كل علم يستهدف عيبًا شائعًا يضر بأداء OCR.

```java
        // Step 3: Configure image preprocessing options
        ImageProcessingOptions processingOptions = ocrEngine.getImageProcessingOptions();

        // Straighten rotated text – essential for skewed scans
        processingOptions.setDeskew(true);

        // Remove isolated pixels that look like speckles
        processingOptions.setDespeckle(true);

        // Boost contrast by 30% – helps low‑contrast prints
        processingOptions.setContrastBoost(1.3f);
```

- **Deskew**: يكتشف زاوية الدوران ويعيد تدوير الصورة لتصبح أفقية. بدون ذلك قد يخطئ محرك OCR في تفسير الأحرف.
- **Despeckle**: يزيل الضوضاء العشوائية التي قد تُخطئ كعلامات ترقيم أو أحرف متفرقة.
- **Contrast Boost**: يعزز الفرق بين المقدمة (النص) والخلفية، وهو عامل رئيسي في **كيفية معالجة OCR** للطباعة الخفيفة.

يمكنك تشغيل أو إيقاف هذه العلامات حسب مادة المصدر. على سبيل المثال، قد لا تحتاج مستندًا مُمسوحًا بشكل مثالي إلى `setDespeckle(true)`، مما يوفر بضع مللي ثانية.

---

## استخراج نص الصورة – الخطوة 4: تشغيل OCR على الصورة المعالجة

بعد تنظيف الصورة، نطلب من Aspose OCR أخيرًا التعرف على النص.

```java
        // Step 4: Run OCR on the preprocessed image
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

نداء `recognize()` يطبق داخليًا خط أنابيب ما قبل المعالجة الذي ضبطناه، ثم يقوم بتقسيم الأحرف والتعرف عليها. النتيجة هي سلسلة نصية عادية يمكنك تمريرها إلى عمليات لاحقة—فهرسة بحث، أتمتة إدخال بيانات، وما إلى ذلك.

---

## كيفية معالجة OCR – المشكلات الشائعة والحالات الخاصة

### 1. حجم الصورة مهم
الصور الكبيرة جدًا (مثلاً > 5 MP) قد تسبب ضغطًا على الذاكرة. إذا واجهت `OutOfMemoryError`، قلل حجم الصورة أولًا باستخدام `processingOptions.setResizeFactor(0.5f)`.

### 2. اللون مقابل التدرج الرمادي
يعمل Aspose OCR بأفضل شكل مع الصور ذات التدرج الرمادي. إذا كان مصدر الصورة ملونًا، فعّل `processingOptions.setConvertToGrayscale(true)` قبل عملية تصحيح الميل.

### 3. ملفات PDF متعددة الصفحات
عند التعامل مع PDFs، استخرج كل صفحة كصورة وشغّل نفس الخط أنابيب في حلقة. توفر الواجهة `PdfImageExtractor` لهذا الغرض.

### 4. دعم اللغات
إذا لم يكن النص باللغة الإنجليزية، اضبط اللغة صراحةً:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

تجاوز هذه الخطوة قد يقلل من **تحسين دقة OCR** لأن المحرك سيحاول تخمين مجموعة الأحرف.

---

## مثال كامل جاهز للتنفيذ (انسخه‑الصقه)

فيما يلي البرنامج الكامل، جاهز للترجمة والتشغيل. استبدل مسار العنصر النائب بموقع صورتك الفعلي.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image to be processed
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/skewed-noisy.jpg"));

        // Step 3: Configure image preprocessing options
        ImageProcessingOptions processingOptions = ocrEngine.getImageProcessingOptions();
        processingOptions.setDeskew(true);          // straighten rotated text
        processingOptions.setDespeckle(true);      // remove isolated pixels
        processingOptions.setContrastBoost(1.3f);   // boost contrast by 30%
        // Optional: processingOptions.setConvertToGrayscale(true);

        // Step 4: Run OCR on the preprocessed image
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**الناتج المتوقع** (مقتطع للختصار):

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
```

إذا رأيت أحرفًا مشوشة، تأكد من صحة مسار الصورة وأن علامات ما قبل المعالجة تتطابق مع حالة الصورة.

---

## ملخص بصري

<img src="preprocess-ocr.png" alt="preprocess image OCR demonstration" style="max-width:100%;">

الرسم البياني يوضح التدفق: **تحميل → تصحيح الميل → إزالة البقع → تعزيز التباين → التعرف → استخراج النص**. كل صندوق يتطابق مع مقتطفات الكود أعلاه.

---

## الخاتمة

لقد استعرضنا طريقة عملية لـ **معالجة صورة OCR** في جافا باستخدام Aspose OCR، بدءًا من إعداد المشروع وحتى ضبط الخيارات التي **تحسن دقة OCR**. من خلال تطبيق تصحيح الميل، إزالة البقع، وتعزيز التباين، تحول صورة JPEG مشوشة ومائلة إلى نص نظيف قابل للبحث—وهو بالضبط ما تحتاجه عندما تريد **استخراج نص الصورة** لتطبيقات لاحقة.

ما الخطوة التالية؟ جرّب ميزات ما قبل المعالجة الأخرى مثل `setBinarizationThreshold` للصور الثنائية، أو ربط عدة صور في مهمة دفعة واحدة. يمكنك أيضًا دمج النتيجة مع Apache Tika للفهرسة، أو تمريرها إلى نموذج لغة لتحليل المشاعر. السماء هي الحد عندما تتقن أساسيات **كيفية معالجة OCR**.

هل لديك أسئلة حول نوع ملف معين أو لغة معينة؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}