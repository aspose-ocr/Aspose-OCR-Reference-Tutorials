---
category: general
date: 2026-02-17
description: जावा में OCR का उपयोग करके इमेज फ़ाइलों से टेक्स्ट पहचानना, PNG रसीदों
  से टेक्स्ट निकालना और Aspose OCR के साथ रसीद को JSON में बदलना सीखें।
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: hi
og_description: जावा में OCR का उपयोग करके इमेज से टेक्स्ट पहचानने, PNG रसीदों से
  टेक्स्ट निकालने और रसीद को JSON में बदलने के लिए चरण‑दर‑चरण गाइड।
og_title: जावा में OCR का उपयोग कैसे करें – छवि से टेक्स्ट पहचानें
tags:
- OCR
- Java
- Aspose
- Image Processing
title: जावा में OCR का उपयोग कैसे करें – छवि से तेज़ी से टेक्स्ट पहचानें
url: /hi/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

from Image Quickly" => "Java में OCR कैसे उपयोग करें – छवि से टेक्स्ट जल्दी पहचानें". We'll translate.

Proceed paragraph.

We'll translate each paragraph.

Let's produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में OCR कैसे उपयोग करें – छवि से टेक्स्ट जल्दी पहचानें

क्या आपने कभी **OCR का उपयोग करके** रसीद की फोटो से टेक्स्ट निकालने के बारे में सोचा है? शायद आपने कुछ ऑनलाइन टूल आज़माए, लेकिन गड़बड़ अक्षर या ऐसे फॉर्मेट मिले जिन्हें आप प्रोसेस नहीं कर पाए। अच्छी खबर यह है कि कुछ ही लाइनों के Java कोड से आप **छवि से टेक्स्ट पहचान** सकते हैं, **PNG रसीदों से टेक्स्ट निकाल** सकते हैं, और यहाँ तक कि **रसीद को JSON में बदल** सकते हैं ताकि आगे की प्रोसेसिंग आसान हो जाए।  

इस ट्यूटोरियल में हम पूरी वर्कफ़्लो को कवर करेंगे—Aspose OCR लाइब्रेरी को लाइसेंस करने से लेकर एक साफ़ JSON पेलोड प्राप्त करने तक, जिसे आप डेटाबेस या मशीन‑लर्निंग मॉडल में फीड कर सकते हैं। कोई फालतू बातें नहीं, सिर्फ एक प्रैक्टिकल, रन‑एबल उदाहरण जो आप अपने IDE में कॉपी‑पेस्ट कर सकते हैं। अंत तक आपके पास एक सेल्फ‑कंटेन्ड प्रोग्राम होगा जो `receipt.png` लेगा और तैयार‑to‑use JSON स्ट्रिंग आउटपुट करेगा।

## आपको क्या चाहिए

- **Java Development Kit (JDK) 8+** – कोई भी हालिया संस्करण चलेगा।  
- **Aspose OCR for Java** लाइब्रेरी (Maven आर्टिफैक्ट `com.aspose:aspose-ocr`)।  
- एक **वैध Aspose OCR लाइसेंस फ़ाइल** (`Aspose.OCR.lic`)। फ्री ट्रायल टेस्टिंग के लिए चलती है, लेकिन उचित लाइसेंस मूल्यांकन सीमाओं को हटाता है।  
- एक इमेज फ़ाइल (PNG, JPEG, आदि) जिसमें वह टेक्स्ट हो जिसे आप पढ़ना चाहते हैं—इसे हम `receipt.png` कहेंगे और इसे किसी ज्ञात फ़ोल्डर में रखें।  
- आपका पसंदीदा IDE (IntelliJ IDEA, Eclipse, VS Code…) – आप जो चाहें चुन सकते हैं।

> **Pro tip:** लाइसेंस फ़ाइल को सोर्स फ़ोल्डर के बाहर रखें और इसे एब्सोल्यूट या रिलेटिव पाथ से रेफ़रेंस करें ताकि वह वर्ज़न कंट्रोल में कमिट न हो।

अब जब प्री‑रिक्विज़िट स्पष्ट हैं, चलिए असली कोड की ओर बढ़ते हैं।

## OCR का उपयोग कैसे करें – मुख्य चरण

नीचे उन कार्यों का हाई‑लेवल ओवरव्यू दिया गया है जो हम करेंगे:

1. **Aspose OCR लाइब्रेरी लोड** करें और अपना लाइसेंस लागू करें।  
2. **`OcrEngine` इंस्टेंस बनाएं** – यह वही इंजन है जो भारी काम करता है।  
3. **`OcrInput` ऑब्जेक्ट तैयार करें** जो उस इमेज की ओर इशारा करता है जिसे आप प्रोसेस करना चाहते हैं।  
4. **`recognize` को `ResultFormat.JSON` के साथ कॉल** करें ताकि निकाले गए टेक्स्ट का JSON प्रतिनिधित्व मिल सके।  
5. **JSON आउटपुट को हैंडल करें** – प्रिंट करें, फ़ाइल में लिखें, या आगे पार्स करें।

इन चरणों की विस्तृत व्याख्या आगे के सेक्शन में दी गई है।

## चरण 1 – Aspose OCR इंस्टॉल करें और लाइसेंस लागू करें

पहले, यदि आप Maven उपयोग कर रहे हैं तो अपने `pom.xml` में Aspose OCR डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

अब, अपने Java कोड में लाइसेंस लोड करें। यह कदम अत्यंत महत्वपूर्ण है; बिना लाइसेंस के लाइब्रेरी इवैल्यूएशन मोड में चलती है और आउटपुट में वॉटरमार्क जोड़ सकती है।

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **यह क्यों महत्वपूर्ण है:** `License` ऑब्जेक्ट OCR इंजन को बताता है कि आप पूरी फीचर सेट (हाई‑एक्यूरेसी रिकग्निशन और JSON एक्सपोर्ट सहित) का उपयोग करने के लिए अधिकृत हैं। इस स्टेप को स्किप करने से आप **छवि से टेक्स्ट पहचान** पाएँगे, लेकिन परिणाम थ्रॉटल हो सकते हैं।

## चरण 2 – OCR इंजन इंस्टेंस बनाएं

`OcrEngine` क्लास सभी OCR ऑपरेशन्स का एंट्री पॉइंट है। इसे आप “ब्रेन” समझ सकते हैं जो पिक्सेल पढ़ता है और तय करता है कि कौन से कैरेक्टर हैं।

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

बाद में आप इंजन को कस्टमाइज़ कर सकते हैं (जैसे भाषा सेट करना, डेस्क्यू एनेबल करना) अगर आपकी रसीदें नॉन‑लैटिन स्क्रिप्ट्स वाली हों या कोण पर स्कैन की गई हों। अधिकांश US‑बेस्ड रसीदों के लिए डिफॉल्ट सेटिंग्स ठीक रहती हैं।

## चरण 3 – वह इमेज लोड करें जिसे आप प्रोसेस करना चाहते हैं

अब हम OCR इंजन को उस फ़ाइल की ओर इशारा करेंगे जिसमें रसीद है। `OcrInput` क्लास कई इमेजेज़ को स्वीकार कर सकता है, लेकिन इस ट्यूटोरियल में हम एक ही PNG को सरलता से उपयोग करेंगे।

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

यदि आपको **PNG फ़ाइलों से टेक्स्ट निकाल**ना बड़े पैमाने पर करना है, तो बस `input.add()` को बार‑बार कॉल करें या फ़ाइल पाथ की लिस्ट पास करें।

## चरण 4 – टेक्स्ट पहचानें और रसीद को JSON में बदलें

यह ट्यूटोरियल का मुख्य भाग है। हम इंजन को टेक्स्ट पहचानने और परिणाम को JSON फॉर्मेट में देने के लिए कहते हैं। `ResultFormat.JSON` फ़्लैग हमारे लिए सारी मेहनत कर देता है।

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

JSON पेलोड में प्रत्येक पहचानी गई लाइन, उसका बाउंडिंग बॉक्स, कॉन्फिडेंस स्कोर, और रॉ टेक्स्ट शामिल होता है। यह स्ट्रक्चर **रसीद को JSON में बदल**ना बेहद आसान बनाता है, जिससे आप इसे किसी भी डाउनस्ट्रीम API में फीड कर सकते हैं।

## चरण 5 – सब कुछ मिलाकर प्रोग्राम चलाएँ

नीचे पूरा, तैयार‑to‑run Java क्लास दिया गया है जो सभी चीज़ों को जोड़ता है। इसे `JsonExportDemo.java` (या अपनी पसंद का कोई नाम) के रूप में सेव करें और अपने IDE या कमांड लाइन से रन करें।

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### अपेक्षित आउटपुट

प्रोग्राम चलाने पर एक JSON स्ट्रिंग प्रिंट होगी जो नीचे दिखाए गए जैसा होगा (सटीक सामग्री आपकी रसीद पर निर्भर करेगी):

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

अब आप इस JSON को डेटाबेस, REST एन्डपॉइंट, या डेटा‑एनालिसिस पाइपलाइन में फीड कर सकते हैं। **रसीद को JSON में बदल**ने का कदम पहले ही पूरा हो चुका है।

## सामान्य प्रश्न और एज केस

### अगर इमेज घुमा हुआ हो तो क्या करें?

Aspose OCR हल्की घुमाव को ऑटोमैटिकली डिटेक्ट और करेक्ट कर लेता है। बहुत ज़्यादा स्क्यूड इमेज के लिए, पहचान से पहले `engine.getImagePreprocessingOptions().setDeskew(true)` कॉल करें।

### कई भाषाओं को कैसे हैंडल करें?

`engine.getLanguage()` का उपयोग करके इच्छित भाषा सेट करें, उदाहरण के लिए `engine.setLanguage(Language.FRENCH)`। यह तब उपयोगी है जब आपको **छवि से टेक्स्ट पहचान**ना हो जिसमें मल्टी‑लैंग्वेज रसीदें हों।

### क्या मैं JSON की बजाय प्लेन टेक्स्ट आउटपुट कर सकता हूँ?

बिल्कुल। `ResultFormat.JSON` को `ResultFormat.TEXT` से बदलें और `result.getText()` कॉल करें।

### क्या OCR को किसी विशेष रीजन तक सीमित किया जा सकता है?

हां—`ocrInput.add(imagePath, new Rectangle(x, y, width, height))` का उपयोग करके आप रसीद के क्षेत्र पर फोकस कर सकते हैं, जिससे स्पीड और एक्यूरेसी दोनों बेहतर होते हैं।

## प्रोडक्शन‑रेडी OCR के लिए प्रो टिप्स

- **लाइसेंस ऑब्जेक्ट को कैश करें** यदि आप लूप में कई फ़ाइलें प्रोसेस कर रहे हैं; बार‑बार बनाना ओवरहेड बढ़ाता है।  
- **बैच प्रोसेस**: सभी रसीद पाथ को एक ही `OcrInput` में लोड करें और एक बार `recognize` कॉल करें। JSON में पेजेज़ की एरे होगी, प्रत्येक में अपनी लाइन्स होंगी।  
- **JSON वैलिडेट करें**: स्ट्रिंग मिलने के बाद, Jackson जैसी लाइब्रेरी से पार्स करके सुनिश्चित करें कि वह वैध है, फिर स्टोर करें।  
- **कॉन्फिडेंस मॉनिटर करें**: JSON में प्रत्येक लाइन के साथ `confidence` फ़ील्ड आता है। 0.85 जैसे थ्रेशोल्ड से नीचे की लाइन्स को फ़िल्टर करें ताकि गड़बड़ डेटा न आए।  
- **लाइसेंस को सुरक्षित रखें**: `Aspose.OCR.lic` को सुरक्षित वॉल्ट या एनवायरनमेंट वैरिएबल में रखें, खासकर क्लाउड डिप्लॉयमेंट में।

## निष्कर्ष

हमने **Java में OCR कैसे उपयोग करें** को कवर किया—**छवि से टेक्स्ट पहचान**, **PNG रसीदों से टेक्स्ट निकाल**, और **रसीद को JSON में बदल**—सब एक संक्षिप्त, एंड‑टू‑एंड उदाहरण के साथ। चरण सरल हैं, कोड पूरी तरह रन‑एबल है, और JSON आउटपुट आपको किसी भी डाउनस्ट्रीम सिस्टम के लिए तैयार स्ट्रक्चर देता है।

अगले कदम में आप अधिक एडवांस्ड परिदृश्यों को एक्सप्लोर कर सकते हैं: JSON को Apache Kafka में रियल‑टाइम प्रोसेसिंग के लिए फीड करना, रेगेक्स पैटर्न से लाइन‑आइटम टोटल निकालना, या स्केलेबिलिटी के लिए क्लाउड OCR सर्विस इंटीग्रेट करना। चाहे जो भी चुनें, आज आपने जो बुनियादी बातें सीखी हैं, वे हमेशा समान रहेंगी।

कोई सवाल है या लागू करते समय कोई समस्या आई? नीचे कमेंट करें, हम साथ मिलकर ट्रबलशूट करेंगे। Happy coding, और उन गंदे रसीद इमेजेज़ को साफ़, सर्चेबल डेटा में बदलने का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}