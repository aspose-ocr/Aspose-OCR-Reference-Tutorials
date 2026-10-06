---
category: general
date: 2026-02-17
description: C# में Aspose OCR का उपयोग करके छवि पर OCR चलाएँ। जानें कि JPG से टेक्स्ट
  कैसे निकालें, OCR के लिए छवि को कैसे प्री‑प्रोसेस करें, और चरण‑दर‑चरण कोड के साथ
  OCR के लिए छवि कैसे लोड करें।
draft: false
keywords:
- run OCR on image
- extract text from jpg
- preprocess image for OCR
- load image for OCR
language: hi
og_description: C# में Aspose OCR का उपयोग करके छवि पर OCR चलाएँ। यह गाइड दिखाता है
  कि कैसे JPG से टेक्स्ट निकाला जाए, चित्र को पूर्व‑प्रसंस्करण किया जाए, और OCR के
  लिए छवि लोड की जाए।
og_title: Aspose OCR के साथ इमेज पर OCR चलाएँ – पूर्ण C# गाइड
tags:
- Aspose OCR
- C#
- Image Processing
title: Aspose OCR के साथ इमेज पर OCR चलाएँ – पूर्ण C# गाइड
url: /hi/net/text-recognition/run-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR के साथ इमेज पर OCR चलाएँ – पूर्ण C# गाइड

क्या आपको **इमेज पर OCR चलाने** की जरूरत पड़ी है लेकिन शुरू कहाँ से करें, समझ नहीं आया? कई वास्तविक‑दुनिया के ऐप्स में – जैसे इनवॉइस स्कैनर या रसीद ट्रैकर – पहला कदम JPEG से भरोसेमंद टेक्स्ट निकालना होता है। अच्छी खबर? Aspose OCR के साथ आप **इमेज पर OCR चलाने** के लिए सिर्फ कुछ ही पंक्तियों का C# कोड लिख सकते हैं, और साथ ही आप **jpg से टेक्स्ट निकालना**, **OCR के लिए इमेज प्री‑प्रोसेस करना**, और **OCR के लिए इमेज लोड करना** कैसे किया जाता है, यह भी सीखेंगे, बिना बिखरे हुए दस्तावेज़ों की खोज किए।

इस ट्यूटोरियल में हम एक पूर्ण, कॉपी‑एंड‑पेस्ट‑तैयार उदाहरण के माध्यम से दिखाएँगे कि इंजन को कैसे सेट‑अप करें, उपयोगी प्री‑प्रोसेसिंग फ़िल्टर जोड़ें, चित्र को रिकग्नाइज़र में फीड करें, और परिणाम को कंसोल में प्रिंट करें। अंत तक आपके पास एक स्व‑संचालित प्रोग्राम होगा जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं और तुरंत इमेज से टेक्स्ट निकालना शुरू कर सकते हैं।

## आपको क्या चाहिए

- .NET 6.0 या बाद का संस्करण (कोड .NET Core पर भी काम करता है)  
- Aspose.OCR NuGet पैकेज (`Install-Package Aspose.OCR`)  
- एक सैंपल JPEG (`input.jpg`) जिसे आप रेफ़रेंस कर सकें  
- C# सिंटैक्स की बुनियादी समझ (कुछ भी जटिल नहीं)

यदि आपके पास ये सब है, तो चलिए शुरू करते हैं। यदि नहीं, तो NuGet पैकेज और एक टेस्ट इमेज ले लें; बाकी गाइड मानती है कि आपने यह कर लिया है।

## चरण 1: OCR इंजन बनाएं – इमेज पर OCR चलाने का मूल

**इमेज पर OCR चलाने** के लिए सबसे पहले `OcrEngine` को इंस्टैंशिएट करना पड़ता है। यह ऑब्जेक्ट पहचान के लिए सभी कॉन्फ़िगरेशन और स्टेट रखता है।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // Step 1 – create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **क्यों महत्वपूर्ण है:** `OcrEngine` Aspose की रिकग्निशन पाइपलाइन का गेटवे है। इसके बिना आप फ़िल्टर, लैंग्वेज पैक या `Recognize` मेथड तक पहुँच नहीं सकते।

## चरण 2: प्री‑प्रोसेसिंग फ़िल्टर जोड़ें – JPG से टेक्स्ट निकालते समय सटीकता बढ़ाएँ

कैमरा से सीधे निकाली गई इमेज अक्सर परफेक्ट नहीं होती। तिरछे एंगल या रैंडम ग्रेन सबसे अच्छे OCR एल्गोरिदम को भी भ्रमित कर सकते हैं। **JPG से टेक्स्ट निकालते** समय कुछ फ़िल्टर जोड़ने से परिणाम में काफी सुधार हो सकता है।

```csharp
        // Step 2 – add preprocessing filters
        // Deskew corrects rotation; DenoiseGaussian reduces visual noise
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });
```

> **प्रो टिप:** यदि आपके स्रोत इमेज पहले से साफ़ हैं, तो आप `DenoiseGaussianFilter` को स्किप कर सकते हैं। बहुत ज़्यादा स्मूदिंग से हल्के अक्षर मिट सकते हैं।

## चरण 3: OCR के लिए इमेज लोड करें – JPEG को इंजन में फीड करना

अब वह भाग आता है जहाँ आप **OCR के लिए इमेज लोड** करते हैं। Aspose एक सुविधाजनक `ImageStream.FromFile` हेल्पर प्रदान करता है जो फ़ाइल पाथ को ऐसे स्ट्रीम में बदल देता है जिसे इंजन समझता है।

```csharp
        // Step 3 – specify the path to the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        // Load the image and run OCR in one call
        var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));
```

> **एज केस:** यदि फ़ाइल मौजूद नहीं है, तो `FromFile` `FileNotFoundException` फेंकेगा। यदि रन‑टाइम पर फ़ाइलें गायब हो सकती हैं, तो कॉल को try/catch में रैप करें।

## चरण 4: पहचाने गए टेक्स्ट को प्राप्त करें और दिखाएँ

अंत में, जब इंजन काम पूरा कर लेता है, तो आप `Text` प्रॉपर्टी के माध्यम से प्लेन‑टेक्स्ट परिणाम प्राप्त कर सकते हैं। इसे कंसोल में प्रिंट करना एक त्वरित डेमो के लिए पर्याप्त है, लेकिन आप इसे डेटाबेस या टेक्स्ट फ़ाइल में भी लिख सकते हैं।

```csharp
        // Step 4 – output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**अपेक्षित आउटपुट**

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
```

सटीक सामग्री आपके द्वारा फीड की गई इमेज पर निर्भर करेगी, लेकिन आपको गड़बड़ी की जगह एक अच्छी तरह फॉर्मेटेड टेक्स्ट ब्लॉक दिखना चाहिए।

![Diagram showing the OCR pipeline – run OCR on image, preprocess, load, recognize](/images/ocr-pipeline.png "run OCR on image pipeline diagram")

### प्रत्येक चरण क्यों महत्वपूर्ण है

| चरण | उद्देश्य | यदि छोड़ा गया तो क्या होगा |
|------|---------|--------------------------|
| **इंजन बनाएं** | आंतरिक स्ट्रक्चर को इनिशियलाइज़ करता है | कोई रिकग्नाइज़र उपलब्ध नहीं – `NullReferenceException` मिलेगा। |
| **फ़िल्टर जोड़ें** | रोटेशन और नॉइज़ को ठीक करके सटीकता बढ़ाता है | तिरछी या शोर वाली इमेज गड़बड़ आउटपुट देगी। |
| **इमेज लोड करें** | इंजन को रॉ बिटमैप प्रदान करता है | इंजन के पास प्रोसेस करने के लिए कुछ नहीं, `Text` फ़ील्ड खाली रहेगा। |
| **परिणाम पढ़ें** | आगे उपयोग के लिए प्लेन‑टेक्स्ट स्ट्रिंग निकालता है | आपने OCR चलाया लेकिन परिणाम नहीं देखा – उपयोगी नहीं! |

## सामान्य वैरिएशन और प्रक्रिया को कैसे ट्यून करें

### लैंग्वेज पैक बदलना

Aspose OCR बॉक्स से बाहर कई भाषाओं को सपोर्ट करता है। यदि आपको **इमेज पर OCR चलाने** वाली फ़ाइलों में फ्रेंच या जर्मन टेक्स्ट निकालना है, तो `Recognize` कॉल से पहले `Language` प्रॉपर्टी सेट करें।

```csharp
ocrEngine.Language = OcrLanguage.French;
```

### मल्टी‑पेज PDF को हैंडल करना

यदि आपका स्रोत एक मल्टी‑पेज PDF है न कि सिंगल JPEG, तो आप पहले प्रत्येक पेज को इमेज में कन्वर्ट कर सकते हैं (Aspose.PDF का उपयोग करके) और फिर प्रत्येक इमेज को उसी पाइपलाइन में फीड कर सकते हैं। पेजों पर लूप करना सीधा है:

```csharp
foreach (var pageImage in pdfPagesAsImages)
{
    var result = ocrEngine.Recognize(ImageStream.FromMemory(pageImage));
    Console.WriteLine(result.Text);
}
```

### बड़े फ़ाइलों से निपटना

हाई‑रेज़ोल्यूशन तस्वीरों को प्रोसेस करते समय मेमोरी की खपत बढ़ सकती है। **OCR के लिए इमेज लोड** करने से पहले इमेज को डाउन‑सैंपल करने पर विचार करें:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

var loadOptions = new JpegLoadOptions { Width = 1024, Height = 768 };
using (var img = (Image)Image.Load(imagePath, loadOptions))
{
    var stream = new MemoryStream();
    img.Save(stream, new JpegOptions());
    var ocrResult = ocrEngine.Recognize(ImageStream.FromMemory(stream.ToArray()));
}
```

## पूर्ण, रन‑टू‑रेडी उदाहरण

नीचे वह पूरा प्रोग्राम है जिसमें हमने अब तक चर्चा किए सभी हिस्से शामिल हैं। इसे एक नए कंसोल प्रोजेक्ट में कॉपी‑पेस्ट करें, `YOUR_DIRECTORY` को उस फ़ोल्डर से बदलें जहाँ `input.jpg` रखी है, और **F5** दबाएँ।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add useful preprocessing filters
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });

        // 3️⃣ Load the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        try
        {
            // Recognize text – this is where we actually run OCR on image
            var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));

            // 4️⃣ Print the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

### परिणाम की पुष्टि करें

1. प्रोग्राम चलाएँ।  
2. कंसोल देखें – आपको `input.jpg` पर मौजूद टेक्स्ट दिखना चाहिए।  
3. यदि आउटपुट गड़बड़ दिखे, तो `DenoiseGaussianFilter` के `Sigma` वैल्यू को एडजस्ट करें या `ContrastEnhancementFilter` जैसे अतिरिक्त फ़िल्टर जोड़ें।

## सारांश और अगले कदम

हमने अभी-अभी Aspose OCR का उपयोग करके **इमेज पर OCR चलाने** की पूरी प्रक्रिया कवर की, इंजन सेट‑अप से लेकर साफ़, पढ़ने योग्य टेक्स्ट डिलीवर करने तक। मुख्य बिंदु:

- `OcrEngine` इंस्टैंस बनाएं।  
- **OCR के लिए इमेज प्री‑प्रोसेस** करने हेतु `DeskewFilter` और `DenoiseGaussianFilter` जैसे फ़िल्टर जोड़ें।  
- `ImageStream.FromFile` से **OCR के लिए इमेज लोड** करें।  
- `Recognize` कॉल करें और `ocrResult.Text` पढ़ें ताकि **JPG से टेक्स्ट निकाला** जा सके।

और आगे बढ़ना चाहते हैं? ये आइडिया आज़माएँ:

- **बैच प्रोसेसिंग** – JPEG फ़ोल्डर पढ़ें और प्रत्येक परिणाम को अलग `.txt` फ़ाइल में आउटपुट करें।  
- **Azure Blob Storage के साथ इंटीग्रेट** – क्लाउड से इमेज लाएँ, OCR चलाएँ, फिर टेक्स्ट को वापस स्टोर करें।  
- **NLP के साथ संयोजन** – निकाले गए टेक्स्ट को लैंग्वेज‑अंडरस्टैंडिंग मॉडल में फीड करें ताकि इनवॉइस को ऑटो‑कैटेगराइज़ किया जा सके।  

फ़िल्टर कॉम्बिनेशन, लैंग्वेज पैक, या PNG और TIFF जैसे फ़ॉर्मेट के साथ प्रयोग करने में संकोच न करें – वही पाइपलाइन काम करेगी जब तक आप **OCR के लिए इमेज लोड** सही ढंग से करते हैं।

---

यदि आपको कोई समस्या आती है, तो नीचे कमेंट करें या उन्नत सेटिंग्स के लिए Aspose OCR डॉक्यूमेंटेशन देखें। हैप्पी कोडिंग, और तस्वीरों को सर्चेबल टेक्स्ट में बदलने का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}