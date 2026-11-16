---
category: general
date: 2026-07-05
description: Python OCR का उपयोग करके छवि से तालिका निकालें। जानें कैसे तालिका निकाली
  जाए, छवि को TSV में परिवर्तित किया जाए, और OCR तालिका छवि Python तकनीकों में निपुण
  बनें।
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: hi
og_description: Python OCR के साथ छवि से तालिका निकालें। यह गाइड दिखाता है कि कैसे
  तालिका निकाली जाए, छवि को TSV में बदला जाए, और OCR तालिका छवि Python टूल्स का उपयोग
  किया जाए।
og_title: इमेज से टेबल निकालें – पाइथन में इमेज को TSV में बदलें
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: इमेज से टेबल निकालें – पायथन में इमेज को TSV में बदलें
url: /hi/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# छवि से तालिका निकालें – Python में छवि को TSV में बदलें

क्या आपने कभी सोचा है कि बिना सिरदर्द के छवि से तालिका कैसे निकाली जाए? इस ट्यूटोरियल में हम **तालिका** डेटा को `aocr` लाइब्रेरी की मदद से चित्र से निकालेंगे और उसे एक साफ़ TSV फ़ाइल में बदलेंगे। कोई जादू नहीं, बस कुछ पंक्तियों का Python कोड और थोड़ा AI‑संचालित पोस्ट‑प्रोसेसिंग।

यदि आपने कभी स्कैन किए हुए इनवॉइस या स्क्रीनशॉट से तालिका को कॉपी‑पेस्ट करने की कोशिश की और गड़बड़ परिणाम मिले, तो आपको समझ आएगा कि OCR‑आधारित तरीका क्यों सीखना ज़रूरी है। अंत तक, आप किसी भी तालिका वाली छवि को Python में फीड करके साफ़, टैब‑सेपरेटेड वैल्यूज़ प्राप्त कर सकेंगे, जो स्प्रेडशीट या डेटाबेस में आसानी से उपयोग हो सकें।

---

## आपको क्या चाहिए

शुरू करने से पहले सुनिश्चित करें कि आपके मशीन पर नीचे दिए गए सभी चीज़ें मौजूद हैं:

| आवश्यकता | क्यों ज़रूरी है |
|-------------|----------------|
| Python 3.9+ | `aocr` पैकेज आधुनिक Python रनटाइम को लक्षित करता है। |
| `aocr` लाइब्रेरी (`pip install aocr`) | वह OCR इंजन और AI पोस्ट‑प्रोसेसर प्रदान करता है जिसका हम उपयोग करेंगे। |
| तालिका वाली छवि फ़ाइल (PNG, JPG, आदि) | वह स्रोत डेटा जिससे हम निकालेंगे। |
| वैकल्पिक: एक वर्चुअल एनवायरनमेंट | डिपेंडेंसीज़ को अलग रखता है—बहुत अनुशंसित। |

इन चीज़ों का होना गाइड के बीच में रुकावटों से बचाएगा।

---

## डिपेंडेंसीज़ इंस्टॉल करें

पहले OCR टूलिंग को इंस्टॉल करें। टर्मिनल खोलें और चलाएँ:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **प्रो टिप:** यदि आपको परमिशन एरर मिलते हैं, तो `pip install` कमांड में `--user` जोड़ें या ग्लोबल इंस्टॉल के लिए `pipx` इस्तेमाल करें।

---

## चरण 1 – OCR इंजन को इनिशियलाइज़ करें

इंजन प्रक्रिया का दिल है। इसे ऐसे समझें जैसे वह “दिमाग” है जो प्रत्येक पिक्सेल को देखता है और तय करता है कि कौन‑सा अक्षर कहाँ होना चाहिए।

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

हम एक फ़ंक्शन कॉल करने के बजाय इंजन को इंस्टैंशिएट क्यों करते हैं? इंजन ऑब्जेक्ट हमें बाद में कस्टम पोस्ट‑प्रोसेसर जोड़ने की सुविधा देता है, जिससे आउटपुट पर बारीक नियंत्रण मिलता है—जब आपको **ocr table image python** की सटीकता चाहिए, तब यह आवश्यक होता है।

---

## चरण 2 – AI पोस्ट‑प्रोसेसर जोड़ें

`aocr` एक हल्का AI पोस्ट‑प्रोसेसर के साथ आता है जो कच्चे OCR परिणामों को साफ़ करता है जबकि सेल बॉर्डर को बरकरार रखता है। कोई अतिरिक्त आर्ग्यूमेंट नहीं चाहिए, जिससे कोड साफ़ रहता है।

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

यदि आप इस चरण को छोड़ देते हैं, तो आपको अभी भी कच्चा टेक्स्ट मिलेगा, लेकिन तालिका की संरचना गड़बड़ होगी—जैसे एक स्प्रेडशीट जहाँ हर सेल एक रहस्य हो। पोस्ट‑प्रोसेसर मूल ग्रिड के अनुसार टेक्स्ट को संरेखित करने का काम करता है।

---

## चरण 3 – अपनी तालिका वाली छवि लोड करें

आप किसी भी पाथ से छवि लोड कर सकते हैं, लेकिन स्पष्टता के लिए हम एक प्लेसहोल्डर डायरेक्टरी का उपयोग करेंगे। `"YOUR_DIRECTORY/invoice_table.png"` को अपनी फ़ाइल के वास्तविक पाथ से बदलें।

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **नोट:** `aocr.Image` स्वचालित रूप से छवि फ़ॉर्मेट पहचानता है और कलर चैनल को सामान्य करता है, इसलिए आपको फ़ाइल को पहले से प्रोसेस करने की ज़रूरत नहीं है जब तक कि वह बहुत ख़राब न हो।

---

## चरण 4 – स्ट्रक्चर्ड OCR चलाएँ

अब इंजन छवि को स्कैन करता है और एक कच्चा टेबल ऑब्जेक्ट लौटाता है। इस ऑब्जेक्ट में रो, कॉलम और प्रत्येक सेल का कच्चा टेक्स्ट होता है।

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

`recognize_structured` का उपयोग सामान्य `recognize` कॉल की बजाय क्यों किया जाता है? स्ट्रक्चर्ड वैरिएंट रो/कॉलम सीमाओं का अनुमान लगाने की कोशिश करता है, जिससे आपको एक मैट्रिक्स‑जैसा परिणाम मिलता है जो बाद में TSV में बदलना बहुत आसान होता है।

---

## चरण 5 – AI पोस्ट‑प्रोसेसर से डेटा साफ़ करें

पोस्ट‑प्रोसेसर चलाने से कच्चा आउटपुट परिष्कृत हो जाता है: यह अनावश्यक कैरेक्टर हटाता है, विभाजित फ्रैगमेंट को मर्ज करता है, और सुनिश्चित करता है कि प्रत्येक सेल का टेक्स्ट सही ढंग से संरेखित हो।

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

यदि आप `processed_table.table` को देखेंगे, तो आपको रो की एक लिस्ट मिलेगी, जहाँ प्रत्येक रो `Cell` ऑब्जेक्ट्स की लिस्ट होगी। प्रत्येक `Cell` का `.text` एट्रिब्यूट साफ़ किया गया स्ट्रिंग रखता है।

---

## चरण 6 – तालिका को TSV के रूप में एक्सपोर्ट करें

अंतिम चरण प्रोसेस्ड डेटा को टैब‑सेपरेटेड वैल्यूज़ (TSV) फ़ाइल में बदलना है—बिल्कुल वही जो आपको **छवि को TSV में बदलने** के लिए Excel या Google Sheets में चाहिए।

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

स्क्रिप्ट चलाने से प्रत्येक रो कंसोल में प्रिंट होगा (यदि आप चाहें) और एक साफ़ TSV फ़ाइल लिखी जाएगी जिसे आप किसी भी स्प्रेडशीट प्रोग्राम में खोल सकते हैं।

### त्वरित सत्यापन

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

आपको ठीक‑ठाक संरेखित कॉलम दिखने चाहिए, जैसे:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

यदि आउटपुट गड़बड़ दिखे, तो छवि की गुणवत्ता (शार्पनेस, कॉन्ट्रास्ट) दोबारा जांचें और OCR इंजन की सेटिंग्स को ट्यून करने पर विचार करें—`engine.set_config(...)` से आप भाषा मॉडल और कॉन्फिडेंस थ्रेशोल्ड समायोजित कर सकते हैं।

---

## सामान्य किनारे के मामलों को संभालना

| स्थिति | सुझाया गया समाधान |
|-----------|-------------------|
| **झुकी हुई छवि** | `Pillow` (`Image.rotate`) का उपयोग करके पहले रोटेट करें, फिर `aocr` को दें। |
| **कम कॉन्ट्रास्ट** | हिस्टोग्राम इक्वलाइज़ेशन (`cv2.equalizeHist`) लागू करके पठनीयता बढ़ाएँ। |
| **मर्ज्ड सेल्स** | ज्ञात डिलिमिटर के आधार पर TSV को बाद में विभाजित करें या उपलब्ध होने पर `merge_cells=False` फ़्लैग इस्तेमाल करें। |
| **मल्टी‑पेज PDF** | प्रत्येक पेज को पहले इमेज में बदलें (`pdf2image`) और पाइपलाइन को लूप में चलाएँ। |

इन ट्यूनिंग से आपका **ocr table image python** वर्कफ़्लो विभिन्न स्रोत सामग्री में भी मजबूत बना रहेगा।

---

## पूर्ण स्क्रिप्ट – वन‑स्टॉप सॉल्यूशन

नीचे पूरी, तैयार‑चलाने‑योग्य स्क्रिप्ट है जो हमने चर्चा किए सभी चरणों को एक साथ जोड़ती है। इसे `extract_table.py` के रूप में सेव करें और `python extract_table.py` चलाएँ।

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकें।

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}