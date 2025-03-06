---
title: ओसीआर छवि पहचान में भाषा चयन के साथ ओसीआरऑपरेशन
linktitle: ओसीआर छवि पहचान में भाषा चयन के साथ ओसीआरऑपरेशन
second_title: Aspose.OCR .NET एपीआई
description: .NET के लिए Aspose.OCR के साथ शक्तिशाली OCR क्षमताओं को अनलॉक करें। छवियों से पाठ को निर्बाध रूप से निकालें।
weight: 12
url: /hi/net/ocr-configuration/ocr-operation-with-language-selection/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ओसीआर छवि पहचान में भाषा चयन के साथ ओसीआरऑपरेशन

## परिचय

छवि पहचान और ऑप्टिकल कैरेक्टर रिकग्निशन (ओसीआर) की दुनिया में, .NET के लिए Aspose.OCR छवियों से सटीक और कुशल पाठ निष्कर्षण चाहने वाले डेवलपर्स के लिए एक शक्तिशाली उपकरण के रूप में सामने आता है। यह चरण-दर-चरण मार्गदर्शिका आपको .NET के लिए Aspose.OCR का उपयोग करके OCR छवि पहचान की प्रक्रिया के बारे में बताएगी, जो भाषा चयन के साथ संचालन पर ध्यान केंद्रित करेगी।

## आवश्यक शर्तें

इससे पहले कि हम ट्यूटोरियल में गहराई से जाएँ, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

-  .NET के लिए Aspose.OCR: सुनिश्चित करें कि आपके पास Aspose.OCR लाइब्रेरी स्थापित है। आप इसे यहां से डाउनलोड कर सकते हैं[.NET डाउनलोड पेज के लिए Aspose.OCR](https://releases.aspose.com/ocr/net/).

- विकास परिवेश: .NET एप्लिकेशन के साथ कार्यशील वातावरण स्थापित करें। यदि आपने अभी तक ऐसा नहीं किया है, तो देखें[प्रलेखन](https://reference.aspose.com/ocr/net/) विस्तृत निर्देशों के लिए.

## नामस्थान आयात करें

अपने .NET एप्लिकेशन में, आवश्यक नामस्थान आयात करके प्रारंभ करें:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## चरण 1: Aspose.OCR को आरंभ करें

Aspose.OCR वर्ग का एक उदाहरण प्रारंभ करके प्रारंभ करें। यह आपके एप्लिकेशन के भीतर OCR क्षमताओं के उपयोग के लिए मंच तैयार करता है।

```csharp
// एक्सस्टार्ट:1
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "Your Document Directory";

// AsposeOcr का एक उदाहरण प्रारंभ करें
AsposeOcr api = new AsposeOcr();
```

## चरण 2: छवि पथ निर्दिष्ट करें

इसके बाद, उस छवि का पथ परिभाषित करें जिस पर आप OCR करना चाहते हैं। सुनिश्चित करें कि छवि आपके एप्लिकेशन से पहुंच योग्य है।

```csharp
//छवि पथ
string fullPath = dataDir + "sample.png";
```

## चरण 3: भाषा चयन के साथ छवि को पहचानें

अब आता है कोर ओसीआर ऑपरेशन। निर्दिष्ट छवि से पाठ को पहचानने के लिए Aspose.OCR लाइब्रेरी का उपयोग करें। भाषा चयन सहित पहचान सेटिंग्स समायोजित करें।

```csharp
// छवि पहचानो
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // भाषा चुनें: कोई नहीं, इंग्लैंड, देउ, पोर, स्पा, फ्रा, आईटीए, सीजे, डैन, डम, इस्ट, फिन, लव, लिट, न ही, पोल, रम, एसआरपी_एचआरवी, एसएलके, एसएलवी, स्वी, ची
});
```

## चरण 4: परिणाम प्रिंट करें और प्रदर्शित करें

ओसीआर ऑपरेशन के बाद, मान्यता प्राप्त पाठ, क्षेत्रों, चेतावनियों और JSON प्रतिनिधित्व सहित परिणामों को प्रिंट और प्रदर्शित करें।

```csharp
// परिणाम प्रिंट करें
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## निष्कर्ष

बधाई हो! आपने .NET के लिए Aspose.OCR का उपयोग करके भाषा चयन के साथ OCR छवि पहचान सफलतापूर्वक निष्पादित की है। इस ट्यूटोरियल ने छवियों से पाठ निकालने के लिए आवश्यक चरणों का प्रदर्शन किया और भाषा विकल्पों के लचीलेपन पर प्रकाश डाला।

## अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या Aspose.OCR बहुभाषी पाठ पहचान के लिए उपयुक्त है?

A1: हाँ, Aspose.OCR विभिन्न भाषाओं का समर्थन करता है, बहुभाषी OCR कार्यों के लिए लचीलापन प्रदान करता है।

### Q2: क्या मैं विशिष्ट छवि विशेषताओं के लिए OCR सेटिंग्स को ठीक कर सकता हूँ?

ए2: बिल्कुल! विभिन्न परिदृश्यों के लिए ओसीआर को अनुकूलित करने के लिए तिरछा कोण, रेखा पहचान और क्षेत्र का पता लगाने जैसे मापदंडों को समायोजित करें।

### Q3: मुझे अतिरिक्त सहायता या सामुदायिक चर्चाएँ कहाँ मिल सकती हैं?

 A3: पर जाएँ[Aspose.OCR फोरम](https://forum.aspose.com/c/ocr/16) समुदाय के साथ समर्थन और चर्चा के लिए।

### Q4: क्या कोई निःशुल्क परीक्षण उपलब्ध है?

 A4: हाँ, अन्वेषण करें[मुफ्त परीक्षण](https://releases.aspose.com/) Aspose.OCR की क्षमताओं का अनुभव करने के लिए।

### Q5: मैं .NET के लिए Aspose.OCR कैसे खरीद सकता हूँ?

 A5: खरीदने के लिए, पर जाएँ[खरीद पृष्ठ](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
