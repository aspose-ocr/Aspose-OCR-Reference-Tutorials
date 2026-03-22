---
category: general
date: 2026-03-21
description: Aspose OCR के साथ इमेज फ़ाइलों को डेस्क्यू करना और टेक्स्ट इमेज को पहचानना
  सीखें। कुछ ही C# कोड लाइनों में JPG को टेक्स्ट में बदलें और इमेज रोटेशन को सही करें।
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: hi
og_description: Aspose OCR का उपयोग करके JPEG छवियों को डेस्क्यू कैसे करें और टेक्स्ट
  निकालें। JPG को टेक्स्ट में बदलने और छवि के घुमाव को सही करने के लिए इस चरण‑दर‑चरण
  गाइड का पालन करें।
og_title: C# में इमेज को डेस्क्यू कैसे करें – त्वरित Aspose OCR ट्यूटोरियल
tags:
- OCR
- C#
- Aspose
title: C# में इमेज को डेस्क्यू कैसे करें – Aspose OCR का उपयोग करके पूर्ण गाइड
url: /hi/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में इमेज को डेस्क्यू कैसे करें – Aspose OCR का उपयोग करके पूर्ण गाइड

क्या आपने कभी स्कैनर से निकली हुई इमेज को **इमेज को डेस्क्यू कैसे करें** के बारे में सोचा है जो अजीब कोण पर टिल्ट हो गई हो? आप अकेले नहीं हैं—कई डेवलपर्स को रसीदों, इनवॉइस या हस्तलिखित नोट्स से टेक्स्ट निकालते समय यही समस्या आती है। अच्छी खबर यह है कि Aspose OCR के साथ आप इमेज का रोटेशन ठीक कर सकते हैं और कुछ ही लाइनों में साफ़, सर्चेबल टेक्स्ट निकाल सकते हैं।

इस ट्यूटोरियल में हम पूरी प्रक्रिया को चरण-दर-चरण देखेंगे: लाइब्रेरी को इंस्टॉल करने से लेकर ऑटोमैटिक डेस्क्यूइंग को सक्षम करने, टेक्स्ट इमेज को पहचानने और अंत में JPG को टेक्स्ट में बदलने तक। अंत तक आपके पास एक तैयार‑चलाने‑योग्य कंसोल ऐप होगा जो **recognize text jpg** फ़ाइलों को बिना मैन्युअल रोटेशन के पहचान लेगा।

## आपको क्या चाहिए

- **.NET 6.0** या बाद का (कोड .NET Core और .NET Framework दोनों पर काम करता है)  
- **Aspose.OCR for .NET** NuGet पैकेज – संस्करण 23.12 या नया सुझाया जाता है  
- एक सैंपल **skewed JPEG** (जैसे `skewed_receipt.jpg`) जिसे आपका ऐप पढ़ सके ऐसी जगह रखें  
- Visual Studio, VS Code, या कोई भी पसंदीदा C# एडिटर  

कोई अन्य थर्ड‑पार्टी टूल्स आवश्यक नहीं हैं। लाइब्रेरी डेस्क्यूइंग, OCR, और यहाँ तक कि भाषा पहचान भी आंतरिक रूप से संभालती है।

![इमेज को डेस्क्यू करने का उदाहरण](/images/deskew-example.png "Aspose OCR का उपयोग करके इमेज को डेस्क्यू कैसे करें")

## चरण 1: प्रोजेक्ट सेट अप करें और Aspose.OCR इंस्टॉल करें

सभी चीज़ें व्यवस्थित रखने के लिए, एक नया कंसोल प्रोजेक्ट शुरू करें:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

`dotnet add package` लाइन **Aspose.OCR** बाइनरीज़ और सभी नेटिव डिपेंडेंसीज़ को जोड़ती है। यदि आप Windows पर हैं तो नेटिव DLLs स्वचालित रूप से मिल जाएँगे; Linux/macOS पर आपको `libgdiplus` पैकेज की आवश्यकता हो सकती है, लेकिन यह एक बार की इंस्टॉल है।

## चरण 2: ऑटोमैटिक डेस्क्यूइंग सक्षम करें (इमेज रोटेशन को सही करें)

अब `Program.cs` खोलें और उसकी सामग्री को नीचे दिए गए कोड से बदलें। यहाँ मुख्य लाइन है `ocrEngine.Settings.Deskew = true;` – यह वह फ़्लैग है जो इंजन को **इमेज को डेस्क्यू कैसे करें** स्वचालित रूप से बताता है।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### डेस्क्यू क्यों सक्षम करें?

जब स्कैनर पेज को कोण पर फीड करता है, तो टेक्स्ट बेसलाइन झुकी हुई होती है। पारंपरिक OCR इंजन प्रत्येक अक्षर को टिल्ट संस्करण के रूप में पढ़ते हैं, जिससे सटीकता में भारी गिरावट आती है। `Deskew = true` सेट करके, Aspose OCR हाउ ट्रांसफ़ॉर्म को तेज़ी से चलाता है, बिटमैप को फिर से क्षैतिज में घुमाता है, और फिर पहचान करता है। परिणाम वही होता है जैसे आप Photoshop में मैन्युअली इमेज को घुमा रहे हों—सिर्फ तेज़ और पूरी तरह स्वचालित।

## चरण 3: टेक्स्ट इमेज को पहचानें और JPG को टेक्स्ट में बदलें

`Recognize` कॉल एक साथ दो काम करता है:

1. **Deskews** इमेज (क्योंकि हमने फ़्लैग ऑन किया है)।  
2. **Extracts** टेक्स्टुअल कंटेंट, जो `OcrResult` ऑब्जेक्ट में रिटर्न होता है।

आप `ocrResult.Text` को साधारण स्ट्रिंग की तरह उपयोग कर सकते हैं, इसे फ़ाइल में लिख सकते हैं, या डाउनस्ट्रीम प्रोसेसिंग पाइपलाइन में फीड कर सकते हैं। यदि आपको प्रत्येक शब्द के रॉ कॉन्फिडेंस स्कोर चाहिए, तो `ocrResult.Words` आपको `Confidence` वैल्यू के साथ एक कलेक्शन देता है।

### उदाहरण आउटपुट

मान लीजिए `skewed_receipt.jpg` में एक साधारण रसीद है, तो आप कुछ इस तरह देख सकते हैं:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

ध्यान दें कि मूल इमेज लगभग 7° घुमा हुआ होने के बावजूद नंबर ठीक से लाइन में हैं। यह लाइब्रेरी में निर्मित **correct image rotation** (सही इमेज रोटेशन) का जादू है।

## चरण 4: उदाहरण चलाएँ और परिणाम सत्यापित करें

कम्पाइल करें और चलाएँ:

```bash
dotnet run
```

यदि सब कुछ सही ढंग से सेट है तो आप कंसोल में निकाला गया टेक्स्ट प्रिंट होते देखेंगे। यदि आपको `FileNotFoundException` जैसी एक्सेप्शन मिलती है, तो अपने JPEG का पाथ दोबारा जांचें और सुनिश्चित करें कि फ़ाइल पढ़ी जा सकती है।

### सामान्य समस्याएँ और प्रो टिप्स

- **Large Images** – OCR मेमोरी उपयोग इमेज के आयामों के साथ बढ़ता है। इंजन को फ़ीड करने से पहले बहुत बड़ी फ़ाइलों (जैसे > 3000 px चौड़ाई) को री‑साइज़ करें।  
- **Non‑Latin Scripts** – डिफ़ॉल्ट रूप से इंजन इंग्लिश मानता है। यदि आपको अन्य लिपियों में **recognize text image** (टेक्स्ट इमेज को पहचानना) चाहिए तो `ocrEngine.Settings.Language = OcrLanguage.French;` (या कोई भी सपोर्टेड भाषा) सेट करें।  
- **Batch Processing** – कई फ़ाइलों के लिए, वही `OcrEngine` इंस्टेंस पुन: उपयोग करें; प्रत्येक फ़ाइल के लिए नया इंजन बनाना अनावश्यक ओवरहेड देता है।  
- **Quality Check** – डेस्क्यू करने के बाद आप `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` के माध्यम से सुधारी गई बिटमैप को एक्सपोर्ट कर सकते हैं ताकि रोटेशन फ़िक्स को विज़ुअली वेरिफ़ाई किया जा सके।

## पूर्ण कार्यशील उदाहरण (सभी एक साथ)

नीचे पूरा, स्व-निहित प्रोग्राम दिया गया है जिसे आप `Program.cs` में कॉपी‑पेस्ट कर सकते हैं। इसमें कमेंट्स, एरर हैंडलिंग, और डेस्क्यू की गई इमेज को सेव करने का वैकल्पिक स्टेप शामिल है।

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

प्रोग्राम चलाने से **recognize text jpg** फ़ाइलें पहचानी जाएँगी, किसी भी स्क्यू को स्वचालित रूप से ठीक किया जाएगा, और साफ़, सर्चेबल टेक्स्ट कंसोल में प्रिंट होगा।

## निष्कर्ष

अब आपके पास एक ठोस, प्रोडक्शन‑रेडी स्निपेट है जो Aspose OCR का उपयोग करके **इमेज को डेस्क्यू कैसे करें** फ़ाइलों को दिखाता है और उनकी सामग्री निकालता है। यह तरीका रसीदों, इनवॉइस, स्कैन किए गए कॉन्ट्रैक्ट्स, या किसी भी JPEG के लिए काम करता है जहाँ टेक्स्ट पूरी तरह क्षैतिज नहीं है।

अगले कदम जिन्हें आप एक्सप्लोर कर सकते हैं:

- **Batch processing** एक फ़ोल्डर में JPEGs को प्रोसेस करना और प्रत्येक परिणाम को `.txt` फ़ाइल में लिखना (यह *convert jpg to text* से जुड़ा है)।  
- OCR स्टेप को ASP.NET Core API में इंटीग्रेट करना ताकि क्लाइंट इमेज अपलोड कर सकें और JSON‑फ़ॉर्मेटेड टेक्स्ट प्राप्त कर सकें।  
- विभिन्न OCR सेटिंग्स जैसे `ocrEngine.Settings.Language` या `ocrEngine.Settings.RecognitionMode` के साथ प्रयोग करना ताकि गैर‑इंग्लिश दस्तावेज़ों की सटीकता बढ़े।

इसे आज़माएँ, सेटिंग्स को ट्यून करें, और इंजन को भारी काम करने दें। जैसा कि हमेशा, यदि आपको कोई समस्या आती है या आपके पास कोई चतुर ऑप्टिमाइज़ेशन है तो नीचे कमेंट छोड़ें। कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}