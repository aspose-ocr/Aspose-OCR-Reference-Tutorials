---
category: general
date: 2026-02-25
description: GPU‑त्वरित OCR का उपयोग करके छवि से तेज़ी से टेक्स्ट पहचानें। GPU मोड
  सेट करना, OCR के लिए छवि लोड करना, और TIFF से टेक्स्ट निकालना सीखें।
draft: false
keywords:
- recognize text from image
- set gpu mode
- gpu accelerated ocr
- load image for ocr
- extract text from tiff
language: hi
og_description: GPU‑संचालित OCR का उपयोग करके छवि से तुरंत पाठ पहचानें। सेट GPU मोड,
  OCR के लिए छवि लोड करना, और TIFF से पाठ निकालना शामिल करने वाला चरण‑दर‑चरण C# ट्यूटोरियल।
og_title: GPU‑त्वरित OCR के साथ छवि से टेक्स्ट पहचानें – C# गाइड
tags:
- Aspose OCR
- C#
- GPU computing
title: C# में GPU‑त्वरित OCR का उपयोग करके छवि से टेक्स्ट पहचानें
url: /hi/net/ocr-optimization/recognize-text-from-image-using-gpu-accelerated-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU‑त्वरित OCR के साथ C# में इमेज से टेक्स्ट पहचानें

क्या आपको **इमेज से टेक्स्ट पहचानने** की ज़रूरत रही है लेकिन आपका CPU हाई‑रिज़ॉल्यूशन स्कैन पर थक गया था? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में—जैसे इनवॉइस डिजिटाइज़ेशन या पुराने समाचारपत्रों का आर्काइव—एक ही TIFF फ़ाइल आपके पाइपलाइन को मिनटों तक रोक सकती है। अच्छी ख़बर? Aspose.OCR आपको एक स्विच फ़्लिप करने देता है और भारी काम आपके GPU को सौंप देता है, जिससे धीमी प्रक्रिया लगभग तुरंत हो जाती है।

इस ट्यूटोरियल में हम पूरे प्रोसेस को कवर करेंगे: **GPU मोड कैसे सेट करें**, **OCR के लिए इमेज कैसे लोड करें**, और **TIFF फ़ाइलों से टेक्स्ट कैसे निकालें**। अंत तक आपके पास एक स्व-समाहित, प्रोडक्शन‑रेडी उदाहरण होगा जिसे आप किसी भी .NET 6+ प्रोजेक्ट में डाल सकते हैं।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

- .NET 6 SDK (या बाद का) इंस्टॉल किया हुआ।
- Visual Studio 2022 या कोई भी एडिटर जो आप पसंद करते हैं।
- Aspose.OCR NuGet पैकेज (`Aspose.OCR`) आपके प्रोजेक्ट में जोड़ा हुआ।
- DirectX 11 या बाद का सपोर्ट करने वाला GPU (ज्यादातर आधुनिक GPU इस मानदंड को पूरा करते हैं)।  
  *यदि आपके पास GPU नहीं है, तो आप अभी भी `GpuMode.Auto` के साथ कोड चला सकते हैं—लाइब्रेरी स्वचालित रूप से CPU पर फ़ॉल बैक हो जाएगी।*

> **Pro tip:** अपने GPU ड्राइवर को अपडेट रखें; पुराने ड्राइवर कभी‑कभी अजीब इनिशियलाइज़ेशन एरर दे सकते हैं।

## Step 1 – Create the OCR engine and set GPU mode

सबसे पहले आपको `OcrEngine` की एक इंस्टेंस चाहिए। यह ऑब्जेक्ट सभी कॉन्फ़िगरेशन रखता है, जिसमें यह भी शामिल है कि इंजन GPU का उपयोग करेगा या नहीं।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Enable GPU acceleration.
            // Use GpuMode.Auto if you want the library to pick CPU when a GPU isn’t available.
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled);

            // The rest of the workflow continues below…
        }
    }
}
```

**Why this matters:** GPU मोड को एनेबल करने से इमेज प्री‑प्रोसेसिंग (बाइनराइज़ेशन, नॉइज़ रिमूवल आदि) ग्राफ़िक्स कार्ड पर चली जाती है। मिड‑रेंज RTX 3060 पर आप शुद्ध CPU प्रोसेसिंग की तुलना में **3‑5× तेज़** गति देख सकते हैं।

## Step 2 – Load image for OCR (TIFF example)

Aspose.OCR कई फ़ॉर्मेट सपोर्ट करता है, लेकिन स्कैन किए गए दस्तावेज़ों के लिए TIFF आम है क्योंकि यह लॉसलेस क्वालिटी रखता है। `ImageStream.FromFile` का उपयोग करके फ़ाइल को मेमोरी में पढ़ें।

```csharp
// Step 2: Load the high‑resolution TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"C:\Data\high_res_scan.tif");

// Optional: If you need to work with a stream (e.g., from a web API), use:
// ocrEngine.Image = ImageStream.FromStream(yourInputStream);
```

**Edge case:** कुछ TIFF फ़ाइलों में कई पेज होते हैं। `ImageStream.FromFile` केवल पहला पेज पढ़ेगा। यदि आपको हर पेज प्रोसेस करना है, तो `ImageInfo.Pages` पर लूप करें और प्रत्येक पेज को अलग‑अलग इंजन को फीड करें।

## Step 3 – Perform the recognition

अब जब इंजन कॉन्फ़िगर हो गया है और इमेज लोड हो गई है, तो `Recognize()` को कॉल करें। यह मेथड एक `OcrResult` ऑब्जेक्ट रिटर्न करता है जिसमें प्लेन‑टेक्स्ट आउटपुट और अतिरिक्त मेटाडेटा होता है।

```csharp
// Step 3: Run OCR
OcrResult result = ocrEngine.Recognize();

// The result may include confidence scores per line, if you enable them in the config.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

**What if the text looks garbled?**  
- सुनिश्चित करें कि इमेज पढ़ने योग्य ओरिएंटेशन में है (ज़रूरत पड़े तो रोटेट करें)।  
- प्री‑प्रोसेसिंग विकल्प जैसे `ocrEngine.Config.DeskewEnabled = true;` को एडजस्ट करें।  
- मल्टी‑लैंग्वेज़ डॉक्यूमेंट्स के लिए `ocrEngine.Config.Language = Language.English;` या उपयुक्त एन्‍युम सेट करें।

## Step 4 – Verify the output and handle errors

एक मजबूत इम्प्लीमेंटेशन null रिज़ल्ट की जाँच करता है और संभावित एक्सेप्शन (जैसे, गायब GPU ड्राइवर) को कैच करता है।

```csharp
try
{
    OcrResult result = ocrEngine.Recognize();

    if (result?.Text == null)
    {
        Console.WriteLine("No text detected – double‑check the image quality.");
    }
    else
    {
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
catch (Exception ex)
{
    Console.WriteLine($"OCR failed: {ex.Message}");
    // You might want to fallback to CPU mode here:
    // ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
}
```

**Why wrap it?** GPU इनिशियलाइज़ेशन `DllNotFoundException` फेंक सकता है अगर आवश्यक नेटिव लाइब्रेरीज़ मौजूद नहीं हैं। कैच ब्लॉक आपको ग्रेसफ़ुल डिग्रेडेशन पाथ देता है।

## Full, runnable example

सब कुछ एक साथ मिलाकर, यहाँ एक पूर्ण प्रोग्राम है जिसे आप अभी कंपाइल और रन कर सकते हैं। फ़ाइल पाथ को अपने मशीन पर मौजूद वास्तविक TIFF से बदलें।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // 1️⃣ Create OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled); // or GpuMode.Auto for fallback

            // 2️⃣ Load the image you want to process
            string imagePath = @"C:\Data\high_res_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Optional: tweak preprocessing (helps with noisy scans)
            ocrEngine.Config.DeskewEnabled = true;
            ocrEngine.Config.RemoveNoiseEnabled = true;

            // 4️⃣ Run recognition and handle the result
            try
            {
                OcrResult result = ocrEngine.Recognize();

                if (string.IsNullOrWhiteSpace(result?.Text))
                {
                    Console.WriteLine("No text found – consider improving image quality.");
                }
                else
                {
                    Console.WriteLine("=== Recognized Text ===");
                    Console.WriteLine(result.Text);
                }
            }
            catch (Exception e)
            {
                Console.WriteLine($"Error during OCR: {e.Message}");
                // Fallback to CPU if GPU failed
                ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
                // You could retry here…
            }
        }
    }
}
```

**Expected output**

यदि TIFF में पठनीय अंग्रेज़ी टेक्स्ट है, तो आपको कुछ इस तरह दिखेगा:

```
=== Recognized Text ===
Invoice #12345
Date: 2024‑11‑08
Total Amount: $1,235.00
...
```

यदि इमेज खाली या अपठनीय है, तो कंसोल आपको स्रोत फ़ाइल की जाँच करने का सुझाव देगा।

## Common questions & variations

| Question | Answer |
|----------|--------|
| **Can I process JPEG or PNG instead of TIFF?** | बिल्कुल। `ImageStream.FromFile` किसी भी फ़ॉर्मेट के साथ काम करता है जो Aspose.OCR सपोर्ट करता है (PNG, JPEG, BMP, आदि)। |
| **What if I have multiple pages in one TIFF?** | `ImageInfo.Pages` पर लूप करें और प्रत्येक पेज को `ocrEngine.Image` असाइन करें, फिर `Recognize()` कॉल करें। |
| **Do I need a license for Aspose.OCR?** | फ्री इवैल्युएशन 100 पेज तक काम करता है। प्रोडक्शन के लिए लाइसेंस खरीदें ताकि इवैल्युएशन वॉटरमार्क हट जाए। |
| **How do I change the language model?** | `ocrEngine.Config.Language = Language.Spanish;` (या कोई भी सपोर्टेड एन्‍युम) सेट करें। |
| **Is there a way to get confidence scores?** | `ocrEngine.Config.EnableConfidence = true;` एनेबल करें और `result.Confidence` को प्रत्येक लाइन के लिए देखें। |

## Conclusion

अब आप **GPU‑त्वरित OCR** पाइपलाइन का उपयोग करके **इमेज से टेक्स्ट पहचानना** जानते हैं। **GPU मोड सेट करके**, **OCR के लिए इमेज लोड करके**, और **TIFF फ़ाइलों से टेक्स्ट निकालकर**, आपने एक तेज़, स्केलेबल सॉल्यूशन बना लिया है जो वास्तविक‑दुनिया के वर्कलोड्स के लिए तैयार है।

अगले कदम? इस कोड को PDF जेनरेटर के साथ चेन करें ताकि सर्चेबल PDFs बन सकें, या एक्सट्रैक्टेड स्ट्रिंग्स को नेचुरल‑लैंग्वेज प्रोसेसिंग पाइपलाइन में फीड करें। आप `GpuMode.Auto` के साथ भी प्रयोग कर सकते हैं ताकि आपका ऐप GPU‑रहित एनवायरनमेंट में भी चल सके।

हैप्पी कोडिंग, और आपका OCR तेज़‑तर्रार रहे! 

![इमेज से टेक्स्ट पहचानने का उदाहरण](https://example.com/ocr-demo.png "GPU‑त्वरित OCR के साथ इमेज से टेक्स्ट पहचानें")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}