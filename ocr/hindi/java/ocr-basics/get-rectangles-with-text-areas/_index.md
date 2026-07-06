---
date: 2026-06-19
description: जाने कैसे जावा में इमेज को टेक्स्ट में बदलें, इमेज से पैराग्राफ निकालें,
  और Aspose OCR Java लाइब्रेरी का उपयोग करके टेक्स्ट एरिया रेक्टैंगल्स प्राप्त करें।
keywords:
- image to text java
- convert scanned image text
- extract paragraphs from image
- aspose ocr java tutorial
linktitle: Image to Text Java – इमेज से टेक्स्ट पहचानें और टेक्स्ट एरिया रेक्टैंगल्स
  प्राप्त करें
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  headline: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  type: TechArticle
- description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  name: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (or add to an existing one) and place the Aspose.OCR
      JAR on the classpath. If you use Maven, add the dependency as described in the
      download package.
  - name: Define Document Directory and Image Path
    text: 'Specify where your sample image resides:'
  - name: Create AsposeOCR Instance
    text: '`AsposeOCR` is the main class that provides OCR functionality. Instantiate
      the OCR engine:'
  - name: Recognize Text in the Image
    text: Load your image and call `RecognizePage` to convert the picture into plain
      text. This single method call performs image preprocessing, character segmentation,
      and language‑specific recognition in one step.
  - name: Get Rectangles with Text Areas
    text: Retrieve the bounding rectangles for each paragraph (or other area types).
      This step returns a collection of `Rectangle` objects that precisely enclose
      the detected text blocks, enabling you to highlight or further process individual
      sections. CODE_BLOCK_PLACEHOLDER_5_END
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR works with Java 11 and later versions.
    question: Is Aspose.OCR compatible with Java 11?
  - answer: Yes, you can use it in any type of project. For licensing details, visit
      [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for both personal and commercial projects?
  - answer: You can obtain a temporary license [here](https://purchase.aspose.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: For support and discussions, visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).
    question: Where can I find community support or official assistance?
  - answer: Yes, the library is thread‑safe and can be used in concurrent environments
      for better performance.
    question: Does Aspose.OCR support multithreading?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Image to Text Java – इमेज को टेक्स्ट में बदलें और टेक्स्ट एरिया रेक्टैंगल्स
  प्राप्त करें
url: /hi/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज को टेक्स्ट में बदलें जावा – इमेज को टेक्स्ट में बदलें और टेक्स्ट एरिया रेक्टेंगल प्राप्त करें

## परिचय

यदि आपको जावा एप्लिकेशन में **इमेज को टेक्स्ट में बदलने** की आवश्यकता है, तो Aspose.OCR for Java तेज़ और सटीक समाधान प्रदान करता है। इस ट्यूटोरियल में हम उन सटीक चरणों को देखेंगे जो इमेज से पैराग्राफ निकालने, प्रत्येक टेक्स्ट एरिया के बाउंडिंग रेक्टेंगल प्राप्त करने, और उन कॉर्डिनेट्स को कंसोल पर प्रिंट करने के लिए आवश्यक हैं। अंत तक आप समझेंगे कि यह तरीका क्यों काम करता है, लाइब्रेरी को कैसे इंटीग्रेट करें, और अपने उपयोग‑केस के लिए इसे कहाँ विस्तारित किया जा सकता है।

## त्वरित उत्तर
`AreasType` एक enumeration है जो टेक्स्ट विभाजन के स्तर (शब्द, पंक्तियाँ, पैराग्राफ) को निर्दिष्ट करता है।

- **“इमेज से टेक्स्ट को पहचानना” का क्या अर्थ है?** इसका मतलब है चित्र में दृश्य अक्षरों को संपादन योग्य स्ट्रिंग डेटा में बदलना।  
- **जावा में इसे कौन सी लाइब्रेरी संभालती है?** Aspose.OCR for Java।  
- **क्या विकास के लिए लाइसेंस चाहिए?** परीक्षण के लिए एक अस्थायी लाइसेंस उपलब्ध है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **क्या मैं एकल शब्दों के बजाय पैराग्राफ निकाल सकता हूँ?** हाँ – पैराग्राफ‑लेवल रेक्टेंगल प्राप्त करने के लिए `AreasType.PARAGRAPHS` का उपयोग करें।  
- **क्या कोड Java 11+ के साथ संगत है?** बिल्कुल, API Java 11 और उसके बाद के संस्करणों के साथ काम करता है।

## Aspose.OCR में “इमेज को टेक्स्ट में बदलें” क्या है?

`convert image to text` प्रक्रिया बिटमैप का विश्लेषण करने, OCR एल्गोरिदम लागू करने, और पहचाने गए अक्षरों को स्ट्रिंग के रूप में लौटाने को दर्शाती है। Aspose.OCR की `RecognizePage` मेथड इस परिवर्तन को करता है और वैकल्पिक रूप से प्रत्येक पहचाने गए टेक्स्ट ब्लॉक के सटीक `Rectangle` कॉर्डिनेट्स भी प्रदान करता है।

## क्यों उपयोग करें यह **java ocr library**?

Aspose.OCR **30+ भाषाओं** का समर्थन करता है और **50 MB** तक की इमेज को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस कर सकता है, जिससे सामान्य सर्वर हार्डवेयर पर सब‑सेकंड प्रतिक्रिया समय मिलता है। लाइब्रेरी थ्रेड‑सेफ़ है, केवल एक JAR की आवश्यकता होती है, और लचीले आउटपुट फ़ॉर्मेट—कच्चा टेक्स्ट, HTML, और सटीक टेक्स्ट‑एरिया रेक्टेंगल—प्रदान करती है, जिससे यह उच्च‑थ्रूपुट एंटरप्राइज़ परिदृश्यों के लिए आदर्श बनती है।

## आवश्यकताएँ

- **Java Development Kit** (JDK 11 या नया) आपके मशीन पर स्थापित होना चाहिए।  
- **Aspose.OCR for Java** लाइब्रेरी – आधिकारिक साइट से [यहाँ](https://releases.aspose.com/ocr/java/) डाउनलोड करें।  
- JAR डिपेंडेंसी को मैनेज करने के लिए एक IDE या बिल्ड टूल (Maven/Gradle)।

## पैकेज आयात करें

अपने जावा प्रोजेक्ट में आवश्यक क्लासेस आयात करें:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## चरण‑दर‑चरण मार्गदर्शिका

### चरण 1: अपना प्रोजेक्ट सेट अप करें
एक नया जावा प्रोजेक्ट बनाएं (या मौजूदा में जोड़ें) और Aspose.OCR JAR को क्लासपाथ पर रखें। यदि आप Maven उपयोग करते हैं, तो डाउनलोड पैकेज में वर्णित डिपेंडेंसी जोड़ें।

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### चरण 2: दस्तावेज़ डायरेक्टरी और इमेज पाथ निर्धारित करें
अपने सैंपल इमेज का स्थान निर्दिष्ट करें:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### चरण 3: AsposeOCR इंस्टेंस बनाएं
`AsposeOCR` मुख्य क्लास है जो OCR कार्यक्षमता प्रदान करता है।

OCR इंजन को इंस्टैंशिएट करें:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### चरण 4: इमेज में टेक्स्ट को पहचानें
अपनी इमेज लोड करें और `RecognizePage` को कॉल करके चित्र को साधारण टेक्स्ट में बदलें। यह एकल मेथड कॉल इमेज प्री‑प्रोसेसिंग, कैरेक्टर सेगमेंटेशन, और भाषा‑विशिष्ट पहचान को एक साथ करता है।

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

### चरण 5: टेक्स्ट एरिया के साथ रेक्टेंगल प्राप्त करें
प्रत्येक पैराग्राफ (या अन्य एरिया टाइप) के बाउंडिंग रेक्टेंगल प्राप्त करें। यह चरण `Rectangle` ऑब्जेक्ट्स का संग्रह लौटाता है जो पहचाने गए टेक्स्ट ब्लॉक्स को सटीक रूप से घेरते हैं, जिससे आप व्यक्तिगत सेक्शन को हाइलाइट या आगे प्रोसेस कर सकते हैं।

CODE_BLOCK_PLACEHOLDER_5_END

## सामान्य समस्याएँ और ट्रबलशूटिंग

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| `IOException` on `RecognizePage` | गलत फ़ाइल पाथ या पढ़ने की अनुमति नहीं है | सुनिश्चित करें कि `imagePath` मौजूदा PNG/JPG की ओर इशारा कर रहा है और एप्लिकेशन को फ़ाइल सिस्टम एक्सेस है। |
| Empty result string | कम गुणवत्ता वाली इमेज या असमर्थित भाषा | इमेज को प्री‑प्रोसेस करें (कॉन्ट्रास्ट बढ़ाएँ, बाइनराइज़ करें) या `api.setLanguage("eng")` के साथ सही भाषा निर्दिष्ट करें। |
| No rectangles returned | गलत `AreasType` उपयोग (जैसे, पैराग्राफ की अपेक्षा `WORDS` उपयोग) | आवश्यकता अनुसार `AreasType.PARAGRAPHS` या `AreasType.LINES` में बदलें। |

## अक्सर पूछे जाने वाले प्रश्न

**Q:** क्या Aspose.OCR जावा 11 के साथ संगत है?  
**A:** हाँ, Aspose.OCR जावा 11 और बाद के संस्करणों के साथ काम करता है।

**Q:** क्या मैं Aspose.OCR को व्यक्तिगत और व्यावसायिक दोनों प्रोजेक्ट्स में उपयोग कर सकता हूँ?  
**A:** हाँ, आप इसे किसी भी प्रकार के प्रोजेक्ट में उपयोग कर सकते हैं। लाइसेंस विवरण के लिए [यहाँ](https://purchase.aspose.com/buy) देखें।

**Q:** मूल्यांकन के लिए अस्थायी लाइसेंस कैसे प्राप्त करें?  
**A:** आप अस्थायी लाइसेंस [यहाँ](https://purchase.aspose.com/temporary-license/) प्राप्त कर सकते हैं।

**Q:** समुदाय समर्थन या आधिकारिक सहायता कहाँ मिल सकती है?  
**A:** समर्थन और चर्चा के लिए [Aspose.OCR फोरम](https://forum.aspose.com/c/ocr/16) देखें।

**Q:** क्या Aspose.OCR मल्टीथ्रेडिंग का समर्थन करता है?  
**A:** हाँ, लाइब्रेरी थ्रेड‑सेफ़ है और बेहतर प्रदर्शन के लिए समवर्ती वातावरण में उपयोग की जा सकती है।

## निष्कर्ष

इस **aspose ocr java tutorial** में आपने Aspose.OCR for Java का उपयोग करके **इमेज को टेक्स्ट में बदलने**, पैराग्राफ निकालने, और प्रत्येक टेक्स्ट ब्लॉक को घेरने वाले सटीक रेक्टेंगल प्राप्त करने का तरीका सीखा। ये क्षमताएँ आपको सर्चेबल PDF बनाने, UI ओवरले में टेक्स्ट हाइलाइट करने, या संरचित डेटा को डाउनस्ट्रीम प्रोसेस में फीड करने में मदद करती हैं। API को और अनुकूलित करने के लिए भाषा सेटिंग्स, विभिन्न इमेज फ़ॉर्मेट, या क्लाउड स्टोरेज इंटीग्रेशन का अन्वेषण करें।

---

**अंतिम अपडेट:** 2026-06-19  
**परीक्षित संस्करण:** Aspose.OCR 23.10 for Java  
**लेखक:** Aspose  

{{< blocks/products/products-backtop-button >}}

## संबंधित ट्यूटोरियल

- [इमेज से टेक्स्ट निकालें – Aspose.OCR for Java के साथ OCR बुनियादी](/ocr/java/ocr-basics/)
- [इमेज जावा से टेक्स्ट निकालें Aspose.OCR डिटेक्ट एरिया मोड के साथ](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [जावा में इमेज को टेक्स्ट में बदलें Aspose.OCR BufferedImage का उपयोग करके](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}