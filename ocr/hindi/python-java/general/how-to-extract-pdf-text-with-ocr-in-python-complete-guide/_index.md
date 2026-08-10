---
category: general
date: 2026-06-19
description: Python में OCR का उपयोग करके PDF कैसे निकालें – चरण‑दर‑चरण ट्यूटोरियल
  जिसमें PDF से टेक्स्ट निकालना, छवि से टेक्स्ट पहचानना, और एक OCR Python उदाहरण शामिल
  है।
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: hi
og_description: Python में OCR का उपयोग करके PDF कैसे निकालें। PDF से टेक्स्ट निकालना,
  इमेज से टेक्स्ट पहचानना सीखें, और एक पूर्ण OCR Python उदाहरण देखें।
og_title: Python में OCR के साथ PDF टेक्स्ट कैसे निकालें – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Python में OCR के साथ PDF टेक्स्ट कैसे निकालें – पूर्ण गाइड
url: /hi/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में OCR के साथ PDF टेक्स्ट निकालने का तरीका – पूर्ण गाइड

क्या आप कभी सोचते थे कि **PDF से टेक्स्ट कैसे निकालें** जब फ़ाइल केवल स्कैन की गई छवि हो? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स—जैसे अनुबंध, चालान, या ऐतिहासिक अभिलेख—में प्राप्त PDF में चयन योग्य टेक्स्ट नहीं होता। अच्छी खबर? कुछ ही पंक्तियों के Python कोड से उन केवल‑छवि पृष्ठों को खोज योग्य, संपादन योग्य टेक्स्ट में बदला जा सकता है।

इस ट्यूटोरियल में हम एक व्यावहारिक **OCR Python example** के माध्यम से चलेंगे जो PDF पढ़ता है, उसकी पहली पेज को इमेज के रूप में रेंडर करता है, और फिर OCR इंजन का उपयोग करके **extracts text from PDF** करता है। अंत तक आप बिल्कुल जानेंगे कि **read PDF with OCR** कैसे किया जाता है, प्रत्येक चरण क्यों महत्वपूर्ण है, और कोड को मल्टी‑पेज डॉक्यूमेंट या विभिन्न भाषाओं के लिए कैसे अनुकूलित किया जाए।

## आप क्या सीखेंगे

- Python के लिए एक भरोसेमंद OCR लाइब्रेरी को इंस्टॉल और सेट अप करें।  
- OCR के अनुकूल PDF पेजों को इमेज में बदलें।  
- **Recognize text from image** और साफ़ Unicode स्ट्रिंग्स प्राप्त करें।  
- सामान्य समस्याएँ (कम‑रिज़ॉल्यूशन PDFs, घुमा हुआ पेज) और उन्हें कैसे टालें।  
- स्क्रिप्ट को कई पेजों या बैच प्रोसेसिंग को संभालने के लिए विस्तारित करें।

**Prerequisites**: Python 3.8+, pip, और वर्चुअल एनवायरनमेंट्स की बुनियादी समझ। पहले से OCR का अनुभव आवश्यक नहीं—बस साथ चलें।

---

## ## Python में OCR के साथ PDF टेक्स्ट निकालना

यह H2 हेडर हमारे मुख्य कीवर्ड को ठीक वहीं रखता है जहाँ सर्च इंजन इसे देखना पसंद करते हैं। चलिए सीधे कोड में डुबकी लगाते हैं।

### चरण 1 – आवश्यक पैकेज स्थापित करें

First, we need an OCR engine. The example below uses the popular **ocr** package (a thin wrapper around Tesseract). If you prefer a different backend, the concepts stay the same.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Pro tip:** On Linux, you’ll also need the Tesseract binary: `sudo apt-get install tesseract-ocr`. macOS users can grab it via Homebrew: `brew install tesseract`.

### चरण 2 – OCR इंजन को इनिशियलाइज़ करें और भाषा सेट करें

Now we spin up the engine and tell it to look for English characters. You can swap `ocr.Language.English` for any supported language code.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Why this matters:** Specifying the language dramatically improves accuracy because the engine can apply language‑specific dictionaries and character models.

### चरण 3 – PDF पेज को इमेज के रूप में लोड करें

OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based indexing).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Edge case:** If the PDF contains vector graphics rather than scanned images, you might get a crisp rendering. For low‑resolution scans, consider increasing the DPI: `ocr.Image.from_pdf(..., dpi=300)`.

### चरण 4 – रेंडर की गई इमेज से टेक्स्ट पहचानें

Here’s the heart of the **ocr python example**. The engine processes the bitmap and returns an object containing the extracted string.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

The `ocr_result.text` attribute holds the plain‑text output, preserving line breaks where possible.

### चरण 5 – निकाले गए टेक्स्ट को प्रिंट या स्टोर करें

Finally, we output the result. In a real application you’d probably write to a file or a database.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Running the script should display something like:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

That’s a complete **extract text from pdf** workflow using OCR.

---

## ## इमेज से टेक्स्ट पहचानें – सटीकता सुधारना

If you’re only interested in **recognize text from image** (say, a JPEG of a receipt), you can skip the PDF conversion step:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Tips for better results:**

- **Pre‑process** the image: convert to grayscale, apply thresholding, or deskew. Pillow makes this easy.
- **Increase DPI** during PDF rendering: higher resolution gives the OCR engine more detail.
- **Enable OCR engine’s config** for page segmentation (`ocr_engine.config = "--psm 6"` for uniform blocks).

## ## OCR के साथ PDF पढ़ें – कई पेजों को संभालना

Most contracts span several pages. Looping over each page is straightforward:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

This function **reads PDF with OCR**, concatenates the output, and inserts a clear page break marker. You can then feed `full_text` into a search index or store it as a `.txt` file.

## ## सामान्य समस्याएँ और उनके समाधान

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| गड़बड़ अक्षर, बहुत सारे `?` | गलत भाषा या भाषा डेटा फ़ाइलें अनुपलब्ध | सही Tesseract भाषा पैक (`tesseract-ocr-<lang>`) इंस्टॉल करें और `ocr_engine.language` सेट करें। |
| लाइनें गायब या शब्द कटे हुए | निम्न DPI (150 से कम) | PDF को 300 DPI या उससे अधिक पर रेंडर करें (`dpi=300`). |
| टेक्स्ट घुमा हुआ या उल्टा | स्कैन किया गया पेज सीधा नहीं है | पहचान से पहले `ocr.Image.deskew(page_image)` का उपयोग करें। |
| बड़े PDFs पर धीमी प्रोसेसिंग | पेजों को एकल थ्रेड पर क्रमिक रूप से प्रोसेस करना | `concurrent.futures.ThreadPoolExecutor` के साथ समानांतर प्रोसेसिंग करें। |

## ## OCR Python उदाहरण का विस्तार

- **Export to PDF/A**: After extraction, you can embed the text back into a searchable PDF using `reportlab` or `pypdf2`।
- **Language detection**: Use `langdetect` on the OCR output to switch `ocr_engine.language` dynamically।
- **Batch processing**: Walk a directory with `os.listdir` and apply `extract_all_pages` to every file।

## ## अपेक्षित आउटपुट और सत्यापन

When you run the script against a clear, English‑language scan, you should see a clean block of text with proper punctuation. Verify by:

1. Comparing a few lines to the original scanned image.  
2. Running a simple word count (`len(ocr_result.text.split())`) to ensure the output isn’t empty.  
3. Optionally, feeding the result into a spell‑checker like `pyspellchecker` to spot OCR errors।

## निष्कर्ष

We’ve covered **how to extract PDF** content when traditional parsing fails, demonstrated a full **ocr python example**, and explained how to **recognize text from image** and **read PDF with OCR** for both single‑page and multi‑page scenarios. With the code snippets above you can now turn any scanned PDF into searchable, editable text—no more manual re‑typing।

Next steps? Try swapping the language to Spanish (`ocr.Language.Spanish`) or experiment with image pre‑processing techniques to boost accuracy. If you’re building a document‑management system, consider indexing the extracted text with Elasticsearch for lightning‑fast search।

Got questions or run into a quirky PDF? Drop a comment, and happy coding!  

![Python में OCR का उपयोग करके PDF निकालने का तरीका](image.png "Python में OCR का उपयोग करके PDF निकालने का तरीका")

## आगे आप क्या सीखें

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose OCR के साथ इमेज से टेक्स्ट निकालें – चरण‑दर‑चरण गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [PDF टेक्स्ट पहचानें – Aspose.OCR for Java के साथ OCR ऑपरेशन्स](/ocr/english/java/ocr-operations/)
- [C# में इमेज टेक्स्ट निकालें भाषा चयन के साथ Aspose.OCR का उपयोग करके](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}