---
date: 2025-12-25
description: Aspose OCR for .NET के साथ OCR की सटीकता में सुधार करें, वर्तनी जांच
  और भाषा समर्थन का उपयोग करके त्रुटियों को ठीक करें और त्रुटि‑रहित टेक्स्ट पहचान
  के लिए शब्दकोश को अनुकूलित करें।
linktitle: Improve OCR Accuracy with Spell Checking in Images
second_title: Aspose.OCR .NET API
title: छवियों में वर्तनी जाँच के साथ OCR की सटीकता में सुधार
url: /hi/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज में स्पेल चेकिंग के साथ OCR सटीकता बढ़ाएँ

## परिचय

जब आप ऑप्टिकल कैरेक्टर रिकग्निशन (OCR) के साथ काम करते हैं, तो अंतिम लक्ष्य **OCR सटीकता में सुधार** करना होता है ताकि निकाला गया टेक्स्ट मूल इमेज से पूरी तरह मेल खाए। गलत वर्तनी वाले शब्द अक्सर त्रुटियों का स्रोत होते हैं, विशेषकर जब स्रोत इमेज शोरयुक्त हो या असामान्य फ़ॉन्ट्स हों। Aspose.OCR for .NET बिल्ट‑इन स्पेल‑चेकिंग क्षमताएँ प्रदान करता है जो न केवल उन गलतियों को सुधारती हैं बल्कि आपको कस्टम डिक्शनरी के साथ इंजन को विस्तारित करने की भी अनुमति देती हैं। इस ट्यूटोरियल में आप सीखेंगे कि स्पेल चेकिंग का उपयोग करके OCR परिणामों को कैसे बढ़ाया जाए, पहले‑और‑बाद के आउटपुट को देखें, और अपनी विशिष्ट भाषा आवश्यकताओं के अनुसार सुधार प्रक्रिया को कैसे अनुकूलित किया जाए।

## त्वरित उत्तर
- **स्पेल चेकिंग OCR के लिए क्या करती है?** यह OCR आउटपुट में गलत वर्तनी वाले शब्दों का स्वचालित रूप से पता लगाती है और उन्हें सबसे संभावित सही विकल्पों से बदल देती है।  
- **यह सुविधा कौन सी लाइब्रेरी प्रदान करती है?** Aspose.OCR for .NET में एक तैयार‑उपयोग स्पेल‑चेकिंग API शामिल है।  
- **क्या मुझे इंटरनेट कनेक्शन की आवश्यकता है?** नहीं, स्पेल‑चेकिंग इंजन पूरी तरह ऑफ़लाइन काम करता है।  
- **क्या मैं अपनी शब्दावली जोड़ सकता हूँ?** हाँ, आप डोमेन‑विशिष्ट शब्दों को संभालने के लिए एक कस्टम यूज़र डिक्शनरी प्रदान कर सकते हैं।  
- **कौन‑सी भाषाएँ समर्थित हैं?** विवरण के लिए “aspose ocr language support” सेक्शन देखें।

## OCR में स्पेल चेकिंग क्या है?

स्पेल चेकिंग OCR इंजन द्वारा लौटाए गए कच्चे टेक्स्ट की जाँच करती है, चयनित भाषा डिक्शनरी में ज्ञात शब्दों से मेल न खाने वाले टोकन की पहचान करती है, और सुधार सुझाती या लागू करती है। यह चरण **OCR सटीकता में सुधार** के लिए आवश्यक है, विशेषकर जब स्कैन किए गए दस्तावेज़, रसीदें या फ़ॉर्म प्रोसेस किए जा रहे हों जहाँ OCR अक्षरों को गलत समझ सकता है।

## Aspose OCR भाषा समर्थन का उपयोग क्यों करें?

Aspose.OCR विस्तृत भाषा पैक्स के साथ आता है और आपको अतिरिक्त डिक्शनरी जोड़ने की सुविधा देता है। **aspose ocr language support** का लाभ उठाने से आप बिना कस्टम पार्सर लिखे बहुभाषी दस्तावेज़ों को संभाल सकते हैं, और आपको भाषा‑विशिष्ट नियम मिलते हैं जो पहचान की गुणवत्ता को और बेहतर बनाते हैं।

## पूर्वापेक्षाएँ

स्पेल‑चेकिंग जादू में डुबने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

- Aspose.OCR for .NET लाइब्रेरी: Aspose.OCR लाइब्रेरी को [release page](https://releases.aspose.com/ocr/net/) से डाउनलोड और इंस्टॉल करें।

- दस्तावेज़ डायरेक्टरी: अपने दस्तावेज़ों के लिए एक निर्दिष्ट फ़ोल्डर सुनिश्चित करें। कोड स्निपेट्स में `"Your Document Directory"` को वास्तविक पथ से बदलें।

## नेमस्पेसेस इम्पोर्ट करें

आइए आपके .NET प्रोजेक्ट में आवश्यक नेमस्पेसेस इम्पोर्ट करके शुरू करते हैं:

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

अब, Aspose.OCR का उपयोग करके इमेज में टेक्स्ट को पहचानें। नीचे इस प्रक्रिया को दर्शाता एक स्निपेट है:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## चरण 3: सुधार से पहले

सुधार से पहले OCR परिणाम प्राप्त करें ताकि इसे सुधारे गए संस्करण से तुलना की जा सके।

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## चरण 4: सुधार के बाद

स्पेल चेकिंग लागू करके सुधारा गया परिणाम प्राप्त करें। निम्नलिखित कोड स्निपेट इस चरण को दर्शाता है:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## चरण 5: गलत वर्तनी वाले शब्द और सुझाव

निम्नलिखित कोड का उपयोग करके गलत वर्तनी वाले शब्दों की सूची और उनके सुझाए गए सुधार प्राप्त करें:

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

## चरण 7: उपयोगकर्ता डिक्शनरी के साथ सुधार

कस्टम यूज़र डिक्शनरी को शामिल करके सुधार को और बेहतर बनाएं:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## सामान्य समस्याएँ और समाधान

| समस्या | क्यों होती है | समाधान |
|-------|----------------|------------|
| कोई सुझाव नहीं मिलता | भाषा पैक लोड नहीं हुआ है या टेक्स्ट बहुत छोटा है। | सुनिश्चित करें कि `RecognitionSettings(Language.Eng)` स्रोत इमेज की भाषा से मेल खाता हो और OCR परिणाम में पर्याप्त अक्षर हों। |
| कस्टम डिक्शनरी लागू नहीं हुई | पथ गलत है या फ़ाइल फ़ॉर्मेट गलत है। | पुष्टि करें कि `dictionary.txt` निर्दिष्ट स्थान पर मौजूद है और प्रत्येक पंक्ति में एक शब्द है। |
| बड़े दस्तावेज़ों पर स्पेल चेकर धीमा हो जाता है | प्रत्येक शब्द को अलग‑अलग प्रोसेस करने से ओवरहेड बढ़ता है। | पेजों को बैच में प्रोसेस करें या .NET Core पर चलाते समय मेमोरी आवंटन बढ़ाएँ। |

## अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या मैं Aspose.OCR को अंग्रेज़ी के अलावा अन्य भाषाओं के लिए उपयोग कर सकता हूँ?

A1: हाँ, Aspose.OCR कई भाषाओं को सपोर्ट करता है। भाषा सेटिंग्स को उसी अनुसार समायोजित करें।

### Q2: मैं Aspose.OCR को अपने .NET प्रोजेक्ट में कैसे इंटीग्रेट करूँ?

A2: विस्तृत इंटीग्रेशन चरणों के लिए [documentation](https://reference.aspose.com/ocr/net/) देखें।

### Q3: क्या Aspose.OCR का ट्रायल वर्ज़न उपलब्ध है?

A3: हाँ, आप [free trial version](https://releases.aspose.com/) के साथ फीचर्स का अन्वेषण कर सकते हैं।

### Q4: क्या मैं स्पेल चेकिंग के लिए कस्टम डिक्शनरी अपलोड कर सकता हूँ?

A4: बिल्कुल! ट्यूटोरियल में दिखाया गया है कि उपयोगकर्ता‑प्रदान की गई डिक्शनरी से सुधार को कैसे बढ़ाया जाए।

### Q5: मैं Aspose.OCR के लिए सपोर्ट कहाँ प्राप्त कर सकता हूँ?

A5: समुदाय समर्थन और मार्गदर्शन के लिए [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) पर जाएँ।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-25  
**Tested With:** Aspose.OCR for .NET latest version  
**Author:** Aspose