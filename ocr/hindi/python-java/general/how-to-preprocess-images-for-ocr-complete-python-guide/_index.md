---
category: general
date: 2026-06-06
description: Python का उपयोग करके OCR के लिए छवियों की पूर्व-प्रसंस्करण कैसे करें।
  Otsu विधि से छवि को बाइनराइज़ करना, स्कैन किए गए दस्तावेज़ों को डेस्क्यू करना, और
  जर्मन टेक्स्ट के लिए OCR की सटीकता सुधारना सीखें।
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: hi
og_description: Python में OCR के लिए छवियों की पूर्व-प्रसंस्करण कैसे करें। यह ट्यूटोरियल
  Otsu का उपयोग करके छवि को बाइनराइज़ करना, स्कैन किए गए दस्तावेज़ों को डेस्क्यू करना,
  और जर्मन छवियों के लिए OCR की सटीकता को सुधारने का तरीका दिखाता है।
og_title: OCR के लिए छवियों की पूर्व-प्रसंस्करण कैसे करें – पूर्ण पायथन गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: OCR के लिए छवियों को कैसे प्रीप्रोसेस करें – पूर्ण पायथन गाइड
url: /hi/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR के लिए इमेज प्रीप्रोसेस कैसे करें – पूर्ण Python गाइड

क्या आपने कभी सोचा है **इमेज को OCR के लिए कैसे प्रीप्रोसेस करें** ताकि टेक्स्ट बिल्कुल स्पष्ट निकले? आप अकेले नहीं हैं। स्कैन किए हुए दस्तावेज़—विशेषकर शोरयुक्त जर्मन पृष्ठ—किसी भी OCR इंजन के लिए दुःस्वप्न बन सकते हैं। अच्छी खबर? कुछ स्मार्ट प्रीप्रोसेसिंग स्टेप्स एक धुंधली, धब्बेदार स्कैन को साफ़, मशीन‑रेडेबल इमेज में बदल सकते हैं।

इस ट्यूटोरियल में हम एक व्यावहारिक उदाहरण के माध्यम से दिखाएंगे **इमेज को OCR के लिए कैसे प्रीप्रोसेस करें** Python का उपयोग करके। आप सीखेंगे **Otsu से इमेज को बाइनराइज़ करना**, **स्कैन किए हुए दस्तावेज़ों को कैसे डेस्क्यू करें**, और कुल मिलाकर **OCR की सटीकता कैसे बढ़ाएँ** जब आपको **जर्मन इमेज फ़ाइलों से टेक्स्ट निकालना** हो। कोई फालतू बातें नहीं, सिर्फ एक कार्यशील स्क्रिप्ट जिसे आप आज ही कॉपी‑पेस्ट कर सकते हैं।

## What You’ll Need

- **Python 3.9+** (कोई भी हालिया संस्करण चलेगा)
- एक OCR लाइब्रेरी जो `OcrEngine` क्लास प्रदान करती है – डेमो के लिए हम मानेंगे कि एक सामान्य `ocr` पैकेज है। इसे `pip install ocr-lib` से इंस्टॉल करें।
- एक शोरयुक्त जर्मन स्कैन (`noisy_german_scan.tif`) जिसे आप टेस्ट करना चाहते हैं।
- Python फ़ंक्शन की बुनियादी समझ (यदि आपने पहले `def` लिखा है, तो आप तैयार हैं)।

> **Pro tip:** यदि आप कोई अलग OCR SDK (जैसे `pytesseract` के माध्यम से Tesseract) उपयोग कर रहे हैं, तो अवधारणाएँ वही रहती हैं—सिर्फ मेथड नामों को अनुकूलित करें।

## Overview of the Solution

1. **एक OCR इंजन इंस्टेंस बनाएं।**  
2. **पहचान भाषा को जर्मन सेट करें।**  
3. **एक कस्टम प्रीप्रोसेसिंग पाइपलाइन बनाएं** जिसमें डेस्क्यूइंग, डिनॉइज़िंग, बाइनराइज़ेशन (Otsu) और कंट्रास्ट स्ट्रेचिंग शामिल हों।  
4. **पाइपलाइन को इंजन से जोड़ें** ताकि हर इमेज स्वचालित रूप से उस पर गुज़रें।  
5. **शोरयुक्त जर्मन स्कैन पर OCR चलाएँ।**  
6. **निकाले गए टेक्स्ट को प्रिंट करें** ताकि परिणाम की पुष्टि हो सके।

नीचे हम प्रत्येक चरण को तोड़कर समझाते हैं, **क्यों** यह महत्वपूर्ण है, और आपको बिल्कुल वही कोड दिखाते हैं जिसकी आपको जरूरत है।

![OCR के लिए इमेज प्रीप्रोसेस कैसे करें उदाहरण](image.png "OCR के लिए इमेज प्रीप्रोसेस कैसे करें उदाहरण")

## Step 1: Create an OCR Engine Instance

सबसे पहले—बिना इंजन के कुछ नहीं होता। `OcrEngine` ऑब्जेक्ट वह एंट्री पॉइंट है जो बाद की सभी प्रोसेसिंग को समन्वयित करता है।

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*Why this matters:* इंजन को इनिशियलाइज़ करने से आंतरिक रिसोर्सेज (जैसे भाषा मॉडल) सेट होते हैं और आपको बाद में कस्टम पाइपलाइन जोड़ने के लिए एक साफ़ स्लेट मिलती है।

## Step 2: Set the Recognition Language to German

OCR की सटीकता भाषा‑निर्भर होती है। इंजन को जर्मन की अपेक्षा बताकर आप सही कैरेक्टर सेट और भाषा मॉडल को सक्रिय करते हैं।

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

यदि आप यह कदम छोड़ देते हैं, तो इंजन डिफ़ॉल्ट रूप से अंग्रेज़ी ले सकता है, जिससे umlauts (ä, ö, ü) और ß कैरेक्टर को गलत पहचान सकता है—जर्मन स्कैन के साथ अक्सर होने वाली समस्या।

## Step 3: Build a Custom Preprocessing Pipeline

यह **इमेज को OCR के लिए कैसे प्रीप्रोसेस करें** का मुख्य भाग है। हम चार ट्रांसफ़ॉर्मेशन को चेन करेंगे:

| ट्रांसफ़ॉर्मेशन | क्या करता है | क्यों मदद करता है |
|----------------|--------------|-------------------|
| **Deskew** | इमेज को क्षैतिज (अधिकतम 5°) पर फिर से घुमाता है | स्कैन अक्सर पूरी तरह संरेखित नहीं होते; डेस्क्यूइंग उस झुकाव को हटाता है जो कैरेक्टर सेगमेंटेशन को भ्रमित करता है। |
| **Denoise** | रैंडम स्पॉट्स को कम करता है (strength 0.7) | शोर झूठी किनारों को बनाता है जिन्हें OCR इंजन कैरेक्टर समझ सकता है। |
| **Binarize (Otsu)** | Otsu मेथड से ब्लैक‑एंड‑व्हाइट में बदलता है | एक साफ़ बाइनरी इमेज फ़ोरग्राउंड (टेक्स्ट) और बैकग्राउंड के बीच तीव्र कंट्रास्ट देती है। |
| **Contrast Stretch** | डायनामिक रेंज को विस्तारित करता है | फीके स्ट्रोक्स की पठनीयता बढ़ाता है, विशेषकर पुराने दस्तावेज़ों पर। |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### How to Deskew Scanned Documents

उपर्युक्त `deskew` कॉल सीधे **स्कैन किए हुए दस्तावेज़ों को कैसे डेस्क्यू करें** का उत्तर देती है। यह आंतरिक रूप से Hough ट्रांसफ़ॉर्म द्वारा प्रमुख टेक्स्ट लाइन एंगल का अनुमान लगाती है और इमेज को फिर से घुमाती है। यदि आपके दस्तावेज़ 5° से अधिक घुंमें हुए हैं, तो `max_angle` को बढ़ाएँ, लेकिन ओवर‑रोटेशन आर्टिफैक्ट से सावधान रहें।

### Binarize Image Using Otsu

`binarize(method="otsu")` लाइन सीधे **Otsu से इमेज को बाइनराइज़ कैसे करें** प्रश्न का उत्तर देती है। Otsu का एल्गोरिद्म एक थ्रेशोल्ड निकालता है जो intra‑class variance को न्यूनतम करता है, जो डार्क टेक्स्ट बनाम लाइट बैकग्राउंड वाले दस्तावेज़ों के लिए आदर्श है।

## Step 4: Attach the Pipeline to the Engine

अब हम OCR इंजन को बताते हैं कि हर आने वाली इमेज को हमने अभी बनाई हुई पाइपलाइन के माध्यम से प्रोसेस किया जाए।

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*Why this matters:* पाइपलाइन को रजिस्टर किए बिना, इंजन कच्ची स्कैन को प्रोसेस करेगा और हमने जो भी सफ़ाई की है, उसे अनदेखा कर देगा। यह कदम **OCR की सटीकता कैसे बढ़ाएँ** को सुनिश्चित करता है, क्योंकि वही प्रीप्रोसेसिंग लगातार लागू होती है।

## Step 5: Recognize Text from a Noisy German Scan

अब सब कुछ एक साथ जोड़ते हैं। हम इंजन को शोरयुक्त जर्मन इमेज देते हैं और उसे काम करने देते हैं।

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

यदि आप प्रदर्शन के बारे में जिज्ञासु हैं, तो कॉल को टाइम कर सकते हैं:

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## Step 6: Output the Recognized Text

अंत में, हम निकाले गए स्ट्रिंग को प्रिंट करते हैं। यह सीधे **जर्मन इमेज से टेक्स्ट निकालें** प्रश्न का उत्तर है।

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### Expected Output

मान लीजिए सैंपल स्कैन में वाक्य “Die schnelle braune Füchsin springt über den faulen Hund.” है, तो आपको कुछ इस तरह दिखना चाहिए:

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

यदि आउटपुट में अभी भी गड़बड़ अक्षर दिखें, तो `denoise` स्ट्रेंथ को समायोजित करें या डेस्क्यूइंग के लिए `max_angle` बढ़ाएँ।

## Common Pitfalls & How to Tackle Them

- **भाषा मॉडल की कमी:** `set_recognition_language(Language.GERMAN)` को भूलने से अक्सर umlauts गायब रह जाते हैं। इस कॉल को दोबारा जाँचें।
- **ओवर‑डिनॉइज़िंग:** 0.9 से ऊपर की स्ट्रेंथ पतली स्ट्रोक्स को मिटा सकती है, विशेषकर पुराने फ़ॉन्ट्स में। अधिकांश मामलों में 0.5‑0.7 रखें।
- **गलत फ़ाइल फ़ॉर्मेट:** कुछ OCR इंजन मल्टी‑पेज TIFF को संभाल नहीं पाते। यदि आपके पास मल्टी‑पेज दस्तावेज़ है, तो पहले उसे सिंगल‑पेज फ़ाइलों में बाँटें।
- **पाइपलाइन क्रम:** दिखाया गया क्रम (डेस्क्यू → डिनॉइज़ → बाइनराइज़ → कंट्रास्ट) जानबूझकर है। बाइनराइज़ करने से पहले डिनॉइज़ करना जरूरी है; नहीं तो शोर स्थिर हो जाता है।

## Extending the Pipeline (What’s Next?)

अब आपके पास एक ठोस बेसलाइन है, आप आगे चाहेंगे:

- **मॉर्फ़ोलॉजिकल ओपनिंग** जोड़ें ताकि छोटे ब्लॉब साफ़ हों (`.morph_open(kernel=3)`)।
- **भाषा मॉडल** को इंटीग्रेट करें पोस्ट‑प्रोसेसिंग करेक्शन के लिए (`ocr_engine.apply_spellcheck()`)।
- **बड़े डेटासेट** के लिए बैच प्रोसेसिंग को `concurrent.futures` से पैराललाइज़ करें।

इन सभी को जोड़ने से **इमेज को OCR के लिए कैसे प्रीप्रोसेस करें** की मूल अवधारणा बनी रहती है, जबकि **OCR की सटीकता कैसे बढ़ाएँ** और भी बेहतर हो जाती है।

## Conclusion

हमने अभी-अभी **इमेज को OCR के लिए कैसे प्रीप्रोसेस करें** को शुरू से अंत तक कवर किया: एक इंजन बनाएं, जर्मन भाषा सेट करें, एक पाइपलाइन बनाएं जो **Otsu से इमेज को बाइनराइज़ करे**, **स्कैन किए हुए दस्तावेज़ों को कैसे डेस्क्यू करें**, और अंत में **जर्मन इमेज से टेक्स्ट निकालें** उच्च विश्वसनीयता के साथ। ऊपर बताए गए छह चरणों का पालन करके आप पहचान की गुणवत्ता में स्पष्ट सुधार देखेंगे—अब और अनंत मैन्युअल सुधार नहीं।

स्क्रिप्ट को अपने स्कैन के साथ चलाएँ, पैरामीटरों के साथ प्रयोग करें, और परिणाम खुद बोलें। किसी विशेष प्रीप्रोसेसिंग ट्यूनिंग के बारे में सवाल हैं? टिप्पणी करें, हम साथ‑साथ गहराई में जाएंगे।

Happy coding, and may your OCR be ever accurate!


## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकें।

- [Aspose.OCR का उपयोग करके भाषा चयन के साथ C# में इमेज टेक्स्ट निकालें](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [OCR इमेज रिकग्निशन में थ्रेशोल्ड वैल्यू कैसे सेट करें](/ocr/english/net/ocr-settings/set-threshold-value/)
- [इमेज OCR – OCR इमेज रिकग्निशन में इमेज पर OCR कैसे करें](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}