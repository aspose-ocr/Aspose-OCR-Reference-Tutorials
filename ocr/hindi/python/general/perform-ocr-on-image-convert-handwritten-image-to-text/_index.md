---
category: general
date: 2026-03-18
description: छवि पर OCR करें और फोटो से हस्तलेखित पाठ निकालें। जानें कि हस्तलेखित
  छवि को कैसे परिवर्तित करें, JPG से पाठ निकालें, और फोटो से पाठ को पहचानें।
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: hi
og_description: फ़ोटो से हस्तलिखित पाठ निकालने के लिए छवि पर OCR करें। यह ट्यूटोरियल
  दिखाता है कि कैसे हस्तलिखित छवि को परिवर्तित करें और JPG फ़ाइलों से पाठ को पहचानें।
og_title: छवि पर OCR करें – पूर्ण हस्तलिखित पाठ मार्गदर्शिका
tags:
- OCR
- Python
- Handwriting Recognition
title: छवि पर OCR करें – हस्तलिखित छवि को पाठ में बदलें
url: /hi/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज पर OCR करें – फुल‑स्टैक हैंडरिटन टेक्स्ट एक्सट्रैक्शन

क्या आपको कभी **perform OCR on image** फ़ाइलों को प्रोसेस करना पड़ा लेकिन यह नहीं पता था कि इंजन गंदे हाथ‑लिखे टेक्स्ट को पढ़ पाएगा या नहीं? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया के ऐप्स में—जैसे खर्च‑रसीद स्कैनर या नोट‑टेकिंग यूटिलिटीज़—आपको ऐसे फ़ोटो मिलेंगे जिनमें लिखावट है और जिन्हें साधारण टेक्स्ट में बदलना होगा।  

इस गाइड में हम दिखाएंगे कि कैसे **convert handwritten image** फ़ाइलों को, **extract text from jpg**, और यहाँ तक कि **recognize text from photo** स्ट्रीम्स को एक छोटे Python‑स्टाइल लाइब्रेरी `ocr` की मदद से किया जा सकता है। अंत तक आपके पास एक तैयार‑स्क्रिप्ट होगी जो हाथ‑लिखे नोट से हर शब्द निकाल लेगी, चाहे पेन कितना भी डगमगाया हो।

## What You’ll Need

- Python 3.8+ (कोड किसी भी हालिया इंटरप्रेटर पर काम करता है)
- काल्पनिक `ocr` पैकेज – इसे `pip install ocr-lib` से इंस्टॉल करें (अपने वास्तविक पैकेज नाम से बदलें)
- एक स्पष्ट फ़ोटोग्राफ़ एक हाथ‑लिखे नोट का, saved as `note.jpg` (या कोई भी अन्य इमेज फ़ॉर्मेट)
- थोड़ी जिज्ञासा—कोई उन्नत ML बैकग्राउंड जरूरी नहीं

बस इतना ही। कोई बाहरी सर्विस, कोई API की नहीं, सिर्फ एक लोकल इंजन जो **perform OCR on image** डेटा को प्रोसेस कर सके।

![perform OCR on image screenshot](example.png)

*Alt text: perform OCR on image स्क्रीनशॉट जिसमें OCR स्क्रिप्ट वाला कोड एडिटर दिख रहा है।*

## Step‑by‑Step Implementation

नीचे हम प्रक्रिया को छोटे‑छोटे हिस्सों में बाँटते हैं। प्रत्येक हेडर में एक कीवर्ड है ताकि आप जल्दी स्किम कर सकें, और हर ब्लॉक यह समझाता है **क्यों** हम यह कर रहे हैं—सिर्फ **क्या** नहीं।

### Step 1: Install and Verify the OCR Library

**perform OCR on image** फ़ाइलों को प्रोसेस करने से पहले, लाइब्रेरी आपके वातावरण में मौजूद होनी चाहिए। टर्मिनल खोलें और चलाएँ:

```bash
pip install ocr-lib
```

> **Pro tip:** यदि आप वर्चुअल एनवायरनमेंट में काम कर रहे हैं (बहुत सुझाया जाता है), तो पहले उसे एक्टिवेट करें। इससे डिपेंडेंसीज़ साफ़ रहती हैं और वर्ज़न कॉन्फ्लिक्ट से बचा जा सकता है।

इंस्टॉलेशन के बाद, सुनिश्चित करें कि Python पैकेज को इम्पोर्ट कर सकता है:

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

यदि आपको सफलता संदेश दिखे, तो आप **convert handwritten image** डेटा को प्रोसेस करने के लिए तैयार हैं।

### Step 2: Create an Engine Instance and Choose Handwritten Mode

अधिकांश OCR इंजन डिफ़ॉल्ट रूप से प्रिंटेड‑टेक्स्ट को पहचानते हैं। चूँकि हम **extract handwritten text** चाहते हैं, हमें मोड को स्पष्ट रूप से बदलना होगा। यह स्टेप महत्वपूर्ण है क्योंकि हैंडराइटिंग अक्सर अलग प्री‑प्रोसेसिंग (जैसे स्ट्रोक स्मूदिंग) की माँग करती है।

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*Why this matters:* हैंडराइटेड कैरेक्टर्स आकार और झुकाव में बहुत विविध हो सकते हैं। `RecognitionMode.HANDWRITTEN` सेट करने से इंजन कर्सिव सैंपल्स पर प्रशिक्षित मॉडल लागू करता है, जिससे सटीकता में काफी बढ़ोतरी होती है।

### Step 3: Load the Photo You Want to Analyze

अब हम वास्तव में **perform OCR on image** कंटेंट को प्रोसेस करेंगे। `load_image` मेथड एक पाथ या फ़ाइल‑जैसे ऑब्जेक्ट को स्वीकार करता है। डेमो के लिए हम JPEG लोड करेंगे, लेकिन वही कॉल PNG, BMP, या यहाँ तक कि PDF पेजेज़ के लिए भी काम करता है।

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

यदि आपकी इमेज क्लाउड बकेट में है, तो पहले उसे डाउनलोड करें या `BytesIO` स्ट्रीम पास करें—`ocr` दोनों को हैंडल करने में लचीला है।

### Step 4: Run the Recognition Process

इंजन तैयार है और इमेज मेमोरी में है, अब हम अंततः **perform OCR on image** करेंगे और रॉ टेक्स्ट प्राप्त करेंगे।

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

`recognize()` कॉल एक साधारण Unicode स्ट्रिंग रिटर्न करता है। अधिकांश उपयोग‑केस में आप इसे सीधे `.txt` फ़ाइल में लिख सकते हैं, नेचुरल‑लैंग्वेज पाइपलाइन को फीड कर सकते हैं, या GUI में दिखा सकते हैं।

### Step 5: Optional – Clean Up or Post‑Process the Output

हैंडराइटन OCR पूरी तरह परफेक्ट नहीं होता; अक्सर आपको अनावश्यक लाइन ब्रेक या गलत पढ़े गए कैरेक्टर्स मिलते हैं। एक त्वरित क्लीन‑अप स्टेप डाउनस्ट्रीम रिज़ल्ट्स को बेहतर बना सकता है।

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

अपने डोमेन के अनुसार स्पेल‑चेकर्स, लैंग्वेज मॉडल्स, या कस्टम रेगेक्स जोड़ें।

### Full Script – Ready to Copy & Paste

सब कुछ मिलाकर, यहाँ पूरा, रन करने योग्य प्रोग्राम है जो JPEG से **extracts handwritten text** करता है और साफ़ परिणाम प्रिंट करता है।

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**Expected output** (आपका वास्तविक टेक्स्ट अलग होगा, बेशक):

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

यदि आपको गड़बड़ टेक्स्ट दिखे, तो इमेज क्वालिटी (अच्छी लाइटिंग, न्यूनतम ब्लर) दोबारा चेक करें और सुनिश्चित करें कि आप `HANDWRITTEN` मोड में हैं। ये दो कारक अधिकांश पहचान त्रुटियों के मुख्य कारण हैं।

## Frequently Asked Questions (FAQ)

| Question | Answer |
|----------|--------|
| **Can I use this to extract text from a PNG?** | बिल्कुल। `engine.load_image("scan.png")` भी वही काम करता है। |
| **What if my image is a PDF page?** | पहले पेज को इमेज में बदलें (जैसे `pdf2image` से) फिर उसे इंजन को दें। |
| **Is the library thread‑safe?** | हाँ, आप प्रत्येक थ्रेड के लिए अलग `OcrEngine` ऑब्जेक्ट बना सकते हैं। |
| **How does this differ from `pytesseract`?** | `ocr` Tesseract बाइनरी को एब्स्ट्रैक्ट करता है और एक बिल्ट‑इन हैंडरिटन मॉडल शामिल करता है, इसलिए आपको बाहरी एक्सिक्यूटेबल इंस्टॉल करने की ज़रूरत नहीं। |
| **What if I need to **extract text from JPG** files in bulk?** | स्क्रिप्ट को लूप में रैप करें, या प्रत्येक फ़ाइल के लिए `engine.load_image` कॉल करें और परिणामों को लिस्ट या CSV में इकट्ठा करें। |

## Edge Cases & Best Practices

1. **Low‑contrast photos** – लोड करने से पहले प्रोग्रामेटिकली कॉन्ट्रास्ट बढ़ाएँ, या `engine.apply_preprocessing('contrast', level=2)` इस्तेमाल करें।
2. **Mixed printed & handwritten** – दो पास चलाएँ: पहले `HANDWRITTEN`, फिर `PRINTED`, और आउटपुट को मर्ज करें।
3. **Large images** – चौड़ाई को ~1500 px तक डाउनस्केल करें; OCR इंजन छोटे बफ़र के साथ तेज़ काम करते हैं बिना सटीकता खोए।
4. **Unicode characters** – लाइब्रेरी UTF‑8 स्ट्रिंग्स रिटर्न करती है, इसलिए आप इमोजी, एक्सेंटेड लेटर्स, या गणितीय सिंबल्स को सीधे हैंडल कर सकते हैं।

## Wrap‑Up

हमने अभी-अभी एक ठोस उदाहरण के साथ दिखाया कि कैसे **perform OCR on image** फ़ाइलों को प्रोसेस किया जाए, विशेष रूप से हैंडरिटन नोट्स के लिए। `ocr` पैकेज को इंस्टॉल करके, इंजन को `HANDWRITTEN` मोड में कॉन्फ़िगर करके, फोटो लोड करके, और `recognize()` कॉल करके, आप **convert handwritten image** डेटा को साफ़, सर्चेबल टेक्स्ट में बदल सकते हैं।  

अब आप **extract text from jpg** फ़ाइलों को बैच में प्रोसेस कर सकते हैं, आउटपुट को नोट‑टेकिंग ऐप में फीड कर सकते हैं, या एक्सेसिबिलिटी के लिए स्पीच सिंथेसिस के साथ जोड़ सकते हैं। संभावनाएँ असीम हैं, और ऊपर दिया गया कोड आपको प्रयोग करने के लिए एक मजबूत आधार देता है।

क्या आपके पास कोई ट्विस्ट है—शायद अलग फ़ाइल फ़ॉर्मेट या कोई मज़ेदार प्री‑प्रोसेसिंग ट्रिक? कमेंट में शेयर करें, और बातचीत जारी रखें। Happy coding, और उन स्क्रिबल्स को डिजिटल गोल्ड में बदलने का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}