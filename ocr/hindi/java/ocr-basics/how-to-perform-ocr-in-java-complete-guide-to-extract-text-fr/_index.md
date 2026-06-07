---
category: general
date: 2026-06-06
description: जावा में OCR कैसे करें – छवि से जल्दी टेक्स्ट निकालें, छवि को टेक्स्ट
  में बदलें, और एक सरल कोड उदाहरण का उपयोग करके JPG से टेक्स्ट पढ़ें।
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: hi
og_description: जावा में OCR कैसे करें – छवि से टेक्स्ट निकालना, छवि को टेक्स्ट में
  बदलना, और JPG से टेक्स्ट पढ़ना सीखें, एक तैयार‑चलाने योग्य उदाहरण के साथ।
og_title: जावा में OCR कैसे करें – चरण-दर-चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: जावा में OCR कैसे करें – छवियों से टेक्स्ट निकालने के लिए पूर्ण गाइड
url: /hi/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में OCR कैसे करें – छवियों से टेक्स्ट निकालने के लिए पूर्ण गाइड

क्या आपने कभी सोचा है कि अपने फ़ोन से ली गई तस्वीर पर **how to perform OCR** कैसे किया जाए? आप अकेले नहीं हैं। चाहे आप रसीद‑स्कैनिंग ऐप बना रहे हों या सिर्फ़ स्कैन किए गए PDF से टेक्स्ट निकालना चाहते हों, जावा में **how to perform OCR** एक ऐसा कौशल है जो जल्दी ही फायदेमंद साबित होता है। इस ट्यूटोरियल में हम एक व्यावहारिक उदाहरण के माध्यम से चलेंगे जो **extracts text from image** फ़ाइलों को, **converts image to text**, और यहाँ तक कि आपको दिखाएगा कि **read text from jpg** को कुछ ही कोड लाइनों से कैसे किया जाए।

> *Pro tip:* वही तरीका PNG, BMP, या किसी भी फ़ॉर्मेट पर काम करता है जो OCR इंजन सपोर्ट करता है—सिर्फ़ फ़ाइल नाम बदल दें।

## जावा में OCR कैसे करें – अवलोकन

ऑप्टिकल कैरेक्टर रिकॉग्निशन (OCR) वह तकनीक है जो अक्षरों की तस्वीरों को वास्तविक, खोज योग्य टेक्स्ट में बदल देती है। जावा इकोसिस्टम में कई लाइब्रेरीज़ हैं—Tesseract, Asprise, और कमर्शियल SDKs—जो सभी समान वर्कफ़्लो प्रदान करती हैं: एक इमेज लोड करें, इंजन को बताएं कि किस भाषा की अपेक्षा है, पहचान चलाएँ, और परिणाम प्राप्त करें। नीचे हम एक generic `OcrEngine` क्लास का उपयोग करेंगे ताकि उदाहरण स्पष्ट रहे, लेकिन आप इसे किसी भी concrete implementation से बदल सकते हैं जो वही पैटर्न फॉलो करता हो।

### आप क्या सीखेंगे

- एक OCR लाइब्रेरी इंस्टॉल करें (हाँ, **ocr in java** आपके सोच से आसान है)।
- एक OCR इंजन इंस्टेंस बनाएं और कॉन्फ़िगर करें।
- एक JPG (या कोई भी इमेज) लोड करें और भाषा सेट करें।
- इमेज को प्रोसेस करें और **extract text from image** फ़ाइलों को निकालें।
- पहचाने गए स्ट्रिंग को कंसोल पर प्रिंट करें।

अंत तक आपके पास एक self‑contained जावा प्रोग्राम होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं और तुरंत चला सकते हैं।

![OCR करने का उदाहरण](ocr-example.png "जावा में OCR करने का चित्रण")

## चरण 1 – OCR लाइब्रेरी इंस्टॉल और इम्पोर्ट करें (ocr in java)

जावा की एक भी लाइन लिखने से पहले, आपको एक ऐसी लाइब्रेरी चाहिए जो वास्तव में भारी काम करे। यदि आप Maven उपयोग कर रहे हैं, तो इस तरह की डिपेंडेंसी जोड़ें ( `com.example.ocr` को अपने चुने हुए SDK के वास्तविक ग्रुप ID से बदलें):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

यदि आप Gradle पसंद करते हैं:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

एक बार JAR आपके क्लासपाथ पर हो जाए, तो उन क्लासेज़ को इम्पोर्ट करें जिनकी आपको आवश्यकता होगी:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

**Why this matters:** सही क्लासेज़ को इम्पोर्ट करने से “cannot find symbol” त्रुटियों से बचा जा सकता है और आपका IDE खुश रहता है—जब आप **convert image to text** करने की कोशिश कर रहे हों तो मिसिंग इम्पोर्ट से अधिक निराशाजनक कुछ नहीं।

## चरण 2 – OCR इंजन इंस्टेंस बनाएं (how to perform OCR)

अब जब लाइब्रेरी तैयार है, इंजन को स्पिन अप करें। इंजन को उस दिमाग की तरह सोचें जो पिक्सेल को देखेगा और अक्षरों का अनुमान लगाएगा।

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

इंजन बनाना आमतौर पर सस्ता होता है; अधिकांश SDKs आंतरिक बफ़र्स को लेज़ीली अलोकेट करते हैं, इसलिए यदि आप बैच प्रोसेस कर रहे हैं तो आप कई इमेजेज़ में वही इंस्टेंस सुरक्षित रूप से पुन: उपयोग कर सकते हैं।

## चरण 3 – इमेज लोड करें और भाषा सेट करें (extract text from image)

अगला कदम इंजन को पढ़ने के लिए कुछ देना है। यहाँ हम डिस्क से एक JPEG लोड करते हैं और OCR इंजन को बताते हैं कि टेक्स्ट मोंगोलियन में है (ISO 639‑2 कोड “mon”)। आप अपने उपयोग‑केस के अनुसार पाथ या भाषा कोड बदल सकते हैं।

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

**Side note:** यदि आप भाषा सेट नहीं करते, तो इंजन डिफ़ॉल्ट रूप से अंग्रेज़ी लेता है, जो तब सटीकता को काफी घटा सकता है जब टेक्स्ट वास्तव में सिरिलिक या कोई अन्य लिपि हो। जब भी संभव हो, सही भाषा निर्दिष्ट करना हमेशा सुनिश्चित करें।

## चरण 4 – इमेज प्रोसेस करें और परिणाम प्राप्त करें (convert image to text)

इमेज और भाषा सेट होने के बाद, इंजन से उसका जादू करने को कहें। `process()` कॉल OCR एल्गोरिद्म चलाता है और एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें पहचाना गया स्ट्रिंग और कॉन्फिडेंस स्कोर होते हैं।

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

पर्दे के पीछे, इंजन प्री‑प्रोसेसिंग कर सकता है—डेस्क्यूइंग, बाइनराइज़ेशन, नॉइज़ रिडक्शन—ताकि आपको ये कदम खुद लिखने न पड़े। यही कारण है कि अधिकांश आधुनिक OCR लाइब्रेरीज़ **convert image to text** कार्यों के लिए उपयोग करने में आनंद देती हैं।

## चरण 5 – निकाले गए टेक्स्ट को आउटपुट करें (read text from jpg)

अंत में, परिणाम से plain‑text निकालें और उसके साथ कुछ उपयोगी करें। इस डेमो में हम इसे सिर्फ़ कंसोल पर प्रिंट करते हैं, लेकिन आप इसे फ़ाइल में लिख सकते हैं, सर्च इंडेक्स में फीड कर सकते हैं, या किसी अन्य सर्विस को पास कर सकते हैं।

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

यह लाइन अकेले यह सिद्ध करती है कि आपने सफलतापूर्वक **read text from jpg** (या कोई भी सपोर्टेड फ़ॉर्मेट) किया है। यदि आउटपुट गड़बड़ दिखे, तो भाषा कोड और इमेज क्वालिटी को दोबारा जांचें।

## पूर्ण कार्यशील उदाहरण (सभी चरण एक साथ)

नीचे एक पूर्ण, तैयार‑चलाने योग्य जावा क्लास है जो हर भाग को जोड़ता है। इसे `OcrDemo.java` नाम की फ़ाइल में कॉपी करें, इमेज पाथ और भाषा को समायोजित करें, फिर `javac OcrDemo.java && java OcrDemo` चलाएँ।

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### अपेक्षित आउटपुट

यदि `input.jpg` में मोंगोलियन वाक्य “Сайн байна уу?” है तो कंसोल में यह दिखेगा:

```
=== Recognized Text ===
Сайн байна уу?
```

यदि इमेज धुंधली है या भाषा कोड गलत है, तो आपको गड़बड़ अक्षर या खाली स्ट्रिंग दिखेगी—सामान्य pitfalls जिन्हें हम आगे चर्चा करेंगे।

## सामान्य समस्याएँ और उन्हें कैसे ठीक करें

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| गड़बड़ सिरिलिक अक्षर | गलत भाषा कोड (डिफ़ॉल्ट अंग्रेज़ी) | Set `ocrEngine.getSettings().setLanguage("mon")` या उपयुक्त कोड सेट करें। |
| कोई आउटपुट नहीं | इमेज पाथ गलत या फ़ाइल पढ़ी नहीं जा रही | पाथ को सत्यापित करें, सुनिश्चित करें फ़ाइल मौजूद है, और प्रक्रिया के पास पढ़ने की अनुमति है। |
| कम सटीकता (<70 %) | इमेज कम‑कॉन्ट्रास्ट या घुमाई हुई है | इमेज को प्री‑प्रोसेस करें: कॉन्ट्रास्ट बढ़ाएँ, डेस्क्यूइंग करें, या ग्रेस्केल में बदलें इससे पहले कि आप इसे इंजन को दें। |
| `OutOfMemoryError` बड़े PDFs पर | एक साथ कई हाई‑रेज़ोल्यूशन पेज लोड करना | पेज़ को एक‑एक करके प्रोसेस करें, या OCR से पहले इमेज को डाउनस्केल करें। |

### प्रो टिप: बैच प्रोसेसिंग

यदि आपको बड़े पैमाने पर **extract text from image** फ़ाइलें निकालनी हों, तो कोर लॉजिक को एक लूप में रैप करें:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

यह स्निपेट दिखाता है कि एक सिंगल JPG से पूरे फ़ोल्डर के स्कैन तक स्केल करना कितना आसान है।

## आगे क्या देखें – अगला क्या एक्सप्लोर करें?

- **Language Packs:** अधिकांश OCR SDKs अतिरिक्त भाषा डेटा फ़ाइलें डाउनलोड करने की अनुमति देते हैं। नया पैक जोड़ने से आप **convert image to text** को अंग्रेज़ी और मोंगोलियन से आगे की भाषाओं के लिए कर सकते हैं।
- **PDF OCR:** इस कोड को Apache PDFBox के साथ मिलाएँ ताकि

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर करने में मदद करेंगे।

- [छवियों से टेक्स्ट निकालें – जावा के लिए Aspose.OCR के साथ OCR बेसिक्स](/ocr/english/java/ocr-basics/)
- [जावा में Aspose.OCR BufferedImage का उपयोग करके इमेज को टेक्स्ट में बदलें](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose.OCR का उपयोग करके भाषा के साथ इमेज टेक्स्ट को OCR कैसे करें](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}