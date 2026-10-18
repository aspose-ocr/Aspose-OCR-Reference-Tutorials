---
category: general
date: 2026-08-28
description: Aspose OCR का उपयोग करके Java में png इमेजेज से टेक्स्ट निकालना सीखें।
  यह ट्यूटोरियल बैच OCR प्रोसेसिंग, फ़ोल्डर से इमेजेज पढ़ना, और extension द्वारा फ़ाइलों
  को फ़िल्टर करने को कवर करता है।
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Aspose OCR का उपयोग करके Java में png इमेजेज से टेक्स्ट निकालना सीखें।
  यह ट्यूटोरियल बैच OCR प्रोसेसिंग, फ़ोल्डर से इमेजेज पढ़ना, और extension द्वारा फ़ाइलों
  को फ़िल्टर करने को कवर करता है।
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Java में png से टेक्स्ट निकालने का तरीका – बैच OCR गाइड
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Java में png से टेक्स्ट निकालने का तरीका – बैच OCR गाइड
url: /hi/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में PNG से टेक्स्ट निकालने का तरीका – बैच OCR गाइड

यदि आपको कभी **PNG से टेक्स्ट निकालने** की आवश्यकता पड़ी है लेकिन आप यह नहीं जानते थे कि इस ऑपरेशन को कई चित्रों तक कैसे स्केल करें, तो आप सही जगह पर हैं। कई डेवलपर्स एकल‑इमेज OCR कॉल से शुरू करते हैं और जल्दी ही प्रदर्शन की सीमाओं का सामना करते हैं जब फ़ोल्डर कई या सैकड़ों फ़ाइलों तक बढ़ जाता है। Aspose OCR for Java के साथ आप एक मजबूत बैच OCR पाइपलाइन बना सकते हैं जो डायरेक्टरी को चलाती है, केवल उन इमेज प्रकारों को फ़िल्टर करती है जिनकी आपको ज़रूरत है, समानांतर में पहचान चलाती है, और परिणामों को स्रोत फ़ाइलों के समान क्रम में लौटाती है। इस गाइड के अंत तक आपके पास एक तैयार‑ड्रॉप Java स्निपेट होगा जो **batch OCR processing** को विश्वसनीय और कुशलता से संभालता है।

![इमेज को टेक्स्ट में बदलने का उदाहरण](https://example.com/convert-images-to-text.png "जावा कंसोल आउटपुट का स्क्रीनशॉट जो PNG फ़ाइलों से परिवर्तित टेक्स्ट दिखाता है")

## त्वरित उत्तर
- **OCR को संभालने वाली लाइब्रेरी कौन सी है?** Aspose OCR for Java.
- **क्या मैं PNG और JPG को साथ में प्रोसेस कर सकता हूँ?** हाँ – नमूना दोनों एक्सटेंशन को फ़िल्टर करता है।
- **क्या OCR इंजन थ्रेड‑सेफ़ है?** एकल साझा `AsposeOCR` इंस्टेंस समवर्ती उपयोग के लिए सुरक्षित है।
- **क्या परीक्षण के लिए मुझे लाइसेंस चाहिए?** Aspose से एक मुफ्त अस्थायी कुंजी उपलब्ध है।
- **क्या सब‑फ़ोल्डर स्वचालित रूप से स्कैन किए जाएंगे?** `Files.walk` पूरे ट्री को पुनरावर्ती रूप से पार करता है।

## extract text from png क्या है?
`extract text from png` वह प्रक्रिया है जिसमें पोर्टेबल नेटवर्क ग्राफ़िक्स (PNG) फ़ाइलों पर ऑप्टिकल कैरेक्टर रिकग्निशन (OCR) लागू की जाती है ताकि दृश्यमान अक्षर खोजने योग्य, संपादन योग्य स्ट्रिंग्स बन जाएँ। Aspose OCR का इंजन पिक्सेल डेटा पढ़ता है, ग्लिफ़ आकार पहचानता है, और एक ही मेथड कॉल में यूनिकोड टेक्स्ट लौटाता है।

## Aspose OCR for Java का उपयोग क्यों करें?
Aspose OCR **30+ भाषाओं** का समर्थन करता है, मानक 8‑कोर सर्वर पर **प्रति मिनट 500 इमेज** तक प्रोसेस करता है, और **200 MB** तक की फ़ाइलों को पूरी इमेज को मेमोरी में लोड किए बिना संभाल सकता है। ये मापी गई क्षमताएँ दर्शाती हैं कि आप कम लागत वाले हार्डवेयर पर बड़े‑पैमाने के बैच जॉब्स को विश्वसनीय रूप से चला सकते हैं बिना मेमोरी सीमाओं के टकराए।

## पूर्वापेक्षाएँ
- Java 17 (या कोई भी हालिया LTS संस्करण)।
- निर्भरता प्रबंधन के लिए Maven या Gradle।
- एक डायरेक्टरी जिसमें आप प्रोसेस करना चाहते हैं PNG/JPG इमेज हों।
- Java स्ट्रीम्स और `java.nio.file` पैकेज की बुनियादी परिचितता।
- (वैकल्पिक) मूल्यांकन के लिए Aspose OCR अस्थायी लाइसेंस कुंजी।

> **Pro tip:** मुफ्त अस्थायी कुंजी 30 दिनों के बाद समाप्त हो जाती है, लेकिन यह परीक्षण के लिए आपको पूर्ण API एक्सेस देती है।

## प्रोजेक्ट सेट अप कैसे करें और Aspose OCR जोड़ें
सबसे पहले, एक Maven (या Gradle) प्रोजेक्ट बनाएं और अपने `pom.xml` में Aspose OCR डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Why this matters:** डिपेंडेंसी को पहले घोषित करने से सुनिश्चित होता है कि कंपाइलर `AsposeOCR`, `ParallelRecognizer`, और संबंधित क्लासेज़ को देख सके। यह यह भी गारंटी देता है कि सभी मशीनों पर एक ही संस्करण उपयोग किया जाए, जो पुनरुत्पादनीय **batch OCR processing** के लिए महत्वपूर्ण है।

बिल्ड पूरा होने के बाद अपने IDE को रिफ्रेश करें; अब आपको **External Libraries** के तहत Aspose पैकेज दिखने चाहिए।

## OCR इंजन को इनिशियलाइज़ कैसे करें – एक ही इंस्टेंस साझा करें
`AsposeOCR` Aspose OCR लाइब्रेरी द्वारा प्रदान किया गया मुख्य OCR इंजन क्लास है। हमें पूरे रन के लिए केवल **एक** OCR इंजन इंस्टेंस की आवश्यकता है। इसे थ्रेड्स के बीच साझा करने से मेमोरी बचती है और गति बढ़ती है क्योंकि इंजन भाषा पैक्स केवल एक बार लोड करता है।

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` थ्रेड‑सेफ़ है, इसलिए आप इसे सुरक्षित रूप से `ParallelRecognizer` को दे सकते हैं जो वर्कर थ्रेड्स का पूल प्रबंधित करेगा।

> **Explanation:** `ParallelRecognizer` इंजन को एक थ्रेड‑पूल में रैप करता है। जब आप कई फ़ाइलें सबमिट करते हैं, तो प्रत्येक को अपना वर्कर थ्रेड मिलता है, जिससे मल्टी‑कोर CPU पर वास्तविक समानांतरता सक्षम होती है।

## फ़ोल्डर से इमेज पढ़ें – डायरेक्टरी ट्री को वॉक करें
`Files.walk` एक Java NIO मेथड है जो पुनरावर्ती रूप से फ़ाइल ट्री को ट्रैवर्स करता है और `Path` ऑब्जेक्ट्स की एक स्ट्रीम लौटाता है। अब हमें **फ़ोल्डर से इमेज पढ़ने** की आवश्यकता है और हर PNG या JPG को इकट्ठा करना है। `Files.walk` API इसे एक‑लाइनर बनाता है, लेकिन हम आवश्यकता पड़ने पर **extract text from png** के लिए एक फ़िल्टर जोड़ेंगे।

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Why we filter here:** `filter` का उपयोग करके हम प्रारंभ में ही **फ़ाइलों को एक्सटेंशन द्वारा फ़िल्टर** कर सकते हैं, जिससे बाद में अनावश्यक I/O कम हो जाता है। यह कोड को पढ़ने योग्य भी रखता है—जटिल regex की आवश्यकता नहीं।

## OCR जॉब्स को असिंक्रोनस रूप से कैसे सबमिट करें
`recognizeAsync` एक इमेज को OCR इंजन को असिंक्रोनस प्रोसेसिंग के लिए सबमिट करता है और एक `Future<OcrResult>` लौटाता है जो लंबित परिणाम को दर्शाता है। फ़ाइलों की सूची तैयार होने पर, हम प्रत्येक पाथ को `ParallelRecognizer` में पुश करते हैं। `recognizeAsync` मेथड एक `Future<OcrResult>` लौटाता है जिसे हम बाद में पुनः प्राप्त करने के लिए स्टोर करते हैं।

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **What’s happening under the hood?** प्रत्येक कॉल को recognizer की आंतरिक executor सर्विस में एक टास्क के रूप में एन्क्यू किया जाता है। टास्क समानांतर में चलते हैं, इसलिए 100 इमेज वाले फ़ोल्डर को एक सिंगल‑थ्रेडेड लूप की तुलना में बहुत कम समय में प्रोसेस किया जा सकता है।

## फ़ाइल क्रम को बनाए रखते हुए परिणाम कैसे प्राप्त करें
`Future<OcrResult>` असिंक्रोनस OCR टास्क का परिणाम रखता है और पहचाने गए टेक्स्ट को प्राप्त करने के लिए `get()` मेथड प्रदान करता है। क्योंकि हमने फ्यूचर्स को `imagePaths` के समान क्रम में स्टोर किया है, हम सरलता से सूची पर इटरेट कर `get()` कॉल कर सकते हैं। यह कॉल केवल उस विशेष इमेज के पूरा होने तक ब्लॉक करता है, जिससे अतिरिक्त बुककीपिंग के बिना क्रम बना रहता है।

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Sample console output** (संक्षिप्त रूप में):
```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Edge case handling:** यदि कोई विशेष इमेज एक्सेप्शन फेंकती है (खराब फ़ाइल, असमर्थित फ़ॉर्मेट), तो हम इसे पकड़ते हैं और बाकी को प्रोसेस करना जारी रखते हैं—यह विश्वसनीय **batch OCR processing** पाइपलाइन के लिए एक आवश्यक आदत है।

## रिसोर्सेज को साफ़ कैसे करें – recognizer को शटडाउन करें
`ParallelRecognizer.shutdown()` आंतरिक थ्रेड पूल को रोकता है, यह सुनिश्चित करता है कि एप्लिकेशन समाप्त होने से पहले सभी OCR टास्क पूर्ण हो जाएँ। आंतरिक थ्रेड पूल को शटडाउन करना कभी न भूलें; अन्यथा आपका JVM एग्ज़िट पर फँस सकता है।

```java
recognizer.shutdown();
```

बस इतना ही! अब प्रोग्राम किसी भी डायरेक्टरी को वॉक करता है, PNG/JPG फ़ाइलों को फ़िल्टर करता है, OCR को समानांतर चलाता है, और मूल क्रम में परिणाम प्रिंट करता है।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑एंड‑पेस्ट)
नीचे पूर्ण, तैयार‑चलाने योग्य Java क्लास दिया गया है। `"YOUR_DIRECTORY"` को अपनी इमेज फ़ोल्डर के पाथ से बदलें और इसे अपने IDE या कमांड लाइन से चलाएँ।

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

क्लास चलाएँ, कंसोल को निकाले गए स्ट्रिंग्स से भरते देखें, और इस बात का जश्न मनाएँ कि आपने बिना I/O पर ब्लॉक करने वाला कोई लूप लिखे **converted images to text** किया।

---

## अक्सर पूछे जाने वाले प्रश्न (FAQs)

**Q: क्या मैं PDFs या TIFFs को भी प्रोसेस कर सकता हूँ?**  
A: बिल्कुल। Aspose OCR 30+ फ़ॉर्मेट्स—जिसमें PDF, TIFF, BMP, और GIF शामिल हैं—को सपोर्ट करता है, इसलिए बस डायरेक्टरी‑वॉक स्टेप में फ़िल्टर में इच्छित एक्सटेंशन जोड़ दें।

**Q: यदि मुझे अंग्रेज़ी के अलावा कोई अन्य भाषा चाहिए, जैसे स्पेनिश?**  
A: `RecognitionLanguage.ENGLISH` को `RecognitionLanguage.SPANISH` (या किसी भी समर्थित भाषा) में बदलें। भाषा पैक्स लाइब्रेरी के साथ बंडल होते हैं, इसलिए अतिरिक्त डाउनलोड की आवश्यकता नहीं है।

**Q: मेरे फ़ोल्डर में सब‑फ़ोल्डर हैं—क्या उन्हें स्कैन किया जाएगा?**  
A: हाँ। `Files.walk` पूरे ट्री को पुनरावर्ती रूप से ट्रैवर्स करता है, इसलिए हर नेस्टेड PNG/J

**Q: मैं 200 MB से बड़ी अत्यधिक बड़ी इमेजेज़ को कैसे संभालूँ?**  
A: `ocrEngine.setUseStreaming(true)` कॉल करके स्ट्रीमिंग मोड सक्षम करें। यह इंजन को इमेज को चंक्स में पढ़ने को कहता है, जिससे पीक मेमोरी उपयोग में काफी कमी आती है।

**Q: क्या मैं समवर्ती OCR थ्रेड्स की संख्या को सीमित कर सकता हूँ?**  
A: हाँ। `ParallelRecognizer` बनाते समय, इच्छित अधिकतम थ्रेड काउंट को दूसरे आर्ग्यूमेंट के रूप में पास करें (उदा., `new ParallelRecognizer(ocrEngine, 4)`).

**अंतिम अपडेट:** 2026-08-28  
**परीक्षण किया गया:** Aspose OCR for Java 24.10  
**लेखक:** Aspose  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```
```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```
```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```
```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```
```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```
```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```
```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```
```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## संबंधित ट्यूटोरियल

- [जावा बैच OCR प्रोसेसिंग गाइड में इमेज को टेक्स्ट में बदलें](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [जावा में इमेज से टेक्स्ट पढ़ें – पूर्ण Aspose OCR गाइड](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Aspose.OCR का उपयोग करके इमेज से टेक्स्ट निकालें – अनुमत अक्षर](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}