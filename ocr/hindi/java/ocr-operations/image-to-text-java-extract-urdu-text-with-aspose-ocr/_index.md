---
category: general
date: 2026-02-17
description: 'इमेज‑टू‑टेक्स्ट जावा ट्यूटोरियल: Aspose OCR का उपयोग करके छवि से उर्दू
  टेक्स्ट निकालना सीखें। पूर्ण जावा OCR उदाहरण शामिल है।'
draft: false
keywords:
- image to text java
- how to extract text
- extract urdu text
- java ocr example
- load image ocr
language: hi
og_description: इमेज‑टू‑टेक्स्ट जावा ट्यूटोरियल दिखाता है कि Aspose OCR का उपयोग करके
  छवि से उर्दू टेक्स्ट कैसे निकाला जाए। पूर्ण जावा OCR उदाहरण को चरण‑दर‑चरण अनुसरण
  करें।
og_title: 'इमेज‑टू‑टेक्स्ट जावा: Aspose OCR के साथ उर्दू टेक्स्ट निकालें'
tags:
- OCR
- Java
- Aspose
title: 'इमेज टू टेक्स्ट जावा: Aspose OCR के साथ उर्दू टेक्स्ट निकालें'
url: /hi/java/ocr-operations/image-to-text-java-extract-urdu-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज टू टेक्स्ट जावा: Aspose OCR के साथ उर्दू टेक्स्ट निकालें

यदि आपको उर्दू दस्तावेज़ों के लिए **image to text java** रूपांतरण करने की आवश्यकता है, तो आप सही जगह पर हैं। कभी सोचा है *कैसे टेक्स्ट निकालें* एक हाथ से लिखे नोट या स्कैन किए हुए समाचार पत्र के पृष्ठ की तस्वीर से? यह गाइड आपको एक **java ocr example** के माध्यम से दिखाएगा जो Aspose OCR का उपयोग करके इमेज से सीधे उर्दू अक्षर निकालता है।

हम लाइब्रेरी को लाइसेंस करने से लेकर कंसोल पर परिणाम प्रिंट करने तक सब कुछ कवर करेंगे। अंत तक आप **load image ocr** फ़ाइलें लोड कर सकेंगे, भाषा को उर्दू सेट कर सकेंगे, और साफ़ Unicode आउटपुट प्राप्त कर सकेंगे—कोई अतिरिक्त टूल्स की आवश्यकता नहीं।  

## आपको क्या चाहिए

- **Java Development Kit (JDK) 8+** – कोड किसी भी नवीनतम JDK पर काम करता है।
- **Aspose.OCR for Java** JAR (Aspose वेबसाइट से डाउनलोड करें)।
- एक वैध **Aspose OCR license** फ़ाइल (`Aspose.OCR.lic`)।
- एक इमेज जिसमें उर्दू टेक्स्ट हो, उदाहरण के लिए `urdu-sample.png`।

इन बुनियादी चीज़ों के होने से आप सीधे कोड में कूद सकते हैं बिना किसी गायब निर्भरताओं की खोज किए।

## image to text java – Aspose OCR सेटअप

सबसे पहले, हमें Aspose को बताना होगा कि हमारे पास लाइसेंस है। बिना लाइसेंस के लाइब्रेरी इवैल्यूएशन मोड में चलती है और आउटपुट में वॉटरमार्क जोड़ देती है।

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Why this matters:** लाइसेंसिंग 5‑सेकंड की प्रोसेसिंग सीमा को हटाता है और 2025‑Q3 में जोड़ा गया पूरा उर्दू भाषा पैक अनलॉक करता है। यदि आप इस चरण को छोड़ देते हैं, तो OCR इंजन अभी भी काम करेगा, लेकिन परिणामों में एक छोटा “Evaluation” टैग दिखेगा।

## टेक्स्ट निकालें – OCR इंजन को इनिशियलाइज़ करें

अब हम इंजन बनाते हैं और स्पष्ट रूप से बताते हैं कि हमें उर्दू में रुचि है। `OcrLanguage.URDU` कॉन्स्टेंट सही कैरेक्टर सेट और सेगमेंटेशन नियम सक्रिय करता है।

```java
        // Step 2: Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3
```

**Pro tip:** यदि आपको एक ही रन में कई भाषाओं को प्रोसेस करना हो, तो आप कॉमा‑सेपरेटेड सूची पास कर सकते हैं, जैसे `OcrLanguage.ENGLISH, OcrLanguage.URDU`। इंजन प्रत्येक क्षेत्र को ऑटो‑डिटेक्ट करेगा।

## इमेज OCR लोड करें – इनपुट तैयार करना

Aspose एक `OcrInput` ऑब्जेक्ट के साथ काम करता है जो एक या कई इमेज रख सकता है। यहाँ हम स्थानीय फ़ाइल से **load image ocr** डेटा लोड करते हैं।

```java
        // Step 3: Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");
```

> **Note:** `YOUR_DIRECTORY` को अपने प्रोजेक्ट रूट से पूर्ण पाथ या रिलेटिव पाथ से बदलें। यदि फ़ाइल नहीं मिलती, तो Aspose `FileNotFoundException` फेंकेगा। `new File(path).exists()` के साथ एक त्वरित जांच बहुत समय बचा सकती है।

## टेक्स्ट को पहचानें – OCR प्रोसेस चलाना

इंजन को कॉन्फ़िगर करने और इमेज लोड करने के बाद, हम अंत में `recognize` कॉल करते हैं। यह मेथड एक `OcrResult` लौटाता है जिसमें निकाली गई स्ट्रिंग होती है।

```java
        // Step 4: Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**What’s happening under the hood?** OCR इंजन इमेज को लाइनों में, फिर कैरेक्टर्स में विभाजित करता है, उर्दू‑विशिष्ट शेपिंग नियम (जैसे जॉइनिंग फॉर्म) लागू करता है। इसलिए भाषा को पहले सेट करना महत्वपूर्ण है; अन्यथा आपको गड़बड़ लैटिन प्लेसहोल्डर मिलेंगे।

## पहचाने गए उर्दू टेक्स्ट को प्रिंट करें

अंतिम चरण बस परिणाम को प्रिंट करना है। क्योंकि उर्दू दाएँ‑से‑बाएँ स्क्रिप्ट उपयोग करता है, सुनिश्चित करें कि आपका कंसोल Unicode सपोर्ट करता हो (अधिकांश आधुनिक टर्मिनल करते हैं)।

```java
        // Step 5: Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

**Expected output (example):**

```
Urdu text:
یہ ایک مثال کا متن ہے جو تصویر سے نکالا گیا ہے۔
```

यदि आपको प्रश्न चिह्न या खाली स्ट्रिंग्स दिखें, तो दोबारा जांचें कि आपका कंसोल एन्कोडिंग UTF‑8 पर सेट है (`chcp 65001` विंडोज़ पर, या Java को `-Dfile.encoding=UTF-8` के साथ चलाएँ)।

## पूर्ण कार्यशील उदाहरण – सभी चरण एक जगह

नीचे पूरा, कॉपी‑एंड‑पेस्ट‑तैयार प्रोग्राम है। कोई बाहरी रेफ़रेंस नहीं, सिर्फ एक ही Java फ़ाइल।

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3

        // Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");

        // Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

इसे चलाएँ:

```bash
javac -cp "aspose-ocr-23.10.jar" UrduDemo.java
java -cp ".:aspose-ocr-23.10.jar" UrduDemo
```

`JAR` संस्करण (`23.10`) को अपने डाउनलोड किए हुए संस्करण से बदलें। कंसोल आपके PNG से निकाली गई उर्दू वाक्य दिखाएगा।

## सामान्य समस्याएँ और किनारे के केस

| Issue | Why it Happens | How to Fix |
|-------|----------------|------------|
| **Empty output** | इमेज बहुत डार्क या कम‑रिज़ॉल्यूशन है। | `BufferedImage` का उपयोग करके इमेज को प्री‑प्रोसेस करें (कॉन्ट्रास्ट बढ़ाएँ, बाइनराइज़ करें) Aspose को फीड करने से पहले। |
| **Garbage characters** | गलत भाषा सेट की गई है (डिफ़ॉल्ट अंग्रेज़ी है)। | सुनिश्चित करें कि `ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU);` को `recognize` से पहले कॉल किया गया है। |
| **License not found** | पाथ में टाइपो या फ़ाइल गायब है। | एक एब्सोल्यूट पाथ उपयोग करें या `.lic` फ़ाइल को क्लासपाथ में रखें और `license.setLicense("Aspose.OCR.lic");` कॉल करें। |
| **Out‑of‑memory on large images** | बड़ी PNG फ़ाइलें हीप को खा लेती हैं। | आंतरिक रूप से डाउनस्केल करने के लिए `ocrEngine.setMaxImageSize(2000);` कॉल करें, या स्वयं इमेज का आकार बदलें। |

## डेमो का विस्तार

- **Batch processing:** फ़ोल्डर पर लूप करें, प्रत्येक फ़ाइल को उसी `OcrInput` में जोड़ें, और परिणाम CSV में एकत्र करें।  
- **Different languages:** `OcrLanguage.URDU` को `OcrLanguage.ARABIC` से बदलें या कई भाषाओं को मिलाएँ।  
- **Saving to file:** `Files.write(Paths.get("output.txt"), ocrResult.getText().getBytes(StandardCharsets.UTF_8));` का उपयोग करें।  

इन सभी विचारों का निर्माण हमने अभी बनाए **java ocr example** पर आधारित है, जिससे आप समाधान को वास्तविक‑दुनिया के प्रोजेक्ट्स के अनुसार अनुकूलित कर सकते हैं।

## निष्कर्ष

अब आपके पास एक ठोस **image to text java** वर्कफ़्लो है जो Aspose OCR का उपयोग करके इमेज से उर्दू अक्षर निकालता है। ट्यूटोरियल ने हर चरण को कवर किया—लाइसेंसिंग और भाषा चयन से लेकर इमेज लोड करने और परिणाम प्रिंट करने तक—ताकि आप कोड को किसी भी Java प्रोजेक्ट में पेस्ट कर सकें और इसका कार्य देख सकें।

अगला, बड़े PDFs, विभिन्न स्क्रिप्ट्स के साथ प्रयोग करें, या OCR चरण को Spring Boot REST एंडपॉइंट में इंटीग्रेट करने की कोशिश करें। वही सिद्धांत—**how to extract text**, **load image o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}