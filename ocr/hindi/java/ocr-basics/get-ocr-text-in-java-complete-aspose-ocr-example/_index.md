---
category: general
date: 2026-01-07
description: Aspose OCR Java का उपयोग करके छवि से OCR टेक्स्ट प्राप्त करें। सीखें
  कि कैसे टेक्स्ट इमेज निकालें, इमेज OCR लोड करें, और कुछ ही मिनटों में जावा OCR उदाहरण
  चलाएँ।
draft: false
keywords:
- get OCR text
- extract text image
- java OCR example
- aspose OCR Java
- load image OCR
language: hi
og_description: Aspose OCR Java के साथ छवियों से OCR टेक्स्ट प्राप्त करें। यह गाइड
  एक जावा OCR उदाहरण दिखाता है, कैसे टेक्स्ट छवि निकाली जाए, और कैसे छवि OCR को कुशलतापूर्वक
  लोड किया जाए।
og_title: जावा में OCR टेक्स्ट प्राप्त करें – पूर्ण Aspose OCR ट्यूटोरियल
tags:
- OCR
- Java
- Aspose
- Image Processing
title: जावा में OCR टेक्स्ट प्राप्त करें – पूर्ण Aspose OCR उदाहरण
url: /hi/java/ocr-basics/get-ocr-text-in-java-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में OCR टेक्स्ट प्राप्त करें – पूर्ण Aspose OCR उदाहरण

क्या आपको कभी स्कैन किए हुए दस्तावेज़ से **OCR टेक्स्ट** प्राप्त करने की जरूरत पड़ी है लेकिन यह नहीं पता था कि कौन सी लाइब्रेरी चुनें? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स—जैसे इनवॉइस ऑटोमेशन, रसीद प्रोसेसिंग, या बहुभाषी फ़ॉर्म डिजिटलीकरण—में छवियों से टेक्स्ट निकालना ऑटोमेशन की पहली कदम है।  

इस ट्यूटोरियल में हम एक **java OCR example** के माध्यम से चलेंगे जो Aspose OCR for Java लाइब्रेरी का उपयोग करता है। अंत तक आप जानेंगे कि कैसे **load image OCR** किया जाए, इंजन चलाया जाए, और **extract text image** डेटा कुछ ही कोड लाइनों से निकाला जाए। कोई फालतू बात नहीं, सिर्फ एक व्यावहारिक समाधान जिसे आप अपने प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं।

## आप क्या सीखेंगे

- Aspose OCR for Java को सेट अप करने का तरीका (Maven कोऑर्डिनेट्स सहित)।
- **load image OCR** करने और भाषा निर्दिष्ट करने के सटीक चरण।
- **get OCR text** को एक साधारण स्ट्रिंग के रूप में प्राप्त करने और उसे कंसोल में प्रिंट करने का तरीका।
- बहुभाषी छवियों को संभालने और भाषाओं को ऑटो‑डिटेक्ट करने के टिप्स।

*Prerequisites*: Java 8 या उससे नया, Maven‑संगत IDE (IntelliJ IDEA, Eclipse, या VS Code), और एक वैध Aspose OCR for Java लाइसेंस (मुफ़्त ट्रायल मूल्यांकन के लिए काम करता है)।

![OCR टेक्स्ट को छवि से प्राप्त करने का फ्लोचार्ट Aspose OCR Java का उपयोग करके](https://example.com/ocr-flowchart.png "OCR टेक्स्ट फ्लो डायग्राम")

## चरण 1 – Aspose OCR डिपेंडेंसी जोड़ें (Load Image OCR)

सबसे पहले, Maven को Aspose OCR लाइब्रेरी खींचने के लिए बताएं। अपना `pom.xml` खोलें और `<dependencies>` के अंदर निम्नलिखित `<dependency>` ब्लॉक डालें:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **Pro tip**: यदि आप Gradle का उपयोग कर रहे हैं, तो समकक्ष है `implementation 'com.aspose:aspose-ocr:23.9'`. डिपेंडेंसी जोड़ना आपके प्रोजेक्ट में **load image OCR** क्षमताएँ लाने का सबसे सस्ता तरीका है।

## चरण 2 – OCR इंजन बनाएं और अपनी छवि लोड करें

अब हम एक छोटा Java क्लास लिखेंगे जो `OcrEngine` इंस्टेंस बनाता है, उसे एक इमेज फ़ाइल की ओर इंगित करता है, और इंजन को बताता है कि कौन सी भाषा को पहचानना है। भाषा को उसके ISO‑639‑2 कोड से पहचाना जाता है (जैसे, तमिल के लिए `"tam"`).

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {

    public static void main(String[] args) throws Exception {
        // 2️⃣ Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load the image you want to process – this is the "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // 2️⃣ Choose the language (ISO‑639‑2). Change "tam" to any supported code.
        engine.getEngineOptions().setLanguage("tam");
        // If you prefer automatic detection, uncomment the next line:
        // engine.getEngineOptions().setAutoDetectLanguage(true);
```

### भाषा को स्पष्ट रूप से सेट क्यों करें?

भाषा निर्दिष्ट करने से फ़ॉल्स पॉज़िटिव कम होते हैं और पहचान तेज़ होती है। बहुभाषी PDFs के लिए आप भाषा कोड की एक एरे पर लूप कर सकते हैं, या सुविधा के लिए ऑटो‑डिटेक्ट सक्षम कर सकते हैं।

## चरण 3 – OCR प्रक्रिया चलाएँ और **Get OCR Text**

इंजन कॉन्फ़िगर होने के बाद, अगली लाइन वास्तव में पहचान करती है। परिणाम ऑब्जेक्ट में निकाली गई स्ट्रिंग और अतिरिक्त मेटाडेटा होता है।

```java
        // 3️⃣ Perform OCR – this is where we finally **get OCR text**
        OcrResult result = engine.recognize();

        // 3️⃣ Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

`LanguageExample` चलाने पर, आपको कुछ इस तरह दिखना चाहिए:

```
=== Extracted Text ===
தமிழ் உரை இங்கு வருகிறது...
```

यदि आपने `setAutoDetectLanguage(true)` उपयोग किया है, तो इंजन आपके लिए भाषा का अनुमान लगाने की कोशिश करेगा, जो अज्ञात दस्तावेज़ों से निपटने में उपयोगी है।

## चरण 4 – सामान्य किनारे मामलों को संभालना (Extract Text Image Variations)

### कम‑रिज़ॉल्यूशन छवियों से निपटना

OCR की सटीकता 300 dpi से नीचे तेज़ी से घटती है। यदि आपकी स्रोत छवि कम‑रिज़ॉल्यूशन है, तो पहले उसे अप‑सैंपल करने पर विचार करें:

```java
engine.getEngineOptions().setResolution(300); // forces 300 DPI
```

### बैकग्राउंड नॉइज़ हटाना

कभी‑कभी स्कैन किए हुए फ़ॉर्म में धब्बे होते हैं जो इंजन को भ्रमित कर देते हैं। आप प्री‑प्रोसेसिंग सक्षम कर सकते हैं:

```java
engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);
```

### विशिष्ट क्षेत्रों से टेक्स्ट निकालना

यदि आपको केवल किसी विशेष आयत (जैसे, टेबल सेल) से टेक्स्ट चाहिए, तो `recognize()` कॉल करने से पहले एक `Rectangle` सेट करें:

```java
engine.setRegion(new Rectangle(50, 100, 400, 200));
```

ये समायोजन आपके **java OCR example** को प्रोडक्शन वर्कलोड्स के लिए पर्याप्त मजबूत बनाते हैं।

## चरण 5 – आउटपुट सत्यापित करें (आपको क्या अपेक्षा करनी चाहिए?)

एक सफल रन छवि का साधारण टेक्स्ट संस्करण प्रिंट करेगा। बहुभाषी छवियों के लिए आप मिश्रित लिपियों को देख सकते हैं:

```
Hello World
こんにちは世界
مرحبا بالعالم
```

यदि आउटपुट खाली या गड़बड़ है, तो दोबारा जांचें:

1. `setImage` में फ़ाइल पाथ (क्या यह सही है?)।
2. भाषा कोड छवि में स्क्रिप्ट से मेल खाता है।
3. छवि की गुणवत्ता (कॉन्ट्रास्ट, DPI) पर्याप्त है।

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा फ़ाइल दिया गया है, जिसे कंपाइल और रन करने के लिए तैयार है। `YOUR_DIRECTORY/multilingual.png` को अपने टेस्ट इमेज के वास्तविक पाथ से बदलें।

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine engine = new OcrEngine();

        // Load the image – this is the core "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // Set language (ISO‑639‑2). For Tamil use "tam". Change as needed.
        engine.getEngineOptions().setLanguage("tam");
        // Uncomment for auto‑detect:
        // engine.getEngineOptions().setAutoDetectLanguage(true);

        // Optional: improve accuracy on low‑res images
        // engine.getEngineOptions().setResolution(300);
        // engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);

        // Perform OCR and retrieve text
        OcrResult result = engine.recognize();

        // Print the extracted text – this is how we **get OCR text**
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

कम्पाइल और रन करें:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.LanguageExample"
```

अब आपको निकाला गया कंटेंट अपने कंसोल में प्रिंट होता दिखेगा।

---

## निष्कर्ष

हमने अभी आपको Aspose OCR for Java का उपयोग करके छवि से **OCR टेक्स्ट प्राप्त करने** का तरीका दिखाया है। इस **java OCR example** को फॉलो करके आप **extract text image** डेटा, **load image OCR** कर सकते हैं, और बहुभाषी या शोरयुक्त इनपुट के लिए इंजन को भी ट्यून कर सकते हैं।  

अब आप आगे कर सकते हैं:

- OCR चरण को बड़े वर्कफ़्लो में इंटीग्रेट करें (जैसे, टेक्स्ट को डेटाबेस में स्टोर करना)।
- इसे एक ट्रांसलेशन API के साथ मिलाकर बहुभाषी स्कैन को एक ही भाषा में बदलें।
- PDF कन्वर्ज़न या बारकोड डिटेक्शन जैसे अन्य Aspose OCR फीचर्स के साथ प्रयोग करें।

इसे आज़माएँ, कुछ चीज़ें तोड़ें, और फिर सेटिंग्स को परिष्कृत करें जब तक आउटपुट एकदम सही न हो। हैप्पी कोडिंग, और आपका OCR हमेशा स्पष्ट रहे!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}