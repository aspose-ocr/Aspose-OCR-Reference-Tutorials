---
title: Aspose.OCR में पाठ क्षेत्रों के साथ आयत प्राप्त करना
linktitle: Aspose.OCR में पाठ क्षेत्रों के साथ आयत प्राप्त करना
second_title: Aspose.OCR जावा एपीआई
description: जावा के लिए Aspose.OCR की शक्ति को अनलॉक करें। इस चरण-दर-चरण मार्गदर्शिका में जानें कि छवियों से पाठ को सहजता से कैसे निकाला जाए। कुशल पाठ पहचान के लिए अभी डाउनलोड करें।
type: docs
weight: 12
url: /hi/java/ocr-basics/get-rectangles-with-text-areas/
---
## परिचय

क्या आप अपने जावा एप्लिकेशन में शक्तिशाली ऑप्टिकल कैरेक्टर रिकग्निशन (ओसीआर) क्षमताओं को एकीकृत करना चाह रहे हैं? जावा के लिए Aspose.OCR छवियों से सटीक और कुशल पाठ निष्कर्षण के लिए आपका पसंदीदा समाधान है। यह ट्यूटोरियल आपको Aspose.OCR का उपयोग करके पाठ क्षेत्रों के साथ आयत प्राप्त करने की प्रक्रिया में मार्गदर्शन करेगा, जिससे आपको इस जावा OCR लाइब्रेरी की पूरी क्षमता का उपयोग करने में मदद मिलेगी।

## आवश्यक शर्तें

ट्यूटोरियल में जाने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित आवश्यक शर्तें हैं:

- जावा विकास पर्यावरण: सुनिश्चित करें कि आपके सिस्टम पर जावा स्थापित है।
-  जावा लाइब्रेरी के लिए Aspose.OCR: Aspose.OCR लाइब्रेरी डाउनलोड करें और सेट करें। आप डाउनलोड लिंक पा सकते हैं[यहाँ](https://releases.aspose.com/ocr/java/).

## पैकेज आयात करें

अपने जावा प्रोजेक्ट में, Aspose.OCR की कार्यक्षमताओं का लाभ उठाने के लिए आवश्यक पैकेज आयात करें:

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

## चरण 1: अपना प्रोजेक्ट सेट करें

सुनिश्चित करें कि आपके पास जावा प्रोजेक्ट तैयार है, और Aspose.OCR लाइब्रेरी एकीकृत है।

## चरण 2: दस्तावेज़ निर्देशिका और छवि पथ को परिभाषित करें

```java
// दस्तावेज़ निर्देशिका का पथ.
String dataDir = "Your Document Directory";

// छवि पथ
String imagePath = dataDir + "p3.png";
```

## चरण 3: Aspose.OCR इंस्टेंस बनाएं

```java
// Aspose.OCR उदाहरण बनाएँ
AsposeOCR api = new AsposeOCR();
```

## चरण 4: छवि में टेक्स्ट को पहचानें

```java
try {
    // फ़ाइल के पूर्ण पथ द्वारा पृष्ठ को पहचानें
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

## चरण 5: पाठ क्षेत्रों के साथ आयत प्राप्त करें

```java
// छवि में पाठ क्षेत्रों के साथ आयत प्राप्त करें।
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// प्रत्येक पाठ क्षेत्र आयत को प्रिंट करें
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## निष्कर्ष

इस ट्यूटोरियल में, आपने सीखा कि छवियों से टेक्स्ट को कुशलतापूर्वक निकालने के लिए जावा के लिए Aspose.OCR को अपने प्रोजेक्ट में कैसे एकीकृत किया जाए। Aspose.OCR एक सहज उपयोगकर्ता अनुभव के लिए सटीक परिणाम प्रदान करते हुए, OCR कार्यों को सरल बनाता है।

## अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या Aspose.OCR जावा 11 के साथ संगत है?

A1: हाँ, Aspose.OCR Java 11 और बाद के संस्करणों के साथ संगत है।

### Q2: क्या मैं व्यक्तिगत और व्यावसायिक दोनों परियोजनाओं के लिए Aspose.OCR का उपयोग कर सकता हूँ?

 A2: हाँ, Aspose.OCR का उपयोग व्यक्तिगत और व्यावसायिक दोनों परियोजनाओं के लिए किया जा सकता है। लाइसेंसिंग विवरण के लिए, यहां जाएं[यहाँ](https://purchase.aspose.com/buy).

### Q3: मैं Aspose.OCR के लिए अस्थायी लाइसेंस कैसे प्राप्त करूं?

 उ3: आप एक अस्थायी लाइसेंस प्राप्त कर सकते हैं[यहाँ](https://purchase.aspose.com/temporary-license/).

### Q4: मुझे Aspose.OCR के लिए समर्थन कहां मिल सकता है?

 A4: समर्थन और चर्चा के लिए, पर जाएँ[Aspose.OCR फोरम](https://forum.aspose.com/c/ocr/16).

### Q5: क्या Aspose.OCR मल्टीथ्रेडिंग का समर्थन करता है?

A5: हाँ, Aspose.OCR समवर्ती वातावरण में बेहतर प्रदर्शन के लिए मल्टीथ्रेडिंग का समर्थन करता है।
