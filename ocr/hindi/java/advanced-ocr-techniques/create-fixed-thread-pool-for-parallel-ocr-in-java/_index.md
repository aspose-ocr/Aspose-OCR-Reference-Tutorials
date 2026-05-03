---
category: general
date: 2026-05-03
description: जावा में फिक्स्ड थ्रेड पूल बनाकर छवियों से तेज़ी से टेक्स्ट निकालें।
  जानें कैसे OCR चलाएँ, छवि को टेक्स्ट में बदलें, और समानांतर OCR प्रोसेसिंग से प्रदर्शन
  को बढ़ाएँ।
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: hi
og_description: जावा में फिक्स्ड थ्रेड पूल बनाकर छवियों से तेज़ी से टेक्स्ट निकालें।
  जानें OCR कैसे चलाएँ, छवि को टेक्स्ट में बदलें, और समानांतर OCR प्रोसेसिंग से प्रदर्शन
  बढ़ाएँ।
og_title: जावा में समानांतर OCR के लिए फिक्स्ड थ्रेड पूल बनाएं
tags:
- Java
- OCR
- Multithreading
title: जावा में समानांतर OCR के लिए फिक्स्ड थ्रेड पूल बनाएं
url: /hi/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में Parallel OCR के लिए Fixed Thread Pool बनाएं

क्या आपको कभी **create fixed thread pool** बनाकर OCR जॉब्स को तेज़ करने की ज़रूरत पड़ी, लेकिन आप नहीं जानते थे कि कहाँ से शुरू करें? आप अकेले नहीं हैं। कई इमेज‑हैवी प्रोजेक्ट्स में बॉटलनेक सिंगल‑थ्रेडेड OCR कॉल होता है, और समाधान आश्चर्यजनक रूप से सरल है: वर्कर थ्रेड्स का एक पूल बनाएं और उन्हें फ़ाइलों को समानांतर रूप से प्रोसेस करने दें।  

इस ट्यूटोरियल में आप सीखेंगे कि Aspose OCR का उपयोग करके **extract text from images** कैसे किया जाता है, **run OCR** को कैसे कुशलता से चलाया जाता है, और **convert image to text** को बिना CPU पर अधिक लोड डाले कैसे किया जाता है। अंत तक आपके पास एक तैयार‑to‑run जावा प्रोग्राम होगा जो **parallel OCR processing** को कुछ नमूना चित्रों पर दर्शाता है।

## आप क्या बनाएँगे

* इमेज पाथ्स (PNG, JPG, TIFF, BMP) की सूची पढ़ता है।
* **Creates a fixed thread pool** को CPU कोर की संख्या के अनुसार आकार देता है।
* प्रत्येक इमेज के लिए OCR टास्क डिस्पैच करता है।
* पहचाने गए टेक्स्ट को इकट्ठा करता है और कंसोल पर प्रिंट करता है।
* Executor को साफ़ तौर पर शटडाउन करता है।

कोई बाहरी बिल्ड टूल नहीं, कोई फैंसी फ्रेमवर्क नहीं—सिर्फ साधारण जावा और Aspose OCR लाइब्रेरी। यदि आपके पास Java 8+ और एक अच्छा IDE है, तो आप तैयार हैं।

## पूर्वापेक्षाएँ

* **Java Development Kit (JDK) 8 या नया** – कोड लैम्ब्डा का उपयोग करता है, इसलिए पुराने संस्करण कंपाइल नहीं होंगे।
* **Aspose OCR for Java** – Aspose वेबसाइट से JAR डाउनलोड करें या Maven (`com.aspose:aspose-ocr`) के माध्यम से प्राप्त करें।
* कुछ टेस्ट इमेजेज वाला फ़ोल्डर (कोड `YOUR_DIRECTORY` की ओर इशारा करता है)।
* जावा कन्करेंसी की बुनियादी जानकारी (बाकी हम समझाएंगे)।

> *Pro tip:* यदि आप Maven का उपयोग कर रहे हैं, तो अपनी `pom.xml` में डिपेंडेंसी जोड़ें और IDE को क्लासपाथ संभालने दें।

---

## चरण 1: आवश्यक इम्पोर्ट जोड़ें

सबसे पहले, आवश्यक क्लासेज़ को स्कोप में लाएँ। यह सिर्फ बायलरप्लेट नहीं है; प्रत्येक इम्पोर्ट JVM को बताता है कि OCR इंजन, इमेज हैंडलिंग यूटिलिटीज़, और कन्करेंसी टूल्स जहाँ स्थित हैं, जिससे हम **create fixed thread pool** इंस्टेंस बना सकें।

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – कोर OCR API।  
* `java.util.*` – इमेज पाथ्स और परिणामों को स्टोर करने के लिए कलेक्शन्स।  
* `java.util.concurrent.*` – कन्करेंसी पैकेज जिसमें `ExecutorService` और `Future` होते हैं।

---

## चरण 2: प्रोसेस करने वाली इमेजेज़ को परिभाषित करें

अगला, हम उन फ़ाइलों की सूची बनाते हैं जिन्हें हम **extract text from images** करना चाहते हैं। `Arrays.asList` का उपयोग कोड को संक्षिप्त रखता है और हमें बाकी लॉजिक को बदले बिना अपना डायरेक्टरी बदलने देता है।

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

बिना झिझक और एंट्रीज़ जोड़ें; थ्रेड पूल आपके CPU कोर की संख्या के आधार पर स्वतः स्केल हो जाएगा।

---

## चरण 3: CPU कोर के अनुसार **Create Fixed Thread Pool** बनाएं

यह ट्यूटोरियल का मुख्य भाग है। हम रनटाइम से पूछते हैं कि कितने कोर उपलब्ध हैं और `Executors` फ़ैक्ट्री से ठीक उसी आकार का पूल मांगते हैं। फिक्स्ड क्यों? क्योंकि थ्रेड्स की पूर्वनिर्धारित संख्या “थ्रेड एक्सप्लोजन” को रोकती है, जो OS को संसाधनों से वंचित कर सकता है।

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` लॉजिकल कोर काउंट (हाइपर‑थ्रेड्स सहित) लौटाता है।  
* `newFixedThreadPool(coreCount)` सुनिश्चित करता है कि हम CPU की क्षमता से अधिक न जाएँ, जो समानांतर में **run OCR** करने का सबसे सुरक्षित तरीका है।

---

## चरण 4: प्रत्येक इमेज के लिए OCR टास्क सबमिट करें

अब हम प्रत्येक फ़ाइल पाथ को एक कॉलेबल में बदलते हैं जो **runs OCR**, टेक्स्ट को पहचानता है, और परिणाम लौटाता है। ध्यान दें कि हम लैम्ब्डा के अंदर एक नया `OcrEngine` इंस्टैंशिएट करते हैं—यह इंजन की स्टेट को थ्रेड‑सेफ़ नहीं होने से बचाता है।

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* प्रत्येक `submit` कॉल लैम्ब्डा को पूल को देती है, जो इसे एक आइडल थ्रेड पर शेड्यूल करता है।  
* `Future<String>` ऑब्जेक्ट्स हमें बाद में पहचाना गया टेक्स्ट प्राप्त करने देते हैं, यदि आवश्यक हो तो क्रम बनाए रखते हैं।

---

## चरण 5: पहचाने गए टेक्स्ट को प्राप्त करें और प्रदर्शित करें

एक बार सभी टास्क क्यू हो जाएँ, हम बस `Future` सूची पर इटरेट करते हैं, `get()` कॉल करके प्रत्येक OCR जॉब के समाप्त होने तक ब्लॉक करते हैं। यही वह जगह है जहाँ **convert image to text** चरण आपके सामने स्पष्ट हो जाता है: `engine.getText()` कॉल कच्चा स्ट्रिंग लौटाता है।

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

सामान्य कंसोल आउटपुट इस प्रकार दिखता है:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

यदि कोई फ़ाइल फेल हो जाती है (शायद वह करप्ट है), तो आप एक लाइन देखेंगे जो `Failed:` से शुरू होती है और उसके बाद पाथ आता है—त्वरित डिबगिंग के लिए उपयोगी।

---

## चरण 6: Executor Service को साफ़ करें

कभी भी पूल को शटडाउन करना न भूलें; अन्यथा JVM चलती रहेगी, यह सोचते हुए कि अभी भी काम है। एक ग्रेसफुल शटडाउन किसी भी चल रहे टास्क को प्रोसेस समाप्त होने से पहले पूरा होने देता है।

```java
executor.shutdown();
```

यदि आपको टाइमआउट लागू करना है तो आप `awaitTermination` भी कॉल कर सकते हैं, लेकिन अधिकांश कमांड‑लाइन यूटिलिटीज़ के लिए साधारण `shutdown()` पर्याप्त है।

---

## पूर्ण कार्यशील उदाहरण

नीचे पूरा, तैयार‑to‑run प्रोग्राम दिया गया है। इसे `ParallelOcrTutorial.java` नाम की फ़ाइल में कॉपी‑पेस्ट करें, इमेज पाथ्स को समायोजित करें, और सामान्य रूप से `javac` + `java` चलाएँ।

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**अपेक्षित परिणाम:** प्रत्येक इमेज की टेक्स्ट सामग्री कंसोल पर `imagePaths` सूची के समान क्रम में प्रिंट होगी। यदि कोई इमेज प्रोसेस नहीं हो पाती, तो आप एक फ़ेल्योर नोटिस देखेंगे, खाली लाइन की जगह।

---

## सामान्य प्रश्न एवं किनारे के मामलों

### यदि मेरे पास थ्रेड्स से अधिक इमेजेज़ हों तो क्या होगा?

Fixed thread pool स्वचालित रूप से अतिरिक्त टास्क को क्यू करेगा। जैसे ही कोई थ्रेड अपना वर्तमान OCR जॉब समाप्त करता है, वह अगला टास्क ले लेता है। यह क्यूइंग व्यवहार **parallel OCR processing** का सार है—आप अधिकतम थ्रूपुट प्राप्त करते हैं बिना CPU को ओवरलोड किए।

### क्या मैं भाषा बदल सकता हूँ?

बिल्कुल। `engine.getLanguage().setEnglish(true);` को उपयुक्त भाषा फ़्लैग से बदलें, उदाहरण के लिए `setFrench(true)` या `recognize()` से पहले कई सेटर्स कॉल करके कई भाषाएँ सक्षम करें।

### बहुत बड़ी इमेजेज़ को कैसे संभालें?

Large files can consume a lot of memory per thread. If you notice `OutOfMemoryError`, consider scaling the image down before feeding it to the engine, or increase the heap size with `-Xmx`. Another approach is to use a **cached thread pool** (

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}