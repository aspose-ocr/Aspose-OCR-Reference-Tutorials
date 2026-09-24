---
category: general
date: 2026-01-02
description: Aspose OCR का उपयोग करके C# में छवि से पाठ निकालें। जानें कि कैसे छवि
  को जल्दी और भरोसेमंद तरीके से JSONL फ़ॉर्मेट में बदलें।
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: hi
og_description: छवि से टेक्स्ट निकालें Aspose OCR के साथ और इसे JSONL फ़ॉर्मेट में
  बदलें। डेवलपर्स के लिए पूर्ण चरण-दर-चरण C# ट्यूटोरियल।
og_title: इमेज से टेक्स्ट निकालें – C# में JSONL में परिवर्तित करें
tags:
- C#
- OCR
- Aspose
- JSONL
title: इमेज से टेक्स्ट निकालें और JSONL में बदलें – C# गाइड
url: /hi/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# छवि से टेक्स्ट निकालें और JSONL में बदलें – पूरा C# ट्यूटोरियल

क्या आपको कभी **छवि से टेक्स्ट निकालने** की जरूरत पड़ी है लेकिन यह नहीं पता था कि कौन‑सी लाइब्रेरी साफ़, संरचित आउटपुट देगी? आप अकेले नहीं हैं। कई रसीद‑प्रोसेसिंग या दस्तावेज़‑डिजिटलीकरण प्रोजेक्ट्स में बाधा यह होती है कि बिटमैप को खोज योग्य टेक्स्ट *और* मशीन‑पठनीय फ़ॉर्मेट में बदलना।  

अच्छी ख़बर? Aspose OCR के साथ आप **छवि से टेक्स्ट निकाल सकते** हैं और कुछ ही लाइनों के कोड से **छवि को JSONL में बदल सकते** हैं ताकि आगे के एनालिटिक्स में उपयोग हो सके। यह गाइड आपको पूरी प्रक्रिया से गुज़राता है, PNG लोड करने से लेकर JSON‑Lines फ़ाइल लिखने तक, जिसे डेटा पाइपलाइन में स्ट्रीम किया जा सकता है।

> **संकेत:** यदि आप पहले से .NET 6 या बाद का उपयोग कर रहे हैं, तो वही कोड बिना किसी अतिरिक्त कॉन्फ़िगरेशन के काम करेगा।

## पूर्वापेक्षाएँ — आपको क्या चाहिए

- **.NET 6 SDK** (या कोई भी नवीनतम .NET संस्करण)
- **Aspose.OCR** NuGet पैकेज  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** सीरियलाइज़ेशन के लिए  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- एक नमूना छवि (जैसे, `receipt.png`) जिसे आप किसी फ़ोल्डर में रख सकते हैं।
- आपका पसंदीदा IDE या एडिटर—Visual Studio, VS Code, Rider, आदि।

कोई भारी सेट‑अप नहीं, कोई बाहरी सेवा नहीं, सिर्फ कुछ NuGet पैकेज।

![C# का उपयोग करके छवि से टेक्स्ट निकालें](https://example.com/assets/ocr-sample.png)

*Alt text: C# का उपयोग करके छवि से टेक्स्ट निकालें Aspose OCR के साथ*

## चरण 1: वह छवि लोड करें जिसे आप प्रोसेस करना चाहते हैं  

जब आप **छवि से टेक्स्ट निकालना** चाहते हैं, तो सबसे पहले OCR इंजन को एक बिटमैप देना होता है। `System.Drawing.Bitmap` का उपयोग सरल है और अधिकांश रास्टर फ़ॉर्मेट्स के लिए काम करता है।

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **क्यों महत्वपूर्ण है:** छवि को `Bitmap` के रूप में लोड करने से OCR इंजन को सीधे पिक्सेल एक्सेस मिलता है, जिससे पहचान की गति और सटीकता दोनों में सुधार होता है, साधारण बाइट‑स्ट्रीम की तुलना में।

## चरण 2: JSON‑Lines आउटपुट के लिए Aspose OCR को कॉन्फ़िगर करें  

Aspose OCR आपको भाषा, आउटपुट फ़ॉर्मेट, और कुछ प्रदर्शन‑ट्यूनिंग विकल्प निर्दिष्ट करने देता है। यहाँ हम **JSON‑Lines** (प्रति लाइन एक JSON ऑब्जेक्ट) का अनुरोध करते हैं क्योंकि यह बाद में लाइन‑बाय‑लाइन प्रोसेसिंग के लिए आदर्श है।

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **प्रो टिप:** यदि आपको बहुभाषी रसीदें चाहिए, तो `Language = Language.Multilingual` सेट करें या `Language` मानों की एक एरे पास करें।

## चरण 3: OCR चलाएँ और परिणाम कैप्चर करें  

अब हम वास्तव में **छवि से टेक्स्ट निकालते** हैं। `Recognize` मेथड एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें `OcrLine` ऑब्जेक्ट्स का संग्रह होता है, प्रत्येक में पहचाने गए टेक्स्ट की लाइन और उसका बाउंडिंग बॉक्स शामिल होता है।

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

इस बिंदु पर `ocrResult.Lines` में वह सब कुछ है जो आपको चाहिए—कच्चा टेक्स्ट, कॉन्फिडेंस स्कोर, और कोऑर्डिनेट्स।

## चरण 4: लाइनों को JSON‑Lines में सीरियलाइज़ करें  

हम संग्रह को एक सुंदर इंडेंटेड JSON स्ट्रिंग में बदलेंगे। यद्यपि JSON‑Lines आमतौर पर कॉम्पैक्ट होते हैं, इंडेंटेशन जोड़ने से विकास के दौरान फ़ाइल को देखना आसान हो जाता है।

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

परिणामी `jsonLines` वेरिएबल कुछ इस तरह दिखेगा (संक्षिप्त रूप में):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

प्रत्येक लाइन के अंत में एक न्यूलाइन कैरेक्टर होगा, जिससे आपको एक सच्ची **JSONL** (JSON‑Lines) फ़ाइल मिलती है।

## चरण 5: JSON‑Lines को डिस्क पर लिखें  

अंत में, हम आउटपुट को स्थायी बनाते हैं ताकि अन्य सेवाएँ—जैसे Spark, Logstash, या एक साधारण Bash स्क्रिप्ट—इसे लाइन दर लाइन इन्जेस्ट कर सकें।

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

जब आप `receipt.jsonl` खोलेंगे, तो आपको प्रति लाइन एक JSON ऑब्जेक्ट दिखाई देगा, जो स्ट्रीमिंग के लिए तैयार है।

## चरण 6: एक्सपोर्ट की पुष्टि करें  

एक त्वरित सैनीटी चेक बाद में डिबगिंग के घंटों को बचा सकता है। चलिए पहले कुछ लाइनों को फिर से पढ़ते हैं और कंसोल पर प्रिंट करते हैं।

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

सामान्य कंसोल आउटपुट:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

यदि आपको ऐसा कुछ दिखे, तो बधाई—आपने सफलतापूर्वक **छवि से टेक्स्ट निकाला** और **छवि को JSONL में बदला** है।

## सामान्य समस्याएँ और उनके समाधान  

| समस्या | क्यों होती है | समाधान |
|-------|----------------|-----|
| **खाली आउटपुट** | छवि पाथ गलत है या फ़ाइल पढ़ी नहीं जा रही। | `File.Exists(imagePath)` का उपयोग करके बिटमैप बनाने से पहले जाँचें। |
| **कम कॉन्फिडेंस स्कोर** | छवि धुंधली या कम कंट्रास्ट वाली है। | छवि को प्री‑प्रोसेस करें (जैसे `Bitmap.RotateFlip`, `Graphics.Clear`) या DPI बढ़ाएँ। |
| **गलत भाषा** | OCR डिफ़ॉल्ट रूप से अंग्रेज़ी मानता है जबकि रसीद किसी अन्य भाषा में है। | `options.Language = Language.Spanish` (या उपयुक्त enum) सेट करें। |
| **JSONL एकल JSON एरे जैसा दिखता है** | आपने `Formatting.None` के साथ न्यूलाइन हैंडलिंग नहीं की। | सुनिश्चित करें कि प्रत्येक सीरियलाइज़्ड ऑब्जेक्ट के अंत में `Environment.NewLine` हो। |

## पूर्ण कार्यशील उदाहरण  

नीचे पूरा, तैयार‑चलाने‑योग्य प्रोग्राम है। इसे एक कंसोल प्रोजेक्ट में पेस्ट करें और **F5** दबाएँ।

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**अपेक्षित परिणाम:** एक `receipt.jsonl` फ़ाइल जिसमें प्रति लाइन एक JSON ऑब्जेक्ट होगा, जिसमें `Text`, `Confidence`, और `BoundingBox` फ़ील्ड्स होंगी। अब आप इस फ़ाइल को किसी भी एनालिटिक्स पाइपलाइन में फीड कर सकते हैं जो JSONL को सपोर्ट करती है।

## अगले कदम – बेसिक OCR से आगे बढ़ें  

- **बैच प्रोसेसिंग:** ऊपर की लॉजिक को `foreach` लूप में रखें ताकि रसीदों के पूरे फ़ोल्डर को हैंडल किया जा सके।  
- **पैरालेलिज़्म:** हजारों छवियों के साथ काम करते समय मल्टी‑कोर स्पीड‑अप के लिए `Parallel.ForEach` उपयोग करें।  
- **पोस्ट‑प्रोसेसिंग:** स्टोर करने से पहले कम‑कॉन्फिडेंस लाइनों (`Confidence < 0.9`) को हटाएँ।  
- **इंटीग्रेशन:** संबंधित SDKs के साथ JSONL को सीधे Azure Blob Storage या AWS S3 पर पुश करें।  
- **वैकल्पिक फ़ॉर्मेट:** यदि आपका डाउनस्ट्रीम सिस्टम अन्य फ़ॉर्मेट पसंद करता है तो `OutputFormat` को `PlainText` या `Xml` में बदलें।

## निष्कर्ष  

आपके पास अब Aspose OCR का उपयोग करके C# में **छवि से टेक्स्ट निकालने** और **छवि को JSONL में बदलने** के लिए एक ठोस, एंड‑टू‑एंड समाधान है। इस ट्यूटोरियल में बिटमैप लोड करने से लेकर आउटपुट की पुष्टि तक सब कुछ कवर किया गया है, साथ ही आपके पाइपलाइन को मजबूत रखने के लिए कई व्यावहारिक टिप्स भी दिए गए हैं।

अपनी रसीदों, इनवॉइसों या स्कैन किए हुए फ़ॉर्म्स के साथ इसे आज़माएँ—देखें OCR इंजन पिक्सेल को सेकंडों में खोज योग्य, लाइन‑स्ट्रक्चर्ड डेटा में बदलता है। यदि आपको किनारे के केस (जैसे तिरछी स्कैन या बहुभाषी टेक्स्ट) मिलते हैं, तो *RecognitionOptions* सेक्शन पर वापस जाएँ और भाषा या प्री‑प्रोसेसिंग स्टेप्स को ट्यून करें।

हैप्पी कोडिंग, और आपके डेटा पाइपलाइन हमेशा साफ़ रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}