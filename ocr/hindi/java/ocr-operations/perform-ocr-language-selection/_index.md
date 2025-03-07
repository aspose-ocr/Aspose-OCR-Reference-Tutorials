---
title: Aspose.OCR में भाषा चयन के साथ OCR निष्पादित करना
linktitle: Aspose.OCR में भाषा चयन के साथ OCR निष्पादित करना
second_title: Aspose.OCR जावा एपीआई
description: जावा के लिए Aspose.OCR के साथ छवियों से सटीक पाठ निष्कर्षण अनलॉक करें। भाषा चयन के साथ सटीक ओसीआर के लिए हमारी चरण-दर-चरण मार्गदर्शिका का पालन करें।
weight: 11
url: /hi/java/ocr-operations/perform-ocr-language-selection/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR में भाषा चयन के साथ OCR निष्पादित करना

## परिचय

प्रौद्योगिकी के निरंतर विकसित होते परिदृश्य में, ऑप्टिकल कैरेक्टर रिकॉग्निशन (ओसीआर) छवियों से सार्थक जानकारी निकालने में महत्वपूर्ण भूमिका निभाता है। जावा के लिए Aspose.OCR एक शक्तिशाली उपकरण के रूप में सामने आता है जो डेवलपर्स को OCR क्षमताओं को उनके जावा अनुप्रयोगों में सहजता से एकीकृत करने में सक्षम बनाता है। इस चरण-दर-चरण मार्गदर्शिका में, हम यह पता लगाएंगे कि Aspose.OCR का उपयोग करके भाषा चयन के साथ OCR कैसे निष्पादित किया जाए, जिससे विविध सामग्री को सटीकता के साथ संसाधित करने की क्षमता का पता लगाया जा सके।

## आवश्यक शर्तें

ट्यूटोरियल में जाने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित आवश्यक शर्तें हैं:

- जावा विकास पर्यावरण: सुनिश्चित करें कि आपके सिस्टम पर जावा स्थापित है, और आपका विकास वातावरण स्थापित है।

-  Aspose.OCR लाइब्रेरी: जावा के लिए Aspose.OCR लाइब्रेरी डाउनलोड और इंस्टॉल करें। आप पुस्तकालय और संबंधित दस्तावेज पा सकते हैं[यहाँ](https://reference.aspose.com/ocr/java/).

- छवि फ़ाइल: एक छवि फ़ाइल तैयार करें जिसमें वह पाठ हो जिसे आप निकालना चाहते हैं। उदाहरण के लिए, आइए "p3.png" नामक फ़ाइल का उपयोग करें।

## पैकेज आयात करें

अपने जावा प्रोजेक्ट में, Aspose.OCR कार्यक्षमता का लाभ उठाने के लिए आवश्यक पैकेज आयात करें। अपनी जावा फ़ाइल की शुरुआत में निम्नलिखित पंक्तियाँ जोड़ें:

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

## चरण 1: अपनी दस्तावेज़ निर्देशिका सेट करें

```java
// दस्तावेज़ निर्देशिका का पथ.
String dataDir = "Your Document Directory";
```

"आपकी दस्तावेज़ निर्देशिका" को उस निर्देशिका के वास्तविक पथ से बदलें जहां आपकी छवि फ़ाइल स्थित है।

## चरण 2: छवि पथ को परिभाषित करें

```java
// छवि पथ
String file = dataDir + "p3.png";
```

अपनी विशिष्ट छवि फ़ाइल को इंगित करने के लिए फ़ाइल चर को समायोजित करें।

## चरण 3: Aspose.OCR API इंस्टेंस बनाएं

```java
// एपीआई उदाहरण बनाएं
AsposeOCR api = new AsposeOCR();
```

इसकी सुविधाओं तक पहुँचने के लिए AsposeOCR ऑब्जेक्ट को आरंभ करें।

## चरण 4: पहचान विकल्प सेट करें

```java
// पहचान विकल्प सेट करें
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

अपनी आवश्यकताओं के आधार पर पहचान सेटिंग्स को अनुकूलित करें। तिरछापन, भाषा और पहचान क्षेत्र जैसे मापदंडों को समायोजित करें।

## चरण 5: ओसीआर निष्पादित करें और परिणाम प्राप्त करें

```java
// परिणाम वस्तु प्राप्त करें
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

निर्दिष्ट छवि फ़ाइल और सेटिंग्स का उपयोग करके ओसीआर ऑपरेशन निष्पादित करें। परिणाम को RecognitionResult ऑब्जेक्ट में कैप्चर करें।

## चरण 6: परिणाम प्रिंट करें और उपयोग करें

```java
// परिणाम प्रिंट करें
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

निकाले गए पाठ, पहचान क्षेत्र, JSON प्रतिनिधित्व, तिरछा कोण और किसी भी चेतावनी को प्रिंट करें। अपने आवेदन में आवश्यकतानुसार परिणामों का उपयोग करें।

## निष्कर्ष

इस ट्यूटोरियल में, हमने भाषा चयन के साथ ओसीआर निष्पादित करने के लिए जावा के लिए Aspose.OCR के सहज एकीकरण के बारे में विस्तार से बताया है। यह शक्तिशाली लाइब्रेरी छवियों से पाठ को सटीक रूप से निकालने का लक्ष्य रखने वाले डेवलपर्स के लिए संभावनाओं की दुनिया खोलती है।

## अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या मैं एक ही पहचान प्रक्रिया में एकाधिक भाषाओं के लिए Aspose.OCR का उपयोग कर सकता हूँ?

A1: हाँ, आप बहुभाषी सामग्री के लिए पहचान सटीकता बढ़ाने के लिए RecognitionSettings में कई भाषाएँ सेट कर सकते हैं।

### Q2: मैं Aspose.OCR के साथ विभिन्न छवि प्रारूपों को कैसे संभाल सकता हूं?

A2: Aspose.OCR PNG, JPEG और TIFF सहित विभिन्न छवि प्रारूपों का समर्थन करता है। बस छवि पथ चर में सही फ़ाइल पथ प्रदान करें।

### Q3: क्या छवि के आकार की कोई सीमा है जिसे Aspose.OCR संसाधित कर सकता है?

A3: Aspose.OCR विभिन्न आकारों की छवियों को संभाल सकता है, लेकिन बड़ी छवियों के लिए अधिक प्रसंस्करण समय और संसाधनों की आवश्यकता हो सकती है।

### Q4: क्या मैं किसी छवि के भीतर विशिष्ट क्षेत्रों के लिए पहचान सेटिंग्स को ठीक कर सकता हूँ?

उ4: बिल्कुल. लक्षित पहचान के लिए छवि के भीतर विशिष्ट आयतों को परिभाषित करने के लिए RecognitionAreas सुविधा का उपयोग करें।

### Q5: क्या Aspose.OCR व्यक्तिगत और व्यावसायिक दोनों परियोजनाओं के लिए उपयुक्त है?

A5: हाँ, Aspose.OCR लचीले लाइसेंसिंग विकल्प प्रदान करता है, जो इसे व्यक्तिगत और व्यावसायिक उपयोग दोनों के लिए उपयुक्त बनाता है।
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
