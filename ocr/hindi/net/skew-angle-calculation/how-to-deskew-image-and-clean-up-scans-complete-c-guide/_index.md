---
category: general
date: 2026-03-18
description: स्कैन की गई फ़ाइलों में छवि को डेस्क्यू कैसे करें और शोर को कम करें।
  फ़ाइल से छवि लोड करना, TIFF से टेक्स्ट निकालना, और Aspose OCR के साथ छवि से टेक्स्ट
  पहचानना सीखें।
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: hi
og_description: Aspose OCR का उपयोग करके छवि को जल्दी से डेस्क्यू कैसे करें। यह गाइड
  आपको दिखाता है कि शोर को कैसे कम करें, फ़ाइल से छवि कैसे लोड करें, और C# में TIFF
  से टेक्स्ट कैसे निकालें।
og_title: इमेज को डेस्क्यू कैसे करें – पूर्ण C# OCR ट्यूटोरियल
tags:
- OCR
- C#
- Image Processing
title: इमेज को डेस्क्यू कैसे करें और स्कैन को साफ़ करें – पूर्ण C# गाइड
url: /hi/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज को डेस्क्यू कैसे करें – पूर्ण C# OCR ट्यूटोरियल

क्या आपने कभी सोचा है **इमेज को डेस्क्यू कैसे करें** फ़ाइलों को जो एक हिलते हुए स्कैनर से ली गई लगती हैं? आप अकेले नहीं हैं। अधिकांश डेवलपर्स को यह समस्या तब आती है जब स्रोत TIFF थोड़ा टेढ़ा-मेढ़ा हो, और OCR परिणाम गड़बड़ हो जाते हैं। अच्छी खबर? कुछ ही पंक्तियों के C# कोड से आप चित्र को सीधा कर सकते हैं, धुंधले बैकग्राउंड को हटाकर, और फ़ाइल से साफ़, खोज योग्य टेक्स्ट निकाल सकते हैं।

इस गाइड में हम **नॉइज़ को कैसे कम करें**, **फ़ाइल से इमेज लोड करें**, और अंत में **इमेज से टेक्स्ट पहचानें** Aspose OCR का उपयोग करके देखेंगे। अंत तक आप **tiff से टेक्स्ट निकालें** दस्तावेज़ों को बिना किसी मेहनत के कर पाएँगे।

> **Pro tip:** यदि आप पहले से ही Aspose OCR का उपयोग अन्य प्रोजेक्ट्स में कर रहे हैं, तो आप इन फ़िल्टरों को बिना किसी अतिरिक्त लाइसेंसिंग झंझट के जोड़ सकते हैं।

---

## आपको क्या चाहिए

- .NET 6 या बाद का (कोड .NET Core पर भी काम करता है)  
- Aspose.OCR NuGet पैकेज (`Install-Package Aspose.OCR`)  
- एक स्कैन किया हुआ TIFF जो थोड़ा घुमा हुआ या शोरयुक्त हो (हम `skewed_scanned_doc.tif` को उदाहरण के रूप में उपयोग करेंगे)  
- एक टेक्स्ट एडिटर या IDE (Visual Studio, VS Code, Rider – अपनी पसंद चुनें)

कोई अतिरिक्त लाइब्रेरीज़ आवश्यक नहीं हैं; हम जिन फ़िल्टरों का उपयोग करेंगे वे Aspose OCR में ही निर्मित हैं।

## चरण 1 – OCR इंजन बनाएं (इमेज को डेस्क्यू कैसे करें)

सबसे पहला काम आप `OcrEngine` को इनिशियलाइज़ करना है। इसे ऐसे समझें जैसे वह दिमाग जो बाद में आपके लिए अक्षरों को पढ़ेगा।

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

इंजन को पहले से बनाना क्यों जरूरी है? यह आपको प्री‑प्रोसेसिंग फ़िल्टर, भाषा पैक, और आउटपुट विकल्पों को जोड़ने के लिए एक ही जगह देता है। यदि आप इस चरण को छोड़कर सीधे `OcrEngine.Recognize` को कॉल करते हैं, तो आप पहले इमेज को साफ़ करने का मौका खो देते हैं, जो कि डेस्क्यू करने के कारण से ही महत्वपूर्ण है।

## चरण 2 – डेस्क्यू और नॉइज़‑रिडक्शन फ़िल्टर जोड़ें (नॉइज़ को कैसे कम करें)

| फ़िल्टर | क्या करता है | क्यों महत्वपूर्ण है |
|--------|--------------|----------------|
| `AutoDeskewFilter` | घूर्णन का पता लगाता है और सुधारता है | टेक्स्ट लाइनों को सीधा करता है ताकि OCR इंजन उन्हें सही पढ़ सके |
| `NoiseReductionFilterV2` | धब्बे और बैकग्राउंड ग्रेन हटाता है | साफ़ पिक्सेल कम गलत पहचान का मतलब देते हैं |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

आप `NoiseReductionFilterV2` को पुराने संस्करण से बदल सकते हैं, लेकिन v2 एल्गोरिद्म आधुनिक स्कैनरों को बेहतर संभालता है। यदि आपका दस्तावेज़ पहले से ही पूरी तरह सपाट है, तो डेस्क्यू फ़िल्टर इमेज को बिना बदलाव के पास कर देगा—कोई नुकसान नहीं।

## चरण 3 – फ़ाइल से इमेज लोड करें (फ़ाइल से इमेज लोड करें)

Aspose एक उपयोगी `ImageStream.FromFile` हेल्पर प्रदान करता है जो विभिन्न फ़ॉर्मैट्स पढ़ता है, जिसमें TIFF, JPEG, PNG, और BMP शामिल हैं। यहाँ हम फ़ाइल को मेमोरी में लोड करने का तरीका दिखाते हैं:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

`YOUR_DIRECTORY` को अपने मशीन पर वास्तविक पथ से बदलें। यदि आप रिलेटिव पाथ का उपयोग कर रहे हैं, तो सुनिश्चित करें कि फ़ाइल आपके executable के साथ ही स्थित हो या कार्यशील डायरेक्टरी को उसी अनुसार सेट करें।

## चरण 4 – प्री‑प्रोसेस्ड इमेज पर OCR चलाएँ (इमेज से टेक्स्ट पहचानें)

फ़िल्टर सेट हो जाने और इमेज लोड हो जाने के बाद, हम अंततः Aspose से अक्षरों को पढ़ने के लिए कहते हैं:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

इंजन के अंदर डेस्क्यू एल्गोरिद्म चलता है, शोर को स्मूद किया जाता है, और फिर न्यूरल‑नेटवर्क‑आधारित रिकग्नाइज़र चलाया जाता है। परिणाम एक `OcrResult` ऑब्जेक्ट में लिपटा होता है जो आपको कच्चा टेक्स्ट, कॉन्फिडेंस स्कोर, और यदि आवश्यक हो तो बाउंडिंग बॉक्स भी देता है।

## चरण 5 – निकाले गए टेक्स्ट को दिखाएँ या सहेजें (TIFF से टेक्स्ट निकालें)

एक त्वरित डेमो के लिए हम टेक्स्ट को कंसोल में प्रिंट करते हैं, लेकिन आप इसे फ़ाइल, डेटाबेस में लिख सकते हैं, या किसी डाउनस्ट्रीम वर्कफ़्लो में फीड कर सकते हैं।

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**अपेक्षित आउटपुट** (उदाहरण, आपके दस्तावेज़ के अनुसार बदल सकता है):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

यदि आउटपुट में अभी भी गड़बड़ अक्षर दिख रहे हैं, तो दोबारा जांचें कि मूल TIFF बहुत कम रिज़ॉल्यूशन (न्यूनतम 300 dpi की सिफ़ारिश) नहीं है और `ocrEngine.Settings.Language` में भाषा सही सेट है।

## पूर्ण कार्यशील उदाहरण (सभी चरण एक जगह)

नीचे पूरा प्रोग्राम है जिसे आप नई कंसोल प्रोजेक्ट में कॉपी‑पेस्ट करके तुरंत चला सकते हैं।

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

`Program.cs` के रूप में फ़ाइल सहेजें, `dotnet run` चलाएँ, और आपको टर्मिनल में साफ़ किया हुआ टेक्स्ट दिखना चाहिए।

## अक्सर पूछे जाने वाले प्रश्न और किनारे के मामलों

### यदि मेरे TIFF में कई पेज हों तो?

Aspose OCR मल्टी‑पेज इमेजेज़ को `image.GetPages()` (या `image.Pages`) के माध्यम से लूप करके प्रोसेस कर सकता है। प्रत्येक पेज अपना `OcrResult` देता है। यदि आपको एक ही स्ट्रिंग चाहिए तो `StringBuilder` से उन्हें जोड़ सकते हैं।

### क्या डेस्क्यू फ़िल्टर बहुत अधिक घुमा हुए इमेजेज़ पर काम करता है?

यह लगभग ±15° तक के घूर्णन को संभालता है। इससे अधिक पर आपको इमेज को मैन्युअली किसी ग्राफ़िक्स लाइब्रेरी (जैसे `System.Drawing` या `SkiaSharp`) से पहले घुमा कर Aspose को देना पड़ सकता है।

### गैर‑अंग्रेज़ी टेक्स्ट की सटीकता कैसे बढ़ाएँ?

भाषा को स्पष्ट रूप से सेट करें:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

यदि बिल्ट‑इन पैक्स आपके वर्णमाला को कवर नहीं करते हैं तो आप कस्टम भाषा पैक्स भी लोड कर सकते हैं।

### क्या मैं इसे Linux पर चला सकता हूँ?

बिल्कुल। Aspose OCR क्रॉस‑प्लेटफ़ॉर्म है; बस यह सुनिश्चित करें कि नेटिव डिपेंडेंसीज़ मौजूद हों (आमतौर पर शुद्ध .NET संस्करण के लिए कोई नहीं)। `dotnet publish -r linux-x64` का उपयोग करके सेल्फ‑कंटेन्ड बाइनरी बनाएं।

## बोनस: डेस्क्यू की गई इमेज को विज़ुअलाइज़ करना

यदि आप OCR से पहले सुधारी गई इमेज देखना चाहते हैं, तो आप इसे डिस्क पर फिर से सहेज सकते हैं:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![इमेज को डेस्क्यू करने का उदाहरण](https://example.com/deskew-demo.png "इमेज को डेस्क्यू करने का उदाहरण")

*इमेज वैकल्पिक टेक्स्ट:* **इमेज को डेस्क्यू करने का उदाहरण** – दिखाता है एक घुमा हुआ TIFF जिसे AutoDeskewFilter द्वारा ठीक किया गया है।

## निष्कर्ष

हमने **इमेज को डेस्क्यू कैसे करें** फ़ाइलों, **नॉइज़ को कैसे कम करें**, और पूरी पाइपलाइन को कवर किया है **इमेज से टेक्स्ट पहचानें**, **फ़ाइल से इमेज लोड करें**, और **TIFF से टेक्स्ट निकालें** Aspose OCR का उपयोग करके C# में। मुख्य बात? केवल दो प्री‑प्रोसेसिंग फ़िल्टर जोड़ने से एक हिलती‑डुलती, धुंधली स्कैन को एक साफ़, खोज योग्य दस्तावेज़ में बदल दिया जाता है, बिना किसी बाहरी टूल के।

अगले चरण के लिए तैयार हैं? यदि आपके दस्तावेज़ उल्टे हैं तो `AutoDeskewFilter` को `AutoRotateFilter` से बदलें, या फीके प्रिंट के लिए `ContrastEnhancementFilter` आज़माएँ। वही पैटर्न—इंजन → फ़िल्टर → लोड → पहचान—सभी Aspose OCR परिदृश्यों के लिए लागू होता है, इसलिए आप इस स्केलेटन को PDFs, PNGs, या कैमरा फ़ोटो के लिए भी पुन: उपयोग कर सकते हैं।

कोडिंग का आनंद लें, और आपका OCR हमेशा सटीक रहे!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}