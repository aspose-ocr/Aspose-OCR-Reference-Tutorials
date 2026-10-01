---
category: general
date: 2026-01-02
description: Aspose.OCR का उपयोग करके ऑफ़लाइन टेक्स्ट पहचान के साथ चीनी टेक्स्ट को
  पहचानना और PNG फ़ाइलों से टेक्स्ट निकालना सीखें। इंटरनेट की आवश्यकता नहीं – कुछ
  ही चरणों में छवि पर OCR करें।
draft: false
keywords:
- recognize chinese text
- extract text from png
- offline text recognition
- perform OCR on image
language: hi
og_description: इंटरनेट के बिना चीनी पाठ को पहचानें। यह ट्यूटोरियल दिखाता है कि ऑफ़लाइन
  टेक्स्ट रिकग्निशन का उपयोग करके PNG से टेक्स्ट कैसे निकालें और C# में इमेज पर OCR
  कैसे लागू करें।
og_title: ऑफ़लाइन चीनी टेक्स्ट को पहचानें – चरण‑दर‑चरण C# गाइड
tags:
- OCR
- C#
- Aspose
title: ऑफ़लाइन चीनी पाठ को पहचानें – पूर्ण C# OCR ट्यूटोरियल
url: /hi/net/text-recognition/recognize-chinese-text-offline-complete-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ऑफ़लाइन चीनी टेक्स्ट पहचान – पूर्ण C# OCR ट्यूटोरियल

क्या आपको कभी स्कैन किए गए PNG से **चीनी टेक्स्ट पहचान**ने की ज़रूरत पड़ी, लेकिन आपका ऐप इंटरनेट के बिना मशीन पर चलता है? आप अकेले नहीं हैं। कई एंटरप्राइज़ परिदृश्यों में—जैसे एयर‑गैप्ड सर्वर या फ़ील्ड डिवाइस—क्लाउड सेवाओं पर निर्भर रहना संभव नहीं है।  

इस गाइड में हम एक स्व-निहित समाधान के माध्यम से चलेंगे जो आपको **png फ़ाइलों से टेक्स्ट निकालने**, **ऑफ़लाइन टेक्स्ट पहचान** चलाने, और Aspose.OCR का उपयोग करके **छवि पर OCR करने** की अनुमति देता है। अंत तक आपके पास एक तैयार‑चलाने योग्य C# कंसोल प्रोग्राम होगा जो चीनी अक्षरों को सीधे कंसोल में प्रिंट करेगा।

## आवश्यकताएँ

- .NET 6 SDK (या कोई भी हालिया .NET संस्करण) स्थानीय रूप से स्थापित।  
- Visual Studio 2022 या VS Code – जो भी आपको पसंद हो।  
- Aspose.OCR for .NET NuGet पैकेज (`Aspose.OCR`) की एक कॉपी।  
- अंग्रेज़ी और सरल चीनी के लिए भाषा संसाधन फ़ाइलें (ट्यूटोरियल दिखाता है कि उन्हें स्वचालित रूप से कैसे डाउनलोड किया जाए)।  
- `chinese_doc.png` नाम की एक छवि को उस फ़ोल्डर में रखें जिसे आप संदर्भित कर सकते हैं (`YOUR_DIRECTORY` प्लेसहोल्डर)।

कोई अतिरिक्त सेवाएँ नहीं, कोई API कुंजी नहीं—सिर्फ एक स्थानीय DLL और कुछ संसाधन फ़ाइलें।

---

## चरण 1 – आवश्यक भाषा संसाधन डाउनलोड करें (एक बार)

Aspose.OCR डिस्क पर भाषा पैक संग्रहीत करता है। जब आप पहली बार ऐप चलाते हैं तो आपको इन्हें डाउनलोड करना पड़ता है। `ResourceManager.DownloadResources` कॉल ठीक यही करती है, और क्योंकि हम अंग्रेज़ी और सरल चीनी दोनों पास करते हैं, इंजन बाद में बिना किसी अतिरिक्त नेटवर्क ट्रैफ़िक के उनके बीच स्विच कर सकता है।

```csharp
using Aspose.OCR;

// Download English and Simplified Chinese language packs (run once)
ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);
```

> **Pro tip:** यदि आपको कई मशीनों पर पुनरुत्पादक बिल्ड चाहिए तो डाउनलोड किए गए फ़ोल्डर (`Aspose.OCR.Resources`) को स्रोत नियंत्रण में रखें।

## चरण 2 – ऑफ़लाइन मोड में OCR इंजन को इनिशियलाइज़ करें

`OfflineMode = true` सेट करने से लाइब्रेरी को किसी भी HTTP कॉल से बचने को कहा जाता है। यह सच्ची **ऑफ़लाइन टेक्स्ट पहचान** की कुंजी है।

```csharp
// Initialise the OCR engine for offline use
var ocrEngine = new OcrEngine()
{
    OfflineMode = true   // Guarantees no network traffic
};
```

> **Why this matters:** कुछ OCR लाइब्रेरीज़ भाषा पैक न मिलने पर क्लाउड सेवाओं पर वापस आती हैं। ऑफ़लाइन मोड को मजबूर करके हम निर्धारक प्रदर्शन और डेटा‑प्राइवेसी नीतियों के अनुपालन की गारंटी देते हैं।

## चरण 3 – वह PNG लोड करें जिसे आप प्रोसेस करना चाहते हैं

हम छवि पढ़ने के लिए `System.Drawing.Bitmap` का उपयोग करेंगे। यदि आपका प्रोजेक्ट .NET 6+ को गैर‑विंडोज प्लेटफ़ॉर्म पर टार्गेट करता है, तो वैकल्पिक रूप से `SkiaSharp` पर विचार करें, लेकिन अधिकांश विंडोज‑केंद्रित डिप्लॉयमेंट्स के लिए `Bitmap` ठीक काम करता है।

```csharp
using System.Drawing;

// Load the PNG that contains Chinese characters
var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
var image = new Bitmap(imagePath);
```

> **Edge case:** यदि PNG बहुत बड़ा है (5 MP से अधिक) तो आप पहचान को तेज़ करने और मेमोरी उपयोग कम करने के लिए पहले इसे डाउनस्केल करना चाह सकते हैं:

```csharp
// Optional downscale for huge images
if (image.Width * image.Height > 5_000_000)
{
    var scaled = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
    image.Dispose();
    image = scaled;
}
```

## चरण 4 – सरल चीनी भाषा के साथ पहचान चलाएँ

यहाँ हम इंजन को ठीक वही भाषा बताते हैं जिसका उपयोग करना है। `RecognitionOptions` ऑब्जेक्ट आपको `DetectOrientation` या `PreserveFormatting` जैसी चीज़ें समायोजित करने की भी अनुमति देता है, लेकिन डिफ़ॉल्ट अधिकांश प्रिंटेड दस्तावेज़ों के लिए अच्छी तरह काम करते हैं।

```csharp
using Aspose.OCR;

// Perform OCR using Simplified Chinese language pack
var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
{
    Language = Language.ChineseSimplified
});
```

## चरण 5 – निकाले गए टेक्स्ट को प्रदर्शित (या आगे प्रोसेस) करें

`OcrResult.Text` प्रॉपर्टी साधारण‑टेक्स्ट प्रतिनिधित्व रखती है। आप इसे कंसोल, फ़ाइल में लिख सकते हैं, या इसे डाउनस्ट्रीम NLP पाइपलाइन में फीड कर सकते हैं।

```csharp
// Output the recognized Chinese text to the console
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

### अपेक्षित आउटपुट

यदि `chinese_doc.png` में वाक्य “你好，世界！” है, तो कंसोल दिखाएगा:

```
=== Recognized Chinese Text ===
你好，世界！
```

> **Note:** OCR की सटीकता छवि की गुणवत्ता, फ़ॉन्ट की स्पष्टता, और कंट्रास्ट पर निर्भर करती है। सर्वोत्तम परिणामों के लिए, उच्च‑रिज़ॉल्यूशन स्कैन (300 dpi या अधिक) का उपयोग करें और सुनिश्चित करें कि टेक्स्ट तिरछा न हो।

---

## पूर्ण कार्यशील उदाहरण

नीचे पूरा, कॉपी‑एंड‑पेस्ट‑तैयार प्रोग्राम है। इसे `Program.cs` के रूप में एक नए कंसोल प्रोजेक्ट में सहेजें और `dotnet run` चलाएँ। सभी चरण एक साथ बंडल किए गए हैं, इसलिए आप संसाधन डाउनलोड से अंतिम आउटपुट तक का प्रवाह देख सकते हैं।

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;

class OfflineExample
{
    static void Main()
    {
        // 1️⃣ Download language resources (only needed once)
        ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);

        // 2️⃣ Initialise OCR engine in offline mode
        var ocrEngine = new OcrEngine()
        {
            OfflineMode = true
        };

        // 3️⃣ Load the PNG image
        var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
        using var image = new Bitmap(imagePath);

        // 4️⃣ Recognise Simplified Chinese text
        var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
        {
            Language = Language.ChineseSimplified
        });

        // 5️⃣ Print the result
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Tip:** यदि आप चाहते हैं कि इंटरनेट पूरी तरह अनुपलब्ध होने पर भी सुगम हैंडलिंग हो, तो `ResourceManager.DownloadResources` कॉल को `try/catch` ब्लॉक में रखें। अन्यथा यह मेथड `NetworkException` फेंकेगा।

---

## अक्सर पूछे जाने वाले प्रश्न (FAQ)

| प्रश्न | उत्तर |
|----------|--------|
| **क्या मैं पारंपरिक चीनी पहचान सकता हूँ?** | हाँ—`Language.ChineseSimplified` को `Language.ChineseTraditional` से बदलें और संबंधित पैक डाउनलोड करें। |
| **यदि मुझे PNG के बजाय JPEG से टेक्स्ट निकालना हो तो क्या करें?** | एक ही कोड काम करता है; बस फ़ाइल एक्सटेंशन बदलें। `Bitmap` अधिकांश सामान्य रास्टर फ़ॉर्मेट्स को सपोर्ट करता है। |
| **क्या प्रत्येक अक्षर के लिए बाउंडिंग बॉक्स प्राप्त करने का कोई तरीका है?** | `RecognitionOptions.DetectRegions = true` सेट करें। तब `OcrResult` में निर्देशांक के साथ `Region` ऑब्जेक्ट्स होंगे। |
| **मैं इसे Linux पर कैसे चलाऊँ?** | `System.Drawing.Common` पैकेज (1.0+) का उपयोग करें। हेडलेस Linux पर आपको `libgdiplus` नेेटिव डिपेंडेंसी की आवश्यकता हो सकती है। |
| **क्या मैं इमेजों के फ़ोल्डर को बैच‑प्रोसेस कर सकता हूँ?** | बिल्कुल—पहचान लॉजिक को `foreach (var file in Directory.GetFiles(folder, "*.png"))` लूप में रैप करें। |

## अगले कदम और संबंधित विषय

- **सटीकता सुधारें**: `RecognitionOptions.PreprocessImage = true` के साथ प्रयोग करें ताकि इंजन स्वचालित रूप से कंट्रास्ट बढ़ा सके।  
- **भाषाओं को मिलाएँ**: आप `ResourceManager.DownloadResources` को भाषाओं की एक एरे पास कर सकते हैं और इंजन को स्वचालित रूप से पहचानने दे सकते हैं।  
- **UI के साथ एकीकृत करें**: कंसोल कोड को WinForms या WPF ऐप में डालें और OCR परिणाम को टेक्स्टबॉक्स में दिखाएँ।  
- **अन्य Aspose लाइब्रेरीज़ का अन्वेषण करें**: PDF जनरेशन के लिए `Aspose.PDF`, स्लाइड ऑटोमेशन के लिए `Aspose.Slides`, आदि।  

यदि आप अन्य इमेज फ़ॉर्मेट्स से टेक्स्ट निकालने में रुचि रखते हैं, तो वही पैटर्न लागू होता है—बस फ़ाइल पाथ बदलें और वैकल्पिक रूप से प्री‑प्रोसेसिंग विकल्प समायोजित करें। कोडिंग का आनंद लें!

![recognize chinese text example](/images/recognize-chinese-text.png "Screenshot showing recognize chinese text output in console")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}