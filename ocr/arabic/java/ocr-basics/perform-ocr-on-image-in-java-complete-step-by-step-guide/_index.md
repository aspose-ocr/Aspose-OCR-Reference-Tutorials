---
category: general
date: 2026-06-16
description: تعرّف على كيفية تنفيذ تقنية التعرف الضوئي على الأحرف (OCR) على ملفات
  الصور في جافا. يغطي هذا الدرس التعرف على النص من ملفات PNG، استخراج النص من الصورة،
  تحويل الصورة إلى نص، وتحميل الصورة للتعرف الضوئي على الأحرف.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: ar
og_description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على الصورة باستخدام جافا.
  يوضح هذا الدليل كيفية التعرف على النص من ملف PNG، استخراج النص من الصورة، وتحويل
  الصورة إلى نص مع مثال جاهز للتنفيذ.
og_title: إجراء التعرف الضوئي على الأحرف في صورة باستخدام جافا – دليل برمجة كامل
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: تنفيذ التعرف الضوئي على الأحرف (OCR) على صورة في جافا – دليل كامل خطوة بخطوة
url: /ar/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء التعرف الضوئي على الأحرف (OCR) على صورة في جافا – دليل كامل خطوة بخطوة

هل احتجت يومًا إلى **perform OCR on image** للملفات لكن لم تكن متأكدًا أي مكتبة جافا تختار؟ لست وحدك. سواء كنت تبني ماسحًا للإيصالات، أو مؤرشف مستندات، أو مجرد فضولي حول تحويل الصور إلى نص قابل للبحث، فإن تعلم كيفية **perform OCR on image** باستخدام جافا مهارة مفيدة.

في هذا الدرس سنستعرض كل ما تحتاجه لـ **perform OCR on image** للملفات: تحميل الصورة، تكوين المحرك، التعرف على النص، وأخيرًا طباعة النتيجة. بنهاية الدرس ستكون قادرًا على **recognize text from PNG**، **extract text from image**، و **convert image to text** باستخدام بضع أسطر من الشيفرة فقط.

## المتطلبات المسبقة

- Java 17 أو أحدث (الشيفرة تُجمّع مع أي JDK حديث)
- Maven مثبت (أو أداة البناء المفضلة لديك)
- إلمام أساسي بصياغة جافا
- ملف PNG ترغب في اختباره (سنسميه `hello.png`)

> **نصيحة احترافية:** إذا لم يكن لديك ملف PNG جاهز، أنشئ واحدًا بأخذ لقطة شاشة لأي نص وحفظها كـ `hello.png` في مجلد اسمه `resources`.

## ما سنبنيه

تطبيق صغير سطر أوامر يُدعى `OcrDemo` يقوم بـ:

1. **Loads image for OCR** – يقرأ ملف PNG من القرص.
2. **Performs OCR on image** – يستخدم محرك Tesseract عبر Tess4J.
3. **Extracts text from image** – يُعيد `String` يحتوي على المحتوى المُتعرف عليه.
4. يطبع النتيجة على سطر الأوامر.

هيا نبدأ.

## الخطوة 1: إعداد المشروع وإضافة Tess4J

أولاً، أنشئ مشروع Maven جديد (أو Gradle إذا تفضّل). أضف تبعية Tess4J، التي تغلف محرك Tesseract OCR الشهير.

```xml
<!-- pom.xml -->
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- Tess4J – Java wrapper for Tesseract OCR -->
    <dependency>
      <groupId>net.sourceforge.tess4j</groupId>
      <artifactId>tess4j</artifactId>
      <version>5.5.1</version>
    </dependency>
  </dependencies>
</project>
```

> **لماذا Tess4J؟** إنها مُصانة بنشاط، تعمل عبر الأنظمة، وتوفر لك واجهة برمجة تطبيقات Java نظيفة لمهام **perform OCR on image**.

## الخطوة 2: إعداد منطق تحميل الصورة

الآن سنكتب طريقة مساعدة تقوم بـ **load image for OCR**. الطريقة تستخدم `ImageIO` في جافا لقراءة ملف PNG إلى `BufferedImage`.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

لاحظ أن اسم الطريقة يعكس بوضوح نية **load image for OCR**، مما يجعل الشيفرة موثقة ذاتيًا.

## الخطوة 3: تكوين محرك OCR لـ **Perform OCR on Image**

مع وجود الصورة، ننشئ كائن `Tesseract`، نفعّل الكشف التلقائي عن اللغة، ونستدعي `doOCR`. هذا هو جوهر طريقة **perform OCR on image** للبيانات.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **لماذا تمكين الكشف التلقائي؟** يسمح ذلك للمحرك باختيار أفضل نموذج لغة للصورة، وهو مفيد خصوصًا عندما **convert image to text** من مصادر تمزج بين الإنجليزية ولغات أخرى.

## الخطوة 4: تجميع كل شيء – التطبيق الرئيسي

إليك نقطة الدخول التي **recognize text from PNG**، **extract text from image**، وأخيرًا تطبع النتيجة. هذا هو المثال الكامل القابل للتنفيذ.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### النتيجة المتوقعة

إذا كان `hello.png` يحتوي على العبارة "Hello, OCR world!"، سيعرض سطر الأوامر شيئًا مثل:

```
=== Recognized Text ===
Hello, OCR world!
```

قد يختلف الإخراج الدقيق قليلًا حسب جودة الصورة، لكن يجب أن ترى النص الذي وضعته في PNG.

## الخطوة 5: معالجة الحالات الشائعة

### 5.1 التعامل مع الصور منخفضة الدقة

إذا كان PNG المصدر غير واضح، تنخفض دقة OCR. حل سريع هو تكبير الصورة قبل تمريرها إلى المحرك:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

استدعِ `upscale(image, 2)` قبل `engine.recognize(image)` لتحسين النتائج.

### 5.2 مستندات متعددة اللغات

إذا كنت تتوقع نصًا بالفرنسية أو الألمانية، ما عليك سوى إضافة رموز اللغات إلى `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

سوف يحاول المحرك بعد ذلك **extract text from image** باستخدام نماذج اللغات المدمجة.

### 5.3 تخطي الصفحات الفارغة

أحيانًا تُظهر صفحة PDF مُمسوحة كـ PNG فارغ. اكتشاف صورة فارغة يوفر وقت المعالجة:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## الخطوة 6: حزم وتشغيل التطبيق

1. **Compile:** `mvn clean compile`
2. **Run:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

تأكد من أن مجلد `tessdata` (الذي يحتوي على ملفات اللغات) موجود بجوار ملف JAR المُجمّع أو حدد مساره المطلق في `OcrEngine`.

## الخلاصة

أصبحت الآن تمتلك نمطًا قويًا وجاهزًا للإنتاج لتطبيق **perform OCR on image** للملفات باستخدام جافا. من **loading image for OCR** إلى **recognize text from PNG**، غطينا كيفية **extract text from image**، **convert image to text**، وتعاملنا مع سيناريوهات صعبة مثل المسحات منخفضة الدقة أو المحتوى متعدد اللغات.

بعد ذلك، قد ترغب في استكشاف:

- **Batch processing** – تكرار عبر دليل يحتوي على PNGs وكتابة كل نتيجة إلى ملف `.txt`.
- **PDF generation** – دمج النص المستخرج مرة أخرى في ملفات PDF قابلة للبحث.
- **Cloud OCR services** – مقارنة أداء Tesseract المحلي مع واجهات برمجة التطبيقات مثل Google Vision أو Azure Cognitive Services.

لا تتردد في التجربة، تعديل المعلمات، ومشاركة ما توصلت إليه. برمجة سعيدة، ولتتحول صورك دائمًا إلى نص نظيف وقابل للبحث!

![مخطط يوضح سير عمل OCR لإجراء OCR على الصورة](https://example.com/ocr-workflow.png "مثال على إجراء OCR على الصورة")

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [التعرف على نص الصورة باستخدام Aspose OCR – دليل OCR كامل لجافا](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [تحويل الصورة إلى نص في جافا باستخدام Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [استخراج النص من صورة جافا باستخدام Aspose.OCR وضع اكتشاف المناطق](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}