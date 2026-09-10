---
category: general
date: 2026-01-13
description: C# में इमेज को डेस्क्यू कैसे करें और इमेज शोर हटाएँ – इमेज कंट्रास्ट
  बढ़ाना सीखें, इमेज OCR को प्रीप्रोसेस करें, और कई इमेज फ़िल्टर लागू करें।
draft: false
keywords:
- how to deskew image
- remove image noise
- increase image contrast
- preprocess image ocr
- multiple image filters
language: hi
og_description: C# में इमेज को डेस्क्यू कैसे करें और इमेज नॉइज़ हटाएँ – इमेज कंट्रास्ट
  बढ़ाना, इमेज OCR को प्रीप्रोसेस करना, और कई इमेज फ़िल्टर लागू करना सीखें।
og_title: इमेज को डेस्क्यू कैसे करें – OCR के लिए पूर्ण C# प्री‑प्रोसेसिंग गाइड
tags:
- OCR
- C#
- Image Processing
title: इमेज को डेस्क्यू कैसे करें – OCR के लिए पूर्ण C# प्री‑प्रोसेसिंग गाइड
url: /hi/net/skew-angle-calculation/how-to-deskew-image-complete-c-pre-processing-guide-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज को डेस्क्यू कैसे करें – OCR के लिए पूर्ण C# प्री‑प्रोसेसिंग गाइड

क्या आपने कभी **इमेज को डेस्क्यू** करने के बारे में सोचा है, इससे पहले कि आप उन्हें OCR इंजन को दें? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया परिदृश्यों में—स्कैन किए गए अनुबंध, रसीदें, या पुरानी फ़ोटोकॉपी—टेक्स्ट थोड़ा कोण पर रहता है, तस्वीर धुंधली दिखती है, और कंट्रास्ट असमान होता है। अच्छी खबर? कुछ ही पंक्तियों के C# कोड से आप उस झुकाव को सीधा कर सकते हैं, इमेज नॉइज़ हटाकर कंट्रास्ट बढ़ा सकते हैं, जिससे आपका OCR एक ठोस आधार प्राप्त करता है।

इस ट्यूटोरियल में हम एक **पूर्ण, चलाने योग्य उदाहरण** के माध्यम से दिखाएंगे कि इमेज को कैसे डेस्क्यू किया जाए, इमेज नॉइज़ कैसे हटाया जाए, इमेज कंट्रास्ट कैसे बढ़ाया जाए, और फिर Aspose.OCR के साथ OCR कैसे चलाया जाए। अंत तक आपके पास एक पुन: उपयोग योग्य पाइपलाइन होगी जो **एक ही, सहज कॉल** में **कई इमेज फ़िल्टर** लागू करती है—बिना किसी अनुमान के।

## आपको क्या चाहिए

- **.NET 6+** (या कोई भी नवीनतम .NET संस्करण; API समान काम करता है)
- **Aspose.OCR for .NET** NuGet पैकेज (`Aspose.OCR` और `Aspose.OCR.Filters`)
- एक नमूना स्कैन की गई इमेज (उदा., `skewed_noisy.png`) जिसमें झुकाव, नॉइज़ और कम कंट्रास्ट हो
- आपका पसंदीदा IDE (Visual Studio, Rider, VS Code—जो भी आपको आरामदायक लगे)

यदि आपका प्रोजेक्ट पहले से सेट है, तो बस NuGet रेफ़रेंस जोड़ें:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Filters
```

> **Pro tip:** Aspose एक मुफ्त ट्रायल प्रदान करता है जिसमें पेज काउंट सीमित है—नीचे दिए गए कोड को आज़माने के लिए एकदम सही।

## Step 1: Create the OCR Engine Instance

पहला कदम `OcrEngine` को इनिशियलाइज़ करना है। इसे वह दिमाग समझें जो बाद में टेक्स्ट पढ़ेगा। यहाँ कोई जटिल बात नहीं, लेकिन यह आगे के सभी कार्यों की नींव है।

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

> **Why this matters:** इंजन को एक बार इनिशियलाइज़ करके कई इमेज पर पुन: उपयोग करने से भाषा डेटा को बार‑बार लोड करने का ओवरहेड बचता है।

## Step 2: Load the Raw Scanned Image

अब हम डिस्क से इमेज लोड करेंगे। `OcrImage.FromFile` मेथड फ़ाइल को Aspose के प्रोसेस करने योग्य फ़ॉर्मेट में पढ़ता है।

```csharp
        // Step 2: Load the raw scanned image (skewed, noisy, low‑contrast)
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");
```

> **Edge case:** यदि आपकी इमेज गैर‑मानक फ़ॉर्मेट (TIFF, BMP) में है, तो भी Aspose इसे संभाल लेता है, लेकिन स्थिरता के लिए पहले PNG में कन्वर्ट करना बेहतर हो सकता है।

## Step 3: Build a Pre‑processing Pipeline (Deskew → Denoise → Contrast)

यहीं पर हम मुख्य प्रश्न **इमेज को डेस्क्यू कैसे करें** का उत्तर देते हैं, साथ ही **इमेज नॉइज़ हटाना** और **इमेज कंट्रास्ट बढ़ाना** भी। Aspose की फ़्लुएंट API हमें फ़िल्टर को चेन करने की सुविधा देती है, जिससे कोड एक वाक्य की तरह पढ़ा जाता है।

```csharp
        // Step 3: Apply Deskew, Denoise, and Contrast filters in one pipeline
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())      // Corrects rotation
            .ApplyFilter(new DenoiseFilter())     // Reduces grainy artifacts
            .ApplyFilter(new ContrastFilter());   // Boosts foreground/background separation
```

### What Each Filter Does

| फ़िल्टर | उद्देश्य | सामान्य प्रभाव |
|--------|----------|----------------|
| **DeskewFilter** | टेक्स्ट लाइनों का कोण पहचानता है और इमेज को घुमाकर उन्हें क्षैतिज बनाता है। | वह झुकाव हटाता है जो OCR को भ्रमित करता है, अक्सर त्रुटि दर को 30‑50 % तक घटाता है। |
| **DenoiseFilter** | एक स्मूदिंग एल्गोरिद्म लागू करता है जो किनारों को बरकरार रखता है जबकि रैंडम पिक्सेल नॉइज़ को हटाता है। | स्कैन की गई रसीदें या कम रोशनी वाली फ़ोटो को साफ़ करता है, जिससे अक्षर स्पष्ट होते हैं। |
| **ContrastFilter** | हिस्टोग्राम को स्ट्रेच करता है ताकि गहरे हिस्से और हल्के हिस्से अधिक स्पष्ट हों। | टेक्स्ट और बैकग्राउंड के बीच अंतर को बढ़ाता है, विशेष रूप से फेडेड दस्तावेज़ों के लिए उपयोगी। |

> **Why chain them?** पहले डेस्क्यू करने से डेनॉइज़र सही ओरिएंटेड इमेज पर काम करता है; अंत में कंट्रास्ट बढ़ाने से साफ़‑सुथरा टेक्स्ट OCR इंजन के लिए प्रमुख बन जाता है।

## Step 4: Perform OCR on the Processed Image

अब इमेज सीधी, साफ़ और हाई‑कंट्रास्ट हो गई है, हम इसे OCR इंजन को देते हैं। हम अंग्रेज़ी भाषा डेटा का उपयोग करेंगे, लेकिन Aspose 150 से अधिक भाषाओं को सपोर्ट करता है।

```csharp
        // Step 4: Recognize text using the English language pack
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);
```

यदि आपको कोई अन्य भाषा चाहिए, तो `OcrLanguage.English` को उपयुक्त enum वैल्यू (जैसे `OcrLanguage.Spanish`) से बदल दें।

## Step 5: Output the Recognized Text

अंत में हम परिणाम को कंसोल पर प्रिंट करेंगे। वास्तविक एप्लिकेशन में आप इसे फ़ाइल, डेटाबेस में लिख सकते हैं या आगे के NLP पाइपलाइन में फीड कर सकते हैं।

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Expected Output

पूरा प्रोग्राम चलाने पर एक सामान्य झुकी हुई रसीद के लिए आउटपुट कुछ इस प्रकार होगा:

```
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
Thank you for your business!
```

यदि आउटपुट गड़बड़ दिखे, तो मूल इमेज को दोबारा चेक करें—अत्यधिक ब्लर या बहुत अंधेरे क्षेत्रों को अतिरिक्त प्री‑प्रोसेसिंग (जैसे `SharpenFilter`) की आवश्यकता हो सकती है।

![how to deskew image example](images/deskewed_example.png "how to deskew image – before and after processing")

*ऊपर की इमेज बाएँ ओर मूल झुकी हुई स्कैन और दाएँ ओर सुधारी हुई, डेनॉइज़्ड, हाई‑कंट्रास्ट संस्करण दिखाती है।*

## Additional Tips & Common Pitfalls

### 1. When the Skew Angle Is Extreme

यदि दस्तावेज़ 30° से अधिक झुका हुआ है, तो `DeskewFilter` संघर्ष कर सकता है। ऐसे में इमेज को मैन्युअली प्री‑रोटेट करें:

```csharp
var manuallyRotated = rawImage.Rotate(45); // rotates 45 degrees clockwise
var processed = manuallyRotated.ApplyFilter(new DeskewFilter());
```

### 2. Handling Color Images

फ़िल्टर आंतरिक रूप से ग्रेस्केल पर काम करते हैं, लेकिन आप मजबूरन कन्वर्ज़न कर सकते हैं:

```csharp
var grayImage = rawImage.ConvertToGrayscale();
var processed = grayImage.ApplyFilter(new DeskewFilter());
```

### 3. Tuning the Denoise Strength

`DenoiseFilter` एक वैकल्पिक `strength` पैरामीटर (0‑100) लेता है। उच्च मान अधिक नॉइज़ हटाते हैं लेकिन बारीक विवरण धुंधला हो सकता है।

```csharp
.ApplyFilter(new DenoiseFilter(strength: 70))
```

### 4. Using Multiple Image Filters Beyond the Basics

Aspose कई अतिरिक्त फ़िल्टर प्रदान करता है: `SharpenFilter`, `BinarizeFilter`, `ResizeFilter` आदि। आप इन्हें मिलाकर अपनी विशिष्ट दस्तावेज़ प्रकार के अनुसार एक कस्टम पाइपलाइन बना सकते हैं।

```csharp
var processed = rawImage
    .ApplyFilter(new DeskewFilter())
    .ApplyFilter(new DenoiseFilter())
    .ApplyFilter(new BinarizeFilter())
    .ApplyFilter(new SharpenFilter());
```

## Full Working Example (Copy‑Paste Ready)

नीचे पूरा प्रोग्राम दिया गया है, जिसे आप सीधे एक कंसोल प्रोजेक्ट में पेस्ट कर सकते हैं।

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load the original scanned image
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // Build preprocessing pipeline: Deskew → Denoise → Contrast
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())
            .ApplyFilter(new DenoiseFilter())
            .ApplyFilter(new ContrastFilter());

        // Run OCR using English language
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);

        // Output recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

`dotnet run` कमांड से प्रोग्राम चलाएँ। यदि सब कुछ सही ढंग से सेट है, तो कंसोल में आपके मूल झुके, नॉइज़ वाले इमेज से निकाला गया साफ़, पठनीय टेक्स्ट प्रदर्शित होगा।

## Conclusion

हमने **इमेज को डेस्क्यू** करने, **इमेज नॉइज़ हटाने**, **इमेज कंट्रास्ट बढ़ाने**, और **एक श्रृंखला के कई इमेज फ़िल्टर** के साथ OCR प्री‑प्रोसेसिंग करने का पूरा तरीका कवर किया। मुख्य सीख यह है कि एक सुव्यवस्थित प्री‑प्रोसेसिंग पाइपलाइन OCR की सटीकता को नाटकीय रूप से बढ़ा सकती है—अक्सर एक मुश्किल से पढ़ी जाने वाली स्कैन को पूरी तरह पठनीय टेक्स्ट में बदल देती है।

अगला कदम? `ContrastFilter` को `BinarizeFilter` से बदलकर देखें कि बाइनरी (काली‑सफ़ेद) रूपांतरण आपके परिणामों को कैसे प्रभावित करता है, या `ResizeFilter` के साथ उच्च‑रिज़ॉल्यूशन इमेज को इंजन में फीड करें। चाहे आप कौन सा फ़िल्टर चुनें, वही पैटर्न लागू होता है, इसलिए आपके भविष्य के सभी OCR प्रोजेक्ट्स के लिए आपके पास एक लचीला आधार है।

PDF, मल्टी‑लैंग्वेज OCR, या इसे ASP.NET API में इंटीग्रेट करने के बारे में सवाल हैं? नीचे टिप्पणी करें, और कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}