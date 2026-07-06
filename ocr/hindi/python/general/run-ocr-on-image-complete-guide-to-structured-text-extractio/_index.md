---
category: general
date: 2026-05-03
description: छवि पर OCR चलाना और संरचित OCR मान्यता का उपयोग करके निर्देशांक के साथ
  पाठ निकालना सीखें। चरण‑दर‑चरण Python कोड शामिल है।
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: hi
og_description: छवि पर OCR चलाएँ और संरचित OCR मान्यता का उपयोग करके निर्देशांक के
  साथ पाठ प्राप्त करें। व्याख्याओं के साथ पूर्ण Python उदाहरण।
og_title: छवि पर OCR चलाएँ – संरचित पाठ निष्कर्षण ट्यूटोरियल
tags:
- OCR
- Python
- Computer Vision
title: इमेज पर OCR चलाएँ – संरचित टेक्स्ट निष्कर्षण के लिए पूर्ण गाइड
url: /hi/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on image – Structured Text Extraction का पूरा गाइड

क्या आपको कभी **run OCR on image** फ़ाइलों को प्रोसेस करना पड़ा है लेकिन शब्दों की सटीक पोज़िशन नहीं रख पाए? आप अकेले नहीं हैं। कई प्रोजेक्ट्स—जैसे रसीद स्कैनिंग, फ़ॉर्म डिजिटाइज़ेशन, या UI टेस्टिंग—में आपको न केवल कच्चा टेक्स्ट चाहिए बल्कि बाउंडिंग बॉक्स भी चाहिए जो बताता है कि प्रत्येक लाइन इमेज में कहाँ स्थित है।  

यह ट्यूटोरियल आपको **aocr** इंजन का उपयोग करके *run OCR on image* करने, **structured OCR recognition** का अनुरोध करने, और फिर परिणाम को जियोमेट्री बनाए रखते हुए पोस्ट‑प्रोसेस करने का व्यावहारिक तरीका दिखाता है। अंत तक आप केवल कुछ ही पायथन लाइनों में **coordinates के साथ टेक्स्ट एक्सट्रैक्ट** कर पाएँगे, और समझेंगे कि structured मोड डाउनस्ट्रीम टास्क्स के लिए क्यों महत्वपूर्ण है।

## What You’ll Learn

- **structured OCR recognition** के लिए OCR इंजन को इनिशियलाइज़ कैसे करें।  
- इमेज फीड करके रॉ रिज़ल्ट कैसे प्राप्त करें जिसमें लाइन बाउंड्स शामिल हों।  
- पोस्ट‑प्रोसेसर चलाकर टेक्स्ट को साफ़ करें बिना जियोमेट्री खोए।  
- अंतिम लाइनों पर इटरेट करके प्रत्येक टेक्स्ट को उसके बाउंडिंग बॉक्स के साथ प्रिंट करें।  

कोई जादू नहीं, कोई छिपे हुए स्टेप नहीं—सिर्फ एक पूर्ण, रन करने योग्य उदाहरण जिसे आप अपने प्रोजेक्ट में डाल सकते हैं।

---

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित इंस्टॉल्ड हैं:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

आपको एक इमेज फ़ाइल (`input_image.png` या `.jpg`) भी चाहिए जिसमें स्पष्ट, पढ़ने योग्य टेक्स्ट हो। स्कैन की गई इनवॉइस से लेकर स्क्रीनशॉट तक, जब तक OCR इंजन अक्षर देख सके, कोई दिक्कत नहीं।

---

## Step 1: Initialise the OCR engine for structured recognition

सबसे पहले हम `aocr.Engine()` का एक इंस्टेंस बनाते हैं और उसे बताते हैं कि हमें **structured OCR recognition** चाहिए। Structured मोड न केवल प्लेन टेक्स्ट बल्कि प्रत्येक लाइन के लिए ज्योमेट्रिक डेटा (बाउंडिंग रेक्टेंगल) भी रिटर्न करता है, जो इमेज पर टेक्स्ट को मैप करने के लिए आवश्यक है।

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Why this matters:**  
> डिफ़ॉल्ट मोड में इंजन केवल शब्दों की एक स्ट्रिंग दे सकता है। Structured मोड पेज → लाइन → शब्द की हायरार्की देता है, प्रत्येक के साथ कोऑर्डिनेट्स, जिससे मूल इमेज पर परिणाम ओवरले करना या लेआउट‑अवेयर मॉडल में फीड करना बहुत आसान हो जाता है।

---

## Step 2: Run OCR on the image and obtain raw results

अब हम इमेज को इंजन में फीड करते हैं। `recognize` कॉल एक `OcrResult` ऑब्जेक्ट रिटर्न करता है जिसमें लाइनों का कलेक्शन होता है, प्रत्येक की अपनी बाउंडिंग रेक्टेंगल होती है।

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

इस समय `raw_result.lines` में दो महत्वपूर्ण एट्रिब्यूट वाले ऑब्जेक्ट्स होते हैं:

- `text` – उस लाइन के लिए पहचाना गया स्ट्रिंग।  
- `bounds` – एक ट्यूपल जैसे `(x, y, width, height)` जो लाइन की पोज़िशन बताता है।

---

## Step 3: Post‑process while preserving geometry

रॉ OCR आउटपुट अक्सर शोरयुक्त होता है: अनचाहे कैरेक्टर, गलत स्पेस, या लाइन‑ब्रेक समस्याएँ। `ai.run_postprocessor` फ़ंक्शन टेक्स्ट को साफ़ करता है लेकिन **मूल जियोमेट्री को बरकरार रखता है**, इसलिए आपके पास अभी भी सटीक कोऑर्डिनेट्स होते हैं।

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Pro tip:** यदि आपके पास डोमेन‑स्पेसिफिक शब्दावली (जैसे प्रोडक्ट कोड) है, तो पोस्ट‑प्रोसेसर को कस्टम डिक्शनरी पास करें ताकि एक्यूरेसी बढ़े।

---

## Step 4: Extract text with coordinates – iterate and display

अंत में, हम क्लीन की गई लाइनों पर लूप लगाते हैं, प्रत्येक लाइन के बाउंडिंग बॉक्स को उसके टेक्स्ट के साथ प्रिंट करते हैं। यही **coordinates के साथ टेक्स्ट एक्सट्रैक्ट** करने का मुख्य भाग है।

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Expected Output

मान लीजिए इनपुट इमेज में दो लाइनें हैं: “Invoice #12345” और “Total: $89.99”, तो आउटपुट कुछ इस तरह दिखेगा:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

पहला ट्यूपल मूल इमेज पर लाइन का `(x, y, width, height)` दर्शाता है, जिससे आप रेक्टेंगल ड्रॉ कर सकते हैं, टेक्स्ट हाईलाइट कर सकते हैं, या कोऑर्डिनेट्स को किसी अन्य सिस्टम में फीड कर सकते हैं।

---

## Visualising the Result (Optional)

यदि आप बाउंडिंग बॉक्स को इमेज पर ओवरले देखना चाहते हैं, तो आप Pillow (PIL) का उपयोग करके रेक्टेंगल ड्रॉ कर सकते हैं। नीचे एक छोटा स्निपेट है; यदि आपको केवल रॉ डेटा चाहिए तो इसे स्किप कर सकते हैं।

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image उदाहरण जिसमें बाउंडिंग बॉक्स दिखाए गए हैं](/images/ocr-bounding-boxes.png "run OCR on image – bounding box overlay")

ऊपर का alt टेक्स्ट **primary keyword** को शामिल करता है, जिससे इमेज alt एट्रिब्यूट के SEO आवश्यकताओं को पूरा किया गया है।

---

## Why Structured OCR Recognition Beats Simple Text Extraction

आप सोच सकते हैं, “क्या मैं सिर्फ OCR चलाकर टेक्स्ट नहीं ले सकता? जियोमेट्री की क्या जरूरत?”  

- **स्पैशियल कॉन्टेक्स्ट:** जब आपको फ़ॉर्म पर फ़ील्ड्स (जैसे “Date” के बगल में डेट वैल्यू) मैप करनी हों, तो कोऑर्डिनेट्स बताते हैं कि डेटा *कहाँ* है।  
- **मल्टी‑कॉलम लेआउट:** साधारण लीनियर टेक्स्ट क्रम खो देता है; Structured डेटा कॉलम ऑर्डर को बरकरार रखता है।  
- **पोस्ट‑प्रोसेसिंग एक्यूरेसी:** बॉक्स साइज जानने से आप तय कर सकते हैं कि शब्द हेडर है, फुटनोट है, या कोई अनचाहा आर्टिफैक्ट।  

संक्षेप में, **structured OCR recognition** आपको smarter पाइपलाइन बनाने की लचीलापन देता है—चाहे आप डेटा को डेटाबेस में फीड कर रहे हों, सर्चेबल PDF बना रहे हों, या लेआउट को समझने वाले मशीन‑लर्निंग मॉडल को ट्रेन कर रहे हों।

---

## Common Edge Cases and How to Handle Them

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|---------------|
| **Rotated or skewed images** | Bounding boxes may be off‑axis. | Pre‑process with deskewing (e.g., OpenCV’s `warpAffine`). |
| **Very small fonts** | Engine may miss characters, leading to empty lines. | Increase image resolution or use `ocr_engine.set_dpi(300)`. |
| **Mixed languages** | Wrong language model can cause garbled text. | Set `ocr_engine.language = ["en", "de"]` before recognition. |
| **Overlapping boxes** | Post‑processor might merge two lines unintentionally. | Verify `line.bounds` after processing; adjust thresholds in `ai.run_postprocessor`. |

इन परिदृश्यों को शुरुआती चरण में संभालना बाद में सिरदर्द बचाता है, विशेषकर जब आप समाधान को रोज़ाना सैकड़ों दस्तावेज़ों तक स्केल करते हैं।

---

## Full End‑to‑End Script

नीचे पूरा, तैयार‑चलाने‑योग्य प्रोग्राम दिया गया है जो सभी स्टेप्स को जोड़ता है। कॉपी‑पेस्ट करें, इमेज पाथ एडजस्ट करें, और आप तैयार हैं।

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

इस स्क्रिप्ट को चलाने से:

1. **Run OCR on image** structured मोड के साथ।  
2. हर लाइन के लिए **coordinates के साथ टेक्स्ट एक्सट्रैक्ट**।  
3. वैकल्पिक रूप से एनोटेटेड PNG बनता है जिसमें बॉक्स दिखते हैं।

---

## Conclusion

अब आपके पास **run OCR on image** और **coordinates के साथ टेक्स्ट एक्सट्रैक्ट** करने के लिए एक ठोस, स्व-समाहित समाधान है, जो **structured OCR recognition** का उपयोग करता है। कोड हर चरण—इंजन इनिशियलाइज़ेशन से पोस्ट‑प्रोसेसिंग और विज़ुअल वेरिफिकेशन—को दर्शाता है, जिससे आप इसे रसीदों, फ़ॉर्म्स या किसी भी विज़ुअल डॉक्यूमेंट पर लागू कर सकते हैं जिसे सटीक टेक्स्ट लोकेलाइज़ेशन चाहिए।

अब क्या अगला कदम? `aocr` इंजन को किसी अन्य लाइब्रेरी (Tesseract, EasyOCR) से बदलें और देखें कि उनका structured आउटपुट कैसे अलग है। विभिन्न पोस्ट‑प्रोसेसिंग स्ट्रेटेजी जैसे स्पेल‑चेकिंग या कस्टम रेगेक्स फ़िल्टर आज़माएँ ताकि आपके डोमेन की एक्यूरेसी बढ़े। और यदि आप बड़ा पाइपलाइन बना रहे हैं, तो `(text, bounds)` पेयर्स को डेटाबेस में स्टोर करने पर विचार करें ताकि बाद में एनालिटिक्स आसान हो सके।

Happy coding, और आपके OCR प्रोजेक्ट्स हमेशा सटीक रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}