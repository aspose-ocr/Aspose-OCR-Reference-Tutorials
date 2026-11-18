---
category: general
date: 2026-06-19
description: Python OCR का उपयोग करके छवि से खोज योग्य PDF बनाएं। OCR को PDF में बदलना,
  छवि से टेक्स्ट निकालना, और छवि पर तेज़ी से OCR करना सीखें।
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: hi
og_description: Python OCR के साथ छवि से खोज योग्य PDF बनाएं। यह गाइड दिखाता है कि
  OCR को PDF में कैसे बदलें, छवि से टेक्स्ट निकालें, और छवि पर OCR कैसे करें।
og_title: Python में सर्चेबल PDF बनाएं – पूर्ण प्रोग्रामिंग मार्गदर्शन
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Python में खोज योग्य PDF बनाएं – पूर्ण चरण‑दर‑चरण मार्गदर्शिका
url: /hi/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में खोज योग्य PDF बनाएं – पूर्ण चरण‑दर‑चरण गाइड

क्या आपको कभी स्कैन किए गए रसीद से **searchable PDF** बनाने की ज़रूरत पड़ी, लेकिन शुरुआत नहीं पता थी? आप अकेले नहीं हैं—कई डेवलपर्स को वही समस्या आती है जब वे पहली बार टेक्स्ट की तस्वीर को ऐसे PDF में बदलने की कोशिश करते हैं जिसे आप वास्तव में खोज सकें।  

इस ट्यूटोरियल में हम एक व्यावहारिक समाधान पर चलेंगे जो आपको **perform OCR on image** करने, उस OCR परिणाम को **searchable PDF** में बदलने, और यदि आपको आगे की प्रोसेसिंग के लिए कच्चा टेक्स्ट चाहिए तो उसे निकालने की सुविधा देता है। कोई फालतू बात नहीं, सिर्फ एक कार्यशील उदाहरण जिसे आप आज ही अपने प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं।

## आप क्या सीखेंगे

- Python में एक हल्का OCR इंजन सेट अप करना  
- **convert OCR to PDF** करने के सटीक चरण और उसे खोज योग्य दस्तावेज़ के रूप में सहेजना  
- डाउनस्ट्रीम विश्लेषण के लिए **extract text from image** करने के तरीके  
- इमेज ओरिएंटेशन और बड़े फ़ाइलों जैसी सामान्य समस्याओं को संभालने के टिप्स  
- एक पूर्ण, चलाने योग्य स्क्रिप्ट जिसे आप अपने उपयोग‑केस के अनुसार अनुकूलित कर सकते हैं  

### पूर्वापेक्षाएँ

- आपके मशीन पर Python 3.8+ स्थापित हो  
- pip और वर्चुअल एन्वायरनमेंट्स की बुनियादी जानकारी (वैकल्पिक लेकिन अनुशंसित)  
- एक इमेज फ़ाइल (PNG, JPEG, आदि) जिसमें स्पष्ट, मशीन‑पठनीय टेक्स्ट हो  

यदि आपके पास ये सब है, तो चलिए शुरू करते हैं।

## चरण 1: आवश्यक लाइब्रेरी स्थापित करें

जो कोड स्निपेट आपने पहले देखा था वह एक काल्पनिक `ocr` पैकेज का उपयोग करता है, लेकिन वही विचार वास्तविक लाइब्रेरीज़ जैसे **EasyOCR**, **pytesseract**, या **pdfminer.six** पर भी लागू होते हैं। इस गाइड के लिए हम **EasyOCR** का उपयोग करेंगे क्योंकि यह पूरी तरह Python में लिखा है, कई भाषाओं को सपोर्ट करता है, और एक सहायक हेल्पर के माध्यम से उपयोगी PDF कन्वर्ज़न मेथड प्रदान करता है।

```bash
pip install easyocr pillow
```

> **Pro tip:** एक वर्चुअल एन्वायरनमेंट (`python -m venv venv && source venv/bin/activate`) के अंदर इंस्टॉल करें ताकि आपकी डिपेंडेंसीज़ साफ़ रहें।

## चरण 2: OCR इंजन को इनिशियलाइज़ करें – इमेज पर OCR करें

अब लाइब्रेरी तैयार है, हम एक OCR इंजन बनाते हैं और उसे अंग्रेज़ी टेक्स्ट के साथ काम करने के लिए बताते हैं। यही वह पहला स्थान है जहाँ हम **perform OCR on image** करते हैं।

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

हमें एक समर्पित रीडर ऑब्जेक्ट की आवश्यकता क्यों है? EasyOCR भाषा मॉडल्स को प्री‑लोड करता है, इसलिए कई इमेज के लिए वही `reader` पुनः उपयोग करना हर बार पुनः‑इनिशियलाइज़ करने की तुलना में बहुत अधिक कुशल होता है।

## चरण 3: इमेज लोड करें – इमेज से टेक्स्ट निकालें

आइए तस्वीर को मेमोरी में लाएँ। यह चरण वह है जहाँ हम बाद में **extract text from image** करेंगे, लेकिन अभी हम केवल इसे लोड करते हैं।

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

यदि आपकी इमेज उल्टी या तिरछी है, तो OCR इंजन को फ़ीड करने से पहले Pillow के `rotate` या `transpose` मेथड्स का उपयोग करने पर विचार करें। एक त्वरित विज़ुअल चेक बाद में कई घंटे की डिबगिंग बचा सकता है।

## चरण 4: OCR इंजन चलाएँ और परिणाम कैप्चर करें

यह प्रक्रिया का मुख्य भाग है—इमेज को OCR इंजन को भेजना और संरचित डेटा वापस प्राप्त करना।

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

`detail=1` फ़्लैग हमें बाउंडिंग बॉक्स देता है, जिसकी हमें बाद में **convert OCR to PDF** के समय आवश्यकता होगी। यदि आप केवल कच्ची स्ट्रिंग्स में रुचि रखते हैं, तो `detail=0` सेट करें।

## चरण 5: OCR परिणाम को खोज योग्य PDF में बदलें – OCR को PDF में बदलें

EasyOCR सीधे PDF राइटर प्रदान नहीं करता, लेकिन हम Pillow और `reportlab` लाइब्रेरी का उपयोग करके स्वयं PDF को जोड़ सकते हैं। ट्यूटोरियल को हल्का रखने के लिए, हम `fpdf2` का उपयोग करेंगे, जो मूल इमेज को एम्बेड करने और अदृश्य टेक्स्ट ओवरले करने की सुविधा देता है।

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

क्या हुआ? हमने स्कैन की गई इमेज को दृश्यमान लेयर के रूप में रखा, फिर पहचाने गए शब्दों को सफ़ेद टेक्स्ट के साथ ऊपर लिखा जो सफ़ेद बैकग्राउंड में मिल जाता है। सर्च टूल अभी भी छिपी हुई लेयर को पढ़ते हैं, इसलिए PDF **searchable** बन जाता है बिना दृश्य रूप बदलें।

## चरण 6: PDF बाइट्स सहेजें – इमेज को PDF में बदलें

यदि आप PDF को मेमोरी में संभालना पसंद करते हैं (जैसे API के माध्यम से भेजना), तो आप सीधे डिस्क पर लिखने के बजाय बाइट्स को कैप्चर कर सकते हैं।

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

यह लाइन क्लासिक **convert image to PDF** वर्कफ़्लो को दर्शाती है: आप इमेज से शुरू करते हैं, OCR चलाते हैं, टेक्स्ट ओवरले करते हैं, और अंत में एक PDF स्ट्रीम उत्पन्न करते हैं।

## चरण 7: परिणाम सत्यापित करें – त्वरित जांच

स्क्रिप्ट चलाने के बाद, `receipt_searchable.pdf` को किसी भी PDF व्यूअर में खोलें और सर्च बॉक्स (Ctrl + F) आज़माएँ। रसीद में मौजूद किसी शब्द को टाइप करें—यदि वह सही स्थान पर कूदता है, तो आपने सफलतापूर्वक **create searchable pdf** कर लिया है!  

यदि सर्च विफल हो, तो दोबारा जाँचें:

1. OCR कॉन्फिडेंस स्कोर (`conf` वैल्यूज़)। कम कॉन्फिडेंस का मतलब हो सकता है कि इमेज धुंधली है।  
2. बाउंडिंग बॉक्स कॉर्डिनेट्स—कभी‑कभी EasyOCR उन्हें अलग ओरिएंटेशन में रिपोर्ट करता है।  
3. यह सुनिश्चित करें कि PDF व्यूअर “image‑only” मोड में नहीं है (दुर्लभ, लेकिन कुछ व्यूअर में यह विकल्प होता है)।

## पूर्ण कार्यशील स्क्रिप्ट

सब कुछ मिलाकर, यहाँ पूरी, तैयार‑चलाने‑योग्य Python फ़ाइल है:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

इसे `searchable_pdf.py` के रूप में सहेजें, `YOUR_DIRECTORY` प्लेसहोल्डर्स को वास्तविक पाथ्स से बदलें, और चलाएँ:

```bash
python searchable_pdf.py
```

आपको एक पुष्टि संदेश दिखाई देगा और आपके फ़ोल्डर में एक नई खोज योग्य PDF बनकर रखी होगी।

## सामान्य प्रश्न और किनारे के मामले

**यदि इमेज रंगीन हो तो?**  
EasyOCR ग्रेस्केल और कलर दोनों इमेज के साथ काम करता है, लेकिन ग्रेस्केल में बदलना (`pil_image.convert("L")`) कभी‑कभी शोरयुक्त स्कैन पर सटीकता बढ़ा सकता है।

**क्या मैं मल्टी‑पेज PDF संभाल सकता हूँ?**  
हां—प्रत्येक पेज इमेज पर लूप चलाएँ, OCR चरण चलाएँ, और प्रत्येक पेज को उसी `FPDF` ऑब्जेक्ट में जोड़ें। प्रत्येक नई इमेज के लिए कर्सर रीसेट करना याद रखें (`self.add_page()`)।

**क्या मूल टेक्स्ट लेयर को अदृश्य सफ़ेद टेक्स्ट की बजाय रख सकते हैं?**  
यदि आपको वास्तविक “text‑under‑image” PDF चाहिए (जैसे एक्सेसिबिलिटी के लिए), तो `pdfminer` या `pikepdf` का उपयोग करके proper PDF टैग्स के साथ एक छिपी हुई टेक्स्ट लेयर एम्बेड करने पर विचार करें। यह अधिक उन्नत है, लेकिन सिद्धांत वही रहता है: बैकग्राउंड इमेज + ओवरले टेक्स्ट।

**यदि OCR कॉन्फिडेंस कम है तो?**  
आप कम‑कॉन्फिडेंस वाले शब्दों को फ़िल्टर कर सकते हैं:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## समापन – हमने क्या हासिल किया

हमने रसीद की एक साधारण इमेज से शुरू किया, **performed OCR on image**, पहचाने गए स्ट्रिंग्स निकाले, और अंत में **create searchable pdf** बनाया जो किसी भी प्रोफ़ेशनल स्कैन किए गए दस्तावेज़ की तरह व्यवहार करता है। प्रक्रिया ने हर द्वितीयक कीवर्ड को कवर किया—**convert OCR to PDF**, **extract text from image**, **convert image to PDF**, और **perform OCR on image**—इसलिए अब आपके पास किसी भी समान प्रोजेक्ट के लिए एक पुन: उपयोग योग्य टूलबॉक्स है।

### आगे के कदम

- अन्य भाषाओं के साथ प्रयोग करें, उनके ISO कोड को `easyocr.Reader(['en', 'es'])` में पास करके।  
- यदि आपको पूरी तरह ऑफ़लाइन समाधान चाहिए तो EasyOCR को Tesseract से बदलें; बाकी पाइपलाइन समान रहती है।  
- OCR कॉन्फिडेंस विज़ुअलाइज़ेशन जोड़ें (इमेज पर बाउंडिंग बॉक्स ड्रॉ करें) ताकि समस्या वाली स्कैन को डिबग किया जा सके।  

क्या आपके पास कोई नया तरीका है जिसे आप साझा करना चाहते हैं? टिप्पणी छोड़ें, fork

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर करने में मदद करेंगे।

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}