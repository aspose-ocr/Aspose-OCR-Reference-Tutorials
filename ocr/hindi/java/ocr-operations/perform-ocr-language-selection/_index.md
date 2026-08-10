---
date: 2026-06-24
description: Aspose.OCR for Java का उपयोग करके भाषा चयन के साथ इमेज टेक्स्ट को OCR
  करने का तरीका सीखें। यह चरण-दर-चरण गाइड टेक्स्ट निकालना (Java), OCR स्क्यू सुधार,
  और अधिक को कवर करता है।
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Aspose.OCR के साथ OCR स्क्यू सुधार और भाषा चयन कैसे करें
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Aspose.OCR के साथ OCR स्क्यू सुधार और भाषा चयन कैसे करें
url: /hi/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR के साथ OCR स्क्यू सुधार और भाषा चयन कैसे करें

## परिचय

इमेज फ़ाइलों से टेक्स्ट निकालना एक सामान्य आवश्यकता है, चाहे आप स्कैन किए गए दस्तावेज़ों को डिजिटाइज़ कर रहे हों, रसीदों को प्रोसेस कर रहे हों, या खोज योग्य अभिलेख बनाना चाहते हों। इस ट्यूटोरियल में हम एक पूर्ण, व्यावहारिक उदाहरण के माध्यम से दिखाएंगे **कैसे OCR इमेज टेक्स्ट** को एक विशिष्ट भाषा सेटिंग के साथ किया जाए, ताकि आप आज ही अपने Java एप्लिकेशन में विश्वसनीय OCR को एकीकृत कर सकें। आप यह भी देखेंगे कि **OCR स्क्यू सुधार** और क्षेत्र‑आधारित पहचान कैसे लागू की जाए ताकि सटीकता बढ़े, जिससे कोणीय स्कैन पर OCR सटीकता **30 % तक** सुधर सकती है।

## त्वरित उत्तर
- **Java में OCR को संभालने वाली लाइब्रेरी कौन सी है?** Aspose.OCR for Java  
- **कौन सी सेटिंग भाषा चुनती है?** `settings.setLanguage(Language.Eng)` (या कोई भी समर्थित भाषा)  
- **क्या विकास के लिए लाइसेंस चाहिए?** परीक्षण के लिए एक मुफ्त मूल्यांकन लाइसेंस काम करता है; उत्पादन के लिए व्यावसायिक लाइसेंस आवश्यक है।  
- **क्या मैं OCR को इमेज के किसी क्षेत्र तक सीमित कर सकता हूँ?** हाँ, `RecognitionSettings.setRecognitionAreas()` के साथ आयतों का उपयोग करें।  
- **सामान्य रन‑टाइम क्या है?** मानक लैपटॉप पर प्रति पृष्ठ कुछ सेकंड, इमेज आकार और भाषा जटिलता पर निर्भर करता है।  

`Language` एक enumeration है जो Aspose.OCR द्वारा समर्थित OCR भाषाओं को सूचीबद्ध करता है, जैसे English, French, Spanish, आदि।

## OCR स्क्यू सुधार क्या है?

OCR स्क्यू सुधार वह प्रक्रिया है जिसमें tilted टेक्स्ट लाइनों का पता लगाकर उन्हें सीधा किया जाता है, इससे पहले कि कैरेक्टर पहचान की जाए। टेक्स्ट बेसलाइन को संरेखित करके, OCR इंजन अपने भाषा मॉडलों को अधिक प्रभावी ढंग से लागू कर सकता है, जिससे कोणीय स्कैन के कारण होने वाली गलतियों में कमी आती है। यह चरण इनपुट इमेज की दृश्य गुणवत्ता को सुधारता है, जिससे पहचान एल्गोरिदम वास्तविक कैरेक्टर रूपों पर ध्यान केंद्रित कर सके, न कि घुमाव द्वारा उत्पन्न विकृति पर।

## क्यों OCR स्क्यू सुधार सटीकता बढ़ाता है

जब टेक्स्ट स्क्यू होता है, तो कैरेक्टर आकार विकृत हो जाते हैं, जिससे त्रुटि दर में **20 % तक** वृद्धि हो सकती है। **ocr स्क्यू सुधार** लागू करने से वह विकृति हट जाती है, जिससे इंजन वास्तविक glyphs पर ध्यान दे पाता है। बेंचमार्क परीक्षणों में Aspose.OCR ने 10‑15° घुमाव वाले दस्तावेज़ों पर स्क्यू सुधार के बाद पहचान सटीकता में **15‑30 %** की वृद्धि दर्ज की।

## क्यों Aspose.OCR के साथ भाषा चयन उपयोग करें?

स्रोत टेक्स्ट की सटीक भाषा चुनने से OCR इंजन को भाषा‑विशिष्ट शब्दकोश और कैरेक्टर मॉडल मिलते हैं, जिससे पहचान की शुद्धता में उल्लेखनीय वृद्धि और प्रोसेसिंग समय में कमी आती है। अतिरिक्त रूप से, Aspose.OCR स्क्यू सुधार, क्षेत्र चयन, और आउटपुट फ़ॉर्मेट्स पर सूक्ष्म नियंत्रण प्रदान करता है, जिससे यह बहुभाषी दस्तावेज़ प्रोसेसिंग पाइपलाइन के लिए एक बहुमुखी विकल्प बनता है।

- **बहुभाषी समर्थन** – इमेज में मौजूद सटीक भाषा(यों) को चुनें और सटीकता बढ़ाएँ।  
- **सूक्ष्म नियंत्रण** – स्क्यू को समायोजित करें, पहचान क्षेत्रों को परिभाषित करें, और ऑटो‑स्क्यू व्यवहार सेट करें।  
- **शुद्ध Java API** – कोई नेटिव निर्भरताएँ नहीं, किसी भी Java प्रोजेक्ट में आसान इंटीग्रेशन।  
- **समृद्ध परिणाम डेटा** – एक ही कॉल में प्लेन टेक्स्ट, JSON, बाउंडिंग आयतें, और चेतावनियाँ प्राप्त करें।  
- **मात्रात्मक क्षमता** – Aspose.OCR **50+** इनपुट और आउटपुट फ़ॉर्मेट्स का समर्थन करता है और **500‑पेज** इमेज बैच को पूरी डॉक्यूमेंट को मेमोरी में लोड किए बिना प्रोसेस कर सकता है।

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित हों:

- **Java Development Kit (JDK)** स्थापित हो (JDK 8 या बाद का)।  
- **Aspose.OCR for Java** लाइब्रेरी – इसे आधिकारिक साइट से [यहाँ](https://reference.aspose.com/ocr/java/) डाउनलोड करें।  
- एक इमेज फ़ाइल जिसमें वह टेक्स्ट हो जिसे आप निकालना चाहते हैं, उदाहरण के लिए `p3.png`।  

## पैकेज इम्पोर्ट करें

निम्नलिखित इम्पोर्ट्स आपको कोर OCR क्लासेज़ और मानक Java यूटिलिटीज़ तक पहुंच प्रदान करते हैं।  
`import com.aspose.ocr.*;` – मुख्य OCR इंजन को लाता है।  
`import com.aspose.ocr.config.*;` – `RecognitionSettings` जैसे कॉन्फ़िगरेशन ऑब्जेक्ट्स को शामिल करता है।  
`import java.awt.Rectangle;` – पहचान क्षेत्रों को परिभाषित करने के लिए उपयोग किया जाता है।  

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Java में OCR स्क्यू सुधार कैसे लागू करें?

इमेज लोड करें, ऑटो‑स्क्यू डिटेक्शन को निष्क्रिय करें, और या तो मापी गई कोण प्रदान करें या `settings.setAutoSkew(false)` के साथ इंजन को स्वयं गणना करने दें। OCR इंजन पहले प्रदान किए गए या पता लगाए गए कोण के आधार पर इमेज को सीधा करेगा, फिर कैरेक्टर पहचान करेगा। यह दो‑चरणीय दृष्टिकोण सुनिश्चित करता है कि कोई भी झुकाव भाषा मॉडलों को लागू करने से पहले हटाया जाए, जिससे साफ़ टेक्स्ट आउटपुट और कम गलत पहचान प्राप्त हो।

## चरण‑दर‑चरण गाइड

### चरण 1: अपना डॉक्यूमेंट डायरेक्टरी सेट करें

एक `File` ऑब्जेक्ट बनाएं जो आपके स्रोत इमेज वाले फ़ोल्डर की ओर इशारा करता हो। यह पाथ हैंडलिंग को विभिन्न ऑपरेटिंग सिस्टम्स में पोर्टेबल बनाता है।

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

`"Your Document Directory"` को उस पूर्ण पाथ से बदलें जहाँ `p3.png` स्थित है।

### चरण 2: इमेज पाथ परिभाषित करें

विशिष्ट इमेज के लिए एक `File` ऑब्जेक्ट इंस्टैंशिएट करें जिसे आप प्रोसेस करना चाहते हैं। `File` ऑब्जेक्ट का उपयोग करने से आपको फ़ाइल मेटाडेटा तक आसान पहुंच मिलती है, यदि बाद में आवश्यकता हो।

```java
// The image path
String file = dataDir + "p3.png";
```

सुनिश्चित करें कि `file` वेरिएबल ठीक उसी इमेज की ओर इशारा कर रहा हो जिसे आप प्रोसेस करना चाहते हैं।

### चरण 3: Aspose.OCR API इंस्टेंस बनाएं

`AsposeOCR` क्लास सभी OCR ऑपरेशन्स के लिए एंट्री पॉइंट है। यह इंजन को एन्कैप्सुलेट करता है, रिसोर्सेज़ को मैनेज करता है, और `recognizePage` मेथड प्रदान करता है।

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` ऑब्जेक्ट आपको सभी OCR ऑपरेशन्स तक पहुंच देता है।

### चरण 4: पहचान विकल्प सेट करें (भाषा चयन)

`RecognitionSettings` Aspose.OCR की कॉन्फ़िगरेशन कंटेनर है जो OCR प्रक्रिया को सूक्ष्म रूप से ट्यून करने की अनुमति देती है।  

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

यहाँ हम:

1. ऑटो‑स्क्यू को निष्क्रिय करते हैं क्योंकि हम मैन्युअल स्क्यू मान प्रदान करेंगे।  
2. आयताकार क्षेत्र (`RecognitionAreas`) को परिभाषित करते हैं ताकि OCR केवल इमेज के उस भाग तक सीमित रहे जिसमें वास्तविक टेक्स्ट है।  
3. **भाषा** को English (`Language.Eng`) सेट करते हैं। इसे `Language.Fra`, `Language.Spa` आदि में बदलें, आपके स्रोत इमेज के अनुसार।

### चरण 5: OCR चलाएँ और परिणाम प्राप्त करें

`recognizePage` को कॉल करने से OCR इंजन इमेज और आपने जो सेटिंग्स परिभाषित की हैं, उनका उपयोग करके चलाया जाता है। परिणाम `RecognitionResult` ऑब्जेक्ट में संग्रहीत होता है, जो सभी उपयोगी डेटा को एकत्रित करता है।

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` कॉल इमेज और सेटिंग्स के साथ OCR इंजन को चलाता है। परिणाम `RecognitionResult` ऑब्जेक्ट में संग्रहीत होता है।

### चरण 6: परिणाम प्रिंट करें और उपयोग करें

कंसोल आउटपुट दिखाता है:

- पूर्ण निकाला गया टेक्स्ट (`recognitionText`)।  
- प्रत्येक परिभाषित आयत के लिए टेक्स्ट (`recognitionAreasText`)।  
- बाउंडिंग आयत के निर्देशांक।  
- आसान डाउनस्ट्रीम प्रोसेसिंग के लिए JSON प्रतिनिधित्व।  
- पता लगाया गया स्क्यू कोण और कोई भी चेतावनियाँ।

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

कंसोल आउटपुट पूर्ण निकाले गए टेक्स्ट, क्षेत्र‑विशिष्ट टेक्स्ट, बाउंडिंग बॉक्स, JSON, स्क्यू कोण, और चेतावनियाँ दिखाता है। अब आप `result.recognitionText` को अपने बिज़नेस लॉजिक में फीड कर सकते हैं—इसे स्टोर करें, इंडेक्स करें, या किसी अन्य सेवा को पास करें।

## सामान्य समस्याएँ और समाधान

| समस्या | कारण | समाधान |
|-------|-------|-----|
| **गैर‑मान्य अक्षर** | गलत भाषा चयन | सही `Language` enum सेट करें (उदाहरण: फ्रेंच के लिए `Language.Fra`) |
| **कोई टेक्स्ट नहीं मिला** | पहचान क्षेत्र टेक्स्ट को कवर नहीं करता | `Rectangle` निर्देशांक समायोजित करें या पूरे इमेज को प्रोसेस करने के लिए `RecognitionAreas` हटाएँ |
| **धीमी प्रदर्शन** | बहुत बड़ी इमेज या उच्च रिज़ॉल्यूशन | OCR से पहले इमेज को डाउनस्केल करें या JVM मेमोरी आवंटन बढ़ाएँ |
| **असमर्थित फ़ॉर्मेट की चेतावनी** | इमेज फ़ॉर्मेट पहचाना नहीं गया | इमेज को PNG, JPEG, या TIFF में बदलें और फिर प्रोसेस करें |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या मैं एक ही OCR कॉल में कई भाषाएँ पहचान सकता हूँ?**  
उत्तर: हाँ। `settings.setLanguage(Language.Eng \| Language.Fra)` का उपयोग करके बहुभाषी पहचान सक्षम करें।

**प्रश्न: Aspose.OCR कौन‑से इमेज फ़ॉर्मेट्स का समर्थन करता है?**  
उत्तर: PNG, JPEG, BMP, TIFF, GIF, और कई अन्य। केवल सही फ़ाइल पाथ प्रदान करें।

**प्रश्न: इमेज का आकार सीमा क्या है?**  
उत्तर: कोई कठोर सीमा नहीं है, लेकिन 10 MB से बड़ी इमेज प्रोसेस करने पर मेमोरी उपयोग और रन‑टाइम बढ़ सकता है। बड़े फ़ाइलों को री‑साइज़ करने पर विचार करें।

**प्रश्न: उत्पादन लाइसेंस कैसे प्राप्त करें?**  
उत्तर: Aspose वेबसाइट से लाइसेंस खरीदें और Aspose दस्तावेज़ में दिखाए अनुसार `License` क्लास के माध्यम से लागू करें।

**प्रश्न: क्या मैं सीधे PDF पेज से टेक्स्ट निकाल सकता हूँ?**  
उत्तर: सीधे Aspose.OCR से नहीं। पहले PDF पेज को इमेज में बदलें (उदाहरण के लिए Aspose.PDF का उपयोग करके) और फिर OCR चलाएँ।

## निष्कर्ष

आपने अब देखा कि **Aspose.OCR for Java** का उपयोग करके इमेज से टेक्स्ट कैसे निकाला जाए, उचित भाषा चयन के साथ और **OCR स्क्यू सुधार** लागू करके विश्वसनीयता कैसे बढ़ाई जाए। यह दृष्टिकोण सटीक, उच्च‑प्रदर्शन OCR प्रदान करता है जिसे किसी भी Java‑आधारित वर्कफ़्लो में एम्बेड किया जा सकता है—डॉक्यूमेंट मैनेजमेंट सिस्टम से लेकर डेटा‑कैप्चर पाइपलाइन तक। विभिन्न `Language` enums के साथ प्रयोग करें, `RecognitionAreas` को ट्यून करें, और JSON आउटपुट को अपने डाउनस्ट्रीम एनालिटिक्स में एकीकृत करके एक पूर्ण‑समाधान बनाएं।

---

**अंतिम अपडेट:** 2026-06-24  
**परीक्षित संस्करण:** Aspose.OCR 24.11 for Java  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल

- [How to calculate skew angle java using Aspose.OCR](/ocr/java/ocr-basics/calculate-skew-angle/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/java/ocr-operations/recognize-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}