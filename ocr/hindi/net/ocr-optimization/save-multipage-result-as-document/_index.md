---
title: मल्टीपेज परिणाम को ओसीआर छवि पहचान में दस्तावेज़ के रूप में सहेजें
linktitle: मल्टीपेज परिणाम को ओसीआर छवि पहचान में दस्तावेज़ के रूप में सहेजें
second_title: Aspose.OCR .NET एपीआई
description: .NET के लिए Aspose.OCR की क्षमता को अनलॉक करें। इस व्यापक चरण-दर-चरण मार्गदर्शिका के साथ बहुपृष्ठ OCR परिणामों को दस्तावेज़ के रूप में सहजता से सहेजें।
weight: 14
url: /hi/net/ocr-optimization/save-multipage-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# मल्टीपेज परिणाम को ओसीआर छवि पहचान में दस्तावेज़ के रूप में सहेजें

## परिचय

.NET के लिए Aspose.OCR का उपयोग करके ऑप्टिकल कैरेक्टर रिकग्निशन (OCR) की आकर्षक दुनिया में आपका स्वागत है! इस ट्यूटोरियल में, हम यह पता लगाएंगे कि बहुपृष्ठ OCR परिणामों को दस्तावेज़ों के रूप में सहेजने के लिए Aspose.OCR की क्षमताओं का उपयोग कैसे किया जाए। चाहे आप एक अनुभवी डेवलपर हों या सिर्फ ओसीआर से शुरुआत कर रहे हों, यह मार्गदर्शिका आपको प्रत्येक चरण में ले जाएगी, यह सुनिश्चित करते हुए कि आप इस शक्तिशाली टूल से अधिकतम लाभ उठा सकें।

## आवश्यक शर्तें

इससे पहले कि हम ट्यूटोरियल में उतरें, आइए सुनिश्चित करें कि आपने सब कुछ सेट कर लिया है:

1.  .NET के लिए Aspose.OCR इंस्टॉल करें: .NET के लिए Aspose.OCR को डाउनलोड और इंस्टॉल करके शुरुआत करें। आप आवश्यक फ़ाइलें पा सकते हैं[यहाँ](https://releases.aspose.com/ocr/net/).

2.  अपना निःशुल्क परीक्षण या लाइसेंस प्राप्त करें: यदि आपने पहले से नहीं किया है, तो आप निःशुल्क परीक्षण प्राप्त कर सकते हैं[यहाँ](https://releases.aspose.com/) या लाइसेंस खरीदें[यहाँ](https://purchase.aspose.com/buy).

3.  दस्तावेज़ीकरण का अन्वेषण करें: अपने आप को इससे परिचित कराएं[प्रलेखन](https://reference.aspose.com/ocr/net/).NET के लिए Aspose.OCR के लिए। विस्तृत जानकारी के लिए यह आपका पसंदीदा संसाधन है।

4.  सहायता फ़ोरम तक पहुंचें: यदि आपको कोई समस्या आती है या आपके कोई प्रश्न हैं, तो[समर्थन मंच](https://forum.aspose.com/c/ocr/16) एक मूल्यवान सामुदायिक संसाधन हैं।

अब जब आप पूरी तरह तैयार हो गए हैं, तो आइए चरण-दर-चरण मार्गदर्शिका देखें।

## नामस्थान आयात करें

आवश्यक नामस्थान आयात करके अपना प्रोजेक्ट शुरू करें:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

## चरण 1: अपनी दस्तावेज़ निर्देशिका सेट करें

```csharp
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "Your Document Directory";
```

 प्रतिस्थापित करना सुनिश्चित करें`"Your Document Directory"` आपकी दस्तावेज़ निर्देशिका के वास्तविक पथ के साथ।

## चरण 2: Aspose.OCR को आरंभ करें

```csharp
// AsposeOcr का एक उदाहरण प्रारंभ करें
AsposeOcr api = new AsposeOcr();
```

 का एक उदाहरण बनाएं`AsposeOcr` OCR कार्यक्षमताओं तक पहुँचने के लिए।

## चरण 3: छवियों को पहचानें

```csharp
// छवि पहचानो
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

एकाधिक छवियों से पाठ को पहचानने के लिए Aspose.OCR का उपयोग करें। अपनी छवि फ़ाइलों के अनुसार फ़ाइल पथ समायोजित करें।

## चरण 4: पसंदीदा प्रारूपों में परिणाम सहेजें

```csharp
// परिणाम को अपने पसंदीदा प्रारूप में सहेजें
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

अपना इच्छित प्रारूप (Docx, Text, Pdf, या XLsx) चुनें और OCR परिणामों को एक बहुपृष्ठ दस्तावेज़ के रूप में सहेजें।

## निष्कर्ष

बधाई हो! आपने सफलतापूर्वक सीख लिया है कि .NET के लिए Aspose.OCR का उपयोग करके मल्टीपेज OCR परिणामों को दस्तावेज़ों के रूप में कैसे सहेजा जाए। यह बहुमुखी उपकरण आपकी परियोजनाओं में पाठ पहचान के लिए संभावनाओं की दुनिया खोलता है।

## अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या परीक्षण उद्देश्यों के लिए अस्थायी लाइसेंस उपलब्ध है?

 उ1: हां, आप अस्थायी लाइसेंस प्राप्त कर सकते हैं[यहाँ](https://purchase.aspose.com/temporary-license/) Aspose.OCR के परीक्षण के लिए।

### Q2: क्या मैं विभिन्न प्रारूपों में छवियों से पाठ को पहचान सकता हूँ?

ए2: बिल्कुल! Aspose.OCR आपके OCR कार्यों में लचीलापन सुनिश्चित करते हुए विभिन्न छवि प्रारूपों का समर्थन करता है।

### Q3: क्या पहचान के लिए छवियों की संख्या पर कोई सीमाएँ हैं?

उ3: आप कितनी छवियों को संसाधित कर सकते हैं यह आपके लाइसेंस पर निर्भर करता है। विवरण के लिए दस्तावेज़ की जाँच करें.

### Q4: मैं OCR पहचान के दौरान त्रुटियों को कैसे संभाल सकता हूँ?

A4: त्रुटि प्रबंधन की सर्वोत्तम प्रथाओं के लिए दस्तावेज़ देखें या सहायता फ़ोरम में सहायता लें।

### Q5: क्या Aspose.OCR अंग्रेजी के अलावा अन्य भाषाओं का समर्थन करता है?

A5: हां, Aspose.OCR कई भाषाओं का समर्थन करता है। भाषा समर्थन विवरण के लिए दस्तावेज़ देखें।
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
