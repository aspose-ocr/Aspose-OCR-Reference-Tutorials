---
category: general
date: 2026-01-15
description: Aspose OCR का उपयोग करके C# में छवि को JSON में बदलें। सीखें कि छवि से
  टेक्स्ट कैसे निकालें, JSON बाउंडिंग बॉक्स प्राप्त करें और रसीद की छवि को पहचानें।
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: hi
og_description: C# में Aspose OCR का उपयोग करके छवि को JSON में बदलें। छवि से टेक्स्ट
  निकालने, रसीद की छवि को पहचानने और JSON बाउंडिंग बॉक्स प्राप्त करने के लिए चरण‑दर‑चरण
  गाइड।
og_title: Aspose OCR C# गाइड के साथ इमेज को JSON में बदलें
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Aspose OCR C# गाइड के साथ छवि को JSON में परिवर्तित करें
url: /hi/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR C# गाइड के साथ इमेज को JSON में बदलें

क्या आपको कभी **इमेज को JSON में बदलने** की ज़रूरत पड़ी है लेकिन आप सुनिश्चित नहीं थे कि कौन सी लाइब्रेरी आपको कच्चा टेक्स्ट और सटीक शब्द निर्देशांक दोनों दे सके? आप अकेले नहीं हैं। कई डेवलपर्स इस समस्या का सामना करते हैं जब वे इमेज फ़ाइलों—विशेषकर रसीदों—से टेक्स्ट निकालने की कोशिश करते हैं, साथ ही डाउनस्ट्रीम प्रोसेसिंग के लिए मशीन‑रीडेबल JSON पेलोड की भी आवश्यकता होती है।

इस ट्यूटोरियल में हम एक पूर्ण **Aspose OCR C# उदाहरण** के माध्यम से दिखाएंगे कि कैसे इमेज से टेक्स्ट निकाला जाए, रसीद इमेज को पहचानें, और प्रत्येक शब्द के लिए **JSON बाउंडिंग बॉक्स** आउटपुट किया जाए। अंत तक आपके पास एक तैयार‑चलाने‑योग्य कंसोल ऐप होगा जो एक सुंदर फ़ॉर्मेटेड JSON स्ट्रिंग प्रिंट करेगा जिसे आप किसी भी API, डेटाबेस, या एनालिटिक्स पाइपलाइन में फीड कर सकते हैं।

> **आपको क्या मिलेगा**  
> • एक पूरी तरह कार्यात्मक C# प्रोजेक्ट जो **इमेज को JSON में बदलता** है  
> • यह समझ कि हम `IncludeBoundingBoxes` क्यों सक्षम करते हैं (यह `json bounding boxes` की कुंजी है)  
> • विभिन्न इमेज फ़ॉर्मेट और भाषाओं को संभालने के टिप्स  

चलिए शुरू करते हैं।

---

## आपको क्या चाहिए

- **.NET 6.0 SDK** (या कोई भी बाद का संस्करण) – कोड .NET 6 को टारगेट करता है लेकिन .NET Framework 4.7+ पर भी काम करता है।  
- **Aspose.OCR for .NET** NuGet पैकेज – आप इसे `dotnet add package Aspose.OCR` के ज़रिए जोड़ सकते हैं।  
- एक सैंपल रसीद इमेज (`receipt.jpg`) जिसे आप अपने प्रोजेक्ट से रेफ़रेंस कर सकें।  
- Visual Studio 2022, VS Code, या कोई भी IDE जो आप पसंद करते हैं।

कोई अन्य बाहरी सेवा आवश्यक नहीं है; सब कुछ स्थानीय रूप से चलता है।

## इमेज को JSON में बदलें – अवलोकन

मुख्य विचार सरल है: इमेज लोड करें, Aspose OCR को इंग्लिश (या कोई भी समर्थित भाषा) पहचानने को कहें, बाउंडिंग बॉक्स शामिल करने को कहें, और अंत में परिणाम **JSON** फ़ॉर्मेट में माँगें। लाइब्रेरी सभी भारी काम करती है—OCR, लेआउट एनालिसिस, और JSON सीरियलाइज़ेशन।

यहाँ फ्लो का एक हाई‑लेवल डायग्राम है (एक छोटा चित्र कल्पना करें):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

यह छोटा डायग्राम पूरी पाइपलाइन को दर्शाता है जिसे हम लागू करेंगे।

## चरण 1: प्रोजेक्ट सेट अप करें और Aspose OCR इंस्टॉल करें

सबसे पहले, एक नया कंसोल प्रोजेक्ट बनाएं और Aspose OCR पैकेज को जोड़ें।

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **प्रो टिप:** यदि आप Visual Studio उपयोग कर रहे हैं, तो प्रोजेक्ट पर राइट‑क्लिक → *Manage NuGet Packages* → **Aspose.OCR** खोजें और नवीनतम स्थिर संस्करण (वर्तमान में 23.12) इंस्टॉल करें।

## चरण 2: वह इमेज लोड करें जिसे आप पहचानना चाहते हैं

हम `OcrImage.FromFile` मेथड का उपयोग करके रसीद इमेज पढ़ेंगे। सुनिश्चित करें कि पाथ एक वास्तविक फ़ाइल की ओर इशारा कर रहा है; अन्यथा आपको `FileNotFoundException` मिलेगा।

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

यदि आपकी इमेज `.csproj` के बगल में रखी है, तो आप बस `"receipt.jpg"` का उपयोग कर सकते हैं।

## चरण 3: JSON बाउंडिंग बॉक्स के लिए OCR विकल्प कॉन्फ़िगर करें

जादू तब होता है जब हम `OutputFormat = OutputFormat.Json` **और** `IncludeBoundingBoxes = true` को सक्षम करते हैं। पहला Aspose को परिणाम JSON के रूप में सीरियलाइज़ करने को बताता है, जबकि दूसरा प्रत्येक शब्द के लिए `x`, `y`, `width`, और `height` जोड़ता है—बिल्कुल वही जो आपको `json bounding boxes` के लिए चाहिए।

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

आप `ocrOptions.Dpi` या `ocrOptions.Language` को भी समायोजित कर सकते हैं यदि आपको उच्च रेज़ॉल्यूशन या अलग भाषा चाहिए।

## चरण 4: पहचान निष्पादित करें – इमेज से टेक्स्ट निकालें

अब हम `Recognize` को कॉल करते हैं। यह मेथड एक `OcrResult` ऑब्जेक्ट रिटर्न करता है जिसमें JSON स्ट्रिंग, कच्चा टेक्स्ट, और अधिक शामिल है।

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

यदि आपको अन्य भाषाओं को संभालना है, तो `Language.English` को `Language.Spanish`, `Language.French` आदि से बदलें। Aspose बॉक्स 30 से अधिक भाषाओं को सपोर्ट करता है।

## चरण 5: परिणाम आउटपुट करें – आपका JSON पेलोड

अंत में, हम JSON को कंसोल में प्रिंट करते हैं। वास्तविक ऐप में आप इसे फ़ाइल में लिख सकते हैं या किसी सर्विस को भेज सकते हैं।

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

प्रोग्राम चलाने पर नीचे दिखाए गए स्निपेट जैसा JSON दस्तावेज़ उत्पन्न होना चाहिए।

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

ध्यान दें कि अब प्रत्येक शब्द के साथ उसका **JSON बाउंडिंग बॉक्स** जुड़ा हुआ है—UI ओवरले या डाउनस्ट्रीम पार्सर में फीड करने के लिए परफेक्ट।

## पूर्ण कार्यशील उदाहरण

नीचे पूरी, कॉपी‑पेस्ट‑तैयार प्रोग्राम है। कोई छिपे हुए भाग नहीं, कोई बाहरी कॉल नहीं—सिर्फ शुद्ध C#।

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **ध्यान रखें:**  
> • **फ़ाइल पाथ त्रुटियाँ** – इमेज लोकेशन दोबारा जांचें।  
> • **NuGet पैकेज गायब** – सुनिश्चित करें `Aspose.OCR` रेफ़रेंस किया गया है।  
> • **असमर्थित इमेज फ़ॉर्मेट** – सर्वोत्तम परिणामों के लिए JPEG, PNG, BMP, या TIFF का उपयोग करें।

## सामान्य प्रश्न और किनारे के मामले

### क्या मैं JPEG की बजाय **PDF पेज** को JSON में बदल सकता हूँ?

हां। पहले PDF पेज को इमेज में बदलें (जैसे `Aspose.PDF` का उपयोग करके), फिर उसी OCR पाइपलाइन में फीड करें। JSON आउटपुट वही रहेगा क्योंकि OCR चरण केवल रास्टर डेटा देखता है।

### अगर रसीद धुंधली हो तो क्या करें?

`ocrOptions` में DPI बढ़ाएँ। उदाहरण के लिए:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

उच्च DPI मेमोरी उपयोग बढ़ा सकता है, इसलिए गुणवत्ता और प्रदर्शन के बीच संतुलन रखें।

### मुझे रसीद पर **एकाधिक भाषाएँ** चाहिए (जैसे इंग्लिश + स्पेनिश)।

आप भाषा की एरे पास कर सकते हैं:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose निर्दिष्ट क्रम में प्रत्येक भाषा को पहचानने की कोशिश करेगा।

### JSON को फ़ाइल में कैसे लिखूँ?

`Console.WriteLine` लाइन को इस तरह बदलें:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

अब आपके पास एक स्थायी फ़ाइल होगी जिसे आप अन्य सर्विसेज़ को भेज सकते हैं।

## दृश्य सारांश

![इमेज को JSON में बदलने का उदाहरण](convert-image-to-json.png "इमेज को JSON में बदलने का उदाहरण")

*स्क्रीनशॉट में डेमो चलाने के बाद कंसोल आउटपुट में JSON पेलोड दिखाया गया है।*

## निष्कर्ष

हमने अभी-अभी दिखाया कि कैसे Aspose OCR का उपयोग करके C# में **इमेज को JSON में बदला** जा सकता है। `OutputFormat` और `IncludeBoundingBoxes` को कॉन्फ़िगर करके आप **इमेज से टेक्स्ट निकाल सकते** हैं, **रसीद इमेज को पहचान सकते** हैं, और प्रत्येक शब्द के लिए सटीक **JSON बाउंडिंग बॉक्स** प्राप्त कर सकते हैं। ऊपर दिया गया पूर्ण, चलाने योग्य कोड स्निपेट आपको तुरंत किसी भी .NET प्रोजेक्ट में डालने के लिए तैयार है।

अब आगे क्या? इस JSON को एक फ्रंट‑एंड व्यूअर में फीड करें जो प्रत्येक शब्द को हाईलाइट करे, या डेटा को मशीन‑लर्निंग मॉडल में भेजें जो रसीदों पर लाइन आइटम क्लासिफ़ाई करे। आप अन्य भाषाओं, उच्च DPI सेटिंग्स, या कई इमेज को लूप में बैच‑प्रोसेस करने के साथ भी प्रयोग कर सकते हैं।

यदि आपको कोई समस्या आती है, तो फ़ाइल पाथ, DPI, और भाषा एरे के बारे में टिप्स याद रखें। इस डेमो के लिए आप अपना GitHub रेपो बना सकते हैं, टिप्पणी छोड़ सकते हैं या इश्यू खोल सकते हैं। कोडिंग का आनंद लें, और तस्वीरों को संरचित JSON में बदलने का मज़ा उठाएँ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}