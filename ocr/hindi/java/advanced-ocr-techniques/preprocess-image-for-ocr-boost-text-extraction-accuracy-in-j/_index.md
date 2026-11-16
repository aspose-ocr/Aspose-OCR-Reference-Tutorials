---
category: general
date: 2026-03-28
description: OCR के लिए छवि को पूर्व‑प्रसंस्करण करें और Aspose OCR के साथ छवि से टेक्स्ट
  पहचानें। फोटो से टेक्स्ट निकालना सीखें, चरण‑दर‑चरण पूर्व‑प्रसंस्करण से OCR की सटीकता
  बढ़ाएँ।
draft: false
keywords:
- preprocess image for OCR
- recognize text from image
- extract text from photo
- improve OCR accuracy preprocessing
- Aspose OCR Java
- image preprocessing pipeline
language: hi
og_description: Aspose OCR Java के साथ OCR के लिए छवि को पूर्व‑प्रसंस्करण करें और
  फोटो से पाठ निकालें। केवल कुछ चरणों में OCR की सटीकता बढ़ाने के लिए इस ट्यूटोरियल
  का पालन करें।
og_title: OCR के लिए छवि का पूर्व-प्रसंस्करण – पूर्ण जावा गाइड
tags:
- OCR
- Java
- Image Processing
title: OCR के लिए छवि को पूर्व-प्रसंस्करण करें – जावा में टेक्स्ट निष्कर्षण की सटीकता
  बढ़ाएँ
url: /hi/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-text-extraction-accuracy-in-j/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR के लिए इमेज प्रीप्रोसेसिंग – एक पूर्ण जावा गाइड

क्या आपने कभी **preprocess image for OCR** करने की कोशिश की है और फिर भी गड़बड़ आउटपुट मिला है? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में, एक कच्चा स्कैन या स्मार्टफ़ोन फोटो में skew, noise, या low contrast होता है जो सबसे स्मार्ट recognition engine को भी भ्रमित कर देता है। अच्छी खबर? एक छोटा preprocessing pipeline—de‑skew, denoise, binarize—OCR की सटीकता को बहुत बढ़ा सकता है।

इस ट्यूटोरियल में हम एक हैंड‑ऑन उदाहरण के माध्यम से दिखाएंगे कि **recognize text from image** कैसे किया जाता है Aspose OCR for Java का उपयोग करके। अंत तक आप **extract text from photo** फ़ाइलों को बहुत कम त्रुटियों के साथ निकाल पाएँगे, और समझेंगे कि प्रत्येक preprocessing स्टेप क्यों महत्वपूर्ण है।

> **आपको क्या मिलेगा**  
> * एक पूरी तरह चलने वाला जावा प्रोग्राम जो एक tilted फोटो को लोड करता है, तीन क्लासिक फ़िल्टर लागू करता है, और साफ़ टेक्स्ट प्रिंट करता है।  
> * de‑skew, denoise, और binarize के “क्यों” की समझ।  
> * एज केसों को संभालने के टिप्स—बड़ी फ़ाइलें, विभिन्न इमेज फ़ॉर्मेट, और कस्टम फ़िल्टर क्रम।

## Prerequisites

- Java 8 या उससे नया इंस्टॉल किया हुआ (कोड JDK 11 के साथ भी कम्पाइल होता है)।  
- Maven या Gradle ताकि Aspose OCR लाइब्रेरी को पुल किया जा सके।  
- एक सैंपल इमेज (जैसे `angled-photo.jpg`) जो थोड़ा rotated है और उसमें कुछ visual noise है।  
- Java के `main` मेथड की बेसिक समझ—गहरी OCR विशेषज्ञता की आवश्यकता नहीं।

यदि इनमें से कुछ भी आपके पास नहीं है, तो Oracle या OpenJDK से नवीनतम JDK डाउनलोड करें और अपने `pom.xml` में निम्न Maven dependency जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Maven Central for the newest version -->
</dependency>
```

अब, कोड में डुबकी लगाएँ।

## Step 1 – Create the OCR Engine Instance

सबसे पहले आपको एक `OcrEngine` ऑब्जेक्ट चाहिए। इसे उस दिमाग की तरह समझें जो बाद में प्रोसेस्ड इमेज को पढ़ेगा।

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **यह क्यों महत्वपूर्ण है:** इंजन recognition settings, language packs, और—हमारे लिए सबसे महत्वपूर्ण—preprocessing options को एन्कैप्सुलेट करता है। इसके बिना आपको मैन्युअली इमेज‑प्रोसेसिंग लाइब्रेरीज़ को चेन करना पड़ेगा, जो एक साफ़ pipeline के उद्देश्य को नष्ट कर देता है।

## Step 2 – Build a Preprocessing Pipeline (de‑skew → denoise → binarize)

Aspose OCR एक बिल्ट‑इन `PreprocessingOptions` क्लास प्रदान करता है जो आपको फ़िल्टर को ठीक उसी क्रम में स्टैक करने देता है जिसकी आपको ज़रूरत है। यहाँ हम तीन फ़िल्टर जोड़ते हैं:

1. **DE_SKEW** – rotated टेक्स्ट को सीधा करता है।  
2. **DENOISE** – ग्रेनी पिक्सेल्स को स्मूद करता है जो अक्षर समझे जा सकते हैं।  
3. **BINARIZE** – इमेज को शुद्ध ब्लैक‑एंड‑व्हाइट में बदलता है, जिससे OCR इंजन का काम आसान हो जाता है।

```java
        // Step 2: Assemble the preprocessing pipeline
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);   // correct rotation
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);  // remove grain
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE); // high‑contrast B&W

        // Attach the pipeline to the OCR engine
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);
```

> **Pro tip:** फ़िल्टरों का क्रम बहुत ज़रूरी है। यदि आप denoise से पहले binarize करते हैं, तो noise काली धब्बों में बदल सकता है जो recognizer को भ्रमित कर देगा। पहले de‑skew करने से टेक्स्ट की baseline क्षैतिज हो जाती है, जिससे denoise और binarize दोनों के परिणाम बेहतर होते हैं।

## Step 3 – Feed the Image to the Engine

अब हम इंजन को उस फ़ाइल की ओर इशारा करते हैं जिसे हम पढ़ना चाहते हैं। पाथ absolute या आपके प्रोजेक्ट रूट के सापेक्ष हो सकता है।

```java
        // Step 3: Run OCR on the target image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

> **अगर इमेज बहुत बड़ी हो तो क्या?** Aspose OCR स्वचालित रूप से 2000 px से बड़े इमेज को सबसे लंबी साइड पर स्केल डाउन कर देता है, लेकिन यदि मेमोरी की चिंता है तो आप `ocrEngine.getRecognitionSettings().setMaxImageDimension(1500)` के ज़रिए इसे ओवरराइड कर सकते हैं।

## Step 4 – Output the Recognized Text

अंत में, हम निकाले गए स्ट्रिंग को कंसोल पर प्रिंट करते हैं। वास्तविक एप्लिकेशन में आप इसे डेटाबेस, फ़ाइल, या किसी downstream NLP pipeline में भेज सकते हैं।

```java
        // Step 4: Print the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Expected Output

यदि `angled-photo.jpg` में वाक्य *“The quick brown fox jumps over the lazy dog.”* है, तो आपको कुछ इस तरह का आउटपुट दिखना चाहिए:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

ध्यान दें कि आउटपुट साफ़ है—कोई अनचाहे सिंबल नहीं, कोई टूटी हुई लाइन नहीं। यही है **preprocess image for OCR** की शक्ति।

## Step 5 – Verify and Tweak (Optional)

भले ही आपके पास एक ठोस pipeline हो, आप कुछ एज केसों का सामना कर सकते हैं:

| Situation | Suggested tweak |
|-----------|-----------------|
| **Very low contrast** (जैसे फेडेड स्कैन किए गए दस्तावेज़) | बाइनराइज़ेशन से पहले एक अतिरिक्त `ContrastAdjustment` फ़िल्टर जोड़ें। |
| **Colorful background** (जैसे रंगीन स्टैंप वाले रसीद) | `BackgroundRemoval` फ़िल्टर जोड़ें या पहले ग्रेस्केल में कन्वर्ट करें। |
| **Multi‑page PDFs** | प्रत्येक पेज इमेज पर लूप चलाएँ और वही `preprocessingOptions` पुनः उपयोग करें। |

आप `preprocessingOptions.addFilter(PreprocessFilter.CONTRAST)` या Aspose OCR API डॉक्यूमेंटेशन में सूचीबद्ध किसी भी फ़िल्टर को कॉल करके प्रयोग कर सकते हैं।

## Full, Runnable Example

नीचे पूरा प्रोग्राम दिया गया है, जिसे आप `PreprocessExample.java` नाम की फ़ाइल में कॉपी‑पेस्ट कर सकते हैं। कंपाइल करने से पहले सुनिश्चित करें कि Maven dependency रिजॉल्व हो गई है।

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing: de‑skew → denoise → binarize
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE);
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);

        // 3️⃣ Perform OCR on the chosen image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // 4️⃣ Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

कम्पाइल और रन करें:

```bash
mvn compile exec:java -Dexec.mainClass=PreprocessExample
```

आपको कंसोल पर साफ़ टेक्स्ट दिखना चाहिए, जिससे पुष्टि होगी कि आपने सफलतापूर्वक **preprocess image for OCR** और **recognize text from image** किया है।

## Common Questions & Answers

**Q1: क्या यह PNG या TIFF फ़ाइलों के साथ काम करता है?**  
हाँ—Aspose OCR JPEG, PNG, BMP, TIFF, और कई अन्य फ़ॉर्मेट्स को सपोर्ट करता है। वही preprocessing pipeline लागू होता है; लाइब्रेरी फ़ॉर्मेट को ऑटो‑डिटेक्ट कर लेती है।

**Q2: अगर मुझे फोन से ली गई फोटो से टेक्स्ट निकालना हो तो क्या करें?**  
फ़ोन की फोटो अक्सर uneven lighting से पीड़ित होती है। बाइनराइज़ेशन से पहले `LIGHTING_CORRECTION` फ़िल्टर जोड़ने से मदद मिल सकती है। कोड परिवर्तन सिर्फ एक लाइन है:

```java
preprocessingOptions.addFilter(PreprocessFilter.LIGHTING_CORRECTION);
```

**Q3: क्या मैं OCR की भाषा बदल सकता हूँ?**  
बिल्कुल। इंजन बनाते समय, भाषा सेट करें:

```java
ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.SPANISH);
```

**Q4: यह OCR accuracy preprocessing को कैसे सुधारता है?**  
हर फ़िल्टर एक विशिष्ट प्रकार के visual noise को कम करता है। De‑skew टेक्स्ट लाइनों को align करता है, denoise रैंडम स्पॉट्स हटाता है, और binarize हाई‑कॉन्ट्रास्ट इमेज बनाता है। मिलकर ये recognition algorithm को साफ़ सिग्नल देते हैं, जिससे character‑level accuracy में 15‑30 % तक की वृद्धि हो सकती है।

## Next Steps & Related Topics

- **Batch processing:** कोर लॉजिक को लूप में रखें ताकि फ़ोटो फ़ोल्डर की पूरी सामग्री प्रोसेस हो सके।  
- **Custom filter order:** दस्तावेज़ों के पहले से हाई‑कॉन्ट्रास्ट होने पर `BINARIZE` को `DENOISE` से पहले आज़माएँ।  
- **Performance tuning:** `ocrEngine.getRecognitionSettings().setThreadCount(4)` सेट करके मल्टी‑कोर मशीन पर पैराललाइज़ करें।  
- **Alternative libraries:** ओपन‑सोर्स परिदृश्य के लिए Aspose OCR की तुलना Tesseract‑Java से करें।  
- **Post‑processing:** कच्चे आउटपुट को और साफ़ करने के लिए spell‑checking या regex क्लीन‑अप लागू करें।

**preprocess image for OCR** वर्कफ़्लो में महारत हासिल करके आप फोटो स्रोतों से टेक्स्ट निकालने को एक पूर्वानुमानित, दोहराने योग्य कार्य बना लेंगे, न कि एक अटक‑बटक प्रयोग।

---

*क्या आप अपने OCR पाइपलाइन को बूस्ट करना चाहते हैं? कोड ले‑आउट करें, फ़िल्टरों को ट्यून करें, और सटीकता में बढ़ोतरी देखें। अगर कोई समस्या आती है, तो नीचे कमेंट करें—हैप्पी कोडिंग!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}