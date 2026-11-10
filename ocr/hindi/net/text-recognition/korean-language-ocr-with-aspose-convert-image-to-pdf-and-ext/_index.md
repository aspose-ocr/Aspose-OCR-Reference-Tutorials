---
category: general
date: 2026-05-28
description: Aspose का उपयोग करके C# में कोरियन भाषा OCR ट्यूटोरियल। सीखें कि कैसे
  स्ट्रीम से इमेज लोड करें, साधारण टेक्स्ट निकालें, इमेज को PDF में बदलें और सर्चेबल
  PDF निर्यात करें।
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: hi
og_description: Aspose का उपयोग करके C# में कोरियन भाषा OCR। स्ट्रीम से इमेज लोड करने,
  साधारण टेक्स्ट निकालने, इमेज को PDF में बदलने और सर्चेबल PDF निर्यात करने के चरण‑दर‑चरण
  गाइड।
og_title: कोरियन भाषा OCR – छवि को PDF में बदलें और टेक्स्ट निकालें (C# गाइड)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'Aspose के साथ कोरियाई भाषा OCR: छवि को PDF में बदलें और C# में टेक्स्ट निकालें'
url: /hi/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose के साथ कोरियन भाषा OCR: इमेज को PDF में बदलें और C# में टेक्स्ट निकालें

क्या आपने कभी सोचा है कि **Korean Language OCR** को बिना क्लाउड पर कुछ भेजे एक तस्वीर पर कैसे चलाया जाए? आप अकेले नहीं हैं। चाहे आप सड़क संकेतों को डिजिटाइज़ कर रहे हों, रसीदों को प्रोसेस कर रहे हों, या बहुभाषी सर्च इंडेक्स बना रहे हों, कोरियन अक्षरों को स्थानीय रूप से पहचानना आपका समय, पैसा और प्राइवेसी समस्याओं को बचा सकता है।

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे कि कैसे **load image from stream**, **extract plain text**, **convert image to PDF**, और अंत में **export searchable PDF** किया जाए—सब Aspose.OCR और कुछ ही लाइनों के C# कोड से। कोई बाहरी सर्विस नहीं, कोई छिपा जादू नहीं—सिर्फ शुद्ध .NET कोड जिसे आप किसी भी कंसोल ऐप में डाल सकते हैं।

## आप क्या सीखेंगे

- एक काम करने वाला कंसोल प्रोग्राम जो फ़ाइल स्ट्रीम के ज़रिए JPEG फ़ाइल पढ़ता है।  
- कोरियन टेक्स्ट को प्लेन Unicode स्ट्रिंग्स के रूप में निकाला गया।  
- OCR रन का विस्तृत JSON रिपोर्ट जो डिबगिंग या एनालिटिक्स के लिए उपयोगी है।  
- एक सर्चेबल PDF जिसे आप किसी भी PDF रीडर में खोल सकते हैं और कोरियन शब्दों को वास्तव में सेलेक्ट कर सकते हैं।  

**Prerequisites**  
- .NET 6.0 या बाद का (कोड .NET Framework 4.7+ पर भी काम करता है)।  
- Aspose.OCR for .NET NuGet पैकेज इंस्टॉल किया हुआ (`Install-Package Aspose.OCR`)।  
- एक फ़ोल्डर जिसमें `korean_sign.jpg` हो और आउटपुट फ़ाइलों के लिए लिखने योग्य स्थान हो।  

यदि आपके पास ये सब पहले से तैयार है, तो चलिए शुरू करते हैं।

## चरण 1: Korean Language OCR के लिए OCR इंजन को इनिशियलाइज़ करें

पहले आपको एक `OcrEngine` इंस्टेंस चाहिए। GPU को एनेबल करना (यदि आपके पास है) पहचान को बहुत तेज़ कर देता है, और ऑटोमैटिक रिसोर्स डाउनलोड को बंद करने से लाइब्रेरी ऑफ़लाइन लैंग्वेज पैक्स का उपयोग करती है जो आप प्रदान करते हैं।

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Why this matters:**  
> *GPU acceleration* बड़े बैचों के लिए प्रोसेसिंग टाइम को सेकंड से मिलिसेकंड तक घटा सकता है। `AutomaticResourceDownload` को `false` सेट करने से डेमो ऑफ़लाइन काम करता है—जो कई एंटरप्राइज़ वातावरण में एक महत्वपूर्ण आवश्यकता है।

## चरण 2: स्ट्रीम से इमेज लोड करें

स्ट्रीम के माध्यम से इमेज पढ़ने से लचीलापन मिलता है: आप फ़ाइलें डिस्क, नेटवर्क शेयर, या मेमोरी‑कैश्ड ब्लॉब्स से ले सकते हैं। यहाँ हम एक लोकल JPEG फ़ाइल खोलते हैं, लेकिन यही पैटर्न किसी भी `Stream` के लिए काम करता है।

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Pro tip:** यदि आपको कभी वेब API के ज़रिए अपलोड की गई इमेज प्रोसेस करनी हो, तो बस `File.OpenRead` को इनकमिंग `IFormFile.OpenReadStream()` से बदल दें—बाकी सब समान रहेगा।

## चरण 3: कोरियन भाषा चुनें और प्री‑प्रोसेसिंग फ़िल्टर लागू करें

Aspose.OCR कुछ प्री‑प्रोसेसिंग स्टेप्स का समर्थन करता है जो पहचान से पहले इमेज को साफ़ करते हैं। कोरियन संकेतों के लिए आमतौर पर डेस्क्यूइंग और डिनॉइज़िंग पर्याप्त होते हैं।

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **What’s happening under the hood?**  
> `Deskew` फ़िल्टर घुमा हुआ टेक्स्ट सीधा करता है, जबकि `Denoise` वह ग्रेन हटाता है जो कैरेक्टर क्लासिफ़ायर को भ्रमित कर सकता है। इन स्टेप्स को छोड़ने से अक्सर गड़बड़ आउटपुट मिलता है, ख़ासकर लो‑रेज़ोल्यूशन फ़ोटो में।

## चरण 4: असिंक्रोनस रूप से प्लेन टेक्स्ट निकालें

अब सच्चाई का क्षण—इंजन को कैरेक्टर पहचानने और हमें साफ़ स्ट्रिंग देने को कहें। `RecognizeAsync` का उपयोग करने से UI रिस्पॉन्सिव रहता है यदि आप इसे डेस्कटॉप या वेब ऐप में एम्बेड करते हैं।

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

जब आप प्रोग्राम चलाते हैं, तो आपको कुछ इस तरह दिखना चाहिए:

```
OCR complete. Extracted text:
서울시청
```

> **Why async?**  
> OCR CPU‑इंटेंसिव हो सकता है। असिंक्रोनस एक्सीक्यूशन आपके थ्रेड को ब्लॉक होने से रोकता है, जो विशेष रूप से ASP.NET Core में थ्रेड स्टारवेशन की समस्या से बचाता है।

## चरण 5: विस्तृत रिकग्निशन रिज़ल्ट प्राप्त करें और JSON के रूप में सेव करें

कभी-कभी आपको केवल रॉ स्ट्रिंग से अधिक चाहिए—शायद आप कॉन्फिडेंस स्कोर, बाउंडिंग बॉक्स, या मूल इमेज डेटा चाहते हों। `RecognizeDetailed` मेथड एक `RecognitionResult` ऑब्जेक्ट रिटर्न करता है जिसे बाद में विश्लेषण के लिए JSON में सीरियलाइज़ किया जा सकता है।

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

`korean_ocr.json` खोलने पर आपको एक संरचना दिखेगी जो इस प्रकार है:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **When to use this?**  
> यदि आप सर्च इंडेक्स बना रहे हैं, तो कॉन्फिडेंस वैल्यूज़ आपको लो‑क्वालिटी रिज़ल्ट फ़िल्टर करने में मदद करती हैं। यदि आपको UI में टेक्स्ट हाइलाइट करना है, तो बाउंडिंग बॉक्स आपका मैप है।

## चरण 6: इमेज को PDF में बदलें और सर्चेबल PDF एक्सपोर्ट करें

Aspose रास्टर से वेक्टर में परिवर्तन को सहज बनाता है। `OutputFormat` को `SearchablePdf` सेट करने से लाइब्रेरी मूल इमेज को एम्बेड करती है और एक अदृश्य टेक्स्ट लेयर ओवरले करती है जिसमें OCR आउटपुट होता है। परिणामी PDF को सर्च, कॉपी और इंडेक्स किया जा सकता है जैसे कोई भी नेटिव PDF।

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

`korean_searchable.pdf` को Adobe Reader या किसी भी PDF व्यूअर में खोलें, **Ctrl+F** दबाएँ, एक कोरियन शब्द टाइप करें, और देखें कि वह पेज पर सही स्थान पर कूदता है। यही सर्चेबल PDF की शक्ति है।

> **Extra tip:** यदि आपको केवल विज़ुअल PDF चाहिए बिना हिडन टेक्स्ट लेयर के, तो `OutputFormat` को `Pdf` में बदल दें।

## पूरा कार्यशील उदाहरण

नीचे पूरा प्रोग्राम दिया गया है—कॉपी‑पेस्ट करें, `YOUR_DIRECTORY` को वास्तविक पाथ से बदलें, और **F5** दबाएँ।

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### अपेक्षित कंसोल आउटपुट

```
OCR complete. Extracted text:
서울시청
```

और आपको अपने स्रोत इमेज के बगल में तीन नई फ़ाइलें मिलेंगी:

- `korean_ocr.json` – पूर्ण रिकग्निशन डेटा।  
- `korean_searchable.pdf` – एक PDF जिसे आप सर्च कर सकते हैं।  
- (वैकल्पिक) कोई भी इंटरमीडिएट लॉग जो आप जोड़ना चाहें।

## सामान्य प्रश्न और किनारे के मामलों

**What if I don’t have a GPU?**  
`EnableGpu = false` सेट करें; छोटे बैचों के लिए CPU फ़ॉलबैक पूरी तरह ठीक है।

**Can I process multiple images in one run?**  
बिल्कुल। कोर लॉजिक को `foreach (var file in Directory.GetFiles(...))` लूप में रैप करें और प्रत्येक इटरेशन में `ocrEngine.Image` को पुनः असाइन करें।

**How do I handle other languages together with Korean?**  
Aspose.OCR आपको `Language = Language.AutoDetect` सेट करने या बिटवाइज़ OR ऑपरेटर (जैसे `Language.Korean | Language.English`) से कई भाषाएँ संयोजित करने की अनुमति देता है।

**What if the OCR confidence is low?**  
`detailedResult.Pages[0].Words` को इंस्पेक्ट करें और उन एंट्रीज़ को फ़िल्टर करें जिनकी `Confidence < 0.7` है। आप प्री‑प्रोसेसिंग फ़िल्टर भी ट्यून कर सकते हैं—`PreprocessFilter.ContrastEnhancement` जोड़ने की कोशिश करें।

## निष्कर्ष

आपने अभी देखा कि कैसे **Korean Language OCR** को एंड‑टू‑एंड किया जाता है, **loading image from stream** से **extract plain text**, फिर **convert image to PDF** और अंत में **export searchable PDF** तक। यह अप्रोच मॉड्यूलर है, इसलिए आप इमेज स्रोत बदल सकते हैं, आउटपुट फ़ॉर्मेट बदल सकते हैं, या JSON को किसी भी डाउनस्ट्रीम पाइपलाइन में प्लग कर सकते हैं।

अगला क्या?

## संबंधित ट्यूटोरियल

- [Aspose.OCR का उपयोग करके भाषा चयन के साथ C# में इमेज टेक्स्ट निकालें](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Aspose OCR के साथ कई भाषाओं के लिए इमेज टेक्स्ट पहचानें](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [इमेज से टेक्स्ट निकालें – .NET के लिए Aspose.OCR के साथ OCR ऑप्टिमाइज़ेशन](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}