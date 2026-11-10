---
category: general
date: 2026-01-07
description: OCR की सटीकता बढ़ाने और Aspose OCR के साथ टेक्स्ट इमेज निकालने के लिए
  इमेज OCR को प्री‑प्रोसेस करें – डेवलपर्स के लिए चरण‑दर‑चरण गाइड।
draft: false
keywords:
- preprocess image OCR
- extract text image
- improve OCR accuracy
- how to preprocess OCR
language: hi
og_description: OCR की सटीकता सुधारने और Aspose OCR का उपयोग करके टेक्स्ट इमेज निकालने
  के लिए इमेज OCR को प्रीप्रोसेस करें। कोड सहित पूर्ण जावा ट्यूटोरियल।
og_title: जावा में इमेज OCR को प्रीप्रोसेस करें – सटीकता बढ़ाएँ
tags:
- OCR
- Java
- Image Processing
title: जावा में इमेज OCR को प्रीप्रोसेस करें – सटीकता बढ़ाएँ और टेक्स्ट निकालें
url: /hi/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में इमेज OCR का प्रीप्रोसेस – पूर्ण गाइड

क्या आप **preprocess image OCR** से जूझते रहे हैं क्योंकि आपके स्कैन धब्बों और तिरछे टेक्स्ट के झंझट जैसा दिखते हैं? आप अकेले नहीं हैं। अधिकांश डेवलपर्स तब रुक जाते हैं जब कच्ची इमेज शोरयुक्त, तिरछी या सिर्फ कम‑कॉन्ट्रास्ट वाली होती है, और OCR इंजन अपेक्षित वाक्यों के बजाय बकवास आउटपुट करता है।  

अच्छी खबर यह है कि कुछ प्रीप्रोसेसिंग स्टेप्स **OCR की सटीकता को काफी बढ़ा** सकते हैं, जिससे एक धुंधली तस्वीर साफ़, मशीन‑रीडेबल टेक्स्ट में बदल जाती है। इस ट्यूटोरियल में हम Aspose OCR for Java का उपयोग करके **how to preprocess OCR** को चरण‑दर‑चरण देखेंगे, और आप देखेंगे कि **extract text image** कंटेंट को विश्वसनीय रूप से कैसे निकालें।

हम वह सब कवर करेंगे जिसकी आपको जरूरत है: आवश्यक लाइब्रेरीज़, चरण‑दर‑चरण कोड, प्रत्येक विकल्प का महत्व, और किनारे के मामलों के लिए टिप्स। अंत तक आपके पास एक तैयार‑चलाने‑योग्य प्रोग्राम होगा जो शोरयुक्त JPEG को लेगा, उसे साफ़ करेगा, और निकाले गए टेक्स्ट को कंसोल पर प्रिंट करेगा।

## आपको क्या चाहिए

- Java Development Kit (JDK) 8 या उससे नया स्थापित हो।  
- निर्भरताओं को प्रबंधित करने के लिए Maven या Gradle (हम Maven स्निपेट दिखाएंगे)।  
- Aspose OCR for Java लाइसेंस (टेस्टिंग के लिए फ्री ट्रायल काम करता है)।  
- एक सैंपल इमेज, जैसे `skewed-noisy.jpg`, जिसे ज्ञात डायरेक्टरी में रखें।  

बस इतना ही—कोई अतिरिक्त इमेज‑प्रोसेसिंग लाइब्रेरी की जरूरत नहीं क्योंकि Aspose OCR में बिल्ट‑इन प्रीप्रोसेसिंग क्षमताएँ आती हैं।

## चरण 1: अपने प्रोजेक्ट में Aspose OCR सेट अप करें

सबसे पहले, अपने `pom.xml` में Aspose OCR डिपेंडेंसी जोड़ें। यह कोर इंजन और इमेज‑प्रोसेसिंग हेल्पर्स को शामिल करता है जिन्हें हम बाद में उपयोग करेंगे।

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- use the latest version available -->
</dependency>
```

यदि आप Gradle पसंद करते हैं, तो समकक्ष है:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** अपनी डिपेंडेंसियों को अपडेट रखें; नए संस्करण अक्सर अधिक स्मार्ट deskew एल्गोरिदम शामिल करते हैं जो आगे **OCR की सटीकता को बढ़ाते** हैं।

## प्रीप्रोसेस इमेज OCR – चरण 2: इमेज लोड करें

अब लाइब्रेरी स्थापित हो गई है, हम एक `OcrEngine` इंस्टेंस बना सकते हैं और उसे उस इमेज की ओर इंगित कर सकते हैं जिसे आप साफ़ करना चाहते हैं।

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to preprocess
        // Replace "YOUR_DIRECTORY" with the actual folder path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/skewed-noisy.jpg"));
```

हम पहले इंजन को क्यों इंस्टैंशिएट करते हैं? Aspose OCR प्रीप्रोसेसिंग पाइपलाइन को सीधे इंजन से जोड़ता है, इसलिए बाद में सेट किए गए विकल्प उसी इमेज स्ट्रीम को प्रभावित करते हैं। यह सुनिश्चित करता है कि **extract text image** ऑपरेशन साफ़ किए गए संस्करण पर काम करे, न कि कच्ची फ़ाइल पर।

## OCR की सटीकता बढ़ाएँ – चरण 3: प्रीप्रोसेसिंग विकल्प कॉन्फ़िगर करें

जादू `ImageProcessingOptions` में होता है। प्रत्येक फ़्लैग एक सामान्य दोष को लक्षित करता है जो OCR प्रदर्शन को नुकसान पहुँचाता है।

```java
        // Step 3: Configure image preprocessing options
        ImageProcessingOptions processingOptions = ocrEngine.getImageProcessingOptions();

        // Straighten rotated text – essential for skewed scans
        processingOptions.setDeskew(true);

        // Remove isolated pixels that look like speckles
        processingOptions.setDespeckle(true);

        // Boost contrast by 30% – helps low‑contrast prints
        processingOptions.setContrastBoost(1.3f);
```

- **Deskew**: घूर्णन का कोण पहचानता है और इमेज को क्षैतिज में वापस घुमाता है। इसके बिना OCR इंजन अक्षरों को गलत समझ सकता है।  
- **Despeckle**: यादृच्छिक शोर को साफ़ करता है जिसे विराम चिह्न या बिखरे अक्षर समझा जा सकता है।  
- **Contrast Boost**: अग्रभूमि (टेक्स्ट) और पृष्ठभूमि के बीच अंतर को बढ़ाता है, जो **how to preprocess OCR** में फेड प्रिंट्स के लिए एक मुख्य कारक है।  

इन फ़्लैग्स को अपने स्रोत सामग्री के आधार पर टॉगल करने में संकोच न करें। उदाहरण के लिए, एक पूरी तरह स्कैन किया गया दस्तावेज़ `setDespeckle(true)` की आवश्यकता नहीं रख सकता, जिससे कुछ मिलीसेकंड बचते हैं।

## टेक्स्ट इमेज निकालें – चरण 4: प्रीप्रोसेस्ड इमेज पर OCR चलाएँ

इमेज साफ़ हो जाने के बाद, हम अंत में Aspose OCR से टेक्स्ट पहचानने को कहते हैं।

```java
        // Step 4: Run OCR on the preprocessed image
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

`recognize()` कॉल आंतरिक रूप से हमारे द्वारा कॉन्फ़िगर किए गए प्रीप्रोसेसिंग पाइपलाइन को लागू करता है, फिर कैरेक्टर सेगमेंटेशन और पहचान करता है। परिणाम एक साधारण‑टेक्स्ट स्ट्रिंग है जिसे आप डाउनस्ट्रीम प्रोसेस में फीड कर सकते हैं—सर्च इंडेक्सिंग, डेटा एंट्री ऑटोमेशन, आप नाम ले सकते हैं।

## OCR को प्रीप्रोसेस कैसे करें – सामान्य गलतियां और किनारे के मामले

### 1. इमेज साइज का महत्व
बहुत बड़ी इमेज (जैसे > 5 MP) मेमोरी पर दबाव डाल सकती हैं। यदि आपको `OutOfMemoryError` मिलता है, तो पहले `processingOptions.setResizeFactor(0.5f)` का उपयोग करके इमेज का आकार बदलें।

### 2. कलर बनाम ग्रेस्केल
Aspose OCR ग्रेस्केल इमेज के साथ सबसे अच्छा काम करता है। यदि आपका स्रोत रंगीन है, तो deskew से पहले `processingOptions.setConvertToGrayscale(true)` सक्षम करें।

### 3. मल्टी‑पेज PDFs
PDF के साथ काम करते समय, प्रत्येक पेज को इमेज के रूप में एक्सट्रैक्ट करें और लूप में वही पाइपलाइन चलाएँ। इस उद्देश्य के लिए API `PdfImageExtractor` प्रदान करता है।

### 4. भाषा समर्थन
यदि आपका टेक्स्ट अंग्रेज़ी नहीं है, तो भाषा को स्पष्ट रूप से सेट करें:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

इस स्टेप को छोड़ने से **OCR की सटीकता को बढ़ाने** में कमी आ सकती है क्योंकि इंजन कैरेक्टर सेट का अनुमान लगाने की कोशिश करता है।

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम दिया गया है, जिसे कंपाइल और रन करने के लिए तैयार है। प्लेसहोल्डर पाथ को अपने वास्तविक इमेज लोकेशन से बदलें।

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image to be processed
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/skewed-noisy.jpg"));

        // Step 3: Configure image preprocessing options
        ImageProcessingOptions processingOptions = ocrEngine.getImageProcessingOptions();
        processingOptions.setDeskew(true);          // straighten rotated text
        processingOptions.setDespeckle(true);      // remove isolated pixels
        processingOptions.setContrastBoost(1.3f);   // boost contrast by 30%
        // Optional: processingOptions.setConvertToGrayscale(true);

        // Step 4: Run OCR on the preprocessed image
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**अपेक्षित आउटपुट** (संक्षिप्त रूप में):

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
```

यदि आप गड़बड़ अक्षर देखते हैं, तो इमेज पाथ सही है और प्रीप्रोसेसिंग फ़्लैग्स इमेज की स्थिति से मेल खाते हैं, इसे दोबारा जांचें।

## विज़ुअल सारांश

<img src="preprocess-ocr.png" alt="preprocess image OCR demonstration" style="max-width:100%;">

डायग्राम फ्लो को दर्शाता है: **Load → Deskew → Despeckle → Contrast Boost → Recognize → Extract Text**। प्रत्येक ब्लॉक ऊपर दिए गए कोड स्निपेट्स से मेल खाता है।

## निष्कर्ष

हमने अभी जावा में Aspose OCR का उपयोग करके **preprocess image OCR** करने का व्यावहारिक तरीका दिखाया, जिसमें प्रोजेक्ट सेटअप से लेकर फाइन‑ट्यूनिंग विकल्पों तक सब कुछ शामिल था जो **OCR की सटीकता को बढ़ाते** हैं। deskew, despeckle, और contrast‑boost लागू करके आप शोरयुक्त, तिरछी JPEG को साफ़, सर्चेबल टेक्स्ट में बदल देते हैं—बिल्कुल वही जो आपको **extract text image** डेटा को डाउनस्ट्रीम एप्लिकेशन के लिए चाहिए।

आगे क्या? बाइनरी इमेज के लिए `setBinarizationThreshold` जैसी अन्य प्रीप्रोसेसिंग फीचर आज़माएँ, या कई इमेज को एक बैच जॉब में जोड़ें। आप परिणाम को Apache Tika के साथ इंडेक्सिंग के लिए इंटीग्रेट कर सकते हैं, या सेंटिमेंट एनालिसिस के लिए लैंग्वेज‑मॉडल में फीड कर सकते हैं। एक बार जब आप **how to preprocess OCR** की बुनियादें समझ लेते हैं, तो संभावनाएँ अनंत हैं।

किसी विशेष फ़ाइल प्रकार या भाषा के बारे में प्रश्न हैं? नीचे कमेंट छोड़ें, और कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}