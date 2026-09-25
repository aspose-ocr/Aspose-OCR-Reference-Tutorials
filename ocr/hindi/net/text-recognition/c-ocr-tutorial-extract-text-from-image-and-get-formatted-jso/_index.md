---
category: general
date: 2026-01-13
description: c# OCR ट्यूटोरियल जो दिखाता है कि छवि से टेक्स्ट कैसे निकालें, OCR के
  लिए छवि लोड करें, और Aspose OCR का उपयोग करके JSON आउटपुट को फॉर्मेट करें। ऑब्जेक्ट
  को JSON में सीरियलाइज़ करना सीखें।
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: hi
og_description: c# OCR ट्यूटोरियल जो आपको इमेज से टेक्स्ट निकालने, OCR के लिए इमेज
  लोड करने, और Aspose OCR के साथ JSON आउटपुट को फॉर्मेट करने के चरणों से गुजराता है।
og_title: c# OCR ट्यूटोरियल – टेक्स्ट निकालें और JSON को फ़ॉर्मेट करें
tags:
- OCR
- C#
- JSON
title: c# OCR ट्यूटोरियल – इमेज से टेक्स्ट निकालें और फ़ॉर्मेटेड JSON प्राप्त करें
url: /hi/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – इमेज से टेक्स्ट निकालें और JSON आउटपुट फ़ॉर्मेट करें

क्या आपने कभी सोचा है कि **इमेज से टेक्स्ट निकालना** C# प्रोजेक्ट में लो‑लेवल पिक्सेल प्रोसेसिंग के बिना कैसे किया जाए? यही समस्या इस *c# ocr tutorial* का समाधान है। कुछ ही मिनटों में आप देखेंगे कि **इमेज को OCR के लिए लोड** कैसे करें, Aspose OCR चलाएँ, और **JSON आउटपुट फ़ॉर्मेट** करें ताकि आप डेटा को सीधे अपने API या डेटाबेस में फीड कर सकें।

हम हर कोड लाइन को विस्तार से देखेंगे, समझाएंगे कि प्रत्येक भाग क्यों महत्वपूर्ण है, और आपको वह सटीक JSON दिखाएंगे जिसकी आपको उम्मीद करनी चाहिए। अंत तक आपके पास एक तैयार‑चलाने‑योग्य कंसोल ऐप होगा जो एक इनवॉइस PNG को साफ़, इंडेंटेड JSON में बदल देगा। कोई फालतू बातें नहीं, सिर्फ एक व्यावहारिक समाधान जिसे आप किसी भी .NET 6+ प्रोजेक्ट में डाल सकते हैं।

## इस c# ocr tutorial में क्या कवर किया गया है

- Aspose.OCR NuGet पैकेज को इंस्टॉल करना  
- OCR प्रोसेसिंग के लिए इमेज फ़ाइल लोड करना  
- अंग्रेज़ी टेक्स्ट (या कोई भी सपोर्टेड भाषा) पहचानना  
- **OCR परिणाम को JSON में सीरियलाइज़** करना और प्रीटी‑प्रिंटिंग लागू करना  
- कंसोल में JSON दिखाना और आवश्यकता पड़ने पर सेव करना  

आपको केवल C# की बुनियादी समझ और एक हालिया .NET SDK चाहिए। और कुछ नहीं। यदि आप इनवॉइस, रसीद या स्कैन किए गए फॉर्म की **इमेज से टेक्स्ट निकालने** के बारे में जिज्ञासु हैं, तो पढ़ते रहें।

---

## चरण 1: c# ocr tutorial पर्यावरण सेट अप करें

कोड लिखने से पहले सुनिश्चित करें कि आपके पास सही टूल्स हैं:

1. **.NET 6 SDK या बाद का संस्करण** – इसे आप Microsoft की साइट से डाउनलोड कर सकते हैं।  
2. **Visual Studio 2022** (Community संस्करण भी ठीक है) या कोई भी एडिटर जो आपको पसंद हो।  
3. **Aspose.OCR NuGet पैकेज** – अपने प्रोजेक्ट फ़ोल्डर में `dotnet add package Aspose.OCR` चलाएँ।

> **Pro tip:** यदि आप CI पाइपलाइन उपयोग कर रहे हैं, तो पैकेज रेफ़रेंस को अपने `.csproj` में जोड़ें ताकि बिल्ड स्वचालित रूप से इसे रिस्टोर कर ले।

---

## चरण 2: OCR के लिए इमेज लोड करें

हमारे ट्यूटोरियल का पहला वास्तविक कदम है वह इमेज लेना जिसे आप प्रोसेस करना चाहते हैं। Aspose OCR PNG, JPEG, और TIFF जैसे सामान्य फ़ॉर्मेट को सपोर्ट करता है।

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **यह क्यों महत्वपूर्ण है:** इमेज को `OcrImage` के रूप में लोड करने से इंजन को बिटमैप डेटा और DPI जानकारी तक पहुँच मिलती है, जिससे पहचान की सटीकता बढ़ती है। इस चरण को छोड़ने या करप्ट फ़ाइल देने से रन‑टाइम एक्सेप्शन आएगा।

---

## चरण 3: इमेज से टेक्स्ट निकालें

अब हम वास्तव में OCR इंजन चलाते हैं। `Recognize` मेथड एक समृद्ध `OcrResult` ऑब्जेक्ट रिटर्न करता है जिसमें रॉ टेक्स्ट, कॉन्फिडेंस स्कोर, और लेआउट विवरण होते हैं।

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **एज केस:** यदि आपको मल्टी‑लैंग्वेज डॉक्यूमेंट प्रोसेस करना है, तो विभिन्न `OcrLanguage` वैल्यूज़ के साथ `Recognize` को दो बार कॉल करें और परिणामों को कॉन्कैटनेट करें। इंजन थ्रेड‑सेफ़ है, इसलिए आप बड़े बैच को पैरललाइज़ भी कर सकते हैं।

---

## चरण 4: ऑब्जेक्ट को JSON में सीरियलाइज़ करें – JSON आउटपुट फ़ॉर्मेट करें

`OcrResult` ऑब्जेक्ट एक साधारण C# क्लास है, इसलिए हम इसे `System.Text.Json` को दे सकते हैं। `WriteIndented` को एनेबल करने से आउटपुट मानव‑पठनीय बन जाता है।

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **आपको क्या मिलेगा:** एक सुंदर इंडेंटेड JSON स्ट्रिंग जिसमें पहचाना गया टेक्स्ट, कॉन्फिडेंस, और पेज लेआउट शामिल है। यह लॉगिंग, वेब सर्विस को भेजने, या NoSQL डेटाबेस में स्टोर करने के लिए एकदम उपयुक्त है।

---

## चरण 5: फ़ॉर्मेटेड JSON दिखाएँ और (वैकल्पिक) सेव करें

अंत में, हम JSON को कंसोल पर आउटपुट करते हैं। यदि चाहें तो `File.WriteAllText` के साथ इसे फ़ाइल में भी लिख सकते हैं।

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**अपेक्षित कंसोल आउटपुट (संक्षिप्त रूप में):**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

यदि OCR इंजन कोई टेक्स्ट नहीं ढूँढ़ पाता, तो `Text` फ़ील्ड एक खाली स्ट्रिंग होगी और `Confidence` `0` होगा। यह इमेज क्वालिटी को दोबारा चेक करने का एक अच्छा संकेत है।

---

## चरण 6: पूर्ण कार्यशील उदाहरण

सब कुछ मिलाकर, यहाँ पूरा प्रोग्राम है जिसे आप नई कंसोल ऐप में कॉपी‑पेस्ट कर सकते हैं:

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

प्रोग्राम चलाएँ (`dotnet run` प्रोजेक्ट फ़ोल्डर से) और देखें कि कंसोल आपके स्कैन किए हुए इनवॉइस का एक सुंदर फ़ॉर्मेटेड JSON कैसे प्रिंट करता है।

---

## सामान्य समस्याएँ एवं टिप्स (c# ocr tutorial एक्स्ट्रा)

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Blank `Text` field** | इमेज लो‑कॉन्ट्रास्ट या रोटेटेड है। | इमेज को प्री‑प्रोसेस करें (कॉन्ट्रास्ट बढ़ाएँ, डेस्क्यू करें) या `OcrEngine.ImagePreprocess` उपयोग करें। |
| **`System.DllNotFoundException`** | नेेटिव Aspose OCR बाइनरीज़ गायब हैं। | सुनिश्चित करें कि NuGet पैकेज सही ढंग से रिस्टोर हुआ है और रनटाइम आर्किटेक्चर (x64/x86) आपके OS से मेल खाता है। |
| **Performance lag on large PDFs** | OCR हर पेज को क्रमिक रूप से प्रोसेस करता है। | प्रत्येक पेज के लिए अलग `OcrEngine` इंस्टेंस बनाकर पैरललाइज़ करें (इंजन थ्रेड‑सेफ़ है)। |
| **JSON too large** | आप हर डिटेल, जिसमें बाउंडिंग बॉक्स भी शामिल है, सीरियलाइज़ कर रहे हैं। | सीरियलाइज़ेशन से पहले एक DTO बनाएं जिसमें केवल `Text` और `Confidence` हों। |

> **याद रखें:** इस ट्यूटोरियल का लक्ष्य एक साफ़, एंड‑टू‑एंड फ्लो दिखाना है। आप बाद में JSON को ट्रिम कर सकते हैं या अतिरिक्त मेटाडेटा जोड़ सकते हैं।

---

## निष्कर्ष

आपने अभी एक **c# ocr tutorial** पूरा किया जिसमें इमेज लोड की, **इमेज से टेक्स्ट निकाला**, और **फ़ॉर्मेटेड JSON आउटपुट** प्राप्त किया **ऑब्जेक्ट को JSON में सीरियलाइज़** करके। चरण सरल थे, कोड चलाने के लिए तैयार है, और JSON डाउनस्ट्रीम कंजम्प्शन के लिए पूरी तरह इंडेंटेड है।

अब आगे क्या? `OcrLanguage.English` को `OcrLanguage.French` से बदलें या रसीदों के फ़ोल्डर को लूप में प्रोसेस करें। आप JSON को सीधे Azure Blob Storage में सेव करने या इसे मशीन‑लर्निंग मॉडल में फीड करने की भी खोज कर सकते हैं।

यदि कोई समस्या आती है, तो इमेज पाथ सही है या नहीं और Aspose OCR लाइसेंस (यदि आपके पास है) `Recognize` कॉल करने से पहले लोड हुआ है, यह दोबारा चेक करें। हैप्पी कोडिंग, और आपका OCR परिणाम हमेशा स्पष्ट रहे!

*Image illustrating the OCR flow (alt text: "c# ocr tutorial diagram showing load image, recognize text, serialize to JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}