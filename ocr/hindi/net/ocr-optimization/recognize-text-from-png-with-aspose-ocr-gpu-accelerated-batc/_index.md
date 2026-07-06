---
category: general
date: 2026-04-01
description: Aspose OCR में GPU डिवाइस आईडी सेट करके और GPU एक्सेलेरेशन को सक्षम करके
  PNG फ़ाइलों से टेक्स्ट को तेज़ी से पहचानना सीखें। चरण‑दर‑चरण C# गाइड।
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: hi
og_description: GPU डिवाइस आईडी सेट करके PNG फ़ाइलों से तेज़ी से टेक्स्ट पहचानें।
  Aspose OCR के साथ GPU एक्सेलेरेशन सक्षम करने के लिए इस पूर्ण C# गाइड का पालन करें।
og_title: png से टेक्स्ट पहचानें – GPU‑त्वरित Aspose OCR ट्यूटोरियल
tags:
- C#
- OCR
- GPU
- Aspose
title: Aspose OCR के साथ PNG से टेक्स्ट पहचानें – GPU‑त्वरित बैच डेमो
url: /hi/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# png से टेक्स्ट पहचानें – पूर्ण C# GPU‑त्वरित बैच ट्यूटोरियल

क्या आपको कभी **png से टेक्स्ट पहचानने** की जरूरत पड़ी है लेकिन प्रक्रिया बहुत धीमी लगती है? आप अकेले नहीं हैं। अधिकांश डेवलपर्स एक सरल OCR कॉल से शुरू करते हैं, फिर कंसोल को देख कर आश्चर्यचकित होते हैं जो जैसे घोंघे की गति से चलता है जब किसी फ़ोल्डर में दर्जनों स्क्रीनशॉट होते हैं।  

अच्छी खबर? Aspose OCR आपके ग्राफ़िक्स कार्ड को भारी काम सौंप सकता है, और कुछ ही लाइनों के साथ आप **gpu device id सेट करें** ताकि आप इच्छित GPU चुन सकें। इस गाइड में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से चलेंगे जो फ़ोल्डर से सभी PNG फ़ाइलें लेता है, GPU एक्सेलेरेशन चालू करता है, पहला GPU चुनता है, और प्रत्येक फ़ाइल के लिए कैरेक्टर काउंट प्रिंट करता है।

अंत तक आपके पास एक स्व-समाहित प्रोग्राम होगा जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं, और आप समझेंगे कि GPU को सक्षम करना क्यों महत्वपूर्ण है, किन किन किनारे मामलों (edge cases) को कैसे संभालना है, और बेहतर प्रदर्शन के लिए क्या समायोजित करना चाहिए।

## What You’ll Need

- **.NET 6.0** या बाद का संस्करण (कोड .NET Core के साथ भी कम्पाइल होता है)।  
- **Aspose.OCR** NuGet पैकेज – इसे `dotnet add package Aspose.OCR` कमांड से इंस्टॉल करें।  
- एक मशीन जिसमें CUDA‑संगत GPU हो (आमतौर पर NVIDIA) और उपयुक्त ड्राइवर स्थापित हो।  
- उन **PNG** इमेजों की एक फ़ोल्डर जिसे आप प्रोसेस करना चाहते हैं।  

यदि इनमें से कोई भी चीज़ अपरिचित लगती है, तो घबराएँ नहीं। नीचे दिए गए चरणों में आपको आवश्यक सभी कमांड मिलेंगे, और हम यह भी चर्चा करेंगे कि जब GPU उपलब्ध न हो तो क्या करना है।

## Step 1: Initialise the OCR Engine and Enable GPU Acceleration  

पहला काम है `OcrEngine` इंस्टेंस बनाना और GPU सपोर्ट को ऑन करना। यह फ़्लैग Aspose को निचले स्तर पर नेटिव CUDA लाइब्रेरीज़ इस्तेमाल करने के लिए बताता है।

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**क्यों महत्वपूर्ण है:** `UseGpuAcceleration` के बिना प्रत्येक इमेज CPU पर प्रोसेस होती है, जो विशेषकर हाई‑रेज़ोल्यूशन PNG के लिए कई गुना धीमी हो सकती है। इस फ़्लैग को सक्षम करने से बाद में विशिष्ट GPU डिवाइस सेट करने की तैयारी भी होती है।

## Step 2: Set GPU Device ID (Optional but Recommended)  

यदि आपके workstation में एक से अधिक GPU हैं, तो आप तय कर सकते हैं कि कौन सा उपयोग करना है। डिवाइस ID  **0** से शुरू होती है, इसलिए `0` पहला GPU, `1` दूसरा GPU, आदि चुनता है।

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**प्रो टिप:** साझा सर्वर पर चलाते समय GPU डिवाइस ID को स्पष्ट रूप से सेट करने से आपका जॉब अन्य प्रक्रियाओं से संसाधन नहीं लेगा। यदि आप यह लाइन छोड़ देते हैं, तो Aspose डिफ़ॉल्ट डिवाइस ले लेगा, जो आमतौर पर सिंगल‑GPU सेटअप के लिए ठीक रहता है।

## Step 3: Gather All PNG Files from Your Batch Folder  

अब हमें उन सभी PNG फ़ाइलों को ढूँढ़ना है जिन पर OCR चलाना है। `Directory.GetFiles` मेथड इस काम को संभालता है।

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**एज केस:** यदि फ़ोल्डर खाली है, तो `imageFiles` एक खाली एरे होगा। हम बाद में इसे एक दोस्ताना संदेश के साथ हैंडल करेंगे।

## Step 4: Process Each Image and Output the Recognised Character Count  

अब मुख्य लूप। प्रत्येक PNG के लिए हम `Recognize` कॉल करते हैं, फिर फ़ाइल नाम और निकाले गए टेक्स्ट की लंबाई प्रिंट करते हैं।

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**आपको क्या दिखेगा:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

यदि किसी इमेज में कोई टेक्स्ट नहीं है, तो काउंट `0` होगा। यह पूरी तरह सामान्य है उन स्क्रीनशॉट्स के लिए जो केवल ग्राफ़िकल होते हैं।

## Step 5: Run the Program and Verify GPU Usage  

फ़ाइल को कम्पाइल करें (`dotnet build`) और चलाएँ (`dotnet run`)। जब कंसोल स्क्रॉल हो रहा हो, तो अपना GPU मॉनिटरिंग टूल (जैसे NVIDIA Smi) खोलें और देखें कि प्रत्येक इमेज के लिए GPU उपयोग में छोटी सी स्पाइक आती है या नहीं। यदि कोई एक्टिविटी नहीं दिख रही है, तो नीचे दिए बिंदुओं की दोबारा जाँच करें:

1. CUDA ड्राइवर इंस्टॉल है।  
2. `UseGpuAcceleration` को `true` सेट किया गया है।  
3. `GpuDeviceId` सही GPU से मेल खाता है।

यदि GPU उपलब्ध नहीं है, तो Aspose स्वचालित रूप से CPU पर फॉल्बैक कर देगा, लेकिन आप गति का लाभ खो देंगे।

## Common Variations & Tips  

| Situation | What to Change |
|-----------|----------------|
| **Different image format** (e.g., JPEG) | सर्च पैटर्न को `*.jpg` या `*.*` में बदलें और Aspose अभी भी टेक्स्ट पहचान लेगा। |
| **Batch size is huge** (thousands of files) | मेमोरी प्रेशर से बचने के लिए चंक्स में प्रोसेस करें: `imageFiles` को छोटे एरे में विभाजित करें। |
| **Need the actual text, not just length** | `WriteLine` में `ocrResult.Text.Length` को `ocrResult.Text` से बदलें। |
| **Running on a headless server** | सुनिश्चित करें कि सर्वर में GPU ड्राइवर हो; अन्यथा `UseGpuAcceleration = false` सेट करें ताकि अनावश्यक एरर न आएँ। |
| **Multiple GPUs, want to balance load** | `foreach` के अंदर `ocrEngine.GpuDeviceId = i % gpuCount` लूप लगाएँ ताकि डिवाइस रोटेट हो। |

## Expected Output & Verification  

जब सब कुछ सही ढंग से काम करता है, तो कंसोल प्रत्येक फ़ाइल नाम के बाद कैरेक्टर काउंट प्रिंट करेगा, जैसा कि पहले दिखाया गया था। वास्तविक OCR आउटपुट को दोबारा जांचने के लिए आप अस्थायी रूप से टेक्स्ट को डम्प कर सकते हैं:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

बस याद रखें कि बड़े बैच के लिए इस लाइन को हटाएँ या कमेंट कर दें; हजारों लाइनों को प्रिंट करने से आपका टर्मिनल भर सकता है।

## Full Working Example (Copy‑Paste Ready)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

इसे `GpuBatchDemo.cs` के रूप में सेव करें, `dotnet add package Aspose.OCR` चलाएँ, फिर `dotnet run` करें। आपको प्रत्येक PNG के लिए कैरेक्टर काउंट लगभग तुरंत दिखना चाहिए, GPU एक्सेलेरेशन के धन्यवाद।

## Conclusion  

अब आप जानते हैं कि **png से टेक्स्ट पहचानें** फ़ाइलों को GPU एक्सेलेरेशन सक्षम करके और Aspose OCR में **gpu device id सेट करके** कैसे कुशलता से प्रोसेस किया जाए। यह पूर्ण, कॉपी‑एंड‑पेस्ट प्रोग्राम फ़ोल्डर डिस्कवरी, एज‑केस चेक्स, और OCR प्रदर्शन पर तुरंत फीडबैक देता है।  

अगला कदम? यदि आपको नॉन‑ब्लॉकिंग प्रोसेसिंग चाहिए तो `Recognize` कॉल को `ocrEngine.RecognizeAsync` से बदलें, या Aspose द्वारा प्रदान किए गए विभिन्न इमेज प्री‑प्रोसेसिंग विकल्पों (जैसे बाइनराइज़ेशन) के साथ प्रयोग करें। आप OCR परिणामों को डेटाबेस या सर्च इंडेक्स में पाइप करके पूर्ण‑टेक्स्ट सर्च समाधान भी बना सकते हैं।

मल्टी‑पेज PDFs को हैंडल करने के बारे में सवाल हैं, या Aspose OCR को Tesseract से तुलना करना चाहते हैं? टिप्पणी छोड़ें या हमारे अन्य ट्यूटोरियल्स देखें **batch OCR C#**, **OCR performance tips**, और **GPU‑ड्रिवेन इमेज प्रोसेसिंग** पर। Happy coding!  

![Console output showing recognised character counts for PNG files – recognize text from png using GPU acceleration](image-placeholder.png "recognize text from png output example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}