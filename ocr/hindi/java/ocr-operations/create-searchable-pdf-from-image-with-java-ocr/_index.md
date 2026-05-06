---
category: general
date: 2026-05-06
description: Aspose OCR का उपयोग करके जावा में छवि से खोज योग्य PDF बनाएं। छवि को
  PDF में बदलना सीखें, वर्तनी सुधार सक्षम करें, और तेज़ परिणामों के लिए OCR GPU का
  उपयोग करें।
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: hi
og_description: Aspose OCR का उपयोग करके जावा में एक छवि से खोज योग्य PDF बनाएं। यह
  गाइड दिखाता है कि कैसे छवि को PDF में बदलें, वर्तनी सुधार सक्षम करें, और OCR GPU
  का उपयोग करें।
og_title: जावा OCR के साथ इमेज से सर्चेबल PDF बनाएं
tags:
- OCR
- Java
- PDF
title: जावा OCR का उपयोग करके छवि से खोज योग्य PDF बनाएं
url: /hi/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज से Java OCR के साथ सर्चेबल PDF बनाएं

क्या आपको कभी **स्कैन की गई तस्वीर से सर्चेबल PDF** बनाना पड़ा, लेकिन शुरुआत कैसे करें, समझ नहीं आया? आप अकेले नहीं हैं—ज्यादातर डेवलपर्स को इमेज‑आधारित PDFs के साथ काम करते समय यही समस्या आती है। सौभाग्य से, Aspose OCR for Java के साथ आप **इमेज को PDF में बदल** सकते हैं, टेक्स्ट को चयन योग्य बना सकते हैं, और एक पॉलिश्ड रिजल्ट के लिए स्पेल करेक्शन भी जोड़ सकते हैं।

इस ट्यूटोरियल में हम एक पूरी, तैयार‑चलाने योग्य उदाहरण के माध्यम से दिखाएंगे कि **OCR GPU** का उपयोग कैसे करें जब वह उपलब्ध हो, **इमेज OCR** को प्रभावी ढंग से कैसे प्रोसेस करें, और डाउनस्ट्रीम सर्च के लिए स्पेल करेक्शन क्यों महत्वपूर्ण है। अंत तक आपके पास एक‑क्लिक समाधान होगा जिससे आप सर्चेबल PDF जेनरेट कर सकते हैं, जिसे आप यूज़र्स को दे सकते हैं या कंप्लायंस के लिए आर्काइव कर सकते हैं।

> **प्रो टिप:** यदि आप ऐसे मशीन पर चल रहे हैं जिसमें GPU नहीं है, तो कोड स्वचालित रूप से CPU पर फॉल बैक हो जाता है, इसलिए आपको कुछ भी री‑राइट करने की जरूरत नहीं।

---

## आपको क्या चाहिए

- **Java 8+** (कोड JDK 8 और उसके बाद के संस्करणों के साथ कम्पाइल होता है)
- **Aspose OCR for Java** लाइब्रेरी (Aspose साइट से नवीनतम JAR डाउनलोड करें)
- एक **इनपुट इमेज** (JPEG, PNG, TIFF, आदि) जिसे आप सर्चेबल PDF में बदलना चाहते हैं
- (वैकल्पिक) **GPU** जिसमें CUDA सपोर्ट हो, यदि आप सबसे तेज़ रिकग्निशन चाहते हैं

कोई अतिरिक्त फ्रेमवर्क नहीं, कोई Maven/Gradle जादू नहीं—सिर्फ क्लासपाथ में एक JAR और आप तैयार हैं।

---

## चरण 1: OCR इंजन को इनिशियलाइज़ करें – प्रोसेस का दिल  

सबसे पहले हम एक `OcrEngine` इंस्टेंस बनाते हैं और उसे स्रोत फ़ाइल की ओर इशारा करते हैं। यह ऑब्जेक्ट वह वर्कहॉर्स है जो इमेज पढ़ेगा, न्यूरल नेटवर्क चलाएगा, और हमें टेक्स्ट वापस देगा।

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*क्यों महत्वपूर्ण है:* इंजन को एक बार इनिशियलाइज़ करके पुनः‑उपयोग करने से नेटीव लाइब्रेरीज़ को बार‑बार लोड करने का ओवरहेड बचता है—एक छोटा परफॉर्मेंस बूस्ट जो जब आप दर्जनों फ़ाइलों को बैच‑प्रोसेस करते हैं तो बड़ा फर्क डालता है।

---

## चरण 2: प्रोसेसिंग डिवाइस चुनें – संभव हो तो OCR GPU इस्तेमाल करें  

यदि आपके वर्कस्टेशन में संगत GPU है, तो आप Aspose को बताकर भारी काम GPU पर करा सकते हैं। अन्यथा इंजन स्वचालित रूप से CPU पर स्विच कर लेता है।

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*क्या फायदा है?* GPU एक्सेलेरेशन प्रत्येक पेज पर सेकंड्स बचा सकता है, खासकर हाई‑रेज़ोल्यूशन स्कैन के लिए। फॉलबैक यह सुनिश्चित करता है कि वही कोड हर जगह काम करे, इसलिए हम **use OCR GPU** को डिफ़ॉल्ट सेटिंग के रूप में सुझाते हैं।

---

## चरण 3: स्कैन को तेज़ करें – सभी CPU कोर का उपयोग करें  

भले ही GPU व्यस्त हो, आसपास के प्री‑प्रोसेसिंग स्टेप्स को पैराललाइज़ किया जा सकता है। थ्रेड काउंट को उपलब्ध प्रोसेसर की संख्या पर सेट करने से इंजन को एक साथ कई चंक्स प्रोसेस करने का मौका मिलता है।

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*नोट:* 4‑कोर लैपटॉप पर यह चार थ्रेड्स बनाएगा; 16‑कोर वर्कस्टेशन पर आपको पूरा लाभ मिलेगा। बस ध्यान रखें कि अधिक थ्रेड्स का मतलब मेमोरी उपयोग बढ़ना भी है।

---

## चरण 4: इमेज को साफ़ करें – प्री‑प्रोसेसिंग फ़िल्टर  

धुंधली या शोर वाली स्कैन गंदा टेक्स्ट उत्पन्न करेगी। कुछ बिल्ट‑इन फ़िल्टर जोड़ने से सटीकता में नाटकीय सुधार आता है।

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*इन फ़िल्टरों का कारण क्या है?* `DeskewFilter` स्कैन के उस घुमाव को ठीक करता है जो अक्सर दस्तावेज़ को एंगल पर स्कैनर में डालने से होता है। `NoiseRemovalFilter` अनावश्यक पिक्सेल्स को हटाता है, जिन्हें अन्यथा अक्षर मान लिया जाता। इसे इस तरह समझें कि OCR इंजन को साफ़ कागज़ दिया गया हो।

---

## चरण 5: स्मार्ट फीचर चालू करें – स्पेल करेक्शन और ऑटो लैंग्वेज डिटेक्शन सक्षम करें  

यदि आप बहुभाषी दस्तावेज़ों से निपट रहे हैं, या बस कम टाइपो चाहते हैं, तो बिल्ट‑इन स्पेल चेकर को ऑन करें और इंजन को भाषा का अनुमान लगाने दें।

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*यह कब उपयोगी है?* मान लीजिए आपकी स्कैन में अंग्रेज़ी और स्पेनिश दोनों सेक्शन हैं। ऑटो‑डिटेक्ट फीचर रन‑टाइम पर डिक्शनरी बदल देता है, जबकि स्पेल करेक्शन “0” को “O” जैसी गलत पढ़ी गई कैरेक्टर्स को ठीक करता है। यह स्टेप एक **searchable PDF** बनाने के लिए आवश्यक है जो सही परिणाम देता है।

---

## चरण 6: परिणाम सहेजें – इमेज को PDF में बदलें और सर्चेबल बनाएं  

अंत में हम इंजन को एक PDF लिखने के लिए कहते हैं जहाँ मूल इमेज एक अदृश्य टेक्स्ट लेयर के पीछे रहती है। यह क्लासिक **convert image to PDF** वर्कफ़्लो है, लेकिन अब PDF सर्चेबल है।

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

आउटपुट फ़ाइल (`output-searchable.pdf`) को किसी भी PDF व्यूअर में खोला जा सकता है; आप टेक्स्ट को चयन, कॉपी और सर्च कर पाएँगे जैसे कि वह नेेटिव PDF हो। अतिरिक्त टूल्स की ज़रूरत नहीं।

---

## पूर्ण कार्यशील उदाहरण – पेस्ट‑एंड‑रन  

नीचे पूरा प्रोग्राम दिया गया है, तैयार‑कम्पाइल करने के लिए। `YOUR_DIRECTORY` को उस फ़ोल्डर से बदलें जहाँ `input.jpg` रखा है।

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**अपेक्षित आउटपुट:** प्रोग्राम चलाने पर कंसोल में *“Searchable PDF generated successfully.”* दिखेगा। `output-searchable.pdf` को Adobe Reader में खोलें, मूल इमेज से कोई शब्द सर्च बॉक्स में टाइप करें और तुरंत उसकी लोकेशन पर जाएँ।

---

## सामान्य प्रश्न और किनारे के केस  

- **यदि GPU नहीं मिलता तो क्या होगा?**  
  `setDeviceType(OcrDeviceType.GPU)` कॉल एक्सेप्शन नहीं फेंकेगा; यह सिर्फ इंजन को पहले GPU आज़माने का निर्देश देता है। अगर विफल रहता है, तो इंजन चुपचाप CPU पर फॉलबैक हो जाता है।

- **क्या मैं एक रन में कई इमेज प्रोसेस कर सकता हूँ?**  
  हाँ। कोड को लूप में रखें, प्रत्येक इटरेशन में फ़ाइल नाम बदलें, और मेमोरी कम रखने के लिए वही `OcrEngine` इंस्टेंस पुनः‑उपयोग करें।

- **मेरी PDF बहुत बड़ी है—मैं इसे कैसे छोटा करूँ?**  
  OCR के बाद आप Aspose के PDF ऑप्टिमाइज़ेशन API का उपयोग कर सकते हैं, या सोर्स इमेज को डाउनस्केल कर सकते हैं (`ImageStream.fromFile(...).setResolution(150)` 150 DPI के लिए)।

- **क़ानूनी अनुपालन के लिए मुझे मूल इमेज रेज़ोल्यूशन रखना है।**  
  `PDF_SEARCHABLE` फॉर्मेट मूल बिटमैप को बिल्कुल वैसा ही रखता है; अदृश्य टेक्स्ट लेयर ऊपर जोड़ दी जाती है बिना विज़ुअल क्वालिटी बदले।

---

## विज़ुअल सारांश  

![create searchable pdf example](placeholder-image.png "create searchable pdf example")  
*Alt text:* *create searchable pdf example – Java OCR इंजन स्कैन की गई JPG को सर्चेबल PDF में बदल रहा है।*

---

## निष्कर्ष  

अब आपके पास **Aspose OCR for Java** का उपयोग करके किसी भी इमेज को **searchable PDF** में बदलने का **पूरा, एंड‑टू‑एंड समाधान** है। **इमेज को PDF में बदलना**, **स्पेल करेक्शन सक्षम करना**, और **संभव हो तो OCR GPU** का उपयोग करके आप तेज़, सटीक और सर्चेबल परिणाम प्राप्त कर सकते हैं जो सभी प्लेटफ़ॉर्म पर काम करते हैं।

अब आगे क्या? इन चीज़ों को आज़माएँ:

- **विभिन्न आउटपुट फॉर्मेट** (`PDF`, `DOCX`, `HTML`) ताकि आप देख सकें टेक्स्ट लेयर कैसे व्यवहार करती है।
- **कस्टम डिक्शनरी** यदि आप डोमेन‑स्पेसिफिक जार्गन प्रोसेस कर रहे हैं।
- **बैच प्रोसेसिंग** ताकि हजारों स्कैन को ऑटोमैटिकली हैंडल किया जा सके।

थ्रेड काउंट बदलें, फ़िल्टर स्वैप करें, या अपनी प्री‑प्रोसेसिंग पाइपलाइन जोड़ें। कोर पैटर्न वही रहता है: लोड → प्री‑प्रोसेस → कॉन्फ़िगर → OCR → सेव।

हैप्पी कोडिंग, और आपके PDFs हमेशा सर्चेबल रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}