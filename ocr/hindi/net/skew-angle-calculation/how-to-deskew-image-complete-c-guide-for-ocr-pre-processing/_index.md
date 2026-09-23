---
category: general
date: 2025-12-29
description: Aspose OCR के साथ छवि को डेस्क्यू करना, बैकग्राउंड हटाना और टेक्स्ट निकालना
  सीखें। OCR के लिए छवि को पूर्व‑प्रसंस्करण करने और छवि से टेक्स्ट पहचानने हेतु चरण‑दर‑चरण
  C# कोड।
draft: false
keywords:
- how to deskew image
- how to remove background
- how to extract text
- preprocess image for ocr
- recognize text from image
language: hi
og_description: इमेज को डेस्क्यू करने और OCR की सटीकता बढ़ाने का तरीका। इस गाइड का
  पालन करके बैकग्राउंड हटाएँ, OCR के लिए इमेज को प्रीप्रोसेस करें और Aspose का उपयोग
  करके इमेज से टेक्स्ट पहचानें।
og_title: इमेज को डेस्क्यू कैसे करें – C# OCR प्री‑प्रोसेसिंग ट्यूटोरियल
tags:
- Aspose OCR
- C#
- Image preprocessing
title: छवि को कैसे सीधा करें – OCR प्री‑प्रोसेसिंग के लिए पूर्ण C# गाइड
url: /hi/net/skew-angle-calculation/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज को डेस्क्यू कैसे करें – OCR प्री‑प्रोसेसिंग के लिए पूर्ण C# गाइड

क्या आप कभी सोचते थे कि स्कैनर से निकली इमेज फ़ाइलें, जो एक टेढ़ी पोस्टकार्ड जैसी दिखती हैं, उन्हें **how to deskew image** कैसे किया जाए? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में स्रोत चित्र झुके हुए, शोरयुक्त, या धब्बेदार पृष्ठभूमि से ग्रस्त होते हैं, और इससे OCR बाधित हो जाता है।  

इस ट्यूटोरियल में हम एक व्यावहारिक समाधान के माध्यम से चलेंगे जो न केवल **how to deskew image** करता है बल्कि **how to remove background**, **how to extract text**, और अंत में **recognize text from image** को Aspose OCR for .NET का उपयोग करके करता है। अंत तक आपके पास एक तैयार‑चलाने‑योग्य C# प्रोग्राम होगा जो OCR के लिए इमेज को प्री‑प्रोसेस करता है और साफ़, खोज योग्य टेक्स्ट लौटाता है।

## आपको क्या चाहिए

- .NET 6 SDK या बाद का (कोड .NET Core और .NET Framework दोनों पर काम करता है)  
- Visual Studio 2022 (या कोई भी एडिटर जो आप पसंद करते हैं)  
- Aspose.OCR NuGet पैकेज (`Install-Package Aspose.OCR`)  
- एक सैंपल इमेज जो skewed और noisy हो (जैसे, `skewed_noisy.jpg`)  

बस इतना ही—कोई अतिरिक्त नेटिव लाइब्रेरी नहीं, कोई जटिल कमांड‑लाइन टूल नहीं। चलिए शुरू करते हैं।

## चरण 1 – इनपुट इमेज लोड करें (How to Deskew Image यहाँ से शुरू होता है)

सबसे पहला काम है इमेज को मेमोरी में लाना। Aspose OCR का `Image.Load` मेथड फ़ाइल पाथ को स्वीकार करता है और एक `Image` ऑब्जेक्ट लौटाता है जिसे आप बदल सकते हैं।

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Program
{
    static void Main()
    {
        // Load the original photo that needs deskewing and cleaning
        Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Why this matters:** इमेज को लोड करने से हमें एक हैंडल मिलता है जिससे हम बाद की सभी ट्रांसफ़ॉर्मेशन लागू कर सकते हैं, डेस्क्यूइंग से लेकर बैकग्राउंड रिमूवल तक।

## चरण 2 – इमेज को डेस्क्यू करें (How to Deskew Image in Practice)

Aspose OCR एक सुविधाजनक `Deskew` फ़िल्टर के साथ आता है जो टिल्ट एंगल को स्वचालित रूप से डिटेक्ट करता है, एक कॉन्फ़िगरेबल थ्रेशोल्ड तक। यहाँ हम **5°** तक की अनुमति देते हैं क्योंकि अधिकांश स्कैन किए गए दस्तावेज़ इससे अधिक नहीं होते।

```csharp
        // Auto‑detect and correct rotation up to 5 degrees
        Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);
```

> **Pro tip:** यदि आपके दस्तावेज़ 5° से अधिक घुमा हुए हैं, तो `angleThreshold` को 10 या 15 कर दें। एल्गोरिद्म बड़े एंगल्स पर भी तेज़ रहता है।

## चरण 3 – डेस्क्यू की गई इमेज को डीनॉइज़ करें

शोर OCR की सटीकता का मौन मारक है। एक सरल डीनॉइज़ पास स्पीकल्स को स्मूद करता है बिना वास्तविक अक्षरों को ब्लर किए।

```csharp
        // Reduce random speckles and grain
        Image denoised = deskewed.Denoise();
```

> **What happens under the hood?** फ़िल्टर एक मीडियन ब्लर लागू करता है जो किनारों (अक्षरों) को संरक्षित रखता है जबकि अलग‑अलग पिक्सेल्स को दबा देता है।

## चरण 4 – बैकग्राउंड हटाएँ (How to Remove Background Effectively)

हल्का या पैटर्न वाला बैकग्राउंड OCR इंजन को भ्रमित कर सकता है। Aspose OCR का `RemoveBackground` मेथड फ़ोरग्राउंड टेक्स्ट को अलग करता है।

```csharp
        // Strip away uneven lighting or paper texture
        Image processedImage = denoised.RemoveBackground();
```

> **Why remove background?** टेक्स्ट और उसके कैनवास के बीच कंट्रास्ट बढ़ाकर, इंजन अक्षरों को अधिक भरोसेमंद तरीके से अलग कर सकता है, जो सीधे **how to extract text** परिणामों को सुधारता है।

## चरण 5 – OCR इंजन को इनिशियलाइज़ करें

अब जब इमेज सीधी, साफ़ और हाई‑कंट्रास्ट है, हम OCR इंजन को इंस्टैंशिएट करते हैं। बेसिक लैटिन स्क्रिप्ट्स के लिए कोई अतिरिक्त कॉन्फ़िगरेशन नहीं चाहिए, लेकिन आवश्यकता पड़ने पर आप भाषा बदल सकते हैं।

```csharp
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Note:** Aspose OCR 100 से अधिक भाषाओं को सपोर्ट करता है। यदि आपको मल्टी‑लैंग्वेज सपोर्ट चाहिए, तो रिकग्निशन से पहले `ocrEngine.Language = OcrLanguage.YourLanguage;` सेट करें।

## चरण 6 – इमेज से टेक्स्ट रिकग्नाइज़ करें (How to Extract Text)

इंजन तैयार होने पर, इसे प्री‑प्रोसेस्ड इमेज दें। `Recognize` मेथड एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें रॉ टेक्स्ट और कॉन्फिडेंस स्कोर होते हैं।

```csharp
        // Perform the actual OCR
        OcrResult ocrResult = ocrEngine.Recognize(processedImage);
```

> **Result insight:** `ocrResult.Text` साधारण स्ट्रिंग रखता है, जबकि `ocrResult.Confidence` (यदि आप क्वेरी करें) आपको बताता है कि इंजन प्रत्येक लाइन के बारे में कितना निश्चित है।

## चरण 7 – रिकग्नाइज़्ड टेक्स्ट आउटपुट करें

अंत में, निकाले गए टेक्स्ट को कंसोल में प्रिंट करें—या इसे फ़ाइल, डेटाबेस, या जो भी आपके वर्कफ़्लो में फिट हो, उसमें लिखें।

```csharp
        // Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

पूरा प्रोग्राम अब चलाने योग्य है। इसे बिल्ड और रन करें, और आपको साफ़, पढ़ने योग्य टेक्स्ट दिखेगा भले ही स्रोत इमेज शुरू में skewed और noisy थी।

![इमेज को डेस्क्यू करने का उदाहरण](/images/deskew-demo.png "Aspose OCR का उपयोग करके इमेज को डेस्क्यू करने का डेमो")

*ऊपर की स्क्रीनशॉट डेस्क्यू की गई इमेज का पहले‑और‑बाद दिखाती है, जो प्री‑प्रोसेसिंग पाइपलाइन के प्रभाव को दर्शाती है।*

## किनारे के केस और सामान्य प्रश्न

### यदि इमेज 5° से अधिक घुमाई गई हो तो क्या करें?

`Deskew` कॉल में `angleThreshold` बढ़ाएँ। एल्गोरिद्म अभी भी सही एंगल को ऑटो‑डिटेक्ट करेगा, बस एक बड़े सर्च विंडो में।

### मेरे दस्तावेज़ में रंगीन टेक्स्ट है—क्या `RemoveBackground` इसे बिगाड़ देगा?

`RemoveBackground` ल्यूमिनेंस पर काम करता है, इसलिए रंगीन टेक्स्ट को क्लीनिंग से पहले ग्रेस्केल में बदल दिया जाता है। यदि आपको डाउनस्ट्रीम प्रोसेसिंग के लिए रंग बनाए रखना है, तो इस स्टेप को छोड़ दें और केवल डीनॉइज़िंग पर भरोसा करें।

### मल्टी‑पेज PDF को कैसे हैंडल करें?

प्रत्येक PDF पेज को इमेज में कन्वर्ट करें (जैसे, Aspose.PDF का उपयोग करके), फिर प्रत्येक इमेज को उसी पाइपलाइन से गुजारें। पेजों पर लूप करें और `ocrResult.Text` स्ट्रिंग्स को जोड़ें।

### हस्तलिखित नोट्स की सटीकता कैसे बढ़ा सकते हैं?

`ocrEngine.Options.UseNeuralNetwork = true;` को सक्षम करने पर विचार करें (नए Aspose संस्करणों में उपलब्ध) और प्रोसेसिंग से पहले इमेज रेज़ोल्यूशन को कम से कम 300 dpi तक बढ़ाएँ।

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा सोर्स फ़ाइल है जिसमें सभी आवश्यक `using` निर्देश और कमेंट्स हैं। इसे एक नए कंसोल प्रोजेक्ट में पेस्ट करें और **F5** दबाएँ।

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the original image (skewed, noisy, etc.)
            Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");

            // 2️⃣ Deskew – auto‑detect tilt up to 5°
            Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);

            // 3️⃣ Denoise – smooth out speckles
            Image denoised = deskewed.Denoise();

            // 4️⃣ Remove background – boost contrast
            Image processedImage = denoised.RemoveBackground();

            // 5️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 6️⃣ Recognize text from the cleaned image
            OcrResult ocrResult = ocrEngine.Recognize(processedImage);

            // 7️⃣ Output the extracted text
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**अपेक्षित आउटपुट** (एक साधारण इनवॉइस का उदाहरण):

```
=== OCR Output ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,250.00
Thank you for your business!
```

यदि आउटपुट गड़बड़ दिखे, तो दोबारा जांचें कि स्रोत इमेज पर्याप्त स्पष्ट है और डेस्क्यू एंगल आपके सेट किए हुए थ्रेशोल्ड से बड़ा नहीं है।

## निष्कर्ष

हमने **how to deskew image** को चरण‑दर‑चरण कवर किया, **how to remove background** दिखाया, प्री‑प्रोसेसिंग द्वारा **how to extract text** प्रदर्शित किया, और अंत में Aspose OCR का उपयोग करके **recognize text from image** किया। पूरी पाइपलाइन एक कॉम्पैक्ट C# प्रोग्राम में है जिसे आप बैच प्रोसेसिंग, PDF कन्वर्ज़न, या बड़े डॉक्यूमेंट‑मैनेजमेंट सिस्टम में इंटीग्रेशन के लिए विस्तारित कर सकते हैं।

अगली चुनौती के लिए तैयार हैं? इस पाइपलाइन में स्कैन किए हुए PDFs के फ़ोल्डर को फीड करने की कोशिश करें, या विभिन्न डीनॉइज़ सेटिंग्स के साथ प्रयोग करें यह देखने के लिए कि वे कॉन्फिडेंस स्कोर को कैसे प्रभावित करती हैं। जितना अधिक आप पैरामीटर्स के साथ खेलेंगे, उतना ही आप स्पीड और एक्यूरेसी के बीच ट्रेड‑ऑफ़ को समझ पाएँगे।

कोई प्रश्न या कठिन इमेज है जो अभी भी सहयोग नहीं कर रही? नीचे कमेंट छोड़ें, और साथ में ट्रबलशूट करें। कोडिंग का आनंद लें, और आपके OCR परिणाम हमेशा क्रिस्टल‑क्लियर रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}