---
title: Aspose.OCR में OCR के लिए आयत तैयार करना
linktitle: Aspose.OCR में OCR के लिए आयत तैयार करना
second_title: Aspose.OCR जावा एपीआई
description: जावा के लिए Aspose.OCR के साथ टेक्स्ट पहचान की शक्ति को अनलॉक करें। निर्बाध एकीकरण के लिए हमारी चरण-दर-चरण मार्गदर्शिका का पालन करें। कुशल ओसीआर क्षमताओं के साथ अपने जावा एप्लिकेशन को बेहतर बनाएं।
weight: 13
url: /hi/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR में OCR के लिए आयत तैयार करना

## परिचय

प्रौद्योगिकी की तेज़ गति वाली दुनिया में, छवियों से पाठ निकालना एक महत्वपूर्ण कार्य बन गया है, जो अनगिनत संभावनाओं के द्वार खोल रहा है। जावा के लिए Aspose.OCR एक शक्तिशाली उपकरण के रूप में सामने आता है, जो ऑप्टिकल कैरेक्टर रिकॉग्निशन (OCR) की जटिल प्रक्रिया को सरल बनाता है। इस व्यापक गाइड में, हम आपको जावा के लिए Aspose.OCR की क्षमता का दोहन करने के लिए आवश्यक कदमों के बारे में बताएंगे, जिससे आप अपने जावा अनुप्रयोगों में पाठ पहचान को सहजता से एकीकृत कर सकेंगे।

## आवश्यक शर्तें

ट्यूटोरियल में गहराई से जाने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित आवश्यक शर्तें हैं:

- जावा डेवलपमेंट किट (जेडीके): जावा के लिए Aspose.OCR को जावा वातावरण की आवश्यकता होती है। Oracle वेबसाइट से नवीनतम JDK डाउनलोड और इंस्टॉल करें।

-  जावा लाइब्रेरी के लिए Aspose.OCR: डाउनलोड लिंक से जावा लाइब्रेरी के लिए Aspose.OCR प्राप्त करें[यहाँ](https://releases.aspose.com/ocr/java/) . दस्तावेज़ में दिए गए इंस्टॉलेशन निर्देशों का पालन करें[यहाँ](https://reference.aspose.com/ocr/java/).

- विकास परिवेश: हमारे साथ कोडिंग शुरू करने के लिए अपना पसंदीदा जावा एकीकृत विकास परिवेश (आईडीई) स्थापित करें।

## पैकेज आयात करें

अपने जावा प्रोजेक्ट में, Aspose.OCR कार्यक्षमताओं को उपलब्ध कराने के लिए आवश्यक पैकेज आयात करें। अपनी जावा फ़ाइल की शुरुआत में निम्नलिखित स्निपेट का उपयोग करें:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## चरण 1: लाइसेंस सेट करें

```java
SetLicense.main(null);
```

 को कॉल करके सुनिश्चित करें कि आपने Aspose.OCR के लिए लाइसेंस सेट कर लिया है`SetLicense` तरीका। पुस्तकालय की पूरी क्षमता को उजागर करने के लिए यह कदम महत्वपूर्ण है।

## चरण 2: दस्तावेज़ निर्देशिका और छवि पथ को परिभाषित करें

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

दस्तावेज़ निर्देशिका और छवि पथ निर्दिष्ट करें जहां OCR प्रसंस्करण के लिए आपकी छवि स्थित है।

## चरण 3: Aspose.OCR इंस्टेंस बनाएं

```java
AsposeOCR api = new AsposeOCR();
```

एपीआई इंस्टेंस बनाने के लिए Aspose.OCR क्लास को इंस्टेंटियेट करें।

## चरण 4: पाठों के साथ आयत तैयार करें

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

उन क्षेत्रों को इंगित करने के लिए टेक्स्ट के साथ आयतों को परिभाषित करें जहां ओसीआर लागू किया जाना चाहिए।

## चरण 5: ओसीआर पहचान करें

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

अंत में, परिभाषित आयतों का उपयोग करके ओसीआर पहचान निष्पादित करें। मान्यता प्राप्त पाठ कंसोल पर मुद्रित किया जाएगा।

## निष्कर्ष

बधाई हो! आपने जावा के लिए Aspose.OCR को अपने प्रोजेक्ट में एकीकृत करने के चरणों को सफलतापूर्वक पार कर लिया है। यह बहुमुखी उपकरण आपको छवियों से आसानी से टेक्स्ट निकालने में सक्षम बनाता है, जो आपके अनुप्रयोगों के लिए अनंत संभावनाएं प्रदान करता है।

## अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या Aspose.OCR अन्य प्रोग्रामिंग भाषाओं के साथ संगत है?

A1: Aspose.OCR .NET, C सहित विभिन्न प्रोग्रामिंग भाषाओं का समर्थन करता है++, और पायथन। अधिक विवरण के लिए दस्तावेज़ की जाँच करें.

### Q2: क्या मैं व्यावसायिक परियोजनाओं के लिए Aspose.OCR का उपयोग कर सकता हूँ?

ए2: हाँ, आप कर सकते हैं। दौरा करना[खरीद पृष्ठ](https://purchase.aspose.com/buy) व्यावसायिक उपयोग के लिए लाइसेंसिंग विकल्प तलाशना।

### Q3: क्या कोई निःशुल्क परीक्षण उपलब्ध है?

 उ3: हाँ, आप निःशुल्क परीक्षण का उपयोग कर सकते हैं[यहाँ](https://releases.aspose.com/).

### Q4: मैं Aspose.OCR के लिए अस्थायी लाइसेंस कैसे प्राप्त करूं?

 A4: अस्थायी लाइसेंस प्राप्त किया जा सकता है[यहाँ](https://purchase.aspose.com/temporary-license/).

### Q5: सहायता चाहिए या कोई प्रश्न हैं?

 A5: Aspose.OCR समुदाय पर जाएँ[मंच](https://forum.aspose.com/c/ocr/16) समर्थन और चर्चा के लिए.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
