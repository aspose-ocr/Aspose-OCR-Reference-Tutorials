---
category: general
date: 2026-04-26
description: स्कैन किए गए PDF पर OCR का उपयोग कैसे करें, PDF से टेक्स्ट निकालें, PDF
  पर OCR चलाएँ, और कुछ चरणों में स्कैन किए गए PDF को खोज योग्य फ़ाइलों में बदलें।
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: hi
og_description: 'Python में OCR का उपयोग कैसे करें: PDF से टेक्स्ट निकालना सीखें,
  PDF पर OCR चलाएँ, और स्कैन किए गए PDF को खोज योग्य दस्तावेज़ों में बदलें।'
og_title: OCR का उपयोग कैसे करें – PDF से टेक्स्ट निकालने के लिए त्वरित गाइड
tags:
- OCR
- Python
- PDF
- Text Extraction
title: OCR का उपयोग कैसे करें – Python के साथ PDF से टेक्स्ट निकालें
url: /hi/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR का उपयोग कैसे करें – Python के साथ PDF से टेक्स्ट निकालें

क्या आप कभी सोचते रहे हैं **how to use OCR** को स्कैन किए गए कॉन्ट्रैक्ट, रसीद, या ईबुक से टेक्स्ट निकालने के लिए? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में प्राप्त PDF सिर्फ एक इमेज होती है, और OCR के बिना आप उसकी सामग्री को सर्च, इंडेक्स या विश्लेषण नहीं कर सकते।  

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे **how to use OCR**, **extract text from PDF**, और क्यों आपको **convert scanned PDF** फ़ाइलों को सर्चेबल डॉक्यूमेंट्स में बदलना चाहिए। हम **loading PDF as image** की बारीकियों को भी कवर करेंगे ताकि OCR इंजन हर पेज को स्पष्ट रूप से देख सके।

> **त्वरित पूर्वावलोकन:** अंत तक आपके पास एक स्क्रिप्ट होगी जो मल्टी‑पेज PDF को लोड करती है, प्रत्येक पेज पर OCR चलाती है, और पहचाने गए टेक्स्ट को प्रिंट करती है – कोई बाहरी सेवा आवश्यक नहीं।

## आपको क्या चाहिए

- Python 3.9+ (कोई भी हालिया संस्करण काम करेगा)
- `aocr` पैकेज (या कोई भी संगत OCR लाइब्रेरी जो `OcrEngine` और `Image.load` प्रदान करती हो)
- एक स्कैन किया हुआ PDF फ़ाइल जिसे आप प्रोसेस करना चाहते हैं (उदाहरण के लिए `contract.pdf`)
- एक मध्यम मात्रा में RAM (≈ 200 MB प्रति 100‑पेज PDF आमतौर पर ठीक रहता है)

यदि आपने अभी तक OCR लाइब्रेरी इंस्टॉल नहीं की है, तो चलाएँ:

```bash
pip install aocr
```

> **Pro tip:** डिपेंडेंसीज़ को व्यवस्थित रखने के लिए एक वर्चुअल एनवायरनमेंट का उपयोग करें।

## चरण 1: PDF को इमेज के रूप में लोड करें – पहेली का पहला टुकड़ा

किसी भी OCR के होने से पहले, PDF को एक इमेज के रूप में प्रस्तुत किया जाना चाहिए। यहाँ पर द्वितीयक कीवर्ड **load pdf as image** काम आता है।

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Why this matters:* `aocr.Image.load` आंतरिक रूप से प्रत्येक PDF पेज को एक बिटमैप में रास्टराइज़ करता है जिसे OCR इंजन समझ सकता है। यदि आप इस चरण को छोड़ देते हैं और कच्चा PDF फीड करते हैं, तो इंजन एक त्रुटि देगा क्योंकि वह पिक्सेल डेटा की अपेक्षा करता है, वेक्टर डेटा नहीं।

> **Note:** पाथ एब्सोल्यूट या रिलेटिव हो सकता है। सुनिश्चित करें कि फ़ाइल पढ़ी जा सकती है; अन्यथा आपको `FileNotFoundError` मिलेगा।

## चरण 2: PDF पर OCR चलाएँ – पिक्सेल को अक्षरों में बदलना

अब जब PDF इमेज के रूप में मौजूद है, हम अंततः **run OCR on PDF** कर सकते हैं। नीचे दिया गया स्निपेट सभी पेजों को एक साथ प्रोसेस करता है:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*What’s happening under the hood?* `process_all_pages` रास्टराइज़्ड पेजों के माध्यम से लूप करता है, OCR मॉडल लागू करता है, और परिणाम ऑब्जेक्ट्स की एक सूची लौटाता है—प्रति पेज एक। प्रत्येक परिणाम में पहचाना गया टेक्स्ट, कॉन्फिडेंस स्कोर, और बाउंडिंग बॉक्स (यदि बाद में चाहिए) शामिल होते हैं।

## चरण 3: PDF से टेक्स्ट निकालें – स्ट्रिंग्स को बाहर निकालना

OCR परिणाम हाथ में होने पर, साधारण टेक्स्ट निकालना बहुत आसान हो जाता है। हम पेजों पर इटररेट करेंगे और आउटपुट प्रिंट करेंगे, जिससे द्वितीयक कीवर्ड **extract text from pdf** प्रदर्शित होगा।

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Expected output** (संक्षिप्त रूप में):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

यदि आपको टेक्स्ट एक ही स्ट्रिंग में चाहिए, तो बस कंकैटेनेट करें:

```python
full_text = "\n".join(r.text for r in page_results)
```

अब आपने सफलतापूर्वक OCR का उपयोग करके **extracted text from PDF** कर लिया है।

## चरण 4: स्कैन किए गए PDF को बदलें – इसे सर्चेबल बनाना

कई डाउनस्ट्रीम टूल्स (जैसे Elasticsearch या SharePoint) एक सर्चेबल PDF की अपेक्षा करते हैं, न कि साधारण‑टेक्स्ट डंप की। आप OCR आउटपुट को मूल PDF में एम्बेड कर सकते हैं, जिससे प्रभावी रूप से **convert scanned PDF** को सर्चेबल संस्करण में बदल दिया जाता है।

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Why bother?* एक सर्चेबल PDF मूल लेआउट और इमेजेज़ को बरकरार रखता है, जबकि टेक्स्ट चयन और इंडेक्सिंग की सुविधा देता है—मानव और मशीन दोनों के लिए जीत‑जीत।

## सामान्य समस्याएँ और किनारे के मामले

### मेमोरी से बड़े मल्टी‑पेज PDFs

यदि आपका PDF सैकड़ों पेजों का है, तो सभी को एक साथ लोड करना RAM को समाप्त कर सकता है। `aocr` लाइब्रेरी लेज़ी लोडिंग का समर्थन करती है:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

फिर पेजों को एक‑एक करके प्रोसेस करें:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### कम‑गुणवत्ता वाले स्कैन

ब्लरी या लो‑कॉन्ट्रास्ट स्कैन पर OCR की सटीकता बहुत घट जाती है। इमेज को इंजन में फीड करने से पहले प्री‑प्रोसेसिंग पर विचार करें:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### भाषा समर्थन

डिफ़ॉल्ट रूप से इंजन इंग्लिश मानता है। किसी अन्य भाषा में **run OCR on PDF** करने के लिए, भाषा कोड सेट करें:

```python
ocr_engine.language = "spa"  # Spanish
```

सुनिश्चित करें कि संबंधित भाषा मॉडल इंस्टॉल किया हुआ है।

## पूर्ण कार्यशील उदाहरण

सब कुछ मिलाकर, यहाँ एक स्व-निहित स्क्रिप्ट है जिसे आप `ocr_pdf.py` नाम की फ़ाइल में डाल सकते हैं और तुरंत चला सकते हैं:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

इसे इस तरह चलाएँ:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

आप कंसोल में टेक्स्ट प्रिंट होते देखेंगे, और यदि आपने `-o` दिया है, तो मूल फ़ाइल के बगल में एक सर्चेबल PDF बन जाएगा।

## प्रो टिप्स और सर्वोत्तम प्रथाएँ

- **Batch processing:** जब दर्जनों PDFs को हैंडल कर रहे हों, तो ऊपर दिया गया लॉजिक एक लूप में रैप करें और प्रत्येक फ़ाइल की सफलता/विफलता को लॉग करें।
- **Confidence filtering:** प्रत्येक `page_result` में एक कॉन्फिडेंस मीट्रिक शामिल होता है। कम कॉन्फिडेंस वाले पेजों को मैन्युअल रिव्यू के लिए डिस्कार्ड या फ़्लैग करें।
- **Parallelism:** यदि आपके CPU में कई कोर हैं, तो `concurrent.futures` का उपयोग करके पेजों को पैरलल में प्रोसेस करने पर विचार करें—सिर्फ मेमोरी उपयोग का ध्यान रखें।
- **Version lock:** `aocr` API विकसित हो सकता है। `requirements.txt` में संस्करण पिन करें (उदाहरण के लिए `aocr==2.3.1`) ताकि ब्रेकिंग चेंजेज़ से बचा जा सके।

## निष्कर्ष

हमने **how to use OCR** को **extract text from PDF**, **run OCR on PDF**, **load PDF as image**, और यहाँ तक कि **convert scanned PDF** को सर्चेबल फ़ॉर्मेट में बदलने तक कवर किया। कोड पूर्ण है, व्याख्याएँ *क्या* और *क्यों* दोनों को कवर करती हैं, और अब आपके पास किसी भी इमेज‑बेस्ड PDF प्रोजेक्ट के लिए एक पुन: उपयोग योग्य पैटर्न है।

अब आगे क्या? निकाले गए टेक्स्ट को एक नेचुरल‑लैंग्वेज पाइपलाइन में फीड करें, सर्चेबल PDFs को Elasticsearch के साथ इंडेक्स करें, या Tesseract या Azure Computer Vision जैसे विभिन्न OCR बैक‑एंड्स के साथ प्रयोग करें। संभावनाएँ असीमित हैं, और टूल्स आपके हाथों में हैं।

हैप्पी कोडिंग, और आपके PDFs हमेशा सर्चेबल रहें! 

![how to use OCR example](/images/ocr_workflow.png "how to use OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}