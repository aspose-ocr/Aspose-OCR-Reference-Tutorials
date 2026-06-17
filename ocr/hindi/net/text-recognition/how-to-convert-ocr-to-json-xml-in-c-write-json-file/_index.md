---
category: general
date: 2026-04-01
description: C# में OCR आउटपुट को JSON और XML में कैसे बदलें – Aspose.OCR का उपयोग
  करके छवि से टेक्स्ट निकालना और C# में JSON फ़ाइल लिखना सीखें।
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: hi
og_description: C# के साथ OCR परिणामों को संरचित JSON और XML फ़ाइलों में कैसे बदलें।
  इमेज से टेक्स्ट निकालने और JSON फ़ाइल लिखने के लिए चरण‑दर‑चरण गाइड C#।
og_title: C# में OCR को JSON और XML में कैसे बदलें – JSON फ़ाइल लिखें
tags:
- OCR
- C#
- Aspose
title: C# में OCR को JSON और XML में कैसे बदलें – JSON फ़ाइल लिखें
url: /hi/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR को JSON और XML में C# – JSON फ़ाइल लिखें

**How to convert OCR** परिणामों को ऐसी चीज़ में बदलना जिसे आप वास्तव में उपयोग कर सकें, कई डेवलपर्स का सवाल है। इस गाइड में हम आपको दिखाएंगे कि कैसे एक छवि से टेक्स्ट निकालें, OCR आउटपुट को सुंदर फ़ॉर्मेटेड JSON और XML में बदलें, और फिर उन फ़ाइलों को C# के साथ डिस्क पर लिखें।

यदि आपने कभी कच्ची OCR स्ट्रिंग को देखा है और सोचा है, “इसे स्टोर करने का कोई बेहतर तरीका होना चाहिए,” तो आप सही जगह पर हैं। अंत तक आपके पास एक पूर्ण, चलाने योग्य प्रोग्राम होगा जो न केवल **extracts text from image** फ़ाइलों से टेक्स्ट निकालता है बल्कि **write JSON file C#** और **write XML file C#** को बिना किसी समस्या के करता है।

## आपको क्या चाहिए

- **.NET 6.0** या बाद का संस्करण (कोड .NET Framework 4.6+ के साथ भी काम करता है)।  
- **Aspose.OCR** NuGet पैकेज – इसे `dotnet add package Aspose.OCR` से इंस्टॉल करें।  
- टेक्स्ट वाली छवि (उदाहरण के लिए `invoice.png`)।  
- कोई भी IDE जो आपको पसंद हो – Visual Studio, Rider, या VS Code चलाएगा।

> **Pro tip:** अपनी इमेज फ़ाइलों को एक समर्पित फ़ोल्डर (जैसे `Resources/`) में रखें ताकि पाथ साफ़ रहें।

## चरण 1: OCR इंजन सेट अप करें – How to Convert OCR

सबसे पहले, हम एक `OcrEngine` इंस्टेंस बनाते हैं और उसे बताते हैं कि किस भाषा की तलाश करनी है। अधिकांश मामलों में अंग्रेज़ी पर्याप्त है, लेकिन आप `Language.English` को किसी भी समर्थित भाषा से बदल सकते हैं।

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Why this matters:** इंजन को सही भाषा के साथ इनिशियलाइज़ करने से सटीकता में काफी सुधार होता है, विशेषकर गैर‑लैटिन स्क्रिप्ट्स के लिए।

## चरण 2: टेक्स्ट पहचानें – Extract Text from Image

अब हम इमेज को इंजन को देते हैं। `Recognize` मेथड एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें कच्चा टेक्स्ट और लोकेशन डेटा दोनों होते हैं।

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

यदि इमेज नहीं मिलती, तो `Recognize` `FileNotFoundException` फेंकता है। डेमो को सरल रखने के लिए हम मान लेते हैं कि पाथ सही है, लेकिन प्रोडक्शन में आप इसे try‑catch ब्लॉक में रैप करना चाहेंगे।

## चरण 3: परिणाम को JSON में बदलें – Write JSON File C#

Aspose.OCR सीरियलाइज़ेशन को बहुत आसान बनाता है। `ToJson` मेथड एक `indent` फ़्लैग लेता है जिससे प्रीटी‑प्रिंटेड आउटपुट मिलता है, जो टेक्स्ट एडिटर में फ़ाइल खोलने के लिए आदर्श है।

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### अपेक्षित JSON नमूना

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **How to extract text**: `Text` प्रॉपर्टी आपको साधारण स्ट्रिंग देती है जिसे आप अन्य सेवाओं (सर्च इंडेक्स, डेटाबेस, आदि) में फीड कर सकते हैं।

## चरण 4: JSON को सहेजें – Write JSON File C# (Continued)

JSON स्ट्रिंग तैयार होने पर, हम इसे `File.WriteAllText` का उपयोग करके फ़ाइल में लिखते हैं। यह डिफ़ॉल्ट रूप से UTF‑8 एन्कोडिंग सुनिश्चित करता है।

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

अब आपके पास `invoice.json` आपकी इमेज के बगल में है, जो डाउनस्ट्रीम प्रोसेसिंग के लिए तैयार है।

## चरण 5: परिणाम को XML में बदलें – Write XML File C#

यदि आप लेगेसी सिस्टम के लिए XML पसंद करते हैं, तो `ToXml` मेथड यह काम करता है। `ToJson` की तरह, यह भी प्रीटी‑प्रिंटिंग को सपोर्ट करता है।

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### अपेक्षित XML नमूना

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## चरण 6: XML को सहेजें – Write XML File C# (Continued)

XML को सहेजना JSON चरण जैसा ही है; बस `.xml` एक्सटेंशन का उपयोग करें।

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ रखते हुए, यहाँ पूरा प्रोग्राम है जिसे आप कॉपी‑पेस्ट करके एक कंसोल ऐप में उपयोग कर सकते हैं:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

प्रोग्राम चलाएँ, और आपको दो नई फ़ाइलें मिलेंगी—`invoice.json` और `invoice.xml`—वहीं जहाँ आपने निर्दिष्ट किया था। उन्हें खोलें और जांचें कि संरचना ऊपर दिए गए नमूनों से मेल खाती है।

## सामान्य प्रश्न और किनारे के मामले

| प्रश्न | उत्तर |
|----------|--------|
| **यदि छवि में कई भाषाएँ हों तो क्या करें?** | `OcrEngine` के अलग‑अलग इंस्टेंस प्रत्येक भाषा के लिए बनाएं या यदि समर्थित हो तो `Language.Multi` का उपयोग करें। |
| **क्या मैं आउटपुट फ़ॉर्मेट को नियंत्रित कर सकता हूँ (जैसे, रीजन डेटा को बाहर रखें)?** | हां। दोनों `ToJson` और `ToXml` वैकल्पिक पैरामीटर स्वीकार करते हैं जिससे फ़ील्ड फ़िल्टर किए जा सकते हैं; `ExportOptions` के लिए Aspose.OCR दस्तावेज़ देखें। |
| **मैं कई पृष्ठों वाले बड़े PDFs को कैसे संभालूँ?** | प्रत्येक पृष्ठ को अलग‑अलग प्रोसेस करें, परिणामों को एकत्रित करें, फिर एक बार सीरियलाइज़ करें। |
| **क्या आउटपुट UTF‑8 सुरक्षित है?** | बिल्कुल—Aspose.OCR आंतरिक रूप से यूनिकोड उपयोग करता है, और `File.WriteAllText` डिफ़ॉल्ट रूप से UTF‑8 लिखता है। |
| **परफ़ॉर्मेंस के बारे में क्या?** | OCR CPU‑इंटेंसिव है। बैच जॉब्स के लिए कोर पर समानांतर प्रोसेसिंग या Aspose के क्लाउड API का उपयोग करने पर विचार करें। |

## निष्कर्ष

अब आप जानते हैं **how to convert OCR** परिणामों को C# का उपयोग करके JSON और XML दोनों में कैसे बदलें। ऊपर दिए गए चरणों का पालन करके आप **extract text from image** कर सकते हैं, फिर **write JSON file C#** और **write XML file C#** कुछ ही लाइनों में लिख सकते हैं। यह तरीका तेज़, विश्वसनीय है, और Aspose.OCR द्वारा समर्थित किसी भी इमेज प्रकार के साथ काम करता है।

Ready for the next challenge? Try feeding the

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}