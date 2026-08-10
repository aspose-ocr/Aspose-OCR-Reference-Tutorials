---
category: general
date: 2026-05-06
description: Aspose OCR का उपयोग करके छवि से पाठ को पहचानने, स्वचालित भाषा पहचान को
  सक्षम करने, और जावा में OCR गति को सुधारने का तरीका।
draft: false
keywords:
- how to use aspose
- recognize text from image
- improve ocr speed
- load image for ocr
- enable automatic language detection
language: hi
og_description: Aspose OCR का उपयोग करके छवि से तेज़ी से टेक्स्ट पहचानना, स्वचालित
  भाषा पहचान सक्षम करना, और जावा में OCR गति में सुधार करना।
og_title: मिक्स्ड‑भाषा छवियों के लिए Aspose OCR का उपयोग कैसे करें
tags:
- Aspose
- OCR
- Java
- Image Processing
title: मिश्रित‑भाषा छवियों के लिए Aspose OCR का उपयोग कैसे करें
url: /hi/java/advanced-ocr-techniques/how-to-use-aspose-ocr-for-mixed-language-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR को मिश्रित‑भाषा छवियों के लिए कैसे उपयोग करें

क्या आपने कभी सोचा है **how to use Aspose** को एक ऐसी तस्वीर से टेक्स्ट निकालने के लिए जिसमें एक साथ कई भाषाएँ हों? आप अकेले नहीं हैं—डेवलपर्स अक्सर तब रुकावट का सामना करते हैं जब कोई छवि अंग्रेज़ी, रूसी, हिंदी या किसी अन्य लिपि को मिलाती है। अच्छी खबर यह है कि Aspose OCR इसे सहजता से संभालता है, और आप भाषा सेट को सीमित करके **recognize text from image** को तेज़ भी कर सकते हैं।

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने‑योग्य Java उदाहरण के माध्यम से चलेंगे जो **loads image for OCR** करता है, **automatic language detection** को सक्रिय करता है, और **improve OCR speed** के लिए एक सरल ट्रिक दिखाता है। अंत तक आपके पास एक स्व-निहित प्रोग्राम होगा जो निकाले गए टेक्स्ट को कंसोल पर प्रिंट करेगा, और आप समझ पाएँगे कि प्रत्येक सेटिंग क्यों महत्वपूर्ण है।

> **Prerequisites** – Java 17+ स्थापित हो, Maven या Gradle निर्भरता प्रबंधन के लिए, और एक Aspose OCR लाइसेंस (मुफ़्त ट्रायल मूल्यांकन के लिए काम करता है)। अन्य कोई लाइब्रेरी आवश्यक नहीं है।

---

## Step 1 – अपने प्रोजेक्ट में Aspose OCR जोड़ें

Aspose **use** करने से पहले, आपको लाइब्रेरी को अपने क्लासपाथ पर जोड़ना होगा। Maven के साथ यह इस प्रकार दिखता है:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

यदि आप Gradle पसंद करते हैं:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** नवीनतम स्थिर रिलीज़ का उपयोग करें; नई संस्करण अक्सर प्रदर्शन सुधार शामिल करते हैं जो सीधे **improve OCR speed** को प्रभावित करते हैं।

---

## Step 2 – OCR Engine Instance बनाएं  

हर Aspose OCR कार्यप्रवाह का दिल `OcrEngine` है। इसे इंस्टैंसिएट करना सरल है, लेकिन यह ध्यान देने योग्य है कि इंजन आंतरिक कैश रखता है। कई छवियों में एक ही इंस्टेंस को पुनः उपयोग करने से वास्तव में **improve OCR speed** हो सकता है क्योंकि लाइब्रेरी दोहराए गए नेटिव इनिशियलाइज़ेशन से बचती है।

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise the OCR engine – one instance per application is ideal
        OcrEngine ocrEngine = new OcrEngine();
```

## Step 3 – **Load Image for OCR**  

Aspose कई इमेज फ़ॉर्मेट (PNG, JPEG, TIFF, BMP) को स्वीकार करता है। यहाँ हम एक PNG लोड करने का प्रदर्शन करते हैं जिसमें अंग्रेज़ी, रूसी, और हिंदी टेक्स्ट है। `ImageStream.fromFile` हेल्पर फ़ाइल‑I/O विवरणों को एब्स्ट्रैक्ट करता है और सुनिश्चित करता है कि इमेज सही ढंग से इंजन में स्ट्रीम हो।

```java
        // Step 3: Load the picture that holds mixed languages
        // Replace the path with the actual location of your image file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));
```

> **What if the image is in memory?** `ImageStream.fromByteArray(byte[])` का उपयोग करें—वेब सेवाओं के लिए उपयुक्त जो इमेज को बाइट स्ट्रीम के रूप में प्राप्त करती हैं।

## Step 4 – Automatic Language Detection सक्षम करें  

डिफ़ॉल्ट रूप से Aspose OCR एक ही भाषा मानता है, जिससे बहुभाषी चित्रों पर गड़बड़ आउटपुट हो सकता है। ऑटोमैटिक डिटेक्शन को चालू करने से इंजन को प्रत्येक टेक्स्ट ब्लॉक की स्क्रिप्ट को पहचानने से पहले पहचानने की अनुमति मिलती है।

```java
        // Step 4: Turn on auto‑detect – this is the key to handling mixed‑language images
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

## Step 5 – भाषा पूल को सीमित करके **Improve OCR Speed**  

पूर्ण ऑटो‑डिटेक्ट Aspose द्वारा समर्थित सभी भाषाओं (70 से अधिक) को स्कैन करता है। यदि आप पहले से संभावित भाषाओं को जानते हैं, तो आप इंजन को एक संकेत दे सकते हैं। छोटा एरे प्रदान करने से सर्च स्पेस कम हो जाता है और इसलिए **improves OCR speed**।

```java
        // Step 5 (optional but recommended): Limit detection to known languages
        // "en" = English, "ru" = Russian, "hi" = Hindi
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });
```

> **Why does this help?** इंजन उन भाषा मॉडलों को स्किप करता है जिनकी उसे आवश्यकता नहीं है, जिससे CPU साइकिल और मेमोरी बचती है। यदि आप बाद में अधिक भाषाएँ जोड़ते हैं, तो केवल एरे को अपडेट करें—कोड को फिर से लिखने की आवश्यकता नहीं।

## Step 6 – पहचान करें और **Recognize Text from Image**

अब भारी काम होता है। `recognize()` एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें साधारण टेक्स्ट, कॉन्फिडेंस स्कोर, और यदि बाद में आवश्यकता हो तो लेआउट जानकारी भी शामिल होती है।

```java
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### अपेक्षित कंसोल आउटपुट

```
=== Extracted Text ===
Hello world!
Привет мир!
नमस्ते दुनिया!
```

यदि छवि में अतिरिक्त शोर या तिरछा टेक्स्ट है, तो आप उन लाइनों के लिए कम कॉन्फिडेंस देख सकते हैं। ऐसे में, Aspose को फीड करने से पहले छवि का पूर्व‑प्रसंस्करण (डेस्क्यू, बाइनराइज़ेशन) करने पर विचार करें।

## Common Questions & Edge Cases

### यदि छवि बहुत बड़ी हो (जैसे, >10 MP) तो क्या करें?

बड़ी छवियाँ अधिक मेमोरी खपत करती हैं और प्रोसेसिंग को धीमा कर सकती हैं। **improve OCR speed** का एक तेज़ तरीका है छवि को पढ़ने योग्य रखते हुए डाउनस्केल करना:

```java
// Example using java.awt for simple resizing (optional)
BufferedImage original = ImageIO.read(new File("large.png"));
int targetWidth = 2000; // adjust based on your needs
BufferedImage resized = new BufferedImage(targetWidth,
        (original.getHeight() * targetWidth) / original.getWidth(),
        BufferedImage.TYPE_INT_RGB);
Graphics2D g = resized.createGraphics();
g.drawImage(original, 0, 0, targetWidth, resized.getHeight(), null);
g.dispose();
ocrEngine.setImage(ImageStream.fromImage(resized));
```

### Arabic जैसी दाएँ‑से‑बाएँ स्क्रिप्ट को कैसे संभालें?

Aspose OCR स्वचालित रूप से स्क्रिप्ट दिशा का सम्मान करता है, लेकिन आप पोस्ट‑प्रोसेसिंग के लिए `RightToLeft` फ़्लैग सेट करना चाह सकते हैं:

```java
ocrEngine.getSettings().setRightToLeft(true);
```

### क्या मैं इमेज के बजाय PDFs से टेक्स्ट निकाल सकता हूँ?

हां—प्रत्येक PDF पेज को एक इमेज में बदलें (Aspose PDF या किसी भी रास्टराइज़र का उपयोग करके) और परिणाम को उसी OCR पाइपलाइन में फीड करें। वही **recognize text from image** लॉजिक लागू होता है।

## Full Working Example (कॉपी‑पेस्ट तैयार)

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates how to use Aspose OCR to recognize text from an image
 * that contains multiple languages, with automatic language detection
 * and a speed‑optimising language whitelist.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine – reuse this instance for many images
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that holds mixed languages (replace with your path)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));

        // Enable automatic detection of language per text block
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // OPTIONAL: Restrict detection to English, Russian, and Hindi to boost speed
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });

        // Run OCR and capture the result
        OcrResult ocrResult = ocrEngine.recognize();

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

`MixedLanguageDemo.java` के रूप में फ़ाइल सहेजें, `javac` से कंपाइल करें, और `java MixedLanguageDemo` से चलाएँ। यदि सब कुछ सही ढंग से सेट है, तो आप कंसोल पर बहुभाषी टेक्स्ट प्रिंट होते देखेंगे।

## निष्कर्ष

अब आप जानते हैं **how to use Aspose** को **recognize text from image** फ़ाइलों के लिए जो कई भाषाएँ शामिल करती हैं, कैसे **enable automatic language detection** किया जाता है, और भाषा पूल को सीमित करके **improve OCR speed** का एक व्यावहारिक टिप। ऊपर दिया गया पूरा कोड कॉपी‑पेस्ट के लिए तैयार है, और व्याख्याएँ आपको समाधान को अनुकूलित करने का आत्मविश्वास देती हैं—चाहे आपको **load image for OCR** को स्ट्रीम, बाइट एरे, या यहाँ तक कि वेबकैम स्नैपशॉट से लेना हो।

अगले कदम? इन चीज़ों के साथ प्रयोग करें:

* कम गुणवत्ता वाले स्कैन के लिए इमेज प्री‑प्रोसेसिंग (डिनॉइज़, बिनराइज़) जोड़ना।  
* डाउनस्ट्रीम सेवाओं के लिए `OcrResult` को JSON के रूप में एक्सपोर्ट करना।  
* इंजन को Spring Boot REST एंडपॉइंट में इंटीग्रेट करना ताकि क्लाइंट इमेज अपलोड कर सकें और तुरंत निकाला गया टेक्स्ट प्राप्त कर सकें।

कोडिंग का आनंद लें, और आपकी OCR पाइपलाइन तेज़, सटीक और बहुभाषी हों!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}