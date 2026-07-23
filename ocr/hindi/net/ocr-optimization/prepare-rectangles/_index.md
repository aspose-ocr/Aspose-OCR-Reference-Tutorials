---
date: 2026-07-23
description: Aspose.OCR for .NET का उपयोग करके छवि से टेक्स्ट निकालना सीखें, OCR सटीकता
  बढ़ाने के लिए आयतें तैयार करें और छवि को टेक्स्ट में कुशलतापूर्वक परिवर्तित करें।
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: OCR इमेज रिकग्निशन में आयतें तैयार करें
og_description: Aspose.OCR for .NET का उपयोग करके छवि से टेक्स्ट निकालना सीखें, OCR
  सटीकता बढ़ाने के लिए आयतें तैयार करें और छवि को टेक्स्ट में कुशलतापूर्वक परिवर्तित
  करें।
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: आयतों के साथ छवि से टेक्स्ट निकालें – OCR गाइड
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: आयतों के साथ छवि से टेक्स्ट निकालें – OCR गाइड
url: /hi/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# छवि से आयतों के साथ पाठ निकालें – OCR गाइड

## परिचय

ऑप्टिकल कैरेक्टर रिकग्निशन (OCR) आपको **extract text from image** फ़ाइलों को खोज योग्य और संपादन योग्य बनाता है। इस ट्यूटोरियल में हम दिखाएंगे कि कैसे कस्टम आयतें तैयार करके OCR की सटीकता बढ़ाई जा सकती है, जो इंजन को आपके आवश्यक सटीक ज़ोन पर केंद्रित करती हैं। Aspose.OCR for .NET का उपयोग करके, आप पूरी कार्यप्रवाह देखेंगे—प्रोजेक्ट सेटअप से लेकर पहचाने गए स्ट्रिंग्स को प्राप्त करने तक—ताकि आप किसी भी .NET एप्लिकेशन में विश्वसनीय इमेज‑टू‑टेक्स्ट रूपांतरण एम्बेड कर सकें।

## त्वरित उत्तर
- **What does “extract text from image” mean?** यह चित्र में दृश्य अक्षरों को मशीन‑पठनीय स्ट्रिंग्स में बदल देता है।  
- **Which library handles this in .NET?** Aspose.OCR for .NET एक पूर्ण‑विशेषताओं वाला OCR इंजन प्रदान करता है।  
- **Do I need a license for production?** एक फ्री ट्रायल विकास के लिए काम करता है; उत्पादन के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **Can I limit OCR to specific zones?** हाँ—उपयोगी पाठ वाले क्षेत्रों को लक्षित करने के लिए आयतें परिभाषित करें।  
- **What .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## आयतों के साथ “extract text from image” क्या है?
`extract text from image` प्रक्रिया परिभाषित आयताकार ज़ोन के भीतर के अक्षरों को पढ़ती है, बाकी सबको अनदेखा करती है। OCR को इन ज़ोन तक सीमित करने से आपको अधिक सटीकता, तेज़ प्रोसेसिंग, और कम पोस्ट‑प्रोसेसिंग प्रयास मिलता है। यह तरीका उस पाठ को अलग करता है जिसकी आपको आवश्यकता है, जबकि बैकग्राउंड ग्राफ़िक्स, सजावटी तत्व, और अन्य दृश्य शोर को हटा देता है जो OCR इंजन को भ्रमित कर सकते हैं।

## OCR से पहले आयतें क्यों तैयार करें?
आयतें तैयार करने से आप OCR इंजन को छवि के सबसे प्रासंगिक भागों पर केंद्रित कर सकते हैं, जिससे गति और सटीकता दोनों में सुधार होता है। विश्लेषण क्षेत्र को संकीर्ण करके आप इंजन को जांचने वाले डेटा की मात्रा घटाते हैं, जिससे तेज़ परिणाम और अतिरिक्त दृश्य अव्यवस्था के कारण कम गलत पहचान होती है।

- **Focus on relevant content:** हेडर, फुटर, या सजावटी ग्राफ़िक्स को छोड़ दें जो इंजन को भ्रमित कर सकते हैं।  
- **Boost performance:** छोटे क्षेत्रों को कम गणनाओं की आवश्यकता होती है, जिससे बड़े स्कैन पर रनटाइम 40 % तक घट जाता है।  
- **Improve accuracy:** दृश्य शोर को कम करने से शोरयुक्त दस्तावेज़ों में अक्षर‑पहचान दर ~85 % से >95 % तक बढ़ जाती है।

## वास्तविक‑दुनिया के प्रोजेक्ट्स के लिए यह क्यों महत्वपूर्ण है
कई व्यावसायिक दस्तावेज़—रसीदें, इनवॉइस, आईडी कार्ड—पाठ को लोगो या बारकोड के साथ मिलाते हैं। उन फ़ील्ड्स के चारों ओर आयतें बनाकर जिन्हें आप वास्तव में चाहते हैं, आप केवल मूल्यवान डेटा निकालते हैं, जिससे डाउनस्ट्रीम सफाई कार्य कम हो जाता है और स्वचालित वर्कफ़्लो की विश्वसनीयता बढ़ती है। यह लक्षित निष्कर्षण पोस्ट‑प्रोसेसिंग प्रयास को घटाता है और डेटा‑हैंडलिंग मानकों के साथ अनुपालन बनाए रखने में मदद करता है।

## सामान्य उपयोग केस
- **Data entry automation:** स्कैन किए गए फ़ॉर्म या खर्च रसीदों से विशिष्ट फ़ील्ड्स निकालें।  
- **Compliance checks:** सत्यापन के लिए कानूनी क्लॉज़ या नियामक बयानों को अलग करें।  
- **Content indexing:** सर्च‑इंजन दृश्यता के लिए केवल छवि का हेडलाइन या कैप्शन इंडेक्स करें।

## पूर्वापेक्षाएँ
- C# और .NET विकास का बुनियादी ज्ञान।  
- Aspose.OCR for .NET लाइब्रेरी स्थापित – इसे **[here](https://releases.aspose.com/ocr/net/)** से डाउनलोड करें या सभी रिलीज़ **[here](https://releases.aspose.com/)** देखें।  
- `sample.png` जैसे एक नमूना चित्र जिसमें वह पाठ हो जिसे आप निकालना चाहते हैं।

## नामस्थान आयात करें
`using` स्टेटमेंट्स OCR इंजन और जियोमेट्री क्लासेज़ को स्कोप में लाते हैं।

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## चरण 1: अपने दस्तावेज़ डायरेक्टरी सेट अप करें
उस फ़ोल्डर को निर्दिष्ट करें जिसमें आपकी छवियां हैं और OCR इंजन का एक इंस्टेंस बनाएं।

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## कई आयतों का उपयोग करके छवि से पाठ कैसे निकालें
छवि को एक बार लोड करें, फिर OCR इंजन को आयतों की सूची दें। प्रत्येक आयत एक रुचि क्षेत्र को परिभाषित करती है, और इंजन प्रत्येक क्षेत्र के लिए अलग स्ट्रिंग लौटाता है, जिससे आप फ़ील्ड्स को व्यक्तिगत रूप से संभाल सकते हैं और आवश्यकतानुसार परिणामों को संयोजित कर सकते हैं।

### आयतें परिभाषित करें
`Rectangle` ऑब्जेक्ट्स प्रत्येक ज़ोन के X‑Y कोऑर्डिनेट्स और आकार को वर्णित करते हैं जिसे आप स्कैन करना चाहते हैं।  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### OCR मान्यता निष्पादित करें
`RecognizeImage` मेथड प्रदान की गई आयत सूची का उपयोग करके छवि को प्रोसेस करता है और प्रत्येक क्षेत्र के लिए पहचाना गया पाठ लौटाता है।  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## RecognitionSettings का उपयोग करके छवि से पाठ कैसे निकालें (वैकल्पिक तरीका)
यदि आप सेटिंग‑आधारित कॉल पसंद करते हैं, तो आप `RecognitionSettings` के साथ वही परिणाम प्राप्त कर सकते हैं। यह ऑब्जेक्ट आपको आयत परिभाषाओं को भाषा, DPI, और अन्य OCR विकल्पों के साथ बंडल करने की सुविधा देता है, जिससे एक साफ़, सिंगल‑पैरामीटर API कॉल मिलती है।

### मान्यता सेटिंग्स परिभाषित करें
`RecognitionSettings` आपको आयत सूची और अतिरिक्त विकल्पों (जैसे भाषा, DPI) को एक ही ऑब्जेक्ट में बंडल करने देता है।  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### पहचाना गया पाठ प्रदर्शित करें
वापसी स्ट्रिंग्स पर इटरेट करें और प्रत्येक क्षेत्र के पाठ को आउटपुट करें।  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## सामान्य समस्याएँ और सुझाव
- **Incorrect rectangle coordinates:** `X`, `Y`, `Width`, और `Height` इच्छित क्षेत्र से मेल खाते हैं, यह सत्यापित करें।  
- **Image quality:** निम्न‑रिज़ॉल्यूशन या अत्यधिक संकुचित छवियां OCR परिणामों को घटाती हैं; बाइनराइज़ेशन जैसी प्री‑प्रोसेसिंग पर विचार करें।  
- **Empty results:** सुनिश्चित करें कि आयतें वास्तव में पठनीय पाठ रखती हैं; अन्यथा इंजन खाली स्ट्रिंग्स लौटाता है।

## समस्या निवारण और सर्वोत्तम अभ्यास
| लक्षण | संभावित कारण | उपाय |
|---------|--------------|--------|
| कोई आउटपुट नहीं या खाली स्ट्रिंग्स | आयतें छवि की सीमा से बाहर | छवि आयाम और आयत कोऑर्डिनेट्स को दोबारा जांचें |
| विकृत अक्षर | कम कंट्रास्ट या शोर | OCR से पहले ग्रेस्केल रूपांतरण और थ्रेशहोल्डिंग लागू करें |
| बड़ी फ़ाइलों पर धीमी प्रदर्शन | बहुत अधिक आयतें या बहुत बड़ी छवि | संभव हो तो छवि को विभाजित करें या आयतों की संख्या घटाएँ |

## निष्कर्ष
अब आप Aspose.OCR for .NET के साथ कस्टम आयतें तैयार करके **extract text from image** करना जानते हैं। यह तरीका OCR प्रोसेसिंग पर सटीक नियंत्रण देता है, जिससे किसी भी .NET समाधान के लिए तेज़, अधिक सटीक टेक्स्ट‑एक्सट्रैक्शन फीचर मिलते हैं।

## अक्सर पूछे जाने वाले प्रश्न

**Q:** क्या मैं Aspose.OCR for .NET को अन्य .NET फ्रेमवर्क्स के साथ उपयोग कर सकता हूँ?  
**A:** हाँ, Aspose.OCR for .NET .NET Framework 4.5+, .NET Core 3.1+, और .NET 5/6/7 के साथ काम करता है।

**Q:** क्या कोई फ्री ट्रायल उपलब्ध है?  
**A:** बिल्कुल! ट्रायल **[here](https://releases.aspose.com/)** डाउनलोड करें।

**Q:** मैं Aspose.OCR for .NET के लिए समर्थन कहाँ प्राप्त कर सकता हूँ?  
**A:** समर्पित सहायता के लिए **[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)** पर जाएँ।

**Q:** क्या मैं परीक्षण के लिए एक अस्थायी लाइसेंस प्राप्त कर सकता हूँ?  
**A:** हाँ, एक अस्थायी लाइसेंस **[here](https://purchase.aspose.com/temporary-license/)** पर उपलब्ध है।

**Q:** आधिकारिक दस्तावेज़ कहाँ है?  
**A:** पूर्ण API रेफ़रेंस **[here](https://reference.aspose.com/ocr/net/)** पर स्थित है।

---

**अंतिम अपडेट:** 2026-07-23  
**परीक्षण किया गया:** Aspose.OCR 24.11 for .NET  
**लेखक:** Aspose  

{{< blocks/products/products-backtop-button >}}

## संबंधित ट्यूटोरियल
- [OCR इमेज रिकग्निशन में पैराग्राफ़ के लिए आयतें निकालना कैसे करें](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [इमेज को OCR कैसे करें – OCR इमेज रिकग्निशन में इमेज पर OCR निष्पादित करना](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Aspose.OCR for .NET का उपयोग करके इमेज से पाठ निकालना कैसे करें](/ocr/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}