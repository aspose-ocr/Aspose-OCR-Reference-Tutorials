---
category: general
date: 2026-04-11
description: Aspose OCR for C# में OCR को ऑफ़लाइन चलाने के लिए कैसे डिसेबल करें, इंटरनेट
  के बिना इमेज से टेक्स्ट निकालें, और OCR के लिए इमेज को सही ढंग से लोड करें, यह सीखें।
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: hi
og_description: Aspose OCR for C# में OCR को कैसे निष्क्रिय करें और ऑफ़लाइन चलाएँ,
  इंटरनेट की आवश्यकता के बिना छवि से टेक्स्ट निकालें, और OCR के लिए छवि को आसानी से
  लोड करें।
og_title: C# में OCR को कैसे निष्क्रिय करें – ऑफ़लाइन Aspose OCR गाइड
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: C# में OCR को कैसे निष्क्रिय करें – ऑफ़लाइन Aspose OCR गाइड
url: /hi/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में OCR को कैसे डिसेबल करें – ऑफ़लाइन Aspose OCR गाइड

क्या आपने कभी सोचा है **how to disable OCR** जब आपको एक पूरी तरह ऑफ़लाइन समाधान चाहिए? शायद आप एक सुरक्षित डेस्कटॉप ऐप बना रहे हैं जो नेटवर्क कनेक्शन पर निर्भर नहीं हो सकता, या आप अनपेक्षित डाउनलोड से बचना चाहते हैं। किसी भी स्थिति में, अच्छी खबर यह है कि Aspose OCR आपको अपने ऑटोमैटिक रिसोर्स फ़ेचिंग को बंद करने, इसे एक लोकल फ़ोल्डर की ओर इंगित करने, और सब कुछ ऑन‑प्रेमाइसेस रखने की अनुमति देता है। इस ट्यूटोरियल में आप यह भी देखेंगे कि कैसे **extract text from image** फ़ाइलों से टेक्स्ट निकाला जाए और सही तरीके से **load image for OCR** किया जाए बिना किसी समस्या के।

हम एक पूरी, तैयार‑चलाने‑योग्य उदाहरण के माध्यम से हर कदम दिखाएंगे—इंजन को इनिशियलाइज़ करने से लेकर पहचाने गए जापानी टेक्स्ट को प्रिंट करने तक। कोई बाहरी डॉक्यूमेंट नहीं, कोई छिपा जादू नहीं; सिर्फ साधारण C# कोड जिसे आप आज ही अपने प्रोजेक्ट में डाल सकते हैं। अंत तक आप समझ जाएंगे कि ऑटो‑डाउनलोड फीचर को डिसेबल करना क्यों महत्वपूर्ण है, रिसोर्सेज़ पाथ कैसे सेट करें, और किन समस्याओं से बचना चाहिए।

## आवश्यकताएँ

- .NET 6.0 (या कोई भी हालिया .NET संस्करण) आपके मशीन पर इंस्टॉल हो।  
- Aspose.OCR for .NET NuGet पैकेज (`Install-Package Aspose.OCR`)।  
- एक फ़ोल्डर जिसमें पहले से ही वह भाषा रिसोर्सेज़ हों जो आपको चाहिए (जैसे, जापानी मॉडल)।  
- एक इमेज फ़ाइल (`japan_doc.png`) जिस पर आप OCR चलाना चाहते हैं।  

यदि आपके पास भाषा पैक्स नहीं हैं, तो Aspose पोर्टल से एक बार डाउनलोड करके उन्हें `AsposeOCRResources` जैसे फ़ोल्डर में अनज़िप कर लें, और आप तैयार हैं। एक बार जब आप ऑटो‑डाउनलोड फीचर को डिसेबल कर देते हैं, तो आगे कोई डाउनलोड नहीं होगा।

![ऑफ़लाइन OCR को कैसे डिसेबल करें](/images/how-to-disable-ocr.png "OCR को डिसेबल करने का चित्रण")

## चरण 1 – OCR इंजन इंस्टेंस बनाएं  

पहला काम है `OcrEngine` को इंस्टैंशिएट करना। इस ऑब्जेक्ट को आप अपने इमेज को पढ़ने वाला दिमाग समझ सकते हैं।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Why this matters:** बिना इंजन के आप कोई भी सेटिंग कॉन्फ़िगर नहीं कर सकते। यह ऑब्जेक्ट सभी सेटिंग्स रखता है, जिसमें वह महत्वपूर्ण फ़्लैग भी शामिल है जो लाइब्रेरी को बताता है कि क्या वह इंटरनेट तक पहुंच सकता है।

## चरण 2 – ऑटोमैटिक रिसोर्स डाउनलोड को डिसेबल करें  

डिफ़ॉल्ट रूप से Aspose OCR गायब भाषा फ़ाइलों को ऑन‑द‑फ़्लाई फ़ेच करने की कोशिश करेगा। सब कुछ ऑफ़लाइन रखने के लिए `AutoDownloadResources` स्विच को `false` कर दें।

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Pro tip:** इसे बंद करने से न केवल प्राइवेसी की गारंटी मिलती है बल्कि पहला रिकॉग्निशन रन तेज़ हो जाता है क्योंकि इंजन अपडेट्स की जाँच में समय बर्बाद नहीं करता।

## चरण 3 – अपने लोकल रिसोर्सेज़ फ़ोल्डर की ओर इंगित करें  

अब इंजन को बताएं कि प्री‑डownload किए गए भाषा पैक्स कहाँ स्थित हैं। यह वही पाथ है जिसे आपने प्रीरेक्विज़िट्स में सेट किया था।

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **What could go wrong?** यदि पाथ गलत है या आवश्यक भाषा फ़ाइल मौजूद नहीं है, तो इंजन `ResourceNotFoundException` फेंकेगा। फ़ोल्डर की स्पेलिंग और यह सुनिश्चित करें कि जापानी मॉडल (`jpn.traineddata`) मौजूद है।

## चरण 4 – लोकल लैंग्वेज मॉडल चुनें  

उस भाषा को चुनें जो आपके डिस्क पर वास्तव में मौजूद है। हमारे उदाहरण में हम जापानी उपयोग कर रहे हैं, लेकिन आप `Language.Japanese` को किसी भी अन्य डाउनलोड की गई भाषा से बदल सकते हैं।

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Edge case:** कुछ भाषाओं को अतिरिक्त डिक्शनरी की आवश्यकता होती है (जैसे, चीनी)। सुनिश्चित करें कि ये सहायक फ़ाइलें भी उसी रिसोर्सेज़ फ़ोल्डर में हों।

## चरण 5 – OCR के लिए इमेज लोड करें  

यहीं पर हम **load image for OCR** करते हैं। `ImageStream.FromFile` मेथड फ़ाइल को एक स्ट्रीम में पढ़ता है जिसे Aspose प्रोसेस कर सकता है।

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **Tip:** समर्थित फ़ॉर्मेट में PNG, JPEG, BMP, और TIFF शामिल हैं। यदि आपको PDFs को हैंडल करना है, तो पहले प्रत्येक पेज को इमेज में बदलें।

## चरण 6 – रिकॉग्निशन प्रोसेस चलाएँ  

अब इंजन वास्तव में पिक्सेल पढ़ता है और उन्हें टेक्स्ट में बदलने की कोशिश करता है।

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Why this step can be slow:** OCR CPU‑इंटेन्सिव होता है, विशेषकर हाई‑रेज़ोल्यूशन इमेज के लिए। यदि परफ़ॉर्मेंस की चिंता है, तो रिकॉग्निशन से पहले इमेज को डाउन‑स्केल करने पर विचार करें।

## चरण 7 – एक्सट्रैक्टेड टेक्स्ट आउटपुट करें  

अंत में, हम **extract text from image** करते हैं और उसे कंसोल पर प्रिंट करते हैं।

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

प्रोग्राम चलाने पर `japan_doc.png` में मौजूद जापानी अक्षर कंसोल में दिखेंगे। यदि सब कुछ सही सेट है, तो आपको कंसोल पर एक साफ़ यूनिकोड टेक्स्ट ब्लॉक दिखाई देगा।

### अपेक्षित आउटपुट

```
これはサンプルの日本語テキストです。
```

(आपका वास्तविक आउटपुट इमेज की सामग्री पर निर्भर करेगा।)

## सामान्य समस्याएँ और उन्हें कैसे टालें  

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Missing language file** | `AutoDownloadResources` false है, इसलिए इंजन इसे फ़ेच नहीं कर सकता। | Verify `ResourcesPath` points to the folder containing `jpn.traineddata`. |
| **Incorrect image path** | `ImageStream.FromFile` `FileNotFoundException` फेंकता है। | Use absolute paths or ensure the working directory is set correctly. |
| **Unsupported image format** | Aspose केवल कुछ फ़ॉर्मेट पढ़ता है। | Convert your image to PNG or JPEG before calling `FromFile`. |
| **Out‑of‑memory on large images** | OCR पूरी इमेज को मेमोरी में लोड करता है। | Resize or tile the image, or increase the process’s memory limit. |

## उदाहरण को विस्तारित करना  

- **Batch processing:** इमेजेज़ की डायरेक्टरी पर लूप चलाएँ, वही रिकॉग्निशन कोड कॉल करें, और प्रत्येक परिणाम को अलग `.txt` फ़ाइल में लिखें।  
- **Different languages:** `Language.Japanese` को `Language.English` (या कोई अन्य) से बदलें, बशर्ते संबंधित रिसोर्स फ़ाइलें रखी हों।  
- **Custom preprocessing:** OCR से पहले बेहतर एक्यूरेसी के लिए Aspose.Imaging का उपयोग करके इमेज को डेस्क्यू या कॉन्ट्रास्ट बढ़ाएँ।

## निष्कर्ष  

अब आप जानते हैं **how to disable OCR** Aspose OCR में C# के लिए और इसे पूरी तरह ऑफ़लाइन चलाना। `AutoDownloadResources` को `false` सेट करके, इंजन को लोकल रिसोर्सेज़ फ़ोल्डर की ओर इंगित करके, और सही तरीके से **load image for OCR** करके, आप बिना इंटरनेट के **extract text from image** भरोसेमंद रूप से कर सकते हैं। यह तरीका सुरक्षित वातावरण, CI पाइपलाइन, या किसी भी स्थिति के लिए आदर्श है जहाँ नेटवर्क एक्सेस सीमित हो।

अगला कदम तैयार है? पूरे स्कैन किए गए PDFs की फ़ोल्डर प्रोसेस करने की कोशिश करें, विभिन्न भाषा पैक्स के साथ प्रयोग करें, या OCR परिणाम को सर्चेबल डेटाबेस में इंटीग्रेट करें। आज आपने जो ऑफ़लाइन सेटअप बनाया है, वह किसी भी ऑन‑प्रेमाइसेस डॉक्यूमेंट‑प्रोसेसिंग वर्कफ़्लो की ठोस नींव है।

कोडिंग का आनंद लें, और यदि कोई समस्या आती है तो टिप्पणी करके बताएं!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}