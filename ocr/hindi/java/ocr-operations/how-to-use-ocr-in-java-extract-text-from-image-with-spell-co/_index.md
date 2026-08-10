---
category: general
date: 2026-05-06
description: जावा में OCR का उपयोग करके छवि से टेक्स्ट निकालने का तरीका। OCR इमेज‑से‑टेक्स्ट
  रूपांतरण सीखें, OCR त्रुटियों को सुधारें और Aspose OCR के साथ OCR के लिए छवि लोड
  करें।
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: hi
og_description: जावा में OCR का उपयोग करके छवि से टेक्स्ट निकालना, OCR त्रुटियों को
  सुधारना और Aspose OCR का उपयोग करके OCR के लिए छवि लोड करना।
og_title: जावा में OCR का उपयोग कैसे करें – पूर्ण गाइड
tags:
- OCR
- Java
- Aspose
title: जावा में OCR का उपयोग कैसे करें – इमेज से टेक्स्ट निकालें और वर्तनी सुधार के
  साथ
url: /hi/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में OCR का उपयोग कैसे करें – इमेज से टेक्स्ट निकालें और स्पेल करेक्शन के साथ

क्या आपने कभी **OCR का उपयोग कैसे करें** को एक धुंधली रसीद की फोटो को साफ, खोज योग्य टेक्स्ट में बदलने के लिए? आप अकेले नहीं हैं। कई प्रोजेक्ट्स में—खर्च‑ट्रैकिंग ऐप्स, इनवॉइस डिजिटाइज़ेशन पाइपलाइन, या यहाँ तक कि एक त्वरित नोट‑लेने वाला स्क्रिप्ट—एक इमेज से विश्वसनीय टेक्स्ट प्राप्त करना पहला बाधा है।  

यह ट्यूटोरियल आपको बिल्कुल दिखाता है कि जावा में OCR का उपयोग कैसे करें, OCR के लिए इमेज लोड करने से लेकर OCR त्रुटियों को सुधारने तक, ताकि परिणाम ऐसा लगे जैसे इंसान ने टाइप किया हो। अंत तक, आप **extract text from image**, **OCR image to text** रूपांतरण कर सकेंगे, और सामान्य पहचान त्रुटियों को स्वचालित रूप से ठीक कर सकेंगे।

## आप क्या बनाएँगे

हम एक छोटा जावा कंसोल प्रोग्राम बनाएँगे जो:

1. PNG (या कोई भी समर्थित फ़ॉर्मेट) को Aspose OCR इंजन में लोड करता है।  
2. बिल्ट‑इन स्पेल‑करेक्शन फीचर को सक्षम करता है ताकि **correct OCR errors**।  
3. पहचान प्रक्रिया चलाता है और साफ़ किया गया टेक्स्ट प्रिंट करता है।  

कोई बाहरी सेवाएँ नहीं, कोई भारी फ्रेमवर्क नहीं—सिर्फ एक सिंगल JAR और कुछ लाइनों का कोड।

### पूर्वापेक्षाएँ

- Java Development Kit (JDK) 8 या नया।  
- Maven (या कोई भी बिल्ड टूल) Aspose OCR लाइब्रेरी को प्राप्त करने के लिए।  
- एक इमेज फ़ाइल (जैसे `receipt.png`) जिसे आप विश्लेषण करना चाहते हैं।  

यदि आपके पास Aspose OCR JAR नहीं है, तो इस डिपेंडेंसी को अपने `pom.xml` में जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Pro tip:** मुफ्त इवैल्यूएशन संस्करण परीक्षण के लिए काम करता है, लेकिन लाइसेंस इवैल्यूएशन वॉटरमार्क को हटा देता है।

## चरण 1 – OCR इंजन को इनिशियलाइज़ करें (Primary Keyword in Action)

पहला काम जो आपको करना है वह है `OcrEngine` की एक इंस्टेंस बनाना। इसे ऐसे समझें जैसे वह दिमाग जो पिक्सेल को पढ़ेगा और उन्हें अक्षरों में बदल देगा।

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Why this matters:* इंजन को इनिशियलाइज़ करने से आंतरिक रिसोर्सेज (भाषा मॉडल, शब्दकोश, आदि) सेट होते हैं। इस चरण को छोड़ने से बाद में इमेज लोड करने पर `NullPointerException` हो सकता है।

## चरण 2 – OCR के लिए इमेज लोड करें

अब हम वास्तव में **load image for OCR**। Aspose एक सुविधाजनक `ImageStream.fromFile` हेल्पर प्रदान करता है, लेकिन आप चाहें तो `byte[]` भी दे सकते हैं।

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Common pitfall:* फ़ाइल पाथ एब्सोल्यूट या वर्किंग डायरेक्टरी के रिलेटिव होना चाहिए। यदि इमेज नहीं मिलती, तो इंजन `IOException` फेंकेगा। पाथ को दोबारा जाँचें, विशेष रूप से जब IDE से चलाते हैं बनाम पैकेज्ड JAR से।

## चरण 3 – **Correct OCR Errors** के लिए स्पेल करेक्शन सक्षम करें

डिफ़ॉल्ट OCR शोरयुक्त हो सकता है—जैसे “l0ve” की जगह “love” या “O” की जगह “0”。 स्पेल करेक्शन को सक्षम करने से इंजन को एक पोस्ट‑प्रोसेसिंग पास चलाने को कहा जाता है जो सामान्य गलतियों को ठीक करता है।

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Why you’d want this:* स्पेल करेक्शन के बिना, आपको आउटपुट को मैन्युअली साफ़ करना पड़ेगा, जो ऑटोमेशन के उद्देश्य को नष्ट कर देता है। बिल्ट‑इन शब्दकोश अंग्रेज़ी और कई अन्य भाषाओं के लिए अच्छा काम करता है।

## चरण 4 – पहचान करें (**OCR Image to Text**)

इमेज लोड हो जाने और स्पेल करेक्शन सक्षम हो जाने के बाद, हम अंततः इंजन से टेक्स्ट पहचानने को कह सकते हैं।

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Edge case:* यदि इमेज लो‑कंट्रास्ट या बहुत टिल्टेड है, तो परिणाम में अभी भी बकवास हो सकता है। इंजन को फीड करने से पहले प्री‑प्रोसेसिंग (जैसे बाइनराइज़ेशन, डेस्क्यू) पर विचार करें।

## चरण 5 – साफ़ किया गया टेक्स्ट आउटपुट करें

अंतिम चरण बस परिणाम को प्रिंट करना है। वास्तविक एप्लिकेशन में आप इसे डेटाबेस या फ़ाइल में लिख सकते हैं, लेकिन इस डेमो के लिए `System.out` पर्याप्त है।

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### अपेक्षित आउटपुट

मान लीजिए `receipt.png` में वस्तुओं की स्पष्ट सूची है, तो आप कुछ इस तरह देख सकते हैं:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

ध्यान दें कि “Qty” और “Price” सही ढंग से लिखे गए हैं भले ही मूल स्कैन में “Qy” जैसा गलती हो।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा प्रोग्राम है जिसे आप `SpellCorrectDemo.java` नाम की फ़ाइल में कॉपी‑पेस्ट कर सकते हैं। सुनिश्चित करें कि Aspose OCR JAR आपके क्लासपाथ में है।

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

इसे चलाएँ:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

अब आपको कंसोल में साफ़ किया गया टेक्स्ट प्रिंट होता दिखेगा।

## बोनस: बेहतर सटीकता के लिए सेटिंग्स को ट्यून करना

डिफ़ॉल्ट कॉन्फ़िगरेशन अधिकांश प्रिंटेड दस्तावेज़ों के लिए काम करता है, लेकिन विशेष परिस्थितियों में आपको कुछ पैरामीटर समायोजित करने पड़ सकते हैं:

| सेटिंग | क्या करता है | कब बदलें |
|---------|--------------|----------|
| `setLanguage(OcrLanguage.English)` | इंग्लिश शब्दकोश को मजबूर करता है (गलत पॉज़िटिव को कम करता है) | यदि आपकी इमेज में केवल अंग्रेज़ी टेक्स्ट है। |
| `setResolution(300)` | इंजन को स्रोत इमेज की DPI बताता है | हाई‑रिज़ॉल्यूशन स्कैन के लिए। |
| `setEnableAutoSkewCorrection(true)` | हल्के टिल्टेड पेजों को ऑटो‑रोटेट करता है | जब इमेज फ़ोन से कैप्चर की गई हों। |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या यह PDFs के साथ काम करता है?**  
A: हाँ। प्रत्येक PDF पेज को इमेज में कनवर्ट करें (जैसे Aspose PDF का उपयोग करके) और इमेज को OCR इंजन में फीड करें।

**Q: अगर मेरी इमेज BMP फ़ॉर्मेट में है तो?**  
A: `ImageStream.fromFile` डिफ़ॉल्ट रूप से PNG, JPEG, BMP, TIFF, और GIF को सपोर्ट करता है। बस फ़ाइल एक्सटेंशन बदल दें।

**Q: क्या मैं स्पेल करेक्शन को डिसेबल कर सकता हूँ?**  
A: बिल्कुल—यदि आपको डाउनस्ट्रीम प्रोसेसिंग के लिए कच्चा OCR आउटपुट चाहिए तो `setEnableSpellCorrection(false)` सेट करें।

## निष्कर्ष

अब आप जानते हैं **how to use OCR** जावा में **extract text from image**, स्वचालित रूप से **correct OCR errors**, और Aspose OCR का उपयोग करके **load image for OCR** सही तरीके से कैसे करें। पाँच‑स्टेप फ्लो—इनिशियलाइज़, लोड, स्पेल करेक्शन सक्षम, पहचान, और आउटपुट—दैनिक OCR कार्यों का अधिकांश भाग कवर करता है।  

अब आप इस लॉजिक को डेटाबेस राइट‑बैक, REST एंडपॉइंट, या बैच प्रोसेसर के साथ जोड़ने पर विचार कर सकते हैं ताकि एक साथ दर्जनों रसीदों को संभाला जा सके। ऊपर दिए गए अतिरिक्त सेटिंग्स टेबल के साथ प्रयोग करें ताकि सटीकता का हर एक कैरेक्टर निकाला जा सके।  

कोडिंग का आनंद लें, और आपकी OCR परिणाम हमेशा आपके कॉफ़ी‑दाग़ वाले रसीदों से भी साफ़ रहें! 

![इमेज → OCR इंजन → सुधरा हुआ टेक्स्ट प्रवाह दिखाने वाला OCR उपयोग डायग्राम]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}