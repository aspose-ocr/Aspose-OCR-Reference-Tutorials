---
category: general
date: 2026-06-22
description: Python में PDF फ़ाइलों को OCR करने, PDF से टेक्स्ट निकालने और स्ट्रीम‑आधारित
  दृष्टिकोण का उपयोग करके PDF को टेक्स्ट में बदलने का तरीका सीखें। स्कैन किए गए PDF
  को प्रोसेस करने के लिए सरल चरण।
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: hi
og_description: Python में PDF फ़ाइलों को OCR कैसे करें? इस गाइड का पालन करके PDF
  से टेक्स्ट निकालें, PDF को टेक्स्ट में बदलें, और स्ट्रीम का उपयोग करके स्कैन किए
  गए PDF को प्रोसेस करें।
og_title: Python में PDF को OCR कैसे करें – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Python में PDF को OCR कैसे करें – PDFs से टेक्स्ट निकालने के लिए पूर्ण गाइड
url: /hi/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में PDF को OCR कैसे करें – PDFs से टेक्स्ट निकालने के लिए पूर्ण गाइड

क्या आप कभी **how to OCR PDF** फ़ाइलों को भारी डेस्कटॉप टूल्स के साथ झंझट किए बिना करने के बारे में सोचते रहे हैं? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में—जैसे इनवॉइस ऑटोमेशन या अभिलेखीय स्कैन को डिजिटाइज़ करना—आपको एक भरोसेमंद तरीका चाहिए जिससे स्कैन किए गए PDF को खोज योग्य, संपादन योग्य टेक्स्ट में बदला जा सके।

इस ट्यूटोरियल में हम एक साफ़, एंड‑टू‑एंड उदाहरण के माध्यम से चलेंगे जो हल्के Python OCR इंजन का उपयोग करके **extracts text from PDF** पृष्ठों को प्रोसेस करता है। अंत तक आप बिल्कुल जान पाएँगे कि **convert PDF to text** कैसे किया जाता है, **load PDF from stream** कैसे किया जाता है, और **process scanned PDF** को प्रभावी ढंग से कैसे किया जाता है। कोई जादू नहीं, बस साधारण Python कोड जिसे आप आज ही अपने प्रोजेक्ट में जोड़ सकते हैं।

## आप क्या सीखेंगे

- PDF इनपुट को समझने वाले Python OCR लाइब्रेरी को इंस्टॉल और कॉन्फ़िगर करना।  
- PDF‑रिकग्निशन मोड को सक्षम करना और आउटपुट फॉर्मेट को प्लेन टेक्स्ट सेट करना।  
- फ़ाइल स्ट्रीम से मल्टी‑पेज PDF लोड करना (क्लासिक “load pdf from stream” पैटर्न)।  
- सभी पृष्ठों पर OCR चलाना और टेक्स्टुअल कंटेंट प्राप्त करना।  
- डाउनस्ट्रीम प्रोसेसिंग के लिए परिणाम प्रिंट या स्टोर करना।

**Prerequisites**  
- आपके मशीन पर Python 3.8+ इंस्टॉल होना चाहिए।  
- pip और वर्चुअल एनवायरनमेंट्स की बुनियादी जानकारी।  
- एक स्कैन किया हुआ PDF फ़ाइल (`multipage.pdf` नाम से उदाहरण में) जिसे किसी ज्ञात डायरेक्टरी में रखा गया हो।

यदि इनमें से कोई भी चीज़ अपरिचित लगती है, तो चिंता न करें—हर कदम को साधारण भाषा में समझाया गया है, और हम आपको आवश्यक सटीक कमांड्स देंगे।

## Step 1: Install the OCR Engine (how to OCR PDF)

सबसे पहले—आपको एक OCR इंजन चाहिए जो PDF इनपुट को संभाल सके। इस गाइड के लिए हम काल्पनिक `ocr` पैकेज का उपयोग करेंगे (API लोकप्रिय कमर्शियल SDKs को मिरर करता है, लेकिन वही पैटर्न Tesseract‑OCR, ABBYY, या Google Vision के साथ भी काम करता है जब सही तरीके से रैप किया जाए)।

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** यदि आप Windows पर हैं और परमिशन एरर मिल रहे हैं, तो `pip install --user ocr` आज़माएँ।

पैकेज इंस्टॉल हो जाने के बाद, आप इसे अपने स्क्रिप्ट में इम्पोर्ट कर सकते हैं और एक इंजन इंस्टेंस बना सकते हैं—यह **how to OCR PDF** का दिल है।

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

`OcrEngine` ऑब्जेक्ट सभी सेटिंग्स को रखता है जिन्हें हम बाद में ट्यून करेंगे, जैसे भाषा, DPI, और—सबसे महत्वपूर्ण—PDF मोड।

## Step 2: Enable PDF Recognition and Choose Output (extract text from PDF)

डिफ़ॉल्ट रूप से कई OCR SDKs मानते हैं कि आप उन्हें इमेजेज़ दे रहे हैं। इंजन को इनकमिंग स्ट्रीम को PDF के रूप में ट्रीट करने के लिए, हम PDF रिकग्निशन फ़्लैग को एनेबल करते हैं और प्लेन‑टेक्स्ट आउटपुट मांगते हैं।

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

आउटपुट फॉर्मेट निर्दिष्ट करने की ज़रूरत क्यों? क्योंकि कुछ इंजन PDF के साथ हिडन टेक्स्ट लेयर्स, सर्चेबल PDFs, या बाउंडिंग बॉक्स के साथ JSON रिटर्न कर सकते हैं। अधिकांश डेटा‑एक्सट्रैक्शन पाइपलाइन के लिए, **extract text from PDF** को प्लेन स्ट्रिंग्स के रूप में लेना सबसे साफ़ डाउनस्ट्रीम फॉर्मेट है।

## Step 3: Load the PDF from a File Stream (load PDF from stream)

स्ट्रीम से PDF लोड करना मेमोरी‑एफ़िशिएंट पैटर्न है—आप पूरे फ़ाइल को एक बार RAM में लोड करने से बचते हैं। यह विशेष रूप से बड़े मल्टी‑पेज डॉक्यूमेंट्स के साथ काम करते समय उपयोगी होता है।

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **What if the file is on S3 or another cloud bucket?**  
> बस `from_file` को ऐसे मेथड से बदल दें जो बाइट बफ़र को स्वीकार करे (जैसे, `ImageStream.from_bytes(s3_object.read())`)। पाइपलाइन का बाकी हिस्सा समान रहता है।

## Step 4: Run OCR on All Pages (process scanned PDF)

अब असली काम शुरू होता है। इंजन हर पेज पर इटररेट करेगा, रिकग्निशन इंजन चलाएगा, और पेज ऑब्जेक्ट्स की एक लिस्ट रिटर्न करेगा—हर एक अपना टेक्स्टुअल कंटेंट एक्सपोज़ करता है।

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

बैकग्राउंड में, OCR लाइब्रेरी प्रत्येक PDF पेज को डिकम्प्रेस करती है, कॉन्फ़िगर किए गए DPI पर रास्टराइज़ करती है, और बिटमैप को अपने न्यूरल‑नेटवर्क मॉडल में फीड करती है। परिणाम? `Page` ऑब्जेक्ट्स का एक कलेक्शन जो एक्सट्रैक्शन के लिए तैयार है।

## Step 5: Retrieve and Display the Recognized Text (convert PDF to text)

अंत में, हम रिटर्न किए गए पेजेज़ पर लूप लगाते हैं और पहचाना गया टेक्स्ट प्रिंट करते हैं। यही वह क्षण है जब **convert PDF to text** वास्तव में होता है।

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### Expected Output

यदि `multipage.pdf` में तीन स्कैन किए गए पेज हैं, तो आपको कुछ इस तरह दिखाई देगा:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

पेजेज़ के बीच साफ़ विभाजन पर ध्यान दें—यह उपयोगी है यदि आपको प्रत्येक पेज का टेक्स्ट डेटाबेस में स्टोर करना है या उसे डाउनस्ट्रीम NLP मॉडल में फ़ीड करना है।

## Handling Common Edge Cases

### 1. PDFs with Mixed Image and Text Layers

कुछ PDFs में पहले से ही हिडन टेक्स्ट लेयर होती है (जैसे, Word से एक्सपोर्ट किया गया)। यदि आप चाहते हैं कि OCR इंजन **ignore existing text** करे और इमेज को फिर से प्रोसेस करे, तो सेट करें:

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. Large Files Exceeding Memory Limits

जब आप गीगाबाइट‑साइज़ PDFs के साथ काम कर रहे हों, तो चंक्स में प्रोसेस करने पर विचार करें:

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. Language and Font Support

यदि आपके स्कैन किए हुए दस्तावेज़ फ्रेंच में हैं या विशेष कैरेक्टर्स शामिल हैं, तो इंजन को बताएं कि कौन सा लैंग्वेज मॉडल उपयोग करना है:

```python
settings.set_language("fr")   # or "en", "de", etc.
```

## Full Script – Ready to Run

नीचे पूरा, रन करने योग्य उदाहरण है जो सभी हिस्सों को जोड़ता है। इसे `ocr_pdf.py` के रूप में सेव करें और `python ocr_pdf.py` चलाएँ।

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**Running the script** प्रत्येक पेज का टेक्स्ट कंसोल में प्रिंट करेगा, बिल्कुल “Expected Output” सेक्शन में दिखाए अनुसार। यहाँ से आप आउटपुट को फ़ाइल में रीडायरेक्ट कर सकते हैं:

```bash
python ocr_pdf.py > extracted_text.txt
```

## Conclusion

हमने अभी-अभी **how to OCR PDF** फ़ाइलों को Python में शुरू से अंत तक कवर किया। इंजन को कॉन्फ़िगर करके, स्ट्रीम के माध्यम से डॉक्यूमेंट लोड करके, और प्रत्येक पहचाने गए पेज पर इटररेट करके, आप **extract text from PDF**, **convert PDF to text**, और **process scanned PDF** कुछ ही लाइनों में कर सकते हैं। यह अप्रोच छोटे दो‑पेज इनवॉइस से लेकर बड़े सैकड़ों‑पेज आर्काइव तक स्केलेबल है।

अब क्या करना है? निकाले गए स्ट्रिंग्स को सर्च इंडेक्स, लैंग्वेज‑मॉडल सारांशकर्ता, या डेटा‑वैलिडेशन पाइपलाइन में फ़ीड करने की कोशिश करें। आप JSON जैसे आउटपुट फॉर्मेट्स के साथ भी प्रयोग कर सकते हैं ताकि एडवांस्ड डॉक्यूमेंट एनालिसिस के लिए पोज़िशनल मेटाडेटा रख सकें।

एन्क्रिप्टेड PDFs को हैंडल करने या क्लाउड स्टोरेज के साथ इंटीग्रेट करने के बारे में प्रश्न हैं? नीचे कमेंट करें—हैप्पी कोडिंग!

![OCR PDF वर्कफ़्लो दिखाने वाला आरेख – how to OCR PDF, load PDF from stream, recognize pages, and extract text](ocr-pdf-workflow.png "how to OCR PDF वर्कफ़्लो आरेख")

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और स्टेप‑बाय‑स्टेप व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}