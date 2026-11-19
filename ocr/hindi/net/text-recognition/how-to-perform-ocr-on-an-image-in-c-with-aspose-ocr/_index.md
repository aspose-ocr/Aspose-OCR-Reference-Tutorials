---
category: general
date: 2026-10-18
description: C# में जल्दी से एक छवि पर OCR करें। JPG से टेक्स्ट निकालना, छवि को टेक्स्ट
  में बदलना और Aspose.OCR का उपयोग करके छवि से टेक्स्ट पढ़ना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- convert image to text
- read text from image
- load image for OCR
language: hi
lastmod: 2026-10-18
og_description: Aspose.OCR के साथ C# में छवि पर OCR करें। यह ट्यूटोरियल दिखाता है
  कि JPG से टेक्स्ट कैसे निकालें, छवि को टेक्स्ट में बदलें और कुछ ही मिनटों में छवि
  से टेक्स्ट पढ़ें।
og_image_alt: Console output displaying recognized Cyrillic text after performing
  OCR on an image
og_title: C# में एक छवि पर OCR करें – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Perform OCR on an image in C# quickly. Learn to extract text from JPG,
    convert image to text and read text from image using Aspose.OCR.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
title: C# में Aspose.OCR के साथ छवि पर OCR कैसे करें
url: /hi/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Aspose.OCR के साथ इमेज पर OCR कैसे करें

यदि आपको .NET एप्लिकेशन में **इमेज पर OCR करना** है, तो यह गाइड आपको एक पूर्ण, तैयार‑चलाने‑योग्य समाधान दिखाता है। आप देखेंगे कि **OCR के लिए इमेज लोड** कैसे करें, Cyrillic अक्षरों को कैसे पहचानें, और **JPG फ़ाइलों से टेक्स्ट निकालें** बिना किसी लो‑लेवल इमेज‑प्रोसेसिंग कोड के।

इस ट्यूटोरियल में आप करेंगे:

* Aspose.OCR NuGet पैकेज इंस्टॉल करेंगे।  
* इमेज फ़ाइल (JPG, PNG, BMP, आदि) लोड करेंगे।  
* OCR इंजन चलाकर **इमेज को टेक्स्ट में बदलें**।  
* **इमेज से टेक्स्ट पढ़ें** और कंसोल में आउटपुट दिखाएँ।  

ये चरण किसी भी .NET‑संगत इमेज के साथ काम करते हैं, इसलिए आप इन्हें PDFs, स्कैन किए हुए रसीदों या स्क्रीनशॉट्स के लिए भी अनुकूलित कर सकते हैं।

## आवश्यकताएँ

* .NET 6.0 SDK या बाद का संस्करण (कोड .NET Framework 4.7+ के साथ भी काम करता है)।  
* Visual Studio 2022 या कोई भी पसंदीदा C# एडिटर।  
* पहली बार चलाने के लिए इंटरनेट एक्सेस – Aspose.OCR स्वचालित रूप से Cyrillic भाषा मॉड्यूल डाउनलोड करता है।  

> **Pro tip:** NuGet पैकेज को हमेशा अपडेट रखें; नए संस्करण पहचान की सटीकता को बेहतर बनाते हैं और भाषा पैक्स जोड़ते हैं।

## चरण 1: Aspose.OCR स्थापित करें

अपने प्रोजेक्ट फ़ोल्डर में एक टर्मिनल खोलें और चलाएँ:

```bash
dotnet add package Aspose.OCR
```

यह पैकेज `OcrEngine` क्लास प्रदान करता है जो **इमेज पर OCR करने** के लिए उपयोग होती है। कमांड समाप्त होने के बाद, पैकेज रेफ़रेंस आपके *.csproj* फ़ाइल में दिखेगा।

## चरण 2: एक कंसोल प्रोग्राम स्केलेटन बनाएं

यदि आपके पास पहले से प्रोजेक्ट नहीं है तो नया कंसोल प्रोजेक्ट बनाएं:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

जेनरेट हुई *Program.cs* को अगले सेक्शनों में दिखाए गए कोड से बदलें। स्केलेटन में आवश्यक `using` निर्देश और एक `Main` मेथड शामिल है जो OCR प्रक्रिया को चलाता है।

## चरण 3: OCR के लिए इमेज लोड करें

कोड की पहली कार्यात्मक लाइन **इमेज को लोड** करती है जिसे आप विश्लेषण करना चाहते हैं। Aspose.OCR किसी भी स्ट्रीम को स्वीकार करता है, इसलिए आप फ़ाइल को डिस्क, वेब URL या एम्बेडेड रिसोर्स से लोड कर सकते हैं।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 3: Load the image containing Cyrillic text
        // Replace the path with the location of your JPG file.
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);
```

*Why this matters*: `ImageStream.FromFile` का उपयोग करने से फ़ॉर्मेट हैंडलिंग एब्स्ट्रैक्ट हो जाती है, जिससे OCR इंजन को मूल फ़ाइल प्रकार की परवाह किए बिना एक सुसंगत बिटमैप मिलता है। `using` स्टेटमेंट के कारण स्ट्रीम स्वचालित रूप से डिस्पोज़ हो जाता है।

## चरण 4: OCR इंजन को इनिशियलाइज़ करें और भाषा सेट करें (वैकल्पिक)

डिफ़ॉल्ट रूप से Aspose.OCR भाषा को स्वचालित रूप से पहचानने की कोशिश करता है। Cyrillic टेक्स्ट के लिए आप स्पष्ट रूप से `Language.Cyrillic` मॉड्यूल का अनुरोध कर सकते हैं, जिससे पहली बार डाउनलोड तेज़ हो जाता है।

```csharp
        // Step 4: Initialize the OCR engine
        var engine = new OcrEngine();

        // Optional: force Cyrillic language to avoid auto‑detection overhead
        engine.Language = Language.Cyrillic;
```

यदि आप भाषा असाइनमेंट छोड़ देते हैं, तो इंजन `Recognize` कॉल करने पर पहली बार आवश्यक मॉड्यूल डाउनलोड कर लेगा। डाउनलोड HTTPS के माध्यम से होता है और बाद के रन के लिए स्थानीय रूप से कैश हो जाता है।

## चरण 5: OCR करें और इमेज को टेक्स्ट में बदलें

अब आप वास्तव में **इमेज पर OCR करेंगे** और एक साधारण‑टेक्स्ट स्ट्रिंग प्राप्त करेंगे। `Recognize` मेथड सभी भारी काम करता है: प्री‑प्रोसेसिंग, लेआउट एनालिसिस, और कैरेक्टर क्लासिफिकेशन।

```csharp
        // Step 5: Perform OCR – convert image to text
        engine.Image = image;
        string recognizedText = engine.Recognize();
```

रिटर्न किया गया `recognizedText` मूल लेआउट के अनुसार लाइन ब्रेक रखता है, जिससे पोस्ट‑प्रोसेसिंग या डेटाबेस में स्टोर करना आसान हो जाता है।

## चरण 6: परिणाम दिखाएँ – इमेज से टेक्स्ट पढ़ें

अंत में, **इमेज से टेक्स्ट पढ़ें** और परिणाम को कंसोल में लिखें। यह चरण यह पुष्टि करता है कि OCR सफल रहा और आपको ठीक वही दिखाता है जो निकाला गया था।

```csharp
        // Step 6: Display the recognized text – read text from image
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

जब आप प्रोग्राम चलाते हैं (`dotnet run`), तो आपको लगभग इस तरह का आउटपुट दिखना चाहिए:

```
=== OCR Result ===
Пример текста на кириллице
```

> **Note:** सटीक आउटपुट स्रोत JPG की गुणवत्ता पर निर्भर करता है। स्पष्ट, हाई‑रेज़ोल्यूशन इमेज सबसे अच्छे परिणाम देती हैं।

## पूर्ण, चलाने योग्य सोर्स कोड

नीचे पूरा प्रोग्राम दिया गया है जिसे आप *Program.cs* में कॉपी‑पेस्ट कर सकते हैं और बिना किसी संशोधन (इमेज पाथ को छोड़कर) चलाए जा सकते हैं।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Load the image containing Cyrillic text
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);

        // Initialize the OCR engine
        var engine = new OcrEngine
        {
            // Force Cyrillic language; optional but speeds up first run
            Language = Language.Cyrillic,
            Image = image
        };

        // Recognize the text – this converts the image to text
        string recognizedText = engine.Recognize();

        // Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

प्रोग्राम चलाने पर निकाले गए कैरेक्टर कंसोल में प्रिंट होते हैं, जिससे यह सिद्ध होता है कि आपने सफलतापूर्वक **JPG से टेक्स्ट निकाला** और **इमेज को टेक्स्ट में बदला** है।

## सामान्य वैरिएशन्स को संभालना

| Scenario | Adjustment |
|----------|------------|
| **Different language** | `engine.Language = Language.English;` या किसी अन्य सपोर्टेड एनोम का उपयोग करें। |
| **Multi‑page PDF** | प्रत्येक पेज को इमेज में बदलें (जैसे `Aspose.PDF` का उपयोग करके) और प्रत्येक इमेज के लिए OCR लूप चलाएँ। |
| **Large batch** | OCR कॉल को `Parallel.ForEach` लूप में रैप करें; मेमोरी ओवरहेड कम करने के लिए एक ही `OcrEngine` इंस्टेंस को पुन: उपयोग करें। |
| **Low‑resolution image** | पहचान से पहले शोर कम करने के लिए `engine.Image = ImageProcessing.Filters.GaussianBlur(image, 1.5);` से प्री‑प्रोसेस करें। |

इन वैरिएशन्स से आप किसी भी भाषा, आकार या क्वालिटी की **JPG फ़ाइलों से टेक्स्ट निकाल** सकते हैं।

## प्रदर्शन टिप्स

* **Cache language modules** – पहला डाउनलोड कुछ सेकंड ले सकता है; बाद के रन तुरंत होते हैं। |
* **Reuse the `OcrEngine`** instance for multiple images to avoid repeated initialization costs. |
* **Limit image size** – अत्यधिक बड़ी फ़ोटो मेमोरी उपयोग बढ़ाती हैं। उन्हें इंजन में फीड करने से पहले अधिकतम 2000 px चौड़ाई तक रिसाइज़ करें।

## निष्कर्ष

अब आप जानते हैं कि C# में Aspose.OCR का उपयोग करके **इमेज पर OCR कैसे करें**। इमेज लोड करके, इंजन को कॉन्फ़िगर करके, और `Recognize` कॉल करके आप **JPG से टेक्स्ट निकाल**, **इमेज को टेक्स्ट में बदल**, और **इमेज से टेक्स्ट पढ़** सकते हैं, वह भी कुछ ही लाइनों के कोड से।

अब आप आगे explore कर सकते हैं:

* OCR परिणामों को डेटाबेस में स्टोर करके सर्चेबल आर्काइव बनाना।  
* वर्कफ़्लो को वेब API में इंटीग्रेट करना जो अपलोडेड इमेज को स्वीकार करता है।  
* अन्य भाषा मॉड्यूल (Arabic, Hindi, आदि) का उपयोग करके अपने एप्लिकेशन की पहुंच बढ़ाना।

विभिन्न इमेज फ़ॉर्मेट, भाषाएँ, और बैच‑प्रोसेसिंग स्ट्रैटेजी के साथ प्रयोग करने में संकोच न करें। मूल पैटर्न—**OCR के लिए इमेज लोड → पहचान → प्लेन‑टेक्स्ट आउटपुट को हैंडल**—समान रहता है, जिससे आपको किसी भी टेक्स्ट‑एक्सट्रैक्शन प्रोजेक्ट के लिए एक ठोस आधार मिलता है।

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर कर सकें।

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to extract text from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}