---
category: general
date: 2026-03-18
description: इमेज से टेक्स्ट निकालने के लिए OCR का उपयोग कैसे करें – PNG फ़ाइलों से
  टेक्स्ट पहचानने और OCR के लिए इमेज लोड करने के लिए एक त्वरित गाइड।
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: hi
og_description: इमेज से टेक्स्ट निकालने के लिए OCR का उपयोग कैसे करें – PNG से टेक्स्ट
  पहचानना सीखें, OCR के लिए इमेज लोड करें, और एक सरल Python स्क्रिप्ट के साथ टेक्स्ट
  निकालें।
og_title: 'OCR का उपयोग कैसे करें: पायथन में छवियों से टेक्स्ट निकालें'
tags:
- OCR
- Python
- Image Processing
title: 'OCR का उपयोग कैसे करें: पायथन में छवियों से टेक्स्ट निकालें'
url: /hi/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR कैसे उपयोग करें: Python में इमेज से टेक्स्ट निकालें

क्या आपने कभी **OCR कैसे उपयोग करें** के बारे में सोचा है जब आपके पास एक गड़बड़ स्क्रीनशॉट या स्कैन किया हुआ रसीद हो? आप अकेले नहीं हैं—डेवलपर्स को लगातार चित्रों से पढ़ने योग्य टेक्स्ट निकालना पड़ता है, खासकर PNG फ़ाइलें जो मोबाइल ऐप्स या वेब अपलोड्स से आती हैं। इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे कि कैसे **इमेज से टेक्स्ट निकालें**, **PNG से टेक्स्ट पहचानें**, और यहाँ तक कि **OCR के लिए इमेज लोड करें** केवल कुछ पंक्तियों के Python कोड से।

हम सब कुछ कवर करेंगे, लाइब्रेरी इंस्टॉल करने से लेकर बहुभाषी दस्तावेज़ों को संभालने तक, ताकि अंत तक आप बिल्कुल जान सकें *इमेज से टेक्स्ट कैसे निकालें*। कोई अस्पष्ट संदर्भ नहीं, सिर्फ एक स्पष्ट, चरण‑दर‑चरण समाधान जिसे आप कॉपी‑पेस्ट करके चला सकते हैं।

## आप क्या सीखेंगे

आगे के कुछ सेक्शन में हम करेंगे:

1. एक हल्का OCR इंजन सेट अप करें (कोई भारी निर्भरताएँ नहीं)।  
2. एक इमेज फ़ाइल—विशेष रूप से PNG—को इंजन में लोड करें।  
3. स्वचालित भाषा पहचान सक्षम करें ताकि इंजन बहुभाषी सामग्री को संभाल सके।  
4. पहचान प्रक्रिया चलाएँ और प्लेन‑टेक्स्ट परिणाम प्राप्त करें।  
5. किनारे के मामलों जैसे गायब फ़ाइलें या असमर्थित फ़ॉर्मेट के लिए वर्कफ़्लो को ट्यून करें।

यदि आप बेसिक Python में सहज हैं, तो आप तैयार हैं। पहले से OCR का अनुभव आवश्यक नहीं, हालांकि लाइब्रेरी की डॉक्यूमेंटेशन को एक झटके में देखना हमेशा फायदेमंद रहता है।

---

![PNG इमेज पर OCR कैसे उपयोग करें](placeholder.png "PNG इमेज पर OCR कैसे उपयोग करें – चरण-दर-चरण गाइड")

## OCR कैसे उपयोग करें – इमेज लोड करें और टेक्स्ट पहचानें {#how-to-use-ocr}

### Step 1: OCR लाइब्रेरी इंस्टॉल करें

सबसे पहले, आपको एक Python पैकेज चाहिए जो `OcrEngine` क्लास प्रदान करता हो। इस ट्यूटोरियल के लिए हम काल्पनिक लेकिन स्पष्ट **SimpleOCR** पैकेज का उपयोग करेंगे, जिसे आप pip के माध्यम से इंस्टॉल कर सकते हैं:

```bash
pip install simple-ocr
```

> **Pro tip:** यदि आप वर्चुअल एनवायरनमेंट में काम कर रहे हैं (बहुत अनुशंसित), तो इंस्टॉल कमांड चलाने से पहले उसे सक्रिय करें। इससे आपके प्रोजेक्ट की निर्भरताएँ साफ़ रहती हैं।

### Step 2: इंजन इम्पोर्ट करें और एक इंस्टेंस बनाएं

इंजन बनाना उतना ही आसान है जितना उसके कन्स्ट्रक्टर को कॉल करना। इंजन को वह “ब्रेन” समझें जो बाद में आप द्वारा फीड की गई इमेज को **प्रोसेस** करेगा।

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

हम हर **बार** नया इंस्टेंस क्यों बनाते हैं? अलगाव के लिए। एक नया इंजन यह सुनिश्चित करता है कि पिछले रन की कोई बची‑हुई स्टेट वर्तमान पहचान को दूषित न करे, जो बैच में कई फ़ाइलें प्रोसेस करते समय बहुत महत्वपूर्ण है।

### Step 3: वह इमेज लोड करें जिसे आप **प्रोसेस** करना चाहते हैं

अब हम वास्तव में **OCR के लिए इमेज लोड** करते हैं। `setImageFromFile` मेथड किसी भी रास्टर इमेज का पाथ लेता है; हम इसे `mixed_doc.png` नामक PNG की ओर इंगित करेंगे।

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

यदि फ़ाइल नहीं मिलती, तो `SimpleOCR` एक स्पष्ट `FileNotFoundError` फेंकेगा। आप इसे कैच करके एक दोस्ताना एरर मैसेज दे सकते हैं:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Step 4: स्वचालित भाषा पहचान सक्षम करें

आधुनिक OCR इंजन अक्सर भाषा पैक्स के साथ आते हैं। `"multilingual"` पास करके हम इंजन को टेक्स्ट को sniff करने और सही भाषा मॉडल को स्वचालित रूप से चुनने को कहते हैं। यह विशेष रूप से तब उपयोगी है जब आपका PNG अंग्रेज़ी और स्पेनिश का मिश्रण रखता हो।

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

यदि आपको भाषा पहले से पता है, तो आप `"multilingual"` को `"eng"` या `"spa"` जैसे विशिष्ट लोकेल से बदल सकते हैं ताकि प्रोसेसिंग तेज़ हो।

### Step 5: पहचान प्रक्रिया चलाएँ

यहाँ पर भारी काम होता है। `recognize()` इमेज को स्कैन करता है, सेगमेंटेशन लागू करता है, न्यूरल नेट चलाता है, और आंतरिक रूप से एक टेक्स्ट बफ़र बनाता है।

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

इंजन बैकग्राउंड में करता है:

- **Pre‑processing** (डेस्क्यूइंग, बाइनराइज़ेशन)  
- **Layout analysis** (कॉलम, टेबल का पता लगाना)  
- **Character classification** (डीप‑लर्निंग मॉडल का उपयोग)  

सारा काम एब्स्ट्रैक्टेड है, इसलिए आपको केवल एक लाइन की ज़रूरत है।

### Step 6: पहचाने गए टेक्स्ट को प्राप्त करें और प्रिंट करें

अंत में, हम रिज़ल्ट ऑब्जेक्ट को फेच करते हैं और प्लेन स्ट्रिंग निकालते हैं। यही वह हिस्सा है जहाँ आप वास्तव में **इमेज से टेक्स्ट निकालें**।

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Expected output** (संक्षिप्त रूप में):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

यदि इमेज में **कोई पहचान योग्य कैरेक्टर नहीं** है, तो `text` एक खाली स्ट्रिंग होगी। आप इसे इस तरह हैंडल कर सकते हैं:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## इमेज से टेक्स्ट निकालें – सामान्य किनारे के मामलों को संभालना

### एक फ़ाइल में कई भाषाएँ

जब दस्तावेज़ कई भाषाओं को मिलाता है, तो `"multilingual"` सेटिंग आमतौर पर सही काम करती है। हालांकि, यदि आप गलत पहचान देखते हैं, तो आप मैन्युअली एक फॉलबैक लिस्ट निर्दिष्ट कर सकते हैं:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### गैर‑PNG फ़ॉर्मेट

भले ही हमारा फोकस **PNG से टेक्स्ट पहचानें** हो, `SimpleOCR` JPEG, BMP, और TIFF को भी स्वीकार करता है। बस `setImageFromFile` में फ़ाइल एक्सटेंशन बदल दें। TIFF स्टैक्स के लिए, आपको एक विशिष्ट पेज चुनना पड़ सकता है:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### बड़ी फ़ाइलें और मेमोरी उपयोग

यदि आप गीगापिक्सेल स्कैन प्रोसेस कर रहे हैं, तो OCR से पहले रीसाइज़ करने पर विचार करें:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

रीसाइज़ करने से मेमोरी पर दबाव कम होता है जबकि सटीक पहचान के लिए पर्याप्त विवरण बना रहता है।

### फेल्ड लोड्स का डिबगिंग

कभी‑कभी इमेज आँखों को ठीक लगती है लेकिन आंतरिक रूप से **करप्ट** होती है। इंजन क्या देख रहा है, यह जानने के लिए वर्बोज़ लॉगिंग सक्षम करें:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## पूर्ण, रन‑तैयार स्क्रिप्ट

नीचे पूरा प्रोग्राम है जो सभी हिस्सों को जोड़ता है। इसे `ocr_demo.py` नाम की फ़ाइल में कॉपी करें, `YOUR_DIRECTORY` प्लेसहोल्डर को समायोजित करें, और `python ocr_demo.py` चलाएँ।

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

इस स्क्रिप्ट को चलाने पर `mixed_doc.png` के अंदर की प्लेन‑टेक्स्ट संस्करण आउटपुट होगा। **फ़ाइल** को किसी भी अन्य चित्र से बदलने में **स्वतंत्र** महसूस करें—**इमेज से टेक्स्ट कैसे निकालें** वही तरीका काम करेगा।

---

## निष्कर्ष

हमने अभी-अभी **OCR कैसे उपयोग करें** को Python में **इमेज से टेक्स्ट निकालें** फ़ाइलों के लिए, विशेष रूप से **PNG से टेक्स्ट पहचानें** एसेट्स और **OCR के लिए इमेज लोड करें** के व्यावहारिक चरणों के साथ चलाया। ऊपर दिया गया स्निपेट एक स्व-समाहित समाधान है: पैकेज इंस्टॉल करें, फ़ाइल फीड करें, बहुभाषी डिटेक्शन सक्षम करें, इंजन चलाएँ, और परिणाम प्राप्त करें।

अब आप कर सकते हैं:

- स्क्रिप्ट को वेब सर्विस में इंटीग्रेट करें जो यूज़र अपलोड स्वीकार करे।  
- PNG में कनवर्ट किए गए PDFs के फ़ोल्डर को बैच‑प्रोसेस करें।  
- पोस्ट‑प्रोसेसिंग (जैसे regex क्लीनिंग, स्पेल‑चेकिंग) जोड़ें ताकि सटीकता बढ़े।

याद रखें, OCR की गुणवत्ता इमेज की स्पष्टता, सही भाषा पैक्स, और कभी‑कभी थोड़ा प्री‑प्रोसेसिंग पर निर्भर करती है—तो प्रयोग करते रहें।  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}