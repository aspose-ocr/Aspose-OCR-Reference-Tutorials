---
category: general
date: 2026-02-28
description: सी# में छवियों को लंबवत संयोजित करके सर्चेबल PDF बनाएं। जानें कि कैसे
  छवियों को लंबवत स्टैक किया जाए और Aspose OCR के साथ स्कैन किए गए पृष्ठों को PDF
  में परिवर्तित किया जाए।
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: hi
og_description: C# में छवियों को लंबवत मिलाकर खोज योग्य PDF बनाएं। यह गाइड दिखाता
  है कि कैसे छवियों को लंबवत स्टैक किया जाए और Aspose OCR का उपयोग करके स्कैन किए
  गए पृष्ठों को PDF में परिवर्तित किया जाए।
og_title: C# में खोज योग्य PDF बनाएं – छवियों को लंबवत संयोजित करें
tags:
- Aspose OCR
- C#
- PDF generation
title: C# में खोज योग्य PDF बनाएं – छवियों को लंबवत संयोजित करें
url: /hi/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में सर्चेबल PDF बनाएं – इमेजेज़ को वर्टिकली कॉम्बाइन करें

क्या आपको कभी **create searchable PDF** कुछ स्कैन किए गए PNGs से बनाना पड़ा लेकिन आप नहीं जानते थे कि कहाँ से शुरू करें? आप अकेले नहीं हैं। कई दस्तावेज़‑ऑटोमेशन प्रोजेक्ट्स में सबसे बड़ी समस्या इमेज फ़ाइलों के एक ढेर को एक साफ़, सर्चेबल PDF में बदलना है जिसे आप इंडेक्स और शेयर कर सकें।  

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने‑योग्य उदाहरण के माध्यम से चलेंगे जो आपको दिखाता है **how to stack images vertically**, **combine images vertically**, और अंत में **convert scanned pages PDF** को Aspose.OCR के GPU‑accelerated इंजन का उपयोग करके एक सिंगल सर्चेबल डॉक्यूमेंट में बदलता है। अंत तक आपके पास एक सेल्फ‑कंटेन्ड प्रोग्राम होगा जिसे आप किसी भी .NET सॉल्यूशन में डाल सकते हैं।

> **आप क्या सीखेंगे**
> - GPU समर्थन के साथ OCR इंजन को इनिशियलाइज़ करें।
> - इमेजेज़ के बैच को समानांतर में प्रोसेस करें।
> - **Combine images vertically** को मल्टी‑पेज स्कैन की नकल करने के लिए उपयोग करें।
> - डाउनस्ट्रीम विश्लेषण के लिए सर्चेबल PDF और विस्तृत JSON रिपोर्ट एक्सपोर्ट करें।

## पूर्वापेक्षाएँ

- .NET 6+ (कोड .NET 6, .NET 7, या .NET 8 पर कंपाइल होता है)
- Aspose.OCR NuGet पैकेज (`Install-Package Aspose.OCR`)
- यदि आप `ProcessingMode.Gpu` सेटिंग रखना चाहते हैं तो GPU‑सक्षम मशीन (CPU फ़ॉलबैक भी काम करता है)
- कुछ स्कैन किए गए PNG/JPEG फ़ाइलों वाला फ़ोल्डर (डेमो `page1.png`, `page2.png`, `page3.png` का उपयोग करता है)

कोई बाहरी सर्विसेज़ नहीं, कोई छिपी हुई कॉन्फ़िगरेशन फ़ाइलें नहीं—सिर्फ शुद्ध C#।

## चरण 1 – OCR इंजन सेट अप करें **Create Searchable PDF** बनाने के लिए

पहले हम एक `OcrEngine` बनाते हैं, GPU एक्सेलेरेशन चालू करते हैं, भाषा के रूप में अंग्रेज़ी चुनते हैं, और कुछ प्री‑प्रोसेसिंग फ़िल्टर जोड़ते हैं। ये फ़िल्टर टिल्टेड पेजों को सीधा (`DeskewFilter`) करके और शोर को हटाकर (`DenoiseFilter`) सटीकता बढ़ाते हैं।

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Why this matters:** OCR इंजन टेक्स्ट को पहचानने का भारी काम करता है। `ProcessingMode.Gpu` को एनेबल करने से आधुनिक ग्राफ़िक्स कार्ड पर पहचान समय आधा हो सकता है, जबकि फ़िल्टर सामान्य स्कैनिंग आर्टिफ़ैक्ट्स को कम करते हैं जो अन्यथा गड़बड़ आउटपुट उत्पन्न करेंगे।

## चरण 2 – बैच प्रोसेसर को कॉन्फ़िगर करें **Convert Scanned Pages PDF** को प्रभावी ढंग से

प्रत्येक पेज को एक‑एक करके प्रोसेस करना कुछ इमेजेज़ के लिए ठीक है, लेकिन वास्तविक प्रोजेक्ट्स में अक्सर दर्जनों या सैकड़ों पेज शामिल होते हैं। Aspose.OCR का `OcrBatchProcessor` हमें पहचान को समानांतर में चलाने देता है, जिससे **convert scanned pages pdf** चरण बहुत तेज़ हो जाता है।

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Pro tip:** यदि आप केवल CPU वाले बॉक्स पर हैं, तो `ProcessingMode = ProcessingMode.Cpu` सेट करें। बैच प्रोसेसर अभी भी `MaxDegreeOfParallelism` का सम्मान करेगा, इसलिए आप इसे मशीन को ओवर‑लोड होने से बचाने के लिए ट्यून कर सकते हैं।

## चरण 3 – बैच पर OCR चलाएँ और परिणाम एकत्र करें

अब हम वास्तव में टेक्स्ट को पहचानते हैं। `Recognize` मेथड `OcrResult` ऑब्जेक्ट्स की एक लिस्ट रिटर्न करता है, जिसमें प्रत्येक में मूल इमेज और निकाला गया टेक्स्ट दोनों होते हैं।

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

इस बिंदु पर आपके पास **create searchable PDF** बनाने के लिए सब कुछ है: इमेजेज़ (अभी भी मेमोरी में) और संबंधित टेक्स्ट लेयर्स।

## चरण 4 – **Combine Images Vertically** और सर्चेबल PDF जेनरेट करें

अधिकांश स्कैन किए गए दस्तावेज़ मल्टी‑पेज PDF होते हैं, इसलिए हमें व्यक्तिगत पेज इमेजेज़ को एक लंबी इमेज में सिलाई करनी होती है जो भौतिक स्टैक को दर्शाती है। Aspose.OCR इस उद्देश्य के लिए `Image.CombineVertical` प्रदान करता है।

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

परिणामी फ़ाइल (`combined_searchable.pdf`) प्रत्येक पेज इमेज के नीचे चयन योग्य, सर्चेबल टेक्स्ट रखती है—बिल्कुल वही जो आपको स्कैन किए गए स्रोतों से **create searchable PDF** बनाने के लिए चाहिए।

![Create searchable PDF example](/images/create-searchable-pdf.png "create searchable pdf example")

*छवि वैकल्पिक पाठ: create searchable pdf example showing a combined PDF with searchable text.*

**Why vertical stacking?** कई OCR लाइब्रेरीज़ प्रत्येक इमेज को अलग पेज मानती हैं। उन्हें स्टैक करके, हम PDF के पेज क्रम को बरकरार रखते हैं जबकि पूरे दस्तावेज़ के लिए एक ही OCR पास का उपयोग करते हैं।

## चरण 5 – पहले पेज के लिए विस्तृत JSON एक्सपोर्ट करें (डाउनस्ट्रीम वर्कफ़्लो के लिए शानदार)

कभी-कभी आपको PDF से अधिक चाहिए; शायद आप OCR डेटा को डेटाबेस या मशीन‑लर्निंग पाइपलाइन में फ़ीड करना चाहते हैं। Aspose.OCR आपको प्रत्येक `OcrResult` को JSON में सीरियलाइज़ करने देता है, जिसमें बाउंडिंग बॉक्स, कॉन्फिडेंस स्कोर, और अधिक शामिल रहते हैं।

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**अपेक्षित JSON स्निपेट (संक्षिप्त):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

अब आप इस JSON को किसी भी डाउनस्ट्रीम सिस्टम में फ़ीड कर सकते हैं—चाहे आप टेक्स्ट को Elasticsearch में इंडेक्स कर रहे हों या इसे कस्टम एनालिटिक्स डैशबोर्ड में भेज रहे हों।

---

## कैसे **Stack Images Vertically** – एक त्वरित सारांश

यदि आप सोच रहे हैं **how to stack images vertically** Aspose के बिना, आप `System.Drawing` का उपयोग करके एक नया बिटमैप बना सकते हैं और प्रत्येक पेज को क्रमशः ड्रॉ कर सकते हैं। हालांकि, Aspose का बिल्ट‑इन `Image.CombineVertical` DPI, पिक्सेल फ़ॉर्मेट, और मेमोरी मैनेजमेंट को आपके लिए संभालता है, जिससे यह प्रोडक्शन कोड के लिए सबसे भरोसेमंद विकल्प बन जाता है।

### वैकल्पिक: `System.Drawing` का उपयोग (सिर्फ जिज्ञासा के लिए)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

मैनुअल तरीका काम करता है, लेकिन आप ऑटोमैटिक DPI हैंडलिंग की सुविधा और परिणाम को सीधे `RecognizeToPdf` में फ़ीड करने की क्षमता खो देते हैं। जब तक आपके पास बहुत विशेष आवश्यकता न हो, `CombineVertical` के साथ रहें।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| **Out‑of‑memory errors** जब दर्जनों हाई‑रेज़ोल्यूशन स्कैन प्रोसेस कर रहे हों | प्रत्येक इमेज PDF लिखे जाने तक मेमोरी में रहती है | `Image` ऑब्जेक्ट्स को तुरंत डिस्पोज़ करें (`using` ब्लॉक्स) या कॉम्बाइन करने से पहले इमेजेज़ को डाउनस्केल करें |
| **Garbage text** OCR के बाद | टिल्टेड स्कैन या कम कॉन्ट्रास्ट | `DeskewFilter` और `DenoiseFilter` रखें; यदि आवश्यक हो तो `ContrastFilter` जोड़ने पर विचार करें |
| **Missing searchable layer** | `Recognize` का उपयोग किया `RecognizeToPdf` के बजाय | सुनिश्चित करें कि आप संयुक्त इमेज पर `ocrEngine.RecognizeToPdf` कॉल करें |
| **GPU fallback fails** उन मशीनों पर जिनके पास उचित ड्राइवर नहीं हैं | `ProcessingMode.Gpu` एक एक्सेप्शन थ्रो करता है | इंजन निर्माण को try/catch में रैप करें और `ProcessingMode.Cpu` पर फ़ॉलबैक करें |

## अगले कदम – वर्कफ़्लो का विस्तार

अब जब आप जानते हैं कि **create searchable PDF** कैसे बनाते हैं, आप चाह सकते हैं:

- `Directory.GetFiles` और `foreach` लूप का उपयोग करके पूरे फ़ोल्डरों को बैच‑प्रोसेस करें।
- कॉम्बाइन करने से पहले प्रत्येक पेज में वॉटरमार्क जोड़ें (`Aspose.Imaging` से `ImageProcessor` का उपयोग करके)।
- यदि बाद में प्रति‑पेज PDF चाहिए तो सर्चेबल PDF को व्यक्तिगत पेजों में विभाजित करें (`Aspose.PDF` के `PdfDocument.Split` का उपयोग करके)।
- इमेजेज़ को क्लाउड से लाने और अंतिम PDF को वापस पुश करने के लिए Azure Blob Storage के साथ इंटीग्रेट करें।

इन सभी एक्सटेंशन में स्वाभाविक रूप से वही कोर कॉन्सेप्ट्स शामिल होते हैं: OCR सेटअप, इमेज हैंडलिंग, और PDF एक्सपोर्ट।

---

## निष्कर्ष

हमने C# में स्कैन किए गए इमेजेज़ के संग्रह से **create searchable PDF** बनाने के लिए सभी आवश्यक चीज़ें कवर कर ली हैं। GPU‑enabled `OcrEngine` को इनिशियलाइज़ करके, `OcrBatchProcessor` के साथ एक समानांतर बैच चलाकर, **combining images vertically**, और अंत में `RecognizeToPdf` को कॉल करके, आप एक साफ़, सर्चेबल डॉक्यूमेंट प्राप्त करते हैं जो आर्काइविंग या इंडेक्सिंग के लिए तैयार है। अतिरिक्त JSON एक्सपोर्ट आपको OCR परिणामों की पूरी दृश्यता देता है, जिससे एनालिटिक्स या कस्टम वर्कफ़्लो के लिए द्वार खुलते हैं।

इसे आज़माएँ, विभिन्न फ़िल्टरों के साथ प्रयोग करें, और देखें आपका दस्तावेज़‑ऑटोमेशन पाइपलाइन कितना स्मूद हो जाता है। यदि आपको कोई अजीब समस्या मिले, तो टिप्पणी छोड़ें—हैप्पी कोडिंग!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}