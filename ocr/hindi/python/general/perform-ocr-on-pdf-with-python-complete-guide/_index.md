---
category: general
date: 2026-06-25
description: Python का उपयोग करके PDF पर OCR करें—जानें कि OCR के लिए PDF कैसे लोड
  करें, PDF पृष्ठों से टेक्स्ट निकालें, और पहचाने गए टेक्स्ट का प्रभावी रूप से पूर्वावलोकन
  करें।
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: hi
og_description: Python में PDF पर OCR करें। यह गाइड दिखाता है कि OCR के लिए PDF कैसे
  लोड करें, PDF पृष्ठों से टेक्स्ट निकालें, और पहचाने गए टेक्स्ट का शीघ्र पूर्वावलोकन
  करें।
og_title: Python के साथ PDF पर OCR करें – चरण‑दर‑चरण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Python के साथ PDF पर OCR करें – पूर्ण मार्गदर्शिका
url: /hi/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF पर OCR करें – पूर्ण गाइड

क्या आपको **PDF पर OCR करने** की ज़रूरत पड़ी है लेकिन शुरू कहाँ से करें, समझ नहीं आया? शायद आपके पास स्कैन किए हुए अनुबंधों का ढेर है, या एक बड़ा हैंडबुक है जो आपके सामान्य टेक्स्ट‑एक्सट्रैक्टर से नहीं निकल रहा। संक्षेप में, आप **PDF को OCR के लिए लोड** करना चाहते हैं, टेक्स्ट निकालना चाहते हैं, और तेज़ प्रीव्यू देखना चाहते हैं—बिना अपनी मशीन की मेमोरी को ख़त्म किए।

ख़ैर, आप सही जगह पर हैं। इस ट्यूटोरियल में हम एक पूरी‑फ़ंक्शनल Python स्क्रिप्ट के माध्यम से **PDF पेजों से टेक्स्ट निकालना**, **पहचाने गए टेक्स्ट का प्रीव्यू** दिखाना, और **बड़े PDF पर OCR** करने की क्लासिक समस्या को कुशलता से हल करना सीखेंगे।

अंत तक आपके पास चलाने योग्य प्रोग्राम, प्रत्येक कॉन्फ़िगरेशन विकल्प की स्पष्ट समझ, और कुछ टिप्स होंगी जो नए उपयोगकर्ताओं को अक्सर पड़ने वाली समस्याओं से बचाएगी।

---

## आप क्या सीखेंगे

- `aocr` लाइब्रेरी का उपयोग करके **PDF को OCR के लिए लोड** करने का तरीका।
- **PDF पेजों पर एक‑एक करके OCR** करने के सटीक चरण।
- मेमोरी उपयोग को नियंत्रित रखते हुए **PDF पेजों से टेक्स्ट निकालने** के तरीके।
- **पहचाने गए टेक्स्ट का प्रीव्यू** कैसे दिखाएँ ताकि परिणामों की जाँच हो सके।
- **बड़े PDF** को RAM ख़त्म किए बिना संभालने की रणनीतियाँ।

> **टिप:** यह गाइड मानता है कि आपके पास Python 3.9+ इंस्टॉल है और आप वर्चुअल एनवायरनमेंट से परिचित हैं। यदि आप Python में नए हैं, तो पहले एक virtualenv सेट‑अप करें—यह बाद में सिरदर्द बचाता है।

---

## पूर्वापेक्षाएँ

| आवश्यकता | क्यों महत्वपूर्ण है |
|----------|-------------------|
| `aocr` Python पैकेज (या कोई भी संगत OCR इंजन) | स्क्रिप्ट में उपयोग की जाने वाली `OcrEngine` क्लास प्रदान करता है। |
| `pip` और एक वर्चुअल एनवायरनमेंट | डिपेंडेंसीज़ को सिस्टम Python से अलग रखता है। |
| अस्थायी इमेज एक्सट्रैक्ट्स के लिए पर्याप्त डिस्क स्पेस | कुछ OCR इंजन पेज इमेज को डिस्क पर लिखते हैं प्रोसेस करने से पहले। |
| वैकल्पिक: `tqdm` प्रोग्रेस बार के लिए | **बड़े PDF पर OCR** करने के काम में UX सुधारता है। |

आवश्यक पैकेज इस प्रकार इंस्टॉल करें:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

यदि आपका PDF पासवर्ड‑प्रोटेक्टेड है, तो बाद में पासवर्ड देना होगा—“Edge Cases” सेक्शन देखें।

---

## चरण 1: OCR इंजन सेट‑अप करना

सबसे पहले, हमें एक OCR इंजन इंस्टेंस चाहिए। इसे ऐसे समझें जैसे वह दिमाग जो प्रत्येक पेज की इमेज पढ़ेगा और साधारण टेक्स्ट आउटपुट देगा।

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **`max_memory_mb` क्यों सेट करें?**  
> OCR इंजन अक्सर पेज इमेज को RAM में कैश करते हैं। मेमोरी को सीमित करके आप 500‑पेज के अनुबंध पर स्क्रिप्ट के क्रैश होने से बचते हैं।

---

## चरण 2: PDF को OCR के लिए लोड करें और सेटिंग्स कॉन्फ़िगर करें

अब हम वास्तव में **PDF को OCR के लिए लोड** करेंगे। पाथ एब्सोल्यूट या रिलेटिव हो सकता है; बस यह सुनिश्चित करें कि फ़ाइल मौजूद है।

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

यदि PDF एन्क्रिप्टेड है, तो `engine.load_pdf` आमतौर पर एक एक्सेप्शन थ्रो करेगा। ऐसे में आप `engine.load_pdf(pdf_path, password="secret")` कॉल कर सकते हैं—बाद में इस पर और चर्चा करेंगे।

---

## चरण 3: PDF पेजों से टेक्स्ट निकालें – मुख्य लूप

यहाँ हम **PDF पर OCR** पेज‑दर‑पेज करेंगे। साथ ही **पहचाने गए टेक्स्ट का प्रीव्यू** पहले कुछ सौ अक्षरों का दिखाएंगे ताकि आप सत्यापित कर सकें कि सब ठीक काम कर रहा है।

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **प्रो टिप:** `tqdm` प्रोग्रेस बार एक विज़ुअल संकेत देता है, विशेष रूप से **बड़े PDF पर OCR** करने वाले दस्तावेज़ों के लिए जो प्रोसेस करने में मिनट लगाते हैं।

---

## चरण 4: सब कुछ एक साथ – रन‑तैयार स्क्रिप्ट

नीचे पूरा, चलाने योग्य उदाहरण दिया गया है। इसे `pdf_ocr.py` के रूप में सेव करें और `python pdf_ocr.py path/to/your/file.pdf` कमांड से चलाएँ।

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### अपेक्षित आउटपुट (उद्धरण)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

आप प्रत्येक पेज का छोटा प्रीव्यू देखेंगे, उसके बाद एक अंतिम पुष्टि कि संयोजित टेक्स्ट फ़ाइल लिखी गई है।

---

## एज केस और व्यावहारिक टिप्स

| स्थिति | क्या करें |
|--------|-----------|
| **एन्क्रिप्टेड PDF** | पासवर्ड पास करें: `engine.load_pdf(pdf_path, password="mySecret")`। |
| **बहुत बड़ा PDF (> 1000 पेज)** | `max_memory_mb` को सावधानी से बढ़ाएँ, या चंक्स में प्रोसेस करें (जैसे 200 पेज़ एक बार)। |
| **मिक्स्ड कंटेंट (प्रिंटेड + हैंडराइटन)** | यदि लाइब्रेरी सपोर्ट करती है तो `engine.recognition_mode` को `aocr.RecognitionMode.MIXED` पर सेट करें। |
| **फ़ॉन्ट्स गायब या स्कैन क्वालिटी ख़राब** | `recognize()` कॉल करने से पहले Pillow जैसी इमेज‑एन्हांसमेंट लाइब्रेरी से पेज प्री‑प्रोसेस करें। |
| **आउट‑ऑफ़‑मेमोरी क्रैश** | `preview_len` घटाएँ या प्रत्येक पेज का टेक्स्ट सीधे डिस्क पर लिखें, लिस्ट में सभी को रखने के बजाय। |

---

## बड़े PDF पर OCR कुशलता से कैसे करें – उन्नत रणनीतियाँ

जब आप **बड़े PDF पर OCR** कर रहे हों, तो गति और स्थिरता दोनों महत्वपूर्ण हो जाते हैं। यहाँ कुछ ट्रिक्स हैं जिन्हें आप स्क्रिप्ट में जोड़ सकते हैं:

1. **पेज‑दर‑पेज पैरललाइज़** – यदि OCR इंजन थ्रेड‑सेफ़ है तो `concurrent.futures.ThreadPoolExecutor` का उपयोग करें।
2. **इंटरमीडिएट इमेज कैश करें** – कुछ इंजन आपको रास्टराइज़्ड पेज SSD पर स्टोर करने देते हैं, जिससे री‑रन पर CPU लोड काफी घट जाता है।
3. **बैच में आउटपुट लिखें** – Python लिस्ट में अपेंड करने के बजाय, आउटपुट फ़ाइल को एक बार खोलें और प्रत्येक पेज का टेक्स्ट तैयार होते ही लिखें।
4. **DPI समायोजित करें** – रास्टराइज़ेशन के दौरान DPI कम करने से मेमोरी घटती है लेकिन सटीकता पर असर पड़ सकता है; आमतौर पर 200‑300 DPI एक अच्छा संतुलन है।

नीचे एक छोटा स्निपेट है जो OCR स्टेप को पैरललाइज़ करने का तरीका दिखाता है (वैकल्पिक, उपयोग करने के लिए अनकमेंट करें):

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

ध्यान रखें: पैरललिज़्म CPU उपयोग बढ़ा सकता है, इसलिए लंबी रन के दौरान सिस्टम तापमान मॉनिटर करें।

---

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या मैं इस स्क्रिप्ट को Tesseract जैसी अन्य OCR लाइब्रेरी के साथ उपयोग कर सकता हूँ?**  
**उत्तर:** बिल्कुल। `aocr` कॉल्स को `pytesseract.image_to` आदि से बदल दें और बाकी लॉजिक समान रहेगा।

---

## आगे क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों से निकटता से जुड़े हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकें।

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}