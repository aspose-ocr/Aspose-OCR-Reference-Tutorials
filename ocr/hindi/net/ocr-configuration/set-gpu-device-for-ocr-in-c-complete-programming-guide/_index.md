---
category: general
date: 2026-03-18
description: Aspose OCR में GPU डिवाइस सेट करके छवि से तेज़ी से टेक्स्ट निकालें। OCR
  के लिए छवि कैसे लोड करें, रसीद की छवि को पहचानें और सटीक परिणाम प्राप्त करें, यह
  सीखें।
draft: false
keywords:
- set GPU device
- extract text from image
- how to extract text
- load image for OCR
- recognize receipt image
language: hi
og_description: Aspose OCR में GPU डिवाइस सेट करें ताकि छवि से तेज़ी से टेक्स्ट निकाला
  जा सके। OCR के लिए छवि लोड करने और रसीद की छवि को पहचानने के लिए इस चरण‑दर‑चरण गाइड
  का पालन करें।
og_title: C# में OCR के लिए GPU डिवाइस सेट करें – पूर्ण प्रोग्रामिंग गाइड
tags:
- OCR
- C#
- GPU
- Aspose
title: C# में OCR के लिए GPU डिवाइस सेट करें – पूर्ण प्रोग्रामिंग गाइड
url: /hi/net/ocr-configuration/set-gpu-device-for-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में OCR के लिए GPU डिवाइस सेट करें – पूर्ण प्रोग्रामिंग गाइड

तेज़ OCR प्रोसेसिंग के लिए **GPU डिवाइस सेट** करना है? इस गाइड में हम आपको बिल्कुल बताएंगे कि Aspose OCR का उपयोग करके GPU डिवाइस कैसे सेट करें, और फिर कुछ ही कोड लाइनों में रसीद की छवि से टेक्स्ट निकालें।  

यदि आप कभी **load image for OCR** करने में संघर्ष कर चुके हैं या यह सोच रहे हैं *कैसे टेक्स्ट निकाला जाए* हाई‑रेज़ॉल्यूशन स्कैन से, तो आप सही जगह पर हैं। अंत तक आपके पास एक चलाने योग्य प्रोग्राम होगा जो रसीद की छवि को पहचानता है, साधारण टेक्स्ट प्रिंट करता है, और यदि GPU उपलब्ध नहीं है तो सुगमता से CPU पर स्विच हो जाता है।

## इस ट्यूटोरियल में क्या कवर किया गया है

हम वह सब कवर करेंगे जिसकी आपको जरूरत है:

* Aspose OCR NuGet पैकेज को इंस्टॉल करना (एकमात्र बाहरी निर्भरता)।  
* GPU डिवाइस (`set GPU device`) सेट करना और वैकल्पिक रूप से अलग GPU इंडेक्स चुनना।  
* OCR के लिए इमेज फ़ाइल लोड करना – हाँ, वह “load image for OCR” स्टेप जो कई शुरुआती लोगों को फँसाता है।  
* पहचान इंजन को चलाकर **recognize receipt image** सामग्री को पहचानना।  
* प्राप्त स्ट्रिंग को निकालना ताकि आप **extract text from image** कर सकें और इसे अपने ऐप में उपयोग कर सकें।  

कोई जादू नहीं, कोई छिपे हुए डॉक लिंक नहीं – सिर्फ एक पूर्ण, स्व-निहित समाधान जिसे आप कॉपी‑पेस्ट करके Visual Studio में आज ही चला सकते हैं।

## पूर्वापेक्षाएँ

* .NET 6.0 या बाद का (कोड .NET Core और .NET Framework पर भी काम करता है)।  
* उपयुक्त ड्राइवरों के साथ GPU‑सक्षम मशीन – अन्यथा लाइब्रेरी स्वचालित रूप से CPU मोड में स्विच कर देगी।  
* एक नमूना रसीद इमेज (जैसे, `receipt_highres.png`) जिसे आप पूर्ण पाथ से रेफ़र कर सकें।  

बस इतना ही। यदि आपको NuGet पैकेज नहीं मिला, तो अपने प्रोजेक्ट फ़ोल्डर में `dotnet add package Aspose.OCR` चलाएँ।

---

## Step 1 – Aspose OCR में GPU डिवाइस सेट करें

पहला काम है OCR इंजन पर **GPU डिवाइस सेट** करना। यह Aspose को भारी काम ग्राफ़िक्स कार्ड पर ऑफ़लोड करने को बताता है, न कि CPU पर।

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // Enable GPU processing – this is where we set the GPU device
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu;

        // (Optional) Choose a specific GPU if you have more than one.
        // The default is device 0, but you can set it to 1, 2, etc.
        ocrEngine.Settings.GpuDeviceId = 0;
```

**यह क्यों महत्वपूर्ण है:**  
जब इंजन `ProcessingMode.Gpu` में चलता है, तो अंतर्निहित CUDA kernels कैरेक्टर सेगमेंटेशन और न्यूरल‑नेटवर्क इनफ़रेंस को नाटकीय रूप से तेज़ कर देते हैं। आधुनिक RTX 3080 पर आप OCR समय को सेकंड से सब‑सेकंड में घटते देखेंगे, विशेषकर हाई‑रेज़ॉल्यूशन रसीदों के लिए।

> **Pro tip:** यदि आप नहीं जानते कि कौन सा GPU इंडेक्स उपयोग करना है, तो `OcrEngine.GetAvailableGpuDevices()` (नए संस्करणों में उपलब्ध) को कॉल करें और सबसे अधिक फ्री मेमोरी वाला डिवाइस चुनें।

---

## Step 2 – OCR के लिए इमेज लोड करें

अब जब इंजन कॉन्फ़िगर हो गया है, हमें **load image for OCR** करना होगा। Aspose एक सुविधाजनक `ImageStream` रैपर प्रदान करता है जो फ़ाइल I/O को एब्स्ट्रैक्ट करता है और मेमोरी, नेटवर्क या डिस्क से स्ट्रीम को सपोर्ट करता है।

```csharp
        // Load the receipt image you want to recognize
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        var imageStream = ImageStream.FromFile(imagePath);
```

**क्या गलत हो सकता है?**  
यदि फ़ाइल पाथ गलत है या इमेज करप्ट है, तो `FromFile` `FileNotFoundException` फेंकेगा। `File.Exists(imagePath)` की जल्दी जाँच करने से आप एक बुरी क्रैश से बच सकते हैं।

---

## Step 3 – रसीद इमेज को पहचानें

इमेज हाथ में होने पर, हम `Recognize` को कॉल करते हैं। यही वह स्टेप है जो वास्तव में **recognize receipt image** सामग्री को GPU‑त्वरित पाइपलाइन के साथ पहचानता है जिसे हमने पहले सेट किया था।

```csharp
        // Perform OCR – this returns an OcrResult object
        var ocrResult = ocrEngine.Recognize(imageStream);
```

**पर्दे के पीछे:**  
इंजन पहले इमेज को एक नॉर्मलाइज़्ड ग्रेस्केल बिटमैप में बदलता है, फिर एक डीप‑लर्निंग मॉडल चलाता है जो कैरेक्टर प्रॉबेबिलिटी की भविष्यवाणी करता है। क्योंकि हम GPU पर हैं, मॉडल पूरे बिटमैप को पैरलल में प्रोसेस करता है, इसलिए बड़े रसीदों का प्रोसेसिंग जल्दी हो जाता है।

---

## Step 4 – इमेज से टेक्स्ट निकालें और आउटपुट वेरिफ़ाई करें

अंत में, हम `OcrResult` से साधारण‑टेक्स्ट परिणाम निकालते हैं और उसे कंसोल में लिखते हैं। यही वह क्षण है जब आप **extract text from image** करते हैं और इसे डाउनस्ट्रीम लॉजिक (जैसे, लाइन आइटम पार्सिंग) में फीड कर सकते हैं।

```csharp
        // Output the recognized plain text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

**अपेक्षित आउटपुट:**  

```
=== OCR Result ===
Store Name
Date: 03/15/2026
Item A   $12.99
Item B   $5.49
Total    $18.48
==================
```

यदि टेक्स्ट गड़बड़ दिखे, तो दोबारा जाँचें कि इमेज हाई‑रेज़ॉल्यूशन है और GPU ड्राइवर अप‑टू‑डेट है। आप `ocrEngine.Settings.PreprocessMode` को टॉगल करके कम रोशनी वाली रसीदों के कंट्रास्ट को भी सुधार सकते हैं।

---

## Step 5 – CPU पर फ़ॉलबैक (एज केस हैंडलिंग)

क्या होगा अगर लक्ष्य मशीन में संगत GPU नहीं है? क्रैश होने की बजाय, आप स्थिति का पता लगा सकते हैं और CPU प्रोसेसिंग पर स्विच कर सकते हैं।

```csharp
        // Detect GPU availability – fallback if needed
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, falling back to CPU mode.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }
```

**यह क्यों शामिल करें?**  
CI पाइपलाइनों या क्लाउड कंटेनरों में अक्सर आप हेडलेस सर्वर पर बिना GPU के चलाते हैं। ग्रेसफ़ुल डिग्रेडेशन सुनिश्चित करता है कि वही कोड हर जगह काम करे।

---

## सामान्य समस्याएँ और व्यावहारिक टिप्स

| समस्या | कैसे बचें |
|---------|--------------|
| `ProcessingMode` सेट करने से पहले इमेज लोड करना भूल जाना। | हमेशा पहले इंजन को कॉन्फ़िगर करें (Step 1)। |
| गलत GPU इंडेक्स (`GpuDeviceId`) उपयोग करना। | उपलब्ध डिवाइसों को क्वेरी करें या डिफ़ॉल्ट `0` रखें। |
| लो‑रेज़ॉल्यूशन इमेज लोड करना, जिससे OCR सटीकता घटे। | रसीदों के लिए कम से कम 300 DPI लक्ष्य रखें। |
| `ImageStream` को डिस्पोज़ न करना – फ़ाइल लॉक हो जाती है। | स्ट्रीम को `using` ब्लॉक में रखें या मैन्युअली `Dispose()` कॉल करें। |
| CUDA‑रहित मशीनों पर `IsGpuAvailable` फ़्लैग को अनदेखा करना। | Step 5 की फ़ॉलबैक लॉजिक जोड़ें। |

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम दिया गया है, जिसे आप सीधे कंपाइल कर सकते हैं। इसे `Program.cs` के रूप में सेव करें, Aspose OCR NuGet पैकेज जोड़ें, और चलाएँ।

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // ---------- Step 1: Set GPU device ----------
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu; // set GPU device
        ocrEngine.Settings.GpuDeviceId = 0; // use the first GPU (change if needed)

        // Optional: fallback if GPU isn't present
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, switching to CPU.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }

        // ---------- Step 2: Load image for OCR ----------
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }
        var imageStream = ImageStream.FromFile(imagePath);

        // ---------- Step 3: Recognize receipt image ----------
        var ocrResult = ocrEngine.Recognize(imageStream);

        // ---------- Step 4: Extract text from image ----------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

प्रोग्राम चलाने पर कंसोल में निकाला गया रसीद टेक्स्ट प्रिंट होगा, बिल्कुल पहले दिखाए गए जैसा। अब आप इस स्ट्रिंग को किसी पार्सर, डेटाबेस, या किसी भी अन्य बिज़नेस लॉजिक में पाइप कर सकते हैं जिसकी आपको ज़रूरत है।

---

## निष्कर्ष

हमने दिखाया कि कैसे Aspose OCR में **GPU डिवाइस सेट** करें, **OCR के लिए इमेज लोड** करें, और **recognize receipt image** करके **extract text from image** को तेज़ गति से किया जाए। पूर्ण, चलाने योग्य उदाहरण “कैसे” और “क्यों” दोनों को दर्शाता है, जिससे आप किसी भी C# OCR प्रोजेक्ट के लिए एक ठोस आधार प्राप्त कर सकते हैं जिसे GPU एक्सेलेरेशन की आवश्यकता है।

अगला कदम उठाने के लिए तैयार हैं? इन चीज़ों के साथ प्रयोग करें:

* `Parallel.ForEach` का उपयोग करके कई इमेज को समानांतर में प्रोसेस करना।  
* कम‑कॉन्ट्रास्ट स्कैन पर परिणाम सुधारने के लिए `ocrEngine.Settings.PreprocessMode` को ट्यून करना।  
* OCR आउटपुट को JSON में एक्सपोर्ट करके डाउनस्ट्रीम एनालिटिक्स के लिए उपयोग करना।  

यदि आपको कोई समस्या आती है तो टिप्पणी छोड़ें, और हैप्पी कोडिंग!

![Diagram showing how to set GPU device for OCR processing](set-gpu-device.png "set GPU device")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}