---
date: 2025-12-13
description: Aspose.OCR for Java का उपयोग करके भाषा चयन के साथ छवि से टेक्स्ट निकालना
  सीखें। यह चरण‑दर‑चरण Aspose OCR Java ट्यूटोरियल सटीक OCR कॉन्फ़िगरेशन दिखाता है।
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspose.OCR का उपयोग करके भाषा चयन के साथ छवि से टेक्स्ट निकालना
url: /hi/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR का उपयोग करके भाषा चयन के साथ इमेज से टेक्स्ट निकालने का तरीका

## परिचय

इमेज फ़ाइलों से टेक्स्ट निकालना एक सामान्य आवश्यकता है, चाहे आप स्कैन किए गए दस्तावेज़ों को डिजिटाइज़ कर रहे हों, रसीदों को प्रोसेस कर रहे हों, या खोज योग्य अभिलेख बनाते हों। Aspose.OCR for Java इस कार्य को सरल बनाता है और भाषा चयन, स्क्यू सुधार, और पहचान क्षेत्रों पर सूक्ष्म नियंत्रण प्रदान करता है। इस ट्यूटोरियल में हम एक पूर्ण, व्यावहारिक उदाहरण के माध्यम से दिखाएंगे **कैसे इमेज से टेक्स्ट निकाला जाए** एक विशिष्ट भाषा सेटिंग के साथ, ताकि आप अपने Java एप्लिकेशन में विश्वसनीय OCR को आज ही एकीकृत कर सकें।

## त्वरित उत्तर
- **Java में OCR को संभालने वाली लाइब्रेरी कौन सी है?** Aspose.OCR for Java  
- **कौन सा सेटिंग भाषा चुनता है?** `settings.setLanguage(Language.Eng)` (या कोई भी समर्थित भाषा)  
- **क्या विकास के लिए लाइसेंस चाहिए?** परीक्षण के लिए एक मुफ्त मूल्यांकन लाइसेंस काम करता है; उत्पादन के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **क्या मैं OCR को इमेज के किसी क्षेत्र तक सीमित कर सकता हूँ?** हाँ, आयतों के साथ `RecognitionSettings.setRecognitionAreas()` का उपयोग करें।  
- **सामान्य रनटाइम क्या है?** मानक लैपटॉप पर प्रति पृष्ठ कुछ सेकंड, इमेज आकार और भाषा जटिलता पर निर्भर करता है।

## ‘इमेज से टेक्स्ट निकालना’ क्या है?
इमेज से टेक्स्ट निकालना (OCR) अक्षरों की दृश्य प्रस्तुति को मशीन‑पठनीय स्ट्रिंग्स में बदलता है। यह खोज, विश्लेषण, और डेटा निष्कर्षण कार्यप्रवाह को सक्षम करता है, जो अन्यथा मैन्युअल ट्रांसक्रिप्शन की आवश्यकता होगी।

## भाषा चयन के साथ Aspose.OCR का उपयोग क्यों करें?
- **बहुभाषी समर्थन** – अपनी इमेज में मौजूद सटीक भाषा(यों) को चुनें ताकि सटीकता बढ़े।  
- **सूक्ष्म नियंत्रण** – स्क्यू को समायोजित करें, पहचान क्षेत्रों को परिभाषित करें, और ऑटो‑स्क्यू व्यवहार सेट करें।  
- **शुद्ध Java API** – कोई नेटिव निर्भरताएँ नहीं, किसी भी Java प्रोजेक्ट में आसानी से एकीकृत किया जा सकता है।  
- **समृद्ध परिणाम डेटा** – एक ही कॉल में प्लेन टेक्स्ट, JSON, बाउंडिंग आयतें, और चेतावनियाँ प्राप्त करें।

## पूर्वापेक्षाएँ

शुरू करने से पहले, सुनिश्चित करें कि आपके पास है:

- **Java Development Kit (JDK)** स्थापित (JDK 8 या बाद का)।  
- **Aspose.OCR for Java** लाइब्रेरी – इसे आधिकारिक साइट से डाउनलोड करें [here](https://reference.aspose.com/ocr/java/).  
- एक इमेज फ़ाइल जिसमें वह टेक्स्ट हो जिसे आप निकालना चाहते हैं, उदाहरण के लिए `p3.png`।

## पैकेज आयात करें

अपने Java स्रोत फ़ाइल में, आवश्यक Aspose.OCR क्लासेस और मानक Java यूटिलिटीज़ को शामिल करें:

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

## स्टेप‑बाय‑स्टेप गाइड

### स्टेप 1: अपना डॉक्यूमेंट डायरेक्टरी सेट करें

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

`"Your Document Directory"` को उस पूर्ण पथ से बदलें जहाँ `p3.png` स्थित है।

### स्टेप 2: इमेज पाथ निर्धारित करें

```java
// The image path
String file = dataDir + "p3.png";
```

सुनिश्चित करें कि `file` वेरिएबल उस सटीक इमेज की ओर इशारा कर रहा है जिसे आप प्रोसेस करना चाहते हैं।

### स्टेप 3: Aspose.OCR API इंस्टेंस बनाएं

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` ऑब्जेक्ट आपको सभी OCR ऑपरेशन्स तक पहुँच प्रदान करता है।

### स्टेप 4: पहचान विकल्प सेट करें (भाषा चयन)

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

1. ऑटो‑स्क्यू को निष्क्रिय करते हैं क्योंकि हम मैन्युअल स्क्यू मान प्रदान करते हैं।  
2. एक आयताकार क्षेत्र (`RecognitionAreas`) को परिभाषित करते हैं ताकि OCR को उस इमेज के हिस्से तक सीमित किया जा सके जिसमें वास्तव में टेक्स्ट है।  
3. **भाषा** को अंग्रेज़ी (`Language.Eng`) पर सेट करते हैं। इसे अपने स्रोत इमेज के अनुसार `Language.Fra`, `Language.Spa` आदि में बदलें।

### स्टेप 5: OCR चलाएँ और परिणाम प्राप्त करें

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` कॉल आपके द्वारा परिभाषित इमेज और सेटिंग्स का उपयोग करके OCR इंजन चलाती है। परिणाम `RecognitionResult` ऑब्जेक्ट में संग्रहीत होता है।

### स्टेप 6: परिणाम प्रिंट करें और उपयोग करें

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
- बाउंडिंग आयत के निर्देशांक।  
- आसान डाउनस्ट्रीम प्रोसेसिंग के लिए JSON प्रतिनिधित्व।  
- पता लगाया गया स्क्यू एंगल और कोई भी चेतावनियाँ।

अब आप `result.recognitionText` को अपने बिज़नेस लॉजिक में फीड कर सकते हैं—इसे स्टोर करें, इंडेक्स करें, या किसी अन्य सर्विस को पास करें।

## सामान्य समस्याएँ और समाधान

| समस्या | कारण | समाधान |
|-------|-------|-----|
| **गड़बड़ अक्षर** | गलत भाषा चयनित की गई | सही `Language` enum सेट करें (उदा., फ़्रेंच के लिए `Language.Fra`)। |
| **कोई टेक्स्ट नहीं मिला** | पहचान क्षेत्र टेक्स्ट को कवर नहीं करता | `Rectangle` निर्देशांक समायोजित करें या पूरी इमेज प्रोसेस करने के लिए `RecognitionAreas` हटाएँ। |
| **धीमी प्रदर्शन** | बहुत बड़ी इमेज या उच्च रिज़ॉल्यूशन | OCR से पहले इमेज को डाउनस्केल करें या JVM के लिए मेमोरी आवंटन बढ़ाएँ। |
| **असमर्थित फॉर्मेट के बारे में चेतावनियाँ** | इमेज फॉर्मेट पहचाना नहीं गया | प्रोसेस करने से पहले इमेज को PNG, JPEG, या TIFF में परिवर्तित करें। |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या मैं एक ही OCR कॉल में कई भाषाओं को पहचान सकता हूँ?**  
**उत्तर:** हाँ। बहुभाषी पहचान सक्षम करने के लिए `settings.setLanguage(Language.Eng | Language.Fra)` का उपयोग करें।

**प्रश्न: Aspose.OCR कौन से इमेज फॉर्मेट्स को सपोर्ट करता है?**  
**उत्तर:** PNG, JPEG, BMP, TIFF, GIF, और कई अन्य। केवल सही फ़ाइल पाथ प्रदान करें।

**प्रश्न: इमेज के आकार की कोई सीमा है?**  
**उत्तर:** कोई कठोर सीमा नहीं है, लेकिन बहुत बड़ी इमेज मेमोरी उपयोग और प्रोसेसिंग समय बढ़ा देती है। बड़े फ़ाइलों को री-साइज़ करने पर विचार करें।

**प्रश्न: प्रोडक्शन लाइसेंस कैसे प्राप्त करें?**  
**उत्तर:** Aspose वेबसाइट से लाइसेंस खरीदें और Aspose दस्तावेज़ में दिखाए अनुसार `License` क्लास के माध्यम से लागू करें।

**प्रश्न: क्या मैं सीधे PDF पेज से टेक्स्ट निकाल सकता हूँ?**  
**उत्तर:** Aspose.OCR के साथ सीधे नहीं। पहले PDF पेज को इमेज में बदलें (जैसे Aspose.PDF का उपयोग करके) और फिर OCR चलाएँ।

## निष्कर्ष

अब आपने देखा कि कैसे Aspose.OCR for Java का उपयोग करके **इमेज से टेक्स्ट निकाला** जाए, उपयुक्त भाषा चुनते हुए और पहचान को विशिष्ट क्षेत्रों तक सीमित करते हुए। यह तरीका सटीक, उच्च‑प्रदर्शन OCR प्रदान करता है जिसे किसी भी Java‑आधारित वर्कफ़्लो में एम्बेड किया जा सकता है—दस्तावेज़ प्रबंधन सिस्टम से लेकर डेटा‑कैप्चर पाइपलाइन तक।

---

**अंतिम अपडेट:** 2025-12-13  
**परीक्षण किया गया संस्करण:** Aspose.OCR 24.11 for Java  
**लेखक:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}