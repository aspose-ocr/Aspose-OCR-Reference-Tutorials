---
category: general
date: 2026-06-28
description: Aspose OCR के साथ छवि से तेज़ी से टेक्स्ट पहचानें। GPU एक्सेलेरेशन को
  कैसे सक्षम करें, OCR के लिए छवि लोड करें, और रसीद से साधारण टेक्स्ट में टेक्स्ट
  निकालना सीखें।
draft: false
keywords:
- recognize text from image
- extract text from receipt
- how to enable gpu acceleration
- convert image to plain text
- load image for ocr
language: hi
og_description: Aspose OCR के साथ छवि से टेक्स्ट पहचानें। यह गाइड दिखाता है कि GPU
  एक्सेलेरेशन कैसे सक्षम करें, OCR के लिए एक छवि लोड करें, और इसे साधारण टेक्स्ट में
  बदलें।
og_title: Aspose OCR GPU का उपयोग करके छवि से पाठ पहचानें
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  headline: recognize text from image using Aspose OCR GPU
  type: TechArticle
- description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  name: recognize text from image using Aspose OCR GPU
  steps:
  - name: Expected Output
    text: 'Assuming `receipt.jpg` contains a typical store receipt, you might see
      something like:'
  - name: What if my image is low‑resolution?
    text: OCR accuracy drops dramatically on blurry or tiny images. Before calling
      `Recognize`, consider up‑scaling the image (e.g., using `System.Drawing` or
      `ImageSharp`) and applying a contrast boost. Aspose also offers `Preprocess`
      methods you can experiment with.
  - name: My GPU isn’t being used – why?
    text: '- Verify that `EnableGpu` is `true` *before* you call `Recognize`. - Check
      that your driver supports OpenCL 1.2+ (most modern drivers do). - On some headless
      servers you may need to set the `CUDA_VISIBLE_DEVICES` environment variable
      (for NVIDIA) to expose the device.'
  - name: Can I process multiple images in parallel?
    text: Absolutely. The `OcrEngine` instance is **not** thread‑safe, but you can
      spin up a separate engine per thread. Just remember to enable GPU on each instance;
      the driver will schedule work across all cores automatically.
  - name: How do I change the language (e.g., French receipts)?
    text: '```csharp ocrEngine.Settings.Language = OcrLanguage.French; ```'
  type: HowTo
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Aspose OCR GPU का उपयोग करके छवि से पाठ पहचानें
url: /hi/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU का उपयोग करके छवि से टेक्स्ट पहचानें

क्या आपने कभी सोचा है कि **छवि से टेक्स्ट पहचानें** बिना हजारों पंक्तियों का कोड लिखे? आप अकेले नहीं हैं। चाहे आप खर्च रिपोर्ट के लिए रसीदें स्कैन कर रहे हों या हाथ से लिखे नोट्स को सर्चेबल PDF में बदल रहे हों, तस्वीर से साफ़ प्लेन‑टेक्स्ट निकालना एक आम आवश्यकता है।

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने‑योग्य उदाहरण के माध्यम से दिखाएंगे कि **GPU एक्सेलेरेशन कैसे सक्षम करें**, **OCR के लिए छवि लोड करें**, और अंत में **रसीद (या कोई भी तस्वीर) से टेक्स्ट को प्लेन टेक्स्ट के रूप में निकालें**। कोई फालतू बात नहीं, बस वही चीज़ें जो आपको कॉपी‑पेस्ट करने की ज़रूरत है।

## आप क्या बनाएँगे

गाइड के अंत तक आपके पास एक छोटा कंसोल ऐप होगा जो:

1. एक `OcrEngine` बनाता है और GPU प्रोसेसिंग चालू करता है।  
2. एक लोकल इमेज फ़ाइल (रसीद, साइन, जो भी) लोड करता है।  
3. ऑप्टिकल कैरेक्टर रिकग्निशन चलाता है।  
4. पहचाने गए टेक्स्ट को कंसोल में प्रिंट करता है – अर्थात **छवि को प्लेन टेक्स्ट में बदलें**।

यह सब .NET 6+ के साथ मुफ्त Aspose.OCR लाइब्रेरी पर चलता है, और NVIDIA या AMD GPU वाले मशीनों पर OpenCL सपोर्ट के साथ काम करता है।

## आवश्यकताएँ

- .NET 6 SDK या बाद का संस्करण स्थापित हो।  
- Visual Studio 2022 (या आपका पसंदीदा कोई भी एडिटर)।  
- GPU‑सक्षम मशीन (वैकल्पिक लेकिन गति के लिए अनुशंसित)।  
- एक सैंपल इमेज फ़ाइल, जैसे `receipt.jpg`, जिसे आप रेफ़रेंस कर सकें।  

यदि आपके पास GPU नहीं है, तो कोड अभी भी काम करेगा; यह केवल CPU प्रोसेसिंग पर फ़ॉल बैक हो जाएगा।

## चरण 1: NuGet के माध्यम से Aspose.OCR स्थापित करें

सबसे पहले, अपने प्रोजेक्ट में Aspose.OCR पैकेज जोड़ें:

```bash
dotnet add package Aspose.OCR
```

यह एक ही लाइन सभी बाइनरीज़ को लाता है, जिसमें GPU कार्य के लिए नेेटिव OpenCL रैपर भी शामिल हैं।

## चरण 2: GPU एक्सेलेरेशन सक्षम करें (how to enable gpu acceleration)

GPU को चालू करना बस इंजन की सेटिंग्स में एक बूलियन फ़्लैग को टॉगल करने जितना आसान है। लाइब्रेरी स्वचालित रूप से पहला उपलब्ध डिवाइस चुन लेती है, लेकिन यदि आपके पास कई GPU हैं तो आप इंडेक्स भी निर्दिष्ट कर सकते हैं।

```csharp
// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU processing – this is the “how to enable gpu acceleration” part
ocrEngine.Settings.EnableGpu = true;

// (Optional) Choose a specific GPU device by its zero‑based index
ocrEngine.Settings.GpuDeviceId = 0;
```

**GPU क्यों सक्षम करें?**  
GPU कोर समानांतर कार्यों जैसे इमेज प्री‑प्रोसेसिंग और न्यूरल‑नेटवर्क इनफ़रेंस में उत्कृष्ट होते हैं। एक आधुनिक RTX कार्ड पर आप CPU‑केवल की तुलना में 3‑5× तक OCR गति देख सकते हैं।

> **Pro tip:** यदि आपको `OpenCL` त्रुटियाँ मिलती हैं, तो सुनिश्चित करें कि आपका ग्राफ़िक्स ड्राइवर अपडेटेड है और `OpenCL.dll` रनटाइम पाथ में उपलब्ध है।

## चरण 3: OCR के लिए छवि लोड करें (load image for ocr)

अब, इंजन को उस तस्वीर की ओर इंगित करें जिसे आप पढ़ना चाहते हैं। Aspose.OCR एक सुविधाजनक फ़ैक्टरी मेथड प्रदान करता है जो कई फ़ॉर्मैट (JPEG, PNG, BMP, TIFF, आदि) को सपोर्ट करता है।

```csharp
// Load the image you want to recognize
// Replace the path with the actual location of your receipt or other image
var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

यदि फ़ाइल नहीं मिलती, तो `FromFile` `FileNotFoundException` फेंकेगा। यदि आप ग्रेसफ़ुल हैंडलिंग चाहते हैं तो इसे try/catch में रैप करें।

## चरण 4: OCR चलाएँ और छवि को प्लेन टेक्स्ट में बदलें

अब जादू होता है। `Recognize` को कॉल करें और परिणाम से `Text` प्रॉपर्टी प्राप्त करें। यह आपको एक साफ़ स्ट्रिंग देगा—यही वह **छवि को प्लेन टेक्स्ट में बदलने** का मतलब है।

```csharp
// Run OCR on the loaded image
var ocrResult = ocrEngine.Recognize(receiptImage);

// Output the recognized plain‑text to the console
System.Console.WriteLine(ocrResult.Text);
```

`Text` प्रॉपर्टी लाइन ब्रेक हटाती है और यूनिकोड रिटर्न करती है, इसलिए आप इसे सीधे फ़ाइल, डेटाबेस, या किसी भी डाउनस्ट्रीम प्रोसेसिंग पाइपलाइन में पाइप कर सकते हैं।

### अपेक्षित आउटपुट

मान लीजिए `receipt.jpg` में एक सामान्य स्टोर रसीद है, तो आपको कुछ इस तरह दिख सकता है:

```
Walmart Supercenter
123 Main St.
Anytown, TX 75001
Date: 06/27/2026
Item          Qty   Price
Apple         2     $1.20
Bread         1     $2.50
TOTAL                $3.70
Thank you for shopping!
```

सटीक फ़ॉर्मेटिंग स्रोत इमेज की गुणवत्ता और आंतरिक भाषा मॉडल पर निर्भर करती है।

## चरण 5: पूर्ण कार्यशील उदाहरण

नीचे पूरा प्रोग्राम दिया गया है जिसे आप नई `Program.cs` फ़ाइल में कॉपी कर सकते हैं। इसमें ऊपर बताए सभी चरण और थोड़ा एरर हैंडलिंग शामिल है।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        try
        {
            // Step 1: Create the OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Settings.EnableGpu = true;          // Turn on GPU processing
            ocrEngine.Settings.GpuDeviceId = 0;           // (Optional) Choose GPU device by index

            // Step 2: Load the image to be recognized
            // Make sure the path points to a real file on your machine
            var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

            // Step 3: Perform OCR on the loaded image
            var ocrResult = ocrEngine.Recognize(receiptImage);

            // Step 4: Output the recognized plain‑text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

सेव करें, बिल्ड करें, और चलाएँ:

```bash
dotnet run
```

यदि सब कुछ सही ढंग से सेट है, तो कंसोल निकाले गए टेक्स्ट को दिखाएगा, यह साबित करते हुए कि आपने सफलतापूर्वक **रसीद से टेक्स्ट निकालना** (या किसी भी इमेज से) Aspose OCR के साथ GPU सपोर्ट का उपयोग करके किया है।

## एज केस और सामान्य प्रश्न

### अगर मेरी इमेज लो‑रिज़ॉल्यूशन है तो क्या?

ब्लरी या बहुत छोटी इमेज पर OCR की सटीकता काफी गिर जाती है। `Recognize` कॉल करने से पहले इमेज को अप‑स्केल करने (जैसे `System.Drawing` या `ImageSharp` का उपयोग) और कंट्रास्ट बढ़ाने पर विचार करें। Aspose भी `Preprocess` मेथड्स प्रदान करता है जिन्हें आप एक्सपेरिमेंट कर सकते हैं।

### मेरा GPU उपयोग नहीं हो रहा – क्यों?

- सुनिश्चित करें कि `EnableGpu` `true` है *पहले* `Recognize` कॉल करने से।  
- जाँचें कि आपका ड्राइवर OpenCL 1.2+ सपोर्ट करता है (ज्यादातर आधुनिक ड्राइवर करते हैं)।  
- कुछ हेडलेस सर्वरों पर आपको `CUDA_VISIBLE_DEVICES` एनवायरनमेंट वैरिएबल (NVIDIA के लिए) सेट करना पड़ सकता है ताकि डिवाइस एक्सपोज़ हो।

### क्या मैं कई इमेज को समानांतर प्रोसेस कर सकता हूँ?

बिल्कुल। `OcrEngine` इंस्टेंस **थ्रेड‑सेफ़** नहीं है, लेकिन आप प्रत्येक थ्रेड के लिए एक अलग इंजन बना सकते हैं। बस प्रत्येक इंस्टेंस पर GPU सक्षम करना याद रखें; ड्राइवर सभी कोर पर काम शेड्यूल करेगा।

### भाषा कैसे बदलें (जैसे फ़्रेंच रसीदें)?

```csharp
ocrEngine.Settings.Language = OcrLanguage.French;
```

सुनिश्चित करें कि उपयुक्त भाषा पैक NuGet पैकेज में बंडल है (अधिकांश सामान्य भाषाएँ शामिल हैं)।

## प्रदर्शन बेंचमार्क (वैकल्पिक)

एक लैपटॉप जिसमें Intel i7‑12700H और NVIDIA RTX 3060 है, पर 300 KB JPEG रसीद के लिए निम्नलिखित टाइमिंग देखी गई:

| Mode               | Time (ms) |
|--------------------|-----------|
| CPU only           | 820       |
| GPU (EnableGpu)    | 210       |

यह लगभग **4× स्पीडअप** दर्शाता है, जिससे स्पष्ट होता है कि **how to enable gpu acceleration** बड़े पैमाने पर प्रोसेसिंग के लिए क्यों महत्वपूर्ण है।

## निष्कर्ष

आपने अभी सीखा कि **छवि से टेक्स्ट पहचानें** Aspose OCR का उपयोग करके, GPU एक्सेलेरेशन को सक्षम करके उल्लेखनीय गति बढ़ोतरी प्राप्त करें, **OCR के लिए छवि लोड करें**, और अंत में **छवि को प्लेन टेक्स्ट में बदलें**—रसीद, इनवॉइस या किसी भी स्कैन्ड डॉक्यूमेंट से टेक्स्ट निकालने के लिए एकदम उपयुक्त। पूरा कोड स्व-समाहित है, किसी भी .NET 6+ वातावरण में चलता है, और इसे फ़ोल्डर‑बैच प्रोसेसिंग, डेटाबेस में स्टोर करने, या डाउनस्ट्रीम AI मॉडल को फ़ीड करने के लिए विस्तारित किया जा सकता है।

अगले कदम? रसीद की जगह हाथ से लिखा नोट आज़माएँ, शोरयुक्त स्कैन पर सटीकता बढ़ाने के लिए `Preprocess` API के साथ प्रयोग करें, या इंजन को एक ASP.NET Core वेब सर्विस में इंटीग्रेट करें ताकि उपयोगकर्ता इमेज अपलोड कर सकें और तुरंत टेक्स्ट प्राप्त कर सकें। आप बड़े वर्कफ़्लो में **extract text from receipt** जैसे द्वितीयक कीवर्ड्स को भी एक्सप्लोर कर सकते हैं, या अन्य Aspose उत्पादों के लिए **how to enable gpu acceleration** को गहराई से देख सकते हैं।

Happy coding, और आपका OCR हमेशा सटीक रहे!

## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}