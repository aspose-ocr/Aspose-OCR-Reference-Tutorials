---
category: general
date: 2026-02-09
description: C# में GPU एक्सेलेरेशन के साथ Aspose OCR का उपयोग कैसे करें। JPG से टेक्स्ट
  पहचानना सीखें, इमेज से टेक्स्ट निकालें, और केवल कुछ ही मिनटों में GPU सक्षम करें।
draft: false
keywords:
- how to use aspose
- recognize text from jpg
- extract text from image
- how to enable gpu
- how to set gpu
language: hi
og_description: C# में GPU के साथ Aspose OCR का उपयोग कैसे करें। यह गाइड आपको दिखाता
  है कि कैसे JPG से टेक्स्ट को पहचानें और GPU एक्सेलेरेशन का उपयोग करके इमेज से टेक्स्ट
  निकालें।
og_title: Aspose OCR को GPU के साथ कैसे उपयोग करें – पूर्ण प्रोग्रामिंग गाइड
tags:
- Aspose
- OCR
- C#
- GPU Acceleration
title: GPU के साथ Aspose OCR का उपयोग कैसे करें – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/net/ocr-optimization/how-to-use-aspose-ocr-with-gpu-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR को GPU के साथ कैसे उपयोग करें – पूर्ण प्रोग्रामिंग गाइड

क्या आपको कभी बड़ी मात्रा में स्कैन किए गए इनवॉइस को तुरंत प्रोसेस करना पड़ा, लेकिन CPU धीमा पड़ गया? यही वह आम समस्या है जब आप **Aspose का उपयोग कैसे करें** बड़े पैमाने पर OCR के लिए चाहते हैं। इस ट्यूटोरियल में हम आपको एक वास्तविक उदाहरण के माध्यम से दिखाएंगे कि **Aspose का उपयोग कैसे करें** JPG फ़ाइलों से टेक्स्ट पहचानने, इमेज से टेक्स्ट निकालने, और अपने GPU का अधिकतम लाभ उठाने के लिए।

इसे एक कॉफ़ी‑ब्रेक walkthrough की तरह समझें—कोई फालतू बात नहीं, सिर्फ वही कोड जो आप Visual Studio में कॉपी‑पेस्ट करके जादू देख सकते हैं। अंत तक आपके पास एक स्व-निहित C# कंसोल ऐप होगा जो किसी भी आधुनिक Windows मशीन पर NVIDIA या AMD GPU के साथ चल सकता है।

![GPU के साथ Aspose OCR का उपयोग कैसे करें](/images/aspose-gpu-example.png)

## आपको क्या चाहिए

- **.NET 6.0** (या बाद का) – कोड .NET 6 को टार्गेट करता है लेकिन .NET 5 और .NET Framework 4.8 के साथ छोटे बदलावों से काम करता है।  
- **Aspose.OCR for .NET** NuGet पैकेज – इसे `dotnet add package Aspose.OCR` के द्वारा इंस्टॉल करें।  
- एक **GPU‑सक्षम मशीन** – ट्यूटोरियल दिखाता है कि **GPU कैसे सक्षम करें** और **GPU कैसे सेट करें** मेमोरी लिमिट, लेकिन यदि कोई संगत GPU नहीं मिलता तो कोड स्वचालित रूप से CPU पर वापस आ जाएगा।  
- `invoice_01.jpg` जैसी इमेज को किसी फ़ोल्डर में रखें जिसे आप रेफ़र कर सकें।

ये सब है? बढ़िया, चलिए शुरू करते हैं।

## Aspose OCR को GPU के साथ कैसे उपयोग करें – प्रारंभिक सेटअप

सबसे पहले आपको OCR इंजन का एक इंस्टेंस बनाना होगा और उसे GPU उपयोग करने के लिए बताना होगा। यह कदम महत्वपूर्ण है क्योंकि बिना इस फ़्लैग के Aspose डिफ़ॉल्ट रूप से CPU प्रोसेसिंग करेगा, जिससे हमारे प्रदर्शन बूस्ट का मतलब ही नहीं रहता।

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 1: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the core of **how to use aspose** with a graphics card
ocrEngine.Configuration.UseGpu = true;

// Optional: limit GPU memory to avoid OOM on low‑end cards
ocrEngine.Configuration.GpuMemoryLimit = 1024; // in MB
```

**क्यों यह महत्वपूर्ण है:** GPU को सक्षम करने से भारी इमेज‑प्रोसेसिंग कर्नेल ग्राफ़िक्स प्रोसेसर पर चले जाते हैं, जो बड़े इमेज के लिए CPU से 10‑20× तेज़ हो सकते हैं। `GpuMemoryLimit` एक सुरक्षा वाल्व है; इसे 1024 MB पर सेट करना अधिकांश मिड‑रेंज कार्डों के लिए ठीक रहता है और ऐप को रिस्पॉन्सिव बनाता है।

> **प्रो टिप:** यदि आप ऐप को ऐसी मशीन पर चलाते हैं जिसमें संगत GPU नहीं है, तो Aspose स्वचालित रूप से CPU मोड में स्विच कर देगा और एक चेतावनी लॉग करेगा। कोई क्रैश नहीं, बस धीमी रन टाइम।

## JPG से टेक्स्ट पहचानें – इमेज लोड करना

अब जब इंजन तैयार है, हमें उसे एक इमेज देना होगा। उदाहरण में JPEG का उपयोग किया गया है क्योंकि **JPG से टेक्स्ट पहचानें** इनवॉइस, रसीद और पासपोर्ट जैसे मामलों में आम है।

```csharp
// Step 2: Load the JPEG image you want to process
// Replace the path with the location of your own image
var inputImage = ImageStream.FromFile(@"C:\OCR\Samples\invoice_01.jpg");

// Verify that the file exists (helps avoid a FileNotFoundException)
if (!System.IO.File.Exists(@"C:\OCR\Samples\invoice_01.jpg"))
{
    Console.WriteLine("Image file not found. Check the path and try again.");
    return;
}
```

**फ़ाइल की जाँच क्यों करें:** गायब फ़ाइल तेज़ डेमो में सबसे आम रन‑टाइम एरर का कारण होती है। इसे शुरुआती स्तर पर संभालने से ट्यूटोरियल शुरुआती‑मित्र बनता है।

## इमेज से टेक्स्ट निकालें – OCR इंजन चलाना

इमेज हाथ में होने पर अगला कदम OCR प्रक्रिया को चलाना है। यही वह जगह है जहाँ Aspose भारी काम करता है और एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें प्लेन टेक्स्ट, कॉन्फिडेंस स्कोर, और यदि आप बाद में चाहें तो बाउंडिंग बॉक्स भी होते हैं।

```csharp
// Step 3: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Step 4: Output the extracted plain‑text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.PlainText);
```

**आपको क्या दिखेगा:** कंसोल Aspose द्वारा पहचाने गए कच्चे अक्षर प्रिंट करेगा। एक साफ़ इनवॉइस के लिए आपको कुछ इस तरह मिल सकता है:

```
=== Extracted Text ===
Invoice #: 2023‑00123
Date: 02/08/2023
Total: $1,245.67
...
```

यदि आउटपुट गड़बड़ दिखे, तो संभवतः आपको इमेज क्वालिटी समायोजित करनी होगी या अतिरिक्त प्री‑प्रोसेसिंग विकल्प (जैसे, डेस्क्यू, बाइनराइज़ेशन) सक्षम करने होंगे। ये इस त्वरित गाइड के दायरे से बाहर हैं लेकिन Aspose की API रेफ़रेंस में दस्तावेज़ित हैं।

## GPU कैसे सक्षम करें – इंजन को कॉन्फ़िगर करना

यदि आप पहले कदम को छोड़ गए हैं तो आप सोच रहे होंगे **GPU कैसे सक्षम करें**। उत्तर सरल है: इंजन की कॉन्फ़िगरेशन ऑब्जेक्ट पर `UseGpu` फ़्लैग को टॉगल करें, जैसा कि पहले दिखाया गया था। नीचे एक संक्षिप्त स्निपेट है जिसे आप किसी भी मौजूदा प्रोजेक्ट में डाल सकते हैं:

```csharp
ocrEngine.Configuration.UseGpu = true;   // Enables GPU
```

पर्दे के पीछे, Aspose आपके हार्डवेयर से मेल खाने वाली नेटिव CUDA/OpenCL लाइब्रेरीज़ लोड करता है। यदि रन‑टाइम उन्हें नहीं ढूँढ पाता, तो यह एक चेतावनी लॉग करता है और CPU पर वापस आ जाता है। अधिकांश Windows सेटअप के लिए अतिरिक्त इंस्टॉलेशन चरणों की आवश्यकता नहीं होती।

## GPU कैसे सेट करें – मेमोरी उपयोग को फाइन‑ट्यून करना

कभी‑कभी कम‑शक्ति वाले GPU पर “out of memory” एरर मिल सकता है। यही वह जगह है जहाँ **GPU कैसे सेट करें** मेमोरी लिमिट काम आती है। प्रॉपर्टी `GpuMemoryLimit` एक इंटीजर लेती है जो मेगाबाइट में मेमोरी दर्शाती है।

```csharp
// Example: restrict GPU usage to 512 MB
ocrEngine.Configuration.GpuMemoryLimit = 512;
```

**कब समायोजित करें:** यदि आप कई इमेज को समानांतर में प्रोसेस कर रहे हैं, तो लिमिट को कम रखें ताकि कार्ड ओवरलोड न हो। इसके विपरीत, 8 GB VRAM वाले वर्कस्टेशन पर आप इसे सुरक्षित रूप से 4096 MB तक बढ़ा सकते हैं ताकि बैच प्रोसेसिंग तेज़ हो।

## पूर्ण, चलाने योग्य उदाहरण

नीचे पूरा प्रोग्राम दिया गया है जिसे आप नई कंसोल प्रोजेक्ट (`dotnet new console`) में कॉपी कर सकते हैं। इसमें हमने चर्चा किए सभी हिस्से और थोड़ा एरर हैंडलिंग शामिल है ताकि यह मजबूत बन सके।

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine and enable GPU
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.Configuration.UseGpu = true;            // how to enable gpu
        ocrEngine.Configuration.GpuMemoryLimit = 1024;   // how to set gpu

        // -------------------------------------------------
        // Step 2: Load the JPEG image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\OCR\Samples\invoice_01.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }

        var inputImage = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // Step 3: Run the OCR engine
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

**अपेक्षित आउटपुट:** `dotnet run` चलाने के बाद कंसोल `invoice_01.jpg` से निकाला गया कच्चा टेक्स्ट प्रिंट करेगा। यदि इमेज में स्पष्ट प्रिंटेड टेक्स्ट है, तो परिणाम मूल दस्तावेज़ के बहुत करीब होना चाहिए।

## सामान्य समस्याएँ और उनका समाधान

| समस्या | क्यों होता है | त्वरित समाधान |
|-------|----------------|-----------|
| **GPU नहीं मिला** | CUDA ड्राइवर गायब या असमर्थित GPU | नवीनतम NVIDIA/AMD ड्राइवर इंस्टॉल करें; `nvidia-smi` या समकक्ष से सत्यापित करें |
| **Out‑of‑memory एरर** | `GpuMemoryLimit` कार्ड के लिए बहुत अधिक | लिमिट को 512 MB या कम करें |
| **गड़बड़ आउटपुट** | कम‑रिज़ॉल्यूशन JPG या अत्यधिक कम्प्रेशन | उच्च‑गुणवत्ता की स्रोत इमेज उपयोग करें या `ocrEngine.Preprocessing.Deskew = true` सक्षम करें |
| **Null `ocrResult`** | इमेज स्ट्रीम लोड नहीं हुई | फ़ाइल पाथ दोबारा जाँचें और सुनिश्चित करें कि फ़ाइल लॉक नहीं है |

इन समस्याओं को पहले से हल करने से बाद में अजीब‑से‑स्टैक‑ट्रेस का पीछा करने से बचा जा सकता है।

## अगले कदम

अब जब आप **Aspose का उपयोग कैसे करें** तेज़ OCR के लिए समझ गए हैं, तो आप आगे देख सकते हैं:

- **बैच प्रोसेसिंग** – JPGs की डायरेक्टरी पर लूप चलाएँ और प्रत्येक परिणाम को `.txt` फ़ाइल में लिखें।  
- **स्ट्रक्चर्ड एक्सट्रैक्शन** – `ocrResult.Regions` का उपयोग करके बाउंडिंग बॉक्स प्राप्त करें और इनवॉइस नंबर जैसे विशिष्ट फ़ील्ड निकालें।  
- **हाइब्रिड CPU/GPU मोड** – छोटे इमेज के लिए CPU चलाएँ और बड़े फ़ाइलों के लिए केवल GPU पर स्विच करें ताकि गति और मेमोरी का संतुलन बना रहे।

इन सभी विस्तारों का आधार वही है जो आपने अभी सेट किया है, और ये आपके अगले ट्यूटोरियल एडवेंचर के लिए बेहतरीन विषय हैं।

---

*हैप्पी कोडिंग! यदि आपको कोई समस्या आती है, तो नीचे कमेंट छोड़ें या Aspose कम्युनिटी फ़ोरम में पिंग करें। GPU तैयार है—आइए OCR को बिजली की गति दें।*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}