---
category: general
date: 2026-07-05
description: Python OCR का उपयोग करके PDF को टेक्स्ट में बदलें। सीखें कि PDF से टेक्स्ट
  कैसे निकालें, बैच OCR प्रोसेसिंग कैसे करें, और कुछ आसान चरणों में OCR के लिए PDF
  लोड करें।
draft: false
keywords:
- convert pdf to text
- extract text from pdf
- batch ocr processing
- load pdf for ocr
- recognize scanned pdf
language: hi
og_description: PDF को जल्दी टेक्स्ट में बदलें। यह ट्यूटोरियल दिखाता है कि PDF से
  टेक्स्ट कैसे निकालें, बैच OCR प्रोसेसिंग कैसे चलाएँ, और Python का उपयोग करके स्कैन
  किए गए PDF फ़ाइलों को कैसे पहचानें।
og_title: Python OCR के साथ PDF को टेक्स्ट में बदलें – चरण‑दर‑चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  headline: Convert PDF to Text with Python OCR – Complete Guide
  type: TechArticle
- description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  name: Convert PDF to Text with Python OCR – Complete Guide
  steps:
  - name: '**Chunked Loading** – Some libraries let you load a range of pages:'
    text: '**Chunked Loading** – Some libraries let you load a range of pages:'
  - name: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
    text: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
  - name: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
    text: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
  - name: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
    text: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
  - name: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
    text: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Python OCR के साथ PDF को टेक्स्ट में बदलें – पूर्ण गाइड
url: /hi/python-java/general/convert-pdf-to-text-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR के साथ PDF को टेक्स्ट में बदलें – पूर्ण गाइड

क्या आपने कभी सोचा है कि **PDF को टेक्स्ट में बदलें** बिना किसी मेहनत के? शायद आपके पास स्कैन किए हुए अनुबंधों, इनवॉइसों या शोध पत्रों का ढेर है और आपको इंडेक्सिंग या विश्लेषण के लिए साधारण‑टेक्स्ट संस्करण चाहिए। अच्छी खबर यह है कि कुछ ही पंक्तियों के Python कोड से यह काम आसानी से हो सकता है।

इस ट्यूटोरियल में हम एक व्यावहारिक समाधान पर चलेंगे जो न केवल **PDF को टेक्स्ट में बदलें** बल्कि आपको **PDF से टेक्स्ट निकालें**, **बैच OCR प्रोसेसिंग** सेट‑अप करने और सही तरीके से **OCR के लिए PDF लोड** करने का तरीका भी दिखाएगा। अंत तक आपके पास एक तैयार‑स्क्रिप्ट होगी जो एक ही बार में **स्कैन किए हुए PDF** पेजों को **पहचान** सके।

## आप क्या सीखेंगे

- एक Python OCR लाइब्रेरी स्थापित और कॉन्फ़िगर करना (हम उदाहरण के लिए एक सामान्य `ocr` पैकेज का उपयोग करेंगे)।  
- मल्टी‑पेज PDF को लोड करके OCR इंजन को देना।  
- परिणामों को इटररेट करके निकाले गए टेक्स्ट को प्रिंट या सेव करना।  
- बड़े फ़ाइलों, एन्क्रिप्टेड PDFs, और मिश्रित‑भाषा दस्तावेज़ों जैसे सामान्य एज केस को संभालना।  

कोई भारी GUI टूल नहीं, कोई मैन्युअल कॉपी‑पेस्ट नहीं—सिर्फ शुद्ध कोड जो आप CI पाइपलाइन या डेस्कटॉप यूटिलिटी में डाल सकते हैं।

![Python OCR का उपयोग करके PDF को टेक्स्ट में बदलें](https://example.com/images/convert-pdf-to-text.png "Python OCR का उपयोग करके PDF को टेक्स्ट में बदलें")

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास ये हैं:

| आवश्यकता | यह क्यों महत्वपूर्ण है |
|-------------|----------------|
| Python 3.9+ | आधुनिक सिंटैक्स, टाइप हिंट्स, और बेहतर प्रदर्शन। |
| `ocr` लाइब्रेरी (या Tesseract के चारों ओर का रैपर) | उदाहरण में उपयोग किए गए `OcrEngine`, `Language`, और `Image` क्लासेज़ प्रदान करती है। |
| एक मल्टी‑पेज स्कैन किया हुआ PDF (जैसे, `contract.pdf`) | यही वह स्रोत है जिसे आप **OCR के लिए PDF लोड** करेंगे। |
| बेसिक कमांड‑लाइन परिचितता | पैकेज इंस्टॉल करने और स्क्रिप्ट चलाने के लिए। |

यदि आप अंतर्गत Tesseract का उपयोग कर रहे हैं, तो इसे अपने OS पैकेज मैनेजर (`apt-get install tesseract-ocr` Linux पर, `brew install tesseract` macOS पर) से इंस्टॉल करें। फिर Python रैपर जोड़ें:

```bash
pip install ocr  # replace with the actual package name, e.g., pytesseract-wrapper
```

## चरण 1: OCR इंजन बनाएं और पहचान भाषा सेट करें

सबसे पहले, हमें एक OCR इंजन इंस्टेंस चाहिए। भाषा को अंग्रेज़ी पर सेट करना सामान्य डिफ़ॉल्ट है, लेकिन आप बाद में अन्य समर्थित भाषाओं में स्विच कर सकते हैं।

```python
import ocr  # hypothetical import; replace with your actual OCR package

# Initialize the OCR engine
engine = ocr.OcrEngine()

# Choose the language for recognition – ENGLISH works for most contracts
engine.language = ocr.Language.ENGLISH
```

**यह क्यों महत्वपूर्ण है:** इंजन वह दिमाग है जो पिक्सेल डेटा को समझता है। `engine.language` को स्पष्ट रूप से परिभाषित करके आप हर पेज पर भाषा पहचान के ओवरहेड से बचते हैं, जिससे **बैच OCR प्रोसेसिंग** काफी तेज़ हो जाती है।

## चरण 2: OCR के लिए PDF दस्तावेज़ लोड करें

अब हम PDF को मेमोरी में लाते हैं। `ocr.Image.load` मेथड फ़ाइल पाथ ले सकता है और एक ऐसा ऑब्जेक्ट रिटर्न करता है जिसे इंजन समझता है।

```python
# Path to your scanned PDF; adjust as needed
pdf_path = "YOUR_DIRECTORY/contract.pdf"

# Load the PDF – this step **load pdf for OCR**
pdf_document = ocr.Image.load(pdf_path)
```

**प्रो टिप:** यदि आपका PDF पासवर्ड‑प्रोटेक्टेड है, तो अधिकांश लाइब्रेरी आपको `password` आर्ग्यूमेंट पास करने देती हैं। इसे पहले ही हैंडल करने से बाद में “फ़ाइल नहीं खोल सकता” जैसी अस्पष्ट त्रुटियों से बचा जा सकता है।

## चरण 3: सभी पेजों पर OCR चलाएँ – एक कॉल में स्कैन किए हुए PDF को पहचानें

पेज‑बाय‑पेज OCR चलाना धीमा हो सकता है, खासकर बड़े दस्तावेज़ों के लिए। `recognize_multi_page` मेथड आंतरिक रूप से **बैच OCR प्रोसेसिंग** करता है, और संभव हो तो कई थ्रेड्स का उपयोग करता है।

```python
# Execute OCR across every page; returns a list of OcrResult objects
page_results = engine.recognize_multi_page(pdf_document)  # List<OcrResult>
```

**अंदर क्या हो रहा है?** इंजन प्रत्येक पेज को अंतर्निहित OCR इंजन (जैसे Tesseract) को स्ट्रीम करता है, टेक्स्ट इकट्ठा करता है, और उसे `OcrResult` में रैप करता है। यह तरीका I/O ओवरहेड को कम करता है और आपको बाद में **PDF से टेक्स्ट निकालें** का साफ़ तरीका देता है।

## चरण 4: परिणामों को इटररेट करें और पहचाना गया टेक्स्ट आउटपुट करें

अंत में, हम प्रत्येक `OcrResult` पर लूप लगाते हैं और टेक्स्ट प्रिंट करते हैं। आप प्रत्येक पेज को अलग‑अलग `.txt` फ़ाइल में लिख सकते हैं या सभी को एक ही दस्तावेज़ में जोड़ सकते हैं।

```python
for page_number, result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(result.text)
    # Optional: save to a file
    # with open(f"page_{page_number}.txt", "w", encoding="utf-8") as f:
    #     f.write(result.text)
```

**enumerate क्यों उपयोग करें?** `enumerate(..., start=1)` का उपयोग करने से आपको मानव‑पठनीय पेज नंबर मिलता है, जो बाद में मूल PDF के किसी विशेष सेक्शन को रेफ़र करने में सहायक होता है।

### अपेक्षित आउटपुट

3‑पेज के अनुबंध के खिलाफ स्क्रिप्ट चलाने पर यह जैसा आउटपुट मिल सकता है:

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed...
```

यदि किसी पेज में कोई पहचान योग्य टेक्स्ट नहीं है, तो संबंधित `result.text` एक खाली स्ट्रिंग होगा—जो खाली या केवल इमेज‑पेजों को पहचानने में मदद करता है।

## बड़े PDFs और मेमोरी प्रतिबंधों को संभालना

500‑पेज के PDF को प्रोसेस करने से RAM जल्दी ख़त्म हो सकती है अगर आप सब कुछ एक साथ लोड करें। यहाँ दो रणनीतियाँ हैं:

1. **चंक्ड लोडिंग** – कुछ लाइब्रेरी आपको पेज रेंज लोड करने देती हैं:

   ```python
   for start in range(0, total_pages, 50):  # process 50 pages at a time
       chunk = pdf_document.select_pages(start, start + 49)
       chunk_results = engine.recognize_multi_page(chunk)
       # handle chunk_results as before
   ```

2. **डिस्क पर स्ट्रीमिंग** – प्रत्येक पेज का टेक्स्ट सीधे फ़ाइल में लिखें बजाय पूरी लिस्ट को मेमोरी में रखने के।

इन दोनों तकनीकों से आपका **PDF को टेक्स्ट में बदलें** वर्कफ़्लो स्केलेबल रहता है।

## त्रुटियों और एज केसों से निपटना

- **एन्क्रिप्टेड PDFs** – `Image.load` में पासवर्ड पास करें:

  ```python
  pdf_document = ocr.Image.load(pdf_path, password="mySecret")
  ```

- **मिश्रित भाषाएँ** – यदि आप अलग स्क्रिप्ट पहचानते हैं तो पेज‑वाइज़ भाषा बदलें:

  ```python
  if detect_spanish(result.text):
      engine.language = ocr.Language.SPANISH
  ```

- **लो‑रिज़ॉल्यूशन स्कैन** – OCR से पहले `Pillow` जैसी लाइब्रेरी से इमेज का कंट्रास्ट बढ़ाएँ। यह **स्कैन किए हुए PDF को पहचानें** चरण की गुणवत्ता को काफी सुधार सकता है।

## पूर्ण स्क्रिप्ट: एक ही रन में PDF को टेक्स्ट में बदलें

नीचे पूरी, तैयार‑चलाने‑योग्य स्क्रिप्ट है जो सब कुछ जोड़ती है। इसे `pdf_to_text.py` के रूप में सेव करें और `python pdf_to_text.py` चलाएँ।

```python
#!/usr/bin/env python3
"""
convert_pdf_to_text.py

A self‑contained script that demonstrates how to convert PDF to text using
Python OCR. It covers loading the PDF, batch processing, and handling common
edge cases.
"""

import os
import ocr  # Replace with your actual OCR package

def convert_pdf_to_text(pdf_path: str, output_dir: str = "output"):
    """Convert a scanned PDF into plain‑text files, one per page."""
    if not os.path.isfile(pdf_path):
        raise FileNotFoundError(f"PDF not found: {pdf_path}")

    os.makedirs(output_dir, exist_ok=True)

    # Step 1 – create engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – load PDF (supports password argument if needed)
    pdf_document = ocr.Image.load(pdf_path)

    # Step 3 – run batch OCR
    page_results = engine.recognize_multi_page(pdf_document)

    # Step 4 – write each page's text to a file
    for page_number, result in enumerate(page_results, start=1):
        page_text = result.text.strip()
        out_file = os.path.join(output_dir, f"page_{page_number}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

        # Also echo to console for quick sanity check
        print(f"--- Page {page_number} ---")
        print(page_text[:200] + ("…" if len(page_text) > 200 else ""))

if __name__ == "__main__":
    # Example usage – adjust the path to your PDF file
    PDF_PATH = "YOUR_DIRECTORY/contract.pdf"
    convert_pdf_to_text(PDF_PATH)
```

**स्क्रिप्ट चलाने** से एक `output` फ़ोल्डर बन जाएगा जिसमें `page_1.txt`, `page_2.txt` आदि होंगे, जिससे **PDF से टेक्स्ट निकालें** संरचित तरीके से हो सकेगा।

## समाधान का परीक्षण

1. **सैनिटी चेक** – जनरेट की गई `.txt` फ़ाइल खोलें और पहले कुछ लाइनों को मूल दस्तावेज़ के हेडर से मिलाएँ।  
2. **परफ़ॉर्मेंस टेस्ट** – `time` कमांड से 100‑पेज PDF पर स्क्रिप्ट का समय मापें। यदि अपेक्षा से अधिक समय ले रहा है, तो लाइब्रेरी के मल्टी‑थ्रेडिंग फ़्लैग (अक्सर `engine.set_threads(4)`) को सक्षम करने पर विचार करें।  
3. **क्वालिटी एश्योरेंस** – OCR आउटपुट को मैन्युअल टाइप किए गए अंश से डिफ़ टूल से तुलना करें। साफ़ स्कैन के लिए 95 % से अधिक कैरेक्टर एक्यूरेसी लक्ष्य रखें।

## अगले कदम और संबंधित विषय

- **एक्यूरसी बढ़ाएँ**: `engine.dpi = 300` सेट करें या OCR से पहले इमेज प्री‑प्रोसेसिंग (डेस्क्यू, डीनॉइज़) लागू करें।  
- **सर्चेबल PDFs**: `PyPDF2` या `pdfplumber` जैसी लाइब्रेरी का उपयोग करके निकाले गए टेक्स्ट को मूल PDF में एम्बेड करें, जिससे वह सर्चेबल बन जाए।  
- **नेचुरल लैंग्वेज प्रोसेसिंग**: निकाले गए टेक्स्ट को spaCy या NLTK में फीड करके एंटिटी एक्सट्रैक्शन, सेंटिमेंट एनालिसिस, या कीवर्ड टैगिंग करें।  
- **ऑटोमेशन पाइपलाइन**: इस स्क्रिप्ट को `watchdog` के साथ जोड़ें ताकि किसी फ़ोल्डर में नया फ़ाइल आने पर स्वचालित रूप से **PDF को टेक्स्ट में बदलें**।

इन पैटर्न को महारत हासिल करके, आप

## आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर कर सकें।

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}