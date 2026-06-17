---
category: general
date: 2026-03-13
description: C# में OCR का उपयोग करके स्कैन से टेक्स्ट निकालना। Aspose OCR, GPU एक्सेलेरेशन
  और चरण‑दर‑चरण कोड के साथ TIFF को टेक्स्ट में बदलना सीखें।
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: hi
og_description: C# में OCR का उपयोग करके स्कैन से टेक्स्ट निकालने का तरीका। यह गाइड
  आपको Aspose OCR और GPU एक्सेलेरेशन के साथ TIFF को टेक्स्ट में बदलने का तरीका दिखाता
  है।
og_title: C# में OCR का उपयोग कैसे करें – स्कैन से तेज़ी से टेक्स्ट निकालें
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C# में OCR का उपयोग कैसे करें – स्कैन से तेज़ी से टेक्स्ट निकालें
url: /hi/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में OCR का उपयोग कैसे करें – स्कैन से तेज़ी से टेक्स्ट निकालें

क्या आप कभी सोचते थे **how to use OCR** को लेकर कि स्कैन किए गए TIFF फ़ाइलों के ढेर से पठनीय टेक्स्ट कैसे निकाला जाए? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में—जैसे इनवॉइस डिजिटाइज़ेशन, ऐतिहासिक दस्तावेज़ों का अभिलेखन, या बस PDFs को सर्चेबल बनाना—डेवलपर्स को **extract text from scans** करने का एक भरोसेमंद तरीका चाहिए बिना किसी परेशानी के।

अच्छी खबर? Aspose OCR और कुछ ही C# लाइनों के साथ आप TIFF को टेक्स्ट में सेकंडों में बदल सकते हैं, यहाँ तक कि एक साधारण वर्कस्टेशन पर भी। नीचे आपको एक पूर्ण, तैयार‑चलाने‑योग्य उदाहरण मिलेगा, साथ ही प्रत्येक चयन के पीछे की तर्कशक्ति ताकि आप इसे अपने वर्कफ़्लो में अनुकूलित कर सकें।

## आपको क्या चाहिए

Before we dive in, make sure you have the following on hand:

| आवश्यकता | क्यों महत्वपूर्ण है |
|--------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | Aspose OCR NuGet पैकेज आधुनिक .NET रनटाइम्स को टार्गेट करता है। |
| Visual Studio 2022 (or any IDE you like) | IntelliSense और आसान डिबगिंग प्रदान करता है। |
| एक CUDA‑संगत GPU और ड्राइवर (वैकल्पिक) | `ocrEngine.UseGpu = true` को सक्षम करता है जिससे बड़े बैचों में उल्लेखनीय गति वृद्धि मिलती है। |
| एक फ़ोल्डर जिसमें आप प्रोसेस करना चाहते हैं TIFF इमेजेज | यह ट्यूटोरियल `*.tif` फ़ाइलों का उपयोग करता है, लेकिन आप पैटर्न को बदल सकते हैं। |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | मुख्य लाइब्रेरी जो भारी काम करती है। |

यदि आप इनमें से कोई भी चीज़ नहीं रखते, अभी प्राप्त कर लें—बाद में पढ़ते‑समय किसी गायब डिपेंडेंसी से रुकना नहीं चाहेंगे।

## समाधान का अवलोकन

उच्च स्तर पर प्रोग्राम तीन चीज़ें करता है:

1. **एक OCR इंजन बनाएं** और वैकल्पिक रूप से GPU एक्सेलेरेशन चालू करें।  
2. **डायरेक्टरी में प्रत्येक TIFF फ़ाइल पर इटररेट करें**, पहचान चलाएँ, और प्राप्त plain‑text को कैप्चर करें।  
3. **टेक्स्ट लिखें** को मूल इमेज के बगल में `.txt` फ़ाइल में।

बस इतना ही। कोड जानबूझकर छोटा है, फिर भी यह स्पष्ट भाषा चयन, उचित रिसोर्स डिस्पोज़ल, और सबसे सामान्य एज केसों के लिए एरर हैंडलिंग जैसी बेस्ट प्रैक्टिसेज़ दिखाता है।

![C# में OCR का उपयोग कैसे करें उदाहरण](/images/how-to-use-ocr-csharp.png "C# में OCR का उपयोग करके स्कैन से टेक्स्ट निकालने का चित्रण")

## चरण 1: OCR इंजन को इनिशियलाइज़ करें (How to Use OCR)

पहली चीज़ जो आपको चाहिए वह है `OcrEngine` का एक इंस्टेंस। यह ऑब्जेक्ट Aspose OCR की सभी कार्यक्षमताओं का गेटवे है। डिफ़ॉल्ट रूप से यह CPU पर काम करता है, लेकिन `UseGpu = true` सेट करने से लाइब्रेरी भारी मैट्रिक्स गणनाओं को आपके ग्राफ़िक्स कार्ड पर ऑफ़लोड कर देती है—बशर्ते आपके पास CUDA‑संगत ड्राइवर इंस्टॉल हो।

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**क्यों यह महत्वपूर्ण है:**  
- **GPU acceleration** उच्च‑रिज़ॉल्यूशन स्कैन के लिए प्रोसेसिंग समय को 70 % तक कम कर सकता है।  
- **Explicit language selection** इंजन को अनुमान लगाने से रोकता है और सटीकता बढ़ाता है, विशेष रूप से गैर‑Latin स्क्रिप्ट्स के लिए।

## चरण 2: इंजन को अपने स्कैन की ओर निर्देशित करें (Convert TIFF to Text)

अब हम प्रोग्राम को बताते हैं कि इमेजेज़ कहाँ खोजनी हैं। `Directory.GetFiles` को `*.tif` फ़िल्टर के साथ उपयोग करने से लॉजिक सरल रहता है और `.jpg` या `.png` जैसी अनावश्यक फ़ाइलें नहीं आतीं।

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**एज केस नोट:** यदि डायरेक्टरी खाली है, तो नीचे का लूप कभी निष्पादित नहीं होगा, जो पूरी तरह ठीक है। बाद में आपको एक मैत्रीपूर्ण “No files found” संदेश दिखेगा।

## चरण 3: प्रत्येक TIFF फ़ाइल को प्रोसेस करें (Extract Text from Scans)

अब प्रोग्राम का दिल: प्रत्येक इमेज को लोड करना, OCR चलाना, और आउटपुट को सहेजना। `ImageStream.FromFile` हेल्पर फ़ाइल को सीधे मेमोरी में स्ट्रीम करता है, जो पहले `Bitmap` लोड करने की तुलना में अधिक कुशल है।

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**हम प्रत्येक इटरेशन को `try/catch` में क्यों रैप करते हैं:**  
डॉक्यूमेंट्स का बैच स्कैन करना गंदा काम है; एक ख़राब TIFF या मेमोरी‑ओवरफ़्लो पूरी रन को रोकना नहीं चाहिए। कैच ब्लॉक समस्या को लॉग करता है और आगे बढ़ता है, जिससे पाइपलाइन मजबूत रहती है।

### अपेक्षित आउटपुट

हर `example.tif` के लिए आपको एक सिब्लिंग `example.txt` मिलेगा जिसमें कुछ इस तरह का कंटेंट होगा:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

यदि OCR इंजन किसी लाइन को पढ़ नहीं पाता, तो वह बस एक खाली लाइन या गड़बड़ कैरेक्टर छोड़ देगा—कोई क्रैश नहीं होगा।

## चरण 4: सफाई और डिस्पोज करें (Best Practice)

`OcrEngine` `IDisposable` को इम्प्लीमेंट करता है, इसलिए काम खत्म होने पर नेटिव रिसोर्सेज़ को फ्री करना शिष्टाचार है। एक छोटे कंसोल ऐप में आप GC पर भरोसा कर सकते हैं, लेकिन स्पष्ट डिस्पोज़ल एक आदत है जिसे अपनाना चाहिए।

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम है जिसे आप एक नई Console App प्रोजेक्ट में पेस्ट कर सकते हैं। यह जैसा है वैसा ही कंपाइल हो जाएगा, बशर्ते आपने Aspose.OCR NuGet पैकेज जोड़ दिया हो।

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### त्वरित चेकलिस्ट

- **GPU flag** – यदि आपके पास CUDA ड्राइवर नहीं है तो इसे हटाएँ या `false` सेट करें।  
- **Language** – `Language.English` को किसी भी अन्य सपोर्टेड भाषा से बदलें।  
- **File pattern** – यदि आपके स्कैन किसी अन्य फॉर्मेट में हैं तो `"*.tif"` को `"*.png"` या `"*.*"` में बदलें।  

## सामान्य गड़बड़ियां और प्रो टिप्स (c# OCR ट्यूटोरियल)

| समस्या | कैसे बचें |
|---------|-----------------|
| **Out‑of‑memory errors** बड़े बैचों पर | फ़ाइलों को छोटे हिस्सों में प्रोसेस करें या हर 50 फ़ाइलों के बाद `GC.Collect()` कॉल करें (बहुत कम आवश्यक)। |
| **GPU not detected** लेकिन `UseGpu = true` | इंजन चुपचाप CPU पर वापस आ जाता है, लेकिन निर्माण के बाद आप `ocrEngine.IsGpuAvailable` जांच सकते हैं। |
| **Wrong language pack** गड़बड़ आउटपुट देता है | हमेशा `ocrEngine.Language` को स्पष्ट रूप से सेट करें; डिफ़ॉल्ट संभवतः `Language.Unknown` हो सकता है। |
| **File path contains Unicode characters** | `Path.GetFullPath` का उपयोग करके सामान्य बनाएं, या Windows पर यदि पाथ बहुत लंबा हो तो `@"\\?\"` प्रीफ़िक्स जोड़ें। |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}