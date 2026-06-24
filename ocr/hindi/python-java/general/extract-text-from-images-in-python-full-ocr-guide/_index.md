---
category: general
date: 2026-06-19
description: Python OCR का उपयोग करके छवियों से टेक्स्ट निकालें। स्वचालित भाषा पहचान,
  समानांतर प्रोसेसिंग और बैच पहचान को एक संक्षिप्त ट्यूटोरियल में सीखें।
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: hi
og_description: Python OCR के साथ छवियों से टेक्स्ट निकालें। यह गाइड स्वचालित भाषा
  पहचान, समानांतर प्रोसेसिंग और बैच मान्यता को एक ही ट्यूटोरियल में दिखाता है।
og_title: Python में छवियों से टेक्स्ट निकालें – पूर्ण OCR गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python में छवियों से टेक्स्ट निकालें – पूर्ण OCR गाइड
url: /hi/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज़ से टेक्स्ट निकालें Python में – पूर्ण OCR गाइड

क्या आपने कभी सोचा है कि **इमेज़ से टेक्स्ट निकालना** बिना हर शब्द को मैन्युअली टाइप किए कैसे संभव है? आप अकेले नहीं हैं। चाहे आप पुराने रसीदों को डिजिटल बना रहे हों, सर्चेबल डॉक्यूमेंट आर्काइव बना रहे हों, या बस कूल AI ट्रिक्स के साथ खेल रहे हों, तस्वीरों से टेक्स्ट निकालने की क्षमता आज के किसी भी Python डेवलपर के लिए आवश्यक कौशल है।

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने‑योग्य उदाहरण के माध्यम से **इमेज़ से टेक्स्ट निकालने** की प्रक्रिया को देखेंगे, जिसमें एक लोकप्रिय OCR इंजन का उपयोग किया गया है। हम ऑटोमैटिक लैंग्वेज डिटेक्शन, स्पीड के लिए पैरालेल प्रोसेसिंग, और बैच इमेज़ रेकग्निशन को कवर करेंगे ताकि आप सेकंड में दर्जनों फ़ाइलों को संभाल सकें। क्या यह वही है जिसकी आपको ज़रूरत है? चलिए शुरू करते हैं।

## आप क्या सीखेंगे

- `ocr.OcrEngine` के साथ OCR इंजन को इंस्टैंशिएट करना।
- **ऑटोमैटिक लैंग्वेज डिटेक्शन** को सक्षम करना ताकि इंजन खुद ही सही भाषा चुन ले।
- कस्टम थ्रेड पूल के साथ **पैरालेल प्रोसेसिंग OCR** को कॉन्फ़िगर करना।
- फ़ाइलों की सूची पर **बैच इमेज़ रेकग्निशन** चलाना।
- प्रत्येक इमेज़ के लिए पहचाने गए टेक्स्ट को प्रिंट करना, जिसे आप सेव या इंडेक्स कर सकते हैं।

कोई बाहरी डॉक्यूमेंटेशन आवश्यक नहीं—आपको जो चाहिए वह सब यहाँ है, और कोड `ocr` पैकेज के साथ बॉक्स से बाहर काम करता है (`pip install ocr` के ज़रिए इंस्टॉल करें)।

## आवश्यकताएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

1. Python 3.8 या उससे नया संस्करण।
2. `ocr` पैकेज (`pip install ocr`)।
3. प्रोसेस करने के लिए PNG (या JPG) इमेज़ की एक फ़ोल्डर।
4. Python फ़ंक्शन और लूप्स की बेसिक समझ।

बस इतना ही—कोई भारी डिपेंडेंसी नहीं, कोई GPU मैजिक नहीं, सिर्फ सादा Python।

![इमेज़ से टेक्स्ट निकालने का उदाहरण](https://example.com/ocr-demo.png "इमेज़ से टेक्स्ट निकालने के आउटपुट का स्क्रीनशॉट")

*Alt text: इमेज़ से टेक्स्ट निकालने का डेमो स्क्रीनशॉट*

## चरण 1 – OCR इंजन सेट अप करें (प्राथमिक कीवर्ड इन एक्शन)

सबसे पहले: एक OCR इंजन इंस्टेंस बनाएं। `ocr.OcrEngine()` को ऑपरेशन के दिमाग़ की तरह समझें; यह कैरेक्टर्स, लाइन्स, और पैराग्राफ़ पढ़ना जानता है।

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

इंजिन को स्पष्ट रूप से क्यों चाहिए? क्योंकि **ocr.OcrEngine उपयोग** आपको भाषा सेटिंग्स, थ्रेडिंग, और बहुत कुछ पर फाइन‑ग्रेन कंट्रोल देता है। यह एक‑लाइनर हेल्पर्स की तुलना में **इमेज़ से टेक्स्ट निकालने** का सबसे लचीला तरीका है।

## चरण 2 – इंजन को ऑटोमैटिक भाषा पहचान करने दें

ज्यादातर OCR लाइब्रेरीज़ को यह बताना पड़ता है कि किस भाषा की तलाश करनी है। यह एक‑भाषा प्रोजेक्ट के लिए ठीक है, लेकिन मिश्रित‑भाषा बैच के लिए झंझट भरा हो सकता है। सौभाग्य से, `ocr` पैकेज **ऑटोमैटिक भाषा पहचान** को सपोर्ट करता है।

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

`engine.language` को `ocr.Language.Auto` सेट करने से इंजन प्रत्येक इमेज़ को sniff करके उपयुक्त भाषा मॉडल चुन लेता है। यह छोटा सा लाइन अंतर्राष्ट्रीय डॉक्यूमेंट्स के साथ काम करते समय घंटों की मैन्युअल कॉन्फ़िगरेशन बचा देता है।

## चरण 3 – पैरालेल प्रोसेसिंग OCR से गति बढ़ाएँ

यदि आपके पास चार या अधिक CPU कोर हैं, तो उनका उपयोग क्यों न करें? इंजन एक थ्रेड पूल बना सकता है, जिससे कई इमेज़ एक साथ प्रोसेस हो सकें। यही वह जगह है जहाँ **पैरालेल प्रोसेसिंग OCR** चमकता है।

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

अपने मशीन के अनुसार संख्या `4` को समायोजित कर सकते हैं। अधिक थ्रेड → तेज़ बैच रन, लेकिन याद रखें कि प्रत्येक थ्रेड मेमोरी खपत करता है, इसलिए अपने वातावरण के लिए एक संतुलित संख्या चुनें।

## चरण 4 – प्रोसेस करने के लिए इमेज़ एकत्र करें

अब हमें फ़ाइल पाथ्स की एक सूची चाहिए। आप यह सूची मैन्युअली बना सकते हैं, CSV से पढ़ सकते हैं, या `glob` का उपयोग कर सकते हैं। स्पष्टता के लिए, हम एक छोटी सूची हार्ड‑कोड करेंगे:

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

`YOUR_DIRECTORY` को अपने सिस्टम पर वास्तविक पाथ से बदलें। यदि आपके पास दर्जनों फ़ाइलें हैं, तो `glob.glob("*.png")` जल्दी से काम संभाल लेगा।

## चरण 5 – बैच इमेज़ रेकग्निशन चलाएँ

यह ट्यूटोरियल का दिल है: एक ही कॉल जो `files` में हर इमेज़ को प्रोसेस करता है और परिणाम ऑब्जेक्ट्स की सूची लौटाता है। यह **बैच इमेज़ रेकग्निशन** फीचर है जो बड़े‑पैमाने पर OCR को प्रैक्टिकल बनाता है।

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

पर्दे के पीछे, इंजन प्रत्येक फ़ाइल को पहले कॉन्फ़िगर किए गए चार वर्कर थ्रेड्स में वितरित करता है, साथ ही प्रत्येक चित्र के लिए ऑटो‑डिटेक्टेड भाषा भी। मेथड एक सूची लौटाता है जहाँ प्रत्येक एलिमेंट में पहचाना गया टेक्स्ट और मेटाडेटा होता है।

## चरण 6 – निकाले गए टेक्स्ट को प्रिंट (या स्टोर) करें

अंत में, हम परिणामों पर लूप चलाते हैं और टेक्स्ट प्रिंट करते हैं। वास्तविक प्रोजेक्ट में आप इसे डेटाबेस या CSV फ़ाइल में लिखेंगे, लेकिन प्रिंट करने से उदाहरण सरल रहता है।

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**अपेक्षित आउटपुट** (संक्षिप्त रूप में):

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

हर ब्लॉक फ़ाइलनाम के बाद OCR‑डेराइव्ड स्ट्रिंग दिखाता है। यदि इमेज़ में कई भाषाएँ हैं, तो आप पहले के **ऑटोमैटिक भाषा पहचान** चरण के कारण उपयुक्त कैरेक्टर्स देखेंगे।

## प्रो टिप्स एवं सामान्य गलतियाँ

- **इमेज़ की क्वालिटी महत्वपूर्ण है** – धुंधली या लो‑कॉन्ट्रास्ट तस्वीरें गड़बड़ आउटपुट देंगी। आवश्यकता पड़ने पर OpenCV (`cv2.threshold`, `cv2.resize`) से प्री‑प्रोसेस करें।
- **थ्रेड काउंट बनाम I/O** – यदि आपकी इमेज़ स्लो नेटवर्क ड्राइव पर हैं, तो अधिक थ्रेड मदद नहीं करेंगे। `top` या `Task Manager` से CPU उपयोग पर नजर रखें।
- **Unicode हैंडलिंग** – `result.text` एक Unicode स्ट्रिंग है। फ़ाइलों में लिखते समय `encoding="utf‑8"` के साथ खोलें ताकि `UnicodeEncodeError` न आए।
- **मेमोरी उपयोग** – बड़े PDFs बहुत RAM ले सकते हैं। यदि `MemoryError` मिले, तो थ्रेड पूल साइज घटाएँ या इमेज़ को छोटे चंक्स में प्रोसेस करें।

## पूर्ण कार्यशील स्क्रिप्ट

नीचे पूरी, कॉपी‑एंड‑पेस्ट‑रेडी स्क्रिप्ट है जिसमें हमने चर्चा किए सभी चरण शामिल हैं। इसे `batch_ocr.py` के रूप में सेव करें और `python batch_ocr.py` चलाएँ।

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

ऐसे चलाएँ:

```bash
python batch_ocr.py ./my_images 4
```

आप प्रत्येक इमेज़ के लिए एक सुंदर फ़ॉर्मेटेड टेक्स्ट ब्लॉक देखेंगे, जिससे साबित होगा कि आप **इमेज़ से टेक्स्ट निकाल सकते** हैं बड़े पैमाने पर।

## आगे क्या?

अब जब आपने Python के साथ **इमेज़ से टेक्स्ट निकालने** की बुनियादें समझ ली हैं, तो आप निम्नलिखित चीज़ों को एक्सप्लोर कर सकते हैं:

- **पोस्ट‑प्रोसेसिंग**: OCR आउटपुट को रेगएक्स या नेचुरल‑लैंग्वेज लाइब्रेरीज़ से साफ़ करें।
- **PDF कन्वर्ज़न**: निकाले गए स्ट्रिंग्स को एक PDF जेनरेटर में फीड करें ताकि सर्चेबल PDFs बन सकें।
- **क्लाउड OCR सर्विसेज**: ऑन‑प्रेम `ocr` परिणामों की तुलना Google Vision या Azure OCR से करें ताकि एज‑केस सटीकता मिल सके।
- **GUI फ्रंट‑एंड**: एक छोटा Flask या FastAPI ऐप बनाएं जो यूज़र्स को इमेज़ अपलोड करने और तुरंत निकाला गया टेक्स्ट देखने की सुविधा दे।

इन सभी टॉपिक्स का आधार वही **Python OCR लाइब्रेरी** है जिसे आपने अभी सेट किया है, और सभी को वही **पैरालेल प्रोसेसिंग OCR** ट्रिक्स मिलेंगी जो हमने यहाँ इस्तेमाल की हैं।

---

*हैप्पी कोडिंग! अगर कोई समस्या आती है, तो नीचे कमेंट करें—मैं हमेशा OCR की गड़बड़ियों को सॉल्व करने के लिए तैयार हूँ।*

## अगला क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}