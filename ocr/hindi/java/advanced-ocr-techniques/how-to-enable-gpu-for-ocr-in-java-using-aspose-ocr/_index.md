---
category: general
date: 2026-08-18
description: Java में OCR के लिए GPU कैसे सक्षम करें और तेज़ी से इमेज टेक्स्ट को पहचानें,
  टेक्स्ट JPG निकालें, फ़िल्टर जोड़ें, तथा Aspose.OCR के साथ भाषा सेट करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize image text
- extract text jpg
- how to add filter
- how to set language
language: hi
lastmod: 2026-08-18
og_description: जावा में OCR के लिए GPU को कैसे सक्षम करें और तुरंत इमेज टेक्स्ट को
  पहचानें, टेक्स्ट JPG निकालें, फ़िल्टर जोड़ें, और Aspose.OCR का उपयोग करके भाषा सेट
  करें।
og_image_alt: Screenshot showing Java code that enables GPU for OCR with Aspose.OCR
og_title: जावा में OCR के लिए GPU कैसे सक्षम करें – पूर्ण Aspose.OCR गाइड
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  headline: How to enable GPU for OCR in Java using Aspose.OCR
  type: TechArticle
- description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  name: How to enable GPU for OCR in Java using Aspose.OCR
  steps:
  - name: 3.1 Set the OCR language
    text: '```java // Choose the language for recognition – this is the “how to set
      language” step engine.setLanguage(OcrLanguage.ENGLISH); ```'
  - name: 3.2 Add a preprocessing filter
    text: 'Noise, compression artifacts, or uneven lighting can hurt accuracy. Adding
      a denoise filter is the typical **how to add filter** approach:'
  - name: Expected output
    text: '``` Recognized text: The quick brown fox jumps over the lazy dog. ```'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Aspose.OCR का उपयोग करके जावा में OCR के लिए GPU कैसे सक्षम करें
url: /hi/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में Aspose.OCR के साथ GPU को सक्षम करने का तरीका

यदि आपको जावा में OCR के लिए **GPU को कैसे सक्षम करें** की आवश्यकता है, तो यह गाइड आपको सटीक चरणों के माध्यम से ले जाता है। GPU एक्सेलेरेशन को सक्षम करने से आप **छवि पाठ को पहचान** कई गुना तेज़ी से कर सकते हैं, जो बड़ी मात्रा में **JPG फ़ाइलों से टेक्स्ट निकालने** के लिए आवश्यक है। हम **फ़िल्टर कैसे जोड़ें**, **भाषा कैसे सेट करें**, और अंतिम परिणाम प्राप्त करने के बारे में भी चर्चा करेंगे।

इस ट्यूटोरियल के अंत तक आपके पास एक पूर्ण, चलाने योग्य प्रोग्राम होगा जो:

* GPU समर्थन के साथ Aspose.OCR इंजन शुरू करता है।  
* OCR भाषा (जैसे, English) को कॉन्फ़िगर करता है।  
* सटीकता बढ़ाने के लिए डीनॉइज़ फ़िल्टर लागू करता है।  
* JPEG इमेज लोड करता है, पहचान चलाता है, और निकाले गए टेक्स्ट को प्रिंट करता है।

> **Prerequisite:** Java 17 या बाद का संस्करण, Maven, और Aspose.OCR for Java लाइसेंस (मुफ़्त ट्रायल मूल्यांकन के लिए काम करता है)।

---

![जावा में OCR के लिए GPU को सक्षम करने का तरीका](/images/ocr-gpu.png){alt="जावा में OCR के लिए GPU को सक्षम करने का तरीका"}

## आपको क्या चाहिए

| आइटम | कारण |
|------|--------|
| **Java Development Kit (JDK) 17+** | उदाहरण को संकलित और चलाने के लिए आवश्यक है। |
| **Maven** | Aspose.OCR के लिए निर्भरता प्रबंधन को सरल बनाता है। |
| **Aspose.OCR for Java** | `OcrEngine` क्लास और GPU समर्थन प्रदान करता है। |
| **A sample JPEG image** (`sample.jpg`) | **extract text JPG** दर्शाने के लिए उपयोग किया जाता है। |
| **GPU‑compatible hardware** (optional but recommended) | हम जो प्रदर्शन वृद्धि कॉन्फ़िगर करेंगे, उसे सक्षम करता है। |

---

## चरण 1: Maven प्रोजेक्ट सेट अप करें

एक नया Maven प्रोजेक्ट बनाएं (या मौजूदा में जोड़ें) और Aspose.OCR डिपेंडेंसी शामिल करें:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-gpu-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Aspose.OCR for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.12</version> <!-- Use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** संस्करण संख्या को अद्यतित रखें; नए रिलीज़ GPU हैंडलिंग को सुधारते हैं और भाषा पैक्स जोड़ते हैं।

---

## चरण 2: OCR इंजन को इनिशियलाइज़ करें और **GPU को कैसे सक्षम करें**

समाधान का हृदय `OcrEngine` है। इसे इंस्टैंशिएट करना सीधा है, लेकिन आपको स्पष्ट रूप से GPU एक्सेलेरेशन को चालू करना होगा:

```java
import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration (this is the “how to enable GPU” part)
        engine.setUseGpu(true); // <-- GPU is now active

        // Step 2.3: Configure language and preprocessing filter (covered later)
```

**GPU को क्यों सक्षम करें?**  
जब `setUseGpu(true)` कॉल किया जाता है, तो Aspose.OCR भारी इमेज‑प्रोसेसिंग कर्नेल्स को ग्राफ़िक्स कार्ड पर ऑफ़लोड कर देता है। आधुनिक NVIDIA/AMD GPU पर पहचान गति ~200 ms प्रति पेज से < 80 ms तक बढ़ सकती है, जिससे बड़े बैचों के लिए कुल प्रोसेसिंग समय काफी घट जाता है।

---

## चरण 3: **भाषा कैसे सेट करें** और **फ़िल्टर कैसे जोड़ें**

### 3.1 OCR भाषा सेट करें

```java
        // Choose the language for recognition – this is the “how to set language” step
        engine.setLanguage(OcrLanguage.ENGLISH);
```

Aspose.OCR 100 से अधिक भाषाओं के लिए भाषा पैक्स के साथ आता है। `ENGLISH` को `FRENCH`, `CHINESE_SIMPLIFIED` आदि से बदलें ताकि आपके स्रोत सामग्री से मेल खाए।

### 3.2 प्रीप्रोसेसिंग फ़िल्टर जोड़ें

शोर, कम्प्रेशन आर्टिफैक्ट्स, या असमान लाइटिंग सटीकता को नुकसान पहुंचा सकते हैं। डीनॉइज़ फ़िल्टर जोड़ना सामान्य **फ़िल्टर कैसे जोड़ें** तरीका है:

```java
        // Add a denoising filter to improve OCR quality – “how to add filter”
        engine.addPreprocessFilter(FilterType.DENOISE);
```

अन्य उपयोगी फ़िल्टर में `FilterType.CONTRAST`, `FilterType.BRIGHTNESS`, और `FilterType.BINARIZE` शामिल हैं। आप `addPreprocessFilter` को बार‑बार कॉल करके कई फ़िल्टर चेन भी बना सकते हैं।

---

## चरण 4: इमेज लोड करें – **extract text JPG**

अब हम इंजन को उस JPEG फ़ाइल की ओर इंगित करते हैं जिसे हम प्रोसेस करना चाहते हैं:

```java
        // Load the JPEG image – this demonstrates “extract text JPG”
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

`YOUR_DIRECTORY` को उस वास्तविक पाथ से बदलें जहाँ `sample.jpg` स्थित है। Aspose.OCR PNG, BMP, TIFF, और PDF को भी सपोर्ट करता है; वही कॉल इन फॉर्मैट्स के लिए भी काम करता है।

---

## चरण 5: OCR करें और **छवि पाठ को पहचानें**

इंजन कॉन्फ़िगर होने के बाद, पहचान रूटीन को कॉल करें:

```java
        // Run the OCR operation – “recognize image text”
        engine.recognize();

        // Retrieve the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);
    }
}
```

`recognize()` मेथड इमेज को GPU (यदि सक्षम हो) पर प्रोसेस करता है और आंतरिक टेक्स्ट बफ़र को भरता है। `getText()` एक साधारण‑टेक्स्ट `String` लौटाता है, जिसे आप फ़ाइल, डेटाबेस में लिख सकते हैं या डाउनस्ट्रीम NLP पाइपलाइन को पास कर सकते हैं।

### अपेक्षित आउटपुट

```
Recognized text: The quick brown fox jumps over the lazy dog.
```

यदि इमेज में कई लाइन्स हैं, तो रिटर्नेड स्ट्रिंग में newline कैरेक्टर्स (`\n`) शामिल होते हैं जो मूल लेआउट को बनाए रखते हैं।

---

## चरण 6: GPU उपयोग की पुष्टि करें (वैकल्पिक)

GPU वास्तव में उपयोग हो रहा है या नहीं, यह सुनिश्चित करने के लिए Aspose लॉगिंग सक्षम करें:

```java
        // Enable diagnostic logging (optional)
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
```

रन के बाद `ocr-debug.log` देखें; आपको `GPU device: NVIDIA GeForce RTX 3080` और `Processing time (GPU): 78 ms` जैसी एंट्रीज़ दिखनी चाहिए। यदि लॉग में **CPU** उल्लेख है, तो ड्राइवर इंस्टॉलेशन और `setUseGpu(true)` कॉल की जाँच करें।

---

## सामान्य समस्याएँ और उन्हें कैसे टालें

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| **`java.lang.UnsatisfiedLinkError: no aspose_ocr_native`** | नेटिव GPU लाइब्रेरीज़ गायब | नवीनतम GPU ड्राइवर इंस्टॉल करें और सुनिश्चित करें कि `aspose-ocr` नेटिव बाइनरीज़ `java.library.path` पर हैं। |
| **डार्क इमेज पर खराब सटीकता** | प्रीप्रोसेसिंग फ़िल्टर नहीं | `engine.addPreprocessFilter(FilterType.BRIGHTNESS)` जोड़ें या `FilterType.CONTRAST` बढ़ाएँ। |
| **`OutOfMemoryError` on large batches** | GPU मेमोरी समाप्त | इमेज को छोटे बैचों में प्रोसेस करें या बहुत बड़े रिज़ॉल्यूशन के लिए GPU डिसेबल करें (`engine.setUseGpu(false)`)। |
| **भाषा आउटपुट गलत** | गलत भाषा सेट | सुनिश्चित करें कि `engine.setLanguage(OcrLanguage.YOUR_LANGUAGE)` स्रोत टेक्स्ट से मेल खाता है। |

---

## पूर्ण, चलाने योग्य उदाहरण

नीचे वह पूरा जावा क्लास है जिसे आप `src/main/java/com/example/HelloWorldOcr.java` में कॉपी‑पेस्ट कर सकते हैं। इसमें सभी चरण, एरर हैंडलिंग, और वैकल्पिक लॉगिंग शामिल हैं।

```java
package com.example;

import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // -------------------------------------------------
        // 1️⃣ Enable GPU acceleration – how to enable GPU
        // -------------------------------------------------
        engine.setUseGpu(true);

        // -------------------------------------------------
        // 2️⃣ Set language – how to set language
        // -------------------------------------------------
        engine.setLanguage(OcrLanguage.ENGLISH); // Change if needed

        // -------------------------------------------------
        // 3️⃣ Add preprocessing filter – how to add filter
        // -------------------------------------------------
        engine.addPreprocessFilter(FilterType.DENOISE);
        // Optional: engine.addPreprocessFilter(FilterType.CONTRAST);

        // -------------------------------------------------
        // 4️⃣ Load the JPEG image – extract text JPG
        // -------------------------------------------------
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        engine.setImage(ImageStream.fromFile(imagePath));

        // -------------------------------------------------
        // 5️⃣ Perform OCR – recognize image text
        // -------------------------------------------------
        engine.recognize();

        // Retrieve and display the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);

        // -------------------------------------------------
        // 6️⃣ Optional: write output to a file
        // -------------------------------------------------
        java.nio.file.Files.writeString(
                java.nio.file.Paths.get("output.txt"),
                text,
                java.nio.charset.StandardCharsets.UTF_8
        );

        // -------------------------------------------------
        // 7️⃣ Optional: enable debug logging to verify GPU usage
        // -------------------------------------------------
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
    }
}
```

**प्रोग्राम चलाना**

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HelloWorldOcr
```

आपको कंसोल में पहचाना गया टेक्स्ट प्रिंट होता दिखेगा और `output.txt` में सेव हो जाएगा। `ocr-debug.log` फ़ाइल GPU उपयोग की पुष्टि करेगी।

---

## निष्कर्ष

इस ट्यूटोरियल में हमने **GPU को कैसे सक्षम करें** Aspose.OCR के लिए जावा में, **छवि पाठ को कैसे पहचानें**, **extract text JPG**, **फ़िल्टर कैसे जोड़ें**, और **भाषा कैसे सेट करें**—सभी एक ही स्व-निहित प्रोग्राम में दिखाया। GPU को सक्षम करने से आपको उल्लेखनीय गति बढ़त मिलती है, जबकि फ़िल्टर और भाषा सेटिंग्स विविध इमेज स्रोतों में उच्च सटीकता सुनिश्चित करती हैं।

**अगले कदम**

* `FilterType.BINARIZE` जैसे अतिरिक्त फ़िल्टर के साथ प्रयोग करें, विशेषकर स्कैन किए गए दस्तावेज़ों के लिए।  
* अन्य भाषाओं (`OcrLanguage.SPANISH`, `OcrLanguage.CHINESE_SIMPLIFIED`) पर स्विच करें ताकि बहुभाषी समर्थन विस्तृत हो सके।  
* इस OCR पाइपलाइन को Apache PDFBox के साथ जोड़ें ताकि PDF पेज़ से सीधे टेक्स्ट निकाला जा सके।  

कोड को बैच प्रोसेसिंग के लिए अनुकूलित करें, इसे Spring Boot सर्विस में इंटीग्रेट करें, या रियल‑टाइम OCR वर्कलोड के लिए मैसेज क्यू के साथ कनेक्ट करें। Happy coding!

## अब आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकें।

- [जावा में Aspose OCR का उपयोग करके इमेज से टेक्स्ट पढ़ने का तरीका – पूर्ण गाइड](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Aspose.OCR का उपयोग करके भाषा के साथ इमेज टेक्स्ट OCR करना](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [जावा में Aspose OCR के साथ इमेज OCR को प्रीप्रोसेस करें – सटीकता बढ़ाएँ और टेक्स्ट निकालें](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}