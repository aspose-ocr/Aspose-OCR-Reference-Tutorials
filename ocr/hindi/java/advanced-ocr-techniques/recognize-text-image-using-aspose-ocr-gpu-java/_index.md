---
category: general
date: 2026-10-30
description: Java में Aspose OCR GPU सपोर्ट के साथ इमेज से तेज़ी से टेक्स्ट निकालना
  सीखें। यह गाइड दिखाता है कि GPU device ID कैसे सेट करें और हाई‑परफ़ॉर्मेंस OCR प्राप्त
  करें।
draft: false
keywords:
- extract text from image
- how to extract text
- aspose ocr gpu
- recognize text image java
- gpu acceleration OCR
lastmod: 2026-10-30
og_description: Java में Aspose OCR GPU सपोर्ट के साथ इमेज से तेज़ी से टेक्स्ट निकालना
  सीखें। यह गाइड दिखाता है कि GPU device ID को ऑप्टिमल परफ़ॉर्मेंस के लिए कैसे सेट
  करें।
og_image_alt: 'Developer guide: extract text from image using Aspose OCR GPU in Java'
og_title: Java में Aspose OCR GPU के साथ इमेज से टेक्स्ट निकालने का तरीका
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to extract text from image quickly with Aspose OCR GPU support
    in Java. This guide shows how to set GPU device ID and achieve high‑performance
    OCR.
  headline: How to extract text from image with Aspose OCR GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—just install a valid Aspose OCR license. The free trial is for evaluation
      only.
    question: Can I use this in a commercial application?
  - answer: Absolutely; as long as the NVIDIA driver and CUDA toolkit are installed,
      the library runs on headless Linux environments.
    question: Does the GPU version work on Linux servers?
  - answer: Aspose OCR can process images up to **5000 × 5000 px** without loading
      the whole file into memory.
    question: What is the maximum image size supported?
  - answer: Replace the old JAR with the new one and update your Maven/Gradle dependency
      version number.
    question: How do I upgrade to the latest Aspose OCR version?
  - answer: Yes—`OcrResult` provides layout information, including word‑level bounding
      boxes, when you enable the `setIncludeLayout(true)` option.
    question: Is there a way to get bounding‑box coordinates for each word?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: Java में Aspose OCR GPU के साथ इमेज से टेक्स्ट निकालने का तरीका
url: /hi/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# छवि से टेक्स्ट निकालने के लिए Aspose OCR GPU को Java में कैसे उपयोग करें

यदि आपने कभी Java एप्लिकेशन में **छवि से टेक्स्ट निकालने** की कोशिश की है और पाया कि उच्च‑रिज़ॉल्यूशन स्कैन पर CPU संघर्ष कर रहा है, तो आप अकेले नहीं हैं। बड़े दस्तावेज़ों को प्रोसेस करते समय कई डेवलपर्स प्रदर्शन बाधाओं का सामना करते हैं। Aspose OCR for Java इस समस्या को GPU पर OCR चलाकर हल करता है, जिससे प्रोसेसिंग समय में नाटकीय कमी आती है। इस ट्यूटोरियल में आप एक पूर्ण, तैयार‑चलाने योग्य उदाहरण देखेंगे जो लाइसेंस सेट करने, GPU एक्सेलेरेशन सक्षम करने, और कई ग्राफ़िक्स कार्ड मौजूद होने पर **set gpu device id** दिखाता है।

## त्वरित उत्तर
- **Java में छवि से टेक्स्ट निकालने का सबसे तेज़ तरीका क्या है?** GPU एक्सेलेरेशन के साथ Aspose OCR का उपयोग करें और उपयुक्त GPU डिवाइस ID सेट करें।  
- **कौन सा Java संस्करण आवश्यक है?** सर्वोत्तम प्रदर्शन के लिए Java 17 या नया संस्करण सुझाया जाता है।  
- **क्या GPU समर्थन के लिए लाइसेंस चाहिए?** हाँ—GPU फीचर्स केवल वैध Aspose OCR लाइसेंस के साथ ही अनलॉक होते हैं।  
- **क्या इसे हेडलेस सर्वर पर चलाया जा सकता है?** बिल्कुल; केवल GPU ड्राइवर और CUDA टूलकिट आवश्यक हैं।  
- **कितनी भाषाएँ समर्थित हैं?** 30 से अधिक भाषाएँ, जिनमें English, Chinese, Arabic, और Hindi शामिल हैं।

## छवि से टेक्स्ट निकालना क्या है?
छवि से टेक्स्ट निकालना का अर्थ है PNG, JPG, या TIFF जैसे बिटमैप फ़ॉर्मेट में संग्रहीत अक्षरों की दृश्य प्रस्तुति को संपादन योग्य, खोज योग्य Unicode टेक्स्ट में बदलना। इस प्रक्रिया को ऑप्टिकल कैरेक्टर रिकग्निशन (OCR) कहा जाता है, जो इंडेक्सिंग, अनुवाद, और डेटा एक्सट्रैक्शन जैसे डाउनस्ट्रीम कार्यों को सक्षम करती है।

## Aspose OCR GPU का उपयोग क्यों करें?
Aspose OCR GPU एक्सेलेरेशन का उपयोग करके बड़े, हाई‑रिज़ॉल्यूशन इमेज को CPU‑केवल प्रोसेसिंग की तुलना में बहुत अधिक कुशलता से संभालता है। यह 30 से अधिक इनपुट फ़ॉर्मेट का समर्थन करता है और 5000 × 5000 px तक की इमेज को कम मेमोरी उपयोग के साथ प्रोसेस कर सकता है, जिससे आधुनिक NVIDIA GPUs पर पहचान गति पाँच गुना तक तेज़ हो जाती है।

## आप क्या चाहिए
- **Java 17** या नया (Java 8+ के साथ संगत, लेकिन LTS रिलीज़ बेहतर JIT प्रदर्शन देती हैं)।  
- **Aspose OCR for Java** लाइब्रेरी (Aspose वेबसाइट से JAR डाउनलोड करें)।  
- एक वैध **Aspose OCR लाइसेंस फ़ाइल** (`Aspose.OCR.lic`). फ्री ट्रायल काम करता है, लेकिन GPU फीचर्स के लिए लाइसेंस्ड संस्करण आवश्यक है।  
- एक इमेज फ़ाइल (`sample-image.png`) जिसमें स्पष्ट, मशीन‑रीडेबल टेक्स्ट हो।  
- एक CUDA‑संगत NVIDIA GPU (या समकक्ष) जिसमें उचित ड्राइवर स्थापित हो।

यदि इनमें से कोई भी परिचित नहीं लग रहा है, तो चिंता न करें—प्रत्येक बिंदु को आगे समझाया जाएगा।

## चरण 1: अपने प्रोजेक्ट में Aspose OCR जोड़ें
सबसे पहले, Aspose OCR JAR को अपने क्लासपाथ में शामिल करें। यदि आप Maven उपयोग कर रहे हैं, तो `pom.xml` में निम्नलिखित डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Gradle के लिए, उपयोग करें:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

यदि आप मैनुअल तरीका पसंद करते हैं, तो JAR को `libs/` फ़ोल्डर में डालें और इसे IDE के मॉड्यूल पाथ में जोड़ें।

> **Pro tip:** संस्करण संख्या को रिलीज़ नोट्स के साथ संरेखित रखें; नए संस्करण अक्सर GPU प्रोसेसिंग के लिए प्रदर्शन सुधार शामिल करते हैं।

## चरण 2: Aspose OCR लाइसेंस लोड करें (GPU उपयोग के लिए आवश्यक)
लाइसेंस के बिना `setEnableGpu(true)` कॉल चुपचाप CPU मोड में वापस आ जाएगा। लाइसेंस को `main` की शुरुआत में लोड करें:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

`YOUR_DIRECTORY` को उस पूर्ण या सापेक्ष पथ से बदलें जहाँ आपने `.lic` फ़ाइल रखी है। गलत पथ `FileNotFoundException` उत्पन्न करेगा, इसलिए वर्तनी दोबारा जांचें।

## चरण 3: OCR इंजन बनाएं और GPU एक्सेलेरेशन सक्षम करें
`OcrEngine` क्लास वह मुख्य घटक है जो इमेज पर OCR ऑपरेशन करता है।

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

डिवाइस ID की ज़रूरत क्यों? मल्टी‑GPU वातावरण में आप एक कार्ड को प्री‑प्रोसेसिंग और दूसरे को OCR के लिए समर्पित कर सकते हैं। ID सेट करने से सुनिश्चित होता है कि भारी काम इच्छित हार्डवेयर पर चले।

## चरण 4: इनपुट इमेज तैयार करें
`OcrInput` क्लास उन इमेजों के संग्रह को दर्शाती है जिन्हें आप प्रोसेस करना चाहते हैं।

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

यदि आपको स्ट्रीम (जैसे अपलोड की गई फ़ाइल) प्रोसेस करनी है, तो `ocrInput.add(InputStream)` का उपयोग करें।

## चरण 5: पहचान प्रक्रिया चलाएँ और परिणाम प्राप्त करें
`OcrResult` क्लास प्लेन टेक्स्ट, कॉन्फिडेंस स्कोर, और वैकल्पिक लेआउट जानकारी को समेटे हुए है जो इंजन द्वारा लौटाई जाती है।

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

कंसोल कुछ इस प्रकार दिखाएगा:

```
Recognized text:
Hello, world!
This is a sample image.
```

यदि इमेज धुंधली है या भाषा समर्थित नहीं है, तो परिणाम खाली हो सकता है। ऐसे में `ocrResult.getConfidence()` मान (0‑100) देखें और प्री‑प्रोसेसिंग के साथ पुनः प्रयास करने का निर्णय लें।

## पूर्ण, चलाने योग्य उदाहरण
सभी भागों को मिलाकर आपको एक सिंगल Java क्लास मिलता है जिसे आप अपने IDE में कॉपी‑पेस्ट कर सकते हैं:

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

> **Expected output:** कंसोल `sample-image.png` में दिखाई देने वाला सटीक टेक्स्ट प्रिंट करेगा। जब GPU सक्रिय होता है, तो प्रोसेसिंग समय सामान्य 300 dpi स्कैन के लिए कई सेकंड (CPU) से घटकर एक सेकंड से भी कम हो जाता है।

## सामान्य प्रश्न और किनारे के मामले

### क्या यह हेडलेस सर्वर पर काम करता है?
हां। GPU ड्राइवर स्थापित होना चाहिए, लेकिन डिस्प्ले की आवश्यकता नहीं है। सुनिश्चित करें कि `CUDA` टूलकिट (या आपके GPU के समकक्ष) सिस्टम `PATH` में उपलब्ध हो। यह सेटअप OCR को क्लाउड‑आधारित या कंटेनराइज़्ड वातावरण में बिना ग्राफ़िकल इंटरफ़ेस के चलाने की अनुमति देता है।

### यदि मेरे पास एक से अधिक GPU हैं और मैं GPU 1 उपयोग करना चाहता हूँ तो क्या करें?
डिवाइस ID को इस प्रकार बदलें:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

ID को `1` सेट करने से OCR इंजन सिस्टम में दूसरे GPU का उपयोग करेगा, जो तब उपयोगी होता है जब पहला GPU अन्य वर्कलोड के लिए आरक्षित हो।

### विभिन्न भाषा में छवि से टेक्स्ट कैसे निकालें?
`recognize` कॉल करने से पहले भाषा सेट करें:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose OCR **30 से अधिक भाषाओं** का समर्थन करता है, जिसमें Arabic और Hebrew जैसे राइट‑टू‑लेफ़्ट स्क्रिप्ट भी शामिल हैं। सही भाषा चुनने से सटीकता में नाटकीय सुधार होता है।

### यदि इमेज में कई पेज हैं (जैसे PDF को इमेज में बदलना) तो क्या करें?
प्रत्येक पेज के लिए एक अलग `OcrInput` एंट्री बनाएं, या फ़ाइलों पर लूप चलाएँ:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

इंजन परिणामों को क्रम में जोड़ता है, जिससे अंतिम आउटपुट में पेज क्रम बना रहता है।

### कम‑विश्वास परिणामों को कैसे संभालें?
कॉन्फिडेंस स्कोर जांचें:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

आम प्री‑प्रोसेसिंग चरणों में बाइनराइज़ेशन, शोर कम करना, या 300 dpi पर रिसाइज़ करना शामिल है। ऐसे प्री‑प्रोसेसिंग के बाद OCR फिर चलाने से अक्सर कॉन्फिडेंस स्तर बढ़ जाता है।

## प्रदर्शन सुझाव
- **Batch processing:** कई इमेज को एक ही `OcrInput` में जोड़ने से GPU कॉन्टेक्स्ट को बार‑बार इनिशियलाइज़ करने की ओवरहेड कम होती है।  
- **Warm‑up:** JVM शुरू करने के बाद एक डमी रिकग्निशन चलाएँ; पहली कॉल में ड्राइवर इनिशियलाइज़ेशन लेटेंसी लगती है।  
- **Memory management:** बड़े `OcrInput` ऑब्जेक्ट्स (`ocrInput.clear()`) को उपयोग समाप्त होने पर डिस्पोज़ करें ताकि GPU मेमोरी मुक्त हो सके।  

## निष्कर्ष
आप अब जानते हैं कि **छवि से टेक्स्ट निकालना** Aspose OCR के GPU इंजन के साथ Java में कैसे कुशलता से किया जाता है, कई ग्राफ़िक्स कार्ड के साथ काम करते समय **set gpu device id** कैसे सेट किया जाता है, और बहु‑भाषी परिदृश्यों को कैसे संभालें। ऊपर दिया गया पूर्ण, चलाने योग्य कोड बॉक्स‑ऑफ़‑टेक्स्ट काम करना चाहिए—सिर्फ अपने लाइसेंस और इमेज पाथ बदलें।

अगला कदम तैयार है? पूरे स्कैन किए गए PDF फ़ोल्डर को प्रोसेस करने, विभिन्न `setLanguage` विकल्पों के साथ प्रयोग करने, या OCR आउटपुट को पोस्ट‑प्रोसेसिंग के लिए मशीन‑लर्निंग मॉडल के साथ संयोजित करने की कोशिश करें। GPU एक्सेलेरेशन से मिलने वाले प्रदर्शन लाभ बड़े‑पैमाने के प्रोजेक्ट्स को संभव बनाते हैं।

कोडिंग का आनंद लें, और यदि कोई समस्या आती है तो टिप्पणी छोड़ने में संकोच न करें!

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं इसे व्यावसायिक एप्लिकेशन में उपयोग कर सकता हूँ?**  
A: हाँ—सिर्फ एक वैध Aspose OCR लाइसेंस स्थापित करें। फ्री ट्रायल केवल मूल्यांकन के लिए है।

**Q: क्या GPU संस्करण Linux सर्वर पर काम करता है?**  
A: बिल्कुल; जब तक NVIDIA ड्राइवर और CUDA टूलकिट स्थापित हैं, लाइब्रेरी हेडलेस Linux वातावरण में चलती है।

**Q: अधिकतम समर्थित इमेज आकार क्या है?**  
A: Aspose OCR पूरी फ़ाइल मेमोरी में लोड किए बिना **5000 × 5000 px** तक की इमेज प्रोसेस कर सकता है।

**Q: नवीनतम Aspose OCR संस्करण में कैसे अपग्रेड करूँ?**  
A: पुराना JAR नए से बदलें और अपने Maven/Gradle डिपेंडेंसी संस्करण संख्या को अपडेट करें।

**Q: क्या प्रत्येक शब्द के बाउंडिंग‑बॉक्स कोऑर्डिनेट्स प्राप्त करने का तरीका है?**  
A: हाँ—`OcrResult` लेआउट जानकारी देता है, जिसमें शब्द‑स्तर बाउंडिंग बॉक्स शामिल हैं, जब आप `setIncludeLayout(true)` विकल्प सक्षम करते हैं।

**अंतिम अपडेट:** 2026-10-30  
**परीक्षित संस्करण:** Aspose OCR for Java 24.11  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल

- [GPU एक्सेलेरेशन के साथ Java OCR में इमेज से टेक्स्ट पहचानें](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [Java में OCR के लिए GPU कैसे सक्षम करें और इमेज से टेक्स्ट निकालें](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [Aspose OCR Java के साथ इमेज से टेक्स्ट निकालने की त्वरित गाइड](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}