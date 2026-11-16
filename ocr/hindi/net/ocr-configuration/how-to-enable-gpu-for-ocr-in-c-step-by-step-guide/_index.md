---
category: general
date: 2026-04-04
description: Aspose OCR में GPU को जल्दी से कैसे सक्षम करें। छवि से टेक्स्ट निकालना,
  OCR के लिए छवि लोड करना और C# का उपयोग करके टेक्स्ट पहचानना सीखें।
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: hi
og_description: Aspose OCR में GPU को जल्दी से कैसे सक्षम करें। इस ट्यूटोरियल का पालन
  करके छवि से टेक्स्ट निकालें, OCR के लिए छवि लोड करें, और C# के साथ टेक्स्ट को पहचानें।
og_title: C# में OCR के लिए GPU कैसे सक्षम करें – पूर्ण गाइड
tags:
- Aspose OCR
- C#
- GPU acceleration
title: C# में OCR के लिए GPU कैसे सक्षम करें – चरण‑दर‑चरण गाइड
url: /hi/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to enable gpu for OCR in C# – Complete Walkthrough

क्या आपने कभी सोचा है **GPU को कैसे सक्षम करें** जब आप Aspose OCR का उपयोग कर रहे हों? शायद आप सैकड़ों रसीदों को प्रोसेस करते‑वक्त प्रदर्शन की बाधा से टकरा गए हैं, और CPU नहीं संभाल पा रहा है। अच्छी खबर यह है कि GPU एक्सेलेरेशन को चालू करना बहुत आसान है, और एक बार चालू हो जाने पर आप OCR इंजन को छवियों पर तेज़ी से काम करते देखेंगे।

इस ट्यूटोरियल में हम न केवल GPU स्विच को ऑन करेंगे, बल्कि आपको **OCR के लिए इमेज लोड करना**, **टेक्स्ट पहचानना**, और अंत में **इमेज से टेक्स्ट निकालना** एक साफ़ C# उदाहरण के साथ दिखाएंगे। अंत तक आपके पास एक तैयार‑चलाने‑योग्य प्रोग्राम होगा जो किसी भी समर्थित तस्वीर से प्लेन‑टेक्स्ट निकाल देगा—बिना किसी बाहरी सेवा के।

## What You’ll Need

- .NET 6+ (या .NET Framework 4.7.2 और बाद के संस्करण)।  
- Aspose.OCR for .NET, संस्करण 24.2.0 या नया (GPU फ़्लैग इस रिलीज़ में जोड़ा गया था)।  
- उपयुक्त ड्राइवरों के साथ GPU‑सक्षम मशीन (NVIDIA CUDA 11+ बहुत अच्छा काम करता है)।  
- वह इमेज फ़ाइल जिसे आप प्रोसेस करना चाहते हैं—जैसे स्कैन की हुई रसीद, फ़ोटो‑लेन इनवॉइस, या हाथ से लिखा नोट।

यदि आपके पास ये सब है, तो चलिए शुरू करते हैं।

## Step 1: How to enable gpu – Configure the OCR Engine

सबसे पहले आपको Aspose OCR को GPU उपयोग करने के लिए बताना होगा। यह `OcrEngine` इंस्टेंस पर `UseGpu` प्रॉपर्टी सेट करके किया जाता है। डिफ़ॉल्ट रूप से यह प्रॉपर्टी `false` रहती है, इसलिए हम इसे स्पष्ट रूप से `true` कर देते हैं।

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**क्यों महत्वपूर्ण है:** जब `UseGpu` `true` होता है, तो लाइब्रेरी भारी मैट्रिक्स गणनाओं को ग्राफ़िक्स प्रोसेसर को सौंप देती है। एक मध्यम RTX 3060 पर आप देखेंगे कि लेटेंसी कई सेकंड से घटकर एक सेकंड के अंश में बदल जाती है।

> **Pro tip:** यदि आप हेडलेस CI वातावरण में चलाते हैं, तो सुनिश्चित करें कि GPU ड्राइवर इंस्टॉल है और सर्विस अकाउंट को डिवाइस तक पहुँच की अनुमति है। अन्यथा इंजन चुपचाप CPU मोड पर वापस आ जाएगा।

## Step 2: Load Image for OCR – Point the Engine at Your File

अब हमें **OCR के लिए इमेज लोड** करनी है। Aspose OCR System.Drawing द्वारा समर्थित किसी भी इमेज फॉर्मेट (PNG, JPEG, BMP, TIFF, आदि) को स्वीकार करता है। `ImageStream.FromFile` हेल्पर फ़ाइल को आवश्यक स्ट्रीम ऑब्जेक्ट में रैप करता है।

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

यदि आप `byte[]` से लोड करना पसंद करते हैं (उदाहरण के लिए जब इमेज डेटाबेस से आती है), तो आप `ImageStream.FromBytes(byteArray)` का उपयोग कर सकते हैं—परिणाम वही रहेगा, सिर्फ स्रोत अलग होगा।

## Step 3: How to recognize text – Run the OCR Process

इंजन कॉन्फ़िगर हो गया और इमेज लोड हो गई, अब **टेक्स्ट पहचानने** का समय है। `Recognize` मेथड सभी भारी काम करता है और एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें प्लेन‑टेक्स्ट, कॉन्फिडेंस स्कोर, और यदि आप बाद में चाहें तो बाउंडिंग बॉक्स भी होते हैं।

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

आप `ocrEngine.Language = OcrLanguage.French;` सेट करके भाषा बदल सकते हैं, `Recognize()` कॉल करने से पहले। GPU एक्सेलेरेशन भाषा पैक चाहे जो भी हो, समान रूप से काम करता है।

## Step 4: How to extract text from image – Output the Result

अंत में हम **इमेज से टेक्स्ट निकालते** हैं `OcrResult` ऑब्जेक्ट की `Text` प्रॉपर्टी पढ़कर। डेमो के लिए हम इसे कंसोल में प्रिंट करेंगे, लेकिन आप इसे फ़ाइल, डेटाबेस में लिख सकते हैं, या किसी अन्य सर्विस में फीड कर सकते हैं।

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**Expected output** (आपका वास्तविक टेक्स्ट इमेज पर निर्भर करेगा):

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

यदि आपको रॉ कॉन्फिडेंस वैल्यू चाहिए, तो आप `ocrResult.Regions` पर इटरेट करके प्रत्येक `Region.Confidence` देख सकते हैं।

## Full Working Example – One File, Ready to Run

नीचे पूरा प्रोग्राम दिया गया है। इसे एक नए कंसोल प्रोजेक्ट में कॉपी‑पेस्ट करें, Aspose.OCR NuGet पैकेज रिस्टोर करें, और **F5** दबाएँ।

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Note:** `YOUR_DIRECTORY/receipt.jpg` को अपनी इमेज के वास्तविक पाथ से बदलें। यदि प्रोग्राम `FileNotFoundException` फेंके, तो पाथ और फ़ाइल परमिशन दोबारा चेक करें।

## Common Questions & Edge Cases

### What if the GPU isn’t detected?

Aspose OCR स्वचालित रूप से CPU मोड पर वापस आ जाएगा और एक वार्निंग लॉग करेगा। यह जानने के लिए कि कौन सा मोड एक्टिव है, `ocrEngine.IsGpuEnabled` को कंस्ट्रक्शन के बाद जांचें—यह `true` तभी लौटाता है जब GPU ड्राइवर सफलतापूर्वक लोड हो गया हो।

### Can I process multiple images in a loop?

बिल्कुल। बस `ocrEngine.Image = …` लाइन को `foreach (var file in files)` लूप के अंदर ले जाएँ। वही `OcrEngine` इंस्टेंस रखें; इसे पुनः‑उपयोग करने से GPU रिसोर्सेज़ को बार‑बार अलोकेट करने का ओवरहेड बचता है।

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### How do I handle non‑English languages?

`Recognize()` कॉल करने से पहले भाषा सेट करें:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

GPU एक्सेलेरेशन वही रहता है; केवल भाषा मॉडल बदलता है।

### What about large, high‑resolution photos?

यदि आपको मेमोरी‑ऑफ़‑एरर मिलती है, तो पहले इमेज को डाउनस्केल करें। Aspose OCR `ImageHelper.Resize` प्रदान करता है—बिना बहुत अधिक डिटेल खोए इमेज को छोटा करने का तेज़ तरीका।

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## Conclusion

हमने **GPU को कैसे सक्षम करें** Aspose OCR के लिए, **OCR के लिए इमेज लोड करना**, **टेक्स्ट पहचानना**, और **इमेज से टेक्स्ट निकालना** को एक संक्षिप्त, प्रोडक्शन‑रेडी C# प्रोग्राम के साथ दिखाया। `UseGpu` फ़्लैग को टॉगल करके आप स्पष्ट गति वृद्धि प्राप्त कर सकते हैं, विशेषकर जब आप रसीदों, इनवॉइसों या किसी भी हाई‑वॉल्यूम डॉक्यूमेंट स्ट्रीम को बैच में प्रोसेस कर रहे हों।

अगला कदम तैयार है? इस OCR पाइपलाइन को डेटाबेस के साथ जोड़ें ताकि निकाले गए रसीदों को स्टोर किया जा सके, या प्लेन‑टेक्स्ट को नेचुरल‑लैंग्वेज‑प्रोसेसिंग मॉडल में फीड करके खर्च़ों की कैटेगराइज़ेशन करें। आप `OcrResult.Regions` कलेक्शन का उपयोग करके बाउंडिंग‑बॉक्स कोऑर्डिनेट्स प्राप्त कर सकते हैं और मूल इमेज पर प्रत्येक शब्द को हाईलाइट करने वाला UI बना सकते हैं।

हैप्पी कोडिंग, और GPU एक्सेलेरेशन से मिलने वाली अतिरिक्त शक्ति का आनंद लें!

---

![how to enable gpu illustration](gpu-ocr-diagram.png "how to enable gpu illustration")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}