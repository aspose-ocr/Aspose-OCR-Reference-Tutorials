---
category: general
date: 2026-03-26
description: कैसे PNG फ़ाइल पर OCR चलाएँ और कस्टम शब्दकोश के साथ इमेज से टेक्स्ट निकालें
  ताकि OCR की सटीकता बढ़े। OCR के लिए इमेज को जल्दी लोड करना सीखें।
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: hi
og_description: PNG फ़ाइल पर OCR चलाकर कस्टम शब्दकोश के साथ छवि से टेक्स्ट निकालें
  और OCR की सटीकता बढ़ाएँ। चरण‑दर‑चरण गाइड।
og_title: OCR कैसे चलाएँ – Python में इमेज से टेक्स्ट निकालें
tags:
- OCR
- Python
- Image Processing
title: OCR कैसे चलाएँ – पायथन में छवि से पाठ निकालें
url: /hi/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR कैसे चलाएँ – Python में इमेज से टेक्स्ट निकालें

क्या आपने कभी **OCR कैसे चलाएँ** इस बारे में सोचा है, जैसे स्कैन की गई इनवॉइस या स्क्रीनशॉट पर और साफ़, खोजने योग्य टेक्स्ट प्राप्त करें? आप अकेले नहीं हैं। कई प्रोजेक्ट्स में बाधा सिर्फ इमेज को OCR के लिए लोड करना और फिर इंजन को डोमेन‑स्पेसिफिक शब्दों को समझाने में होती है।  

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने‑योग्य उदाहरण के माध्यम से चलेंगे जो **इमेज फ़ाइलों से टेक्स्ट निकालता** है, आपको दिखाता है कि **PNG से टेक्स्ट कैसे पहचानें** और यहाँ तक कि कस्टम डिक्शनरी और विशेष अक्षरों के साथ **OCR की सटीकता सुधारने** के ट्रिक्स भी दर्शाता है। अंत तक आपके पास एक स्व-निहित स्क्रिप्ट होगी जिसे आप किसी भी Python कोडबेस में डाल सकते हैं।

## आपको क्या चाहिए

- Python 3.8+ (कोड टाइप हिंट्स का उपयोग करता है लेकिन पहले के 3.x संस्करणों पर भी चलता है)
- वह `ocr` लाइब्रेरी जो आपके लक्ष्य OCR इंजन के साथ आती है (इंस्टॉल करने के लिए `pip install ocr‑engine` – वास्तविक पैकेज नाम से बदलें)
- एक इमेज फ़ाइल (`input.png`) जिसे आप प्रोसेस करना चाहते हैं
- वैकल्पिक: एक प्लेन‑टेक्स्ट फ़ाइल (`invoice_terms.txt`) जिसमें डोमेन‑स्पेसिफिक शब्द हों, प्रत्येक पंक्ति में एक

कोई भारी बाहरी निर्भरताएँ नहीं, कोई क्लाउड API कुंजियाँ नहीं, सिर्फ एक स्थानीय OCR इंजन।

---

## चरण 1: OCR लाइब्रेरी इंस्टॉल और इम्पोर्ट करें

सबसे पहले, सुनिश्चित करें कि OCR पैकेज इंस्टॉल है। यदि आप काल्पनिक `ocr-engine` पैकेज का उपयोग कर रहे हैं, तो चलाएँ:

```bash
pip install ocr-engine
```

अब उन क्लासेज़ को इम्पोर्ट करें जिनकी आपको आवश्यकता होगी:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **प्रो टिप:** यदि आप वर्चुअल एनवायरनमेंट में हैं, तो इंस्टॉल करने से पहले उसे एक्टिवेट करें ताकि आपका ग्लोबल Python साफ़ रहे।

## चरण 2: OCR इंजन इंस्टेंस बनाएँ

एक इंजन ऑब्जेक्ट बनाना हर OCR कार्य का प्रवेश बिंदु है। इसे सॉफ़्टवेयर में स्कैनर हार्डवेयर को चालू करने जैसा समझें।

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

यह क्यों महत्वपूर्ण है: इंजन में भाषा पैक्स, रिकग्निशन मोड, और बाद में आप जो भी कस्टम रिसोर्सेज़ जोड़ेंगे, उनकी कॉन्फ़िगरेशन रहती है। इसके बिना आप **OCR के लिए इमेज लोड** नहीं कर सकते या रिकग्निशन पाइपलाइन नहीं चला सकते।

## चरण 3: वह इमेज लोड करें जिसे आप पहचानना चाहते हैं

यहाँ हम वास्तव में **OCR के लिए इमेज लोड** करते हैं। `Imaging.Image.load()` मेथड फ़ाइल को पढ़ता है और उसे इंजन द्वारा अपेक्षित आंतरिक बिटमैप फ़ॉर्मेट में बदल देता है।

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

यदि आपके पास JPEG या TIFF है, तो वही मेथड काम करेगा—सिर्फ एक्सटेंशन बदलें। इंजन स्वचालित रूप से फ़ॉर्मेट का पता लगा लेता है।

> **एज केस:** बहुत बड़ी इमेज (5 MP से अधिक) मेमोरी स्पाइक का कारण बन सकती हैं। यदि प्रदर्शन समस्याएँ आती हैं तो Pillow के साथ डाउन‑स्केल करने पर विचार करें।

## चरण 4: कस्टम डिक्शनरी प्रदान करके सटीकता बढ़ाएँ

अधिकांश OCR इंजन जेनरिक लैंग्वेज मॉडल के साथ आते हैं। इनवॉइस, रसीद या कानूनी दस्तावेज़ों के लिए अक्सर शब्द छूट जाते हैं। एक कस्टम शब्द सूची प्रदान करने से इंजन को “ये शब्द वैध हैं, इन्हें सही मानें” बताया जाता है।

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

आम प्रविष्टियाँ इस प्रकार हो सकती हैं:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

इनको जोड़ने से **OCR सटीकता सुधारें** मीट्रिक में नाटकीय सुधार आता है—विशेषकर गैर‑ASCII प्रतीकों के लिए।

## चरण 5: डिफ़ॉल्ट सेट में न मौजूद विशेष अक्षर जोड़ें

यदि आपका डोमेन यूरो साइन (€) या स्कैंडिनेवियन Ø जैसे प्रतीकों का उपयोग करता है, तो आप उन्हें स्पष्ट रूप से जोड़ सकते हैं:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

अब इंजन इन ग्लिफ़्स को मान्य मानते हुए पहचान चरण में उपयोग करेगा, जिससे “गर्बेज” आउटपुट की संभावना कम हो जाएगी।

## चरण 6: OCR प्रक्रिया चलाएँ और टेक्स्ट प्राप्त करें

अंत में, रिकग्नाइज़र को कॉल करें और प्लेन‑टेक्स्ट परिणाम निकालें। `recognize()` कॉल एक रिच ऑब्जेक्ट लौटाता है; अधिकांश उपयोग‑केस में हमें केवल रॉ स्ट्रिंग चाहिए होती है।

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**अपेक्षित आउटपुट** (संक्षिप्त रूप में):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

यदि आउटपुट गड़बड़ दिखे, तो दोबारा जांचें कि आपकी कस्टम डिक्शनरी और विशेष अक्षर सही ढंग से लोड हुए हैं।

---

## विज़ुअल ओवरव्यू

![how to run OCR diagram](ocr-workflow.png){alt="OCR चलाने का आरेख"}

ऊपर दिया गया आरेख इमेज लोड करने से लेकर साफ़ टेक्स्ट प्राप्त करने तक के प्रवाह को दर्शाता है, और जहाँ आप कस्टम डिक्शनरी और कैरेक्टर सेट इन्जेक्ट कर सकते हैं, उसे हाइलाइट करता है।

---

## सामान्य प्रश्न और गड़बड़ियाँ

### क्या यह मल्टी‑पेज PDFs के साथ काम करता है?

हाँ—हर पेज को PNG में बदलें (`pdf2image` या समान टूल से) और उन्हें क्रमशः उसी `ocr_engine` इंस्टेंस को फीड करें। इंजन प्रत्येक इमेज को स्वतंत्र रूप से प्रोसेस करता है, इसलिए आपको स्ट्रिंग्स की एक सूची मिलेगी जिसे आप जोड़ सकते हैं।

### अगर इमेज घुमा हुआ हो तो क्या करें?

अधिकांश आधुनिक OCR इंजन ऑटो‑डिटेक्ट ओरिएंटेशन करते हैं, लेकिन आप मैन्युअली घुमाने के लिए उपयोग कर सकते हैं:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### अंग्रेज़ी के अलावा अन्य भाषाओं को कैसे हैंडल करें?

इमेज लोड करने से पहले भाषा मॉडल बदलें:

```python
ocr_engine.set_language("de")  # German
```

सुनिश्चित करें कि संबंधित भाषा पैक इंस्टॉल हो।

---

## पूर्ण स्क्रिप्ट – कॉपी‑पेस्ट के लिए तैयार

नीचे पूरा प्रोग्राम दिया गया है, जिसे प्लेसहोल्डर पाथ्स बदलने के बाद चलाया जा सकता है।

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

इसे चलाएँ:

```bash
python run_ocr.py
```

आपको कंसोल में निकाला गया टेक्स्ट दिखेगा। वहाँ से आप इसे फ़ाइल में लिख सकते हैं, डेटाबेस में डाल सकते हैं, या डाउनस्ट्रीम NLP पाइपलाइन को पास कर सकते हैं।

---

## पुनरावलोकन और आगे के कदम

हमने **OCR कैसे चलाएँ** PNG पर, **इमेज से टेक्स्ट निकालें**, और डिक्शनरी व कस्टम कैरेक्टर्स के साथ **OCR की सटीकता सुधारें** के व्यावहारिक तरीकों को कवर किया।  

अगले कदम में विचार करें:

- **बैच प्रोसेसिंग:** इमेज की डायरेक्टरी पर लूप चलाएँ।
- **पोस्ट‑प्रोसेसिंग:** रेगएक्स का उपयोग करके इनवॉइस नंबर या डेट्स निकालें।
- **इंटीग्रेशन:** स्क्रिप्ट को Flask API में हुक करें ताकि ऑन‑डिमांड OCR सर्विसेज मिलें।

यदि आप अधिक उन्नत विषयों में रुचि रखते हैं, तो **OpenCV प्री‑प्रोसेसिंग के साथ इमेज लोड** ट्यूटोरियल देखें, या Tesseract 4+ जैसे डीप‑लर्निंग आधारित OCR मॉडल्स को LSTM लेयर्स के साथ एक्सप्लोर करें।

---

### प्रयोग करते रहें!

`invoice_terms.txt` को मेडिकल टर्मिनोलॉजी की सूची से बदलें, ग्रीक अक्षर जोड़ें, या इंजन को लो‑रेज़ोल्यूशन फोटो दें और देखें कि सटीकता कितनी दूर तक पहुँचती है। जितना अधिक आप टिंकर करेंगे, उतना ही आप प्री‑प्रोसेसिंग, कस्टम शब्दावली, और इंजन सेटिंग्स के बीच के ट्रेड‑ऑफ़ को समझ पाएँगे।

हैप्पी कोडिंग, और आपके OCR परिणाम हमेशा स्पष्ट रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}