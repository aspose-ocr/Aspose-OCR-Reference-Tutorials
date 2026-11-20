---
category: general
date: 2026-06-19
description: Python में एक सरल OCR इंजन के साथ छवियों से टेक्स्ट निकालें। सीखें कि
  स्कैन की गई छवियों को टेक्स्ट में कैसे बदलें, तस्वीरों से टेक्स्ट को पहचानें, और
  Python में इमेज फ़ाइलों को कुशलतापूर्वक सूचीबद्ध करें।
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: hi
og_description: Python में हल्के OCR इंजन का उपयोग करके छवियों से टेक्स्ट निकालें।
  यह गाइड आपको दिखाता है कि स्कैन की गई छवियों को टेक्स्ट में कैसे बदलें, तस्वीरों
  से टेक्स्ट कैसे पहचानें, और कुछ ही चरणों में Python में इमेज फ़ाइलों की सूची कैसे
  बनाएं।
og_title: Python में छवियों से टेक्स्ट निकालें – पूर्ण बैच OCR गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Python में छवियों से टेक्स्ट निकालें – पूर्ण बैच OCR गाइड
url: /hi/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में इमेज से टेक्स्ट निकालें – पूर्ण बैच OCR गाइड

क्या आपको कभी **इमेज से टेक्स्ट निकालना** पड़ा लेकिन शुरू करने का तरीका नहीं पता था? आप अकेले नहीं हैं—डेवलपर्स अक्सर स्कैन किए गए PDF, फ़ोटो में रसीदें, या स्क्रीनशॉट को सर्चेबल टेक्स्ट में बदलने की चुनौती का सामना करते हैं। इस ट्यूटोरियल में हम एक पूरी, तैयार‑चलाने‑योग्य उदाहरण के माध्यम से दिखाएंगे कि **स्कैन की गई इमेज को टेक्स्ट में कैसे बदलें**, तस्वीरों से टेक्स्ट कैसे पहचानें, और यहाँ तक कि **list image files python**‑स्टाइल में फ़ाइलों की सूची बनाएं। अंत तक आपके पास एक पुन: उपयोग योग्य स्क्रिप्ट होगी जो एक ही बार में पूरे फ़ोल्डर को प्रोसेस कर सके।

हम वह सब कवर करेंगे जिसकी आपको ज़रूरत है: आवश्यक लाइब्रेरीज़, प्रत्येक चरण का महत्व, एज‑केस हैंडलिंग, और थोड़ा ट्रबलशूटिंग। बाहरी दस्तावेज़ों का पीछा करने की ज़रूरत नहीं; नीचे दिया गया कोड सेल्फ‑कंटेन्ड है, और व्याख्याएँ “कैसे” *और* “क्यों” दोनों का उत्तर देती हैं। अपना पसंदीदा IDE खोलें, और चलिए शुरू करते हैं।

---

## What You’ll Build

- OCR इंजन को इनिशियलाइज़ करें (उदाहरण के लिए हम `ocr` पैकेज का उपयोग करेंगे)।
- एक डायरेक्टरी स्कैन करें और **list image files python**‑स्टाइल में PNG, JPG, और TIFF फ़ाइलों को फ़िल्टर करके सूची बनाएं।
- सभी मिली तस्वीरों पर **batch OCR** ऑपरेशन चलाएँ।
- प्रत्येक फ़ाइल के लिए निकाला गया टेक्स्ट साफ़‑साफ़ लेबल के साथ प्रिंट करें।

> **Pro tip:** यदि आपके पास `ocr` लाइब्रेरी नहीं है, तो आप कुछ छोटे बदलावों के साथ इसे `pytesseract` से बदल सकते हैं—कोर लॉजिक वही रहता है।

---

## Prerequisites

- Python 3.8+ (स्क्रिप्ट f‑strings और type hints का उपयोग करता है)।
- एक OCR लाइब्रेरी जो `OcrEngine` के साथ `recognize_batch` एक्सपोज़ करती हो। इस गाइड में हम एक काल्पनिक `ocr` पैकेज मान रहे हैं, लेकिन पैटर्न वास्तविक लाइब्रेरीज़ पर भी लागू होता है।
- एक फ़ोल्डर जिसमें वे इमेज फ़ाइलें हों जिन्हें आप प्रोसेस करना चाहते हैं (`.png`, `.jpg`, `.tif`)।

---

## Step 1 – Install & Import Required Modules

पहले, सुनिश्चित करें कि OCR पैकेज उपलब्ध है। यदि आप `pytesseract` जैसी वास्तविक लाइब्रेरी इस्तेमाल कर रहे हैं, तो इम्पोर्ट को उसी अनुसार बदलें।

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **Why this matters:** `os` को इम्पोर्ट करने से हमें क्रॉस‑प्लेटफ़ॉर्म पाथ हैंडलिंग मिलती है, जबकि `typing.List` IDE ऑटोकम्प्लीट और भविष्य‑प्रूफ़िंग में मदद करता है।

---

## Step 2 – **Extract Text from Images**: Initialize the OCR Engine

इंजन बनाना किसी भी OCR काम की पहली कदम है। हम भाषा को ऑटो‑डिटेक्ट पर सेट करते हैं ताकि इंजन मिश्रित‑भाषा दस्तावेज़ों को संभाल सके।

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **Explanation:** इंजन निर्माण को एक फ़ंक्शन में एन्कैप्सुलेट करने से कोड मॉड्यूलर रहता है। अगर बाद में आपको DPI या OCR मोड बदलना पड़े, तो आप केवल इस एक जगह को एडिट करेंगे।

---

## Step 3 – **List Image Files Python**: Gather Files from a Directory

अब हमें हर तस्वीर को लोकेट करना है जिसे हम प्रोसेस करना चाहते हैं। नीचे दिया गया लिस्ट कॉम्प्रिहेंशन एक सामान्य “list image files python” पैटर्न को दर्शाता है।

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **Edge case handling:** फ़ंक्शन सब‑फ़ोल्डर को इग्नोर करता है (बाद में आप रीकर्शन जोड़ सकते हैं) और हिडन फ़ाइलों को स्वचालित रूप से फ़िल्टर कर देता है क्योंकि वे आमतौर पर सपोर्टेड एक्सटेंशन से समाप्त नहीं होतीं।

---

## Step 4 – **Convert Scanned Images to Text**: Run Batch OCR

ज्यादातर OCR लाइब्रेरीज़ एक बैच मेथड प्रदान करती हैं जो एक‑एक इमेज प्रोसेस करने से कहीं तेज़ होती है। यहाँ हम इसे कॉल कर रहे हैं।

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **Why batch?** सभी इमेज को एक साथ भेजने से ओवरहेड कम होता है (जैसे OCR मॉडल को बार‑बार लोड करना) और अक्सर बेहतर CPU/GPU उपयोग मिलता है।

---

## Step 5 – **Recognize Text from Pictures**: Display the Results

अंत में, हम फ़ाइल नामों और OCR परिणामों की जोड़ी पर इटररेट करते हैं, और प्रत्येक इमेज के लिए एक साफ़ हेडर प्रिंट करते हैं।

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **Tip:** `strip()` OCR द्वारा अक्सर जोड़े गए लीडिंग/ट्रेलिंग व्हाइटस्पेस को हटाता है।

---

## Full Script – Put It All Together

नीचे पूरा, चलाने योग्य प्रोग्राम दिया गया है। इसे `batch_ocr.py` के रूप में सेव करें और `python batch_ocr.py <your_folder>` चलाएँ।

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### Expected Output

मान लीजिए फ़ोल्डर में `invoice1.png` और `receipt.jpg` हैं, तो आप कुछ इस तरह देख सकते हैं:

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

प्रत्येक ब्लॉक स्पष्ट रूप से लेबल किया गया है, जिससे डाउनस्ट्रीम प्रोसेसिंग (जैसे डेटाबेस में सेव करना) आसान हो जाता है।

---

## Handling Common Pitfalls

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **No text appears** | OCR भाषा डिटेक्ट नहीं हुई या इमेज बहुत लो‑कॉन्ट्रास्ट है। | भाषा को फ़ोर्स करें (`engine.language = ocr.Language.English`) या इमेज को प्री‑प्रोसेस करें (कॉन्ट्रास्ट बढ़ाएँ)। |
| **Memory error on large batches** | इंजन सभी इमेज एक साथ लोड करने की कोशिश करता है। | `image_files` को चंक्स में बाँटें (`batch_size = 20`) और `recognize_batch` को बार‑बार कॉल करें। |
| **Unsupported file format** | आपने `.gif` या `.bmp` जोड़ दिया। | `supported_exts` ट्यूपल को एक्सटेंड करें या इमेज को पहले PNG/JPG में कन्वर्ट करें। |
| **Unicode garbling** | OCR बाइट्स रिटर्न करता है न कि स्ट्रिंग। | सुनिश्चित करें कि OCR लाइब्रेरी Unicode आउटपुट दे (`result.text.decode('utf‑8')` अगर ज़रूरी हो)। |

---

## Extending the Workflow

अब जब आप **extract text from images** कर सकते हैं, तो इन अगले कदमों पर विचार करें:

- **Export to CSV** – प्रत्येक फ़ाइलनाम और उसके निकाले गए टेक्स्ट को स्प्रेडशीट में लिखें ताकि एनालिटिक्स आसान हो।
- **Parallel processing** – `concurrent.futures.ThreadPoolExecutor` का उपयोग करके कई बैच एक साथ हैंडल करें।
- **Integrate with cloud OCR** – स्थानीय इंजन को Google Vision या Azure OCR से बदलें ताकि जटिल लेआउट पर अधिक सटीकता मिले।
- **Add image preprocessing** – Pillow या OpenCV जैसी लाइब्रेरीज़ से इमेज को डेस्क्यू, डीनॉइज़, या थ्रेशहोल्ड करें, जिससे OCR परिणाम बेहतर हों।

इन सभी आइडियाज़ में हमने जो कोर फ़ंक्शन बनाए हैं, वही उपयोग होते हैं, इसलिए आपको स्क्रैच से शुरू नहीं करना पड़ेगा।

---

## Conclusion

हमने अभी-अभी Python में **extract text from images** के लिए एक पूर्ण समाधान पर चर्चा की, जिसमें **list image files python** से लेकर **recognize text from pictures** तक और अंत में **convert scanned images to text** बैच में शामिल है। स्क्रिप्ट जानबूझकर सरल रखी गई है, फिर भी बड़ी प्रोजेक्ट्स के लिए पर्याप्त लचीली है—चाहे आप रसीदें डिजिटाइज़ कर रहे हों, सर्चेबल आर्काइव बना रहे हों, या डेटा‑एक्सट्रैक्शन पाइपलाइन चला रहे हों।

इसे चलाएँ, प्री‑प्रोसेसिंग स्टेप्स को ट्यून करें, और अपनी OCR सटीकता को बढ़ते देखें। अगर कोई समस्या आती है, तो “Handling Common Pitfalls” तालिका को दोबारा देखें; अधिकांश मुद्दे छोटे कॉन्फ़िगरेशन बदलावों से हल हो जाते हैं।

अगली चुनौती के लिए तैयार हैं? `pdf2image` का उपयोग करके PDF‑to‑image कन्वर्ज़न स्टेप जोड़ें, फिर उन इमेज को उसी पाइपलाइन में फीड करें। OCR को Python के समृद्ध इकोसिस्टम के साथ मिलाकर संभावनाएँ अनंत हैं।

Happy coding, and may your text be ever legible!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}