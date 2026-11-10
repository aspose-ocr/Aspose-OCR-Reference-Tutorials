---
category: general
date: 2026-02-17
description: Aspose OCR Java लाइब्रेरी का उपयोग करके छवि से टेक्स्ट पहचानना और OCR
  के लिए छवि लोड करना सीखें। स्पेल‑करेक्टर के साथ चरण‑दर‑चरण मार्गदर्शिका।
draft: false
keywords:
- recognize text from image
- load image for OCR
- Aspose OCR Java
- spell corrector OCR
- OCR engine setup
language: hi
og_description: Aspose OCR Java का उपयोग करके छवि से पाठ पहचानें। यह ट्यूटोरियल दिखाता
  है कि OCR के लिए छवि कैसे लोड करें, वर्तनी सुधार सक्षम करें, और साफ़ पाठ आउटपुट
  करें।
og_title: छवि से पाठ पहचानें – पूर्ण Aspose OCR जावा गाइड
tags:
- Java
- OCR
- Aspose
title: Aspose OCR के साथ इमेज से टेक्स्ट पहचानें – जावा ट्यूटोरियल
url: /hi/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज से टेक्स्ट पहचानें Aspose OCR – Java ट्यूटोरियल

क्या आपको कभी **इमेज से टेक्स्ट पहचानने** की ज़रूरत पड़ी, लेकिन यह तय नहीं कर पाए कि कौन सी लाइब्रेरी चुनें? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में—जैसे इनवॉइस स्कैन करना, हाथ से लिखे नोट्स को डिजिटल बनाना, या स्क्रीनशॉट से कैप्शन निकालना—सटीक OCR परिणाम प्राप्त करना बहुत महत्वपूर्ण है।

इस गाइड में हम OCR के लिए इमेज लोड करने, Aspose OCR के बिल्ट‑इन स्पेल करेक्टर को चालू करने, और अंत में साफ़ किया गया टेक्स्ट प्रिंट करने की प्रक्रिया देखेंगे। अंत तक आपके पास एक तैयार‑चलाने‑योग्य Java प्रोग्राम होगा जो कुछ ही लाइनों के कोड से **इमेज से टेक्स्ट पहचानता** है।

## इस ट्यूटोरियल में क्या कवर किया गया है

- अपने Aspose OCR लाइसेंस को कैसे लागू करें (ताकि डेमो वॉटरमार्क के बिना चले)  
- `OcrEngine` इंस्टेंस बनाना और पहचान भाषा के रूप में English चुनना  
- `OcrInput` का उपयोग करके **OCR के लिए इमेज लोड** करें और उसे उन PNG फ़ाइल की ओर इंगित करें जिसमें गलत शब्द हैं  
- स्पेल‑करेक्टर को सक्षम करना, वैकल्पिक रूप से एक कस्टम डिक्शनरी की ओर इंगित करना  
- पहचान चलाना और सुधारित परिणाम प्रिंट करना  

कोई बाहरी सर्विस नहीं, कोई छिपी हुई कॉन्फ़िगरेशन फ़ाइल नहीं—सिर्फ साधारण Java और Aspose OCR JAR।

> **Pro tip:** यदि आप Aspose में नए हैं, तो Aspose वेबसाइट से एक मुफ्त 30‑दिन का ट्रायल लाइसेंस प्राप्त करें और `.lic` फ़ाइल को उस फ़ोल्डर में रखें जिसे आप अपने कोड से रेफ़र कर सकते हैं।

## आवश्यकताएँ

- Java 8 या उससे नया (कोड JDK 11 के साथ भी कम्पाइल होता है)  
- आपके क्लासपाथ में Aspose.OCR for Java JAR  
- एक वैध `Aspose.OCR.lic` फ़ाइल (या आप इवैल्यूएशन मोड में चला सकते हैं, लेकिन डेमो में वॉटरमार्क जुड़ जाएगा)  
- एक इमेज फ़ाइल (`misspelled.png`) जिसमें जानबूझकर स्पेलिंग त्रुटियों के साथ कुछ टेक्स्ट हो—स्पेल करेक्टर को काम में देखते हुए एकदम सही  

सब कुछ तैयार है? बढ़िया—चलिए शुरू करते हैं।

## चरण 1: अपना Aspose OCR लाइसेंस लागू करें

इंजन किसी भी भारी काम को करने से पहले, इसे पता होना चाहिए कि आप लाइसेंसधारी हैं। अन्यथा आउटपुट में आपको “Trial version” बैनर मिलेगा।

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – replace the path with where you stored your .lic file
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

*क्यों यह महत्वपूर्ण है:* लाइसेंसिंग ट्रायल वॉटरमार्क को निष्क्रिय करती है और पूर्ण स्पेल‑करेक्टर डिक्शनरी को अनलॉक करती है। इस चरण को छोड़ने से प्रोग्राम चलेगा, लेकिन आपका आउटपुट “Aspose OCR Demo” टेक्स्ट से भर जाएगा।

## चरण 2: OCR इंजन बनाएं और कॉन्फ़िगर करें

अब हम इंजन को शुरू करते हैं और उसे बताते हैं कि कौन सी भाषा उपयोग करनी है। English सबसे सामान्य है, लेकिन Aspose कई भाषाओं को सपोर्ट करता है।

```java
        // Step 2: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Choose English for recognition – you could pick French, German, etc.
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
```

*हमने भाषा क्यों सेट की:* भाषा मॉडल कैरेक्टर सेट निर्धारित करता है और स्पेल‑करेक्टर के सुझावों को प्रभावित करता है। गलत भाषा का उपयोग करने से सटीकता में काफी गिरावट आ सकती है।

## चरण 3: स्पेल करेक्शन सक्षम करें और (वैकल्पिक रूप से) कस्टम डिक्शनरी की ओर इंगित करें

Aspose OCR एक बिल्ट‑इन English डिक्शनरी के साथ आता है, लेकिन यदि आपके पास डोमेन‑स्पेसिफिक शब्द हैं (जैसे मेडिकल जार्गन या प्रोडक्ट कोड), तो आप अपनी खुद की डिक्शनरी प्रदान कर सकते हैं।

```java
        // Step 3: Turn on the spell corrector
        engine.getSpellCorrector().setEnable(true); // activate spell‑checking

        // Optional: use a custom dictionary folder
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english");
```

*करेक्टर क्या करता है:* जब OCR इंजन कोई ऐसा शब्द देखता है जो डिक्शनरी में नहीं है, तो वह सबसे नज़दीकी मिलते‑जुलते शब्द से बदलने की कोशिश करता है। इसलिए डेमो “recieve” को स्वचालित रूप से “receive” में बदल सकता है।

## चरण 4: OCR के लिए इमेज लोड करें

यह वह भाग है जो सीधे **OCR के लिए इमेज लोड** करने का उत्तर देता है। हम एक `OcrInput` ऑब्जेक्ट बनाते हैं और अपनी PNG फ़ाइल जोड़ते हैं।

```java
        // Step 4: Prepare the image input
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // path to the image you want to process
```

*हम `OcrInput` क्यों उपयोग करते हैं:* यह फ़ाइल‑रीडिंग लॉजिक को एब्स्ट्रैक्ट करता है और आपको बाद में कई पेज़ जोड़ने की सुविधा देता है यदि आपको मल्टी‑पेज PDF या इमेज सेट प्रोसेस करना हो।

## चरण 5: पहचान चलाएँ और सुधारित टेक्स्ट प्राप्त करें

इंजन अब भारी काम करता है—कैरेक्टर पहचानना, भाषा मॉडल लागू करना, और अंत में स्पेलिंग सुधारना।

```java
        // Step 5: Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Step 6: Output the corrected text to the console
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

*अपेक्षित आउटपुट:* मान लीजिए `misspelled.png` में वाक्य “Ths is a smple test” है, तो कंसोल प्रिंट करेगा:

```
Corrected text:
This is a simple test
```

ध्यान दें कि गलत शब्द (`Ths`, `smple`) स्वचालित रूप से ठीक हो गए हैं।

## पूर्ण, तैयार‑चलाने‑योग्य उदाहरण

नीचे पूरा प्रोग्राम एक ब्लॉक में दिया गया है। कॉपी‑पेस्ट करें, पाथ समायोजित करें, और **Run** दबाएँ।

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (replace with your license file)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Select the language for recognition (e.g., English)
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);

        // Enable the built‑in spell corrector and optionally set a custom dictionary
        engine.getSpellCorrector().setEnable(true);                     // activate spell‑checking
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english"); // optional

        // Prepare the input image containing the text to be recognized
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // load image for OCR

        // Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Output the corrected text
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

**Tip:** यदि आप PNG के बजाय JPEG या BMP प्रोसेस करना चाहते हैं, तो बस फ़ाइल एक्सटेंशन बदल दें—Aspose OCR सभी सामान्य रास्टर फ़ॉर्मेट्स को सपोर्ट करता है।

## सामान्य प्रश्न एवं किनारे के मामलों

- **अगर मेरी इमेज लो‑रेज़ोल्यूशन है तो क्या करें?**  
  Aspose को फीड करने से पहले DPI बढ़ाएँ, जैसे `java.awt.Image` जैसी लाइब्रेरी से री‑स्केल करके। उच्च DPI इंजन को अधिक पिक्सेल देता है, जिससे आमतौर पर सटीकता बेहतर होती है।

- **क्या मैं एक ही इमेज में कई भाषाएँ पहचान सकता हूँ?**  
  हाँ। `engine.getLanguage().setLanguage(OcrLanguage.MULTI_LANGUAGE);` कॉल करें और वैकल्पिक रूप से `engine.getLanguage().addLanguage(OcrLanguage.SPANISH);` के माध्यम से भाषाओं की सूची प्रदान करें।

- **मेरी कस्टम डिक्शनरी उपयोग नहीं हो रही—क्यों?**  
  सुनिश्चित करें कि फ़ोल्डर में सादा‑टेक्स्ट फ़ाइलें हों, प्रत्येक पंक्ति में एक शब्द हो, और पाथ पूर्ण (absolute) या आपके वर्किंग डायरेक्टरी के सापेक्ष सही हो।

- **मैं कॉन्फिडेंस स्कोर कैसे निकालूँ?**  
  `result.getConfidence()` पूरे पेज के लिए 0 और 1 के बीच का फ्लोट रिटर्न करता है। प्रति‑कैरेक्टर कॉन्फिडेंस के लिए `result.getWordList()` देखें।

## निष्कर्ष

अब आप जानते हैं कि Aspose OCR for Java का उपयोग करके **इमेज से टेक्स्ट कैसे पहचानें**, **OCR के लिए इमेज कैसे लोड करें**, और सामान्य टाइपो को साफ़ करने के लिए स्पेल‑करेक्टर को कैसे सक्षम करें। ऊपर दिया गया पूर्ण उदाहरण किसी भी Maven या Gradle प्रोजेक्ट में डालने के लिए तैयार है, और कुछ छोटे बदलावों से आप इसे फ़ोल्डर बैच‑प्रोसेसिंग, वेब सर्विस में इंटीग्रेट करने, या डॉक्यूमेंट‑मैनेजमेंट सिस्टम के साथ जोड़ने के लिए स्केल कर सकते हैं।

अगले कदम के लिए तैयार हैं? मल्टी‑पेज PDF फीड करने की कोशिश करें, उद्योग‑विशिष्ट शब्दावली के लिए कस्टम डिक्शनरी के साथ प्रयोग करें, या आउटपुट को ट्रांसलेशन API में जोड़ें। संभावनाएँ अनंत हैं, और मुख्य पैटर्न—license → engine → language → spell‑corrector → input → recognize → output—वही रहता है।

कोडिंग का आनंद लें, और आपकी OCR परिणाम हमेशा सटीक रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}