---
category: general
date: 2026-04-03
description: C# में Aspose OCR का उपयोग करके इमेज को डेस्क्यू कैसे करें – OCR के लिए
  इमेज को प्री‑प्रोसेस करना सीखें, इमेज से टेक्स्ट पहचानें और मिनटों में OCR की सटीकता
  बढ़ाएँ।
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from image
- improve ocr accuracy
- load image for ocr
language: hi
og_description: C# में Aspose OCR का उपयोग करके छवि को डेस्क्यू कैसे करें। यह गाइड
  आपको दिखाता है कि OCR के लिए छवि को कैसे प्रीप्रोसेस करें, छवि से टेक्स्ट को पहचानें
  और सटीकता बढ़ाएँ।
og_title: Aspose OCR के साथ इमेज को डेस्क्यू कैसे करें – पूर्ण C# गाइड
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Aspose OCR के साथ छवि को डेस्क्यू कैसे करें – पूर्ण C# गाइड
url: /hi/net/ocr-optimization/how-to-deskew-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR के साथ इमेज को डेस्क्यू कैसे करें – पूर्ण C# गाइड

क्या आपने कभी **इमेज को डेस्क्यू करने** के बारे में सोचा है इससे पहले कि आप इसे OCR इंजन को दें? आप अकेले नहीं हैं—झुके हुए स्कैन, कोण पर ली गई तस्वीरें, या यहाँ तक कि थोड़ा टेढ़े-मेढ़े PDFs भी किसी भी टेक्स्ट‑रिकग्निशन लाइब्रेरी को भ्रमित कर सकते हैं।  

इस चरण‑दर‑चरण ट्यूटोरियल में हम पूरे वर्कफ़्लो को देखेंगे: चित्र को लोड करने से लेकर, **OCR के लिए इमेज को प्री‑प्रोसेस** (डेस्क्यू, डिनॉइज़, कॉन्ट्रास्ट बूस्ट, ऑटो‑रोटेट) तक, और अंत में **इमेज से टेक्स्ट को पहचानना** Aspose OCR के साथ, तथा कुछ टिप्स **OCR की सटीकता बढ़ाने** के लिए। अंत तक आपके पास एक तैयार‑चलाने‑योग्य C# कंसोल ऐप होगा जो शोरयुक्त, झुकी हुई PNG को प्रो की तरह संभालता है।

## आपको क्या चाहिए

- **.NET 6+** (या .NET Framework 4.7.2 – API समान काम करता है)
- **Aspose.OCR for .NET** NuGet पैकेज (`Install-Package Aspose.OCR`)
- एक सैंपल इमेज जो **झुकी हुई** और **शोरयुक्त** हो (उदाहरण के लिए `skewed_noisy.png`)
- Visual Studio, Rider, या कोई भी एडिटर जो आपको पसंद हो – कोई विशेष टूलिंग आवश्यक नहीं

> **Pro tip:** यदि आपके पास झुकी हुई सैंपल नहीं है, तो Paint में एक साफ़ स्क्रीनशॉट को 10‑15° घुमा दें और इमेज एडिटर से थोड़ा “साल्ट‑एंड‑पेपर” शोर जोड़ें। कोड उसी तरह काम करता है।

अब, चलिए शुरू करते हैं।

## इमेज को डेस्क्यू कैसे करें और OCR की सटीकता बढ़ाएँ

पहली चीज़ जो आपको करनी है वह है Aspose के `OcrEngine` को **डेस्क्यू** करने के लिए बताना, जो आने वाले बिटमैप को सीधा करता है। इस इंजन में एक बिल्ट‑इन `ImagePreprocessingOptions` क्लास है जो आपको एक साथ कई क्वालिटी‑बढ़ाने वाली सुविधाएँ टॉगल करने देती है।

```csharp
using Aspose.OCR;
using System.Drawing;

/// <summary>
/// Demonstrates how to deskew image, denoise, boost contrast, and run OCR.
/// </summary>
class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing options
        ImagePreprocessingOptions opts = new ImagePreprocessingOptions
        {
            Deskew = true,          // <-- this is the key to how to deskew image
            Denoise = true,
            ContrastBoost = 30,    // increase contrast by 30 %
            AutoRotate = true
        };
        ocrEngine.PreprocessingOptions = opts;

        // 3️⃣ Load the image you want to process
        Image input = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run OCR on the pre‑processed bitmap
        string text = ocrEngine.Recognize(input);

        // 5️⃣ Show the result
        System.Console.WriteLine(text);
    }
}
```

### यह क्यों काम करता है

- **Deskew = true** इंजन को बताता है कि वह टेक्स्ट बेसलाइन का पता लगाए और इमेज को तब तक घुमाए जब तक बेसलाइन क्षैतिज न हो जाए। इसके बिना, केवल 5° का झुकाव भी सटीकता को 15‑20 % तक घटा सकता है।
- **Denoise** उन रैंडम स्पीकल्स को हटाता है जो अक्सर कम‑रिज़ॉल्यूशन दस्तावेज़ स्कैन करने के बाद दिखाई देते हैं।
- **ContrastBoost** फोरग्राउंड (टेक्स्ट) और बैकग्राउंड (पेपर) के बीच अंतर को बढ़ाता है, जो **OCR की सटीकता बढ़ाने** के लिए आवश्यक है।
- **AutoRotate** पोर्ट्रेट बनाम लैंडस्केप ओरिएंटेशन को स्वचालित रूप से संभालता है, जिससे आपको मैन्युअल चेक करने की जरूरत नहीं पड़ती।

ऊपर दिया गया कोड एक **पूरा, चलाने योग्य उदाहरण** है—सिर्फ `YOUR_DIRECTORY` को अपनी फ़ाइल के पाथ से बदलें और F5 दबाएँ।

## OCR के लिए इमेज को प्री‑प्रोसेस – डिनॉइज़िंग और कॉन्ट्रास्ट बूस्ट

आप सोच सकते हैं कि क्या आपको वास्तव में डिनॉइज़िंग और कॉन्ट्रास्ट एन्हांसमेंट दोनों की जरूरत है। छोटा जवाब: **हाँ, अधिकांश वास्तविक‑दुनिया के मामलों में**। यहाँ एक त्वरित विवरण है:

| फीचर | क्या करता है | कब महत्वपूर्ण है |
|---------|--------------|-----------------|
| **Deskew** | झुकी हुई टेक्स्ट लाइनों को सीधा करता है | स्कैन किए फ़ॉर्म, फ़ोन‑कैमरा कैप्चर |
| **Denoise** | अलग‑अलग पिक्सेल हटाता है | कम‑रोशनी स्कैन, सस्ते स्कैनर |
| **ContrastBoost** | गहरे टेक्स्ट को हल्का और बैकग्राउंड को गहरा करता है | फीके दस्तावेज़, फीका इंक |
| **AutoRotate** | पोर्ट्रेट बनाम लैंडस्केप का पता लगाता है | मिश्रित ओरिएंटेशन वाले मल्टी‑पेज PDFs |

यदि आप एक शुद्ध, पूरी तरह संरेखित स्कैन प्रोसेस कर रहे हैं, तो आप फ़्लैग्स को बंद कर सकते हैं, लेकिन **OCR के लिए इमेज को प्री‑प्रोसेस** एक सुरक्षित डिफ़ॉल्ट है जो शायद ही कभी नुकसान पहुंचाता है।

## इमेज से टेक्स्ट को पहचानें – Aspose OCR का उपयोग करके

जब प्री‑प्रोसेसिंग पाइपलाइन समाप्त हो जाती है, तो इंजन साफ़ किए गए बिटमैप को अपने आंतरिक रिकग्नाइज़र को देता है। `Recognize` मेथड एक साधारण `string` लौटाता है जिसमें लाइन ब्रेक संरक्षित रहते हैं। यदि आवश्यक हो तो आप परिणाम को आगे पोस्ट‑प्रोसेस कर सकते हैं (जैसे, व्हाइटस्पेस ट्रिम करना, स्पेल‑चेक चलाना)।

```csharp
string recognizedText = ocrEngine.Recognize(inputImage);
Console.WriteLine("--- OCR RESULT ---");
Console.WriteLine(recognizedText);
```

### अपेक्षित आउटपुट

यदि `skewed_noisy.png` में वाक्य “Hello World!” है, तो कंसोल कुछ इस तरह प्रिंट करेगा:

```
--- OCR RESULT ---
Hello World!
```

मध्यम शोर के साथ भी, आपको **95 % से अधिक सटीकता** दिखनी चाहिए, धन्यवाद उन प्री‑प्रोसेसिंग स्टेप्स को जो हमने सक्षम किए हैं।

## OCR के लिए इमेज लोड करें – फ़ाइल‑हैंडलिंग टिप्स

`Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png")` लाइन **OCR के लिए इमेज लोड करने** का सबसे सरल तरीका है, लेकिन कुछ बारीकियों को ध्यान में रखना चाहिए:

1. **File locks** – `FromFile` फ़ाइल हैंडल को तब तक खुला रखता है जब तक `Image` डिस्पोज़ नहीं हो जाता। यदि आप बाद में फ़ाइल को डिलीट या मूव करने की योजना बनाते हैं तो इसे `using` ब्लॉक में रैप करें।
2. **Supported formats** – Aspose OCR BMP, JPEG, PNG, TIFF, और GIF को सपोर्ट करता है। यदि आपके पास PDFs हैं, तो प्रत्येक पेज को पहले इमेज के रूप में एक्सट्रैक्ट करें (Aspose.PDF मदद कर सकता है)।
3. **Memory usage** – बड़े इमेज (5 MP से अधिक) काफी RAM खा सकते हैं। यदि आप `OutOfMemoryException` का सामना करते हैं तो इंजन को पास करने से पहले `Bitmap` के साथ डाउन‑स्केल करने पर विचार करें।

```csharp
using (Image input = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png"))
{
    string result = ocrEngine.Recognize(input);
    Console.WriteLine(result);
}
```

## OCR की सटीकता बढ़ाएँ – वास्तविक‑दुनिया की टिप्स

स्वचालित प्री‑प्रोसेसिंग के साथ भी, कुछ एज केस अभी भी OCR इंजनों को भ्रमित कर सकते हैं। नीचे कुछ सिद्ध रणनीतियाँ हैं जिन्हें आप अपने पाइपलाइन में जोड़ सकते हैं:

- **Binarize the image** (`opts.Binarization = true`) जब बैकग्राउंड असमान हो।
- **Set language** (`ocrEngine.Language = Language.English`) ताकि कैरेक्टर सेट सीमित हो सके।
- **Increase DPI**: यदि आप स्कैनिंग प्रक्रिया को नियंत्रित करते हैं, तो कम से कम 300 dpi का लक्ष्य रखें।
- **Crop margins**: बड़े सफ़ेद बॉर्डर हटाएँ; वे लाइन डिटेक्शन को भ्रमित कर सकते हैं।
- **Validate output**: रेगुलर एक्सप्रेशन्स का उपयोग करके डेट, नंबर, या ज्ञात पैटर्न चेक करें, फिर कम‑कनफ़िडेंस लाइनों को मैन्युअल रिव्यू के लिए फ्लैग करें।

> **Remember:** लक्ष्य सिर्फ **इमेज से टेक्स्ट को पहचानना** नहीं है, बल्कि इसे विभिन्न दस्तावेज़ क्वालिटी में भरोसेमंद तरीके से करना है।

## पूर्ण कार्यशील उदाहरण – सभी स्टेप्स एक फ़ाइल में

नीचे अंतिम, स्व-समाहित प्रोग्राम है जिसे आप नई कंसोल प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं।

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class DeskewOcrDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine engine = new OcrEngine();

        // Preprocess settings (deskew, denoise, contrast, auto‑rotate)
        engine.PreprocessingOptions = new ImagePreprocessingOptions
        {
            Deskew = true,
            Denoise = true,
            ContrastBoost = 30,
            AutoRotate = true
        };

        // Load image – make sure the path is correct
        const string imagePath = @"YOUR_DIRECTORY/skewed_noisy.png";

        // Using block prevents file‑handle leaks
        using (Image img = Image.FromFile(imagePath))
        {
            // Run OCR
            string text = engine.Recognize(img);

            // Output result
            Console.WriteLine("--- OCR RESULT ---");
            Console.WriteLine(text);
        }
    }
}
```

प्रोग्राम चलाएँ, और आपको कंसोल में साफ़, डेस्क्यू किया हुआ टेक्स्ट प्रिंट होता दिखेगा। यदि आप `skewed_noisy.png` को एक साफ़, सीधा स्कैन से बदलते हैं, तो आउटपुट समान रहेगा—सिर्फ एक छोटा परफॉर्मेंस बूस्ट क्योंकि इंजन डेस्क्यू स्टेप को स्किप कर देता है।

## निष्कर्ष

हमने Aspose OCR का उपयोग करके **इमेज को डेस्क्यू करने** का तरीका कवर किया, आपको **OCR के लिए इमेज को प्री‑प्रोसेस** करने का दिखाया, **OCR के लिए इमेज लोड करने** का सही तरीका प्रदर्शित किया, और अंत में **इमेज से टेक्स्ट को पहचानने** के साथ **OCR की सटीकता बढ़ाने** पर ध्यान दिया। पूरा कोड स्निपेट किसी भी .NET प्रोजेक्ट में डालने के लिए तैयार है, और अतिरिक्त टिप्स आपको कठिन इनपुट को संभालने के लिए एक रोडमैप देते हैं।

अगली चुनौती के लिए तैयार हैं? कई इमेज को जोड़कर एक मल्टी‑पेज OCR वर्कफ़्लो बनाएं, या गैर‑अंग्रेज़ी दस्तावेज़ों के लिए कस्टम भाषा पैक्स के साथ प्रयोग करें। वही प्री‑प्रोसेसिंग सिद्धांत लागू होते हैं—डेस्क्यू, डिनॉइज़, कॉन्ट्रास्ट बूस्ट, और Aspose को भारी काम करने दें।

किसी विशेष फ़ाइल टाइप के बारे में सवाल हैं या `ContrastBoost` वैल्यू को ट्यून करने में मदद चाहिए? नीचे टिप्पणी छोड़ें या Aspose फ़ोरम पर पूछें। कोडिंग का आनंद लें, और आपका OCR हमेशा सटीक रहे!  

![बाएँ ओर मूल झुकी हुई इमेज और दाएँ ओर डेस्क्यू की हुई, साफ़ परिणाम दिखाता डायग्राम](deskew-diagram.png "मूल झुकी हुई इमेज और डेस्क्यू परिणाम दिखाने वाला डायग्राम – इमेज को डेस्क्यू करने का उदाहरण")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}