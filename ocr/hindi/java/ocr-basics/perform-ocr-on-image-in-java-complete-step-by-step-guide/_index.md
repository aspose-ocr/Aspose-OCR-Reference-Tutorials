---
category: general
date: 2026-06-16
description: जावा में इमेज फ़ाइलों पर OCR कैसे करें, सीखें। यह ट्यूटोरियल PNG से टेक्स्ट
  पहचानने, इमेज से टेक्स्ट निकालने, इमेज को टेक्स्ट में बदलने और OCR के लिए इमेज लोड
  करने को कवर करता है।
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: hi
og_description: जावा का उपयोग करके छवि पर OCR करें। यह गाइड दिखाता है कि PNG से टेक्स्ट
  कैसे पहचाना जाए, छवि से टेक्स्ट निकाला जाए, और तैयार‑से‑चलाने वाले उदाहरण के साथ
  छवि को टेक्स्ट में कैसे बदला जाए।
og_title: जावा में इमेज पर OCR करें – पूर्ण प्रोग्रामिंग ट्यूटोरियल
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
title: जावा में इमेज पर OCR करें – पूर्ण चरण-दर-चरण गाइड
url: /hi/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज पर OCR करें Java में – पूर्ण चरण‑दर‑चरण गाइड

क्या आपको कभी **इमेज पर OCR करना** पड़ा लेकिन सही Java लाइब्रेरी चुनने में दुविधा हुई? आप अकेले नहीं हैं। चाहे आप रसीद स्कैनर, दस्तावेज़ अभिलेखागार बना रहे हों, या सिर्फ तस्वीरों को खोज योग्य टेक्स्ट में बदलने में रुचि रखते हों, **इमेज पर OCR करना** Java के साथ सीखना एक उपयोगी कौशल है।

इस ट्यूटोरियल में हम सब कुछ कवर करेंगे जो आपको **इमेज पर OCR करना** फ़ाइलों के लिए चाहिए: इमेज लोड करना, इंजन को कॉन्फ़िगर करना, टेक्स्ट पहचानना, और अंत में परिणाम प्रिंट करना। अंत तक आप **PNG फ़ाइलों से टेक्स्ट पहचानना**, **इमेज स्रोतों से टेक्स्ट निकालना**, और **इमेज को टेक्स्ट में बदलना** कुछ ही लाइनों के कोड से कर पाएँगे।

## आवश्यकताएँ

- Java 17 या नया (कोड किसी भी हालिया JDK के साथ कम्पाइल होता है)
- Maven स्थापित (या आपका पसंदीदा बिल्ड टूल)
- Java सिंटैक्स की बुनियादी समझ
- एक PNG फ़ाइल जिसे आप टेस्ट करना चाहते हैं (हम इसे `hello.png` कहेंगे)

> **प्रो टिप:** अगर आपके पास PNG नहीं है, तो किसी भी टेक्स्ट की स्क्रीनशॉट लेकर उसे `hello.png` नाम से `resources` फ़ोल्डर में सेव कर लें।

## हम क्या बनाएँगे

एक छोटा कंसोल एप्लिकेशन `OcrDemo` जिसका उद्देश्य है:

1. **OCR के लिए इमेज लोड करना** – डिस्क से PNG पढ़ता है।
2. **इमेज पर OCR करना** – Tess4J के माध्यम से Tesseract इंजन का उपयोग करता है।
3. **इमेज से टेक्स्ट निकालना** – पहचाने गए कंटेंट को `String` के रूप में लौटाता है।
4. परिणाम को कंसोल में प्रिंट करता है।

चलिए शुरू करते हैं।

## चरण 1: प्रोजेक्ट सेट‑अप और Tess4J जोड़ें

पहले एक नया Maven प्रोजेक्ट बनाएँ (या Gradle अगर आप चाहें)। Tess4J डिपेंडेंसी जोड़ें, जो लोकप्रिय Tesseract OCR इंजन को रैप करता है।

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

> **Tess4J क्यों?** यह सक्रिय रूप से मेंटेन किया जाता है, क्रॉस‑प्लेटफ़ॉर्म काम करता है, और आपको **इमेज पर OCR करना** कार्यों के लिए एक साफ़ Java API देता है।

## चरण 2: इमेज‑लोडिंग लॉजिक तैयार करें

अब हम एक हेल्पर मेथड लिखेंगे जो **OCR के लिए इमेज लोड करता** है। यह मेथड Java के `ImageIO` का उपयोग करके PNG को `BufferedImage` में पढ़ता है।

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

ध्यान दें कि मेथड का नाम स्पष्ट रूप से **OCR के लिए इमेज लोड** करने के इरादे को दर्शाता है, जिससे कोड स्वयं‑डॉक्यूमेंटेड बन जाता है।

## चरण 3: OCR इंजन को **इमेज पर OCR करने** के लिए कॉन्फ़िगर करें

इमेज हाथ में होने पर, हम एक `Tesseract` इंस्टेंस बनाते हैं, ऑटोमैटिक लैंग्वेज डिटेक्शन सक्षम करते हैं, और `doOCR` कॉल करते हैं। यही वह मुख्य भाग है जिससे हम **इमेज पर OCR करना** डेटा पर करते हैं।

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

> **ऑटो‑डिटेक्ट क्यों?** यह इंजन को इमेज के लिए सबसे उपयुक्त भाषा मॉडल चुनने देता है, जो विशेष रूप से तब उपयोगी होता है जब आप **इमेज को टेक्स्ट में बदलना** चाहते हैं और स्रोत में अंग्रेज़ी के साथ अन्य लिपियाँ भी हों।

## चरण 4: सब कुछ एक साथ रखें – मुख्य एप्लिकेशन

यहाँ वह एंट्री पॉइंट है जो **PNG से टेक्स्ट पहचानता**, **इमेज से टेक्स्ट निकालता**, और अंत में परिणाम प्रिंट करता है। यह पूरा, चलाने योग्य उदाहरण है।

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

### अपेक्षित आउटपुट

यदि `hello.png` में वाक्य “Hello, OCR world!” है, तो कंसोल कुछ इस तरह दिखेगा:

```
=== Recognized Text ===
Hello, OCR world!
```

सटीक आउटपुट इमेज की गुणवत्ता के आधार पर थोड़ा बदल सकता है, लेकिन आपको PNG में रखे टेक्स्ट जैसा ही दिखना चाहिए।

## चरण 5: सामान्य किनारी मामलों को संभालना

### 5.1 लो‑रेज़ोल्यूशन इमेजेस से निपटना

यदि स्रोत PNG धुंधली है, तो OCR की सटीकता घटती है। एक त्वरित समाधान है इमेज को अपस्केल करना और फिर इंजन को देना:

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

`engine.recognize(image)` से पहले `upscale(image, 2)` कॉल करें ताकि परिणाम बेहतर हों।

### 5.2 मल्टी‑लैंग्वेज दस्तावेज़

यदि आप फ्रेंच या जर्मन टेक्स्ट की उम्मीद करते हैं, तो बस `setLanguage` में भाषा कोड जोड़ दें:

```java
tesseract.setLanguage("eng+fra+deu");
```

इंजन तब संयुक्त भाषा मॉडलों का उपयोग करके **इमेज से टेक्स्ट निकालना** करेगा।

### 5.3 खाली पेजेस को स्किप करना

कभी‑कभी स्कैन किया गया PDF पेज एक खाली PNG के रूप में रेंडर होता है। खाली इमेज का पता लगाना प्रोसेसिंग टाइम बचाता है:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## चरण 6: एप्लिकेशन को पैकेज और रन करना

1. **कम्पाइल:** `mvn clean compile`
2. **रन:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

सुनिश्चित करें कि `tessdata` फ़ोल्डर (जिसमें भाषा फ़ाइलें हैं) कम्पाइल्ड JAR के बगल में हो या `OcrEngine` में उसका एब्सोल्यूट पाथ निर्दिष्ट करें।

## निष्कर्ष

अब आपके पास एक ठोस, प्रोडक्शन‑रेडी पैटर्न है **इमेज पर OCR करना** फ़ाइलों के लिए Java में। **OCR के लिए इमेज लोड** करने से लेकर **PNG से टेक्स्ट पहचानने** तक, हमने **इमेज से टेक्स्ट निकालना**, **इमेज को टेक्स्ट में बदलना**, और लो‑रेज़ोल्यूशन स्कैन या मल्टी‑लैंग्वेज कंटेंट जैसे कठिन परिदृश्यों को कैसे संभालें, यह कवर किया।

आगे आप यह देख सकते हैं:

- **बैच प्रोसेसिंग** – PNGs की डायरेक्टरी पर लूप चलाएँ और प्रत्येक परिणाम को `.txt` फ़ाइल में लिखें।
- **PDF जनरेशन** – निकाले गए टेक्स्ट को फिर से सर्चेबल PDFs में एम्बेड करें।
- **क्लाउड OCR सेवाएँ** – स्थानीय Tesseract प्रदर्शन की तुलना Google Vision या Azure Cognitive Services जैसे APIs से करें।

प्रयोग करें, पैरामीटर बदलें, और अपने निष्कर्ष साझा करें। कोडिंग का आनंद लें, और आपकी इमेजेस हमेशा साफ़, सर्चेबल टेक्स्ट में बदलें!

![Diagram showing the OCR workflow to perform OCR on image](https://example.com/ocr-workflow.png "perform OCR on image example")


## आप अगला क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर कर सकें।

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}