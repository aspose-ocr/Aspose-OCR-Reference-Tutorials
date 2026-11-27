---
category: general
date: 2026-11-26
description: Aspose.OCR का उपयोग करके PNG फ़ाइलों पर OCR कैसे करें, PNG को टेक्स्ट
  में बदलें, और सायरिलिक टेक्स्ट निकालें – डेवलपर्स के लिए चरण‑दर‑चरण गाइड।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: hi
lastmod: 2026-11-26
og_description: C# में Aspose.OCR का उपयोग करके PNG फ़ाइलों पर OCR कैसे करें और सायरिलिक
  टेक्स्ट निकालें। PNG को टेक्स्ट में बदलने के लिए इस पूर्ण ट्यूटोरियल का पालन करें।
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Aspose.OCR के साथ PNG इमेजेज़ पर OCR कैसे करें – C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: C# में Aspose.OCR का उपयोग करके PNG छवियों पर OCR कैसे करें
url: /hi/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG छवियों पर Aspose.OCR के साथ C# में OCR कैसे करें

यदि आपको PNG फ़ाइल पर **OCR कैसे करें** करने की आवश्यकता है, तो यह गाइड Aspose.OCR का उपयोग करके PNG को टेक्स्ट में बदलने के सटीक चरण दिखाता है। चाहे आप स्कैन किए गए दस्तावेज़ों से Cyrillic टेक्स्ट निकाल रहे हों या केवल PNG स्क्रीनशॉट से टेक्स्ट पहचान रहे हों, यह समाधान तुरंत काम करता है और केवल कुछ ही पंक्तियों के C# कोड की आवश्यकता होती है।

इस ट्यूटोरियल में आप सीखेंगे कि कैसे:

* **OCR के लिए छवि लोड करें** स्थानीय फ़ोल्डर से,
* इंजन को **Cyrillic टेक्स्ट निकालें** के लिए कॉन्फ़िगर करें,
* **PNG से टेक्स्ट पहचानें** और एक साफ़ स्ट्रिंग प्राप्त करें,
* गुम भाषा मॉड्यूल और बड़ी छवियों जैसी सामान्य समस्याओं को संभालें।

Aspose.OCR के साथ कोई पूर्व अनुभव आवश्यक नहीं है—सिर्फ एक .NET विकास वातावरण और वह PNG छवि जिसे आप प्रोसेस करना चाहते हैं।

## आवश्यकताएँ

* .NET 6.0 (या बाद का) स्थापित हो।
* एक लाइसेंस प्राप्त या ट्रायल कॉपी **Aspose.OCR for .NET** की। आप Aspose वेबसाइट से मुफ्त ट्रायल प्राप्त कर सकते हैं।
* Visual Studio 2022 (या कोई भी IDE जो .NET को सपोर्ट करता है)।
* एक PNG फ़ाइल जिसमें वह टेक्स्ट हो जिसे आप निकालना चाहते हैं (उदाहरण में `sample_image.png` उपयोग किया गया है)।

## चरण 1: Aspose.OCR NuGet पैकेज स्थापित करें

अपने प्रोजेक्ट फ़ोल्डर में एक टर्मिनल खोलें और चलाएँ:

```bash
dotnet add package Aspose.OCR
```

यह पैकेज कोर OCR इंजन और सभी भाषा मॉड्यूल शामिल करता है। जब आप कोई ऐसी भाषा अनुरोध करते हैं जो स्थानीय रूप से उपलब्ध नहीं है, तो Aspose.OCR स्वचालित रूप से आवश्यक मॉड्यूल डाउनलोड कर लेता है।

## चरण 2: OCR इंजन का इंस्टेंस बनाएं (OCR कैसे करें)

किसी भी OCR वर्कफ़्लो में पहला कार्यात्मक कदम इंजन को इंस्टैंशिएट करना है। यह ऑब्जेक्ट सभी बाद की ऑपरेशन्स जैसे छवि लोड करना और पहचान करना को प्रबंधित करता है।

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**यह क्यों महत्वपूर्ण है:** `OcrEngine` क्लास OCR पाइपलाइन को संलग्न करती है। एक ही इंस्टेंस बनाकर और इसे कई छवियों में पुनः उपयोग करने से मेमोरी ओवरहेड कम होता है और प्रदर्शन बेहतर होता है।

## चरण 3: OCR के लिए छवि लोड करें – स्रोत PNG फ़ाइल निर्दिष्ट करें

छवि लोड करना वह बिंदु है जहाँ आप **OCR के लिए छवि लोड करें**। Aspose.OCR कई इनपुट प्रकार स्वीकार करता है; सबसे सरल `ImageStream.FromFile` है।

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **Pro tip:** विभिन्न पर्यावरणों में रनटाइम त्रुटियों से बचने के लिए एक पूर्ण पथ या `Path.Combine` का उपयोग करें।

### बड़ी छवियों को संभालना

यदि PNG 2 MB से बड़ी है, तो प्रोसेसिंग गति बढ़ाने के लिए पहचान से पहले इसे डाउन‑स्केल करने पर विचार करें:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## चरण 4: भाषा कॉन्फ़िगर करें – Cyrillic टेक्स्ट निकालें

डिफ़ॉल्ट रूप से, Aspose.OCR अंग्रेज़ी मानता है। **Cyrillic टेक्स्ट निकालने** के लिए, `Language` प्रॉपर्टी को `Language.Cyrillic` सेट करें। आवश्यक मॉड्यूल कोड पहली बार चलाने पर स्वचालित रूप से डाउनलोड हो जाएगा।

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

यदि आपको कई भाषाओं को पहचानना है (जैसे, अंग्रेज़ी और Cyrillic), तो आप उन्हें संयोजित कर सकते हैं:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### किनारा मामला: गुम भाषा मॉड्यूल

यदि डाउनलोड विफल हो जाता है (जैसे, ऑफ़लाइन पर्यावरण), तो इंजन `OcrException` फेंकेगा। इसे पकड़ें ताकि एक सुगम बैकअप प्रदान किया जा सके:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## चरण 5: पहचान ऑपरेशन निष्पादित करें (PNG से टेक्स्ट पहचानें)

अब जबकि छवि और भाषा सेट हो गई हैं, आप **PNG से टेक्स्ट पहचानें** कर सकते हैं। `Recognize` मेथड OCR पाइपलाइन को सिंक्रोनस रूप से चलाता है।

```csharp
// Run OCR
ocrEngine.Recognize();
```

**यह क्यों काम करता है:** आंतरिक रूप से, Aspose.OCR चयनित भाषा के लिए ट्यून किए गए न्यूरल‑नेटवर्क आधारित रेकग्नाइज़र में छवि फीड करने से पहले प्री‑प्रोसेसिंग (बाइनराइज़ेशन, शोर हटाना) लागू करता है।

## चरण 6: पहचाने गए टेक्स्ट को प्राप्त करें और प्रदर्शित करें (PNG को टेक्स्ट में बदलें)

पहचान के बाद, निकाला गया स्ट्रिंग `Text` प्रॉपर्टी के माध्यम से उपलब्ध होता है। यह **PNG को टेक्स्ट में बदलें** में अंतिम चरण है।

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### अपेक्षित आउटपुट

यदि `sample_image.png` में Cyrillic वाक्यांश “Привет мир” है, तो कंसोल यह प्रदर्शित करेगा:

```
=== OCR Result ===
Привет мир
```

आउटपुट में लाइन ब्रेक और विराम चिह्न वही हो सकते हैं जैसे छवि में दिखते हैं। यदि आवश्यक हो तो आप स्ट्रिंग को `String.Trim()`, `Regex`, या अन्य टेक्स्ट‑क्लीनिंग यूटिलिटीज़ से पोस्ट‑प्रोसेस कर सकते हैं।

## चरण 7: वैकल्पिक – परिणाम को फ़ाइल में सहेजें

OCR परिणाम को सहेजने से डाउनस्ट्रीम प्रोसेसिंग (जैसे, इंडेक्सिंग, अनुवाद) संभव होती है। यहाँ टेक्स्ट को UTF‑8 फ़ाइल में लिखने का एक त्वरित तरीका है:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## सामान्य समस्याएँ और उन्हें कैसे टालें

| Issue | Symptom | Fix |
|-------|----------|-----|
| **भाषा मॉड्यूल गुम** | `OcrException` पर `Language = Language.Cyrillic` | पहली बार चलाते समय इंटरनेट कनेक्टिविटी सुनिश्चित करें या Aspose के ऑफ़लाइन पैकेज के माध्यम से मॉड्यूल पहले से डाउनलोड करें। |
| **धुंधली या कम‑कॉन्ट्रास्ट वाली छवि** | कम सटीकता, कई “?” अक्षर | छवि को प्री‑प्रोसेस करें: कॉन्ट्रास्ट बढ़ाएँ, शार्पनिंग लागू करें, या इंजन में फीड करने से पहले ग्रेस्केल में बदलें। |
| **बहुत बड़ी PNG** | लंबा प्रोसेसिंग समय, संभावित `OutOfMemoryException` | जैसा कि चरण 3 में दिखाया गया है, डाउनस्केल करें, या मल्टी‑पेज छवि को अलग‑अलग टाइल्स में विभाजित करें। |
| **Non‑UTF‑8 अक्षर** | बिखरा हुआ आउटपुट | सुनिश्चित करें कि कंसोल या फ़ाइल राइटर UTF‑8 एन्कोडिंग (`Encoding.UTF8`) का उपयोग कर रहा है। |

## पूर्ण, चलाने योग्य उदाहरण

नीचे वह पूर्ण प्रोग्राम है जो ऊपर बताए सभी चरणों को सम्मिलित करता है। इसे एक नए कंसोल प्रोजेक्ट में कॉपी करें और फ़ाइल पाथ्स को समायोजित करने के बाद चलाएँ।

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### यह कैसे काम करता है

1. **Engine creation** – OCR पाइपलाइन तैयार करता है।  
2. **Image loading** – प्रदर्शन के लिए कच्ची PNG और डाउन‑स्केल्ड दोनों संस्करणों को सपोर्ट करता है।  
3. **Language selection** – **Cyrillic टेक्स्ट निकालें** को दर्शाता है जबकि गुम मॉड्यूल को संभालता है।  
4. **Recognition** – मुख्य **PNG से टेक्स्ट पहचानें** कॉल।  
5. **Result handling** – **PNG को टेक्स्ट में बदलें** दिखाता है और आउटपुट को फ़ाइल में लिखता है।

`dotnet run` के साथ प्रोग्राम चलाएँ। यदि सब कुछ सही ढंग से सेट है, तो आप कंसोल में पहचाना गया टेक्स्ट प्रिंट होते और `ocr_output.txt` में सहेजा हुआ देखेंगे।

## निष्कर्ष

इस ट्यूटोरियल में आपने Aspose.OCR for .NET का उपयोग करके PNG फ़ाइलों पर **OCR कैसे करें** सीख लिया, जिसमें **OCR के लिए छवि लोड करें** से लेकर **Cyrillic टेक्स्ट निकालें** और **PNG को टेक्स्ट में बदलें** तक सब कुछ शामिल है। पूर्ण, चलाने योग्य उदाहरण मानक वर्कफ़्लो, सामान्य किनारा मामलों, और व्यावहारिक टिप्स को दर्शाता है जो आपके OCR पाइपलाइन को विश्वसनीय बनाते हैं।

**अगले कदम**

* अतिरिक्त भाषाओं (Arabic, Chinese) के साथ **PNG से टेक्स्ट पहचानें** का अन्वेषण करें `Language` फ़्लैग्स को संयोजित करके।  
* OCR परिणाम को Azure Cognitive Search के साथ एकीकृत करें ताकि खोज योग्य दस्तावेज़ अभिलेख बन सकें।  
* Aspose.OCR के `OcrEngine` सेटिंग्स जैसे `Resolution` के साथ प्रयोग करें

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [C# में Aspose.OCR मॉडल डाउनलोड करें और PNG से टेक्स्ट निकालें](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [C# में OCR कैसे करें – Aspose के साथ Cyrillic टेक्स्ट पहचानें](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [C# में बैच OCR कैसे करें – PNG फ़ाइलों से तेज़ी से टेक्स्ट निकालें](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}