---
category: general
date: 2026-05-31
description: Python OCR का उपयोग करके स्कैन की गई छवियों से खोज योग्य PDF बनाएं। सीखें
  कि स्कैन की गई इमेज PDF को कैसे बदलें, TIFF को PDF में कैसे परिवर्तित करें, और मिनटों
  में OCR टेक्स्ट लेयर कैसे जोड़ें।
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: hi
og_description: तुरंत खोज योग्य PDF बनाएं। यह गाइड दिखाता है कि कैसे OCR चलाएँ, स्कैन
  किए गए इमेज PDF को परिवर्तित करें, और एक ही पायथन स्क्रिप्ट का उपयोग करके OCR टेक्स्ट
  लेयर जोड़ें।
og_title: Python के साथ खोज योग्य PDF बनाएं – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Python के साथ खोज योग्य PDF बनाएं – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python से Searchable PDF बनाएं – चरण‑दर‑चरण गाइड

क्या आपने कभी सोचा है कि **स्कैन की गई पेज से searchable PDF** कैसे बनाएं बिना कई टूल्स के झंझट के? आप अकेले नहीं हैं। कई ऑफिस वर्कफ़्लो में एक स्कैन किया हुआ TIFF या JPEG साझा ड्राइव पर आता है, और अगला व्यक्ति टेक्स्ट को मैन्युअली कॉपी‑पेस्ट करता है—दुखद, त्रुटिप्रवण, और समय‑सापेक्ष।  

इस ट्यूटोरियल में हम एक साफ़, प्रोग्रामेटिक समाधान देखेंगे जो आपको **स्कैन की गई इमेज PDF को कन्वर्ट**, **TIFF को PDF में बदल**, और **OCR टेक्स्ट लेयर जोड़** एक ही बार में देता है। अंत तक आपके पास एक तैयार‑स्क्रिप्ट होगा जो OCR चलाता है, छिपा हुआ टेक्स्ट एम्बेड करता है, और एक searchable PDF आउटपुट करता है जिसे आप इंडेक्स, सर्च या भरोसे के साथ शेयर कर सकते हैं।

## आपको क्या चाहिए

- Python 3.9+ (कोई भी हालिया संस्करण चलेगा)
- `aspose-ocr` और `aspose-pdf` पैकेज ( `pip install aspose-ocr aspose-pdf` के माध्यम से इंस्टॉल)
- एक स्कैन की गई इमेज फ़ाइल (`.tif`, `.png`, `.jpg`, या यहाँ तक कि एक PDF पेज जो सिर्फ इमेज है)
- थोड़ा RAM (OCR इंजन हल्का है; लैपटॉप भी संभाल सकता है)

> **Pro tip:** यदि आप Windows पर हैं, तो पैकेज प्राप्त करने का सबसे आसान तरीका है कि आप कमांड को एक एलेवेटेड PowerShell विंडो में चलाएँ।

```bash
pip install aspose-ocr aspose-pdf
```

अब जब प्री‑रिक्विज़िट्स समाप्त हो गए हैं, चलिए कोड में डुबकी लगाते हैं।

## Step 1: OCR Engine इंस्टेंस बनाएं – *create searchable pdf*

सबसे पहले हम OCR इंजन को स्पिन‑अप करते हैं। इसे वह दिमाग समझें जो हर पिक्सेल को पढ़ेगा और उसे अक्षरों में बदल देगा।

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **यह क्यों महत्वपूर्ण है:** इंजन को केवल एक बार इनिशियलाइज़ करने से मेमोरी उपयोग कम रहता है। यदि आप प्रत्येक पेज के लिए `OcrEngine()` को लूप में कॉल करेंगे, तो जल्दी ही रिसोर्सेज ख़त्म हो जाएंगे।

## Step 2: स्कैन की गई इमेज लोड करें – *convert tiff to pdf* & *convert scanned image pdf*

अब, इंजन को उस फ़ाइल की ओर इंगित करें जिसे आप प्रोसेस करना चाहते हैं। API किसी भी रास्टर इमेज को स्वीकार करता है, इसलिए TIFF भी JPEG की तरह काम करेगा।

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

यदि आपके पास ऐसा PDF है जिसमें केवल स्कैन की गई इमेज है, तो आप अभी भी `load_image` का उपयोग कर सकते हैं क्योंकि Aspose स्वचालित रूप से पहला पेज एक्सट्रैक्ट कर लेगा।

## Step 3: PDF Save Options तैयार करें – *add OCR text layer*

यहाँ हम यह कॉन्फ़िगर करते हैं कि अंतिम PDF कैसे दिखेगा। मुख्य फ़्लैग है `create_searchable_pdf`; इसे `True` सेट करने से लाइब्रेरी एक अदृश्य टेक्स्ट लेयर एम्बेड करती है जो विज़ुअल कंटेंट को मिरर करती है।

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **टेक्स्ट लेयर क्या करती है:** जब आप परिणामी फ़ाइल को Adobe Reader में खोलते हैं और टेक्स्ट सिलेक्ट करने की कोशिश करते हैं, तो आपको छिपे हुए कैरेक्टर्स दिखेंगे। सर्च इंजन भी इन्हें इंडेक्स कर सकते हैं—कम्प्लायंस या आर्काइविंग के लिए परफेक्ट।

## Step 4: OCR चलाएँ और सेव करें – *how to run OCR* in a single call

अब जादू होता है। एक मेथड कॉल पूरे रिकग्निशन इंजन को चलाता है और searchable PDF को डिस्क पर लिख देता है।

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

`recognize` मेथड एक स्टेटस ऑब्जेक्ट रिटर्न करता है जिसे आप एरर्स के लिए जांच सकते हैं, लेकिन अधिकांश सरल परिदृश्यों में ऊपर दिया गया सिंगल कॉल पर्याप्त है।

### Expected Output

स्क्रिप्ट चलाने पर प्रिंट होगा:

```
PDF saved as searchable PDF.
```

यदि आप `scanned_page_searchable.pdf` खोलते हैं तो आप देखेंगे कि आप टेक्स्ट सिलेक्ट, कॉपी‑पेस्ट कर सकते हैं, और `Ctrl+F` सर्च भी चला सकते हैं। यही **create searchable pdf** वर्कफ़्लो की पहचान है।

## Full Working Script

नीचे पूरा, तैयार‑चलाने योग्य स्क्रिप्ट दिया गया है। प्लेसहोल्डर पाथ्स को अपने वास्तविक फ़ाइल लोकेशन से बदलें।

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

इसे `create_searchable_pdf.py` के रूप में सेव करें और चलाएँ:

```bash
python create_searchable_pdf.py
```

## सामान्य प्रश्न और एज केस

### 1️⃣ क्या मैं मल्टी‑पेज PDFs प्रोसेस कर सकता हूँ?

हां। `ocr_engine.load_image("file.pdf")` उपयोग करें और फिर प्रत्येक पेज के लिए `ocr_engine.recognize(pdf_save_options, page_number)` लूप में कॉल करें। लाइब्रेरी स्वचालित रूप से मल्टी‑पेज searchable PDF जेनरेट करेगी।

### 2️⃣ यदि मेरा स्रोत फ़ाइल हाई‑रेज़ोल्यूशन TIFF (300 dpi+) है तो क्या करें?

उच्च DPI बेहतर OCR सटीकता देता है लेकिन मेमोरी उपयोग भी बढ़ाता है। यदि आप `MemoryError` का सामना करते हैं, तो पहले इमेज को डाउनस्केल करें:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ OCR की भाषा कैसे बदलूँ?

इंजन को इमेज लोड करने से पहले `language` प्रॉपर्टी सेट करें:

```python
ocr_engine.language = "fra"   # French
```

समर्थित भाषा कोड की पूरी सूची Aspose डॉक्यूमेंटेशन में उपलब्ध है।

### 4️⃣ यदि मुझे मूल इमेज क्वालिटी बनाए रखनी है तो क्या करें?

`PdfSaveOptions` क्लास में `compression` प्रॉपर्टी है। इसे `PdfCompression.None` सेट करने से रास्टर डेटा बिल्कुल वैसा ही रहेगा जैसा था।

```python
pdf_save_options.compression = "None"
```

## प्रोडक्शन‑रेडी डिप्लॉयमेंट के टिप्स

- **बैच प्रोसेसिंग:** कोर लॉजिक को एक फ़ंक्शन में रैप करें जो फ़ाइल पाथ्स की लिस्ट लेता हो। प्रत्येक सफलता/विफलता को ऑडिट ट्रेल के लिए CSV में लॉग करें।
- **पैरालेलिज़्म:** `concurrent.futures.ThreadPoolExecutor` का उपयोग करके कई कोर पर OCR चलाएँ। बस याद रखें कि प्रत्येक थ्रेड को अपना `OcrEngine` इंस्टेंस चाहिए।
- **सिक्योरिटी:** यदि आप संवेदनशील दस्तावेज़ों को हैंडल कर रहे हैं, तो स्क्रिप्ट को सैंडबॉक्स्ड एनवायरनमेंट में चलाएँ और प्रोसेसिंग के बाद टेम्प फ़ाइलें तुरंत डिलीट कर दें।

## निष्कर्ष

अब आप जानते हैं कि कैसे **create searchable PDF** फ़ाइलें स्कैन की गई इमेजेज़ से एक संक्षिप्त Python स्क्रिप्ट के माध्यम से बनाएं। OCR इंजन को इनिशियलाइज़ करके, TIFF (या कोई भी रास्टर) लोड करके, `PdfSaveOptions` को **add OCR text layer** के लिए कॉन्फ़िगर करके, और अंत में `recognize` कॉल करके, पूरा **convert scanned image pdf** और **convert TIFF to PDF** पाइपलाइन एक ही दोहराने योग्य कमांड बन जाता है।

अगला कदम? इस स्क्रिप्ट को एक फ़ाइल‑वॉचर के साथ जोड़ें ताकि कोई भी नई स्कैन फ़ोल्डर में डाली जाए तो वह स्वचालित रूप से searchable बन जाए। या विभिन्न OCR भाषाओं के साथ प्रयोग करें ताकि बहुभाषी आर्काइव्स को सपोर्ट किया जा सके। OCR को PDF जेनरेशन के साथ मिलाकर संभावनाएँ असीमित हैं।

**how to run OCR** को अन्य भाषाओं या फ्रेमवर्क में उपयोग करने के बारे में और सवाल हैं? नीचे कमेंट करें, और हैप्पी कोडिंग! 

![Diagram showing the flow from scanned image → OCR engine → searchable PDF (create searchable pdf)](searchable-pdf-flow.png "Create searchable pdf flow diagram")


## आगे आप क्या सीखें?

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}