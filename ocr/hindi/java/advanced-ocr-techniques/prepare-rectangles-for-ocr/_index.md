---
date: 2025-12-06
description: Aspose.OCR for Java का उपयोग करके OCR टेक्स्ट पहचान कैसे करें, छवियों
  से टेक्स्ट निकालें, और लक्षित पहचान के लिए आयतें तैयार करें, सीखें।
language: hi
linktitle: Preparing Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspose.OCR में OCR टेक्स्ट पहचान के लिए आयतों की तैयारी
url: /java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR टेक्स्ट रिकग्निशन के लिए रेक्टेंगल तैयार करना Aspose.OCR में

## परिचय

आज के डेटा‑ड्रिवेन विश्व में, **ocr text recognition** स्कैन किए गए दस्तावेज़ों, स्क्रीनशॉट्स और फ़ोटो को सर्चेबल, एडिटेबल कंटेंट में बदलने का मुख्य आधार है। Aspose.OCR for Java इस प्रक्रिया को तेज़ और भरोसेमंद बनाता है, ख़ासकर जब आपको इमेज के विशिष्ट क्षेत्रों पर ध्यान केंद्रित करना हो। इस ट्यूटोरियल में हम हर वह कदम देखेंगे जो रेक्टेंगल तैयार करने के लिए आवश्यक हैं, जिससे OCR केवल उन क्षेत्रों तक सीमित रहे जिनमें आपको रुचि है, और आपको सटीक नियंत्रण तथा बेहतर प्रदर्शन मिलेगा।

## त्वरित उत्तर
- **Java में OCR टेक्स्ट रिकग्निशन कौन सी लाइब्रेरी संभालती है?** Aspose.OCR for Java।  
- **प्रोडक्शन उपयोग के लिए लाइसेंस चाहिए?** हाँ – एक वैध Aspose.OCR लाइसेंस पूरी कार्यक्षमता अनलॉक करता है।  
- **क्या मैं OCR को इमेज के कुछ हिस्सों तक सीमित कर सकता हूँ?** बिल्कुल; आप रेक्टेंगल परिभाषित करके लक्ष्य ज़ोन को बाउंड कर सकते हैं।  
- **मुख्य प्री‑रिक्विज़िट्स क्या हैं?** JDK 17+, Aspose.OCR for Java, और एक Java IDE।  
- **क्या यह तरीका इमेज से टेक्स्ट निकालने के लिए उपयुक्त है?** हाँ, यह **extract text image java** प्रोजेक्ट्स के लिए एक प्रभावी तरीका है।

## OCR टेक्स्ट रिकग्निशन क्या है?
OCR (Optical Character Recognition) टेक्स्ट रिकग्निशन पिक्सेल‑आधारित इमेज को मशीन‑रीडेबल कैरेक्टर्स में बदलता है। यह आपको ऐसी सामग्री को सर्च, एडिट और एनालाइज़ करने देता है जो मूल रूप से केवल तस्वीरों के रूप में मौजूद थी।

## OCR टेक्स्ट रिकग्निशन के लिए रेक्टेंगल क्यों तैयार करें?
रेक्टेंगल परिभाषित करने से इंजन उन क्षेत्रों पर फोकस करता है जहाँ वास्तव में टेक्स्ट है, जिससे:
* प्रोसेसिंग टाइम कम होता है।
* शोरयुक्त बैकग्राउंड को नजरअंदाज़ करके सटीकता बढ़ती है।
* आप केवल वही डेटा निकाल सकते हैं जिसकी आपको ज़रूरत है—फ़ॉर्म, इनवॉइस और रसीदों के लिए परफ़ेक्ट।

## प्री‑रिक्विज़िट्स

शुरू करने से पहले सुनिश्चित करें कि आपके पास हैं:

- **Java Development Kit (JDK)** – Aspose.OCR for Java JDK 17 या बाद के संस्करण के साथ काम करता है। इसे Oracle की वेबसाइट से डाउनलोड करें।
- **Aspose.OCR for Java लाइब्रेरी** – आधिकारिक डाउनलोड पेज से नवीनतम JAR प्राप्त करें [here](https://releases.aspose.com/ocr/java/)। इंस्टॉलेशन गाइड यहाँ देखें [here](https://reference.aspose.com/ocr/java/)।
- **डेवलपमेंट एनवायरनमेंट** – कोई भी Java IDE (IntelliJ IDEA, Eclipse, VS Code, आदि) चलेगा।

## पैकेज इम्पोर्ट करें

अपने Java सोर्स फ़ाइल में आवश्यक Aspose.OCR क्लासेज़ और स्टैंडर्ड Java यूटिलिटीज़ इम्पोर्ट करें:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *हम `java.awt.Rectangle` इम्पोर्ट करते हैं क्योंकि OCR API उन रेक्टेंगल की अपेक्षा करता है जो स्कैन करने वाले क्षेत्रों को परिभाषित करते हैं।*

## चरण 1: लाइसेंस सेट अप करें

```java
SetLicense.main(null);
```

`SetLicense` को कॉल करने से आपका Aspose.OCR लाइसेंस एक्टिवेट हो जाता है, मूल्यांकन सीमाएँ हटती हैं और पूर्ण‑फ़ीचर OCR टेक्स्ट रिकग्निशन सक्षम हो जाता है।

## चरण 2: डॉक्यूमेंट डायरेक्टरी और इमेज पाथ निर्धारित करें

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

`"Your Document Directory"` को उस एब्सोल्यूट पाथ से बदलें जहाँ आपकी इमेज (`p.png`) स्थित है। यही इमेज प्रोसेस की जाएगी।

## चरण 3: Aspose.OCR इंस्टेंस बनाएं

```java
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` को इंस्टैंशिएट करने से आपको `RecognizePage` मेथड तक पहुंच मिलती है, जो वास्तविक OCR करता है।

## चरण 4: टेक्स्ट के साथ रेक्टेंगल तैयार करें

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

हर `Rectangle(x, y, width, height)` Aspose.OCR को ठीक‑ठीक बताता है कि टेक्स्ट कहाँ देखना है। अपने स्रोत इमेज के लेआउट के अनुसार कॉर्डिनेट्स समायोजित करें।

## चरण 5: OCR रिकग्निशन चलाएँ

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` कॉल केवल परिभाषित रेक्टेंगल को प्रोसेस करता है और निकाले गए स्ट्रिंग को रिटर्न करता है। कंसोल आउटपुट आपको **ocr text recognition** परिणाम तुरंत वेरिफ़ाई करने देता है।

## सामान्य समस्याएँ और टिप्स

| Issue | Cause | Solution |
|-------|-------|----------|
| **No output** | Incorrect rectangle coordinates or image path | `dataDir` वैल्यू को दोबारा चेक करें और सुनिश्चित करें कि रेक्टेंगल वास्तव में टेक्स्ट क्षेत्रों को कवर करते हैं। |
| **Garbage characters** | Low‑resolution image or unsupported font | उच्च‑रिज़ॉल्यूशन स्रोत उपयोग करें या इमेज प्री‑प्रोसेसिंग (जैसे बाइनराइज़ेशन) लागू करें। |
| **License not applied** | `SetLicense` not called before OCR | सुनिश्चित करें कि `SetLicense.main(null);` किसी भी API कॉल से पहले चलाया गया हो। |
| **Performance lag** | Too many large rectangles | रेक्टेंगल की संख्या सीमित रखें और उन्हें टेक्स्ट के आसपास जितना संभव हो टाइट रखें। |

## निष्कर्ष

आपने अब सीखा कि Aspose.OCR for Java को कैसे इंटीग्रेट करें, लाइसेंस सेट अप करें, इमेज पाथ निर्धारित करें, और सबसे महत्वपूर्ण बात—रेक्टेंगल तैयार करके **ocr text recognition** को इमेज के विशिष्ट भागों पर फोकस करें। यह तकनीक किसी भी **java ocr tutorial** के लिए आदर्श है जो सटीक, हाई‑परफ़ॉर्मेंस टेक्स्ट एक्सट्रैक्शन चाहता है।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या Aspose.OCR अन्य प्रोग्रामिंग भाषाओं के साथ संगत है?**  
A: हाँ, Aspose.OCR .NET, C++, और Python को भी सपोर्ट करता है। भाषा‑विशिष्ट सैंपल्स के लिए आधिकारिक डॉक्यूमेंटेशन देखें।

**Q: क्या मैं Aspose.OCR को कमर्शियल प्रोजेक्ट में उपयोग कर सकता हूँ?**  
A: बिल्कुल। आप [Aspose स्टोर](https://purchase.aspose.com/buy) से कमर्शियल लाइसेंस खरीद सकते हैं।

**Q: क्या कोई फ्री ट्रायल उपलब्ध है?**  
A: हाँ, आप ट्रायल वर्ज़न यहाँ से डाउनलोड कर सकते हैं [here](https://releases.aspose.com/)।

**Q: मूल्यांकन के लिए टेम्पररी लाइसेंस कैसे प्राप्त करें?**  
A: टेम्पररी लाइसेंस [Aspose टेम्पररी‑लाइसेंस पोर्टल](https://purchase.aspose.com/temporary-license/) से मिलते हैं।

**Q: कम्युनिटी सपोर्ट कहाँ मिल सकता है?**  
A: प्रश्न, टिप्स और कोड सैंपल्स के लिए Aspose.OCR [फ़ोरम](https://forum.aspose.com/c/ocr/16) देखें।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.OCR for Java 24.12  
**Author:** Aspose  

---