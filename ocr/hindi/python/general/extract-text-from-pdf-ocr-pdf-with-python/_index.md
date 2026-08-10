---
category: general
date: 2026-04-29
description: Aspose OCR का उपयोग करके Python में PDF से टेक्स्ट निकालें। बैच OCR PDF
  प्रोसेसिंग सीखें, स्कैन किए गए PDF टेक्स्ट को बदलें, और कम‑विश्वास वाले पृष्ठों
  को संभालें।
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: hi
og_description: Python में Aspose OCR के साथ PDF से टेक्स्ट निकालें। यह गाइड बैच OCR
  PDF प्रोसेसिंग, स्कैन किए गए PDF टेक्स्ट को बदलना, और कम‑विश्वास परिणामों को संभालना
  दिखाता है।
og_title: PDF से टेक्स्ट निकालें – Python के साथ OCR PDF
tags:
- OCR
- Python
- PDF processing
title: PDF से टेक्स्ट निकालें – Python के साथ OCR PDF
url: /hi/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF से टेक्स्ट निकालें – Python के साथ OCR PDF

क्या आपको कभी **PDF से टेक्स्ट निकालने** की ज़रूरत पड़ी है लेकिन फ़ाइल सिर्फ एक स्कैन की हुई इमेज है? आप अकेले नहीं हैं—कई डेवलपर्स इस समस्या का सामना करते हैं जब वे PDFs को सर्चेबल डेटा में बदलने की कोशिश करते हैं। अच्छी खबर? Aspose OCR for Python के साथ आप कुछ लाइनों में स्कैन किए गए PDF टेक्स्ट को कन्वर्ट कर सकते हैं, और जब आपके पास दर्जनों फ़ाइलें हों तो **batch OCR PDF processing** भी चला सकते हैं।

इस ट्यूटोरियल में हम पूरे वर्कफ़्लो को कवर करेंगे: लाइब्रेरी सेटअप, एकल PDF पर OCR चलाना, बैच में स्केल करना, और लो‑कन्फिडेंस पेज़ेस को हैंडल करना ताकि आपको पता चल सके कब मैन्युअल रिव्यू की ज़रूरत है। अंत तक आपके पास एक तैयार‑टू‑रन स्क्रिप्ट होगी जो किसी भी स्कैन किए गए PDF से टेक्स्ट निकालती है, और आप प्रत्येक स्टेप के पीछे का कारण समझ पाएँगे।

## आपको क्या चाहिए

- Python 3.8 या नया (कोड f‑strings का उपयोग करता है, इसलिए 3.6+ काम करता है, लेकिन 3.8+ की सलाह दी जाती है)
- Aspose OCR for Python लाइसेंस या एक फ्री ट्रायल की (आप इसे Aspose वेबसाइट से प्राप्त कर सकते हैं)
- एक फ़ोल्डर जिसमें एक या अधिक स्कैन किए गए PDFs हों जिन्हें आप प्रोसेस करना चाहते हैं
- जनरेट किए गए *.txt* रिपोर्टों के लिए पर्याप्त डिस्क स्पेस

बस इतना ही—कोई भारी बाहरी डिपेंडेंसी नहीं, कोई OpenCV जिम्नास्टिक नहीं। Aspose OCR इंजन आपके लिए भारी काम संभालता है।

## पर्यावरण सेटअप

First, install the Aspose OCR package from PyPI:

```bash
pip install aspose-ocr
```

If you have a license file (`Aspose.OCR.lic`), place it in your project root and activate it like so:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Pro tip:** लाइसेंस फ़ाइल को संस्करण नियंत्रण से बाहर रखें; इसे `.gitignore` में जोड़ें ताकि आकस्मिक एक्सपोज़र से बचा जा सके।

## एकल PDF पर OCR करना

अब चलिए एक स्कैन किए गए PDF से टेक्स्ट निकालते हैं। मुख्य चरण हैं:

1. `OcrEngine` का एक इंस्टेंस बनाएं।
2. इसे PDF फ़ाइल की ओर इंगित करें।
3. प्रत्येक पेज के लिए `OcrResult` प्राप्त करें।
4. सादा‑टेक्स्ट आउटपुट को डिस्क पर लिखें।
5. इंजन को डिस्पोज़ करें ताकि नेटिव रिसोर्सेज़ मुक्त हो सकें।

Here’s the full, runnable script:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**What you’ll see:** For each page the script prints something like `Page 1: confidence 97.45%`. If a page falls under the 80 % threshold, a warning appears, letting you know that the OCR might have missed characters.

### यह क्यों काम करता है

- **`OcrEngine`** नेटिव Aspose OCR लाइब्रेरी का गेटवे है; यह इमेज प्री‑प्रोसेसिंग से लेकर कैरेक्टर रिकग्निशन तक सब कुछ संभालता है।
- **`extract_from_pdf`** प्रत्येक PDF पेज को स्वचालित रूप से रास्टराइज़ करता है, इसलिए आपको PDF को इमेज में बदलने की ज़रूरत नहीं है।
- **Confidence स्कोर** आपको क्वालिटी चेक्स ऑटोमेट करने देते हैं—क़ानूनी या मेडिकल दस्तावेज़ों को प्रोसेस करते समय जहाँ सटीकता महत्वपूर्ण है, यह आवश्यक है।

## Python के साथ बैच OCR PDF प्रोसेसिंग

अधिकांश रियल‑वर्ल्ड प्रोजेक्ट्स में एक से अधिक फ़ाइलें होती हैं। चलिए सिंगल‑फ़ाइल स्क्रिप्ट को **batch OCR PDF processing** पाइपलाइन में विस्तारित करते हैं जो एक डायरेक्टरी को ट्रैवर्स करती है, प्रत्येक PDF को प्रोसेस करती है, और परिणामों को मिलते‑जुलते सब‑फ़ोल्डर में स्टोर करती है।

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### यह कैसे मदद करता है

- **Scalability:** फ़ंक्शन फ़ोल्डर को एक बार ट्रैवर्स करता है, प्रत्येक PDF के लिए एक समर्पित आउटपुट सब‑फ़ोल्डर बनाता है। यह तब चीज़ों को व्यवस्थित रखता है जब आपके पास दर्जनों दस्तावेज़ हों।
- **Reusability:** `ocr_pdf_file` को अन्य स्क्रिप्ट्स (जैसे, वेब सर्विस) से कॉल किया जा सकता है क्योंकि यह एक शुद्ध फ़ंक्शन है।
- **Error handling:** यदि इनपुट फ़ोल्डर खाली है तो स्क्रिप्ट एक दोस्ताना संदेश प्रिंट करती है, जिससे आप साइलेंट फेल्योर से बचते हैं।

## स्कैन किए गए PDF टेक्स्ट को कन्वर्ट करना – एज केस हैंडलिंग

जबकि ऊपर दिया गया कोड अधिकांश PDFs के लिए काम करता है, आपको कुछ क्विर्क्स का सामना हो सकता है:

| स्थिति | क्यों होता है | कैसे निपटें |
|-----------|----------------|-----------------|
| **Encrypted PDFs** | PDF पासवर्ड‑प्रोटेक्टेड है। | पासवर्ड को `extract_from_pdf(pdf_path, password="yourPwd")` में पास करें। |
| **Multi‑language documents** | Aspose OCR डिफ़ॉल्ट रूप से अंग्रेज़ी पर सेट है। | `ocr_engine.language = "spa"` सेट करें स्पेनिश के लिए, या मिश्रित भाषाओं के लिए सूची प्रदान करें। |
| **Very large PDFs (>500 pages)** | प्रत्येक पेज RAM में लोड होने के कारण मेमोरी उपयोग बढ़ जाता है। | `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` का उपयोग करके PDF को चंक्स में प्रोसेस करें और लूप करें। |
| **Poor scan quality** | कम DPI या अधिक शोर से confidence कम हो जाता है। | `engine.image_preprocessing = True` के साथ PDF को प्री‑प्रोसेस करें या DPI को `engine.dpi = 300` से बढ़ाएँ। |

> **Watch out:** इमेज प्री‑प्रोसेसिंग को ऑन करने से CPU टाइम में उल्लेखनीय वृद्धि हो सकती है। यदि आप नाइटली बैच चला रहे हैं, तो पर्याप्त समय शेड्यूल करें या एक अलग वर्कर स्पिन अप करें।

## आउटपुट की जाँच

After the script finishes, you’ll find a folder structure like:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

किसी भी `.txt` फ़ाइल को खोलें; आपको साफ़, UTF‑8 एन्कोडेड टेक्स्ट दिखना चाहिए जो मूल स्कैन किए गए कंटेंट को प्रतिबिंबित करता है। यदि आपको गड़बड़ अक्षर दिखें, तो PDF की भाषा सेटिंग्स दोबारा जांचें और सुनिश्चित करें कि मशीन पर सही फ़ॉन्ट पैक्स इंस्टॉल हैं।

## रिसोर्सेज़ को क्लीन अप करना

Aspose OCR नेटिव DLLs पर निर्भर करता है, इसलिए काम खत्म होने पर `engine.dispose()` को कॉल करना आवश्यक है। इस स्टेप को भूलने से मेमोरी लीक्स हो सकते हैं, खासकर लंबे‑चलने वाले बैच जॉब्स में।

```python
# Always the last line of your script
engine.dispose()
```

## पूर्ण एंड‑टू‑एंड उदाहरण

Putting everything together, here’s a single

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}