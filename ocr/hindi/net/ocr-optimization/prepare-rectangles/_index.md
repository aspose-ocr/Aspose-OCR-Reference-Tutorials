---
title: ओसीआर छवि पहचान में आयत तैयार करें
linktitle: ओसीआर छवि पहचान में आयत तैयार करें
second_title: Aspose.OCR .NET एपीआई
description: हमारे व्यापक गाइड के साथ .NET के लिए Aspose.OCR की क्षमता को अनलॉक करें। चरण-दर-चरण जानें कि छवि पहचान के लिए आयत कैसे तैयार करें। निर्बाध OCR एकीकरण के साथ अपने .NET अनुप्रयोगों को उन्नत करें।
weight: 11
url: /hi/net/ocr-optimization/prepare-rectangles/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ओसीआर छवि पहचान में आयत तैयार करें

## परिचय

प्रौद्योगिकी के निरंतर विकसित होते परिदृश्य में, ऑप्टिकल कैरेक्टर रिकॉग्निशन (ओसीआर) छवियों को मशीन-पठनीय पाठ में बदलने में महत्वपूर्ण भूमिका निभाता है। .NET के लिए Aspose.OCR उन डेवलपर्स के लिए एक मजबूत समाधान के रूप में सामने आता है जो अपने .NET अनुप्रयोगों में OCR क्षमताओं का निर्बाध एकीकरण चाहते हैं। इस व्यापक गाइड में, हम .NET के लिए Aspose.OCR का उपयोग करके OCR छवि पहचान में आयत तैयार करने की प्रक्रिया का पता लगाएंगे।

## आवश्यक शर्तें

ट्यूटोरियल में जाने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित आवश्यक शर्तें हैं:

- .NET विकास का कार्यसाधक ज्ञान।
-  .NET लाइब्रेरी के लिए Aspose.OCR स्थापित। आप इसे डाउनलोड कर सकते हैं[यहाँ](https://releases.aspose.com/ocr/net/).
- छवि पहचान अवधारणाओं की बुनियादी समझ।

## नामस्थान आयात करें

आइए अपनी OCR यात्रा शुरू करने के लिए आवश्यक नामस्थान आयात करके शुरुआत करें:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## चरण 1: अपनी दस्तावेज़ निर्देशिका सेट करें

 उस निर्देशिका को निर्दिष्ट करके प्रारंभ करें जहां आपके दस्तावेज़ संग्रहीत हैं। प्रतिस्थापित करें`"Your Document Directory"` आपके दस्तावेज़ों के वास्तविक पथ के साथ।

```csharp
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "Your Document Directory";

// AsposeOcr का एक उदाहरण प्रारंभ करें
AsposeOcr api = new AsposeOcr();
```

## चरण 2: एकाधिक आयतों वाली छवि को पहचानें

इस चरण में, हम प्रदर्शित करेंगे कि एकाधिक आयतों का उपयोग करके किसी छवि से टेक्स्ट को कैसे पहचाना जाए। इन उप-चरणों का पालन करें:

### 2.1 आयतों को परिभाषित करें

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 2.2 ओसीआर पहचान करें

```csharp
// पहला मामला
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// मान्यता प्राप्त पाठ प्रदर्शित करें
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## चरण 3: पहचान सेटिंग्स के साथ छवि को पहचानें

इस चरण में, हम छवि पहचान के लिए RecognitionSettings का उपयोग करके एक वैकल्पिक विधि प्रदर्शित करेंगे:

### 3.1 पहचान सेटिंग्स को परिभाषित करें

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 3.2 मान्यता प्राप्त पाठ प्रदर्शित करें

```csharp
// मान्यता प्राप्त पाठ प्रदर्शित करें
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## निष्कर्ष

बधाई हो! आपने .NET के लिए Aspose.OCR का उपयोग करके OCR छवि पहचान में आयत तैयार करने की प्रक्रिया को सफलतापूर्वक नेविगेट कर लिया है। यह मार्गदर्शिका आपको OCR को अपने .NET अनुप्रयोगों में निर्बाध रूप से एकीकृत करने, उनकी पाठ पहचान क्षमताओं को बढ़ाने का अधिकार देती है।

### अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या मैं अन्य .NET फ्रेमवर्क के साथ .NET के लिए Aspose.OCR का उपयोग कर सकता हूँ?

A1: हां, .NET के लिए Aspose.OCR विभिन्न .NET फ्रेमवर्क के साथ संगत है।

### Q2: क्या .NET के लिए Aspose.OCR का निःशुल्क परीक्षण उपलब्ध है?

 ए2: बिल्कुल! आप नि:शुल्क परीक्षण का उपयोग कर सकते हैं[यहाँ](https://releases.aspose.com/).

### Q3: मैं .NET के लिए Aspose.OCR के लिए समर्थन कैसे प्राप्त करूं?

 A3: पर जाएँ[Aspose.OCR फोरम](https://forum.aspose.com/c/ocr/16) समर्पित समर्थन के लिए.

### Q4: क्या मैं परीक्षण उद्देश्यों के लिए अस्थायी लाइसेंस प्राप्त कर सकता हूँ?

 उ4: हाँ, आप अस्थायी लाइसेंस प्राप्त कर सकते हैं[यहाँ](https://purchase.aspose.com/temporary-license/).

### Q5: मुझे .NET के लिए Aspose.OCR का दस्तावेज़ कहां मिल सकता है?

 A5: दस्तावेज़ उपलब्ध है[यहाँ](https://reference.aspose.com/ocr/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
