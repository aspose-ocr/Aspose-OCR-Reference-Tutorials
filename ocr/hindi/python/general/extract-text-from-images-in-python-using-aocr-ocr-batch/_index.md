---
category: general
date: 2026-06-25
description: Python aocr लाइब्रेरी के साथ छवियों से टेक्स्ट निकालें – बैच OCR सीखें,
  पहचान मोड को प्रिंटेड सेट करें, और एक AI पोस्टप्रोसेसर जोड़ें।
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: hi
og_description: Python aocr लाइब्रेरी का उपयोग करके छवियों से टेक्स्ट निकालें। यह
  ट्यूटोरियल बैच OCR, प्रिंटेड रिकग्निशन मोड, और वैकल्पिक AI पोस्टप्रोसेसर दिखाता
  है।
og_title: Python में छवियों से टेक्स्ट निकालें – पूर्ण aocr बैच गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Python में aocr OCR बैच का उपयोग करके छवियों से टेक्स्ट निकालें
url: /hi/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में aocr OCR बैच का उपयोग करके छवियों से टेक्स्ट निकालें

क्या आपको कभी **छवियों से टेक्स्ट निकालना** पड़ा है लेकिन दहियों छोटे‑छोटे कदमों से अभिभूत महसूस किया? आप अकेले नहीं हैं। चाहे आप स्कैन किए हुए फ़ॉर्म को डिजिटल बना रहे हों, रसीदों से डेटा निकाल रहे हों, या एक खोज योग्य अभिलेख बना रहे हों, बड़े पैमाने पर भरोसेमंद OCR परिणाम प्राप्त करना एक खड़ी पहाड़ी चढ़ने जैसा लग सकता है।

अच्छी खबर? **aocr लाइब्रेरी** के साथ आप सिर्फ कुछ ही पंक्तियों में एक पूर्ण **Python OCR बैच** बना सकते हैं। इस गाइड में हम OCR बैच बनाने, फ़ोल्डर से सभी समर्थित छवियों को लोड करने, सही **recognition mode printed** चुनने, और अतिरिक्त सटीकता के लिए **AI postprocessor** जोड़ने की प्रक्रिया को चरण‑दर‑चरण देखेंगे। अंत तक आपके पास एक तैयार‑चलाने‑योग्य स्क्रिप्ट होगी जो छवियों से टेक्स्ट निकालती है और प्रत्येक फ़ाइल के लिए कैप्चर किए गए टेक्स्ट की मात्रा बताती है।

## आप क्या सीखेंगे

- `aocr` पैकेज को कैसे स्थापित और इम्पोर्ट करें।
- `OcrBatch` को सेट‑अप करके हजारों फ़ाइलों को स्वचालित रूप से संभालें।
- प्रिंटेड दस्तावेज़ों के लिए सर्वोत्तम recognition mode चुनें।
- (वैकल्पिक) शोरयुक्त परिणामों को साफ़ करने के लिए AI post‑processor जोड़ें।
- प्रत्येक फ़ाइल पाथ के साथ उसके निकाले गए टेक्स्ट की लंबाई दिखाएँ।
- असमर्थित फ़ॉर्मेट या खाली पेज़ जैसी किनारी स्थितियों को संभालने के टिप्स।

### पूर्वापेक्षाएँ

- आपके मशीन पर Python 3.8 या उससे नया स्थापित हो।  
- Python स्क्रिप्टिंग (लूप, इम्पोर्ट आदि) की बुनियादी समझ।  
- स्कैन की गई छवियों (PNG, JPG, TIFF आदि) वाला फ़ोल्डर उपलब्ध हो।  

यदि आपके पास ये सब है, तो चलिए शुरू करते हैं—बिना किसी बाहरी सेवा के।

## चरण 1: aocr लाइब्रेरी स्थापित करें

सबसे पहले। `aocr` पैकेज स्टैंडर्ड लाइब्रेरी का हिस्सा नहीं है, इसलिए आपको इसे PyPI से डाउनलोड करना होगा।

```bash
pip install aocr
```

> **Pro tip:** निर्भरताओं को अलग रखने के लिए एक वर्चुअल एनवायरनमेंट (`python -m venv .venv`) का उपयोग करें।  

इंस्टॉल होने के बाद, आप कोर क्लासेज़ को इम्पोर्ट कर सकते हैं।

```python
# core imports
import aocr
```

## चरण 2: OCR बैच इंस्टेंस बनाएं

`OcrBatch` वह कार्यकर्ता है जो आपके डायरेक्टरी को स्कैन करेगा और हर इमेज फ़ाइल का ट्रैक रखेगा। इसे एक कन्वेयर बेल्ट की तरह समझें जो चित्रों को OCR इंजन में फीड करता है।

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

इस चरण पर बैच खाली है, लेकिन अगले चरण में हम इसे भरेंगे।

## चरण 3: फ़ोल्डर से सभी समर्थित छवियों को (रिकर्सिवली) जोड़ें

आपके पास संभवतः नेस्टेड फ़ोल्डर स्ट्रक्चर है—शायद क्लाइंट या महीने के अनुसार सब‑फ़ोल्डर। `add_folder` मेथड आपके लिए ट्री को ट्रैवर्स करता है और हर पढ़ी जा सकने वाली इमेज को जोड़ता है।

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

`"YOUR_DIRECTORY/scanned_forms/"` को अपने सिस्टम के वास्तविक पाथ से बदलें। इस कॉल के बाद `ocr_batch.file_paths` में पूर्ण फ़ाइल नामों की सूची होगी, और बैच को ठीक‑ठीक पता होगा कि उसे कितनी आइटम प्रोसेस करनी हैं।

## चरण 4: प्रिंटेड टेक्स्ट के लिए Recognition Mode चुनें

`aocr` इंजन कई मोड सपोर्ट करता है (हैंडराइटन, प्रिंटेड, मिक्स्ड)। चूँकि हम साफ़, प्रिंटेड फ़ॉर्म्स के साथ काम कर रहे हैं, इसलिए मोड को उसी अनुसार सेट करें। यह छोटा फ़्लैग सटीकता को काफी बढ़ा सकता है क्योंकि इंजन कर्सिव स्क्रिप्ट्स के लिए आवश्यक भारी‑हैंडेड ह्यूरिस्टिक्स को स्किप कर देता है।

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **क्यों महत्वपूर्ण है:** प्रिंटेड टेक्स्ट में बेसलाइन और कैरेक्टर शैप्स लगातार होते हैं, जिससे OCR मॉडल टाइटर कैरेक्टर डिक्शनरी लागू कर सकता है। यदि आप मोड को “auto” रखते हैं तो लो‑रेज़ोल्यूशन स्कैन पर अतिरिक्त शोर मिल सकता है।

## चरण 5: (वैकल्पिक) AI Post‑Processor जोड़ें

यदि आपके स्कैन ब्लर, कम कॉन्ट्रास्ट, या अजीब फ़ॉन्ट्स से ग्रस्त हैं, तो AI post‑processor कच्चे OCR आउटपुट को साफ़ कर सकता है, इससे पहले कि आप इसे डाउनस्ट्रीम सिस्टम को दें। `set_ai_postprocessor` मेथड एक ऐसे ऑब्जेक्ट की अपेक्षा करता है जो `process(text: str) -> str` इंटरफ़ेस को इम्प्लीमेंट करता हो।

नीचे एक न्यूनतम उदाहरण है जिसमें एक काल्पनिक `SimpleCleaner` क्लास का उपयोग किया गया है। वास्तविक प्रोजेक्ट में आप HuggingFace ट्रांसफ़ॉर्मर, कस्टम लैंग्वेज मॉडल, या यहाँ तक कि नियम‑आधारित स्पेल‑चेकर भी लगा सकते हैं।

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

यदि आप इस चरण को छोड़ देते हैं, तो बैच केवल कच्ची OCR स्ट्रिंग्स लौटाएगा।

## चरण 6: पूरे बैच पर OCR चलाएँ और परिणाम एकत्र करें

अब असली काम शुरू होता है। `run` मेथड हर फ़ाइल पर लूप करता है, OCR इंजन चलाता है, वैकल्पिक AI post‑processor के माध्यम से आउटपुट पास करता है, और स्ट्रिंग्स की एक सूची लौटाता है—प्रति इमेज एक।

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

चूंकि मेथड एक साधारण Python लिस्ट लौटाता है, आप इसे किसी भी कलेक्शन की तरह उपयोग कर सकते हैं—स्टोर करें, CSV में लिखें, या डेटाबेस में फीड करें।

## चरण 7: प्रत्येक फ़ाइल पाथ के साथ निकाले गए टेक्स्ट की लंबाई दिखाएँ

एक त्वरित वैधता जांच के लिए प्रिंट करें कि प्रत्येक फ़ाइल से कितने कैरेक्टर निकाले गए। यदि कोई पेज़ खाली है या OCR फेल हो गया, तो आप `0` लंबाई देखेंगे।

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

आम तौर पर आउटपुट इस प्रकार दिखता है:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

`0` फ़्लैग तुरंत बताता है कि किन फ़ाइलों को दोबारा देखना चाहिए (शायद वे करप्ट हैं या इमेज नहीं हैं)।

## सामान्य किनारी स्थितियों को संभालना

### 1. असमर्थित फ़ाइल टाइप्स

`aocr` उन फ़ाइलों को चुपचाप स्किप कर देता है जिन्हें वह डिकोड नहीं कर सकता। यदि आपको संदेह है कि आपके पास PDFs या BMPs मिश्रित हैं, तो पहले उन्हें फ़िल्टर करें:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. बड़े बैच और मेमोरी खपत

हजारों हाई‑रेज़ोल्यूशन स्कैन चलाने से मेमोरी उपयोग बहुत बढ़ सकता है। इसे चंक्स में प्रोसेस करके कम करें:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. खाली या लो‑कॉन्ट्रास्ट पेज़

यदि किसी पेज़ पर 10 से कम कैरेक्टर निकले हैं, तो आप उसे मैन्युअल रिव्यू के लिए फ़्लैग कर सकते हैं:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ मिलाकर, यहाँ एक स्क्रिप्ट है जिसे आप कॉपी‑पेस्ट करके तुरंत चला सकते हैं। इसे `batch_ocr.py` के रूप में सेव करें।

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**अपेक्षित आउटपुट** (संक्षिप्त रूप में):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

इसे इस तरह चलाएँ:

```bash
python batch_ocr.py
```

यदि सब कुछ सही ढंग से सेट है, तो आपको हर इमेज के लिए एक लाइन दिखेगी, जिसमें निकाले गए टेक्स्ट की कैरेक्टर काउंट रिपोर्ट होगी।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या यह PDFs पर काम करता है?**  
उत्तर: बॉक्स‑से‑बॉक्स नहीं। `aocr` केवल रास्टर इमेजेस को संभालता है। PDFs को पहले PNG/TIFF में बदलें (उदाहरण के लिए `pdf2image` का उपयोग करके)।

**प्रश्न: क्या मैं recognition mode को handwritten में बदल सकता हूँ?**  
उत्तर: बिल्कुल—सिर्फ `aocr.RecognitionMode.PRINTED` को `aocr.RecognitionMode.HANDWRITTEN` से बदल दें। इससे रन टाइम थोड़ा धीमा होगा लेकिन कर्सिव नोट्स पर बेहतर परिणाम मिलेंगे।

**प्रश्न: यदि मुझे बहुभाषी समर्थन चाहिए तो?**  
उत्तर: लाइब्रेरी भाषा पैक्स के साथ आती है। इच्छित भाषा मॉड्यूल इंस्टॉल करें (`pip install aocr-lang-fr` फ़्रेंच के लिए, आदि) और चलाने से पहले `ocr_batch.language = "fr"` सेट करें।

## अगले कदम और संबंधित विषय

- **पैरेलल प्रोसेसिंग:** बैच निष्पादन को `concurrent.futures.ThreadPoolExecutor` में रैप करके कई CPU कोर उपयोग करें।  
- **परिणाम संग्रहीत करना:** `ocr_results` को CSV या SQLite डेटाबेस में लिखें ताकि डाउनस्ट्रीम एनालिटिक्स हो सके।  
- **क्लाउड AI के साथ इंटीग्रेशन:** `SimpleCleaner` को HuggingFace के ट्रांसफ़ॉर्मर मॉडल से बदलें ताकि अत्याधुनिक स्पेलिंग करेक्शन मिल सके।  
- **aocr को फाइन‑ट्यून करना:** यदि आपके पास कस्टम फ़ॉन्ट सेट है, तो `aocr.Trainer` का उपयोग करके प्रिंटेड‑मोड की सटीकता बढ़ाएँ।

---

बस इतना ही—अब आपके पास एक ठोस

## आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [Aspose OCR के साथ छवि से टेक्स्ट निकालें – चरण‑दर‑चरण गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [फ़ोल्डरों पर OCR ऑपरेशन का उपयोग करके छवियों से टेक्स्ट निकालें](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Aspose.OCR for .NET में सूची के साथ बैच OCR छवियों को कैसे करें](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}