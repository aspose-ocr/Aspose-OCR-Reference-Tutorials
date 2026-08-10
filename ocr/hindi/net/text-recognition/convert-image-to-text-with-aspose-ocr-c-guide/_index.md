---
category: general
date: 2026-02-14
description: Aspose OCR का उपयोग करके C# में छवि को टेक्स्ट में बदलें। सीखें कि कैसे
  तस्वीर से अरबी टेक्स्ट निकाला जाए, OCR के लिए छवि लोड करें, और अरबी को प्रभावी ढंग
  से पहचाना जाए।
draft: false
keywords:
- convert image to text
- extract text from picture
- how to extract arabic text
- load image for ocr
- how to recognize arabic
language: hi
og_description: Aspose OCR का उपयोग करके C# में छवि को टेक्स्ट में बदलें। यह ट्यूटोरियल
  दिखाता है कि चित्र से अरबी टेक्स्ट कैसे निकालें, OCR के लिए छवि लोड करें, और अरबी
  को पहचानें।
og_title: Aspose OCR के साथ इमेज को टेक्स्ट में बदलें – C# गाइड
tags:
- OCR
- C#
- Aspose
title: Aspose OCR के साथ इमेज को टेक्स्ट में बदलें – C# गाइड
url: /hi/net/text-recognition/convert-image-to-text-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR के साथ इमेज को टेक्स्ट में बदलें – C# गाइड

क्या आप C# एप्लिकेशन में **इमेज को टेक्स्ट में बदलना** चाहते हैं? इमेज को टेक्स्ट में बदलना एक सामान्य कार्य है, विशेष रूप से जब आपको **पिक्चर से टेक्स्ट निकालना** पड़ता है ऐसी फ़ाइलों से जिनमें गैर‑लैटिन स्क्रिप्ट होते हैं। इस ट्यूटोरियल में हम एक पूर्ण, तुरंत चलाने योग्य उदाहरण के माध्यम से आपको ले चलेंगे जो दिखाता है **कैसे अरबी टेक्स्ट निकाला जाए**, कैसे **OCR के लिए इमेज लोड की जाए**, और Aspose.OCR लाइब्रेरी का उपयोग करके **अरबी** अक्षरों को पहचानने के लिए आवश्यक सटीक चरण।

हम सब कुछ कवर करेंगे, NuGet पैकेज को इंस्टॉल करने से लेकर मिसिंग फ़ॉन्ट्स या लो‑रिज़ॉल्यूशन स्कैन जैसी एज केसों को संभालने तक। अंत तक, आपके पास एक स्व-निहित प्रोग्राम होगा जो पहचाने गए अरबी स्ट्रिंग को कंसोल पर प्रिंट करेगा—बिना किसी बाहरी टूल के।

## आप क्या सीखेंगे

- .NET प्रोजेक्ट में Aspose.OCR जोड़ने का तरीका (2026 तक का नवीनतम संस्करण)
- **इमेज को टेक्स्ट में बदलने** के लिए आवश्यक सटीक कोड और प्रत्येक लाइन का महत्व
- अरबी ग्लिफ़्स के साथ काम करते समय सटीकता बढ़ाने के टिप्स
- फ़ाइल पाथ या स्ट्रीम से **OCR के लिए इमेज लोड करने** का तरीका
- सामान्य समस्याओं को हल करने के तरीके (जैसे, गलत भाषा सेटिंग, असमर्थित इमेज फॉर्मेट)

> **Pro tip:** यदि आप .NET 6 या बाद के संस्करण को टार्गेट कर रहे हैं, तो आप टॉप‑लेवल स्टेटमेंट्स का उपयोग करके कोड को और छोटा रख सकते हैं। नीचे दिया गया उदाहरण अधिकतम संगतता के लिए क्लासिक `Program` क्लास का उपयोग करता है।

## आवश्यकताएँ

- .NET 6 SDK (या कोई भी नवीनतम .NET संस्करण)
- Visual Studio 2022 या VS Code के साथ C# एक्सटेंशन
- NuGet पैकेज `Aspose.OCR` (`dotnet add package Aspose.OCR` के माध्यम से इंस्टॉल करें)
- एक इमेज फ़ाइल जिसमें अरबी टेक्स्ट हो (उदाहरण के लिए `arabic_sign.jpg`)

---

## इमेज को टेक्स्ट में बदलें – चरण‑दर‑चरण कार्यान्वयन

नीचे पूर्ण स्रोत फ़ाइल दी गई है जिसे आप नई कंसोल प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं। इसमें **सभी आवश्यक `using` निर्देश**, एक `Main` मेथड, और इनलाइन कमेंट्स शामिल हैं जो प्रत्येक ऑपरेशन के *क्यों* को समझाते हैं।

```csharp
// ------------------------------------------------------------
// Program.cs – Complete example to convert image to text
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine – this object holds the core logic.
            var ocrEngine = new Engine();

            // 2️⃣ Configure OCR options.
            //    We set the language to Arabic because the picture contains Arabic script.
            //    You can replace Language.Arabic with any other supported language.
            var ocrOptions = new OcrOptions
            {
                Language = Language.Arabic
            };

            // 3️⃣ Load the image you want to process.
            //    ImageStream.FromFile reads the file into a stream that Aspose can handle.
            //    If your image is in a different folder, adjust the path accordingly.
            var inputImage = ImageStream.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");

            // 4️⃣ Run OCR – the Recognize method returns an OcrResult object.
            var ocrResult = ocrEngine.Recognize(inputImage, ocrOptions);

            // 5️⃣ Output the recognized text to the console.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### अपेक्षित आउटपुट

यदि `arabic_sign.jpg` में वाक्यांश **"مطار دولي"** (जिसका अर्थ “International Airport” है) मौजूद है, तो कंसोल कुछ इस तरह दिखाएगा:

```
=== OCR Result ===
مطار دولي
```

सटीक वर्तनी इमेज की गुणवत्ता के आधार पर थोड़ी बदल सकती है, लेकिन आपको गिबरिश की बजाय अरबी अक्षर दिखने चाहिए।

---

## अरबी टेक्स्ट निकालना – भाषा कॉन्फ़िगर करना

हम स्पष्ट रूप से `Language = Language.Arabic` क्यों सेट करते हैं? Aspose.OCR कई भाषाओं को सपोर्ट करता है, लेकिन डिफ़ॉल्ट रूप से यह अंग्रेज़ी पर सेट होता है। अरबी दाएँ‑से‑बाएँ स्क्रिप्ट का उपयोग करता है और इसका ग्लिफ़ आकार संदर्भ‑निर्भर होता है। इंजन को सही भाषा बताकर आप सक्षम करते हैं:

- **Ligature detection** – ऐसे अक्षर जो साथ जुड़ते हैं (उदा., “لا”)
- **Right‑to‑left ordering** – आउटपुट स्ट्रिंग सही दिशा में होगी
- **Improved dictionary checks** – इंजन अरबी शब्द सूची को क्रॉस‑रेफ़रेंस करके सटीकता बढ़ा सकता है

यदि आपको कभी **पिक्चर से टेक्स्ट निकालना** पड़े जिसमें कई भाषाएँ हों, तो आप `OcrOptions.Language` में `Language` एनेम्स की एक एरे पास कर सकते हैं (उदा., `new[] { Language.Arabic, Language.English }`).

---

## OCR के लिए इमेज लोड करना – पिक्चर पढ़ना

`ImageStream.FromFile(...)` लाइन **OCR के लिए इमेज लोड करने** का सबसे सरल तरीका है। हालांकि, आपको ऐसे परिदृश्य मिल सकते हैं जहाँ:

- इमेज डेटाबेस BLOB में स्थित है।
- आपको पिक्चर HTTP अनुरोध के माध्यम से प्राप्त होती है।
- फ़ाइल गैर‑मानक फॉर्मेट में है (उदा., कई पृष्ठों वाला TIFF)।

ऐसे मामलों में, आप `MemoryStream` से एक `ImageStream` बना सकते हैं:

```csharp
byte[] bytes = System.IO.File.ReadAllBytes("path/to/image.png");
using var memStream = new System.IO.MemoryStream(bytes);
var inputImage = ImageStream.FromStream(memStream);
```

दोनों तरीकों से इंजन को समान आंतरिक प्रतिनिधित्व मिलता है, इसलिए OCR की गुणवत्ता अपरिवर्तित रहती है।

---

## अरबी को पहचानना – इंजन चलाना

जब आप `ocrEngine.Recognize(inputImage, ocrOptions)` कॉल करते हैं, तो इंजन कई आंतरिक चरणों को निष्पादित करता है:

1. **Pre‑processing** – शोर कम करना, बाइनराइज़ेशन, और डेस्क्यूइंग।
2. **Segmentation** – इमेज को लाइनों, शब्दों और अक्षरों में विभाजित करना।
3. **Classification** – प्रत्येक सेगमेंट को ज्ञात अरबी ग्लिफ़्स से मिलाना।
4. **Post‑processing** – भाषा नियम और कॉन्फिडेंस थ्रेशोल्ड लागू करना।

यदि आप कम कॉन्फिडेंस स्कोर देखते हैं, तो विचार करें:

- **Increasing image resolution** (अरबी के लिए न्यूनतम 300 dpi की सिफ़ारिश की जाती है)।
- **Adjusting contrast** इमेज फीड करने से पहले (एक सरल इमेज‑प्रोसेसिंग लाइब्रेरी जैसे `System.Drawing` या `ImageSharp` का उपयोग करें)।
- **Enabling `ocrOptions.UseLanguageDictionary = true`** कड़ी डिक्शनरी जांच के लिए।

---

## सामान्य समस्याएँ और उन्हें कैसे टालें

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| खाली आउटपुट | गलत फ़ाइल पाथ या असमर्थित फ़ॉर्मेट | पाथ की जाँच करें, `File.Exists` का उपयोग करें, और सुनिश्चित करें कि इमेज PNG/JPEG/BMP है |
| गड़बड़ अक्षर | भाषा अरबी पर सेट नहीं है | `OcrOptions` में `Language = Language.Arabic` सेट करें |
| कम सटीकता | इमेज धुंधली या लो‑dpi है | उच्च‑रिज़ॉल्यूशन स्रोत का उपयोग करें या शार्पनिंग फ़िल्टर लागू करें |
| Exception `ArgumentNullException` | `inputImage` null है | सुनिश्चित करें कि फ़ाइल मौजूद है और स्ट्रीम सही ढंग से खुली है |

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

यदि आप नेमस्पेस के बिना एक सिंगल फ़ाइल पसंद करते हैं, तो यहाँ एक कॉम्पैक्ट संस्करण है जो अभी भी बेस्ट प्रैक्टिसेज़ का पालन करता है:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class ConvertImageToText
{
    static void Main()
    {
        // Engine creation
        var engine = new Engine();

        // Set OCR options – Arabic language
        var options = new OcrOptions { Language = Language.Arabic };

        // Load image – change the path to your actual file
        var image = ImageStream.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");

        // Perform recognition
        var result = engine.Recognize(image, options);

        // Show result
        Console.WriteLine("=== Recognized Arabic Text ===");
        Console.WriteLine(result.Text);
    }
}
```

`dotnet run` के साथ प्रोग्राम चलाएँ और आप कंसोल में अरबी टेक्स्ट प्रिंट होते देखेंगे।

---

## विज़ुअल पुनरावलोकन

नीचे एक प्लेसहोल्डर स्क्रीनशॉट है जो कंसोल आउटपुट को दर्शाता है। **alt text** में SEO अनुपालन के लिए मुख्य कीवर्ड शामिल है।

![इमेज को टेक्स्ट में बदलने का उदाहरण – कंसोल में अरबी OCR परिणाम दिखाता हुआ](convert-image-to-text-example.png)

---

## निष्कर्ष

हमने अभी-अभी Aspose OCR का उपयोग करके C# में **इमेज को टेक्स्ट में बदलना** दिखाया है। ट्यूटोरियल ने लाइब्रेरी को इंस्टॉल करने से लेकर भाषा कॉन्फ़िगर करने, **अरबी टेक्स्ट निकालने**, पिक्चर लोड करने, और अंत में एक ही मेथड कॉल से **अरबी को पहचानने** तक सब कुछ कवर किया।  

इस ज्ञान से सुसज्जित होकर, आप अब OCR को किसी भी .NET प्रोजेक्ट में इंटीग्रेट कर सकते हैं—चाहे वह डेस्कटॉप यूटिलिटी हो, वेब API, या स्कैन किए गए दस्तावेज़ों के बैच को प्रोसेस करने वाली बैकग्राउंड सर्विस।

### आगे क्या?

- `Language.Arabic` को `Language.French`, `Language.ChineseSimplified` आदि में बदलकर अन्य भाषाओं के साथ प्रयोग करें।
- OCR को **पिक्चर से टेक्स्ट निकालने** पाइपलाइन के साथ मिलाएँ जो परिणामों को डेटाबेस में स्टोर करती हैं।
- `ocrResult.Confidence` प्रॉपर्टी का उपयोग करके कम‑कॉन्फिडेंस लाइनों को सहेजने से पहले फ़िल्टर करें।

एज केस या परफॉर्मेंस ट्यूनिंग के बारे में सवाल हैं? टिप्पणी छोड़ें या चर्चा थ्रेड में पूछें। कोडिंग का आनंद लें, और आपकी इमेज हमेशा साफ़, सर्चेबल टेक्स्ट प्रदान करें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}