---
category: general
date: 2026-01-12
description: Python के साथ PNG फ़ाइलों पर OCR जल्दी चलाएँ। जानें कि कैसे छवि और इनवॉइस
  से टेक्स्ट निकालें, और Aspose.OCR का उपयोग करके OCR के लिए छवि लोड करें।
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: hi
og_description: PNG पर तुरंत OCR चलाएँ। यह गाइड दिखाता है कि कैसे छवि और इनवॉइस से
  टेक्स्ट निकाला जाए, OCR के लिए छवि लोड करें, और परिणामों को JSON और CSV के रूप में
  सहेजा जाए।
og_title: PNG पर OCR चलाएँ – पूर्ण पायथन ट्यूटोरियल
tags:
- OCR
- Python
- Image Processing
title: PNG पर OCR चलाएँ – छवियों से टेक्स्ट निकालने के लिए पूर्ण पायथन गाइड
url: /hi/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG पर OCR चलाएँ – इमेज से टेक्स्ट निकालने के लिए पूर्ण Python गाइड

क्या आपको कभी **run OCR on PNG** फ़ाइलों को चलाने की ज़रूरत पड़ी है लेकिन यह नहीं पता था कि कौन‑सी लाइब्रेरी आपको साफ़, संरचित परिणाम देगी? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में—जैसे इनवॉइस ऑटोमेशन या रसीद स्कैनिंग—पहला कदम **extract text from image** फ़ाइलों से टेक्स्ट निकालना होता है, और PNG एक सामान्य फ़ॉर्मेट है क्योंकि यह लॉसलेस क्वालिटी को बनाए रखता है।

इस ट्यूटोरियल में हम Aspose.OCR Python पैकेज का उपयोग करके एक व्यावहारिक उदाहरण से गुजरेंगे। गाइड के अंत तक आप जानेंगे कि कैसे **load image for OCR** किया जाता है, प्रत्येक टेक्स्ट लाइन को निकाला जाता है, उस डेटा को एक साफ़ JSON ऑब्जेक्ट में बदला जाता है, और यहाँ तक कि इसे CSV में डंप किया जा सकता है आगे की प्रोसेसिंग के लिए। कोई फालतू बातें नहीं, सिर्फ एक व्यावहारिक, तुरंत चलाने योग्य समाधान।

## आप क्या सीखेंगे

- Aspose.OCR लाइब्रेरी को कैसे इंस्टॉल और इम्पोर्ट करें।  
- **run OCR on PNG** करने के सटीक चरण और परिणाम ऑब्जेक्ट को कैसे हैंडल करें।  
- **extract text from invoice** फ़ाइलों को निकालने और आउटपुट को JSON या CSV के रूप में फॉर्मेट करने के तरीके।  
- लो‑कॉन्ट्रास्ट इमेज, मल्टी‑लैंग्वेज डॉक्यूमेंट्स, और कॉन्फिडेंस स्कोर से निपटने के टिप्स।  
- एक पूर्ण, कॉपी‑एंड‑पेस्ट कोड सैंपल जिसे आप आज ही एक्सीक्यूट कर सकते हैं।  

> **Prerequisite:** Python 3.8+ और pip की बुनियादी जानकारी। यदि आपने पहले कभी Aspose का उपयोग नहीं किया है, तो चिंता न करें—यह गाइड आपको शुरू करने के लिए आवश्यक सब कुछ कवर करता है।

## चरण 1 – Aspose.OCR इंस्टॉल करें और अपना वातावरण तैयार करें

**run OCR on PNG** करने से पहले, लाइब्रेरी आपके सिस्टम पर मौजूद होनी चाहिए।

```bash
pip install aspose-ocr
```

> **Pro tip:** वर्चुअल एनवायरनमेंट (`python -m venv venv`) का उपयोग करें ताकि डिपेंडेंसीज़ अलग रहें। यह कई प्रोजेक्ट्स को संभालते समय वर्ज़न टकराव को रोकता है।

इंस्टॉल होने के बाद, उन मॉड्यूल्स को इम्पोर्ट करें जिनकी हमें आवश्यकता होगी:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

यहाँ हम `asposeocr` को भारी काम के लिए और बिल्ट‑इन `json` लाइब्रेरी को बाद में सीरियलाइज़ेशन के लिए लाते हैं।

## चरण 2 – OCR इंजन बनाएं और भाषा सेट करें

OCR इंजन वह मुख्य घटक है जो वास्तव में पिक्सेल पढ़ता है। अधिकांश अंग्रेज़ी इनवॉइस के लिए, आपको English भाषा पैक चाहिए होगा:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Why this matters:** भाषा निर्दिष्ट करने से कैरेक्टर सेट सीमित हो जाता है, जिससे सटीकता बढ़ती है और प्रोसेसिंग तेज़ होती है। यदि आपको कभी मल्टी‑लैंग्वेज इनवॉइस संभालने की ज़रूरत पड़े, तो बस `ocr.Language.ENGLISH` को उपयुक्त enum से बदल दें।

## चरण 3 – OCR के लिए इमेज लोड करें

अब हम **load image for OCR** करेंगे। `Image.load` मेथड फ़ाइल पाथ को स्वीकार करता है, और यह PNG, JPEG, BMP, आदि के साथ काम करता है।

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Edge case:** यदि PNG असामान्य रूप से बड़ा है (5 MB से अधिक), तो मेमोरी उपयोग को उचित रखने के लिए पहले उसका आकार बदलने पर विचार करें। Pillow इसे एक लाइन में कर सकता है:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

## चरण 4 – PNG पर OCR चलाएँ और परिणाम कैप्चर करें

इंजन तैयार और इमेज लोड हो जाने के बाद, अब **run OCR on PNG** करने और संरचित परिणाम प्राप्त करने का समय है।

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

`ocr_result` ऑब्जेक्ट में `OcrRegion` आइटम्स का संग्रह होता है, प्रत्येक में पहचाना गया टेक्स्ट और कॉन्फिडेंस स्कोर (0‑100) होता है। यही वह जगह है जहाँ आपको **extract text from invoice** लाइनों के लिए आवश्यक विस्तृत डेटा मिलता है।

## चरण 5 – परिणाम को JSON में बदलें और प्रिटी‑प्रिंट करें

अधिकांश डाउनस्ट्रीम सिस्टम JSON को पसंद करते हैं, इसलिए हम OCR आउटपुट को एक सुंदर फॉर्मेटेड स्ट्रिंग में बदलेंगे।

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### नमूना आउटपुट

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

ध्यान दें कि प्रत्येक लाइन में कॉन्फिडेंस मेट्रिक शामिल है—यदि आप **extract text from invoice** को स्वचालित रूप से करना चाहते हैं तो लो‑कॉन्फिडेंस एंट्रीज़ को फ़िल्टर करने के लिए यह परफेक्ट है।

## चरण 6 – OCR डेटा को CSV के रूप में सेव करें (प्रति टेक्स्ट + कॉन्फिडेंस एक लाइन)

CSV स्प्रेडशीट या तेज़ डेटा इम्पोर्ट के लिए आदर्श है। Aspose एक-लाइनर प्रदान करता है जिससे सब कुछ CSV फ़ाइल में डंप किया जा सकता है।

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

जनरेटेड CSV इस तरह दिखेगा:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

अब आप इसे Excel, Google Sheets में खोल सकते हैं, या डेटाबेस में फीड कर सकते हैं।

## बोनस – लो‑कॉन्फिडेंस टेक्स्ट और मल्टी‑पेज PDFs को हैंडल करना

### कॉन्फिडेंस द्वारा फ़िल्टरिंग

यदि आप केवल हाई‑सर्टेन्टी लाइन्स चाहते हैं, तो लिखने से पहले JSON को फ़िल्टर करें:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### मल्टी‑पेज डॉक्यूमेंट्स

Aspose.OCR स्वचालित रूप से मल्टी‑पेज PNG या PDF की प्रत्येक पेज के लिए एक नया `page` एंट्री बनाता है। सभी को प्रोसेस करने के लिए `ocr_data["pages"]` के माध्यम से लूप करें—कोई अतिरिक्त कोड नहीं चाहिए।

## पूर्ण कार्यशील उदाहरण

नीचे **complete script** है जिसे आप कॉपी, पेस्ट और तुरंत चला सकते हैं। `YOUR_DIRECTORY` को उस फ़ोल्डर से बदलें जिसमें आपका PNG फ़ाइल है।

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

`python run_ocr.py` के साथ स्क्रिप्ट चलाएँ और आप कंसोल में JSON डंप, डिस्क पर CSV फ़ाइल, और हाई‑कॉन्फिडेंस एंट्रीज़ की फ़िल्टर की हुई लिस्ट देखेंगे।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं इसे स्कैन किए हुए रसीद से टेक्स्ट निकालने के लिए उपयोग कर सकता हूँ इनवॉइस की बजाय?**  
A: बिल्कुल। वही वर्कफ़्लो लागू होता है—सिर्फ `image_path` को अपनी रसीद PNG की ओर इंगित करें। यदि रसीद में अलग भाषा है, तो `engine.language` को उसी अनुसार बदलें।

**Q: यदि मेरे PNG में घुमा हुआ टेक्स्ट है तो क्या होगा?**  
A: Aspose.OCR स्वचालित रूप से ओरिएंटेशन का पता लगाता है, लेकिन जिद्दी मामलों में आप Pillow के साथ इमेज को मैन्युअली घुमा सकते हैं इससे पहले कि उसे इंजन को दें।

**Q: क्या मुझे Aspose.OCR के लिए पेड लाइसेंस चाहिए?**  
A: लाइब्रेरी एक मुफ्त इवैल्यूएशन मोड प्रदान करती है जिसमें आउटपुट पर वॉटरमार्क होता है। प्रोडक्शन उपयोग के लिए आपको लाइसेंस की आवश्यकता होगी, जिसे आप Aspose वेबसाइट से प्राप्त कर सकते हैं।

## निष्कर्ष

हमने Python का उपयोग करके **run OCR on PNG** फ़ाइलों के लिए आवश्यक सभी चीज़ें कवर कर ली हैं: SDK इंस्टॉल करना, इमेज लोड करना, संरचित टेक्स्ट निकालना, और परिणाम को JSON या CSV के रूप में सेव करना। चाहे आप एक साधारण स्क्रिप्ट के लिए **extract text from image** करना चाहते हों या ऑटोमेटेड अकाउंटिंग पाइपलाइन के लिए **extract text from invoice**, ऊपर दिए गए चरण आपको एक ठोस, प्रोडक्शन‑रेडी आधार प्रदान करते हैं।

अगले चरण में, आप खोज सकते हैं:

- बड़े पैमाने पर इनवॉइस स्टोरेज के लिए CSV आउटपुट को डेटाबेस के साथ इंटीग्रेट करना।  
- डेट्स, अमाउंट्स, या टैक्स IDs निकालने के लिए रेगुलर एक्सप्रेशन के साथ पोस्ट‑प्रोसेसिंग जोड़ना।  
- यदि आपके इनवॉइस में QR कोड हैं तो `ocr_engine.recognize_barcode` फीचर का उपयोग करना।  

इसे आज़माएँ, कॉन्फिडेंस थ्रेशोल्ड को समायोजित करें, और देखें कि आपका डॉक्यूमेंट‑प्रोसेसिंग वर्कफ़्लो कितना आसान हो जाता है। यदि आपके पास और प्रश्न या कोई शानदार उपयोग‑केस है तो नीचे कमेंट करें—हैप्पी OCRing!  

![run OCR on PNG उदाहरण](run-ocr-on-png.png "run OCR on PNG – OCR परिणाम का विज़ुअल उदाहरण")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}