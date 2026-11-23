---
category: general
date: 2026-09-16
description: जावा में तेज़ OCR के लिए GPU को कैसे सक्षम करें, इमेज फ़ाइलों से टेक्स्ट
  पहचानें और Aspose OCR का उपयोग करके इमेज को टेक्स्ट में बदलें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize text from image
- extract text from image
- how to perform ocr
- convert image to text
language: hi
lastmod: 2026-09-16
og_description: जावा में OCR के लिए GPU कैसे सक्षम करें, इमेज फ़ाइलों से टेक्स्ट पहचानें
  और Aspose OCR के साथ इमेज को टेक्स्ट में बदलें – एक पूर्ण चरण‑दर‑चरण गाइड।
og_image_alt: Screenshot showing Java code that enables GPU for OCR and extracts text
  from an image
og_title: जावा में GPU को सक्षम कैसे करें और छवियों से टेक्स्ट निकालें
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  headline: How to enable GPU and extract text from images in Java
  type: TechArticle
- description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  name: How to enable GPU and extract text from images in Java
  steps:
  - name: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
    text: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
  - name: '**Segmentation** – locate text lines, words, and characters.'
    text: '**Segmentation** – locate text lines, words, and characters.'
  - name: '**Classification** – match each character against the built‑in language
      model.'
    text: '**Classification** – match each character against the built‑in language
      model.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: जावा में GPU को सक्षम कैसे करें और छवियों से टेक्स्ट निकालें
url: /hi/java/advanced-ocr-techniques/how-to-enable-gpu-and-extract-text-from-images-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में GPU सक्षम करने और छवियों से टेक्स्ट निकालने का तरीका

यदि आपको ऑप्टिकल कैरेक्टर रिकग्निशन के लिए **GPU कैसे सक्षम करें** की आवश्यकता है, तो यह गाइड आपको सटीक चरण दिखाता है। GPU एक्सेलेरेशन को चालू करके आप **छवि से टेक्स्ट पहचान** फ़ाइलों को CPU‑केवल प्रोसेसिंग की तुलना में कई गुना तेज़ी से कर सकते हैं। उदाहरण में Aspose OCR for Java का उपयोग किया गया है, लेकिन ये अवधारणाएँ किसी भी GPU‑संगत OCR लाइब्रेरी पर लागू होती हैं।

इस ट्यूटोरियल में आप सीखेंगे:

* OCR इंजन में GPU एक्सेलेरेशन सक्षम करें।  
* एक छवि लोड करें और **छवि से टेक्स्ट निकालें** फ़ाइलें।  
* **छवि को टेक्स्ट में बदलें** कुछ ही पंक्तियों के कोड से।  

कोई बाहरी सेवा आवश्यक नहीं है—सब कुछ आपके मशीन पर स्थानीय रूप से चलता है। एक बुनियादी Java विकास वातावरण और Aspose OCR for Java लाइब्रेरी ही एकमात्र पूर्वापेक्षाएँ हैं।

## आवश्यकताएँ

| आवश्यकता | संस्करण / विवरण |
|-------------|------------------|
| Java Development Kit (JDK) | 8 या नया |
| Maven या Gradle (निर्भरता प्रबंधन के लिए) | कोई भी नवीनतम संस्करण |
| CUDA समर्थन वाला GPU (वैकल्पिक लेकिन अनुशंसित) | NVIDIA GPU with driver ≥ 450 |
| Aspose OCR for Java library | 23.9 या नया (Aspose वेबसाइट से डाउनलोड करें) |

यदि आपके पास GPU नहीं है, तो कोड अभी भी काम करेगा; यह केवल CPU पर चलेगा।

## चरण 1: अपने प्रोजेक्ट में Aspose OCR जोड़ें

Maven के लिए, अपने `pom.xml` में निम्नलिखित डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

Gradle के लिए, इसे `build.gradle` में रखें:

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

ये एंट्रीज़ OCR इंजन और नेटीव GPU बाइनरीज़ को स्वचालित रूप से पुल करती हैं।

## चरण 2: OCR इंजन के लिए GPU कैसे सक्षम करें

मुख्य कार्य यह है कि `OcrEngine` को GPU उपयोग करने के लिए बताया जाए। Aspose OCR एक सरल फ़्लैग प्रदान करता है:

```java
// Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the “how to enable gpu” step
ocrEngine.setGpuEnabled(true);
```

**यह क्यों महत्वपूर्ण है:** जब `setGpuEnabled(true)` कॉल किया जाता है, लाइब्रेरी CUDA‑आधारित कर्नेल लोड करती है जो इमेज प्री‑प्रोसेसिंग और कैरेक्टर सेगमेंटेशन चरणों को समानांतर बनाते हैं। एक आधुनिक NVIDIA कार्ड पर, आप डिफ़ॉल्ट CPU पाथ की तुलना में 2‑4× गति सुधार देख सकते हैं।

> **प्रो टिप:** फ्लैग सक्षम करने से पहले `SystemInfo.isCudaSupported()` चलाकर जांचें कि आपका GPU पहचाना गया है या नहीं। यदि मेथड `false` लौटाता है, तो इंजन स्वचालित रूप से CPU पर वापस आ जाएगा।

## चरण 3: वह छवि लोड करें जिसे आप प्रोसेस करना चाहते हैं

आप OCR इंजन को Aspose द्वारा समर्थित किसी भी इमेज फ़ॉर्मेट (JPEG, PNG, BMP, TIFF, आदि) को फीड कर सकते हैं। यहाँ JPEG फ़ाइल लोड करने का तरीका है:

```java
// Load the image that contains the text to be recognized
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

**एज केस:** यदि छवि बड़ी है (5 MB से अधिक) तो मेमोरी खपत कम करने के लिए पहले उसका आकार बदलने पर विचार करें। OCR इंजन 300 dpi के आसपास की छवियों के साथ सबसे अच्छा काम करता है।

## चरण 4: OCR करें और **छवि से टेक्स्ट पहचानें**

अब जबकि इंजन कॉन्फ़िगर हो गया है और छवि लोड हो गई है, आप पहचान चला सकते हैं:

```java
// Execute OCR – this is the core “how to perform ocr” step
String recognizedText = ocrEngine.recognize();
```

`recognize()` मेथड एक प्लेन‑टेक्स्ट `String` लौटाता है। आंतरिक रूप से, इंजन कई चरण चलाता है:

1. **प्री‑प्रोसेसिंग** – डि‑स्क्यू, बाइनराइज़, और कंट्रास्ट बढ़ाएँ (GPU‑एक्सेलेरेटेड)।  
2. **सेगमेंटेशन** – टेक्स्ट लाइनों, शब्दों और कैरेक्टर्स को खोजें।  
3. **क्लासिफिकेशन** – प्रत्येक कैरेक्टर को बिल्ट‑इन लैंग्वेज मॉडल से मिलाएँ।  

क्योंकि GPU सक्रिय है, चरण 1 और 2 समानांतर निष्पादन से सबसे अधिक लाभान्वित होते हैं।

## चरण 5: निकाले गए टेक्स्ट को प्रदर्शित या संग्रहीत करें

अंत में, परिणाम को कंसोल, फ़ाइल, या किसी भी डाउनस्ट्रीम प्रोसेसर में आउटपुट करें:

```java
// Show the extracted text – this completes the “convert image to text” flow
System.out.println("Recognized text:\n" + recognizedText);

// Optional: write the text to a file
Files.write(Paths.get("output.txt"), recognizedText.getBytes(StandardCharsets.UTF_8));
```

**सामान्य आउटपुट** (एक नमूना छवि जिसमें “Hello World” है):

```
Recognized text:
Hello World
```

यदि OCR किसी भी कैरेक्टर को पहचानने में विफल रहता है, तो `recognizedText` एक खाली स्ट्रिंग होगी। ऐसे में छवि की गुणवत्ता दोबारा जांचें या प्रदर्शन की तुलना के लिए GPU को डिसेबल करें।

## सामान्य समस्याओं का समाधान

| समस्या | कारण | समाधान |
|-------|-------|-----|
| **GPU नहीं मिला** | CUDA ड्राइवर अनुपलब्ध या असमर्थित GPU | नवीनतम NVIDIA ड्राइवर स्थापित करें और `nvidia-smi` से सत्यापित करें। |
| **गलत कैरेक्टर** | कम कंट्रास्ट या शोरयुक्त पृष्ठभूमि | इंजन को फीड करने से पहले छवि को प्री‑प्रोसेस करें (जैसे, कंट्रास्ट बढ़ाएँ)। |
| **मेमोरी समाप्ति त्रुटि** | सीमित GPU मेमोरी पर बहुत बड़ी छवियां | छवि को ≤ 2000 px चौड़ाई तक रिसाइज़ करें या टाइल्स में प्रोसेस करें। |
| **भाषा असंगति** | डिफ़ॉल्ट भाषा मॉडल अंग्रेज़ी है लेकिन टेक्स्ट किसी अन्य भाषा में है | `recognize()` से पहले `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (या उपयुक्त enum) कॉल करें। |

## पूर्ण, चलाने योग्य उदाहरण

नीचे एक स्व-समाहित Java क्लास है जो सभी चरणों को एक साथ जोड़ता है। इसे `GpuEnabledOcrExample.java` के रूप में सेव करें, इमेज पाथ समायोजित करें, और `javac`/`java` या अपने IDE के माध्यम से चलाएँ।

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class GpuEnabledOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn on GPU acceleration for faster processing
        // This is the core "how to enable gpu" call
        ocrEngine.setGpuEnabled(true);

        // Optional sanity check – ensures CUDA is available
        if (!SystemInfo.isCudaSupported()) {
            System.out.println("CUDA not detected. Falling back to CPU.");
        }

        // Step 3: Load the image that contains the text to be recognized
        // Replace with the absolute path to your image file
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Perform the OCR operation and obtain the recognized text
        // This answers "how to perform ocr" and "recognize text from image"
        String recognizedText = ocrEngine.recognize();

        // Step 5: Display the extracted text – completes "convert image to text"
        System.out.println("Recognized text:\n" + recognizedText);

        // (Optional) Save the result to a text file
        Path output = Paths.get("recognized_output.txt");
        Files.write(output, recognizedText.getBytes());
        System.out.println("Text saved to " + output.toAbsolutePath());
    }
}
```

### अपेक्षित परिणाम

प्रोग्राम चलाने पर निकाला गया टेक्स्ट कंसोल में प्रिंट होगा और वही सामग्री `recognized_output.txt` में लिखी जाएगी। GPU सक्षम होने पर, 2 MP छवि के लिए कुल निष्पादन समय आमतौर पर NVIDIA RTX 3060 पर 200 ms से कम रहता है, जबकि केवल CPU पर लगभग 500 ms लगता है।

## निष्कर्ष

आप अब जानते हैं **GPU कैसे सक्षम करें** Aspose OCR के लिए Java में, **छवि से टेक्स्ट पहचान** फ़ाइलों को, और **छवि को टेक्स्ट में बदलें** कुछ सरल कोड लाइनों से। GPU एक्सेलेरेशन का उपयोग करके आप तेज़ प्रोसेसिंग प्राप्त करते हैं, जो बैच‑ओरिएंटेड या रियल‑टाइम एप्लिकेशन्स जैसे इनवॉइस स्कैनिंग, रसीद प्रोसेसिंग, और दस्तावेज़ डिजिटलीकरण के लिए आवश्यक है।

**अगले कदम**

* विभिन्न भाषा मॉडलों (`ocrEngine.setLanguage`) के साथ प्रयोग करें ताकि फ्रेंच, जर्मन, या चीनी में **छवि से टेक्स्ट निकालें**।  
* OCR आउटपुट को Apache Tika के साथ मिलाकर निकाले गए कंटेंट को स्वचालित रूप से इंडेक्स करें।  
* यदि आपको PDF दस्तावेज़ के भीतर **छवि से टेक्स्ट पहचान** फ्रेम्स की आवश्यकता है, तो बड़े PDFs को पेज‑बाय‑पेज स्ट्रीम करने का अन्वेषण करें।

सैंपल को अपनी आवश्यकताओं के अनुसार अनुकूलित करने, अपने स्वयं के सर्विसेज़ में एकीकृत करने, और अपने परिणाम साझा करने में संकोच न करें। Happy coding!

## अगला क्या सीखें?

निम्नलिखित ट्यूटोरियल्स इस गाइड में प्रदर्शित तकनीकों पर आधारित करीबी संबंधित विषयों को कवर करते हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का पता लगाने में मदद करेंगे।

- [Java में Aspose OCR का उपयोग करके छवि से टेक्स्ट पढ़ने का तरीका – पूर्ण गाइड](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Aspose OCR के साथ टेक्स्ट इमेज पहचानें – पूर्ण Java OCR ट्यूटोरियल](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [image to text java: Aspose.OCR के साथ छवि को टेक्स्ट में बदलें](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}