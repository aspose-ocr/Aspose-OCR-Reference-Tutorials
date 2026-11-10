---
category: general
date: 2026-05-31
description: Python की aocr लाइब्रेरी का उपयोग करके छवि से टेक्स्ट निकालें। जानें
  कैसे इमेज को OCR किया जाए, OCR के लिए इमेज लोड करें, और कुछ ही लाइनों में विशेष
  अक्षरों को पहचानें।
draft: false
keywords:
- extract text from image
- recognize special characters
- convert image to text
- how to ocr image
- load image for ocr
language: hi
og_description: Python की aocr लाइब्रेरी का उपयोग करके छवि से टेक्स्ट निकालें। यह
  गाइड दिखाता है कि कैसे छवि को OCR किया जाए, OCR के लिए छवि लोड करें, और विशेष अक्षरों
  को जल्दी पहचानें।
og_title: Python OCR के साथ छवि से टेक्स्ट निकालें – इमेज को OCR कैसे करें
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  headline: Extract Text from Image with Python OCR – How to OCR Image
  type: TechArticle
- description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  name: Extract Text from Image with Python OCR – How to OCR Image
  steps:
  - name: 5.1 Low‑Resolution Images
    text: 'If the image is under 150 dpi, the OCR accuracy can drop dramatically.
      A quick fix is to upscale before feeding it to aocr:'
  - name: 5.2 Incorrect Language Detection
    text: 'aocr auto‑detects language, but you can force a specific script for better
      results:'
  - name: 5.3 Noise and Background Patterns
    text: 'A noisy background can confuse the model. Pre‑process with OpenCV to binarize:'
  type: HowTo
- questions:
  - answer: Not directly. Convert PDF pages to images first (e.g., using `pdf2image`)
      and then feed each image to aocr.
    question: Does this work on PDFs?
  - answer: For typical 300 dpi scans, aocr processes a page in ~0.3 s on a modern
      laptop—roughly twice as fast as vanilla Tesseract with default settings.
    question: How fast is aocr compared to Tesseract?
  - answer: 'Absolutely. Wrap the `main` function in a loop over `Path(folder).glob("*.png")`
      and collect results in a CSV. --- ## Conclusion You now have a solid, end‑to‑end
      workflow to **extract text from image** using Python’s aocr library. From loading
      the file to printing Unicode output, every step is expla'
    question: Can I batch‑process a folder of images?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Python OCR के साथ छवि से टेक्स्ट निकालें – छवि को OCR कैसे करें
url: /hi/python/general/extract-text-from-image-with-python-ocr-how-to-ocr-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR के साथ इमेज से टेक्स्ट निकालें – OCR कैसे करें

क्या आपको कभी **इमेज से टेक्स्ट निकालने** की ज़रूरत पड़ी है लेकिन यह नहीं पता था कि कौन‑सी लाइब्रेरी “Ł”, “Ž”, या “ß” जैसे अजीब सिंबल्स को संभाल सकती है? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स—जैसे स्कैन किए हुए रसीदें, बहुभाषी साइनज, या ऐतिहासिक दस्तावेज़—में **स्पेशल कैरेक्टर्स को पहचानने** की क्षमता एक उपयोगी डेटासेट और एक डेड‑एंड के बीच का अंतर बन सकती है।

अच्छी खबर? कुछ ही पंक्तियों के Python कोड और हल्के **aocr** पैकेज के साथ, आप किसी भी तस्वीर को सर्चेबल टेक्स्ट में बदल सकते हैं। नीचे आप एक पूरी, रन‑टू‑डेड स्क्रिप्ट देखेंगे, साथ ही प्रत्येक कदम के पीछे का *क्यों* भी, ताकि आप सिर्फ कॉपी‑पेस्ट न करें बल्कि समझें कि क्या हो रहा है।

## इस ट्यूटोरियल में क्या कवर किया गया है

- **aocr** लाइब्रेरी को इंस्टॉल और इम्पोर्ट करना  
- OCR के लिए इमेज लोड करना (आम समस्याओं सहित)  
- इंजन चलाकर **इमेज को टेक्स्ट में बदलना**  
- परिणाम प्रिंट करना और स्पेशल‑कैरेक्टर आउटपुट को हैंडल करना  
- बेसिक फ्लो को मल्टी‑लैंग्वेज सपोर्ट और एरर हैंडलिंग के लिए एक्सटेंड करना  

इस गाइड के अंत तक आप किसी भी भाषा की **इमेज से टेक्स्ट निकालने** में सक्षम हो जाएंगे, और जब डिफ़ॉल्ट सेटिंग्स पर्याप्त न हों तो प्रक्रिया को कैसे ट्यून करना है, यह भी जानेंगे।

## प्री‑रिक्विज़िट्स

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | aocr आधुनिक टाइपिंग फीचर्स पर निर्भर करता है |
| `pip` access | लाइब्रेरी इंस्टॉल करने के लिए |
| एक सैंपल इमेज (जैसे `multilingual.png`) | हम इसे स्पेशल कैरेक्टर्स दिखाने के लिए इस्तेमाल करेंगे |
| वर्चुअल एनवायरनमेंट की बेसिक समझ (वैकल्पिक) | डिपेंडेंसीज़ को साफ़ रखने में मदद करता है |

कोई भारी बाहरी टूल जैसे Tesseract ज़रूरी नहीं—**aocr** एक तेज़ न्यूरल इंजन बंडल करता है जो आउट‑ऑफ़‑द‑बॉक्स काम करता है।

---

## Step 1: Install the aocr Library

सबसे पहले, टर्मिनल (या IDE की कंसोल) खोलें और चलाएँ:

```bash
pip install aocr
```

*Pro tip:* अगर आप कई प्रोजेक्ट्स के बीच स्विच करते हैं, तो पहले एक वर्चुअल एनवायरनमेंट बनाएं:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # macOS/Linux
.\ocr-env\Scripts\activate    # Windows
pip install aocr
```

यह OCR डिपेंडेंसीज़ को आपके सिस्टम की बाकी चीज़ों से अलग रखता है—एक चीज़ जो बाद में बहुत सिरदर्द बचाती है।

---

## Step 2: Load Image for OCR

अब पैकेज तैयार है, हमें **OCR के लिए इमेज लोड** करनी है। `OcrEngine` क्लास को फ़ाइल का पाथ चाहिए, इसलिए सुनिश्चित करें कि इमेज मौजूद है और रीडेबल है।

```python
import aocr

# Step 2: Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Step 2b: Point to your image file (adjust the path as needed)
image_path = r"YOUR_DIRECTORY/multilingual.png"
ocr_engine.load_image(image_path)
```

> **Why this matters:**  
> - `load_image` जल्दी से सैनीटी चेक करता है (फ़ाइल मौजूद है या नहीं, सपोर्टेड फ़ॉर्मेट)।  
> - रॉ स्ट्रिंग (`r"..."`) का उपयोग करने से Windows पाथ में अनजाने एस्केप‑कैरेक्टर बग से बचा जा सकता है।  
> - अगर इमेज बहुत बड़ी है, तो aocr मेमोरी उपयोग को नियंत्रित रखने के लिए ऑटोमैटिकली डाउनस्केल कर देगा।  

अगर आपको `FileNotFoundError` मिलता है, तो पाथ दोबारा चेक करें और सुनिश्चित करें कि फ़ाइल एक्सटेंशन PNG, JPEG, या BMP में से कोई एक है।

---

## Step 3: Perform OCR – Convert Image to Text

इमेज मेमोरी में लोड हो गई, अब अगला कॉल वास्तव में **स्पेशल कैरेक्टर्स को पहचानता** है और एक Unicode स्ट्रिंग बनाता है।

```python
# Step 3: Run the OCR engine
recognized_text = ocr_engine.recognize()
```

पर्दे के पीछे, aocr एक हल्का convolutional‑recurrent नेटवर्क चलाता है जो मल्टी‑लैंग्वेज डेटासेट्स पर ट्रेन किया गया है। इसलिए आप Cyrillic, Latin‑extended, और यहाँ‑तक कि कुछ दुर्लभ glyphs को सही ढंग से दिखते देखेंगे।

---

## Step 4: Display the Extracted Text

आख़िर में, चलिए परिणाम को प्रिंट करते हैं। आउटपुट में वह सभी कैरेक्टर शामिल होंगे जो इंजन डिकोड कर सका, जिसमें वो परेशान करने वाले diacritics भी शामिल हैं।

```python
# Step 4: Show what we extracted
print("=== OCR RESULT ===")
print(recognized_text)
```

**Sample output** (आपका वास्तविक परिणाम इमेज कंटेंट पर निर्भर करेगा):

```
=== OCR RESULT ===
Łąka žužuҖß – multilingual test string
```

*Image example:*  
![Extract text from image example output](https://example.com/ocr-output.png "Extract text from image example output")

> **Note:** `print` कॉल आधुनिक Python में डिफ़ॉल्ट रूप से UTF‑8 एन्कोडिंग इस्तेमाल करता है, इसलिए अधिकांश टर्मिनलों में आपको स्पेशल कैरेक्टर्स सही दिखेंगे। अगर आउटपुट गड़बड़ दिखे, तो अपना कंसोल UTF‑8 पर सेट करें या स्ट्रिंग को `encoding='utf-8'` के साथ फ़ाइल में लिखें।

---

## Step 5: Handling Edge Cases & Common Pitfalls

### 5.1 Low‑Resolution Images

अगर इमेज 150 dpi से कम है, तो OCR की सटीकता काफी गिर सकती है। एक त्वरित समाधान है aocr को फ़ीड करने से पहले इमेज को upscale करना:

```python
from PIL import Image

img = Image.open(image_path)
img = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
img.save("upscaled.png")
ocr_engine.load_image("upscaled.png")
```

### 5.2 Incorrect Language Detection

aocr ऑटो‑डिटेक्ट करता है भाषा, लेकिन बेहतर परिणामों के लिए आप किसी खास स्क्रिप्ट को फोर्स कर सकते हैं:

```python
ocr_engine.set_language("rus")   # forces Cyrillic detection
```

सपोर्टेड लैंग्वेज कोड्स में `eng`, `deu`, `fra`, `rus`, `spa` आदि शामिल हैं।

### 5.3 Noise and Background Patterns

शोरयुक्त बैकग्राउंड मॉडल को भ्रमित कर सकता है। OpenCV से प्री‑प्रोसेस करके बाइनराइज़ करें:

```python
import cv2

raw = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)
_, thresh = cv2.threshold(raw, 127, 255, cv2.THRESH_BINARY | cv2.THRESH_OTSU)
cv2.imwrite("clean.png", thresh)
ocr_engine.load_image("clean.png")
```

---

## Full Script – One‑Click Solution

नीचे **पूरा, रन‑एबल उदाहरण** है जो सभी हिस्सों को जोड़ता है। इसे `ocr_demo.py` के रूप में सेव करें और `python ocr_demo.py` चलाएँ।

```python
# ocr_demo.py
# -------------------------------------------------
# Complete example: extract text from image using aocr
# -------------------------------------------------

import aocr
from pathlib import Path
import sys

def main(image_path: str):
    # Verify the file exists early – gives a nicer error message
    if not Path(image_path).is_file():
        sys.exit(f"❌ File not found: {image_path}")

    # 1️⃣ Create OCR engine
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Load the image (you can also call preprocess_image() here)
    ocr_engine.load_image(image_path)

    # Optional: force language if you know it (uncomment)
    # ocr_engine.set_language("eng")

    # 3️⃣ Run OCR – this is where we **convert image to text**
    recognized_text = ocr_engine.recognize()

    # 4️⃣ Output – includes special characters like Ł, Ž, Җ, ß
    print("\n=== OCR RESULT ===")
    print(recognized_text)

if __name__ == "__main__":
    # Example usage: python ocr_demo.py multilingual.png
    if len(sys.argv) != 2:
        sys.exit("Usage: python ocr_demo.py <path-to-image>")
    main(sys.argv[1])
```

ऐसे चलाएँ:

```bash
python ocr_demo.py YOUR_DIRECTORY/multilingual.png
```

आपको कंसोल में निकाले गए कैरेक्टर्स दिखने चाहिए, जिससे पुष्टि होगी कि आपने सफलतापूर्वक **इमेज से टेक्स्ट निकाला** और **स्पेशल कैरेक्टर्स को पहचाना**।

---

## Frequently Asked Questions

**Q: क्या यह PDFs पर काम करता है?**  
A: सीधे नहीं। पहले PDF पेजेज को इमेज में बदलें (जैसे `pdf2image` का उपयोग करके) और फिर प्रत्येक इमेज को aocr में फ़ीड करें।

**Q: Tesseract की तुलना में aocr की गति कैसी है?**  
A: सामान्य 300 dpi स्कैन के लिए, aocr एक पेज को लगभग ~0.3 s में प्रोसेस करता है—डिफ़ॉल्ट सेटिंग्स वाले वैनिला Tesseract से लगभग दो गुना तेज़।

**Q: क्या मैं इमेज की फ़ोल्डर को बैच‑प्रोसेस कर सकता हूँ?**  
A: बिल्कुल। `main` फ़ंक्शन को `Path(folder).glob("*.png")` के लूप में रैप करें और परिणामों को CSV में जमा करें।

---

## Conclusion

अब आपके पास Python के aocr लाइब्रेरी का उपयोग करके **इमेज से टेक्स्ट निकालने** का एक ठोस, एंड‑टू‑एंड वर्कफ़्लो है। फ़ाइल लोड करने से लेकर Unicode आउटपुट प्रिंट करने तक, हर कदम समझाया गया है ताकि आप इसे अपने प्रोजेक्ट्स में आसानी से एडेप्ट कर सकें—चाहे आप रसीद‑स्कैनिंग सर्विस बना रहे हों या बहुभाषी दस्तावेज़ आर्काइव।

अगले चरण में, इन संबंधित टॉपिक्स को एक्सप्लोर करें:

- **convert image to text** for PDFs (use `pdf2image` + OCR)  
- **recognize special characters** in handwritten notes (experiment with `ocr_engine.set_dpi(600)`)  
- **load image for OCR** in a web API (Flask + aocr)  

इसे आज़माएँ, लैंग्वेज सेटिंग्स को ट्यून करें, और देखें आपका डेटा तुरंत सर्चेबल बन जाए। कोई सवाल या कूल यूज़‑केस है? नीचे कमेंट करें—हैप्पी कोडिंग!

## What Should You Learn Next?

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}