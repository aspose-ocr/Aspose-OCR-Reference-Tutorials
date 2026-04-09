---
category: general
date: 2026-04-08
description: जानिए कैसे Aspose OCR का उपयोग करके छवि पर OCR करें और C# में JSON फ़ाइल
  लिखें। यह Aspose OCR C# ट्यूटोरियल OCR छवि को JSON में रूपांतरित करने को दिखाता
  है, जिसमें कॉन्फिडेंस वैल्यूज़ शामिल हैं।
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: hi
og_description: छवि पर OCR करें और परिणामों को C# में JSON फ़ाइल में निर्यात करें।
  यह ट्यूटोरियल Aspose OCR C# वर्कफ़्लो को पूरी तरह कवर करता है, जिसमें कॉन्फिडेंस
  स्कोर शामिल हैं।
og_title: C# में इमेज पर OCR करके JSON बनाएं – Aspose OCR गाइड
tags:
- Aspose
- OCR
- C#
- JSON
title: Aspose के साथ C# में इमेज पर OCR करके JSON बनाएं
url: /hi/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# के साथ Aspose का उपयोग करके इमेज पर OCR करके JSON बनाएं

क्या आपको कभी **इमेज पर OCR करने** की ज़रूरत पड़ी है लेकिन आप नहीं जानते थे कि परिणाम को संरचित फ़ॉर्मेट में कैसे प्राप्त करें? आप अकेले नहीं हैं—डेवलपर्स लगातार पूछते हैं, “स्कैन की गई तस्वीर को उपयोगी डेटा में कैसे बदलें?” अच्छी खबर यह है कि Aspose.OCR इसे बहुत आसान बनाता है, और आप **JSON फ़ाइल C#**‑स्टाइल में confidence स्कोर सहित भी लिख सकते हैं।

इस गाइड में हम एक पूर्ण **aspose OCR C# tutorial** के माध्यम से चलेंगे जो इमेज लोड करने से लेकर पहचाने गए टेक्स्ट को JSON के रूप में निर्यात करने तक सब कुछ कवर करता है। अंत तक आपके पास एक चलने योग्य कंसोल ऐप होगा जो **इमेज पर OCR करता है**, आउटपुट को JSON में बदलता है (confidence मानों सहित), और एक ही लाइन कोड से इसे सहेजता है। कोई छिपे हुए कदम नहीं, कोई बाहरी स्क्रिप्ट नहीं—सिर्फ शुद्ध C#।

## आवश्यकताएँ

- .NET 6.0 SDK या बाद का संस्करण (कोड .NET Core और .NET Framework के साथ भी काम करता है)
- Visual Studio 2022 (या आपका पसंदीदा कोई भी एडिटर)
- एक वैध **Aspose.OCR for .NET** लाइसेंस या एक मुफ्त अस्थायी लाइसेंस (टेस्टिंग के लिए फ्री ट्रायल काम करता है)
- एक इमेज फ़ाइल (`input.png`) जिसे आप प्रोसेस करना चाहते हैं (कोई भी सामान्य फ़ॉर्मेट—PNG, JPG, BMP—चल जाएगा)

बस इतना ही। यदि इनमें से कोई भी चीज़ आपके पास नहीं है, तो अभी प्राप्त करें; ट्यूटोरियल का बाकी हिस्सा मानता है कि ये पहले से मौजूद हैं।

## चरण 1: Aspose.OCR NuGet पैकेज स्थापित करें

सबसे पहले—लाइब्रेरी को अपने प्रोजेक्ट में जोड़ें। प्रोजेक्ट फ़ोल्डर में एक टर्मिनल खोलें और चलाएँ:

```bash
dotnet add package Aspose.OCR
```

यह नवीनतम संस्करण (अप्रैल 2026 तक यह 23.12 है) को डाउनलोड करता है और आवश्यक DLLs को `bin` फ़ोल्डर में जोड़ता है। अतिरिक्त कोई कॉन्फ़िगरेशन आवश्यक नहीं है।

## चरण 2: OCR इंजन को इनिशियलाइज़ करें (इमेज पर OCR करें)

अब हम एक `OcrEngine` इंस्टेंस बनाते हैं और उसे बताते हैं कि कौन सी भाषा उपयोग करनी है। English (`"en"`) सबसे सामान्य है, लेकिन आप इसे `"fr"`, `"de"` या किसी भी समर्थित भाषा में बदल सकते हैं।

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**हम यहाँ इनिशियलाइज़ क्यों करते हैं:** `OcrEngine` में पहचान प्रक्रिया के लिए सभी कॉन्फ़िगरेशन रखे होते हैं। भाषा को पहले से सेट करने से इंजन सही कैरेक्टर सेट का उपयोग करता है, जिससे सटीकता में उल्लेखनीय सुधार होता है।

## चरण 3: इमेज को पहचानें और confidence कैप्चर करें

इंजन तैयार होने पर, हम उसे इमेज फ़ाइल देते हैं। `RecognizeImage` मेथड एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें निकाला गया टेक्स्ट और प्रत्येक शब्द के लिए confidence स्कोर दोनों होते हैं।

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**अंदर क्या हो रहा है?** Aspose एक न्यूरल‑नेटवर्क‑आधारित रेकग्नाइज़र चलाता है जो प्रत्येक पिक्सेल ब्लॉक का विश्लेषण करता है, उसे अपनी भाषा मॉडल से मिलाता है, और एक confidence वैल्यू (0‑100) जोड़ता है जो बताती है कि वह प्रत्येक शब्द के बारे में कितना निश्चित है।

## चरण 4: परिणाम को JSON में बदलें (OCR इमेज से JSON)

Aspose इस परिवर्तन को बेहद आसान बनाता है। `includeConfidence: true` पास करने पर हमें एक JSON पेलोड मिलता है जो इस प्रकार दिखता है:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

यहाँ वह कोड है जो JSON स्ट्रिंग उत्पन्न करता है:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**confidence शामिल क्यों करें?** यदि आप डेटा को डाउनस्ट्रीम प्रोसेसेस (जैसे वेलिडेशन, UI हाइलाइटिंग) में फीड करने की योजना बनाते हैं, तो यह जानना कि कौन से शब्द अस्थिर हैं, आपको यह तय करने में मदद करता है कि उपयोगकर्ता से पुष्टि माँगी जाए या नहीं।

## चरण 5: JSON फ़ाइल C#‑स्टाइल में लिखें

अब हम वास्तव में **JSON फ़ाइल C#** लिखते हैं। `File.WriteAllText` मेथड एटॉमिक है और क्रॉस‑प्लेटफ़ॉर्म काम करता है, जिससे यह कंसोल ऐप्स के लिए एकदम उपयुक्त है।

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

यही पूरा वर्कफ़्लो है—पाँच संक्षिप्त कदम जो **इमेज पर OCR करते हैं**, आउटपुट को JSON में बदलते हैं, और उसे सहेजते हैं।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा प्रोग्राम दिया गया है जिसे आप `Program.cs` में कॉपी‑पेस्ट कर सकते हैं। सुनिश्चित करें कि `input.png` संकलित बाइनरी के समान फ़ोल्डर में मौजूद हो या पाथ को उसी अनुसार समायोजित करें।

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### अपेक्षित आउटपुट

जब आप प्रोग्राम चलाते हैं (`dotnet run`), तो आपको कुछ इस प्रकार दिखेगा:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

और `output.json` में वह संरचित JSON होगा जो पहले दिखाया गया था, प्रत्येक शब्द के लिए confidence प्रतिशत सहित।

## प्रो टिप्स और किनारे के केस

- **Missing file handling:** यदि आप डायनामिक पाथ की उम्मीद करते हैं तो `RecognizeImage` कॉल को `try/catch` में `FileNotFoundException` के साथ रैप करें।
- **Different languages:** फ्रेंच के लिए `ocrEngine.Language = "fr"` सेट करें, या `ocrEngine.LoadLanguage("custom.lang")` के माध्यम से एक कस्टम भाषा पैक लोड करें।
- **Large documents:** मल्टी‑पेज PDFs के लिए, पहले प्रत्येक पेज को इमेज में बदलें (जैसे `Aspose.PDF` का उपयोग करके) और OCR चरणों को लूप में चलाएँ।
- **Performance tuning:** यदि आपको केवल तेज़ परिणाम चाहिए, तो `RecognitionMode.Fast` पर स्विच करें—आपको थोड़ा सटीकता का नुकसान होगा लेकिन गति बढ़ेगी।
- **JSON formatting:** प्रीटी‑प्रिंटेड JSON चाहिए? Aspose JSON स्ट्रिंग को डीसिरियलाइज़ करने के बाद `JsonConvert.SerializeObject` को `Formatting.Indented` के साथ उपयोग करें।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या यह .NET Framework के साथ काम करता है?**  
**उत्तर:** बिल्कुल। वही NuGet पैकेज .NET Standard 2.0 को टार्गेट करता है, इसलिए आप इसे .NET Framework 4.6.1 और उसके बाद के संस्करणों से रेफ़रेंस कर सकते हैं।

**प्रश्न: यदि मुझे पूरे दस्तावेज़ के लिए confidence चाहिए, न कि प्रति शब्द?**  
**उत्तर:** `OcrResult` में `OverallConfidence` भी उपलब्ध है। आप इसे मैन्युअली JSON में जोड़ सकते हैं:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**प्रश्न: क्या मैं JSON को सीधे वेब API में स्ट्रीम कर सकता हूँ?**  
**उत्तर:** हाँ। `File.WriteAllText` को `HttpClient` POST से बदलें जो `jsonResult

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}