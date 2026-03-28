---
category: general
date: 2026-03-28
description: Aspose OCR का उपयोग करके जावा में छवि पर OCR चलाएँ, छवि को टेक्स्ट में
  बदलें, PNG से थाई टेक्स्ट को तेज़ी और भरोसेमंद तरीके से निकालें।
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: hi
og_description: जावा और Aspose OCR का उपयोग करके छवि पर OCR चलाएँ। जानें कि छवि को
  टेक्स्ट में कैसे बदलें, PNG से थाई टेक्स्ट कैसे निकालें, और सामान्य समस्याओं को
  कैसे संभालें।
og_title: जावा के साथ इमेज पर OCR चलाएँ – थाई टेक्स्ट को तेज़ी से निकालें
tags:
- OCR
- Java
- Aspose
- Image Processing
title: जावा के साथ छवि पर OCR चलाएँ – PNG से थाई टेक्स्ट निकालें
url: /hi/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा के साथ इमेज पर OCR चलाएँ – पूर्ण‑विशेष ट्यूटोरियल

क्या आपने कभी सोचा है कि **run OCR on image** फ़ाइलों को सीधे जावा कोड से कैसे चलाया जाए? शायद आपके पास थाई रसीदों, स्कैन किए गए दस्तावेज़ों या स्क्रीनशॉट्स का संग्रह है और आपको टेक्स्ट चाहिए बिना मैन्युअल टाइप किए। यह एक आम समस्या है, विशेषकर जब स्रोत PNG हो और भाषा लैटिन नहीं हो।  

इस गाइड में हम आपको दिखाएंगे कि **run OCR on image** को Aspose OCR लाइब्रेरी का उपयोग करके कैसे किया जाए, तस्वीर को साधारण टेक्स्ट में बदला जाए, और थाई अक्षरों को भरोसेमंद तरीके से निकाला जाए। अंत तक आप **convert image to text**, **extract text from PNG**, और यहाँ तक कि **recognize Thai text** कुछ ही लाइनों के कोड से कर पाएँगे।

## इस ट्यूटोरियल में क्या कवर किया गया है

* Maven/Gradle प्रोजेक्ट में Aspose OCR डिपेंडेंसी सेट करना।  
* `OcrEngine` को इनिशियलाइज़ करना और थाई भाषा के लिए कॉन्फ़िगर करना।  
* PNG फ़ाइल पर OCR चलाना और संभावित त्रुटियों को संभालना।  
* परिणाम को कंसोल पर प्रिंट करना और आउटपुट की पुष्टि करना।  

Aspose का कोई पूर्व अनुभव आवश्यक नहीं—बस एक बेसिक जावा IDE और वह इमेज फ़ाइल चाहिए जिसे आप प्रोसेस करना चाहते हैं।

## आवश्यकताएँ

* Java 8 या नया स्थापित हो (लाइब्रेरी Java 11+ के साथ भी काम करती है)।  
* एक बिल्ड टूल – Maven या Gradle (हम Maven स्निपेट दिखाएंगे)।  
* Aspose OCR लाइसेंस (फ्री ट्रायल टेस्टिंग के लिए काम करता है, लेकिन लाइसेंस से इवैल्युएशन लिमिट हट जाती है)।  
* एक PNG जिसमें थाई टेक्स्ट हो, उदाहरण के लिए `input.png` को अपने प्रोजेक्ट की resources फ़ोल्डर में रखें।

---

## चरण 1: अपने प्रोजेक्ट में Aspose OCR जोड़ें

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Pro tip:** लाइब्रेरी संस्करण को आधिकारिक Aspose रिलीज़ नोट्स के साथ सिंक रखें; नए संस्करण भाषा पैक्स और परफ़ॉर्मेंस सुधार जोड़ते हैं।

डिपेंडेंसी रेज़ॉल्व हो जाने के बाद, आपका IDE आवश्यक क्लासेज़ को ऑटो‑इम्पोर्ट कर देगा।

## चरण 2: OCR इंजन को इनिशियलाइज़ करें

इंजन प्रक्रिया का दिल है – इसे “ब्रेन” समझें जो पिक्सेल पैटर्न का विश्लेषण करता है। हम इसे यह भी बताएँगे कि हमें केवल थाई अक्षर चाहिए।

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

भाषा को स्पष्ट रूप से सेट क्यों करें? क्योंकि `"th"` निर्दिष्ट करने से कैरेक्टर सेट सीमित हो जाता है, जिससे पहचान तेज़ होती है और समान दिखने वाले glyphs की गलत पढ़ाई कम होती है।

## चरण 3: PNG फ़ाइल पर OCR चलाएँ

अब हम इंजन को वह इमेज देंगे जिसे हम डिकोड करना चाहते हैं। `recognizeImage` मेथड एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें निकाला गया स्ट्रिंग और कॉन्फिडेंस स्कोर होते हैं।

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

यदि फ़ाइल नहीं मिलती, तो Aspose `FileNotFoundException` फेंकता है। प्रोडक्शन कोड में इसे `try‑catch` ब्लॉक में रैप करना अच्छा रहेगा, लेकिन इस ट्यूटोरियल के लिए हम इसे सरल रखेंगे।

## चरण 4: पहचाने गए टेक्स्ट को आउटपुट करें

अंत में, हम परिणाम को प्रिंट करेंगे। `getText()` मेथड एक साधारण जावा `String` लौटाता है जिसे आप स्टोर, नेटवर्क पर भेज या फ़ाइल में लिख सकते हैं।

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

जब आप प्रोग्राम चलाएँगे, तो आपको कुछ इस तरह दिखना चाहिए:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

यदि आउटपुट गड़बड़ दिखे, तो सुनिश्चित करें कि स्रोत PNG हाई‑रेज़ोल्यूशन (कम से कम 300 dpi) हो और भाषा कोड `"th"` आपके लक्ष्य भाषा से मेल खाता हो।

### पूरा कोड लिस्टिंग

नीचे पूरी, तैयार‑चलाने‑योग्य जावा फ़ाइल दी गई है। इसे अपने IDE में कॉपी‑पेस्ट करें, यदि आवश्यक हो तो इमेज पाथ बदलें, और **Run** दबाएँ।

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![इमेज पर OCR चलाने का उदाहरण](image.png "इमेज पर OCR चलाने का उदाहरण – जावा कोड जो PNG से थाई टेक्स्ट निकालता है")

## चरण 5: सामान्य वैरिएशन और एज केस

### अन्य फ़ॉर्मैट में इमेज को टेक्स्ट में बदलना

यदि आपको JPEG या BMP के लिए **convert image to text** चाहिए, तो बस `imagePath` में फ़ाइल एक्सटेंशन बदल दें। Aspose OCR PNG, JPEG, BMP, TIFF, और यहाँ तक कि PDF पेजेज़ को भी सपोर्ट करता है।

### कई भाषाओं के साथ PNG से टेक्स्ट निकालना

आप इंजन को एक साथ कई भाषाएँ डिटेक्ट करने के लिए कह सकते हैं:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

परिणाम में थाई और अंग्रेज़ी दोनों अक्षर मिलेंगे, जो द्विभाषी रसीदों के लिए उपयोगी है।

### लो‑क्वालिटी इमेज को हैंडल करना

फ़ज़ी स्कैन के लिए, प्री‑प्रोसेसिंग सक्षम करने पर विचार करें:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

यह बिल्ट‑इन डीनॉइज़ और कॉन्ट्रास्ट‑एन्हांसमेंट एल्गोरिद्म को ट्रिगर करता है, जिससे **extract text from PNG** चरण बेहतर होता है।

### लाइसेंस एक्टिवेशन

लाइसेंस के बिना, Aspose 100 पेजेज़ के बाद आउटपुट में एक वॉटरमार्क लाइन जोड़ देता है। अपना लाइसेंस जल्दी एक्टिवेट करें:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

`.lic` फ़ाइल को अपने JAR के बगल में रखें या एब्सोल्यूट पाथ से रेफ़र करें।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या यह Linux पर काम करता है?**  
**उत्तर:** बिल्कुल। Aspose OCR शुद्ध जावा है, इसलिए कोई भी JVM‑कम्पैटिबल OS ठीक रहेगा।

**प्रश्न: अगर PNG में हाथ से लिखा थाई टेक्स्ट हो तो?**  
**उत्तर:** हैंडराइटिंग रिकग्निशन सीमित है; आपको एक समर्पित न्यूरल‑नेटवर्क मॉडल की जरूरत पड़ सकती है। Aspose OCR प्रिंटेड टेक्स्ट में उत्कृष्ट है।

**प्रश्न: क्या मैं इमेजेज़ के फ़ोल्डर को बैच‑प्रोसेस कर सकता हूँ?**  
**उत्तर:** `Files.list(Paths.get("folder"))` पर लूप लगाकर `recognizeImage` कॉल को रैप करें। प्रदर्शन के लिए वही `OcrEngine` इंस्टेंस पुनः उपयोग करें।

## निष्कर्ष

हमने जावा में **run OCR on image** फ़ाइलों को प्रोसेस करने का एक पूर्ण, एंड‑टू‑एंड उदाहरण देखा, विशेष रूप से PNG से **extract Thai text** करने के लिए। `OcrEngine` को इनिशियलाइज़ करके, भाषा सेट करके, `recognizeImage` को कॉल करके, और परिणाम प्रिंट करके, अब आपके पास बिना थर्ड‑पार्टी सर्विस के **convert image to text** करने का भरोसेमंद तरीका है।

अब आप आगे कर सकते हैं:

* बड़े पैमाने पर **extract text from PNG** फ़ाइलों को डेटा‑माइनिंग प्रोजेक्ट्स के लिए प्रोसेस करना।  
* OCR आउटपुट को ट्रांसलेशन API के साथ जोड़कर अंग्रेज़ी अनुवाद प्राप्त करना।  
* Aspose द्वारा सपोर्टेड अन्य भाषाओं (जैसे चीनी या अरबी) को भाषा कोड बदलकर एक्सप्लोर करना।

अपनी खुद की इमेजेज़ के साथ इसे आज़माएँ—प्री‑प्रोसेसिंग सेटिंग्स को ट्यून करें, विभिन्न फ़ॉर्मैट्स के साथ प्रयोग करें, और देखें कि वास्तविक वर्कफ़्लो में यह समाधान कितना मजबूत लगता है।

हैप्पी कोडिंग, और आपके OCR पाइपलाइन हमेशा सटीक रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}