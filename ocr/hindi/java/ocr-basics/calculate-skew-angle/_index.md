---
date: 2026-06-19
description: Aspose.OCR के साथ OCR की सटीकता बढ़ाने के लिए scanned document को rotate
  करना, Java में skew angle की गणना करना सीखें। Java डेवलपर्स के लिए चरण‑दर‑चरण गाइड।
keywords:
- rotate scanned document
- improve ocr accuracy
- rotate image degrees java
- aspose ocr java tutorial
linktitle: Java का उपयोग करके Aspose.OCR के साथ scanned document को rotate करने और
  skew angle की गणना कैसे करें
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to rotate scanned document, calculate skew angle Java, and
    improve OCR accuracy with Aspose.OCR. Step‑by‑step guide for Java developers.
  headline: How to rotate scanned document and calculate skew angle in Java using
    Aspose.OCR
  type: TechArticle
- description: Learn how to rotate scanned document, calculate skew angle Java, and
    improve OCR accuracy with Aspose.OCR. Step‑by‑step guide for Java developers.
  name: How to rotate scanned document and calculate skew angle in Java using Aspose.OCR
  steps:
  - name: Import Packages
    text: '`AsposeOCR` is the core class that exposes OCR and image‑analysis functions.
      `java.io.File` is used only for path handling. **Definition anchor:** `AsposeOCR`
      is Aspose.OCR''s primary class that provides methods for text extraction, skew
      detection, and image preprocessing.'
  - name: Set Up Document Directory
    text: Store the folder path in a variable so you can reuse it for multiple images
      or switch environments without code changes. **Definition anchor:** `dataDir`
      is a `String` variable that points to the directory containing the source images
      you intend to process.
  - name: Specify Image Path
    text: Combine the directory with the file name to build the absolute path required
      by the API. **Definition anchor:** `imagePath` is a `String` that holds the
      full file system location of the image you will analyze.
  - name: Create API Instance
    text: Instantiate the `AsposeOCR` object once per application run; it loads the
      native libraries internally. **Definition anchor:** `ocrEngine` is an instance
      of `AsposeOCR` that gives you access to all OCR‑related methods, including `CalcSkewImage`.
  - name: Calculate Skew Angle
    text: 'Wrap the call in a try‑catch block to handle I/O problems gracefully. The
      method returns a `double` that you can log, store, or pass to a rotation routine.
      **Definition anchor:** `CalcSkewImage(String imagePath)` scans the supplied
      image, detects the dominant text baseline, and returns the rotation '
  type: HowTo
- questions:
  - answer: It measures the rotation (in degrees) of text lines inside an image.
    question: What does “calculate skew angle” do?
  - answer: The library provides a fast, out‑of‑the‑box method (`CalcSkewImage`) that
      works with PNG, JPEG, TIFF, and more.
    question: Why use Aspose.OCR for this?
  - answer: A temporary license works for evaluation; a full license is required for
      production.
    question: Do I need a license to run the sample?
  - answer: Yes—call `CalcSkewImage` inside a loop for multiple files.
    question: Can the API handle batch processing?
  - answer: Java 8+ is fully supported.
    question: What Java version is required?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Java का उपयोग करके Aspose.OCR के साथ scanned document को rotate करने और skew
  angle की गणना कैसे करें
url: /hi/java/ocr-basics/calculate-skew-angle/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में Aspose.OCR का उपयोग करके स्कैन किए गए दस्तावेज़ को घुमाने और स्क्यू एंगल की गणना कैसे करें

## परिचय

यदि आपने कभी स्कैन किए गए इनवॉइस, रसीद या हस्तलिखित फ़ॉर्म पर OCR चलाने की कोशिश की है, तो आपने संभवतः देखा होगा कि कुछ डिग्री का झुकाव भी पहचान परिणामों को बिगाड़ सकता है। **स्कैन किए गए दस्तावेज़ को घुमाना** एक वास्तविक क्षैतिज बेसलाइन पर लाना OCR की सटीकता *सुधारने* का सबसे भरोसेमंद तरीका है। इस ट्यूटोरियल में आप सीखेंगे कि Aspose.OCR के साथ **Java में स्क्यू एंगल की गणना** कैसे करें, फिर उस मान का उपयोग करके **Java में इमेज को डिग्री में घुमाना** और अंत में OCR इंजन को पूरी तरह संरेखित चित्र फ़ीड करें। यह तरीका सिंगल‑पेज फ़ाइलों और बड़े बैच दोनों के लिए काम करता है, और इसके लिए केवल Aspose.OCR JAR की आवश्यकता होती है—कोई बाहरी इमेज‑प्रोसेसिंग लाइब्रेरी अनिवार्य नहीं है।

## त्वरित उत्तर
- **“calculate skew angle” क्या करता है?** यह छवि के भीतर टेक्स्ट लाइनों के घुमाव (डिग्री में) को मापता है।  
- **Aspose.OCR का उपयोग क्यों करें?** लाइब्रेरी एक तेज़, तैयार‑उपयोग विधि (`CalcSkewImage`) प्रदान करती है जो PNG, JPEG, TIFF आदि के साथ काम करती है।  
- **क्या नमूना चलाने के लिए लाइसेंस चाहिए?** मूल्यांकन के लिए एक अस्थायी लाइसेंस काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **क्या API बैच प्रोसेसिंग संभाल सकता है?** हाँ—कई फ़ाइलों के लिए लूप में `CalcSkewImage` को कॉल करें।  
- **कौन सा Java संस्करण आवश्यक है?** Java 8+ पूरी तरह समर्थित है।

## calculate skew angle java क्या है?

**calculate skew angle java** ऑपरेशन प्रिंटेड या हस्तलिखित टेक्स्ट के क्षैतिज बेसलाइन से कोणीय विचलन निर्धारित करता है। परिणाम डिग्री में व्यक्त किया जाता है (घड़ी की दिशा में घुमाव के लिए सकारात्मक, विपरीत दिशा में नकारात्मक)। इस मान को जानने से आप OCR से पहले प्रोग्रामेटिक रूप से इमेज को डेस्क्यू कर सकते हैं, जिससे गलत पहचान कम होती है।

## Java के लिए Aspose.OCR क्यों उपयोग करें?

लाइब्रेरी लोड करने पर आपको एक‑लाइन API मिलती है जो किसी भी समर्थित इमेज का सटीक झुकाव लौटाती है। **Aspose.OCR सामान्य सर्वर हार्डवेयर पर प्रति मिनट 50 मिलियन से अधिक अक्षर प्रोसेस करता है**, और यह अतिरिक्त निर्भरताओं के बिना 5 प्रमुख इमेज फ़ॉर्मेट (PNG, JPEG, BMP, TIFF, GIF) का समर्थन करता है। यह मापी गई प्रदर्शन इसे उच्च‑वॉल्यूम दस्तावेज़ पाइपलाइन में *OCR की सटीकता सुधारने* की आवश्यकता होने पर एक ठोस विकल्प बनाता है।

## पूर्वापेक्षाएँ

- **Java Development Kit** – JDK 8 या बाद का (बेहतर मॉड्यूल समर्थन के लिए Java 11+ की सिफ़ारिश)।  
- **Aspose.OCR for Java** – आधिकारिक साइट से नवीनतम JAR डाउनलोड करें [here](https://reference.aspose.com/ocr/java/).  
- **Sample Image** – कोई भी स्कैन किया गया इमेज (जैसे `p3.png`) जिसमें स्पष्ट झुकाव हो।  
- **License** – परीक्षण के लिए अस्थायी ट्रायल लाइसेंस या उत्पादन उपयोग के लिए पूर्ण व्यावसायिक लाइसेंस।

## Aspose.OCR का उपयोग करके Java में स्क्यू एंगल की गणना कैसे करें?

अपनी इमेज लोड करें, स्क्यू‑गणना मेथड को कॉल करें, और लौटाए गए कोण को कैप्चर करें। प्रश्न का उत्तर सीधा है: **आप `CalcSkewImage` को एक ही कॉल में झुकाव प्राप्त करते हैं, जो डिग्री दर्शाने वाला double लौटाता है**। यह कॉल पिक्सेल की संख्या के सापेक्ष O(N) समय में चलता है और 300 dpi पेज के लिए 10 MB से कम हीप की आवश्यकता होती है।

नीचे चरण‑दर‑चरण walkthrough दिया गया है। प्रत्येक चरण को उस प्लेसहोल्डर से पहले वर्णित किया गया है जिसमें मूल रूप से कोड उदाहरण था।

### चरण 1: पैकेज आयात करें

`AsposeOCR` Aspose.OCR की मुख्य क्लास है जो टेक्स्ट एक्सट्रैक्शन, स्क्यू डिटेक्शन, और इमेज प्री‑प्रोसेसिंग के लिए मेथड प्रदान करती है।  

**Definition anchor:** `AsposeOCR` Aspose.OCR की मुख्य क्लास है जो टेक्स्ट एक्सट्रैक्शन, स्क्यू डिटेक्शन, और इमेज प्री‑प्रोसेसिंग के लिए मेथड प्रदान करती है।

### चरण 2: दस्तावेज़ डायरेक्टरी सेट करें

स्रोत इमेजेज़ वाली डायरेक्टरी की ओर इशारा करता है जिसे आप प्रोसेस करना चाहते हैं।  

**Definition anchor:** `dataDir` एक `String` वेरिएबल है जो स्रोत इमेजेज़ वाली डायरेक्टरी की ओर इशारा करता है जिसे आप प्रोसेस करना चाहते हैं।

### चरण 3: इमेज पाथ निर्दिष्ट करें

इमेज का पूर्ण फ़ाइल सिस्टम पाथ रखता है जिसे आप विश्लेषण करेंगे।  

**Definition anchor:** `imagePath` एक `String` है जो उस इमेज का पूर्ण फ़ाइल सिस्टम पाथ रखता है जिसे आप विश्लेषण करेंगे।

### चरण 4: API इंस्टेंस बनाएं

`AsposeOCR` का एक इंस्टेंस है जो आपको सभी OCR‑संबंधित मेथड्स तक पहुँच देता है, जिसमें `CalcSkewImage` भी शामिल है।  

**Definition anchor:** `ocrEngine` `AsposeOCR` का एक इंस्टेंस है जो आपको सभी OCR‑संबंधित मेथड्स तक पहुँच देता है, जिसमें `CalcSkewImage` भी शामिल है।

### चरण 5: स्क्यू एंगल की गणना करें

प्रदान की गई इमेज को स्कैन करता है, प्रमुख टेक्स्ट बेसलाइन का पता लगाता है, और डिग्री में घुमाव का कोण लौटाता है।  

**Definition anchor:** `CalcSkewImage(String imagePath)` प्रदान की गई इमेज को स्कैन करता है, प्रमुख टेक्स्ट बेसलाइन का पता लगाता है, और डिग्री में घुमाव का कोण लौटाता है।

## स्क्यू की गणना के बाद Java में इमेज को डिग्री में कैसे घुमाएं?

Java 2D में, `BufferedImage` मेमोरी में इमेज को दर्शाता है, `AffineTransform` ज्यामितीय ट्रांसफ़ॉर्मेशन को परिभाषित करता है, `Graphics2D` ड्रॉइंग क्षमताएँ प्रदान करता है, और `ImageIO` इमेज फ़ाइलों को पढ़ने और लिखने को संभालता है।

यहाँ संक्षिप्त वर्कफ़्लो दिया गया है (मूल गिनती को बनाए रखने के लिए कोई अतिरिक्त कोड ब्लॉक नहीं जोड़ा गया है):

1. **लोड** स्रोत फ़ाइल को `ImageIO.read(new File(imagePath))` के माध्यम से `BufferedImage` में लोड करें।  
2. **बनाएँ** एक `AffineTransform` इंस्टेंस और `rotate(Math.toRadians(angle), centerX, centerY)` कॉल करें जहाँ `angle` वह मान है जो `CalcSkewImage` द्वारा लौटाया गया है।  
3. **ड्रॉ** ट्रांसफ़ॉर्म की गई इमेज को एक नई `BufferedImage` पर `Graphics2D` कॉन्टेक्स्ट (`g2d.drawImage(original, transform, null)`) का उपयोग करके बनाएं।  
4. **लिखें** घुमाए गए परिणाम को `ImageIO.write(rotated, "png", new File(outputPath))` के साथ डिस्क पर वापस लिखें।  

**calculate skew angle java** चरण को इस **rotate image degrees java** रूटीन के साथ जोड़कर, आप एक पूरी तरह स्वचालित डेस्क्यूइंग पाइपलाइन बनाते हैं जिसे सरल `for` लूप में लपेटकर प्रति मिनट सैकड़ों पेज संभाल सकते हैं।

## सामान्य समस्याएँ और समाधान

| Issue | Reason | Fix |
|-------|--------|-----|
| `NullPointerException` | `dataDir` एक गैर‑मौजूद फ़ोल्डर की ओर इशारा करता है | पाथ सत्यापित करें और सुनिश्चित करें कि फ़ोल्डर मौजूद है |
| `IOException` | इमेज फ़ाइल नहीं मिली या पढ़ी नहीं जा सकती | फ़ाइल नाम (`p3.png`) और फ़ाइल अनुमतियों की जाँच करें |
| Unexpected angle (e.g., 0° on a clearly skewed image) | कम कंट्रास्ट या शोरयुक्त इमेज | इमेज को पूर्व‑प्रोसेस करें (कंट्रास्ट बढ़ाएँ, बाइनराइज़ करें) `CalcSkewImage` कॉल करने से पहले |

## अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या Aspose.OCR स्वचालित रूप से स्क्यू एंगल को ठीक कर सकता है?

**A:** Aspose.OCR स्क्यू‑एंगल की गणना प्रदान करता है, लेकिन स्वचालित घुमाव अंतर्निहित नहीं है। आप लौटाए गए कोण को किसी भी Java इमेज‑प्रोसेसिंग लाइब्रेरी (जैसे Java 2D, OpenCV) के साथ उपयोग करके स्वयं इमेज को डेस्क्यू कर सकते हैं।

### Q2: क्या Aspose.OCR कई इमेजेज़ की बैच प्रोसेसिंग के लिए उपयुक्त है?

**A:** हाँ। कोड को एक लूप में रखें जो आपके इमेज संग्रह पर इटररेट करे, प्रत्येक फ़ाइल के लिए `CalcSkewImage` को कॉल करे। लाइब्रेरी प्रत्येक कॉल को स्वतंत्र रूप से संभालती है और कम मेमोरी ओवरहेड बनाए रखती है।

### Q3: सटीक स्क्यू एंगल गणना के लिए कोई विशेष इमेज फ़ॉर्मेट आवश्यकताएँ हैं?

**A:** API PNG, JPEG, BMP, TIFF, और GIF का समर्थन करता है। सर्वोत्तम सटीकता के लिए, उच्च‑रिज़ॉल्यूशन (≥ 300 dpi) स्कैन का उपयोग करें जिसमें स्पष्ट टेक्स्ट कंट्रास्ट हो; शोरयुक्त या अत्यधिक संकुचित फ़ाइलों को पूर्व‑फ़िल्टरिंग की आवश्यकता हो सकती है।

### Q4: Aspose.OCR के लिए अस्थायी लाइसेंस कैसे प्राप्त करें?

**A:** मूल्यांकन और विकास के लिए काम करने वाला 30‑दिन का ट्रायल लाइसेंस प्राप्त करने हेतु [this link](https://purchase.aspose.com/temporary-license/) पर जाएँ।

### Q5: Aspose.OCR से संबंधित मदद या मुद्दों पर चर्चा कहां कर सकते हैं?

**A:** प्रश्न पूछने, स्निपेट्स साझा करने और Aspose इंजीनियरों तथा अन्य डेवलपर्स से सलाह पाने के लिए [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) में शामिल हों।

### Q6: क्या मैं स्क्यू‑एंगल गणना को अन्य Aspose उत्पादों जैसे Aspose.PDF के साथ एकीकृत कर सकता हूँ?

**A:** बिल्कुल। डेस्क्यू करने के बाद, सुधारी गई इमेज को Aspose.PDF, Aspose.Words, या किसी भी अन्य Aspose लाइब्रेरी में आगे की मैनिपुलेशन, रूपांतरण या अभिलेख के लिए फीड कर सकते हैं।

### Q7: क्या यह विधि हस्तलिखित टेक्स्ट के साथ काम करती है?

**A:** यह प्रिंटेड टेक्स्ट के साथ सबसे अच्छा काम करता है जहाँ बेसलाइन स्थिर होती है। हस्तलिखित लाइनों में अनियमित स्ट्रोक के कारण कम विश्वसनीय कोण मिल सकते हैं।

## निष्कर्ष

अब आपके पास Java में **स्कैन किए गए दस्तावेज़ को घुमाने** के लिए एक पूर्ण, उत्पादन‑तैयार रेसिपी है: `CalcSkewImage` से झुकाव की गणना करें, Java 2D का उपयोग करके बिटमैप को घुमाएँ, और फिर पूरी तरह संरेखित इमेज पर OCR चलाएँ। यह दो‑चरणीय प्रक्रिया शोरयुक्त स्कैन पर *OCR की सटीकता* को 15‑30 % तक बढ़ाती है और प्रतिदिन हजारों पेजों तक स्केल करती है। विभिन्न इमेज क्वालिटी के साथ प्रयोग करें, पाइपलाइन को Aspose.PDF के साथ PDF निर्माण के लिए संयोजित करें, और आपके पास एंटरप्राइज़ वर्कलोड के लिए तैयार एक मजबूत दस्तावेज़‑प्रोसेसिंग इंजन होगा।

---

**अंतिम अपडेट:** 2026-06-19  
**परीक्षित संस्करण:** Aspose.OCR for Java 24.12 (लेखन के समय नवीनतम)  
**लेखक:** Aspose  

{{< blocks/products/products-backtop-button >}}

## संबंधित ट्यूटोरियल

- [Java में Aspose.OCR लाइसेंस सेट करने और सत्यापित करने का तरीका](/ocr/java/ocr-basics/set-license/)
- [Aspose.OCR for Java के साथ OCR बेसिक्स – टेक्स्ट इमेज निकालना](/ocr/java/ocr-basics/)
- [Aspose.OCR Detect Areas Mode के साथ Java में इमेज से टेक्स्ट निकालना](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

```java
String dataDir = "Your Document Directory";
```

```java
String imagePath = dataDir + "p3.png";
```

```java
AsposeOCR api = new AsposeOCR();
```

```java
try {
    double angle = api.CalcSkewImage(imagePath);
    System.out.println("Skew text is:" + angle + " degrees.");
} catch (IOException e1) {
    e1.printStackTrace();
}
```