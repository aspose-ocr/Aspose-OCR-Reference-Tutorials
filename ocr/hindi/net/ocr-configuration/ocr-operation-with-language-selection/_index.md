---
date: 2025-12-21
description: Aspose.OCR for .NET का उपयोग करके OCR कैसे करें और छवि से टेक्स्ट निकालें,
  यह सीखें। यह चरण‑दर‑चरण गाइड बहुभाषी टेक्स्ट पहचान और भाषा चयन को दर्शाता है।
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: Aspose.OCR में भाषा चयन के साथ OCR कैसे करें
url: /hi/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR में भाषा चयन के साथ OCR कैसे करें

## परिचय

यदि आपको .NET एप्लिकेशन में छवियों पर **OCR कैसे करें** और इमेज फ़ाइलों से टेक्स्ट निकालना है, तो Aspose.OCR for .NET एक तेज़, सटीक और भाषा‑सचेत समाधान प्रदान करता है। इस ट्यूटोरियल में हम एक वास्तविक उदाहरण के माध्यम से OCR इमेज पहचान को भाषा चयन के साथ दिखाएंगे, ताकि आप कुछ ही कोड लाइनों से तस्वीरों से बहुभाषी टेक्स्ट निकाल सकें।

## तुरंत जवाब
- **Aspose.OCR क्या करता है?** यह छवियों में मुद्रित और हस्तलिखित टेक्स्ट को पहचानता है और निकाला गया टेक्स्ट लौटाता है.  
- **क्या मैं भाषा चुन सकता हूँ?** हाँ – आप किसी भी समर्थित भाषा जैसे English, German, Spanish, Chinese आदि को निर्दिष्ट कर सकते हैं.  
- **क्या विकास के लिए लाइसेंस चाहिए?** मूल्यांकन के लिए एक फ्री ट्रायल काम करता है; उत्पादन उपयोग के लिए लाइसेंस आवश्यक है.  
- **कौन से .NET संस्करण समर्थित हैं?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **क्या स्क्यू सुधार स्वचालित है?** आप `AutoSkew` को सक्षम कर सकते हैं और `SkewAngle` सेटिंग को फाइन‑ट्यून कर सकते हैं.

## OCR टास्क के लिए Aspose.OCR क्यों चुनें?

- **उच्च सटीकता** विभिन्न फ़ॉन्ट्स और इमेज क्वालिटी में।  
- **इनबिल्ट भाषा चयन** बाहरी भाषा पैक्स की आवश्यकता को समाप्त करता है।  
- **सरल API** जो मौजूदा C# प्रोजेक्ट्स में साफ़-सुथरे ढंग से एकीकृत होती है।  
- **कोई बाहरी निर्भरताएँ नहीं** – सब कुछ स्थानीय रूप से चलता है, जिससे आपका डेटा सुरक्षित रहता है।

## ज़रूरी शर्तें

कोड में जाने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

- Aspose.OCR for .NET: सुनिश्चित करें कि आपके पास Aspose.OCR लाइब्रेरी स्थापित है। आप इसे [Aspose.OCR for .NET download page](https://releases.aspose.com/ocr/net/) से डाउनलोड कर सकते हैं।

- Development Environment: .NET एप्लिकेशन के साथ एक कार्यशील वातावरण सेट करें। यदि आपने अभी तक नहीं किया है, तो विस्तृत निर्देशों के लिए [documentation](https://reference.aspose.com/ocr/net/) देखें।

## नेमस्पेस इंपोर्ट करें

अपने .NET एप्लिकेशन में, आवश्यक नेमस्पेसेस को इम्पोर्ट करके शुरू करें:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## चरण 1: Aspose.OCR को इनिशियलाइज़ करें

Aspose.OCR क्लास का एक इंस्टेंस इनिशियलाइज़ करके शुरू करें। यह आपके एप्लिकेशन में OCR क्षमताओं का उपयोग करने के लिए मंच तैयार करता है।

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## चरण 2: इमेज पाथ निर्दिष्ट करें

अगला, उस इमेज का पाथ परिभाषित करें जिस पर आप OCR करना चाहते हैं। सुनिश्चित करें कि इमेज आपके एप्लिकेशन से एक्सेसिबल हो।

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## चरण 3: भाषा चयन के साथ इमेज को पहचानें

अब मुख्य OCR ऑपरेशन आता है। निर्दिष्ट इमेज से टेक्स्ट पहचानने के लिए Aspose.OCR लाइब्रेरी का उपयोग करें। पहचान सेटिंग्स को समायोजित करें, जिसमें भाषा चयन भी शामिल है।

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## चरण 4: परिणाम प्रिंट और डिस्प्ले करें

OCR ऑपरेशन के बाद, परिणाम प्रिंट और डिस्प्ले करें, जिसमें पहचाना गया टेक्स्ट, एरिया, वार्निंग्स, और JSON प्रतिनिधित्व शामिल हैं।

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## सामान्य समस्याएँ और सुझाव

- **गलत भाषा चयन** – यदि आउटपुट गड़बड़ दिखता है, तो दोबारा जांचें कि `Language` प्रॉपर्टी स्रोत इमेज की भाषा से मेल खाती है।  
- **झुकी हुई इमेजेज** – बेहतर सटीकता के लिए `AutoSkew` को सक्षम करें या झुके स्कैन पर `SkewAngle` को मैन्युअली समायोजित करें।  
- **बड़ी फ़ाइलें** – मेमोरी बचाने के लिए बड़ी इमेजेज को चंक्स में प्रोसेस करें या `RecognizeImage` में फीड करने से पहले रिज़ॉल्यूशन कम करें।

## निष्कर्ष

बधाई हो! आपने Aspose.OCR for .NET का उपयोग करके भाषा चयन के साथ **OCR कैसे करें** सीख लिया है। इस ट्यूटोरियल ने आपको इमेज फ़ाइलों से टेक्स्ट निकालना, पहचान सेटिंग्स को कस्टमाइज़ करना, और बहुभाषी कंटेंट को आसानी से हैंडल करना दिखाया।

## FAQ's

### Q1: क्या Aspose.OCR बहुभाषी टेक्स्ट पहचान के लिए उपयुक्त है?

A1: हाँ, Aspose.OCR विभिन्न भाषाओं को सपोर्ट करता है, जिससे बहुभाषी OCR कार्यों के लिए लचीलापन मिलता है।

### Q2: क्या मैं विशिष्ट इमेज विशेषताओं के लिए OCR सेटिंग्स को फाइन‑ट्यून कर सकता हूँ?

A2: बिल्कुल! विभिन्न परिदृश्यों के लिए OCR को ऑप्टिमाइज़ करने हेतु स्क्यू एंगल, लाइन रिकग्निशन, और एरिया डिटेक्शन जैसे पैरामीटर को समायोजित करें।

### Q3: अतिरिक्त समर्थन या समुदाय चर्चा कहाँ पा सकते हैं?

A3: समर्थन और समुदाय चर्चा के लिए [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) पर जाएँ।

### Q4: क्या कोई फ्री ट्रायल उपलब्ध है?

A4: हाँ, Aspose.OCR की क्षमताओं को अनुभव करने के लिए [free trial](https://releases.aspose.com/) देखें।

### Q5: मैं Aspose.OCR for .NET कैसे खरीद सकता हूँ?

A5: खरीदने के लिए, [purchase page](https://purchase.aspose.com/buy) पर जाएँ।

---

**अंतिम अपडेट:** 2025-12-21  
**परीक्षित संस्करण:** Aspose.OCR 24.11 for .NET  
**लेखक:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}