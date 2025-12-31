---
category: general
date: 2025-12-30
description: बैच OCR प्रोसेसिंग और OCR टेक्स्ट एक्सट्रैक्शन के लिए Aspose OCR में
  GPU को कैसे सक्षम करें। GPU डिवाइस सेट करना और Aspose को प्रभावी ढंग से उपयोग करना
  सीखें।
draft: false
keywords:
- how to enable gpu
- batch ocr processing
- ocr text extraction
- set gpu device
- how to use aspose
language: hi
og_description: Aspose OCR में GPU को कैसे सक्षम करें। बैच OCR प्रोसेसिंग, OCR टेक्स्ट
  एक्सट्रैक्शन, GPU डिवाइस सेट करना और Aspose का उपयोग कैसे करें, इस गाइड का पालन
  करें।
og_title: Aspose OCR के लिए GPU कैसे सक्षम करें – पूर्ण ट्यूटोरियल
tags:
- Aspose
- OCR
- GPU
- C#
title: Aspose OCR के लिए GPU कैसे सक्षम करें – चरण‑दर‑चरण गाइड
url: /hi/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR के लिए GPU कैसे सक्षम करें – पूर्ण ट्यूटोरियल

क्या आप कभी सोचते थे कि Aspose OCR का उपयोग करते समय **GPU कैसे सक्षम करें**? आप अकेले नहीं हैं—बड़े दस्तावेज़ मात्रा को संभालने वाले डेवलपर्स अक्सर प्रदर्शन की बाधाओं का सामना करते हैं क्योंकि OCR इंजन CPU पर फँसा रहता है। अच्छी खबर? GPU एक्सेलेरेशन को चालू करना काफी सरल है, और यह प्रत्येक पृष्ठ से सेकंड घटा सकता है। इस गाइड में हम **GPU कैसे सक्षम करें**, **बैच OCR प्रोसेसिंग** चलाएंगे, पहचाने गए टेक्स्ट को निकालेंगे, और सही GPU डिवाइस भी चुनेंगे। अंत तक आप **Aspose का उपयोग कैसे करें** यह जान जाएंगे तेज़ OCR टेक्स्ट एक्सट्रैक्शन के लिए।

## इस ट्यूटोरियल में क्या कवर किया गया है

हम Aspose OCR लाइब्रेरी को सेटअप करके शुरू करेंगे, फिर GPU सपोर्ट को सक्षम करेंगे, और अंत में इंजन के माध्यम से TIFF इमेजों की एक बैच चलाएँगे। इस दौरान हम समझाएँगे कि आपको **GPU डिवाइस सेट** क्यों मैन्युअली करना पड़ सकता है, किन समस्याओं से बचना चाहिए, और यह कैसे सत्यापित करें कि टेक्स्ट एक्सट्रैक्शन वास्तव में काम किया। कोई बाहरी दस्तावेज़ नहीं, सिर्फ एक पूर्ण, कॉपी‑एंड‑पेस्ट समाधान जिसे आप आज ही चला सकते हैं।

> **Prerequisites**  
> - .NET 6.0 या बाद का (कोड आधुनिक C# सिंटैक्स का उपयोग करता है)  
> - Aspose.OCR for .NET NuGet पैकेज (वर्ज़न 23.10 या नया)  
> - उपयुक्त ड्राइवर स्थापित CUDA‑संगत GPU  
> - बैच रन के लिए कुछ नमूना `.tif` फ़ाइलों वाला फ़ोल्डर  

यदि आपके पास ये बुनियादी चीज़ें हैं, तो चलिए शुरू करते हैं।

## Aspose OCR में GPU कैसे सक्षम करें

पहले आपको `OcrEngine` को GPU उपयोग करने के लिए बताना होगा। यह दो सरल प्रॉपर्टीज़ के माध्यम से किया जाता है: `UseGpu` और वैकल्पिक रूप से `GpuDeviceId`। `UseGpu` को `true` सेट करने से इंजन GPU मोड में स्विच हो जाता है, जबकि `GpuDeviceId` आपको यह चुनने देता है कि कौन सा GPU (यदि आपके पास एक से अधिक हैं) भारी काम संभालेगा।

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **Why this matters** – CPU संस्करण प्रत्येक पिक्सेल को क्रमिक रूप से प्रोसेस करता है, जो हाई‑रिज़ॉल्यूशन इमेजों के लिए बॉटलनेक बन सकता है। GPU संस्करण हजारों थ्रेड्स को समानांतर चलाता है, जिससे प्रति पृष्ठ समय में नाटकीय कमी आती है।

### दृश्य अवलोकन  

![जब “GPU कैसे सक्षम करें” सेट किया जाता है तो OCR इंजन कैसे कार्य को GPU को सौंपता है इसका आरेख](/images/enable-gpu-diagram.png){: .center .responsive alt="GPU सक्षम करने का तरीका"}

*(यदि आप इमेज नहीं देख पा रहे हैं, तो बस एक फ्लोचार्ट की कल्पना करें जहाँ OCR इंजन इमेज बफ़र को CUDA कोर को सौंपता है।)*

## Aspose के साथ बैच OCR प्रोसेसिंग

अब जब इंजन GPU‑रेडी है, तो चलिए इसे फ़ाइलों की सूची देते हैं। बैच प्रोसेसिंग उतनी ही सरल है जितनी कि `List<string>` पर लूप करना जिसमें आपके इमेज पाथ्स हों। क्योंकि हम GPU का उपयोग कर रहे हैं, इंजन स्वचालित रूप से प्रत्येक इमेज को डिवाइस पर क्यू करेगा, जिससे पाइपलाइन व्यस्त रहेगी।

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **Pro tip** – वास्तव में बड़े बैचों के लिए, `Parallel.ForEach` को `ocrEngine.Clone()` के साथ उपयोग करने पर विचार करें ताकि थ्रेड‑सेफ़्टी समस्याओं से बचा जा सके। `Clone` मेथड इंजन की एक शैलो कॉपी बनाता है जो अभी भी उसी GPU कॉन्टेक्स्ट की ओर इशारा करती है।

### अपेक्षित आउटपुट

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

यदि संख्याएँ उचित दिखती हैं, तो आपका **बैच OCR प्रोसेसिंग** काम कर रहा है और GPU उपयोग में है।

## OCR टेक्स्ट एक्सट्रैक्शन – परिणाम प्राप्त करना

`Recognize` मेथड एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें कच्चा टेक्स्ट, कॉन्फिडेंस स्कोर, और यदि आवश्यक हो तो बाउंडिंग बॉक्स भी होते हैं। चलिए साधारण टेक्स्ट निकालते हैं और उसे फ़ाइल में लिखते हैं ताकि आप एक्सट्रैक्शन की पुष्टि कर सकें।

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **Why extract to a file?** – OCR टेक्स्ट को स्टोर करने से डाउनस्ट्रीम प्रोसेसिंग (सर्च इंडेक्सिंग, डेटा माइनिंग, आदि) बिना इंजन को फिर से चलाए संभव होती है। यह डिबगिंग के लिए एक स्थायी रिकॉर्ड भी प्रदान करता है।

## इष्टतम प्रदर्शन के लिए GPU डिवाइस सेट करें

यदि आपके वर्कस्टेशन में कई GPU हैं—उदाहरण के लिए, मशीन लर्निंग के लिए एक समर्पित RTX और एक इंटीग्रेटेड ग्राफ़िक्स कार्ड—तो आपको सुनिश्चित करना होगा कि आप सही डिवाइस को टारगेट कर रहे हैं। `GpuDeviceId` प्रॉपर्टी एक इंटीजर लेती है जो `CudaDeviceInfo.GetDevices()` द्वारा रिपोर्ट किए गए डिवाइस इंडेक्स से मेल खाता है।

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **Edge case** – कुछ पुराने GPU आवश्यक CUDA वर्ज़न को सपोर्ट नहीं करते। ऐसे में `UseGpu = true` silently CPU पर फ़ॉल्बैक हो जाएगा, इसलिए इनिशियलाइज़ेशन के बाद हमेशा `ocrEngine.IsGpuEnabled` चेक करें।

## वास्तविक‑दुनिया प्रोजेक्ट में Aspose OCR का उपयोग कैसे करें

सब कुछ एक साथ रखते हुए, यहाँ एक कॉम्पैक्ट, रीडी‑टू‑रन कंसोल एप्लिकेशन है जो **GPU कैसे सक्षम करें** को दर्शाता है, **बैच OCR प्रोसेसिंग** चलाता है, टेक्स्ट एक्सट्रैक्ट करता है, और आपको GPU डिवाइस चुनने देता है।

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### सैंपल चलाना

1. NuGet पैकेज इंस्टॉल करें: `dotnet add package Aspose.OCR --version 23.10.0`  
2. `imageFiles` में पाथ्स को अपने स्वयं के `.tif` फ़ाइलों के स्थान से बदलें।  
3. बिल्ड और रन करें: `dotnet run`।  

आपको GPU की सूची दिखाई देगी, उसके बाद प्रत्येक इमेज के लिए एक लाइन होगी जिसमें कैरेक्टर काउंट और जेनरेटेड `.txt` फ़ाइल का पाथ रिपोर्ट होगा।

## सामान्य प्रश्न और समस्याएँ

- **क्या यह केवल CPU वाले मशीन पर काम करता है?**  
  हाँ—यदि `UseGpu` `true` है लेकिन कोई संगत GPU नहीं मिला, तो Aspose CPU पर फ़ॉल्बैक कर देता है। आप `ocrEngine.IsGpuEnabled` के माध्यम से मोड की पुष्टि कर सकते हैं।

- **यदि मुझे “CUDA driver version is insufficient” त्रुटि मिलती है तो क्या करें?**  
  अपने NVIDIA ड्राइवर को नवीनतम वर्ज़न में अपडेट करें जो Aspose के साथ बंडल किए गए CUDA टूलकिट से मेल खाता हो। लाइब्रेरी को हालिया GPU फीचर्स के लिए कम से कम CUDA 11.0 चाहिए।

- **क्या मैं सीधे PDFs प्रोसेस कर सकता हूँ?**  
  Aspose OCR रास्टर इमेजों पर काम करता है। पहले PDF पेजों को इमेज में कनवर्ट करें (उदाहरण के लिए Aspose.PDF का उपयोग करके) और फिर उन्हें OCR इंजन को फीड करें।

- **शोरयुक्त स्कैन पर सटीकता कैसे बढ़ाएँ?**  
  `ocrEngine.Preprocess = true` जैसी प्री‑प्रोसेसिंग विकल्प सक्षम करें या उच्च‑रिज़ॉल्यूशन इमेज (300 dpi या अधिक) फीड करें। GPU एक्सेलेरेशन अभी भी लागू रहेगा।

## निष्कर्ष

हमने **GPU कैसे सक्षम करें** Aspose OCR के लिए कवर किया, **बैच OCR प्रोसेसिंग** को समझाया, **OCR टेक्स्ट एक्सट्रैक्शन** दिखाया, और इष्टतम प्रदर्शन के लिए **GPU डिवाइस सेट** करने का तरीका बताया। पूर्ण कोड सैंपल का पालन करके आप अब किसी भी .NET प्रोजेक्ट में तेज़, GPU‑पावर्ड OCR को इंटीग्रेट कर सकते हैं और “Aspose का उपयोग कैसे करें” सवाल का आत्मविश्वास के साथ जवाब दे सकते हैं।

अगले कदम के लिए तैयार हैं? भाषा डिटेक्शन जोड़ें, एक्सट्रैक्टेड टेक्स्ट को सर्च इंडेक्स में फीड करें, या बड़े दस्तावेज़ आर्काइव के लिए मल्टी‑GPU स्केलिंग के साथ प्रयोग करें। जब आप Aspose की मजबूत API को आधुनिक GPU की कच्ची शक्ति के साथ मिलाते हैं, तो आकाश ही सीमा है।

हैप्पी कोडिंग, और आपकी OCR जॉब्स उतनी ही तेज़ चलें जितनी आपका GPU संभाल सकता है!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}