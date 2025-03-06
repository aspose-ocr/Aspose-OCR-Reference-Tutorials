---
title: ओसीआर छवि पहचान में वर्तनी जांच के साथ परिणाम सुधार
linktitle: ओसीआर छवि पहचान में वर्तनी जांच के साथ परिणाम सुधार
second_title: Aspose.OCR .NET एपीआई
description: .NET के लिए Aspose.OCR के साथ OCR सटीकता बढ़ाएँ। वर्तनी को सही करें, शब्दकोशों को अनुकूलित करें और त्रुटि रहित पाठ पहचान को सहजता से प्राप्त करें।
weight: 13
url: /hi/net/ocr-optimization/result-correction-with-spell-checking/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ओसीआर छवि पहचान में वर्तनी जांच के साथ परिणाम सुधार

## परिचय

ऑप्टिकल कैरेक्टर रिकॉग्निशन (ओसीआर) के क्षेत्र में, छवियों से सार्थक जानकारी निकालने के लिए सटीक परिणाम प्राप्त करना महत्वपूर्ण है। एक आम चुनौती पहचान प्रक्रिया में गलत वर्तनी वाले शब्दों से निपटना है। सौभाग्य से, .NET के लिए Aspose.OCR वर्तनी जाँच के माध्यम से OCR परिणामों को बढ़ाने के लिए एक शक्तिशाली समाधान प्रदान करता है।

यह ट्यूटोरियल आपको .NET के लिए Aspose.OCR का उपयोग करके वर्तनी जांच के साथ परिणाम सुधार की प्रक्रिया में मार्गदर्शन करेगा। अंत तक, आप अधिक परिष्कृत और त्रुटि-मुक्त आउटपुट सुनिश्चित करते हुए, ओसीआर-व्युत्पन्न पाठ की सटीकता में सुधार करने में सक्षम होंगे।

## आवश्यक शर्तें

इससे पहले कि हम वर्तनी जांच जादू में उतरें, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:

-  .NET लाइब्रेरी के लिए Aspose.OCR: Aspose.OCR लाइब्रेरी को डाउनलोड और इंस्टॉल करें[रिलीज पेज](https://releases.aspose.com/ocr/net/).

- दस्तावेज़ निर्देशिका: सुनिश्चित करें कि आपके पास अपने दस्तावेज़ों के लिए एक निर्दिष्ट निर्देशिका है। कोड स्निपेट में "आपकी दस्तावेज़ निर्देशिका" को वास्तविक पथ से बदलें।

## नामस्थान आयात करें

आइए आपके .NET प्रोजेक्ट में आवश्यक नेमस्पेस आयात करके शुरुआत करें:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## चरण 1: Aspose.OCR को आरंभ करें

OCR प्रक्रिया को किकस्टार्ट करने के लिए Aspose.OCR का एक उदाहरण प्रारंभ करें।

```csharp
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "Your Document Directory";

// AsposeOcr का एक उदाहरण प्रारंभ करें
AsposeOcr api = new AsposeOcr();
```

## चरण 2: छवि को पहचानें

इसके बाद, Aspose.OCR का उपयोग करके छवि में टेक्स्ट को पहचानें। इस प्रक्रिया को प्रदर्शित करने वाला एक स्निपेट यहां दिया गया है:

```csharp
// छवि पहचानो
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## चरण 3: सुधार से पहले

संशोधित संस्करण के साथ तुलना करने के लिए सुधार से पहले ओसीआर परिणाम पुनः प्राप्त करें।

```csharp
// परिणाम प्राप्त करें
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## चरण 4: सुधार के बाद

सही परिणाम प्राप्त करने के लिए वर्तनी जाँच लागू करें। निम्नलिखित कोड स्निपेट इस चरण को दर्शाता है:

```csharp
// सही परिणाम प्राप्त करें
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## चरण 5: गलत वर्तनी वाले शब्द और सुझाव

निम्नलिखित कोड का उपयोग करके सुझाए गए सुधारों के साथ गलत वर्तनी वाले शब्दों की सूची प्राप्त करें:

```csharp
// सुझावों के साथ गलत वर्तनी वाले शब्दों की सूची प्राप्त करें
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## चरण 6: उपयोगकर्ता पाठ को सही करें

Aspose.OCR लाइब्रेरी का उपयोग करके उपयोगकर्ता द्वारा प्रदत्त विशिष्ट पाठ को सही करें:

```csharp
// सही उपयोगकर्ता पाठ
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## चरण 7: उपयोगकर्ता शब्दकोश के साथ सुधार

एक कस्टम उपयोगकर्ता शब्दकोश को शामिल करके सुधार को और बढ़ाएं:

```csharp
// उपयोगकर्ता शब्दकोश के साथ सही परिणाम प्राप्त करें
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## निष्कर्ष

बधाई हो! आपने .NET के लिए Aspose.OCR की वर्तनी-जांच क्षमताओं को सफलतापूर्वक नेविगेट कर लिया है। यह सुविधा आपको OCR परिणामों को परिष्कृत करने, सटीकता सुनिश्चित करने और त्रुटियों को दूर करने का अधिकार देती है।

## अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या मैं अंग्रेजी के अलावा अन्य भाषाओं के लिए Aspose.OCR का उपयोग कर सकता हूँ?

A1: हां, Aspose.OCR कई भाषाओं का समर्थन करता है। भाषा सेटिंग्स को तदनुसार समायोजित करें।

### Q2: मैं Aspose.OCR को अपने .NET प्रोजेक्ट में कैसे एकीकृत करूं?

 A2: देखें[प्रलेखन](https://reference.aspose.com/ocr/net/) विस्तृत एकीकरण चरणों के लिए.

### Q3: क्या Aspose.OCR के लिए कोई परीक्षण संस्करण उपलब्ध है?

 उ3: हां, आप इसके साथ सुविधाओं का पता लगा सकते हैं[निःशुल्क परीक्षण संस्करण](https://releases.aspose.com/).

### Q4: क्या मैं वर्तनी जाँच के लिए एक कस्टम शब्दकोश अपलोड कर सकता हूँ?

उ4: बिल्कुल! ट्यूटोरियल दर्शाता है कि उपयोगकर्ता द्वारा प्रदत्त शब्दकोश का उपयोग करके सुधार कैसे बढ़ाया जाए।

### Q5: मैं Aspose.OCR के लिए समर्थन कहाँ से प्राप्त कर सकता हूँ?

 A5: पर जाएँ[Aspose.OCR फोरम](https://forum.aspose.com/c/ocr/16) सामुदायिक समर्थन और मार्गदर्शन के लिए।
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
