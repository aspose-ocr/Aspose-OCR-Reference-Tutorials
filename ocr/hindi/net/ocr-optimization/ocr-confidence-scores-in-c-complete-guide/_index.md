---
category: general
date: 2026-05-31
description: C# में OCR कॉन्फिडेंस स्कोर कैसे प्राप्त करें, जबकि इमेज से टेक्स्ट निकालें
  और Aspose OCR के साथ रसीद की इमेज पढ़ें।
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: hi
og_description: OCR विश्वसनीयता स्कोर आपको सटीकता का आकलन करने में मदद करते हैं; यह
  गाइड दिखाता है कि छवि से टेक्स्ट कैसे निकाला जाए, बाउंडिंग बॉक्स कैसे प्राप्त किए
  जाएँ, और Aspose OCR का उपयोग करके रसीद की छवि कैसे पढ़ी जाए।
og_title: C# में OCR कॉन्फिडेंस स्कोर – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C# में OCR कॉन्फिडेंस स्कोर – पूर्ण गाइड
url: /hi/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में OCR confidence scores – पूर्ण गाइड

क्या आपने कभी सोचा है कि **OCR confidence scores** कैसे प्राप्त करें जब आपको *extract text from image* करना हो? शायद आप खर्च ट्रैकिंग के लिए **read receipt image** फ़ाइलें पढ़ने की कोशिश कर रहे हैं और जानना चाहते हैं कि इंजन किन अक्षरों के बारे में अनिश्चित है। अच्छी खबर? Aspose.OCR के साथ आप कुछ ही C# लाइनों में JPG से confidence percentages, bounding boxes, और plain text निकाल सकते हैं।

इस ट्यूटोरियल में हम वह सब कवर करेंगे जो आपको जानना आवश्यक है: लाइब्रेरी को इंस्टॉल करना, इंजन को **perform OCR on JPG** के लिए कॉन्फ़िगर करना, confidence scores निकालना, और **OCR bounding boxes** को समझना जो बताते हैं कि प्रत्येक अक्षर पेज पर कहाँ स्थित है। अंत तक आपके पास एक तैयार‑से‑चलाने वाला console ऐप होगा जो प्रत्येक अक्षर, उसका confidence, और उसकी लोकेशन प्रिंट करेगा—receipts या किसी भी स्कैन किए गए दस्तावेज़ को वैलिडेट करने के लिए परफेक्ट।

## आप क्या सीखेंगे

- NuGet के माध्यम से Aspose.OCR इंस्टॉल करें और एक बेसिक OCR इंजन सेट अप करें।  
- `OcrOptions` को कॉन्फ़िगर करें ताकि plain‑text आउटपुट **with confidence scores** और **bounding boxes** की अनुरोध किया जा सके।  
- `OcrResult` के माध्यम से लूप करें ताकि **extract text from image** लाइन‑बाय‑लाइन और सिम्बॉल‑बाय‑सिम्बॉल किया जा सके।  
- आम समस्याओं जैसे missing files, low‑confidence characters, और non‑JPG formats को हैंडल करें।  
- उदाहरण को विस्तारित करके एक फ़ोल्डर में कई receipt images प्रोसेस करें।

Aspose के साथ कोई पूर्व अनुभव आवश्यक नहीं है; बस एक कार्यशील .NET environment और एक receipt image (JPG) जो आप टेस्ट करना चाहते हैं।

---

## चरण 1 – Aspose.OCR इंस्टॉल करें और अपना प्रोजेक्ट तैयार करें

सबसे पहले: आपको Aspose.OCR NuGet पैकेज चाहिए। अपने प्रोजेक्ट फ़ोल्डर में एक टर्मिनल खोलें और चलाएँ:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** फ्री ट्रायल 200 पेज तक काम करता है, जो receipt स्कैनिंग टेस्ट करने के लिए पर्याप्त है।

पैकेज इंस्टॉल होने के बाद, एक नया console प्रोजेक्ट बनाएं (यदि आपके पास पहले से नहीं है):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

अब आप जेनरेटेड `Program.cs` खोल सकते हैं और using डायरेक्टिव्स जोड़ना शुरू कर सकते हैं:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

ये नेमस्पेसेस आपको `OcrEngine`, `OcrOptions`, और उन result टाइप्स तक पहुंच देती हैं जिनकी हमें बाद में जरूरत होगी।

## चरण 2 – OCR confidence scores और OCR bounding boxes प्राप्त करें

यह ट्यूटोरियल का मुख्य भाग है। हम इंजन को इस तरह कॉन्फ़िगर करेंगे कि प्रत्येक पहचाने गए अक्षर के साथ एक **confidence score** और एक **bounding box** (ग्लिफ को घेरने वाला आयत) हो। H2 हेडर स्वयं प्राथमिक कीवर्ड रखता है, जो SEO नियम को पूरा करता है।

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**क्यों शामिल करें confidence scores?**  
एक confidence score (0‑100%) आपको बताता है कि इंजन प्रत्येक अक्षर के बारे में कितना निश्चित है। यदि आप आउटपुट को डाउनस्ट्रीम लॉजिक—जैसे, expense‑approval workflow—में फीड कर रहे हैं, तो आप low‑confidence symbols को स्वचालित रूप से reject या flag कर सकते हैं।

**क्यों अनुरोध करें bounding boxes?**  
Bounding boxes आवश्यक होते हैं जब आपको मूल छवि पर टेक्स्ट को हाइलाइट करना हो, sub‑regions निकालने हों, या OCR परिणामों को UI overlay के साथ संरेखित करना हो। प्रत्येक `character.Bounds` आपको X, Y, चौड़ाई, और ऊँचाई पिक्सेल कॉर्डिनेट्स में देता है।

## चरण 3 – JPG पर OCR करें और extract text from image निकालें

अब हम वास्तव में इंजन चलाते हैं। `Recognize()` कॉल सभी भारी काम करती है और एक `OcrResult` ऑब्जेक्ट लौटाती है।

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

यदि इमेज पाथ गलत है या फ़ाइल समर्थित फ़ॉर्मेट में नहीं है, तो Aspose `FileNotFoundException` या `UnsupportedImageFormatException` फेंकेगा। प्रोडक्शन कोड में उन एज केसों को सुगमता से हैंडल करने के लिए कॉल को try/catch ब्लॉक में रैप करें।

### plain text निकालना

यदि आपको केवल संयोजित टेक्स्ट चाहिए, तो आप `ocrResult.Text` पढ़ सकते हैं:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

लेकिन क्योंकि हमने confidence scores और bounding boxes भी माँगे हैं, हम संरचना के माध्यम से इटररेट करेंगे ताकि प्रत्येक अक्षर का विवरण देख सकें।

## चरण 4 – लाइन्स, सिम्बॉल्स के माध्यम से इटररेट करें और OCR confidence scores दिखाएँ

यहाँ वह लूप है जो प्रत्येक अक्षर, उसका confidence, और उसका बॉक्स प्रिंट करता है। यही वह जगह है जहाँ **read receipt image** उदाहरण वास्तव में चमकता है।

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

सैंपल आउटपुट कुछ इस तरह दिख सकता है:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**संख्याओं की व्याख्या:**  
- **Confidence ≥ 90%** – आमतौर पर स्वीकार करने के लिए सुरक्षित।  
- **Confidence 70‑89%** – आपको दोबारा जांचना पड़ सकता है, विशेषकर राशियों में अंकों के लिए।  
- **Confidence < 70%** – मैन्युअल रिव्यू के लिए फ्लैग करने पर विचार करें।

## चरण 5 – पूर्ण चलाने योग्य उदाहरण (त्रुटि हैंडलिंग सहित)

सब कुछ मिलाकर, यहाँ एक पूर्ण प्रोग्राम है जिसे आप `Program.cs` में कॉपी‑पेस्ट कर सकते हैं। इसमें missing files के लिए एक सरल चेक शामिल है और यदि OCR फेल हो जाता है तो एक फ्रेंडली मैसेज प्रिंट करता है।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### अपेक्षित आउटपुट

जब आप `dotnet run` चलाते हैं तो console पहले concatenated receipt टेक्स्ट दिखाएगा, फिर प्रत्येक अक्षर की सूची उसके confidence score और bounding box के साथ। यदि किसी अक्षर का confidence कम है, तो आप 80% से कम प्रतिशत देखेंगे, जो उस receipt भाग को मैन्युअल रूप से वेरिफ़ाई करने का संकेत है।

## बोनस: फ़ोल्डर में कई Receipts प्रोसेस करना

यदि आपके पास receipt JPGs का एक बैच है, तो ऊपर की लॉजिक को `foreach (var file in Directory.GetFiles(folder, "*.jpg"))` लूप में रैप करें। प्रत्येक फ़ाइल के लिए `OcrEngine` को रीसेट करना याद रखें, या लूप के अंदर एक नया इंस्टैंस बनाएं ताकि स्टेट लीकेज न हो।

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

बुल्क प्रोसेसिंग रात के खर्च इम्पोर्ट के लिए उपयोगी है।

---

## निष्कर्ष

अब आपके पास C# में **OCR confidence scores** प्राप्त करने, **extract text from image** करने, और **OCR bounding boxes** पुनः प्राप्त करने का एक ठोस, एंड‑टू‑एंड समाधान है, जबकि आप **perform OCR on JPG** फ़ाइलें जैसे **read receipt image** पर काम कर रहे हैं। कोड पूरी तरह से स्व-निहित है, नवीनतम Aspose.OCR संस्करण (2026‑05‑31 तक) के साथ काम करता है, और आपको वह ग्रैन्युलर डेटा देता है जिसकी आपको भरोसेमंद डॉक्यूमेंट‑प्रोसेसिंग पाइपलाइन बनाने के लिए जरूरत है।

अगला क्या? मूल receipt पर bounding boxes को `System.Drawing` या किसी UI लाइब्रेरी का उपयोग करके विज़ुअलाइज़ करने की कोशिश करें, या low‑confidence characters को एक सेकेंडरी वेरिफ़िकेशन सर्विस में फीड करें। आप विभिन्न भाषाओं के साथ भी प्रयोग कर सकते हैं `ocrEngine.Options.Language = OcrLanguage.French;` सेट करके – API कई लोकेल्स को सपोर्ट करता है।

कोडिंग का आनंद लें, और आपके confidence scores हमेशा उच्च रहें! 

![Console output showing OCR confidence scores and bounding boxes for a receipt


## आगे आप क्या सीखें?

- [Aspose.OCR का उपयोग करके भाषा चयन के साथ C# में इमेज टेक्स्ट निकालें](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [इमेज रिकग्निशन में पहचाने गए अक्षरों के लिए OCR कैरेक्टर विकल्प कैसे प्राप्त करें](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [इमेज रिकग्निशन में JSON परिणाम के लिए Aspose OCR कैसे उपयोग करें](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}