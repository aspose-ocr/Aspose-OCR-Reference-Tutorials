---
category: general
date: 2026-02-17
description: जानेँ कि कैसे फिक्स्ड थ्रेड पूल जावा का उपयोग करके PNG इमेजेज़ से टेक्स्ट
  निकाला जाए, पैरलल OCR प्रोसेसिंग के साथ, और एक्ज़ीक्यूटर सर्विस को सही तरीके से
  बंद किया जाए।
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: hi
og_description: जाने कैसे एक फिक्स्ड थ्रेड पूल जावा समानांतर में PNG इमेजेज़ से टेक्स्ट
  निकाल सकता है, स्कैन किए गए पृष्ठों का टेक्स्ट बदल सकता है, और एक्ज़ीक्यूटर सर्विस
  को सुरक्षित रूप से बंद कर सकता है।
og_title: स्थिर थ्रेड पूल जावा – PNG के लिए समानांतर OCR
tags:
- java
- ocr
- multithreading
- aspose
title: स्थिर थ्रेड पूल जावा – PNG के लिए समानांतर OCR
url: /hi/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# फ़िक्स्ड थ्रेड पूल जावा – PNG के लिए समानांतर OCR

क्या आपने कभी सोचा है कि कई PNG फ़ाइलों पर OCR को **fixed thread pool java** का उपयोग करके कैसे तेज़ किया जाए? इस ट्यूटोरियल में हम **extract text from PNG** इमेजेज़ को समानांतर रूप से प्रोसेस करेंगे, **convert scanned pages text** को संपादन योग्य स्ट्रिंग्स में बदलेंगे, और काम पूरा होने पर **shut down executor service** को सुरक्षित रूप से बंद करेंगे।

यदि आप कभी एक सिंगल‑थ्रेडेड लूप को देखते रहे हैं जो मिनटों तक चलता रहता है, तो आप प्रत्येक पेज के समाप्त होने का इंतज़ार करने की निराशा को समझते हैं, इससे पहले कि अगला शुरू भी हो। अच्छी खबर? कुछ ही लाइनों के जावा और Aspose OCR के साथ आप अपने सभी CPU कोर की शक्ति को उजागर कर सकते हैं, स्कैन किए गए पेज़ को खोज योग्य टेक्स्ट में बदल सकते हैं, और अपना एप्लिकेशन रिस्पॉन्सिव रख सकते हैं।  

नीचे आपको एक पूर्ण, तैयार‑चलाने योग्य उदाहरण मिलेगा, साथ ही यह समझाने के लिए कि प्रत्येक भाग क्यों महत्वपूर्ण है, सामान्य गड़बड़ियों और टिप्स के बारे में जो आप किसी भी OCR लाइब्रेरी पर लागू कर सकते हैं।

---

## आपको क्या चाहिए

- **Java 17** (या कोई भी हालिया JDK) – कोड आधुनिक `var` सिंटैक्स का थोड़ा उपयोग करता है, लेकिन पुराने संस्करणों पर भी काम करता है।  
- **Aspose.OCR for Java** लाइब्रेरी – आप इसे Maven Central से प्राप्त कर सकते हैं या Aspose से ट्रायल डाउनलोड कर सकते हैं।  
- उन **PNG** फ़ाइलों का सेट जिन्हें आप प्रोसेस करना चाहते हैं – जैसे स्कैन किए हुए रसीदें, किताब के पेज़, या स्क्रीनशॉट।  
- जावा कन्करेंसी की बुनियादी जानकारी – आवश्यक नहीं, लेकिन मददगार है।

बस इतना ही। कोई बाहरी सर्विस नहीं, कोई Docker नहीं, सिर्फ़ साधारण जावा और थोड़ा मल्टीथ्रेडिंग जादू।

## चरण 1: Aspose OCR निर्भरता और लाइसेंस जोड़ें (वैकल्पिक)

सबसे पहले, सुनिश्चित करें कि Aspose OCR JAR आपके क्लासपाथ पर है। यदि आप Maven उपयोग करते हैं, तो जोड़ें:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

यदि आपके पास लाइसेंस नहीं है, तो लाइब्रेरी इवैल्यूएशन मोड में चलेगी; कोड वही काम करेगा। लाइसेंस लोड करने के लिए (प्रोडक्शन के लिए अनुशंसित), `Aspose.OCR.lic` को अपने resources फ़ोल्डर में रखें और उपयोग करें:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **प्रो टिप:** लाइसेंस फ़ाइल को संस्करण नियंत्रण के बाहर रखें ताकि आकस्मिक एक्सपोज़र से बचा जा सके।

## चरण 2: एक थ्रेड‑सेफ़ `OcrEngine` इंस्टेंस बनाएं

Aspose OCR का `OcrEngine` थ्रेड‑सेफ़ है जब तक आप उसी इंस्टेंस को टास्क्स के बीच पुनः उपयोग करते हैं। इसे एक बार बनाना मेमोरी बचाता है और हर इमेज के लिए इंजन को पुनः‑इनिशियलाइज़ करने के ओवरहेड से बचाता है।

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

क्यों पुनः उपयोग? इंजन को एक भारी‑वज़न वाले कार्यकर्ता के रूप में सोचें जो भाषा मॉडल्स को मेमोरी में लोड करता है। हर इमेज के लिए नया इंजन बनाना ऐसे होगा जैसे हर छोटे काम के लिए नया विशेषज्ञ नियुक्त करना – महँगा और अनावश्यक।

## चरण 3: एक Fixed Thread Pool Java सेट अप करें

अब आता है शो का स्टार: एक **fixed thread pool java**। हम इसे लॉजिकल प्रोसेसर की संख्या के अनुसार आकार देंगे ताकि हर कोर को काम मिले बिना ओवर‑सब्सक्राइब किए।

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

*फ़िक्स्ड* पूल (कैश्ड के बजाय) उपयोग करने से आपको संसाधनों का पूर्वानुमेय उपयोग मिलता है और जब सैकड़ों इमेज एक साथ आते हैं तो “out‑of‑memory” स्पाइक्स से बचाव होता है।

## चरण 4: उन PNG फ़ाइलों की सूची बनाएं जिन्हें आप प्रोसेस करना चाहते हैं (Extract Text from PNG)

उन इमेजों के पाथ एकत्र करें जिन्हें आप OCR करना चाहते हैं। वास्तविक प्रोजेक्ट में आप डायरेक्टरी स्कैन कर सकते हैं या डेटाबेस से पढ़ सकते हैं; यहाँ हम कुछ उदाहरण हार्ड‑कोड करेंगे।

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **नोट:** फ़ाइल एक्सटेंशन **png** महत्वपूर्ण है क्योंकि Aspose OCR स्वचालित रूप से फ़ॉर्मेट पहचान लेता है, लेकिन आप JPEG या TIFF भी फीड कर सकते हैं।

## चरण 5: OCR टास्क सबमिट करें – Parallel OCR Processing

हर इमेज एक callable बन जाती है जो पहचानित टेक्स्ट लौटाती है। चूँकि `OcrEngine` साझा किया गया है, हमें केवल फ़ाइल पाथ टास्क में पास करना है।

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

क्यों `Future` में रैप करें? यह हमें सभी जॉब्स तुरंत फायर करने देता है, फिर बाद में परिणामों को उसी क्रम में एकत्र करने की सुविधा देता है जिसमें वे सबमिट किए गए थे – जब **convert scanned pages text** को फिर से डॉक्यूमेंट में डालना हो तो पेज क्रम बनाए रखने के लिए यह परफ़ेक्ट है।

## चरण 6: परिणाम प्राप्त करें और प्रदर्शित करें (Convert Scanned Pages Text)

अब हम प्रत्येक `Future` के समाप्त होने का इंतज़ार करते हैं और आउटपुट प्रिंट करते हैं। `get()` कॉल केवल उस विशिष्ट टास्क के पूरा होने तक ब्लॉक करता है, पूरे पूल के नहीं।

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

सामान्य कंसोल आउटपुट इस प्रकार दिखता है:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

यदि आप परिणाम फ़ाइलों में लिखना पसंद करते हैं, तो `System.out.println` को `Files.writeString` कॉल से बदल दें।

## चरण 7: Executor Service को साफ़-सुथरे ढंग से बंद करें

जब सभी टास्क समाप्त हो जाएँ, तो **shut down executor service** करना अत्यंत महत्वपूर्ण है; अन्यथा आपका JVM नॉन‑डेमन थ्रेड्स को जीवित रखेगा, जिससे ग्रेसफ़ुल एग्ज़िट नहीं हो पाएगा।

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

`awaitTermination` पैटर्न पूल को मौजूदा कार्य समाप्त करने का मौका देता है इससे पहले कि हम ज़बरदस्ती बंद करें। इस चरण को नजरअंदाज़ करना लंबे‑चलाने वाले एप्लिकेशन्स में मेमोरी लीक्स का आम स्रोत है।

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ मिलाकर, यहाँ पूरा प्रोग्राम है जिसे आप `ParallelBatchDemo.java` में कॉपी‑पेस्ट करके चला सकते हैं:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}