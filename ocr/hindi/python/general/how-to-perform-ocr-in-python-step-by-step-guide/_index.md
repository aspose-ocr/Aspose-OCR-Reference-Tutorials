---
category: general
date: 2026-01-12
description: OCR कैसे करें और छवि को जल्दी से टेक्स्ट में बदलें। विशेष अक्षरों को
  पहचानना, छवि से टेक्स्ट निकालना, और OCR के लिए छवि लोड करना सीखें, एक पूर्ण पायथन
  उदाहरण के साथ।
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: hi
og_description: Python में OCR कैसे करें, छवि को टेक्स्ट में बदलें, और विशेष अक्षरों
  को पहचानें। छवियों से टेक्स्ट निकालने के लिए इस व्यावहारिक गाइड का पालन करें।
og_title: Python में OCR कैसे करें – पूर्ण ट्यूटोरियल
tags:
- OCR
- Python
- Image Processing
title: Python में OCR कैसे करें – चरण‑दर‑चरण गाइड
url: /hi/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में OCR कैसे करें – चरण‑दर‑चरण गाइड

क्या आपको कभी **OCR** करना पड़ा है किसी स्क्रीनशॉट पर जिसमें लैटिन और सिरिलिक दोनों अक्षर हों? आप अकेले नहीं हैं। कई प्रोजेक्ट्स में—चाहे रसीदों को डिजिटल बनाना हो, बहुभाषी दस्तावेज़ों को इंडेक्स करना हो, या खोज योग्य आर्काइव बनाना हो—**how to perform OCR** जल्दी ही सबसे प्रमुख सवाल बन जाता है।  

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे कि कैसे **image to text** बदलें, **विशेष अक्षरों को पहचानें**, और **image से टेक्स्ट निकालें** एक सरल Python लाइब्रेरी का उपयोग करके। अंत तक आपके पास एक तैयार‑स्क्रिप्ट होगी जो OCR के लिए इमेज लोड करती है, बहुभाषी कंटेंट को संभालती है, और परिणाम प्रिंट करती है।

## आपको क्या चाहिए

शुरू करने से पहले सुनिश्चित करें कि आपके पास ये प्री‑रिक्विज़िट्स हों:

- आपके मशीन पर Python 3.8+ स्थापित हो।  
- `ocr` पैकेज (या कोई संगत OCR लाइब्रेरी) `pip install ocr` के माध्यम से स्थापित हो।  
- एक इमेज फ़ाइल (`multilingual.png`) जिसमें लैटिन और सिरिलिक दोनों ग्लीफ़ हों।  
- एक बेसिक टेक्स्ट एडिटर या IDE—VS Code, PyCharm, या यहाँ तक कि साधा Notepad भी चलेगा।  

यदि आपके पास `ocr` पैकेज नहीं है, तो आप इसे `pytesseract` से बदल सकते हैं कुछ छोटे बदलावों के साथ; मूल अवधारणाएँ समान रहती हैं।

## चरण 1: OCR लाइब्रेरी इंस्टॉल और इम्पोर्ट करें

सबसे पहले, OCR इंजन को तैयार करते हैं। हम लाइब्रेरी को इम्पोर्ट करेंगे, एक इंजन इंस्टेंस बनाएँगे, और बहुभाषी सपोर्ट के लिए उसे कॉन्फ़िगर करेंगे।

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**यह क्यों महत्वपूर्ण है:**  
इंजन बनाना बुनियादी आधार है—इसके बिना आप बाद में **load image for OCR** नहीं कर सकते। भाषा पैक्स को एनेबल करने से इंजन “Ŀ”, “Ҕ”, और “Ǣ” जैसे अक्षरों को सही ढंग से पहचान सकता है। यदि आप इस चरण को छोड़ते हैं, तो गैर‑लैटिन स्क्रिप्ट्स के लिए आउटपुट गड़बड़ हो जाएगा।

## चरण 2: बहुभाषी टेक्स्ट वाली इमेज लोड करें

अब हम इंजन को उस फ़ाइल की ओर इशारा करते हैं जिसे हम प्रोसेस करना चाहते हैं। पाथ एब्सोल्यूट या रिलेटिव हो सकता है; बस यह सुनिश्चित करें कि वह पढ़ी जा सकने वाली इमेज की ओर इशारा करे।

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![OCR उदाहरण कैसे करें](/images/ocr-example.png "बहुभाषी इमेज पर OCR कैसे करें")

**यह क्यों महत्वपूर्ण है:**  
`load_image` कॉल पिक्सेल डेटा को मेमोरी में पढ़ता है, जिससे OCR एल्गोरिदम के लिए तैयारी होती है। यदि इमेज बड़ी है, तो इंजन स्वचालित रूप से उसे डाउनस्केल कर सकता है; आप बाद में `engine.set_max_resolution(3000)` के साथ हाई‑रेज़ोल्यूशन स्कैन के लिए इसे फाइन‑ट्यून कर सकते हैं।

## चरण 3: रिकग्निशन प्रोसेस चलाएँ

इंजन तैयार और इमेज लोड हो जाने के बाद, अब हम अंततः टेक्स्ट कंटेंट निकाल सकते हैं।

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**यह क्यों महत्वपूर्ण है:**  
`recognize()` बैकएंड में भारी‑वजन वाला न्यूरल नेटवर्क चलाता है। यह एक ऑब्जेक्ट रिटर्न करता है जिसमें कच्चा टेक्स्ट, कॉन्फिडेंस स्कोर, और यदि आप विज़ुअल डिबगिंग के लिए चाहते हैं तो बाउंडिंग बॉक्स भी होते हैं।

## चरण 4: पहचाने गए टेक्स्ट को आउटपुट करें

आइए देखें कि इंजन ने क्या पाया। हम टेक्स्ट को कंसोल पर प्रिंट करेंगे, लेकिन आप इसे फ़ाइल या डेटाबेस में भी लिख सकते हैं।

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### अपेक्षित आउटपुट

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

यदि आपको कुछ ऐसा ही दिखे, तो बधाई—आपने सफलतापूर्वक **convert image to text** और **recognize special characters** कर लिया है।

## सामान्य समस्याओं का समाधान

भले ही स्क्रिप्ट सीधी हो, आप कुछ अड़चनों का सामना कर सकते हैं। नीचे मेरे अनुभव से कुछ व्यावहारिक टिप्स दी गई हैं।

### 1. भाषा पैक्स नहीं मिले

यदि आपको सिरिलिक अक्षरों की जगह प्रश्नवाचक चिह्न (`?`) दिख रहे हैं, तो दोबारा जांचें कि भाषा पैक्स इंस्टॉल हैं या नहीं। कई OCR इंजनों के लिए आपको संबंधित `.traineddata` फ़ाइलें डाउनलोड करके इंजन के `tessdata` फ़ोल्डर में रखना पड़ता है।

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. कम इमेज क्वालिटी

धुंधली या कम कॉन्ट्रास्ट वाली इमेजेज़ कम कॉन्फिडेंस स्कोर देती हैं। OpenCV के साथ इमेज को प्री‑प्रोसेस करें:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. बड़ी फ़ाइलें और मेमोरी उपयोग

10 MB की फोटो प्रोसेस करने से मेमोरी स्पाइक हो सकता है। `engine.set_max_image_size(2000)` से रिज़ॉल्यूशन को सीमित करें, या इमेज को टाइल्स में बाँटकर प्रत्येक टाइल को अलग‑अलग OCR करें।

### 4. बाउंडिंग बॉक्स कैप्चर करना

यदि आपको प्रत्येक शब्द के स्थान को हाइलाइट करना है (UI ओवरले के लिए उपयोगी), तो `result.boxes` तक पहुँचें:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## पूर्ण स्क्रिप्ट – एक‑क्लिक एक्सीक्यूशन

सब कुछ मिलाकर, यहाँ एक सिंगल फ़ाइल है जिसे आप `python ocr_demo.py` के रूप में चला सकते हैं। इसमें एरर हैंडलिंग, वैकल्पिक प्री‑प्रोसेसिंग, और स्पष्टता के लिए कमेंट्स शामिल हैं।

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

इसे चलाएँ:

```bash
python ocr_demo.py path/to/multilingual.png
```

आपको पहले दिखाए गए समान आउटपुट मिलना चाहिए, जिससे पुष्टि होगी कि आपने सफलतापूर्वक **extract text from image** कर लिया है।

## निष्कर्ष

हमने **how to perform OCR** को Python में शुरू से अंत तक कवर किया: लाइब्रेरी इंस्टॉल करना, इमेज लोड करना, बहुभाषी कंटेंट को पहचानना, और सबसे आम एज केसों को संभालना। इस गाइड को फॉलो करके आप अब **convert image to text**, **recognize special characters**, और **extract text from image** अपने प्रोजेक्ट्स में कर सकते हैं—अब मैन्युअल ट्रांसक्रिप्शन की जरूरत नहीं।

अब आगे क्या? इन चीज़ों को आज़माएँ:

- अधिक भाषा पैक्स जोड़ें (जैसे `spa` स्पेनिश के लिए)।  
- परिणामों को JSON में एक्सपोर्ट करें ताकि डाउनस्ट्रीम प्रोसेसिंग आसान हो।  
- OCR स्टेप को एक Flask API में इंटीग्रेट करें ताकि अन्य सर्विसेज़ इसे कॉल कर सकें।  

यदि आपको कोई अजीब समस्या मिले, तो अधिकांश OCR लाइब्रेरीज़ के आसपास की कम्युनिटी सक्रिय है—“ocr library language pack installation” सर्च करें या नीचे कमेंट डालें। Happy coding, और तस्वीरों को खोज योग्य टेक्स्ट में बदलने का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}