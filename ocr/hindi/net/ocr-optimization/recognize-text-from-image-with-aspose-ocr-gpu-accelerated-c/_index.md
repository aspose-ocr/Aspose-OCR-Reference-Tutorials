---
category: general
date: 2026-01-13
description: Aspose OCR का उपयोग करके छवि से टेक्स्ट को पहचानना और रसीद से तेज़ी से
  टेक्स्ट निकालना सीखें। इसमें OCR के लिए छवि लोड करना और GPU डिवाइस आईडी सेट करने
  के चरण शामिल हैं।
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: hi
og_description: Aspose OCR के साथ छवि से तुरंत टेक्स्ट पहचानें। OCR के लिए छवि लोड
  करने, GPU डिवाइस आईडी सेट करने और रसीद से टेक्स्ट निकालने के लिए इस चरण‑दर‑चरण गाइड
  का पालन करें।
og_title: छवि से पाठ को पहचानें – पूर्ण GPU‑त्वरित C# गाइड
tags:
- Aspose OCR
- C#
- GPU computing
title: Aspose OCR के साथ छवि से टेक्स्ट पहचानें – GPU‑त्वरित C# ट्यूटोरियल
url: /hi/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज से टेक्स्ट पहचानें – पूर्ण GPU‑त्वरित C# गाइड

क्या आपको **इमेज से टेक्स्ट पहचानने** की जरूरत पड़ी है लेकिन CPU संस्करण बहुत धीमा लगा? शायद आप **रसीद से टेक्स्ट निकालने** की कोशिश कर रहे हैं और लेटेंसी आपके यूज़र अनुभव को नुकसान पहुँचा रही है। अच्छी खबर यह है कि आपको धीमी परफ़ॉर्मेंस से समझौता नहीं करना पड़ेगा—Aspose OCR का GPU पैकेज प्रक्रिया को टर्बो‑चार्ज कर सकता है, और कोड केवल कुछ लाइनों का है।

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे कि **OCR के लिए इमेज लोड करना**, **GPU डिवाइस ID सेट करना**, और अंत में साधारण‑टेक्स्ट परिणाम प्राप्त करना कैसे किया जाता है। अंत तक आपके पास एक तैयार‑स्निपेट होगा जो किसी भी आधुनिक Windows या Linux मशीन पर, समर्थित NVIDIA कार्ड के साथ काम करेगा।

---

## आपको क्या चाहिए

- **.NET 6+** (या .NET Framework 4.7.2+) – API दोनों के साथ काम करता है।
- **Aspose.OCR** NuGet पैकेज **और** **Aspose.OCR.Gpu** ऐड‑ऑन।
- कम से कम 2 GB VRAM वाला NVIDIA GPU (डेमो उपयोग को 1 GB तक सीमित करता है)।
- एक सैंपल इमेज, उदाहरण के लिए, स्कैन की गई रसीद (`receipt.jpg`)।

यदि आपके पास पहले से प्रोजेक्ट है, तो बस `dotnet add package Aspose.OCR` और `dotnet add package Aspose.OCR.Gpu` चलाएँ। कोई अतिरिक्त नेटिव लाइब्रेरी आवश्यक नहीं है; SDK आवश्यक CUDA बाइनरीज़ के साथ आता है।

---

## चरण‑दर‑चरण कार्यान्वयन

### ## Aspose OCR और GPU का उपयोग करके इमेज से टेक्स्ट कैसे पहचानें

नीचे **पूर्ण, स्वतंत्र प्रोग्राम** दिया गया है। इसे एक नए कंसोल प्रोजेक्ट में कॉपी‑पेस्ट करें और `Ctrl+F5` दबाएँ।

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **प्रो टिप:** यदि आपके मशीन में कई GPU हैं, तो `DeviceId` को `1`, `2` आदि में बदलें ताकि कम व्यस्त कार्ड चुना जा सके। यदि ID सीमा से बाहर है तो SDK स्पष्ट `GpuDeviceNotFoundException` फेंकेगा।

### ### चरण 1: OCR के लिए इमेज लोड करें

`OcrImage.FromFile` कॉल केवल बिटमैप पढ़ने से अधिक करती है—यह इमेज को (डेस्क्यू, बाइनराइज़ेशन) आंतरिक ह्यूरिस्टिक्स के आधार पर प्री‑प्रोसेस करती है। इसलिए **OCR के लिए इमेज लोड करना** एक अलग चरण है: यदि आपकी इमेज डेटाबेस में है तो आप `MemoryStream` का उपयोग कर सकते हैं।

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

यदि आपको **इमेज से टेक्स्ट पहचानना** है जो पहले से मेमोरी में है:

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### चरण 2: GPU डिवाइस ID और मेमोरी लिमिट सेट करें

GPU संसाधन सीमित होते हैं। `DeviceId` और `MaxMemoryMb` को उजागर करके, Aspose आपको **GPU डिवाइस ID सेट करने** की अनुमति देता है, जिससे एक प्रक्रिया पूरे कार्ड को हॉग नहीं कर पाएगी।

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

यदि आप मेमोरी कैप को पार कर जाते हैं, तो इंजन स्वचालित रूप से सिस्टम RAM में स्पिल करेगा, जो धीमा है लेकिन क्रैश से बचाता है।

### ### चरण 3: रसीद से टेक्स्ट निकालें (इमेज से टेक्स्ट पहचानें)

`Recognize` मेथड भारी काम करती है। आप Aspose OCR द्वारा समर्थित कोई भी भाषा पास कर सकते हैं; रसीदों के लिए आमतौर पर अंग्रेज़ी काम करती है, लेकिन आप `OcrLanguage.Spanish` या कस्टम लैंग्वेज पैक भी जोड़ सकते हैं।

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**अपेक्षित आउटपुट** (उदाहरण):

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

---

## सामान्य वैरिएशन और एज केस

| स्थिति | क्या बदलें | क्यों |
|-----------|----------------|-----|
| **एक इमेज में कई रसीदें** | प्रत्येक क्रॉप्ड रीजन पर `ocrEngine.Recognize` कॉल करें (`OcrImage.Crop` का उपयोग करें) | छोटे, साफ़ एरिया से सटीकता बढ़ती है। |
| **कम‑रिज़ॉल्यूशन स्कैन (<150 dpi)** | पहचान से पहले `receiptImage.Resize(2.0)` से प्री‑अपस्केल करें | अधिक पिक्सेल डेंसिटी GPU को अधिक डेटा देती है। |
| **गैर‑अंग्रेज़ी रसीदें** | `OcrLanguage.French` (या कस्टम `.traineddata`) पास करें | भाषा‑विशिष्ट मॉडल फ़ॉल्स पॉज़िटिव्स को कम करते हैं। |
| **GPU उपलब्ध नहीं** | `try‑catch` ब्लॉक में `OcrEngine` (CPU) पर फॉलबैक करें | हेडलेस सर्वरों पर भी ऐप काम करता रहता है। |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

---

## प्रोडक्शन‑रेडी OCR के लिए टिप्स

- **बैच प्रोसेसिंग:** पहचान लूप को `Parallel.ForEach` में रैप करें लेकिन समानांतरता की डिग्री को GPU स्ट्रीम की संख्या तक सीमित रखें (आमतौर पर प्रति कार्ड 1‑2)।
- **मेमोरी हाइजीन:** `OcrImage` ऑब्जेक्ट्स को तुरंत डिस्पोज़ करें (`receiptImage.Dispose()`), विशेषकर जब हजारों रसीदें प्रोसेस कर रहे हों।
- **लॉगिंग:** प्रत्येक लाइन के लिए `ocrResult.Confidence` कैप्चर करें; कम कॉन्फिडेंस मैन्युअल रिव्यू वर्कफ़्लो ट्रिगर कर सकता है।
- **सुरक्षा:** संवेदनशील रसीदों को संभालते समय इमेज फ़ाइलों को एन्क्रिप्टेड टेम्प फ़ोल्डर्स में रखें और प्रोसेसिंग के बाद साफ़ कर दें।

---

## निष्कर्ष

अब आपके पास एक **पूर्ण, चलाने योग्य उदाहरण** है जो दिखाता है कि **Aspose OCR के GPU एक्सेलेरेशन** के साथ **इमेज से टेक्स्ट पहचानें**, **OCR के लिए इमेज लोड करें**, **GPU डिवाइस ID सेट करें**, और अंत में **रसीद से टेक्स्ट निकालें** कुछ संक्षिप्त चरणों में। कोड कॉपी‑पेस्ट के लिए तैयार है, और व्याख्याएँ आपको इसे मल्टी‑लैंग्वेज, मल्टी‑GPU, या हाई‑थ्रूपुट परिदृश्यों में अनुकूलित करने के लिए पर्याप्त संदर्भ देती हैं।

अगली चुनौती के लिए तैयार हैं? `GpuOcrEngine` में लाइव वीडियो स्ट्रीम फीड करके रियल‑टाइम रसीद स्कैनिंग आज़माएँ, या परिणाम को बुककीपिंग API में इंटीग्रेट करें। तेज़ GPU OCR को साफ़ C# डिज़ाइन के साथ मिलाकर संभावनाएँ असीम हैं।

*हैप्पी कोडिंग, और आपका OCR हमेशा तेज़ रहे!*

![इमेज से टेक्स्ट पहचानें डेमो स्क्रीनशॉट](placeholder-image.png "इमेज से टेक्स्ट पहचानें उदाहरण")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}