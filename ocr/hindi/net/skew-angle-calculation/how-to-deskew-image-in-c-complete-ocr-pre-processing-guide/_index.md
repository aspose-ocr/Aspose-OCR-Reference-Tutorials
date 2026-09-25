---
category: general
date: 2026-01-10
description: Aspose.OCR के साथ छवि को डेस्क्यू कैसे करें और OCR परिणामों में सुधार
  करें। OCR के लिए छवि को पूर्व-प्रसंस्करण करना सीखें, स्कैन से शोर हटाएँ, और स्कैन
  से पाठ को पहचानें।
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from scan
- how to use ocr
- remove noise from scan
language: hi
og_description: इमेज को डेस्क्यू कैसे करें और OCR की सटीकता बढ़ाएँ। यह गाइड दिखाता
  है कि OCR के लिए इमेज को कैसे प्री‑प्रोसेस करें, स्कैन से शोर हटाएँ, और Aspose.OCR
  का उपयोग करके स्कैन से टेक्स्ट को पहचानें।
og_title: C# में इमेज को डेस्क्यू कैसे करें – पूर्ण OCR प्री‑प्रोसेसिंग गाइड
tags:
- OCR
- C#
- Image Processing
title: C# में छवि को डेस्क्यू कैसे करें – पूर्ण OCR प्री‑प्रोसेसिंग गाइड
url: /hi/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में इमेज को डेस्क्यू कैसे करें – पूर्ण OCR प्री‑प्रोसेसिंग गाइड

क्या आपने कभी **इमेज को डेस्क्यू** करने के बारे में सोचा है इससे पहले कि आप उन्हें OCR इंजन को दें? आप अकेले नहीं हैं। स्कैन किए गए दस्तावेज़ अक्सर तिरछे, शोरयुक्त, या कम‑कॉन्ट्रास्ट होते हैं, और यह किसी भी टेक्स्ट‑रिकग्निशन प्रयास को बिगाड़ देता है।  

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से जाएंगे जो **OCR के लिए इमेज को प्री‑प्रोसेस** करता है, स्कैन से शोर हटाता है, और अंत में Aspose.OCR लाइब्रेरी का उपयोग करके **स्कैन से टेक्स्ट को पहचानें** है। अंत तक आपके पास C# में **OCR का उपयोग कैसे करें** की स्पष्ट समझ होगी, जबकि कोड छोटा और सरल रहेगा।

> **Pro tip:** यहाँ तक कि एक छोटा रोटेशन (5‑10°) भी OCR की सटीकता को 30 % या अधिक घटा सकता है। डेस्क्यूइंग वह पहला कदम है जिसे आपको कभी नहीं छोड़ना चाहिए।

## आपको क्या चाहिए

- **.NET 6+** (कोड .NET Framework पर भी काम करता है, लेकिन .NET 6 वर्तमान LTS है)
- **Aspose.OCR for .NET** – आप इसे NuGet से प्राप्त कर सकते हैं (`Install-Package Aspose.OCR`)
- एक नमूना TIFF/PNG/JPEG जो घुमा हुआ या शोरयुक्त हो (हम उदाहरण में `noisy_rotated.tif` का उपयोग करेंगे)
- कोई भी IDE जो आपको पसंद हो – Visual Studio, Rider, या VS Code चलेगा

बस इतना ही। कोई अतिरिक्त लाइब्रेरी नहीं, कोई बाहरी सेवा नहीं।

## चरण 1 – स्रोत इमेज लोड करें (यह क्यों महत्वपूर्ण है)

इमेज को **डेस्क्यू** करने से पहले, हमें इसे Aspose `ImageStream` में पढ़ना होगा। यह ऑब्जेक्ट फ़ाइल I/O को एब्स्ट्रैक्ट करता है और OCR इंजन को एक सुसंगत इंटरफ़ेस प्रदान करता है।

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the original scan – replace the path with your own file
var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");

// Quick sanity check – make sure the image loaded
if (sourceImage == null)
{
    Console.WriteLine("Failed to load the image. Check the path and file permissions.");
    return;
}
```

*पहले लोड क्यों करें?* क्योंकि सभी बाद के फ़िल्टर मेमोरी में मौजूद इमेज पर काम करते हैं। यदि फ़ाइल पढ़ी नहीं जा सकती, तो पूरी पाइपलाइन विफल हो जाती है।

## चरण 2 – प्री‑प्रोसेसिंग पाइपलाइन बनाएं (Deskew + Denoise + Contrast)

एक मजबूत OCR वर्कफ़्लो आमतौर पर कई फ़िल्टरों को जोड़ता है। यहाँ हम **OCR के लिए इमेज को प्री‑प्रोसेस** करते हैं और, उससे भी अधिक महत्वपूर्ण, **इमेज को डेस्क्यू** स्वचालित रूप से करते हैं।

```csharp
// Create a pipeline that will run three filters in order
var preprocessPipeline = new PreprocessPipeline()
{
    // 1️⃣ DeskewFilter – detects rotation up to 30° and corrects it
    new DeskewFilter { MaxAngle = 30 },

    // 2️⃣ DenoiseFilter – smooths out speckles while keeping edges
    new DenoiseFilter { Strength = 0.8 },

    // 3️⃣ ContrastBoostFilter – makes faint characters pop
    new ContrastBoostFilter { Level = 1.3 }
};
```

**इन तीनों का चयन क्यों?**  
- **DeskewFilter** “इमेज को डेस्क्यू कैसे करें” समस्या को स्वचालित रूप से हल करता है; आपको कोण का अनुमान लगाने की आवश्यकता नहीं है।  
- **DenoiseFilter** “स्कैन से शोर हटाएँ” की आवश्यकता को पूरा करता है, जो अन्यथा भ्रामक अक्षर बनाता है।  
- **ContrastBoostFilter** OCR इंजन को गहरे टेक्स्ट को हल्के बैकग्राउंड से अलग करने में मदद करता है, जो एक क्लासिक समस्या है जब आप *OCR के लिए इमेज को प्री‑प्रोसेस* करते हैं।

## चरण 3 – पाइपलाइन लागू करें (परिवर्तन देखना)

अब हम वास्तव में फ़िल्टर चलाते हैं। लौटाया गया `processedImage` वही है जिसे हम OCR इंजन को देंगे।

```csharp
// Apply all filters – the result is a cleaned‑up bitmap
var processedImage = preprocessPipeline.Apply(sourceImage);

// Optional: Save the cleaned image for visual verification
processedImage.Save("cleaned_output.tif");
Console.WriteLine("Image preprocessing complete – cleaned_output.tif saved.");
```

यदि आप `cleaned_output.tif` खोलते हैं, तो आपको दिखेगा कि टेक्स्ट सीधा है, कम दानेदार है, और अधिक कॉन्ट्रास्ट वाला है। यह दृश्य जांच उपयोगी है जब आप *स्कैन से शोर हटाएँ* और यह पुष्टि करना चाहते हैं कि डेस्क्यू काम किया।

## चरण 4 – OCR इंजन बनाएं और कॉन्फ़िगर करें (OCR का उपयोग कैसे करें)

एक साफ़ इमेज हाथ में होने पर, हम `OcrEngine` को इंस्टैंशिएट करते हैं। यह Aspose के साथ **OCR का उपयोग कैसे करें** का मुख्य भाग है।

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    // Assign the pre‑processed image
    Image = processedImage,

    // Optional: Set language (English is default)
    // Language = Language.English,
    
    // Enable automatic page segmentation (helps with multi‑column scans)
    AutoPageSegmentation = true
};
```

*`AutoPageSegmentation` सेट क्यों करें?* क्योंकि कई स्कैन में टेबल या कई कॉलम होते हैं। इसे ऑन करने से इंजन पेज को बुद्धिमानी से विभाजित कर सकता है, जिससे अंतिम **स्कैन से टेक्स्ट को पहचानें** परिणाम सुधरता है।

## चरण 5 – पहचान प्रक्रिया चलाएँ (अंत में टेक्स्ट पहचानें)

अब सच्चाई का क्षण: हम इंजन से टेक्स्ट पढ़ने को कहते हैं।

```csharp
// Kick off the OCR process
ocrEngine.Recognize();

// Retrieve the plain‑text result
string recognizedText = ocrEngine.Text;

// Show the output in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

यदि सब कुछ सुचारू रूप से चला, तो आप एक साफ़ टेक्स्ट ब्लॉक देखेंगे जो मूल दस्तावेज़ से मेल खाता है। यह सही तरीके से **इमेज को डेस्क्यू**, **शोर हटाने**, और **OCR के लिए इमेज को प्री‑प्रोसेस** करने का परिणाम है।

## चरण 6 – पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम दिया गया है, जिसे कंपाइल करने के लिए तैयार है। केवल फ़ाइल पाथ बदलें और आप तैयार हैं।

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");
        if (sourceImage == null)
        {
            Console.WriteLine("Unable to load image. Check the path.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Build the preprocessing pipeline
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
        {
            new DeskewFilter { MaxAngle = 30 },          // how to deskew image
            new DenoiseFilter { Strength = 0.8 },       // remove noise from scan
            new ContrastBoostFilter { Level = 1.3 }      // improves OCR accuracy
        };

        // -------------------------------------------------
        // 3️⃣ Apply the pipeline
        // -------------------------------------------------
        var processedImage = preprocessPipeline.Apply(sourceImage);
        processedImage.Save("cleaned_output.tif");
        Console.WriteLine("Preprocessing finished – cleaned_output.tif saved.");

        // -------------------------------------------------
        // 4️⃣ Configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Image = processedImage,
            AutoPageSegmentation = true   // how to use OCR effectively
        };

        // -------------------------------------------------
        // 5️⃣ Recognize text from scan
        // -------------------------------------------------
        ocrEngine.Recognize();
        string result = ocrEngine.Text;

        Console.WriteLine("\n=== Recognized Text ===");
        Console.WriteLine(result);
    }
}
```

**अपेक्षित आउटपुट** (संक्षिप्त रूप में):

```
=== Recognized Text ===
This is a sample scanned document.
It contains several lines of text,
and the OCR engine has correctly read them.
```

यदि आउटपुट गड़बड़ दिखे, तो दोबारा जांचें कि स्रोत इमेज 30° से अधिक घुमा नहीं है, या `DeskewFilter.MaxAngle` बढ़ाएँ।

## अक्सर पूछे जाने वाले प्रश्न (एज केस और विविधताएँ)

| Question | Answer |
|----------|--------|
| **अगर मेरा स्कैन 45° घुमा हुआ है तो क्या करें?** | `DeskewFilter` `MaxAngle` पर सीमित रहता है। इसे बढ़ाएँ (जैसे, `MaxAngle = 60`) या पाइपलाइन में फीड करने से पहले ग्राफ़िक्स लाइब्रेरी से इमेज को पहले‑घुमा दें। |
| **क्या मैं PDFs को पेज‑बाय‑पेज प्रोसेस कर सकता हूँ?** | हां। प्रत्येक PDF पेज को इमेज में बदलें (जैसे, `Aspose.Pdf` का उपयोग करके) और हर बिटमैप पर वही पाइपलाइन चलाएँ। |
| **मेरे दस्तावेज़ फ्रेंच में हैं – क्या मुझे कुछ बदलना चाहिए?** | `ocrEngine.Language = Language.French;` सेट करें या एक कस्टम भाषा पैक लोड करें। पाइपलाइन का बाकी हिस्सा वही रहता है। |
| **क्या मूल रिज़ॉल्यूशन को बनाए रखने का कोई तरीका है?** | `PreprocessPipeline` मूल बिटमैप पर काम करता है, DPI को संरक्षित रखता है। केवल तब `ImageStream.Resize` कॉल करने से बचें जब आपको प्रदर्शन के लिए डाउनस्केल करने की आवश्यकता हो। |
| **कॉन्ट्रास्ट बूस्टिंग रंगीन स्कैन को कैसे प्रभावित करता है?** | `ContrastBoostFilter` प्रत्येक चैनल पर काम करता है; यह ग्रेस्केल या कलर इमेज दोनों के लिए सुरक्षित है, लेकिन आप पहले `new GrayscaleFilter()` से ग्रेस्केल में भी बदल सकते हैं। |

## इमेज उदाहरण (विज़ुअल सहायता)

![इमेज को डेस्क्यू करने का उदाहरण](/images/deskew-example.png)

*यह चित्र 12° घुमा हुआ, शोरयुक्त स्कैन का पहले/बाद दिखाता है जिसे डेस्क्यू और साफ़ किया गया है।*

## निष्कर्ष

हमने Aspose.OCR का उपयोग करके **इमेज को डेस्क्यू** करने को कवर किया, एक पूर्ण **OCR के लिए इमेज को प्री‑प्रोसेस** पाइपलाइन दिखायी, **स्कैन से शोर हटाने** का तरीका बताया, और अंत में कुछ लाइनों के C# कोड से **स्कैन से टेक्स्ट को पहचानें**। `DeskewFilter`, `DenoiseFilter`, और `ContrastBoostFilter` को जोड़कर आप एक साफ़ बिटमैप प्राप्त करते हैं जो OCR इंजन को बिना किसी आर्टिफैक्ट के काम करने देता है।  

अगले कदम? विभिन्न फ़िल्टर स्ट्रेंथ के साथ प्रयोग करें, शुद्ध ब्लैक‑एंड‑व्हाइट आउटपुट के लिए `BinarizationFilter` जोड़ें, या साफ़ की गई इमेज को डाउनस्ट्रीम NLP पाइपलाइन में फीड करें। यही पैटर्न रसीदों, पासपोर्ट और ऐतिहासिक दस्तावेज़ों के लिए भी काम करता है।  

क्या आपके पास अन्य भाषाओं या फ्रेमवर्क में **OCR का उपयोग कैसे करें** के बारे में और प्रश्न हैं? टिप्पणी छोड़ें, और कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}