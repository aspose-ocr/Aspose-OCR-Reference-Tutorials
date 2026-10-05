---
category: general
date: 2026-02-19
description: OCR के लिए छवि को डेस्क्यू करने और शोर हटाने के तरीके सीखें। यह ट्यूटोरियल
  दिखाता है कि टेक्स्ट इमेज को कैसे पहचानें, इमेज की घूर्णन को कैसे सुधारें, और Aspose
  OCR के साथ इमेज OCR को कैसे प्री‑प्रोसेस करें।
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: hi
og_description: इमेज को डेस्क्यू कैसे करें और शोर को साफ़ करें ताकि आप टेक्स्ट इमेज
  को तेज़ी से पहचान सकें। इमेज रोटेशन को सही करने और Aspose के साथ इमेज OCR को प्री‑प्रोसेस
  करने के लिए इस गाइड का पालन करें।
og_title: इमेज को डेस्क्यू कैसे करें – पूर्ण OCR प्री‑प्रोसेसिंग ट्यूटोरियल
tags:
- OCR
- Java
- Image Processing
title: इमेज को डेस्क्यू कैसे करें — चरण‑दर‑चरण OCR प्री‑प्रोसेसिंग गाइड
url: /hi/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Deskew Image — Complete OCR Pre‑Processing Tutorial

क्या आप कभी **छवि को डेस्क्यू कैसे करें** यह सोचते रहे हैं, OCR इंजन को फ़ीड करने से पहले? शायद आपने रसीदों का एक बैच स्कैन किया है, और पृष्ठ थोड़ा झुके हुए दिखते हैं, या स्कैन में यादृच्छिक बिंदु बिखरे हुए हैं। यह एक आम समस्या है—झुके हुए, शोरयुक्त चित्र टेक्स्ट पहचान में बाधा डालते हैं।  

अच्छी खबर? आप Aspose.OCR का उपयोग करके कुछ ही Java लाइनों में इमेज को सीधा (इमेज रोटेशन सुधार) और शोर हटाने (शोर कैसे हटाएँ) कर सकते हैं। इस गाइड में हम पूरी प्रक्रिया को देखेंगे: शोरयुक्त‑झुकी हुई PNG को लोड करना, डेस्क्यू + मीडियन डिनॉइज़ लागू करना, और **टेक्स्ट इमेज को पहचानना** और परिणाम प्रिंट करना। अंत तक आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जिसे आप किसी भी Java प्रोजेक्ट में डाल सकते हैं।

## What You’ll Need

- **Java 17** या नया (कोड पुराने संस्करणों के साथ भी कम्पाइल हो सकता है, लेकिन 17 सबसे उपयुक्त है)।  
- **Aspose.OCR for Java** – आप नवीनतम JAR Maven Central से प्राप्त कर सकते हैं (`com.aspose:aspose-ocr`)।  
- एक इमेज फ़ाइल जो दोनों ही झुकी हुई और शोरयुक्त हो (जैसे `noisy-rotated.png`)।  
- एक साधारण IDE (IntelliJ, Eclipse, या यहाँ तक कि VS Code)।  

कोई जटिल बिल्ड टूल आवश्यक नहीं; एक साधारण `javac` + `java` रन पर्याप्त है।

---

## Step 1 – Create the OCR Engine Instance  

पहला काम है `OcrEngine` को इनिशियलाइज़ करना। इसे वह दिमाग समझें जो बाद में आपके लिए अक्षरों को पढ़ेगा।

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tip:** यदि आप कई इमेज प्रोसेस कर रहे हैं तो इंजन को सिंगलटन के रूप में रखें; यह आंतरिक बफ़र्स को पुन: उपयोग करता है और गति बढ़ाता है।

## Step 2 – Enable Deskew and Median Denoise (How to Remove Noise)

अब हम इंजन को **इमेज रोटेशन सुधार** और **शोर कैसे हटाएँ** बताते हैं। दोनों फ़िल्टर वैकल्पिक हैं, लेकिन साथ में उपयोग करने से सटीकता में काफी सुधार होता है।

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

मीडियन डिनॉइज़ क्यों? यह किनारों (अक्षरों को परिभाषित करने वाली रेखाएँ) को बनाए रखता है जबकि अलग‑अलग पिक्सेल को हटाता है—एक साफ़ OCR के लिए बिल्कुल सही।

## Step 3 – Load the Image You Want to Process  

यहाँ हम इंजन को उस फ़ाइल की ओर इंगित करते हैं जिसे साफ़ करना है। `ImageStream.fromFile` PNG को मेमोरी में पढ़ता है।

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

यदि आपकी इमेज रिमोट सर्वर पर है, तो बस `InputStream` पास करें—Aspose इसे सहजता से संभालता है।

## Step 4 – Run OCR and Capture the Recognized Text  

प्रिप्रोसेसिंग सक्षम होने के बाद, इंजन अब सुधारी गई इमेज को पढ़ता है। `recognize()` कॉल एक `RecognitionResult` लौटाता है जिसमें निकाली गई स्ट्रिंग होती है।

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

आपको कंसोल में साफ़, पठनीय टेक्स्ट दिखना चाहिए, भले ही मूल चित्र झुका हुआ और धुंधला हो।

## Step 5 – Verify the Result (What to Expect)

जब सब कुछ सही चलता है, तो कंसोल कुछ इस तरह प्रिंट करता है:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

यदि आउटपुट में अभी भी गड़बड़ अक्षर दिखें, तो जाँचें:

- इमेज रेज़ोल्यूशन (≥ 300 dpi आदर्श है)।  
- फ़ाइल पाथ सही है या नहीं।  
- क्या अतिरिक्त फ़िल्टर (जैसे `setContrastStretch`) मदद कर सकते हैं।

---

## Optional: Visual Confirmation with an Example Image  

नीचे एक झुकी हुई, शोरयुक्त रसीद की छोटी प्रीव्यू है। झुकाव देखें—हमारा कोड इसे आपके लिए सीधा कर देगा।

![छवि को डेस्क्यू करने का उदाहरण](deskew-demo.png "छवि को डेस्क्यू करने का तरीका")

*Alt text: छवि को डेस्क्यू करने का उदाहरण – प्रोसेसिंग से पहले और बाद।*

---

## Frequently Asked Questions

### Does this work with PDFs or only PNG/JPEG?  
Aspose.OCR सीधे PDFs पढ़ सकता है; बस `ImageStream.fromFile` को `ImageStream.fromPdf` से बदलें। वही प्री‑प्रोसेसिंग फ़्लैग लागू होते हैं, इसलिए आप अभी भी **छवि को डेस्क्यू कैसे करें** और **शोर कैसे हटाएँ** प्राप्त करेंगे।

### What if I need to keep the original orientation for later steps?  
आप प्री‑प्रोसेसिंग से पहले इमेज को क्लोन कर सकते हैं:

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### Can I change the deskew angle manually?  
हां—`setDeskewAngle(double degrees)` आपको ऑटो‑डिटेक्ट एल्गोरिद्म को ओवरराइड करने की अनुमति देता है। यह तब उपयोगी होता है जब ऑटो‑डिटेक्ट अत्यधिक रोटेशन पर फेल हो जाता है।

### How does median denoise differ from Gaussian blur?  
मीडियन फ़िल्टर प्रत्येक पिक्सेल को उसके पड़ोसियों के मीडियन से बदलता है, जिससे किनारे संरक्षित रहते हैं। Gaussian ब्लर सब कुछ स्मूद कर देता है, जिससे अक्षर की स्ट्रोक भी धुंधली हो सकती है—इसलिए OCR के लिए मीडियन अधिक सुरक्षित विकल्प है।

---

## Wrapping Up  

इस ट्यूटोरियल में हमने **छवि को डेस्क्यू कैसे करें** को कवर किया, **शोर कैसे हटाएँ** को प्रदर्शित किया, और Aspose OCR के बिल्ट‑इन प्री‑प्रोसेसिंग का उपयोग करके **टेक्स्ट इमेज को पहचानना** दिखाया। `setDeskew(true)` और `setMedianDenoise(true)` को सक्षम करके आप स्वचालित रूप से **इमेज रोटेशन सुधार** और स्पीकल्स को साफ़ कर सकते हैं, जिससे एक गंदा स्कैन साफ़ टेक्स्ट स्ट्रिंग में बदल जाता है।  

बिना झिझक प्रयोग करें: विभिन्न डिनॉइज़ रणनीतियों को आज़माएँ, PDFs फीड करें, या लूप में कई इमेज प्रोसेस करें। वही पैटर्न—इंजन → प्री‑प्रोसेस → पहचान—हर परिदृश्य में लागू होता है, जिससे यह किसी भी OCR पाइपलाइन के लिए एक ठोस आधार बन जाता है।

**अगले कदम** जिन्हें आप एक्सप्लोर कर सकते हैं:

- **बैच प्रोसेसिंग** – इमेज फ़ोल्डर पर इटररेट करें और प्रत्येक परिणाम को `.txt` फ़ाइल में लिखें।  
- **भाषा पैक्स** – विशिष्ट भाषा शब्दकोश लोड करके गैर‑अंग्रेज़ी टेक्स्ट की सटीकता बढ़ाएँ।  
- **एडवांस्ड फ़िल्टर** – जैसे `setContrastStretch` या `setBinarization` कम कॉन्ट्रास्ट स्कैन के लिए।  

और सवाल हैं? टिप्पणी करें, और कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}