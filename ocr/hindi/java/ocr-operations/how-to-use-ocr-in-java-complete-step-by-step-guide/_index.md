---
category: general
date: 2026-02-22
description: जावा में OCR का उपयोग करके छवि से टेक्स्ट निकालना, OCR की सटीकता सुधारना,
  और व्यावहारिक कोड उदाहरणों के साथ OCR के लिए छवि लोड करना।
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: hi
og_description: जावा में OCR का उपयोग करके छवि से टेक्स्ट निकालने और OCR की सटीकता
  सुधारने का तरीका। तैयार‑से‑चलाने वाले उदाहरण के लिए इस गाइड का पालन करें।
og_title: जावा में OCR का उपयोग कैसे करें – पूर्ण चरण-दर-चरण मार्गदर्शिका
tags:
- OCR
- Java
- Image Processing
title: जावा में OCR का उपयोग कैसे करें – पूर्ण चरण-दर-चरण मार्गदर्शिका
url: /hi/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use OCR in Java – Complete Step‑by‑Step Guide

क्या आपको कभी **how to use OCR** एक झुके हुए स्क्रीनशॉट पर उपयोग करना पड़ा और आश्चर्य हुआ कि आउटपुट गड़बड़ क्यों दिख रहा है? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया के एप्लिकेशन—रसीदें स्कैन करना, फॉर्म को डिजिटल बनाना, या मीम्स से टेक्स्ट निकालना—में भरोसेमंद परिणाम पाने के लिए कुछ सरल सेटिंग्स पर निर्भर होना पड़ता है।

इस ट्यूटोरियल में हम **how to use OCR** को *extract text from image* फ़ाइलों से टेक्स्ट निकालने के लिए कैसे उपयोग किया जाए, **improve OCR accuracy** कैसे बढ़ाया जाए, और एक लोकप्रिय Java OCR लाइब्रेरी का उपयोग करके **load image for OCR** सही तरीके से कैसे किया जाए, यह दिखाएंगे। अंत तक आपके पास एक स्व-निहित प्रोग्राम होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं।

## What You’ll Learn

- वह सटीक कोड जो आपको **load image for OCR** करने के लिए चाहिए (कोई छिपी हुई डिपेंडेंसी नहीं)।
- कौन‑से प्री‑प्रोसेसिंग फ़्लैग **improve OCR accuracy** को बढ़ाते हैं और क्यों महत्वपूर्ण हैं।
- OCR परिणाम को कैसे पढ़ें और कंसोल में प्रिंट करें।
- सामान्य गड़बड़ियाँ—जैसे ROI सेट न करना या नॉइज़ रिडक्शन को अनदेखा करना—और उन्हें कैसे टालें।

### Prerequisites

- Java 17 या नया (कोड किसी भी हालिया JDK के साथ कम्पाइल होता है)।
- एक OCR लाइब्रेरी जो `OcrEngine`, `ImagePreprocessingOptions`, `OcrInput`, और `OcrResult` क्लासेज़ प्रदान करती हो (उदाहरण के लिए, इस स्निपेट में उपयोग किया गया काल्पनिक `com.example.ocr` पैकेज)। इसे अपनी वास्तविक लाइब्रेरी से बदलें।
- एक सैंपल इमेज (`skewed_noisy.png`) जिसे आप किसी फ़ोल्डर में रख सकते हैं।

> **Pro tip:** यदि आप कोई कमर्शियल SDK उपयोग कर रहे हैं, तो लाइसेंस फ़ाइल को अपने क्लासपाथ पर रखें; नहीं तो इंजन इनिशियलाइज़ेशन एरर फेंकेगा।

---

## Step 1: Create an OCR Engine Instance – **how to use OCR** effectively

सबसे पहले आपको एक `OcrEngine` ऑब्जेक्ट चाहिए। इसे उस दिमाग की तरह समझें जो पिक्सेल को समझेगा।

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*Why this matters:* बिना इंजन के आपके पास भाषा मॉडल, कैरेक्टर सेट, या इमेज ह्यूरिस्टिक्स का कोई संदर्भ नहीं रहता। इसे जल्दी बनाकर रखने से बाद में प्री‑प्रोसेसिंग विकल्प जोड़ना आसान हो जाता है।

---

## Step 2: Configure Image Preprocessing – **improve OCR accuracy**

प्री‑प्रोसेसिंग वह गुप्त मसाला है जो शोरयुक्त स्कैन को साफ़, मशीन‑रीडेबल टेक्स्ट में बदल देता है। नीचे हम डेस्क्यू, हाई‑लेवल नॉइज़ रिडक्शन, ऑटो‑कॉन्ट्रास्ट, और ROI को सक्षम करते हैं ताकि चित्र के प्रासंगिक हिस्से पर फोकस किया जा सके।

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*Why this matters:*  
- **Deskew** घुमा हुआ टेक्स्ट को सीधा करता है, जो रसीदें स्कैन करने पर आवश्यक है जब वे पूरी तरह सपाट नहीं होतीं।  
- **Noise reduction** बिखरे हुए पिक्सेल को हटाता है जो अन्यथा कैरेक्टर के रूप में पढ़े जा सकते हैं।  
- **Auto‑contrast** टोनल रेंज को विस्तारित करता है, जिससे हल्के अक्षर उभर कर दिखते हैं।  
- **ROI** इंजन को अनावश्यक बॉर्डर अनदेखा करने को कहता है, जिससे समय और मेमोरी दोनों बचते हैं।

यदि आप इनमें से कोई भी कदम छोड़ देते हैं, तो **improve OCR accuracy** परिणाम में गिरावट देख सकते हैं।

---

## Step 3: Load the Image for OCR – **load image for OCR** correctly

अब हम वास्तव में इंजन को उस फ़ाइल की ओर इशारा करते हैं जिसे पढ़ना है। `OcrInput` क्लास कई इमेजेज़ को स्वीकार कर सकता है, लेकिन इस उदाहरण में हम इसे सरल रखते हैं।

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*Why this matters:* पाथ एब्सोल्यूट या वर्किंग डायरेक्टरी के रिलेटिव होना चाहिए; नहीं तो इंजन `FileNotFoundException` फेंकेगा। साथ ही, `add` मेथड का नाम यह संकेत देता है कि आप कई इमेजेज़ को कतार में लगा सकते हैं—बैच प्रोसेसिंग के लिए उपयोगी।

---

## Step 4: Perform OCR and Output the Recognized Text – **how to use OCR** end‑to‑end

अंत में, हम इंजन से टेक्स्ट पहचानने को कहते हैं और उसे प्रिंट करते हैं। `OcrResult` ऑब्जेक्ट में रॉ स्ट्रिंग, कॉन्फिडेंस स्कोर, और लाइन‑बाय‑लाइन मेटाडाटा (यदि बाद में चाहिए) होते हैं।

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Expected output** (मान लेते हैं सैंपल इमेज में “Hello, OCR World!” लिखा है):

```
=== OCR Output ===
Hello, OCR World!
```

यदि परिणाम गड़बड़ दिखे, तो Step 2 पर वापस जाएँ और प्री‑प्रोसेसिंग विकल्पों को समायोजित करें—शायद नॉइज़ रिडक्शन लेवल कम करें या ROI रेक्टैंगल को बदलें।

---

## Full, Runnable Example

नीचे एक पूर्ण Java प्रोग्राम है जिसे आप `OcrDemo.java` नाम की फ़ाइल में कॉपी‑पेस्ट कर सकते हैं। यह सभी चरणों को एक साथ जोड़ता है।

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

फ़ाइल को सेव करें, `javac OcrDemo.java` से कम्पाइल करें, और `java OcrDemo` चलाएँ। यदि सब कुछ सही ढंग से सेट है तो कंसोल में निकाला गया टेक्स्ट दिखेगा।

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **What if my image is in JPEG format?** | `OcrInput.add()` मेथड किसी भी सपोर्टेड रास्टर फ़ॉर्मेट—PNG, JPEG, BMP, TIFF—को स्वीकार करता है। बस पाथ में फ़ाइल एक्सटेंशन बदल दें। |
| **Can I process multiple pages at once?** | बिल्कुल। प्रत्येक फ़ाइल के लिए `ocrInput.add()` कॉल करें, फिर वही `ocrInput` को `recognize()` में पास करें। इंजन एक कंकैटेनेटेड `OcrResult` लौटाएगा। |
| **What if the OCR result is empty?** | जाँचें कि ROI वास्तव में टेक्स्ट रखता है या नहीं। साथ ही सुनिश्चित करें कि `setDeskewEnabled(true)` ऑन है; 90° रोटेशन इंजन को इमेज खाली समझा सकता है। |
| **How do I change the language model?** | अधिकांश लाइब्रेरीज़ `OcrEngine` पर `setLanguage(String)` मेथड प्रदान करती हैं। `recognize()` से पहले इसे कॉल करें, जैसे `ocrEngine.setLanguage("eng")`। |
| **Is there a way to get confidence scores?** | हाँ, `OcrResult` अक्सर प्रति लाइन या प्रति कैरेक्टर `getConfidence()` देता है। इसे कम‑कॉन्फिडेंस परिणामों को फ़िल्टर करने के लिए उपयोग करें। |

---

## Conclusion

हमने Java में **how to use OCR** को शुरुआत से अंत तक कवर किया: इंजन बनाना, **improve OCR accuracy** के लिए प्री‑प्रोसेसिंग कॉन्फ़िगर करना, सही तरीके से **load image for OCR** करना, और अंत में निकाले गए टेक्स्ट को प्रिंट करना। पूरा कोड स्निपेट चलाने के लिए तैयार है, और प्रत्येक लाइन के पीछे का “क्यों” भी समझाया गया है।

अगला कदम तैयार है? ROI रेक्टैंगल को बदलकर इमेज के विभिन्न हिस्सों पर फोकस करें, `NoiseReduction.MEDIUM` के साथ प्रयोग करें, या आउटपुट को सर्चेबल PDF में इंटीग्रेट करें। आप क्लाउड सर्विसेज़ का उपयोग करके **extract text from image** जैसे संबंधित टॉपिक भी एक्सप्लोर कर सकते हैं, या थ्रेडेड क्यू के साथ हजारों फ़ाइलों को बैच‑प्रोसेस कर सकते हैं।

OCR, इमेज प्री‑प्रोसेसिंग, या Java इंटीग्रेशन के बारे में और सवाल हैं? कमेंट करें, और हैप्पी कोडिंग!

![How to use OCR example](/images/ocr-demo.png "how to use OCR – Java example showing preprocessing and result")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}