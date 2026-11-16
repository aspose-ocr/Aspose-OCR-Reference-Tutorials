---
category: general
date: 2026-07-05
description: Python में तेज़ी से इमेज पर OCR करें। जानें कि OCR के लिए इमेज कैसे लोड
  करें, स्कैन किए हुए फॉर्म से टेक्स्ट निकालें, और Python में OCR का उपयोग करके इमेज
  को पहचानें।
draft: false
keywords:
- perform OCR on image
- load image for OCR
- how to use OCR Python
- extract text from scanned form
- OCR recognize image Python
language: hi
og_description: Python में इमेज पर OCR करें। यह ट्यूटोरियल दिखाता है कि OCR के लिए
  इमेज कैसे लोड करें, स्कैन किए गए फ़ॉर्म से टेक्स्ट निकालें, और OCR का उपयोग करके
  इमेज को पहचानें।
og_title: Python के साथ इमेज पर OCR करें – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image in Python quickly. Learn how to load image for
    OCR, extract text from scanned form, and use OCR recognize image Python.
  headline: Perform OCR on Image with Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python के साथ छवि पर OCR करें – पूर्ण गाइड
url: /hi/python-java/general/perform-ocr-on-image-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज पर OCR करें – पूर्ण गाइड

क्या आपको कभी **इमेज फ़ाइलों पर OCR करना** पड़ा है लेकिन Python में कहाँ से शुरू करें, यह नहीं पता था? आप अकेले नहीं हैं। चाहे आप रसीदें डिजिटाइज़ कर रहे हों, शोरयुक्त सर्वे फ़ॉर्म से डेटा निकाल रहे हों, या सिर्फ़ स्कैन किए गए PDF को सर्चेबल टेक्स्ट में बदल रहे हों, स्कैन किए गए फ़ॉर्म से टेक्स्ट निकालना कई डेवलपर्स के लिए रोज़मर्रा की समस्या है।

इस ट्यूटोरियल में हम **OCR Python** लाइब्रेरीज़ का उपयोग कैसे करें, इसे चरण‑दर‑चरण देखेंगे, चित्र लोड करने से लेकर फ़िल्टर किया हुआ परिणाम दिखाने तक। अंत तक आप बिल्कुल जान पाएँगे कि **load image for OCR** कैसे करें, confidence थ्रेशोल्ड कैसे सेट करें, और **OCR recognize image Python** मेथड को कैसे कॉल करें जो असली काम करता है।

> **आपको क्या मिलेगा:** एक तैयार‑स्क्रिप्ट जो इमेज लोड करती है, OCR चलाती है, और साफ़, confidence‑फ़िल्टर किया हुआ टेक्स्ट प्रिंट करती है। कोई अस्पष्ट रेफ़रेंस नहीं, कोई मिसिंग इम्पोर्ट नहीं—सिर्फ़ एक पूर्ण, कॉपी‑पेस्ट समाधान।

---

## आपको क्या चाहिए

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* Python 3.9 या उससे नया (कोड 3.10+ पर भी चलता है)।  
* एक OCR पैकेज जो नीचे दिखाए गए `ocr` API को फॉलो करता हो – उदाहरण के लिए, काल्पनिक `simple-ocr` लाइब्रेरी या कोई भी रैपर जो `OcrEngine`, `Language`, और `Image` को एक्सपोज़ करता हो।  
* एक इमेज फ़ाइल (`.png`, `.jpg`, आदि) जिसमें वह टेक्स्ट हो जिसे आप निकालना चाहते हैं।  
* एक टर्मिनल या IDE जहाँ आप एक ही Python स्क्रिप्ट चला सकें।

अगर आपके पास ये सब है, बढ़िया—चलते हैं।

---

## इमेज पर OCR करें – इंजन सेटअप करना

सबसे पहले आपको एक OCR इंजन इंस्टेंस बनाना होगा। इंजन को ऑपरेशन का दिमाग समझिए; यह पिक्सेल को पढ़ता है और उन्हें अक्षरों में बदलता है।

```python
# Import the OCR library – replace `ocr` with your actual package name
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*क्यों ज़रूरी है:* बिना इंजन के प्रोसेस करने को कुछ नहीं रहता। `OcrEngine` ऑब्जेक्ट वह सभी कॉन्फ़िगरेशन रखता है जिसे आप बाद में बदलेंगे, जैसे भाषा और confidence थ्रेशोल्ड।

---

## OCR के लिए इमेज लोड करें – स्कैन किए हुए फ़ॉर्म की तैयारी

अब जब इंजन मौजूद है, हमें **load image for OCR** करना होगा। लाइब्रेरी का `Image.load()` मेथड डिस्क से फ़ाइल पढ़ता है और उसे एक आंतरिक प्रतिनिधित्व में बदलता है जिसे इंजन समझता है।

```python
# Step 2: Load the image you want to process
# Replace the path with the actual location of your noisy form
image_path = "YOUR_DIRECTORY/noisy_form.png"
image = ocr.Image.load(image_path)
```

> **टिप:** अगर आप PDFs के साथ काम कर रहे हैं, तो पहले प्रत्येक पेज को इमेज में बदलें (जैसे `pdf2image` का उपयोग करके)। OCR इंजन केवल रास्टर इमेज को स्वीकार करता है।

---

## OCR Python का उपयोग कैसे करें – भाषा और confidence सेट करना

ज्यादातर OCR इंजन कई भाषाओं को सपोर्ट करते हैं और आपको कम‑confidence वाले अक्षरों को फ़िल्टर करने देते हैं। इन पैरामीटरों को पहले सेट करने से आपको केवल भरोसेमंद टेक्स्ट मिलता है।

```python
# Step 3: Choose language and set a confidence threshold
engine.language = ocr.Language.ENGLISH          # you can switch to FR, DE, etc.
engine.min_confidence = 85                     # accept only characters >85 % confidence
```

*85 % क्यों?* व्यवहार में, 80‑90 % के आसपास का थ्रेशोल्ड अधिकांश बकवास को हटा देता है जबकि अच्छा टेक्स्ट रखता है। अपनी स्कैन की क्वालिटी के अनुसार इसे समायोजित करें।

---

## स्कैन किए हुए फ़ॉर्म से टेक्स्ट निकालें – इमेज को पहचानना

इंजन तैयार है और इमेज लोड हो गई है, अब **perform OCR on image** करने का समय है। `recognize()` मेथड एक रिज़ल्ट ऑब्जेक्ट लौटाता है जिसमें निकाला गया टेक्स्ट और वैकल्पिक रूप से बाउंडिंग‑बॉक्स डेटा होता है।

```python
# Step 4: Perform OCR recognition on the image
result = engine.recognize(image)
```

अगर लाइब्रेरी सपोर्ट करती है, तो `result` में `result.confidences` (प्रति‑अक्षर confidence स्कोर की लिस्ट) और `result.words` (स्ट्रक्चर्ड वर्ड ऑब्जेक्ट) भी हो सकते हैं। इस गाइड में हम साधारण टेक्स्ट आउटपुट पर ध्यान देंगे।

---

## OCR Recognize Image Python – फ़िल्टर किया हुआ परिणाम दिखाना

अंत में, फ़िल्टर किया हुआ टेक्स्ट प्रिंट करते हैं। कम‑confidence वाले प्रतीक प्रश्न चिह्न (`?`) के रूप में दिखते हैं क्योंकि हमने `min_confidence` को 85 % पर सेट किया है।

```python
# Step 5: Show the filtered text
print("Filtered text:")
print(result.text)
```

### अपेक्षित आउटपुट

```
Filtered text:
Name: John Doe
Date: 2023‑04‑15
Amount: $123.45
Signature: ?
```

ध्यान दें कि अपठनीय सिग्नेचर `?` में बदल गया। यही confidence फ़िल्टर का उद्देश्य है—आउटपुट को साफ़ रखना ताकि आगे की प्रोसेसिंग आसान हो।

---

## सामान्य समस्याएँ और प्रो टिप्स

| समस्या | क्यों होती है | त्वरित समाधान |
|-------|----------------|-----------|
| **खाली आउटपुट** | इमेज बहुत डार्क या लो‑रेज़ोल्यूशन है। | OpenCV से प्री‑प्रोसेस करें: कंट्रास्ट बढ़ाएँ, रिज़ॉल्यूशन ≥300 dpi रखें। |
| **गड़बड़ अक्षर** | गलत भाषा चुनी गई। | `engine.language` को दस्तावेज़ की भाषा से मिलाएँ (जैसे `ocr.Language.FRENCH`)। |
| **बहुत सारे `?` चिन्ह** | confidence थ्रेशोल्ड बहुत ऊँचा है। | `engine.min_confidence` को 70‑80 % पर घटाएँ, विशेषकर शोरयुक्त स्कैन के लिए। |
| **Unicode त्रुटियाँ** | आउटपुट में non‑ASCII अक्षर हैं लेकिन कंसोल एन्कोडिंग गलत है। | `python -X utf8` चलाएँ या `PYTHONIOENCODING=utf-8` सेट करें। |

**प्रो टिप:** अगर आपको टेबल निकालनी है, तो रॉ टेक्स्ट फ़िल्टर करने के बाद एक लेआउट‑अवेयर OCR इंजन (जैसे Tesseract का `--psm 6`) चलाएँ।

---

## पूर्ण स्क्रिप्ट – चलाने के लिए तैयार

नीचे पूरा, स्व-निर्भर स्क्रिप्ट दिया गया है जिसमें हमने चर्चा किए सभी चरण शामिल हैं। इसे `perform_ocr.py` के रूप में सेव करें, इमेज पाथ एडजस्ट करें, और `python perform_ocr.py` चलाएँ।

```python
# perform_ocr.py
# -------------------------------------------------
# Complete Python script to perform OCR on image,
# load image for OCR, configure engine, and display
# filtered results. Works with any OCR library that
# follows the simple `ocr` API shown here.
# -------------------------------------------------

import ocr  # Replace with your actual OCR package name

def main():
    # 1️⃣ Create the engine
    engine = ocr.OcrEngine()

    # 2️⃣ Configure language and confidence
    engine.language = ocr.Language.ENGLISH
    engine.min_confidence = 85  # Only keep chars >85 % confidence

    # 3️⃣ Load the image (adjust the path)
    image_path = "YOUR_DIRECTORY/noisy_form.png"
    image = ocr.Image.load(image_path)

    # 4️⃣ Recognize the text
    result = engine.recognize(image)

    # 5️⃣ Print the filtered output
    print("Filtered text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

चलाएँ, और आपको कंसोल में फ़िल्टर किया हुआ टेक्स्ट दिखेगा—बिल्कुल वही जो **extract text from scanned form** चरण का वादा करता है।

---

## आगे क्या?

अब जब आप जानते हैं कि **perform OCR on image** और **extract text from scanned form** कैसे किया जाता है, आप आगे देख सकते हैं:

* **बैच प्रोसेसिंग** – इमेज की डायरेक्टरी पर लूप चलाकर परिणामों की CSV बनाएं।  
* **पोस्ट‑प्रोसेसिंग** – regex या spaCy का उपयोग करके डेट, अमाउंट, या IDs जैसे फ़ील्ड निकालें।  
* **इंटीग्रेशन** – OCR आउटपुट को डेटाबेस, Google Sheets, या REST API में फीड करें।  

इन सभी विचारों में वही कोर फ़ंक्शन शामिल हैं जो हमने कवर किए: इमेज लोड करना, इंजन कॉन्फ़िगर करना, और **OCR recognize image Python** मेथड को कॉल करना।

---

## निष्कर्ष

हमने एक पूर्ण, प्रोडक्शन‑रेडी उदाहरण के साथ दिखाया कि कैसे **perform OCR on image** Python से किया जाता है। **load image for OCR** से लेकर भाषा कॉन्फ़िगर करने, confidence थ्रेशोल्ड सेट करने, और अंत में **extract text from scanned form** करने तक, हर कदम स्पष्ट कोड और व्याख्या के साथ प्रस्तुत किया गया। अब आपके पास एक ठोस आधार है जिससे आप अधिक जटिल परिदृश्यों को संभाल सकें—चाहे वह बैच जॉब्स हों, मल्टी‑लैंग्वेज सपोर्ट हो, या टेबल एक्सट्रैक्शन।

स्क्रिप्ट चलाएँ, थ्रेशोल्ड समायोजित करें, और देखें कि आपके दस्तावेज़ मिनटों में सर्चेबल बन जाएँ। कोई सवाल या कठिन फ़ॉर्म है जो सहयोग नहीं कर रहा? नीचे कमेंट करें, हम साथ मिलकर ट्रबलशूट करेंगे। हैप्पी कोडिंग!

![इमेज पर OCR करने का उदाहरण](example.png "इमेज पर OCR करने का उदाहरण")


## अगला आप क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों से निकटता से जुड़े हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}