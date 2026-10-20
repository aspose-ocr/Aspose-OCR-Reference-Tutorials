---
category: general
date: 2026-03-28
description: Python के साथ PDF को जल्दी OCR करने का तरीका सीखें। यह गाइड आपको दिखाता
  है कि PDF से टेक्स्ट कैसे निकालें, PDF से टेक्स्ट कैसे पहचानें, और Aspose OCR का
  उपयोग करके स्कैन किए गए PDF को टेक्स्ट में कैसे बदलें।
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: hi
og_description: Python के साथ PDF को OCR करने में माहिर बनें। PDF से टेक्स्ट निकालें,
  PDF से टेक्स्ट पहचानें, और स्कैन किए गए PDF को मिनटों में टेक्स्ट में बदलें।
og_title: Python में PDF को OCR कैसे करें – पूर्ण गाइड
tags:
- PDF
- OCR
- Python
- Aspose
title: Python में PDF को OCR कैसे करें – चरण‑दर‑चरण गाइड
url: /hi/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में PDF को OCR कैसे करें – चरण‑दर‑चरण गाइड

क्या आपने कभी सोचा है **how to OCR PDF** जब फ़ाइल केवल पेज की तस्वीर हो? आप अकेले नहीं हैं। इस ट्यूटोरियल में हम OCR PDF फ़ाइलों के सटीक चरणों को देखेंगे, PDF से टेक्स्ट निकालेंगे, और स्कैन किए गए PDF को सर्चेबल टेक्स्ट में बदलेंगे—सिर्फ साधारण Python कोड के साथ।

हम सब कुछ Aspose OCR लाइब्रेरी को इंस्टॉल करने से लेकर प्रत्येक पेज से पहचाने गए टेक्स्ट को निकालने तक कवर करेंगे। अंत तक आप **OCR PDF with Python**, **extract text from PDF**, और **convert scanned PDF to text** बिना बिखरे दस्तावेज़ों की खोज किए कर पाएँगे। कोई फालतू बात नहीं, सिर्फ एक व्यावहारिक, चलाने योग्य उदाहरण जिसे आप कॉपी‑पेस्ट कर सकते हैं।

## आपको क्या चाहिए

* Python 3.8+ (नवीनतम स्थिर रिलीज़ सबसे अच्छा काम करती है)  
* Aspose OCR for Python लाइसेंस या एक फ्री ट्रायल कुंजी – आप इसे Aspose वेबसाइट से प्राप्त कर सकते हैं।  
* एक स्कैन किया हुआ PDF जिसे आप प्रोसेस करना चाहते हैं (हम इसे `input.pdf` कहेंगे)।  

यदि आपके पास ये सब पहले से है, तो बढ़िया—आइए शुरू करें। यदि नहीं, तो पैकेज को इंस्टॉल करना बहुत आसान है और हम आपको दिखाएंगे कैसे।

## OCR PDF कैसे करें – पर्यावरण सेटअप

सबसे पहले आपको Aspose OCR मॉड्यूल को अपने मशीन पर लाना होगा। पैकेज का नाम `aspose-ocr` है, और आप इसे pip के माध्यम से इंस्टॉल कर सकते हैं:

```bash
pip install aspose-ocr
```

> **Pro tip:** एक वर्चुअल एनवायरनमेंट (`python -m venv venv`) का उपयोग करें ताकि आपकी डिपेंडेंसीज़ व्यवस्थित रहें।

पैकेज इंस्टॉल हो जाने के बाद, आप इसे इम्पोर्ट करने और OCR इंजन को शुरू करने के लिए तैयार हैं। यह हर **ocr pdf with python** वर्कफ़्लो की बुनियाद है जिसे आप बाद में बनाएँगे।

## Python के साथ OCR PDF – Aspose OCR को इम्पोर्ट करना

अब लाइब्रेरी उपलब्ध है, चलिए इसे अपने स्क्रिप्ट में लाते हैं। हम इंजन को *direct PDF mode* में सेट करेंगे, जो Aspose को PDF बाइट्स को सीधे फ़ाइल से पढ़ने का निर्देश देता है, बजाय प्रत्येक पेज को पहले इमेज में बदलने के।

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

`PdfMode.DIRECT` क्यों उपयोग करें? क्योंकि यह अतिरिक्त रास्टराइज़ेशन स्टेप को छोड़ देता है, जिससे प्रक्रिया तेज़ होती है और मूल लेआउट बरकरार रहता है—विशेष रूप से तब उपयोगी जब आपको **recognize text from PDF** सटीक रूप से चाहिए।

## PDF से टेक्स्ट पहचानें – इंजन चलाना

इंजन तैयार होने पर, इसे अपने स्कैन किए हुए फ़ाइल की ओर इंगित करें। `recognize_from_pdf` मेथड सभी भारी काम करता है: यह प्रत्येक पेज को पार्स करता है, OCR एल्गोरिद्म चलाता है, और एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें `Page` ऑब्जेक्ट्स का संग्रह होता है।

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

यदि आप सोच रहे हैं कि यह एन्क्रिप्टेड PDFs के साथ काम करता है या नहीं—हां, जब तक आप `ocr_engine.password = "secret"` के माध्यम से पासवर्ड प्रदान करते हैं `recognize_from_pdf` को कॉल करने से पहले। यह एक एज केस है जिसे कई ट्यूटोरियल छोड़ देते हैं, लेकिन वास्तविक‑दुनिया के पाइपलाइन में उपयोगी है।

## PDF से टेक्स्ट निकालें – पेज परिणामों तक पहुँच

`ocr_result.pages` सूची में प्रत्येक पेज के लिए एक एंट्री होती है। प्रत्येक `Page` ऑब्जेक्ट में `.text` एट्रिब्यूट होता है जिसमें स्कैन किए हुए पेज का प्लेन‑टेक्स्ट प्रतिनिधित्व होता है। चलिए लूप लगाते हैं और परिणाम प्रिंट करते हैं ताकि आप ठीक वही देख सकें जो निकाला गया है।

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

स्क्रिप्ट चलाने पर कुछ इस तरह का आउटपुट मिलेगा:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

यह आउटपुट साबित करता है कि आपने सफलतापूर्वक **extract text from PDF** और **recognize text from PDF** Aspose OCR का उपयोग करके किया है। अब आप इन स्ट्रिंग्स को डेटाबेस, सर्च इंडेक्स, या किसी भी डाउनस्ट्रीम NLP पाइपलाइन में पाइप कर सकते हैं।

![how to ocr pdf example](placeholder-image.png "how to ocr pdf example")

*Image alt text:* **how to ocr pdf example** – प्रत्येक पेज के पहचाने गए टेक्स्ट का कंसोल आउटपुट दिखाता है।

## स्कैन किए गए PDF को टेक्स्ट में बदलें – आउटपुट सहेजना

ज्यादातर डेवलपर्स केवल कंसोल में टेक्स्ट देखना नहीं चाहते; उन्हें एक स्थायी फ़ाइल चाहिए। नीचे एक छोटा हेल्पर है जो प्रत्येक पेज के टेक्स्ट को अलग `.txt` फ़ाइल में लिखता है, प्रभावी रूप से **convert scanned PDF to text** `output` नामक फ़ोल्डर में करता है।

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

स्क्रिप्ट समाप्त होने के बाद आपके पास एक व्यवस्थित डायरेक्टरी होगी:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

अब आपने पूरी तरह से **convert scanned PDF to text** कर लिया है और उन फ़ाइलों को किसी भी डाउनस्ट्रीम प्रोसेस—सर्च, एनालिटिक्स, या यहाँ तक कि एक साधारण `grep`—में फीड कर सकते हैं।

## सामान्य प्रश्न और किनारे के मामलों

**यदि मेरा PDF वास्तविक टेक्स्ट के साथ मिश्रित इमेजेज़ रखता है तो क्या होगा?**  
Aspose OCR सब कुछ पहचानने की कोशिश करेगा, लेकिन आप उन पेजों के लिए OCR को डिसेबल करके गति बढ़ा सकते हैं जिनमें पहले से ही सिलेक्टेबल टेक्स्ट है। `ocr_engine.auto_detect_page_orientation = True` सेट करें और फिर ज्ञात‑अच्छे पेजों के लिए `ocr_engine.recognize_from_pdf(..., detect_text=False)` कॉल करें।

**क्या मैं भाषा मॉडल को नियंत्रित कर सकता हूँ?**  
बिल्कुल। `ocr_engine.language = aocr.Language.English` (या कोई भी समर्थित भाषा) को `recognize_from_pdf` कॉल करने से पहले सेट करें। यह गैर‑English दस्तावेज़ों की सटीकता को बढ़ाता है।

**बहुत बड़े PDFs (100+ पेज) को कैसे हैंडल करें?**  
उन्हें चंक्स में प्रोसेस करें। `recognize_from_pdf` मेथड `page_range` आर्ग्यूमेंट स्वीकार करता है, उदाहरण के लिए `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`। मेमोरी उपयोग कम रखने के लिए रेंज पर लूप करें।

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ रखने के लिए, यहाँ एक सिंगल स्क्रिप्ट है जिसे आप `ocr_pdf.py` नाम की फ़ाइल में डाल सकते हैं और चला सकते हैं:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

इसे इस तरह चलाएँ:

```bash
python ocr_pdf.py
```

आपको कंसोल आउटपुट में प्रत्येक पेज का टेक्स्ट और सहेजी गई `.txt` फ़ाइलों का स्थान दिखना चाहिए।

## निष्कर्ष

हमने Python का उपयोग करके **how to OCR PDF** को कवर किया, एक साफ़ तरीका दिखाया **ocr pdf with python** का, बताया **extract text from PDF** कैसे किया जाए, **recognize text from PDF** के मैकेनिक्स को समझाया, और अंत में एक तैयार‑से‑उपयोग स्निपेट दिया जो **convert scanned PDF to text** करता है। पूरा प्रोसेस अब...

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}