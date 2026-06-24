---
category: general
date: 2026-06-22
description: Python का उपयोग करके छवियों से बाउंडिंग बॉक्स निर्देशांक प्राप्त करें।
  Aspose OCR और JSON पार्सिंग के साथ इमेज से टेक्स्ट निकालना मिनटों में सीखें।
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: hi
og_description: Python का उपयोग करके छवियों से बाउंडिंग बॉक्स निर्देशांक प्राप्त करें।
  यह गाइड दिखाता है कि Aspose OCR के साथ Python में छवि से टेक्स्ट कैसे निकाला जाए
  और लेआउट डेटा को पार्स किया जाए।
og_title: Python में OCR से बाउंडिंग बॉक्स कोऑर्डिनेट्स प्राप्त करें – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Python में OCR से बाउंडिंग बॉक्स निर्देशांक प्राप्त करें – पूर्ण गाइड
url: /hi/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR से Python में बाउंडिंग बॉक्स कोऑर्डिनेट्स प्राप्त करें – पूर्ण गाइड

क्या आपको कभी स्कैन किए गए इनवॉइस में हर शब्द के **बाउंडिंग बॉक्स कोऑर्डिनेट्स** प्राप्त करने की ज़रूरत पड़ी, लेकिन शुरुआत कैसे करें, समझ नहीं आया? आप अकेले नहीं हैं। कई ऑटोमेशन प्रोजेक्ट्स में, आपको टेक्स्ट को इमेज पर लोकेट करना पड़ता है ताकि उसे हाइलाइट, रिडैक्ट या डाउनस्ट्रीम एनालिटिक्स में फीड किया जा सके। अच्छी खबर? कुछ ही लाइनों के Python कोड और Aspose.OCR के साथ आप टेक्स्ट **और** उसकी सटीक पोजीशन एक ही पास में निकाल सकते हैं।

इस ट्यूटोरियल में हम एक हैंड‑ऑन उदाहरण के माध्यम से दिखाएंगे कि कैसे **extract text from image python**‑स्टाइल में टेक्स्ट निकालें, फिर JSON लेआउट डेटा में जाकर बाउंडिंग बॉक्स निकालें। कोई फालतू बात नहीं, सिर्फ एक काम करने वाला स्क्रिप्ट, प्रत्येक स्टेप के महत्व की व्याख्या, और सामान्य समस्याओं से बचने के टिप्स।

---

## आप क्या बनाएँगे

इस गाइड के अंत तक आपके पास एक तैयार‑चलाने‑योग्य Python स्क्रिप्ट होगी जो:

1. एक इमेज (जैसे, इनवॉइस PNG) को Aspose OCR में लोड करती है।
2. इंजन को JSON लेआउट जानकारी आउटपुट करने के लिए कॉन्फ़िगर करती है।
3. JSON को Python डिक्शनरी में पार्स करती है।
4. प्रत्येक पहचाने गए शब्द पर इटररेट करके उसका टेक्स्ट **और** बाउंडिंग बॉक्स कोऑर्डिनेट्स प्रिंट करती है।

आप देखेंगे कि कोड को मल्टी‑पेज PDFs, विभिन्न इमेज फॉर्मैट्स, और कस्टम कोऑर्डिनेट सिस्टम के लिए कैसे अनुकूलित किया जाए।

### पूर्वापेक्षाएँ

- आपके मशीन पर Python 3.8+ इंस्टॉल हो।  
- Aspose.OCR for Python का सक्रिय लाइसेंस या फ्री ट्रायल (लाइब्रेरी लाइसेंस के बिना भी चलती है लेकिन वॉटरमार्क जोड़ती है)।  
- `pip install aspose-ocr` (PyPI पर पैकेज का नाम)।  
- एक सैंपल इमेज जिसका नाम `invoice.png` हो, जिसे आप किसी फ़ोल्डर में रख सकते हैं।

बस इतना ही—कोई भारी फ्रेमवर्क नहीं, कोई बाहरी सर्विस नहीं। चलिए शुरू करते हैं।

---

## Step 1: Install and Import the Required Libraries

सबसे पहले, सुनिश्चित करें कि Aspose OCR पैकेज और बिल्ट‑इन `json` मॉड्यूल उपलब्ध हैं। `json` मॉड्यूल Python के साथ आता है, इसलिए हमें केवल Aspose इंस्टॉल करना है।

```bash
pip install aspose-ocr
```

अब इन्हें अपने स्क्रिप्ट में इम्पोर्ट करें:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **यह क्यों महत्वपूर्ण है:** `aspose.ocr` को इम्पोर्ट करने से आपको हाई‑परफ़ॉर्मेंस OCR इंजन मिल जाता है, जबकि `json` आपको रॉ लेआउट स्ट्रिंग को नेेटिव Python डिक्शनरी में बदलने की सुविधा देता है जिससे ट्रैवर्सल आसान हो जाता है।

---

## Step 2: Create the OCR Engine and Load Your Image

इंजन प्रोसेस का दिल है। आप इसे इंस्टैंशिएट करते हैं, फिर उसे उस इमेज की ओर पॉइंट करते हैं जिसे आप स्कैन करना चाहते हैं।

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **प्रो टिप:** `"YOUR_DIRECTORY/invoice.png"` को अपने वास्तविक फ़ाइल के एब्सोल्यूट या रिलेटिव पाथ से बदलें। अगर फ़ाइल नहीं मिलती, तो Aspose `FileNotFoundError` थ्रो करेगा, इसलिए स्पेलिंग दोबारा चेक करें।

---

## Step 3: Configure the Engine to Output JSON Layout Data

Aspose OCR प्लेन टेक्स्ट, OCR‑only JSON, या फुल लेआउट JSON रिटर्न कर सकता है जिसमें शब्दों, लाइनों, और यहाँ तक कि व्यक्तिगत कैरेक्टर्स के कोऑर्डिनेट्स शामिल होते हैं। **बाउंडिंग बॉक्स कोऑर्डिनेट्स** पाने के लिए हमें लेआउट JSON चाहिए।

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **JSON क्यों?** JSON भाषा‑निर्पेक्ष, मानव‑पठनीय, और Python डिक्शनरी में साफ़ मैप होता है। लेआउट JSON में एक `"words"` एरे होता है जहाँ प्रत्येक एंट्री में टेक्स्ट और `boundingBox` एरे (आठ नंबर, चार कोने के पॉइंट) होते हैं।

---

## Step 4: Run Recognition and Grab the Raw JSON String

अब हम वास्तव में OCR चलाते हैं। `recognize()` मेथड एक `OcrResult` ऑब्जेक्ट रिटर्न करता है, जिससे हम JSON स्ट्रिंग निकाल सकते हैं।

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

अगर आप `layout_json` को प्रिंट करेंगे तो आपको कुछ इस तरह दिखेगा:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **एज केस:** कुछ इमेजेज़ में अगर OCR इंजन कोई टेक्स्ट डिटेक्ट नहीं कर पाता तो `"words"` एरे खाली रह सकता है। ऐसे में इमेज क्वालिटी (कॉन्ट्रास्ट, रिज़ॉल्यूशन) चेक करें।

---

## Step 5: Parse the JSON into a Python Dictionary

नेेटिव Python स्ट्रक्चर के साथ काम करना स्ट्रिंग मैनिपुलेशन से कहीं आसान है। `json.loads()` फ़ंक्शन से स्ट्रिंग को डिक्शनरी में बदलें।

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

अब `layout_data["words"]` शब्दों और उनके बाउंडिंग बॉक्स की डिक्शनरीज़ की लिस्ट है।

---

## Step 6: Iterate Over Words and **Get Bounding Box Coordinates**

यह हमारे ट्यूटोरियल का कोर है: प्रत्येक शब्द पर लूप लगाएँ, टेक्स्ट निकालें, और कोऑर्डिनेट्स प्रिंट करें। यही वह जगह है जहाँ हम **बाउंडिंग बॉक्स कोऑर्डिनेट्स** प्राप्त करते हैं।

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**सैंपल आउटपुट** (आपके नंबर इमेज के आधार पर अलग होंगे):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **आठ‑पॉइंट फॉर्मेट क्यों?** चार कोने (टॉप‑लेफ़्ट, टॉप‑राइट, बॉटम‑राइट, बॉटम‑लेफ़्ट) आपको शब्द के चारों ओर पॉलीगॉन ड्रॉ करने की अनुमति देते हैं, भले ही टेक्स्ट स्क्यू हो। अगर आपको सिर्फ साधा रेक्टैंगल चाहिए, तो आप `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min`, और `height = max(y…) - y_min` निकाल सकते हैं।

---

## Optional Enhancements

### 1. Convert Bounding Boxes to Simple Rectangles

अगर आपका डाउनस्ट्रीम टूल `(x, y, width, height)` फॉर्मेट चाहता है, तो एक हेल्पर जोड़ें:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Handle Multi‑Page PDFs

Aspose OCR PDF स्ट्रीम्स को भी स्वीकार कर सकता है। इमेज लोडिंग लाइन को इस तरह बदलें:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

हर पेज के लिए `set_page_number` को इटररेट करें और कोऑर्डिनेट्स को पेज‑वाइज़ कलेक्ट करें।

### 3. Visualize Bounding Boxes

अगर आप बाउंडिंग बॉक्स को मूल इमेज पर देखना चाहते हैं, तो Pillow का उपयोग करें:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

अब आप हर पहचाने गए शब्द के चारों ओर लाल आउटलाइन देखेंगे—डिबगिंग या UI ओवरले के लिए परफ़ेक्ट।

---

## Common Questions & Gotchas

- **JSON बहुत बड़ा हो गया तो?** बड़े डॉक्यूमेंट्स के लिए JSON को स्ट्रीम करें या पेज‑बाय‑पेज प्रोसेस करें ताकि मेमोरी कम रहे।
- **कुछ शब्द क्यों नहीं दिख रहे?** लो कॉन्ट्रास्ट या हैंडराइटन टेक्स्ट अक्सर OCR को फेल कर देता है। इमेज को प्री‑प्रोसेस (कॉन्ट्रास्ट बढ़ाएँ, बाइनराइज़) करें।
- **क्या मैं कैरेक्टर‑लेवल कोऑर्डिनेट्स पा सकता हूँ?** हाँ—`engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` सेट करें ताकि `"characters"` एरे मिले।
- **कोऑर्डिनेट सिस्टम ज़ीरो‑बेस्ड है?** बिल्कुल। (0, 0) इमेज के टॉप‑लेफ़्ट कोर्नर को दर्शाता है।

---

## Full Script – Ready to Copy & Run

नीचे पूरा, रन‑एबल उदाहरण है जो सभी स्टेप्स को जोड़ता है। इसे `extract_bboxes.py` के रूप में सेव करें और `python extract_bboxes.py` चलाएँ।

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}