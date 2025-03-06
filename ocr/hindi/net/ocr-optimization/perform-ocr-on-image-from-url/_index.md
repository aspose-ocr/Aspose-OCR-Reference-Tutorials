---
title: ओसीआर छवि पहचान में यूआरएल से छवि पर ओसीआर निष्पादित करें
linktitle: ओसीआर छवि पहचान में यूआरएल से छवि पर ओसीआर निष्पादित करें
second_title: Aspose.OCR .NET एपीआई
description: .NET के लिए Aspose.OCR के साथ सहज OCR एकीकरण का अन्वेषण करें। छवियों से पाठ को सटीकता से पहचानें।
weight: 10
url: /hi/net/ocr-optimization/perform-ocr-on-image-from-url/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ओसीआर छवि पहचान में यूआरएल से छवि पर ओसीआर निष्पादित करें

## परिचय

ऑप्टिकल कैरेक्टर रिकॉग्निशन (OCR) के क्षेत्र में, .NET के लिए Aspose.OCR एक शक्तिशाली उपकरण के रूप में सामने आता है जो डेवलपर्स को सटीकता के साथ छवियों से पाठ सामग्री निकालने का अधिकार देता है। यदि आप अपने .NET एप्लिकेशन में ओसीआर क्षमताओं को एकीकृत करना चाहते हैं और आसानी से टेक्स्ट पहचान करना चाहते हैं, तो यह चरण-दर-चरण मार्गदर्शिका आपको यूआरएल से एक छवि पर ओसीआर निष्पादित करने की प्रक्रिया के बारे में बताएगी।

## आवश्यक शर्तें

ट्यूटोरियल में गहराई से जाने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

-  .NET के लिए Aspose.OCR: सुनिश्चित करें कि आपके पास Aspose.OCR लाइब्रेरी आपके .NET प्रोजेक्ट में एकीकृत है। आप इसे यहां से डाउनलोड कर सकते हैं[रिलीज पेज](https://releases.aspose.com/ocr/net/).

- विकास परिवेश: अपनी मशीन पर एक कार्यशील .NET विकास परिवेश स्थापित करें।

## नामस्थान आयात करें

अपने .NET प्रोजेक्ट में, Aspose.OCR कार्यात्मकताओं तक पहुँचने के लिए आवश्यक नामस्थान शामिल करें। अपने प्रोजेक्ट में निम्नलिखित कोड स्निपेट जोड़ें:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## चरण 1: अपनी दस्तावेज़ निर्देशिका सेट करें

 उस निर्देशिका को निर्दिष्ट करके प्रारंभ करें जहां आपके दस्तावेज़ संग्रहीत हैं। प्रतिस्थापित करें`"Your Document Directory"` आपके दस्तावेज़ों के वास्तविक पथ के साथ।

```csharp
string dataDir = "Your Document Directory";
```

## चरण 2: पहचान के लिए छवि प्राप्त करें

उस छवि का URL प्रदान करें जिस पर आप OCR करना चाहते हैं। सुनिश्चित करें कि छवि सार्वजनिक रूप से पहुंच योग्य है।

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

## चरण 3: AsposeOcr को आरंभ करें

OCR कार्यात्मकताओं तक पहुँचने के लिए AsposeOcr वर्ग का एक उदाहरण बनाएँ।

```csharp
AsposeOcr api = new AsposeOcr();
```

## चरण 4: छवि को पहचानें

निर्दिष्ट छवि URL से पाठ को पहचानने के लिए Aspose.OCR लाइब्रेरी का उपयोग करें। अपनी आवश्यकताओं के आधार पर पहचान सेटिंग्स समायोजित करें।

```csharp
RecognitionResult result = api.RecognizeImageFromUri(uri, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    RecognitionAreas = new List<Rectangle>()
    {
        new Rectangle(1,3,390,70),
        new Rectangle(1,72,390,70)
    }
});
```

## चरण 5: परिणाम प्रिंट करें

मान्यता प्राप्त पाठ, क्षेत्रों और किसी भी चेतावनी सहित मान्यता परिणाम प्रदर्शित करें।

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

## चरण 6: निष्पादित करें और सत्यापित करें

अपना एप्लिकेशन चलाएं, और यदि सब कुछ सही ढंग से सेट किया गया है, तो आपको ओसीआर प्रक्रिया को सफलतापूर्वक निष्पादित होते देखना चाहिए।

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## निष्कर्ष

.NET के लिए Aspose.OCR के साथ, आपके .NET अनुप्रयोगों में OCR क्षमताओं को एकीकृत करना एक सहज अनुभव बन जाता है। इस ट्यूटोरियल ने आपको यूआरएल से एक छवि पर ओसीआर निष्पादित करने की प्रक्रिया के माध्यम से मार्गदर्शन किया है, जो आपको अपनी परियोजनाओं में टेक्स्ट पहचान की शक्ति का लाभ उठाने के लिए आधार प्रदान करता है।

## अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या Aspose.OCR अनेक भाषाओं को संभालने के लिए उपयुक्त है?

A1: हाँ, Aspose.OCR विभिन्न भाषाओं में पाठ की पहचान का समर्थन करता है, जो इसे अंतर्राष्ट्रीय अनुप्रयोगों के लिए बहुमुखी बनाता है।

### Q2: क्या मैं Aspose.OCR का उपयोग सिंगल-लाइन और मल्टी-लाइन टेक्स्ट पहचान दोनों के लिए कर सकता हूँ?

ए2: बिल्कुल! Aspose.OCR आपके विशिष्ट उपयोग के मामले को अनुकूलित करते हुए, सिंगल-लाइन और मल्टी-लाइन टेक्स्ट दोनों को पहचानने के लिए लचीलापन प्रदान करता है।

### Q3: क्या Aspose.OCR के लिए कोई लाइसेंसिंग विकल्प उपलब्ध हैं?

 उ3: हां, आप लाइसेंसिंग विकल्प तलाश सकते हैं और खरीदारी कर सकते हैं[असपोज़ स्टोर](https://purchase.aspose.com/buy).

### Q4: क्या Aspose.OCR के लिए कोई निःशुल्क परीक्षण उपलब्ध है?

 A4: हाँ, आप Aspose.OCR पर जाकर निःशुल्क आज़मा सकते हैं[पृष्ठ जारी करता है](https://releases.aspose.com/).

### Q5: मुझे Aspose.OCR से संबंधित समर्थन या सामुदायिक चर्चाएँ कहाँ मिल सकती हैं?

 A5: पर जाएँ[Aspose.OCR फोरम](https://forum.aspose.com/c/ocr/16) समुदाय के समर्थन और उससे जुड़ने के लिए।
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
