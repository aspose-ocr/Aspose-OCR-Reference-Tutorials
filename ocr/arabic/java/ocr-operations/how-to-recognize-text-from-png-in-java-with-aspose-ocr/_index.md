---
category: general
date: 2026-11-14
description: تعلم كيفية التعرف على النص من ملفات PNG في جافا باستخدام Aspose OCR.
  يغطي الدليل أيضًا كيفية استخراج النص من الصورة وتحميل الصورة للتعرف الضوئي على الأحرف.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from png
- extract text from image
- convert scanned image to text
- load image for ocr
- read text from image java
language: ar
lastmod: 2026-11-14
og_description: التعرف على النص من ملفات PNG في جافا باستخدام Aspose OCR. اتبع هذا
  الدليل خطوة بخطوة لاستخراج النص من الصورة، وتحميل الصورة للتعرف الضوئي على الأحرف،
  وقراءة النص من مشاريع جافا التي تتعامل مع الصور.
og_image_alt: Screenshot of Java console showing recognized text from a PNG file
og_title: التعرف على النص من PNG في جافا – دليل Aspose OCR الكامل
schemas:
- author: Aspose
  dateModified: '2026-11-14'
  description: Learn how to recognize text from PNG in Java using Aspose OCR. The
    guide also covers how to extract text from image and load image for OCR.
  headline: How to recognize text from PNG in Java with Aspose OCR
  type: TechArticle
tags:
- Aspose OCR
- Java
- Image processing
title: كيفية التعرف على النص من PNG في Java باستخدام Aspose OCR
url: /ar/java/ocr-operations/how-to-recognize-text-from-png-in-java-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف على النص من ملفات PNG في جافا باستخدام Aspose OCR

إذا كنت بحاجة إلى **التعرف على النص من ملفات PNG** في تطبيق جافا، فإن هذا الدليل يوضح لك حلاً كاملاً وجاهزًا للتنفيذ. في نهاية الشرح ستتمكن من **استخراج النص من الصورة**، تحويل صورة ممسوحة ضوئيًا إلى نص، و**تحميل الصورة للـ OCR** باستخدام مكتبة Aspose OCR.

يعرض المثال أيضًا كيفية **قراءة النص من صورة جافا**، بحيث يمكنك دمج OCR في أي خدمة خلفية، أداة سطح مكتب، أو مشروع أندرويد.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* مجموعة تطوير جافا (JDK) 8 أو أحدث مثبتة.
* Maven أو Gradle لإدارة الاعتمادات (المثال يستخدم Maven).
* ملف ترخيص Aspose OCR for Java (الإصدار التجريبي المجاني يكفي للاختبار).
* صورة باسم `input.png` موجودة في مجلد يمكنك الإشارة إليه من الشيفرة.

تضمن هذه المتطلبات أن يتم تجميع الشيفرة وتشغيلها دون إعدادات إضافية.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

أضف حزمة Aspose OCR Maven إلى ملف `pom.xml`. سيؤدي ذلك إلى سحب جميع الفئات الضرورية، بما في ذلك `OcrEngine` و `ImageStream`.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

> **نصيحة محترف:** استخدم أحدث رقم إصدار (تحقق من Maven Central) للاستفادة من تحسينات الأداء ودعم اللغات الجديدة.

## الخطوة 2: تحميل صورة PNG للـ OCR

يعمل محرك OCR مع `ImageStream`. يجب أن تشير إليه إلى الموقع الدقيق لملف PNG الذي تريد معالجته.

```java
// Load the PNG image that contains the text you want to recognize
String imagePath = "YOUR_DIRECTORY/input.png";
ImageStream imageStream = ImageStream.fromFile(imagePath);
ocrEngine.setImage(imageStream);
```

*لماذا هذا مهم*: تحميل الصورة بشكل صحيح يجنب الخطأ الشائع “فشل OCR” الناتج عن تنسيق غير مدعوم أو مسار ملف مفقود.

## الخطوة 3: إنشاء وتكوين محرك OCR

قم بإنشاء كائن `OcrEngine` ويفضل تعديل إعدادات اللغة أو التعرف إذا لزم الأمر. الإعداد الافتراضي يعمل مع النص الإنجليزي المطبوع، لكن يمكنك تغيير `ocrEngine.setLanguage(Language.French)` للغات أخرى.

```java
// Step 3: Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Optional: set recognition language (default is English)
// ocrEngine.setLanguage(Language.English);
```

## الخطوة 4: تشغيل عملية OCR

استدعاء `process()` يقوم بالعمل الشاق—مسح الصورة، تقسيم الأحرف، وتحويلها إلى نص يونيكود.

```java
// Step 4: Execute the OCR operation
boolean success = ocrEngine.process();
```

إذا أعاد `process()` القيمة `true`، فإن المحرك نجح في **تحويل الصورة الممسوحة إلى نص**. وإلا، تحقق من مخرجات وحدة التحكم للرسائل التشخيصية.

## الخطوة 5: استرجاع وعرض النص المعترف به

عند نجاح OCR، يمكنك جلب السلسلة الكاملة باستخدام `getText()`. هذا هو جوهر وظيفة **قراءة النص من صورة جافا**.

```java
if (success) {
    System.out.println("Recognized text:");
    System.out.println(ocrEngine.getText());
} else {
    System.err.println("OCR failed. Verify the image path and file format.");
}
```

الآن تطبع وحدة التحكم الأحرف الدقيقة التي ظهرت في `input.png`. يمكنك معالجة السلسلة لاحقًا—تخزينها في قاعدة بيانات، تمريرها إلى فهرس بحث، أو إجراء تحليل لغوي طبيعي.

## مثال كامل قابل للتنفيذ

دمج جميع الخطوات معًا ينتج فئة واحدة مكتفية ذاتيًا. انسخ الشيفرة أدناه إلى ملف باسم `SimpleOcrDemo.java`، استبدل `YOUR_DIRECTORY` بالمسار المطلق أو النسبي إلى ملف PNG، ثم شغّله باستخدام `mvn exec:java`.

```java
import com.aspose.ocr.*;

public class SimpleOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image to be processed
        String imagePath = "YOUR_DIRECTORY/input.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Run the OCR process
        if (ocrEngine.process()) {
            // Step 4: Retrieve and display the recognized text
            System.out.println("Recognized text:");
            System.out.println(ocrEngine.getText());
        } else {
            System.err.println("OCR failed. Check the image path and format.");
        }
    }
}
```

**الناتج المتوقع** (مثال لصورة PNG بسيطة تحتوي على “Hello World”):

```
Recognized text:
Hello World
```

إذا احتوت الصورة على عدة أسطر، فإن المحرك يحافظ على فواصل الأسطر، مما يجعل المعالجة اللاحقة سهلة.

## معالجة الحالات الشائعة

| الحالة | الإجراء الموصى به |
|-----------|--------------------|
| **الصورة ليست PNG** | حوّل الملف إلى PNG أو استخدم `ImageStream.fromFile` مع تنسيق مدعوم (BMP, JPEG, TIFF). |
| **مسح بدقة منخفضة** | زد DPI قبل OCR (`ocrEngine.setResolution(300)`) لتحسين الدقة. |
| **نص غير إنجليزي** | استدعِ `ocrEngine.setLanguage(Language.<YourLanguage>)` وتأكد من تثبيت حزمة اللغة. |
| **دفعة كبيرة من الملفات** | أعد استخدام نسخة واحدة من `OcrEngine` واستدعِ `setImage` بشكل متكرر لتجنب عبء التهيئة المتكرر. |

هذه النصائح تساعدك على **استخراج النص من الصورة** بثقة عبر مصادر متنوعة.

## اعتبارات الأداء

* **سلامة الخيوط** – `OcrEngine` غير آمن للاستخدام المتعدد الخيوط. أنشئ نسخة منفصلة لكل خيط إذا كنت تخطط لمعالجة صور متزامنة.
* **استهلاك الذاكرة** – الصور الكبيرة تستهلك مساحة كومة أكبر. فكر في تصغير حجم الصور باستخدام `ImageResize` قبل تمريرها إلى المحرك.
* **الترخيص** – النسخة التجريبية تضيف علامة مائية إلى النص الناتج. استخدم نسخة مرخصة للإنتاج.

## الخطوات التالية

الآن بعد أن أصبحت قادرًا على **التعرف على النص من ملفات PNG**، قد ترغب في استكشاف ما يلي:

* **المعالجة الدفعية** – تكرار عبر مجلد وكتابة كل نتيجة OCR إلى ملف `.txt`.
* **التكامل مع Apache Tika** – دمج OCR مع استخراج البيانات الوصفية لإنشاء خطوط بحث نصي كامل.
* **استخدام Aspose OCR مع Spring Boot** – إنشاء نقطة نهاية HTTP تستقبل صورًا مرفوعة وتعيد نصًا مشفرًا بصيغة JSON.

هذه الإضافات تبني على المفاهيم الأساسية التي غطيناها في هذا الدليل.

---

*لقد تعلمت كيفية تحميل صورة للـ OCR، تحويل صورة ممسوحة ضوئيًا إلى نص، وقراءة النص من صورة جافا باستخدام Aspose OCR. طبّق النمط على صيغ صور أخرى، لغات مختلفة، وسيناريوهات نشر متعددة لتستفيد من قدرات أتمتة المستندات القوية.*


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [مثال OCR لجافا – تحميل صورة والتعرف على النص باستخدام Aspose](/ocr/english/java/ocr-basics/java-ocr-example-load-image-and-recognize-text-with-aspose/)
- [OCR دفعي للصور في جافا – استخراج النص من ملفات PNG بسرعة](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)
- [استخراج النص من صورة جافا باستخدام Aspose OCR – دليل](/ocr/english/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}