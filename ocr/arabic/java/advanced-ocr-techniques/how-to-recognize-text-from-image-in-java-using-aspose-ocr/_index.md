---
category: general
date: 2026-09-29
description: تعلم كيفية التعرف على النص من الصورة باستخدام Java و Aspose OCR. يوضح
  هذا الدليل أيضًا كيفية استخراج النص من ملفات JPG وكيفية تحسين دقة OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- extract text from jpg
- how to improve OCR accuracy
- Aspose OCR Java
- Java image processing
language: ar
lastmod: 2026-09-29
og_description: التعرف على النص من الصورة في جافا باستخدام Aspose OCR. اتبع هذا الدليل
  خطوة بخطوة لاستخراج النص من ملف JPG وتعلم كيفية تحسين دقة OCR.
og_image_alt: Java code screenshot that recognizes text from image using Aspose OCR
og_title: التعرف على النص من الصورة في جافا – دليل Aspose OCR الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to recognize text from image with Java and Aspose OCR. This
    guide also shows how to extract text from jpg and how to improve OCR accuracy.
  headline: How to recognize text from image in Java using Aspose OCR
  type: TechArticle
- description: Learn how to recognize text from image with Java and Aspose OCR. This
    guide also shows how to extract text from jpg and how to improve OCR accuracy.
  name: How to recognize text from image in Java using Aspose OCR
  steps:
  - name: '**Pre‑process the image** – apply contrast stretching or binarization using
      OpenCV before handing it to Aspose OCR. Cleaner edges give higher confidence.'
    text: '**Pre‑process the image** – apply contrast stretching or binarization using
      OpenCV before handing it to Aspose OCR. Cleaner edges give higher confidence.'
  - name: '**Crop unnecessary margins** – the engine spends time analyzing blank space,
      which can lower the overall confidence score.'
    text: '**Crop unnecessary margins** – the engine spends time analyzing blank space,
      which can lower the overall confidence score.'
  - name: '**Choose the correct language pack** – loading only the languages you need
      speeds up recognition and reduces false positives.'
    text: '**Choose the correct language pack** – loading only the languages you need
      speeds up recognition and reduces false positives.'
  - name: '**Use the latest Aspose OCR version** – each release includes updated neural
      models that improve accuracy out‑of‑the‑box.'
    text: '**Use the latest Aspose OCR version** – each release includes updated neural
      models that improve accuracy out‑of‑the‑box.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: كيفية التعرف على النص من صورة في جافا باستخدام Aspose OCR
url: /ar/java/advanced-ocr-techniques/how-to-recognize-text-from-image-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف على النص من صورة في جافا باستخدام Aspose OCR

إذا كنت بحاجة إلى **التعرف على النص من صورة** في تطبيق جافا، فإن هذا الدليل يوضح لك حلاً جاهزًا للتنفيذ. ستتعرف على كيفية استخراج النص من ملفات jpg، تمكين تسريع GPU، وتطبيق تصحيح الإملاء للإجابة على السؤال الشائع *كيف تحسن دقة OCR*.

يغطي الدليل كل ما تحتاجه: إعداد Maven، الشيفرة المصدرية الكاملة، شرح كل خيار تكوين، ونصائح للتعامل مع الصور منخفضة الجودة. في النهاية ستحصل على برنامج يعمل ويطبع النص المعترف به على وحدة التحكم.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* Java 17 (أو أحدث) مثبت – يدعم Aspose OCR Java 8+ لكن الإصدارات الأحدث تعطي أداءً أفضل.
* Maven 3.8+ لإدارة الاعتمادات.
* رخصة Aspose OCR for Java (الإصدار التجريبي المجاني يكفي للتقييم).  
* صورة JPG (`sample.jpg`) تحتوي على نص واضح ومقروء.

إذا كان أي من هذه مفقودًا، قم بتثبيت JDK من [oracle.com/java](https://www.oracle.com/java/technologies/downloads/) واتبع دليل تثبيت Maven على موقع Apache.

## إضافة Aspose OCR إلى مشروعك

أنشئ ملف `pom.xml` (أو أضفه إلى ملف موجود) وضمنه اعتماد Aspose OCR:

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <dependencies>
    <dependency>
      <groupId>com.aspose</groupId>
      <artifactId>aspose-ocr</artifactId>
      <version>23.12</version> <!-- latest stable at time of writing -->
    </dependency>
  </dependencies>
</project>
```

شغّل `mvn clean compile` لتنزيل المكتبة. يجلب الاعتماد جميع الثنائيات الأصلية المطلوبة لاستخدام GPU وتصحيح الإملاء.

## الخطوة 1: إعداد محرك OCR للتعرف على النص من الصورة

أول ما تقوم به هو إنشاء نسخة من `OcrEngine`. هذا الكائن يدير كامل خط أنابيب OCR.

```java
// Step 1: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

إنشاء المحرك لا يحمل أي صورة بعد؛ فهو فقط يجهز الموارد الداخلية. هذا الفصل يسمح لك بإعادة استخدام نفس المحرك لعدة صور، وهو مفيد في سيناريوهات الدفعات.

## الخطوة 2: تمكين تسريع GPU لمعالجة أسرع

إذا كان جهازك يحتوي على GPU متوافق، فإن تشغيله يمكن أن يقلل وقت التعرف بنسبة تصل إلى 70 ٪. هذا يجيب مباشرةً على *كيف تحسن دقة OCR* من حيث السرعة، مما يتيح لك استخدام صور ذات دقة أعلى دون تأثير على الأداء.

```java
// Step 2 (optional): Use GPU if available
engine.getConfiguration().setUseGpu(true);
```

> **نصيحة احترافية:** عند التشغيل على خادم بدون واجهة رسومية، تأكد من تثبيت تعريفات CUDA؛ وإلا سيعود الاستدعاء إلى CPU دون حدوث خطأ.

## الخطوة 3: تفعيل تصحيح الإملاء لتحسين دقة OCR

تصحيح الإملاء هو نموذج لغوي خفيف يصلح الأخطاء الشائعة في التعرف (مثال: “l0ve” → “love”). تفعيله أحد أكثر الطرق فعالية للإجابة على *كيف تحسن دقة OCR* للنص المطبوع.

```java
// Step 3 (optional): Enable spell correction
engine.getConfiguration().setSpellCorrector(true);
```

إذا كنت تعالج ملاحظات مكتوبة بخط اليد، قد ترغب في تعطيل هذه الميزة لأن النموذج مخصص للخطوط المطبوعة.

## الخطوة 4: تحميل صورة JPG التي تريد استخراج النص منها

الآن قم بتحميل ملف الصورة. الدالة المساعدة `ImageStream.fromFile` تقبل أي صيغة يدعمها Aspose OCR، لكن المثال يركز على JPG لأنها الصيغة الأكثر شيوعًا على الويب.

```java
// Step 4: Load the image that contains the text to be recognized
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

**لماذا JPG؟** ضغط JPEG قد يضيف تشويهات تُربك OCR. للحصول على أقصى دقة، استخدم صورة بدقة لا تقل عن 300 DPI وتجنب الضغط المفرط. إذا كان لديك PNG أو TIFF، يمكنك تمريره مباشرة إلى `fromFile`؛ الشيفرة نفسها تعمل دون تعديل.

## الخطوة 5: تنفيذ OCR واسترجاع النص المعترف به

أخيرًا، استدعِ `recognize()` واطبع النتيجة. تُعيد الطريقة كائن `OcrResult` يحتوي على النص الخام، درجات الثقة، ومربعات الإحاطة لكل كلمة.

```java
// Step 5: Run OCR and get the result
OcrResult result = engine.recognize();
System.out.println("=== Recognized text ===");
System.out.println(result.getText());
```

### النتيجة المتوقعة

```
=== Recognized text ===
Welcome to Aspose OCR demo.
This text was extracted from a JPG image.
```

إذا احتوت النتيجة على أحرف مشوهة، راجع **الخطوة 3** (تصحيح الإملاء) وتأكد من أن الصورة تلبي توصية DPI.

## الاختلافات الشائعة وحالات الحافة

| الحالة | التعديل الموصى به |
|-----------|------------------------|
| **صورة منخفضة الدقة (< 150 DPI)** | قم بتكبير الصورة قبل تمريرها إلى المحرك أو استخدم `engine.getConfiguration().setScaleFactor(2.0)` لتمكين إعادة التحجيم داخليًا. |
| **مستند متعدد اللغات** | اضبط `engine.getConfiguration().setLanguage("eng,spa")` لتحميل قواميس الإنجليزية والإسبانية معًا. |
| **دفعة كبيرة من الملفات** | أعد استخدام نفس نسخة `OcrEngine`، فقط استدعِ `engine.setImage(...)` لكل ملف جديد. هذا يجنب تحميل المكتبة الأصلية مرارًا. |
| **بيئة ذات ذاكرة محدودة** | عطل GPU (`setUseGpu(false)`) وتصحيح الإملاء (`setSpellCorrector(false)`) لتقليل استهلاك الذاكرة. |
| **استخراج نص من PNG بدلاً من JPG** | لا تحتاج لتغيير الشيفرة؛ فقط وجه `fromFile` إلى مسار `.png`. المكتبة تكتشف الصيغة تلقائيًا. |

## نصائح احترافية لتحسين دقة OCR

1. **معالجة مسبقة للصورة** – طبّق تمدد التباين أو التحويل إلى ثنائي باستخدام OpenCV قبل تمريرها إلى Aspose OCR. الحواف النقية تعطي ثقة أعلى.
2. **قص الهوامش غير الضرورية** – المحرك يضيع وقتًا في تحليل المساحات الفارغة، مما قد يقلل من درجة الثقة العامة.
3. **اختر حزمة اللغة الصحيحة** – تحميل اللغات التي تحتاجها فقط يسرّع التعرف ويقلل الإيجابيات الزائفة.
4. **استخدم أحدث نسخة من Aspose OCR** – كل إصدار يتضمن نماذج عصبية محدثة تحسّن الدقة مباشرةً.

## مثال كامل قابل للتنفيذ

فيما يلي الفئة الكاملة في جافا التي تجمع جميع الخطوات. احفظها باسم `SimpleOcr.java`، عدّل مسار الصورة، وشغّل `mvn exec:java -Dexec.mainClass=SimpleOcr`.

```java
import com.aspose.ocr.*;

public class SimpleOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: (Optional) Enable GPU acceleration for faster processing
        engine.getConfiguration().setUseGpu(true);

        // Step 3: (Optional) Enable spell correction to improve OCR accuracy
        engine.getConfiguration().setSpellCorrector(true);

        // Step 4: Load the image that contains the text to be recognized
        // This example extracts text from jpg, but any supported format works.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Step 5: Perform OCR and retrieve the recognized text
        OcrResult result = engine.recognize();

        System.out.println("=== Recognized text ===");
        System.out.println(result.getText());
    }
}
```

تشغيل البرنامج يطبع النص المعترف به على وحدة التحكم، مؤكدًا أنك نجحت في تعلم كيفية **التعرف على النص من صورة**، وكيفية **استخراج النص من jpg**، والتقنيات الرئيسية لـ **كيف تحسن دقة OCR**.

## الخلاصة

في هذا الدليل تعلمت كيفية **التعرف على النص من صورة** في جافا باستخدام Aspose OCR، وكيفية **استخراج النص من jpg**، وعدة طرق عملية للإجابة على *كيف تحسن دقة OCR*. النهج مكتمل ذاتيًا: كل ما تحتاجه هو اعتماد Maven، ملف JPEG، وبعض إعدادات التكوين.

الخطوات التالية التي قد تستكشفها:

* تحويل النص المعترف به إلى PDF قابل للبحث باستخدام Aspose PDF.
* معالجة مجلد كامل من الصور بحلقة بسيطة (OCR دفعي).
* دمج محرك OCR في نقطة نهاية REST باستخدام Spring Boot لمعالجة الصور عند الطلب.

لا تتردد في تجربة جودة صور مختلفة، حزم لغات، وإعدادات عتاد لتلاحظ كيف يؤثر كل عامل على أداء OCR. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Preprocess Image OCR in Java with Aspose OCR – Boost Accuracy & Extract Text](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [How to Use OCR in Java – Recognize Text from Image Quickly](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Recognize Text from Image with Aspose OCR – Full Java Guide](/ocr/english/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}