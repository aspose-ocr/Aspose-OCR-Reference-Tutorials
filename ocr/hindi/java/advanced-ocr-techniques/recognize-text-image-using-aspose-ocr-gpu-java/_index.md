---
category: general
date: 2026-02-17
description: Aspose OCR GPU समर्थन के साथ जावा में टेक्स्ट इमेज को जल्दी पहचानें।
  इमेज से टेक्स्ट निकालना सीखें और इष्टतम प्रदर्शन के लिए GPU डिवाइस आईडी सेट करें।
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: hi
og_description: Aspose OCR GPU समर्थन के साथ जावा में टेक्स्ट इमेज को जल्दी पहचानें।
  यह गाइड दिखाता है कि इमेज से टेक्स्ट कैसे निकालें और GPU डिवाइस आईडी कैसे सेट करें।
og_title: Aspose OCR GPU का उपयोग करके टेक्स्ट छवि को पहचानें – जावा
tags:
- Java
- OCR
- Aspose
- GPU
title: Aspose OCR GPU का उपयोग करके टेक्स्ट इमेज को पहचानें – जावा
url: /hi/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU – Java का उपयोग करके टेक्स्ट इमेज को पहचानें

क्या आपको कभी Java एप्लिकेशन में **recognize text image** करने की ज़रूरत पड़ी, लेकिन बड़े फ़ाइलों पर CPU धीमा हो रहा था? आप अकेले नहीं हैं—कई डेवलपर्स हाई‑रिज़ॉल्यूशन स्कैन प्रोसेस करते समय इस समस्या से जूझते हैं। अच्छी खबर? Aspose OCR आपको GPU पर **extract text from image** करने देता है, जिससे प्रोसेसिंग समय में काफी कमी आती है।  

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने योग्य उदाहरण के माध्यम से दिखाएंगे कि लाइसेंस कैसे सेट करें, GPU एक्सेलेरेशन कैसे सक्षम करें, और जब आपके पास कई ग्राफ़िक्स कार्ड हों तो **set gpu device id** कैसे सेट करें। अंत तक आपके पास एक स्व-समाहित प्रोग्राम होगा जो पहचानित टेक्स्ट को कंसोल पर प्रिंट करेगा—कोई अतिरिक्त कदम नहीं।

## आपको क्या चाहिए

- **Java 17** या नया (API Java 8+ के साथ संगत है, लेकिन नवीनतम LTS बेहतर प्रदर्शन देता है)।  
- **Aspose OCR for Java** लाइब्रेरी (Aspose वेबसाइट से JAR डाउनलोड करें)।  
- एक वैध **Aspose OCR license file** (`Aspose.OCR.lic`). फ्री ट्रायल काम करता है, लेकिन GPU फीचर लाइसेंस वाले संस्करण में ही उपलब्ध हैं।  
- एक इमेज फ़ाइल (`sample-image.png`) जिसमें स्पष्ट, मशीन‑रीडेबल टेक्स्ट हो।  
- एक GPU‑सक्षम वातावरण (NVIDIA CUDA‑संगत कार्ड सबसे अच्छा काम करता है)।  

यदि इनमें से कोई भी चीज़ अपरिचित लग रही हो, चिंता न करें—प्रत्येक बुलेट पॉइंट को आगे समझाया जाएगा।

## चरण 1: अपने प्रोजेक्ट में Aspose OCR जोड़ें

सबसे पहले, Aspose OCR JAR को अपने क्लासपाथ में शामिल करें। यदि आप Maven उपयोग कर रहे हैं, तो `pom.xml` में निम्नलिखित डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Gradle के लिए, यह है:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

यदि आप मैन्युअल तरीका पसंद करते हैं, तो JAR को अपने `libs/` फ़ोल्डर में डालें और इसे IDE के मॉड्यूल पाथ में जोड़ें।

> **Pro tip:** लाइब्रेरी के रिलीज़ नोट्स के साथ संस्करण संख्या को सिंक में रखें; नए संस्करण अक्सर GPU प्रोसेसिंग के लिए प्रदर्शन सुधार लाते हैं।

## चरण 2: Aspose OCR लाइसेंस लोड करें (GPU उपयोग के लिए आवश्यक)

लाइसेंस के बिना `setEnableGpu(true)` कॉल चुपचाप CPU मोड पर वापस आ जाएगा। लाइसेंस को `main` की शुरुआत में लोड करें:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

`YOUR_DIRECTORY` को उस फ़ोल्डर के पूर्ण या सापेक्ष पाथ से बदलें जहाँ आपने `.lic` फ़ाइल रखी है। यदि पाथ गलत है, तो Aspose `FileNotFoundException` फेंकेगा, इसलिए वर्तनी दोबारा जांचें।

## चरण 3: OCR इंजन बनाएं और GPU एक्सेलेरेशन सक्षम करें

अब हम `OcrEngine` को इंस्टैंशिएट करते हैं और उसे GPU उपयोग करने के लिए बताते हैं। `setGpuDeviceId` मेथड आपको कई कार्ड मौजूद होने पर एक विशिष्ट कार्ड चुनने की अनुमति देता है।

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

डिवाइस आईडी की ज़रूरत क्यों? मल्टी‑GPU सर्वर में आप एक कार्ड को इमेज प्री‑प्रोसेसिंग के लिए और दूसरे को OCR के लिए आरक्षित कर सकते हैं। आईडी सेट करने से सही हार्डवेयर भारी काम संभालता है।

## चरण 4: इनपुट इमेज तैयार करें

Aspose OCR विभिन्न फ़ॉर्मैट (PNG, JPG, BMP, TIFF) को सपोर्ट करता है। अपनी फ़ाइल को `OcrInput` ऑब्जेक्ट में रैप करें:

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

यदि आपको स्ट्रीम प्रोसेस करनी है (जैसे अपलोड की गई फ़ाइल), तो `ocrInput.add(InputStream)` का उपयोग करें।

## चरण 5: पहचान प्रक्रिया चलाएँ और परिणाम प्राप्त करें

`recognize` मेथड एक `OcrResult` लौटाता है जिसमें प्लेन टेक्स्ट, कॉन्फिडेंस स्कोर, और यदि आवश्यक हो तो लेआउट जानकारी भी होती है।

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

कंसोल कुछ इस तरह दिखेगा:

```
Recognized text:
Hello, world!
This is a sample image.
```

यदि इमेज धुंधली है या भाषा समर्थित नहीं है, तो परिणाम खाली हो सकता है। ऐसे में `ocrResult.getConfidence()` वैल्यू (0‑100) जांचें और प्री‑प्रोसेसिंग के साथ फिर से प्रयास करने का निर्णय लें।

## पूर्ण, चलाने योग्य उदाहरण

सभी हिस्सों को मिलाकर आपको एक सिंगल Java क्लास मिलेगा जिसे आप अपने IDE में कॉपी‑पेस्ट कर सकते हैं:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Expected output:** कंसोल `sample-image.png` में दिखाई देने वाला सटीक टेक्स्ट प्रिंट करेगा। यदि GPU सक्रिय है, तो आप देखेंगे कि प्रोसेसिंग समय सामान्य 300 dpi स्कैन के लिए कई सेकंड (CPU) से घटकर एक सेकंड से भी कम हो जाता है।

## सामान्य प्रश्न और किनारे के मामलों

### क्या यह हेडलेस सर्वर पर काम करता है?

हां। GPU ड्राइवर इंस्टॉल होना चाहिए, लेकिन डिस्प्ले की ज़रूरत नहीं है। बस सुनिश्चित करें कि `CUDA` टूलकिट (या आपके GPU के लिए समकक्ष) सिस्टम `PATH` में हो।

### अगर मेरे पास एक से अधिक GPU हैं और मैं GPU 1 उपयोग करना चाहता हूँ तो क्या करें?

डिवाइस आईडी बदलें:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### अलग भाषा में इमेज से टेक्स्ट निकालने के लिए कैसे करें?

`recognize` कॉल करने से पहले भाषा सेट करें:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose 30 से अधिक भाषाओं को सपोर्ट करता है; पूरी सूची के लिए API डॉक्यूमेंटेशन देखें।

### अगर इमेज में कई पेज हैं (जैसे PDF को इमेज में बदला गया हो) तो क्या करें?

प्रत्येक पेज के लिए एक अलग `OcrInput` एंट्री बनाएं, या फ़ाइलों पर लूप चलाएँ:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

इंजन क्रम में परिणामों को जोड़ देगा।

### कम‑विश्वास वाले परिणामों को कैसे संभालें?

कॉन्फिडेंस स्कोर जांचें:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

आम प्री‑प्रोसेसिंग स्टेप्स में बाइनराइज़ेशन, नॉइज़ रिडक्शन, या 300 dpi पर रिसाइज़िंग शामिल हैं।

## प्रदर्शन टिप्स

- **Batch processing:** कई इमेज को एक ही `OcrInput` में जोड़ने से GPU कॉन्टेक्स्ट को बार‑बार इनिशियलाइज़ करने का ओवरहेड कम होता है।  
- **Warm‑up:** JVM शुरू करने के बाद एक डमी रिकग्निशन चलाएँ; पहला कॉल ड्राइवर इनिशियलाइज़ेशन लेटेंसी लाता है।  
- **Memory management:** बड़े `OcrInput` ऑब्जेक्ट्स (`ocrInput.clear()`) को उपयोग के बाद डिस्पोज़ करें ताकि GPU मेमोरी मुक्त हो सके।  

## निष्कर्ष

आप अब जानते हैं कि Java में Aspose OCR के GPU इंजन के साथ **recognize text image** को प्रभावी ढंग से कैसे किया जाए, किसी भी समर्थित भाषा में **extract text from image** कैसे किया जाए, और कई ग्राफ़िक्स कार्ड के साथ काम करते समय **set gpu device id** कैसे सेट किया जाए। ऊपर दिया गया पूर्ण, चलाने योग्य कोड बॉक्स‑आउट‑ऑफ़‑द‑बॉक्स काम करेगा—बस अपनी लाइसेंस और इमेज पाथ बदलें।

अगले कदम के लिए तैयार हैं? स्कैन किए गए PDFs के फ़ोल्डर को प्रोसेस करने की कोशिश करें, विभिन्न `setLanguage` विकल्पों के साथ प्रयोग करें, या OCR को पोस्ट‑प्रोसेसिंग के लिए मशीन‑लर्निंग मॉडल के साथ मिलाएँ। संभावनाएँ असीमित हैं, और GPU एक्सेलेरेशन से मिलने वाले प्रदर्शन लाभ बड़े‑पैमाने के प्रोजेक्ट्स को भी संभव बनाते हैं।

हैप्पी कोडिंग, और यदि कोई समस्या आए तो टिप्पणी करके बताएं!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}