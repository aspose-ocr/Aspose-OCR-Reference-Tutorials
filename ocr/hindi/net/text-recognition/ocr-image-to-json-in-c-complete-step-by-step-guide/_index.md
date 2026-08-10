---
category: general
date: 2026-02-11
description: C# में OCR इमेज को JSON में बदलें। इमेज से टेक्स्ट निकालना सीखें, C#
  में इमेज फ़ाइल पढ़ें, JSON आउटपुट को फॉर्मेट करें और Aspose.OCR के साथ C# में JSON
  को सुंदर रूप से प्रिंट करें।
draft: false
keywords:
- ocr image to json
- extract text from image
- read image file c#
- format json output
- pretty print json c#
language: hi
og_description: C# में OCR इमेज को JSON में बदलें। यह गाइड दिखाता है कि इमेज से टेक्स्ट
  कैसे निकाला जाए, C# में इमेज फ़ाइल पढ़ी जाए, JSON आउटपुट को फ़ॉर्मेट किया जाए और
  Aspose.OCR का उपयोग करके C# में JSON को सुंदर रूप से प्रिंट किया जाए।
og_title: C# में OCR इमेज को JSON में बदलें – पूर्ण चरण‑दर‑चरण गाइड
tags:
- OCR
- C#
- JSON
title: C# में OCR इमेज को JSON में बदलें – पूर्ण चरण‑दर‑चरण गाइड
url: /hi/net/text-recognition/ocr-image-to-json-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में इमेज को JSON में OCR – पूर्ण चरण‑दर‑चरण गाइड

क्या आपको कभी **ocr image to json** करने की ज़रूरत पड़ी, लेकिन यह नहीं पता था कि कौन‑सी लाइब्रेरी चुनें या परिणाम को कैसे सुंदर रूप में प्राप्त करें? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया के ऐप्स—रसीद स्कैनिंग, आईडी वेरिफिकेशन, या साधारण दस्तावेज़ अभिलेख—में आप इमेज से टेक्स्ट निकालना चाहते हैं और एक साफ़ JSON पेलोड चाहते हैं जिसे डाउनस्ट्रीम सर्विसेज़ उपयोग कर सकें।

इस ट्यूटोरियल में हम पूरी पाइपलाइन को कवर करेंगे: C# में इमेज फ़ाइल पढ़ने से लेकर Aspose.OCR के साथ टेक्स्ट निकालने, फिर इंजन से संरचित JSON आउटपुट माँगने, और अंत में उस JSON को प्री‑टिंट करके मानव‑पठनीय बनाना। अंत तक आपके पास एक स्व‑समाहित, प्रोडक्शन‑रेडी स्निपेट होगा जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं।

हम सामान्य समस्याओं (जैसे लापता लैंग्वेज पैक्स) पर भी चर्चा करेंगे और कुछ तेज़ वैरिएशन दिखाएंगे—जैसे XML आउटपुट में स्विच करना या मल्टी‑पेज PDF को हैंडल करना। कोई बाहरी दस्तावेज़ीकरण आवश्यक नहीं; सब कुछ यहाँ उपलब्ध है।

## What You’ll Need

- **.NET 6+** (कोड .NET Framework 4.7+ के साथ भी काम करता है)
- **Aspose.OCR for .NET** – NuGet से इंस्टॉल करें (`Install-Package Aspose.OCR`)
- एक सैंपल इमेज (जैसे `receipt.png`) जिसे आप रेफ़रेंस कर सकें
- C# सिंटैक्स की बेसिक समझ (यदि आपने “Hello World” लिखा है, तो आप तैयार हैं)

> *Pro tip:* यदि आप CI सर्वर पर हैं, तो `AutomaticResourceDownload = true` सेट करें ताकि Aspose रन‑टाइम पर भाषा डेटा को स्वचालित रूप से डाउनलोड कर ले—कोई मैन्युअल DLL जुग्लिंग नहीं।

## Step 1: Read image file C# and create the OCR engine  

सबसे पहले हम डिस्क से इमेज लोड करते हैं। `System.Drawing.Image` का उपयोग कोड को छोटा रखता है और PNG, JPEG, BMP, तथा मल्टी‑पेज TIFF (डिफ़ॉल्ट रूप से पहला पेज चुना जाता है) को सपोर्ट करता है।

```csharp
using System.Drawing;          // For Image
using Aspose.OCR;              // Core OCR classes
using Aspose.OCR.Models;       // Language and output enums
using System.Text.Json;        // JSON parsing & pretty‑print

// 1️⃣ Configure the OCR engine – this is where we tell Aspose what language we expect
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // extract text from image in English
    AutomaticResourceDownload = true,        // auto‑download language packs if missing
    OutputFormat = OcrOutputFormat.Json      // ask for JSON rather than plain text
};
```

**Why this matters:**  
- `AutomaticResourceDownload` इंग्लिश भाषा फ़ाइल स्थानीय रूप से न होने पर रन‑टाइम क्रैश को रोकता है।  
- `OutputFormat` को `Json` सेट करने से इंजन पहले से ही रॉ OCR परिणाम को संरचित ऑब्जेक्ट में बदल देता है—कोई मैन्युअल स्ट्रिंग पार्सिंग नहीं चाहिए।

## Step 2: Run OCR and obtain JSON output  

अब हम लोड किए गए बिटमैप को इंजन में फीड करते हैं। `Recognize` मेथड एक `OcrResult` रिटर्न करता है जिसमें `Text` प्रॉपर्टी JSON स्ट्रिंग रखती है।

```csharp
// 2️⃣ Load the image you want to process
using (var receiptImage = Image.FromFile(@"C:\Images\receipt.png"))
{
    // 3️⃣ Perform OCR – this call blocks until the engine finishes
    var ocrResult = ocrEngine.Recognize(receiptImage);

    // 4️⃣ The OCR engine gave us JSON straight away
    string rawJson = ocrResult.Text;
    
    // Optional: write the raw JSON to a file for debugging
    System.IO.File.WriteAllText(@"C:\Temp\ocr_raw.json", rawJson);
}
```

**Edge case:** यदि इमेज करप्टेड है या पाथ गलत है, तो `Image.FromFile` `FileNotFoundException` थ्रो करता है। यदि इनपुट अनिश्चित है तो ब्लॉक को `try/catch` में रैप करें।

## Step 3: Parse and format the JSON – pretty print JSON C#  

OCR इंजन से मिलने वाला रॉ JSON कॉम्पैक्ट और आँखों के लिए कठिन होता है। `System.Text.Json` का उपयोग करके हम इसे `JsonDocument` में डीसिरियलाइज़ कर सकते हैं, फिर इंडेंटेशन के साथ री‑सीरियलाइज़ कर सकते हैं।

```csharp
// 5️⃣ Parse the JSON string into a DOM-like structure
using var jsonDoc = JsonDocument.Parse(rawJson);

// 6️⃣ Pretty‑print with indentation (2 spaces by default)
string prettyJson = JsonSerializer.Serialize(
    jsonDoc.RootElement,
    new JsonSerializerOptions { WriteIndented = true });

// 7️⃣ Output to console – you could also send this to an API or a file
Console.WriteLine(prettyJson);

// 8️⃣ Save the pretty JSON for later use
System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
```

**What you’ll see:**  

```json
{
  "Lines": [
    {
      "Text": "Store Name",
      "BoundingBox": { "X": 12, "Y": 5, "Width": 150, "Height": 20 }
    },
    {
      "Text": "Total: $23.45",
      "BoundingBox": { "X": 12, "Y": 200, "Width": 100, "Height": 20 }
    }
  ],
  "Language": "English",
  "Confidence": 0.96
}
```

अब JSON में लाइन‑बाय‑लाइन टेक्स्ट, बाउंडिंग बॉक्स, डिटेक्टेड लैंग्वेज, और कॉन्फिडेंस स्कोर शामिल है—डाउनस्ट्रीम एनालिटिक्स या UI कंपोनेंट में फीड करने के लिए एकदम उपयुक्त।

## Step 4: Bonus – Switching output format or language  

यदि आपको **format json output** को XML में बदलना है या स्पेनिश रसीद OCR करनी है, तो बस इंजन कॉन्फ़िगरेशन को बदलें:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;          // extract text from image in Spanish
ocrEngine.OutputFormat = OcrOutputFormat.Xml;     // ask for XML instead of JSON
```

बाकी कोड वही रहता है; आपको केवल डीसिरियलाइज़ेशन स्टेप बदलना होगा (XML के लिए `XmlDocument` उपयोग करें)।

## Full Working Example  

सब कुछ एक साथ जोड़ते हुए, यहाँ एक सिंगल फ़ाइल है जिसे आप कॉन्सोल ऐप में कॉपी‑पेस्ट कर सकते हैं:

```csharp
// ---------------------------------------------------------------
// ocr_image_to_json_demo.cs
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Text.Json;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Configure OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            AutomaticResourceDownload = true,
            OutputFormat = OcrOutputFormat.Json
        };

        // Path to your image – adjust as needed
        string imagePath = @"C:\Images\receipt.png";

        try
        {
            using (var receiptImage = Image.FromFile(imagePath))
            {
                var ocrResult = ocrEngine.Recognize(receiptImage);
                string rawJson = ocrResult.Text;

                // Parse & pretty‑print
                using var jsonDoc = JsonDocument.Parse(rawJson);
                string prettyJson = JsonSerializer.Serialize(
                    jsonDoc.RootElement,
                    new JsonSerializerOptions { WriteIndented = true });

                Console.WriteLine("=== Pretty‑Printed OCR JSON ===");
                Console.WriteLine(prettyJson);

                // Optional: write to file
                System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Error processing image: {ex.Message}");
        }
    }
}
```

इस प्रोग्राम को चलाने पर एक सुंदर इंडेंटेड JSON पेलोड कंसोल में प्रिंट होगा और `C:\Temp\ocr_pretty.json` में सेव होगा। `try/catch` ब्लॉक यह सुनिश्चित करता है कि यदि इमेज पढ़ी नहीं जा सकती, तो आपको साइलेंट क्रैश की बजाय स्पष्ट एरर मैसेज मिलेगा।

## Common Questions & Gotchas  

- **What if the OCR returns empty text?**  
  आमतौर पर इसका मतलब है इमेज बहुत नॉइज़ी है या लैंग्वेज मिसमैच है। इमेज कॉन्ट्रास्ट बढ़ाएँ या `Language` को `AutoDetect` पर सेट करें।  

- **Can I process multiple images in a loop?**  
  बिल्कुल। `using (var img = Image.FromFile(...))` ब्लॉक को `foreach (var file in Directory.GetFiles(...))` लूप में रखें और प्रत्येक `prettyJson` को लिस्ट में जमा करें या अलग‑अलग फ़ाइलों में लिखें।

- **Is the JSON schema stable?**  
  Aspose `Json` आउटपुट फ़ॉर्मेट के लिए बैकवर्ड कम्पैटिबिलिटी गारंटी देता है, लेकिन यदि आप किसी विशिष्ट API वर्ज़न को टारगेट कर रहे हैं तो रेस्पॉन्स में `Version` एट्रिब्यूट चेक करना न भूलें।

- **Do I need a license for Aspose.OCR?**  
  फ्री इवैल्यूएशन की 100 पेज तक की सीमा है। प्रोडक्शन के लिए लाइसेंस खरीदें और इसे इस तरह सेट करें: `License license = new License(); license.SetLicense("Aspose.OCR.lic");`।

## Conclusion  

अब आपके पास **complete, self‑contained solution to ocr image to json** C# में है। इमेज फ़ाइल पढ़ने, OCR इंजन कॉन्फ़िगर करने, JSON आउटपुट माँगने, और उसे प्री‑टिंट करने के बाद आप टेक्स्ट एक्सट्रैक्शन को किसी भी .NET सर्विस में बिना स्ट्रिंग हैक्स के इंटीग्रेट कर सकते हैं।  

अब आप **extract text from image** को अन्य फ़ाइल टाइप्स (PDF, मल्टी‑पेज TIFF) के लिए एक्सप्लोर कर सकते हैं, विभिन्न लैंग्वेज़ के साथ प्रयोग कर सकते हैं, या JSON को NoSQL स्टोर में एनालिटिक्स के लिए पाइप कर सकते हैं। सीमाएँ केवल आपकी कल्पना हैं—सिर्फ एरर हैंडलिंग को ग्रेसफ़ुल रखें और स्केल अप करते समय लाइसेंसिंग पर ध्यान दें।

Happy coding, and may your OCR pipelines be ever accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}