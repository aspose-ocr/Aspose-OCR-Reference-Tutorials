---
category: general
date: 2026-06-28
description: Python OCR का उपयोग करके टेक्स्ट इमेज को पहचानना, टेक्स्ट PNG फ़ाइलें
  निकालना, और मजबूत त्रुटि संभाल के साथ पहचाने गए टेक्स्ट को प्रिंट करना सीखें।
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: hi
og_description: Python में टेक्स्ट इमेज को पहचानने, टेक्स्ट PNG निकालने और पहचाने
  गए टेक्स्ट को सुरक्षित रूप से प्रिंट करने के लिए चरण‑दर‑चरण ट्यूटोरियल।
og_title: Python OCR के साथ टेक्स्ट इमेज को पहचानें – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python OCR के साथ टेक्स्ट इमेज को पहचानें – पूर्ण गाइड
url: /hi/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR के साथ टेक्स्ट इमेज को पहचानें – पूर्ण गाइड

क्या आपने कभी सोचा है कि **टेक्स्ट इमेज को** एक Python स्क्रिप्ट में बिना भारी फ्रेमवर्क को जोड़े कैसे पहचानें? आप अकेले नहीं हैं। कई डेवलपर्स को एक तेज़ तरीका चाहिए *load image OCR* स्क्रीनशॉट, स्कैन किया हुआ रसीद, या साधारण PNG को लोड करने और टेक्स्ट वापस पाने का।  

इस ट्यूटोरियल में हम एक न्यूनतम OCR इंजन सेट करेंगे, एक कस्टम लॉगर जोड़ेंगे, **load image OCR**, **process image OCR** चलाएंगे, और अंत में **print recognized text** करेंगे। अंत तक आपके पास एक स्व-निहित स्क्रिप्ट होगी जो आवश्यकता पड़ने पर **extract text png** फ़ाइलों को भी निकाल सकती है।

## आप क्या सीखेंगे

- एक पूरी तरह कार्यशील Python स्निपेट जो OCR इंजन बनाता है, हर चरण को लॉग करता है, और विफलताओं को सहजता से संभालता है।  
- *why* प्रत्येक पंक्ति महत्वपूर्ण है, इसका स्पष्ट स्पष्टीकरण—ताकि आप कोड को Tesseract, EasyOCR, या किसी अन्य बैकएंड के साथ अनुकूलित कर सकें।  
- सामान्य समस्याओं (गायब फ़ॉन्ट, भ्रष्ट PNG) के लिए टिप्स और उन्हें डिबग करने के तरीके।  

### आवश्यकताएँ

- Python 3.8+ स्थापित हो  
- एक OCR लाइब्रेरी जो `OcrEngine` क्लास प्रदान करती है (उदाहरण में एक काल्पनिक लेकिन सामान्य API का उपयोग किया गया है; इसे `pytesseract`, `easyocr` आदि से बदलें)।  
- वह PNG इमेज जिसे आप विश्लेषण करना चाहते हैं, `input.png` के रूप में एक फ़ोल्डर में सहेजी गई हो।  

> **Pro tip:** यदि आप `pytesseract` का उपयोग कर रहे हैं, तो पहले सिस्टम Tesseract बाइनरी इंस्टॉल करें (`sudo apt install tesseract-ocr` Linux पर) और फिर `pip install pytesseract pillow`।

---

## ## Recognize Text Image: Setting Up the Logger

एक अच्छा लॉगर किसी भी OCR पाइपलाइन का अनसुना नायक होता है। यह आपको बताता है *कब* इंजन शुरू हुआ, *कौन* फ़ाइल खोली गई, और *क्यों* वह विफल हो सकता है।

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Why this matters:*  
लॉगर डायग्नोस्टिक आउटपुट को OCR कोर से अलग करता है, जिससे लॉग को फ़ाइल, मॉनिटरिंग सर्विस, या बाद में UI में रीडायरेक्ट करना आसान हो जाता है।  

---

## ## Load Image OCR: Feeding the Engine a PNG

इंजन को **process image OCR** करने से पहले उसे एक उचित इमेज ऑब्जेक्ट चाहिए। अधिकांश लाइब्रेरी Pillow `Image` इंस्टेंस को स्वीकार करती हैं।

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Key points:*  

- **load image ocr** – `Image.from_file` PNG डिकोडिंग विवरणों को एब्स्ट्रैक्ट करता है।  
- पाथ को कॉन्फ़िगरेबल रखें; हार्ड‑कोडिंग स्क्रिप्ट को नाज़ुक बना देती है।  
- लॉगर कॉल पुष्टि करता है कि इमेज सफलतापूर्वक पढ़ी गई, जो फ़ाइल के गायब या भ्रष्ट होने पर उपयोगी होता है।  

---

## ## Process Image OCR: Recognizing the Text

अब भारी काम शुरू होता है। इंजन बिटमैप को स्कैन करता है, अपने न्यूरल नेटवर्क या हेयूरिस्टिक्स लागू करता है, और एक Unicode स्ट्रिंग आउटपुट करता है।

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*Why we wrap it in `try/except`:*  
OCR कम‑रिज़ॉल्यूशन PNG, असमर्थित कलर स्पेस, या गायब भाषा डेटा पर फेल हो सकता है। `OcrException` को पकड़ने से आप **print recognized text** केवल तभी दिखा सकते हैं जब वह वास्तव में मौजूद हो, जिससे उपयोगकर्ता को अजीब स्टैक ट्रेस से बचाया जा सके।  

---

## ## Print Recognized Text & Extract Text PNG

यदि पहचान सफल रही, तो हम परिणाम दिखाते हैं और वैकल्पिक रूप से इसे एक `.txt` फ़ाइल में लिखते हैं जो मूल PNG नाम के समान हो।

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*What you get:*  

- **print recognized text** – टर्मिनल में तुरंत विज़ुअल फीडबैक।  
- एक साइड‑बाय‑साइड `.txt` फ़ाइल जो प्रभावी रूप से **extract text png** को डाउनस्ट्रीम प्रोसेसिंग (सर्च इंडेक्सिंग, डेटा एंट्री, आदि) के लिए उपलब्ध कराती है।  

---

## ## Common Edge Cases & How to Tackle Them

| स्थिति | लक्षण | समाधान |
|-----------|---------|-----|
| PNG केवल ग्रेस्केल है | OCR खाली स्ट्रिंग लौटाता है | इमेज को RGB में बदलें (`Image.convert("RGB")`) फिर इंजन को फीड करें। |
| भाषा समर्थित नहीं | `OcrException` कोड `LANG_NOT_FOUND` के साथ | भाषा पैक इंस्टॉल करें (उदाहरण: फ्रेंच के लिए `tesseract‑lang‑fra`) और `ocr_engine.language = "fra"` सेट करें। |
| बहुत बड़ी इमेज (> 5 MB) | धीमी पहचान या मेमोरी एरर | `set_image` से पहले `image.thumbnail((2000, 2000))` से डाउनस्केल करें। |
| अनपेक्षित अक्षर | गड़बड़ आउटपुट | सुनिश्चित करें कि फ़ाइल वास्तव में PNG है; कुछ फ़ाइलें PNG दिखती हैं लेकिन JPEG होती हैं। `Image.verify()` से वैधता जांचें। |

---

## ## Full Working Example (Copy‑Paste Ready)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**Expected console output (happy path):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

यदि कुछ गड़बड़ होता है, तो कस्टम लॉगर की बदौलत आपको स्पष्ट `[ERROR]` लाइन के साथ कारण दिखेगा।

---

## ## Next Steps & Related Topics

- **extract text png** बैचों से: स्क्रिप्ट को `for` लूप में लपेटें जो डायरेक्टरी ट्री को पार करता है।  
- **process image ocr** को प्री‑प्रोसेसिंग (डेस्क्यू, कंट्रास्ट बूस्ट) के साथ OpenCV का उपयोग करके इंजन को फीड करने से पहले लागू करें।  
- क्लाउड OCR सर्विस (Google Vision, Azure Read) पर स्विच करें `OcrEngine` इम्प्लीमेंटेशन बदलकर—आपका बाकी कोड वही रहेगा।  
- `reportlab` का उपयोग करके **print recognized text** को PDFs में लिखना सीखें, जिससे स्वचालित रिपोर्ट जनरेशन संभव हो।  

---

## Conclusion

हमने Python में **recognize text image** करने का एक कॉम्पैक्ट, प्रोडक्शन‑रेडी तरीका दिखाया, PNG लोड करने से लेकर **print recognized text** तक और परिणाम सहेजने तक। एक छोटा लॉगर जोड़कर, एक्सेप्शन हैंडल करके, और वैकल्पिक रूप से आउटपुट को स्थायी बनाकर, स्क्रिप्ट तेज़ प्रयोगों और बड़े पाइपलाइनों दोनों के लिए तैयार है।

अपने स्वयं के स्क्रीनशॉट्स के साथ इसे चलाएँ, इमेज प्री‑प्रोसेसिंग के साथ प्रयोग करें, और आप जल्द ही किसी भी PNG से टेक्स्ट निकाल पाएँगे। प्रश्न हैं? टिप्पणी करें—हैप्पी OCRing!  

![टेक्स्ट इमेज पहचान उदाहरण](placeholder.png)


## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन तरीकों का अन्वेषण कर सकें।

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}