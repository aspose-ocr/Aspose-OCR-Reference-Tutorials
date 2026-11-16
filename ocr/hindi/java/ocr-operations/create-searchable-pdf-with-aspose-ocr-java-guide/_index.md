---
category: general
date: 2026-03-26
description: Aspose.OCR Java का उपयोग करके खोज योग्य PDF बनाएं – इमेज OCR लोड करना
  सीखें, प्राथमिक भाषा सेट करें, इमेज से टेक्स्ट निकालें और OCR PDF सहेजें।
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: hi
og_description: Aspose.OCR Java के साथ खोज योग्य PDF बनाएं। इमेज OCR लोड करने, प्राथमिक
  भाषा सेट करने, इमेज से टेक्स्ट निकालने और OCR PDF सहेजने के लिए चरण-दर-चरण गाइड।
og_title: Aspose.OCR के साथ खोज योग्य PDF बनाएं – जावा गाइड
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Aspose.OCR के साथ खोज योग्य PDF बनाएं – जावा गाइड
url: /hi/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR के साथ खोज योग्य PDF बनाएं – जावा गाइड

क्या आपको कभी स्कैन किए गए दस्तावेज़ से **create searchable pdf** बनाने की ज़रूरत पड़ी, लेकिन शुरुआत कहाँ से करें, यह नहीं पता था? आप अकेले नहीं हैं—कई डेवलपर्स को जावा में OCR को पहली बार अपनाते समय यही समस्या आती है। अच्छी खबर यह है कि Aspose.OCR पूरी पाइपलाइन को—इमेज लोड करने से लेकर प्राथमिक भाषा सेट करने और अंत में OCR‑सक्षम PDF सेव करने तक—बहुत आसान बनाता है। इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे कि कैसे **extracts text from image** किया जाता है, **set primary language** सेट किया जाता है, और अंत में **save OCR pdf** प्राप्त किया जाता है जिसे आप किसी भी रीडर में खोल सकते हैं।

हम कुछ व्यावहारिक टिप्स भी कवर करेंगे, जैसे तेज़ प्रोसेसिंग के लिए GPU एक्सेलेरेशन सक्षम करना और मिश्रित‑भाषा दस्तावेज़ों (हमारे केस में तमिल + अंग्रेज़ी) को संभालना। अंत तक आपके पास एक ठोस, प्रोडक्शन‑रेडी स्निपेट होगा जिसे आप अपने प्रोजेक्ट में जोड़ सकते हैं।

## आपको क्या चाहिए

- **Java 17** (या कोई भी नया JDK; Aspose.OCR Java 8+ को सपोर्ट करता है)
- **Aspose.OCR for Java** लाइब्रेरी (आधिकारिक साइट से डाउनलोड करें या Maven के माध्यम से जोड़ें)
- एक **license file** (या 30‑दिन का ट्रायल)
- एक इमेज फ़ाइल जिसमें टेक्स्ट हो (डेमो में `sample-mixed-tamil-eng.jpg` उपयोग किया गया है)

कोई अतिरिक्त फ्रेमवर्क नहीं, कोई नेटिव डिपेंडेंसी नहीं—सिर्फ साधारण जावा और Aspose.JARs।

## चरण 1: खोज योग्य PDF बनाएं – प्रोजेक्ट सेटअप

कोड में जाने से पहले, सुनिश्चित करें कि प्रोजेक्ट **create searchable pdf** फ़ाइलों के लिए तैयार है।

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip:** संस्करण संख्या को अद्यतित रखें; नए रिलीज़ अक्सर GPU उपयोग के लिए प्रदर्शन सुधार शामिल करते हैं।

अब `RecentFeaturesDemo` नाम की एक साधारण जावा क्लास बनाएं। इस क्लास में वह सभी लॉजिक होगा जिसकी हमें **load image OCR**, भाषा सेटिंग्स को कॉन्फ़िगर करने, और अंत में **save OCR pdf** करने की आवश्यकता है।

## चरण 2: इमेज OCR लोड करें और इंजन इनिशियलाइज़ करें

पाइपलाइन में पहला वास्तविक कदम **load image OCR** है। यह Aspose.OCR को बताता है कि किस फ़ाइल का विश्लेषण करना है।

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Why this matters:** GPU सक्षम करना (`setUseGpu(true)`) आधुनिक हार्डवेयर पर प्रोसेसिंग समय को 70 % तक कम कर सकता है, जबकि समानांतर प्रोसेसिंग सुनिश्चित करती है कि GPU व्यस्त होने पर CPU निष्क्रिय न रहे।

## चरण 3: प्राथमिक भाषा सेट करें (और एक द्वितीयक भी)

यदि आप इस चरण को छोड़ते हैं, तो Aspose.OCR भाषा का अनुमान लगाने की कोशिश करेगा, जो धीमा और कम सटीक होता है। यहाँ बताया गया है कि कैसे **set primary language** को तमिल पर सेट करें और अंग्रेज़ी को फॉलबैक के रूप में जोड़ें।

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explanation:** प्राथमिक भाषा पहचान के दौरान उपयोग किए जाने वाले कैरेक्टर सेट और शब्दकोश को प्रभावित करती है। द्वितीयक भाषा जोड़ना मिश्रित‑स्क्रिप्ट दस्तावेज़ों (जैसे कि एक रसीद जिसमें तमिल और अंग्रेज़ी दोनों टेक्स्ट हो) के लिए महत्वपूर्ण है।  

> **Edge case:** यदि आपके दस्तावेज़ में दो से अधिक भाषाएँ हैं, तो आप प्रत्येक अतिरिक्त भाषा के लिए `addAdditionalLanguage(...)` कॉल कर सकते हैं।

## चरण 4: इमेज का प्री‑प्रोसेसिंग – डेस्क्यू और डीनॉइज़

स्कैन की गई इमेज अक्सर घूर्णन या बैकग्राउंड शोर से प्रभावित होती हैं। प्री‑प्रोसेसिंग OCR इंजन को **extract text from image** अधिक विश्वसनीय रूप से करने में मदद करती है।

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tip:** यदि आप जानते हैं कि इमेज पहले से साफ़ है, तो आप `setDenoise(true)` को छोड़ सकते हैं जिससे कुछ मिलीसेकंड बचेंगे।

## चरण 5: इमेज फ़ाइल लोड करें

अब जब इंजन तैयार है, हम इसे उस फ़ाइल की ओर इशारा करते हैं जिसे हम विश्लेषण करना चाहते हैं।

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **What if the path is wrong?** यदि पथ गलत है तो Aspose.OCR स्पष्ट `FileNotFoundException` फेंकता है। यदि आपको सुगम त्रुटि संभालना है तो कॉल को try‑catch में लपेटें।

## चरण 6: OCR चलाएँ और इमेज से टेक्स्ट निकालें

सब कुछ कॉन्फ़िगर हो जाने के बाद, अब पहचान को वास्तव में चलाने का समय है। यह चरण **extracts text from image** करता है और PDF निर्माण के लिए आवश्यक डेटा तैयार करता है।

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

डेमो इमेज के लिए सामान्य कंसोल आउटपुट इस प्रकार दिखता है:

```
வணக்கம் World
This is a mixed language sample.
```

आप देखेंगे कि तमिल पंक्ति सही ढंग से रेंडर हुई है, उसके बाद अंग्रेज़ी। यह **set primary language** को सही तरीके से सेट करने का परिणाम है।

## चरण 7: OCR PDF सेव करें – अंतिम भाग

पज़ल का अंतिम भाग **save OCR pdf** है। Aspose.OCR मूल इमेज के ऊपर एक अदृश्य टेक्स्ट लेयर एम्बेड कर सकता है, जिससे PDF खोज योग्य बन जाता है।

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

`searchable.pdf` को Adobe Reader में खोलें, **Ctrl + F** दबाएँ, और आप तमिल और अंग्रेज़ी दोनों शब्दों को खोज सकते हैं—बिल्कुल वही जो **create searchable pdf** वर्कफ़्लो का वादा करता है।

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट)

नीचे पूरा प्रोग्राम दिया गया है जिसे आप जैसा है वैसा कंपाइल और रन कर सकते हैं। प्लेसहोल्डर पाथ को अपने डायरेक्टरीज़ से बदलें।

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

इसे इस प्रकार चलाएँ:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

आपको कंसोल में निकाला गया टेक्स्ट दिखना चाहिए, उसके बाद यह पुष्टि कि **searchable pdf** डिस्क पर लिखा गया है।

## सामान्य प्रश्न और किनारे के मामले

### यदि मुझे **load image OCR** को बाइट एरे से लोड करना हो तो क्या करें?

आप `ImageStream.fromFile(imagePath)` को `ImageStream.fromBytes(byteArray)` से बदल सकते हैं। यह तब उपयोगी होता है जब इमेज डेटाबेस या वेब सर्विस से आती है।

### ऐसे PDFs को कैसे हैंडल करें जिनमें पहले से इमेजेज हों?

Aspose.OCR सीधे PDF पेजों पर काम कर सकता है: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`। पहचान से पहले इंजन प्रत्येक पेज को आंतरिक रूप से रास्टराइज़ करेगा।

### मेरा GPU पहचान नहीं रहा—क्या मुझे `setUseGpu(true)` रखना चाहिए?

यदि `setUseGpu(true)` विफल हो जाता है, तो Aspose.OCR स्वचालित रूप से CPU पर वापस आ जाता है। इसे सक्षम करने से पहले आप `ocrEngine.getEngineSettings().isGpuAvailable()` की जाँच कर सकते हैं।

### क्या मैं **save OCR pdf** को कस्टम मेटाडाटा के साथ कर सकता हूँ?

हाँ। पहचान के बाद, `ocrEngine.getPdfSaveOptions().setTitle("My Document")` या `setAuthor("John Doe")` का उपयोग करके `save` कॉल करने से पहले सेट करें।

## बड़े बैचों के लिए प्रदर्शन टिप्स

- **Batch processing:** कई इमेजेज़ में एक ही `OcrEngine` इंस्टेंस को पुनः उपयोग करें। रन के बीच केवल `ocrEngine.clear()` कॉल करें।
- **Thread pool:** प्रत्येक इमेज टास्क को `Callable` में लपेटें और `ExecutorService` को सबमिट करें। चूँकि हमने समानांतर प्रोसेसिंग सक्षम की है, प्रत्येक थ्रेड मल्टी‑कोर उपयोग से लाभान्वित होगा।
- **Memory management:** गीगापिक्सेल इमेजेज़ के लिए `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` के साथ डाउन‑सैंपलिंग पर विचार करें ताकि RAM उपयोग उचित रहे।

## निष्कर्ष

हमने अभी-अभी Aspose.OCR for Java का उपयोग करके एक पूर्ण **create searchable pdf** वर्कफ़्लो दिखाया। **load image OCR** से शुरू करके, हम

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}