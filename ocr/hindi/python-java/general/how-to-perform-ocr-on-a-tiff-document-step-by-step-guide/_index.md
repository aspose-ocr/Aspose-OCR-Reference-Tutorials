---
category: general
date: 2026-01-12
description: OCR को तेज़ और सटीक रूप से कैसे करें। दस्तावेज़ पर OCR चलाना, TIFF से
  टेक्स्ट निकालना, OCR के लिए इमेज लोड करना और Python में OCR भाषा सेट करना सीखें।
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: hi
og_description: Python में OCR कैसे करें। यह ट्यूटोरियल दिखाता है कि दस्तावेज़ पर
  OCR कैसे चलाएँ, TIFF से टेक्स्ट निकालें, OCR के लिए इमेज लोड करें और OCR भाषा सेट
  करें।
og_title: TIFF दस्तावेज़ पर OCR कैसे करें – पूर्ण गाइड
tags:
- OCR
- Python
- Image Processing
title: TIFF दस्तावेज़ पर OCR कैसे करें – चरण‑दर‑चरण गाइड
url: /hi/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF दस्तावेज़ पर OCR कैसे करें – पूर्ण गाइड

क्या आप कभी सोचे हैं **OCR कैसे करें** एक स्कैन किए गए TIFF फ़ाइल पर, बिना सही लाइब्रेरी खोजने में घंटों बिताए? आप अकेले नहीं हैं। कई डेवलपर्स को तब समस्या आती है जब उन्हें TIFF इमेज से टेक्स्ट निकालना होता है, विशेष रूप से जब प्रदर्शन और भाषा सेटिंग्स महत्वपूर्ण होते हैं।

इस ट्यूटोरियल में हम वह सब कवर करेंगे जो आपको जानना आवश्यक है: OCR पैकेज को इंस्टॉल करने से लेकर, OCR के लिए इमेज लोड करने, OCR भाषा सेट करने, और अंत में **दस्तावेज़ पर OCR चलाने** तक। अंत तक आपके पास एक तैयार‑से‑चलाने वाला स्क्रिप्ट होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं।

> **प्रो टिप:** जबकि उदाहरण में एक सामान्य `ocr` मॉड्यूल का उपयोग किया गया है, वही अवधारणाएँ Tesseract, EasyOCR, या किसी भी आधुनिक OCR इंजन पर लागू होती हैं जो Python API प्रदान करता है।

---

## आपको क्या चाहिए

- Python 3.8+ (कोई भी नवीनतम संस्करण काम करेगा)
- एक OCR लाइब्रेरी जो `OcrEngine` क्लास प्रदान करती है (उदाहरण में एक काल्पनिक `ocr` पैकेज का उपयोग किया गया है; इसे अपने वास्तविक पैकेज से बदलें)
- एक मल्टी‑पेज TIFF फ़ाइल जिसे आप प्रोसेस करना चाहते हैं (हम इसे `big_document.tif` कहेंगे)
- यदि आप थ्रेड काउंट सेट करने की योजना बना रहे हैं तो कम से कम 4 CPU कोर वाला मशीन

कोई बाहरी सेवाएँ नहीं, कोई क्लाउड की नहीं—सिर्फ स्थानीय कोड जो सेकंडों में चल जाता है।

![OCR कैसे करें उदाहरण](/images/ocr-example.png "TIFF दस्तावेज़ पर OCR कैसे करें – निकाले गए टेक्स्ट का पूर्वावलोकन")

*छवि वैकल्पिक पाठ: TIFF दस्तावेज़ पर OCR कैसे करें – निकाले गए टेक्स्ट का पूर्वावलोकन.*

---

## चरण 1: OCR लाइब्रेरी स्थापित करें और इम्पोर्ट करें

सबसे पहले: लाइब्रेरी को अपने मशीन पर प्राप्त करें। अधिकांश OCR पैकेज PyPI पर उपलब्ध हैं, इसलिए एक साधारण `pip install` ही काम कर देता है।

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

अब उन क्लासेज़ को इम्पोर्ट करें जिनकी आपको आवश्यकता होगी। यदि आप Tesseract का उपयोग कर रहे हैं, तो इम्पोर्ट लाइन अलग दिखेगी, लेकिन बाकी कोड समान रहेगा।

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*क्यों यह महत्वपूर्ण है:* सही सिम्बॉल्स को पहले इम्पोर्ट करने से बाद में नेमस्पेस टकराव से बचा जा सकता है और स्क्रिप्ट पढ़ने में आसान बनती है।

---

## चरण 2: OCR इंजन बनाएं और कॉन्फ़िगर करें (OCR भाषा सेट करें)

इंजन को कॉन्फ़िगर करना वह जगह है जहाँ आप **OCR भाषा सेट** करते हैं ताकि पहचान सटीक हो। डिफ़ॉल्ट अंग्रेज़ी है, लेकिन आप एक ही लाइन में फ्रेंच, जर्मन, या यहाँ तक कि मल्टी‑लिंगुअल मोड में स्विच कर सकते हैं।

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **क्यों 4 थ्रेड्स?** अधिकांश आधुनिक लैपटॉप में कम से कम चार कोर होते हैं, और थ्रेड काउंट को सीमित करने से OCR प्रक्रिया पूरी मशीन को कब्ज़ा नहीं करती—विशेष रूप से तब उपयोगी जब स्क्रिप्ट साझा सर्वर पर चलती है।

यदि आपको कोई अन्य भाषा चाहिए, तो बस `ocr.Language.ENGLISH` को `ocr.Language.FRENCH`, `ocr.Language.SPANISH` आदि से बदल दें।

---

## चरण 3: OCR के लिए इमेज लोड करें (Load Image for OCR)

अब हम **OCR के लिए इमेज लोड** करते हैं। `Image.load` मेथड TIFF फ़ाइल को मेमोरी में पढ़ता है और मल्टी‑पेज दस्तावेज़ों को स्वचालित रूप से संभालता है।

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*एज केस:* यदि फ़ाइल बहुत बड़ी है, तो RAM खत्म हो सकती है। ऐसे में, `Image.load_page(page_number)` (यदि लाइब्रेरी समर्थन करती है) के साथ एक बार में एक पेज लोड करने पर विचार करें।

---

## चरण 4: दस्तावेज़ पर OCR चलाएँ

इंजन तैयार है और इमेज लोड हो गई है, अब **दस्तावेज़ पर OCR चलाने** का समय है। `process` मेथड भारी काम करता है और एक रिज़ल्ट ऑब्जेक्ट लौटाता है।

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

पर्दे के पीछे, इंजन इमेज को टेक्स्ट ब्लॉक्स में विभाजित करता है, पहचान मॉडल चलाता है, और परिणामों को जोड़ता है। यह कॉल ब्लॉकिंग है, यानी स्क्रिप्ट पूरी TIFF प्रोसेस होने तक रुकती है—बैच जॉब्स के लिए एकदम सही।

---

## चरण 5: TIFF से टेक्स्ट निकालें और आउटपुट सत्यापित करें

अंत में, हम **TIFF से टेक्स्ट निकालते** हैं `result` के `text` एट्रिब्यूट को एक्सेस करके। चलिए पहले 200 कैरेक्टर प्रिंट करते हैं एक त्वरित चेक के लिए।

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**अपेक्षित आउटपुट (उदाहरण):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

यदि आपको पूरा टेक्स्ट चाहिए, तो बस `ocr_result.text` का उपयोग करें। डाउनस्ट्रीम प्रोसेसिंग के लिए आप इसे `.txt` फ़ाइल में लिखना चाह सकते हैं:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ मिलाकर, यहाँ एक तैयार‑से‑चलाने वाला स्क्रिप्ट है। प्लेसहोल्डर पैकेज नाम को उस वास्तविक पैकेज से बदलें जिसे आपने इंस्टॉल किया है।

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

स्क्रिप्ट को इस तरह चलाएँ:

```bash
python ocr_tiff_example.py
```

आपको कंसोल में एक प्रीव्यू दिखेगा और `extracted_text.txt` नाम की फ़ाइल में पूरी ट्रांसक्रिप्शन होगी।

---

## सामान्य प्रश्न और किनारे के मामले

- **यदि TIFF में कई पेज हों तो क्या होगा?**  
  अधिकांश OCR इंजन प्रत्येक पेज को आंतरिक रूप से एक अलग इमेज मानते हैं। `ocr_result.text` में पेजों के बीच एक नई लाइन होगी। यदि आपको पेज‑वाइस हैंडलिंग चाहिए, तो `Image.load_page(page_number)` के साथ इटररेट करें।

- **क्या मैं TIFF की बजाय PNG या JPEG प्रोसेस कर सकता हूँ?**  
  बिल्कुल। `Image.load` मेथड आमतौर पर Pillow या अंतर्निहित लाइब्रेरी द्वारा समर्थित किसी भी फॉर्मेट को स्वीकार करता है। बस फ़ाइल एक्सटेंशन बदल दें।

- **मेरा टेक्स्ट गड़बड़ है—क्या मुझे भाषा बदलनी चाहिए?**  
  हाँ। **OCR भाषा सेट** चरण गैर‑अंग्रेज़ी दस्तावेज़ों के लिए अत्यंत महत्वपूर्ण है। सुनिश्चित करें कि भाषा पैक इंस्टॉल है (जैसे फ्रेंच के लिए `tesseract‑lang‑fra`)।

- **मेमोरी खत्म हो रही है?**  
  `set_memory_limit` को घटाएँ या पेज‑बाय‑पेज प्रोसेस करें। कुछ इंजन आपको पहचान से पहले इमेज को डाउनस्केल करने की भी अनुमति देते हैं।

---

## निष्कर्ष

यही है—Python का उपयोग करके TIFF फ़ाइल पर **OCR कैसे करें** पर एक संक्षिप्त, पूर्ण‑कार्यशील गाइड। हमने लाइब्रेरी इंस्टॉल करने, इंजन कॉन्फ़िगर करने (जिसमें **OCR भाषा सेट** शामिल है), **OCR के लिए इमेज लोड**, **दस्तावेज़ पर OCR चलाएँ**, और अंत में **TIFF से टेक्स्ट निकालें** सभी को कवर किया।

बिना झिझक प्रयोग करें: थ्रेड काउंट बदलें, भाषाएँ स्विच करें, या OCR आउटपुट को एक नेचुरल‑लैंग्वेज पाइपलाइन में फीड करें। बुनियादी चीज़ें समझने के बाद संभावनाएँ अनंत हैं।

और सवाल हैं? नीचे टिप्पणी छोड़ें, और कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}