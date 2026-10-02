---
category: general
date: 2026-09-23
description: Aspose OCR का उपयोग करके Java में छवियों पर OCR कैसे करें, छवि से टेक्स्ट
  निकालना, और कस्टम डिक्शनरी के साथ स्पेल करेक्शन सक्षम करना सीखें।
draft: false
keywords:
- how to perform ocr
- how to extract text from image
- java ocr maven dependency
- java image to text conversion
- aspose ocr java
lastmod: 2026-09-23
og_description: Java में Aspose OCR के साथ छवियों पर OCR कैसे करें। यह गाइड छवि लोड
  करने, छवि से टेक्स्ट निकालने, और सटीक परिणामों के लिए स्पेल करेक्शन जोड़ने को दर्शाता
  है।
og_image_alt: 'Aspose OCR Java tutorial: extracting text from images with spell correction'
og_title: Java में Aspose OCR के साथ छवियों पर OCR कैसे करें
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  headline: How to perform OCR on images with Aspose OCR in Java
  type: TechArticle
- description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  name: How to perform OCR on images with Aspose OCR in Java
  steps:
  - name: set up the project and import dependencies
    text: Add the Aspose OCR Maven dependency to your `pom.xml`. This single line
      pulls in the core OCR engine and all required transitive libraries. > **Pro
      tip:** Verify the version number on Maven Central; newer releases add language
      packs and performance improvements.
  - name: load the image for OCR
    text: '`OcrEngine` works with any `InputStream`. Use `ImageStream` to wrap a file
      path, byte array, or URL. **Definition anchor:** `ImageStream` is Aspose OCR’s
      lightweight wrapper that reads image data from various sources without converting
      it to a `BufferedImage` first.'
  - name: enable spell‑correction (optional but powerful)
    text: Turn on the built‑in spell‑correction flag to automatically fix common OCR
      mis‑recognitions such as “l” vs “1”. Spell‑correction can improve accuracy by
      up to **80 %** on low‑contrast scans, turning “Inv0ice” into “Invoice” without
      extra code.
  - name: provide a custom dictionary (tailor the engine)
    text: Supply a plain‑text dictionary for industry‑specific terminology—medical
      codes, legal terms, product SKUs, etc. **Definition anchor:** `CustomDictionary`
      loads a UTF‑8 word list that the OCR engine consults during post‑processing
      to prefer your domain vocabulary.
  - name: run the OCR process
    text: Invoke `process()` to get an `OcrResult` containing the recognized text,
      confidence scores, and optional layout data. If an error occurs, `ocrResult.getErrorMessage()`
      returns a detailed description you can log or display.
  - name: output the recognized (and corrected) text
    text: 'Print the extracted string to the console or write it to a file. For quick
      testing, a simple `System.out.println` is sufficient. Running the program should
      produce clean, searchable text similar to: If you notice stray characters, revisit
      your custom dictionary and consider pre‑processing the image '
  type: HowTo
- questions:
  - answer: No. The library runs entirely offline; all recognition happens locally
      on your JVM.
    question: Does Aspose OCR require an internet connection?
  - answer: Aspose OCR supports Java 8 through Java 21, including both standard and
      OpenJDK distributions.
    question: Which Java versions are supported?
  - answer: Yes. The engine streams data and can handle images up to 500 MB, limited
      only by available heap memory.
    question: Can I process images larger than 10 MB?
  - answer: Purchase a commercial license from the Aspose store and set the license
      file with `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: How do I license Aspose OCR for production?
  - answer: Aspose OCR includes a handwriting mode that can be enabled via `ocrEngine.getEngineOptions().setHandwriting(true);`,
      improving accuracy on cursive scripts.
    question: Is there built‑in support for handwritten text?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- image to text
- OCR Maven dependency
title: Java में Aspose OCR के साथ छवियों पर OCR कैसे करें
url: /hi/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज पर OCR करें – पूर्ण जावा ट्यूटोरियल

यदि आप जावा का उपयोग करके इमेज फ़ाइलों पर **OCR कैसे करें** के लिए एक विश्वसनीय तरीका खोज रहे हैं, तो आप सही जगह पर आए हैं। Aspose OCR for Java के साथ आप कुछ ही कोड लाइनों में इमेज एसेट्स से टेक्स्ट निकाल सकते हैं, कस्टम डिक्शनरी के साथ सटीकता बढ़ा सकते हैं, और शोरयुक्त स्कैन को साफ़ करने के लिए स्पेल‑करेक्शन सक्षम कर सकते हैं। यह ट्यूटोरियल आपको हर चरण के माध्यम से ले जाता है—OCR के लिए इमेज लोड करने से लेकर सुधारा गया टेक्स्ट प्रिंट करने तक—ताकि आप आज ही अपने एप्लिकेशन में इमेज‑टू‑टेक्स्ट रूपांतरण को एकीकृत कर सकें।

## त्वरित उत्तर
- **OCR शुरू करने के लिए मुख्य क्लास कौन सी है?** `OcrEngine` Aspose OCR की मुख्य क्लास है जो ऑप्टिकल कैरेक्टर रिकग्निशन करती है।
- **कौन सा Maven आर्टिफैक्ट OCR समर्थन जोड़ता है?** Add `com.aspose:aspose-ocr` to your `pom.xml`.
- **क्या विकास के लिए लाइसेंस की आवश्यकता है?** A free temporary license works for testing; a commercial license is required for production.
- **क्या मैं कम गुणवत्ता वाले स्कैन पर सटीकता बढ़ा सकता हूँ?** Yes—enable spell‑correction and supply a custom dictionary.
- **क्या मल्टी‑पेज सपोर्ट अंतर्निहित है?** Process each page image in a loop; the engine is thread‑safe for concurrent execution.

## OCR कैसे करें क्या है?
वाक्यांश **OCR कैसे करें** उस प्रक्रिया को दर्शाता है जिसमें इमेज में प्रिंटेड या हाथ से लिखे टेक्स्ट को ऑप्टिकल कैरेक्टर रिकग्निशन तकनीक का उपयोग करके संपादन योग्य, खोज योग्य डिजिटल अक्षरों में बदला जाता है। Aspose OCR इस प्रक्रिया को एक सिंगल‑पास इंजन के साथ लागू करता है जो 20 से अधिक रास्टर फ़ॉर्मैट और 50+ भाषाओं का समर्थन करता है।

## जावा के लिए Aspose OCR क्यों उपयोग करें?
Aspose OCR **20+ इमेज फ़ॉर्मैट** (जैसे PNG, JPEG, TIFF, BMP, और GIF) का समर्थन करता है और पूरे दस्तावेज़ को मेमोरी में लोड किए बिना **सैकड़ों‑पृष्ठ बैच** को प्रोसेस कर सकता है, सामान्य 4‑कोर सर्वर पर **300 पृष्ठ प्रति मिनट** तक की गति प्रदान करता है। इसके बिल्ट‑इन स्पेल‑करेक्शन और कस्टम डिक्शनरी फीचर शोरयुक्त इनवॉइस पर सामान्य OCR त्रुटि दर को 12 % से घटाकर 2 % से कम कर देते हैं।

## पूर्वापेक्षाएँ
- **Java Development Kit (JDK) 8+** – मानक जावा रनटाइम।
- **Aspose OCR for Java** library – नवीनतम JAR Maven Central या Aspose डाउनलोड पोर्टल से प्राप्त करें।
- वह इमेज फ़ाइल (उदाहरण के लिए `invoice.png`) जिसे आप प्रोसेस करना चाहते हैं।
- (वैकल्पिक) `custom_dict.txt` – एक UTF‑8 टेक्स्ट फ़ाइल जिसमें डोमेन‑विशिष्ट शब्द होते हैं, प्रत्येक पंक्ति में एक।

बस इतना ही चाहिए—कोई बाहरी सेवाएँ या भारी फ्रेमवर्क नहीं।

## जावा में इमेज पर OCR कैसे करें?
अपनी इमेज लोड करें, स्पेल‑करेक्शन सक्षम करें, वैकल्पिक रूप से एक कस्टम डिक्शनरी प्रदान करें, इंजन चलाएँ, और परिणाम पढ़ें। यह तरीका सिंगल‑पेज फ़ाइलों और बैच प्रोसेसिंग दोनों के लिए काम करता है, और इंजन स्वचालित रूप से इमेज डिकोडिंग, भाषा पहचान, और कॉन्फिडेंस स्कोरिंग को संभालता है, जिससे आपको आगे की प्रोसेसिंग के लिए एक विश्वसनीय टेक्स्ट आउटपुट मिलता है। निम्नलिखित सेक्शन प्रत्येक चरण को स्पष्ट व्याख्याओं और आपको कॉपी करने के लिए सटीक कोड के साथ विभाजित करते हैं।

### चरण 1: प्रोजेक्ट सेट अप करें और निर्भरताएँ इम्पोर्ट करें
अपने `pom.xml` में Aspose OCR Maven निर्भरता जोड़ें। यह एकल पंक्ति कोर OCR इंजन और सभी आवश्यक ट्रांज़िटिव लाइब्रेरीज़ को लाती है।

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

> **Pro tip:** Maven Central पर संस्करण संख्या सत्यापित करें; नए रिलीज़ में भाषा पैक्स और प्रदर्शन सुधार शामिल होते हैं।

### चरण 2: OCR के लिए इमेज लोड करें
`OcrEngine` किसी भी `InputStream` के साथ काम करता है। फ़ाइल पाथ, बाइट एरे, या URL को रैप करने के लिए `ImageStream` का उपयोग करें।

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Definition anchor:** `ImageStream` Aspose OCR का हल्का रैपर है जो विभिन्न स्रोतों से इमेज डेटा पढ़ता है बिना पहले इसे `BufferedImage` में परिवर्तित किए।

### चरण 3: स्पेल‑करेक्शन सक्षम करें (वैकल्पिक लेकिन शक्तिशाली)
बिल्ट‑इन स्पेल‑करेक्शन फ़्लैग को चालू करें ताकि सामान्य OCR गलतियों जैसे “l” बनाम “1” को स्वचालित रूप से ठीक किया जा सके।

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

स्पेल‑करेक्शन कम‑कॉन्ट्रास्ट स्कैन पर सटीकता को **80 %** तक बढ़ा सकता है, “Inv0ice” को “Invoice” में बदल देता है बिना अतिरिक्त कोड के।

### चरण 4: कस्टम डिक्शनरी प्रदान करें (इंजन को अनुकूलित करें)
उद्योग‑विशिष्ट शब्दावली के लिए एक प्लेन‑टेक्स्ट डिक्शनरी प्रदान करें—मेडिकल कोड, कानूनी शब्द, प्रोडक्ट SKU आदि।

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

**Definition anchor:** `CustomDictionary` एक UTF‑8 शब्द सूची लोड करता है जिसे OCR इंजन पोस्ट‑प्रोसेसिंग के दौरान आपके डोमेन शब्दावली को प्राथमिकता देने के लिए उपयोग करता है।

### चरण 5: OCR प्रक्रिया चलाएँ
`process()` को कॉल करें ताकि आपको एक `OcrResult` मिले जिसमें पहचाना गया टेक्स्ट, कॉन्फिडेंस स्कोर, और वैकल्पिक लेआउट डेटा हो।

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

यदि कोई त्रुटि होती है, तो `ocrResult.getErrorMessage()` एक विस्तृत विवरण लौटाता है जिसे आप लॉग या डिस्प्ले कर सकते हैं।

### चरण 6: पहचाने गए (और सुधारे गए) टेक्स्ट को आउटपुट करें
निकाले गए स्ट्रिंग को कंसोल पर प्रिंट करें या फ़ाइल में लिखें। त्वरित परीक्षण के लिए, एक साधारण `System.out.println` पर्याप्त है।

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

प्रोग्राम चलाने पर साफ़, खोज योग्य टेक्स्ट उत्पन्न होना चाहिए जो इस प्रकार हो:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

यदि आपको अनावश्यक अक्षर दिखें, तो अपनी कस्टम डिक्शनरी को पुनः देखें और इमेज को प्री‑प्रोसेस करने पर विचार करें (कॉन्ट्रास्ट बढ़ाएँ, डिनॉइज़ करें, या ग्रेस्केल में बदलें)।

## कस्टम डिक्शनरी का उपयोग करके इमेज से टेक्स्ट कैसे निकालें?
प्रोसेसिंग से पहले डिक्शनरी लोड करें, फिर `ocrEngine.setCustomDictionary(customDict)` कॉल करें। इंजन सूची में मौजूद शब्दों को प्राथमिकता देगा, जिससे विशेष शब्दावली के लिए फॉल्स पॉज़िटिव्स में नाटकीय रूप से कमी आएगी। डोमेन‑विशिष्ट शब्द प्रदान करके, आप OCR पोस्ट‑प्रोसेसर को अस्पष्ट अक्षरों को हल करने में मदद करते हैं, जैसे अक्षर “O” और संख्या “0” के बीच अंतर करना, जिससे तकनीकी दस्तावेज़ों पर कुल सटीकता में सुधार होता है।

## जावा OCR Maven निर्भरता को सही तरीके से कैसे जोड़ें?
अपने `pom.xml` के `<dependencies>` सेक्शन के भीतर निम्न स्निपेट जोड़ें। यह निर्भरता कोर Aspose OCR लाइब्रेरी और सभी आवश्यक ट्रांज़िटिव कंपोनेंट्स को लाती है, जिससे OCR इंजन अतिरिक्त कॉन्फ़िगरेशन के बिना इंस्टैंशिएट किया जा सकता है। फ़ाइल अपडेट करने के बाद `mvn clean install` चलाना सुनिश्चित करें ताकि Maven केंद्रीय रिपॉजिटरी से नवीनतम संस्करण को रिजॉल्व करे।

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

## सामान्य प्रश्न और किनारे के मामले
### यदि इमेज अलग फ़ॉर्मेट (PDF, TIFF, आदि) में हो तो क्या करें?
Aspose OCR रास्टर फ़ॉर्मैट को सीधे संभालता है। PDFs के लिए, पहले प्रत्येक पेज को इमेज के रूप में एक्सट्रैक्ट करें—Aspose PDF for Java `PdfExtractor` प्रदान करता है जो इसे कुशलता से करता है। एक बार जब आपके पास `BufferedImage` या बाइट स्ट्रीम हो, तो वही `setImage` कॉल काम करता है। यह तरीका आपको मल्टी‑पेज दस्तावेज़ को पूरे PDF को मेमोरी में बदलने के बिना प्रोसेस करने देता है, जिससे वर्कफ़्लो तेज़ और स्केलेबल रहता है।

### मैं मल्टी‑पेज दस्तावेज़ों को कैसे संभालूँ?
प्रत्येक पेज इमेज पर इटरेट करें, एक नया `OcrEngine` (या मौजूदा को रीसेट) बनाएं, और `OcrResult.getText()` मानों को जोड़ें। यह तरीका प्रत्येक पेज के लिए स्पेल‑चेकिंग कॉन्टेक्स्ट को स्वतंत्र रखता है। पेजों को क्रमिक या समानांतर थ्रेड्स में प्रोसेस करके, आप उच्च थ्रूपुट बनाए रख सकते हैं जबकि सुनिश्चित करते हैं कि प्रत्येक पेज को वही डिक्शनरी और स्पेल‑करेक्शन सेटिंग्स मिलें।

### क्या मैं भाषा या कैरेक्टर सेट को सीमित कर सकता हूँ?
हाँ। `ocrEngine.getEngineOptions().setLanguage(Language.English)` (या कोई भी समर्थित भाषा) कॉल करके पहचान सीमा को संकीर्ण करें, जिससे प्रोसेसिंग **30 %** तक तेज़ हो जाती है। भाषा को सीमित करने से इंजन को विचार करने वाले कैरेक्टर सेट में कमी आती है, जिससे अस्पष्टता घटती है और गति व सटीकता दोनों में सुधार होता है, विशेषकर उन दस्तावेज़ों के लिए जिनमें केवल लैटिन अक्षर होते हैं।

### बड़ी बैचों पर प्रदर्शन कैसा रहता है?
इंजन रीड‑ओनली ऑपरेशन्स के लिए थ्रेड‑सेफ़ है। एक थ्रेड पूल बनाएं और प्रत्येक इमेज को अपने `OcrEngine` इंस्टेंस को असाइन करें। 4‑कोर मशीन पर, आप समानांतर निष्पादन के साथ **≈250 पृष्ठ/मिनट** प्राप्त कर सकते हैं। पर्याप्त हीप मेमोरी आवंटित करें और CPU उपयोग की निगरानी करें ताकि हजारों हाई‑रेज़ोल्यूशन इमेज प्रोसेस करते समय बॉटलनेक से बचा जा सके।

## बेहतर सटीकता के लिए टिप्स
- **इमेज को प्री‑प्रोसेस करें**: OCR से पहले कॉन्ट्रास्ट बढ़ाएँ, मीडियन फ़िल्टर लागू करें, या ग्रेस्केल में बदलें।
- **300 dpi या अधिक** स्कैन का उपयोग करें; कम रिज़ॉल्यूशन से त्रुटि दर बहुत बढ़ जाती है।
- **कस्टम डिक्शनरी को केंद्रित रखें**: अत्यधिक असंबंधित शब्द स्पेल‑चेकर को भ्रमित कर सकते हैं।
- **रेजेक्स के साथ पोस्ट‑प्रोसेस करें**: निकाले जाने के बाद तिथियों, संख्याओं, या आईडी को वैलिडेट करें ताकि शेष विसंगतियों को पकड़ा जा सके।

## अगले कदम
अब जब आप जानते हैं **इमेज पर OCR कैसे करें** और **इमेज फ़ाइल से टेक्स्ट कैसे निकालें**, आप निम्नलिखित का अन्वेषण कर सकते हैं:
- OCR आउटपुट को एक सर्चेबल PDF के रूप में सहेजना जिसमें हिडन टेक्स्ट लेयर हो।
- निकाले गए इनवॉइस डेटा को सीधे रिलेशनल डेटाबेस में स्टोर करना।
- हैंडराइटन नोट्स को और साफ़ करने के लिए मशीन‑लर्निंग मॉडल लागू करना।
- उपयोगकर्ता द्वारा अपलोड की गई तस्वीरों के लिए OCR वर्कफ़्लो को RESTful वेब सर्विस के रूप में एक्सपोज़ करना।

इनमें से प्रत्येक विस्तार ऊपर वर्णित कोर चरणों पर आधारित है, इसलिए आपको परिवर्तन सहज लगेगा।

---

**अंतिम अपडेट:** 2026-09-23  
**परीक्षण किया गया:** Aspose OCR 24.12 for Java  
**लेखक:** Aspose  

## अक्सर पूछे जाने वाले प्रश्न
**Q: क्या Aspose OCR को इंटरनेट कनेक्शन की आवश्यकता है?**  
A: नहीं। लाइब्रेरी पूरी तरह ऑफ़लाइन चलती है; सभी पहचान आपके JVM पर स्थानीय रूप से होती है।

**Q: कौन से जावा संस्करण समर्थित हैं?**  
A: Aspose OCR Java 8 से लेकर Java 21 तक समर्थन देता है, जिसमें स्टैंडर्ड और OpenJDK दोनों वितरण शामिल हैं।

**Q: क्या मैं 10 MB से बड़ी इमेज प्रोसेस कर सकता हूँ?**  
A: हाँ। इंजन डेटा को स्ट्रीम करता है और 500 MB तक की इमेज को संभाल सकता है, केवल उपलब्ध हीप मेमोरी द्वारा सीमित।

**Q: उत्पादन के लिए Aspose OCR को कैसे लाइसेंस करें?**  
A: Aspose स्टोर से एक व्यावसायिक लाइसेंस खरीदें और लाइसेंस फ़ाइल को `License license = new License(); license.setLicense("Aspose.OCR.lic");` के साथ सेट करें।

**Q: क्या हैंडराइटन टेक्स्ट के लिए बिल्ट‑इन समर्थन है?**  
A: Aspose OCR में एक हैंडराइटिंग मोड शामिल है जिसे `ocrEngine.getEngineOptions().setHandwriting(true);` के माध्यम से सक्षम किया जा सकता है, जिससे कर्सिव स्क्रिप्ट पर सटीकता बढ़ती है।

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

## संबंधित ट्यूटोरियल
- [Aspose OCR जावा के साथ इमेज पर OCR करने का चरण-दर-चरण गाइड](/ocr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/)
- [जावा में इमेज OCR को प्रीप्रोसेस करें, सटीकता बढ़ाएँ, टेक्स्ट निकालें](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [जावा में OCR के लिए GPU कैसे सक्षम करें, इमेज से टेक्स्ट पहचानें](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}