---
category: general
date: 2026-03-18
description: Python और Aspose OCR का उपयोग करके PNG से टेक्स्ट निकालें। OCR के लिए
  इमेज कैसे लोड करें, कई फ़ाइलों पर OCR चलाएँ, और समानांतर इमेज पहचान के साथ बैच OCR
  इमेज प्राप्त करना सीखें।
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: hi
og_description: Python में Aspose OCR का उपयोग करके PNG से टेक्स्ट निकालें। यह ट्यूटोरियल
  दिखाता है कि OCR के लिए इमेज कैसे लोड करें, कई फ़ाइलों पर OCR प्रक्रिया कैसे चलाएँ,
  और समानांतर इमेज पहचान का उपयोग करके बैच OCR इमेज कैसे चलाएँ।
og_title: PNG से टेक्स्ट निकालें – समांतर OCR गाइड
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: PNG से टेक्स्ट निकालें – बैच इमेज पहचान के लिए समांतर OCR गाइड
url: /hi/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG से टेक्स्ट निकालें – बैच इमेज रिकग्निशन के लिए Parallel OCR गाइड

क्या आपको कभी **PNG फ़ाइलों से टेक्स्ट निकालना** पड़ा है लेकिन एक ही इमेज को प्रोसेस करने में बहुत समय लग रहा था? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स—जैसे इनवॉइस स्कैनर, रसीद डिजिटलाइज़र, या आर्काइव टूल्स—में गति महत्वपूर्ण होती है, और प्रत्येक PNG को एक‑एक करके प्रोसेस करना काम नहीं करता।  

इस गाइड में हम एक पूर्ण, तैयार‑चलाने‑योग्य समाधान देखेंगे जो **इमेज को OCR के लिए लोड करता है**, **ocr multiple files** को **batch OCR images** शैली में चलाता है, और Python के `threading` मॉड्यूल के साथ **parallel image recognition** का उपयोग करता है। अंत तक आपके पास एक स्क्रिप्ट होगी जो किसी भी संख्या में PNG से सेकंड में, मिनट में नहीं, टेक्स्ट निकाल लेगी।

## What You’ll Need

- Python 3.8 या नया (दिखाया गया सिंटैक्स 3.10+ पर भी काम करता है)।  
- Aspose OCR for Java/​Python पैकेज (`aspose-ocr`)। इसे `pip` के ज़रिए इंस्टॉल कर सकते हैं।  
- एक फ़ोल्डर जिसमें कुछ PNG फ़ाइलें हों जिन्हें आप प्रोसेस करना चाहते हैं।  
- थोड़ा RAM—हर थ्रेड एक छोटा OCR इंजन इंस्टेंस रखता है, इसलिए लैपटॉप भी दर्जनों वर्कर चला सकता है।

कोई बाहरी सर्विस नहीं, कोई क्लाउड की नहीं, और कोई रहस्यमय कॉन्फ़िग फ़ाइल नहीं। सिर्फ़ शुद्ध Python कोड जिसे आप कॉपी‑पेस्ट करके चला सकते हैं।

## Why extract text from PNG in parallel?

PNG को प्रोसेस करना CPU‑बाउंड होता है: OCR इंजन कई इमेज‑एनालिसिस एल्गोरिदम चलाता है जो पिक्सेल डेटा को खा लेते हैं। जब आपके पास दस, बीस, या सौ इमेज हों, तो कुल रनटाइम मूलतः प्रत्येक व्यक्तिगत रन का योग होता है।  

हर फ़ाइल के लिए एक थ्रेड स्पॉन करके, हम ऑपरेटिंग सिस्टम को इन CPU‑हैवी जॉब्स को एक साथ शेड्यूल करने देते हैं। मल्टी‑कोर मशीन पर यह अक्सर वॉल‑क्लॉक टाइम को आधा—या यहाँ तक कि चौथा—बना देता है। ट्रेड‑ऑफ़ थोड़ा अधिक मेमोरी फुटप्रिंट है, लेकिन अधिकांश बैच जॉब्स के लिए गति में बढ़ोतरी पूरी तरह से क़ीमती है।

> **Pro tip:** यदि आप सैकड़ों मेगाबाइट इमेजेस के साथ काम कर रहे हैं, तो `threading` की बजाय `concurrent.futures.ProcessPoolExecutor` का उपयोग करने पर विचार करें। प्रोसेस GIL‑बाउंड CPython इंटरप्रेटर पर असली पैरललिज़्म देते हैं, लेकिन थोड़ा अधिक ओवरहेड की कीमत पर।

## Step 1: Install Aspose OCR for Python

सबसे पहले—आइए OCR लाइब्रेरी को आपके सिस्टम पर स्थापित करें।

```bash
pip install aspose-ocr
```

यह एक ही लाइन नवीनतम Aspose OCR बाइनरीज़ और उसके Python बाइंडिंग्स को खींचती है। यदि आपको परमिशन एरर मिलता है, तो `--user` जोड़ें या वर्चुअल एनवायरनमेंट का उपयोग करें।

## Step 2: Load image for OCR – the worker function

अब हम वह कोर रूटीन परिभाषित करते हैं जो प्रत्येक थ्रेड में चलाया जाएगा। यह **loads image for OCR**, रिकग्निशन चलाता है, और निकाले गए टेक्स्ट का एक प्रीव्यू प्रिंट करता है।

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

ध्यान देने योग्य कुछ बातें:

- **हर थ्रेड के लिए नया `OcrEngine` क्यों?** इंजन आंतरिक बफ़र्स रखता है; एक ही इंस्टेंस को साझा करने से रेस कंडीशन और गड़बड़ आउटपुट हो सकता है।  
- **न्यूलाइन हटाना क्यों?** कंसोल में लॉग करते समय लाइन को साफ़ रखने के लिए।  
- **एरर हैंडलिंग?** प्रोडक्शन में आप बॉडी को `try/except` में रैप करेंगे और शायद फ़ाइल में लॉग करेंगे—जो हम बाद में कवर करेंगे।

## Step 3: List the PNG files you want to process

आप सूची को हार्ड‑कोड कर सकते हैं, लेकिन अधिक लचीला तरीका है डायरेक्टरी स्कैन करना। नीचे स्पष्टता के लिए हम तीन फ़ाइलें मैन्युअली लिस्ट कर रहे हैं; पाथ को अपने फ़ोल्डर के अनुसार बदलें।

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

यदि आप ऑटोमैटिक डिस्कवरी पसंद करते हैं:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

यह छोटा बदलाव आपको **extract text from PNG** फ़ाइलों को बल्क में निकालने देता है बिना हर बार सोर्स कोड छुए।

## Step 4: Set up ocr multiple files with batch OCR images

अब हम प्रत्येक इमेज के लिए एक थ्रेड बनाते हैं। यह **batch OCR images** पैटर्न का दिल है।

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

लिस्ट कॉम्प्रिहेंशन कोड को संक्षिप्त रखता है, और प्रत्येक `Thread` ऑब्जेक्ट टार्गेट फ़ंक्शन और उसके आर्ग्युमेंट (`image_path`) को स्टोर करता है।  

> **Side note:** Python का `threading` मॉड्यूल नेटिव OS थ्रेड्स का उपयोग करता है, इसलिए 4‑कोर लैपटॉप पर आमतौर पर एक बार में चार थ्रेड वास्तव में चलेंगे; बाकी कोर फ्री होते ही शेड्यूल किया जाएगा।

## Step 5: Run parallel image recognition

वर्कर्स को लॉन्च करना सीधा है: लिस्ट पर इटररेट करें और `start()` कॉल करें। उसके बाद `join()` से प्रत्येक थ्रेड के खत्म होने का इंतज़ार करें।

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

स्क्रिप्ट समाप्त होने पर आपको इस तरह की लाइनों की श्रृंखला दिखेगी:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

यह आउटपुट पुष्टि करता है कि प्रत्येक PNG प्रोसेस हो गया और निकाला गया टेक्स्ट आगे की हैंडलिंग (जैसे डेटाबेस में सेव करना या NLP पाइपलाइन में फीड करना) के लिए उपलब्ध है।

## Step 6: Verify the results and handle edge cases

### Checking for empty results

कभी‑कभी इमेज बहुत नॉइज़ी होती है, या OCR इंजन कोई कैरेक्टर नहीं पहचान पाता। एक त्वरित वैधता जांच आपको डाउनस्ट्रीम एरर्स से बचा सकती है।

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### Limiting the number of concurrent threads

यदि आप इसे एक छोटे VM पर चलाते हैं, तो सैकड़ों थ्रेड स्पॉन करना शेड्यूलर को ओवरवेल्म कर सकता है। आप एक सेमाफोर से कन्करेंसी को सीमित कर सकते हैं:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Saving results to a file

प्रिंट करने के बजाय, आप फ़ाइलनाम और निकाले गए टेक्स्ट के साथ एक CSV चाहते हो सकते हैं:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

CSV को **एक बार** थ्रेड फ़ंक्शन के बाहर खोलें ताकि रेस कंडीशन से बचा जा सके; `csv` मॉड्यूल का राइटर साधारण राइट्स के लिए थ्रेड‑सेफ़ है।

## Full Working Example

सब कुछ मिलाकर, यहाँ एक सिंगल स्क्रिप्ट है जिसे आप `batch_ocr.py` नाम की फ़ाइल में डाल सकते हैं और चला सकते हैं:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}