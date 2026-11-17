---
category: general
date: 2026-08-22
description: Java OCR में GPU को सक्षम करके छवि से तेज़ी से टेक्स्ट पहचानने का तरीका।
  PNG से टेक्स्ट निकालना, image options सेट करना, और Aspose OCR का उपयोग करके प्रभावी
  रूप से टेक्स्ट पहचानना सीखें।
draft: false
keywords:
- how to enable gpu
- recognize text image java
- aspose ocr java tutorial
- extract text from png
- set image options
lastmod: 2026-08-22
og_description: Java OCR में GPU को सक्षम करके छवि से तेज़ी से टेक्स्ट पहचानने का
  तरीका। यह गाइड दिखाता है कि PNG से टेक्स्ट कैसे निकालें, image options सेट करें,
  और Aspose OCR का उपयोग करके प्रभावी रूप से टेक्स्ट कैसे पहचानें।
og_image_alt: Java OCR GPU example code snippet showing Aspose OCR usage
og_title: Java में OCR के लिए GPU कैसे सक्षम करें – तेज़ टेक्स्ट निष्कर्षण
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  headline: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  type: TechArticle
- description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  name: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  steps:
  - name: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
    text: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
  - name: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
    text: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
  - name: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
    text: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR trial includes full GPU support; you just need to
      enable it in code.
    question: Does the free trial support GPU acceleration?
  - answer: Aspose OCR can rasterize PDF pages internally, but for best performance
      convert to high‑resolution PNG first.
    question: Can I process PDFs directly without converting to images?
  - answer: CUDA 11.2 or newer is recommended; older versions may work but are not
      officially tested.
    question: What CUDA version is required?
  - answer: Validate file size and type before processing, and run the OCR in a sandboxed
      thread to mitigate risks.
    question: Is it safe to run OCR on untrusted user uploads?
  - answer: Set `ocrEngine.setDebugMode(true)`; the console will list the selected
      GPU device and memory statistics.
    question: How do I enable logging to verify GPU usage?
  type: FAQPage
tags:
- OCR
- Java
- GPU
title: Java में OCR के लिए GPU कैसे सक्षम करें – छवि से तेज़ टेक्स्ट पहचानें
url: /hi/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में OCR के लिए GPU सक्षम कैसे करें – छवि से तेज़ टेक्स्ट पहचानें

जावा OCR एप्लिकेशन में GPU त्वरण को सक्षम करने से प्रोसेसिंग समय में नाटकीय कमी आ सकती है, विशेष रूप से जब आपको बड़े चित्रों या उच्च‑वॉल्यूम बैचों से टेक्स्ट निकालना हो। इस ट्यूटोरियल में आप सीखेंगे **GPU कैसे सक्षम करें**, **छवि से टेक्स्ट कैसे पहचानें** फ़ाइलों को, और Aspose OCR लाइब्रेरी का उपयोग करके **PNG से टेक्स्ट कैसे निकालें** के सटीक चरण। हम इमेज‑प्रि‑प्रोसेसिंग विकल्पों को भी देखेंगे जो सटीकता बढ़ाते हैं और “टेक्स्ट कैसे पहचानें” के सामान्य प्रश्नों के उत्तर देंगे।

## त्वरित उत्तर
- **सबसे बड़ा गति लाभ क्या है?** CPU‑केवल OCR की तुलना में मिड‑रेंज RTX 2060 पर 5× तक तेज़।  
- **क्या मुझे विशेष लाइसेंस चाहिए?** एक मानक Aspose OCR लाइसेंस GPU के लिए काम करता है; बस GPU फ़्लैग सक्षम करें।  
- **कौन सा जावा संस्करण आवश्यक है?** इष्टतम प्रदर्शन के लिए Java 17 या नया अनुशंसित है।  
- **क्या इसे Docker के अंदर चलाया जा सकता है?** हाँ – `--gpus all` फ़्लैग जोड़ें और कंटेनर में NVIDIA ड्राइवर स्थापित करें।  
- **क्या कोड अन्य इमेज फ़ॉर्मैट्स के साथ संगत है?** वही API JPEG, TIFF, BMP, और PNG के लिए बिना परिवर्तन के काम करता है।

## आपको क्या चाहिए

आपको एक GPU‑सक्षम मशीन, Aspose OCR for Java लाइब्रेरी, और Java 17 (या नया) विकास वातावरण चाहिए। सामान्य सेटअप में NVIDIA RTX 3060 या कोई भी CUDA‑संगत कार्ड, Maven Central से नवीनतम Aspose OCR JAR, और बेंचमार्किंग के लिए एक नमूना PNG इनवॉइस शामिल है।

**सीधा उत्तर (40‑70 शब्द):** शुरू करने के लिए आपको Java 17 स्थापित करना होगा, अपने प्रोजेक्ट में Aspose OCR डिपेंडेंसी जोड़नी होगी, यह सत्यापित करना होगा कि JVM कम से कम एक CUDA डिवाइस देख रहा है, और एक टेस्ट इमेज तैयार रखनी होगी। इन पूर्वशर्तों के पूरा होने पर आप OCR इंजन में GPU सक्षम कर सकते हैं और GPU गति पर इमेज प्रोसेस करना शुरू कर सकते हैं।

- **Java 17** (या नया) – कोड पहले के संस्करणों के साथ भी कम्पाइल हो सकता है लेकिन 17 सबसे बेहतर API समर्थन देता है।  
- **Aspose OCR for Java** – Aspose वेबसाइट या Maven Central से नवीनतम JAR प्राप्त करें।  
- **एक CUDA‑संगत GPU** – उदाहरण: NVIDIA RTX 3060, RTX 2070, या कोई भी आधुनिक कार्ड उचित ड्राइवर के साथ।  
- **टेस्ट इमेज** – बड़े‑फ़ॉर्मैट PNG इनवॉइस प्रदर्शन मापने के लिए उपयुक्त है।

> **प्रो टिप:** लैपटॉप में इंटीग्रेटेड और डिस्क्रीट ग्राफ़िक्स दोनों होने पर, ड्राइवर कंट्रोल पैनल के माध्यम से JVM को डिस्क्रीट GPU उपयोग करने के लिए मजबूर करें; अन्यथा लाइब्रेरी चुपचाप CPU पर वापस आ जाती है।

![GPU सक्षम करने का उदाहरण](image.png "GPU सक्षम करने का उदाहरण")
[GPU सक्षम करने का उदाहरण](image.png "GPU सक्षम करने का उदाहरण")

*Alt text: GPU सक्षम करने का उदाहरण, जिसमें जावा कोड स्निपेट दिखाया गया है.*

## चरण 1 – Aspose OCR स्थापित करें और GPU उपलब्धता सत्यापित करें

GpuSettings वह क्लास है जो Aspose OCR इंजन के लिए GPU उपयोग को नियंत्रित करता है।

Maven डिपेंडेंसी जोड़ें (या JAR को `libs/` में डालें):

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Check for the latest version -->
</dependency>
```

उपलब्ध डिवाइसों की सूची के लिए sanity‑check स्निपेट चलाएँ:

```java
import com.aspose.ocr.GpuSettings;

public class GpuCheck {
    public static void main(String[] args) {
        GpuSettings settings = new GpuSettings();
        System.out.println("GPU enabled? " + settings.getEnable());
        System.out.println("Detected GPU count: " + settings.getDeviceCount());
    }
}
```

यदि आउटपुट में शून्य‑से‑अधिक डिवाइस काउंट दिखता है, तो आपका JVM GPU देख रहा है। यदि यह शून्य दिखाता है, तो ड्राइवर इंस्टॉलेशन और `CUDA_PATH` एन्वायरनमेंट वैरिएबल को दोबारा जाँचें।

## चरण 2 – Aspose OCR में GPU कैसे सक्षम करें

**सीधा उत्तर (40‑70 शब्द):** `GpuSettings` ऑब्जेक्ट बनाकर, `setEnable(true)` सेट करके, वैकल्पिक रूप से डिवाइस आईडी निर्दिष्ट करके, और इस सेटिंग्स ऑब्जेक्ट को `AsposeOCR` कन्स्ट्रक्टर में पास करके GPU सक्षम करें। इसके बाद सभी बाद के OCR कॉल चयनित GPU पर चलेंगे, जिससे प्रदर्शन अनुभाग में वर्णित गति सुधार मिलेंगे।

`GpuSettings` क्लास आपको GPU उपयोग टॉगल करने और कई GPU मौजूद होने पर विशिष्ट डिवाइस चुनने की सुविधा देती है।

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.GpuSettings;
import com.aspose.ocr.ImageProcessingOptions;
import com.aspose.ocr.RecognitionLanguage;
import com.aspose.ocr.OcrResult;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // 2️⃣ Enable GPU processing (auto‑detects available device)
        GpuSettings gpuSettings = new GpuSettings();
        gpuSettings.setEnable(true);          // turn GPU on
        gpuSettings.setDeviceId(0);           // first GPU (change if you have multiple)
        ocrEngine.setGpuSettings(gpuSettings);

        // 3️⃣ Optimize image preprocessing for GPU performance
        ImageProcessingOptions imgOpts = new ImageProcessingOptions();
        imgOpts.setAutoDeskew(true);
        imgOpts.setBinarization(true);
        ocrEngine.setImageProcessingOptions(imgOpts);

        // 4️⃣ Recognize text from an image file (PNG in this case)
        OcrResult result = ocrEngine.recognizeImage(
                "YOUR_DIRECTORY/large_invoice.png",
                RecognitionLanguage.ENGLISH);

        // 5️⃣ Output the detected text
        System.out.println("Detected text:\n" + result.getText());
    }
}
```

### GPU क्यों सक्षम करें?

GPU त्वरण OCR मॉडल द्वारा किए जाने वाले भारी मैट्रिक्स‑मल्टिप्लिकेशन कार्य को हजारों समानांतर कोर पर ले जाता है। व्यावहारिक रूप से आप **2‑5× गति‑वृद्धि** एक मध्यम RTX 2060 पर देखेंगे, और नए कार्डों पर और भी अधिक। इसका ट्रेड‑ऑफ़ थोड़ा अधिक मेमोरी फुटप्रिंट है, लेकिन आम तौर पर इनवॉइस‑साइज़ PNG के लिए यह समस्या नहीं बनता।

## चरण 3 – जावा में छवि से टेक्स्ट पहचानें – सर्वोत्तम प्रथाएँ

`recognizeImage` मेथड दिए गए इमेज फ़ाइल को प्रोसेस करता है और निकाला गया टेक्स्ट लौटाता है।

**सीधा उत्तर (40‑70 शब्द):** GPU सक्षम होने के बाद `ocrEngine.recognizeImage(filePath)` कॉल करें; मेथड स्वचालित रूप से फ़ाइल फ़ॉर्मैट पहचानता है, GPU पर OCR मॉडल चलाता है, और निकाला गया टेक्स्ट लौटाता है। सर्वोत्तम सटीकता के लिए, कॉल से पहले इमेज को बाइनराइज़ और डेस्क्यू करें।

ऊपर का कोड यह पहले से ही करता है, लेकिन यहाँ एक संक्षिप्त संस्करण है जो OCR कॉल को अलग करता है:

```java
// Assuming ocrEngine is already configured with GPU
String imagePath = "sample.png";
OcrResult ocrResult = ocrEngine.recognizeImage(imagePath, RecognitionLanguage.ENGLISH);
String extractedText = ocrResult.getText();

System.out.println("Extracted text from PNG:");
System.out.println(extractedText);
```

**आपको यह ध्यान देगा:** `recognizeImage` मेथड स्वचालित रूप से फ़ाइल प्रकार पहचान लेता है, इसलिए आप JPEG, TIFF, या PNG बिना अतिरिक्त फ़्लैग के पास कर सकते हैं। इसलिए **PNG से टेक्स्ट निकालना** बॉक्स से बाहर काम करता है।

### बड़ी फ़ाइलों को संभालना

यदि आपका PNG 5 MB से बड़ा है, तो OCR से पहले इसे स्केल डाउन करने पर विचार करें:

```java
imgOpts.setResizeFactor(0.5); // shrink to 50 % of original dimensions
ocrEngine.setImageProcessingOptions(imgOpts);
```

डाऊन‑सैंपलिंग GPU मेमोरी उपयोग को घटाती है और अक्सर सटीकता बढ़ाती है क्योंकि मॉडल साफ़ किनारे देखता है।

## चरण 4 – बेहतर सटीकता के लिए छवि विकल्प कैसे सेट करें

ImageOptions एक कॉन्फ़िगरेशन ऑब्जेक्ट है जो OCR से पहले डेस्क्यूइंग और बाइनराइज़ेशन जैसे प्री‑प्रोसेसिंग चरणों को समायोजित करने की अनुमति देता है।

**सीधा उत्तर (40‑70 शब्द):** `ImageOptions` ऑब्जेक्ट का उपयोग करके ऑटो‑डेस्क्यू, बाइनराइज़ेशन, और वैकल्पिक री‑साइज़िंग को सक्षम करें, फिर इमेज को OCR इंजन को पास करें। सामान्य मान `setAutoDeskew(true)`, `setBinarization(true)`, और बड़े स्कैन के लिए 0.5 से 0.8 के बीच री‑साइज़ फ़ैक्टर होते हैं। ये सेटिंग्स कंट्रास्ट और अलाइनमेंट सुधारती हैं, जिससे न्यूरल नेटवर्क शोरयुक्त या टिल्टेड दस्तावेज़ों में अक्षरों को अधिक सटीकता से पहचानता है।

वाक्यांश **छवि कैसे सेट करें** प्री‑प्रोसेसिंग के दौरान स्वाभाविक रूप से आता है। Aspose OCR कई नॉब्स प्रदान करता है:

| विकल्प                     | क्या करता है                               | सामान्य मान |
|----------------------------|--------------------------------------------|-------------|
| `setAutoDeskew(true)`      | टिल्टेड टेक्स्ट लाइनों को सीधा करता है    | true        |
| `setBinarization(true)`    | कंट्रास्ट के लिए ब्लैक‑एंड‑व्हाइट में बदलता है | true        |
| `setResizeFactor(x)`       | इमेज को स्केल करता है (0 < x ≤ 1)          | 0.5‑0.8     |
| `setContrastAdjustment(y)` | कंट्रास्ट बढ़ाता है (0‑100)                | 30          |

आप इन्हें किसी भी क्रम में संयोजित कर सकते हैं; लाइब्रेरी इमेज को न्यूरल नेट में फीड करने से पहले क्रमिक रूप से लागू करती है। प्रयोग आवश्यक है—विभिन्न इनवॉइस को अलग‑अलग थ्रेशहोल्ड की जरूरत पड़ सकती है।

## चरण 5 – किनारे के मामलों में टेक्स्ट कैसे पहचानें

`GpuExample` क्लास Aspose OCR के साथ GPU त्वरण का उपयोग करके एक पूर्ण एंड‑टू‑एंड OCR वर्कफ़्लो दर्शाती है।

**सीधा उत्तर (40‑70 शब्द):** कम‑रिज़ॉल्यूशन स्कैन के लिए पहले इमेज को अपस्केल करें या उच्च‑dpi स्रोत मांगें; हस्तलिखित नोट्स के लिए कस्टम प्रशिक्षित मॉडल का उपयोग करें; और बहु‑भाषी दस्तावेज़ों के लिए `RecognitionLanguage` को कॉमा‑सेपरेटेड सूची के रूप में पास करें। ये समायोजन सुनिश्चित करते हैं कि GPU‑त्वरित इंजन अभी भी विश्वसनीय परिणाम दे।

GPU शक्ति के साथ भी कुछ स्थितियों में OCR फेल हो सकता है:

1. **कम‑रिज़ॉल्यूशन स्कैन (< 150 dpi).** पहले अपस्केल करें या उपयोगकर्ता से उच्च‑रिज़ॉल्यूशन स्कैन माँगें।  
2. **हस्तलिखित नोट्स.** डिफ़ॉल्ट मॉडल प्रिंटेड टेक्स्ट पर केंद्रित है; कर्सिव के लिए आपको कस्टम प्रशिक्षित मॉडल चाहिए।  
3. **एकाधिक भाषाएँ.** `RecognitionLanguage` को कॉमा‑सेपरेटेड सूची के रूप में पास करें, जैसे `RecognitionLanguage.ENGLISH_FRENCH`।

```java
ocrEngine.recognizeImage("multilang.png",
        RecognitionLanguage.ENGLISH_FRENCH);
```

## अपेक्षित आउटपुट

`large_invoice.png` के खिलाफ पूर्ण `GpuExample` क्लास चलाने पर कुछ इस तरह का आउटपुट दिखना चाहिए:

```
Detected text:
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
...
```

यदि गड़बड़ दिखे, तो दोबारा जाँचें कि `gpuSettings.setEnable(true)` वास्तव में प्रभावी हुआ है (डिबग लॉगिंग सक्षम करने पर कंसोल GPU डिवाइस सूचीबद्ध करेगा)।

## सामान्य कठिनाइयाँ और प्रो टिप्स

- **GPU डिवाइस आईडी सेट करना भूल गए।** मल्टी‑GPU सेटअप में `setDeviceId(1)` आवश्यक हो सकता है।  
- **NVIDIA रनटाइम के बिना Docker में चलाना।** `docker run` कमांड में `--gpus all` जोड़ें।  
- **CPU‑केवल और GPU‑सक्षम कोड पाथ को मिलाना।** प्रत्येक थ्रेड के लिए एक ही `AsposeOCR` इंस्टेंस रखें ताकि स्टेट क्लैश न हो।  
- **मेमोरी लीक।** सेवा लंबे समय तक चलने पर `ocrEngine.dispose()` कॉल करें।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न:** क्या फ्री ट्रायल GPU त्वरण का समर्थन करता है?  
**उत्तर:** हाँ, Aspose OCR ट्रायल में पूर्ण GPU समर्थन शामिल है; आपको केवल कोड में इसे सक्षम करना है।

**प्रश्न:** क्या मैं इमेज में बदलने के बिना सीधे PDF प्रोसेस कर सकता हूँ?  
**उत्तर:** Aspose OCR PDF पेजों को आंतरिक रूप से रास्टराइज़ कर सकता है, लेकिन सर्वोत्तम प्रदर्शन के लिए पहले हाई‑रिज़ॉल्यूशन PNG में बदलें।

**प्रश्न:** कौन सा CUDA संस्करण आवश्यक है?  
**उत्तर:** CUDA 11.2 या नया अनुशंसित है; पुराने संस्करण काम कर सकते हैं लेकिन आधिकारिक रूप से परीक्षण नहीं किए गए हैं।

**प्रश्न:** क्या अनट्रस्टेड यूज़र अपलोड्स पर OCR चलाना सुरक्षित है?  
**उत्तर:** प्रोसेसिंग से पहले फ़ाइल आकार और प्रकार को वैलिडेट करें, और जोखिम कम करने के लिए OCR को सैंडबॉक्स्ड थ्रेड में चलाएँ।

**प्रश्न:** GPU उपयोग सत्यापित करने के लिए लॉगिंग कैसे सक्षम करें?  
**उत्तर:** `ocrEngine.setDebugMode(true)` सेट करें; कंसोल चयनित GPU डिवाइस और मेमोरी स्टैटिस्टिक्स सूचीबद्ध करेगा।

## निष्कर्ष

हमने **GPU कैसे सक्षम करें** Aspose OCR के लिए जावा में दिखाया, **छवि से टेक्स्ट कैसे पहचानें**, **PNG से टेक्स्ट कैसे निकालें**, **छवि विकल्प कैसे सेट करें**, और वास्तविक‑दुनिया की फ़ाइलों में **टेक्स्ट कैसे पहचानें** के पहलुओं को कवर किया। GPU चालू होने पर आपका OCR पाइपलाइन स्पष्ट रूप से तेज़ हो जाएगा, जिससे बैच इनवॉइस प्रोसेसिंग या लाइव डॉक्यूमेंट स्कैनिंग जैसे हाई‑थ्रूपुट परिदृश्यों के लिए उपयुक्त बनता है।

अगले कदम के लिए तैयार हैं? डिफ़ॉल्ट अंग्रेज़ी मॉडल को बहु‑भाषी मॉडल से बदलें, या शोरयुक्त रसीदों के लिए कस्टम प्री‑प्रोसेसिंग पाइपलाइन के साथ प्रयोग करें। आकाश ही सीमा है—विशेषकर जब आपके पास GPU भारी काम संभाल रहा हो।

---

**अंतिम अपडेट:** 2026-08-22  
**परीक्षण किया गया:** Aspose OCR for Java 24.10  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल

- [Aspose OCR पूर्ण जावा OCR ट्यूटोरियल के साथ छवि से टेक्स्ट पहचानें](/ocr/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [जावा में Aspose OCR लाइसेंस कैसे सेट करें और सत्यापित करें](/ocr/java/ocr-basics/set-license/)
- [Aspose.OCR डिटेक्ट एरिया मोड के साथ जावा में छवि से टेक्स्ट निकालें](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}