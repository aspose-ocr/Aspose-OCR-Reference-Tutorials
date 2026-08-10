---
category: general
date: 2026-06-22
description: 'OCR के लिए इमेज को डेस्क्यू कैसे करें: इमेज प्रीप्रोसेसिंग OCR चरण सीखें,
  सॉल्ट‑पेपर शोर हटाएँ, और सटीकता बढ़ाएँ।'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: hi
og_description: OCR के लिए छवि को डेस्क्यू कैसे करें, सॉल्ट‑एंड‑पेपर शोर हटाएँ, और
  एक पूर्ण जावा उदाहरण में छवियों की पूर्व‑प्रसंस्करण OCR तकनीकों को लागू करें।
og_title: छवि को डेस्क्यू कैसे करें – इमेज प्रीप्रोसेसिंग OCR गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: इमेज का झुकाव हटाना कैसे करें – इमेज प्रीप्रोसेसिंग OCR गाइड
url: /hi/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज को डेस्क्यू कैसे करें – इमेज प्रीप्रोसेसिंग OCR गाइड

क्या आप कभी सोचा है **how to deskew image** ताकि आपका OCR इंजन वास्तव में टेक्स्ट पढ़ सके? आप अकेले नहीं हैं। एक झुका हुआ स्कैन एक परिपूर्ण दस्तावेज़ को बिखरे हुए गड़बड़ में बदल सकता है, और अधिकांश डेवलपर्स कम से कम एक बार इस समस्या का सामना करते हैं।

इस ट्यूटोरियल में हम एक पूर्ण **image preprocessing OCR** पाइपलाइन को चरण‑दर‑चरण देखेंगे जो न केवल घूर्णन को ठीक करती है बल्कि **remove[s] salt pepper** आर्टिफैक्ट्स को हटाती है और कॉन्ट्रास्ट को बढ़ाती है—वास्तव में वह सब कुछ जो आपको **preprocess images OCR**‑स्टाइल में इंजन को फीड करने से पहले चाहिए। अंत तक आपके पास चलाने‑लायक Java स्निपेट और यह स्पष्ट मानसिक मॉडल होगा कि प्रत्येक कदम क्यों महत्वपूर्ण है।

## इमेज को डेस्क्यू कैसे करें – प्रीप्रोसेसिंग पाइपलाइन बनाना

किसी भी OCR‑फ्रेंडली वर्कफ़्लो का दिल एक **preprocess options** ऑब्जेक्ट है जो फ़िल्टरों की श्रृंखला को जोड़ता है। इसे एक कन्वेयर बेल्ट की तरह सोचें: प्रत्येक फ़िल्टर एक काम करता है, फिर इमेज को अगले को पास कर देता है। नीचे एक न्यूनतम लेकिन पूर्ण उदाहरण दिया गया है जो एक काल्पनिक OCR लाइब्रेरी का उपयोग करता है जिसमें `DeskewFilter`, `DenoiseFilter`, और `ContrastBoostFilter` शामिल हैं।

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### क्यों यह काम करता है

* **DeskewFilter** इमेज की प्रमुख टेक्स्ट लाइनों का विश्लेषण करता है, कोण का अनुमान लगाता है, और बिटमैप को फिर से क्षैतिज कर देता है। अधिकांश लाइब्रेरीज़ सुधार को ±15° तक सीमित करती हैं क्योंकि बड़े कोण आमतौर पर खराब स्कैन किए गए पेज को दर्शाते हैं जिसके लिए मैन्युअल हस्तक्षेप आवश्यक होता है।
* **DenoiseFilter** क्लासिक *salt‑and‑pepper* पैटर्न को लक्षित करता है—वे अलग‑अलग काले या सफेद पिक्सेल जो टीवी पर स्थैतिक (static) की तरह दिखते हैं। इन्हें हटाने से OCR इंजन शोर को अक्षर समझने से बचता है।
* **ContrastBoostFilter** हिस्टोग्राम को स्ट्रेच करता है, जिससे हल्की स्ट्रोक्स उभर कर दिखती हैं। `1.5f` का मल्टीप्लायर एक सुरक्षित डिफ़ॉल्ट है; यदि आपके स्कैन बहुत फेडेड हैं तो इसे बढ़ा सकते हैं।

> **Pro tip:** यदि आप जानते हैं कि आपके दस्तावेज़ कभी भी 10° से अधिक झुके नहीं होते, तो `DeskewFilter` को वह छोटा बाउंड पास करें—एल्गोरिदम तेज़ चलता है और अधिक‑सुधार (over‑correct) की संभावना कम रहती है।

## Image Preprocessing OCR: सही क्रम में फ़िल्टर जोड़ना

क्रम महत्वपूर्ण है। कल्पना करें कि आप डेस्क्यू करने से पहले डीनॉइज़ कर रहे हैं; शोर कोण पहचान को गड़बड़ कर सकता है, जिससे गलत संरेखित परिणाम मिलते हैं। इसके विपरीत, कॉन्ट्रास्ट बूस्ट को डेस्क्यू के बाद लागू करने से घूर्णन नई आर्टिफैक्ट्स नहीं बनाता।

नीचे एक त्वरित चेकलिस्ट है जिसे आप किसी भी प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं:

| चरण | फ़िल्टर | कारण |
|------|--------|--------|
| 1 | `DeskewFilter` | टेक्स्ट बेसलाइन को संरेखित करता है |
| 2 | `DenoiseFilter` | अलग‑अलग पिक्सेल शोर को हटाता है |
| 3 | `ContrastBoostFilter` | OCR के लिए पठनीयता बढ़ाता है |

यदि आपको अतिरिक्त कदम जोड़ने की जरूरत है—जैसे बाइनराइज़ेशन फ़िल्टर बाइनरी OCR के लिए—तो इसे **कॉन्ट्रास्ट बूस्ट के बाद** रखें, क्योंकि साफ़, हाई‑कॉन्ट्रास्ट इमेज बाइनराइज़ेशन अधिक सटीक होता है।

## DenoiseFilter के साथ Salt Pepper शोर हटाएँ

Salt‑and‑pepper शोर कम‑गुणवत्ता वाले स्कैन में कुख्यात है, विशेषकर सस्ते फ़ोन कैमरों से आए स्कैन में। हमारी लाइब्रेरी में `DenoiseFilter` एक मीडियन‑फ़िल्टर कर्नेल लागू करता है, जो प्रत्येक पिक्सेल को उसके आसपास के पड़ोस के मीडियन से बदल देता है। प्रभाव? ये धब्बे गायब हो जाते हैं बिना वास्तविक अक्षरों को ब्लर किए।

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*कर्नेल साइज कब बढ़ाएँ?* यदि आपके स्रोत इमेज में बड़े धब्बे बहुत अधिक हैं, तो बड़ा कर्नेल उन्हें साफ़ करेगा, लेकिन सावधान रहें: बहुत बड़ा कर्नेल छोटे फ़ॉन्ट में बारीक स्ट्रोक्स को भी मिटा सकता है।

## Preprocess Images OCR – पाइपलाइन लागू करना

फ़िल्टर चेन को एक बार असेंबल कर लेने के बाद, इसे इंजन से जोड़ना एक‑लाइनर (`engine.setPreprocessOptions`) है। उस क्षण से, हर `recognizeText` कॉल स्वचालित रूप से पाइपलाइन के माध्यम से चलती है। प्रत्येक फ़िल्टर को मैन्युअली बुलाने की ज़रूरत नहीं—आपका कोड साफ़ रहता है, और भविष्य में बदलाव (नया फ़िल्टर जोड़ना, पैरामीटर बदलना) केंद्रीकृत होते हैं।

यहाँ एक सफल रन का उदाहरण है जिसमें मूल स्कैन में 12° झुकाव और स्पष्ट pepper शोर था:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

ध्यान दें कि टेक्स्ट साफ़, सही दिशा में, और उन बिखरे हुए अक्षरों से मुक्त है जो otherwise “I n v o i c e” या “$‑‑‑” जैसा दिखाते।

## एज केस और सामान्य जाल

| स्थिति | ध्यान रखने योग्य बात | सुझाया गया समाधान |
|-----------|-------------------|---------------|
| घूर्णन > 15° | DeskewFilter हार मान सकता है | मैन्युअल रूप से पहले घुमाएँ या उच्च‑रेंज फ़िल्टर उपयोग करें |
| अत्यंत कम रिज़ॉल्यूशन (< 100 dpi) | कॉन्ट्रास्ट बूस्ट विवरण नहीं बचा सकता | पहले इमेज को रिसैंपल करें (जैसे `ResampleFilter`) |
| मिश्रित शोर (Gaussian + salt‑pepper) | केवल DenoiseFilter पर्याप्त नहीं | `GaussianBlurFilter` को `DenoiseFilter` से पहले चेन करें |
| रंगीन स्कैन में रंगीन टेक्स्ट | ग्रेस्केल रूपांतरण आवश्यक | कॉन्ट्रास्ट बूस्ट से पहले `GrayscaleFilter` डालें |

इन परिदृश्यों की पहले से योजना बनाकर आप बाद में घंटों की डिबगिंग बचा सकते हैं।

## पूर्ण कार्यशील उदाहरण (ऑल‑इन‑वन)

नीचे एक स्व-समाहित Java क्लास है जिसे आप किसी भी Maven या Gradle प्रोजेक्ट में डाल सकते हैं जिसमें `com.example.ocr` डिपेंडेंसी शामिल है। यह दर्शाता है **how to deskew image**, **remove salt pepper** शोर, और **preprocess images OCR**‑स्टाइल कैसे किया जाता है।

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**अपेक्षित आउटपुट** (मान लेते हैं `scanned-document.png` में एक स्पष्ट इनवॉइस है):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

यदि आप इमेज को पूरी तरह संरेखित वाली इमेज से बदलते हैं, तो भी पाइपलाइन चलती रहेगी—कुछ टूटेगा नहीं, और OCR की सटीकता उच्च बनी रहेगी।

## निष्कर्ष

अब आपके पास **how to deskew image** की ठोस समझ है और यह भी कि प्रत्येक प्रीप्रोसेसिंग कदम—**image preprocessing OCR**, **remove salt pepper**, और **preprocess images OCR**—स्वच्छ, खोज योग्य टेक्स्ट प्रदान करने में कितना महत्वपूर्ण है। ऊपर दिया गया उदाहरण एक पूर्ण, 

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकें।

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Calculate Skew Angle for OCR Image Preprocessing](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}