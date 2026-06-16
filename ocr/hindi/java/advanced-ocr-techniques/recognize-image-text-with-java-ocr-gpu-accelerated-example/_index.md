---
category: general
date: 2026-03-28
description: Aspose OCR का उपयोग करके जावा में इमेज टेक्स्ट को पहचानना, टेक्स्ट PNG
  फ़ाइलें निकालना, और बड़े चित्रों के तेज़ OCR के लिए GPU एक्सेलेरेशन का उपयोग करना
  सीखें।
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: hi
og_description: जानेँ कैसे जावा में छवि टेक्स्ट को पहचानें, टेक्स्ट PNG फ़ाइलें निकालें,
  और बड़े चित्रों के OCR के लिए GPU तेज़ी का उपयोग करें।
og_title: Java OCR के साथ छवि पाठ को पहचानें – GPU‑त्वरित उदाहरण
tags:
- OCR
- Java
- GPU
title: Java OCR के साथ छवि पाठ को पहचानें – GPU‑त्वरित उदाहरण
url: /hi/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR के साथ इमेज टेक्स्ट पहचान – GPU‑त्वरित उदाहरण

क्या आपको कभी बड़े PNG से **इमेज टेक्स्ट पहचान** करनी पड़ी लेकिन CPU संस्करण बहुत धीमा लगा? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया पाइपलाइन—जैसे इनवॉइस स्कैनिंग या ऐतिहासिक दस्तावेज़ों का अभिलेख—में इमेज का आकार बहुत बड़ा हो सकता है, और डिफ़ॉल्ट OCR इंजन इसे संभाल नहीं पाता।  

अच्छी खबर: Aspose OCR for Java आपको **GPU एक्सेलेरेशन का उपयोग** करने देता है जिससे प्रक्रिया तेज़ हो जाती है, और कोड आश्चर्यजनक रूप से संक्षिप्त है। इस ट्यूटोरियल में आप एक पूर्ण, चलाने योग्य Java OCR उदाहरण देखेंगे जो **PNG फ़ाइलों से टेक्स्ट निकालता** है, CUDA‑सक्षम GPU का उपयोग करता है, और **बड़ी OCR इमेज** को कुछ ही पंक्तियों के कोड से संभालता है। अंत तक आप जान जाएंगे कि इसे अपने Java प्रोजेक्ट में कैसे जोड़ें और प्रत्येक सेटिंग क्यों महत्वपूर्ण है।

## आप क्या सीखेंगे

- Maven या Gradle प्रोजेक्ट में Aspose OCR सेटअप करने का तरीका।  
- GPU पर **इमेज टेक्स्ट पहचान** करने की चरण‑दर‑चरण प्रक्रिया।  
- GPU स्ट्रीम्स की संख्या कॉन्फ़िगर करने से थ्रूपुट कैसे बढ़ सकता है।  
- आउटपुट को कैसे सत्यापित करें और सामान्य समस्याओं का समाधान कैसे करें।  

> **पूर्वापेक्षाएँ** – Java 17 (या बाद का), नवीनतम ड्राइवर वाला CUDA‑संगत GPU, और एक वैध Aspose OCR for Java लाइसेंस (मुफ़्त ट्रायल मूल्यांकन के लिए काम करता है)। अन्य कोई बाहरी लाइब्रेरी आवश्यक नहीं है।

---

## चरण 1: Aspose OCR निर्भरता जोड़ें

सबसे पहले, Aspose OCR लाइब्रेरी को अपने बिल्ड में लाएँ। यदि आप **Maven** उपयोग करते हैं, तो अपने `pom.xml` में निम्न स्निपेट जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

यदि आप **Gradle** उपयोग करते हैं, तो इसे `build.gradle` में रखें:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **प्रो टिप:** नवीनतम संस्करण (मार्च 2026 तक) GPU वर्कलोड के लिए प्रदर्शन सुधार शामिल करता है, इसलिए हमेशा नवीनतम रिलीज़ प्राप्त करें।

---

## चरण 2: OCR इंजन को इनिशियलाइज़ करें और GPU सक्षम करें

OCR इंजन बनाना सरल है। महत्वपूर्ण भाग GPU फ़्लैग को ऑन करना है—अन्यथा इंजन CPU मोड में वापस चला जाता है।

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### GPU क्यों सक्षम करें?

जब आप `setUseGpu(true)` सक्षम करते हैं, तो Aspose भारी कॉन्वॉल्यूशन न्यूरल नेटवर्क गणनाओं को ग्राफ़िक्स कार्ड पर स्थानांतरित कर देता है। यह **बड़ी OCR इमेज** की प्रोसेसिंग समय में सेकंड्स बचा सकता है, विशेष रूप से जब इमेज 4000 × 4000 px से बड़ी हो। यदि आपके वातावरण में संगत GPU नहीं है, तो यह कॉल बस एक no‑op बन जाता है और इंजन CPU पर जारी रहता है—कोई क्रैश नहीं, बस धीमी गति।

---

## चरण 3: PNG इमेज को पहचानें और उसका टेक्स्ट निकालें

अब इंजन को उस फ़ाइल की ओर इंगित करें जिसे आप प्रोसेस करना चाहते हैं। उदाहरण में `sample-large.png` उपयोग किया गया है, लेकिन आप इसे किसी भी PNG या JPEG से बदल सकते हैं।

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

जब आप प्रोग्राम चलाएँगे, तो आपको कुछ इस तरह दिखना चाहिए:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

यह आउटपुट पुष्टि करता है कि **इमेज टेक्स्ट पहचान** ऑपरेशन सफल रहा और आपने सफलतापूर्वक **PNG से टेक्स्ट निकाला** है।

---

## चरण 4: GPU उपयोगिता सत्यापित करें (वैकल्पिक लेकिन उपयोगी)

यदि आप जिज्ञासु हैं कि GPU वास्तव में उपयोग हो रहा है या नहीं, तो अपने सिस्टम के GPU मॉनिटरिंग टूल को खोलें (उदा., Linux पर `nvidia-smi`)। जब Java प्रोसेस चल रहा हो, तो आपको मेमोरी उपयोग और कंप्यूट उपयोग में एक मामूली स्पाइक दिखना चाहिए।

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

यदि आपको कोई गतिविधि नहीं दिखती, तो दोबारा जांचें कि:

1. CUDA ड्राइवर GPU मॉडल से मेल खाता है।  
2. `setUseGpu(true)` कॉल कोड में बाद में ओवरराइड नहीं किया गया है।  
3. आपकी लाइसेंस फ़ाइल (यदि आपके पास है) GPU उपयोग को प्रतिबंधित नहीं कर रही है।

---

## चरण 5: सामान्य किनारे मामलों को संभालना

### GPU मेमोरी से अधिक बड़ी इमेजेस

जब इमेज बहुत बड़ी हो (जैसे 8000 × 8000 px), तो GPU मेमोरी समाप्त हो सकती है। एक त्वरित समाधान है कि Aspose को फीड करने से पहले इमेज को डाउनस्केल करें:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

फिर `"sample-resized.png"` को `recognizeImage` में पास करें। इससे OCR सटीक रहता है जबकि GPU सीमा के भीतर रहता है।

### मल्टी‑पेज PDFs

Aspose OCR PDFs को पेज‑बाय‑पेज भी संभाल सकता है। प्रत्येक पेज पर लूप करें, उसे इमेज में बदलें, और इंजन को फीड करें। वही **GPU एक्सेलेरेशन का उपयोग** फ़्लैग लागू होता है, जिससे आपको तेज़ PDF‑से‑टेक्स्ट पाइपलाइन मिलती है।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूर्ण Java क्लास दिया गया है, जिसे कंपाइल और रन किया जा सकता है। `YOUR_DIRECTORY` को अपने PNG फ़ाइल के पाथ से बदलें।

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**अपेक्षित आउटपुट** – इमेज से इंजन द्वारा पढ़े गए सभी टेक्स्ट का साधारण‑टेक्स्ट प्रतिनिधित्व। यदि इमेज में टेबल है, तो आपको सेल सामग्री लाइन ब्रेक्स के साथ जुड़ी हुई मिलेगी; Aspose लेआउट नहीं रखता, लेकिन आप आवश्यकता अनुसार स्ट्रिंग को पोस्ट‑प्रोसेस कर सकते हैं।

---

## अक्सर पूछे जाने वाले प्रश्न

| प्रश्न | उत्तर |
|----------|--------|
| **क्या मुझे पेड लाइसेंस चाहिए?** | ट्रायल 200 पेज तक काम करता है और OCR के लिए वॉटरमार्क को डिसेबल करता है। प्रोडक्शन के लिए, लाइसेंस सीमाओं को हटाता है और पूरी GPU स्टैक को अनलॉक करता है। |
| **अगर मेरा GPU पुराना है (जैसे GTX 750) तो क्या?** | पुराने GPU अभी भी काम कर सकते हैं लेकिन गति कम होगी; सुनिश्चित करें कि आपके पास कम से कम Compute Capability 3.0 हो। |
| **क्या मैं JPG या BMP फ़ाइलें प्रोसेस कर सकता हूँ?** | बिल्कुल—`recognizeImage` किसी भी फॉर्मेट को स्वीकार करता है जो Java ImageIO सपोर्ट करता है। |
| **क्या कई इमेजेज को बैच‑प्रोसेस करने का तरीका है?** | OCR कॉल को लूप में रखें, और `setGpuStreams` को बढ़ाने पर विचार करें ताकि आप जितनी कॉन्करेंट स्ट्रीम्स चाहते हैं उतनी मिलें। |
| **अगर मुझे लेआउट बनाए रखना है तो क्या?** | Aspose OCR के `LayoutOptions` का उपयोग करके बाउंडिंग बॉक्स प्राप्त करें; यह त्वरित गाइड के दायरे से बाहर है लेकिन API में दस्तावेज़ित है। |

---

## निष्कर्ष

अब आपके पास एक संक्षिप्त, एंड‑टू‑एंड **java ocr example** है जो **इमेज टेक्स्ट पहचान** करता है, **PNG से टेक्स्ट निकालता** है, और **GPU एक्सेलेरेशन** का उपयोग करके **बड़ी OCR इमेज** की प्रोसेसिंग को तेज़ करता है। GPU स्ट्रीम काउंट को समायोजित करके और आवश्यक होने पर ओवरसाइज़्ड इमेज को डाउनस्केल करके, आप समाधान को लगभग किसी भी हार्डवेयर कॉन्फ़िगरेशन के अनुसार अनुकूलित कर सकते हैं।  

अगले कदम के लिए तैयार हैं? स्कैन किए गए रसीदों के फ़ोल्डर को उसी पाइपलाइन में फीड करने की कोशिश करें, या Aspose के `TextRegion` API के साथ प्रयोग करें ताकि मूल लेआउट बना रहे। और यदि आपको कोई समस्या आती है, तो Aspose फोरम और Javadoc उत्कृष्ट संसाधन हैं—बस यहाँ कवर किए गए मूल बातें याद रखें।  

कोडिंग का आनंद लें, और आपका OCR बिजली की गति से तेज़ हो!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}