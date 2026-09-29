---
date: 2026-02-09
description: Aspose OCR Java लाइब्रेरी का उपयोग करके छवि को टेक्स्ट में बदलना और टेक्स्ट
  एरिया आयतों को निकालना सीखें। कोड उदाहरणों के साथ चरण‑दर‑चरण गाइड।
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: छवि को पाठ में बदलें – छवि से पाठ पहचानें और पाठ क्षेत्र के आयताकार क्षेत्रों
  को प्राप्त करें
url: /hi/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज को टेक्स्ट में बदलें – इमेज से टेक्स्ट पहचानें और टेक्स्ट एरिया के आयताकार प्राप्त करें

## परिचय

यदि आपको **इमेज को टेक्स्ट में बदलने** और **इमेज से टेक्स्ट पहचानने** की आवश्यकता है किसी Java एप्लिकेशन में, तो Aspose.OCR for Java एक तेज़, सटीक तरीका प्रदान करता है। इस ट्यूटोरियल में हम उन सटीक चरणों को देखेंगे जो इमेज से पैराग्राफ निकालने, प्रत्येक टेक्स्ट एरिया के बाउंडिंग आयताकार प्राप्त करने, और उन निर्देशांक को कंसोल में प्रिंट करने के लिए आवश्यक हैं। अंत तक आप समझेंगे कि यह तरीका क्यों काम करता है, लाइब्रेरी को कैसे इंटीग्रेट करें, और अपने उपयोग‑केस के लिए इसे कहाँ विस्तारित कर सकते हैं।

## त्वरित उत्तर
- **“इमेज से टेक्स्ट पहचानना” का क्या मतलब है?** इसका अर्थ है चित्र में मौजूद दृश्य अक्षरों को संपादन योग्य स्ट्रिंग डेटा में बदलना।  
- **Java में यह कौन सी लाइब्रेरी संभालती है?** Aspose.OCR for Java।  
- **क्या विकास के लिए लाइसेंस चाहिए?** परीक्षण के लिए एक अस्थायी लाइसेंस उपलब्ध है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **क्या मैं एकल शब्दों के बजाय पैराग्राफ निकाल सकता हूँ?** हाँ – `AreasType.PARAGRAPHS` का उपयोग करके पैराग्राफ‑स्तर के आयताकार प्राप्त करें।  
- **क्या कोड Java 11+ के साथ संगत है?** बिल्कुल, API Java 11 और बाद के संस्करणों के साथ काम करता है।

## Aspose.OCR में “इमेज को टेक्स्ट में बदलना” क्या है?
Aspose.OCR की `RecognizePage` मेथड बिटमैप का विश्लेषण करती है, OCR एल्गोरिदम लागू करती है, और पहचाना गया स्ट्रिंग लौटाती है। जब आप टेक्स्ट एरिया का अनुरोध करते हैं, तो लाइब्रेरी प्रत्येक टेक्स्ट ब्लॉक के सटीक `Rectangle` निर्देशांक भी गणना करती है, जिससे बाद में विशिष्ट सेक्शन को हाइलाइट या प्रोसेस करना आसान हो जाता है।

## इस **java ocr library** का उपयोग क्यों करें?
- **उच्च सटीकता** – कई भाषाओं और जटिल फ़ॉन्ट्स को सपोर्ट करता है।  
- **आसान इंटीग्रेशन** – एक ही JAR पूरी OCR क्षमता जोड़ता है।  
- **लचीला आउटपुट** – आप कच्चा टेक्स्ट, फॉर्मेटेड HTML, या सटीक टेक्स्ट‑एरिया आयताकार प्राप्त कर सकते हैं।  
- **थ्रेड‑सेफ़** – उच्च‑थ्रूपुट सर्वर वातावरण के लिए उपयुक्त।

## पूर्वापेक्षाएँ

- **Java Development Kit** (JDK 11 या नया) आपके मशीन पर स्थापित होना चाहिए।  
- **Aspose.OCR for Java** लाइब्रेरी – इसे आधिकारिक साइट से डाउनलोड करें [here](https://releases.aspose.com/ocr/java/)।  
- JAR डिपेंडेंसी को मैनेज करने के लिए कोई IDE या बिल्ड टूल (Maven/Gradle)।

## पैकेज इम्पोर्ट करें

अपने Java प्रोजेक्ट में आवश्यक क्लासेस इम्पोर्ट करें:

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

## चरण‑दर‑चरण गाइड

### चरण 1: अपना प्रोजेक्ट सेट अप करें
एक नया Java प्रोजेक्ट बनाएं (या मौजूदा में जोड़ें) और Aspose.OCR JAR को क्लासपाथ पर रखें। यदि आप Maven उपयोग करते हैं, तो डाउनलोड पैकेज में वर्णित डिपेंडेंसी जोड़ें।

### चरण 2: डॉक्यूमेंट डायरेक्टरी और इमेज पाथ निर्धारित करें
अपनी सैंपल इमेज जहाँ स्थित है, उसे निर्दिष्ट करें:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### चरण 3: Aspose.OCR इंस्टेंस बनाएं
OCR इंजन को इंस्टैंशिएट करें:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### चरण 4: इमेज में टेक्स्ट पहचानें
`RecognizePage` को कॉल करके चित्र को साधारण टेक्स्ट में बदलें। यह चरण मुख्य **recognize text image java** क्षमता को दर्शाता है:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### चरण 5: टेक्स्ट एरिया के आयताकार प्राप्त करें
अब प्रत्येक पैराग्राफ (या अन्य एरिया टाइप) के बाउंडिंग आयताकार प्राप्त करें। यही वह जगह है जहाँ आप **extract paragraphs from image** करते हैं और उनके निर्देशांक प्राप्त करते हैं:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## सामान्य समस्याएँ एवं ट्रबलशूटिंग

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| `IOException` on `RecognizePage` | फ़ाइल पाथ गलत या पढ़ने की अनुमति नहीं है | सुनिश्चित करें `imagePath` एक मौजूदा PNG/JPG की ओर इशारा करता है और एप्लिकेशन को फ़ाइल सिस्टम एक्सेस है। |
| खाली परिणाम स्ट्रिंग | कम‑गुणवत्ता वाली इमेज या असमर्थित भाषा | इमेज को प्री‑प्रोसेस करें (कॉन्ट्रास्ट बढ़ाएँ, बाइनराइज़ करें) या `api.setLanguage("eng")` के साथ सही भाषा निर्दिष्ट करें। |
| कोई आयताकार नहीं मिला | गलत `AreasType` उपयोग किया (जैसे, पैराग्राफ की अपेक्षा `WORDS`) | आवश्यकता अनुसार `AreasType.PARAGRAPHS` या `AreasType.LINES` में बदलें। |

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या Aspose.OCR Java 11 के साथ संगत है?**  
A: हाँ, Aspose.OCR Java 11 और बाद के संस्करणों के साथ काम करता है।

**Q: क्या मैं Aspose.OCR को व्यक्तिगत और व्यावसायिक दोनों प्रोजेक्ट्स में उपयोग कर सकता हूँ?**  
A: हाँ, आप इसे किसी भी प्रकार के प्रोजेक्ट में उपयोग कर सकते हैं। लाइसेंस विवरण के लिए देखें [here](https://purchase.aspose.com/buy)।

**Q: मूल्यांकन के लिए अस्थायी लाइसेंस कैसे प्राप्त करूँ?**  
A: आप अस्थायी लाइसेंस यहाँ से प्राप्त कर सकते हैं [here](https://purchase.aspose.com/temporary-license/)।

**Q: समुदाय समर्थन या आधिकारिक सहायता कहाँ मिल सकती है?**  
A: समर्थन और चर्चा के लिए देखें [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)।

**Q: क्या Aspose.OCR मल्टीथ्रेडिंग को सपोर्ट करता है?**  
A: हाँ, लाइब्रेरी थ्रेड‑सेफ़ है और बेहतर प्रदर्शन के लिए समवर्ती वातावरण में उपयोग की जा सकती है।

## निष्कर्ष

इस **aspose ocr java tutorial** में आपने सीखा कि कैसे Aspose.OCR for Java का उपयोग करके **इमेज को टेक्स्ट में बदलें**, पैराग्राफ निकालें, और प्रत्येक टेक्स्ट ब्लॉक को घेरने वाले सटीक आयताकार प्राप्त करें। ये क्षमताएँ आपको सर्चेबल PDFs बनाने, UI ओवरले में टेक्स्ट हाइलाइट करने, या संरचित डेटा को डाउनस्ट्रीम प्रोसेस में फीड करने में मदद करती हैं। API को आगे अनुकूलित करके भाषा सेटिंग्स बदलें, विभिन्न इमेज फ़ॉर्मैट संभालें, या क्लाउड स्टोरेज के साथ इंटीग्रेट करें।

---

**Last Updated:** 2026-02-09  
**Tested With:** Aspose.OCR 23.10 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}