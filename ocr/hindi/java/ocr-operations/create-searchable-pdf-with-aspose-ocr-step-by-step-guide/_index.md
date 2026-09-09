---
category: general
date: 2026-01-02
description: Aspose OCR का उपयोग करके स्कैन की गई इमेज PDF से सर्चेबल PDF बनाएं। OCR
  भाषा सेट करना, टेक्स्ट लेयर PDF एम्बेड करना और हाई कॉम्प्रेशन PDF विकल्प लागू करना
  सीखें।
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: hi
og_description: तेज़ी से खोज योग्य PDF बनाएं। यह गाइड दिखाता है कि स्कैन की गई इमेज
  PDF को कैसे बदलें, टेक्स्ट लेयर एम्बेड करें, OCR भाषा सेट करें और उच्च संपीड़न वाला
  PDF सक्षम करें।
og_title: Aspose OCR के साथ खोज योग्य PDF बनाएं – पूर्ण गाइड
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Aspose OCR के साथ खोज योग्य PDF बनाएं – चरण‑दर‑चरण गाइड
url: /hi/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# खोज योग्य PDF बनाएं – पूर्ण प्रोग्रामिंग ट्यूटोरियल

क्या आपको कभी स्कैन की गई छवियों से **searchable PDF** फ़ाइलें बनानी पड़ी हों लेकिन शुरू करने के बारे में अनिश्चित रहे हों? आप अकेले नहीं हैं। कई दस्तावेज‑भारी कार्यप्रवाहों में, केवल छवि‑PDF खोज और अनुक्रमण के लिए एक बंद रास्ता है।  

अच्छी खबर यह है कि Aspose OCR के साथ आप कुछ ही Java लाइनों में **scanned image PDF** को पूरी तरह खोज योग्य दस्तावेज़ में **convert** कर सकते हैं। यह ट्यूटोरियल आपको हर चरण से ले जाता है—OCR इंजन को इनिशियलाइज़ करना, हाई कॉम्प्रेशन PDF सेटिंग्स कॉन्फ़िगर करना, हिडन टेक्स्ट लेयर एम्बेड करना, और सही OCR भाषा चुनना।

इस गाइड के अंत तक आपके पास एक रन करने योग्य प्रोग्राम होगा जो एक खोज योग्य PDF उत्पन्न करता है, एक फ़ाइल जिसे आप बिना किसी समस्या के किसी भी सर्च इंजन या डॉक्यूमेंट मैनेजमेंट सिस्टम में डाल सकते हैं।

---

## खोज योग्य PDF बनाएं – अवलोकन

कोड में कूदने से पहले, चलिए स्पष्ट करते हैं कि “searchable PDF बनाना” वास्तव में क्या मतलब रखता है। एक खोज योग्य PDF दो समानांतर लेयर्स रखता है:

1. **Visual layer** – मूल स्कैन की गई छवि (या रेंडर किया गया पेज)।  
2. **Text layer** – अदृश्य लेकिन मशीन‑रीडेबल कैरेक्टर्स जो OCR द्वारा निकाले जाते हैं।

जब आप ऐसा PDF Adobe Reader में खोलते हैं और टेक्स्ट सेलेक्ट करते हैं, तो आप वास्तव में छवि नहीं, बल्कि हिडन टेक्स्ट लेयर के साथ इंटरैक्ट कर रहे होते हैं। यह ड्यूल‑लेयर अप्रोच ही **embed text layer PDF** फ़ंक्शनैलिटी को सक्षम करता है।

---

## Aspose OCR का उपयोग करके स्कैन्ड इमेज PDF को Convert करें

पहले आपको एक स्कैन्ड इमेज (PNG, JPEG, TIFF) चाहिए जिसे आप PDF में बदलना चाहते हैं। Aspose OCR उस इमेज को पढ़ सकता है, OCR चलाता है, और परिणाम को PDF राइटर को दे देता है।

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**यह क्यों काम करता है:**  
- `setCreateSearchablePdf(true)` Aspose को हिडन टेक्स्ट लेयर जनरेट करने के लिए बताता है, जिससे **embed text layer pdf** की आवश्यकता पूरी होती है।  
- `setCompressionLevel(9)` फ़ाइल को **high compression pdf** रेंज में धकेलता है, अंतिम आकार को घटाते हुए OCR की सटीकता को नहीं खोता।  
- `RecognitionLanguage.ENGLISH` आर्ग्यूमेंट दिखाता है कि **set OCR language** कैसे सेट करें; आप इसे फ्रेंच, जर्मन आदि में बदल सकते हैं, आपके स्रोत सामग्री के आधार पर।

---

## हाई कॉम्प्रेशन PDF सेटिंग्स

बड़े स्कैन्ड PDF जल्दी ही सैकड़ों मेगाबाइट तक बढ़ सकते हैं। Aspose एक सरल कॉम्प्रेशन API प्रदान करता है जो PDF स्तर पर काम करता है। `setCompressionLevel` मेथड 0 (कोई कॉम्प्रेशन नहीं) से 9 (अधिकतम कॉम्प्रेशन) तक के मान स्वीकार करता है।  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

कुछ टिप्स:

- **Lossless इमेज फॉर्मेट** (PNG) का उपयोग करें टेक्स्ट‑हेवी स्कैन के लिए; फ़ोटो के लिए JPEG बेहतर है।  
- यदि आप कस्टम फ़ॉन्ट एम्बेड करते हैं तो **फ़ॉन्ट सबसेटिंग** एनेबल करें—Aspose इसे स्वचालित रूप से searchable PDF बनाते समय करता है।  
- प्रत्येक बदलाव के बाद **आउटपुट साइज** टेस्ट करें; कभी‑कभी लेवल‑8 कॉम्प्रेशन आपको लेवल‑9 की तुलना में 10 % आकार घटाव देता है, गुणवत्ता में नगण्य अंतर के साथ।

---

## खोज योग्यता के लिए Text Layer PDF एम्बेड करें

यदि आप `setCreateSearchablePdf(true)` कॉल को छोड़ देते हैं, तो परिणामी फ़ाइल ठीक दिखेगी लेकिन आप उसकी सामग्री को सर्च नहीं कर पाएंगे। हिडन टेक्स्ट लेयर प्रत्येक पहचाने गए कैरेक्टर को पेज पर उसकी लोकेशन से मैप करके बनाई जाती है।  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**ध्यान रखने योग्य बातें:**  

- **Mixed‑language दस्तावेज़** – आपको OCR दो बार चलाना पड़ सकता है, प्रत्येक भाषा के लिए एक बार, और फिर टेक्स्ट लेयर्स को मर्ज करना होगा।  
- **जटिल लेआउट** (टेबल, मल्टी‑कॉलम) – Aspose एक अच्छा काम करता है, लेकिन आउटपुट को ऐसे PDF व्यूअर से डबल‑चेक करें जो हिडन टेक्स्ट दिखाता हो (जैसे Adobe Acrobat का “Edit PDF” मोड)।

---

## सटीक पहचान के लिए OCR भाषा सेट करें

OCR इंजन की सटीकता इस बात पर निर्भर करती है कि आप उसे कौन सी भाषा की उम्मीद कराते हैं। Aspose कई बिल्ट‑इन भाषाओं के साथ आता है, और आप कस्टम लैंग्वेज पैक्स भी जोड़ सकते हैं।

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**भाषा कब बदलें:**  

- दस्तावेज़ में **non‑Latin स्क्रिप्ट** (Cyrillic, Arabic) हों – उपयुक्त `RecognitionLanguage` में स्विच करें।  
- मिश्रित भाषा वाले पेज – आप `recognizeImageAndSave` को दो बार कॉल कर सकते हैं, हर बार अलग भाषा के साथ, और फिर PDFs को मर्ज कर सकते हैं।

---

## पूरा उदाहरण चलाएँ

नीचे पूरा, तैयार‑से‑चलाने वाला प्रोग्राम दिया गया है। प्लेसहोल्डर पाथ्स को वास्तविक फ़ाइल लोकेशन से बदलें, सुनिश्चित करें कि Aspose OCR JAR आपके क्लासपाथ में है, और एक्सीक्यूट करें।

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**अपेक्षित आउटपुट:** जब आप प्रोग्राम चलाते हैं, तो कंसोल प्रिंट करता है:

```
Searchable PDF created.
```

`searchable.pdf` को किसी भी PDF व्यूअर में खोलें, टेक्स्ट सेलेक्ट करने की कोशिश करें, और आप हिडन लेयर को क्रिया में देखेंगे। आपने सफलतापूर्वक **searchable pdf** को स्कैन्ड इमेज से **create** कर लिया है।

---

![create searchable pdf example](image-placeholder.png "create searchable pdf example")

*ऊपर का स्क्रीनशॉट (प्लेसहोल्डर) आमतौर पर PDF व्यूअर को दिखाता है जिसमें स्कैन्ड पेज पर चयन योग्य टेक्स्ट होता है।*

---

## निष्कर्ष

हमने Aspose OCR का उपयोग करके **searchable PDF** फ़ाइलें बनाने के लिए आवश्यक सभी चीज़ें कवर कर ली हैं:

- OCR इंजन को इनिशियलाइज़ करें।  
- `recognizeImageAndSave` में PNG/JPEG फीड करके **Convert scanned image PDF** करें।  
- `setCreateSearchablePdf(true)` का उपयोग करके **embed text layer PDF** बनाएं।  
- हल्का रखने के लिए **high compression PDF** हेतु `setCompressionLevel(9)` लागू करें।  
- अधिकतम सटीकता के लिए सही `RecognitionLanguage` चुनें और **set OCR language** सेट करें।

अब आप बैच प्रोसेसिंग, विभिन्न भाषाओं, या कई स्कैन्ड पेजों को एक ही खोज योग्य PDF में संयोजित करने के साथ प्रयोग कर सकते हैं। वही पैटर्न स्पेनिश या जापानी जैसी अन्य भाषाओं के लिए भी काम करता है—बस `RecognitionLanguage` एनीम को बदल दें।

यदि आपको कोई समस्या आती है तो टिप्पणी छोड़ें, और कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}