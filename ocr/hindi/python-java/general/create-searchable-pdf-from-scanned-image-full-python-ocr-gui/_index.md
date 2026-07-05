---
category: general
date: 2026-07-05
description: Python के साथ खोज योग्य PDF बनाएं। जानें कि स्कैन किए गए PNG को OCR कैसे
  करें, स्कैन की गई इमेज PDF को कैसे बदलें, और कुछ ही मिनटों में खोज योग्य PDF प्राप्त
  करें।
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: hi
og_description: तेज़ी से सर्चेबल PDF बनाएं। यह गाइड दिखाता है कि कैसे PNG को OCR करें,
  स्कैन की गई इमेज PDF को बदलें, और Python का उपयोग करके सर्चेबल PDF बनाएं।
og_title: स्कैन की गई छवि से खोज योग्य PDF बनाएं – पायथन OCR ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: स्कैन की गई छवि से खोज योग्य PDF बनाएं – पूर्ण पाइथन OCR गाइड
url: /hi/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# स्कैन किए गए इमेज से सर्चेबल PDF बनाएं – पूर्ण Python OCR गाइड

क्या आपने कभी सोचा है कि **सर्चेबल PDF** कैसे बनाएं स्कैन की गई तस्वीर से, बिना महंगे सॉफ़्टवेयर के भुगतान किए? आप अकेले नहीं हैं। कई कार्यालयों में, PDFs केवल फ्लैट इमेज के रूप में आते हैं—खोजने में कठिन, कॉपी‑पेस्ट असंभव, और अनुपालन ऑडिट के लिए एक दुःस्वप्न। अच्छी खबर? कुछ ही पंक्तियों के Python कोड से आप उस स्थिर PNG को पूरी तरह सर्चेबल PDF में बदल सकते हैं, और प्रक्रिया उतनी ही आसान है जितनी आप सोचते हैं।

इस ट्यूटोरियल में हम एक पूर्ण **OCR रिकग्निशन उदाहरण** के माध्यम से चलेंगे, जिसमें सही लाइब्रेरी को इंस्टॉल करने से लेकर अंतिम PDF फ़ाइल लिखने तक सब कुछ शामिल है। अंत तक आप बिल्कुल जानेंगे कि **स्कैन की गई इमेज PDF** फ़ाइलों को कैसे **convert scanned image pdf** किया जाता है, प्रोग्रामेटिकली **how to ocr pdf** कैसे किया जाता है, और आपके पास एक पुन: उपयोग योग्य स्क्रिप्ट होगी जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं।

## आप क्या सीखेंगे

- एक Python OCR लाइब्रेरी इंस्टॉल और कॉन्फ़िगर करें (हम `pytesseract` और `pdf2image` का उपयोग करेंगे)।
- OCR इंजन को इनिशियलाइज़ करें और भाषा सेट करें।
- स्कैन की गई PNG (या कोई भी इमेज) लोड करें और उस पर OCR चलाएँ।
- OCR परिणाम को **सर्चेबल PDF** (बाइट एरे) में बदलें और सेव करें।
- मल्टी‑पेज दस्तावेज़ों, विभिन्न भाषाओं, और सामान्य समस्याओं को संभालने के टिप्स।

OCR का कोई पूर्व अनुभव आवश्यक नहीं—सिर्फ एक कार्यशील Python 3 वातावरण और थोड़ा जिज्ञासा।

---

## सर्चेबल PDF – अवलोकन

नीचे उन चरणों का एक हाई‑लेवल फ्लोचार्ट है जिन्हें हम लागू करेंगे।  

![सर्चेबल PDF वर्कफ़्लो डायग्राम](https://example.com/flowchart.png "सर्चेबल PDF वर्कफ़्लो डायग्राम")

*Alt text: सर्चेबल PDF वर्कफ़्लो डायग्राम जिसमें इंजन इनिशियलाइज़ेशन, इमेज लोड, OCR रिकग्निशन, PDF कन्वर्ज़न, और फ़ाइल राइट शामिल हैं।*

---

## चरण 1: OCR इंजन को प्रारंभ करें (how to ocr pdf)

हमें बिल्कुल भी इंजन को इनिशियलाइज़ क्यों करना पड़ता है? OCR इंजन वह दिमाग है जो पिक्सेल पैटर्न को अक्षरों में बदलता है। एक इंजन इंस्टेंस बनाकर और स्पष्ट रूप से भाषा सेट करके, हम लाइब्रेरी को बताते हैं कि कौन सा अक्षरमाला अपेक्षित है, जिससे सटीकता में बहुत सुधार होता है।

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Pro tip:** यदि आपको कई भाषाओं में दस्तावेज़ OCR करने हैं, तो Tesseract के संबंधित भाषा पैक्स इंस्टॉल करें और `ocr_language` को `"eng+spa"` जैसी सूची पास करें।

---

## चरण 2: स्कैन की गई इमेज लोड करें (convert scanned image pdf)

पज़ल का अगला हिस्सा इमेज डेटा को Python में लाना है। चाहे आपके पास एकल PNG हो या मल्टी‑पेज TIFF, `PIL.Image` क्लास इसे खोल सकती है। यदि आप पहले से स्कैन की गई इमेज वाली PDF से शुरू कर रहे हैं, तो `pdf2image` प्रत्येक पेज को इमेज में बदल देगा।

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Why this matters:** इमेज को Pillow ऑब्जेक्ट के रूप में लोड करने से हमें उसके रॉ पिक्सेल डेटा तक पहुंच मिलती है, जिसकी OCR इंजन को आवश्यकता होती है। इस चरण को छोड़कर सीधे रॉ बाइट्स फीड करने से त्रुटियां आएंगी।

---

## चरण 3: इमेज पर OCR रिकग्निशन करें (ocr recognition example)

अब मज़ेदार हिस्सा—इंजन को टेक्स्ट पढ़ने देना। `pytesseract.image_to_pdf_or_hocr` एक PDF बाइट स्ट्रीम लौटाता है जिसमें पहले से ही एक अदृश्य टेक्स्ट लेयर होती है, जो **सर्चेबल PDF** बनाने के लिए बिल्कुल सही है।

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Edge case:** यदि आपकी इमेज कम कंट्रास्ट वाली है, तो OCR से पहले एक साधा थ्रेशहोल्ड लागू करने पर विचार करें:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

यह छोटा प्री‑प्रोसेसिंग कदम सटीकता को नाटकीय रूप से बढ़ा सकता है।

---

## चरण 4: PDF बाइट्स को फ़ाइल में लिखें (convert png searchable pdf)

OCR लाइब्रेरी हमें एक बाइट एरे देती है—इसे एक PDF फ़ाइल की कच्ची सामग्री समझें। अब हमें बस उन बाइट्स को डिस्क पर लिखना है।

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**What you’ll see:** परिणामी फ़ाइल को किसी भी PDF व्यूअर में खोलें और उस शब्द को खोजने की कोशिश करें जो मूल इमेज में मौजूद है। हाइलाइट सीधे उस स्थान पर कूदना चाहिए, यह साबित करते हुए कि अदृश्य टेक्स्ट लेयर काम कर रही है।

---

## चरण 5: मल्टी‑पेज दस्तावेज़ों के लिए विस्तार (convert scanned image pdf)

वास्तविक दुनिया के कॉन्ट्रैक्ट अक्सर कई पेजों में होते हैं। **स्कैन की गई इमेज PDF** फ़ाइलों को कई पेजों के साथ प्रोसेस करने के लिए, प्रत्येक पेज पर लूप करें, OCR चलाएँ, और परिणामी PDFs को जोड़ें।

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Why merge?** प्रत्येक `image_to_pdf_or_hocr` कॉल एक स्वतंत्र PDF बनाता है। उन्हें मर्ज करने से अंतिम दस्तावेज़ मूल पेज क्रम को बरकरार रखता है।

---

## सामान्य समस्याएँ और उनके समाधान

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| PDF खोलने के बाद टेक्स्ट सर्चेबल नहीं है | Tesseract कोई अक्षर नहीं पा रहा (खाली आउटपुट) | इमेज क्वालिटी जांचें, DPI बढ़ाएँ, या प्री‑प्रोसेसिंग लागू करें (कंट्रास्ट, बाइनराइज़ेशन)। |
| गड़बड़ अक्षर (जैसे �) | गलत भाषा पैक या फ़ॉन्ट नहीं मिला | सही भाषा डेटा (`tesseract‑lang‑eng`) इंस्टॉल करें और सुनिश्चित करें `ocr_language` मेल खाता हो। |
| PDF फ़ाइल का आकार बहुत बड़ा (>10 MB एक‑पेज इमेज के लिए) | स्रोत PNG लॉसलेस है; OCR पूरी‑रिज़ॉल्यूशन इमेज जोड़ता है | OCR से पहले इमेज को डाउनस्केल करें (`image.thumbnail((1240, 1754))` A4 के लिए)। |
| Windows पर “tesseract.exe not found” त्रुटि | Tesseract बाइनरी PATH में नहीं है | `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` जोड़ें (पाथ समायोजित करें)। |

---

## पूर्ण, तैयार‑चलाने‑योग्य स्क्रिप्ट

सब कुछ एक साथ लाते हुए, यहाँ एक सिंगल फ़ाइल है जिसे आप कॉपी‑पेस्ट करके चला सकते हैं:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

इसे `create_searchable_pdf.py` के रूप में सेव करें, प्लेसहोल्डर्स को वास्तविक पाथ्स से बदलें, और चलाएँ:

```bash
python create_searchable_pdf.py
```

आपको एक

## अगला आप क्या सीखेंगे?

निम्नलिखित ट्यूटोरियल्स निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}