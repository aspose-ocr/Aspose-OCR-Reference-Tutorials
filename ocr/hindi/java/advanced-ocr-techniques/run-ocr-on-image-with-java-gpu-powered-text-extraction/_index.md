---
category: general
date: 2026-03-07
description: जावा का उपयोग करके छवि पर OCR चलाएँ। PNG से टेक्स्ट पहचानना, रसीद से
  टेक्स्ट निकालना, और OCR के लिए छवि लोड करना सीखें, एक पूर्ण जावा OCR उदाहरण के साथ।
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: hi
og_description: जावा के साथ छवि पर OCR चलाएँ। यह गाइड दिखाता है कि PNG से टेक्स्ट
  कैसे पहचाना जाए, रसीद से टेक्स्ट कैसे निकाला जाए, और पूर्ण जावा OCR उदाहरण का उपयोग
  करके OCR के लिए छवि कैसे लोड की जाए।
og_title: जावा के साथ इमेज पर OCR चलाएँ – GPU‑संचालित टेक्स्ट निष्कर्षण
tags:
- OCR
- Java
- GPU
- Image Processing
title: जावा के साथ इमेज पर OCR चलाएँ – GPU‑संचालित टेक्स्ट एक्सट्रैक्शन
url: /hi/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java के साथ इमेज पर OCR चलाएँ – GPU‑संचालित टेक्स्ट एक्सट्रैक्शन

क्या आपको **इमेज फ़ाइलों पर OCR चलाने** की ज़रूरत थी लेकिन Java में शुरू करने का तरीका नहीं पता था? आप अकेले नहीं हैं—कई डेवलपर्स पहली बार स्कैन किए हुए रसीद या PNG स्क्रीनशॉट से टेक्स्ट निकालने की कोशिश करते समय इसी समस्या का सामना करते हैं।  

इस ट्यूटोरियल में हम आपको **एक पूर्ण Java OCR उदाहरण** के माध्यम से ले जाएंगे जो न केवल **PNG फ़ाइलों से टेक्स्ट पहचानता** है बल्कि **रसीद इमेज से टेक्स्ट निकालना** भी दिखाता है, और साथ ही गति के लिए GPU एक्सेलेरेशन का उपयोग करता है। अंत तक आपके पास एक तैयार‑चलाने‑योग्य प्रोग्राम होगा जो इमेज को OCR के लिए लोड करता है, प्रोसेस करता है, और प्लेन‑टेक्स्ट परिणाम प्रिंट करता है।

## आप क्या सीखेंगे

- एक साधारण `ImageInputStream` का उपयोग करके **OCR के लिए इमेज लोड** करना।
- GPU सपोर्ट को एनेबल करना ताकि इंजन आधुनिक हार्डवेयर पर तेज़ चले।
- **PNG से टेक्स्ट पहचानने** और रसीद से उपयोगी स्ट्रिंग्स निकालने के सटीक चरण।
- सामान्य समस्याएँ (जैसे, गलत GPU डिवाइस ID) और बेस्ट‑प्रैक्टिस टिप्स।
- एक पूर्ण, रन‑एबल कोड स्निपेट जिसे आप अपने IDE में कॉपी‑पेस्ट कर सकते हैं।

**पूर्वापेक्षाएँ**

- Java 17 या उससे नया (कोड संक्षिप्तता के लिए `var` कीवर्ड का उपयोग करता है, लेकिन आप Java 8 पर हों तो स्पष्ट टाइप्स से बदल सकते हैं)।
- एक OCR लाइब्रेरी जो `OcrEngine`, `ImageInputStream`, और `OcrResult` क्लासेस प्रदान करती है (उदाहरण के लिए, काल्पनिक *FastOCR* SDK; इसे आप अपनी वास्तविक लाइब्रेरी से बदलें)।
- यदि आप प्रदर्शन बूस्ट चाहते हैं तो GPU‑सक्षम मशीन (वैकल्पिक लेकिन अनुशंसित)।

---

## चरण 1: इमेज पर OCR चलाएँ – GPU एक्सेलेरेशन एनेबल करें

सबसे पहले OCR इंजन बनाना और उसे GPU उपयोग करने के लिए बताना है। यह कदम महत्वपूर्ण है क्योंकि GPU सपोर्ट न होने पर इंजन CPU पर फॉल बैक हो जाता है, जो हाई‑रेज़ोल्यूशन रसीदों के लिए स्पष्ट रूप से धीमा हो सकता है।

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**यह क्यों महत्वपूर्ण है:**  
GPU एक्सेलेरेशन OCR इंजन द्वारा किए जाने वाले भारी मैट्रिक्स कैलकुलेशन को ग्राफ़िक्स कार्ड पर स्थानांतरित करता है। यदि आपके पास कई GPU हैं, तो `setGpuDeviceId` वैल्यू बदलकर सबसे अधिक मेमोरी वाले को चुन सकते हैं। GPU को एनेबल न करना “मेरी OCR इतनी धीमी क्यों है?” जैसी शिकायतों का आम कारण है।

> **प्रो टिप:** यदि आपके मशीन में संगत GPU नहीं है, तो `setUseGpu(true)` कॉल बस इग्नोर हो जाएगी—कोई क्रैश नहीं, बस प्रोसेसिंग धीमी होगी।

---

## चरण 2: OCR के लिए इमेज लोड करें

अब जब इंजन तैयार है, हमें उसे एक इमेज देना है। नीचे दिया गया उदाहरण डिस्क पर संग्रहीत PNG रसीद को लोड करने का तरीका दिखाता है। आप अपने OCR लाइब्रेरी द्वारा सपोर्ट किए गए किसी भी इमेज फ़ॉर्मेट के साथ पाथ बदल सकते हैं।

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**एज केस:**  
यदि फ़ाइल मौजूद नहीं है या पाथ गलत है, तो `ImageInputStream` एक `IOException` फेंकेगा। इस कॉल को try‑catch ब्लॉक में रैप करें और एक मददगार संदेश लॉग करें:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## चरण 3: PNG से टेक्स्ट पहचानें

इमेज लोड हो जाने पर, OCR इंजन अब अपना जादू दिखा सकता है। यह चरण वास्तव में **PNG से टेक्स्ट पहचानता** है (या किसी भी अन्य सपोर्टेड फ़ॉर्मेट से) और एक `OcrResult` ऑब्जेक्ट रिटर्न करता है।

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**अंदर क्या हो रहा है?**  
इंजन प्री‑प्रोसेसिंग (डेस्क्यू, बिनैराइज़ेशन) करता है, कैरेक्टर डिटेक्ट करने के लिए न्यूरल नेटवर्क चलाता है, और फिर उन्हें टेक्स्ट लाइनों में असेंबल करता है। चूँकि हमने पहले GPU एनेबल किया था, ये न्यूरल‑नेटवर्क कैलकुलेशन ग्राफ़िक्स कार्ड पर होते हैं, जिससे कुल रन‑टाइम में सेकंड्स बचते हैं।

---

## चरण 4: रसीद से टेक्स्ट निकालें

पहचान के बाद, आमतौर पर आपको केवल रॉ टेक्स्ट चाहिए होता है। `OcrResult` क्लास आमतौर पर एक `getText()` मेथड प्रदान करता है जो एक सिंगल `String` रिटर्न करता है। आप फिर इसे पोस्ट‑प्रोसेस कर सकते हैं (जैसे, रेगेक्स से टोटल, डेट आदि निकालना)।

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**रसीद का सामान्य आउटपुट:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

अब आप इस स्ट्रिंग को अपने स्वयं के पार्सर में फीड करके टोटल अमाउंट, लाइन आइटम्स या टैक्स जानकारी निकाल सकते हैं।

---

## चरण 5: पूर्ण Java OCR उदाहरण – रन‑तैयार

सब कुछ मिलाकर, यहाँ **पूर्ण Java OCR उदाहरण** है जिसे आप `Main.java` फ़ाइल में डाल सकते हैं। सुनिश्चित करें कि OCR लाइब्रेरी आपके क्लासपाथ में है।

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**अपेक्षित कंसोल आउटपुट** (ऊपर दिए गए सैंपल रसीद को मानते हुए):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

यदि आउटपुट गड़बड़ दिखे, तो जाँचें कि इमेज स्पष्ट (हाई DPI) है और OCR लैंग्वेज पैक आपके रसीद की भाषा से मेल खाता है।

---

## सामान्य प्रश्न एवं समस्याएँ

| प्रश्न | उत्तर |
|----------|--------|
| *अगर मेरा GPU डिटेक्ट नहीं हो रहा है तो क्या करें?* | इंजन स्वचालित रूप से CPU पर फॉल बैक हो जाएगा। ड्राइवर चेक करें और सुनिश्चित करें कि `setGpuDeviceId` मौजूद डिवाइस से मेल खाता है (`nvidia-smi` Linux पर मदद कर सकता है)। |
| *क्या मैं JPEG या TIFF फ़ाइलों को प्रोसेस कर सकता हूँ?* | हाँ—सिर्फ `ImageInputStream` में फ़ाइल एक्सटेंशन बदल दें। OCR लाइब्रेरी आमतौर पर फ़ॉर्मेट को ऑटो‑डिटेक्ट करती है। |
| *क्या कई रसीदों को बैच‑प्रोसेस किया जा सकता है?* | कोड को लूप में रैप करें और वही `OcrEngine` इंस्टेंस री‑यूज़ करें; हर इमेज के लिए री‑इनीशियलाइज़ करने से GPU मेमोरी बर्बाद होगी। |
| *लो‑कॉन्ट्रास्ट रसीदों की एक्यूरेसी कैसे बढ़ाएँ?* | इमेज को प्री‑प्रोसेस करें (कॉन्ट्रास्ट बढ़ाएँ, ग्रेस्केल में बदलें) इससे पहले कि उसे OCR इंजन को दें। कुछ लाइब्रेरीज़ `preprocess` API भी देती हैं। |

---

## निष्कर्ष

आप अब जानते हैं **Java में इमेज फ़ाइलों पर OCR कैसे चलाएँ**, इमेज लोड करने से लेकर रसीद से साफ़ टेक्स्ट निकालने तक। इस walkthrough में **PNG से टेक्स्ट पहचानना**, **रसीद से टेक्स्ट निकालना**, और एक **java OCR उदाहरण** दिखाया गया है जिसे आप किसी भी प्रोजेक्ट में एडेप्ट कर सकते हैं।  

अगले कदम? GPU फ़्लैग को ऑफ़ करके प्रदर्शन अंतर देखें, विभिन्न इमेज रिज़ॉल्यूशन के साथ प्रयोग करें, या रेगेक्स‑आधारित पार्सर इंटीग्रेट करके टोटल ऑटोमैटिकली निकालें। यदि आप अधिक एडवांस्ड टॉपिक्स में रुचि रखते हैं, तो **OCR पोस्ट‑प्रोसेसिंग**, **भाषा मॉडल करेक्शन**, या **बैच प्रोसेसिंग पाइपलाइन** देखें।

कोडिंग का आनंद लें, और आपकी रसीदें हमेशा पठनीय रहें!  

![run OCR on image example](/images/run-ocr-on-image.png "run OCR on image – Java example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}