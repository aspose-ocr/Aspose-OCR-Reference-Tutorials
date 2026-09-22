---
category: general
date: 2026-01-02
description: Aspose OCR का उपयोग करके जावा में छवियों को टेक्स्ट में बदलें। बैच OCR
  प्रोसेसिंग में निपुण बनें, फ़ोल्डर से छवियों को पढ़ें, और फ़ाइलों को एक्सटेंशन के
  आधार पर फ़िल्टर करें।
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: hi
og_description: इमेज को जल्दी से टेक्स्ट में बदलें जावा के साथ। यह ट्यूटोरियल बैच
  OCR प्रोसेसिंग, फ़ोल्डर से इमेज पढ़ने, और एक्सटेंशन के आधार पर फ़ाइलों को फ़िल्टर
  करने को कवर करता है।
og_title: जावा में छवियों को टेक्स्ट में बदलें – पूर्ण बैच OCR गाइड
tags:
- OCR
- Java
- Aspose
title: जावा में छवियों को पाठ में बदलें – बैच OCR प्रोसेसिंग गाइड
url: /hi/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में इमेज को टेक्स्ट में बदलें – बैच OCR प्रोसेसिंग गाइड

क्या आपको कभी **इमेज को टेक्स्ट में बदलने** की जरूरत पड़ी, लेकिन एक साथ दर्जनों फाइलों को कैसे संभालें, समझ नहीं आया? आप अकेले नहीं हैं—डेवलपर्स लगातार PNG, JPG और अन्य स्कैन से डेटा निकालने की कोशिश में लगे रहते हैं। अच्छी खबर? Aspose OCR के साथ आप मिनटों में एक बैच OCR प्रोसेसिंग पाइपलाइन बना सकते हैं, फ़ोल्डर स्ट्रक्चर से इमेज पढ़ सकते हैं, और एक्सटेंशन के आधार पर फ़ाइलों को फ़िल्टर कर सकते हैं ताकि आप केवल आवश्यक फ़ाइलों पर काम करें।

इस ट्यूटोरियल में हम एक स्व-निहित जावा प्रोग्राम बनाएँगे जो एक डायरेक्टरी को ट्रैवर्स करता है, हर `.png` या `.jpg` फ़ाइल को चुनता है, प्रत्येक चित्र को Aspose OCR को असिंक्रोनस रूप से भेजता है, और निकाले गए टेक्स्ट को मूल क्रम में प्रिंट करता है। अंत तक आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं जिसे **इमेज को टेक्स्ट में बदलने** की स्केलेबिलिटी चाहिए।

---

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## आप क्या बनाएँगे

- थ्रेड‑सेफ़ और कुशल `AsposeOCR` इंजन जिसे सभी थ्रेड्स में साझा किया जाएगा।  
- `ParallelRecognizer` जो OCR जॉब्स को समानांतर चलाता है, **बैच OCR प्रोसेसिंग** के लिए परफेक्ट।  
- `java.nio.file.Files` का उपयोग करके **फ़ोल्डर से इमेज पढ़ने** की लॉजिक।  
- PNG फ़ाइलों से **टेक्स्ट निकालने** के लिए सरल फ़िल्टर, जबकि JPG भी संभालता है।  
- रिसोर्स लीक से बचने के लिए इंटरनल थ्रेड पूल का क्लीन शटडाउन।

### आवश्यकताएँ

- Java 17 (या कोई भी हालिया LTS संस्करण)।  
- Maven या Gradle ताकि Aspose OCR लाइब्रेरी को पुल किया जा सके।  
- एक फ़ोल्डर जिसमें आप प्रोसेस करना चाहते हैं PNG/JPG इमेज हों।  
- Java स्ट्रीम्स की बेसिक समझ—कोई फैंसी चीज़ नहीं चाहिए।

> **Pro tip:** अगर आपके पास अभी लाइसेंस नहीं है, तो Aspose एक फ्री टेम्पररी की देता है जिसे आप टेस्टिंग के लिए इस्तेमाल कर सकते हैं।

---

## Step 1 – प्रोजेक्ट सेट‑अप और Aspose OCR जोड़ें

सबसे पहले, एक नया Maven प्रोजेक्ट बनाएं (या Gradle, जैसा आप चाहें)। `pom.xml` में Aspose OCR डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Why this matters:** डिपेंडेंसी को पहले घोषित करने से कंपाइलर को `AsposeOCR`, `ParallelRecognizer` और संबंधित क्लासेज़ दिखते हैं। यह यह भी सुनिश्चित करता है कि सभी मशीनों पर एक ही वर्ज़न इस्तेमाल हो, जो पुनरुत्पादनीय **बैच OCR प्रोसेसिंग** के लिए बहुत ज़रूरी है।

बिल्ड पूरा होने के बाद, अपने IDE को रिफ्रेश करें और आपको `External Libraries` के तहत Aspose पैकेज दिखेंगे।

---

## Step 2 – इमेज को टेक्स्ट में बदलें – OCR इंजन इनिशियलाइज़ करें

पूरे रन के लिए हमें केवल **एक** OCR इंजन इंस्टेंस चाहिए। इसे थ्रेड्स में शेयर करने से मेमोरी बचती है और गति बढ़ती है क्योंकि इंजन भाषा पैक्स सिर्फ एक बार लोड करता है।

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

> **Explanation:** `ParallelRecognizer` इंजन को एक थ्रेड‑पूल में रैप करता है। जब आप कई फ़ाइलें सबमिट करते हैं, तो प्रत्येक को अपना वर्कर थ्रेड मिलता है, जिससे मल्टी‑कोर CPU पर असली समानांतरता मिलती है।

---

## Step 3 – फ़ोल्डर से इमेज पढ़ें – डायरेक्टरी ट्री को वॉक करें

अब हमें **फ़ोल्डर से इमेज पढ़नी** है और हर PNG या JPG को इकट्ठा करना है। `Files.walk` API इसे एक‑लाइनर बना देता है, लेकिन हम एक फ़िल्टर जोड़ेंगे ताकि जरूरत पड़ने पर **PNG से टेक्स्ट निकालें**।

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

> **Why we filter here:** `filter` का उपयोग करके हम **एक्सटेंशन के आधार पर फ़ाइलों को फ़िल्टर** कर सकते हैं, जिससे बाद में अनावश्यक I/O कम हो जाता है। यह कोड को पढ़ने योग्य भी बनाता है—जटिल रेगेक्स की जरूरत नहीं।

---

## Step 4 – बैच OCR प्रोसेसिंग – जॉब्स को असिंक्रोनसली सबमिट करें

फ़ाइलों की लिस्ट तैयार होने पर, हम प्रत्येक पाथ को `ParallelRecognizer` में पुश करते हैं। `recognizeAsync` मेथड एक `Future<OcrResult>` रिटर्न करता है जिसे बाद में रिट्रिव किया जाएगा।

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

> **What’s happening under the hood?** हर कॉल टास्क को recognizer के इंटरनल executor service में एन्क्यू करता है। टास्क समानांतर चलते हैं, इसलिए 100 इमेज वाला फ़ोल्डर एक सिंगल‑थ्रेडेड लूप की तुलना में बहुत कम समय में प्रोसेस हो जाता है।

---

## Step 5 – मूल क्रम में रिज़ल्ट रिट्रिव करें – फ़ाइल सीक्वेंस को बनाए रखें

चूंकि हमने futures को `imagePaths` के समान क्रम में स्टोर किया है, हम लिस्ट पर इटरेट करके `get()` कॉल कर सकते हैं। यह कॉल केवल उस विशेष इमेज के पूरा होने तक ब्लॉक करता है, जिससे अतिरिक्त बुककीपिंग के बिना क्रम बना रहता है।

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

**Sample console output** (संक्षिप्त रूप में):

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

> **Edge case handling:** अगर कोई इमेज एक्सेप्शन थ्रो करती है (करप्ट फ़ाइल, असपोर्टेड फ़ॉर्मेट), तो हम उसे कैच करके बाकी प्रोसेसिंग जारी रखते हैं—जो भरोसेमंद **बैच OCR प्रोसेसिंग** पाइपलाइन के लिए आवश्यक है।

---

## Step 6 – क्लीन‑अप – Recognizer को शटडाउन करें

इंटरनल थ्रेड पूल को कभी न भूलें शटडाउन करना; नहीं तो आपका JVM एग्ज़िट पर हैंग कर सकता है।

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

बस! अब प्रोग्राम किसी भी डायरेक्टरी को वॉक करेगा, PNG/JPG फ़ाइलों को फ़िल्टर करेगा, समानांतर OCR चलाएगा, और रिज़ल्ट प्रिंट करेगा।

---

## पूरा कार्यशील उदाहरण

नीचे पूरी, कॉपी‑एंड‑पेस्ट‑रेडी जावा क्लास दी गई है। `"YOUR_DIRECTORY"` को अपने इमेज फ़ोल्डर के पाथ से बदलें और इसे अपने IDE या कमांड लाइन से चलाएँ।

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

क्लास चलाएँ, कंसोल में निकाले गए स्ट्रिंग्स भरते देखें, और इस बात का जश्न मनाएँ कि आपने बिना किसी ब्लॉकिंग I/O लूप के **इमेज को टेक्स्ट में बदल दिया**।

---

## अक्सर पूछे जाने वाले प्रश्न (FAQs)

**Q: क्या मैं PDFs या TIFFs भी प्रोसेस कर सकता हूँ?**  
A: बिल्कुल। Aspose OCR कई फ़ॉर्मेट सपोर्ट करता है—सिर्फ Step 2 में फ़िल्टर में उपयुक्त फ़ाइल एक्सटेंशन जोड़ दें।

**Q: अगर मुझे स्पेनिश जैसी अलग भाषा चाहिए तो?**  
A: `RecognitionLanguage.ENGLISH` को `RecognitionLanguage.SPANISH` में बदलें। सुनिश्चित करें कि भाषा पैक इंस्टॉल है (Aspose अधिकांश प्रमुख भाषाओं को बॉक्स से बाहर शामिल करता है)।

**Q: मेरे फ़ोल्डर में सब‑फ़ोल्डर हैं—क्या वे स्कैन होंगे?**  
A: हाँ। `Files.walk` पूरी ट्री को रीकर्सिवली ट्रैवर्स करता है, इसलिए हर नेस्टेड PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}