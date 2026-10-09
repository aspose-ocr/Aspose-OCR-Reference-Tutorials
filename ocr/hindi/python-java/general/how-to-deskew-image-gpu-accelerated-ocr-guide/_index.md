---
category: general
date: 2026-01-02
description: इमेज को डेस्क्यू करने और इमेज कॉन्ट्रास्ट बढ़ाने के तरीकों को सीखें ताकि
  सादा टेक्स्ट जल्दी प्राप्त हो सके। इसमें चरण-दर-चरण पायथन कोड और टेक्स्ट निकालने
  के टिप्स शामिल हैं।
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: hi
og_description: इमेज को डेस्क्यू करने और कंट्रास्ट बढ़ाने के तरीके ताकि साधारण टेक्स्ट
  प्राप्त हो सके। टेबल एक्सट्रैक्शन और GPU एक्सेलेरेशन के साथ पूर्ण पायथन उदाहरण।
og_title: इमेज को डेस्क्यू कैसे करें – पूर्ण GPU OCR ट्यूटोरियल
tags:
- OCR
- Python
- Image Processing
title: इमेज को डेस्क्यू कैसे करें – GPU‑त्वरित OCR गाइड
url: /hi/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज को डेस्क्यू कैसे करें – GPU‑त्वरित OCR गाइड

क्या आपने कभी सोचा है **how to deskew image** जब आपकी रसीदें अजीब कोण पर आती हैं? आप अकेले नहीं हैं; एक तिरछी फोटो एक पूरी तरह पढ़ी जा सकने वाली रसीद को गड़बड़ बना सकती है। अच्छी खबर यह है कि कुछ ही पायथन लाइनों के साथ आप ऑटो‑डेस्क्यू कर सकते हैं, कंट्रास्ट बढ़ा सकते हैं, और साफ़ प्लेन टेक्स्ट निकाल सकते हैं—बिना मैन्युअल फ़ोटोशॉप के।  

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे कि न केवल **how to deskew image** बल्कि **how to boost contrast**, **how to get plain text**, और यहाँ तक कि **how to extract text** टेबल्स से भी कैसे किया जाता है, जो OCR इंजन पहचानता है। अंत तक आपके पास एक स्व-निहित स्क्रिप्ट होगी जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं।

## What You’ll Need

- Python 3.9+ स्थापित (कोड टाइप हिंट्स का उपयोग करता है, इसलिए नया इंटरप्रेटर मददगार है)
- `ocr` लाइब्रेरी जिसमें `OcrEngine`, `EngineMode`, `ImageProcessingOptions`, और `OcrResult` उपलब्ध हैं (इंस्टॉल करने के लिए `pip install ocr‑sdk` – अपने वास्तविक पैकेज नाम से बदलें)
- एक GPU जिसमें संगत ड्राइवर हों, यदि आप स्पीड बूस्ट चाहते हैं (वैकल्पिक लेकिन अनुशंसित)
- एक इमेज फ़ाइल जो थोड़ा रोटेटेड या लो‑कंट्रास्ट हो, जैसे `receipt_skewed.jpg`

> **Pro tip:** यदि आपके पास GPU नहीं है, तो बस `EngineMode.GPU` को `EngineMode.CPU` में बदल दें और स्क्रिप्ट अभी भी चलेगी—सिर्फ थोड़ा धीमी।

## Step‑by‑Step Implementation

नीचे हम समाधान को तार्किक भागों में विभाजित करते हैं। प्रत्येक भाग में एक वर्णनात्मक **H2** है जिसमें मुख्य कीवर्ड *how to deskew image* या कोई द्वितीयक कीवर्ड शामिल है। कोड पूर्ण, टिप्पणी सहित, और चलाने के लिए तैयार है।

### How to Deskew Image with GPU‑Accelerated OCR

पहला कदम है OCR इंजन को GPU पर चलाने के लिए सेट करना और ऑटो‑डेस्क्यू फीचर को सक्षम करना। ऑटो‑डेस्क्यू इमेज की ज्योमेट्री का विश्लेषण करता है और उसे सीधा कर देता है।

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Why this matters:** GPU एक्सेलेरेशन प्रोसेसिंग समय को सेकंड से मिलीसेकंड में घटा सकता है, जो प्रति मिनट दर्जनों रसीदें संभालते समय बहुत महत्वपूर्ण है।

### Boost Image Contrast for Better Recognition

लो‑कंट्रास्ट रसीद किसी भी OCR सिस्टम के लिए दुःस्वप्न है। कंट्रास्ट बढ़ाकर हम इंजन को स्पष्ट किनारे प्रदान करते हैं।

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **How to boost contrast:** `set_contrast_boost` मेथड प्रतिशत लेता है; 30 % अधिकांश स्कैन की गई रसीदों के लिए सुरक्षित डिफ़ॉल्ट है। यदि आपकी इमेज बहुत डार्क है, तो इसे 50 % तक बढ़ाएँ या प्रयोग करें।

### Get Plain Text from the Processed Image

अब जब इमेज सीधी और उज्ज्वल है, हम इसे इंजन में फीड करते हैं और प्लेन टेक्स्ट परिणाम मांगते हैं।

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Expected output** (संक्षिप्त रूप में):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **How to get plain text:** `get_text()` मेथड लेआउट जानकारी को हटाकर एक साफ़ स्ट्रिंग लौटाता है, जिसे आप डेटाबेस में स्टोर कर सकते हैं, API को भेज सकते हैं, या डाउनस्ट्रीम एनालिटिक्स में फीड कर सकते हैं।

### How to Extract Text from Detected Tables

अक्सर रसीदों में टेबलर डेटा (आइटम, क्वांटिटी, प्राइस) होता है। OCR SDK टेबल्स का पता लगा सकता है और आपको रो और सेल्स पर इटररेट करने देता है।

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Sample table output**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Why extract tables:** स्ट्रक्चर्ड डेटा से कुल जोड़ना, रिपोर्ट बनाना, या अकाउंटिंग सॉफ़्टवेयर में फीड करना बहुत आसान हो जाता है।

### Full Working Script

सब कुछ मिलाकर, यहाँ वह स्क्रिप्ट है जिसे आप `deskew_and_ocr.py` में कॉपी‑पेस्ट कर सकते हैं:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

इसे चलाएँ:

```bash
python deskew_and_ocr.py
```

आपको कंसोल में साफ़ किया हुआ टेक्स्ट और कोई भी डिटेक्टेड टेबल्स प्रिंट होते दिखेंगे।

## Common Edge Cases & How to Handle Them

| Situation | What to Do |
|-----------|------------|
| **Image is upside‑down** | `set_auto_deskew(True)` की कॉन्फिडेंस बढ़ाएँ और साथ ही `set_rotation_correction(True)` कॉल करें यदि SDK यह सपोर्ट करता है। |
| **Contrast boost makes the image too bright** | `set_contrast_boost` को पास किया गया प्रतिशत घटाएँ (जैसे, 15 %)। |
| **GPU not available** | `EngineMode.GPU` को `EngineMode.CPU` में बदलें; पाइपलाइन का बाकी हिस्सा अपरिवर्तित रहता है। |
| **Tables are missed** | उच्च रेज़ोल्यूशन स्कैन आज़माएँ या `set_table_detection(True)` को एनेबल करें यदि लाइब्रेरी यह प्रदान करती है। |

## Next Steps: From Plain Text to Structured Data

अब जब आप **how to deskew image**, **how to boost contrast**, और **how to get plain text** जानते हैं, आप आगे कर सकते हैं:

- रेगुलर एक्सप्रेशन के साथ प्लेन टेक्स्ट को पार्स करके की‑वैल्यू पेयर्स निकालें (जैसे `total`, `date`)।
- परिणामों को SQLite या PostgreSQL डेटाबेस में स्टोर करें ताकि बाद में रिपोर्टिंग हो सके।
- स्क्रिप्ट को सर्वरलेस फ़ंक्शन (AWS Lambda, Azure Functions) में इंटीग्रेट करें ताकि अपलोड्स ऑटोमैटिक प्रोसेस हों।

इन सभी एक्सटेंशन का आधार वही है जो हमने यहाँ कवर किया है।

## Conclusion

हमने **how to deskew image** को GPU‑त्वरित OCR इंजन के साथ किया, **how to boost contrast** को शार्पर रिकग्निशन के लिए दिखाया, ठीक‑ठीक **how to get plain text** बताया, और यहाँ तक कि **how to extract text** टेबल्स से भी कवर किया। पूरा, चलाने योग्य स्क्रिप्ट सब कुछ जोड़ता है, ताकि आप इसे किसी भी पायथन प्रोजेक्ट में डालकर तिरछी, लो‑कंट्रास्ट फ़ोटो से साफ़ डेटा निकालना तुरंत शुरू कर सकें।

अपनी कुछ रसीदों के साथ इसे आज़माएँ, कंट्रास्ट लेवल को ट्यून करें, और OCR को भारी काम करने दें। यदि कोई अजीब बात मिले, तो ऊपर दी गई एज़‑केस टेबल को फिर देखें—अधिकतर समस्याएँ सिर्फ एक छोटा बदलाव ही हल कर देता है।

हैप्पी कोडिंग, और आपकी इमेजेस हमेशा सीधी और उज्ज्वल रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}