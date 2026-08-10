---
category: general
date: 2026-06-16
description: जावा में OCR बाउंडिंग बॉक्स ट्यूटोरियल दिखाता है कि कैसे इमेज से टेक्स्ट
  निकालें, इमेज से टेक्स्ट पढ़ें, और JPG फ़ाइलों के लिए OCR कॉन्फिडेंस स्कोर प्राप्त
  करें।
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: hi
og_description: जावा में OCR बाउंडिंग बॉक्स आपको JPG फ़ाइलों से टेक्स्ट पहचानने, इमेज
  से टेक्स्ट निकालने, और OCR कॉन्फिडेंस स्कोर देखने की सुविधा देता है—सभी एक सरल कोड
  उदाहरण में।
og_title: जावा में OCR बाउंडिंग बॉक्स – छवि से टेक्स्ट निकालें
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: जावा में OCR बाउंडिंग बॉक्स – छवि से टेक्स्ट निकालें
url: /hi/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में OCR बाउंडिंग बॉक्स – इमेज से टेक्स्ट निकालें

क्या आप कभी यह सोचते रहे हैं कि जावा इमेज में प्रत्येक टेक्स्ट के टुकड़े के लिए **ocr bounding box** कैसे प्राप्त करें? इस ट्यूटोरियल में हम आपको दिखाएंगे कि कैसे **extract text from image** फ़ाइलों से टेक्स्ट निकालें, **read text from image** करें, और यहाँ तक कि **ocr confidence score** देखें जबकि आप **recognize text from jpg** फ़ाइलों को पढ़ते हैं। छोटा जवाब? आधुनिक OCR लाइब्रेरी का उपयोग करके कुछ लाइनों का कोड, साथ ही यह समझाने के लिए कि प्रत्येक कॉल क्यों महत्वपूर्ण है।

नीचे आपको एक पूर्ण, तैयार‑से‑चलाने‑योग्य उदाहरण, चरण‑दर‑चरण विवरण, और कुछ व्यावहारिक टिप्स मिलेंगी जिन्हें आप सीधे अपने प्रोजेक्ट में कॉपी कर सकते हैं। अंत तक, आप कुछ इस तरह का आउटपुट दे पाएँगे:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## आपको क्या चाहिए

- **Java 11** या नया (नीचे दिया गया सिंटैक्स संक्षिप्तता के लिए `var` कीवर्ड का उपयोग करता है, लेकिन आप इसे पुराने JDK के लिए हटा सकते हैं)।
- एक OCR लाइब्रेरी जो Java API प्रदान करती है – इस गाइड के लिए हम **[Tesseract4J](https://github.com/nguyenq/tess4j)** का उपयोग करेंगे, जो लोकप्रिय Tesseract इंजन के चारों ओर एक हल्का रैपर है।
- एक JPEG इमेज (`.jpg`) जिसमें स्पष्ट, मुद्रित टेक्स्ट हो।
- आपका पसंदीदा IDE (IntelliJ IDEA, Eclipse, VS Code…) – कोई भी चलेगा।

यदि आप लाइब्रेरी नहीं रखते हैं, तो बस यह Maven डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

अब चलिए शुरू करते हैं।

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR बाउंडिंग बॉक्स: इंजन सेटअप करना

पहली चीज़ जो आपको करनी है वह है OCR इंजन का एक इंस्टेंस बनाना। इसे ऐसे समझें जैसे आप स्कैनर को चालू कर रहे हैं जो बाद में पिक्सेल पढ़ेगा।

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**क्यों यह महत्वपूर्ण है:**  
`datapath` सेट किए बिना, Tesseract को नहीं पता चलेगा कि उसके भाषा पैक कहाँ स्थित हैं, और आपको “Failed loading language” जैसी अजीब त्रुटि मिलेगी। `setLanguage` कॉल वैकल्पिक है यदि आपको केवल डिफ़ॉल्ट अंग्रेज़ी पैक चाहिए, लेकिन स्पष्ट रूप से सेट करने से कोड भविष्य के पाठकों के लिए स्पष्ट रहता है।

## वह इमेज लोड करें जिसे आप प्रोसेस करना चाहते हैं

अब, इंजन को वह JPEG फ़ाइल दें जिसे आप विश्लेषण करना चाहते हैं। लाइब्रेरी `File` या `BufferedImage` को स्वीकार करती है; हम सरलता के लिए `File` का उपयोग करेंगे।

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Pro tip:**  
यदि आपकी इमेज रिसोर्सेज में रहती है (जैसे, किसी JAR के अंदर), तो `getResourceAsStream` का उपयोग करें और इसे `ImageIO.read` से रैप करें। इस तरह ट्यूटोरियल स्थानीय रूप से और पैकेज्ड ऐप दोनों में काम करेगा।

## OCR पहचान करें

अब हम वास्तव में इंजन को चित्र पढ़ने के लिए कहते हैं। परिणाम एक साधारण‑टेक्स्ट स्ट्रिंग होगा, लेकिन हम प्रत्येक लाइन के लिए **ocr confidence score** और **ocr bounding box** भी चाहते हैं।

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**क्यों हम `doOCR` की बजाय `getWords` का उपयोग करते हैं:**  
`doOCR` आपको कच्ची स्ट्रिंग देता है लेकिन स्थानिक जानकारी को हटा देता है। `RIL_WORD` (या यदि आप लाइन‑लेवल बॉक्स चाहते हैं तो `RIL_TEXTLINE`) के साथ `getWords` कॉल करने से हमें `Word` ऑब्जेक्ट्स की एक सूची मिलती है, जिनमें प्रत्येक में टेक्स्ट, कॉन्फिडेंस, और बाउंडिंग रेक्टेंगल होता है। यही **ocr bounding box** फीचर का मूल है।

## आउटपुट को समझना

ऊपर दिया गया स्निपेट एक साफ़ JPEG पर चलाने से आपको इस तरह का आउटपुट मिलेगा:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – पहचाने गए अक्षर।  
- **Confidence** – 0 और 1 के बीच का फ्लोटिंग‑पॉइंट मान; अधिक होने पर इंजन अधिक निश्चित होता है।  
- **Box** – वह आयत जो शब्द को पिक्सेल निर्देशांक (x, y, width, height) में घेरता है।  

अब आप **read text from image** कर सकते हैं और साथ ही ठीक‑ठीक जान सकते हैं कि प्रत्येक स्निपेट कैनवास पर कहाँ स्थित है—हाइलाइटिंग, क्रॉपिंग, या डाउनस्ट्रीम NLP पाइपलाइन में फीड करने के लिए परफेक्ट।

## किनारे के मामलों और सामान्य समस्याएँ

| स्थिति | ध्यान देने योग्य बात | समाधान / कार्य‑विधि |
|-----------|-------------------|-------------------|
| इमेज धुंधली या कम‑कॉन्ट्रास्ट वाली है | कॉन्फिडेंस स्कोर बहुत गिर जाता है (अक्सर 0.6 से नीचे)। | OpenCV से प्री‑प्रोसेस करें: कॉन्ट्रास्ट बढ़ाएँ, थ्रेशहोल्ड लागू करें। |
| JPEG में घुमा हुआ टेक्स्ट है | बाउंडिंग बॉक्स विकृत या गायब दिखते हैं। | `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` का उपयोग करके Tesseract को ऑरिएंटेशन ऑटो‑डिटेक्ट करने दें। |
| बड़े इमेज से OutOfMemoryError आता है | बड़े चित्र लोड करने पर Java हीप भर जाता है। | OCR से पहले इमेज को डाउनस्केल करें (`ImageIO.read` → `BufferedImage.getScaledInstance`)। |
| आपको शब्द‑लेवल के बजाय लाइन‑लेवल बॉक्स चाहिए | `RIL_WORD` शब्द‑लेवल बॉक्स देता है। | `ITesseract.PageIteratorLevel.RIL_TEXTLINE` पर स्विच करें। |
| गैर‑अंग्रेज़ी अक्षर � के रूप में दिखते हैं | भाषा डेटा लोड नहीं हुआ। | उपयुक्त `.traineddata` फ़ाइल डाउनलोड करें और `setDatapath` को उसकी फ़ोल्डर की ओर इंगित करें। |

इन समस्याओं को शुरुआती चरण में हल करने से बाद में घंटों की डिबगिंग बचती है।

## पूर्ण कार्यशील उदाहरण (सभी चरण एक फ़ाइल में)

नीचे एक स्व-निहित जावा क्लास है जिसे आप `src/main/java` फ़ोल्डर में कॉपी‑पेस्ट करके `mvn exec:java` के साथ चला सकते हैं। यह हमने जो कुछ भी चर्चा की, उसे एक साथ लाता है।

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स निकटता से संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [जावा में Aspose.OCR डिटेक्ट एरिया मोड के साथ इमेज से टेक्स्ट निकालें](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [इमेज से टेक्स्ट निकालें – जावा के लिए Aspose.OCR के साथ OCR मूल बातें](/ocr/english/java/ocr-basics/)
- [Aspose.OCR का उपयोग करके भाषा के साथ इमेज टेक्स्ट को OCR कैसे करें](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}