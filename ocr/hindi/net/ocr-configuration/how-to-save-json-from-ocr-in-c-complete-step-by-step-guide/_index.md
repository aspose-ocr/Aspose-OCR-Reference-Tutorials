---
category: general
date: 2026-03-02
description: Aspose OCR का उपयोग करके छवि से टेक्स्ट निकालते समय JSON को कैसे सहेजें,
  सीखें। इसमें JSON फ़ाइल लिखने का कोड, बिटमैप इमेज लोड करने के टिप्स, और पूर्ण C#
  उदाहरण शामिल हैं।
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: hi
og_description: Aspose OCR के साथ छवि से टेक्स्ट निकालते हुए JSON कैसे सहेँ, जानें।
  पूर्ण C# कोड, JSON फ़ाइल लिखने के चरण, और व्यावहारिक टिप्स।
og_title: C# में OCR से JSON कैसे सहेजें – पूर्ण प्रोग्रामिंग ट्यूटोरियल
tags:
- C#
- OCR
- Aspose
- JSON
title: C# में OCR से JSON कैसे सहेजें – पूर्ण चरण‑दर‑चरण मार्गदर्शिका
url: /hi/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में OCR से JSON कैसे सहेजें – पूर्ण चरण‑दर‑चरण गाइड

क्या आपने कभी सोचा है **JSON कैसे सहेजें** जिसमें वह टेक्स्ट हो जो आपने अभी-अभी एक तस्वीर से निकाला है? आप अकेले नहीं हैं। कई डेवलपर्स को तब रुकावट आती है जब उन्हें *छवि से टेक्स्ट निकालना* पड़ता है और फिर उस जानकारी को एक सुन्दर फ़ॉर्मेटेड JSON फ़ाइल में सहेजना होता है। अच्छी खबर? सही टूल्स होने पर समाधान बहुत सरल है।

इस ट्यूटोरियल में हम एक वास्तविक परिदृश्य को देखेंगे: Aspose.OCR का उपयोग करके **छवि से टेक्स्ट निकालना**, फिर **JSON फ़ाइल लिखना**, और अंत में **JSON को डिस्क पर कैसे सहेजें**। साथ ही हम आपको **बिटमैप इमेज लोड** करने का सही तरीका दिखाएंगे, और कुछ संभावित किनारे के मामलों को कवर करेंगे। अंत तक आपके पास एक स्व-निहित C# कंसोल ऐप होगा जो तस्वीर लोड करने से लेकर तैयार‑उपयोग JSON दस्तावेज़ उत्पन्न करने तक सब कुछ कर सकेगा।

## आपको क्या चाहिए

- .NET 6.0 या बाद का संस्करण (कोड .NET Core और .NET Framework के साथ भी काम करता है)
- Aspose.OCR for .NET (आप मुफ्त ट्रायल NuGet पैकेज ले सकते हैं)
- एक नमूना PNG या JPG इमेज जिसमें अंग्रेज़ी टेक्स्ट हो
- Visual Studio, VS Code, या कोई भी C#‑संगत IDE

कोई अतिरिक्त लाइब्रेरी आवश्यक नहीं है—सिर्फ मानक `System.Drawing` नेमस्पेस बिटमैप हैंडलिंग के लिए और `System.Text.Json` सीरियलाइज़ेशन के लिए।

---

## चरण 1 – बिटमैप इमेज लोड करें (“load bitmap image” भाग)

कोई OCR करने से पहले, आपको इमेज को मेमोरी में `Bitmap` के रूप में लोड करना होगा। इसे ऐसा समझें जैसे आप किताब खोलते हैं इससे पहले कि आप उसके पन्ने पढ़ना शुरू करें।

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **Pro tip:** यदि इमेज बड़ी है, तो प्रदर्शन सुधारने के लिए पहले उसका आकार बदलने पर विचार करें। OCR इंजन 2 MB से कम आकार की इमेज पर तेज़ काम करता है।

---

## चरण 2 – Aspose OCR इंजन को कॉन्फ़िगर करें

अब बिटमैप तैयार है, हमें एक `OcrEngine` चाहिए। यह ऑब्जेक्ट **छवि से टेक्स्ट निकालना** जानता है और वैकल्पिक रूप से बाउंडिंग बॉक्स जैसी ज्योमेट्री डेटा भी दे सकता है।

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

`ExportBoundingBoxes` को सक्षम क्यों करें? यदि आपको UI में शब्दों को हाइलाइट करना है, तो ये निर्देशांक बहुत उपयोगी होते हैं। यदि आपको इसकी ज़रूरत नहीं है, तो फ़्लैग को `false` सेट कर सकते हैं और JSON थोड़ा हल्का रहेगा।

---

## चरण 3 – OCR चलाएँ और संरचित परिणाम प्राप्त करें

इंजन कॉन्फ़िगर हो जाने के बाद, अगला कदम वास्तविक **टेक्स्ट निकालने** का ऑपरेशन है। `RecognizeToOcrResult` मेथड एक समृद्ध ऑब्जेक्ट लौटाता है जिसमें पहचाना गया टेक्स्ट, कॉन्फिडेंस स्कोर, और वैकल्पिक लेआउट डेटा शामिल होते हैं।

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

`ocrResult` वेरिएबल अब वह सब कुछ रखता है जिसकी आपको आवश्यकता है। यदि आप इसे डिबगर में देखेंगे, तो आपको `Page`, `Paragraph`, `Line`, और `Word` ऑब्जेक्ट्स की एक पदानुक्रमित संरचना दिखेगी, प्रत्येक के पास अपना `Text` प्रॉपर्टी होगा।

---

## चरण 4 – परिणाम को फॉर्मेटेड JSON स्ट्रिंग में सीरियलाइज़ करें

यहीं पर **JSON कैसे सहेजें** का जादू शुरू होता है। हम `System.Text.Json` का उपयोग करेंगे क्योंकि यह बिल्ट‑इन, तेज़, और डिफ़ॉल्ट रूप से प्रीटी प्रिंटिंग को सपोर्ट करता है।

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

यदि आपको अलग नामकरण शैली चाहिए (जैसे camelCase), तो विकल्पों में `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` जोड़ दें।

---

## चरण 5 – JSON को डिस्क पर लिखें (“write json file” चरण)

अंत में, हम वास्तव में **JSON फ़ाइल लिखते** हैं। यह C# वातावरण में **JSON कैसे सहेजें** का ठोस उत्तर है।

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

इस लाइन के चलने के बाद, आपको अपनी मूल इमेज के बगल में एक सुंदर इंडेंटेड `sample-page.json` मिलेगा। इसे किसी भी टेक्स्ट एडिटर से खोलें या किसी अन्य सेवा में फीड करें—आपका OCR डेटा अब पोर्टेबल है।

---

## चरण 6 – आउटपुट की जाँच करें (आपको क्या दिखना चाहिए?)

प्रोग्राम चलाने पर कंसोल में एक छोटा पुष्टि संदेश प्रिंट होना चाहिए:

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

जनरेट की गई JSON फ़ाइल खोलें और आपको कुछ इस तरह दिखेगा:

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

यदि `ExportBoundingBoxes` फ़्लैग `true` था, तो प्रत्येक शब्द में `Rectangle` निर्देशांक भी शामिल होंगे। यह डाउनस्ट्रीम UI कार्य के लिए उपयोगी है।

---

## सामान्य प्रश्न एवं किनारे के मामले

### यदि इमेज पाथ अमान्य हो तो क्या करें?

बिटमैप लोडिंग को `try/catch` ब्लॉक में रखें और स्पष्ट त्रुटि दिखाएँ:

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### गैर‑अंग्रेज़ी भाषाओं को कैसे संभालें?

सिर्फ `Language` प्रॉपर्टी बदल दें:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Aspose 50 से अधिक भाषाओं को सपोर्ट करता है, इसलिए अपनी स्रोत सामग्री के अनुसार उपयुक्त भाषा चुनें।

### क्या मुझे `Bitmap` ऑब्जेक्ट्स को डिस्पोज़ करना चाहिए?

हाँ। `Bitmap` `IDisposable` को इम्प्लीमेंट करता है, इसलिए इसे तुरंत नेटीव रिसोर्सेज़ मुक्त करने के लिए `using` स्टेटमेंट में रैप करें।

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### यदि मैं बिना इंडेंटेशन के कॉम्पैक्ट JSON चाहता हूँ तो क्या करें?

`JsonSerializerOptions` को बदलें:

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

यह फ़ाइल आकार को कम करता है—बैंडविड्थ‑सीमित परिदृश्यों में उपयोगी।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम दिया गया है जिसमें सभी चरण, एरर हैंडलिंग, और बेस्ट‑प्रैक्टिस टिप्स शामिल हैं। इसे `Program.cs` के रूप में सेव करें और कमांड लाइन या अपने IDE से चलाएँ।

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**यह क्या करता है:**  
1. जांचता है कि इमेज मौजूद है।  
2. इसे `using` ब्लॉक के साथ सुरक्षित रूप से लोड करता है।  
3. OCR चलाकर **छवि से टेक्स्ट निकालता** है।  
4. परिणाम को एक सुंदर इंडेंटेड JSON स्ट्रिंग में सीरियलाइज़ करता है।  
5. उस स्ट्रिंग को डिस्क पर सहेजता है, जिससे मुख्य प्रश्न **JSON कैसे सहेजें** का उत्तर मिलता है।

`dotnet run` चलाएँ (या Visual Studio में F5 दबाएँ) और फ़ाइल लिखे जाने के बाद पुष्टि संदेश देखें।

---

## निष्कर्ष

अब आपके पास OCR‑आधारित टेक्स्ट एक्सट्रैक्शन से उत्पन्न **JSON कैसे सहेजें** की एक पूर्ण, प्रोडक्शन‑रेडी रेसिपी है। बिटमैप इमेज लोड करने से लेकर साफ़ JSON फ़ाइल लिखने तक, प्रत्येक चरण को कोड के “क्यों” के साथ समझाया गया है, ताकि आप इसे अपने प्रोजेक्ट में आसानी से अनुकूलित कर सकें।

यदि आप अगले चरण के बारे में जिज्ञासु हैं, तो विचार करें:

- **PDF से टेक्स्ट निकालना** प्रत्येक पेज को पहले इमेज में बदलकर।  
- बाउंडिंग‑बॉक्स डेटा का उपयोग करके WPF या WinForms UI में शब्दों को हाइलाइट करना।  
- फ़ाइल लिखने के बजाय JSON को सीधे वेब API में स्ट्रीम करना (`HttpClient` का उपयोग करके)।

इसे आज़माएँ, विकल्पों को समायोजित करें, और OCR डेटा को अपनी एप्लिकेशन को शक्ति दें। प्रश्न हैं? टिप्पणी छोड़ें, और हैप्पी कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}