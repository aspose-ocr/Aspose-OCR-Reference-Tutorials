---
date: 2025-12-12
description: Aspose.OCR for Java का उपयोग करके Detect Areas Mode के साथ OCR कैसे करें,
  छवि से टेक्स्ट निकालें और स्पेल‑चेक्ड परिणाम प्राप्त करें, सीखें। यह चरण‑दर‑चरण
  Aspose OCR Java ट्यूटोरियल है।
linktitle: How to Perform OCR with Detect Areas Mode in Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspise.OCR for Java का उपयोग करके डिटेक्ट एरिया मोड के साथ OCR कैसे करें
url: /hi/java/ocr-operations/perform-ocr-detect-areas-mode/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR में Detect Areas Mode के साथ OCR कैसे करें

## Introduction

Optical Character Recognition (OCR) तब आवश्यक हो जाता है जब आपको **इमेज फ़ाइलों से टेक्स्ट निकालना** होता है और उसे खोज योग्य, संपादन योग्य डेटा में बदलना होता है। इस **Aspose OCR Java ट्यूटोरियल** में हम एक व्यावहारिक उदाहरण के माध्यम से दिखाएंगे कि **OCR कैसे किया जाता है** शक्तिशाली *Detect Areas Mode* फीचर का उपयोग करके, और साथ ही बिल्ट‑इन स्पेल‑चेक क्षमता को भी प्रदर्शित करेंगे। इस गाइड के अंत तक आपके पास एक तैयार‑चलाने‑योग्य कोड स्निपेट होगा जो फोटो‑टाइप दस्तावेज़ से टेक्स्ट पहचानता है और साफ़, सुधारा हुआ आउटपुट देता है।

## Quick Answers
- **What is Detect Areas Mode?** एक सेटिंग जो फ़ोटोग्राफ़िक इमेजेज़ के लिए OCR को अनुकूलित करती है और स्वचालित रूप से टेक्स्ट ब्लॉक्स का पता लगाती है।  
- **Which language does the example use?** Java, Aspose.OCR लाइब्रेरी के साथ।  
- **Do I need a license for testing?** विकास के लिए एक फ्री ट्रायल काम करता है; उत्पादन के लिए एक कमर्शियल लाइसेंस आवश्यक है।  
- **Can the result be spell‑checked?** हाँ – API “ocr with spell check” सेक्शन लौटाता है।  
- **What file type is used in the demo?** *Receipt.jpg* नाम की एक JPEG इमेज।

## Prerequisites

ट्यूटोरियल शुरू करने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित प्री‑रिक्विज़िट्स मौजूद हैं:

- Java Development Environment: सुनिश्चित करें कि आपके मशीन पर Java इंस्टॉल है।  
- Aspose.OCR for Java: Aspose.OCR लाइब्रेरी डाउनलोड और इंस्टॉल करें। आप डाउनलोड लिंक [here](https://releases.aspose.com/ocr/java/) पर पा सकते हैं।  
- Document for OCR: एक इमेज डॉक्यूमेंट (जैसे **Receipt.jpg**) तैयार करें जिसमें वह टेक्स्ट हो जिसे आप निकालना चाहते हैं।

## Import Packages

अपने Java प्रोजेक्ट में Aspose.OCR उपयोग करने के लिए आवश्यक पैकेज इम्पोर्ट करें। यहाँ एक उदाहरण है:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.DetectAreasMode;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionResult.LinesResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Step 1: Set Up the OCR Operation

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String file = dataDir + "Receipt.jpg";

// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();

// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setDetectAreasMode(DetectAreasMode.PHOTO);
```

इस चरण में हम OCR इंजन को इनिशियलाइज़ करते हैं, उसे इमेज फ़ाइल की ओर पॉइंट करते हैं, और **Detect Areas Mode** को एनेबल करते हैं ताकि इंजन तस्वीर को एक सामान्य फोटो मानकर बिखरे हुए टेक्स्ट ब्लॉक्स को पहचान सके।

## Step 2: Perform OCR and Retrieve Results

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

यहाँ हम वास्तव में **OCR करते हैं**। `RecognizePage` कॉल एक `RecognitionResult` लौटाता है जिसमें कच्चा टेक्स्ट, लेआउट जानकारी, और स्पेल‑चेक्ड आउटपुट शामिल होते हैं।

## Step 3: Print OCR Results

```java
// Print result
printResult(result);
```

हेल्पर मेथड `printResult` (पूरा सोर्स पैकेज में उपलब्ध) कई प्रकार की जानकारी प्रदर्शित करता है: निकाला गया टेक्स्ट, कॉन्फिडेंस स्कोर, डिटेक्टेड पैराग्राफ, लाइन‑बाय‑लाइन डेटा, कैरेक्टर अल्टरनेटिव्स, वार्निंग्स, JSON पेलोड, और **OCR with spell check** सुधरा हुआ टेक्स्ट।

## Why Use Detect Areas Mode?

- **Optimised for photos** – स्वचालित रूप से टेक्स्ट रीजन को अलग करता है, शोर को कम करता है।  
- **Improved accuracy** – विशेष रूप से रसीदों, इनवॉइसेज़, और स्कैन किए गए फॉर्म्स पर बेहतर परिणाम देता है।  
- **Built‑in spell checking** – अतिरिक्त प्रोसेसिंग के बिना सामान्य OCR त्रुटियों को साफ़ करता है।

## Common Use Cases

| परिदृश्य | लाभ |
|----------|-----|
| रसीद प्रोसेसिंग | व्यापारी के नाम, कुल राशि और तिथियों को जल्दी से निकालना। |
| इनवॉइस डिजिटलीकरण | लाइन आइटम और टैक्स जानकारी को अकाउंटिंग सिस्टम के लिए एक्सट्रैक्ट करना। |
| पहचान दस्तावेज़ स्कैनिंग | ड्राइवर लाइसेंस या पासपोर्ट से नाम और नंबर कैप्चर करना। |

## Troubleshooting Tips & Common Pitfalls

- **Incorrect file path** – `dataDir` को दोबारा जांचें और सुनिश्चित करें कि इमेज मौजूद है।  
- **Low‑resolution images** – 300 dpi से कम रेज़ोल्यूशन पर OCR की सटीकता काफी घट जाती है; इमेज को प्री‑प्रोसेस करने पर विचार करें।  
- **Missing license** – वैध लाइसेंस के बिना API ट्रायल मोड में चलता है और परिणामों पर वॉटरमार्क लगा सकता है।  

## Conclusion

बधाई हो! आपने Aspose.OCR for Java का उपयोग करके Detect Areas Mode के साथ **OCR कैसे किया जाता है** सफलतापूर्वक सीख लिया है। यह तरीका न केवल इमेज फ़ाइलों से टेक्स्ट निकालता है बल्कि स्पेल‑चेक्ड, साफ़ आउटपुट भी प्रदान करता है—डेटा पाइपलाइन या UI डिस्प्ले के लिए एकदम उपयुक्त।

## Frequently Asked Questions

**Q: क्या Aspose.OCR कई भाषाओं को संभाल सकता है?**  
A: हाँ, Aspose.OCR कई भाषाओं का समर्थन करता है, जिससे यह वैश्विक एप्लिकेशन्स के लिए बहुमुखी बनता है।

**Q: क्या Aspose.OCR बड़े‑पैमाने पर OCR ऑपरेशन्स के लिए उपयुक्त है?**  
A: बिल्कुल। लाइब्रेरी हाई‑थ्रूपुट परिदृश्यों के लिए डिज़ाइन की गई है और बैच प्रोसेसिंग पाइपलाइन में इंटीग्रेट की जा सकती है।

**Q: क्या मैं Aspose.OCR को वेब एप्लिकेशन्स में इंटीग्रेट कर सकता हूँ?**  
A: हाँ, आप Java API को सर्वलेट‑आधारित या Spring Boot वेब सर्विसेज़ में एम्बेड करके OCR को एक REST एन्डपॉइंट के रूप में प्रदान कर सकते हैं।

**Q: क्या Aspose.OCR स्पेल‑चेकिंग क्षमताएँ प्रदान करता है?**  
A: हाँ, जैसा कि दिखाया गया है, परिणाम में “ocr with spell check” सेक्शन शामिल होता है जो सामान्य पहचान त्रुटियों को सुधारता है।

**Q: क्या Aspose.OCR सपोर्ट के लिए कोई कम्युनिटी फ़ोरम है?**  
A: हाँ, आप सपोर्ट प्राप्त कर सकते हैं और कम्युनिटी के साथ जुड़ सकते हैं [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) पर।

---

**Last Updated:** 2025-12-12  
**Tested With:** Aspose.OCR for Java 23.12 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}