---
category: general
date: 2026-03-05
description: Aspose OCR के साथ C# में TIFF को टेक्स्ट में बदलें—स्कैन की गई इमेज फ़ाइलों
  से तेज़ी से टेक्स्ट निकालें और OCR प्रोसेसिंग के लिए C# में इमेज फ़ाइल कैसे लोड
  करें, सीखें।
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: hi
og_description: Aspose OCR का उपयोग करके C# में TIFF को टेक्स्ट में बदलें। स्कैन किए
  गए चित्रों से टेक्स्ट निकालने और इमेज फ़ाइलों को कुशलतापूर्वक लोड करने की पूरी कार्यप्रणाली
  सीखें।
og_title: C# में TIFF को टेक्स्ट में बदलें – स्कैन की गई छवि का टेक्स्ट निकालें
tags:
- OCR
- C#
- Aspose
title: C# में TIFF को टेक्स्ट में बदलें – स्कैन की गई छवि से टेक्स्ट निकालें
url: /hi/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में TIFF को टेक्स्ट में बदलें – स्कैन किए गए इमेज टेक्स्ट निकालें

क्या आपको **C# में TIFF को टेक्स्ट में बदलने** की जरूरत है? आप अकेले नहीं हैं जो मल्टी‑पेज स्कैन की गई इमेजेज़ से जूझ रहे हैं जो खोज योग्य स्ट्रिंग्स में बदलने से इनकार करती हैं।  
इस गाइड में हम एक पूर्ण, तैयार‑चलाने‑योग्य समाधान के माध्यम से चलेंगे जो एक TIFF फ़ाइल लेता है, उसे Aspose OCR को देता है, और साधारण टेक्स्ट आउटपुट करता है—कोई अतिरिक्त सेवाएँ नहीं, कोई छिपा जादू नहीं।

> **Pro tip:** यदि आप हाई‑रेज़ोल्यूशन स्कैन के साथ काम कर रहे हैं, तो GPU प्रोसेसिंग को सक्षम करने से प्रत्येक पेज पर सेकंड बच सकते हैं।

हम आपको दिखाएंगे कि कैसे **स्कैन की गई इमेज फ़ाइलों से टेक्स्ट निकालें** और OCR इंजन में **इमेज फ़ाइल C# में लोड करें** का सबसे अच्छा तरीका, ताकि आप इस लॉजिक को आज ही किसी भी .NET प्रोजेक्ट में एम्बेड कर सकें।

---

## आप क्या चाहिए

| आवश्यकता | कारण |
|-------------|--------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | आधुनिक रनटाइम, `Span<T>` और async I/O को सपोर्ट करता है |
| Aspose.OCR for .NET (NuGet package `Aspose.OCR`) | वह OCR इंजन जिसे हम उपयोग करेंगे |
| A valid Aspose OCR license file (`Aspose.OCR.lic`) | बिना इस के आप मूल्यांकन सीमाओं का सामना करेंगे |
| A TIFF file (single‑ or multi‑page) to test | उदाहरण के रूप में उपयोग किया गया: `scanned_multi_page.tif` |
| GPU with CUDA 11+ (optional) | `EngineMode = Gpu` होने पर पहचान तेज़ हो जाती है |

यदि आपके पास इनमें से कोई भी नहीं है, तो अभी NuGet पैकेज प्राप्त करें:

```bash
dotnet add package Aspose.OCR
```

---

## चरण 1: प्रोजेक्ट सेट अप करें और नेमस्पेसेस इम्पोर्ट करें

एक नया कंसोल एप्लिकेशन बनाएं (या कोड को मौजूदा प्रोजेक्ट में जोड़ें)। सबसे पहले हम उन क्लासेज़ को इम्पोर्ट करते हैं जिनकी हमें आवश्यकता होगी।

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Why this matters:** `Aspose.OCR.Image` को इम्पोर्ट करने से हमें `ImageStream` फ़ैक्टरी मिलती है, जो डिस्क या स्ट्रीम से सीधे TIFF फ़ाइलें पढ़ सकती है। इस चरण को छोड़ने से कंपाइल‑टाइम एरर होगा।

---

## चरण 2: OCR इंजन को इनिशियलाइज़ करें और प्रोसेसिंग मोड चुनें

OCR इंजन को किसी भी इमेज असाइन करने **से पहले** कॉन्फ़िगर करना आवश्यक है। यहाँ हम तय करते हैं कि CPU पर चलाना है या GPU का उपयोग करना है।

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*यदि आप ग्राफ़िक्स कार्ड के बिना हेडलेस सर्वर पर हैं, तो `Gpu` को `Cpu` या `Auto` में बदलें।*  
इंजन मोड मेमोरी एलोकेशन और गति को प्रभावित करता है; बड़े, हाई‑रेज़ोल्यूशन TIFFs पर GPU मोड 2‑3× तेज़ हो सकता है।

---

## चरण 3: अपना Aspose OCR लाइसेंस लागू करें

लाइसेंस के बिना चलाने से आपको कुछ पेज और वॉटरमार्क तक ही सीमित रखा जाता है। अपना लाइसेंस जल्दी लोड करें ताकि बाद की सभी ऑपरेशन्स बिना प्रतिबंध के हों।

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Common pitfall:** `SetLicense` को `Recognize()` के बाद रखने से इंजन उस कॉल के लिए ट्रायल मोड में वापस चला जाएगा।

---

## चरण 4: TIFF फ़ाइल लोड करें – सिंगल और मल्टी‑पेज इमेजेज़ को हैंडल करना

Aspose OCR बॉक्स से बाहर मल्टी‑पेज TIFFs पढ़ सकता है, लेकिन आपको सही स्ट्रीम फीड करनी होगी। यहाँ एक मजबूत पैटर्न है जो दोनों परिस्थितियों में काम करता है।

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### क्यों उपयोग करें `ImageStream.FromFile`?

- यह अंतर्निहित `FileStream` को एब्स्ट्रैक्ट करता है, और TIFF पेज एन्क्यूमरेशन को आंतरिक रूप से संभालता है।  
- यह `MemoryStream` के साथ भी काम करता है, इसलिए आप डेटाबेस या वेब API से इमेजेज़ लोड कर सकते हैं बिना फ़ाइल सिस्टम को छुए।

### किनारे का मामला: बहुत बड़े TIFFs

यदि आपका TIFF 200 MB से बड़ा है, तो मेमोरी एक्सेप्शन से बचने के लिए इसे पेज‑दर‑पेज लोड करने पर विचार करें:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## चरण 5: आउटपुट सत्यापित करें

जब आप प्रोग्राम चलाएंगे, तो आपको कुछ इस तरह दिखना चाहिए:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

यदि टेक्स्ट गड़बड़ दिखता है, तो दोबारा जांचें:

1. **Resolution** – OCR 300 dpi या उससे अधिक पर सबसे अच्छा काम करता है।  
2. **EngineMode** – यदि GPU ड्राइवर पुराना है तो `Cpu` में स्विच करें।  
3. **License** – सुनिश्चित करें कि लाइसेंस फ़ाइल पाथ सही है और फ़ाइल पढ़ी जा सकती है।

---

## अक्सर पूछे जाने वाले प्रश्न (FAQ)

### क्या यह अन्य इमेज फ़ॉर्मैट्स के साथ काम करता है?

बिल्कुल। `ImageStream.FromFile` JPEG, PNG, BMP, और यहां तक कि PDF (Aspose.PDF के माध्यम से) को सपोर्ट करता है। बस फ़ाइल एक्सटेंशन बदल दें।

### यदि मुझे डेटाबेस में संग्रहीत इमेजेज़ को प्रोसेस करना हो तो क्या करें?

BLOB को `MemoryStream` में पढ़ें और उसे `ImageStream.FromStream(memoryStream)` को पास करें। OCR इंजन इसे फ़ाइल‑आधारित स्ट्रीम की तरह ही ट्रीट करता है।

### क्या मैं इसे Linux पर चला सकता हूँ?

हाँ—Aspose OCR क्रॉस‑प्लेटफ़ॉर्म है। उचित .NET रनटाइम इंस्टॉल करें और सुनिश्चित करें कि GPU (यदि उपयोग किया गया) के लिए आवश्यक नेटिव लाइब्रेरी उपलब्ध हैं।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम है, कंपाइल करने के लिए तैयार। `YOUR_DIRECTORY` और लाइसेंस फ़ाइल पाथ को अपनी वास्तविक लोकेशन से बदलें।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

`Program.cs` के रूप में सहेजें, `dotnet run` चलाएँ, और टेक्स्ट देखें।

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}