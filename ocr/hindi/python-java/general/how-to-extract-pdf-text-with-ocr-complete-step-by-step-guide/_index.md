---
category: general
date: 2026-03-26
description: OCR का उपयोग करके PDF टेक्स्ट कैसे निकालें। सीखें कि PDF को इमेज के रूप
  में लोड करें, PDF टेक्स्ट को पहचानें और एक सरल Python उदाहरण के साथ PDF से टेक्स्ट
  निकालें।
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: hi
og_description: OCR का उपयोग करके PDF टेक्स्ट कैसे निकालें। यह गाइड आपको दिखाता है
  कि PDF को इमेज के रूप में कैसे लोड करें, PDF टेक्स्ट को कैसे पहचानें और Python में
  PDF से टेक्स्ट कैसे निकालें।
og_title: OCR के साथ PDF टेक्स्ट निकालने का तरीका – पूर्ण ट्यूटोरियल
tags:
- OCR
- Python
- PDF processing
title: OCR के साथ PDF टेक्स्ट कैसे निकालें – पूर्ण चरण-दर-चरण गाइड
url: /hi/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF टेक्स्ट को OCR के साथ निकालें – पूर्ण चरण‑दर‑चरण गाइड

क्या आपने कभी सोचा है **PDF को कैसे निकालें** जब वह वास्तव में केवल स्कैन की गई इमेजेज़ हों? आप अकेले नहीं हैं—कई डेवलपर्स को यह समस्या आती है जब उन्हें सर्चेबल कंटेंट चाहिए लेकिन उनके पास केवल इमेज‑ओनली PDFs होते हैं। अच्छी खबर? कुछ लाइनों का कोड और एक मजबूत OCR लाइब्रेरी उन पिक्चर‑PDFs को तुरंत प्लेन टेक्स्ट में बदल सकती है।  

इस ट्यूटोरियल में हम **OCR का उपयोग कैसे करें** यह दिखाएंगे: PDF को इमेज के रूप में लोड करना, PDF टेक्स्ट को पहचानना, और अंत में **PDF से टेक्स्ट निकालें** किसी भी लंबाई के दस्तावेज़ से। अंत तक आपके पास एक रन करने योग्य स्क्रिप्ट, प्रत्येक चरण की स्पष्ट व्याख्या, और सामान्य समस्याओं से बचने के लिए कुछ टिप्स होंगी।

## आपको क्या चाहिए

- Python 3.9 या नया (कोड 3.10+ पर भी काम करता है)  
- `ocr` Python पैकेज (या कोई भी संगत OCR लाइब्रेरी जो `OcrEngine`, `OcrEngineMode`, और `Imaging.Image` प्रदान करती हो)  
- एक मल्टी‑पेज PDF जिसे आप प्रोसेस करना चाहते हैं (डेमो के लिए इसे `multi_page.pdf` कहेंगे)  
- वर्चुअल एनवायरनमेंट्स की बुनियादी जानकारी (वैकल्पिक लेकिन अनुशंसित)

> **Pro tip:** यदि आप Windows पर हैं, तो Anaconda Prompt का उपयोग करें; macOS/Linux पर, बस `python -m venv venv && source venv/bin/activate` चलाएँ।

## चरण 1: OCR लाइब्रेरी इंस्टॉल करें

सबसे पहले, OCR पैकेज को PyPI से प्राप्त करें। नीचे का उदाहरण एक काल्पनिक `ocr` पैकेज का उपयोग करता है जो कोड स्निपेट में दिखाए गए API को दर्शाता है, लेकिन अधिकांश वास्तविक लाइब्रेरीज़ (जैसे `pytesseract` + `pdf2image`) समान पैटर्न फॉलो करती हैं।

```bash
pip install ocr
```

यदि आप कोई अलग इंजन उपयोग कर रहे हैं, तो `ocr` को उपयुक्त नाम से बदलें (उदा., `pip install pytesseract pdf2image`)।

## चरण 2: OCR इंजन को इनिशियलाइज़ करें

इंजन इंस्टेंस बनाना **PDF को कैसे निकालें** टेक्स्ट का आधार है। इंजन को प्रत्येक PDF पेज के पिक्सेल को समझने वाला दिमाग समझें।

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **यह क्यों महत्वपूर्ण है:** `set_engine_mode` आपको स्पीड और एक्यूरेसी के बीच संतुलन देता है। `DEFAULT` एक संतुलित विकल्प है; यदि आपको अधिक प्रिसीजन चाहिए, तो `HIGH_ACCURACY` पर स्विच करें (यदि लाइब्रेरी इसे सपोर्ट करती है)।

## चरण 3: PDF को इमेज ऑब्जेक्ट के रूप में लोड करें

OCR इमेजेज़ पर काम करता है, PDF कंटेनर पर नहीं, इसलिए हमें पहले PDF को इमेज रिप्रेजेंटेशन में बदलना होगा। `Imaging.Image.load` मेथड मल्टी‑पेज PDFs को ऑटोमैटिकली हैंडल करता है।

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **एज केस:** कुछ लाइब्रेरीज़ केवल सिंगल‑पेज इमेज़ स्वीकार करती हैं। ऐसे में आपको `pdf2image.convert_from_path` का उपयोग करके प्रत्येक पेज को लूप करना पड़ेगा। हमारा `load` कॉल इस प्रक्रिया को एब्स्ट्रैक्ट करता है, जिससे **load pdf as image** एक‑लाइनर बन जाता है।

## चरण 4: सभी पेजों पर टेक्स्ट पहचानें

अब **recognize PDF text** का मुख्य भाग आता है। इंजन हर पेज को स्कैन करता है और परिणाम ऑब्जेक्ट्स की एक लिस्ट रिटर्न करता है—प्रति पेज एक।

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

प्रत्येक `page_result` में `get_text()` (प्लेन टेक्स्ट) और `get_confidence()` (वैकल्पिक क्वालिटी मेट्रिक) जैसे मेथड्स होते हैं।  

> **टिप:** यदि आपको केवल पहला पेज चाहिए, तो मल्टी‑पेज हेल्पर की बजाय `recognize(pdf_image[0])` कॉल करें।

## चरण 5: परिणामों पर इटरेट करें और निकाला हुआ टेक्स्ट आउटपुट करें

अंत में, हम परिणामों के ऊपर लूप लगाते हैं और प्रत्येक पेज का टेक्स्ट प्रिंट करते हैं। यह **extract text from PDF** वर्कफ़्लो को पूरा करता है।

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### अपेक्षित आउटपुट

यदि `multi_page.pdf` में तीन पेज हैं जिनमें क्रमशः “Hello”, “World”, और “Python” शब्द हैं, तो आपको मिलेगा:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

बस—आपका PDF अब पूरी तरह सर्चेबल है और टेक्स्ट डाउनस्ट्रीम प्रोसेसिंग (इंडेक्सिंग, सेंटिमेंट एनालिसिस, आदि) के लिए तैयार है।

## चरण 6: सामान्य समस्याओं का समाधान

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Blank output** | PDF पेज कम DPI पर स्कैन किए गए हैं, जिससे अक्षर अस्पष्ट होते हैं। | OCR से पहले इमेज को अपस्केल करें: `pdf_image = pdf_image.resize(300)` (300 DPI एक अच्छा स्पॉट है)। |
| **Garbage characters** | गैर‑लैटिन अल्फाबेट्स को भाषा पैक्स चाहिए। | उपयुक्त भाषा मॉडल लोड करें: `ocr_engine.load_language('spa')` स्पेनिश के लिए, आदि। |
| **Memory blow‑up on huge PDFs** | सभी पेज एक साथ लोड करने से RAM भर जाता है। | पेजों को बैच में प्रोसेस करें: `for img in pdf_image.split(batch=10): …` (प्स्यूडो‑कोड)। |
| **Slow performance** | बड़े दस्तावेज़ पर `DEFAULT` मोड धीमा हो सकता है। | `FAST` मोड पर स्विच करें या `concurrent.futures` से OCR को पैरलल चलाएँ। |

## बोनस: निकाले हुए टेक्स्ट को फ़ाइल में सेव करें

अधिकांश वास्तविक‑दुनिया पाइपलाइन को टेक्स्ट को स्थायी रूप से रखना पड़ता है। यहाँ एक छोटा हेल्पर है जो सब कुछ `output.txt` में लिखता है।

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

अब आप `output.txt` को सर्च इंजन, डेटाबेस, या किसी भी NLP मॉडल में फीड कर सकते हैं।

## सब कुछ एक साथ – पूर्ण स्क्रिप्ट

नीचे पूरा, तैयार‑टू‑रन प्रोग्राम दिया गया है। कॉपी‑पेस्ट करें, फ़ाइल पाथ्स को एडजस्ट करें, और आप तैयार हैं।

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

इसे चलाएँ:

```bash
python extract_pdf_ocr.py
```

आपको प्रत्येक पेज की सामग्री कंसोल में प्रिंट होते देखनी चाहिए, उसके बाद एक पुष्टि संदेश कि फ़ाइल `extracted_text.txt` बन गई है।

## निष्कर्ष

हमने **PDF को कैसे निकालें** इमेज‑ओनली दस्तावेज़ों से OCR इंजन का उपयोग करके, लाइब्रेरी इंस्टॉल करने से लेकर मल्टी‑पेज परिणामों को हैंडल करने और आउटपुट सेव करने तक, सभी चरणों को कवर किया। अब आप जानते हैं **OCR का उपयोग कैसे करें**, **PDF को इमेज के रूप में लोड करें**, और **PDF टेक्स्ट को पहचानें** भरोसेमंद तरीके से।  

अगले कदम? डिफ़ॉल्ट इंजन मोड को हाई‑एक्यूरेसी सेटिंग में बदलें, मल्टी‑लैंग्वेज PDFs के लिए भाषा पैक्स आज़माएँ, या निकाले हुए टेक्स्ट को Elasticsearch जैसे फुल‑टेक्स्ट सर्च इंडेक्स में पाइप करें। एक बार जब आप PDF फ़ाइलों से टेक्स्ट निकालने की बुनियादें समझ लेते हैं, तो संभावनाएँ असीमित हैं।

---

![how to extract pdf example](images/ocr_flowchart.png){alt="how to extract pdf workflow diagram"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}