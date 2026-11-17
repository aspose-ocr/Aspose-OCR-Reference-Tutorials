---
category: general
date: 2026-11-17
description: जावा में छवि पर OCR कैसे करें और सरल कोड उदाहरण का उपयोग करके चित्रों
  से टेक्स्ट निकालें, सीखें। इसमें इमेज पढ़ने के जावा टिप्स शामिल हैं।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: hi
lastmod: 2026-11-17
og_description: जावा में छवि पर OCR कैसे करें और तेज़ी से टेक्स्ट निकालें। इस गाइड
  का पालन करके छवि को जावा में पढ़ें और तैयार‑से‑चलाने वाले उदाहरण के साथ छवि को टेक्स्ट
  में बदलें।
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: जावा में इमेज पर OCR कैसे करें – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: जावा में छवि पर OCR कैसे करें – चरण-दर-चरण मार्गदर्शिका
url: /hi/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to perform OCR on an image in Java – step‑by‑step guide

यदि आपको किसी चित्र पर **OCR कैसे करें** की आवश्यकता है, तो यह ट्यूटोरियल जावा में एक पूर्ण, चलाने योग्य समाधान दिखाता है। आप देखेंगे कि कैसे एक इमेज फ़ाइल पढ़ें, OCR इंजन को कॉन्फ़िगर करें, और वह टेक्स्ट निकालें जो इंजन पहचानता है।

स्कैन किए गए दस्तावेज़ों, रसीदों या स्क्रीनशॉट्स के साथ काम करने के लिए अक्सर दृश्य सामग्री को खोज योग्य टेक्स्ट में बदलना आवश्यक होता है। यह गाइड आपको हर चरण के माध्यम से ले जाता है, इमेज लोड करने से लेकर निकाले गए टेक्स्ट को प्रिंट करने तक, और यह असमर्थित फ़ाइल फ़ॉर्मेट और null परिणाम जैसी सामान्य समस्याओं को भी कवर करता है।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* Java Development Kit (JDK) 8 या उससे नया स्थापित हो।
* एक बिल्ड टूल (Maven या Gradle) ताकि OCR लाइब्रेरी को पुल किया जा सके।
* एक इमेज फ़ाइल (JPEG, PNG, BMP) जिसे आप प्रोसेस करना चाहते हैं।

कोड **`com.asprise.ocr` पैकेज** की OCR लाइब्रेरी का उपयोग करता है क्योंकि यह केवल एक JAR की आवश्यकता रखती है और सभी प्रमुख प्लेटफ़ॉर्म पर काम करती है। इसे किसी अन्य प्रदाता (Tesseract, Google Vision, आदि) से बदलने के लिए इम्पोर्ट स्टेटमेंट्स और इंजन‑इनिशियलाइज़ेशन कोड को स्वैप करें।

## Step 1: Add the OCR dependency

यदि आप Maven उपयोग कर रहे हैं, तो अपनी `pom.xml` में निम्नलिखित डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Gradle के लिए, यह लाइन `build.gradle` में रखें:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

इन लाइनों से सुनिश्चित होता है कि **read image Java** कोड कम्पाइल हो सके और OCR इंजन रन‑टाइम पर उपलब्ध हो।

## Step 2: Read the image with Java

इमेज फ़ाइल पढ़ना किसी भी **extract text image** वर्कफ़्लो में पहला ठोस कदम है। जावा की बिल्ट‑इन `ImageIO` क्लास अधिकांश सामान्य फ़ॉर्मेट को संभालती है।

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**यह क्यों महत्वपूर्ण है:** `ImageIO.read` असमर्थित फ़ॉर्मेट या भ्रष्ट फ़ाइलों के लिए `null` लौटाता है। ऊपर दिया गया मेथड समस्या को लॉग करता है और `null` लौटाता है ताकि अगला कदम सुगमता से प्रतिक्रिया दे सके।

## Step 3: Create and configure the OCR engine

OCR इंजन को यह जानना आवश्यक है कि कौन सी भाषा को पहचानना है। भाषा सेट करने से सटीकता में उल्लेखनीय सुधार होता है, विशेषकर गैर‑अंग्रेज़ी दस्तावेज़ों के लिए।

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**यह क्यों महत्वपूर्ण है:** इंजन को शुरू करना एक अपेक्षाकृत भारी ऑपरेशन है, इसलिए इसे एक बार बनाकर कई इमेज के लिए पुनः उपयोग करना चाहिए यदि आपका एप्लिकेशन बैच प्रोसेसिंग करता है।

## Step 4: Perform OCR and convert the image to text

अब जब इमेज लोड हो गई है और इंजन तैयार है, आप पहचान चरण चला सकते हैं। यह **how to perform OCR** का मुख्य भाग है।

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**एज‑केस हैंडलिंग:** यदि इमेज `null` है, तो मेथड एक खाली स्ट्रिंग लौटाता है बजाय `NullPointerException` फेंके। इससे उपयोगकर्ता‑प्रदान फ़ाइलों से निपटते समय कोड अधिक मजबूत बनता है।

## Step 5: Display the extracted text

अंत में, परिणाम को कंसोल पर प्रिंट करें या किसी अन्य कंपोनेंट (जैसे डेटाबेस या UI विजेट) को फॉरवर्ड करें।

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

जब आप प्रोग्राम को `java OcrDemo sample.jpg` के साथ चलाते हैं, तो कंसोल में पहचाने गए अक्षर दिखेंगे। यह **convert image to text** चक्र पूरा करता है।

### Expected output

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

यदि इमेज में कोई पढ़ने योग्य अक्षर नहीं हैं, तो प्रोग्राम `(no text detected)` प्रिंट करता है।

## Common variations and how to adapt them

| Variation | What changes | When to use |
|-----------|--------------|-------------|
| **Different language** | `"eng"` को `"spa"` (स्पेनिश), `"fra"` (फ़्रेंच) आदि से बदलें | जब दस्तावेज़ अंग्रेज़ी के अलावा किसी अन्य भाषा में हो |
| **Batch processing** | फ़ाइल पाथ की सूची पर लूप करें, वही `Ocr` इंस्टेंस पुनः उपयोग करें | बड़ी संख्या में स्कैन किए गए पेजों के लिए |
| **Higher accuracy** | `Ocr.SPEED_SLOW` उपयोग करें या `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` को सक्षम करें केवल संख्यात्मक स्कैन के लिए | जब OCR गुणवत्ता अत्यंत महत्वपूर्ण हो (जैसे इनवॉइस नंबर) |
| **Tesseract alternative** | इम्पोर्ट को `net.sourceforge.tess4j.Tesseract` में बदलें और इनिशियलाइज़ेशन कोड समायोजित करें | उन प्रोजेक्ट्स में जो पहले से Tesseract पर निर्भर हैं |

## Pro tips

* **Resize large images** को इंजन में फीड करने से पहले छोटा करें; OCR गति पिक्सेल संख्या के साथ स्केल करती है।
* **Pre‑process** इमेज (ग्रेस्केल, कंट्रास्ट बूस्ट) को OpenCV जैसी लाइब्रेरीज़ से करें यदि स्रोत शोरयुक्त हो।
* **Cache the OCR engine** यदि आप इसे कम समय में कई बार कॉल करते हैं—इंजन को शुरू/बंद करने में ओवरहेड लगता है।
* **Validate the result** को रेगुलर एक्सप्रेशन से जांचें जब आप किसी विशिष्ट फ़ॉर्मेट (जैसे तिथि, फोन नंबर) की अपेक्षा करते हैं।

## Conclusion

अब आप जावा में **OCR कैसे करें** जानते हैं, फ़ाइल पढ़ने से लेकर निकाले गए टेक्स्ट को प्रदर्शित करने तक। ट्यूटोरियल ने **read image Java**, **extract text image**, **convert image to text**, और **image to text java** तकनीकों को कवर किया, और वास्तविक दुनिया के परिदृश्यों के लिए व्यावहारिक टिप्स प्रदान किए।

अब आप कर सकते हैं:

* OCR चरण को वेब सर्विस में इंटीग्रेट करें जो अपलोड प्राप्त करता है।
* आउटपुट को सर्च इंडेक्स के साथ जोड़ें ताकि स्कैन किए गए दस्तावेज़ों पर फुल‑टेक्स्ट सर्च हो सके।
* मल्टी‑लैंग्वेज सपोर्ट या कस्टम कैरेक्टर सेट जैसी उन्नत OCR विकल्पों का अन्वेषण करें।

Happy coding, and enjoy turning pictures into searchable text!

## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच का पता लगा सकें।

- [How to Use OCR in Java – Extract Text from Image with Spell Correction](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Convert Image to Text in Java Using Aspose OCR – Full Guide](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [How to Enable GPU for OCR in Java – Extract Text from Image](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}