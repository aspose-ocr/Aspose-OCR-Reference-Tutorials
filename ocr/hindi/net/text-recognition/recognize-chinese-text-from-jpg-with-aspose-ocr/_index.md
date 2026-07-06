---
category: general
date: 2026-04-08
description: Aspose OCR का उपयोग करके JPG छवियों से चीनी पाठ को पहचानना सीखें। यह
  चरण‑दर‑चरण गाइड आपको यह भी दिखाता है कि कैसे जल्दी से छवि से पाठ निकालें।
draft: false
keywords:
- recognize chinese text
- extract text from image
- recognize text from jpg
- Aspose OCR C#
- offline OCR resources
language: hi
og_description: Aspose OCR का उपयोग करके JPG छवियों से चीनी पाठ को पहचानें। ऑफ़लाइन
  छवि से पाठ निकालने के लिए इस पूर्ण गाइड का पालन करें।
og_title: Aspose OCR के साथ JPG से चीनी पाठ को पहचानें
tags:
- OCR
- C#
- Aspose
title: Aspose OCR के साथ JPG से चीनी पाठ को पहचानें
url: /hi/net/text-recognition/recognize-chinese-text-from-jpg-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JPG से Aspose OCR के साथ चीनी टेक्स्ट पहचानें

क्या आपको कभी JPG फ़ाइल से **चीनी टेक्स्ट पहचानने** की ज़रूरत पड़ी है लेकिन आप नहीं जानते थे कि कहाँ से शुरू करें? आप अकेले नहीं हैं—कई डेवलपर्स को बहुभाषी स्कैनिंग ऐप्स बनाते समय यह समस्या आती है। अच्छी खबर यह है कि Aspose OCR इसे बहुत आसान बना देता है, यहाँ तक कि जब आपको ऑफ़लाइन काम करना पड़े।

इस ट्यूटोरियल में हम पूरी प्रक्रिया को देखेंगे कि कैसे इमेज से टेक्स्ट निकाला जाए, **छवि से टेक्स्ट निकालें** शैली में, और दिखाएंगे कि C# का उपयोग करके **JPG से टेक्स्ट पहचानें** कैसे किया जाता है। अंत तक आपके पास एक चलने योग्य प्रोग्राम होगा जो चीनी‑भाषा वाली तस्वीर पढ़ेगा और पहचाने गए अक्षरों को कंसोल में प्रिंट करेगा।

## आपको क्या चाहिए

- .NET 6.0 या बाद का (कोई भी हालिया संस्करण काम करेगा)
- Aspose.OCR NuGet पैकेज (`Install-Package Aspose.OCR`)
- एक चीनी भाषा संसाधन फ़ाइल (ट्यूटोरियल दिखाता है कि इसे ऑफ़लाइन कैसे लोड करें)
- `chinese_sample.jpg` नाम की इमेज फ़ाइल, जिसे आप नियंत्रित फ़ोल्डर में रखें

कोई जटिल IDE ट्रिक्स आवश्यक नहीं—Visual Studio, Rider, या यहाँ तक कि VS Code भी चलेंगे।

## चरण 1: प्रोजेक्ट सेट अप करें और Aspose OCR इंस्टॉल करें

पहले, एक नया कंसोल प्रोजेक्ट बनाएं और Aspose OCR लाइब्रेरी को जोड़ें।

```bash
dotnet new console -n ChineseOcrDemo
cd ChineseOcrDemo
dotnet add package Aspose.OCR
```

> **प्रो टिप:** यदि आप कॉर्पोरेट प्रॉक्सी के पीछे हैं, तो `--no-cache` फ़्लैग जोड़ें ताकि नया डाउनलोड ज़बरदस्त हो।

## चरण 2: स्वचालित संसाधन डाउनलोड को निष्क्रिय करें

Aspose OCR ऑन‑द‑फ़्लाई भाषा पैक डाउनलोड कर सकता है, लेकिन प्रोडक्शन में आप आमतौर पर फ़ाइलों को अपने ऐप के साथ शिप करना चाहते हैं। स्वचालित डाउनलोड को निष्क्रिय करने से अनपेक्षित नेटवर्क कॉल्स रोकते हैं।

```csharp
using Aspose.Ocr;

// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Turn off the auto‑download feature
ocrEngine.Options.EnableAutomaticResourceDownload = false;
```

हम यह क्यों करते हैं? संसाधनों को स्थानीय रखने से प्रदर्शन स्थिर रहता है और आप ऐप को बिना इंटरनेट वाले मशीनों पर चला सकते हैं।

## चरण 3: ऑफ़लाइन चीनी भाषा संसाधन लोड करें

Aspose भाषा डेटा को अलग‑अलग फ़ाइलों में प्रदान करता है। मान लीजिए आपने चीनी पैक (`zh`) को अपने executable के बगल में `Resources` फ़ोल्डर में रख दिया है, तो इसे इस तरह लोड करें:

```csharp
// Path to the folder that contains the language files
string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");

// Tell the engine where to look for resources
ocrEngine.Options.ResourcesFolder = resourcePath;

// Load the Simplified Chinese resources (offline = true)
ocrEngine.LoadLanguageResources("zh", offline: true);
```

> **सावधान:** यदि पाथ गलत है, तो आपको `FileNotFoundException` मिलेगा। फ़ोल्डर नाम और Linux पर केस‑सेंसिटिविटी को दोबारा जांचें।

## चरण 4: इंजन भाषा को चीनी सेट करें

अब डेटा लोड हो गया है, इंजन को सही भाषा कोड की ओर इंगित करें।

```csharp
ocrEngine.Language = "zh"; // “zh” = Simplified Chinese
```

भाषा को स्पष्ट रूप से सेट करने से सटीकता बढ़ती है क्योंकि OCR को स्क्रिप्ट अनुमान लगाने में समय नहीं लगाना पड़ता।

## चरण 5: JPG इमेज से टेक्स्ट पहचानें

यह ट्यूटोरियल का मुख्य भाग है—JPG को इंजन में फीड करना और टेक्स्ट निकालना।

```csharp
// Full path to the image you want to process
string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");

// Run the OCR operation
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

// Output the raw result
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

यदि सब कुछ सुचारू रूप से चलता है, तो कंसोल में `chinese_sample.jpg` में मौजूद चीनी अक्षर दिखेंगे। आप गुणवत्ता मीट्रिक के लिए `ocrResult.Confidence` भी एक्सेस कर सकते हैं।

## चरण 6: पूर्ण कार्यशील उदाहरण

सभी हिस्सों को जोड़ने से आपको एक तैयार‑चलाने‑योग्य प्रोग्राम मिलता है। इसे `Program.cs` के रूप में अपने प्रोजेक्ट फ़ोल्डर में सहेजें।

```csharp
using System;
using System.IO;
using Aspose.Ocr;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Disable automatic resource download
        // -------------------------------------------------
        ocrEngine.Options.EnableAutomaticResourceDownload = false;

        // -------------------------------------------------
        // 3️⃣ Load Chinese language resources (offline)
        // -------------------------------------------------
        string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");
        ocrEngine.Options.ResourcesFolder = resourcePath;
        ocrEngine.LoadLanguageResources("zh", offline: true);

        // -------------------------------------------------
        // 4️⃣ Set language to Simplified Chinese
        // -------------------------------------------------
        ocrEngine.Language = "zh";

        // -------------------------------------------------
        // 5️⃣ Recognize text from a JPG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // -------------------------------------------------
        // 6️⃣ Show the result
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine($"\nConfidence: {ocrResult.Confidence:P2}");
    }
}
```

### अपेक्षित आउटपुट

```
=== Recognized Chinese Text ===
欢迎使用Aspose OCR示例
Confidence: 96.45%
```

आपका सटीक आउटपुट स्रोत इमेज पर निर्भर करेगा, लेकिन आपको चीनी अक्षरों का एक ब्लॉक और उसके बाद एक confidence प्रतिशत दिखना चाहिए।

## चरण 7: सामान्य विविधताएँ और किनारे के मामलों

### PNG या BMP से टेक्स्ट पहचानना

`RecognizeImage` मेथड .NET के `System.Drawing` द्वारा समर्थित किसी भी फॉर्मेट को स्वीकार करता है। केवल फ़ाइल एक्सटेंशन बदलें:

```csharp
ocrEngine.RecognizeImage("sample.png");
```

### कई भाषाओं को संभालना

यदि आपको **छवि से टेक्स्ट निकालें** ऐसी इमेज चाहिए जिसमें अंग्रेज़ी और चीनी दोनों मिश्रित हों, तो दोनों भाषा पैक लोड करें और `ocrEngine.Language = "zh,en";` सेट करें। इंजन स्वचालित रूप से स्क्रिप्ट्स के बीच स्विच करेगा।

### कम‑रिज़ॉल्यूशन इमेजेज़ से निपटना

कम DPI OCR की सटीकता को बिगाड़ सकता है। `RecognizeImage` कॉल करने से पहले आप तस्वीर को अपस्केल कर सकते हैं:

```csharp
using System.Drawing;

Bitmap bmp = new Bitmap(imagePath);
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
highRes.Save("highres.jpg");
ocrResult = ocrEngine.RecognizeImage("highres.jpg");
```

ध्यान रखें, अपस्केलिंग जादू से विवरण नहीं जोड़ती, लेकिन एल्गोरिद्म को अधिक पिक्सेल काम करने के लिए देती है।

## चरण 8: परीक्षण और सत्यापन

एक त्वरित sanity check यह है कि OCR आउटपुट को ज्ञात ग्राउंड ट्रुथ स्ट्रिंग से तुलना करें।

```csharp
string expected = "欢迎使用Aspose OCR示例";
bool matches = ocrResult.Text.Trim() == expected;
Console.WriteLine($"Match with expected? {matches}");
```

यदि `matches` `false` है, तो इमेज को थोड़ा बदलें (जैसे कंट्रास्ट बढ़ाएँ) या `ocrEngine.Options.UseAdvancedPreprocessing = true` सक्षम करें।

## निष्कर्ष

आपने अभी-अभी Aspose OCR का उपयोग करके JPG फ़ाइल से **चीनी टेक्स्ट पहचानने** का तरीका सीखा, और अब आप पूरी तरह ऑफ़लाइन परिदृश्य में **छवि से टेक्स्ट निकालें** भी कर सकते हैं। पूर्ण समाधान—इनिशियलाइज़ेशन, संसाधन लोडिंग, भाषा चयन, और इमेज प्रोसेसिंग—एक ही आसान‑चलाने‑योग्य कंसोल ऐप में समा जाता है।

अब आगे क्या? उसी इंजन को कई इमेजेज़ की बैच प्रोसेसिंग के लिए फीड करें, विभिन्न भाषा पैक्स के साथ प्रयोग करें, या OCR स्टेप को ASP .NET Web API में इंटीग्रेट करें ताकि उपयोगकर्ता तस्वीरें अपलोड कर सकें और तुरंत अनूदित टेक्स्ट प्राप्त कर सकें। जब आप भरोसेमंद OCR को आधुनिक .NET टूलिंग के साथ जोड़ते हैं तो संभावनाएँ अनंत हैं।

कोडिंग का आनंद लें, और अगर कोई समस्या आती है तो टिप्पणी छोड़ने में संकोच न करें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}