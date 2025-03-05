---
title: जावा के लिए Aspose.OCR में URL से छवि पर OCR निष्पादित करना
linktitle: जावा के लिए Aspose.OCR में URL से छवि पर OCR निष्पादित करना
second_title: Aspose.OCR जावा एपीआई
description: Aspose.OCR के साथ जावा में निर्बाध छवि पाठ निष्कर्षण अनलॉक करें। आसान एकीकरण के साथ उच्च सटीकता ओसीआर।
type: docs
weight: 11
url: /hi/java/advanced-ocr-techniques/perform-ocr-image-from-url/
---
## परिचय

जावा के लिए Aspose.OCR का उपयोग करके URL से एक छवि पर ऑप्टिकल कैरेक्टर रिकॉग्निशन (OCR) करने के बारे में हमारी चरण-दर-चरण मार्गदर्शिका में आपका स्वागत है। यह ट्यूटोरियल आपके जावा एप्लिकेशन में Aspose.OCR को सहजता से एकीकृत करने में आपकी मदद करने के लिए डिज़ाइन किया गया है, जिससे आप आसानी से छवियों से टेक्स्ट निकाल सकते हैं। Aspose.OCR एक शक्तिशाली OCR लाइब्रेरी है जो विभिन्न छवि प्रारूपों का समर्थन करती है, जो इसे पाठ निष्कर्षण की आवश्यकता वाले अनुप्रयोगों के लिए एक मूल्यवान उपकरण बनाती है।

## आवश्यक शर्तें

ट्यूटोरियल में जाने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित शर्तें हैं:

1. जावा विकास पर्यावरण: सुनिश्चित करें कि आपकी मशीन पर एक कार्यशील जावा विकास वातावरण स्थापित है।

2.  Aspose.OCR लाइब्रेरी: जावा लाइब्रेरी के लिए Aspose.OCR डाउनलोड और इंस्टॉल करें। आप लाइब्रेरी और संबंधित दस्तावेज़ यहां पा सकते हैं[Aspose.OCR वेबसाइट](https://reference.aspose.com/ocr/java/).

## पैकेज आयात करें

अपने जावा प्रोजेक्ट में, Aspose.OCR के लिए आवश्यक पैकेज आयात करें:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## चरण 1: एपीआई इंस्टेंस बनाएं

AsposeOCR वर्ग का एक उदाहरण प्रारंभ करें:

```java
AsposeOCR api = new AsposeOCR();
```

## चरण 2: छवि URL को परिभाषित करें

उस छवि का URL निर्दिष्ट करें जिससे आप OCR करना चाहते हैं:

```java
String uri = "https://www.example.com/your-image.png";
```

## चरण 3: पहचान विकल्प सेट करें

पहचान सेटिंग्स कॉन्फ़िगर करें, जैसे ऑटो-स्क्यू अक्षम करना और पहचान क्षेत्रों को परिभाषित करना:

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);

// आयतों का उपयोग करके पहचान क्षेत्रों को परिभाषित करें
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
```

## चरण 4: ओसीआर निष्पादित करें

OCR मान्यता प्रक्रिया लागू करें:

```java
RecognitionResult result = null;
try {
    result = api.RecognizePageFromUri(uri, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

## चरण 5: परिणाम प्रिंट करें

निकाले गए पाठ, पहचान क्षेत्र पाठ, JSON आउटपुट और किसी भी चेतावनी सहित पहचान परिणाम प्रदर्शित करें:

```java
System.out.println("Result: \n" + result.recognitionText + "\n\n");
System.out.println("RecognitionAreasText: \n");
for (String text : result.recognitionAreasText) {
    System.out.println(text);
}
System.out.println("JSON: \n" + result.GetJson());
System.out.println("Warnings: \n");
for (String warning : result.warnings) {
    System.out.println(warning);
}
```

Aspose.OCR को अपने जावा एप्लिकेशन में एकीकृत करने और छवियों से सटीकता के साथ टेक्स्ट निकालने के लिए इन चरणों को दोहराएं।

## निष्कर्ष

अंत में, जावा के लिए Aspose.OCR का लाभ उठाना OCR कार्यों के लिए एक मजबूत समाधान प्रदान करता है, जो डेवलपर्स को छवियों से पाठ को सहजता से निकालने में सक्षम बनाता है। चरण-दर-चरण मार्गदर्शिका एक सहज एकीकरण प्रक्रिया सुनिश्चित करती है, जिससे यह सभी स्तरों के डेवलपर्स के लिए सुलभ हो जाती है।

## अक्सर पूछे जाने वाले प्रश्न

### Q1: छवियों से पाठ को पहचानने में Aspose.OCR कितना सटीक है?

A1: Aspose.OCR पाठ पहचान में उच्च सटीकता प्रदान करता है, खासकर जब सटीक पहचान क्षेत्रों के साथ कॉन्फ़िगर किया गया हो।

### Q2: क्या Aspose.OCR OCR पहचान के दौरान कई भाषाओं को संभाल सकता है?

A2: हां, Aspose.OCR विविध अनुप्रयोगों के लिए बहुमुखी प्रतिभा प्रदान करते हुए, कई भाषाओं में पाठ की पहचान का समर्थन करता है।

### Q3: क्या वाणिज्यिक परियोजनाओं में Aspose.OCR का उपयोग करने के लिए कोई लाइसेंस संबंधी विचार हैं?

A3: हाँ, व्यावसायिक उपयोग के लिए Aspose.OCR लाइसेंसिंग शर्तों का अनुपालन सुनिश्चित करें। को देखें[buy.aspose.com](https://purchase.aspose.com/buy) लाइसेंसिंग विवरण के लिए.

### Q4: मैं Aspose.OCR-संबंधित मुद्दों के लिए समर्थन कैसे प्राप्त कर सकता हूं?

 A4: पर जाएँ[Aspose.OCR फोरम](https://forum.aspose.com/c/ocr/16) सामुदायिक समर्थन और चर्चा के लिए। प्रीमियम सहायता के लिए, अस्थायी लाइसेंस प्राप्त करने पर विचार करें[अस्थायी लाइसेंस](https://purchase.aspose.com/temporary-license/).

### Q5: क्या जावा के लिए Aspose.OCR के लिए कोई निःशुल्क परीक्षण उपलब्ध है?

 A5: हां, यहां उपलब्ध निःशुल्क परीक्षण के साथ Aspose.OCR की सुविधाओं का पता लगाएं[विज्ञप्ति.aspose.com](https://releases.aspose.com/).
