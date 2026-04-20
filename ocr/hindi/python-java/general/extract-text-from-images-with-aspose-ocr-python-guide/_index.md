---
category: general
date: 2026-03-18
description: Aspose OCR का उपयोग करके Python में छवियों से टेक्स्ट निकालना और स्कैन
  की गई छवियों के टेक्स्ट को संपादन योग्य स्ट्रिंग्स में बदलना सीखें। चरण‑दर‑चरण कोड
  शामिल है।
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: hi
og_description: Aspose OCR का उपयोग करके Python में छवियों से टेक्स्ट निकालें। यह
  ट्यूटोरियल दिखाता है कि कैसे कुछ ही कोड लाइनों में स्कैन की गई छवियों के टेक्स्ट
  को परिवर्तित किया जा सकता है।
og_title: Aspose OCR के साथ छवियों से टेक्स्ट निकालें – पायथन गाइड
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Aspose OCR के साथ छवियों से टेक्स्ट निकालें – पायथन गाइड
url: /hi/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR के साथ इमेज से टेक्स्ट निकालें – Python गाइड

क्या आपको कभी **इमेज से टेक्स्ट निकालने** की ज़रूरत पड़ी है लेकिन आप नहीं जानते थे कि कहाँ से शुरू करें? आप अकेले नहीं हैं—डेवलपर्स लगातार स्कैन किए गए PDFs, शोरयुक्त स्क्रीनशॉट्स, या फ़ोटोग्राफ़ किए गए रसीदों को सर्चेबल, एडिटेबल स्ट्रिंग्स में बदलने की परेशानी का सामना करते हैं।  

अच्छी खबर? Aspose OCR for Python के साथ आप **स्कैन की गई इमेजेज़ का टेक्स्ट** बल्क में बदल सकते हैं, वह भी अपने IDE से बाहर निकले बिना। इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने‑योग्य उदाहरण के माध्यम से दिखाएंगे कि इसे कैसे करें, प्रत्येक चरण क्यों महत्वपूर्ण है, और किन बातों का ध्यान रखें।

## आप क्या सीखेंगे

- Python पर्यावरण में Aspose OCR लाइब्रेरी सेट अप करें।  
- इमेज फ़ाइलों (PNG, JPG, TIFF, आदि) की सूची तैयार करें।  
- एक ही मेथड कॉल से बैच OCR चलाएँ।  
- प्रत्येक फ़ाइल के लिए निकाले गए टेक्स्ट को एक्सेस और डिस्प्ले करें।  
- असमर्थित फ़ॉर्मैट्स और बड़े‑फ़ाइल मेमोरी उपयोग जैसी सामान्य समस्याओं को संभालें।  

अंत तक, आपके पास एक पुन: उपयोग योग्य स्क्रिप्ट होगी जो मांग पर **इमेज से टेक्स्ट निकाल सकती** है—डेटा एंट्री को ऑटोमेट करने, दस्तावेज़ों को इंडेक्स करने, या डाउनस्ट्रीम NLP पाइपलाइनों को फ़ीड करने के लिए परफेक्ट।

![इमेज से टेक्स्ट निकालने का उदाहरण](/images/ocr-extract-text.png "इमेज से टेक्स्ट निकालें")

*Image alt text: “Aspose OCR का उपयोग करके Python में इमेज से टेक्स्ट निकालें”*

## आवश्यकताएँ

- Python 3.8 या नया (कोड f‑strings का उपयोग करता है)।  
- एक वैध Aspose OCR for Python लाइसेंस या फ्री ट्रायल की।  
- वे इमेजेज़ जिन्हें आप प्रोसेस करना चाहते हैं, स्थानीय रूप से संग्रहीत (PNG, JPG, या TIFF का कोई भी मिश्रण)।  

यदि आपके पास पहले से एक वर्चुअल एनवायरनमेंट है, तो बढ़िया—यदि नहीं, तो इसे इस तरह बनाएँ:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

## चरण 1: Aspose OCR SDK स्थापित करें

Aspose अपना OCR इंजन PyPI के माध्यम से वितरित करता है, इसलिए एक ही `pip` कमांड काम कर देता है:

```bash
pip install aspose-ocr
```

> **Pro tip:** संस्करण को पिन करें (जैसे, `aspose-ocr==22.12`) ताकि बाद में अनपेक्षित ब्रेकिंग बदलावों से बचा जा सके।

## चरण 2: OCR इंजन क्लास इम्पोर्ट करें

कोर क्लास जिससे आप इंटरैक्ट करेंगे वह `OcrEngine` है। इसे अपने स्क्रिप्ट के शीर्ष पर इम्पोर्ट करें:

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *यह क्यों महत्वपूर्ण है:* केवल आवश्यक चीज़ें इम्पोर्ट करने से स्टार्ट‑अप टाइम कम रहता है, विशेषकर जब आप बाद में स्क्रिप्ट को बड़े एप्लिकेशन में एम्बेड करते हैं।

## चरण 3: प्रोसेस करने के लिए इमेज फ़ाइलें परिभाषित करें

एक Python सूची बनाएं जिसमें प्रत्येक इमेज का पूर्ण पाथ हो जिसे आप स्कैन करना चाहते हैं। `YOUR_DIRECTORY` को वास्तविक फ़ोल्डर पाथ से बदलें।

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **Edge case:** यदि आपके पास सैकड़ों फ़ाइलें हैं, तो इस सूची को प्रोग्रामेटिकली `glob.glob('*.png')` से जेनरेट करने पर विचार करें ताकि मैन्युअल एडिट से बचा जा सके।

## चरण 4: सभी इमेजेज़ पर एक साथ OCR चलाएँ

Aspose OCR एक सुविधाजनक `processMultiple` मेथड प्रदान करता है जो `OcrResult` ऑब्जेक्ट्स की सूची लौटाता है—प्रत्येक इनपुट फ़ाइल के लिए एक।

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *बैच प्रोसेसिंग क्यों?* प्रत्येक इमेज को अलग‑अलग भेजने से अतिरिक्त ओवरहेड (इंजन इनिशियलाइज़ करना, नेटिव लाइब्रेरीज़ लोड करना) बढ़ता है। बैच कॉल CPU चर्न को कम करता है और कुल कार्य को तेज़ बनाता है।

### त्रुटियों को सहजता से संभालना

यदि कोई इमेज पढ़ी नहीं जा सकती (खराब फ़ाइल, असमर्थित फ़ॉर्मैट), `processMultiple` एक एक्सेप्शन उठाएगा। स्क्रिप्ट को जीवित रखने के लिए कॉल को `try/except` ब्लॉक में रैप करें:

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## चरण 5: प्रत्येक फ़ाइल के लिए निकाला गया टेक्स्ट आउटपुट करें

परिणामों पर इटरेट करें, प्रत्येक `OcrResult` को उसकी मूल फ़ाइल नाम के साथ जोड़ें। `getText()` मेथड पहचाने गए स्ट्रिंग को लौटाता है।

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### अपेक्षित आउटपुट

पूरा स्क्रिप्ट तीन सरल स्क्रीनशॉट्स पर चलाने से कुछ इस तरह का आउटपुट मिल सकता है:

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

यदि किसी इमेज में कोई पहचानने योग्य कैरेक्टर नहीं है, तो आपको एक खाली स्ट्रिंग दिखेगी—कोई त्रुटि नहीं होगी, और आप तय कर सकते हैं कि उस फ़ाइल को मैन्युअल रिव्यू के लिए फ़्लैग करें या नहीं।

## बोनस: OCR सटीकता को फाइन‑ट्यून करना

Aspose OCR कई वैकल्पिक सेटिंग्स प्रदान करता है जिन्हें आप प्रयोग कर सकते हैं:

| सेटिंग | क्या करता है | कब उपयोग करें |
|---------|--------------|-------------|
| `ocr_engine.setLanguage('eng')` | इंग्लिश भाषा मॉडल को फोर्स करता है (फ़ॉल्स पॉज़िटिव्स को कम करता है)। | मुख्यतः अंग्रेज़ी दस्तावेज़। |
| `ocr_engine.setResolution(300)` | लो‑dpi स्कैन पर सटीकता बढ़ाता है। | 200 dpi से कम स्कैन। |
| `ocr_engine.setPageSegMode('single_block')` | पूरी इमेज को एक टेक्स्ट ब्लॉक के रूप में ट्रीट करता है। | सरल रसीदें या आईडी कार्ड। |

आप इन लाइनों को `ocr_engine` बनाने के तुरंत बाद जोड़ सकते हैं:

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## सामान्य समस्याएँ और उन्हें कैसे टालें

1. **Large TIFF stacks** – एक मल्टी‑पेज TIFF को एक साथ लोड करने पर गीगाबाइट्स RAM खपत हो सकती है। `processMultiple` को फ़ीड करने से पहले फ़ाइल को सिंगल‑पेज इमेजेज़ में विभाजित करें।  
2. **Non‑Latin scripts** – यदि आपको ऐसी इमेजेज़ से **टेक्स्ट निकालना** है जिनमें सिरिलिक, अरबी, या चीनी कैरेक्टर्स हैं, तो भाषा कोड को तदनुसार बदलें (`'rus'`, `'ara'`, `'chi_sim'`)।  
3. **File path spaces** – स्पेस वाले Windows पाथ्स `FileNotFoundError` का कारण बन सकते हैं। प्रत्येक पाथ को रॉ स्ट्रिंग (`r"C:\My Folder\image.png"`) में रैप करें या `os.path.abspath` का उपयोग करें।  

इन समस्याओं को पहले ही हल करने से बाद में अस्पष्ट रनटाइम एरर्स से बचा जा सकता है।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा स्क्रिप्ट है जिसे आप `batch_ocr.py` नाम की फ़ाइल में कॉपी‑पेस्ट कर सकते हैं। इसमें ऊपर चर्चा किए गए सभी बेस्ट‑प्रैक्टिस ट्यूनिंग शामिल हैं।

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

सेव करें, अपना वर्चुअल एनवायरनमेंट एक्टिवेट करें, और चलाएँ:

```bash
python batch_ocr.py
```

आपको कंसोल में निकाले गए स्ट्रिंग्स प्रिंट होते दिखेंगे, आगे की प्रोसेसिंग के लिए तैयार (जैसे, डेटाबेस में सेव करना या नेचुरल‑लैंग्वेज मॉडल को फ़ीड करना)।

## निष्कर्ष

इस गाइड में हमने दिखाया कि Aspose OCR for Python का उपयोग करके **इमेज से टेक्स्ट निकालना** कैसे किया जाता है, जिसमें इंस्टॉलेशन से लेकर बैच प्रोसेसिंग और एरर हैंडलिंग तक सब कुछ शामिल है। स्क्रिप्ट कॉम्पैक्ट, पूरी तरह कार्यशील, और एक्स्टेंड करने में आसान है—चाहे आपको **स्कैन की गई इमेजेज़ का टेक्स्ट** CSV फ़ाइलों में बदलना हो, सर्च इंडेक्स को फ़ीड करना हो, या बस डेटा एंट्री को ऑटोमेट करना हो।  

अगले कदम के लिए तैयार हैं? इस OCR पाइपलाइन को PDF मर्जर के साथ जोड़ने पर विचार करें ताकि सर्चेबल PDFs बन सकें, या इसे क्लाउड स्टोरेज ट्रिगर में हुक करें ताकि हर अपलोडेड स्कैन तुरंत प्रोसेस हो। संभावनाएँ असीमित हैं, और अब आपके पास निर्माण के लिए एक मजबूत आधार है।  

कोई प्रश्न या सुधार के विचार हैं? नीचे कमेंट करें, और हैप्पी कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}