---
category: general
date: 2026-03-07
description: जावा OCR के साथ छवि से टेक्स्ट निकालें। OCR के लिए छवि कैसे लोड करें,
  भाषा कैसे कॉन्फ़िगर करें, और कुछ ही मिनटों में पूर्ण जावा OCR ट्यूटोरियल चलाएँ,
  यह सीखें।
draft: false
keywords:
- extract text from image
- load image for ocr
- use OCR in java
- java ocr tutorial
language: hi
og_description: जावा OCR का उपयोग करके छवि से टेक्स्ट निकालें। यह ट्यूटोरियल दिखाता
  है कि OCR के लिए छवि कैसे लोड करें, भाषा कैसे कॉन्फ़िगर करें, और जावा OCR ट्यूटोरियल
  को चरण‑दर‑चरण चलाएँ।
og_title: जावा में छवि से पाठ निकालें – पूर्ण OCR गाइड
tags:
- OCR
- Java
- Image Processing
title: जावा में छवि से पाठ निकालें – जावा OCR ट्यूटोरियल
url: /hi/java/ocr-basics/extract-text-from-image-in-java-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में इमेज से टेक्स्ट निकालें – पूर्ण OCR गाइड

क्या आपको कभी **इमेज से टेक्स्ट निकालने** की ज़रूरत पड़ी है लेकिन जावा में कहाँ से शुरू करें, यह नहीं पता था? आप अकेले नहीं हैं—डेवलपर्स अक्सर स्कैन किए गए संकेत, रसीदें, या हाथ से लिखे नोट्स को सर्चेबल स्ट्रिंग्स में बदलते समय इस समस्या का सामना करते हैं।  

अच्छी खबर? केवल कुछ मिनटों में आप एक कार्यशील OCR पाइपलाइन बना सकते हैं जो कन्नड़, अंग्रेज़ी, या कोई भी समर्थित भाषा पढ़ सके। इस ट्यूटोरियल में हम **OCR के लिए इमेज लोड करेंगे**, इंजन को कॉन्फ़िगर करेंगे, और एक **जावा OCR ट्यूटोरियल** के माध्यम से चलेंगे जिसे आप आज ही कॉपी‑पेस्ट करके चला सकते हैं।

## इस गाइड में क्या कवर किया गया है

हम आवश्यक टूल्स की सूची से शुरू करेंगे, फिर सीधे एक **स्टेप‑बाय‑स्टेप** इम्प्लीमेंटेशन में डुबकी लगाएंगे। अंत तक आप सक्षम होंगे:

* जावा `ImageInputStream` में इमेज फ़ाइल लोड करना।
* एक विशिष्ट भाषा (हमारे उदाहरण में कन्नड़) को पहचानने के लिए OCR इंजन को कॉन्फ़िगर करना।
* पहचान प्रक्रिया चलाना और निकाले गए टेक्स्ट को प्रिंट करना।
* बेहतर सटीकता के लिए सेटिंग्स को ट्यून करना और सामान्य समस्याओं को संभालना।

कोई बाहरी दस्तावेज़ीकरण आवश्यक नहीं—आपको जो कुछ भी चाहिए वह यहाँ ही है।  

**Prerequisites**: Java 17 या नया, Maven या Gradle जैसा बिल्ड टूल, और एक OCR लाइब्रेरी जो `OcrEngine` क्लास प्रदान करती है (उदाहरण के लिए, काल्पनिक *SimpleOCR* SDK)। यदि आप Maven उपयोग कर रहे हैं, तो बाद में दिखाए गए डिपेंडेंसी को जोड़ें।

---

## चरण 1 – अपना प्रोजेक्ट सेट अप करें और OCR लाइब्रेरी जोड़ें

कोड लिखने से पहले, सुनिश्चित करें कि आपका प्रोजेक्ट OCR क्लासेज़ को देख सकता है। Maven के साथ, इस स्निपेट को अपने `pom.xml` में डालें:

```xml
<!-- Maven dependency for SimpleOCR (replace with your actual OCR SDK) -->
<dependency>
    <groupId>com.example</groupId>
    <artifactId>simple-ocr</artifactId>
    <version>1.4.2</version>
</dependency>
```

यदि आप Gradle पसंद करते हैं, तो समकक्ष यह है:

```gradle
implementation 'com.example:simple-ocr:1.4.2'
```

> **Pro tip:** लाइब्रेरी का संस्करण हमेशा अपडेट रखें; नए रिलीज़ अक्सर भाषा‑मॉडल सुधार लाते हैं जो सटीकता बढ़ाते हैं।

डिपेंडेंसी रिजॉल्व हो जाने के बाद, अपने IDE को रिफ्रेश करें और आप कोड लिखने के लिए तैयार हैं।

## चरण 2 – आवश्यक क्लासेज़ इम्पोर्ट करें

नीचे उदाहरण के लिए आवश्यक इम्पोर्ट्स की पूरी सूची दी गई है। इन्हें जानबूझकर न्यूनतम रखा गया है ताकि आप प्रत्येक क्लास क्या करता है, ठीक से देख सकें।

```java
import com.example.ocr.OcrEngine;      // Main OCR engine
import com.example.ocr.OcrResult;      // Holds recognition result
import com.example.io.ImageInputStream; // Wrapper for image files
import java.nio.file.Paths;             // Convenient path handling
import java.io.IOException;             // For proper exception handling
```

> **Why these imports?** `OcrEngine` और `OcrResult` OCR प्रक्रिया का दिल हैं, जबकि `ImageInputStream` फ़ाइल‑रीडिंग बायलरप्लेट को एब्स्ट्रैक्ट करता है। `java.nio.file.Paths` का उपयोग कोड को OS‑अग्नॉस्टिक बनाता है।

## चरण 3 – OCR के लिए इमेज लोड करें

अब वह भाग आता है जो अक्सर लोगों को उलझन में डाल देता है: इंजन को सही इमेज फ़ॉर्मेट देना। OCR SDK एक `ImageInputStream` की अपेक्षा करता है, जिसे आप डिस्क पर किसी भी फ़ाइल से प्राप्त कर सकते हैं।

```java
// Step 3: Load the image that contains the text you want to extract
String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));
```

> **Edge case:** यदि इमेज करप्टेड है या असमर्थित फ़ॉर्मेट (जैसे, GIF) में है, तो कंस्ट्रक्टर `IOException` थ्रो करेगा। कॉल को try‑catch ब्लॉक में रैप करें या पहले फ़ाइल को वैलिडेट करें।

## चरण 4 – इंजन को विशिष्ट भाषा पहचानने के लिए कॉन्फ़िगर करें

अधिकांश OCR इंजन मल्टी‑लैंग्वेज सपोर्ट के साथ आते हैं। सटीकता बढ़ाने के लिए आपको इंजन को ठीक-ठीक बताना चाहिए कि कौन सी भाषा देखनी है। हमारे केस में हम कन्नड़ के लिए भाषा कोड `"kn"` का उपयोग करते हैं।

```java
// Step 4: Create and configure the OCR engine for Kannada
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setLanguage("kn"); // 'kn' = Kannada
```

> **Why set the language?** कैरेक्टर सेट को सीमित करने से फॉल्स पॉज़िटिव कम होते हैं, विशेषकर उन स्क्रिप्ट्स के साथ काम करते समय जिनमें कई समान ग्लिफ़ होते हैं।

यदि आपको कभी भाषा बदलनी पड़े, तो बस कोड स्ट्रिंग बदलें—और कोई बदलाव आवश्यक नहीं।

## चरण 5 – OCR प्रक्रिया चलाएँ और टेक्स्ट निकालें

इमेज लोड हो जाने और इंजन कॉन्फ़िगर हो जाने के बाद, वास्तविक पहचान एक सिंगल मेथड कॉल है। रिज़ल्ट ऑब्जेक्ट आपको प्लेन टेक्स्ट और वैकल्पिक रूप से कॉन्फिडेंस स्कोर देता है।

```java
// Step 5: Run OCR and retrieve the recognized text
OcrResult ocrResult = ocrEngine.recognize(imageStream);
String extractedText = ocrResult.getText();
```

> **Common question:** *अगर OCR खाली स्ट्रिंग रिटर्न करता है तो क्या करें?*  
> आमतौर पर इसका मतलब है कि इमेज क्वालिटी बहुत कम है (ब्लर, लो कॉन्ट्रास्ट) या भाषा सही से सेट नहीं हुई। इमेज को प्री‑प्रोसेस करने की कोशिश करें (कॉन्ट्रास्ट बढ़ाएँ, बाइनराइज़ करें) या भाषा कोड को दोबारा चेक करें।

## चरण 6 – परिणाम दिखाएँ

अंत में, आउटपुट को कंसोल पर प्रिंट करें। वास्तविक एप्लिकेशन में आप इसे डेटाबेस में स्टोर कर सकते हैं या सर्च इंडेक्स में फीड कर सकते हैं।

```java
// Step 6: Output the recognized Kannada text
System.out.println("Extracted text:");
System.out.println(extractedText);
```

### अपेक्षित आउटपुट

यदि स्रोत इमेज में कन्नड़ वाक्यांश “ಕರ್ನಾಟಕ” (Karnataka) है, तो कंसोल में यह दिखना चाहिए:

```
Extracted text:
ಕರ್ನಾಟಕ
```

बस इतना ही—एक पूर्ण **जावा में OCR उपयोग** वर्कफ़्लो जो आप किसी भी भाषा या इमेज स्रोत के लिए अनुकूलित कर सकते हैं।

---

## पूर्ण कार्यशील उदाहरण

नीचे पूरा प्रोग्राम दिया गया है, जिसे कंपाइल करने के लिए तैयार है। `YOUR_DIRECTORY` को अपनी इमेज फ़ाइल के वास्तविक पाथ से बदलें।

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.nio.file.Paths;
import java.io.IOException;

public class KannadaOcrExample {
    public static void main(String[] args) {
        try {
            // Create OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Configure for Kannada (language code "kn")
            ocrEngine.getConfig().setLanguage("kn");

            // Load the image you want to extract text from
            String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
            ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));

            // Run the OCR process
            OcrResult ocrResult = ocrEngine.recognize(imageStream);

            // Print the extracted text
            System.out.println("Extracted text:");
            System.out.println(ocrResult.getText());
        } catch (IOException e) {
            System.err.println("Failed to load image or run OCR: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error during OCR: " + e.getMessage());
        }
    }
}
```

> **Tip:** प्रोडक्शन कोड के लिए, कई इमेजेज़ पर एक ही `OcrEngine` इंस्टेंस को पुनः उपयोग करने पर विचार करें; इसे बार‑बार बनाना महंगा हो सकता है।

---

## अक्सर पूछे जाने वाले प्रश्न & किनारे के केस

### शोरयुक्त फोटो पर सटीकता कैसे बढ़ाएँ?

- **Pre‑process** इमेज: ग्रेस्केल में बदलें, मीडियन फ़िल्टर लागू करें, या कॉन्ट्रास्ट बढ़ाएँ।
- **Resize** इमेज को कम से कम 300 DPI पर रीसाइज़ करें; अधिकांश OCR इंजन इस रिज़ॉल्यूशन की अपेक्षा करते हैं।
- **Set a whitelist** कैरेक्टर्स की यदि आप अपेक्षित आउटपुट जानते हैं (जैसे, केवल अंक)।

### क्या मैं इस अप्रोच को PDFs के लिए उपयोग कर सकता हूँ?

हां। प्रत्येक पेज को इमेज के रूप में एक्सट्रैक्ट करें (PDFBox या iText का उपयोग करके), फिर उन इमेजेज़ को उसी पाइपलाइन में फीड करें। कोड समान रहता है; केवल इमेज‑स्रोत बदलता है।

### यदि मुझे एक इमेज में कई भाषाएँ पहचाननी हों तो क्या करें?

अधिकांश SDK आपको कॉमा‑सेपरेटेड लिस्ट पास करने देते हैं, जैसे `"en,kn"`। इंजन प्रदान किए गए किसी भी स्क्रिप्ट से मेल करने की कोशिश करेगा।

### क्या कॉन्फिडेंस स्कोर प्राप्त करने का कोई तरीका है?

`OcrResult` अक्सर एक `getConfidence()` मेथड शामिल करता है जो प्रत्येक लाइन के लिए 0 से 1 के बीच का फ़्लोट रिटर्न करता है। इसका उपयोग लो‑कॉन्फिडेंस रिज़ल्ट्स को फ़िल्टर करने के लिए करें।

---

## अगले कदम

अब जब आप जावा का उपयोग करके **इमेज से टेक्स्ट निकाल सकते हैं**, आप निम्नलिखित का अन्वेषण कर सकते हैं:

- **Batch processing** – इमेजेज़ के फ़ोल्डर पर लूप चलाएँ और परिणाम CSV में लिखें।
- **Integration with Apache Tika** – OCR को डॉक्यूमेंट पार्सिंग के साथ मिलाकर एकीकृत सर्च इंडेक्स बनाएं।
- **Server‑side API** – OCR लॉजिक को REST एंडपॉइंट (Spring Boot इसे आसान बनाता है) के माध्यम से एक्सपोज़ करें।
- **Alternative libraries** – यदि आपको ओपन‑सोर्स समाधान चाहिए तो `tess4j` के माध्यम से Tesseract आज़माएँ।

इनमें से प्रत्येक विषय इस **java ocr tutorial** में कवर किए गए कोर कॉन्सेप्ट्स पर आधारित है, इसलिए कोड के साथ प्रयोग करने और उसे विस्तारित करने में संकोच न करें।

---

## निष्कर्ष

हमने एक पूर्ण जावा उदाहरण के माध्यम से चलकर दिखाया है कि कैसे **इमेज से टेक्स्ट निकाला** जाता है, बिल्कुल कैसे **OCR के लिए इमेज लोड करें**, भाषा सेटिंग्स कॉन्फ़िगर करें, और **जावा में OCR उपयोग करें** ताकि पठनीय स्ट्रिंग्स प्राप्त हो सकें। यह स्निपेट सेल्फ‑कंटेन्ड है, त्रुटियों को सुगमता से संभालता है, और न्यूनतम झंझट के साथ किसी भी जावा प्रोजेक्ट में डाला जा सकता है।  

इसे चलाएँ, भाषा कोड को ट्यून करें, और जल्द ही आप स्कैन किए गए दस्तावेज़ों को सर्चेबल डेटा में बदलते देखेंगे बिना किसी परेशानी के। कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}