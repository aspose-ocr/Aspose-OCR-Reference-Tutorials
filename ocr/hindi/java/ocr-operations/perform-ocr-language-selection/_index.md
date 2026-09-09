---
date: 2026-02-12
description: Aspose.OCR for Java का उपयोग करके भाषा चयन के साथ इमेज टेक्स्ट को OCR
  करने का तरीका सीखें। यह चरण‑दर‑चरण गाइड जावा में टेक्स्ट निकालना, OCR स्क्यू सुधार
  और अधिक को कवर करता है।
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspose.OCR का उपयोग करके भाषा के साथ इमेज टेक्स्ट को OCR कैसे करें
url: /hi/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR का उपयोग करके भाषा के साथ इमेज टेक्स्ट को OCR करने का तरीका

## परिचय

इमेज फ़ाइलों से टेक्स्ट निकालना एक सामान्य आवश्यकता है, चाहे आप स्कैन किए गए दस्तावेज़ों को डिजिटल बना रहे हों, रसीदों को प्रोसेस कर रहे हों, या खोज योग्य अभिलेख बनाते हों। इस ट्यूटोरियल में हम एक पूर्ण, हैंड‑ऑन उदाहरण के माध्यम से दिखाएंगे **इमेज टेक्स्ट को OCR करने का तरीका** एक विशिष्ट भाषा सेटिंग के साथ, ताकि आप आज ही अपने Java एप्लिकेशन में विश्वसनीय OCR को इंटीग्रेट कर सकें। आप यह भी देखेंगे कि OCR स्क्यू सुधार और क्षेत्र‑आधारित पहचान को कैसे संभालें ताकि सटीकता अधिकतम हो सके।

## त्वरित उत्तर
- **जावा में OCR को संभालने वाली लाइब्रेरी कौन सी है?** Aspose.OCR for Java  
- **कौन सा सेटिंग भाषा चुनता है?** `settings.setLanguage(Language.Eng)` (या कोई भी समर्थित भाषा)  
- **क्या विकास के लिए लाइसेंस चाहिए?** परीक्षण के लिए एक मुफ्त मूल्यांकन लाइसेंस काम करता है; उत्पादन के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **क्या मैं OCR को इमेज के किसी क्षेत्र तक सीमित कर सकता हूँ?** हाँ, आयतों के साथ `RecognitionSettings.setRecognitionAreas()` का उपयोग करें।  
- **सामान्य रनटाइम क्या है?** इमेज आकार और भाषा जटिलता के आधार पर, मानक लैपटॉप पर प्रति पृष्ठ कुछ सेकंड।

## भाषा चयन के साथ इमेज टेक्स्ट को OCR करने का तरीका
इस सेक्शन में हम मुख्य प्रश्न **इमेज को OCR कैसे करें** जब आपको टेक्स्ट की भाषा पता हो, का उत्तर देंगे। सही भाषा का चयन करने से पहचान की सटीकता में उल्लेखनीय सुधार होता है क्योंकि OCR इंजन भाषा‑विशिष्ट शब्दकोश और कैरेक्टर मॉडल लागू कर सकता है।

### यह क्यों महत्वपूर्ण है
- **उच्च सटीकता** – भाषा‑विशिष्ट मॉडल गलत पहचान को कम करते हैं।  
- **परफॉर्मेंस बूस्ट** – इंजन अनावश्यक भाषा जाँच को छोड़ देता है।  
- **डायाक्रिटिक का बेहतर हैंडलिंग** – फ्रेंच, स्पेनिश, जर्मन आदि को सही ढंग से पहचाना जाता है जब मिलते‑जुलते `Language` enum का उपयोग किया जाता है।

## “इमेज से टेक्स्ट निकालना” क्या है?
इमेज से टेक्स्ट (OCR) निकालना दृश्य अक्षरों को मशीन‑पढ़ने योग्य स्ट्रिंग्स में बदल देता है। यह खोज, विश्लेषण, और डेटा एक्सट्रैक्शन वर्कफ़्लो को सक्षम बनाता है, जो अन्यथा मैन्युअल ट्रांसक्रिप्शन की आवश्यकता होती।

## भाषा चयन के साथ Aspose.OCR क्यों उपयोग करें?
- **बहुभाषी समर्थन** – इमेज में मौजूद सटीक भाषा(यों) को चुनें और सटीकता बढ़ाएँ।  
- **सूक्ष्म नियंत्रण** – स्क्यू को समायोजित करें, पहचान क्षेत्रों को परिभाषित करें, और ऑटो‑स्क्यू व्यवहार सेट करें।  
- **शुद्ध Java API** – कोई नेटिव डिपेंडेंसी नहीं, किसी भी Java प्रोजेक्ट में आसानी से इंटीग्रेट करें।  
- **समृद्ध परिणाम डेटा** – एक कॉल में प्लेन टेक्स्ट, JSON, बाउंडिंग रेक्टेंगल, और वार्निंग्स प्राप्त करें।

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित हों:

- **Java Development Kit (JDK)** स्थापित हो (JDK 8 या बाद का)।  
- **Aspose.OCR for Java** लाइब्रेरी – इसे आधिकारिक साइट [here](https://reference.aspose.com/ocr/java/) से डाउनलोड करें।  
- एक इमेज फ़ाइल जिसमें वह टेक्स्ट हो जिसे आप निकालना चाहते हैं, जैसे `p3.png`।

## पैकेज आयात करें

अपने Java स्रोत फ़ाइल में आवश्यक Aspose.OCR क्लासेज़ और मानक Java यूटिलिटीज़ शामिल करें:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## चरण‑दर‑चरण मार्गदर्शिका

### चरण 1: अपना दस्तावेज़ डायरेक्टरी सेट करें

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

`"Your Document Directory"` को उस पूर्ण पाथ से बदलें जहाँ `p3.png` स्थित है।

### चरण 2: इमेज पाथ निर्धारित करें

```java
// The image path
String file = dataDir + "p3.png";
```

सुनिश्चित करें कि `file` वेरिएबल ठीक उसी इमेज की ओर इशारा कर रहा है जिसे आप प्रोसेस करना चाहते हैं।

### चरण 3: Aspose.OCR API इंस्टेंस बनाएं

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` ऑब्जेक्ट आपको सभी OCR ऑपरेशन्स तक पहुंच प्रदान करता है।

### चरण 4: मान्यता विकल्प सेट करें (भाषा चयन)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

यहाँ हम:

1. ऑटो‑स्क्यू को डिसेबल करते हैं क्योंकि हम मैन्युअल स्क्यू वैल्यू प्रदान करेंगे।  
2. एक आयताकार क्षेत्र (`RecognitionAreas`) परिभाषित करते हैं ताकि OCR केवल इमेज के उस भाग तक सीमित रहे जिसमें वास्तव में टेक्स्ट है।  
3. **भाषा** को अंग्रेज़ी (`Language.Eng`) सेट करते हैं। इसे `Language.Fra`, `Language.Spa` आदि में बदलें, आपके स्रोत इमेज के अनुसार।

### चरण 5: OCR चलाएँ और परिणाम प्राप्त करें

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` कॉल आपके द्वारा परिभाषित इमेज और सेटिंग्स के साथ OCR इंजन को चलाता है। परिणाम `RecognitionResult` ऑब्जेक्ट में संग्रहीत होता है।

### चरण 6: परिणाम प्रिंट करें और उपयोग करें

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

कंसोल आउटपुट दिखाता है:

- पूर्ण निकाला गया टेक्स्ट (`recognitionText`)।  
- प्रत्येक परिभाषित आयत के लिए टेक्स्ट (`recognitionAreasText`)।  
- बाउंडिंग रेक्टेंगल कॉर्डिनेट्स।  
- आसान डाउनस्ट्रीम प्रोसेसिंग के लिए JSON प्रतिनिधित्व।  
- पता लगाया गया स्क्यू एंगल और कोई भी वार्निंग्स।

अब आप `result.recognitionText` को अपने बिज़नेस लॉजिक में फीड कर सकते हैं—इसे स्टोर करें, इंडेक्स करें, या किसी अन्य सर्विस को पास करें।

## सामान्य समस्याएँ और समाधान

| समस्या | कारण | समाधान |
|-------|-------|-----|
| **गड़बड़ अक्षर** | गलत भाषा चयनित | सही `Language` enum सेट करें (उदा., फ्रेंच के लिए `Language.Fra`)। |
| **कोई टेक्स्ट नहीं मिला** | मान्यता क्षेत्र टेक्स्ट को कवर नहीं करता | `Rectangle` निर्देशांक समायोजित करें या पूरे इमेज को प्रोसेस करने के लिए `RecognitionAreas` हटाएँ। |
| **धीमी प्रदर्शन** | बहुत बड़ी इमेज या उच्च रेज़ोल्यूशन | OCR से पहले इमेज को छोटा करें या JVM के लिए मेमोरी आवंटन बढ़ाएँ। |
| **असमर्थित फ़ॉर्मेट के बारे में चेतावनी** | इमेज फ़ॉर्मेट पहचाना नहीं गया | प्रोसेस करने से पहले इमेज को PNG, JPEG, या TIFF में बदलें। |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या मैं एक ही OCR कॉल में कई भाषाओं को पहचान सकता हूँ?**  
**उत्तर:** हाँ। `settings.setLanguage(Language.Eng \| Language.Fra)` का उपयोग करके बहुभाषी पहचान सक्षम करें।

**प्रश्न: Aspose.OCR कौन से इमेज फ़ॉर्मेट सपोर्ट करता है?**  
**उत्तर:** PNG, JPEG, BMP, TIFF, GIF, और कई अन्य। केवल सही फ़ाइल पाथ प्रदान करें।

**प्रश्न: इमेज के लिए कोई आकार सीमा है?**  
**उत्तर:** कोई कठोर सीमा नहीं है, लेकिन बहुत बड़ी इमेजें मेमोरी उपयोग और प्रोसेसिंग समय बढ़ा देती हैं। बड़े फ़ाइलों को रीसाइज़ करने पर विचार करें।

**प्रश्न: मैं प्रोडक्शन लाइसेंस कैसे प्राप्त करूँ?**  
**उत्तर:** Aspose वेबसाइट से लाइसेंस खरीदें और Aspose दस्तावेज़ में दिखाए अनुसार `License` क्लास के माध्यम से लागू करें।

**प्रश्न: क्या मैं सीधे PDF पेज से टेक्स्ट निकाल सकता हूँ?**  
**उत्तर:** Aspose.OCR के साथ सीधे नहीं। पहले PDF पेज को इमेज में बदलें (उदा., Aspose.PDF का उपयोग करके) और फिर OCR चलाएँ।

## निष्कर्ष

आपने अब देखा कि **इमेज से टेक्स्ट निकालना** Aspose.OCR for Java का उपयोग करके कैसे किया जाता है, जबकि उपयुक्त भाषा का चयन किया गया और पहचान को विशिष्ट क्षेत्रों तक सीमित किया गया। यह तरीका सटीक, उच्च‑प्रदर्शन OCR प्रदान करता है जिसे किसी भी Java‑आधारित वर्कफ़्लो में एम्बेड किया जा सकता है—दस्तावेज़ प्रबंधन सिस्टम से लेकर डेटा‑कैप्चर पाइपलाइन तक। आगे बढ़ने के लिए तैयार हैं? भाषा enum को बदलें, विभिन्न पहचान क्षेत्रों के साथ प्रयोग करें, और परिणामों को अपने एप्लिकेशन लॉजिक में इंटीग्रेट करें।

---

**अंतिम अपडेट:** 2026-02-12  
**परीक्षित संस्करण:** Aspose.OCR 24.11 for Java  
**लेखक:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}