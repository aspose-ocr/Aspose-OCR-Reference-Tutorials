---
category: general
date: 2026-06-28
description: Python का उपयोग करके बैच OCR कैसे करें। कई छवियों को OCR करना सीखें,
  PNG से टेक्स्ट निकालें, और एक पूर्ण Python OCR ट्यूटोरियल के साथ इमेज को टेक्स्ट
  में बदलें।
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: hi
og_description: Python में बैच OCR कैसे करें, यह पहली पंक्ति में समझाया गया है। इस
  Python OCR ट्यूटोरियल का पालन करके PNG फ़ाइलों से टेक्स्ट को कुशलतापूर्वक निकालें।
og_title: Python में बैच OCR कैसे करें – पूर्ण प्रोग्रामिंग गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python में बैच OCR कैसे करें – पूर्ण चरण‑दर‑चरण मार्गदर्शिका
url: /hi/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में बैच OCR कैसे करें – पूर्ण चरण‑दर‑चरण गाइड

क्या आपने कभी सोचा है **how to batch OCR** स्कैन की हुई पृष्ठों के ढेर को बिना ऐसे लूप लिखे जो आपके UI को ब्लॉक करे? आप अकेले नहीं हैं। दर्जनों PNG फ़ाइलों को एक‑एक करके प्रोसेस करना पेंट सूखते देखे जैसा लग सकता है, ख़ासकर जब प्रत्येक इमेज को डिकोड करने में एक‑दो सेकंड लगते हैं।  

इस ट्यूटोरियल में हम आपको एक साफ़, नॉन‑ब्लॉकिंग तरीका दिखाएंगे जिससे आप एक साथ **OCR multiple images** कर सकें, **extract text from PNG** फ़ाइलों से टेक्स्ट निकाल सकें, और आधुनिक Python OCR इंजन का उपयोग करके **convert image to text** कर सकें। अंत तक आपके पास एक तैयार‑चलाने‑योग्य स्क्रिप्ट होगी जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं – एक तेज़ *python ocr tutorial* या प्रोडक्शन‑ग्रेड बैच जॉब के लिए एकदम उपयुक्त।

## आप क्या बनाएँगे

- एक OCR इंजन को इनिशियलाइज़ करें और उसकी भाषा को लैटिन (या कोई भी आवश्यक भाषा) पर सेट करें।  
- इंजन को इमेज पाथ की सूची (हमारे उदाहरण में PNG) दें।  
- एक बैच ऑपरेशन लॉन्च करें जो Future‑like ऑब्जेक्ट रिटर्न करता है।  
- थ्रेड पूल के साथ सभी परिणामों को एक साथ प्राप्त करें, जिससे आपका मुख्य थ्रेड मुक्त रहे।  
- प्रत्येक पेज के पहचाने गए टेक्स्ट को प्रिंट करें, साफ़ रूप से अलग किया हुआ।

कोई छिपा जादू नहीं, बस साधारण Python और एक थर्ड‑पार्टी OCR लाइब्रेरी (हम उदाहरण के लिए काल्पनिक `pyocr` पैकेज का उपयोग करेंगे)।

**आवश्यकताएँ**  
- Python 3.8+ स्थापित हो।  
- `concurrent.futures` और Python फ़ंक्शन्स की बुनियादी समझ।  
- `OcrEngine` क्लास प्रदान करने वाली OCR लाइब्रेरी तक पहुँच (जैसे, `pip install pyocr`)।  

यदि आपके पास इनमें से कोई भी नहीं है, तो अभी प्राप्त करें – यह सोचने से आसान है।

---

## Python में बैच OCR – मुख्य अवधारणाएँ

कोड में डुबने से पहले, चलिए प्रत्येक चरण के पीछे के “क्यों” का उत्तर देते हैं।

1. **भाषा क्यों सेट करें?**  
   जब इंजन को पता हो कि कौन से अक्षर अपेक्षित हैं, तो OCR की सटीकता बहुत बढ़ जाती है। लैटिन अंग्रेज़ी, फ़्रेंच, स्पेनिश आदि के लिए काम करता है। आवश्यकता होने पर `Language.Japanese` या `Language.Arabic` पर स्विच करें।

2. **बैच ऑपरेशन क्यों उपयोग करें?**  
   एक बैच कॉल इंजन को आंतरिक रूप से काम शेड्यूल करने देता है, अक्सर नेटिव थ्रेड्स या GPU एक्सेलेरेशन का उपयोग करता है। यह एक हैंडल रिटर्न करता है जिसे आप बाद में क्वेरी कर सकते हैं, जिसका मतलब है कि आप प्रत्येक इमेज प्रोसेस होते समय ब्लॉक नहीं होते।

3. **ThreadPoolExecutor क्यों?**  
   हमें मिलने वाला Future ऑब्जेक्ट *lazy* है – यह केवल तब परिणाम खींचना शुरू करता है जब हम पूछते हैं। `getAll` को थ्रेड पूल देकर, हम Python को प्रत्येक पेज का टेक्स्ट समानांतर में फ़ेच करने देते हैं, जिससे कुल रनटाइम काफी घट जाता है।

4. **परिणामों को enumerate क्यों करें?**  
   परिणामों का क्रम इनपुट पाथ्स के क्रम से मेल खाता है, इसलिए हम सुरक्षित रूप से प्रत्येक पेज नंबर को लेबल कर सकते हैं।

इन “क्यों” बिंदुओं को समझने से आप इस पैटर्न को अन्य लाइब्रेरीज़ या बड़े डेटा सेट्स में अनुकूलित कर सकते हैं।

## चरण 1: आवश्यक पैकेज इंस्टॉल और इम्पोर्ट करें

पहले, सुनिश्चित करें कि OCR लाइब्रेरी इंस्टॉल है। उदाहरण में एक generic `pyocr` पैकेज उपयोग किया गया है; इसे अपने पसंदीदा वास्तविक लाइब्रेरी (जैसे, `pytesseract`, `easyocr`) से बदलें।

```bash
pip install pyocr
```

अब वह सब इम्पोर्ट करें जिसकी हमें जरूरत है।

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Pro tip:** `pathlib` से `Path` का उपयोग करने से आपका स्क्रिप्ट OS‑agnostic बनता है और पढ़ने में आसान होता है।

## चरण 2: OCR इंजन बनाएं और भाषा सेट करें

इंजन बनाना सीधा है। इस डेमो के लिए हम इसे लैटिन पर लॉक करेंगे।

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

`setLanguage` कॉल कुछ इंजनों के लिए वैकल्पिक है, लेकिन यह एक अच्छी आदत है। यह OCR मॉडल को उस कैरेक्टर सेट पर फोकस करने को बताता है जिसकी आपको जरूरत है, जिससे गति और सटीकता दोनों में सुधार होता है।

## चरण 3: प्रोसेस करने के लिए इमेज फ़ाइलों की सूची बनाएं (Extract Text from PNG)

उन सभी PNG फ़ाइलों को इकट्ठा करें जिन्हें आप कन्वर्ट करना चाहते हैं। `Path.glob` का उपयोग करने से आप बिना स्क्रिप्ट एडिट किए पूरे फ़ोल्डर को ड्रॉप कर सकते हैं।

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Why this matters:** सूची को सॉर्ट करने से हम एक निर्धारित क्रम की गारंटी देते हैं, जो बाद में प्रत्येक परिणाम को सही पेज नंबर से मिलाता है।

## चरण 4: बैच OCR ऑपरेशन लॉन्च करें (Convert Image to Text)

अब हम सूची को इंजन को देते हैं। यह मेथड एक Future‑like कंटेनर रिटर्न करता है जिसे हम बाद में पोल करेंगे।

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

इंजन के अंदर यह अपने स्वयं के वर्कर थ्रेड्स या यहाँ तक कि GPU पाइपलाइन भी स्पिन अप कर सकता है। हमें सिर्फ़ यह चाहिए कि हमारे पास एक हैंडल (`batch_future`) हो जो व्यक्तिगत परिणामों को फ़ेच करना जानता हो।

## चरण 5: सभी परिणाम एक साथ प्राप्त करें (OCR Multiple Images)

यहीं पर हम वास्तव में *batch* काम करते हैं। `getAll` को `ThreadPoolExecutor` देकर, प्रत्येक पेज का टेक्स्ट अपने थ्रेड में फ़ेच किया जाता है।

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

आप `max_workers` को अपने CPU कोर या OCR लाइब्रेरी की सिफ़ारिशों के आधार पर ट्यून कर सकते हैं। अधिक वर्कर्स ≠ हमेशा तेज़ – अपने CPU उपयोग को देखें।

## चरण 6: पहचाने गए टेक्स्ट को आउटपुट करें (Python OCR Tutorial Finale)

अंत में, प्रत्येक पेज का टेक्स्ट प्रिंट करें। `Result` ऑब्जेक्ट `getText()` एक्सपोज़ करता है – यदि आपकी लाइब्रेरी अलग मेथड नाम उपयोग करती है तो उसे समायोजित करें।

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**अपेक्षित आउटपुट (उदाहरण)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

यदि कोई इमेज फेल हो जाती है, तो अधिकांश इंजन एक खाली स्ट्रिंग एम्बेड करते हैं या एक्सेप्शन थ्रो करते हैं – आप लूप को `try/except` ब्लॉक में रैप करके एज केस को ग्रेसफुली हैंडल कर सकते हैं।

## पूर्ण स्क्रिप्ट – चलाने के लिए तैयार

नीचे पूरी, सेल्फ‑कंटेन्ड स्क्रिप्ट है। इसे `batch_ocr.py` नाम की फ़ाइल में कॉपी‑पेस्ट करें, `YOUR_DIRECTORY` को एडजस्ट करें, और `python batch_ocr.py` चलाएँ।

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

सेव करें, रन करें, और देखें कि कंसोल में निकाला गया टेक्स्ट भरता है। सरल, तेज़, और पूरी तरह असिंक्रोनस।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| **कोई आउटपुट नहीं** – खाली स्ट्रिंग्स | OCR इंजन ने कोई टेक्स्ट नहीं पाया (इमेज बहुत शोरयुक्त है) | इमेज को प्री‑प्रोसेस करें: बाइनराइज़ करें, डेस्क्यू करें, या DPI बढ़ाएँ |
| **`FileNotFoundError`** | गलत डायरेक्टरी पाथ या PNG फ़ाइलें गायब हैं | `YOUR_DIRECTORY` को दोबारा जांचें और सुनिश्चित करें कि फ़ाइलें `.png` पर समाप्त हों |
| **उच्च CPU उपयोग** | `max_workers` आपके मशीन के लिए बहुत अधिक सेट है | `max_workers` कम करें या यदि समर्थित हो तो GPU एक्सेलेरेशन सक्षम करें |
| **Unicode गड़बड़ी** | इंजन ने डिफ़ॉल्ट रूप से एक अलग भाषा चुनी | बैच OCR से पहले `engine.setLanguage(Language.Latin)` (या उपयुक्त) कॉल करें |

इन समस्याओं को जल्दी हल करने से आप कई घंटे डिबगिंग से बचते हैं।

## ट्यूटोरियल का विस्तार – अगले कदम

- अन्य फ़ॉर्मैट (JPEG, TIFF) में कई इमेज OCR करें – बस ग्लोब पैटर्न बदलें।  
- PNG से टेक्स्ट निकालें और उसे सर्च इंडेक्स (जैसे, Elasticsearch) में फ़ीड करें।  
- `reportlab` या `PyPDF2` का उपयोग करके PDF जनरेशन के लिए इमेज को टेक्स्ट में बदलें।  
- `multiprocessing` या Celery जैसे टास्क क्यू के साथ मशीनों में समानांतर चलाएँ बड़े डेटा सेट्स के लिए।  

इनमें से प्रत्येक विषय आपके द्वारा अभी पूरा किए गए **python ocr tutorial** पर स्वाभाविक रूप से बनता है।

## निष्कर्ष

हमने **how to batch OCR** की एक संग्रहित PNG फ़ाइलों पर प्रक्रिया की, बैच‑ओरिएंटेड API की शक्ति दर्शाई, और थ्रेड‑पूल्ड अप्रोच के साथ **extract text from PNG** कैसे करें दिखाया। ऊपर दिया गया पूर्ण स्क्रिप्ट प्रोडक्शन‑रेडी है, और अब आपके पास किसी भी OCR‑हैवी Python प्रोजेक्ट के लिए एक ठोस आधार है।

इसे चलाएँ, भाषा सेटिंग्स को ट्यून करें, और शायद `pyocr` को `pytesseract` से बदलें – पैटर्न वही रहता है। सवाल हैं या कोई कूल यूज़‑केस शेयर करना चाहते हैं? कमेंट डालें, और बातचीत जारी रखें।

*कोडिंग का आनंद लें!*

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दर्शाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Aspose OCR के साथ इमेज से टेक्स्ट निकालें – चरण‑दर‑चरण गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [फ़ोल्डर्स पर OCR ऑपरेशन का उपयोग करके इमेज से टेक्स्ट निकालें](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Aspose.OCR for .NET में लिस्ट के साथ बैच OCR इमेज कैसे करें](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}