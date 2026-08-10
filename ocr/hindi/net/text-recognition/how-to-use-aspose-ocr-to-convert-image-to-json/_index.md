---
category: general
date: 2026-03-15
description: Aspose OCR का उपयोग करके छवियों से टेक्स्ट निकालने और C# में इमेज को
  JSON में बदलने का तरीका। PNG से टेक्स्ट पहचानना सीखें और जल्दी से संरचित आउटपुट
  प्राप्त करें।
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: hi
og_description: Aspose OCR का उपयोग करके छवियों से टेक्स्ट निकालने और C# में इमेज
  को JSON में बदलने का तरीका। यह गाइड आपको PNG से टेक्स्ट पहचानने और संरचित आउटपुट
  प्राप्त करने की प्रक्रिया में मार्गदर्शन करता है।
og_title: Aspose OCR का उपयोग करके इमेज को JSON में कैसे बदलें
tags:
- Aspose
- OCR
- C#
- JSON
title: Aspose OCR का उपयोग करके इमेज को JSON में कैसे बदलें
url: /hi/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR का उपयोग करके इमेज को JSON में कैसे कनवर्ट करें

Aspose OCR का उपयोग कैसे करें, यह डेवलपर्स के लिए एक सामान्य प्रश्न है जब उन्हें चित्रों से टेक्स्ट निकालना होता है। यदि आप **इमेज को JSON में कनवर्ट** करना चाहते हैं या **PNG से टेक्स्ट पहचानना** चाहते हैं, तो यह गाइड आपको पूरी तरह कवर करता है—बिना किसी फालतू के, सिर्फ एक व्यावहारिक, अंत‑से‑अंत समाधान।

अगले कुछ मिनटों में हम वह सब कवर करेंगे जिसकी आपको ज़रूरत है: लाइब्रेरी इंस्टॉल करना, JSON आउटपुट के लिए इंजन को कॉन्फ़िगर करना, एक रसीद PNG लोड करना, OCR चलाना, और अंत में परिणाम को `.json` फ़ाइल में लिखना। अंत तक आप **इमेज से टेक्स्ट निकालने** में सक्षम होंगे एक ही मेथड कॉल से, और समझेंगे कि हर कदम क्यों महत्वपूर्ण है।

> **Pro tip:** Aspose OCR कई इमेज फ़ॉर्मैट्स (PNG, JPEG, BMP, TIFF) के साथ काम करता है। नीचे दिया गया कोड सभी को संभाल लेगा, इसलिए आपको फ़ॉर्मैट‑विशिष्ट लॉजिक लिखने की ज़रूरत नहीं है।

## आपको क्या चाहिए

- .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.6+ पर भी काम करता है)  
- एक वैध Aspose.OCR NuGet पैकेज (फ्री ट्रायल या लाइसेंस्ड)  
- वह इमेज फ़ाइल जिसे आप प्रोसेस करना चाहते हैं (उदाहरण के लिए `receipt.png`)  
- Visual Studio, VS Code, या कोई भी पसंदीदा C# एडिटर  

बस इतना ही—कोई अतिरिक्त डिपेंडेंसी नहीं, कोई बाहरी सर्विस नहीं। तैयार हैं? चलिए शुरू करते हैं।

![Aspose OCR इंजन का उपयोग कैसे करें](image-placeholder.png "Aspose OCR इंजन का उपयोग कैसे करें")

## Aspose OCR का उपयोग – JSON आउटपुट कॉन्फ़िगर करें

OCR के लिए **how to use aspose** करते समय सबसे पहला काम `OcrEngine` इंस्टेंस बनाना और उसे JSON आउटपुट देने के लिए सेट करना है। यह छोटा कॉन्फ़िगरेशन स्विच आपको बाद में मैन्युअल रूप से परिणाम को सीरियलाइज़ करने से बचाता है।

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Why this matters:** `OutputFormat` को `Json` सेट करने का मतलब है कि OCR इंजन पहले से ही टेक्स्ट को पेज, लाइन और शब्दों की हाइरार्की में व्यवस्थित कर देता है। आपको बाद में रॉ स्ट्रिंग्स को पार्स करने की ज़रूरत नहीं पड़ती, जिससे डाउनस्ट्रीम प्रोसेसिंग—जैसे डेटाबेस में डेटा फीड करना—काफी साफ़ हो जाता है।

## Aspose OCR के साथ इमेज को JSON में कनवर्ट करें

अब जब इंजन कॉन्फ़िगर हो गया है, चलिए **इमेज को JSON में कनवर्ट** करने के हिस्से को विस्तार से देखते हैं।

1. **इमेज लोड करें** – `Image.FromFile` किसी भी सपोर्टेड फ़ॉर्मैट के लिए काम करता है। यदि आप स्ट्रीम (जैसे अपलोडेड फ़ाइल) से काम कर रहे हैं, तो `Image.FromStream` का उपयोग कर सकते हैं।  
2. **`Recognize` चलाएँ** – यह मेथड एक `OcrResult` ऑब्जेक्ट रिटर्न करता है। क्योंकि हमने आउटपुट को JSON सेट किया है, `ocrResult.Text` में पहले से ही JSON स्ट्रिंग होती है।  
3. **फ़ाइल लिखें** – `File.WriteAllText` JSON को सहेजने का सबसे सरल तरीका है। यदि आपको इसे क्लाउड बकेट में स्टोर करना है, तो इस लाइन को उपयुक्त SDK कॉल से बदल दें।

### अपेक्षित JSON आउटपुट

एक सामान्य JSON पेलोड इस प्रकार दिखता है (संक्षिप्त रूप में):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

अब आप इस स्ट्रक्चर को किसी भी डाउनस्ट्रीम सिस्टम में फीड कर सकते हैं—चाहे वह रिपोर्टिंग टूल हो, मशीन‑लर्निंग मॉडल, या साधारण लॉग फ़ाइल।

## Aspose OCR का उपयोग करके इमेज से टेक्स्ट निकालें

यदि आपको केवल रॉ स्ट्रिंग चाहिए (अर्थात आप JSON की परवाह नहीं करते), तो आउटपुट फ़ॉर्मैट को फिर से प्लेन टेक्स्ट पर सेट कर दें:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**When to choose plain text?**  
- जल्दी डिबगिंग या कंसोल आउटपुट।  
- ऐसे परिदृश्य जहाँ आप कस्टम पोस्ट‑प्रोसेसिंग (जैसे रेगेक्स एक्सट्रैक्शन) लागू करेंगे।  

लेकिन याद रखें, **इमेज से टेक्स्ट निकालना** JSON के साथ करने से आपको पोज़िशनल डेटा मिलता है—UI में टेक्स्ट हाइलाइट करने या फ़ॉर्म फ़ील्ड्स के साथ संरेखित करने में उपयोगी।

## PNG फ़ाइलों से टेक्स्ट पहचानें

PNG एक लॉसलेस फ़ॉर्मैट है, जो अक्सर भारी कॉम्प्रेस्ड JPEG की तुलना में बेहतर OCR सटीकता देता है। जब आप **PNG से टेक्स्ट पहचानें** तो सबसे अच्छे परिणाम पाने के लिए यहाँ एक त्वरित चेकलिस्ट है:

| Checklist Item | Why It Helps |
|----------------|--------------|
| 300+ DPI का उपयोग करें | उच्च रेज़ोल्यूशन इंजन को अधिक पिक्सेल देता है, जिससे परिणाम बेहतर होते हैं। |
| इमेज को ग्रेस्केल रखें | शोर कम होता है; Aspose OCR स्वचालित रूप से कन्वर्ट करता है, लेकिन प्री‑प्रोसेसिंग से गति बढ़ सकती है। |
| बैकग्राउंड क्लटर हटाएँ | साफ़ बैकग्राउंड कॉन्फिडेंस स्कोर को सुधारते हैं। |

यदि आपको कम कॉन्फिडेंस स्कोर मिलते हैं, तो DPI बढ़ाने या इमेज को थ्रेशहोल्ड फ़िल्टर से प्रोसेस करने की कोशिश करें, फिर Aspose को फीड करें।

## प्रोग्रामेटिकली OCR परिणाम निकालें

सिर्फ JSON सहेजने से आगे, आप प्रोग्रामेटिकली विशिष्ट फ़ील्ड्स पढ़ना चाह सकते हैं—जैसे रसीद पर कुल राशि। क्योंकि JSON में हाइरार्की होती है, आप इसे एक C# ऑब्जेक्ट में डीसिरियलाइज़ कर सकते हैं:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

अब आप `ocrData` को LINQ के साथ क्वेरी कर सकते हैं:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Why this works:** JSON पहले से ही बताता है कि प्रत्येक शब्द पेज पर कहाँ स्थित है, इसलिए लेआउट में थोड़े बदलाव होने पर भी आप फ़ील्ड्स को भरोसेमंद तरीके से ढूँढ़ सकते हैं।

## किनारे के मामलों और सामान्य जाल

- **Null Result:** यदि `ocrEngine.Recognize` `null` रिटर्न करता है, तो इमेज असपोर्टेड या करप्ट हो सकती है। हमेशा इसे हैंडल करें:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Large Files:** मल्टी‑मेगाबाइट इमेज के लिए, OCR से पहले इमेज को स्ट्रीम करने या रिसाइज़ करने पर विचार करें ताकि मेमोरी उपयोग कम रहे।

- **License Issues:** ट्रायल वर्ज़न आउटपुट में वॉटरमार्क जोड़ता है। सुनिश्चित करें कि आप प्रोग्राम की शुरुआत में अपना लाइसेंस लोड करें:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Non‑Latin Scripts:** Aspose OCR कई भाषाओं को सपोर्ट करता है, लेकिन आपको `Language` प्रॉपर्टी को उचित रूप से सेट करना होगा (उदाहरण: `ocrEngine.Configuration.Language = Language.English;`)।

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}