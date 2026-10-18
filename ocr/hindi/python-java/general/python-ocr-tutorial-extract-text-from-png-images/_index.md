---
category: general
date: 2026-06-25
description: Python OCR ट्यूटोरियल जो आपको दिखाता है कि कैसे टेक्स्ट PNG फ़ाइलों से
  निकालें, टेक्स्ट इमेज पढ़ें, और एक सरल, लाइसेंस‑फ्री इंजन का उपयोग करके इमेज टेक्स्ट
  को पहचानें।
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: hi
og_description: Python OCR ट्यूटोरियल आपको OCR के लिए इमेज लोड करना, PNG फ़ाइलों से
  टेक्स्ट निकालना, और कुछ ही कोड लाइनों में इमेज टेक्स्ट को पहचानना सिखाता है।
og_title: Python OCR ट्यूटोरियल – PNG से टेक्स्ट निकालें
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: 'पायथन OCR ट्यूटोरियल: PNG छवियों से पाठ निकालें'
url: /hi/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR ट्यूटोरियल – PNG इमेज से टेक्स्ट निकालें

क्या आपने कभी सोचा है कि **python ocr tutorial** कैसे रसीद की स्क्रीनशॉट को संपादन योग्य टेक्स्ट में बदल सकता है? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में हमें *read text image* फ़ाइलें जल्दी से पढ़नी होती हैं, और खुद करना हर बार GUI से कॉपी‑पेस्ट करने से बेहतर है।  

इस गाइड में हम एक हैंड‑ऑन उदाहरण के माध्यम से चलेंगे जो **extracts text PNG** फ़ाइलें निकालता है, आपको दिखाता है कि *load image for OCR* कैसे किया जाता है, और अंत में *recognize image text* परिणाम को प्रिंट करता है—सब कुछ एक मुफ्त, केवल‑मूल्यांकन OCR इंजन के साथ। कोई लाइसेंस की नहीं, कोई भारी डिपेंडेंसी नहीं—सिर्फ सादा Python और कुछ छोटे पैकेज।

## आप क्या सीखेंगे

- हल्के OCR लाइब्रेरी को कैसे इंस्टॉल और इम्पोर्ट करें।
- **load image for OCR** करने के सटीक चरण और सामान्य समस्याओं से कैसे निपटें।
- विभिन्न गुणवत्ता की *read text image* फ़ाइलों को पढ़ने के तरीके।
- **extract text png** फ़ाइलों की सटीकता बढ़ाने के टिप्स।
- पहचाने गए स्ट्रिंग को कैसे दिखाएँ और वैकल्पिक रूप से डिस्क पर लिखें।

इस ट्यूटोरियल के अंत तक आपके पास एक पुन: उपयोग योग्य स्क्रिप्ट होगी जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं जहाँ आपको **recognize image text** तुरंत चाहिए। कोई जादू नहीं, बस स्पष्ट कोड और व्याख्याएँ।

### पूर्वापेक्षाएँ

- Python 3.8 या नया (लाइब्रेरी 3.7+ के साथ काम करती है लेकिन 3.8+ की सलाह दी जाती है)।
- pip और वर्चुअल एनवायरनमेंट की बुनियादी जानकारी।
- `sample.png` नाम की एक इमेज फ़ाइल (या कोई भी PNG जिसे आप टेस्ट करना चाहते हैं) जो आप रेफ़रेंस कर सकें।

यदि इनमें से कोई भी अपरिचित लग रहा हो, तो एक मिनट रुकें और उन्हें सेट‑अप कर लें—विश्वास कीजिए, परिणाम इसके लायक है।

---

## Python OCR ट्यूटोरियल – इंजन सेट‑अप

सबसे पहले: हमें एक OCR इंजन ऑब्जेक्ट चाहिए। वह लाइब्रेरी जिसे हम उपयोग करेंगे, एक छोटे रैपर है जो एक नेटिव OCR इंजन के चारों ओर बना है और मूल्यांकन के लिए बॉक्स से बाहर काम करता है। इसे लाइसेंस की की आवश्यकता नहीं होती, जिससे **python ocr tutorial** तेज़ प्रोटोटाइप बनाने के लिए परफ़ेक्ट बन जाता है।

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**क्यों महत्वपूर्ण है:** इंजन बनाकर OCR रन‑टाइम को आपके बाकी कोड से अलग किया जाता है, जिससे आप कई इमेज पर बिना बार‑बार भारी रिसोर्सेज़ को री‑इनिशियलाइज़ किए इसे पुनः उपयोग कर सकते हैं।

---

## Load Image for OCR – PNG फ़ाइल पढ़ना

अब जब इंजन मौजूद है, हमें *load image for OCR* करना होगा। लाइब्रेरी का `Image.load` मेथड पाथ लेता है और स्वचालित रूप से PNG, JPEG, BMP, और कुछ अन्य फॉर्मैट डिकोड कर देता है।

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **Pro tip:** यदि आपकी PNG में अल्फा चैनल है, तो लाइब्रेरी इसे स्वचालित रूप से हटा देगी। हालांकि, *read text image* कार्यों के लिए सबसे अच्छे परिणाम पाने हेतु इमेज को ग्रेस्केल में रखें—यह शोर को कम करता है और पहचान की गति बढ़ाता है।

---

## Recognize Image Text – OCR इंजन चलाना

इमेज ऑब्जेक्ट तैयार होने के बाद, हम अंततः **recognize image text** कर सकते हैं। यह *python ocr tutorial* का मुख्य भाग है और केवल एक लाइन के कोड से किया जाता है।

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**अंदर क्या हो रहा है?** इंजन कई प्री‑प्रोसेसिंग फ़िल्टर (डेस्क्यू, बाइनराइज़ेशन) चलाता है और फिर बिटमैप को एक न्यूरल नेटवर्क में फीड करता है जिसे लाखों कैरेक्टर पर प्रशिक्षित किया गया है। इसलिए आप अक्सर कम‑रिज़ॉल्यूशन PNG पर भी आश्चर्यजनक रूप से सटीक आउटपुट देखते हैं।

---

## निकाले गए टेक्स्ट को दिखाएँ और सेव करें

परिणाम मिलना अच्छा है, लेकिन आप शायद इसे देखना या कहीं स्टोर करना चाहेंगे। `result` ऑब्जेक्ट एक `text` एट्रिब्यूट एक्सपोज़ करता है जिसमें साधारण स्ट्रिंग आउटपुट रहता है।

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**अपेक्षित आउटपुट** (मान लीजिए `sample.png` में “Hello, OCR!” लिखा है):

```
Eval-mode result: Hello, OCR!
```

यदि आपको पढ़ने योग्य कैरेक्टर की बजाय गड़बड़ मिल रही है, तो सामान्य फिक्स के लिए अगले सेक्शन को देखें।

---

## जब आप Extract Text PNG करते हैं तो सामान्य समस्याएँ

सबसे बेहतरीन OCR इंजन भी कुछ इमेज पर फँस जाते हैं। नीचे सामान्य बाधाएँ और उनके समाधान दिए गए हैं।

### 1. कम कंट्रास्ट या डार्क बैकग्राउंड

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. तिरछी टेक्स्ट लाइन्स

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. गैर‑अंग्रेज़ी कैरेक्टर

यदि आपकी PNG में एक्सेंटेड लेटर्स या गैर‑लैटिन स्क्रिप्ट हैं, तो इंजन को उचित भाषा पैक के साथ इनिशियलाइज़ करें:

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. बहुत बड़ी इमेज

4000×3000 PNG को प्रोसेस करना धीमा हो सकता है। पठनीयता बनाए रखते हुए इसे डाउनस्केल करें:

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

ये ट्यूनिंग्स एक मजबूत *python ocr tutorial* का हिस्सा हैं जो हॅपी‑पाथ से परे भी काम करता है।

---

## पूर्ण स्क्रिप्ट – वन‑फ़ाइल समाधान

नीचे पूरी, तैयार‑चलाने‑योग्य स्क्रिप्ट है जिसमें सभी चरण और वैकल्पिक सुधार शामिल हैं। इसे `ocr_extract.py` में कॉपी‑पेस्ट करें और `python ocr_extract.py` चलाएँ।

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**चलाएँ:**  
```bash
python ocr_extract.py ./sample.png
```

आपको पहचाना गया स्ट्रिंग प्रिंट होते हुए दिखेगा और इमेज के बगल में `sample_extracted.txt` फ़ाइल बन जाएगी।

---

## विज़ुअल ओवरव्यू

![Python OCR tutorial – load image for OCR and extract text from PNG](/images/python-ocr-flow.png)

*Alt text:* *Python OCR ट्यूटोरियल डायग्राम जो लोड इमेज फॉर OCR से टेक्स्ट PNG निकालने तक का फ्लो दिखाता है।*

डायग्राम **load image for OCR** → **recognize image text** → **extract text PNG** की रैखिक प्रगति को दर्शाता है और जहाँ आप प्री‑प्रोसेसिंग स्टेप्स इन्जेक्ट कर सकते हैं, उसे हाईलाइट करता है।

---

## निष्कर्ष

हमने अभी एक **python ocr tutorial** पूरा किया जो दिखाता है कि *load image for OCR*, *recognize image text*, और अंत में **extract text png** फ़ाइलें केवल कुछ Python कमांड्स से कैसे निकाली जा सकती हैं। स्क्रिप्ट पूरी तरह कार्यशील है, सामान्य एज केस को संभालती है, और बैच प्रोसेसिंग या मल्टी‑लैंग्वेज सपोर्ट के लिए विस्तारित की जा सकती है।

अगली चुनौती के लिए तैयार हैं? PDF को इमेज में बदलकर इंजन को फीड करें, विभिन्न भाषा पैक्स के साथ प्रयोग करें, या OCR स्टेप को एक Flask API में इंटीग्रेट करें ताकि आपका वेब ऐप अपलोडेड स्क्रीनशॉट को रियल‑टाइम पढ़ सके। *read text image* ऑटोमेशन की संभावनाएँ लगभग अनंत हैं।

कोई सवाल या ऐसी जटिल इमेज है जिसे आप नहीं तोड़ पा रहे? नीचे कमेंट करें, और मिलकर ट्रबलशूट करें। Happy coding!

## आगे क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}