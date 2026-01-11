---
category: general
date: 2026-01-10
description: कैसे तेज़ी से OCR चलाएँ और एक छवि से अरबी टेक्स्ट निकालें। इमेज को टेक्स्ट
  में बदलना सीखें, PNG से टेक्स्ट पढ़ें, और Aspose OCR के साथ टेक्स्ट निकालना देखें।
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: hi
og_description: C# में OCR कैसे चलाएँ और PNG छवि से अरबी टेक्स्ट निकालें। यह गाइड
  आपको चरण‑दर‑चरण दिखाता है कि कैसे छवि को टेक्स्ट में बदलें और PNG से टेक्स्ट पढ़ें।
og_title: C# में OCR कैसे चलाएँ – PNG से अरबी टेक्स्ट निकालें
tags:
- OCR
- C#
- Aspose
title: C# में OCR कैसे चलाएँ – PNG से अरबी टेक्स्ट निकालें
url: /hi/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में OCR कैसे चलाएँ – PNG से अरबी टेक्स्ट निकालें

क्या आपने कभी सोचा है **OCR कैसे चलाएँ** एक ऐसी तस्वीर पर जिसमें अरबी अक्षर हों? आप अकेले नहीं हैं। कई डेवलपर्स को एक बाधा आती है जब उन्हें PNG से **अरबी टेक्स्ट निकालना** होता है लेकिन उन्हें नहीं पता कि कौन-सी लाइब्रेरी दाएँ‑से‑बाएँ स्क्रिप्ट को बिना समस्या के संभालेगी।  

इस ट्यूटोरियल में हम आपको वह सब बताएँगे जो आपको **इमेज को टेक्स्ट में बदलने**, **PNG से टेक्स्ट पढ़ने**, और अंत में **टेक्स्ट कैसे निकालें** Aspose.OCR का उपयोग करके एक साफ़ C# कंसोल ऐप में जानने की ज़रूरत है। अंत तक आपके पास एक तैयार‑चलाने‑योग्य प्रोग्राम होगा जो अरबी स्ट्रिंग को सीधे आपके टर्मिनल पर प्रिंट करेगा।

## आप क्या सीखेंगे

- Aspose.OCR NuGet पैकेज को इंस्टॉल और रेफ़रेंस करें।  
- OCR इंजन को अरबी भाषा समर्थन के लिए कॉन्फ़िगर करें।  
- PNG इमेज लोड करें और रिकग्निशन प्रोसेस चलाएँ।  
- निकाले गए टेक्स्ट को प्राप्त करें और प्रदर्शित करें।  
- बेहतर सटीकता के लिए सेटिंग्स को ट्यून करें और सामान्य समस्याओं को संभालें।  

OCR में कोई पूर्व अनुभव आवश्यक नहीं है, बस C# की बुनियादी समझ और एक .NET विकास वातावरण (Visual Studio, Rider, या `dotnet` CLI) पर्याप्त है।

---

## OCR कैसे चलाएँ – Aspose OCR सेटअप

### चरण 1: Aspose.OCR NuGet पैकेज जोड़ें

पहला काम OCR लाइब्रेरी को प्राप्त करना है। Aspose.OCR एक व्यावसायिक उत्पाद है, लेकिन यह एक मुफ्त ट्रायल प्रदान करता है जो सीखने के लिए पूरी तरह उपयुक्त है।

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

वैकल्पिक रूप से, Visual Studio में **NuGet Package Manager** खोलें, **Aspose.OCR** खोजें, और **Install** पर क्लिक करें।

> **Pro tip:** यदि आप लाइब्रेरी को CI पाइपलाइन में उपयोग करने की योजना बना रहे हैं, तो संस्करण को लॉक करने के लिए `-v` फ़्लैग जोड़ें, उदाहरण के लिए, `dotnet add package Aspose.OCR -v 23.10`।

### चरण 2: नया कंसोल प्रोजेक्ट बनाएं (यदि आपके पास नहीं है)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

अब आपके पास एक नया `Program.cs` फ़ाइल तैयार है हमारे कोड के लिए।

---

## अरबी टेक्स्ट निकालें – OCR कोड लिखना

नीचे पूरा, तैयार‑चलाने‑योग्य प्रोग्राम दिया गया है। इसे `Program.cs` के रूप में सहेजें (या ऑटो‑जनरेटेड फ़ाइल को बदलें)।

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### प्रत्येक पंक्ति क्यों महत्वपूर्ण है

- **`OcrEngine`**: वह मुख्य क्लास जो इमेज लोडिंग, भाषा चयन, और रिकग्निशन को समन्वयित करता है।  
- **`Language = OcrLanguage.Arabic`**: अरबी दाएँ‑से‑बाएँ स्क्रिप्ट और विशिष्ट ग्लिफ़्स का उपयोग करती है; भाषा सेट करने से इंजन सही कैरेक्टर मॉडल लागू करता है।  
- **`ImageStream.FromFile`**: PNG, JPEG, BMP और कई अन्य फ़ॉर्मेट संभालता है। यदि आपको कभी `MemoryStream` (जैसे अपलोडेड फ़ाइल) से पढ़ना हो, तो इस कॉल को उसी अनुसार बदलें।  
- **`Recognize()`**: भारी काम करता है—पिक्सेल विश्लेषण, सेगमेंटेशन, और कैरेक्टर वर्गीकरण।  
- **`ocrEngine.Text`**: अंतिम Unicode स्ट्रिंग, आगे की प्रोसेसिंग, स्टोरेज, या डिस्प्ले के लिए तैयार।  

### अपेक्षित आउटपुट

यदि `arabic_sample.png` में वाक्य “مرحبا بالعالم” (Hello World) है, तो कंसोल प्रिंट करेगा:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

यदि आउटपुट गड़बड़ दिखे, तो सुनिश्चित करें कि इमेज स्पष्ट है, भाषा अरबी पर सेट है, और OCR इंजन संस्करण दस्तावेज़ के साथ मेल खाता है।

---

## इमेज को टेक्स्ट में बदलें – सटीकता को ट्यून करना

डिफ़ॉल्ट सेटिंग्स अधिकांश साफ़ स्कैन के लिए काम करती हैं, लेकिन वास्तविक दुनिया की इमेज को अक्सर कुछ अतिरिक्त ट्यूनिंग की जरूरत होती है।

| Setting | क्या करता है | कब उपयोग करें |
|---------|--------------|-------------|
| `ocrEngine.Config.Preprocess = true` | स्वचालित बाइनराइज़ेशन और शोर हटाने को सक्षम करता है। | छायाओं वाले स्कैन किए गए दस्तावेज़। |
| `ocrEngine.Config.Deskew = true` | हल्की झुकाव को सुधारने के लिए इमेज को घुमाता है। | कोण पर ली गई फ़ोटो। |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | पूरी इमेज को एक टेक्स्ट ब्लॉक के रूप में लेता है। | सरल कैप्शन या सिंगल‑लाइन लेबल। |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | केवल अरबी अक्षरों तक पहचान को सीमित करता है। | मिश्रित‑भाषा पृष्ठों पर फॉल्स पॉज़िटिव को कम करता है। |

आप इन पंक्तियों को इंजन बनाने के तुरंत बाद जोड़ सकते हैं:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## PNG से टेक्स्ट पढ़ें – विभिन्न इमेज स्रोतों को संभालना

कभी‑कभी PNG डेटाबेस में रहता है या वेब अनुरोध से आता है। यहाँ एक त्वरित वैरिएंट है जो `byte[]` से पढ़ता है:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

बाकी प्रवाह समान रहता है, जिसका अर्थ है **टेक्स्ट कैसे निकालें** स्रोत की परवाह किए बिना स्थिर रहता है।

---

## टेक्स्ट कैसे निकालें – उन्नत विकल्प और किनारे के मामलों

### 1. मल्टी‑पेज PDF या TIFF

यदि आपको मल्टी‑पेज दस्तावेज़ को OCR करना है, तो प्रत्येक पेज पर लूप करें:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **नोट:** इस स्निपेट के लिए आपको `Aspose.PDF` पैकेज की आवश्यकता होगी।

### 2. भाषा का स्वतः पता लगाना

Aspose.OCR ऑटो‑डिटेक्ट भी प्रदान करता है, लेकिन यह धीमा है। यदि आपको यकीन नहीं है कि इमेज में अरबी या कोई अन्य स्क्रिप्ट है, तो इसे सक्षम करें:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

### 3. प्रदर्शन टिप्स

- **`OcrEngine`** ऑब्जेक्ट को कई इमेज के लिए पुनः उपयोग करें; हर बार नया इंस्टेंस बनाना ओवरहेड जोड़ता है।  
- **समानांतर में चलाएँ** केवल तभी जब आपके पास प्रत्येक थ्रेड के लिए अलग इंजन इंस्टेंस हो—एक ही इंस्टेंस साझा करने से रेस कंडीशन होती है।

---

## निष्कर्ष

हमने C# में **OCR कैसे चलाएँ** को शुरू से अंत तक कवर किया है, आपको दिखाते हुए **अरबी टेक्स्ट निकालें**, **इमेज को टेक्स्ट में बदलें**, **PNG से टेक्स्ट पढ़ें**, और विभिन्न परिदृश्यों में **टेक्स्ट कैसे निकालें** का उत्तर दिया है। सैंपल कोड पूर्ण, स्वतंत्र, और किसी भी .NET कंसोल प्रोजेक्ट में पेस्ट करने के लिए तैयार है।

अगला कदम? `OcrLanguage.Arabic` को कोरियन या सर्बियन सिरिलिक से बदलें और लाइब्रेरी की बहुभाषी शक्ति देखें। शोरयुक्त स्कैन पर सटीकता बढ़ाने के लिए प्री‑प्रोसेसिंग फ़्लैग्स के साथ प्रयोग करें, या OCR रूटीन को वेब API में एकीकृत करें ताकि उपयोगकर्ता इमेज अपलोड कर सकें और तुरंत टेक्स्ट परिणाम प्राप्त कर सकें।

कोडिंग का आनंद लें, और आपके OCR परिणाम हमेशा स्पष्ट रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}