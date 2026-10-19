---
category: general
date: 2026-03-18
description: इमेज पर OCR चलाएँ ताकि PNG से टेक्स्ट निकाला जा सके और सर्चेबल PDF बनाया
  जा सके। सीखें कि कैसे टेक्स्ट इमेज को पहचानें और मिनटों में PNG को PDF में बदलें।
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: hi
og_description: PNG से टेक्स्ट निकालने के लिए इमेज पर OCR चलाएँ, टेक्स्ट इमेज को पहचानें,
  और एक सर्चेबल PDF बनाएं। इस चरण‑दर‑चरण गाइड का पालन करें।
og_title: इमेज पर OCR चलाएँ – PNG से तेज़ी से टेक्स्ट निकालें
tags:
- OCR
- Python
- Image Processing
title: इमेज पर OCR चलाएँ – PNG से तेज़ी से टेक्स्ट निकालें
url: /hi/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on Image – Extract Text from PNG Quickly

क्या आपको कभी **इमेज पर OCR चलाना** पड़ा लेकिन शुरुआत नहीं पता थी? शायद आपके पास `article.png` नाम की स्कैन की हुई लेख है और आप सिर्फ सादा टेक्स्ट चाहते हैं, या आप आर्काइविंग के लिए सर्चेबल PDF चाहिए। चाहे जो भी हो, आप सही जगह पर हैं। इस ट्यूटोरियल में हम PNG से टेक्स्ट निकालने, टेक्स्ट इमेज को पहचानने, और यहाँ तक कि उस PNG को सर्चेबल PDF में बदलने की पूरी प्रक्रिया को कुछ ही लाइनों के कोड से दिखाएंगे।

> **What you’ll get:** एक पूर्ण, रन करने योग्य स्क्रिप्ट जो PNG लोड करती है, OCR चलाती है, hOCR आउटपुट सेव करती है, और वैकल्पिक रूप से सर्चेबल PDF बनाती है। कोई मिसिंग इम्पोर्ट नहीं, कोई “see the docs” डेड‑एंड नहीं—बस एक सेल्फ‑कंटेन्ड सॉल्यूशन जिसे आप आज ही अपने प्रोजेक्ट में डाल सकते हैं।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास हैं:

- **Python 3.8+** (यहाँ इस्तेमाल किया गया सिंटैक्स किसी भी हालिया वर्ज़न पर काम करता है)
- वह **`ocr_engine`** लाइब्रेरी जो आप उपयोग कर रहे हैं (उदाहरण में `OcrEngine` क्लास मान ली गई है; आवश्यकता अनुसार Tesseract, EasyOCR आदि से बदलें)
- एक PNG इमेज जिसे आप प्रोसेस करना चाहते हैं (जैसे `article.png` को किसी ऐसे फ़ोल्डर में रखें जिसे आप रेफ़र कर सकें)
- आउटपुट डायरेक्टरी में लिखने की अनुमति

यदि आप बैकएंड में Tesseract का उपयोग कर रहे हैं, तो इसे इस तरह इंस्टॉल करें:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

और फिर Python रैपर इंस्टॉल करें:

```bash
pip install pytesseract Pillow
```

*Pro tip:* अपनी OCR लाइब्रेरी को अपडेटेड रखें—नए लैंग्वेज पैक्स और परफ़ॉर्मेंस ट्यूनिंग अक्सर आते रहते हैं।

## Run OCR on Image – Step‑by‑Step Guide

नीचे **पूरा स्क्रिप्ट** दिया गया है। इसे `run_ocr.py` नाम की फ़ाइल में कॉपी‑पेस्ट करके `python run_ocr.py` कमांड से चलाएँ।

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### What the script does, in plain English

1. **Instantiate** the OCR engine so you can control its settings.  
2. **Load** the PNG file (`article.png`). The script aborts early if the file isn’t there—no mysterious `NoneType` errors later.  
3. **Select** `hocr` as the export format. This format keeps the original layout, which is essential for later converting the image into a searchable PDF.  
4. **Run** the recognition engine; the heavy lifting happens here.  
5. **Write** the hOCR XML to `article.hocr`. You now have a machine‑readable representation of the text and its coordinates.  
6. *(Optional)* Switch to `"pdf"` and generate a searchable PDF in one extra step.

**Expected output** एक UTF‑8‑encoded `.hocr` फ़ाइल है जो कुछ इस तरह दिखती है (संक्षिप्त रूप में):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

यदि आप PDF सेक्शन को अनकमेंट करेंगे, तो आपको `article_searchable.pdf` भी मिलेगा, जिसे आप किसी भी PDF व्यूअर में खोल सकते हैं और **Ctrl + F** सर्च बॉक्स से तुरंत शब्द खोज सकते हैं।

![Run OCR on image example output](example.png "Run OCR on image – hOCR and PDF results")

## How to Extract Text from PNG Using OcrEngine

अगर आपको सिर्फ रॉ टेक्स्ट चाहिए (कोई लेआउट नहीं, कोई PDF नहीं), तो आप hOCR स्टेप को पूरी तरह स्किप कर सकते हैं:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Why choose plain text?* यह हल्का होता है, इंडेक्सिंग के लिए परफ़ेक्ट, और डाउनस्ट्रीम NLP पाइपलाइन के साथ बेहतरीन काम करता है।

## Recognize Text Image and Generate Searchable PDF

सर्चेबल PDF बनाना दो‑स्टेप प्रोसेस है:

1. **Run OCR** with `hocr` (जैसा ऊपर किया) ताकि लेआउट जानकारी मिल सके।  
2. **Combine** the original PNG with the hOCR into a PDF using the engine’s PDF exporter.

अधिकांश आधुनिक OCR लाइब्रेरी (Tesseract, ABBYY, Google Vision) एक `pdf` एक्सपोर्ट प्रदान करती हैं जो यही करती है। मुख्य स्क्रिप्ट के *Optional* ब्लॉक में दिखाया गया स्निपेट इस पैटर्न को दर्शाता है। अगर आपकी लाइब्रेरी में बिल्ट‑इन PDF एक्सपोर्टर नहीं है, तो आप **`pdf2image`** + **`reportlab`** का उपयोग करके इमेज और hOCR को जोड़ सकते हैं—बस बताइए, मैं एक छोटा अतिरिक्त उदाहरण शेयर कर दूँगा।

## Convert PNG to PDF with OCR Output

कभी‑कभी आपको सिर्फ **सादा PDF** चाहिए जिसमें इमेज हो (कोई सर्चेबल लेयर नहीं)। यह और भी आसान है:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

यदि आपको सर्चेबल वर्ज़न चाहिए तो इसे OCR स्टेप के साथ मिलाएँ, या आर्काइविंग के लिए इसे एक सटीक विज़ुअल रेप्लिका के रूप में रखें।

## Common Pitfalls & Tips

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Blurry or low‑resolution PNG** | OCR accuracy drops dramatically below ~300 DPI. | `Image.resize((width*2, height*2), Image.LANCZOS)` से अपस्केल करें, फिर इंजन को दें। |
| **Wrong language** | Engine defaults to English; non‑English characters become garbled. | `ocr_engine.setLanguage('deu')` (या उपयुक्त ISO कोड) को `recognize()` से पहले कॉल करें। |
| **Missing hOCR output** | Some engines default to plain text when `setExportFormat` isn’t called. | सुनिश्चित करें कि `setExportFormat("hocr")` **recognize()** से **पहले** चलाया गया है। |
| **File permission errors** | Trying to write to a read‑only folder. | प्रोजेक्ट के अंदर कोई पाथ इस्तेमाल करें या पहले `os.makedirs(..., exist_ok=True)` चलाएँ। |
| **Large PDFs cause memory spikes** | PDF exporter keeps the whole image in RAM. | पेजेज़ को चंक्स में प्रोसेस करें या स्ट्रीमिंग PDF राइटर का उपयोग करें। |

*Pro tip:* बड़े बैच से पहले हमेशा एक छोटी सैंपल इमेज पर टेस्ट करें। इससे घंटों की डिबगिंग बचती है।

## Wrap‑Up

अब आप जानते हैं **इमेज पर OCR कैसे चलाएँ**, **PNG से टेक्स्ट कैसे निकालें**, **टेक्स्ट इमेज को पहचानें** downstream टास्क के लिए, **सर्चेबल PDF कैसे बनाएं**, और **PNG को PDF में कैसे बदलें** जब आपको सिर्फ एक साधा आर्काइव चाहिए। दिया गया स्क्रिप्ट एक पूर्ण, कॉपी‑एंड‑पेस्ट समाधान है जो तुरंत काम करता है, और वैकल्पिक सेक्शन आपको आउटपुट को अपनी वर्कफ़्लो के अनुसार कस्टमाइज़ करने की सुविधा देते हैं।

### What’s next?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}