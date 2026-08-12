---
category: general
date: 2026-08-12
description: Python में OCR का उपयोग करके छवि से टेक्स्ट को पहचानना, टेक्स्ट निकालना,
  छवि को टेक्स्ट में बदलना, और AI पोस्ट‑प्रोसेसिंग के साथ OCR टेक्स्ट को साफ़ करना।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- clean up OCR text
language: hi
lastmod: 2026-08-12
og_description: Python में OCR का उपयोग करके चित्रों को संपादन योग्य टेक्स्ट में बदलना
  सीखें। छवि से टेक्स्ट पहचानना, टेक्स्ट निकालना, छवि को टेक्स्ट में परिवर्तित करना,
  और AI के साथ OCR टेक्स्ट को साफ़ करना जानें।
og_image_alt: Screenshot of Python code converting an image to clean text using OCR
  and AI post‑processing
og_title: Python में OCR का उपयोग कैसे करें – पूर्ण प्रोग्रामिंग गाइड
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  headline: How to use OCR in Python – step‑by‑step guide
  type: TechArticle
- description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  name: How to use OCR in Python – step‑by‑step guide
  steps:
  - name: Loads an image file (PNG, JPEG, or TIFF).
    text: Loads an image file (PNG, JPEG, or TIFF).
  - name: Recognizes text from the image using an OCR engine.
    text: Recognizes text from the image using an OCR engine.
  - name: Improves the raw output with an AI‑driven post‑processor.
    text: Improves the raw output with an AI‑driven post‑processor.
  - name: Prints the cleaned‑up text to the console.
    text: Prints the cleaned‑up text to the console.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- AI post‑processing
title: Python में OCR का उपयोग कैसे करें – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/python/general/how-to-use-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में OCR कैसे उपयोग करें – चरण‑दर‑चरण गाइड

यदि आपको स्कैन किए गए दस्तावेज़ों या स्क्रीनशॉट को संपादन योग्य टेक्स्ट में बदलने के लिए **how to use OCR** की आवश्यकता है, तो यह ट्यूटोरियल Python में एक पूर्ण समाधान दिखाता है। आप छवि से टेक्स्ट पहचानना, छवि से टेक्स्ट निकालना, छवि को टेक्स्ट में बदलना, और एक हल्के AI पोस्ट‑प्रोसेसर के साथ OCR टेक्स्ट को साफ़ करना सीखेंगे।

यह गाइड आवश्यक लाइब्रेरीज़ को इंस्टॉल करने से लेकर कम‑गुणवत्ता वाली छवियों को संभालने तक सब कुछ कवर करता है, ताकि आप बिना यह अनुमान लगाए कि कौन सा चरण गायब है, OCR को किसी भी ऑटोमेशन पाइपलाइन में एकीकृत कर सकें।

## आप क्या बनाएँगे

1. एक इमेज फ़ाइल (PNG, JPEG, या TIFF) लोड करता है।  
2. OCR इंजन का उपयोग करके छवि से टेक्स्ट पहचानता है।  
3. कच्चे आउटपुट को एक AI‑ड्रिवेन पोस्ट‑प्रोसेसर से सुधारता है।  
4. साफ़ किया गया टेक्स्ट कंसोल में प्रिंट करता है।

कोई बाहरी सेवा आवश्यक नहीं है—सब कुछ स्थानीय रूप से चलता है, जिससे समाधान ऑफ़लाइन वातावरण या प्राइवेसी‑संवेदनशील प्रोजेक्ट्स के लिए उपयुक्त बनता है।

## पूर्वापेक्षाएँ

- Python 3.9 या उससे नया।  
- `pytesseract` और `Pillow` लाइब्रेरीज़ (`pip install pytesseract pillow`)।  
- Tesseract‑OCR बाइनरी इंस्टॉल किया हुआ और आपके सिस्टम के `PATH` में उपलब्ध।  
- Python में फ़ंक्शन्स की बुनियादी समझ।  

यदि आपके पास ये सभी चीज़ें पहले से हैं, तो आप सीधे पहले कोड ब्लॉक पर जा सकते हैं।

## Python के साथ OCR कैसे उपयोग करें

**how to use OCR** का मूल भाग OCR इंजन को इनिशियलाइज़ करना और उसे एक इमेज फीड करना है। इस ट्यूटोरियल में हम `pytesseract` का उपयोग करते हैं, जो ओपन‑सोर्स Tesseract इंजन के चारों ओर एक हल्का रैपर है।

```python
import pytesseract
from PIL import Image

def load_image(path: str) -> Image.Image:
    """
    Open an image file and return a Pillow Image object.
    Pillow handles many formats (PNG, JPEG, TIFF) and ensures
    the image is in a mode that Tesseract can read.
    """
    return Image.open(path)
```

> **Why this step matters** – Tesseract एक साफ़, सही ओरिएंटेड इमेज की अपेक्षा करता है। Pillow का उपयोग करने से OCR चलने से पहले इमेज डेटा नॉर्मलाइज़ हो जाता है, जिससे बाद के **recognize text from image** ऑपरेशन की सटीकता बढ़ती है।

## Recognize text from image

अब हम `pytesseract.image_to_string` को कॉल करके कच्ची स्ट्रिंग निकालते हैं। यह क्लासिक “recognize text from image” कॉल है।

```python
def ocr_recognize(image: Image.Image) -> str:
    """
    Run Tesseract OCR on the supplied image and return the raw text.
    """
    raw_text = pytesseract.image_to_string(image, lang='eng')
    return raw_text
```

> **Why we separate the function** – OCR चरण को अलग करने से आप बाद में इंजन बदल सकते हैं (जैसे EasyOCR पर स्विच) बिना पाइपलाइन के बाकी हिस्सों को छुए। यह यूनिट टेस्टिंग को भी आसान बनाता है।

## Extract text from image and improve quality

कच्चा OCR आउटपुट अक्सर लाइन ब्रेक, अनचाहे कैरेक्टर या गलत पहचाने गए शब्द रखता है। एक AI पोस्ट‑प्रोसेसर इन आर्टिफैक्ट्स को स्वचालित रूप से साफ़ कर सकता है। नीचे `transformers` लाइब्रेरी का उपयोग करके एक छोटा लोकल लैंग्वेज मॉडल चलाने का न्यूनतम उदाहरण दिया गया है। यदि आप चाहें तो इसे किसी भी प्रॉप्राइटरी सर्विस से बदल सकते हैं।

```python
from transformers import pipeline

# Initialize a zero‑shot text‑generation pipeline once (expensive operation)
_ai_postprocessor = pipeline("text2text-generation", model="google/flan-t5-small")

def clean_ocr_text(raw: str) -> str:
    """
    Send the raw OCR string to a lightweight AI model that rewrites
    the text, removing obvious errors and normalizing whitespace.
    """
    # The prompt guides the model to act as a post‑processor
    prompt = f"Clean up the following OCR output, fixing spelling mistakes and removing extra line breaks:\n\n{raw}"
    result = _ai_postprocessor(prompt, max_length=512, do_sample=False)
    # The pipeline returns a list of dicts; we take the generated text
    cleaned = result[0]["generated_text"]
    return cleaned.strip()
```

> **Why an AI post‑processor helps** – पारंपरिक OCR इंजन कैरेक्टर रिकग्निशन में माहिर होते हैं लेकिन लेआउट और शोर से जूझते हैं। एक लैंग्वेज मॉडल संदर्भ समझता है, इसलिए वह “Th1s 1s 4 test.” को “This is a test.” में बदल सकता है। यह चरण सीधे **clean up OCR text** की आवश्यकता को पूरा करता है।

## Convert image to text – full script

सब कुछ मिलाकर एक छोटा स्क्रिप्ट बनता है जो **convert image to text** को एंड‑टू‑एंड करता है।

```python
import sys
from pathlib import Path

def main(image_path: str):
    """
    Complete pipeline:
    1. Load image.
    2. Recognize text from image.
    3. Clean up OCR text.
    4. Print the final result.
    """
    # 1️⃣ Load the image file
    img = load_image(image_path)

    # 2️⃣ Recognize text from image (raw OCR)
    raw_text = ocr_recognize(img)
    print("=== Raw OCR output ===")
    print(raw_text)
    print("\n---\n")

    # 3️⃣ Clean up OCR text with AI post‑processor
    cleaned_text = clean_ocr_text(raw_text)
    print("=== Cleaned‑up text ===")
    print(cleaned_text)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python ocr_pipeline.py <path-to-image>")
        sys.exit(1)

    image_file = Path(sys.argv[1])
    if not image_file.is_file():
        print(f"Error: file '{image_file}' does not exist.")
        sys.exit(1)

    main(str(image_file))
```

### अपेक्षित आउटपुट

`sample.png` जैसी सैंपल इमेज के साथ स्क्रिप्ट चलाने पर यह आउटपुट मिल सकता है:

```
=== Raw OCR output ===
Th1s 1s 4 sampl3
text from an im4ge.

--- 

=== Cleaned‑up text ===
This is a sample text from an image.
```

ध्यान दें कि AI पोस्ट‑प्रोसेसर ने गलत पढ़े गए कैरेक्टर को ठीक किया और अनावश्यक लाइन ब्रेक हटा दिया। यह पूर्ण **extract text from image** वर्कफ़्लो को दर्शाता है और OCR टेक्स्ट को साफ़ करने के लाभ को दिखाता है।

## सामान्य किनारी मामलों को संभालना

| स्थिति                                 | सुझाया गया बदलाव                                                               |
|----------------------------------------|---------------------------------------------------------------------------------|
| कम‑कॉन्ट्रास्ट इमेज                     | OCR से पहले `ImageEnhance` के साथ ग्रेस्केल में बदलें और कॉन्ट्रास्ट बढ़ाएँ।   |
| बहु‑भाषा दस्तावेज़                     | `lang` को कॉमा‑सेपरेटेड लिस्ट पास करें (उदा., `lang='eng+fra'`)।            |
| बहुत बड़ी इमेज ( > 2000 px )           | Tesseract को तेज़ करने के लिए `img.thumbnail((2000, 2000))` से डाउनस्केल करें। |
| Tesseract बाइनरी गायब है               | `pytesseract.pytesseract.tesseract_cmd` को एक्सीक्यूटेबल की ओर इंगित करें।   |
| AI पोस्ट‑प्रोसेसर बहुत धीमा है          | छोटा मॉडल (`t5-small`) उपयोग करें या GPU पर पोस्ट‑प्रोसेसर चलाएँ।           |

> **Pro tip:** मॉड्यूल इम्पोर्ट टाइम पर AI मॉडल ऑब्जेक्ट (`_ai_postprocessor`) को कैश करें, जैसा कि दिखाया गया है, ताकि हर कॉल पर री‑लोडिंग से बचा जा सके। यह कई इमेज प्रोसेस करने पर लेटेंसी को काफी घटा देता है।

## वैकल्पिक दृष्टिकोण

- **EasyOCR**: एक प्यूरे‑Python OCR लाइब्रेरी जो 80 से अधिक भाषाओं को बिना बाहरी बाइनरी के सपोर्ट करती है। यदि आप केवल pip‑सॉल्यूशन चाहते हैं तो `ocr_recognize` को `EasyOCR.Reader` से बदलें।  
- **Cloud OCR APIs**: Google Cloud Vision, Azure Computer Vision, या Amazon Textract जटिल लेआउट के लिए अधिक सटीकता प्रदान करते हैं, लेकिन नेटवर्क एक्सेस और बिलिंग की आवश्यकता होती है।  
- **Custom post‑processing**: निर्धारक क्लीन‑अप के लिए रेगुलर एक्सप्रेशन्स (`re.sub`) सामान्य पैटर्न (जैसे हाइफ़न‑वाले लाइन ब्रेक हटाना) को AI मॉडल के बिना ठीक कर सकते हैं।

## सारांश

अब आप **how to use OCR** को Python में इमेज से टेक्स्ट पहचानने, इमेज से टेक्स्ट निकालने, इमेज को टेक्स्ट में बदलने, और AI पोस्ट‑प्रोसेसर के साथ OCR टेक्स्ट को साफ़ करने के लिए जानते हैं। पूरा स्क्रिप्ट एक प्रोडक्शन‑रेडी पाइपलाइन दर्शाता है जिसे आप अतिरिक्त प्री‑प्रोसेसिंग (नॉइज़ रिडक्शन, डेस्क्यूइंग) या डाउनस्ट्रीम एक्शन (डेटाबेस में सेव करना, सर्च इंडेक्स में फीड करना) के साथ विस्तारित कर सकते हैं।

### अगले कदम

- विभिन्न AI मॉडलों (जैसे `gpt‑2`, `flan‑ul2`) के साथ प्रयोग करें ताकि देखें कि आपके डोमेन के लिए कौन सा सबसे अच्छा क्लीन‑अप देता है।  
- Flask या FastAPI का उपयोग करके पाइपलाइन को वेब सर्विस में इंटीग्रेट करें, जिससे स्क्रिप्ट एक ऑन‑डिमांड OCR एंडपॉइंट बन जाए।  
- बैच प्रोसेसिंग का अन्वेषण करें: इमेज की डायरेक्टरी पर लूप चलाएँ और प्रत्येक साफ़ आउटपुट को संबंधित `.txt` फ़ाइल में लिखें।

कोड को अपने विशिष्ट वर्कफ़्लो के अनुसार अनुकूलित करने में संकोच न करें, और साफ़, सर्चेबल टेक्स्ट को आपके एप्लिकेशन के अगले चरण को सशक्त बनने दें। Happy coding!

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}