---
category: general
date: 2026-01-12
description: OCR इंजन Python का उपयोग करके PDF से टेक्स्ट निकालें – सीखें कि OCR के
  साथ PDF कैसे पढ़ें, OCR के लिए इमेज लोड करें, और संरचित परिणाम प्राप्त करें।
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: hi
og_description: OCR इंजन Python का उपयोग करके PDF से टेक्स्ट निकालें। यह ट्यूटोरियल
  दिखाता है कि OCR के साथ PDF को कैसे पढ़ें, OCR के लिए इमेज लोड करें, और विश्वसनीय
  परिणामों के लिए OCR इंजन Python का उपयोग करें।
og_title: OCR इंजन पायथन के साथ PDF से टेक्स्ट निकालें – पूर्ण गाइड
tags:
- OCR
- Python
- PDF
- Text Extraction
title: OCR इंजन पायथन के साथ PDF से टेक्स्ट निकालें – चरण‑दर‑चरण गाइड
url: /hi/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF से टेक्स्ट निकालें OCR इंजन Python – पूर्ण ट्यूटोरियल

क्या आपको कभी **PDF से टेक्स्ट निकालना** पड़ा है लेकिन फ़ाइल सिर्फ स्कैन की हुई इमेज है? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में प्राप्त PDF में चयन योग्य टेक्स्ट नहीं होता, इसलिए आगे बढ़ने का एकमात्र तरीका **OCR के साथ PDF पढ़ना** है।  

इस गाइड में हम एक व्यावहारिक, एंड‑टू‑एंड समाधान के माध्यम से चलेंगे जो बिल्कुल दिखाएगा कि **OCR के लिए इमेज लोड** कैसे करें, **OCR इंजन Python** को कैसे शुरू करें, और संरचित टेक्स्ट कैसे निकालें जिसे आप डाउनस्ट्रीम पाइपलाइनों में फीड कर सकते हैं। कोई अस्पष्ट संदर्भ नहीं, सिर्फ एक पूर्ण, चलाने योग्य उदाहरण जिसे आप आज ही कॉपी‑पेस्ट कर सकते हैं।

## आप क्या सीखेंगे

- आवश्यक Python OCR लाइब्रेरी को कैसे इंस्टॉल और इम्पोर्ट करें।  
- PDF फ़ाइल से **OCR के लिए इमेज लोड** करने के सटीक चरण।  
- इंजन की `recognize_structured()` मेथड को कैसे कॉल करें और ब्लॉक्स, लाइन्स, वर्ड्स पर इटरेट करें।  
- लो‑कन्फिडेंस परिणाम और मल्टी‑पेज PDFs को हैंडल करने के टिप्स।  

इस ट्यूटोरियल के अंत तक आपके पास एक स्क्रिप्ट होगी जो भरोसेमंद रूप से **PDF से टेक्स्ट निकालती** है, चाहे वह एक पेज हो या सौ पेज।

---

![OCR इंजन द्वारा PDF प्रोसेसिंग और संरचित टेक्स्ट आउटपुट दिखाता आरेख।](images/ocr_flow.png "PDF से टेक्स्ट निकालने का आरेख")

*Image alt text: OCR प्रोसेसिंग चरणों को दर्शाता PDF से टेक्स्ट निकालने का आरेख।*

## आवश्यकताएँ

- Python 3.9 या नया (कोड f‑strings और टाइप हिंट्स का उपयोग करता है)।  
- एक pip‑installable OCR पैकेज जो `OcrEngine` क्लास प्रदान करता है (उदाहरण के लिए, एक काल्पनिक `pyocr` लाइब्रेरी)।  
- वह PDF फ़ाइल जिसे आप प्रोसेस करना चाहते हैं, स्थानीय रूप से सहेजी हुई (जैसे, `form.pdf`)।  

यदि आपके पास OCR लाइब्रेरी नहीं है, तो इसे इस तरह इंस्टॉल करें:

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## चरण 1: PDF से टेक्स्ट निकालें – OCR इंजन सेटअप

**OCR के साथ PDF पढ़ने** से पहले हमें एक इंजन इंस्टेंस चाहिए। इंजन को ऐसे सोचें जैसे वह दिमाग हो जो प्रत्येक पिक्सेल को देखता है और तय करता है कि वह किस अक्षर का प्रतिनिधित्व करता है।

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **Why this matters:** इंजन को एक बार इनिशियलाइज़ करने से आप लोडेड लैंग्वेज पैक्स को कई फ़ाइलों में पुनः उपयोग कर सकते हैं, जिससे समय और मेमोरी दोनों बचते हैं।

---

## चरण 2: OCR के लिए इमेज लोड – अपने PDF को तैयार करना

PDF एक रॉ इमेज नहीं है, इसलिए लाइब्रेरी आमतौर पर एक हेल्पर प्रदान करती है जो पहला पेज (या सभी पेज) को ऐसी इमेज में बदल देती है जिसे OCR इंजन समझ सके।

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **Tip:** यदि आपका PDF कई पेजों वाला है, तो कई OCR लाइब्रेरियां आपको `page=2` पास करने या `engine.load_image(pdf_path, page=n)` को लूप करने देती हैं। बड़े दस्तावेज़ों के लिए पेजों को बैच में प्रोसेस करने पर विचार करें ताकि मेमोरी स्पाइक से बचा जा सके।

---

## चरण 3: OCR इंजन Python का उपयोग – संरचित टेक्स्ट पहचानना

अब भारी काम होता है। `recognize_structured()` कॉल ब्लॉक्स → लाइन्स → वर्ड्स की एक हायरार्की लौटाता है, प्रत्येक में भाषा, कॉन्फिडेंस, और बाउंडिंग बॉक्स की जानकारी होती है।

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **What you get:**  
> - `structured_result.blocks` – टॉप‑लेवल कंटेनर (अक्सर पैराग्राफ या कॉलम)।  
> - प्रत्येक ब्लॉक में `lines` होते हैं, और प्रत्येक लाइन में `words` होते हैं।  
> - कॉन्फिडेंस स्कोर आपको शंकास्पद परिणामों को फ़िल्टर करने में मदद करते हैं।

---

## चरण 4: परिणामों पर इटरेट करना – ब्लॉक्स, लाइन्स, वर्ड्स तक पहुंचना

नीचे एक कॉम्पैक्ट लूप है जो सबसे उपयोगी जानकारी प्रिंट करता है। इसे JSON, CSV लिखने या डेटाबेस में फीड करने के लिए विस्तारित करने में संकोच न करें।

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### अपेक्षित आउटपुट

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **Why you’ll love this:** हायरार्की इस तरह बनती है जैसे मनुष्य पेज पढ़ते हैं, जिससे बाद में टेबल या कॉलम लेआउट को पुनः बनाना आसान हो जाता है।

---

## चरण 5: एज केस हैंडल करना – लो कॉन्फिडेंस & मल्टी‑पेज PDFs

### लो‑कॉन्फिडेंस वर्ड्स

यदि किसी वर्ड का कॉन्फिडेंस `0.70` से नीचे गिर जाता है, तो आप उसे मैन्युअल रिव्यू के लिए फ़्लैग करना चाहेंगे:

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### सभी पेज प्रोसेस करना

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **Pro tip:** यदि आपका OCR लाइब्रेरी हर बार इमेज को री‑रेंडर करता है, तो मध्यवर्ती इमेज को PNG के रूप में कैश करें—यह बड़े बैचों में सेकंड बचा सकता है।

---

## पूर्ण कार्यशील स्क्रिप्ट

सब कुछ एक साथ जोड़ते हुए, यहाँ एक सिंगल फ़ाइल है जिसे आप तुरंत चला सकते हैं:

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

इसे `extract_pdf_ocr.py` के रूप में सहेजें और चलाएँ:

```bash
python extract_pdf_ocr.py
```

आपको कंसोल में ब्लॉक‑लेवल विवरण प्रिंट होते दिखेंगे, साथ ही कोई भी लो‑कॉन्फिडेंस वार्निंग भी।

---

## निष्कर्ष

हमने अभी-अभी **OCR इंजन Python** का उपयोग करके **PDF से टेक्स्ट निकालने** का एक पूर्ण, प्रोडक्शन‑रेडी तरीका कवर किया। लाइब्रेरी इंस्टॉल करने से लेकर **OCR के लिए इमेज लोड** करने, **OCR के साथ PDF पढ़ने**, और अंत में संरचित आउटपुट पर इटरेट करने तक, अब आपके पास एक पुन: उपयोग योग्य स्क्रिप्ट है जिसे आप किसी भी प्रोजेक्ट में अनुकूलित कर सकते हैं।

आप आगे क्या कर सकते हैं:

- हायरार्की को JSON में एक्सपोर्ट करना ताकि डाउनस्ट्रीम NLP पाइपलाइन में उपयोग हो सके।  
- भाषा डिटेक्शन जोड़ना ताकि OCR मॉडल को ऑन‑द‑फ़्लाई स्विच किया जा सके।  
- `pdf2image` के साथ इंटीग्रेट करना ताकि जटिल लेआउट वाले PDFs को प्री‑प्रोसेस किया जा सके।  

इसे मल्टी‑पेज इनवॉइस बैच पर आज़माएँ, कॉन्फिडेंस थ्रेशोल्ड को ट्यून करें, और देखें कि स्कैन किए हुए PDFs को सर्चेबल, एडिटेबल टेक्स्ट में बदलना कितना तेज़ हो सकता है। यदि कोई समस्या आती है, तो नीचे कमेंट छोड़ें—हैप्पी OCRing!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}