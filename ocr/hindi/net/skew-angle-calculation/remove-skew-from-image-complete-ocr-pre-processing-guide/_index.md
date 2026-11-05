---
category: general
date: 2026-02-14
description: छवि से स्क्यू हटाना, OCR के लिए छवि को पूर्व-प्रसंस्करण करना, छवि में
  शोर कम करना और C# में Aspose OCR का उपयोग करके छवि से पाठ निकालना सीखें।
draft: false
keywords:
- remove skew from image
- preprocess image for ocr
- reduce noise in image
- extract text from image
- recognize text from document
language: hi
og_description: छवि से विकृति हटाएँ, OCR के लिए छवि को पूर्व-प्रसंस्करण करें और Aspose
  OCR का उपयोग करके चरण-दर-चरण C# ट्यूटोरियल के साथ छवि से पाठ निकालें।
og_title: इमेज से स्क्यू हटाएँ – पूर्ण OCR प्री‑प्रोसेसिंग गाइड
tags:
- OCR
- CSharp
- ImageProcessing
title: इमेज से स्क्यू हटाएँ – पूर्ण OCR प्री‑प्रोसेसिंग गाइड
url: /hi/net/skew-angle-calculation/remove-skew-from-image-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज से स्क्यू हटाएँ – पूर्ण OCR प्री‑प्रोसेसिंग गाइड

क्या आपको कभी OCR इंजन को फ़ीड करने से पहले **इमेज से स्क्यू हटाने** की ज़रूरत पड़ी है? आप अकेले नहीं हैं—स्कैन किए गए दस्तावेज़, रसीदों की फ़ोटो, या स्क्रीनशॉट अक्सर टिल्टेड आते हैं, और वह छोटा एंगल टेक्स्ट रिकग्निशन को बिगाड़ सकता है।  

अच्छी खबर? Aspose OCR के कुछ फ़िल्टरों की मदद से आप इमेज को सीधा कर सकते हैं, शोर कम कर सकते हैं, कंट्रास्ट बढ़ा सकते हैं, और फिर **इमेज से टेक्स्ट निकालें** एक ही सहज पाइपलाइन में। इस गाइड में हम पूरी प्रक्रिया को देखेंगे, स्क्यू वाली तस्वीर को लोड करने से लेकर **डॉक्यूमेंट से टेक्स्ट पहचानें** और परिणाम प्रिंट करने तक।

---

## आप क्या बनाएँगे

इस ट्यूटोरियल के अंत तक आपके पास एक तैयार‑चलाने योग्य C# कंसोल ऐप होगा जो:

1. `DeskewFilter` का उपयोग करके **इमेज से स्क्यू हटाता है**।  
2. `DenoiseFilter` के साथ **इमेज में शोर कम करता है**।  
3. कंट्रास्ट बढ़ाकर **OCR के लिए इमेज को प्री‑प्रोसेस करता है**।  
4. Aspose OCR के `Engine` के माध्यम से **डॉक्यूमेंट से टेक्स्ट पहचानता है**।  
5. **इमेज से टेक्स्ट निकालता है** और कंसोल पर दिखाता है।  

कोई बाहरी सर्विस नहीं, सिर्फ Aspose OCR NuGet पैकेज और कुछ लाइनों का कोड।

## आवश्यकताएँ

- .NET 6.0 SDK या उससे नया (कोड .NET Core और .NET Framework पर भी काम करता है)।  
- Visual Studio 2022 या कोई भी एडिटर जो आपको पसंद हो।  
- Aspose.OCR for .NET स्थापित (`dotnet add package Aspose.OCR`)।  
- `skewed_noisy.jpg` नाम की सैंपल इमेज को किसी फ़ोल्डर में रखें जिसे आप रेफ़र कर सकें।  

यदि आपके पास ये हैं, तो चलिए शुरू करते हैं।

## चरण 1: स्रोत इमेज लोड करें

पहली चीज़ जो हमें चाहिए वह है एक `ImageStream` जो उस फ़ाइल की ओर इशारा करता है जिसे हम साफ़ करना चाहते हैं।

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the source image that needs cleaning
ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **यह क्यों महत्वपूर्ण है:** `ImageStream` अंतर्निहित बिटमैप को एब्स्ट्रैक्ट करता है, जिससे Aspose फ़िल्टर बिना आपको रॉ पिक्सेल डेटा मैनेज किए काम कर सकते हैं।

## चरण 2: प्री‑प्रोसेसिंग पाइपलाइन बनाएं (स्क्यू हटाएँ और शोर कम करें)

प्रत्येक फ़िल्टर को अलग‑अलग कॉल करने के बजाय, Aspose आपको उन्हें `ImageProcessingPipeline` में चेन करने देता है। इससे कोड साफ़ रहता है और ऑपरेशन्स सही क्रम में होते हैं।

```csharp
// Create a pipeline and add desired filters
var processingPipeline = new ImageProcessingPipeline()
    .AddFilter(new DeskewFilter())                     // Remove skew
    .AddFilter(new DenoiseFilter())                    // Reduce noise
    .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)
```

### क्रम का महत्व क्यों है

1. **Deskew पहले** – डेनॉइज़िंग से पहले इमेज को सीधा करने से शोर फ़िल्टर स्लैंटेड एजेज़ को आर्टिफैक्ट्स समझने से बचता है।  
2. **Denoise दूसरा** – जब तस्वीर लेवल पर हो जाती है, एल्गोरिद्म सिग्नल को ग्रेन से बेहतर अलग कर सकता है।  
3. **Contrast boost आख़िर में** – इमेज साफ़ होने के बाद कंट्रास्ट बढ़ाने से OCR पढ़ने योग्यता अधिकतम होती है बिना शोर बढ़ाए।  

## चरण 3: पाइपलाइन लागू करें और साफ़ इमेज प्राप्त करें

अब हम मूल स्ट्रीम पर पाइपलाइन चलाते हैं।

```csharp
// Apply the pipeline to obtain a cleaned image
ImageStream cleanedImage = processingPipeline.Apply(sourceImage);
```

इस चरण पर इमेज डेस्क्यू, डेनॉइज़्ड और उच्च कंट्रास्ट वाली है—OCR के लिए एकदम उपयुक्त।

## चरण 4: OCR इंजन को इनिशियलाइज़ करें और टेक्स्ट पहचानें

एक साफ़ इमेज हाथ में होने पर हम अंततः इसे Aspose OCR में फ़ीड कर सकते हैं।

```csharp
// Initialise the OCR engine
Engine ocrEngine = new Engine();

// Recognise text from the cleaned image
OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);
```

> **टिप:** यदि आपको भाषा‑विशिष्ट ट्यूनिंग चाहिए, तो `Engine` एक `Language` प्रॉपर्टी स्वीकार करता है (जैसे, `ocrEngine.Language = Language.English;`)। अधिकांश लैटिन‑आधारित दस्तावेज़ों के लिए डिफ़ॉल्ट ठीक काम करता है।

## चरण 5: निकाले गए टेक्स्ट को दिखाएँ

एक त्वरित `Console.WriteLine` परिणाम दिखाता है।

```csharp
// Output the extracted text
Console.WriteLine(ocrResult.Text);
```

जब आप प्रोग्राम चलाएँगे तो आपको `skewed_noisy.jpg` की टेक्स्टुअल सामग्री टर्मिनल में प्रिंट होती दिखेगी—साफ़, पठनीय, और डाउनस्ट्रीम प्रोसेसिंग के लिए तैयार।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा, कॉपी‑पेस्ट‑तैयार प्रोग्राम है। इसे `Program.cs` के रूप में सेव करें, `YOUR_DIRECTORY` को वास्तविक पाथ से बदलें, और `dotnet run` चलाएँ।

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the source image that needs cleaning
            ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

            // Step 2: Create an image‑processing pipeline and add desired filters
            var processingPipeline = new ImageProcessingPipeline()
                .AddFilter(new DeskewFilter())                     // Remove skew
                .AddFilter(new DenoiseFilter())                    // Reduce noise
                .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)

            // Step 3: Apply the pipeline to obtain a cleaned image
            ImageStream cleanedImage = processingPipeline.Apply(sourceImage);

            // Step 4: Initialise the OCR engine and recognize text from the cleaned image
            Engine ocrEngine = new Engine();
            OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);

            // Step 5: Display the extracted text
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**अपेक्षित आउटपुट** (एक साधारण रसीद का उदाहरण):

```
=== Extracted Text ===
Store: Coffee Corner
Date: 02/12/2026
Item          Qty   Price
Latte          2    $5.80
Croissant      1    $2.50
Total                $8.30
```

यदि आउटपुट गड़बड़ दिखे, तो इमेज पाथ सही है और स्रोत फ़ाइल में वास्तव में पढ़ने योग्य टेक्स्ट है, यह दोबारा जाँचें।

## सामान्य प्रश्न और किनारे के मामले

### अगर इमेज 90° घुमा हुआ है, न कि हल्का स्क्यू?

`DeskewFilter` छोटे एंगल (±15°) को संभालता है। पूर्ण रोटेशन के लिए, डेस्क्यू स्टेप से पहले `new RotateFilter { Angle = 90 }` कॉल करें।

### मेरी इमेज PNG फ़ॉर्मेट में है—क्या कुछ बदलता है?

नहीं। `ImageStream.FromFile` फ़ॉर्मेट को ऑटो‑डिटेक्ट करता है, इसलिए PNG, JPEG, BMP, या TIFF सभी एक ही तरह काम करते हैं।

### मैं शोर कम करने की शक्ति को कैसे ट्यून करूँ?

`DenoiseFilter` एक `Strength` प्रॉपर्टी (0‑100) प्रदान करता है। उच्च मान अधिक ग्रेन हटाते हैं लेकिन बारीक विवरण धुंधला कर सकते हैं। टेक्स्ट‑भारी दस्तावेज़ों के लिए 30‑50 के आसपास के मानों के साथ प्रयोग करें।

### मुझे फ़ाइलों की बैच प्रोसेस करनी है—क्या मैं पाइपलाइन को पुनः उपयोग कर सकता हूँ?

बिल्कुल। `processingPipeline` को एक बार बनाएं, फिर प्रत्येक फ़ाइल पर लूप करें:

```csharp
foreach (var path in Directory.GetFiles("batch_folder", "*.jpg"))
{
    var src = ImageStream.FromFile(path);
    var cleaned = processingPipeline.Apply(src);
    var result = ocrEngine.Recognize(cleaned);
    // Save or log result.Text
}
```

एक ही `Engine` इंस्टेंस को पुनः उपयोग करने से प्रदर्शन भी बेहतर होता है।

## प्रोडक्शन‑रेडी OCR के लिए प्रो टिप्स

- **पाइपलाइन को कैश करें**: फ़िल्टरों को बार‑बार इंस्टैंशिएट करना हाई‑थ्रूपुट पर महंगा हो सकता है।  
- **OCR भाषा सेट करें**: गैर‑इंग्लिश डॉक्यूमेंट्स के लिए `ocrEngine.Language = Language.Spanish;`।  
- **खाली परिणाम संभालें**: आगे बढ़ने से पहले हमेशा `ocrResult.Text?.Length > 0` चेक करें।  
- **इंटरमीडिएट इमेज लॉग करें**: `cleanedImage` को डिस्क पर सेव करना (`cleanedImage.Save("debug.png");`) फ़िल्टर पैरामीटर को फाइन‑ट्यून करने में मदद करता है।  

## निष्कर्ष

हमने दिखाया कि कैसे Aspose OCR के शक्तिशाली फ़िल्टर पाइपलाइन का उपयोग करके **इमेज से स्क्यू हटाएँ**, **इमेज में शोर कम करें**, और **OCR के लिए इमेज को प्री‑प्रोसेस करें**, फिर **डॉक्यूमेंट से टेक्स्ट पहचानें** और अंत में **इमेज से टेक्स्ट निकालें**। पूरा वर्कफ़्लो 50 लाइनों से कम C# कोड में है और बैच प्रोसेसिंग, कस्टम भाषा मॉडल या अतिरिक्त फ़िल्टरों के लिए आसानी से विस्तारित किया जा सकता है।  

अगले कदम के लिए तैयार हैं? ब्लैक‑एंड‑व्हाइट आउटपुट के लिए `BinarizeFilter` जोड़ें, या विभिन्न `ContrastBoostFilter` लेवल्स के साथ प्रयोग करें कि वे पहचान की सटीकता को कैसे प्रभावित करते हैं। जितना अधिक आप पाइपलाइन के साथ खेलेंगे, उतना ही बेहतर आप समझेंगे कि प्रत्येक फ़िल्टर साफ़ OCR परिणाम में कैसे योगदान देता है।  

कोडिंग का आनंद लें, और आपकी इमेजेस हमेशा सीधी रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}