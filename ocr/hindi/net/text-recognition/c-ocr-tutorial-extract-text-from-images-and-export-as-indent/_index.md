---
category: general
date: 2026-05-02
description: c# OCR ट्यूटोरियल जो दिखाता है कि कैसे टेक्स्ट इमेज को c# में निकालें
  और PNG टेक्स्ट को पहचानें, फिर JsonSerializer c# का उपयोग करके इंडेंटेड JSON लिखें।
  डेवलपर्स के लिए स्टेप‑बाय‑स्टेप गाइड।
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: hi
og_description: c# OCR ट्यूटोरियल जो दिखाता है कि कैसे टेक्स्ट इमेज को c# में एक्सट्रैक्ट
  करें और PNG टेक्स्ट को पहचानें, फिर JsonSerializer c# के साथ इंडेंटेड JSON लिखें।
  पूर्ण, चलाने योग्य उदाहरण।
og_title: c# OCR ट्यूटोरियल – टेक्स्ट निकालें और इंडेंटेड JSON के रूप में निर्यात
  करें
tags:
- OCR
- C#
- Aspose
- JSON
title: c# OCR ट्यूटोरियल – छवियों से टेक्स्ट निकालें और इंडेंटेड JSON के रूप में निर्यात
  करें
url: /hi/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – छवियों से टेक्स्ट निकालें और इंडेंटेड JSON के रूप में निर्यात करें

क्या आपको कभी एक **c# ocr tutorial** की ज़रूरत पड़ी है जो टेक्स्ट की तस्वीर से सीधे एक सुंदर फ़ॉर्मेटेड JSON फ़ाइल तक ले जाए? आप अकेले नहीं हैं। कई प्रोजेक्ट्स में – जैसे इनवॉइस स्कैनिंग, रसीद पार्सिंग, या यहाँ तक कि साधारण मीम‑टेक्स्ट एक्सट्रैक्शन – आपके पास एक PNG फ़ाइल होती है और आप सोचते हैं कि बिना कस्टम रिकग्नाइज़र लिखे शब्दों को कैसे निकाला जाए।  

यह गाइड आपको एक व्यावहारिक समाधान देता है: हम Aspose.OCR का उपयोग करके **extract text image c#** करेंगे, **recognize png text** करेंगे, और फिर C# में `JsonSerializer` के साथ **write indented json** लिखेंगे। अंत तक आपके पास एक स्व-निहित कंसोल ऐप होगा जिसे आप किसी भी .NET सॉल्यूशन में डाल सकते हैं। कोई अस्पष्ट “see the docs” लिंक नहीं, सिर्फ एक पूर्ण, कॉपी‑एंड‑पेस्ट‑तैयार उदाहरण।

## आपको क्या चाहिए

- **.NET 6** (या कोई भी हालिया .NET संस्करण)। पुराने फ्रेमवर्क काम करेंगे, लेकिन दिखाया गया सिंटैक्स .NET 6+ को लक्षित करता है।
- **Aspose.OCR for .NET** – NuGet के माध्यम से इंस्टॉल करें: `dotnet add package Aspose.OCR`।
- एक सैंपल PNG इमेज (`text.png`) जिसमें स्पष्ट, मशीन‑रीडेबल टेक्स्ट हो।
- आपका पसंदीदा IDE या एडिटर – Visual Studio, VS Code, Rider, आदि।

> **प्रो टिप:** यदि आप कई इमेज प्रोसेस करने की योजना बना रहे हैं, तो प्रत्येक फ़ाइल के लिए नया `OcrEngine` बनाने के बजाय एक ही `OcrEngine` इंस्टेंस को पुनः उपयोग करने पर विचार करें। यह ओवरहेड को कम करता है और थ्रूपुट को सुधारता है।

## चरण 1: c# ocr tutorial प्रोजेक्ट सेट अप करें

सबसे पहले, एक कंसोल प्रोजेक्ट बनाएं। नीचे दिए गए कमांड स्कैफ़ोल्डिंग बनाते हैं और OCR लाइब्रेरी को जोड़ते हैं:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

अब जेनरेटेड `Program.cs` खोलें। हम बाद में इसकी सामग्री को पूरे उदाहरण से बदलेंगे, लेकिन अभी के लिए सुनिश्चित करें कि प्रोजेक्ट बिल्ड हो रहा है:

```bash
dotnet build
```

यदि आपको कोई त्रुटि नहीं दिखती, तो आप आगे बढ़ने के लिए तैयार हैं।

## चरण 2: इमेज से PNG टेक्स्ट को पहचानें

किसी भी **c# ocr tutorial** का मुख्य भाग OCR इंजन ही है। Aspose.OCR लो‑लेवल डिटेल्स को एब्स्ट्रैक्ट करता है और आपको एक साफ़ `OcrEngine` क्लास देता है। नीचे हम इंजन बनाते हैं, इसे एक PNG फ़ाइल की ओर इशारा करते हैं, और टेक्स्ट को पहचानने के लिए कहते हैं।

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### यह क्यों काम करता है

- **`RecognizeImage`** कई फॉर्मैट्स (PNG, JPEG, BMP) को स्वीकार करता है। हम विशेष रूप से **recognize png text** करते हैं क्योंकि PNG लॉसलेस डिटेल को संरक्षित रखता है, जो OCR के लिए आदर्श है।
- रिटर्न किया गया `OcrResult` केवल साधारण टेक्स्ट ही नहीं, बल्कि प्रति‑ग्लिफ कॉन्फिडेंस स्कोर भी रखता है, जो बाद में कम‑कॉन्फिडेंस कैरेक्टर्स को फ़िल्टर करने में उपयोगी है।

## चरण 3: JsonSerializer c# के साथ इंडेंटेड JSON लिखें

अब जब हमारे पास `ocrResult` है, हमारे **c# ocr tutorial** में अगला तार्किक कदम इस ऑब्जेक्ट को मानव‑पठनीय JSON में बदलना है। बिल्ट‑इन `System.Text.Json` सीरियलाइज़र यह काम करता है, और हम इसे स्पष्टता के लिए **write indented json** करने के लिए कॉन्फ़िगर करेंगे।

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### `JsonSerializer` का सही उपयोग

- `WriteIndented` फ़्लैग तीसरे‑पक्षी लाइब्रेरीज़ को शामिल किए बिना **write indented json** करने का सबसे सरल तरीका है।
- यदि आपको कभी camel‑case प्रॉपर्टी नाम चाहिए, तो विकल्पों में `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` जोड़ें।
- `jsonOutput` स्ट्रिंग को `File.WriteAllText("result.json", jsonOutput);` के साथ सेव किया जा सकता है – वास्तविक‑दुनिया पाइपलाइन के लिए एक उपयोगी ट्रिक।

## चरण 4: आउटपुट चलाएँ और सत्यापित करें

प्रोग्राम को कंपाइल और रन करें:

```bash
dotnet run
```

मान लेते हैं कि `text.png` में वाक्यांश *“Hello, OCR World!”* है, तो आपको कुछ इस तरह दिखना चाहिए:

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

वह JSON **indented** है, जिससे इसे लॉग में पढ़ना या डाउनस्ट्रीम सर्विसेज़ को हैंड‑ऑफ़ करना आसान हो जाता है।

### किनारे के केस और टिप्स

| स्थिति | क्या करें |
|-----------|------------|
| **Image is blurry** | `ocrEngine.Config.Dpi` बढ़ाएँ (उदा., `ocrEngine.Config.Dpi = 300`) `RecognizeImage` कॉल करने से पहले। |
| **Non‑English language** | `ocrEngine.Config.Language = OcrLanguage.German` सेट करें (या कोई भी समर्थित भाषा)। |
| **Large batch of files** | डायरेक्टरी पर लूप करें, वही `OcrEngine` इंस्टेंस पुनः उपयोग करें; प्रत्येक JSON परिणाम को एक अनोखे फ़ाइलनाम के साथ सहेजें। |
| **Need only high‑confidence text** | सीरियलाइज़ेशन से पहले `ocrResult.Lines` को फ़िल्टर करें जहाँ `Confidence` ≥ 0.95 हो। |

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे *पूरा* प्रोग्राम है, जिसे `Program.cs` में डालने के लिए तैयार है। इसमें सभी चरण, एरर हैंडलिंग, और टिप्पणी शामिल हैं जो कोड को स्वयं‑स्पष्टीकरण बनाती हैं।

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

कोड चलाएँ, कंसोल या जेनरेटेड `.json` फ़ाइल को देखें, और आप निकाले गए टेक्स्ट को कॉन्फिडेंस स्कोर के साथ देखेंगे, सब कुछ साफ़ तौर पर **indented**।

## निष्कर्ष

अब आपके पास एक ठोस **c# ocr tutorial** है जो दिखाता है कि कैसे **extract text image c#**, **recognize png text**, और `JsonSerializer` का उपयोग करके **write indented json** किया जाता है। उदाहरण पूर्ण, चलाने योग्य, और वास्तविक‑दुनिया परिदृश्यों के लिए व्यावहारिक टिप्स शामिल करता है।  

अगले कदम? Aspose.OCR को किसी अन्य इंजन (जैसे, Tesseract) से बदलें और देखें कि `OcrResult` की संरचना कैसे बदलती है, या JSON को एक डाउनस्ट्रीम API में फीड करें जो OCR डेटा को डेटाबेस में स्टोर करता है। आप **use jsonserializer c#** विकल्पों के साथ भी प्रयोग कर सकते हैं जैसे कि डेट फॉर्मेटिंग या एनीम हैंडलिंग के लिए कस्टम कन्वर्टर्स।

कोडिंग का आनंद लें, और आपकी OCR पाइपलाइन्स हमेशा सटीक रहें!  

---  

![c# ocr tutorial diagram](image.png "Diagram illustrating OCR flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}