---
category: general
date: 2026-02-14
description: Aspose OCR का उपयोग करके छवि से टेक्स्ट निकालें। जानें कि OCR के लिए
  छवि कैसे लोड करें, आयत से टेक्स्ट कैसे पढ़ें, और इस Aspose OCR ट्यूटोरियल को मिनटों
  में फॉलो करें।
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: hi
og_description: इमेज से तुरंत टेक्स्ट निकालें। यह गाइड दिखाता है कि OCR के लिए इमेज
  कैसे लोड करें, आयत से टेक्स्ट कैसे पढ़ें, और Aspose OCR ट्यूटोरियल को कैसे पूरा
  करें।
og_title: Aspose OCR के साथ छवि से टेक्स्ट निकालें – त्वरित गाइड
tags:
- Aspose
- OCR
- Java
title: Aspose OCR के साथ छवि से टेक्स्ट निकालें – चरण‑दर‑चरण डेमो
url: /hi/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR के साथ इमेज से टेक्स्ट निकालें – चरण‑दर‑चरण डेमो

क्या आपको कभी **इमेज से टेक्स्ट निकालना** पड़ा है लेकिन शुरुआत कहाँ से करें, समझ नहीं आया? आप अकेले नहीं हैं—कई डेवलपर्स को रसीद स्कैनिंग या आईडी वेरिफिकेशन जैसी पहली बार की चुनौतियों में यही समस्या आती है। अच्छी खबर? Aspose OCR के साथ आप इमेज लोड कर सकते हैं, टेक्स्ट वाले सटीक क्षेत्र को परिभाषित कर सकते हैं, और कुछ ही लाइनों में कैरेक्टर निकाल सकते हैं।

इस **aspose ocr tutorial** में हम सब कुछ कवर करेंगे: OCR के लिए इमेज लोड करना, वह रेक्टेंगल सेट करना जो इंजन को बताता है कि कहाँ देखना है, और अंत में निकाले गए टेक्स्ट को पढ़ना। अंत में आपके पास एक रन करने योग्य जावा प्रोग्राम होगा जो ROI टेक्स्ट को कंसोल में प्रिंट करेगा—कोई रहस्य नहीं, सिर्फ एक स्पष्ट, काम करने वाला समाधान।

## What You’ll Need

शुरू करने से पहले सुनिश्चित करें कि आपके पास बुनियादी चीजें हैं:

| Prerequisite | Why it matters |
|--------------|----------------|
| **Java JDK 8+** | Aspose OCR एक जावा लाइब्रेरी के रूप में आती है; कोई भी आधुनिक JDK चलेगा। |
| **Aspose.OCR for Java** (Aspose वेबसाइट से डाउनलोड करें या Maven के ज़रिए जोड़ें) | `OcrEngine`, `ImageStream`, और संबंधित क्लासेज़ प्रदान करता है। |
| **An image file** (जैसे `receipt.jpg`) जिसमें प्रिंटेबल टेक्स्ट हो | हम इस फ़ाइल के अंदर एक रेक्टेंगल पर इंजन को पॉइंट करेंगे। |
| **IDE or editor** (IntelliJ, Eclipse, VS Code…) | सैंपल को जल्दी से कंपाइल और रन करने में मदद करता है। |

यदि आप Maven उपयोग कर रहे हैं, तो इस डिपेंडेंसी को अपने `pom.xml` में जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **Pro tip:** ऊपर दिया गया वर्ज़न नंबर फ़रवरी 2026 तक का वर्तमान वर्ज़न है। नवीनतम रिलीज़ पर अपडेट करने से आपको बग‑फ़िक्स और परफ़ॉर्मेंस सुधार मिलेंगे।

## Step 1 – Initialize the OCR Engine

सबसे पहले: आपको `OcrEngine` का एक इंस्टेंस चाहिए। इसे आप उस दिमाग़ की तरह समझें जो पिक्सेल का विश्लेषण करेगा।

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

ऐसे क्यों बनाते हैं? Aspose इंजन (जो कॉन्फ़िगरेशन रखता है) को इमेज डेटा से अलग करता है, जिससे आप चाहें तो एक ही इंजन को कई इमेज के लिए पुनः उपयोग कर सकते हैं।

## Step 2 – Load Image for OCR

अब हम वास्तव में **load image for OCR** करते हैं। `ImageStream.fromFile` हेल्पर फ़ाइल को एक स्ट्रीम में पढ़ता है जिसे Aspose समझ सकता है।

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

यदि फ़ाइल नहीं मिलती, तो इंजन एक्सेप्शन फेंकेगा, इसलिए प्रोडक्शन कोड में इसे try‑catch ब्लॉक में रैप करना अच्छा रहेगा। इस डेमो में हम एक्सेप्शन को ऊपर तक उठने देते हैं—कोड को साफ़ रखता है।

## Step 3 – Define the Rectangle (Read Text from Rectangle)

यहीं पर **read text from rectangle** वाला हिस्सा चमकता है। आप इंजन को ठीक‑ठीक बताते हैं कि कहाँ देखना है, जिससे प्रोसेसिंग तेज़ होती है और फ़ॉल्स पॉज़िटिव कम होते हैं।

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **Why a rectangle?**  
> अधिकांश दस्तावेज़ों की लेआउट पूर्वानुमेय होती है—जैसे रसीद में कुल राशि हमेशा नीचे के पास दिखती है। उस हिस्से पर फोकस करने से OCR इंजन अनावश्यक ग्राफ़िक्स को नजरअंदाज़ करता है और सटीकता बढ़ती है।

**Edge case:** यदि रेक्टेंगल इमेज की सीमाओं से बाहर जाता है, तो Aspose चुपचाप उसे क्लैंप कर देता है, लेकिन डेटा खो जाएगा। एक त्वरित वैधता जांच इस समस्या से बचा सकती है:

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## Step 4 – Process the Image

सब कुछ सेट हो जाने पर, हम इंजन को अपना जादू करने के लिए कहते हैं।

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

`process()` कॉल एक `OcrResult` ऑब्जेक्ट रिटर्न करता है जिसमें निकाला गया टेक्स्ट, कॉन्फिडेंस स्कोर, और यदि बाद में चाहिए तो प्रत्येक शब्द के बाउंडिंग बॉक्स भी होते हैं।

## Step 5 – Output the Extracted Text

अंत में, परिणाम को प्रिंट करें। वास्तविक एप्लिकेशन में आप इसे डेटाबेस में स्टोर कर सकते हैं या किसी अन्य सर्विस को भेज सकते हैं, लेकिन इस ट्यूटोरियल के लिए कंसोल आउटपुट पर्याप्त है।

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**Expected output** (मान लें कि रेक्टेंगल ने रसीद पर कुल राशि को कैप्चर किया है):

```
ROI text:
$12.34
```

यदि ROI खाली है या इमेज धुंधली है, तो आपको खाली स्ट्रिंग या गड़बड़ कैरेक्टर दिखेंगे। रेक्टेंगल को समायोजित करें, इमेज क्वालिटी बेहतर करें, या Aspose की प्री‑प्रोसेसिंग ऑप्शन (जैसे `setAutoSkewCorrection(true)`) सक्षम करें।

## Full Working Example

नीचे पूरा, तैयार‑चलाने‑योग्य प्रोग्राम दिया गया है। इसे `RoiDemo.java` नाम की फ़ाइल में कॉपी‑पेस्ट करें, इमेज पाथ को समायोजित करें, और `javac RoiDemo.java && java RoiDemo` चलाएँ।

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **Result verification:** रन करने के बाद, कंसोल आउटपुट की तुलना रेक्टेंगल के अंदर वास्तविक टेक्स्ट से करें। यदि मेल खाता है, तो आपने Aspose OCR का उपयोग करके **extract text from image** सफलतापूर्वक किया है।

## Common Questions & Tips

### What if I need to process multiple ROIs in the same image?
प्रत्येक क्षेत्र के लिए एक नया `Rectangle` बनाएँ, `setRegionOfInterest` फिर से कॉल करें, और `process()` को पुनः चलाएँ। इंजन वही इमेज डेटा पुनः उपयोग करता है, इसलिए परफ़ॉर्मेंस तेज़ रहता है।

### How does Aspose handle different languages or fonts?
आप भाषा मॉडल को `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)` के ज़रिए बदल सकते हैं। गैर‑लैटिन स्क्रिप्ट्स के लिए उपयुक्त भाषा पैक लोड करें (Aspose डाउनलोड पेज पर उपलब्ध)।

### Does the library support PDF input?
हां—Aspose OCR सीधे PDF स्ट्रीम को स्वीकार कर सकता है। बस `ImageStream.fromFile` को `ImageStream.fromPdfFile("doc.pdf")` से बदलें और वैकल्पिक रूप से पेज नंबर निर्दिष्ट करें।

### Can I improve accuracy on low‑quality scans?
प्री‑प्रोसेसिंग सक्षम करें:

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

इन विकल्पों से शोर साफ़ होता है और टेक्स्ट को पहचान से पहले संरेखित किया जाता है।

## Conclusion

हमने अभी-अभी एक पूर्ण **aspose ocr tutorial** पूरा किया जिसमें दिखाया गया कि **extract text from image**, **load image for OCR**, और **read text from rectangle** को जावा में कैसे किया जाता है। मुख्य चरण थे: इंजन को इनिशियलाइज़ करना, इमेज फीड करना, ROI परिभाषित करना, प्रोसेस करना, और अंत में परिणाम प्रिंट करना।

अब आप आगे explore कर सकते हैं:

* **Batch processing** – रसीदों के फ़ोल्डर को लूप करके प्रत्येक कुल राशि को डेटाबेस में स्टोर करना।  
* **Dynamic ROI detection** – इमेज‑प्रोसेसिंग लाइब्रेरी (OpenCV) का उपयोग करके टेक्स्ट ब्लॉक्स को स्वचालित रूप से लोकेट करना।  
* **Post‑processing** – OCR की गड़बड़ियों को साफ़ करने के लिए रेगुलर एक्सप्रेशन या फज़ी मैचिंग लागू करना।

इन विचारों को आज़माएँ, अपने दस्तावेज़ों के अनुसार रेक्टेंगल को समायोजित करें, और आप जल्दी ही एक मजबूत टेक्स्ट‑एक्सट्रैक्शन पाइपलाइन बना लेंगे। Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}