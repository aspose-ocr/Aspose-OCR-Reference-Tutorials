---
category: general
date: 2026-01-09
description: Aspose OCR के साथ PNG से तेज़ी से टेक्स्ट निकालें। जानें कि इमेज टेक्स्ट
  कैसे पढ़ें, OCR की सटीकता कैसे बढ़ाएँ, और C# में साफ़ परिणाम प्राप्त करें।
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: hi
og_description: Aspose OCR के साथ PNG से तेज़ी से टेक्स्ट निकालें। इमेज टेक्स्ट पढ़ना
  सीखें, OCR की सटीकता बढ़ाएँ, और C# में साफ़ परिणाम प्राप्त करें।
og_title: PNG से टेक्स्ट निकालें – पूर्ण Aspose OCR ट्यूटोरियल
tags:
- Aspose OCR
- C#
- Image Processing
title: PNG से टेक्स्ट निकालें – पूर्ण Aspose OCR ट्यूटोरियल
url: /hi/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG से टेक्स्ट निकालें – पूर्ण Aspose OCR ट्यूटोरियल

क्या आपको कभी **PNG से टेक्स्ट निकालना** पड़ा है लेकिन परिणाम बेतुके अक्षरों से भरे हुए थे? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया के प्रोजेक्ट्स – इनवॉइस, रसीदें, या स्कैन किए गए फॉर्म – में OCR आउटपुट की गुणवत्ता ऑटोमेशन पाइपलाइन को सफल या विफल कर सकती है।

इस गाइड में हम आपको Aspose OCR का उपयोग करके इमेज टेक्स्ट पढ़ने का **स्टेप‑बाय‑स्टेप** तरीका दिखाएंगे, कस्टम डिक्शनरी जोड़कर **OCR की सटीकता बढ़ाएँगे**, शोर को साफ़ करेंगे, और अंत में एक साफ़ स्ट्रिंग प्रिंट करेंगे। अंत तक आपके पास एक तैयार‑चलाने‑योग्य C# कंसोल ऐप होगा जो PNG इमेज से भरोसेमंद रूप से टेक्स्ट निकालता है।

> **आपको क्या मिलेगा**  
> * एक पूर्ण, चलाने योग्य कोड सैंपल।  
> * यह समझना कि कस्टम डिक्शनरी क्यों महत्वपूर्ण है।  
> * लो‑कॉन्ट्रास्ट स्कैन जैसे एज केस को संभालने के टिप्स।  

## आवश्यकताएँ

- .NET 6 SDK या बाद का (कोड .NET 6 को टार्गेट करता है, लेकिन .NET 5 भी काम करता है)।  
- Visual Studio 2022 या आपका पसंदीदा कोई भी एडिटर।  
- एक **PNG** इमेज जिसे आप प्रोसेस करना चाहते हैं – उदाहरण के लिए `invoice.png`।  
- **Aspose.OCR** NuGet पैकेज (`dotnet add package Aspose.OCR`)।  

कोई अतिरिक्त कॉन्फ़िगरेशन फ़ाइल की आवश्यकता नहीं है; सब कुछ एक ही `.cs` फ़ाइल में रहता है।

## चरण 1 – Aspose OCR स्थापित करें और संदर्भित करें

पहले, लाइब्रेरी को अपने प्रोजेक्ट में जोड़ें। अपने सॉल्यूशन फ़ोल्डर में एक टर्मिनल खोलें और चलाएँ:

```bash
dotnet add package Aspose.OCR
```

यह एकल लाइन नवीनतम स्थिर संस्करण (जनवरी 2026 तक, संस्करण 23.9) को फ़ेच करती है। पैकेज में `OcrEngine` क्लास शामिल है जिसका हम पूरे ट्यूटोरियल में उपयोग करेंगे।

## चरण 2 – OCR इंजन को प्रारंभ करें

एक `OcrEngine` इंस्टेंस बनाना बुनियाद है। इसे ऐसे समझें जैसे आप एक स्कैनर को चालू कर रहे हैं जो पिक्सेल को पढ़ने के लिए तैयार है।

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **प्रो टिप:** यदि आप लूप में कई इमेज प्रोसेस करने की योजना बना रहे हैं, तो वही `OcrEngine` इंस्टेंस पुनः उपयोग करें। यह आंतरिक संसाधनों को कैश करता है और बाद के कॉल्स को तेज़ बनाता है।

## चरण 3 – कस्टम डिक्शनरी के साथ सटीकता बढ़ाएँ

आउट‑ऑफ़‑द‑बॉक्स OCR अच्छा है, लेकिन यह “Aspose”, “OCR”, या “SDK” जैसे डोमेन‑स्पेसिफिक शब्दों पर ठोकर खा सकता है। इन शब्दों को **कस्टम डिक्शनरी** में जोड़ने से इंजन को पता चलता है कि ये स्ट्रिंग्स वैध हैं, जिससे गलत पहचान कम होती है।

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### कस्टम डिक्शनरी क्यों मदद करती है

- OCR के पीछे **स्टैटिस्टिकल मॉडल** सामान्य भाषा पैटर्न को भारी वज़न देते हैं। दुर्लभ शब्दों की संभावना कम होती है और वे समान दिखने वाले अक्षरों से बदल सकते हैं।  
- उन्हें स्पष्ट रूप से सूचीबद्ध करके आप मॉडल की अनुमानित प्रक्रिया को ओवरराइड करते हैं।  
- यह विशेष रूप से **इमेज टेक्स्ट पढ़ने** के लिए उपयोगी है जिसमें प्रोडक्ट कोड, संक्षिप्ताक्षर, या ब्रांड नाम होते हैं।

## चरण 4 – PNG फ़ाइल से टेक्स्ट पहचानें

अब हम इंजन को इमेज पाथ देते हैं। `RecognizeImage` मेथड एक रॉ स्ट्रिंग रिटर्न करता है जिसमें अभी भी अज्ञात टोकन (जैसे “#@!”) हो सकते हैं जिन्हें इंजन मैप नहीं कर सका।

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **एज केस:** यदि फ़ाइल नहीं मिलती, तो `RecognizeImage` `FileNotFoundException` फेंकता है। प्रोडक्शन कोड में इसे try‑catch ब्लॉक में रैप करें।

## चरण 5 – `CleanText` के साथ परिणाम साफ़ करें

Aspose OCR एक हेल्पर के साथ आता है जो “अज्ञात” के रूप में चिन्हित अक्षरों को हटाता है। यह चरण **इमेज से टेक्स्ट निकालने** वाले प्रोजेक्ट्स के लिए महत्वपूर्ण है जहाँ डाउनस्ट्रीम पार्सर केवल अल्फ़ान्यूमेरिक और बेसिक पंक्चुएशन की उम्मीद करता है।

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

`CleanText` मेथड लाइन एंडिंग्स को भी सामान्यीकृत करता है, जिससे आउटपुट को डेटाबेस में सुरक्षित रूप से स्टोर किया जा सके या अन्य सर्विसेज को पास किया जा सके।

## चरण 6 – साफ़ किए गए टेक्स्ट को आउटपुट करें

अंत में, परिणाम को डिस्प्ले या स्टोर करें। एक कंसोल ऐप में `Console.WriteLine` यह काम कर देता है।

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

जब आप प्रोग्राम चलाएँगे, तो आपको `invoice.png` की सामग्री को प्रतिबिंबित करने वाला एक साफ़ टेक्स्ट ब्लॉक दिखना चाहिए। यदि इमेज में शब्द “Aspose” है, तो कस्टम डिक्शनरी सुनिश्चित करती है कि वह सही रूप में दिखे, न कि “A5p0se” जैसा।

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ मिलाते हुए, यहाँ पूरा `Program.cs` है जिसे आप नई कंसोल प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं:

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**अपेक्षित आउटपुट** (मान लेते हैं PNG में एक साधारण इनवॉइस है):

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

यदि आपको अनचाहे प्रतीक दिखें, तो इमेज की क्वालिटी दोबारा जांचें या कस्टम डिक्शनरी में और शब्द जोड़ें।

## बोनस: कम‑गुणवत्ता स्कैन को संभालना

कभी‑कभी PNG 72 dpi पर स्कैन किए जाते हैं या उनमें भारी कम्प्रेशन आर्टिफैक्ट्स होते हैं। यहाँ कुछ त्वरित ट्रिक्स हैं जिससे **OCR की सटीकता बढ़े** बिना C# छोड़े:

1. `SixLabors.ImageSharp` जैसी लाइब्रेरी से **इमेज को प्री‑प्रोसेस** करें – कंट्रास्ट बढ़ाएँ, ग्रेस्केल में बदलें, या शोर कम करने के लिए हल्का ब्लर लागू करें।  
2. `OcrEngine` पर **`Resolution` प्रॉपर्टी सेट करें** (जैसे, `ocrEngine.Resolution = 300;`) ताकि इंजन इमेज को हाई‑रेज़ोल्यूशन मान ले।  
3. यदि आप गैर‑इंग्लिश टेक्स्ट के साथ काम कर रहे हैं तो **भाषा पैक सक्षम करें** (`ocrEngine.Language = Language.English;`)।

इन सभी तीन तरीकों को `RecognizeImage` कॉल से पहले जोड़ा जा सकता है।

## अक्सर पूछे जाने वाले प्रश्न

- **क्या यह अन्य इमेज फ़ॉर्मैट्स के साथ काम करता है?**  
  हाँ। `RecognizeImage` JPEG, BMP, TIFF, और यहाँ तक कि PDF (इमेज कंटेनर के रूप में) को भी स्वीकार करता है। वही स्टेप्स लागू होते हैं।

- **क्या मैं फ़ोल्डर में कई PNG से टेक्स्ट निकाल सकता हूँ?**  
  बिल्कुल। कोर लॉजिक को `foreach (var file in Directory.GetFiles(folder, "*.png"))` लूप में रैप करें और प्रत्येक परिणाम को लिस्ट में स्टोर करें या अलग फ़ाइलों में लिखें।

- **अगर मुझे टेक्स्ट के कॉर्डिनेट्स चाहिए तो?**  
  Aspose OCR `OcrResult` ऑब्जेक्ट्स भी देता है जिनमें बाउंडिंग बॉक्स शामिल होते हैं। उन्नत परिदृश्य के लिए `ocrEngine.RecognizeImageToResult(imagePath)` का उपयोग करें।

## निष्कर्ष

हमने Aspose OCR का उपयोग करके **PNG फ़ाइलों से टेक्स्ट निकालने** के लिए **पूरा, एंड‑टू‑एंड** समाधान दिखाया। इंजन को इनिशियलाइज़ करके, उसे **कस्टम डिक्शनरी** फ़ीड करके, रॉ आउटपुट को साफ़ करके, और कुछ सामान्य पिटफ़ॉल्स को संभालकर आप अपने C# एप्लिकेशन में भरोसेमंद रूप से **इमेज टेक्स्ट पढ़** सकते हैं और **OCR की सटीकता बढ़ा** सकते हैं।

अगला कदम तैयार है? PNG को स्कैन की गई रसीद से बदलें, डिक्शनरी में और डोमेन‑स्पेसिफिक शब्द जोड़ें, या आउटपुट को डेटाबेस के साथ इंटीग्रेट करके ऑटोमैटिक इनवॉइस प्रोसेसिंग बनाएं। जब आप Aspose OCR को .NET के समृद्ध इकोसिस्टम के साथ मिलाते हैं तो संभावनाएँ अनंत हैं।

हैप्पी कोडिंग, और आपका OCR हमेशा स्पॉट‑ऑन रहे! 

![PNG से टेक्स्ट निकालने का उदाहरण](/images/extract-text-from-png.png "PNG से टेक्स्ट निकालें – Aspose OCR डेमो")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}