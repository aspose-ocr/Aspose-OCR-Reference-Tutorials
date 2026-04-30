---
category: general
date: 2026-04-29
description: Aspose OCR को C# में उपयोग करके बैच में तेज़ी से इमेजेज़ का OCR करें।
  सीखें कि JPG फ़ाइलों से टेक्स्ट कैसे निकालें, स्कैन से टेक्स्ट पढ़ें, और इमेज सूची
  को समानांतर रूप से प्रोसेस करें।
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: hi
og_description: Aspose OCR के साथ छवियों को तेज़ी से बैच OCR करें। यह गाइड दिखाता
  है कि JPG से टेक्स्ट कैसे निकालें, स्कैन से टेक्स्ट पढ़ें, और इमेज सूची को समानांतर
  रूप से कैसे प्रोसेस करें।
og_title: C# में बैच OCR छवियां – JPG स्कैन की समानांतर OCR
tags:
- C#
- OCR
- Aspose
- Image Processing
title: C# में बैच OCR छवियां – JPG स्कैन की समानांतर OCR
url: /hi/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में बैच OCR इमेजेज – JPG स्कैन की पैरलल OCR

क्या आपको **बैच OCR इमेजेज** की जरूरत कभी पड़ी लेकिन आप नहीं जानते थे कि इसे कई फ़ाइलों में कैसे स्केल किया जाए? आप अकेले नहीं हैं—डेवलपर्स अक्सर स्कैन से एक‑एक करके टेक्स्ट पढ़ने पर अटक जाते हैं। अच्छी खबर यह है कि Aspose OCR के साथ आप **jpg फ़ाइलों से टेक्स्ट निकाल सकते हैं**, **स्कैन से टेक्स्ट पढ़ सकते हैं**, और **इमेज लिस्ट** को पैरलल में प्रोसेस कर सकते हैं, बस कुछ ही लाइनों के C# कोड से।

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने‑योग्य उदाहरण के माध्यम से दिखाएंगे कि यह कैसे किया जाता है। अंत तक आपके पास एक स्व-निहित कंसोल ऐप होगा जो JPEG स्कैन की फ़ोल्डर को पहचानता है, प्रत्येक पेज का टेक्स्ट प्रिंट करता है, और बताता है कि प्रत्येक ऑपरेशन में कितना समय लगा। कोई बाहरी डॉक्यूमेंट नहीं, कोई अधूरे कोड स्निपेट नहीं—सिर्फ एक पूरा समाधान जिसे आप Visual Studio में डालकर चला सकते हैं।

## आपको क्या चाहिए

- **.NET 6.0** या बाद का (कोड .NET Framework 4.6+ पर भी कंपाइल होता है)
- **Aspose.OCR** NuGet पैकेज (`Install-Package Aspose.OCR`)
- कुछ JPG या स्कैन की गई इमेज फ़ाइलें जिन्हें आप प्रोसेस करना चाहते हैं
- कोई भी IDE जो आपको पसंद हो; मैं Visual Studio 2022 इस्तेमाल कर रहा हूँ, लेकिन VS Code भी ठीक चलता है

बस इतना ही। अगर आपके पास पहले से NuGet पैकेज है, तो आप तैयार हैं।

## चरण 1 – OCR इंजन को इनिशियलाइज़ करें (Batch OCR Images Setup)

सबसे पहले हम एक `OcrEngine` इंस्टेंस बनाते हैं और उसे बताते हैं कि किस भाषा को देखना है। अधिकांश मामलों में English पर्याप्त है, लेकिन आप `OcrLanguage.English` को किसी भी सपोर्टेड भाषा से बदल सकते हैं।

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*क्यों महत्वपूर्ण है:* इंजन को एक बार इनिशियलाइज़ करके सभी इमेजेज में री‑यूज़ करना, प्रत्येक फ़ाइल के लिए नया इंस्टेंस बनाने से कहीं अधिक कुशल है। यह Aspose को आंतरिक रिसोर्सेज़ शेयर करने देता है, जो **पैरलल OCR प्रोसेसिंग** के लिए आवश्यक है।

## चरण 2 – इमेजेज की लिस्ट बनाएं (Process Image List)

अब हम उन फ़ाइल पाथ्स का कलेक्शन परिभाषित करते हैं जिन्हें हम बैच रेकग्नाइज़र में फीड करना चाहते हैं। आप इस लिस्ट को `Directory.GetFiles` से डायनामिकली जेनरेट कर सकते हैं, लेकिन स्पष्टता के लिए हम कुछ एंट्रीज़ हार्ड‑कोड करेंगे।

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*टिप:* अगर आपके पास हजारों स्कैन हैं, तो `Directory.EnumerateFiles` को `*.jpg` जैसे फ़िल्टर के साथ इस्तेमाल करें ताकि पूरी लिस्ट को मेमोरी में लोड करने से बचा जा सके।

## चरण 3 – बैच रेकग्निशन चलाएं (Parallel OCR Processing)

अब मुख्य भाग: `BatchRecognize` को कॉल करना। इस मेथड में `maxDegreeOfParallelism` आर्ग्यूमेंट होता है, जो तय करता है कि Aspose कितनी थ्रेड्स स्पिन अप करेगा। डिफ़ॉल्ट रूप से यह चार थ्रेड्स इस्तेमाल करता है, लेकिन अगर आपके CPU में अधिक कोर हैं तो आप इसे बढ़ा सकते हैं।

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*क्या हो रहा है बैकग्राउंड में?* Aspose `imagePaths` कलेक्शन को चंक्स में बाँटता है, प्रत्येक चंक को अलग थ्रेड को देता है, और फिर परिणामों को एग्रीगेट करता है। यह **jpg फ़ाइलों से टेक्स्ट निकालने** का सबसे कुशल तरीका है जब आपके पास **इमेज लिस्ट** है जिसे एक साथ प्रोसेस किया जा सकता है।

## चरण 4 – परिणाम दिखाएँ (Read Text from Scans)

अंत में हम `recognitionResults` कलेक्शन पर लूप लगाते हैं और प्रत्येक फ़ाइल का टेक्स्ट व प्रोसेसिंग टाइम प्रिंट करते हैं। `OcrResult` ऑब्जेक्ट हमें स्रोत फ़ाइल का नाम भी देता है, जो लॉग या आउटपुट स्टोर करने में मदद करता है।

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**अपेक्षित आउटपुट (उदाहरण):**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

ध्यान दें कि प्रत्येक ब्लॉक फ़ाइलनाम, OCR में लगा समय, और निकाला गया टेक्स्ट दिखाता है। यही वह जानकारी है जिसकी आपको **स्कैन से टेक्स्ट पढ़ते** समय प्रोडक्शन पाइपलाइन में जरूरत होती है।

## सामान्य एज़ केसों को संभालना

| स्थिति | ध्यान देने योग्य बात | त्वरित समाधान |
|-----------|-------------------|-----------|
| **फ़ाइल नहीं मिली** | `BatchRecognize` के अंदर `FileNotFoundException` फेंका जाता है | `imagePaths` में जोड़ने से पहले `File.Exists` से पाथ वैलिडेट करें। |
| **असमर्थित फ़ॉर्मेट** | Aspose केवल रास्टर इमेजेज (JPG, PNG, BMP, TIFF) को सपोर्ट करता है। | PDFs को पहले इमेज में बदलें (Aspose.PDF इस्तेमाल करें) या उन फ़ाइलों को स्किप करें। |
| **मेमोरी प्रेशर** | बहुत बड़ी इमेजेज कई थ्रेड्स चलने पर RAM को ख़त्म कर सकती हैं। | `maxDegreeOfParallelism` कम करें या OCR से पहले इमेजेज को रिसाइज़ करें। |
| **नॉन‑English टेक्स्ट** | भाषा English सेट होने पर अन्य स्क्रिप्ट्स मिस हो जाएँगी। | `Language = OcrLanguage.French` (या मल्टी‑लिंगुअल कॉम्बो) सेट करें। |

ये टिप्स आपके बैच जॉब को मजबूत बनाते हैं, विशेषकर जब आप **इमेज लिस्ट** को यूज़र अपलोड या स्कैन्ड आर्काइव से प्रोसेस कर रहे हों।

## प्रो टिप – पैरललिज़्म ट्यून करना

अगर आप इसे 8‑कोर मशीन पर चलाते हैं, तो पैरललिज़्म को 6 या 8 तक बढ़ाएँ और स्पीड में सुधार देखें। हालांकि, याद रखें कि प्रत्येक थ्रेड बिटमैप के लिए मेमोरी भी खपत करता है। एक अच्छा नियम:

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

`maxThreads` को `BatchRecognize` में पास करके डायनामिक, मशीन‑अवेयर कॉन्फ़िगरेशन बनाएं।

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट रेडी)

नीचे पूरा प्रोग्राम दिया गया है, जो कंपाइल करने के लिए तैयार है। बस `YOUR_DIRECTORY` को उस पाथ से बदलें जहाँ आपके JPG स्कैन स्थित हैं।

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **नोट:** `using System.IO;` लाइन `Directory` हेल्पर के लिए आवश्यक है। कोड तब एक फ्रेंडली मैसेज प्रिंट करता है जब कोई JPG नहीं मिलता, जिससे साइलेंट फेल्योर से बचा जा सके।

## निष्कर्ष

हमने एक साफ़, **बैच OCR इमेजेज** वर्कफ़्लो दिखाया जो **jpg फ़ाइलों से टेक्स्ट निकालता है**, **स्कैन से टेक्स्ट पढ़ता है**, और **इमेज लिस्ट** को प्रभावी ढंग से **पैरलल OCR प्रोसेसिंग** के साथ प्रोसेस करता है। पूरा, रन‑एबल उदाहरण दिखाता है कि इंजन को कैसे सेट‑अप करें, फ़ाइलों की कलेक्शन फीड करें, और परिणामों को संभालें—सभी जबकि मेमोरी उपयोग और थ्रेड काउंट को नियंत्रित रखें।

अगला कदम तैयार है? भाषा को French में बदलें, PDF‑से‑इमेज कन्वर्ज़न जोड़ें, या OCR टेक्स्ट को डेटाबेस में स्टोर करें। पैटर्न वही रहता है: एक बार इनिशियलाइज़ करें, लिस्ट फीड करें, और Aspose को पैरलल में भारी काम करने दें।

कोई सवाल है या अपने खुद के ट्यूनिंग शेयर करना चाहते हैं? नीचे कमेंट करें, और हैप्पी कोडिंग! 

![Batch OCR images processing flow](https://example.com/placeholder.png "Diagram illustrating batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}