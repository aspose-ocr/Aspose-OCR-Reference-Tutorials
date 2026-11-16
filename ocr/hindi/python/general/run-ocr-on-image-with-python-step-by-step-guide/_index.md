---
category: general
date: 2026-08-12
description: Python और Aspose AI का उपयोग करके छवि पर OCR चलाएँ, छवि से पाठ निकालें
  और स्पेल‑चेकिंग पोस्ट‑प्रोसेसर के साथ OCR की सटीकता में सुधार करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: hi
lastmod: 2026-08-12
og_description: Python में छवि पर OCR चलाएँ और तुरंत छवि से टेक्स्ट निकालें, साथ ही
  Aspose AI पोस्ट‑प्रोसेसिंग का उपयोग करके OCR की सटीकता में सुधार करें।
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: Python के साथ छवि पर OCR चलाएँ – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Python के साथ इमेज पर OCR चलाएँ – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज पर OCR चलाएँ Python के साथ – चरण‑दर‑चरण गाइड

यदि आपको Python में **run OCR on image** फ़ाइलों को चलाने की आवश्यकता है, तो यह गाइड आपको पूरे वर्कफ़्लो के माध्यम से ले जाएगा। आप सीखेंगे कि कैसे **extract text from image** किया जाए, **OCR text correction** लागू किया जाए, और केवल कुछ पंक्तियों के कोड से **improve OCR accuracy** किया जाए।

स्कैन किए गए दस्तावेज़ों, रसीदों या स्क्रीनशॉट्स को प्रोसेस करने से अक्सर शोरयुक्त टेक्स्ट प्राप्त होता है। एक स्पेल‑चेकिंग पोस्ट‑प्रोसेसर जोड़कर आप कच्चे OCR आउटपुट को साफ़, खोजने योग्य सामग्री में बदल सकते हैं बिना किसी अलग टूल के। यह ट्यूटोरियल आपको सब कुछ कवर करता है—इमेज लोड करने से लेकर सुधारे हुए परिणाम को प्रदर्शित करने तक।

## आवश्यकताएँ

* Python 3.9 या उससे नया स्थापित हो।
* Aspose.OCR और Aspose.AI Python पैकेजों तक पहुँच (या उनके समकक्ष ओपन‑सोर्स रैपर्स)।
* एक सैंपल इमेज (जैसे `sample.png`) को ज्ञात डायरेक्टरी में रखें।
* Python फ़ंक्शन्स और ऑब्जेक्ट‑ओरिएंटेड कोड की बुनियादी परिचितता।

आप आवश्यक लाइब्रेरीज़ को pip के साथ इंस्टॉल कर सकते हैं:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro tip:** निर्भरताओं को अलग रखने के लिए एक वर्चुअल एनवायरनमेंट (`python -m venv .venv`) उपयोग करें।

## चरण 1: इमेज पर OCR चलाएँ – इंजन इंस्टेंस बनाएँ

पहला कदम `OcrEngine` ऑब्जेक्ट बनाना है। यह ऑब्जेक्ट OCR इंजन कॉन्फ़िगरेशन को समाहित करता है और इमेज हैंडलिंग तथा रिकग्निशन के लिए मेथड्स प्रदान करता है।

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

इंजन को एक बार बनाकर कई इमेज पर पुनः उपयोग करने से स्टार्टअप ओवरहेड कम होता है और सत्र के दौरान सेटिंग्स सुसंगत रहती हैं।

## चरण 2: OCR के लिए इमेज लोड करें

रिकग्निशन होने से पहले, इंजन को यह जानना आवश्यक है कि कौन सी तस्वीर का विश्लेषण करना है। `load_image` मेथड फ़ाइल पाथ या बाइनरी स्ट्रीम स्वीकार करता है।

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **Why this matters:** इमेज को सही तरीके से लोड करना सटीक OCR का आधार है। उच्च‑रिज़ॉल्यूशन इमेज (300 dpi या अधिक) प्रदान करने से आमतौर पर **improve OCR accuracy** होता है क्योंकि इंजन अक्षरों को स्पष्ट रूप से पहचान सकता है।

## चरण 3: इमेज से टेक्स्ट निकालें – बेसिक रिकग्निशन करें

इमेज लोड होने पर, आप `recognize()` कॉल करके एक रिज़ल्ट ऑब्जेक्ट प्राप्त कर सकते हैं। इस रिज़ल्ट में कच्चा टेक्स्ट, कॉन्फिडेंस स्कोर, और वैकल्पिक रूप से प्रत्येक शब्द के बाउंडिंग बॉक्स शामिल होते हैं।

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

इस चरण पर आपने सफलतापूर्वक **run OCR on image** किया है और कच्चे अक्षर निकाले हैं। हालांकि, टेक्स्ट में गलत वर्तनी हो सकती है, विशेषकर कम‑गुणवत्ता वाले स्कैन में।

## चरण 4: OCR टेक्स्ट सुधार – पोस्ट‑प्रोसेसिंग स्पेल‑चेकर जोड़ें

Aspose AI एक लचीला पोस्ट‑प्रोसेसिंग पाइपलाइन प्रदान करता है। एक कस्टम स्पेल‑चेकर को प्लग इन करके आप सामान्य OCR त्रुटियों को सुधार सकते हैं (जैसे, “l” बनाम “1”, “O” बनाम “0”)।

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**How the spell‑checker works:** `MySpellChecker` को एक `process(text: str) -> str` मेथड इम्प्लीमेंट करना चाहिए। इसके अंदर, आप `pyspellchecker` या `symspellpy` जैसी लाइब्रेरीज़ का उपयोग करके असंभावित शब्द क्रमों को शब्दकोश‑सत्यापित विकल्पों से बदल सकते हैं।

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## चरण 5: मूल और सुधारा गया OCR टेक्स्ट दिखाएँ

अंत में, कच्चे और सुधारे हुए आउटपुट की तुलना करें। यह आपको यह सत्यापित करने में मदद करता है कि **OCR text correction** वास्तव में आपके उपयोग केस के लिए **improved OCR accuracy** करता है।

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### अपेक्षित आउटपुट

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

सुधारी गई लाइन दर्शाती है कि स्पेल‑चेकर ने सामान्य OCR गलत‑पहचान को बदल दिया (`Th1s` → `This`, `s4mpl3` → `simple`, `rec3pt` → `receipt`, `som3` → `some`, `err0rs` → `errors`)।

## चरण 6: OCR सटीकता बढ़ाएँ – बेस्ट‑प्रैक्टिस चेकलिस्ट

पोस्ट‑प्रोसेसिंग के साथ भी, आप OCR इंजन की बेसलाइन क्वालिटी बढ़ा सकते हैं:

| Checklist item | Why it helps |
|----------------|--------------|
| **उच्च‑रिज़ॉल्यूशन इमेज (≥300 dpi) उपयोग करें** | अधिक पिक्सेल डेटा अक्षर की अस्पष्टता को कम करता है। |
| **रंगीन इमेज को ग्रेस्केल में बदलें** | इंजन को भ्रमित करने वाले क्रोमा शोर को हटाता है। |
| **इमेज डेस्क्यूइंग लागू करें** | झुके हुए टेक्स्ट को सीधा करता है, लाइन‑ब्रेक त्रुटियों को रोकता है। |
| **भाषा/लोकेल को स्पष्ट रूप से सेट करें** | रिकग्नाइज़र को सही कैरेक्टर सेट की ओर मार्गदर्शन करता है। |
| **भाषा मॉडल सक्षम करें** (यदि लाइब्रेरी समर्थन करती है) | संदर्भ‑सचेत भविष्यवाणियाँ प्रदान करता है, आगे **improving OCR accuracy** करता है। |

आप इन प्री‑प्रोसेसिंग स्टेप्स को Pillow या OpenCV के साथ इमेज को `ocr_engine` को देने से पहले लागू कर सकते हैं।

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## पूर्ण चलाने योग्य स्क्रिप्ट

सब कुछ मिलाकर, निम्नलिखित स्क्रिप्ट `run_ocr.py` नामक फ़ाइल में कॉपी‑पेस्ट करने और चलाने के लिए तैयार है।

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

स्क्रिप्ट चलाने से मूल और सुधारा गया टेक्स्ट प्रिंट होता है, यह पुष्टि करता है कि आपने सफलतापूर्वक **run OCR on image**, **extract text from image**, और **OCR text correction** के माध्यम से **improved OCR accuracy** किया है।

## निष्कर्ष

अब आप जानते हैं कि Python में **run OCR on image** फ़ाइलों को कैसे चलाएँ, कच्चा टेक्स्ट निकालें, और साफ़ परिणाम प्राप्त करने के लिए पोस्ट‑प्रोसेसिंग स्पेल‑चेकर लागू करें। **improve OCR accuracy** के लिए चेकलिस्ट का पालन करके आप इस वर्कफ़्लो को रसीदों, इनवॉइस, आईडी कार्ड या किसी भी स्कैन किए दस्तावेज़ में अनुकूलित कर सकते हैं।

### आगे क्या?

* बहुभाषी OCR के लिए **language‑specific dictionaries** का अन्वेषण करें।
* पाइपलाइन को डेटाबेस या सर्च इंडेक्स (जैसे, Elasticsearch) के साथ एकीकृत करें ताकि निकाला गया टेक्स्ट खोज योग्य हो।
* सरल स्पेल‑चेकर को न्यूरल लैंग्वेज मॉडल (जैसे, GPT‑based correction) से बदलें ताकि और अधिक सटीकता मिले।

विभिन्न इमेज प्री‑प्रोसेसिंग तकनीकों, विभिन्न पोस्ट‑प्रोसेसरों, या वैकल्पिक OCR इंजनों के साथ प्रयोग करने में संकोच न करें। मूल पैटर्न—**run OCR on image → extract text from image → OCR text correction → improve OCR accuracy**—वही रहता है, जो आपको किसी भी दस्तावेज़‑डिजिटलीकरण प्रोजेक्ट के लिए एक मजबूत आधार प्रदान करता है।

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में माहिर बनने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर करने में मदद करती हैं।

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}