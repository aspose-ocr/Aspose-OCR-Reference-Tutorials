---
category: general
date: 2026-03-28
description: छवि पर OCR करें और बाउंडिंग बॉक्स निर्देशांक के साथ साफ़ टेक्स्ट प्राप्त
  करें। सीखें कि OCR कैसे निकालें, OCR को साफ़ करें, और परिणाम चरण‑दर‑चरण प्रदर्शित
  करें।
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: hi
og_description: छवि पर OCR करें, आउटपुट को साफ़ करें, और संक्षिप्त ट्यूटोरियल में
  बाउंडिंग बॉक्स के निर्देशांक दिखाएँ।
og_title: इमेज पर OCR करें – साफ़ परिणाम और बाउंडिंग बॉक्स
tags:
- OCR
- Computer Vision
- Python
title: छवि पर OCR करें – साफ परिणाम प्राप्त करें और बाउंडिंग बॉक्स निर्देशांक दिखाएँ
url: /hi/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज पर OCR करें – परिणाम साफ़ करें और बाउंडिंग बॉक्स कॉर्डिनेट्स दिखाएँ

क्या आपको कभी **perform OCR on image** फ़ाइलों को प्रोसेस करना पड़ा, लेकिन लगातार गड़बड़ टेक्स्ट मिल रहा था और यह नहीं पता चल रहा था कि प्रत्येक शब्द तस्वीर में कहाँ स्थित है? आप अकेले नहीं हैं। कई प्रोजेक्ट्स—इनवॉइस डिजिटाइज़ेशन, रसीद स्कैनिंग, या साधारण टेक्स्ट एक्सट्रैक्शन—में कच्चा OCR आउटपुट सिर्फ पहला कदम होता है। अच्छी खबर? आप उस आउटपुट को साफ़ कर सकते हैं और तुरंत प्रत्येक क्षेत्र के बाउंडिंग बॉक्स कॉर्डिनेट्स देख सकते हैं, बिना बहुत सारा बायलरप्लेट कोड लिखे।

इस गाइड में हम **OCR कैसे निकालें**, एक **how to clean OCR** पोस्ट‑प्रोसेसर चलाएँ, और अंत में **display bounding box coordinates** प्रत्येक साफ़ किए गए क्षेत्र के लिए दिखाएँगे। अंत तक आपके पास एक एकल, रन करने योग्य स्क्रिप्ट होगी जो धुंधली फोटो को साफ़, संरचित टेक्स्ट में बदल देगी, जो आगे की प्रोसेसिंग के लिए तैयार है।

## आपको क्या चाहिए

- Python 3.9+ (नीचे दिया गया सिंटैक्स 3.8 और उसके बाद के संस्करणों पर काम करता है)
- एक OCR इंजन जो `recognize(..., return_structured=True)` को सपोर्ट करता हो – उदाहरण के लिए, नीचे के स्निपेट में उपयोग किया गया काल्पनिक `engine` लाइब्रेरी। इसे Tesseract, EasyOCR, या किसी भी SDK से बदलें जो क्षेत्र डेटा रिटर्न करता हो।
- Python फ़ंक्शन और लूप्स की बेसिक समझ
- एक इमेज फ़ाइल जिसे आप स्कैन करना चाहते हैं (PNG, JPG, आदि)

> **Pro tip:** यदि आप Tesseract इस्तेमाल कर रहे हैं, तो `pytesseract.image_to_data` फ़ंक्शन पहले से ही बाउंडिंग बॉक्स देता है। आप उसके परिणाम को एक छोटे एडेप्टर में रैप कर सकते हैं जो नीचे दिखाए गए `engine.recognize` API की नकल करता हो।

---

![perform OCR on image example](image-placeholder.png "perform OCR on image example")

*Alt text: इमेज पर OCR करने और बाउंडिंग बॉक्स कॉर्डिनेट्स को विज़ुअलाइज़ करने की प्रक्रिया दिखाने वाला डायग्राम*

## चरण 1 – इमेज पर OCR करें और संरचित क्षेत्रों को प्राप्त करें

सबसे पहले OCR इंजन को यह बताना है कि वह केवल प्लेन टेक्स्ट नहीं, बल्कि टेक्स्ट क्षेत्रों की एक संरचित सूची रिटर्न करे। इस सूची में कच्चा स्ट्रिंग और उसे घेरने वाला आयत (रेकटैंगल) शामिल होता है।

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**यह क्यों महत्वपूर्ण है:**  
जब आप केवल प्लेन टेक्स्ट माँगते हैं तो आप स्पैटियल कॉन्टेक्स्ट खो देते हैं। संरचित डेटा आपको बाद में **display bounding box coordinates** करने, टेक्स्ट को टेबल्स के साथ अलाइन करने, या सटीक लोकेशन को डाउनस्ट्रीम मॉडल को फीड करने की सुविधा देता है।

## चरण 2 – पोस्ट‑प्रोसेसर के साथ OCR आउटपुट को साफ़ करें

OCR इंजन अक्षरों को पहचानने में अच्छे होते हैं, लेकिन अक्सर वे अतिरिक्त स्पेसेस, लाइन‑ब्रेक आर्टिफैक्ट्स, या गलत पहचान वाले सिम्बॉल छोड़ देते हैं। एक पोस्ट‑प्रोसेसर टेक्स्ट को सामान्यीकृत करता है, सामान्य OCR त्रुटियों को ठीक करता है, और व्हाइटस्पेस को ट्रिम करता है।

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

यदि आप अपना खुद का क्लीनर बना रहे हैं, तो विचार करें:

- नॉन‑ASCII कैरेक्टर्स हटाएँ (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- कई स्पेसेस को एक ही स्पेस में बदलें
- स्पष्ट टाइपो के लिए `pyspellchecker` जैसी स्पेल‑चेकर लागू करें

**आपको क्यों परवाह करनी चाहिए:**  
एक साफ़ स्ट्रिंग सर्चिंग, इंडेक्सिंग, और डाउनस्ट्रीम NLP पाइपलाइन को बहुत अधिक भरोसेमंद बनाती है। दूसरे शब्दों में, **how to clean OCR** अक्सर एक उपयोगी डेटासेट और सिरदर्द के बीच का अंतर होता है।

## चरण 3 – प्रत्येक साफ़ किए गए क्षेत्र के लिए बाउंडिंग बॉक्स कॉर्डिनेट्स दिखाएँ

अब टेक्स्ट साफ़ हो गया है, हम प्रत्येक क्षेत्र पर इटररेट करते हैं, उसका आयत और साफ़ किया हुआ स्ट्रिंग प्रिंट करते हैं। यही वह हिस्सा है जहाँ हम अंततः **display bounding box coordinates** करते हैं।

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**नमूना आउटपुट**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

अब आप इन कॉर्डिनेट्स को किसी ड्राइंग लाइब्रेरी (जैसे OpenCV) में फीड करके मूल इमेज पर बॉक्स ओवरले कर सकते हैं, या बाद में क्वेरीज़ के लिए उन्हें डेटाबेस में स्टोर कर सकते हैं।

## पूर्ण, रन‑टू‑डैड स्क्रिप्ट

नीचे पूरा प्रोग्राम दिया गया है जो तीनों चरणों को जोड़ता है। प्लेसहोल्डर `engine` कॉल्स को अपने वास्तविक OCR SDK से बदलें।

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### कैसे चलाएँ

```bash
python perform_ocr.py sample_invoice.jpg
```

आपको बाउंडिंग बॉक्स की सूची के साथ साफ़ किया हुआ टेक्स्ट दिखेगा, बिल्कुल ऊपर के नमूना आउटपुट की तरह।

## अक्सर पूछे जाने वाले प्रश्न और किनारे के केस

| प्रश्न | उत्तर |
|----------|--------|
| **यदि OCR इंजन `return_structured` को सपोर्ट नहीं करता तो क्या करें?** | एक हल्का रैपर लिखें जो इंजन के रॉ आउटपुट (आमतौर पर शब्दों की सूची और उनके कॉर्डिनेट्स) को `text` और `bounding_box` एट्रिब्यूट वाले ऑब्जेक्ट्स में बदल दे। |
| **क्या मैं कॉन्फिडेंस स्कोर प्राप्त कर सकता हूँ?** | कई SDK प्रत्येक क्षेत्र के लिए कॉन्फिडेंस मेट्रिक एक्सपोज़ करते हैं। इसे प्रिंट स्टेटमेंट में जोड़ें: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`। |
| **घुमाए हुए टेक्स्ट को कैसे हैंडल करें?** | `recognize` कॉल करने से पहले OpenCV के `cv2.minAreaRect` से इमेज को डेस्क्यू करें। |
| **यदि मुझे आउटपुट JSON में चाहिए तो?** | `processed_result.regions` को `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)` से सीरियलाइज़ करें। |
| **क्या बॉक्स को विज़ुअलाइज़ करने का कोई तरीका है?** | लूप के अंदर OpenCV उपयोग करें: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` और फिर `cv2.imwrite("annotated.jpg", img)`। |

## निष्कर्ष

आपने अभी **perform OCR on image**, कच्चे आउटपुट को साफ़ करना, और प्रत्येक क्षेत्र के लिए **display bounding box coordinates** करना सीख लिया है। तीन‑स्टेप फ्लो—recognize → post‑process → iterate—एक पुन: उपयोग योग्य पैटर्न है जिसे आप किसी भी Python प्रोजेक्ट में डाल सकते हैं जिसे भरोसेमंद टेक्स्ट एक्सट्रैक्शन चाहिए।

### आगे क्या?

- **विभिन्न OCR बैक‑एंड्स** (Tesseract, EasyOCR, Google Vision) को एक्सप्लोर करें और उनकी एक्यूरेसी की तुलना करें।
- **डेटाबेस के साथ इंटीग्रेट** करें ताकि क्षेत्र डेटा को सर्चेबल आर्काइव्स में स्टोर किया जा सके।
- **भाषा डिटेक्शन** जोड़ें ताकि प्रत्येक क्षेत्र को उपयुक्त स्पेल‑चेकर के माध्यम से रूट किया जा सके।
- **मूल इमेज पर बॉक्स ओवरले** करें ताकि विज़ुअल वेरिफिकेशन हो (ऊपर के OpenCV स्निपेट को देखें)।

यदि आपको कोई अजीब व्यवहार मिलता है, तो याद रखें कि सबसे बड़ा फ़ायदा एक ठोस पोस्ट‑प्रोसेसिंग स्टेप से आता है; एक साफ़ स्ट्रिंग कच्चे कैरेक्टर डंप की तुलना में बहुत आसान होती है।

हैप्पी कोडिंग, और आपके OCR पाइपलाइन हमेशा साफ़ रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}