---
category: general
date: 2026-10-11
description: Aspose.OCR के साथ C# में इमेज पर OCR कैसे करें, सीखें, जिसमें System.Drawing.Common
  को इंस्टॉल करना और JPG फ़ाइलों से टेक्स्ट निकालना शामिल है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: hi
lastmod: 2026-10-11
og_description: Aspose.OCR का उपयोग करके C# में छवि पर OCR करें। यह गाइड आपको दिखाता
  है कि System.Drawing.Common कैसे स्थापित करें, OCR के लिए एक छवि लोड करें, और JPG
  से टेक्स्ट निकालें।
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: C# में छवि पर OCR करें – चरण‑दर‑चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Aspose.OCR का उपयोग करके C# में इमेज पर OCR कैसे करें
url: /hi/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Aspose.OCR का उपयोग करके इमेज पर OCR कैसे करें

यदि आपको .NET एप्लिकेशन में **perform OCR on image** फ़ाइलों को प्रोसेस करना है, तो यह गाइड आपको एक पूर्ण समाधान दिखाता है। Aspose.OCR का उपयोग करके आप जल्दी से **recognize text from picture** फ़ाइलों जैसे JPG को पहचान सकते हैं और परिणाम को कंसोल विंडो में प्रदर्शित कर सकते हैं।

आप सीखेंगे कि:

* **install System.Drawing.Common package** – वह लाइब्रेरी जो `Image` क्लास प्रदान करती है,
* **load image for OCR** – JPEG या PNG को मेमोरी में पढ़ें,
* भाषा मॉडल को कॉन्फ़िगर करें,
* **perform OCR on image** और अंत में,
* **extract text from JPG** और इसे आउटपुट करें।

ये चरण .NET 6+ के लिए लिखे गए हैं, लेकिन ये .NET Framework 4.6.1 या बाद के संस्करणों के साथ भी काम करते हैं।

---

## आवश्यकताएँ

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | C# कंसोल ऐप के लिए रनटाइम प्रदान करता है। |
| Visual Studio 2022 (or any IDE) | NuGet पैकेज जोड़ना और प्रोग्राम चलाना आसान बनाता है। |
| Internet connection (first run only) | Aspose.OCR स्वचालित रूप से भाषा मॉड्यूल डाउनलोड करता है। |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | **extract text from JPG** को प्रदर्शित करने के लिए उपयोग किया जाता है। |

---

## चरण 1: Install System.Drawing.Common package स्थापित करें

`System.Drawing.Common` NuGet पैकेज `Image` क्लास प्रदान करता है जिसे आप **load image for OCR** करेंगे। पैकेज मैनेजर कंसोल खोलें और चलाएँ:

```powershell
Install-Package System.Drawing.Common
```

> **Pro tip:** यदि आप Linux/macOS पर प्लेटफ़ॉर्म‑विशिष्ट चेतावनियों का सामना करते हैं तो `net6.0-windows` को टार्गेट करें या प्रोजेक्ट फ़ाइल में `<UseWindowsForms>true</UseWindowsForms>` जोड़ें।

---

## चरण 2: Add the Aspose.OCR NuGet package जोड़ें

Aspose.OCR में OCR इंजन और भाषा मॉडल शामिल हैं। इसे इस प्रकार इंस्टॉल करें:

```powershell
Install-Package Aspose.OCR
```

पैकेज हल्का है; आवश्यक भाषा डेटा (जैसे Cyrillic) पहली बार जब आप `OcrEngine.Language` सेट करते हैं, तब डाउनलोड हो जाता है।

---

## चरण 3: How to load image for OCR

इमेज को लोड करना वह पहला ठोस कदम है जिसके बाद आप **perform OCR on image** कर सकते हैं। `Image.FromFile` मेथड GDI+ द्वारा समर्थित किसी भी फॉर्मेट को पढ़ता है, जिसमें JPG, PNG, BMP, और TIFF शामिल हैं।

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*यदि फ़ाइल मौजूद नहीं है, तो `FileNotFoundException` फेंका जाता है – उत्पादन कोड के लिए इस कॉल को try/catch ब्लॉक में रखें।*

---

## चरण 4: इंजन को कॉन्फ़िगर करें और **perform OCR on image**

एक `OcrEngine` इंस्टेंस बनाएं, भाषा मॉडल चुनें, लोड की गई इमेज असाइन करें, और `Recognize()` को कॉल करें।

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

`Recognize()` मेथड एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें निकाला गया टेक्स्ट, कॉन्फिडेंस स्कोर, और बाउंडिंग बॉक्स होते हैं। भाषा मॉड्यूल पहली बार उपयोग पर स्वचालित रूप से डाउनलोड हो जाता है, इसलिए अतिरिक्त फ़ाइलों की आवश्यकता नहीं है।

---

## चरण 5: **Extract text from JPG** और इसे प्रदर्शित करें

अब आप **recognize text from picture** कर सकते हैं और परिणाम आउटपुट कर सकते हैं। `OcrResult` की `Text` प्रॉपर्टी में साधारण स्ट्रिंग होती है।

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### अपेक्षित कंसोल आउटपुट

```
Recognized text:
Пример текста на кириллице
```

यदि स्रोत इमेज में अंग्रेज़ी टेक्स्ट है, तो आउटपुट वही अंग्रेज़ी वाक्य होगा जो आपने इमेज में रखा था।

---

## किनारे के मामलों और सर्वोत्तम‑प्रैक्टिस टिप्स

| Situation | Recommendation |
|-----------|----------------|
| **Large images ( > 5 MB )** | OCR से पहले इमेज को सबसे लंबे पक्ष पर ≤ 2000 px तक रीसेज़ करें ताकि मेमोरी उपयोग कम हो और गति बढ़े। |
| **Multiple languages in one picture** | `ocrEngine.AddLanguage(OcrLanguage.English)` को Cyrillic के अलावा कॉल करें, फिर `ocrEngine.Language = OcrLanguage.Multilingual` सेट करें। |
| **Low‑contrast scans** | इंजन को बिटमैप पास करने से पहले `System.Drawing.Graphics` से कंट्रास्ट बढ़ाएँ। |
| **Running on Linux/macOS** | `libgdiplus` नेटिव डिपेंडेंसी इंस्टॉल है यह सुनिश्चित करें (`sudo apt-get install -y libgdiplus`)। |
| **Repeated OCR calls** | एक ही `OcrEngine` इंस्टेंस को पुन: उपयोग करें और केवल `ocrEngine.Image` को बदलें ताकि मॉड्यूल को बार‑बार लोड करने से बचा जा सके। |

---

## पूर्ण, चलाने योग्य प्रोग्राम

नीचे पूरा कंसोल एप्लिकेशन दिया गया है जो सभी पिछले चरणों को सम्मिलित करता है। कोड को एक नए C# कंसोल प्रोजेक्ट में कॉपी करें, इमेज पाथ बदलें, और चलाएँ।

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Running the program** कंसोल में पहचाना गया स्ट्रिंग प्रिंट करता है, यह पुष्टि करता है कि आपने सफलतापूर्वक **performed OCR on image** और **extract text from JPG** किया है।

---

## निष्कर्ष

अब आप जानते हैं कि C# में Aspose.OCR का उपयोग करके **perform OCR on image** फ़ाइलों को कैसे किया जाता है, आवश्यक **System.Drawing.Common package** को इंस्टॉल करने से लेकर **load image for OCR**, उपयुक्त भाषा चुनने, और अंत में **extract text from JPG** करने तक। यह एंड‑टू‑एंड उदाहरण आपको अधिक उन्नत दस्तावेज़‑प्रोसेसिंग पाइपलाइन बनाने के लिए एक ठोस आधार देता है, जैसे कि चित्रों के फ़ोल्डर को बैच‑प्रोसेस करना या OCR को वेब API में इंटीग्रेट करना।

### आगे क्या?

* PDF में **recognize text from picture** को एक्सप्लोर करें, पहले प्रत्येक पेज को इमेज में बदलकर।
* `OcrEngine` की प्रॉपर्टीज़ `Resolution`, `Threshold`, और `MaxProcessingTime` के साथ प्रयोग करें ताकि शोरयुक्त स्कैन पर सटीकता को फाइन‑ट्यून किया जा सके।
* OCR आउटपुट को एक नेचुरल‑लैंग्वेज प्रोसेसिंग लाइब्रेरी के साथ मिलाकर निकाले गए कंटेंट को स्वचालित रूप से वर्गीकृत करें।

कोड को अन्य इमेज फॉर्मेट्स के लिए अनुकूलित करने, एरर हैंडलिंग जोड़ने, या बड़े एप्लिकेशन में इंटीग्रेट करने में संकोच न करें। हैप्पी कोडिंग!

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर करने में मदद करती हैं।

- [C# में इमेज से टेक्स्ट निकालें – पूर्ण Aspose OCR गाइड](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Aspose.OCR का उपयोग करके भाषा चयन के साथ C# में इमेज टेक्स्ट निकालें](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Aspose OCR का उपयोग करके स्ट्रीम से इमेज टेक्स्ट एक्सट्रैक्शन कैसे करें](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}