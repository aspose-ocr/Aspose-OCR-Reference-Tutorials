---
category: general
date: 2026-01-02
description: Aspose OCR और GPU समर्थन का उपयोग करके PNG पर OCR तेज़ी से चलाएँ। जानें
  कि छवि से टेक्स्ट कैसे पहचाना जाए, छवि से टेक्स्ट कैसे निकाला जाए और GPU मेमोरी
  सीमा कैसे सेट की जाए।
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: hi
og_description: Aspose OCR और GPU त्वरण का उपयोग करके PNG पर OCR को कुशलतापूर्वक चलाएँ।
  यह ट्यूटोरियल आपको दिखाता है कि छवि से टेक्स्ट कैसे पहचाना जाए, छवि से टेक्स्ट कैसे
  निकाला जाए और GPU मेमोरी उपयोग को कैसे नियंत्रित किया जाए।
og_title: GPU के साथ PNG पर OCR चलाएँ – पूर्ण C# गाइड
tags:
- OCR
- C#
- GPU
title: GPU के साथ PNG पर OCR चलाएँ – पूर्ण C# गाइड
url: /hi/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU के साथ PNG पर OCR चलाएँ – पूर्ण C# गाइड

क्या आपको कभी **PNG पर OCR चलाने** की ज़रूरत पड़ी है लेकिन प्रदर्शन की सीमा पर अटके हुए महसूस किया? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया पाइपलाइन में एक ही उच्च‑रिज़ॉल्यूशन PNG CPU‑केवल OCR इंजन को धीमा कर सकता है, जिससे जो काम तेज़ी से होना चाहिए वह एक मिनट तक इंतज़ार बन जाता है।  

अच्छी खबर यह है कि Aspose OCR GPU एक्सटेंशन के साथ आता है जो आपको **recognize text from image** फ़ाइलों को बहुत कम समय में प्रोसेस करने देता है। इस ट्यूटोरियल में हम एक व्यावहारिक उदाहरण के माध्यम से दिखाएंगे कि C# का उपयोग करके **run OCR on PNG** कैसे किया जाए, **extract text from image** कैसे निकाला जाए, और यहाँ तक कि **set GPU memory limit** कैसे सेट किया जाए ताकि आप अपने हार्डवेयर बजट के भीतर रहें।  

हम प्रत्येक चरण के पीछे का “how” और “why” भी कवर करेंगे, ताकि आप केवल कॉपी‑पेस्ट स्निपेट नहीं, बल्कि एक ठोस मानसिक मॉडल के साथ आगे बढ़ें।

## आप क्या सीखेंगे

- Aspose OCR के GPU समर्थन का उपयोग करने के लिए आवश्यक पूर्वापेक्षाएँ।  
- `Bitmap` में PNG लोड करने और OCR इंजन को फीड करने का तरीका।  
- उत्तम प्रदर्शन के लिए `GpuDevice` और `GpuMemoryLimitMb` को कॉन्फ़िगर करने का तरीका।  
- **recognize text from image** करने और साधारण टेक्स्ट परिणाम प्राप्त करने का तरीका।  
- लो‑मेमोरी GPUs या मल्टी‑पेज PNGs जैसे सामान्य एज केस को संभालने के टिप्स।  

इस गाइड के अंत तक आप GPU गति पर **run OCR on PNG** फ़ाइलें चला सकेंगे और अपने OCR कार्यों की मेमोरी फुटप्रिंट को आत्मविश्वास से नियंत्रित कर सकेंगे।

![GPU त्वरण के साथ PNG पर OCR चलाने का आरेख](run-ocr-on-png-diagram.png "run OCR on PNG उदाहरण")

## पूर्वापेक्षाएँ

शुरू करने से पहले, सुनिश्चित करें कि आपके पास है:

1. .NET 6.0 या बाद का संस्करण (कोड .NET Core और .NET Framework के साथ भी काम करता है)।  
2. CUDA समर्थन वाला NVIDIA GPU (उदाहरण में डिवाइस इंडेक्स 0 चुना गया है)।  
3. Aspose.OCR NuGet पैकेज और उसके GPU एक्सटेंशन (`Aspose.OCR.Extensions`).  
4. एक नमूना PNG (`input.png`) जिसे आप अपने प्रोजेक्ट से संदर्भित कर सकें, ऐसी फ़ोल्डर में रखें।  

यदि इनमें से कोई भी अपरिचित लग रहा है, तो चिंता न करें—हम जहाँ आवश्यक होगा, वैकल्पिक विकल्पों का उल्लेख करेंगे।

---

## चरण 1 – Aspose OCR और GPU एक्सटेंशन इंस्टॉल करें

सबसे पहले यह सुनिश्चित करें। सही लाइब्रेरीज़ के बिना बाकी कोड कम्पाइल नहीं होगा।

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

`Aspose.OCR.Extensions` पैकेज GPU त्वरण के लिए आवश्यक नेटिव CUDA बाइनरीज़ को शामिल करता है।  
*Pro tip:* यदि आपके मशीन में GPU नहीं है, तो भी आप प्रोजेक्ट को कम्पाइल कर सकते हैं; बाद में केवल `PreferGpu = false` सेट करें।

---

## चरण 2 – वह PNG लोड करें जिसे आप प्रोसेस करना चाहते हैं

अब हम वास्तव में **run OCR on PNG** करते हैं, इसे `Bitmap` में लोड करके। यह चरण सरल है लेकिन एक छोटी सी नोट आवश्यक है: `Bitmap` फ़ाइल पाथ की अपेक्षा करता है, इसलिए सुनिश्चित करें कि पाथ आपके एक्सीक्यूटेबल के सापेक्ष सही हो।

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

यदि PNG असामान्य रूप से बड़ा है (उदाहरण के लिए, किसी एक पक्ष में > 5000 px), तो GPU मेमोरी समाप्त होने से बचने के लिए पहले इसे डाउनस्केल करना चाह सकते हैं। बाद में **set GPU memory limit** विकल्प यहाँ उपयोगी साबित होता है।

---

## चरण 3 – GPU उपयोग के लिए OCR इंजन बनाएं और कॉन्फ़िगर करें

यह ट्यूटोरियल का मुख्य भाग है: GPU का उपयोग करके OCR इंजन को **recognize text from image** करने के लिए कॉन्फ़िगर करना। दो प्रॉपर्टीज़ मुख्य हैं:

- `GpuDevice` – कौन सा CUDA डिवाइस उपयोग करना है, चुनता है।  
- `GpuMemoryLimitMb` – इंजन द्वारा आवंटित की जा सकने वाली GPU मेमोरी की मात्रा को सीमित करता है।  

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**मेमोरी लिमिट क्यों सेट करें?** कुछ GPUs डिस्प्ले के साथ मेमोरी साझा करते हैं या एक साथ कई वर्कलोड चलाते हैं। आवंटन को सीमित करके आप आउट‑ऑफ़‑मेमोरी क्रैश से बचते हैं, विशेषकर जब कई PNGs को समानांतर में प्रोसेस किया जाता है।

---

## चरण 4 – रिकग्निशन विकल्प निर्धारित करें (भाषा और GPU प्राथमिकता)

`RecognitionOptions` ऑब्जेक्ट इंजन को बताता है कि कौन सी भाषा खोजनी है और क्या छोटे इमेज के लिए भी **prefer GPU** करना है। अधिकांश अंग्रेज़ी दस्तावेज़ों के लिए यह पर्याप्त है, लेकिन आप `Language.English` को अन्य समर्थित लोकेल्स से बदल सकते हैं।

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

यदि आपको कभी अंग्रेज़ी के अलावा किसी भाषा में **extract text from image** करने की ज़रूरत पड़े, तो केवल `Language` एन्‍युम को बदलें। लाइब्रेरी बॉक्स से बाहर दर्जनों भाषाओं का समर्थन करती है।

---

## चरण 5 – OCR चलाएँ और परिणाम प्राप्त करें

सभी सेटअप के बाद, अंतिम कॉल एक ही लाइन है जो वास्तव में **run OCR on PNG** करता है और एक समृद्ध परिणाम ऑब्जेक्ट लौटाता है।

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult` में केवल साधारण टेक्स्ट (`ocrResult.Text`) ही नहीं, बल्कि कॉन्फिडेंस स्कोर, बाउंडिंग बॉक्स, और यहाँ तक कि हाइलाइटेड शब्दों के साथ मूल इमेज भी शामिल है—यदि आपको डिबग या एक्सट्रैक्शन को विज़ुअलाइज़ करने की ज़रूरत हो तो यह उपयोगी है।

**अपेक्षित आउटपुट** (एक नमूना PNG के लिए जिसमें “Hello World” लिखा है):

```
=== OCR Output ===
Hello World
```

यदि टेक्स्ट गड़बड़ दिखे, तो दोबारा जांचें कि PNG खराब नहीं है और GPU मेमोरी लिमिट इमेज साइज के लिए बहुत कम नहीं है।

---

## चरण 6 – एज केस को संभालना और सर्वोत्तम‑प्रैक्टिस टिप्स

### लो‑मेमोरी GPUs

यदि आपको `CudaException: out of memory` जैसी एक्सेप्शन मिलती है, तो `GpuMemoryLimitMb` को कम करें या प्रोसेसिंग से पहले PNG को टाइल्स में विभाजित करें। टाइलिंग `Graphics.DrawImage` के साथ `Bitmap` क्लोन पर की जा सकती है।

### बैच में कई PNGs

जब आप PNGs के फ़ोल्डर को प्रोसेस करते हैं, तो वही `OcrEngine` इंस्टेंस पुन: उपयोग करें—एक बार इनिशियलाइज़ करने से GPU कॉन्टेक्स्ट स्विच बचते हैं।

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### CPU पर फॉलबैक

यदि GPU उपलब्ध नहीं है, तो बस `PreferGpu = false` सेट करें। इंजन बिना किसी कोड परिवर्तन के स्वचालित रूप से CPU पर फॉलबैक कर देगा।

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## पूर्ण कार्यशील उदाहरण

नीचे पूर्ण प्रोग्राम दिया गया है जिसे आप नई कंसोल प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं। इसमें ऊपर बताए सभी चरण और कुछ सुरक्षा जांचें शामिल हैं।

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

`Program.cs` के रूप में फ़ाइल सहेजें, `dotnet run` चलाएँ, और आपको कंसोल में निकाला गया टेक्स्ट दिखना चाहिए।

---

## निष्कर्ष

हमने अभी दिखाया कि Aspose OCR के GPU एक्सटेंशन का उपयोग करके **run OCR on PNG** फ़ाइलें कैसे चलाएँ, **recognize text from image** कैसे करें, और **extract text from image** करते समय **set GPU memory limit** को कैसे नियंत्रित करें। `GpuDevice` और `GpuMemoryLimitMb` को कॉन्फ़िगर करके आप अपने एप्लिकेशन को तेज़ और स्थिर रख सकते हैं, भले ही GPU मध्यम हो।

अब आप आगे कर सकते हैं:

- अन्य भाषाओं के साथ प्रयोग करें (`Language.French`, `Language.Spanish`)।  
- OCR चरण को बड़े दस्तावेज़‑प्रोसेसिंग पाइपलाइन में इंटीग्रेट करें।  
- कच्चे टेक्स्ट को परिष्कृत करने के लिए स्पेल‑चेकिंग या एंटिटी एक्सट्रैक्शन जैसी पोस्ट‑प्रोसेसिंग जोड़ें।  

याद रखें, मुख्य बात केवल कोड नहीं बल्कि यह समझना है कि प्रत्येक सेटिंग क्यों महत्वपूर्ण है। जब आप जानते हैं कि **set GPU memory limit** कैसे करें और कब CPU पर फॉलबैक करना है, तो आप ऐसे OCR समाधान बनाएँगे जो सहजता से स्केल हों।  

यदि आपके पास किसी विशिष्ट PNG साइज, मल्टी‑पेज TIFFs, या GPU त्रुटियों के समाधान के बारे में प्रश्न हैं, तो नीचे टिप्पणी छोड़ें, और कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}