---
category: general
date: 2026-07-21
description: जावा OCR का उपयोग करके छवि से टेक्स्ट निकालें। जानें कि PNG को टेक्स्ट
  में कैसे बदलें, PNG से टेक्स्ट पढ़ें, OCR के लिए छवि लोड करें, और कुछ ही चरणों में
  छवि पर OCR करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: hi
lastmod: 2026-07-21
og_description: जावा के साथ छवि से टेक्स्ट निकालें। यह गाइड आपको दिखाता है कि PNG
  को टेक्स्ट में कैसे बदलें, PNG से टेक्स्ट पढ़ें, OCR के लिए छवि लोड करें, और छवि
  पर प्रभावी ढंग से OCR करें।
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: जावा में छवि से टेक्स्ट निकालें – चरण‑दर‑चरण OCR ट्यूटोरियल
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
title: जावा में छवि से पाठ निकालें – पूर्ण OCR मार्गदर्शिका
url: /hi/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज से टेक्स्ट निकालें Java – पूरा OCR गाइड

क्या आपको **इमेज से टेक्स्ट निकालना** पड़ा है लेकिन सही Java लाइब्रेरी चुनने में दुविधा हुई? आप अकेले नहीं हैं। चाहे आप रसीदें डिजिटल कर रहे हों, PDFs स्कैन कर रहे हों, या सर्चेबल आर्काइव बना रहे हों, PNG से टेक्स्ट निकालना कई डेवलपर्स के लिए रोज़मर्रा की समस्या है।

इस ट्यूटोरियल में हम एक हैंड‑ऑन समाधान देखेंगे जो आपको **PNG को टेक्स्ट में बदलना**, **PNG से टेक्स्ट पढ़ना**, **OCR के लिए इमेज लोड करना**, और **इमेज पर OCR करना**—सिर्फ कुछ लाइनों के साफ़ Java कोड से संभव बनाता है। अंत तक आपके पास एक रन करने योग्य प्रोग्राम होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं।

## आप क्या बनाएँगे

हम एक छोटा Java कंसोल एप बनायेंगे जो:

1. डिस्क से एक PNG फ़ाइल लोड करेगा।  
2. इमेज को OCR इंजन (Tess4J, Tesseract का Java रैपर) को भेजेगा।  
3. पहचाने गए टेक्स्ट को कंसोल पर प्रिंट करेगा।

कोई बाहरी सर्विस नहीं, कोई जादू नहीं—सिर्फ शुद्ध Java और एक ओपन‑सोर्स OCR इंजन।

## प्री‑रिक्विज़िट्स

- **Java 17** या बाद का संस्करण (कोड पुराने संस्करणों के साथ भी कम्पाइल हो सकता है, पर Java 17 नवीनतम भाषा सुविधाएँ देता है)।  
- **Maven** या **Gradle** डिपेंडेंसी मैनेजमेंट के लिए।  
- एक सैंपल PNG जिसका नाम `sample.png` हो और जिसे आप रेफ़रेंस कर सकें (जैसे `src/main/resources` फ़ोल्डर में)।  
- Java के `main` मेथड और एक्सेप्शन हैंडलिंग की बेसिक समझ।

अगर इनमें से कोई भी चीज़ अजनबी लग रही है, तो चिंता न करें—हर स्टेप में एक त्वरित रीकैप दिया गया है।

## स्टेप 1: प्रोजेक्ट सेट अप करें और OCR लाइब्रेरी जोड़ें

पहले एक नया Maven प्रोजेक्ट बनायें (या Gradle अगर आप पसंद करते हैं)। Tess4J डिपेंडेंसी जोड़ें, जो आपके लिए Tesseract बाइनरी लाता है।

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

> **प्रो टिप:** अगर आप Gradle इस्तेमाल कर रहे हैं, तो समकक्ष लाइन है `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`।

यह लाइब्रेरी आपको `Tesseract` क्लास देती है, जो **इमेज पर OCR करना** का भारी काम संभालती है।

## स्टेप 2: OCR के लिए इमेज लोड करें

अब हमें **OCR के लिए इमेज लोड करना** है। Tess4J `java.awt.image.BufferedImage` के साथ काम करता है, इसलिए हम `ImageIO` से PNG पढ़ेंगे।

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

ऊपर दिया गया मेथड **OCR के लिए इमेज लोड करने** की लॉजिक को साफ़‑सुथरे ढंग से अलग करता है, जिससे बाकी कोड टेस्ट करना आसान हो जाता है। टिप्पणी देखें – यह मूल स्निपेट को प्रतिबिंबित करती है और स्पष्टता के लिए विस्तारित की गई है।

## स्टेप 3: इमेज पर OCR करें

इमेज मेमोरी में होने के बाद, अब हम **इमेज पर OCR करना** शुरू कर सकते हैं। `Tesseract` इंस्टेंस हमारा इंजन है; हम इसे Tess4J के साथ आने वाले डिफ़ॉल्ट अंग्रेज़ी लैंग्वेज डेटा का उपयोग करने के लिए कॉन्फ़िगर करेंगे।

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

यहाँ हमने मूल “स्टेप 1” और “स्टेप 4” को एक ही मेथड में मिलाया है, क्योंकि `Tesseract` ऑब्जेक्ट बनाना हल्का है और कोड को कॉम्पैक्ट रखना चाहते हैं। टिप्पणी अभी भी मूल स्टेप्स का संदर्भ देती है।

## स्टेप 4: सब कुछ एक साथ लाएँ – मेन मेथड

अंत में, हम सब कुछ `main` में जोड़ते हैं। यहीं पर आप **PNG से टेक्स्ट पढ़ेंगे** और परिणाम कंसोल पर देखेंगे।

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

जब आप `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (या Gradle समकक्ष) चलाएँगे, तो आपको कुछ इस तरह का आउटपुट दिखेगा:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

यह आउटपुट साबित करता है कि आपने सफलतापूर्वक **इमेज से टेक्स्ट निकालना**, **PNG को टेक्स्ट में बदलना**, और **PNG से टेक्स्ट पढ़ना** एक ही साफ़ प्रोग्राम में किया है।

## सामान्य एज़ केसों को संभालना

### लो‑क्वालिटी इमेजेज

अगर PNG धुंधली है या कॉन्ट्रास्ट कम है, तो OCR की सटीकता घटती है। एक त्वरित समाधान है इमेज को प्री‑प्रोसेस करना:

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

### मल्टी‑लैंग्वेज सपोर्ट

Tess4J कई भाषाओं को सपोर्ट करता है। बस उपयुक्त `.traineddata` फ़ाइल डाउनलोड करें और `tesseract.setLanguage("spa")` जैसे कोड से स्पैनिश सेट करें।

### बड़े PDFs या मल्टी‑पेज इमेजेज

अगर आपको PDF के अंदर **इमेज से टेक्स्ट निकालना** है, तो पहले प्रत्येक पेज को PNG में विभाजित करें (PDFBox का उपयोग करके) और फिर प्रत्येक PNG को वही OCR रूटीन में फीड करें।

## पूर्ण कार्यशील उदाहरण (सारा कोड एक जगह)

नीचे पूरा, तैयार‑चलाने‑योग्य Java क्लास दिया गया है। इसे `src/main/java/com/example/ocrdemo/OcrDemo.java` में कॉपी‑पेस्ट करें और आप तैयार हैं।

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

क्लास चलाने पर OCR परिणाम प्रिंट होगा, जिससे पुष्टि होगी कि आपने सफलतापूर्वक **इमेज पर OCR करना** किया और अपनी PNG को एडिटेबल टेक्स्ट में बदल दिया।

## रीकैप & अगले कदम

हमने एक हल्के Java सेटअप से **इमेज से टेक्स्ट निकालना** शुरू किया। अब आप जानते हैं कि **OCR के लिए इमेज लोड करना**, **इमेज पर OCR करना**, और **PNG से टेक्स्ट पढ़ना** कैसे किया जाता है—जो किसी भी डॉक्यूमेंट‑डिजिटाइज़ेशन पाइपलाइन के मूल बिल्डिंग ब्लॉक्स हैं।

और आगे बढ़ना चाहते हैं? ये आइडियाज़ आज़माएँ:

- **बैच प्रोसेसिंग:** PNG की डायरेक्टरी पर लूप चलाएँ और प्रत्येक परिणाम को `.txt` फ़ाइल में लिखें।  
- **डेटाबेस इंटीग्रेशन:** एक्सट्रैक्टेड स्ट्रिंग्स को मेटाडेटा के साथ स्टोर करें ताकि सर्चेबल आर्काइव बन सके।  
- **NLP के साथ संयोजन:** OCR आउटपुट को सेंटिमेंट‑एनालिसिस मॉडल में फीड करें और जल्दी इनसाइट्स प्राप्त करें।  

इन सभी एक्सटेंशन का आधार वही कोर कॉन्सेप्ट्स हैं जो हमने कवर किए हैं, इसलिए आप प्रयोग करने के लिए तैयार हैं।

---

*हैप्पी कोडिंग! अगर आपको कोई दिक्कत आए*

## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और स्टेप‑बाय‑स्टेप एक्सप्लानेशन हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकते हैं और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकते हैं।

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}