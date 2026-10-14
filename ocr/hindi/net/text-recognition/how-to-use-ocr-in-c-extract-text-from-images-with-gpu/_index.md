---
category: general
date: 2026-02-13
description: C# में OCR का उपयोग करके इमेज फ़ाइलों से टेक्स्ट निकालना, GPU प्रोसेसिंग
  सक्षम करना, और स्कैन को जल्दी से टेक्स्ट में बदलना सीखें।
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: hi
og_description: C# में OCR का उपयोग कैसे करें? यह गाइड आपको दिखाता है कि इमेज फ़ाइलों
  से टेक्स्ट कैसे निकालें, GPU प्रोसेसिंग को सक्षम करें, और स्कैन को टेक्स्ट में कैसे
  बदलें।
og_title: C# में OCR का उपयोग कैसे करें – GPU के साथ छवियों से टेक्स्ट निकालें
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: C# में OCR का उपयोग कैसे करें – GPU के साथ छवियों से टेक्स्ट निकालें
url: /hi/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use OCR in C# – Extract Text from Images with GPU

क्या आपने कभी सोचा है **OCR का उपयोग करके** स्कैन किए गए दस्तावेज़ से टेक्स्ट निकालना कितना आसान हो सकता है? आप अकेले नहीं हैं—डेवलपर्स लगातार पूछते हैं, “इमेज फ़ाइलों से टेक्स्ट को प्रभावी ढंग से कैसे निकाला जाए?” अच्छी खबर यह है कि Aspose.OCR के साथ आप यही कर सकते हैं, और आप **GPU प्रोसेसिंग को सक्षम** भी कर सकते हैं जिससे समर्थित हार्डवेयर पर गति में उल्लेखनीय बढ़ोतरी मिलती है।

इस ट्यूटोरियल में हम एक पूर्ण, एंड‑टू‑एंड उदाहरण के माध्यम से दिखाएंगे कि **OCR का उपयोग कैसे करें**, **इमेज से टेक्स्ट कैसे निकालें**, **स्कैन को टेक्स्ट में कैसे बदलें**, और यदि GPU उपलब्ध नहीं है तो क्या करना है। अंत तक आपके पास एक तैयार‑चलाने योग्य C# कंसोल ऐप होगा जो पहचान किया गया टेक्स्ट प्रिंट करेगा और बताएगा कि GPU वास्तव में उपयोग हुआ या नहीं।

## What You’ll Need

- .NET 6 SDK या बाद का संस्करण (कोड .NET Core के साथ भी काम करता है)  
- Visual Studio 2022 या आपका पसंदीदा कोई भी एडिटर  
- Aspose.OCR for .NET पैकेज (NuGet के माध्यम से उपलब्ध)  
- एक हाई‑रेज़ोल्यूशन इमेज फ़ाइल (जैसे `highres_scan.tif`) परीक्षण के लिए  

कोई जटिल सेटअप नहीं—सिर्फ कुछ NuGet कमांड और आप तैयार हैं।

## Step 1: Install Aspose.OCR and Prepare the Project

सबसे पहले OCR लाइब्रेरी को अपने प्रोजेक्ट में जोड़ें। अपने सॉल्यूशन फ़ोल्डर में एक टर्मिनल खोलें और चलाएँ:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

यह एक नया कंसोल प्रोजेक्ट **OcrDemo** बनाता है और `Aspose.OCR` NuGet पैकेज जोड़ता है। लाइब्रेरी में वह `OcrEngine` क्लास है जिसका हम उपयोग करेंगे।

> **Pro tip:** यदि आपके मशीन में डेडिकेटेड GPU है, तो सुनिश्चित करें कि नवीनतम ग्राफ़िक्स ड्राइवर इंस्टॉल हो; अन्यथा लाइब्रेरी स्वतः CPU मोड में फ़ॉल्बैक कर देगी।

## Step 2: Write the Complete OCR Code

अब `Program.cs` खोलें और उसकी सामग्री को नीचे दिए गए कोड से बदलें। हर लाइन पर टिप्पणी है ताकि आप समझ सकें *क्यों* हम यह कर रहे हैं।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Why This Works

- **ProcessingMode = Gpu** इंजन को पहले GPU का उपयोग करने को बताता है। लाइब्रेरी लो‑लेवल CUDA/OpenCL कॉल्स को एब्स्ट्रैक्ट कर देती है, इसलिए आपको डिवाइस कॉन्टेक्स्ट खुद मैनेज करने की ज़रूरत नहीं।  
- **IsGpuEnabled** एक बूलियन है जो पुष्टि करता है कि GPU पाथ सफल रहा या नहीं। यदि आप `false` देखते हैं, तो इंजन स्वतः CPU पर फ़ॉल्बैक हो गया—पैनिक करने की जरूरत नहीं।  
- **RecognizeImage** सभी भारी काम करता है: इमेज लोड करता है, OCR मॉडल चलाता है, और प्लेन‑टेक्स्ट परिणाम लौटाता है। जब तक आपके पास विशेष आवश्यकताएँ (जैसे डेस्क्यूइंग) न हों, आपको बिटमैप को मैन्युअली प्री‑प्रोसेस करने की ज़रूरत नहीं।

## Step 3: Run the Application and Verify the Output

कम्पाइल और एग्जीक्यूट करें:

```bash
dotnet run
```

यदि सब कुछ सही ढंग से सेट है, तो आपको कुछ इस तरह दिखेगा:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

यदि GPU उपलब्ध नहीं है, तो पहली लाइन `GPU used: False` दिखाएगी, लेकिन निकाला गया टेक्स्ट अभी भी प्रदर्शित होगा—ग्रेसफुल फ़ॉल्बैक की वजह से।

> **Common question:** *अगर मेरी इमेज JPEG है और TIFF नहीं?*  
> `RecognizeImage` मेथड .NET के `System.Drawing` द्वारा समर्थित किसी भी फॉर्मेट (JPEG, PNG, BMP, आदि) को स्वीकार करता है। बस `imagePath` में फ़ाइल एक्सटेंशन बदल दें।

## Step 4: Optional – Tweak Settings for Better Accuracy

Aspose.OCR कुछ सेटिंग्स प्रदान करता है जिन्हें आप समायोजित कर सकते हैं:

| Setting | What it Does | When to Use |
|---------|--------------|-------------|
| `ocrEngine.Language` | विशिष्ट भाषा को फोर्स करता है (जैसे `OcrLanguage.English`) | जब आप दस्तावेज़ की भाषा जानते हों |
| `ocrEngine.PageSegMode` | पेज को ब्लॉक्स में कैसे विभाजित किया जाए, नियंत्रित करता है | मल्टी‑कॉलम लेआउट के लिए |
| `ocrEngine.DetectOrientation` | टेक्स्ट को ऑटो‑रोटेट करता है जो सीधा नहीं है | उल्टे स्कैन के मामलों में |

इन प्रॉपर्टीज़ को `RecognizeImage` कॉल करने से पहले सेट किया जा सकता है। उदाहरण के लिए:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Step 5: Visualize the Flow (Image with Alt Text)

नीचे एक सरल डायग्राम है जो **OCR का उपयोग कैसे करें** को वैकल्पिक GPU एक्सेलेरेशन के साथ दर्शाता है। यह कोड चलाने के लिए आवश्यक नहीं है, लेकिन बड़े चित्र को समझने में मदद करता है।

![GPU प्रोसेसिंग के साथ OCR कैसे उपयोग करें, आवश्यक होने पर CPU पर फ़ॉल्बैक को दर्शाता हुआ डायग्राम](/images/ocr-gpu-flow.png)

*Alt text:* *GPU प्रोसेसिंग के साथ OCR कैसे उपयोग करें, आवश्यक होने पर CPU पर फ़ॉल्बैक को दर्शाता हुआ डायग्राम*।

## Edge Cases & Troubleshooting

1. **Out‑of‑Memory on GPU** – बहुत बड़ी इमेजेज़ GPU मेमोरी को ओवरफ़्लो कर सकती हैं। ऐसे में लाइब्रेरी स्वतः CPU पर फ़ॉल्बैक कर देती है। मेमोरी उपयोग कम रखने के लिए इमेज को प्री‑स्केल करें।  
2. **Unsupported Image Format** – यदि `RecognizeImage` *NotSupportedException* फेंकता है, तो फ़ाइल एक्सटेंशन चेक करें और सुनिश्चित करें कि इमेज करप्ट नहीं है। अक्सर PNG में कन्वर्ट करने से समस्या हल हो जाती है।  
3. **Low Confidence Scores** – जब OCR परिणाम में कई अपरिचित कैरेक्टर हों, तो प्री‑प्रोसेसिंग (बाइनराइज़ेशन, नॉइज़ रिमूवल) पर विचार करें या हाई‑रेज़ोल्यूशन स्कैन का उपयोग करें।  

## Wrap‑Up: What We Achieved

हमने **C# कंसोल ऐप में OCR का उपयोग कैसे करें** को कवर किया, दिखाया कि **इमेज फ़ाइलों से टेक्स्ट कैसे निकाला जाए**, और तेज़ परिणामों के लिए **GPU प्रोसेसिंग को कैसे सक्षम किया जाए**। अब आप जानते हैं कि **स्कैन को टेक्स्ट में कैसे बदलें**, GPU वास्तव में उपयोग हुआ या नहीं, और किन सेटिंग्स को किन किन परिस्थितियों में ट्यून करना है।

### Next Steps

- आउटपुट को **सर्च इंडेक्स** (जैसे Elasticsearch) में फीड करें ताकि आपके स्कैन किए गए PDF सर्चेबल बन जाएँ।  
- **बैच प्रोसेसिंग** के साथ प्रयोग करें—इमेज फ़ोल्डर पर लूप चलाएँ और प्रत्येक परिणाम को `.txt` फ़ाइल में लिखें।  
- OCR को **ट्रांसलेशन API** के साथ जोड़ें ताकि स्कैन किए गए विदेशी भाषा दस्तावेज़ों का स्वचालित अनुवाद हो सके।  

और सवाल हैं? कमेंट करें, और हैप्पी कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}