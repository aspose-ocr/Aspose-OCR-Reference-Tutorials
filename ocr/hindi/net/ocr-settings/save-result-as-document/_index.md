---
date: 2025-12-27
description: Aspose.OCR for .NET का उपयोग करके छवि से टेक्स्ट निकालना, छवियों में
  टेक्स्ट पहचानना और छवि को विभिन्न दस्तावेज़ फ़ॉर्मैट में PDF .NET में परिवर्तित
  करना सीखें।
linktitle: Save Result as Document in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: इमेज को PDF में बदलें .NET – OCR इमेज पहचान में परिणाम को दस्तावेज़ के रूप
  में सहेजें
url: /hi/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज को PDF .NET में बदलें – OCR इमेज रिकग्निशन में परिणाम को दस्तावेज़ के रूप में सहेजें

## Introduction

Aspose.OCR for .NET के साथ ऑप्टिकल कैरेक्टर रिकग्निशन (OCR) की रोमांचक दुनिया में आपका स्वागत है! इस ट्यूटोरियल में आप सीखेंगे कि कैसे **इमेज को PDF .NET में बदलें**, इमेज से टेक्स्ट निकालें, और OCR आउटपुट को PDF, DOCX, TXT, और Excel जैसे सर्चेबल दस्तावेज़ फ़ॉर्मैट में सहेजें। चाहे आपको सर्चेबल PDF बनाना हो या OCR परिणाम को Excel में एक्सपोर्ट करना हो, नीचे दिए गए चरण आपको प्रक्रिया को तेज़ और प्रभावी ढंग से पूरा करने में मदद करेंगे।

## Quick Answers
- **“image to pdf .net” क्या मतलब है?** यह इमेज फ़ाइलों को .NET लाइब्रेरीज़ (इस केस में Aspose.OCR) का उपयोग करके PDF दस्तावेज़ में बदलने को दर्शाता है।  
- **मैं OCR परिणाम को किन फ़ॉर्मैट में एक्सपोर्ट कर सकता हूँ?** DOCX, TXT, PDF, और XLSX बॉक्स से बाहर ही सपोर्टेड हैं।  
- **प्रोडक्शन उपयोग के लिए लाइसेंस चाहिए?** हाँ, प्रोडक्शन के लिए एक कमर्शियल लाइसेंस आवश्यक है; मूल्यांकन के लिए एक फ्री ट्रायल उपलब्ध है।  
- **क्या मैं PDF से सर्चेबल टेक्स्ट एक्सट्रैक्ट कर सकता हूँ?** बिल्कुल – जेनरेट किया गया PDF एक **ocr to searchable pdf** है जिसे आप इंडेक्स कर सकते हैं।  
- **कौन से .NET वर्ज़न सपोर्टेड हैं?** Aspose.OCR .NET Framework 4.5+, .NET Core 3.1+, और .NET 5/6+ के साथ काम करता है।  

## What is “image to pdf .net”?
“Image to PDF .NET” वह प्रक्रिया है जिसमें रास्टर इमेज (PNG, JPEG, TIFF आदि) को प्रोग्रामेटिकली .NET लाइब्रेरी की मदद से PDF फ़ाइल में बदल दिया जाता है। Aspose.OCR न केवल इमेज को कन्वर्ट करता है बल्कि OCR भी करता है, जिससे आप **इमेज में टेक्स्ट को पहचान** सकते हैं और उस टेक्स्ट को उत्पन्न PDF में एम्बेड कर सकते हैं, जिससे वह सर्चेबल बन जाता है।

## Why use Aspose.OCR for this task?
- **उच्च सटीकता** – उन्नत OCR इंजन जो कई भाषाओं और फ़ॉन्ट्स को संभालता है।  
- **वन‑स्टेप कन्वर्ज़न** – आप टेक्स्ट को पहचान सकते हैं और सीधे PDF, DOCX, TXT, या Excel में सहेज सकते हैं बिना अतिरिक्त पोस्ट‑प्रोसेसिंग के।  
- **कोई एक्सटर्नल डिपेंडेंसी नहीं** – शुद्ध .NET लाइब्रेरी, कोई नेटिव बाइनरी आवश्यक नहीं।  
- **लचीलापन** – आउटपुट फ़ॉर्मैट को आसानी से बदल सकते हैं, OCR से दस्तावेज़ बनाएं या डेटा एनालिसिस के लिए OCR को Excel में एक्सपोर्ट करें।

## Prerequisites

इस OCR यात्रा पर निकलने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित प्री‑रिक्विज़िट्स मौजूद हों:

- Aspose.OCR for .NET. सुनिश्चित करें कि आपने Aspose.OCR लाइब्रेरी इंस्टॉल की हुई है। आप इसे [here](https://releases.aspose.com/ocr/net/) से डाउनलोड कर सकते हैं।

- Document Directory: अपने दस्तावेज़ों के लिए एक निर्धारित फ़ोल्डर रखें, और प्रदान किए गए कोड में `dataDir` वेरिएबल को उसी अनुसार अपडेट करें।

## Import Namespaces

कोड को OCR क्षमताओं से लैस करने के लिए आवश्यक नेमस्पेसेज़ इम्पोर्ट करें।

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

अब उदाहरण को कई चरणों में विभाजित करते हैं:

## How to Convert Image to PDF .NET Using Aspose.OCR

### Step 1: Initialize Aspose.OCR

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

यह चरण Aspose.OCR API को इनिशियलाइज़ करके आधार तैयार करता है।

### Step 2: Recognize Image

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

यहाँ हम Aspose.OCR का उपयोग करके **निर्दिष्ट इमेज में टेक्स्ट को पहचानते** हैं ( `"sample.png"` को अपनी इमेज फ़ाइल से बदलें)। यही वह जगह है जहाँ **extract text from image** ऑपरेशन होता है।

### Step 3: Save Result in Different Formats

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

अपनी ज़रूरतों के अनुसार इस चरण को कस्टमाइज़ करें। Aspose.OCR आपको **पहचाने गए टेक्स्ट को विभिन्न दस्तावेज़ फ़ॉर्मैट जैसे DOCX, TXT, PDF, और XLSX में सहेजने** की सुविधा देता है, जिससे प्रभावी रूप से **creating a document from OCR** या **exporting OCR to Excel** संभव होता है।

### Step 4: Display Success Message

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

एक साधारण पुष्टि संदेश जो आपको बताता है कि प्रक्रिया बिना किसी समस्या के पूरी हो गई है।

इन चरणों का पालन करके, आपने .NET में Aspose.OCR की शक्ति का उपयोग करके इमेज में टेक्स्ट को पहचानना और विभिन्न दस्तावेज़ फ़ॉर्मैट में परिणाम सहेजना, जिसमें एक **ocr to searchable pdf** भी शामिल है, सफलतापूर्वक किया है।

## Common Issues and Solutions
- **इमेज पहचान नहीं हो रही** – सुनिश्चित करें कि इमेज की रेज़ोल्यूशन पर्याप्त है (कम से कम 300 dpi) और वह सपोर्टेड फ़ॉर्मैट (PNG, JPEG, TIFF) में हो।  
- **भाषा पहचान गलत** – `RecognitionSettings` ऑब्जेक्ट में उचित `Language` प्रॉपर्टी सेट करें (उदाहरण: `Language = Language.English`)।  
- **आउटपुट फ़ाइल नहीं बन रही** – जाँचें कि `dataDir` एक वैध, राइटेबल फ़ोल्डर की ओर इशारा कर रहा है और फ़ाइल नाम यूनिक हैं।

## Frequently Asked Questions

**Q: क्या Aspose.OCR विभिन्न इमेज फ़ॉर्मैट को सपोर्ट करता है?**  
A: हाँ, Aspose.OCR कई इमेज फ़ॉर्मैट को सपोर्ट करता है, जिससे आपके OCR कार्यों में लचीलापन मिलता है।

**Q: क्या मैं बेहतर सटीकता के लिए रिकग्निशन सेटिंग्स कस्टमाइज़ कर सकता हूँ?**  
A: बिल्कुल! Aspose.OCR आपको OCR प्रक्रिया को आपके विशिष्ट आवश्यकताओं के अनुसार ट्यून करने के लिए रिकग्निशन सेटिंग्स प्रदान करता है।

**Q: क्या फ्री ट्रायल उपलब्ध है?**  
A: हाँ, आप एक फ्री ट्रायल [here](https://releases.aspose.com/) से शुरू कर सकते हैं।

**Q: मैं Aspose.OCR के लिए टेम्पररी लाइसेंस कैसे प्राप्त करूँ?**  
A: टेम्पररी लाइसेंस [here](https://purchase.aspose.com/temporary-license/) से प्राप्त किए जा सकते हैं।

**Q: सहायता या कम्युनिटी से जुड़ने के लिए कहाँ जाएँ?**  
A: सपोर्ट और चर्चा के लिए Aspose.OCR कम्युनिटी [Aspose Forum](https://forum.aspose.com/c/ocr/16) में जुड़ें।

## Conclusion

संक्षेप में, Aspose.OCR for .NET **image to pdf .net** कन्वर्ज़न, टेक्स्ट एक्सट्रैक्शन, और दस्तावेज़ जेनरेशन के लिए असीम संभावनाएँ खोलता है। चाहे आप डेटा एक्सट्रैक्ट कर रहे हों, सर्चेबल PDF बना रहे हों, या OCR परिणाम को Excel में एक्सपोर्ट कर रहे हों, Aspose.OCR अपनी सहज API और मजबूत फीचर सेट के साथ प्रक्रिया को सरल बनाता है।

---

**Last Updated:** 2025-12-27  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}