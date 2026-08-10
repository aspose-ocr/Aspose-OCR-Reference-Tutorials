---
category: general
date: 2026-03-20
description: Aspose OCR के साथ छवि को डेस्क्यू करने और छवि शोर को हटाने के तरीके सीखें।
  यह चरण‑दर‑चरण गाइड यह भी दिखाता है कि OCR के लिए छवि को कैसे पूर्व‑प्रसंस्करण किया
  जाए और OCR की सटीकता को कैसे बढ़ाया जाए।
draft: false
keywords:
- how to deskew image
- remove image noise
- preprocess image for OCR
- recognize text from image
- improve OCR accuracy
language: hi
og_description: Aspose OCR के साथ छवि को डेस्क्यू करना और शोर को साफ़ करना सीखें।
  कुछ ही मिनटों में अपनी OCR सटीकता बढ़ाएँ।
og_title: छवि को डेस्क्यू कैसे करें – OCR पूर्व‑प्रसंस्करण के लिए पूर्ण C# गाइड
tags:
- OCR
- C#
- Image Processing
title: छवि को डेस्क्यू कैसे करें – OCR प्री‑प्रोसेसिंग के लिए संपूर्ण C# गाइड
url: /hi/net/ocr-optimization/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज को डेस्क्यू कैसे करें – OCR प्री‑प्रोसेसिंग के लिए पूर्ण C# गाइड

क्या आपने कभी **इमेज को डेस्क्यू कैसे करें** उन फ़ाइलों के बारे में सोचा है जो स्कैनर से अजीब कोण पर निकली थीं? आप अकेले नहीं हैं; कई डेवलपर्स को यह समस्या आती है जब वे फ़ोटो को OCR इंजन में फ़ीड करने की कोशिश करते हैं। अच्छी खबर यह है कि कुछ ही पंक्तियों के C# और Aspose OCR के साथ आप इमेज को सीधा, शोर‑मुक्त और कंट्रास्ट बढ़ा सकते हैं—फ़ोटोशॉप की ज़रूरत नहीं।

इस ट्यूटोरियल में हम हर चीज़ को कवर करेंगे: स्क्यूड तस्वीर को लोड करने से लेकर **remove image noise**, **preprocess image for OCR**, और अंत में **recognize text from image** तक, साथ ही उच्च **improve OCR accuracy** स्कोर के साथ। अंत तक आपके पास एक तैयार‑चलाने‑योग्य कंसोल ऐप होगा जो गंदे स्कैन को साफ़, खोज योग्य टेक्स्ट में बदल देगा।

## आपको क्या चाहिए

- .NET 6 या बाद का (कोड `using var` सिंटैक्स का उपयोग करता है, जो C# 8 से समर्थित है)
- Aspose OCR NuGet पैकेज (`Aspose.OCR`) – `dotnet add package Aspose.OCR` के ज़रिए इंस्टॉल करें
- एक सैंपल इमेज जो स्क्यूड और नॉइज़ी दोनों हो (जैसे, `skewed_noisy.png`)
- आपका पसंदीदा IDE या एडिटर (Visual Studio, VS Code, Rider… आप चुनें)

> **Pro tip:** यदि आपके पास सैंपल फ़ाइल नहीं है, तो एक स्पष्ट स्क्रीनशॉट को कुछ डिग्री घुमा दें और इमेज एडिटर से “सॉल्ट‑एंड‑पेपर” शोर जोड़ें। पाइपलाइन उसी तरह काम करेगी।

## चरण 1: Deskew फ़िल्टर के साथ इमेज को डेस्क्यू कैसे करें

पहले हम रोटेशन को ठीक करते हैं। Aspose एक `DeskewFilter` प्रदान करता है जो कॉन्फ़िगरेबल `MaxAngle` तक के एंगल को स्वचालित रूप से डिटेक्ट कर सकता है। इसे **5°** पर सेट करना अधिकांश स्कैन किए गए दस्तावेज़ों के लिए सुरक्षित डिफ़ॉल्ट है।

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image class

// Initialize the OCR engine – English is the most common language
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};

// Build the preprocessing pipeline
var preprocessPipeline = new PreprocessPipeline()
    .Add(new DeskewFilter { MaxAngle = 5 })          // This is where we answer “how to deskew image”
    .Add(new DespeckleFilter { Strength = 2 })      // Next we’ll remove image noise
    .Add(new ContrastFilter { Level = 1.5 });        // Finally we boost contrast for OCR
```

**Why this matters:**  
यदि टेक्स्ट तिरछा है, तो OCR एल्गोरिद्म अक्षरों को गलत समझ सकता है—जैसे “l” को “i” समझना। पहले **डेस्क्यू** करके, आप इंजन को एक सीधी कैनवास देते हैं।

## चरण 2: Despeckle के साथ इमेज नॉइज़ हटाएँ

सस्ते फ़ोन या पुराने स्कैनर से स्कैन अक्सर ऐसे बिंदु दिखाते हैं जो यादृच्छिक डॉट्स की तरह लगते हैं। ये बिंदु कैरेक्टर रेकग्नाइज़र को भ्रमित करते हैं। `DespeckleFilter` इमेज को स्मूद करता है जबकि किनारों को बरकरार रखता है।

```csharp
// The DespeckleFilter is already part of the pipeline (see Step 1)
// Strength = 2 is a balanced setting; increase for very noisy pics
```

यदि आपको **remove image noise** अधिक आक्रामक रूप से चाहिए, तो `Strength` को 3 या 4 तक बढ़ाएँ—पर पतली स्ट्रोक्स के नुकसान का ध्यान रखें।

## चरण 3: OCR के लिए इमेज प्री‑प्रोसेस – कंट्रास्ट बूस्ट

लो‑कंट्रास्ट स्कैन (ह्ला ग्रे ऑन व्हाइट पेपर) OCR को फेड लेटर मिस करवा सकते हैं। `ContrastFilter` टोनल रेंज को स्ट्रेच करता है, जिससे डार्क पिक्सेल और डार्क और लाइट पिक्सेल और लाइट हो जाते हैं।

```csharp
// Contrast level of 1.5 is a good starting point.
// You can experiment with values between 1.0 (no change) and 2.0 (strong boost).
```

**Edge case:** यदि आपका स्रोत इमेज पहले से ही हाई‑कंट्रास्ट है, तो इस फ़िल्टर को लागू करने से विवरण धुंधला हो सकता है। ऐसे में `Level` को `1.0` सेट करें (प्रभावी रूप से इसे डिसेबल कर देता है)।

## चरण 4: स्रोत इमेज को लोड और साफ़ करें

अब हम वास्तव में तस्वीर को लोड करते हैं और उसे उस पाइपलाइन से चलाते हैं जो हमने अभी बनाई है।

```csharp
// Load the source image – replace the path with your own file location
var sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

// Apply the entire preprocessing pipeline
var cleanedImage = preprocessPipeline.Apply(sourceImage);
```

> **Note:** `Apply` मेथड एक नया `Image` ऑब्जेक्ट रिटर्न करता है; मूल अपरिवर्तित रहता है। यह “पहले” और “बाद” की तुलना को आसान बनाता है यदि आप प्रक्रिया को डिबग करना चाहते हैं।

## चरण 5: Aspose OCR का उपयोग करके इमेज से टेक्स्ट पहचानें

एक सीधी, नॉइज़‑फ्री, हाई‑कंट्रास्ट तस्वीर हाथ में होने पर, हम अंत में इसे OCR इंजन को सौंपते हैं।

```csharp
// Perform OCR on the cleaned image
var ocrResult = ocrEngine.Recognize(cleanedImage);

// Output the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**What you should see:** कंसोल मूल स्कैन की टेक्स्ट सामग्री प्रिंट करेगा, आमतौर पर बहुत कम मिस‑रिकग्निशन के साथ, बनिस्बत सीधे फ़ाइल फ़ीड करने के।

## चरण 6: OCR सटीकता को सत्यापित और सुधारें

एक ठोस पाइपलाइन के साथ भी कुछ अक्षर अभी भी गलत हो सकते हैं—ख़ासकर अगर मूल फ़ॉन्ट असामान्य हो। यहाँ कुछ तेज़ ट्रिक्स हैं **improve OCR accuracy** के लिए:

| समस्या | त्वरित समाधान |
|-------|-----------|
| छोटे विराम चिह्न गायब | कंट्रास्ट स्टेप से पहले `BinaryThresholdFilter` जोड़ें |
| मिश्रित भाषा (जैसे, English + Spanish) | `ocrEngine.Language = Language.English | Language.Spanish;` सेट करें |
| बहुत गहरा बैकग्राउंड | डेस्क्यू से पहले इमेज को इनवर्ट करें (`new InvertFilter()`) |
| बड़े दस्तावेज़ | पेजेज़ को समानांतर में प्रोसेस करें (`Parallel.ForEach`) ताकि गति बढ़े |

फ़िल्टरों के क्रम के साथ प्रयोग करें; कभी‑कभी **contrast** को **despeckle** से पहले लागू करने से लो‑क्वालिटी स्कैन पर बेहतर परिणाम मिलते हैं।

## पूरा कार्यशील उदाहरण

नीचे पूरा प्रोग्राम है जिसे आप नई कंसोल प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं। इसमें हमने चर्चा किए सभी हिस्से और कुछ सुरक्षा जाँचें शामिल हैं।

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine (English language)
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // -------------------------------------------------
        // 2️⃣ Build preprocessing pipeline:
        //    Deskew → Despeckle → Contrast Boost
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
            .Add(new DeskewFilter { MaxAngle = 5 })          // how to deskew image
            .Add(new DespeckleFilter { Strength = 2 })      // remove image noise
            .Add(new ContrastFilter { Level = 1.5 });        // preprocess image for OCR

        // -------------------------------------------------
        // 3️⃣ Load the source image (adjust path as needed)
        // -------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/skewed_noisy.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ File not found: {imagePath}");
            return;
        }

        var sourceImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // 4️⃣ Apply the pipeline → cleaned image
        // -------------------------------------------------
        var cleanedImage = preprocessPipeline.Apply(sourceImage);

        // -------------------------------------------------
        // 5️⃣ Recognize text (this is the “recognize text from image” step)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(cleanedImage);

        // -------------------------------------------------
        // 6️⃣ Output the result
        // -------------------------------------------------
        Console.WriteLine("\n=== OCR Output ===\n");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Expected output** (मान लीजिए सैंपल इमेज में “Hello World!” है):

```
=== OCR Output ===

Hello World!
```

यदि आप गड़बड़ अक्षर देखते हैं, तो पाइपलाइन क्रम को दोबारा जाँचें या `DespeckleFilter.Strength` को बढ़ाएँ।

## निष्कर्ष

हमने **इमेज को डेस्क्यू कैसे करें**, **remove image noise**, **preprocess image for OCR**, और अंत में **recognize text from image** को Aspose OCR का उपयोग करके कवर किया—साथ ही **improve OCR accuracy** पर भी ध्यान रखा। पूरा, चलाने योग्य उदाहरण हर कदम को संदर्भ में दिखाता है, इसलिए आप इसे किसी भी .NET प्रोजेक्ट में डाल सकते हैं और तुरंत टेक्स्ट निकालना शुरू कर सकते हैं।

अगली चुनौती के लिए तैयार हैं? पाइपलाइन को मल्टी‑पेज PDFs को हैंडल करने के लिए विस्तारित करें, या मल्टी‑लैंग्वेज दस्तावेज़ों के लिए लैंग्वेज पैक्स के साथ प्रयोग करें। वही अवधारणाएँ लागू होती हैं—बस `Language` फ़्लैग बदलें और शायद पेजेज़ को उल्टा करने के लिए `RotateFilter` जोड़ें।

कोई सवाल या ऐसी जटिल इमेज है जो अभी भी सहयोग नहीं कर रही? नीचे कमेंट डालें, और हम साथ में ट्रबलशूट करेंगे। Happy coding!

![इमेज को डेस्क्यू करने का उदाहरण](/images/deskew-example.png "Aspose OCR का उपयोग करके इमेज को डेस्क्यू करने का चित्रण")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}