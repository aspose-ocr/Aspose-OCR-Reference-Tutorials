---
category: general
date: 2026-02-14
description: 'बैच इमेज OCR को आसान बनाएं: जावा में समानांतर प्रोसेसिंग के साथ Aspose
  OCR का उपयोग करके PNG फ़ाइलों से टेक्स्ट निकालना सीखें।'
draft: false
keywords:
- batch image OCR
- extract text from png
- parallel OCR Java
- Aspose OCR async
- OCR batch processing
language: hi
og_description: बैच इमेज OCR ट्यूटोरियल जो जावा में Aspose OCR के असिंक्रोनस API का
  उपयोग करके PNG फ़ाइलों से टेक्स्ट निकालने का तरीका दिखाता है।
og_title: जावा में बैच इमेज OCR – तेज़ PNG टेक्स्ट निष्कर्षण
tags:
- Java
- OCR
- Aspose
- Image Processing
title: जावा में बैच इमेज OCR – PNG फ़ाइलों से तेज़ी से टेक्स्ट निकालें
url: /hi/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/
---

डायग्राम".

Now ensure all shortcodes remain.

Now produce final output with everything.

Let's craft the final markdown.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Batch Image OCR in Java – PNG फ़ाइलों से तेज़ी से टेक्स्ट निकालें

क्या आपको कभी **batch image OCR** को PNG स्कैन की फ़ोल्डर पर चलाने की ज़रूरत पड़ी है लेकिन गति को लेकर चिंतित रहे हैं? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स—इनवॉइस डिजिटाइज़ेशन, स्कैन की गई पुस्तकों का अभिलेख, या रसीदों की प्रोसेसिंग—में डेवलपर्स को **PNG से टेक्स्ट निकालना** जल्दी और भरोसेमंद तरीके से करना पड़ता है।  

अच्छी खबर? Aspose OCR के असिंक्रोनस API के साथ आप कुछ ही Java लाइनों में एक समानांतर OCR पाइपलाइन बना सकते हैं। इस गाइड में हम पूरी, चलाने योग्य समाधान को चरण‑दर‑चरण देखेंगे, प्रत्येक भाग क्यों महत्वपूर्ण है समझाएंगे, और परिणामों को कैसे सत्यापित करें दिखाएंगे। अंत तक आपके पास एक स्व‑निहित प्रोग्राम होगा जो पूरी बैच PNG फ़ाइलों को समानांतर में प्रोसेस करता है, आपको साफ़, स्पेल‑चेक्ड टेक्स्ट आउटपुट देता है।

## आप क्या सीखेंगे

- बैच प्रोसेसिंग के लिए PNG फ़ाइलों की सूची कैसे बनाएं  
- Aspose `OcrEngine` को अंग्रेज़ी भाषा और स्पेल करेक्शन के लिए कॉन्फ़िगर करना  
- `processAsync` के साथ असिंक्रोनस OCR चलाना और `Future` परिणाम को संभालना  
- प्रत्येक इमेज के लिए पहचाना गया टेक्स्ट पढ़ना और प्रदर्शित करना  
- स्केलिंग, एरर हैंडलिंग, और प्रदर्शन ट्यूनिंग के टिप्स  

### पूर्वापेक्षाएँ

- Java 8 या नया स्थापित हो (कोड मानक `java.util.concurrent` पैकेज का उपयोग करता है)  
- Aspose OCR for Java लाइसेंस या फ्री ट्रायल (Aspose वेबसाइट से डाउनलोड करें)  
- एक फ़ोल्डर जिसमें कुछ PNG स्क्रीनशॉट या स्कैन किए हुए पेज हों जिन्हें आप टेस्ट करना चाहते हैं  

अब, चलिए शुरू करते हैं।

## चरण 1 – बैच के लिए अपने PNG फ़ाइलें इकट्ठा करें

OCR इंजन को काम करने से पहले यह जानना पड़ता है कि कौन‑सी इमेज प्रोसेस करनी है। सबसे सरल तरीका है `List<String>` बनाना जिसमें पूर्ण या सापेक्ष फ़ाइल पाथ हों।

```java
// Step 1: Prepare a list of PNG files you want to run OCR on
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png",
        "YOUR_DIRECTORY/page4.png");
```

**यह क्यों महत्वपूर्ण है:**  
सूची को पहले से बनाकर इंजन को प्रत्येक फ़ाइल को स्वतंत्र रूप से शेड्यूल करने की सुविधा मिलती है, जो वास्तविक बैच प्रोसेसिंग की नींव है। यदि बाद में आपको डायरेक्टरी को डायनामिक स्कैन करना हो, तो बस स्थैतिक `Arrays.asList` को `Files.walk` स्ट्रीम से बदल दें।

## चरण 2 – Aspose OCR इंजन को इनिशियलाइज़ और ट्यून करें

Aspose का `OcrEngine` अत्यधिक कॉन्फ़िगरेबल है। यहाँ हम भाषा को अंग्रेज़ी सेट करते हैं और स्पेल करेक्शन चालू करते हैं—दो विकल्प जो शोरयुक्त PNG स्कैन से निकाले गए टेक्स्ट की गुणवत्ता को काफी बढ़ाते हैं।

```java
// Step 2: Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions()
         .setLanguage(OcrLanguage.ENGLISH)          // English language model
         .setSpellCorrectionEnabled(true);          // Enable spell‑checking
```

**इन सेटिंग्स का कारण:**  
- **Language selection** इंजन को बताता है कि कौन‑सा कैरेक्टर सेट और डिक्शनरी उपयोग करनी है, जिससे गलत पहचान कम होती है।  
- **Spell correction** सामान्य OCR त्रुटियों (जैसे “1” बनाम “l”) को आउटपुट को पोस्ट‑प्रोसेस किए बिना पकड़ लेता है।

> **प्रो टिप:** यदि आपकी इमेज में कई भाषाएँ हैं, तो आप `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.FRENCH)` जैसी सूची पास कर सकते हैं।

## चरण 3 – असिंक्रोनस बैच प्रोसेसिंग शुरू करें

भारी काम `processAsync` में होता है। यह एक `Future<List<OcrResult>>` लौटाता है, जिससे आपका मुख्य थ्रेड बैकग्राउंड में OCR चलाते हुए अन्य काम कर सकता है।

```java
// Step 3: Start asynchronous processing of the image batch
Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

// (Optional) Do something useful while OCR runs, e.g., log progress, load UI, etc.
System.out.println("OCR started – you can perform other tasks now...");
```

**असिंक्रोनस क्यों:**  
OCR को क्रमिक रूप से चलाना बहुत धीमा हो सकता है—प्रत्येक PNG को एक सेकंड या उससे अधिक लग सकता है। कार्य को थ्रेड पूल को सौंपकर आप कई CPU कोर का उपयोग करते हैं और कुल रन‑टाइम को काफी घटा देते हैं।

## चरण 4 – परिणाम तैयार होने पर प्राप्त करें

जब आप आउटपुट का उपयोग करने के लिए तैयार हों, तो बस `Future` पर `get()` कॉल करें। यह कॉल केवल OCR समाप्त होने तक ब्लॉक करती है, फिर आपको इनपुट सूची के समान क्रम में `OcrResult` ऑब्जेक्ट्स की सूची देती है।

```java
// Step 4: Wait for all results and retrieve them
List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion
```

**टाइम‑आउट को संभालना:**  
यदि आप अनिश्चित ब्लॉक से बचना चाहते हैं, तो `ocrFuture.get(60, TimeUnit.SECONDS)` का उपयोग करें और `TimeoutException` को पकड़ कर फॉलबैक लागू करें।

## चरण 5 – प्रत्येक PNG के लिए पहचाना गया टेक्स्ट दिखाएँ

अब आपके पास परिणाम हैं, उन पर इटररेट करें और मूल फ़ाइल नाम के साथ निकाला गया टेक्स्ट प्रिंट करें। यही वह जगह है जहाँ आप अंततः **PNG से टेक्स्ट निकालते** हैं।

```java
// Step 5: Show the OCR output for each image
for (int i = 0; i < ocrResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(ocrResults.get(i).getText());
    System.out.println("---");
}
```

**अपेक्षित आउटपुट उदाहरण**

```
File: YOUR_DIRECTORY/page1.png
Invoice #12345
Date: 2024‑03‑01
Total: $1,250.00
---
File: YOUR_DIRECTORY/page2.png
...
```

यदि OCR इंजन पेज को पहचान नहीं पाता, तो संबंधित `getText()` एक खाली स्ट्रिंग लौटाएगा—उत्पादन कोड में हमेशा इसे चेक करना अच्छा रहता है।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा, तैयार‑चलाने‑योग्य प्रोग्राम है जो सभी भागों को जोड़ता है। इसे `ParallelOcrDemo.java` नाम की फ़ाइल में कॉपी‑पेस्ट करें, `YOUR_DIRECTORY` को अपने PNG फ़ोल्डर के पाथ से बदलें, और `javac ParallelOcrDemo.java && java ParallelOcrDemo` चलाएँ।

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare a list of image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png",
                "YOUR_DIRECTORY/page4.png");

        // Step 2: Create and configure the OCR engine (set language and enable spell‑checking)
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions()
                 .setLanguage(OcrLanguage.ENGLISH)
                 .setSpellCorrectionEnabled(true);

        // Step 3: Start asynchronous processing of the image batch
        Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

        // (Optional) Perform other work here while OCR runs in the background...
        System.out.println("OCR processing started in background...");

        // Step 4: Wait for all results and retrieve them
        List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion

        // Step 5: Display the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### डेमो चलाना

1. **कम्पाइल** – `javac -cp "aspose-ocr.jar" ParallelOcrDemo.java`  
2. **चलाएँ** – `java -cp ".:aspose-ocr.jar" ParallelOcrDemo`  

आपको प्रत्येक PNG फ़ाइल नाम के बाद निकाला गया टेक्स्ट, डैश से अलग दिखना चाहिए।  

> **नोट:** यदि आपको `LicenseException` मिलता है, तो इंजन बनाने से पहले अपना Aspose लाइसेंस लोड करना सुनिश्चित करें:

```java
License lic = new License();
lic.setLicense("Aspose.OCR.Java.lic");
```

## स्केलिंग अप – वास्तविक‑दुनिया बैच OCR के लिए टिप्स

| स्थिति | सिफ़ारिश |
|-----------|----------------|
| **Hundreds of PNGs** | `ocrEngine.setThreadPoolSize(8)` (या अधिक, CPU कोर के अनुसार) के द्वारा थ्रेड पूल आकार बढ़ाएँ। |
| **Memory constraints** | फ़ाइलों को छोटे बैच (जैसे 50) में प्रोसेस करें और प्रत्येक बैच के बाद `OcrResult` सूची को रिलीज़ करें। |
| **Variable image quality** | `setPreprocessingOptions` को सक्षम करें ताकि पहचान से पहले ऑटो‑रोटेट, डेस्क्यू या कंट्रास्ट बढ़ाया जा सके। |
| **Multiple languages** | `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.SPANISH)` कॉल करें और वैकल्पिक रूप से कस्टम डिक्शनरी सेट करें। |
| **Error handling** | `ocrFuture.get()` को `ExecutionException` के लिए try‑catch ब्लॉक में रखें, ताकि फेल हुई फ़ाइलों को लॉग किया जा सके बिना पूरी बैच को रोकें। |

इन रणनीतियों से आपका **batch image OCR** पाइपलाइन मजबूत बना रहेगा, चाहे इनपुट सेट कितना भी बड़ा हो।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या यह JPEG या TIFF फ़ाइलों के साथ काम करता है?**  
**उत्तर:** बिल्कुल। `processAsync` मेथड Aspose OCR द्वारा समर्थित किसी भी फॉर्मेट (PNG, JPEG, TIFF, BMP, आदि) को स्वीकार करता है। बस अपनी सूची में फ़ाइल एक्सटेंशन बदल दें।

**प्रश्न: यदि मुझे लेआउट (टेबल, कॉलम) को संरक्षित रखना है तो क्या करें?**  
**उत्तर:** Aspose OCR `getLayoutResult()` मेथड प्रदान करता है जो पोज़िशनल डेटा देता है। आप प्रत्येक शब्द के बाउंडिंग बॉक्स का विश्लेषण करके टेबल पुनर्निर्मित कर सकते हैं।

**प्रश्न: क्या मैं इसे सर्वरलेस प्लेटफ़ॉर्म पर चला सकता हूँ?**  
**उत्तर:** हाँ—JAR को Aspose लाइब्रेरी के साथ पैकेज करें और AWS Lambda, Azure Functions, या Google Cloud Functions पर डिप्लॉय करें। OCR थ्रेड पूल के लिए फ़ंक्शन की मेमोरी अलोकेशन पर्याप्त रखना याद रखें।

## निष्कर्ष

आपके पास अब एक पूर्ण, स्व‑निहित **batch image OCR** समाधान है जो Aspose OCR के असिंक्रोनस API का उपयोग करके जावा में **PNG से टेक्स्ट निकालता** है। इस ट्यूटोरियल में फ़ाइल सूची तैयार करने से लेकर भाषा और स्पेल‑चेकिंग कॉन्फ़िगर करने, समानांतर प्रोसेसिंग लॉन्च करने, परिणाम संभालने, और प्रोडक्शन वर्कलोड के लिए पाइपलाइन स्केल करने तक सब कुछ कवर किया गया है।

अगला कदम तैयार है? भाषा को फ्रेंच में बदलें, कस्टम डिक्शनरी के साथ प्रयोग करें, या आउटपुट को सर्चेबल ElasticSearch इंडेक्स में इंटीग्रेट करें। तेज़ बैच OCR को आधुनिक जावा कॉन्करेंसी के साथ मिलाकर संभावनाएँ असीमित हैं।

Happy coding, and may your text extraction be swift and spot‑on! 

![एकाधिक PNG फ़ाइलों को संभालते हुए समानांतर OCR कार्यकर्ताओं का आरेख](/images/batch-ocr-diagram.png){: .center alt="बैच इमेज OCR प्रोसेसिंग डायग्राम"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}