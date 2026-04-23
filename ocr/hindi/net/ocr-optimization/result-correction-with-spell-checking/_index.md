---
date: 2026-04-23
description: Aspose OCR for .NET के साथ OCR की सटीकता बढ़ाएँ, वर्तनी जांच, OCR भाषा
  पैक समर्थन और कस्टम शब्दकोशों का उपयोग करके स्कैन किए गए दस्तावेज़ों की OCR गुणवत्ता
  को सुधारें।
keywords:
- improve ocr accuracy
- ocr language pack
- process scanned documents
- boost ocr quality
- ocr spell checking
linktitle: छवियों में वर्तनी जांच के साथ OCR की सटीकता में सुधार करें
second_title: Aspose.OCR .NET API
title: छवियों में वर्तनी जाँच के साथ OCR की सटीकता में सुधार
url: /hi/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# छवियों में स्पेल चेकिंग के साथ OCR सटीकता में सुधार

जब आप ऑप्टिकल कैरेक्टर रिकग्निशन (OCR) के साथ काम करते हैं, तो अंतिम लक्ष्य **OCR सटीकता में सुधार** करना है ताकि निकाला गया टेक्स्ट मूल छवि से पूरी तरह मेल खाए। गलत वर्तनी वाले शब्द, शोरयुक्त पृष्ठभूमि, और असामान्य फ़ॉन्ट सामान्य कारण हैं जो परिणाम को घटाते हैं। Aspose.OCR के बिल्ट‑इन स्पेल‑चेकिंग इंजन को उसके व्यापक OCR भाषा पैक के साथ जोड़कर, आप किसी भी स्कैन किए गए दस्तावेज़ के लिए **OCR गुणवत्ता में वृद्धि** कर सकते हैं।

## स्पेल चेकिंग के साथ OCR सटीकता में सुधार कैसे करें

इस सेक्शन में हम पूरी कार्यप्रवाह को देखेंगे—छवि लोड करने से लेकर स्पेल चेकिंग लागू करने तक और अंत में एक कस्टम यूज़र डिक्शनरी के साथ आउटपुट को परिपूर्ण करेंगे। आप वास्तविक‑विश्व के पहले‑और‑बाद के नमूने देखेंगे, समझेंगे कि स्कैन किए गए दस्तावेज़ों की प्रोसेसिंग में यह क्यों महत्वपूर्ण है, और OCR स्पेल‑चेकिंग फीचर से अधिकतम लाभ पाने के टिप्स खोजेंगे।

## त्वरित उत्तर
- **स्पेल चेकिंग OCR के लिए क्या करती है?** यह OCR आउटपुट में गलत वर्तनी वाले शब्दों का स्वतः पता लगाती है और उन्हें सबसे संभावित सही विकल्पों से बदल देती है।  
- **कौन सी लाइब्रेरी यह फीचर प्रदान करती है?** Aspose.OCR for .NET में एक तैयार‑उपयोग स्पेल‑चेकिंग API शामिल है।  
- **क्या मुझे इंटरनेट कनेक्शन की आवश्यकता है?** नहीं, स्पेल‑चेकिंग इंजन पूरी तरह ऑफ़लाइन काम करता है।  
- **क्या मैं अपनी शब्दावली जोड़ सकता हूँ?** हाँ, आप डोमेन‑विशिष्ट शब्दों को संभालने के लिए एक कस्टम यूज़र डिक्शनरी प्रदान कर सकते हैं।  
- **कौन सी भाषाएँ समर्थित हैं?** विवरण के लिए “aspose ocr language support” सेक्शन देखें।

## OCR में स्पेल चेकिंग क्या है?

स्पेल चेकिंग OCR इंजन द्वारा लौटाए गए कच्चे टेक्स्ट की जाँच करती है, उन टोकनों की पहचान करती है जो चयनित भाषा शब्दकोश में ज्ञात शब्दों से मेल नहीं खाते, और सुधार सुझाती या लागू करती है। यह चरण **OCR सटीकता में सुधार** के लिए आवश्यक है, विशेष रूप से स्कैन किए गए दस्तावेज़ों, रसीदों, या फॉर्म्स को प्रोसेस करते समय जहाँ OCR अक्षरों को गलत समझ सकता है।

## Aspose OCR भाषा पैक का उपयोग क्यों करें?

Aspose.OCR व्यापक भाषा पैकों के साथ आता है और आपको अतिरिक्त शब्दकोश जोड़ने की अनुमति देता है। **aspose ocr language support** का उपयोग करने का मतलब है कि आप कस्टम पार्सर लिखे बिना बहुभाषी दस्तावेज़ों को संभाल सकते हैं, और आपको भाषा‑विशिष्ट नियमों तक पहुंच मिलती है जो पहचान की गुणवत्ता को और बेहतर बनाते हैं।

## आवश्यकताएँ

स्पेल‑चेकिंग जादू में डुबने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित आवश्यकताएँ मौजूद हैं:

- Aspose.OCR for .NET लाइब्रेरी: Aspose.OCR लाइब्रेरी को [release page](https://releases.aspose.com/ocr/net/) से डाउनलोड और इंस्टॉल करें।
- दस्तावेज़ डायरेक्टरी: सुनिश्चित करें कि आपके पास अपने दस्तावेज़ों के लिए एक निर्दिष्ट डायरेक्टरी है। कोड स्निपेट्स में `"Your Document Directory"` को वास्तविक पथ से बदलें।

## नेमस्पेस इम्पोर्ट करें

आइए अपने .NET प्रोजेक्ट में आवश्यक नेमस्पेस इम्पोर्ट करके शुरू करें:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## चरण 1: Aspose.OCR को इनिशियलाइज़ करें

OCR प्रक्रिया को शुरू करने के लिए Aspose.OCR का एक इंस्टेंस इनिशियलाइज़ करें।

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## चरण 2: इमेज को पहचानें

अब, Aspose.OCR का उपयोग करके छवि में टेक्स्ट को पहचानें। यहाँ इस प्रक्रिया को दर्शाने वाला एक स्निपेट है:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## चरण 3: सुधार से पहले

सुधारित संस्करण से तुलना करने के लिए सुधार से पहले OCR परिणाम प्राप्त करें।

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## चरण 4: सुधार के बाद

स्पेल चेकिंग लागू करके सुधारा हुआ परिणाम प्राप्त करें। निम्नलिखित कोड स्निपेट इस चरण को दर्शाता है:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## चरण 5: गलत वर्तनी वाले शब्द और सुझाव

निम्नलिखित कोड का उपयोग करके गलत वर्तनी वाले शब्दों की सूची और सुझाए गए सुधार प्राप्त करें:

```csharp
// Get list of misspelled words with suggestions
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

## चरण 6: उपयोगकर्ता टेक्स्ट को सुधारें

Aspose.OCR लाइब्रेरी का उपयोग करके विशिष्ट उपयोगकर्ता‑प्रदान किए गए टेक्स्ट को सुधारें:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## चरण 7: यूज़र डिक्शनरी के साथ सुधार

एक कस्टम यूज़र डिक्शनरी को शामिल करके सुधार को और बेहतर बनाएं:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## OCR गुणवत्ता बढ़ाने के टिप्स
- **सही OCR भाषा पैक चुनें** जो स्रोत दस्तावेज़ से मेल खाता हो। फ्रेंच दस्तावेज़ पर `Language.Eng` का उपयोग करने से सटीकता में काफी कमी आएगी।  
- **छवियों को पूर्व‑प्रसंस्करण करें** (डेस्क्यू, डिनॉइज़, कंट्रास्ट बढ़ाएँ) OCR इंजन को देने से पहले; साफ़ छवियां कम गलत वर्तनी उत्पन्न करती हैं।  
- **एक संक्षिप्त यूज़र डिक्शनरी रखें**—प्रति पंक्ति एक शब्द—ताकि स्पेल चेकर कस्टम शब्दों को जल्दी ढूंढ सके और बड़े बैचों को धीमा न करे।  
- **पृष्ठों को बैच में प्रोसेस करें** जब मल्टी‑पेज PDFs को संभाल रहे हों; यह मेमोरी उपयोग को कम करता है और स्पेल‑चेकिंग चरण को तेज़ करता है।

## सामान्य समस्याएँ और समाधान

| समस्या | कारण | समाधान |
|-------|----------------|------------|
| कोई सुझाव नहीं मिला | भाषा पैक लोड नहीं है या टेक्स्ट बहुत छोटा है। | सुनिश्चित करें कि `RecognitionSettings(Language.Eng)` स्रोत छवि की भाषा से मेल खाता हो और OCR परिणाम में पर्याप्त अक्षर हों। |
| कस्टम शब्दकोश लागू नहीं हुआ | गलत पथ या फ़ाइल फ़ॉर्मेट। | जाँचें कि `dictionary.txt` निर्दिष्ट स्थान पर मौजूद है और प्रति पंक्ति एक शब्द का उपयोग करता है। |
| स्पेल चेकर बड़े दस्तावेज़ों में धीमा हो जाता है | प्रत्येक शब्द को अलग‑अलग प्रोसेस करने से ओवरहेड बढ़ता है। | पृष्ठों को बैच में प्रोसेस करें या .NET Core पर चलाते समय मेमोरी आवंटन बढ़ाएँ। |

## अक्सर पूछे जाने वाले प्रश्न

### प्रश्न 1: क्या मैं Aspose.OCR को अंग्रेज़ी के अलावा अन्य भाषाओं के लिए उपयोग कर सकता हूँ?
A1: हाँ, Aspose.OCR कई भाषाओं को समर्थन देता है। भाषा सेटिंग्स को उसी अनुसार समायोजित करें।

### प्रश्न 2: मैं Aspose.OCR को अपने .NET प्रोजेक्ट में कैसे इंटीग्रेट करूँ?
A2: विस्तृत इंटीग्रेशन चरणों के लिए [documentation](https://reference.aspose.com/ocr/net/) देखें।

### प्रश्न 3: क्या Aspose.OCR के लिए कोई ट्रायल संस्करण उपलब्ध है?
A3: हाँ, आप फीचर्स को [free trial version](https://releases.aspose.com/) के साथ एक्सप्लोर कर सकते हैं।

### प्रश्न 4: क्या मैं स्पेल चेकिंग के लिए कस्टम शब्दकोश अपलोड कर सकता हूँ?
A4: बिल्कुल! ट्यूटोरियल दिखाता है कि कैसे यूज़र‑प्रदान किए गए शब्दकोश का उपयोग करके सुधार को बढ़ाया जा सकता है।

### प्रश्न 5: मैं Aspose.OCR के लिए समर्थन कहाँ प्राप्त कर सकता हूँ?
A5: समुदाय समर्थन और मार्गदर्शन के लिए [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) पर जाएँ।

---

**अंतिम अपडेट:** 2026-04-23  
**परीक्षण किया गया:** Aspose.OCR for .NET latest version  
**लेखक:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}