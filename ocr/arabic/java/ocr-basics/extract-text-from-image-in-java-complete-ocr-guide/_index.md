---
category: general
date: 2026-07-21
description: استخراج النص من الصورة باستخدام Java OCR. تعلم كيفية تحويل PNG إلى نص،
  قراءة النص من PNG، تحميل الصورة للتعرف الضوئي على الأحرف، وإجراء OCR على الصورة
  في بضع خطوات فقط.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: ar
lastmod: 2026-07-21
og_description: استخراج النص من الصورة باستخدام جافا. يوضح لك هذا الدليل كيفية تحويل
  PNG إلى نص، قراءة النص من PNG، تحميل الصورة للتعرف الضوئي على الأحرف، وإجراء التعرف
  الضوئي على الأحرف على الصورة بكفاءة.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: استخراج النص من الصورة في جافا – دليل OCR خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: استخراج النص من الصورة في جافا – دليل OCR الكامل
url: /ar/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة في جافا – دليل OCR الكامل

هل احتجت يومًا إلى **استخراج النص من الصورة** لكن لم تكن متأكدًا أي مكتبة جافا تختار؟ أنت لست وحدك. سواء كنت تقوم برقمنة الإيصالات، أو مسح ملفات PDF، أو بناء أرشيف قابل للبحث، فإن استخراج النص من ملف PNG هو نقطة ألم يومية للعديد من المطورين.

في هذا الدرس سنستعرض حلًا عمليًا يتيح لك **تحويل PNG إلى نص**، **قراءة النص من PNG**، **تحميل الصورة لـ OCR**، و**إجراء OCR على الصورة**—كل ذلك ببضع أسطر من شفرة جافا نظيفة. بنهاية الدرس ستحصل على برنامج قابل للتنفيذ يمكنك إدراجه في أي مشروع.

## ما ستبنيه

سننشئ تطبيقًا صغيرًا من نوع console بجافا يقوم بـ:

1. تحميل ملف PNG من القرص.  
2. إرسال الصورة إلى محرك OCR (Tess4J، غلاف جافا لـ Tesseract).  
3. طباعة النص المُعترف به إلى وحدة التحكم.

بدون خدمات خارجية، بدون سحر—فقط جافا صافية ومحرك OCR مفتوح المصدر.

## المتطلبات المسبقة

- **Java 17** أو أحدث (الشفرة تُجمّع مع إصدارات أقدم، لكن Java 17 يوفّر أحدث ميزات اللغة).  
- **Maven** أو **Gradle** لإدارة الاعتمادات.  
- صورة PNG تجريبية باسم `sample.png` موجودة في مجلد يمكنك الإشارة إليه (مثلاً `src/main/resources`).  
- معرفة أساسية بطريقة `main` في جافا ومعالجة الاستثناءات.

إذا كان أي من هذه غير مألوف لك، لا تقلق—كل خطوة تتضمن ملخصًا سريعًا.

## الخطوة 1: إعداد المشروع وإضافة مكتبة OCR

أولًا، أنشئ مشروع Maven جديد (أو Gradle إذا تفضّل). أضف اعتماد Tess4J، الذي يجلب لك ثنائيات Tesseract تلقائيًا.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
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

> **نصيحة احترافية:** إذا كنت تستخدم Gradle، فإن السطر المكافئ هو `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

إضافة هذه المكتبة توفر لك الفئة `Tesseract`، التي تتولى **إجراء OCR على بيانات الصورة**.

## الخطوة 2: تحميل الصورة لـ OCR

الآن نحتاج إلى **تحميل الصورة لـ OCR**. يعمل Tess4J مع `java.awt.image.BufferedImage`، لذا سنقرأ ملف PNG باستخدام `ImageIO`.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

الطريقة أعلاه تعزل بوضوح منطق **تحميل الصورة لـ OCR**، مما يجعل باقي الشفرة أسهل للاختبار. لاحظ التعليق—إنه يعكس المقتطف الأصلي مع توسيعه للوضوح.

## الخطوة 3: إجراء OCR على الصورة

مع وجود الصورة في الذاكرة، يمكننا الآن **إجراء OCR على الصورة**. كائن `Tesseract` هو محركنا؛ سنقوم بتكوينه لاستخدام بيانات اللغة الإنجليزية الافتراضية التي تأتي مع Tess4J.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

قمنا بدمج “الخطوة 1” و“الخطوة 4” الأصليتين في طريقة واحدة، لأن إنشاء كائن `Tesseract` غير مكلف ونريد أن تظل الشفرة مدمجة. لا يزال التعليق يشير إلى الخطوات الأصلية لتتبع العملية.

## الخطوة 4: جمع كل شيء معًا – طريقة main

أخيرًا، نجمع كل شيء في `main`. هنا ستقوم بـ **قراءة النص من PNG** ورؤية النتيجة مطبوعة في وحدة التحكم.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

عند تشغيل الأمر `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (أو ما يعادله في Gradle)، يجب أن ترى شيئًا مشابهًا لـ:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

هذا الإخراج يثبت أنك نجحت في **استخراج النص من الصورة**، **تحويل PNG إلى نص**، و**قراءة النص من PNG** في برنامج واحد منظم.

## معالجة الحالات الشائعة

### صور منخفضة الجودة

إذا كان ملف PNG غير واضح أو منخفض التباين، تنخفض دقة OCR. حل سريع هو معالجة الصورة مسبقًا:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### دعم متعدد اللغات

يمكن لـ Tess4J التعامل مع العديد من اللغات. فقط حمّل ملف `.traineddata` المناسب وعيّن `tesseract.setLanguage("spa")` للإسبانية، على سبيل المثال.

### ملفات PDF الكبيرة أو الصور متعددة الصفحات

إذا كنت بحاجة إلى **استخراج النص من صورة** داخل ملف PDF، قسّم كل صفحة إلى PNG أولًا (باستخدام PDFBox) ثم مرّر كل PNG إلى روتين OCR نفسه.

## مثال كامل يعمل (كل الشفرة في مكان واحد)

فيما يلي الفئة الجافا الكاملة الجاهزة للتنفيذ. انسخ‑الصقها إلى `src/main/java/com/example/ocrdemo/OcrDemo.java` وستكون جاهزًا للانطلاق.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

تشغيل الفئة يطبع نتيجة OCR، مؤكدًا أنك نجحت في **إجراء OCR على الصورة** وتحويل PNG إلى نص قابل للتحرير.

## ملخص وخطوات قادمة

بدأنا بـ **استخراج النص من الصورة** باستخدام إعداد جافا خفيف. الآن تعرف كيف **تحمل الصورة لـ OCR**، **تجري OCR على الصورة**، و**تقرأ النص من PNG**—وهي اللبنات الأساسية لأي خط أنابيب رقمنة مستندات.

هل تريد التعمق أكثر؟ جرّب الأفكار التالية:

- **معالجة دفعات:** تكرار عبر مجلد من PNGs وكتابة كل نتيجة إلى ملف `.txt`.  
- **التكامل مع قاعدة بيانات:** خزن السلاسل المستخرجة جنبًا إلى جنب مع البيانات الوصفية لأرشيفات قابلة للبحث.  
- **دمج مع معالجة اللغة الطبيعية:** مرّر مخرجات OCR إلى نموذج تحليل مشاعر للحصول على رؤى سريعة.  

كل من هذه الامتدادات يبني على المفاهيم الأساسية التي غطيناها، لذا فأنت جاهز للتجربة.

---

*برمجة سعيدة! إذا واجهت أي مشاكل

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}