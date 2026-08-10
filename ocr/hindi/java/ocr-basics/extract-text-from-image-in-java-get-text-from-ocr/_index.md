---
category: general
date: 2026-05-25
description: जावा में OCR का उपयोग करके छवि से टेक्स्ट निकालें। जानें कि OCR के लिए
  छवि कैसे लोड करें, फोटो से टेक्स्ट कैसे पहचानें, और एक सरल कोड उदाहरण के साथ OCR
  से टेक्स्ट कैसे प्राप्त करें।
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: hi
og_description: जावा में इमेज से टेक्स्ट निकालें, चरण-दर-चरण गाइड के साथ। OCR के लिए
  इमेज लोड करना सीखें, फोटो से टेक्स्ट पहचानें, और OCR से प्रभावी ढंग से टेक्स्ट प्राप्त
  करें।
og_title: जावा में छवि से टेक्स्ट निकालें – OCR से टेक्स्ट प्राप्त करें
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: जावा में इमेज से टेक्स्ट निकालें – OCR से टेक्स्ट प्राप्त करें
url: /hi/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में इमेज से टेक्स्ट निकालें – OCR से टेक्स्ट प्राप्त करें

क्या आपको कभी **इमेज से टेक्स्ट निकालने** की ज़रूरत पड़ी है लेकिन यह नहीं पता था कि कौन सी जावा लाइब्रेरी चुनें? आप अकेले नहीं हैं। चाहे आप रसीदों को डिजिटल बना रहे हों, प्रोडक्ट फ़ोटो से सीरियल नंबर निकाल रहे हों, या सिर्फ़ एक मज़ेदार साइड प्रोजेक्ट के साथ खेल रहे हों, एक तस्वीर को संपादन योग्य टेक्स्ट में बदलना एक आम चुनौती है।

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने‑योग्य उदाहरण के माध्यम से चलेंगे जो आपको दिखाएगा कि कैसे **OCR के लिए इमेज लोड करें**, इंजन को कॉन्फ़िगर करें, और अंत में **फ़ोटो से टेक्स्ट पहचानें** ताकि आप केवल कुछ लाइनों के कोड से **OCR से टेक्स्ट प्राप्त कर सकें**। कोई अस्पष्ट संदर्भ नहीं—आपको जो कुछ भी चाहिए वह यहाँ है।

## आप क्या सीखेंगे

* जावा में एक हल्का OCR इंजन सेट अप करना।  
* **OCR के लिए इमेज लोड करें** और विभिन्न फ़ाइल पाथ को संभालने के सटीक कदम।  
* जब आप **इमेज से टेक्स्ट निकालना** चाहते हैं और भाषा अंग्रेज़ी नहीं है, तो भाषा को कॉन्फ़िगर करना क्यों महत्वपूर्ण है।  
* परिणाम को सुरक्षित रूप से आउटपुट करना और जब इंजन कुछ नहीं लौटाए तो क्या करना है।  
* सबसे सामान्य pitfalls से बचने के लिए कुछ प्रो टिप्स।  

इस गाइड के अंत तक आपके पास एक स्व-निहित प्रोग्राम होगा जो यूक्रेनी अक्षरों वाली JPEG (या PNG) पढ़ता है और पहचाने गए स्ट्रिंग को कंसोल में प्रिंट करता है। भाषा या इमेज बदलने में संकोच न करें—सब कुछ मॉड्यूलर है।

![Diagram showing the flow of extracting text from image using Java OCR engine](/images/extract-text-from-image-java.png)

*Alt text: जावा में इमेज से टेक्स्ट निकालने की प्रक्रिया का फ्लो डायग्राम.*

## आवश्यकताएँ

* **Java Development Kit (JDK) 11+** – कोड आधुनिक मॉड्यूल सिस्टम का उपयोग करता है, लेकिन पुराने संस्करण मामूली बदलावों के साथ काम करेंगे।  
* **Maven या Gradle** – OCR लाइब्रेरी को प्राप्त करने के लिए (हम **Asprise OCR** को एक हल्का, विकास‑के‑लिए‑नि:शुल्क विकल्प के रूप में उपयोग करेंगे)।  
* एक सैंपल इमेज फ़ाइल (जैसे `ukrainian_sign.jpg`) को ऐसी जगह रखें जहाँ आपका प्रोग्राम पढ़ सके।  
* जावा के `main` मेथड और एक्सेप्शन हैंडलिंग की बुनियादी समझ।  

यदि आपके पास ये हैं, तो आप शुरू करने के लिए तैयार हैं। अन्यथा, Oracle या AdoptOpenJDK से JDK प्राप्त करें और एक साधा Maven प्रोजेक्ट सेट अप करें—कुछ भी जटिल नहीं।

## चरण 1: OCR डिपेंडेंसी जोड़ें

सबसे पहले, अपने बिल्ड टूल को OCR इंजन प्राप्त करने के लिए बताएं। Maven के लिए, इसे `pom.xml` में डालें:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

यदि आप Gradle पसंद करते हैं, तो समकक्ष यह है:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

ये कोऑर्डिनेट्स एक कॉम्पैक्ट JAR लाते हैं जिसमें `OcrEngine`, `OcrLanguage`, और वह हेल्पर क्लासेस शामिल हैं जिनका हम उपयोग करेंगे। बेसिक लैटिन और सिरिलिक स्क्रिप्ट्स के लिए कोई अतिरिक्त नेटिव बाइनरी आवश्यक नहीं है।

## चरण 2: **इमेज से टेक्स्ट निकालने** के लिए जावा क्लास बनाएं

अब हम वास्तविक प्रोग्राम लिखेंगे। नीचे दिया गया कोड `ExtractTextDemo.java` के रूप में `src/main/java/com/example/ocr/` में सेव करें।

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### यह संरचना क्यों काम करती है

* **अलग‑अलग क्रमांकित ब्लॉक्स** प्रवाह को आसानी से फॉलो करने में मदद करते हैं, विशेषकर जब आप **OCR के लिए इमेज लोड करें** या **फ़ोटो से टेक्स्ट पहचानें** खोज रहे हों।  
* इमेज लोडिंग और पहचान के चारों ओर `try/catch` प्रोग्राम को सुगमता से फेल होने देता है—जब फ़ाइल पाथ गलत हो या OCR इंजन भाषा डेटा न पाए, तब उपयोगी।  
* भाषा को शुरुआती चरण (चरण 2) में सेट करना गैर‑अंग्रेज़ी स्क्रिप्ट्स की सटीकता को काफी बढ़ाता है। यदि बाद में आपको अन्य भाषाओं के लिए **java image to text** चाहिए, तो बस `OcrLanguage.UKRAINIAN` को `OcrLanguage.ENGLISH`, `FRENCH` आदि से बदल दें।  

## चरण 3: प्रोग्राम बनाएं और चलाएँ

प्रोजेक्ट रूट से, यह कमांड चलाएँ:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

या, यदि आप Gradle उपयोग कर रहे हैं:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

मान लीजिए `ukrainian_sign.jpg` में टेक्स्ट *«Ласкаво просимо»* (यूक्रेनी में “Welcome”) है, तो आपको कुछ इस तरह दिखना चाहिए:

```
=== OCR Result ===
Ласкаво просимо
```

यह आउटपुट पुष्टि करता है कि आपने सफलतापूर्वक **इमेज से टेक्स्ट निकाला** और एक ही रन में **OCR से टेक्स्ट प्राप्त किया**।

## चरण 4: वर्कफ़्लो को ट्यून करें – वास्तविक प्रोजेक्ट्स में **Java Image to Text**

हालांकि डेमो न्यूनतम है, वास्तविक‑दुनिया के अनुप्रयोगों को अक्सर थोड़ा अधिक चाहिए:

| परिदृश्य | क्या समायोजित करें | कारण |
|----------|----------------|--------|
| **Batch processing** | `List<Path>` पर लूप चलाएँ और प्रत्येक परिणाम को डेटाबेस में संग्रहीत करें। | जब आपके पास सैकड़ों फ़ोटो हों तो मैनुअल काम कम करता है। |
| **Different image formats** | `ImageIO.read(new File(path))` का उपयोग करके प्री‑प्रोसेस करें, फिर `BufferedImage` को `ocrEngine.getImage().loadFromBufferedImage(bufImg)` में पास करें। | कन्वर्ज़न के बाद PNG, BMP, या यहाँ तक कि PDFs को संभालता है। |
| **Performance tuning** | यदि आप थोड़ी कम सटीकता के साथ ठीक हैं तो `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` कॉल करें। | लो‑एंड हार्डवेयर पर पहचान को तेज़ करता है। |
| **Post‑processing** | व्हाइटस्पेस ट्रिम करें, सामान्य OCR गलत पढ़ाइयों को बदलें (`0` → `O`, `1` → `I`). | डाउनस्ट्रीम डेटा क्वालिटी में सुधार करता है। |

ये विविधताएँ मूल विचार—**फ़ोटो से टेक्स्ट पहचानें**—को बरकरार रखती हैं जबकि प्रोडक्शन वर्कलोड्स के लिए लचीलापन प्रदान करती हैं।

## सामान्य समस्याएँ एवं प्रो टिप्स

1. **गलत भाषा सेटिंग** – यदि आप चरण 2 भूल जाते हैं, तो इंजन डिफ़ॉल्ट रूप से अंग्रेज़ी उपयोग करता है, जिससे सिरिलिक अक्षर गड़बड़ में बदल जाते हैं। हमेशा भाषा कोड को दोबारा जांचें।  
2. **इमेज क्वालिटी महत्वपूर्ण है** – कम रेज़ोल्यूशन या धुंधली फ़ोटो सटीकता को घटा देती हैं। आवश्यकता होने पर कंट्रास्ट एन्हांसमेंट या बाइनराइज़ेशन के साथ प्री‑प्रोसेस करें।  
3. **फ़ाइल पाथ की अजीब बातें** – Windows पर बैकस्लैश को एस्केप करना पड़ता है (`C:\\images\\file.jpg`)। `java.nio.file` से `Path.of(...)` उपयोग करने से यह समस्या हल हो जाती है।  
4. **मेमोरी लीक्स** – `OcrEngine` नेटिव रिसोर्सेज़ रखता है। जब आप समाप्त हों तो `ocrEngine.dispose()` कॉल करें, विशेषकर लोंग‑रनिंग सर्विसेज़ में।  
5. **थ्रेड सेफ़्टी** – इंजन डिफ़ॉल्ट रूप से थ्रेड‑सेफ़ नहीं है। प्रत्येक थ्रेड के लिए अलग इंस्टेंस बनाएं या एक्सेस को सिंक्रोनाइज़ करें।  

## पूर्ण कार्यशील उदाहरण (ऑल‑इन‑वन)

नीचे एक एकल फ़ाइल है जिसे आप किसी भी IDE में कॉपी‑पेस्ट कर सकते हैं। इसमें `dispose()` कॉल और कोड को थोड़ा साफ़ बनाने के लिए एक छोटा हेल्पर मेथड शामिल है।

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

इस प्रोग्राम को चलाने पर पहले दिखाए गए समान कंसोल आउटपुट मिलेगा। `OcrLanguage.UKRAINIAN` को `OcrLanguage.ENGLISH` या किसी अन्य समर्थित भाषा से बदलने में संकोच न करें ताकि देख सकें इंजन कैसे अनुकूलित होता है।

## निष्कर्ष

हमने जावा का उपयोग करके **इमेज से टेक्स्ट निकालने** के लिए आवश्यक सभी चीज़ें कवर की हैं: OCR डिपेंडेंसी जोड़ने से लेकर **OCR के लिए इमेज लोड करने** तक,

## संबंधित ट्यूटोरियल्स

- [Aspose OCR के साथ टेक्स्ट इमेज पहचानें – पूर्ण जावा OCR ट्यूटोरियल](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Aspose.OCR का उपयोग करके भाषा के साथ इमेज टेक्स्ट को OCR कैसे करें](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose.OCR BufferedImage का उपयोग करके जावा में इमेज को टेक्स्ट में बदलें](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}