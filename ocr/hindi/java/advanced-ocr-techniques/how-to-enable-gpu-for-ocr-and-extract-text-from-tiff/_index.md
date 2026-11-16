---
category: general
date: 2026-09-23
description: Aspose OCR for Java में GPU एक्सेलेरेशन सक्षम करके TIFF फ़ाइल से तेज़ी
  से टेक्स्ट निकालना सीखें। चरण‑दर‑चरण गाइड में TIFF लोड करना, GPU डिवाइस ID सेट करना,
  और टेक्स्ट पढ़ना शामिल है।
draft: false
keywords:
- extract text from tiff file
- gpu acceleration java
- ocr tiff java
- aspose ocr gpu
lastmod: 2026-09-23
og_description: Aspose OCR for Java में GPU एक्सेलेरेशन सक्षम करके TIFF फ़ाइल से तेज़ी
  से टेक्स्ट निकालना सीखें। गाइड में TIFF लोड करना, GPU डिवाइस चुनना, और निकाले गए
  टेक्स्ट को पढ़ना दिखाया गया है।
og_image_alt: 'Tutorial image: enabling GPU for OCR in Java'
og_title: OCR Java में GPU एक्सेलेरेशन के साथ TIFF फ़ाइल से टेक्स्ट निकालें
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to extract text from tiff file quickly by enabling GPU acceleration
    in Aspose OCR for Java. Step‑by‑step guide covers loading TIFF, setting GPU device
    ID, and reading text.
  headline: How to extract text from tiff file using GPU in OCR Java
  type: TechArticle
- questions:
  - answer: Absolutely—Aspose OCR runs on Windows, Linux, and macOS as long as the
      CUDA toolkit and drivers are installed.
    question: Does this work on Linux?
  - answer: Omit the `setUseGpu(true)` call or explicitly call `setUseGpu(false)`;
      the engine will run on CPU.
    question: What if I don’t have a GPU?
  - answer: Yes. `setImage` accepts JPEG, PNG, BMP, PDF, and more.
    question: Can I extract text from other formats?
  - answer: Accuracy drops sharply below 300 dpi. Pre‑process the image (binarization,
      deskew) for better results.
    question: How accurate is OCR on low‑resolution TIFFs?
  - answer: The library handles 30+ raster and document formats, including TIFF, JPEG,
      PNG, BMP, PDF, and GIF.
    question: How many formats does Aspose OCR support?
  type: FAQPage
tags:
- OCR
- Java
- GPU acceleration
title: GPU का उपयोग करके OCR Java में TIFF फ़ाइल से टेक्स्ट कैसे निकालें
url: /hi/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU का उपयोग करके OCR Java में TIFF फ़ाइल से टेक्स्ट निकालना कैसे करें

यदि आपको **tiff फ़ाइल से टेक्स्ट निकालना** जल्दी चाहिए, तो Aspose OCR for Java में GPU एक्सेलेरेशन चालू करना सबसे तेज़ तरीका है। पहले 100 शब्दों में हम बताएँगे कि GPU क्यों महत्वपूर्ण है, फिर आपको TIFF लोड करने, GPU सक्षम करने, वैकल्पिक रूप से एक विशिष्ट डिवाइस चुनने, OCR चलाने, और अंत में निकाले गए टेक्स्ट को पढ़ने की प्रक्रिया दिखाएँगे। अंत तक आप कुछ ही कोड लाइनों में TIFF को टेक्स्ट में बदल सकेंगे।

## त्वरित उत्तर
- **GPU OCR का मुख्य लाभ क्या है?** बड़े मल्टी‑पेज TIFFs के लिए 5× तक तेज़ प्रोसेसिंग।  
- **कौन सा Java संस्करण आवश्यक है?** Java 17 या नया (Java 8+ भी काम करता है)।  
- **क्या मुझे विशेष लाइसेंस चाहिए?** उत्पादन उपयोग के लिए एक वैध Aspose OCR for Java लाइसेंस आवश्यक है।  
- **क्या मैं इसे Linux पर चला सकता हूँ?** हां—Aspose OCR क्रॉस‑प्लेटफ़ॉर्म है; बस CUDA टूलकिट इंस्टॉल करें।  
- **क्या GPU वैकल्पिक है?** `setUseGpu(false)` कॉल करके आप CPU पर वापस जा सकते हैं।

## OcrEngine क्या है?
`OcrEngine` क्लास Aspose OCR for Java का मुख्य घटक है। यह सभी OCR कार्यक्षमता को संलग्न करता है, जिससे आप इमेज लोड कर सकते हैं, भाषा और GPU उपयोग जैसी प्रोसेसिंग विकल्पों को कॉन्फ़िगर कर सकते हैं, और पहचाने गए टेक्स्ट और कॉन्फिडेंस डेटा को एक सुविधाजनक ऑब्जेक्ट में प्राप्त कर सकते हैं।

`OcrEngine` Aspose OCR की कोर क्लास है जो OCR प्रोसेसिंग इंजन को दर्शाती है और इमेज लोड करने, विकल्प कॉन्फ़िगर करने, और परिणाम प्राप्त करने के मेथड प्रदान करती है।

## Java में OCR के लिए GPU कैसे सक्षम करें?
अपनी इमेज लोड करें, GPU चालू करें, और `recognize` कॉल करें—बस इतना ही चाहिए। `setUseGpu(true)` के साथ GPU सक्षम करने से इंजन पिक्सेल‑गहन कार्य को ग्राफ़िक्स कार्ड पर ऑफ़लोड कर देता है, जिससे प्रोसेसिंग समय काफी घट जाता है, विशेष रूप से हाई‑रिज़ॉल्यूशन या मल्टी‑पेज TIFFs के लिए।

## आपको क्या चाहिए
- Java 17 या नया (कोड Java 8+ पर भी चलता है)।  
- Aspose OCR for Java 23.10 (या नवीनतम रिलीज़)।  
- नवीनतम ड्राइवर के साथ स्थापित CUDA‑संगत GPU।  
- एक सैंपल मल्टी‑पेज TIFF फ़ाइल (उदाहरण के लिए `sample_large.tif`)।  

Maven नहीं है? बस JAR को अपने क्लासपाथ में डाल दें।

![GPU सक्षम करने का ट्यूटोरियल](gpu-ocr.png)

[GPU सक्षम करने का ट्यूटोरियल](gpu-ocr.png)

*Image alt text: Java में OCR के लिए GPU सक्षम करना*

## चरण 1: OCR के लिए TIFF इमेज लोड करें

`setImage` मेथड फ़ाइल को `ImageStream` में रैप करता है, जिससे इंजन मैन्युअल स्प्लिटिंग के बिना मल्टी‑पेज TIFFs को संभाल सकता है। यदि फ़ाइल नहीं मिलती, तो एक स्पष्ट `FileNotFoundException` फेंका जाता है।

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **यह क्यों महत्वपूर्ण है:** `setImage` कॉल पेज हैंडलिंग को एब्स्ट्रैक्ट कर देती है, इसलिए आप एक ही इंजन इंस्टेंस से पूरे दस्तावेज़ को प्रोसेस कर सकते हैं।

## चरण 2: GPU एक्सेलेरेशन सक्षम करें

GPU चालू करना एक सिंगल बूलियन फ़्लैग है। अधिकांश सिस्टम में डिफ़ॉल्ट GPU डिवाइस 0 होता है, लेकिन आप Aspose को स्वचालित रूप से इष्टतम डिवाइस चुनने दे सकते हैं।

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **प्रो टिप:** कई GPUs वाले वर्कस्टेशनों पर, डिवाइस ID निर्दिष्ट करने से अनपेक्षित स्लो इंटीग्रेटेड GPU पर फॉलबैक से बचा जा सकता है।

## चरण 3: GPU डिवाइस ID सेट करें (वैकल्पिक)

यदि आप जानते हैं कि कौन सा GPU OCR संभालेगा—शायद एक समर्पित AI कार्ड—तो आप इसे स्पष्ट रूप से `setGpuDeviceId` के साथ सेट कर सकते हैं।  

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **एज केस:** अमान्य ID पास करने से `IllegalArgumentException` ट्रिगर होता है। वैध IDs की सूची के लिए `ocrEngine.getEngineOptions().getAvailableGpuDevices()` का उपयोग करें।

## चरण 4: इमेज प्रोसेस करें और इमेज से टेक्स्ट निकालें

OCR चलाने पर एक `OcrResult` मिलता है जिसमें साधारण स्ट्रिंग और वैकल्पिक कॉन्फिडेंस स्कोर होते हैं।  

```java
        // Perform OCR – this is where we "convert TIFF to text"
        OcrResult ocrResult = ocrEngine.process();

        // Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

### अपेक्षित आउटपुट

यदि TIFF में “Hello, World!” है तो परिणाम इस प्रकार दिखेगा:

```
Recognized text:
Hello, World!
```

इंजन स्वचालित रूप से लाइन ब्रेक, विराम चिह्न, और बेसिक लेआउट डिटेक्शन को संभालता है। प्रति‑पेज एक्सट्रैक्शन के लिए, `ocrResult.getPages()` देखें।

## चरण 5: आउटपुट सत्यापित करें और सामान्य समस्याओं को संभालें

GPU कई कारणों से बायपास हो सकता है। यदि स्थापित ड्राइवर संस्करण न्यूनतम आवश्यक से पुराना है, तो लाइब्रेरी CUDA इनिशियलाइज़ नहीं कर पाएगी। अपर्याप्त वीडियो मेमोरी से इंजन CPU पर फॉलबैक हो सकता है, और कुछ इंटीग्रेटेड ग्राफ़िक्स में OCR एक्सेलेरेशन के लिए आवश्यक कंप्यूट क्षमता नहीं होती।

### GPU क्यों उपयोग नहीं हो रहा हो सकता है?
- **ड्राइवर असंगति:** GPU ड्राइवर को Aspose रिलीज़ नोट्स में सूचीबद्ध न्यूनतम संस्करण को पूरा करना चाहिए।  
- **अपर्याप्त मेमोरी:** बहुत बड़ी इमेजेज VRAM से अधिक हो सकती हैं; तब इंजन CPU पर फॉलबैक हो जाता है और एक चेतावनी लॉग करता है।  
- **असमर्थित हार्डवेयर:** इंटीग्रेटेड ग्राफ़िक्स अक्सर आवश्यक कंप्यूट क्षमता नहीं रखते।

### प्रोग्रामेटिक रूप से CPU पर फॉलबैक कैसे करें
यदि आपको CPU प्रोसेसिंग सुनिश्चित करनी है, तो इंजन के विकल्प सेटर को फॉल्स फ़्लैग के साथ कॉल करें। यह किसी भी GPU प्रयास को निष्क्रिय कर देता है और OCR पाइपलाइन को पूरी तरह होस्ट प्रोसेसर पर चलाता है, जो असंगत ग्राफ़िक्स कार्ड वाले मशीनों में उपयोगी है।

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### लूप में TIFF से टेक्स्ट पढ़ना
जब कई फ़ाइलें प्रोसेस कर रहे हों, तो GPU एक्सेलेरेशन सक्षम रखते हुए एक डायरेक्टरी पर इटरेट करें।

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

यह स्निपेट दिखाता है कि कैसे **TIFF फ़ाइलों से टेक्स्ट पढ़ें** बल्क में, बिना परफ़ॉर्मेंस बूस्ट खोए।

## अक्सर पूछे जाने वाले प्रश्न (FAQ)

**Q: क्या यह Linux पर काम करता है?**  
A: बिल्कुल—Aspose OCR Windows, Linux, और macOS पर चलता है जब तक CUDA टूलकिट और ड्राइवर इंस्टॉल हों।

**Q: अगर मेरे पास GPU नहीं है तो?**  
A: `setUseGpu(true)` कॉल को छोड़ दें या स्पष्ट रूप से `setUseGpu(false)` कॉल करें; इंजन CPU पर चलेगा।

**Q: क्या मैं अन्य फ़ॉर्मैट्स से टेक्स्ट निकाल सकता हूँ?**  
A: हाँ। `setImage` JPEG, PNG, BMP, PDF, और अधिक को स्वीकार करता है।

**Q: लो‑रिज़ॉल्यूशन TIFFs पर OCR की सटीकता कितनी है?**  
A: 300 dpi से नीचे सटीकता तेज़ी से गिरती है। बेहतर परिणामों के लिए इमेज को प्री‑प्रोसेस करें (बाइनरीज़ेशन, डेस्क्यू)।

**Q: Aspose OCR कितने फ़ॉर्मैट्स को सपोर्ट करता है?**  
A: लाइब्रेरी 30+ रास्टर और डॉक्यूमेंट फ़ॉर्मैट्स को संभालती है, जिसमें TIFF, JPEG, PNG, BMP, PDF, और GIF शामिल हैं।

## निष्कर्ष

अब आप जानते हैं **GPU एक्सेलेरेशन का उपयोग करके Aspose OCR for Java में tiff फ़ाइल से टेक्स्ट कैसे निकालें**, कैसे विशिष्ट GPU डिवाइस ID सेट करें, और कैसे एक या कई TIFFs को प्रभावी रूप से प्रोसेस करें। एक ही फ़्लैग टॉगल करके आप OCR लॉजिक बदले बिना बड़े गति सुधार प्राप्त कर सकते हैं।

अगले कदम आप आज़मा सकते हैं:
- समानांतर थ्रेड्स में सैकड़ों TIFFs का बैच प्रोसेसिंग।  
- विशेषीकृत शब्दावली की पहचान सुधारने के लिए कस्टम भाषा पैक्स लोड करना।  
- फ़ॉर्मेटिंग साफ़ करने के लिए regex के साथ निकाले गए टेक्स्ट का पोस्ट‑प्रोसेसिंग।

यदि आपको कोई समस्या आती है, तो नीचे टिप्पणी छोड़ें। कोडिंग का आनंद लें!

---

**अंतिम अपडेट:** 2026-09-23  
**परीक्षित संस्करण:** Aspose OCR for Java 23.10  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल्स

- [Java OCR के लिए GPU सक्षम करने का चरण-दर-चरण गाइड](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/)
- [Aspose OCR के साथ इमेज से टेक्स्ट पहचानने का पूर्ण Java गाइड](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)
- [Java में इमेज OCR को प्री‑प्रोसेस करके सटीकता बढ़ाएँ और टेक्स्ट निकालें](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}