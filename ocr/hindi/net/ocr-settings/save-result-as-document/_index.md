---
title: परिणाम को OCR छवि पहचान में दस्तावेज़ के रूप में सहेजें
linktitle: परिणाम को OCR छवि पहचान में दस्तावेज़ के रूप में सहेजें
second_title: Aspose.OCR .NET एपीआई
description: .NET के लिए Aspose.OCR की क्षमता को अनलॉक करें। छवियों में टेक्स्ट को आसानी से पहचानें और परिणामों को विभिन्न दस्तावेज़ प्रारूपों में सहेजें।
weight: 10
url: /hi/net/ocr-settings/save-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# परिणाम को OCR छवि पहचान में दस्तावेज़ के रूप में सहेजें

## परिचय

.NET के लिए Aspose.OCR के साथ ऑप्टिकल कैरेक्टर रिकग्निशन (OCR) की रोमांचक दुनिया में आपका स्वागत है! इस व्यापक ट्यूटोरियल में, हम छवियों में टेक्स्ट को पहचानने के लिए Aspose.OCR का उपयोग करने की जटिलताओं को समझेंगे और प्रदर्शित करेंगे कि परिणामों को विभिन्न दस्तावेज़ प्रारूपों के रूप में कैसे सहेजा जाए।

## आवश्यक शर्तें

इससे पहले कि हम इस ओसीआर यात्रा को शुरू करें, सुनिश्चित करें कि आपके पास निम्नलिखित शर्तें हैं:

-  .NET के लिए Aspose.OCR. सुनिश्चित करें कि आपके पास Aspose.OCR लाइब्रेरी स्थापित है। आप इसे डाउनलोड कर सकते हैं[यहाँ](https://releases.aspose.com/ocr/net/).

-  दस्तावेज़ निर्देशिका: अपने दस्तावेज़ों के लिए एक निर्दिष्ट निर्देशिका रखें, और उसे अद्यतन करें`dataDir` तदनुसार दिए गए कोड में परिवर्तनीय।

## नामस्थान आयात करें

आवश्यक नामस्थान आयात करके प्रारंभ करें। ये बिल्डिंग ब्लॉक्स हैं जो आपके कोड को ओसीआर क्षमताओं के साथ सशक्त बनाएंगे।

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

अब, आइए उदाहरण को कई चरणों में विभाजित करें:

## चरण 1: Aspose.OCR को आरंभ करें

```csharp
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "Your Document Directory";

// AsposeOcr का एक उदाहरण प्रारंभ करें
AsposeOcr api = new AsposeOcr();
```

यह चरण Aspose.OCR API को प्रारंभ करके चरण निर्धारित करता है।

## चरण 2: छवि को पहचानें

```csharp
// छवि पहचानो
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

यहां, हम निर्दिष्ट छवि के भीतर पाठ को पहचानने के लिए Aspose.OCR का उपयोग करते हैं ("sample.png" को अपनी छवि फ़ाइल से बदलें)।

## चरण 3: परिणाम को विभिन्न प्रारूपों में सहेजें

```csharp
// परिणाम को अपने पसंदीदा प्रारूप में सहेजें
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

अपनी आवश्यकताओं के आधार पर इस चरण को अनुकूलित करें। Aspose.OCR आपको मान्यता प्राप्त टेक्स्ट को DOCX, TXT, PDF और XLSX जैसे विभिन्न दस्तावेज़ प्रारूपों में सहेजने की अनुमति देता है।

## चरण 4: सफलता संदेश प्रदर्शित करें

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

आपको यह बताने के लिए एक सरल पुष्टिकरण संदेश कि प्रक्रिया बिना किसी रुकावट के पूरी हो गई।

इन चरणों का पालन करके, आपने छवियों के भीतर पाठ को पहचानने और विभिन्न दस्तावेज़ प्रारूपों में परिणामों को सहेजने में .NET के लिए Aspose.OCR की शक्ति का सफलतापूर्वक उपयोग किया है।

## निष्कर्ष

अंत में, .NET के लिए Aspose.OCR छवियों में पाठ पहचान के लिए संभावनाओं की दुनिया खोलता है। चाहे आप डेटा निकाल रहे हों या खोजने योग्य दस्तावेज़ बना रहे हों, Aspose.OCR अपने सहज एपीआई के साथ प्रक्रिया को सरल बनाता है।

## अक्सर पूछे जाने वाले प्रश्न

### Q1. क्या Aspose.OCR विभिन्न छवि प्रारूपों के साथ संगत है?

A1: हाँ, Aspose.OCR आपके OCR कार्यों में लचीलापन सुनिश्चित करते हुए, छवि प्रारूपों की एक विस्तृत श्रृंखला का समर्थन करता है।

### Q2: क्या मैं बेहतर सटीकता के लिए पहचान सेटिंग्स को अनुकूलित कर सकता हूँ?

ए2: बिल्कुल! Aspose.OCR आपकी विशिष्ट आवश्यकताओं के अनुसार OCR प्रक्रिया को बेहतर बनाने के लिए पहचान सेटिंग्स प्रदान करता है।

### Q3: क्या कोई निःशुल्क परीक्षण उपलब्ध है?

 उ3: हाँ, आप निःशुल्क परीक्षण के साथ शुरुआत कर सकते हैं[यहाँ](https://releases.aspose.com/).

### Q4: मैं Aspose.OCR के लिए अस्थायी लाइसेंस कैसे प्राप्त कर सकता हूं?

 A4: अस्थायी लाइसेंस प्राप्त किया जा सकता है[यहाँ](https://purchase.aspose.com/temporary-license/).

### Q5: मैं कहां से सहायता मांग सकता हूं या समुदाय से जुड़ सकता हूं?

 A5: Aspose.OCR समुदाय में शामिल हों[एस्पोज़ फोरम](https://forum.aspose.com/c/ocr/16) समर्थन और चर्चा के लिए.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
