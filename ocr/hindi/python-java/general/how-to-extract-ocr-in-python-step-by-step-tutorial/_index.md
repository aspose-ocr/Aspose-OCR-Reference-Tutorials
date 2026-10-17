---
category: general
date: 2026-04-26
description: Python का उपयोग करके छवियों से OCR निकालना – एक Python OCR उदाहरण जो
  दिखाता है कि OCR के लिए छवि कैसे लोड करें और रसीद से टेक्स्ट निकालें।
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: hi
og_description: Python का उपयोग करके छवियों से OCR निकालने का तरीका। एक Python OCR
  उदाहरण सीखें, OCR के लिए छवि लोड करें, और मिनटों में रसीद से टेक्स्ट निकालें।
og_title: Python में OCR निकालना कैसे करें – पूर्ण गाइड
tags:
- OCR
- Python
- Image Processing
title: Python में OCR निकालने का तरीका – चरण-दर-चरण ट्यूटोरियल
url: /hi/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to extract ocr in Python – Complete Guide

क्या आपने कभी **how to extract ocr** को धुंधली रसीद या स्कैन किए गए इनवॉइस से निकालने के बारे में सोचा है? आप अकेले नहीं हैं—डेवलपर्स अक्सर तब रुक जाते हैं जब उन्हें इमेज से साफ़, मशीन‑रीडेबल टेक्स्ट चाहिए होता है। अच्छी खबर? सिर्फ कुछ पंक्तियों के Python कोड से आप रसीद की तस्वीर को उच्च‑विश्वास, सर्चेबल टेक्स्ट में बदल सकते हैं।

इस ट्यूटोरियल में हम एक **python ocr example** के माध्यम से दिखाएंगे कि **how to load image for ocr** कैसे किया जाता है, इंजन को चलाया जाता है, और केवल उन अक्षरों को रखा जाता है जिनका confidence 85 % से ऊपर है। अंत तक आप **extract text from receipt** इमेजेज़ को बिना दस्तावेज़ों की खोज या API पैरामीटर अनुमान लगाए निकाल पाएँगे।

## What You’ll Need

- Python 3.9 या नया (हम जो सिंटैक्स उपयोग करते हैं वह 3.8+ पर काम करता है)
- `aocr` पैकेज (या कोई भी OCR लाइब्रेरी जो `OcrEngine` क्लास प्रदान करती हो)। इसे इस तरह इंस्टॉल करें:

```bash
pip install aocr
```

- एक सैंपल रसीद इमेज (`receipt.png`) जिसे आप किसी फ़ोल्डर में रख सकते हैं।
- एक टेक्स्ट एडिटर या IDE—VS Code, PyCharm, या यहाँ तक कि एक साधा नोटबुक भी चलेगा।

बस इतना ही। कोई भारी‑फ़्रेमवर्क नहीं, कोई बाहरी सर्विस नहीं, सिर्फ शुद्ध Python।

![High‑confidence OCR result – how to extract ocr from a receipt](/images/ocr-high-confidence.png)

*Image alt text: Python OCR का उपयोग करके रसीद से OCR निकालने का तरीका*

## Step 1 – Create the OCR Engine Instance (how to extract ocr)

सबसे पहले हम एक OCR इंजन बनाते हैं। इसे ऐसे समझें जैसे वह दिमाग जो पिक्सेल को पढ़ेगा।

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Why?** `OcrEngine` को इंस्टैंशिएट करने से आपको एक नई कॉन्फ़िगरेशन ऑब्जेक्ट मिलती है। बाद में आप भाषा मॉडल, DPI सेटिंग्स, या प्री‑प्रोसेसिंग स्टेप्स को बदल सकते हैं—बिना कोर प्रोसेसिंग लूप को छुए।

## Step 2 – Load the Image for OCR

अब हम इंजन को उस इमेज की ओर इशारा करते हैं जिसे हम विश्लेषण करना चाहते हैं। यहाँ **load image for ocr** कीवर्ड काम आता है।

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Pro tip:** यदि आपकी इमेज किसी अलग डायरेक्टरी में है, तो `os.path.join` का उपयोग करके प्लेटफ़ॉर्म‑इंडिपेंडेंट पाथ बनाएँ।

**Why load the image this way?** `Image.load` हेल्पर फ़ाइल को ऐसे फॉर्मेट में पढ़ता है जिसे इंजन समझता है, और सामान्य फॉर्मेट्स (PNG, JPEG, TIFF) को स्वचालित रूप से हैंडल करता है। इस स्टेप को छोड़ने या रॉ बाइट्स देने से `ValueError` आएगा।

## Step 3 – Run the OCR Process

अब हम वास्तव में OCR चलाते हैं। `process` मेथड एक रिच रिज़ल्ट ऑब्जेक्ट लौटाता है जिसमें पहचाने गए सिम्बॉल, confidence स्कोर, और बाउंडिंग बॉक्स शामिल होते हैं।

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**What does `ocr_result` contain?** अधिकांश लाइब्रेरीज़ में यह शामिल होता है:

- `text`: कच्चा संयोजित स्ट्रिंग।
- `symbol_confidences`: `(char, confidence)` ट्यूपल की लिस्ट।
- `boxes`: प्रत्येक अक्षर के लिए कोऑर्डिनेट्स (विज़ुअल डिबगिंग में उपयोगी)।

प्रति‑अक्षर confidence तक पहुँच होना अगले स्टेप के लिए आवश्यक है।

## Step 4 – Keep Only High‑Confidence Symbols (≥ 85 %)

रसीद में अक्सर धब्बे, हल्की प्रिंट, या बैकग्राउंड शोर होते हैं। लो‑confidence सिम्बॉल को फ़िल्टर करने से डाउनस्ट्रीम पार्सिंग में काफी सुधार होता है।

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Why 85 %?** अनुभवजन्य रूप से, 0.85 के आसपास का थ्रेशोल्ड अधिकांश प्रिंटेड रसीदों के लिए recall और precision के बीच संतुलन बनाता है। यदि आपको नंबर गायब दिखें, तो थ्रेशोल्ड कम करें; यदि गड़बड़ टेक्स्ट मिले, तो इसे बढ़ाएँ।

## Step 5 – Output the High‑Confidence Extracted Text

अंत में, हम सफ़ाई किया हुआ स्ट्रिंग प्रिंट (या स्टोर) करते हैं। यही हमारे **extract text from receipt** वर्कफ़्लो का मुख्य भाग है।

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

आम तौर पर आउटपुट इस प्रकार दिखता है:

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

अब आप इस स्ट्रिंग को CSV राइटर, डेटाबेस, या किसी भी डाउनस्ट्रीम एनालिटिक्स पाइपलाइन में फीड कर सकते हैं।

## Full, Ready‑to‑Run Script

नीचे पूरा कोड स्निपेट दिया गया है जिसे आप `ocr_receipt.py` में कॉपी‑पेस्ट करके तुरंत चला सकते हैं।

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

फ़ाइल सेव करें, सुनिश्चित करें कि `receipt.png` मौजूद है, और चलाएँ:

```bash
python ocr_receipt.py
```

आपको कंसोल में साफ़ की गई रसीद टेक्स्ट दिखाई देगी।

## Edge Cases & What‑If Scenarios

| Situation | Suggested Fix |
|-----------|----------------|
| **Very low confidence across the board** | इमेज को प्री‑प्रोसेस करें: कंट्रास्ट बढ़ाएँ, ग्रेस्केल में बदलें, या डिनॉइज़िंग फ़िल्टर (`cv2.GaussianBlur`) लागू करें। |
| **Non‑Latin characters** | `OcrEngine` को भाषा मॉडल पास करें (उदाहरण: `ocr_engine.language = "spa"` स्पेनिश के लिए)। |
| **Multiple receipts in one image** | पूरी इमेज पर OCR चलाएँ, फिर परिणाम को रेगुलर एक्सप्रेशन से विभाजित करें जो `\n\n+` (डबल लाइन ब्रेक) को पहचानता हो। |
| **Need the raw OCR text as well** | डिबगिंग के लिए फ़िल्टर किए हुए संस्करण के साथ `ocr_result.text` भी रखें। |

इन विविधताओं से आपका **how to use OCR** ज्ञान सबसे सरल केस से आगे बढ़ता है।

## Common Pitfalls (And How to Avoid Them)

- **Forgetting to install the library** – `pip install aocr` को इम्पोर्ट करने से पहले सफलतापूर्वक चलना चाहिए।
- **Using the wrong path separator** on Windows (`\` vs `/`). `os.path.join` का उपयोग करें।
- **Hard‑coding the confidence threshold** without testing – पहले कुछ रसीदों पर तेज़ विज़ुअल चेक ज़रूर करें।
- **Ignoring Unicode normalisation** – कुछ रसीदों में विशेष डैश कैरेक्टर होते हैं; आउटपुट को स्टोर करने से पहले `unicodedata.normalize('NFKC', text)` चलाएँ।

## Next Steps – Going Beyond the Basics

अब जब आप एकल रसीद से **how to extract ocr** डेटा निकालना जानते हैं, तो आप आगे कर सकते हैं:

1. **Batch process a folder of receipts** – सभी PNG/JPG फ़ाइलों पर लूप चलाएँ और प्रत्येक परिणाम को CSV में लिखें।
2. **Integrate with a database** – `high_confidence_text` को SQLite में स्टोर करें ताकि तेज़ लुक‑अप हो सके।
3. **Apply natural‑language parsing** – रेगेक्स या `dateutil` का उपयोग करके डेट, टोटल, और टैक्स एंपाउंट निकालें।
4. **Experiment with alternative libraries** – `pytesseract`, `easyocr`, या क्लाउड सर्विसेज़ (Google Vision, Azure OCR) को आज़माएँ यदि आपको मल्टी‑लिंगुअल सपोर्ट या उच्च सटीकता चाहिए।

इन सभी टॉपिक्स में हमारे सेकेंडरी कीवर्ड्स स्वाभाविक रूप से शामिल होते हैं: *python ocr example*, *extract text from receipt*, *load image for ocr*, और *how to use OCR*।

## Conclusion

हमने एक पूर्ण **python ocr example** के माध्यम से दिखाया कि **how to extract ocr** टेक्स्ट को रसीद इमेज से कैसे निकाला जाए, लो‑confidence सिम्बॉल को फ़िल्टर किया जाए, और साफ़ परिणाम आउटपुट किया जाए। स्टेप्स सरल हैं, कोड स्वयं‑समाहित है, और यह तरीका बड़े प्रोजेक्ट्स में आसानी से अनुकूलित किया जा सकता है।

अपनी रसीदों के साथ इसे आज़माएँ, confidence थ्रेशोल्ड को समायोजित करें, और फिर बैच प्रोसेसिंग की ओर बढ़ें। यदि आपको कोई अजीब चीज़ मिलती है—जैसे धुंधला लोगो या अनोखा फ़ॉन्ट—तो ऊपर दिए गए एज़‑केस टिप्स याद रखें। Happy coding, और आपका OCR पाइपलाइन हमेशा सटीक रहे!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}