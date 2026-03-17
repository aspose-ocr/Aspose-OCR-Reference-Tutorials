---
category: general
date: 2026-03-17
description: c# OCR ट्यूटोरियल – जानिए कैसे इमेज फ़ाइलों से टेक्स्ट निकालें, WebP
  फ़ोटो से टेक्स्ट पढ़ें, और एक सरल OcrEngine का उपयोग करके इमेज को टेक्स्ट में बदलें।
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: hi
og_description: c# OCR ट्यूटोरियल आपको दिखाता है कि कैसे इमेज फ़ाइलों से टेक्स्ट निकाला
  जाए, WebP फ़ोटो से टेक्स्ट पढ़ा जाए, और कुछ लाइनों के कोड से इमेज को टेक्स्ट में
  बदला जाए।
og_title: c# OCR ट्यूटोरियल – मिनटों में छवियों से टेक्स्ट निकालें
tags:
- C#
- OCR
- Image Processing
title: 'c# OCR ट्यूटोरियल: इमेज (WebP, फोटो) से टेक्स्ट निकालें – त्वरित गाइड'
url: /hi/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR ट्यूटोरियल – इमेज से टेक्स्ट निकालें (WebP, फोटो)

क्या आपको कभी **इमेज से टेक्स्ट निकालें** फ़ाइलों से टेक्स्ट निकालने की ज़रूरत पड़ी है लेकिन C# में कहाँ से शुरू करें, यह नहीं पता था? शायद आपके पास एक WebP स्क्रीनशॉट, रसीद की JPEG, या स्कैन किया हुआ PDF पेज है और आप सिर्फ अंदर के शब्द चाहते हैं। इस **c# OCR tutorial** में हम एक पूर्ण, तैयार‑चलाने‑योग्य उदाहरण के माध्यम से चलेंगे जो फोटो से टेक्स्ट पढ़ता है, WebP और अन्य आधुनिक फ़ॉर्मेट को संभालता है, और इमेज को साधारण टेक्स्ट में बदलता है—सिर्फ कुछ लाइनों में।

**क्या फ़ायदा है?** आप किसी भी टेक्स्ट वाली तस्वीर को सर्चेबल स्ट्रिंग्स में बदल सकेंगे, उन्हें डेटाबेस में डाल सकेंगे, या डाउनस्ट्रीम AI पाइपलाइन में फीड कर सकेंगे। कोई जादू नहीं, बस एक ठोस OCR इंजन, कुछ .NET APIs, और प्रत्येक चरण के “क्यों” की स्पष्ट व्याख्याएँ।

## आपको क्या चाहिए

- **.NET 6 SDK** (या बाद का)। नीचे दिया गया कोड .NET 6+ पर कंपाइल होता है और Windows, Linux, या macOS पर चलता है।
- **Visual Studio 2022** या कोई भी एडिटर जो आप पसंद करते हैं (VS Code भी ठीक काम करता है)।
- **`Microsoft.Windows.SDK.Contracts`** NuGet पैकेज (`Windows.Media.Ocr` प्रदान करता है)। इंस्टॉल करें:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- वह इमेज फ़ाइल जिसे आप प्रोसेस करना चाहते हैं – इस ट्यूटोरियल के लिए हम एक **WebP** फोटो जिसका नाम `photo.webp` है, `YOUR_DIRECTORY` फ़ोल्डर में रखेंगे।

> प्रो टिप: यदि आप गैर‑Windows प्लेटफ़ॉर्म पर हैं, तो आप `OcrEngine` को **Tesseract** जैसी क्रॉस‑प्लेटफ़ॉर्म लाइब्रेरी से बदल सकते हैं। आसपास का कोड लगभग वही रहता है।

## चरण 1: C# OCR ट्यूटोरियल प्रोजेक्ट सेट अप करें

सबसे पहले, एक नया कंसोल ऐप बनाएं। टर्मिनल खोलें और चलाएँ:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

आवश्यक पैकेज जोड़ें (जैसा ऊपर दिखाया गया है) और अपने IDE में प्रोजेक्ट खोलें। यह स्कैफ़ोल्डिंग हमें **c# OCR tutorial** के लिए एक साफ़ शुरुआत देता है।

## चरण 2: नेमस्पेसेस इम्पोर्ट करें और इमेज तैयार करें

हमें कुछ `using` निर्देशों की जरूरत है ताकि कंपाइलर को पता चले कि `OcrEngine`, `SoftwareBitmap`, और इमेज‑लोडिंग हेल्पर्स कहाँ हैं।

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **इन नेमस्पेसेस की आवश्यकता क्यों?**  
> `Windows.Media.Ocr` में `OcrEngine` क्लास है जो वास्तविक पहचान करता है। `Windows.Graphics.Imaging` हमें इमेज (WebP सहित) को `SoftwareBitmap` में डिकोड करने देता है जिसे इंजन समझता है। `System.IO` और `Windows.Storage.Streams` हेल्पर्स फ़ाइल लोडिंग को आसान बनाते हैं।

अब, इमेज लोड करें। बिल्ट‑इन डिकोडर WebP, HEIF, PNG, JPEG, और अधिक को संभाल सकता है, इसलिए आप **WebP से टेक्स्ट पढ़ सकते हैं** बिना अतिरिक्त प्लगइन्स के।

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **एज केस:** यदि आपकी इमेज पहले से ही ब्लैक‑एंड‑व्हाइट है, तो आप कन्वर्ज़न स्टेप को स्किप कर सकते हैं। ग्रेस्केल कन्वर्ज़न एक छोटा प्रदर्शन लाभ है और अक्सर शोरयुक्त फ़ोटो पर पहचान को बेहतर बनाता है।

## चरण 3: OCR इंजन चलाएँ – फोटो से टेक्स्ट पहचानें

यह **c# OCR tutorial** का मुख्य भाग है। हम `OcrEngine` का एक इंस्टेंस बनाते हैं, उसे बिटमैप फीड करते हैं, और पहचाना गया टेक्स्ट निकालते हैं।

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**क्या हो रहा है?**  
- `TryCreateFromUserProfileLanguages()` आपके Windows यूज़र प्रोफ़ाइल में सेट भाषा(यों) को चुनता है, जो आमतौर पर अंग्रेज़ी, स्पेनिश आदि को कवर करता है। यदि आपको कोई विशिष्ट भाषा चाहिए, तो `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))` उपयोग करें।  
- `RecognizeAsync` बैकग्राउंड थ्रेड पर भारी काम करता है, और एक `OcrResult` लौटाता है जिसमें कच्चा स्ट्रिंग, शब्द बॉन्डिंग बॉक्स, और कॉन्फिडेंस स्कोर होते हैं।  
- अंत में, हम `ocrResult.Text` प्रिंट करते हैं, जिससे आपको **convert image to text** परिणाम मिलता है जिसे आप कहीं और पाइप कर सकते हैं।

## चरण 4: पूर्ण, चलाने योग्य उदाहरण

सब कुछ मिलाकर, यहाँ एक स्व-निहित प्रोग्राम है जिसे आप `Program.cs` में कॉपी‑पेस्ट कर सकते हैं। यह कंपाइल होता है, चलाता है, और `photo.webp` से निकाले गए टेक्स्ट को प्रिंट करता है।

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### अपेक्षित आउटपुट

यदि `photo.webp` में वाक्य “Hello, world! This is a test.” है तो आपको कुछ इस तरह दिखेगा:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

सटीक लाइन ब्रेक स्रोत इमेज के लेआउट पर निर्भर करते हैं, लेकिन **extract text from image** परिणाम हमेशा एक साधारण स्ट्रिंग होगा जिसे आप आगे मैनिपुलेट कर सकते हैं।

## सामान्य प्रश्न और एज केस

### क्या यह अन्य इमेज फ़ॉर्मेट्स के साथ काम करता है?

बिल्कुल। उपयोग किया गया डिकोडर (`BitmapDecoder`) JPEG, PNG, BMP, GIF, **WebP**, HEIF, और अधिक को ऑटो‑डिटेक्ट करता है। इसलिए आप **WebP से टेक्स्ट पढ़ सकते हैं**, JPEG, या यहाँ तक कि TIFF भी कोड बदले बिना।

### अगर OCR इंजन कम कॉन्फिडेंस रिटर्न करता है तो क्या करें?

आप `ocrResult.Lines` और प्रत्येक `OcrWord` के `ConfidenceScore` को देख सकते हैं। यदि स्कोर एक थ्रेशहोल्ड (जैसे 0.6) से नीचे है, तो विचार करें:

- इमेज का प्री‑प्रोसेसिंग (कॉन्ट्रास्ट बढ़ाएँ, शार्पन, डेस्क्यू)।
- उच्च‑रिज़ॉल्यूशन स्रोत इमेज का उपयोग।
- मल्टी‑लैंग्वेज सपोर्ट के लिए **Tesseract** जैसी समर्पित लाइब्रेरी पर स्विच करना।

### एक ही इमेज में कई भाषाओं को कैसे हैंडल करें?

प्रत्येक भाषा के लिए अलग `OcrEngine` इंस्टेंस बनाएं और उन्हें क्रमिक रूप से चलाएँ, या ऐसी लाइब्रेरी उपयोग करें जो मिश्रित‑भाषा डिटेक्शन को सपोर्ट करती हो। बिल्ट‑इन इंजन के लिए, आप एक `Language` ऑब्जेक्ट पास कर सकते हैं:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### क्या मैं इसे Linux/macOS पर चला सकता हूँ?

`Windows.Media.Ocr` API केवल Windows के लिए है। गैर‑Windows प्लेटफ़ॉर्म पर, OCR सेक्शन को **Tesseract** ( `Tesseract.Net.SDK` के माध्यम से) से बदलें। लोडिंग और प्री‑प्रोसेसिंग कोड समान रहता है, इसलिए इस **c# OCR tutorial** का बाकी हिस्सा अभी भी लागू होता है।

## बेहतर सटीकता के लिए प्रो टिप्स

- **Resize** बड़े इमेज को अधिकतम 2000 px पर सबसे लंबे साइड तक रीसाइज़ करें – OCR इंजन मध्यम आकार पर तेज़ काम करते हैं।  
- **Denoise** साधारण Gaussian ब्लर का उपयोग करके यदि फोटो ग्रेनी है।  
- **Deskew** बिटमैप को यदि टेक्स्ट पूरी तरह क्षैतिज नहीं है तो; `SoftwareBitmap` को `OcrEngine` में पास करने से पहले घुमा सकते हैं।  
- **Cache** `OcrEngine` इंस्टेंस को यदि आप बैच में कई इमेज प्रोसेस कर रहे हैं; बार‑बार बनाना ओवरहेड जोड़ता है।

## खोजने योग्य संबंधित विषय

- **Convert image to text** को **Tesseract** के साथ क्रॉस‑प्लेटफ़ॉर्म प्रोजेक्ट्स के लिए उपयोग करें।  
- **Extract text from PDF** को प्रत्येक पेज को पहले इमेज में रेंडर करके निकालें।  
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}