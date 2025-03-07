---
title: ओसीआर छवि पहचान में रेखाओं के लिए आयत प्राप्त करें
linktitle: ओसीआर छवि पहचान में रेखाओं के लिए आयत प्राप्त करें
second_title: Aspose.OCR .NET एपीआई
description: सटीक OCR छवि पहचान के लिए .NET के लिए Aspose.OCR का अन्वेषण करें। पाठ निष्कर्षण की शक्ति को सहजता से उजागर करें।
weight: 10
url: /hi/net/image-and-drawing-recognition/get-rectangles-for-lines/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ओसीआर छवि पहचान में रेखाओं के लिए आयत प्राप्त करें

## परिचय

.NET के लिए Aspose.OCR की दुनिया में आपका स्वागत है, एक शक्तिशाली उपकरण जो आपको अपने .NET अनुप्रयोगों में ऑप्टिकल कैरेक्टर रिकग्निशन (OCR) की क्षमता का उपयोग करने की अनुमति देता है। चाहे आप एक अनुभवी डेवलपर हों या जिज्ञासु उत्साही, यह मार्गदर्शिका आपको Aspose.OCR का उपयोग करके OCR छवि पहचान में रेखाओं के लिए आयत प्राप्त करने की प्रक्रिया के बारे में बताएगी।

## आवश्यक शर्तें

ट्यूटोरियल में जाने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित आवश्यक शर्तें हैं:

- C# और .NET विकास का बुनियादी ज्ञान।
- एक एकीकृत विकास वातावरण (आईडीई) जैसे विजुअल स्टूडियो।
-  .NET लाइब्रेरी के लिए Aspose.OCR स्थापित। आप इसे डाउनलोड कर सकते हैं[यहाँ](https://releases.aspose.com/ocr/net/).
- ओसीआर पहचान के लिए पाठ युक्त एक नमूना छवि।

## नामस्थान आयात करें

सुनिश्चित करें कि आपके प्रोजेक्ट में आवश्यक नामस्थान आयातित हैं। अपनी C# फ़ाइल के शीर्ष पर निम्नलिखित पंक्तियाँ जोड़ें:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

अब, आइए ओसीआर छवि पहचान में रेखाओं के लिए आयत प्राप्त करने की प्रक्रिया को आसान चरणों में विभाजित करें।

## चरण 1: अपनी दस्तावेज़ निर्देशिका सेट करें

```csharp
// एक्सस्टार्ट:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

 प्रतिस्थापित करें`"Your Document Directory"` आपकी दस्तावेज़ निर्देशिका के वास्तविक पथ के साथ।

## चरण 2: Aspose.OCR को आरंभ करें

```csharp
// एक्सस्टार्ट:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

 का एक उदाहरण बनाएं`AsposeOcr` OCR कार्यक्षमता तक पहुँचने के लिए क्लास।

## चरण 3: छवि पथ निर्दिष्ट करें

```csharp
// एक्सस्टार्ट:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

जिस छवि पर आप OCR निष्पादित करना चाहते हैं उसका पूरा पथ परिभाषित करें।

## चरण 4: छवि को पहचानें और आयत प्राप्त करें

```csharp
// एक्सस्टार्ट:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

 का उपयोग करें`GetRectangles` निर्दिष्ट छवि में पंक्तियों के लिए आयतों को पुनः प्राप्त करने की विधि।

## चरण 5: परिणाम प्रिंट करें

```csharp
// एक्सस्टार्ट:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

पता लगाए गए क्षेत्रों के निर्देशांक को कंसोल पर प्रिंट करें।

## निष्कर्ष

बधाई हो! आपने .NET के लिए Aspose.OCR का उपयोग करके OCR छवि पहचान में रेखाओं के लिए आयत सफलतापूर्वक प्राप्त कर लिए हैं। यह बहुमुखी उपकरण आपके अनुप्रयोगों में पाठ निष्कर्षण के लिए संभावनाओं की दुनिया खोलता है।

## अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या मैं किसी भी प्रकार की छवि के साथ .NET के लिए Aspose.OCR का उपयोग कर सकता हूँ?

A1: Aspose.OCR आपके OCR अनुप्रयोगों में लचीलापन सुनिश्चित करते हुए, छवि प्रारूपों की एक विस्तृत श्रृंखला का समर्थन करता है।

### Q2: OCR पहचान कितनी सटीक है?

A2: Aspose.OCR उच्च सटीकता के लिए उन्नत एल्गोरिदम का लाभ उठाता है, जो इसे विभिन्न पाठ पहचान परिदृश्यों के लिए उपयुक्त बनाता है।

### Q3: क्या कोई परीक्षण संस्करण उपलब्ध है?

 A3: हां, आप .NET के लिए Aspose.OCR की क्षमताओं का पता लगा सकते हैं[मुफ्त परीक्षण](https://releases.aspose.com/).

### Q4: मुझे व्यापक दस्तावेज कहां मिल सकते हैं?

 A4: का संदर्भ लें[प्रलेखन](https://reference.aspose.com/ocr/net/) विस्तृत जानकारी और उपयोग दिशानिर्देशों के लिए।

### Q5: सहायता की आवश्यकता है या विशिष्ट प्रश्न हैं?

 A5: पर जाएँ[Aspose.OCR फोरम](https://forum.aspose.com/c/ocr/16) सामुदायिक समर्थन और चर्चा के लिए।
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
