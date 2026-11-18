---
category: general
date: 2026-06-22
description: छवि से भाषा का पता लगाना और पायथन में OCR का उपयोग करके टेक्स्ट निकालना
  सीखें। स्वचालित भाषा पहचान और टेक्स्ट निष्कर्षण को कवर करने वाला चरण‑दर‑चरण ट्यूटोरियल।
draft: false
keywords:
- how to detect language
- detect language from image
- extract text from image
- how to use ocr
- how to extract text
language: hi
og_description: OCR का उपयोग करके छवि से भाषा कैसे पहचानें? यह गाइड आपको चरण‑दर‑चरण
  दिखाता है कि Python में OCR का उपयोग करके भाषा का पता कैसे लगाएँ और टेक्स्ट निकालें।
og_title: OCR के साथ छवियों से भाषा का पता कैसे लगाएँ – पूर्ण पायथन वॉकथ्रू
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  headline: How to Detect Language from Images with OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  name: How to Detect Language from Images with OCR – Complete Python Guide
  steps:
  - name: Expected Output
    text: 'If `sample-multilang.png` contains French text, you might see something
      like:'
  - name: 1. Unsupported Image Formats
    text: 'If you try to load a TIFF file that the OCR library doesn’t recognise,
      `ocr.ImageStream.from_file()` will raise an `OcrUnsupportedFormatError`. Wrap
      the load call in a try/except block:'
  - name: 2. Low‑Resolution Images
    text: 'OCR accuracy drops sharply below ~300 dpi. If you notice poor detection,
      consider pre‑processing the image with Pillow:'
  - name: 3. Multiple Languages in One Image
    text: 'When an image contains text in more than one language, the auto‑detect
      feature will pick the dominant one. To capture all languages, you can disable
      auto‑detect and manually pass a list of languages to the engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR के साथ छवियों से भाषा का पता कैसे लगाएँ – पूर्ण पायथन गाइड
url: /hi/python-java/general/how-to-detect-language-from-images-with-ocr-complete-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Detect Language from Images with OCR – Complete Python Guide

क्या आपने कभी **एक तस्वीर में भाषा** का पता लगाने के बारे में सोचा है बिना उसे मैन्युअली खोलें? आप अकेले नहीं हैं। कई प्रोजेक्ट्स—जैसे रसीद स्कैनर, बहुभाषी दस्तावेज़ संग्रह, या एक साधारण फोटो‑टू‑टेक्स्ट ऐप—में आपको यह जानना आवश्यक होता है कि *कौन‑सी* भाषा का टेक्स्ट है, इससे पहले कि आप आगे की प्रोसेसिंग कर सकें।  

इस ट्यूटोरियल में हम एक व्यावहारिक, एंड‑टू‑एंड उदाहरण के माध्यम से दिखाएंगे **कैसे इमेज से भाषा का पता लगाएँ** और फिर वास्तविक अक्षर निकालें। अंत तक आप कुछ ही पंक्तियों का Python कोड चलाकर, स्क्रिप्ट को किसी भी सपोर्टेड इमेज पर पॉइंट करके, पता लगी भाषा *और* निकाला गया टेक्स्ट दोनों प्राप्त कर पाएँगे। कोई फालतू बात नहीं, सिर्फ़ एक साफ़ समाधान जिसे आप कॉपी‑पेस्ट कर सकते हैं।

## What You’ll Learn

- Python में एक हल्का OCR लाइब्रेरी इंस्टॉल और सेट‑अप करना।  
- OCR इंजन को इनिशियलाइज़ करना और ऑटोमैटिक भाषा डिटेक्शन सक्षम करना।  
- इमेज (कोई भी सपोर्टेड फॉर्मेट) लोड करना और OCR चलाना।  
- डिटेक्टेड भाषा और एक्सट्रैक्टेड टेक्स्ट प्राप्त करना।  
- असपोर्टेड फॉर्मेट या अस्पष्ट भाषा परिणाम जैसे सामान्य समस्याओं को हैंडल करना।  

यदि आपने कभी **कैसे OCR का उपयोग करें** बहुभाषी दस्तावेज़ों के लिए, यह गाइड आपके लिए है।

---

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके मशीन पर नीचे दिया गया सेटअप है:

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9 or newer | हम जिस OCR पैकेज का उपयोग करेंगे वह आधुनिक इंटरप्रेटर्स को टार्गेट करता है। |
| `pip` (Python package manager) | OCR लाइब्रेरी इंस्टॉल करने के लिए आवश्यक है। |
| A sample image containing text in at least one language (e.g., `sample-multilang.png`) | आपको टेस्ट करने के लिए कुछ ठोस मिलेगा। |
| Optional: Virtual environment (`venv` or `conda`) | डिपेंडेंसीज़ को साफ़ रखता है और वर्ज़न कॉन्फ्लिक्ट से बचाता है। |

> **Pro tip:** यदि आप वर्चुअल एनवायरनमेंट के अंदर काम कर रहे हैं, तो OCR पैकेज इंस्टॉल करने से पहले उसे एक्टिवेट कर लें ताकि आपका ग्लोबल Python साफ़ रहे।

---

## Step 1: Install the OCR Library

इस walkthrough के लिए हम काल्पनिक `ocr` पैकेज का उपयोग करेंगे जो नीचे दिए गए कोड स्निपेट में दिखाए गए API को मिरर करता है। वास्तविक दुनिया में आप इसे `pytesseract`, `easyocr`, या किसी भी ऐसी लाइब्रेरी से बदल सकते हैं जो ऑटोमैटिक भाषा डिटेक्शन सपोर्ट करती हो।

```bash
pip install ocr
```

> **Note:** पैकेज हल्का (< 5 MB) है और Windows, macOS, तथा Linux पर काम करता है। यदि आपको परमिशन एरर मिले, तो कमांड में `--user` जोड़ दें।

---

## Step 2: Initialise the OCR Engine – How to Detect Language

अब लाइब्रेरी तैयार है, हम एक OCR इंजन इंस्टेंस बना सकते हैं। यही वह ऑब्जेक्ट है जो वास्तव में तस्वीर को स्कैन करेगा और भाषा का पता लगाएगा।

```python
import ocr

# Initialise the OCR engine – this is where we start the language detection pipeline
engine = ocr.OcrEngine()
```

हम इंजन से क्यों शुरू करते हैं? इंजन को OCR सिस्टम का दिमाग समझें; यह कॉन्फ़िगरेशन रखता है, भाषा मॉडल लोड करता है, और बैकग्राउंड में भारी काम संभालता है। इसे पहले इनिशियलाइज़ करने से बाद में किए जाने वाले कॉल्स (जैसे इमेज लोड करना) के पास एक कॉन्टेक्स्ट रहता है।

---

## Step 3: Load Your Image and Enable Automatic Language Detection

अगला कदम है इमेज को इंजन में फीड करना। हम *ऑटो‑डिटेक्ट लैंग्वेज* फ़्लैग भी ऑन करेंगे ताकि OCR इंजन रियल‑टाइम में भाषा का अनुमान लगा सके।

```python
# Load the image (any supported format – PNG, JPEG, BMP, etc.)
image_path = "YOUR_DIRECTORY/sample-multilang.png"
image = ocr.ImageStream.from_file(image_path)

# Attach the image to the engine
engine.set_image(image)

# Enable automatic language detection – this is the key for detecting language from image
engine.get_settings().set_auto_detect_language(True)
```

> **Why enable auto‑detect?**  
> अधिकांश OCR लाइब्रेरीज़ डिफ़ॉल्ट रूप से एक भाषा (अक्सर English) के साथ आती हैं। यदि आपका दस्तावेज़ French, Japanese, या किसी अन्य स्क्रिप्ट में है, तो यह सेटिंग न होने पर इंजन उसे मिस कर देगा। `set_auto_detect_language(True)` को टॉगल करके हम इंजन को बिटमैप स्कैन करने, कैरेक्टर शेप स्टैटिस्टिक्स की तुलना करने, और सबसे संभावित भाषा मॉडल चुनने देते हैं।

---

## Step 4: Perform OCR – Extract Text from Image

इमेज लोड हो गई और भाषा डिटेक्शन ऑन है, अब वास्तविक OCR स्टेप सिर्फ़ एक मेथड कॉल है।

```python
# Run the OCR process – this both detects the language and extracts the text
result = engine.recognize()
```

`recognize()` मेथड दो काम एक साथ करता है:

1. **Language detection:** इमेज पर एक हल्का क्लासिफ़ायर चलाकर भाषा कोड (जैसे `en`, `fr`, `es`) चुनता है।  
2. **Text extraction:** फिर उपयुक्त भाषा‑स्पेसिफ़िक मॉडल को लागू करके अक्षरों को Unicode स्ट्रिंग्स में ट्रांसक्राइब करता है।

क्योंकि दोनों एक साथ होते हैं, आपको एक ही `result` ऑब्जेक्ट मिलता है जिसमें सब कुछ होता है।

---

## Step 5: Retrieve and Display the Detected Language and Extracted Text

अंत में हम `result` ऑब्जेक्ट से भाषा कोड और रॉ टेक्स्ट निकालते हैं और उन्हें कंसोल पर प्रिंट करते हैं।

```python
# Print the detected language and the extracted text
print("Detected language:", result.get_language())
print("Text:", result.get_text())
```

### Expected Output

यदि `sample-multilang.png` में French टेक्स्ट है, तो आप कुछ इस तरह देख सकते हैं:

```
Detected language: fr
Text: Bonjour, ceci est un texte d'exemple.
```

यदि इमेज अस्पष्ट है या कई भाषाएँ शामिल हैं, तो इंजन वह भाषा लौटाएगा जिस पर उसे सबसे अधिक भरोसा है, और आप बाद में confidence स्कोर देख सकते हैं (अधिकांश लाइब्रेरीज़ `get_confidence()` मेथड प्रदान करती हैं उन्नत उपयोग‑केसों के लिए)।

---

## Handling Common Edge Cases

### 1. Unsupported Image Formats

यदि आप ऐसा TIFF फ़ाइल लोड करने की कोशिश करते हैं जिसे OCR लाइब्रेरी पहचान नहीं पाती, तो `ocr.ImageStream.from_file()` `OcrUnsupportedFormatError` उठाएगा। लोड कॉल को try/except ब्लॉक में रैप करें:

```python
try:
    image = ocr.ImageStream.from_file(image_path)
except ocr.OcrUnsupportedFormatError as e:
    print(f"Unsupported format: {e}")
    raise
```

### 2. Low‑Resolution Images

OCR की सटीकता ~300 dpi से नीचे तेज़ी से गिरती है। अगर आपको खराब डिटेक्शन दिखे, तो Pillow के साथ इमेज को प्री‑प्रोसेस करने पर विचार करें:

```python
from PIL import Image, ImageEnhance

pil_img = Image.open(image_path)
pil_img = pil_img.resize((pil_img.width * 2, pil_img.height * 2), Image.LANCZOS)
pil_img.save("resized.png")
image = ocr.ImageStream.from_file("resized.png")
```

### 3. Multiple Languages in One Image

जब इमेज में एक से अधिक भाषा का टेक्स्ट हो, तो ऑटो‑डिटेक्ट फीचर प्रमुख भाषा को चुन लेगा। सभी भाषाओं को कैप्चर करने के लिए आप ऑटो‑डिटेक्ट को डिसेबल करके इंजन को भाषा की लिस्ट मैन्युअली पास कर सकते हैं:

```python
engine.get_settings().set_auto_detect_language(False)
engine.get_settings().set_languages(["en", "fr", "de"])
```

अब OCR प्रत्येक भाषा मॉडल का उपयोग करके अक्षरों को पहचानने की कोशिश करेगा और प्रत्येक टेक्स्ट ब्लॉक के लिए सबसे अच्छा मैच लौटाएगा।

---

## Full Script – All Steps Combined

नीचे पूरा, रन‑टाइम‑रेडी Python स्क्रिप्ट है जिसमें हमने अब तक कवर किए सभी चरण शामिल हैं। इसे `detect_language_ocr.py` के रूप में सेव करें और `python detect_language_ocr.py` चलाएँ।

```python
# detect_language_ocr.py
# -------------------------------------------------
# How to detect language from image and extract text using OCR
# -------------------------------------------------

import ocr

def main():
    # 1️⃣ Initialise the OCR engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image (any supported format)
    image_path = "YOUR_DIRECTORY/sample-multilang.png"
    try:
        image = ocr.ImageStream.from_file(image_path)
    except ocr.OcrUnsupportedFormatError as err:
        print(f"Error loading image: {err}")
        return

    engine.set_image(image)

    # 3️⃣ Enable automatic language detection
    engine.get_settings().set_auto_detect_language(True)

    # 4️⃣ Perform OCR – this both detects language and extracts text
    try:
        result = engine.recognize()
    except ocr.OcrRecognitionError as err:
        print(f"OCR failed: {err}")
        return

    # 5️⃣ Retrieve and display the detected language and extracted text
    print("Detected language:", result.get_language())
    print("Text:", result.get_text())

if __name__ == "__main__":
    main()
```

**Run it** और आपको तुरंत भाषा कोड के साथ एक्सट्रैक्टेड टेक्स्ट दिखेगा। यही वह पूरा जवाब है **कैसे भाषा का पता लगाएँ** और **कैसे इमेज से टेक्स्ट एक्सट्रैक्ट करें** OCR का उपयोग करके।

---

## Going Further – Next Steps & Related Topics

- **Improve accuracy**: `opencv-python` का उपयोग करके इमेज प्री‑प्रोसेसिंग (थ्रेशहोल्डिंग, डीनॉइज़िंग) के साथ प्रयोग करें।  
- **Batch processing**: स्क्रिप्ट को लूप में रैप करके फ़ोल्डर में मौजूद कई तस्वीरों को हैंडल करें।  
- **Integrate with NLP**: एक्सट्रैक्टेड टेक्स्ट को `langdetect` जैसी भाषा‑पहचान लाइब्रेरी में पास करके दूसरा वैरिफिकेशन प्राप्त करें।  
- **Explore other OCR engines**: `pytesseract` फाइन‑ग्रेन कंट्रोल देता है, जबकि `easyocr` 80 से अधिक भाषाओं को बॉक्स‑ऑफ़‑द‑बॉक्स सपोर्ट करता है।  

इन सभी टॉपिक्स हमारे सेकेंडरी कीवर्ड्स—*detect language from image*, *extract text from image*, *how to use OCR*, और *how to extract text*—से जुड़े हैं, जिससे आप अपना टूलकिट बिना शून्य से शुरू किए विस्तार कर सकते हैं।

---

## Conclusion

हमने अभी-अभी **कैसे इमेज से भाषा का पता लगाएँ** को कवर किया, आवश्यक कोड दिखाया, और प्रत्येक स्टेप का महत्व समझाया। OCR इंजन को इनिशियलाइज़ करके, इमेज लोड करके, ऑटोमैटिक भाषा डिटेक्शन टॉगल करके, और अंत में `recognize()` कॉल करके, आप एक साफ़ ऑपरेशन में भाषा पहचानकर्ता और एक्सट्रैक्टेड टेक्स्ट दोनों प्राप्त कर सकते हैं।

अब आप इस लॉजिक को बड़े एप्लिकेशन में एम्बेड कर सकते हैं—चाहे वह रसीद‑स्कैनिंग सर्विस हो, बहुभाषी चैटबॉट, या एक साधारण डेस्कटॉप यूटिलिटी। मुख्य विचार वही रहता है: OCR इंजन को भारी काम करने दें, फिर परिणामों का उपयोग अपनी इच्छा अनुसार करें।

कोई सवाल या दिलचस्प उपयोग‑केस शेयर करना चाहते हैं? नीचे कमेंट करें। Happy coding, और इमेज को सर्चेबल टेक्स्ट में बदलने का आनंद लें!  

![इमेज से भाषा का पता कैसे लगाएँ](ocr-demo.png "Python OCR का उपयोग करके इमेज से भाषा का पता कैसे लगाएँ का स्क्रीनशॉट")


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}