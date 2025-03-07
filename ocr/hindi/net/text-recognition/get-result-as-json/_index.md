---
title: OCR छवि पहचान में JSON के रूप में परिणाम प्राप्त करें
linktitle: OCR छवि पहचान में JSON के रूप में परिणाम प्राप्त करें
second_title: Aspose.OCR .NET एपीआई
description: .NET के लिए Aspose.OCR की शक्ति को उजागर करें। JSON प्रारूप में OCR परिणाम सहजता से प्राप्त करना सीखें। इस चरण-दर-चरण मार्गदर्शिका के साथ अपनी छवि पहचान बढ़ाएँ।
weight: 12
url: /hi/net/text-recognition/get-result-as-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR छवि पहचान में JSON के रूप में परिणाम प्राप्त करें

## परिचय

प्रौद्योगिकी के लगातार विकसित हो रहे परिदृश्य में, ऑप्टिकल कैरेक्टर रिकॉग्निशन (ओसीआर) एक महत्वपूर्ण उपकरण के रूप में खड़ा है, जो मशीनों को छवियों की व्याख्या करने और जानकारी निकालने में सक्षम बनाता है। .NET के लिए Aspose.OCR डेवलपर्स को OCR क्षमताओं को उनके अनुप्रयोगों में निर्बाध रूप से एकीकृत करने का अधिकार देता है। यह ट्यूटोरियल आपको .NET के लिए Aspose.OCR का उपयोग करके JSON प्रारूप में OCR परिणाम प्राप्त करने की प्रक्रिया में मार्गदर्शन करेगा।

## आवश्यक शर्तें

ट्यूटोरियल में गहराई से जाने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित आवश्यक शर्तें हैं:

- विजुअल स्टूडियो: सुनिश्चित करें कि आपके सिस्टम पर विजुअल स्टूडियो स्थापित है।
-  .NET के लिए Aspose.OCR: से लाइब्रेरी डाउनलोड और इंस्टॉल करें[.NET दस्तावेज़ीकरण के लिए Aspose.OCR](https://reference.aspose.com/ocr/net/).

## नामस्थान आयात करें

एकीकरण शुरू करने के लिए, आवश्यक नामस्थान आयात करें:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## चरण 1: अपनी दस्तावेज़ निर्देशिका सेट करें

अपनी दस्तावेज़ निर्देशिका का पथ परिभाषित करके प्रारंभ करें:

```csharp
string dataDir = "Your Document Directory";
```

## चरण 2: Aspose.OCR को आरंभ करें

इसकी कार्यक्षमता का लाभ उठाने के लिए Aspose.OCR का एक उदाहरण त्वरित करें:

```csharp
AsposeOcr api = new AsposeOcr();
```

## चरण 3: छवि को पहचानें

किसी छवि के भीतर टेक्स्ट को पहचानने के लिए OCR इंजन का उपयोग करें:

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

## चरण 4: JSON में पहचान परिणाम प्रदर्शित करें

JSON प्रारूप में मान्यता परिणाम प्रदर्शित करें:

```csharp
Console.WriteLine(result.GetJson());
```

## चरण 5: निष्पादन को अंतिम रूप दें

एक सफलता संदेश के साथ प्रक्रिया समाप्त करें:

```csharp
Console.WriteLine("GetResultAsJson executed successfully");
```

## निष्कर्ष

.NET के लिए Aspose.OCR आपके अनुप्रयोगों में OCR क्षमताओं के एकीकरण को सुव्यवस्थित करता है। इस चरण-दर-चरण मार्गदर्शिका का पालन करके, आप आसानी से JSON प्रारूप में OCR परिणाम प्राप्त कर सकते हैं, जिससे आपकी छवि पहचान वर्कफ़्लो की दक्षता बढ़ जाएगी।

## अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या .NET के लिए Aspose.OCR का निःशुल्क परीक्षण उपलब्ध है?

 उ1: हाँ, आप निःशुल्क परीक्षण का उपयोग कर सकते हैं[यहाँ](https://releases.aspose.com/).

### Q2. मुझे .NET के लिए Aspose.OCR का दस्तावेज़ कहाँ मिल सकता है?

 A2: दस्तावेज़ उपलब्ध है[यहाँ](https://reference.aspose.com/ocr/net/).

### Q3. मैं .NET के लिए Aspose.OCR के लिए अस्थायी लाइसेंस कैसे प्राप्त कर सकता हूं?

 ए3: विजिट करें[इस लिंक](https://purchase.aspose.com/temporary-license/) अस्थायी लाइसेंस विकल्पों के लिए.

### Q4. मुझे .NET के लिए Aspose.OCR के लिए सामुदायिक समर्थन कहां मिल सकता है?

 ए4: समुदाय के साथ जुड़ें[Aspose.OCR फोरम](https://forum.aspose.com/c/ocr/16).

### Q5: क्या मैं .NET के लिए Aspose.OCR का लाइसेंस खरीद सकता हूँ?

 A5: हाँ, आप लाइसेंस खरीद सकते हैं[यहाँ](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
