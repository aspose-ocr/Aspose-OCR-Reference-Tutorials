---
category: general
date: 2025-12-30
description: छवि को जल्दी से डेस्क्यू कैसे करें और छवि से पाठ निकालते समय कंट्रास्ट
  बढ़ाने का तरीका सीखें ताकि OCR की सटीकता में सुधार हो।
draft: false
keywords:
- how to deskew image
- how to boost contrast
- extract text from image
- recognize text image
- improve ocr accuracy
language: hi
og_description: इमेज को जल्दी से डेस्क्यू कैसे करें और इमेज से टेक्स्ट निकालते समय
  कंट्रास्ट कैसे बढ़ाएँ, ताकि OCR की सटीकता में सुधार हो।
og_title: इमेज को डेस्क्यू करने और बेहतर OCR सटीकता के लिए कंट्रास्ट बढ़ाने का तरीका
tags:
- OCR
- C#
- Image Processing
title: इमेज को डेस्क्यू कैसे करें और बेहतर OCR सटीकता के लिए कंट्रास्ट बढ़ाएँ
url: /hi/net/ocr-optimization/how-to-deskew-image-and-boost-contrast-for-better-ocr-accura/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज को डेस्क्यू कैसे करें और बेहतर OCR सटीकता के लिए कंट्रास्ट बढ़ाएँ

क्या आपने कभी **इमेज को डेस्क्यू** करने के बारे में सोचा है जो स्कैनर या स्मार्टफ़ोन से आती हैं?  
आप अकेले नहीं हैं—अधिकांश डेवलपर्स को यह समस्या तब आती है जब स्रोत चित्र थोड़ा टिल्ट या नॉइज़ी हो, और OCR आउटपुट एक गड़बड़ mess बन जाता है।  

अच्छी खबर यह है कि कुछ ही C# लाइनों के साथ आप चित्र को सीधा कर सकते हैं, बैकग्राउंड साफ़ कर सकते हैं, और यहाँ तक कि कंट्रास्ट भी बढ़ा सकते हैं ताकि इंजन टेक्स्ट को प्रो की तरह पढ़े। इस गाइड में हम यह भी दिखाएंगे कि **इमेज से टेक्स्ट निकालें** और **टेक्स्ट इमेज कंटेंट को पहचानें** Aspose.OCR के साथ, जबकि **OCR सटीकता सुधारें** को हमेशा ध्यान में रखें।

## आपको क्या चाहिए

- **.NET 6.0** या बाद का संस्करण (कोड .NET Framework 4.7+ पर भी कंपाइल होता है)  
- **Aspose.OCR** NuGet पैकेज (वर्ज़न 23.12 या नया) – `dotnet add package Aspose.OCR` के ज़रिए इंस्टॉल करें  
- एक सैंपल इमेज जो घुमा हुआ और नॉइज़ी दोनों हो (उदा., `noisy_rotated.jpg`)  
- Visual Studio, VS Code, या कोई भी IDE जो आप पसंद करते हैं  

बस इतना ही—कोई अतिरिक्त नेटिव लाइब्रेरी नहीं, कोई भारी OpenCV बाइंडिंग नहीं। सिर्फ़ शुद्ध मैनेज्ड कोड।

---

## चरण 1: प्रोजेक्ट सेट अप करें और नेमस्पेसेस इम्पोर्ट करें

पहले, एक नया कंसोल ऐप बनाएं और आवश्यक नेमस्पेसेस को स्कोप में लाएँ। यह चरण आगे आने वाले सभी कोड की नींव है।

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later
        }
    }
}
```

**क्यों महत्वपूर्ण है:**  
`Aspose.OCR` आपको `OcrEngine` क्लास देता है, जबकि `Aspose.OCR.Filters` उपयोगी प्री‑प्रोसेसिंग फ़िल्टर जैसे `DeskewFilter` और `ContrastBoostFilter` प्रदान करता है। इन्हें पहले इम्पोर्ट करने से कोड साफ़ रहता है और कंपाइलर को पता चलता है कि हम क्या इस्तेमाल करने वाले हैं।

---

## चरण 2: OCR इंजन इनिशियलाइज़ करें और डेस्क्यू फ़िल्टर जोड़ें

अब हम वास्तव में **इमेज को डेस्क्यू** करेंगे। `DeskewFilter` स्वचालित रूप से रोटेशन एंगल (आपके द्वारा सेट किए गए मैक्स तक) का पता लगाता है और बिटमैप को फिर से क्षैतिज कर देता है।

```csharp
// Inside Main()
var ocrEngine = new OcrEngine();

// Deskew: correct up to 15 degrees of rotation
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
```

**क्या हो रहा है बैकएंड में?**  
फ़िल्टर इमेज में सबसे लंबी क्षैतिज टेक्स्ट लाइन को स्कैन करता है, टिल्ट का अनुमान लगाता है, और उल्टा रोटेशन लागू करता है। `MaxAngle` को 15° तक सीमित रखने से उन इमेजेज़ को ओवर‑करेक्ट करने से बचते हैं जो पहले से ही सीधी हैं।

> **प्रो टिप:** यदि आपके स्रोत इमेजेज़ उल्टे हो सकते हैं, तो `MaxAngle` को 180° तक बढ़ाएँ—फ़िल्टर फिर भी सही ओरिएंटेशन ढूँढ लेगा।

---

## चरण 3: डीनॉइज़ फ़िल्टर से शोर घटाएँ

एक नॉइज़ी स्कैन सबसे स्मार्ट OCR इंजन को भी भ्रमित कर सकता है। `DenoiseFilter` स्पीकल्स को स्मूद करता है बिना फाइन डिटेल्स को मिटाए।

```csharp
// Denoise: strength ranges from 0 (off) to 1 (max)
ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });
```

**क्यों चाहिए:**  
शोर फॉल्स एज बनाता है जिन्हें OCR एल्गोरिद्म कैरेक्टर समझ लेता है। `0.7` स्ट्रेंथ अधिकांश स्कैन्ड डॉक्यूमेंट्स के लिए एक अच्छा संतुलन है; बहुत साफ़ या बहुत गंदे इनपुट के लिए इसे समायोजित करें।

---

## चरण 4: कंट्रास्ट बढ़ाएँ – “कंट्रास्ट कैसे बढ़ाएँ” का व्यावहारिक उपयोग

यहाँ हम द्वितीयक कीवर्ड **how to boost contrast** का उत्तर देते हैं। `ContrastBoostFilter` डार्क टेक्स्ट और लाइट बैकग्राउंड के बीच का अंतर बढ़ाता है, जिससे अक्षर अधिक स्पष्ट हो जाते हैं।

```csharp
// Contrast boost: level > 1 increases contrast
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });
```

**तर्क:**  
उच्च कंट्रास्ट से फेड स्ट्रोक्स मिस होने की संभावना कम हो जाती है। `1.3` लेवल सामान्य ब्लैक‑ऑन‑व्हाइट डॉक्यूमेंट्स के लिए अच्छा काम करता है; कलर फोटो के लिए `1.5` या उससे अधिक की ज़रूरत पड़ सकती है।

---

## चरण 5: OCR चलाएँ और टेक्स्ट निकालें

इमेज को प्री‑प्रोसेस करने के बाद, हम अंत में **इमेज से टेक्स्ट निकालें** `Recognize` मेथड से करते हैं। यह मेथड एक `OcrResult` ऑब्जेक्ट रिटर्न करता है जिसमें रॉ स्ट्रिंग और कॉन्फिडेंस स्कोर होते हैं।

```csharp
// Perform OCR on the prepared image
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/noisy_rotated.jpg");

// Output the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**आपको क्या मिलेगा:**  
`ocrResult.Text` में वह प्लेन‑टेक्स्ट होगा जो इंजन पढ़ सका। यदि आपको शब्द‑स्तर का कॉन्फिडेंस चाहिए, तो `ocrResult.Regions` देखें—प्रत्येक रीजन में `Confidence` प्रॉपर्टी होती है।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम है जिसे आप `Program.cs` में पेस्ट कर सकते हैं। सुनिश्चित करें कि इमेज पाथ आपके मशीन पर वास्तविक फ़ाइल की ओर इशारा कर रहा हो।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Deskew – correct up to 15° rotation
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

            // 3️⃣ Denoise – smooth out speckles (strength 0.7)
            ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });

            // 4️⃣ Contrast boost – make text pop (level 1.3)
            ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });

            // 5️⃣ Recognize the image
            var imagePath = @"YOUR_DIRECTORY\noisy_rotated.jpg";
            var ocrResult = ocrEngine.Recognize(imagePath);

            // 6️⃣ Show the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**अपेक्षित आउटपुट (उदाहरण):**

```
=== OCR Output ===
Invoice #12345
Date: 2024-09-30
Total Amount: $1,250.00
Thank you for your business!
```

यदि परिणाम गड़बड़ दिखे, तो इमेज क्वालिटी दोबारा जांचें, `Strength` या `Level` को ट्यून करें, या अधिक आक्रामक डेस्क्यूइंग के लिए `MaxAngle` बढ़ाएँ।

---

## सामान्य प्रश्न एवं किनारे के केस

### अगर इमेज उल्टी‑नीचे है तो क्या करें?

`DeskewFilter` में `MaxAngle = 180` सेट करें। फ़िल्टर 180° रोटेशन का पता लगाएगा और सही ढंग से फ़्लिप करेगा।

### मेरा डॉक्यूमेंट रंगीन है (जैसे ब्लू हाइलाइट्स वाला स्कैन किया फ़ॉर्म)।

कंट्रास्ट बूस्ट से पहले `ColorFilter` जोड़ें, या मैन्युअली इमेज को ग्रेस्केल में बदलें:

```csharp
ocrEngine.Filters.Add(new GrayscaleFilter());
```

### मुझे कई फ़ाइलों को बैच में प्रोसेस करना है।

OCR लॉजिक को एक `foreach` लूप में रैप करें जो किसी डायरेक्टरी के फ़ाइलों पर इटररेट करे:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Scans", "*.jpg"))
{
    var result = ocrEngine.Recognize(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

### OCR कॉन्फिडेंस कैसे जानें?

`ocrResult.Regions` को इन्स्पेक्ट करें:

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"Text: {region.Text} – Confidence: {region.Confidence:P2}");
}
```

उच्च कॉन्फिडेंस वैल्यू (लगभग 100% के करीब) आमतौर पर दर्शाती है कि प्री‑प्रोसेसिंग स्टेप्स सफल रहे।

---

## OCR सटीकता बढ़ाने के टिप्स

| टिप | क्यों मदद करता है |
|-----|-------------------|
| **लॉसलेस इमेज फॉर्मेट्स का उपयोग करें** (PNG, TIFF) | JPEG कम्प्रेशन एजेज़ को ब्लर कर सकता है, जिससे पहचान प्रभावित होती है। |
| **DPI को 300+ रखें** | प्रत्येक कैरेक्टर में अधिक पिक्सेल होने से इंजन को अधिक डेटा मिलता है। |
| **अनावश्यक मार्जिन को क्रॉप करें** | शोर कम होता है और प्रोसेसिंग तेज़ होती है। |
| **कंट्रास्ट बूस्ट के बाद बाइनरी थ्रेशहोल्ड लागू करें** (ब्लैक/व्हाइट) शुद्ध टेक्स्ट डॉक्यूमेंट्स के लिए | इमेज को दो रंगों तक सीमित करता है, जो अधिकांश OCR इंजन पसंद करते हैं। |
| **पहले छोटे सैंपल से टेस्ट करें** | बड़े पैमाने पर लागू करने से पहले `Strength` और `Level` को फाइन‑ट्यून करने की सुविधा मिलती है। |

---

## निष्कर्ष

हमने **इमेज को डेस्क्यू** करने, **कंट्रास्ट कैसे बढ़ाएँ** और Aspose.OCR का उपयोग करके **इमेज से टेक्स्ट निकालें** की पूरी पाइपलाइन देखी। `DeskewFilter`, `DenoiseFilter`, और `ContrastBoostFilter` को `Recognize` से पहले चेन करने से अधिकांश रियल‑वर्ल्ड स्कैन में **OCR सटीकता सुधारें** में स्पष्ट सुधार दिखेगा।

कोड को चलाएँ, फ़िल्टर पैरामीटर्स को अपने डॉक्यूमेंट की विशेषताओं के अनुसार ट्यून करें, और आप सबसे गंदे फ़ोटो से भी साफ़ टेक्स्ट निकाल पाएँगे। आगे बढ़ना चाहते हैं? भाषा‑विशिष्ट डिक्शनरी जोड़ें, या आउटपुट को पोस्ट‑प्रोसेसिंग के लिए स्पेल‑चेकर में फीड करें।

हैप्पी कोडिंग, और आपके OCR परिणाम हमेशा क्रिस्टल‑क्लियर रहें! 

--- 

![छवि को डेस्क्यू करने का उदाहरण](deskew_example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}