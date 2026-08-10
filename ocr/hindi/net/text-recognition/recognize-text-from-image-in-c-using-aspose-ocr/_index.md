---
category: general
date: 2026-05-31
description: Aspose OCR के साथ C# में छवि से पाठ को पहचानना सीखें, जिसमें TIFF फ़ाइलों
  से पाठ निकालना और OCR के लिए छवि को कुशलतापूर्वक लोड करना शामिल है।
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: hi
og_description: Aspose OCR के साथ छवि से टेक्स्ट पहचानने के लिए चरण-दर-चरण गाइड, जिसमें
  TIFF से निष्कर्षण और OCR के लिए सही इमेज लोडिंग शामिल है।
og_title: C# में Aspose OCR का उपयोग करके छवि से टेक्स्ट पहचानें
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Aspose OCR का उपयोग करके C# में छवि से टेक्स्ट पहचानें
url: /hi/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Aspose OCR का उपयोग करके छवि से टेक्स्ट पहचानें

क्या आपको **छवि से टेक्स्ट पहचानने** की जरूरत पड़ी है लेकिन C# में कहाँ से शुरू करें, यह नहीं पता था? आप अकेले नहीं हैं—कई डेवलपर्स स्कैन किए गए दस्तावेज़ या मल्टी‑पेज TIFF के साथ काम करते समय इस समस्या का सामना करते हैं। इस गाइड में हम आपको एक पूर्ण, तैयार‑चलाने‑योग्य उदाहरण के माध्यम से ले जाएंगे जो Aspose OCR लाइब्रेरी का उपयोग करके **छवि से टेक्स्ट पहचानता** है, और साथ ही दिखाएंगे कि **tiff से टेक्स्ट निकालें** और **OCR के लिए छवि लोड करें** बिना सिरदर्द के।

हम NuGet पैकेज को इंस्टॉल करने से लेकर GPU एक्सेलेरेशन को हैंडल करने और आवश्यकता पड़ने पर CPU पर फॉल बैक करने तक सब कुछ कवर करेंगे। इस ट्यूटोरियल के अंत तक आपके पास एक कंसोल एप्लिकेशन होगा जो पहचाने गए टेक्स्ट और प्रोसेसिंग टाइम को प्रिंट करेगा—कोई अधूरी जानकारी नहीं, कोई अस्पष्ट रेफ़रेंस नहीं।

## आप क्या बनाएँगे

- एक साधारण .NET कंसोल एप्लिकेशन जो एक छवि (मल्टी‑पेज TIFF सहित) लोड करता है  
- एक OCR इंजन जो GPU उपयोग के लिए कॉन्फ़िगर किया गया है, साथ ही सुगम CPU फॉल‑बैक  
- छवि से साधारण टेक्स्ट का निष्कर्षण, कंसोल में प्रिंट किया गया  
- टाइमिंग जानकारी ताकि आप GPU बनाम CPU के प्रदर्शन प्रभाव को देख सकें  

**पूर्वापेक्षाएँ**

- .NET 6 SDK या बाद का संस्करण (कोड .NET Core और .NET Framework दोनों पर काम करता है)  
- C# और कमांड लाइन की बुनियादी समझ  
- Aspose.OCR NuGet पैकेज को डाउनलोड करने के लिए इंटरनेट एक्सेस  

यदि आपके पास ये हैं, तो चलिए शुरू करते हैं।

![Aspose OCR का उपयोग करके छवि से टेक्स्ट पहचानने के लिए C# कोड](image.png "Aspose OCR का उपयोग करके छवि से टेक्स्ट पहचानने के लिए C# कोड")

## चरण 1 – छवि से टेक्स्ट पहचानें: OCR इंजन सेट अप करें

सबसे पहले, हमें एक `OcrEngine` इंस्टेंस चाहिए। Aspose OCR आपको प्रोसेसिंग डिवाइस चुनने की अनुमति देता है—गति के लिए GPU, सुरक्षा के लिए CPU। इंजन एक मेमोरी‑लिमिट संकेत भी लेता है, जो साझा मशीनों पर उपयोगी हो सकता है।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**यह क्यों महत्वपूर्ण है:**  
`OcrDevice.Gpu` चुनने से बड़े चित्रों, विशेषकर मल्टी‑पेज TIFFs के लिए पहचान समय में सेकंड घट सकते हैं। `GpuMemoryLimit` आपके एप्लिकेशन को साझा वर्कस्टेशन पर सभी GPU मेमोरी हॉग करने से रोकता है।

## चरण 2 – OCR के लिए छवि लोड करें (TIFF समर्थन सहित)

अब हम इंजन को एक छवि देते हैं। Aspose का `ImageStream.FromFile` लाइब्रेरी द्वारा समर्थित **किसी भी** फॉर्मेट को स्वीकार करता है—TIFF, PNG, JPEG, जो भी आप चाहें। यह चरण सीधे **OCR के लिए छवि लोड करें** की आवश्यकता को पूरा करता है।

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**प्रो टिप:** यदि आप मल्टी‑पेज TIFF के साथ काम कर रहे हैं, तो Aspose स्वचालित रूप से प्रत्येक पेज को एक अलग फ्रेम के रूप में मानता है, और इंजन उन्हें क्रमशः प्रोसेस करेगा। अतिरिक्त कोड की आवश्यकता नहीं।

## चरण 3 – पहचान चलाएँ और **tiff से टेक्स्ट निकालें**

इंजन तैयार है और छवि लोड हो गई है, अब हम OCR ऑपरेशन शुरू करते हैं। `Recognize` मेथड एक `OcrResult` लौटाता है जिसमें साधारण टेक्स्ट, कॉन्फिडेंस स्कोर, और टाइमिंग विवरण होते हैं।

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**एज केस हैंडलिंग:**  
यदि GPU उपलब्ध नहीं है, तो भी `engine.Recognize()` काम करता है क्योंकि इंजन चुपचाप CPU पर स्विच कर देता है। आप पहचान के बाद `engine.Device` जांच सकते हैं यदि आपको लॉग करना हो कि वास्तव में कौन सा डिवाइस उपयोग हुआ।

## चरण 4 – पहचाने गए साधारण टेक्स्ट को प्राप्त करें

टेक्स्ट निकालना बहुत आसान है—सिर्फ `Text` प्रॉपर्टी पढ़ें। यही वह जगह है जहाँ हम अंततः **tiff से टेक्स्ट निकालते** हैं (या किसी अन्य छवि से) और उपयोगकर्ता को प्रस्तुत करते हैं।

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

आपको कच्चे अक्षर दिखेंगे, लाइन ब्रेक्स स्रोत छवि में जैसा है वैसा ही संरक्षित रहेगा। यदि आपको अधिक संरचित आउटपुट चाहिए (जैसे JSON या CSV), तो आप `result.Regions` और `result.Lines` में जा सकते हैं, लेकिन साधारण टेक्स्ट आमतौर पर त्वरित स्क्रिप्ट्स के लिए पर्याप्त होता है।

## चरण 5 – प्रोसेसिंग टाइम मापें और GPU फॉल‑बैक को हैंडल करें

परफ़ॉर्मेंस महत्वपूर्ण है, विशेषकर जब आप दर्जनों पेज प्रोसेस कर रहे हों। `ProcessingTime` प्रॉपर्टी आपको ठीक‑ठीक बताती है कि OCR को कितना समय लगा, चाहे वह GPU पर चला हो या CPU पर।

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**आपको क्यों परवाह करनी चाहिए:**  
यदि आप समय में वृद्धि देखते हैं, तो आप `GpuMemoryLimit` को ट्यून कर सकते हैं या स्पष्ट रूप से CPU पर स्विच कर सकते हैं (`Device = OcrDevice.Cpu`)। दूसरी ओर, बड़े TIFF पर सब‑सेकंड परिणाम दर्शाता है कि आपका GPU एक्सेलेरेशन सही काम कर रहा है।

## पूर्ण, तैयार‑चलाने‑योग्य उदाहरण

नीचे दिया गया कोड एक नए कंसोल प्रोजेक्ट (`dotnet new console -n OcrDemo`) में कॉपी करें और `dotnet add package Aspose.OCR` चलाएँ। फिर `YOUR_DIRECTORY/sample_multi_page.tif` को अपनी छवि के पाथ से बदलें।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**अपेक्षित आउटपुट (संक्षिप्त रूप में):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

यदि आपके मशीन में सक्षम GPU नहीं है, तो_elapsed time_ कुछ सेकंड अधिक हो सकता है, लेकिन टेक्स्ट फिर भी सही ढंग से निकाला जाएगा।

## सामान्य प्रश्न और ट्रिकें

- **यदि छवि बहुत बड़ी है (10 MB से अधिक)?**  
  इसे इंजन को देने से पहले रेज़ोल्यूशन कम करें, या यदि आपके पास पर्याप्त VRAM है तो `GpuMemoryLimit` बढ़ाएँ।  
- **क्या मैं कई छवियों को लूप में प्रोसेस कर सकता हूँ?**  
  बिल्कुल। वही `OcrEngine` इंस्टेंस पुनः उपयोग करें और प्रत्येक इटरेशन में नया `ImageStream` असाइन करें।  
- **क्या मुझे कुछ डिस्पोज़ करना पड़ेगा?**  
  `OcrEngine` `IDisposable` को इम्प्लीमेंट करता है। GPU रिसोर्सेज़ को साफ़ रखने के लिए इसे `using` ब्लॉक में रैप करें।  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **अंग्रेज़ी के अलावा अन्य भाषाएँ?**  
  `engine.Language = OcrLanguage.Spanish` (या कोई भी समर्थित भाषा) को `Recognize()` कॉल से पहले सेट करें।  

## निष्कर्ष

अब आपके पास एक पूर्ण, एंड‑टू‑एंड समाधान है जो C# में Aspose OCR का उपयोग करके **छवि से टेक्स्ट पहचानता** है। ट्यूटोरियल ने दिखाया कि **OCR के लिए छवि लोड करें**, **tiff से टेक्स्ट निकालें**, और GPU फॉल‑बैक को सुगमता से हैंडल करते हुए परफ़ॉर्मेंस कैसे मापें।

अब आप आगे कर सकते हैं:

- विभिन्न छवि फॉर्मेट (BMP, PDF) के साथ प्रयोग करें और देखें कि Aspose उन्हें कैसे हैंडल करता है।  
- यदि आपको लेआउट‑अवेयर डेटा चाहिए तो `result.Regions` में बाउंडिंग‑बॉक्स डेटा देखें।  


## आगे क्या सीखें?

- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}