---
category: general
date: 2026-10-30
description: Aspose OCR Java का उपयोग करके इमेज से टेक्स्ट निकालें – जानें कैसे PNG
  को टेक्स्ट में बदलें, OCR के लिए इमेज लोड करें, और Java OCR ट्यूटोरियल का पालन करें।
draft: false
keywords:
- convert png to text
- ocr image to text
- extract text from png
- aspose ocr java
- extract text image java
lastmod: 2026-10-30
og_description: Aspose OCR Java के साथ इमेज से टेक्स्ट निकालें। इस स्टेप‑बाय‑स्टेप
  Java OCR ट्यूटोरियल का पालन करें ताकि PNG को टेक्स्ट में बदला जा सके, OCR के लिए
  इमेज लोड की जा सके, और बहुभाषी कंटेंट को प्रभावी ढंग से संभाला जा सके।
og_image_alt: Screenshot of Java OCR code converting PNG to text using Aspose OCR
og_title: Java OCR के साथ PNG को टेक्स्ट में बदलें – Aspose गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: extract text from image using Aspose OCR Java – learn how to convert
    PNG to text, load image for OCR, and follow a java ocr tutorial.
  headline: Extract text from image – convert PNG to text in Java
  type: TechArticle
- questions:
  - answer: Yes, a commercial license is required for production use; a free trial
      is available for evaluation.
    question: Can I use Aspose OCR in a commercial application without extra licensing
      fees?
  - answer: Absolutely. The library includes language packs for Arabic, Hebrew, Persian,
      and other RTL scripts.
    question: Does Aspose OCR support right‑to‑left scripts such as Arabic or Hebrew?
  - answer: Aspose OCR can process images up to 10 000 × 10 000 pixels using streaming
      mode, which keeps memory usage under 200 MB.
    question: How large of an image can the engine handle?
  - answer: Yes, `OcrResult.getWords()` returns a collection where each word has a
      `getConfidence()` method.
    question: Is there a way to get confidence scores for each recognized word?
  - answer: The library supports JDK 8, 11, 17, and later LTS releases.
    question: What Java versions are officially supported?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- Image Processing
title: इमेज से टेक्स्ट निकालें – Java में PNG को टेक्स्ट में बदलें
url: /hi/java/ocr-basics/extract-text-from-image-convert-png-to-text-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# छवि से टेक्स्ट निकालें – जावा में PNG को टेक्स्ट में बदलें

क्या आपको कभी **छवि से टेक्स्ट निकालने** की ज़रूरत पड़ी है लेकिन यह नहीं पता था कि कौन सी लाइब्रेरी बिना झंझट के यह काम कर सके? आप अकेले नहीं हैं—डेवलपर्स लगातार पूछते हैं, “जावा में PNG को टेक्स्ट में कैसे बदलें?” अच्छी खबर यह है कि Aspose OCR पूरी प्रक्रिया को आसान बना देता है। इस गाइड में हम एक पूर्ण **जावा OCR ट्यूटोरियल** के माध्यम से चलेंगे, आपको दिखाएंगे कि **OCR के लिए छवि लोड करें** कैसे करें, और अंत में साफ़, खोजने योग्य टेक्स्ट प्राप्त करेंगे।

हम इंजन सेटअप से लेकर बहुभाषी सामग्री को संभालने तक सब कुछ कवर करेंगे, इसलिए अंत तक आप किसी भी आकार, फ़ॉर्मेट या भाषा की **PNG को टेक्स्ट में बदलें** फ़ाइलें बना सकेंगे। कोई बाहरी सेवाएँ नहीं, कोई API कुंजी नहीं—सिर्फ एक JAR और कुछ लाइनों का कोड।

## त्वरित उत्तर
- **जावा में PNG को टेक्स्ट में बदलने वाली कौन सी लाइब्रेरी?** Aspose OCR for Java.  
- **बेसिक कन्वर्ज़न के लिए कितनी कोड लाइनों की आवश्यकता है?** लाइब्रेरी जोड़ने के बाद लगभग पाँच लाइनों की आवश्यकता होती है।  
- **क्या Aspose OCR अंग्रेज़ी के अलावा अन्य भाषाओं का समर्थन करता है?** हाँ—70 से अधिक भाषा पैक्स, जिसमें खमेर, चीनी, अरबी और अन्य शामिल हैं।  
- **क्या मैं OCR इंजन ऑफ़लाइन चला सकता हूँ?** बिल्कुल; इंजन पूरी तरह से ऑन‑प्रिमाइसेस काम करता है, बिना इंटरनेट कनेक्शन के।  
- **किस जावा संस्करण की आवश्यकता है?** JDK 8 या नया; JDK 11+ पूरी तरह समर्थित है।

## PNG को टेक्स्ट में बदलना क्या है?
**PNG को टेक्स्ट में बदलना** का मतलब है PNG छवि के भीतर दिखाई देने वाले टेक्स्ट कैरेक्टर्स को निकालना और उन्हें एक साधारण‑टेक्स्ट स्ट्रिंग में बदलना जिसे आप संपादित, खोज या संग्रहित कर सकते हैं। इस प्रक्रिया को आमतौर पर ऑप्टिकल कैरेक्टर रिकग्निशन (OCR) कहा जाता है। यह पिक्सेल पैटर्न का विश्लेषण करके और उन्हें भाषा‑विशिष्ट शब्दकोशों से मिलाकर काम करता है, जिससे स्कैन किए गए दस्तावेज़, स्क्रीनशॉट या किसी भी बिटमैप में पढ़ने योग्य टेक्स्ट को संपादन योग्य डेटा में बदलना संभव होता है।

## जावा के लिए Aspose OCR क्यों उपयोग करें?
Aspose OCR **50+ इनपुट फ़ॉर्मेट** (जैसे PNG, JPEG, BMP, TIFF) का समर्थन करता है और **सैकड़ों‑पृष्ठ दस्तावेज़** को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस कर सकता है, इसके स्ट्रीमिंग आर्किटेक्चर के कारण। लाइब्रेरी **70+ भाषा पैक्स** प्रदान करती है, उच्च‑रिज़ॉल्यूशन स्कैन पर **95 % तक की सटीकता** देती है, और यह मासिक अपडेट प्राप्त करती है जो नई स्क्रिप्ट और प्रदर्शन सुधार जोड़ते हैं।

## आपको क्या चाहिए
- JDK 8 या नया स्थापित हो (कोड JDK 11+ पर भी काम करता है)।  
- Maven या Gradle का उपयोग करके Aspose OCR लाइब्रेरी प्राप्त करें, या आप Aspose वेबसाइट से JAR मैन्युअली डाउनलोड कर सकते हैं।  
- एक PNG छवि जिसमें कुछ पढ़ने योग्य टेक्स्ट हो (हमारे उदाहरण के लिए हम `khmer-sign.png` का उपयोग करेंगे)।  
- एक IDE या टेक्स्ट एडिटर जिसमें आप सहज हों—IntelliJ IDEA, Eclipse, VS Code, कोई भी चलेगा।  

बस इतना ही। कोई भारी फ्रेमवर्क नहीं, कोई क्लाउड क्रेडेंशियल नहीं। तैयार हैं? चलिए छवि फ़ाइलों से टेक्स्ट निकालना शुरू करते हैं।

## अपने प्रोजेक्ट में Aspose OCR कैसे जोड़ें?
OCR इंजन को अपने बिल्ड कॉन्फ़िगरेशन में जोड़ें ताकि क्लासेस कंपाइल टाइम पर उपलब्ध हों। यह चरण सुनिश्चित करता है कि Aspose OCR JAR और उसकी डिपेंडेंसीज़ सही ढंग से रेफ़रेंसेड हों, जिससे आप अपने जावा स्रोत फ़ाइलों में आवश्यक पैकेज इम्पोर्ट कर सकें। एक बार डिपेंडेंसी घोषित हो जाने पर, Maven या Gradle लाइब्रेरी को सेंट्रल रिपॉज़िटरी से डाउनलोड करेगा और कंपाइलेशन व रनटाइम एक्ज़ीक्यूशन के लिए क्लासपाथ पर रखेगा।

**Maven** – `pom.xml` में यह डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check the latest version on Maven Central -->
</dependency>
```

**Gradle** – अपने `build.gradle` में निम्न पंक्ति जोड़ें:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

यदि आप मैन्युअल तरीका पसंद करते हैं, तो Aspose डाउनलोड पेज से JAR डाउनलोड करें और इसे अपने प्रोजेक्ट के `libs` फ़ोल्डर में डालें, फिर इसे बिल्ड पाथ में जोड़ें।

> **Pro tip:** हमेशा नवीनतम स्थिर संस्करण चुनें; पुराने रिलीज़ में भाषा पैक्स या बग‑फिक्सेज़ नहीं हो सकते।

## OCR इंजन इंस्टेंस कैसे बनाएं?
OcrEngine वह कोर क्लास है जो OCR पहचान करता है। यह सभी आंतरिक बफ़र्स, भाषा डेटा, और प्रोसेसिंग सेटिंग्स को समेटे रहता है जो छवि पिक्सेल को टेक्स्ट में बदलने के लिए आवश्यक हैं। प्रत्येक ऑपरेशन के लिए एक नया इंस्टेंस बनाना निश्चित परिणाम सुनिश्चित करता है, विशेषकर जब आप रन के बीच भाषाओं या प्रोसेसिंग मोड्स को बदलते हैं।

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        // ... further steps will follow
    }
}
```

हम हर बार नया इंजन क्यों बनाते हैं? क्योंकि इंजन भाषा शब्दकोशों को कैश करता है; इसे रीसेट करने से विभिन्न भाषा स्कैन के बीच क्रॉस‑कंटैमिनेशन रोकता है।

## इच्छित भाषा कैसे सक्षम करें (वैकल्पिक लेकिन अनुशंसित)?
OcrLanguage वह विशिष्ट भाषा शब्दकोश दर्शाता है जिसे इंजन पहचान के दौरान उपयोग करता है। उपयुक्त भाषा का चयन सर्च स्पेस को घटाता है, प्रोसेसिंग को तेज़ करता है, और इमेज में अपेक्षित कैरेक्टर सेट पर फोकस करके सटीकता बढ़ाता है।

`OcrLanguage` एक विशिष्ट भाषा शब्दकोश दर्शाता है। हमारे उदाहरण में हम खमेर (`khm`) को सक्षम करेंगे, लेकिन आप इसे `ENG` (अंग्रेज़ी), `CHN` (चीनी) आदि से बदल सकते हैं।

```java
// Enable Khmer language support (ISO 639‑2 code "khm")
ocrEngine.getLanguages().add(OcrLanguage.KHM);
```

> **यह क्यों महत्वपूर्ण है:** जब आप **OCR के लिए छवि लोड करें**, इंजन केवल सक्षम भाषा शब्दकोशों को खोजेगा। सभी भाषाओं को चालू छोड़ने से प्रक्रिया धीमी हो सकती है और फॉल्स पॉज़िटिव्स बढ़ सकते हैं।

## OCR के लिए छवि लोड कैसे करें – PNG को टेक्स्ट में बदलना
ImageStream एक रैपर है जो इमेज फ़ाइल को OCR इंजन के साथ संगत स्ट्रीम में पढ़ता है, फ़ॉर्मेट डिटेक्शन को स्वचालित रूप से संभालता है। यह लो‑लेवल I/O को एब्स्ट्रैक्ट करता है, जिससे आप फ़ाइल हैंडलिंग विवरणों की चिंता किए बिना एक सरल ऑब्जेक्ट को इंजन को पास कर सकते हैं।

ImageStream एक रैपर है जो इमेज फ़ाइल को OCR इंजन के साथ संगत स्ट्रीम में पढ़ता है, फ़ॉर्मेट डिटेक्शन को स्वचालित रूप से संभालता है।

```java
// Load the PNG that contains the text you want to extract
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));
```

यदि आपकी छवि किसी अन्य फ़ॉर्मेट (JPEG, BMP, TIFF) में है, तो वही मेथड काम करता है—Aspose स्वचालित रूप से फ़ॉर्मेट का पता लगाता है। बस यह सुनिश्चित करें कि फ़ाइल पाथ सही है; अन्यथा आपको `FileNotFoundException` मिलेगा।

## OCR प्रक्रिया कैसे चलाएँ और PNG को टेक्स्ट में बदलें?
OcrResult पहचान ऑपरेशन का परिणाम रखता है, जिसमें निकाला गया टेक्स्ट और प्रत्येक कैरेक्टर या शब्द के लिए कॉन्फिडेंस मेट्रिक्स शामिल हैं। इंजन पर `recognize()` मेथड कॉल करने के बाद, आपको एक OcrResult ऑब्जेक्ट मिलता है जिसे आप रॉ स्ट्रिंग और अतिरिक्त विवरणों के लिए क्वेरी कर सकते हैं।

`ocrEngine.recognize()` एक `OcrResult` लौटाता है जिसमें निकाली गई स्ट्रिंग के लिए `getText()` और प्रति‑कैरेक्टर कॉन्फिडेंस मेट्रिक के लिए `getConfidence()` होता है।

```java
// Run OCR and fetch the recognized text
String recognizedText = ocrEngine.recognize().getText();
```

बस इतना ही—आपने अभी **PNG को टेक्स्ट में बदलें**। लौटाई गई स्ट्रिंग में लाइन ब्रेक और व्हाइटस्पेस वही हो सकते हैं जैसा इंजन ने देखा। आप इसे `trim()`, `replaceAll("\\s+", " ")` या किसी भी अन्य क्लीन‑अप के साथ पोस्ट‑प्रोसेस कर सकते हैं।

## परिणाम कैसे आउटपुट करें (या सहेजें)?
Result OcrResult का एक इंस्टेंस है जो `getText()` के माध्यम से पहचाना गया टेक्स्ट प्रदान करता है। कंसोल में परिणाम प्रिंट करना OCR की सफलता की जल्दी जाँच करने का तरीका है, जबकि प्रोडक्शन में आप टेक्स्ट को फ़ाइल, डेटाबेस या किसी अन्य सर्विस में लिख सकते हैं।

`System.out.println(result.getText());` निकाले गए टेक्स्ट को प्रिंट करता है।

```java
System.out.println("Recognized text:");
System.out.println(recognizedText);
```

**अपेक्षित आउटपुट** (प्रदान किए गए खमेर साइन के लिए) इस प्रकार दिख सकता है:

```
សួស្តី
Welcome
```

यदि आउटपुट गड़बड़ है, तो चरण 3 में सही भाषा सक्षम की है या नहीं और छवि बहुत धुंधली तो नहीं, दोबारा जांचें। इमेज रिज़ॉल्यूशन बढ़ाने (जैसे 300 dpi स्कैन) से अक्सर मदद मिलती है।

## पूरा कार्यशील उदाहरण कैसा दिखता है?
नीचे एक स्व-निहित जावा प्रोग्राम है जो डिपेंडेंसी जोड़ने से लेकर OCR परिणाम प्रिंट करने तक हर चरण दर्शाता है। क्लास `ExtractTextExample` में एक `main` मेथड है जो इंजन बनाता है, भाषा सेट करता है, छवि लोड करता है, पहचान चलाता है, और टेक्स्ट आउटपुट करता है। आप इस कोड को `ExtractTextExample.java` नाम की फ़ाइल में कॉपी‑पेस्ट करके सीधे चला सकते हैं।

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable the language you need (Khmer in this case)
        ocrEngine.getLanguages().add(OcrLanguage.KHM);

        // 3️⃣ Load the PNG image you want to extract text from
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));

        // 4️⃣ Run OCR – this step actually converts PNG to text
        String recognizedText = ocrEngine.recognize().getText();

        // 5️⃣ Show the result
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

प्रोग्राम चलाएँ:

```bash
mvn compile exec:java -Dexec.mainClass=ExtractTextExample
```

या, यदि आप Gradle उपयोग कर रहे हैं:

```bash
./gradlew run --args='ExtractTextExample'
```

आपको कंसोल में निकाला गया टेक्स्ट प्रिंट होता दिखेगा, जो पुष्टि करता है कि आपने Aspose OCR का उपयोग करके सफलतापूर्वक **छवि से टेक्स्ट निकालें** किया है।

## सामान्य समस्याएँ और उन्हें कैसे ठीक करें
| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| खाली स्ट्रिंग लौटाई गई | कोई भाषा सक्षम नहीं या गलत भाषा कोड | उपयुक्त `OcrLanguage` जोड़ें (जैसे, अंग्रेज़ी के लिए `ENG`)। |
| गड़बड़ अक्षर | छवि रिज़ॉल्यूशन बहुत कम या शोरयुक्त पृष्ठभूमि | उच्च‑रिज़ॉल्यूशन स्रोत उपयोग करें, या शार्पनिंग फ़िल्टर से पूर्व‑प्रसंस्करण करें। |
| `OutOfMemoryError` | बहुत बड़ी छवि पूरी साइज में लोड हुई | इंजन को फीड करने से पहले छवि को डाउनस्केल करें (`ImageStream.fromFile(...).scale(0.5)`)। |
| `FileNotFoundException` | गलत पाथ | एब्सोल्यूट या रिलेटिव पाथ सत्यापित करें; `Paths.get(...).toAbsolutePath()` का उपयोग करें। |

> **याद रखें:** OCR एक प्रायिक प्रक्रिया है। पूरी सेटिंग्स के साथ भी आपको कुछ अक्षरों को मैन्युअली सुधारना पड़ सकता है, विशेषकर कर्सिव स्क्रिप्ट्स के लिए।

## इस ट्यूटोरियल के बाद आप कौन से अगले कदम उठा सकते हैं?
- **Batch processing:** PNG फ़ाइलों की डायरेक्टरी पर लूप करें, प्रत्येक छवि के लिए वही लॉजिक कॉल करें।  
- **PDF output:** निकाले गए टेक्स्ट को फिर से एक सर्चेबल PDF में एम्बेड करने के लिए Aspose PDF का उपयोग करें।  
- **Language detection:** भाषा सेट करने से पहले `ocrEngine.detectLanguage()` कॉल करें ताकि इंजन स्वचालित रूप से अनुमान लगा सके।  
- **Cloud integration:** कोड को एक REST एंडपॉइंट में रैप करें और माइक्रो‑सर्विसेज को स्केलेबल OCR सर्विसेज़ के लिए कॉल करने दें।

इन सभी विषयों का निर्माण हमने अभी पूरा किया **जावा OCR ट्यूटोरियल** पर आधारित है, और ये दिखाते हैं कि Aspose OCR API कितनी बहुमुखी है।

## अक्सर पूछे जाने वाले प्रश्न
**Q: क्या मैं Aspose OCR को व्यावसायिक एप्लिकेशन में अतिरिक्त लाइसेंस शुल्क के बिना उपयोग कर सकता हूँ?**  
A: हाँ, उत्पादन उपयोग के लिए एक व्यावसायिक लाइसेंस आवश्यक है; मूल्यांकन के लिए एक मुफ्त ट्रायल उपलब्ध है।

**Q: क्या Aspose OCR अरबी या हिब्रू जैसी दाएँ‑से‑बाएँ स्क्रिप्ट्स का समर्थन करता है?**  
A: बिल्कुल। लाइब्रेरी में अरबी, हिब्रू, फ़ारसी और अन्य RTL स्क्रिप्ट्स के लिए भाषा पैक्स शामिल हैं।

**Q: इंजन कितनी बड़ी छवि संभाल सकता है?**  
A: Aspose OCR स्ट्रीमिंग मोड का उपयोग करके 10 000 × 10 000 पिक्सेल तक की छवियों को प्रोसेस कर सकता है, जिससे मेमोरी उपयोग 200 MB से कम रहता है।

**Q: क्या प्रत्येक पहचाने गए शब्द के लिए कॉन्फिडेंस स्कोर प्राप्त करने का कोई तरीका है?**  
A: हाँ, `OcrResult.getWords()` एक कलेक्शन लौटाता है जहाँ प्रत्येक शब्द का `getConfidence()` मेथड होता है।

**Q: आधिकारिक तौर पर कौन से जावा संस्करण समर्थित हैं?**  
A: लाइब्रेरी JDK 8, 11, 17, और बाद के LTS रिलीज़ को समर्थन देती है।

## निष्कर्ष
हमने एक पूर्ण **जावा OCR ट्यूटोरियल** के माध्यम से चलकर दिखाया है जो आपको **छवि से टेक्स्ट निकालें** फ़ाइलें, **PNG को टेक्स्ट में बदलें**, और Aspose OCR का उपयोग करके सही ढंग से **OCR के लिए छवि लोड करें** देता है। चरण सरल हैं: लाइब्रेरी जोड़ें, एक इंजन बनाएं, सही भाषा सक्षम करें, PNG लोड करें, `recognize()` चलाएँ, और आउटपुट को संभालें। इस आधार के साथ आप डेटा एंट्री को ऑटोमेट कर सकते हैं, सर्चेबल आर्काइव बना सकते हैं, या किसी भी एप्लिकेशन को शक्ति दे सकते हैं जिसे चित्रों से मशीन‑रीडेबल टेक्स्ट चाहिए।

इसे अपने स्वयं के चित्रों के साथ आज़माएँ—शायद रसीद का स्क्रीनशॉट या स्कैन किया हुआ कॉन्ट्रैक्ट। भाषा सेटिंग्स को समायोजित करें, रिज़ॉल्यूशन के साथ प्रयोग करें, और आप जल्दी देखेंगे कि समाधान कितना लचीला है। यदि आपको समस्या आती है, तो फिर से समस्याओं की तालिका देखें या Aspose की आधिकारिक दस्तावेज़ीकरण देखें; यह विस्तृत और अद्यतन रहता है।

कोडिंग का आनंद लें, और आपका अगला प्रोजेक्ट साफ़, सर्चेबल टेक्स्ट से भरपूर हो!

---

**अंतिम अद्यतन:** 2026-10-30  
**परीक्षित संस्करण:** Aspose OCR for Java 24.10  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल
- [छवि से टेक्स्ट निकालें जावा – OCR के लिए छवि लोड करें](/ocr/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/)
- [Aspose OCR जावा उदाहरण – इमेज को तेज़ी से टेक्स्ट में बदलें](/ocr/java/ocr-operations/aspose-ocr-java-example-convert-image-to-text-fast/)
- [बैच इमेज OCR जावा – PNG फ़ाइलों से तेज़ी से टेक्स्ट निकालें](/ocr/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}