---
category: general
date: 2026-06-25
description: Python का उपयोग करके OCR के लिए छवि को पूर्व‑प्रसंस्करण करें और स्कैन
  किए गए दस्तावेज़ से टेक्स्ट पहचानें। पूर्ण कोड के साथ चरण‑दर‑चरण ट्यूटोरियल।
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: hi
og_description: Python के साथ OCR के लिए छवि को पूर्व‑प्रसंस्करण करें और स्कैन किए
  गए दस्तावेज़ से पाठ को पहचानें। इस विस्तृत, चलाने योग्य ट्यूटोरियल का पालन करें।
og_title: Python में OCR के लिए इमेज का प्रीप्रोसेसिंग – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python में OCR के लिए छवि का पूर्व-प्रसंस्करण – पूर्ण मार्गदर्शिका
url: /hi/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR के लिए इमेज प्रीप्रोसेसिंग Python में – पूर्ण गाइड

क्या आपने कभी सोचा है कि **इमेज को OCR के लिए प्रीप्रोसेस** कैसे किया जाए ताकि टेक्स्ट साफ़ और भरोसेमंद निकले? आप अकेले नहीं हैं—ज्यादातर डेवलपर्स को वही समस्या आती है जब स्कैन किया गया पेज तिरछा हो या कॉन्ट्रास्ट बिगड़ गया हो। अच्छी खबर यह है कि कुछ ही लाइनों के Python कोड से आप इस गड़बड़ी को ठीक कर सकते हैं, इमेज को बाइनराइज़ कर सकते हैं, और आपको साफ़, सर्चेबल टेक्स्ट वापस मिल सकता है।

इस ट्यूटोरियल में हम **इमेज को OCR के लिए प्रीप्रोसेस** *और* **स्कैन किए गए डॉक्यूमेंट फ़ाइलों से टेक्स्ट रीकग्नाइज़** करने के सटीक चरणों को देखेंगे, एक लोकप्रिय OCR लाइब्रेरी का उपयोग करके। अंत तक आपके पास एक तैयार‑चलाने‑योग्य स्क्रिप्ट होगी, आप समझेंगे कि हर सेटिंग क्यों महत्वपूर्ण है, और कठिन किनारे के मामलों के लिए इसे कैसे ट्यून किया जाए।

## What You’ll Need

- Python 3.8 या नया (कोड 3.10+ पर भी काम करता है)
- एक OCR पैकेज जो `OcrEngine`, `ImagePreProcessingOptions`, और `Image` क्लासेज़ प्रदान करता हो (उदाहरण में उपयोग किया गया काल्पनिक `ocr` मॉड्यूल)
- एक स्कैन किया हुआ या फ़ोटो लिया हुआ डॉक्यूमेंट जो थोड़ा स्क्यू या लो‑कॉन्ट्रास्ट हो
- आपका पसंदीदा IDE या साधारण टर्मिनल—कोई भारी GUI ज़रूरी नहीं

बस इतना ही। कोई अतिरिक्त बाइनरी नहीं, कोई Docker जिम्नास्टिक नहीं। चलिए शुरू करते हैं।

## Preprocess Image for OCR – Step‑by‑Step

नीचे मुख्य वर्कफ़्लो को पाँच स्पष्ट चरणों में बाँटा गया है। प्रत्येक चरण में **क्यों** हम यह करते हैं, सटीक **कोड**, और एक छोटा **व्याख्यान** शामिल है कि पीछे क्या हो रहा है।

### Step 1: Create an OCR Engine Instance

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Why this matters:*  
`OcrEngine` ऑब्जेक्ट ऑपरेशन का दिमाग है। यह भाषा पैक्स, कॉन्फिडेंस थ्रेशोल्ड, और—हमारे लिए सबसे महत्वपूर्ण—इमेज‑प्रीप्रोसेसिंग फ़्लैग्स जैसी कॉन्फ़िगरेशन रखता है। इसे पहले इंस्टैंशिएट करने से हमें बाद में उपयोग होने वाले ट्रिक्स के लिए एक साफ़ स्लेट मिलती है।

### Step 2: Enable Automatic Deskewing and Binarization

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Why this matters:*  
- **Deskewing** इमेज को घुमाता है ताकि टेक्स्ट की लाइन्स क्षैतिज हो जाएँ। OCR इंजन तब संघर्ष करते हैं जब बेसलाइन कुछ डिग्री से अधिक टिल्ट हो।  
- **Binarization** चित्र को शुद्ध ब्लैक‑एंड‑व्हाइट में बदल देता है, बैकग्राउंड नॉइज़ को हटाता है जो कैरेक्टर क्लासिफ़ायर को भ्रमित कर सकता है।  
दोनों विकल्प कई आधुनिक लाइब्रेरीज़ में *ऑटोमैटिक* होते हैं, लेकिन आपको इन्हें ऑन करना पड़ता है—इसीलिए स्पष्ट असाइनमेंट आवश्यक है।

> **Pro tip:** यदि आपके स्रोत इमेज पहले से ही पूरी तरह अलाइन्ड हैं, तो आप `auto_deskew=False` सेट करके प्रोसेसिंग टाइम का एक मिलीसेकंड बचा सकते हैं।

### Step 3: Load the Skewed Image You Want to Process

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Why this matters:*  
`Image.load` मेथड फ़ाइल को मेमोरी में पढ़ता है और उसे OCR इंजन द्वारा समझे जाने वाले ऑब्जेक्ट में रैप करता है। यह DPI जैसी मेटाडाटा भी निकालता है, जो डेस्क्यूइंग के डिफ़ॉल्ट स्केलिंग फ़ैक्टर को प्रभावित कर सकता है।

> **Edge case:** यदि इमेज एक मल्टी‑पेज TIFF है, तो आपको प्रत्येक पेज पर इटररेट करना पड़ेगा या `ocr.MultiPageImage.load` जैसे हेल्पर का उपयोग करना पड़ेगा। वही प्रीप्रोसेसिंग सेटिंग्स हर पेज पर लागू होंगी।

### Step 4: Perform OCR on the Pre‑processed Image

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Why this matters:*  
अब इंजन हमने पहले सक्षम किए हुए डेस्क्यूइंग और बाइनराइज़ेशन स्टेप्स को लागू करता है, फिर साफ़ किए गए बिटमैप पर अपना न्यूरल नेटवर्क (या क्लासिक Tesseract‑स्टाइल पाइपलाइन) चलाता है। रिटर्न किया गया `result` ऑब्जेक्ट आमतौर पर प्लेन टेक्स्ट, कॉन्फिडेंस स्कोर, और कभी‑कभी प्रत्येक शब्द के पोज़िशनल डेटा को शामिल करता है।

> **What if the text is still garbled?**  
इमेज रेज़ोल्यूशन चेक करें: OCR सबसे अच्छा 300 dpi या उससे अधिक पर काम करता है। यदि आपका स्रोत कम है, तो लोड करने से पहले अपस्केल करने पर विचार करें, या डॉक्यूमेंट स्रोत से मूल स्कैन मांगें।

### Step 5: Output the Recognized Text

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Why this matters:*  
`result.text` वह प्लेन‑स्ट्रिंग है जो इंजन ने पढ़ी है। इसे प्रिंट करना त्वरित डिबगिंग के लिए सुविधाजनक है; वास्तविक एप्लिकेशन में आप इसे `.txt` फ़ाइल, डेटाबेस, या डाउनस्ट्रीम NLP पाइपलाइन में फीड करेंगे।

---

## Recognize Text from Scanned Document – Going Beyond the Basics

अब बेसिक पाइपलाइन काम कर रही है, चलिए कुछ सामान्य वैरिएशन्स देखते हैं जो आपको **स्कैन किए गए डॉक्यूमेंट** इमेजेज़ से टेक्स्ट रीकग्नाइज़ करते समय मिल सकते हैं।

### 1. Handling Multiple Languages

यदि आपके डॉक्यूमेंट में अंग्रेज़ी और फ़्रेंच दोनों हैं, तो स्टेप 1 से पहले इंजन को कॉन्फ़िगर करें:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

अधिकांश OCR इंजन ISO‑639‑2 कोड्स को सपोर्ट करते हैं; अतिरिक्त भाषा पैक्स लोड करने में थोड़ा ओवरहेड लगता है लेकिन मल्टी‑लैंग्वेज पेजेज़ पर सटीकता में उल्लेखनीय सुधार होता है।

### 2. Fine‑Tuning Binarization Thresholds

ऑटोमैटिक बाइनराइज़ेशन अधिकांश मामलों में काम करता है, लेकिन कुछ पुराने फोटोकॉपीज़ को कस्टम थ्रेशोल्ड चाहिए:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

120 से 220 के बीच मानों के साथ प्रयोग करें जब तक बैकग्राउंड हट न जाए और हल्के कैरेक्टर भी न मिटें।

### 3. Extracting Layout Information

कभी‑कभी आपको केवल रॉ टेक्स्ट से अधिक चाहिए—आपको पता होना चाहिए कि प्रत्येक पैराग्राफ पेज पर कहाँ है। कई इंजन `result.blocks` कलेक्शन प्रदान करते हैं:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

यह टेबल्स को री‑कंस्ट्रक्ट करने या कॉलम ऑर्डर को बनाए रखने में अमूल्य है।

### 4. Processing a Batch of Files

यदि आपके पास स्कैन किए हुए PDFs का फ़ोल्डर है जो JPEGs में कन्वर्ट हो चुके हैं, तो पूरे फ्लो को लूप में रैप करें:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

लूप वही `engine` इंस्टेंस पुन: उपयोग करता है, जो प्रत्येक फ़ाइल के लिए नया इंस्टैंस बनाने से अधिक प्रभावी है।

### 5. Dealing with Low‑Resolution Scans

लो‑रेज़ोल्यूशन इमेजेज़ (< 150 dpi) अक्सर धुंधले कैरेक्टर उत्पन्न करती हैं। एक तेज़ समाधान है कि OCR इंजन को फीड करने से पहले हाई‑क्वालिटी एल्गोरिद्म से अपस्केल करें:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

अपस्केलिंग जादू से डिटेल नहीं बनाता, लेकिन बाइनराइज़ेशन स्टेप तेज़ किनारों के साथ काम कर सकता है, जिससे मामूली सुधार मिलता है।

---

## Expected Output

मॉडरेटली स्क्यूड, 300 dpi स्कैन पर मूल पाँच‑स्टेप स्क्रिप्ट चलाने से कुछ इस तरह का आउटपुट प्रिंट होना चाहिए:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

यदि आपको गड़बड़ अक्षर दिखें, तो प्रीप्रोसेसिंग फ़्लैग्स, इमेज रेज़ोल्यूशन, और भाषा कॉन्फ़िगरेशन को दोबारा चेक करें।

---

## Conclusion

हमने वह सब कवर किया जो आपको **इमेज को OCR के लिए प्रीप्रोसेस** और **स्कैन किए गए डॉक्यूमेंट** फ़ाइलों से **टेक्स्ट रीकग्नाइज़** करने के लिए Python में चाहिए। एक नई इंजन इंस्टेंस से शुरू करके, हमने ऑटोमैटिक डेस्क्यूइंग और बाइनराइज़ेशन को सक्षम किया, स्क्यूड इमेज लोड की, रीकग्निशन चलाया, और साफ़ टेक्स्ट प्रिंट किया। साथ ही हमने मल्टी‑लैंग्वेज सपोर्ट, मैन्युअल थ्रेशोल्ड ट्यूनिंग, लेआउट एक्सट्रैक्शन, बैच प्रोसेसिंग, और लो‑रेज़ोल्यूशन वर्कअराउंड्स को भी एक्सप्लोर किया।

स्क्रिप्ट को अपने स्कैन पर आज़माएँ—शायद रसीदों का ढेर, हाथ से लिखा फ़ॉर्म, या पुराना अख़बार क्लिप। एक बार आरामदायक हो जाने पर, PDF जेनरेशन लेयर जोड़ें या आउटपुट को सर्च इंडेक्स में फीड करें। संभावनाएँ अनंत हैं।

**अगली चुनौती के लिए तैयार?** हमारे ट्यूटोरियल देखें *“Extract Tables from Scanned PDFs with Python”* और *“Train Custom OCR Models with TensorFlow”* ताकि आप अपने डॉक्यूमेंट‑ऑटोमेशन टूलबॉक्स को और विस्तारित कर सकें।

Happy coding, and may your OCR always be crisp!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}