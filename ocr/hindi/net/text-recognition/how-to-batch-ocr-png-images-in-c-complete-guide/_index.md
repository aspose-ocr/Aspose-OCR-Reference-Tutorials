---
category: general
date: 2026-04-26
description: PNG छवियों को तेज़ी से बैच OCR कैसे करें। PNG से टेक्स्ट निकालना, छवियों
  को टेक्स्ट में बदलना, पहचाने गए टेक्स्ट को लिखना, और Aspose OCR के साथ PNG डायरेक्टरी
  पढ़ना सीखें।
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: hi
og_description: C# में Aspose OCR के साथ PNG इमेजेज़ को बैच में OCR कैसे करें। यह
  गाइड दिखाता है कि PNG से टेक्स्ट कैसे निकालें, इमेजेज़ को टेक्स्ट में कैसे बदलें,
  और पहचाने गए टेक्स्ट को प्रभावी ढंग से कैसे लिखें।
og_title: C# में PNG छवियों का बैच OCR कैसे करें – चरण‑दर‑चरण
tags:
- OCR
- C#
- Aspose
title: C# में PNG छवियों का बैच OCR कैसे करें – पूर्ण मार्गदर्शिका
url: /hi/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में PNG इमेजेज़ को बैच OCR करने का पूरा गाइड

क्या आपने कभी सोचा है कि **कैसे एक पूरे फ़ोल्डर की PNG फ़ाइलों को बैच OCR** किया जाए बिना प्रत्येक इमेज के लिए अलग प्रोग्राम लिखे? आप अकेले नहीं हैं जो दर्जनों स्क्रीनशॉट, स्कैन किए हुए रसीदें या ग्राफ़िक्स को सर्चेबल टेक्स्ट में बदलने की कोशिश कर रहे हैं। इस ट्यूटोरियल में हम एक व्यावहारिक समाधान पर चलते हैं जो **PNG से टेक्स्ट निकालता है**, **इमेजेज़ को टेक्स्ट में बदलता है**, और **पहचाने गए टेक्स्ट को अलग‑अलग फ़ाइलों में लिखता है**—सभी PNG डायरेक्टरी को स्वचालित रूप से पढ़ते हुए।

इस गाइड के अंत तक आपके पास एक तैयार‑चलाने‑योग्य C# कंसोल ऐप होगा जो एक ही बार में किसी भी संख्या में इमेजेज़ को प्रोसेस कर सकेगा। कोई अतिरिक्त स्क्रिप्ट नहीं, कोई मैन्युअल कॉपी‑पेस्ट नहीं—सिर्फ कोड जो आपके लिए भारी काम कर देगा।

## आपको क्या चाहिए

- **.NET 6.0** या बाद का संस्करण (कोड .NET Framework पर भी ठीक चलता है)।  
- **Aspose.OCR for .NET** NuGet पैकेज (टेस्टिंग के लिए फ्री ट्रायल काम करता है)।  
- एक फ़ोल्डर जिसमें कुछ *.png* फ़ाइलें हों जिन्हें आप OCR करना चाहते हैं।  
- Visual Studio 2022 या कोई भी C# IDE जो आपको पसंद हो।

यदि आपके पास ये सब है, तो हम सीधे इम्प्लीमेंटेशन की ओर बढ़ सकते हैं।

## चरण 1 – इनपुट और आउटपुट फ़ोल्डर तैयार करें *(Read PNG Directory)*

सबसे पहले हमें प्रोग्राम को उस फ़ोल्डर की ओर इशारा करना है जिसमें इमेजेज़ हैं और यह तय करना है कि परिणामी *.txt* फ़ाइलें कहाँ रखी जाएँगी। `Directory.GetFiles` का उपयोग करके हम डायरेक्टरी में मौजूद हर PNG का साफ़ एनेरेबल प्राप्त कर लेते हैं।

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**यह क्यों महत्वपूर्ण है:**  
- वाइल्डकार्ड (`*.png`) का उपयोग यह सुनिश्चित करता है कि हम केवल इमेज फ़ाइलों को प्रोसेस करें, बाकी किसी भी अनचाही फ़ाइल को नजरअंदाज़ करें।  
- आउटपुट फ़ोल्डर को रन‑टाइम पर बनाना बाद में `DirectoryNotFoundException` से बचाता है।

> **प्रो टिप:** यदि आपको अन्य फ़ॉर्मैट (JPEG, BMP) भी सपोर्ट करने हैं, तो सर्च पैटर्न को विस्तारित करें या `Directory.EnumerateFiles` को कई एक्सटेंशन के साथ कॉल करें।

## चरण 2 – OCR इंजन को इनिशियलाइज़ करें *(Convert Images to Text)*

Aspose.OCR दो प्रकार के इंजन प्रदान करता है: CPU‑आधारित `OcrEngine` और GPU‑त्वरित `GpuOcrEngine`। अधिकांश बैच जॉब्स के लिए CPU इंजन पर्याप्त है, लेकिन यदि आपके पास सक्षम GPU है तो क्लास नाम बदलकर आप इसे उपयोग कर सकते हैं।

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**यह क्यों महत्वपूर्ण है:**  
- भाषा निर्दिष्ट करने से सटीकता में काफी सुधार आता है क्योंकि इंजन को पता होता है कि कौन सा कैरेक्टर सेट अपेक्षित है।  
- यदि बड़े बैच में प्रदर्शन बाधा आती है तो `GpuOcrEngine` में स्विच करना सिर्फ एक‑लाइन का बदलाव है।

## चरण 3 – बैच रिकग्नाइज़र बनाएं

Aspose एक सुविधाजनक `BatchRecognizer` प्रदान करता है जो फ़ाइल पाथ्स के एनेरेबल को स्वीकार करता है और परिणामों को एक‑एक करके स्ट्रीम करता है। यह सभी इमेजेज़ को एक साथ मेमोरी में लोड करने से बचाता है—बड़े फ़ोल्डरों के लिए यह एक अहम बात है।

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**यह क्यों महत्वपूर्ण है:**  
- बैच रिकग्नाइज़र लूप लॉजिक को एन्कैप्सुलेट करता है, जिससे हमें प्रत्येक परिणाम के साथ क्या करना है इस पर ध्यान देना आसान हो जाता है, न कि सुरक्षित इटरेशन कैसे करें।

## चरण 4 – सभी इमेजेज़ पर OCR चलाएँ और आउटपुट लिखें *(Write Recognized Text)*

अब हम वास्तव में OCR करते हैं। `Recognize` मेथड एक `IEnumerable<RecognitionResult>` लौटाता है जहाँ प्रत्येक परिणाम में निकाला गया टेक्स्ट और अन्य मेटाडेटा होते हैं।

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**यह क्यों महत्वपूर्ण है:**  
- `File.WriteAllText` का उपयोग करने से टेक्स्ट डिफ़ॉल्ट रूप से UTF‑8 एन्कोडिंग के साथ सेव हो जाता है, जिससे विशेष अक्षर सुरक्षित रहते हैं।  
- क्रमिक नामकरण (`out_0.txt`, `out_1.txt`) प्रोसेसिंग क्रम से मेल खाता है, जो डिबगिंग में मददगार है।

> **एज केस:** यदि कोई इमेज OCR नहीं हो पाती (जैसे करप्ट फ़ाइल), तो `RecognitionResult.Text` खाली रहेगा। आप लूप के अंदर एक साधा चेक जोड़कर फेल्योर को लॉग कर सकते हैं:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## चरण 5 – सब कुछ एक साथ रखें – पूर्ण कार्यशील उदाहरण

नीचे पूरा प्रोग्राम दिया गया है जिसे आप नई कंसोल प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं। इसमें `using` निर्देश, फ़ोल्डर वैलिडेशन, और एक छोटा कंसोल UI शामिल है जिससे आपको पता चलेगा कि बैच कब समाप्त हुआ।

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**अपेक्षित आउटपुट:**  
प्रोग्राम चलाने पर कुछ इस तरह का संदेश दिखेगा:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

और आप आउटपुट फ़ोल्डर के अंदर `out_0.txt` … `out_11.txt` देखेंगे, प्रत्येक फ़ाइल में उसकी संबंधित इमेज का प्लेन‑टेक्स्ट संस्करण होगा।

## सामान्य प्रश्न और टिप्स

| प्रश्न | उत्तर |
|----------|--------|
| *क्या मैं सब‑फ़ोल्डर्स को भी OCR कर सकता हूँ?* | हाँ—`Directory.GetFiles` को `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)` से बदल दें। |
| *यदि मुझे कोई अलग भाषा चाहिए तो?* | `ocrEngine.Language = Language.Spanish;` (या कोई भी सपोर्टेड एन्‍युम) सेट करें। |
| *हजारों फ़ाइलों वाले बड़े बैच को कैसे संभालें?* | चंक्स में प्रोसेस करने या `Parallel.ForEach` के साथ थ्रॉटल्ड डिग्री ऑफ़ पैरालेलिज़्म उपयोग करने पर विचार करें, ताकि मेमोरी खत्म न हो। |
| *क्या आउटपुट हमेशा UTF‑8 रहता है?* | `File.WriteAllText` डिफ़ॉल्ट रूप से BOM‑रहित UTF‑8 देता है, जो अधिकांश लैटिन‑आधारित भाषाओं के लिए ठीक है। एशियाई स्क्रिप्ट्स के लिए आपको स्पष्ट रूप से `Encoding.UTF8` सेट करना पड़ सकता है। |
| *क्या मैं कॉन्फिडेंस स्कोर प्राप्त कर सकता हूँ?* | `RecognitionResult` में `Confidence` उपलब्ध है—आप इसे टेक्स्ट के साथ लॉग करके क्वालिटी कंट्रोल कर सकते हैं। |

## विज़ुअल ओवरव्यू *(How to Batch OCR – Diagram)*

![PNG फ़ोल्डर → OCR इंजन → बैच रिकग्नाइज़र → आउटपुट txt फ़ाइलें दिखाते हुए बैच OCR वर्कफ़्लो डायग्राम](https://example.com/diagram-how-to-batch-ocr.png "बैच OCR कैसे करें")

*Alt टेक्स्ट में मुख्य कीवर्ड शामिल है, जिससे SEO इमेज आवश्यकताओं को पूरा किया गया है।*

## निष्कर्ष

हमने अभी-अभी **कैसे एक डायरेक्टरी की PNG फ़ाइलों को बैच OCR** किया, Aspose.OCR का उपयोग करके, PNG डायरेक्टरी को पढ़ने से लेकर प्रत्येक पहचाने गए टेक्स्ट फ़ाइल को लिखने तक। यह समाधान पूरी तरह से स्व-निहित है, किसी भी आधुनिक .NET रनटाइम पर काम करता है, और GPU एक्सेलेरेशन, मल्टी‑लैंग्वेज सपोर्ट, या पैरालेल प्रोसेसिंग के लिए विस्तारित किया जा सकता है।

अगला कदम उठाने के लिए तैयार हैं? `Language.Latin` को किसी अन्य भाषा से बदलें, या आउटपुट को सर्च इंडेक्स में इंटीग्रेट करें ताकि आपके दस्तावेज़ तुरंत सर्चेबल बन जाएँ। बैच OCR में महारत हासिल करने के बाद संभावनाएँ असीमित हैं।

हैप्पी कोडिंग, और यदि कोई समस्या आती है तो कमेंट्स में बताइए!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}