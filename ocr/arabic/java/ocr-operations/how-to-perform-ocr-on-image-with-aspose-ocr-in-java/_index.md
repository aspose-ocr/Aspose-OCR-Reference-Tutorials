---
category: general
date: 2026-09-10
description: قم بإجراء التعرف الضوئي على الحروف (OCR) على الصورة باستخدام Aspose OCR
  Java. تعلم كيفية التعرف على النص من JPEG، واستخراج النص من الصورة، وتحويل الصورة
  إلى نص بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- recognize text from JPEG
- extract text from image
- convert image to text
- load image for OCR
language: ar
lastmod: 2026-09-10
og_description: قم بتنفيذ التعرف الضوئي على الأحرف (OCR) على صورة باستخدام Aspose
  OCR Java. يوضح هذا الدرس كيفية التعرف على النص من ملف JPEG، استخراج النص من الصورة،
  وتحويل الصورة إلى نص في بضع أسطر من الشيفرة.
og_image_alt: Screenshot of Java code that performs OCR on an image using Aspose OCR
og_title: إجراء التعرف الضوئي على الأحرف في الصورة باستخدام Aspose OCR – دليل Java
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  headline: How to perform OCR on image with Aspose OCR in Java
  type: TechArticle
- description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  name: How to perform OCR on image with Aspose OCR in Java
  steps:
  - name: Prerequisites
    text: '* Java Development Kit (JDK) 8 or later. * Maven or Gradle to manage dependencies
      (the example uses Maven). * A valid Aspose OCR for Java license (or a temporary
      evaluation key). * An image file named `sample.jpg` placed in a known directory.'
  - name: Load image for OCR
    text: '```java // Step 1: Load the image you want to process String imagePath
      = "YOUR_DIRECTORY/sample.jpg"; ImageStream imageStream = ImageStream.fromFile(imagePath);
      ```'
  - name: Create and configure the OCR engine
    text: '```java // Step 2: Create an OCR engine instance OcrEngine engine = new
      OcrEngine();'
  - name: Recognize text from JPEG
    text: '```java // Step 3: Attach the image to the engine engine.setImage(imageStream);'
  - name: Extract text from image and output
    text: '```java // Step 5: Output the recognized text System.out.println("=== Recognized
      Text ==="); System.out.println(result.getText()); ```'
  - name: Expected output
    text: 'Assuming `sample.jpg` contains the text “Hello World”, the console will
      display:'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: كيفية إجراء التعرف الضوئي على الأحرف (OCR) على صورة باستخدام Aspose OCR في
  جافا
url: /ar/java/ocr-operations/how-to-perform-ocr-on-image-with-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إجراء OCR على صورة باستخدام Aspose OCR في Java

إذا كنت بحاجة إلى **perform OCR on image** ملفات في تطبيق Java، فإن هذا الدليل يوفر حلاً كاملاً وجاهزًا للتنفيذ. سترى كيفية **recognize text from JPEG** الملفات، **extract text from image** البيانات، و **convert image to text** باستخدام API الحديثة لـ Aspose OCR.

يستعرض الدليل كل خطوة مطلوبة — من تحميل الصورة إلى طباعة النص المعترف به — حتى تتمكن من دمج وظيفة OCR دون الحاجة للبحث عن موارد إضافية. لا تحتاج إلى أدوات خارجية بخلاف مكتبة Aspose OCR for Java.

## ما ستحققه

* **Load an image for OCR** مباشرةً من نظام الملفات.  
* تمكين معالجة ما قبل Aspose OCR (مثل إزالة الضوضاء) لتحسين الدقة.  
* **Recognize text from JPEG** وغيرها من صيغ الراستر.  
* **Extract text from image** وإخراجها إلى وحدة التحكم.  
* فهم كيفية **convert image to text** في عينة كود جاهزة للإنتاج.  

### المتطلبات المسبقة

* Java Development Kit (JDK) 8 أو أحدث.  
* Maven أو Gradle لإدارة التبعيات (المثال يستخدم Maven).  
* ترخيص صالح لـ Aspose OCR for Java (أو مفتاح تقييم مؤقت).  
* ملف صورة باسم `sample.jpg` موجود في دليل معروف.

> **نصيحة احترافية:** استخدم صور JPEG عالية الدقة (300 dpi أو أعلى) للحصول على أفضل معدلات التعرف.  

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

إذا كنت تدير التبعيات باستخدام Maven، أدرج المقتطف التالي في ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

لـ Gradle، أضف:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

هذه الإحداثيات تجلب أحدث مكتبة مستقرة لـ Aspose OCR، والتي تشمل ميزات المعالجة المسبقة المستخدمة لاحقًا.

## إجراء OCR على صورة — خطوة بخطوة

الأقسام التالية تفصل البرنامج الكامل. كل كتلة هي قطعة مستقلة يمكنك نسخها، لصقها، وتشغيلها.

### تحميل صورة لـ OCR

```java
// Step 1: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ImageStream imageStream = ImageStream.fromFile(imagePath);
```

*لماذا هذا مهم:*  
`ImageStream.fromFile` يقرأ البايتات الخام لملف JPEG ويجهزه لمحرك OCR. تعمل الطريقة مع أي صيغة راستر يدعمها Aspose OCR، لذا يمكنك استبدال JPEG بـ PNG أو BMP دون تعديل الكود.

### إنشاء وتكوين محرك OCR

```java
// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();

// Enable preprocessing to improve accuracy (e.g., denoising)
engine.getPreprocessing().setDenoise(true);
```

*لماذا هذا مهم:*  
إنشاء كائن `OcrEngine` يخصص محرك التعرف الأساسي. تمكين علامة **denoise** يزيل الضوضاء البصرية التي غالبًا ما تعيق اكتشاف الأحرف، خاصةً في ملفات JPEG الممسوحة ضوئيًا.

### التعرف على النص من JPEG

```java
// Step 3: Attach the image to the engine
engine.setImage(imageStream);

// Step 4: Perform OCR recognition
OcrResult result = engine.recognize();
```

*لماذا هذا مهم:*  
`engine.setImage` يربط بيانات الصورة بخط أنابيب OCR. `engine.recognize()` ينفذ عملية التعرف بالكامل، ويعيد كائن `OcrResult` يحتوي على النص المستخرج ومقاييس الثقة.

### استخراج النص من الصورة وإخراجه

```java
// Step 5: Output the recognized text
System.out.println("=== Recognized Text ===");
System.out.println(result.getText());
```

*لماذا هذا مهم:*  
`result.getText()` يوفر تمثيل النص العادي لمحتوى الصورة. طباعة ذلك إلى وحدة التحكم تُظهر أن **convert image to text** نجحت، ويمكنك توجيه هذه السلسلة إلى ملفات، قواعد بيانات، أو خدمات لاحقة.

## مثال كامل قابل للتنفيذ

فيما يلي الفئة الكاملة بلغة Java التي تضم جميع الخطوات. استبدل `YOUR_DIRECTORY` بالمسار المطلق لملف JPEG الخاص بك.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the image for OCR
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ImageStream imageStream = ImageStream.fromFile(imagePath);

        // Create and configure the OCR engine
        OcrEngine engine = new OcrEngine();
        engine.getPreprocessing().setDenoise(true); // improve accuracy

        // Attach the image and run recognition
        engine.setImage(imageStream);
        OcrResult result = engine.recognize();

        // Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### النتيجة المتوقعة

بافتراض أن `sample.jpg` يحتوي على النص “Hello World”، ستظهر وحدة التحكم:

```
=== Recognized Text ===
Hello World
```

إذا كانت الصورة تحتوي على عدة أسطر، سيظهر كل سطر في سطر منفصل في النتيجة.

## الاختلافات الشائعة وحالات الحافة

| الحالة                                 | التعديل المقترح |
|----------------------------------------|-------------------|
| **Low‑resolution JPEG** (≤150 dpi)     | زيادة `engine.getPreprocessing().setUpsample(true);` للسماح لـ Aspose بزيادة الدقة قبل التعرف. |
| **Colored background** (e.g., scanned forms) | تمكين `engine.getPreprocessing().setBinarize(true);` لتحويل الصورة إلى أبيض وأسود. |
| **Non‑Latin script** (e.g., Cyrillic) | تعيين اللغة: `engine.getLanguage().setLanguage(OcrLanguage.RUSSIAN);`. |
| **Large batch processing**             | إعادة استخدام كائن `OcrEngine` واحد عبر عدة صور لتقليل عبء بدء التشغيل. |
| **Need confidence scores**             | الوصول إلى `result.getConfidence()` للحصول على قيم الثقة لكل حرف. |

هذه التعديلات توضح كيف يمكنك **load image for OCR** تحت ظروف مختلفة مع الاستمرار في **perform OCR on image** بشكل موثوق.

## اعتبارات الأداء

* **Memory usage:** كل `ImageStream` يحتفظ بالصورة بالكامل في الذاكرة. للملفات الكبيرة جدًا (مثلاً >10 MB)، فكر في بث الصورة على أجزاء باستخدام `ImageStream.fromByteArray`.  
* **Thread safety:** `OcrEngine` *ليس* آمنًا للخطوط المتعددة. أنشئ نسخة منفصلة لكل خيط إذا كنت تخطط لتوازي مهام OCR.  
* **License mode:** وضع التقييم يحد من عدد الصفحات المعالجة لكل جلسة. انشر نسخة مرخصة للعبء الإنتاجي.  

## الخلاصة

أنت الآن تعرف كيف **perform OCR on image** ملفات في Java باستخدام Aspose OCR. يغطي الدليل تحميل الصورة، تمكين المعالجة المسبقة، التعرف على النص من JPEG، استخراج النص، وتحويل الصورة إلى نص — كل ذلك في برنامج واحد مختصر.  

من هنا يمكنك استكشاف مواضيع ذات صلة مثل **recognize text from JPEG** على نطاق واسع، دمج الناتج مع فهرس بحث، أو دمج OCR مع معالجة اللغة الطبيعية لإنشاء خطوط معالجة مستندات أذكى. جرب خيارات المعالجة المسبقة لتحقيق أفضل دقة لمصادر صورك المحددة.

--- 

*صورة توضح ناتج الكود*  
![perform OCR on image Java example](image-placeholder.png){alt="أداء OCR على صورة باستخدام Aspose OCR Java"}

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [التعرف على نص الصورة باستخدام Aspose OCR – دليل OCR كامل لجافا](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [كيفية إجراء OCR لنص الصورة مع اللغة باستخدام Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [معالجة صورة OCR في Java باستخدام Aspose OCR – تحسين الدقة واستخراج النص](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}