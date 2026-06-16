---
category: general
date: 2026-03-26
description: 'Python OCR ट्यूटोरियल: सीखें कि कैसे इमेज से टेक्स्ट निकालें, OCR के
  लिए इमेज लोड करें और Aspose OCR का उपयोग करके रसीद से टेक्स्ट पहचानें, केवल कुछ
  ही चरणों में।'
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: hi
og_description: 'Python OCR ट्यूटोरियल: जल्दी सीखें कि इमेज से टेक्स्ट कैसे निकाला
  जाए, OCR के लिए इमेज लोड करें और Aspise OCR के साथ रसीद से टेक्स्ट पहचानें।'
og_title: Python OCR ट्यूटोरियल – छवि से टेक्स्ट निकालें
tags:
- OCR
- Aspose
- Python
title: Python OCR ट्यूटोरियल – Aspose के साथ छवि से टेक्स्ट निकालें
url: /hi/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR tutorial – Aspose के साथ इमेज से टेक्स्ट निकालें

क्या आपने कभी सोचा है कि धुंधली रसीद या स्कैन किए गए फॉर्म से टेक्स्ट कैसे निकालें बिना कस्टम रेगेक्स लिखने में घंटों खर्च किए? आप अकेले नहीं हैं। इस **python ocr tutorial** में हम OCR के लिए इमेज लोड करने, Python में OCR करने, और अंत में Aspose OCR लाइब्रेरी का उपयोग करके रसीद फ़ाइलों से टेक्स्ट पहचानने की प्रक्रिया देखेंगे।  

इस गाइड के अंत तक आपके पास एक तैयार‑चलाने‑योग्य स्क्रिप्ट होगी जो किसी भी समर्थित इमेज फ़ॉर्मेट को पढ़ेगी, टेक्स्ट निकालेंगी, और उसे कंसोल में प्रिंट करेगी। कोई बाहरी सर्विस नहीं, कोई API कुंजी नहीं—सिर्फ शुद्ध Python और एक शक्तिशाली OCR इंजन।  

## आपको क्या चाहिए

- Python 3.8 या नया (कोड टाइप हिंट्स का उपयोग करता है, इसलिए नवीनतम इंटरप्रेटर बेहतर है)
- `asposeocrjava` पैकेज `pip install aspose-ocr` द्वारा इंस्टॉल किया गया
- एक सैंपल इमेज – उदाहरण के लिए `receipt_noisy.jpg` जिसमें एक सामान्य स्टोर रसीद है
- (वैकल्पिक) डिपेंडेंसीज़ को व्यवस्थित रखने के लिए एक वर्चुअल एनवायरनमेंट

यदि आपने ये सभी बिंदु पूरे कर लिए हैं, तो हम सीधे कोड की ओर बढ़ सकते हैं।  

## चरण 1: Aspose OCR क्लासेज़ को इंस्टॉल और इम्पोर्ट करें

सबसे पहले, सुनिश्चित करें कि Aspose OCR पैकेज उपलब्ध है। फिर उन क्लासेज़ को इम्पोर्ट करें जिनकी हमें आवश्यकता होगी।

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**क्यों यह महत्वपूर्ण है:** केवल आवश्यक सिम्बॉल्स को इम्पोर्ट करने से नेमस्पेस साफ़ रहता है और इंटरप्रेटर को बताता है कि लाइब्रेरी के कौन से हिस्से हम वास्तव में उपयोग कर रहे हैं। यह बाद के कोड लाइनों को भी छोटा करता है, जिससे ट्यूटोरियल को फॉलो करना आसान हो जाता है।

> **प्रो टिप:** यदि आप Jupyter नोटबुक का उपयोग कर रहे हैं, तो इंस्टॉल लाइन के पहले `!` लगाएँ ताकि वह सेल के भीतर चल सके।

## चरण 2: OCR इंजन बनाएं और डीप‑लर्निंग मोड सक्षम करें

Aspose कई इंजन मोड्स प्रदान करता है। अधिकांश वास्तविक रसीदों के लिए, डीप‑लर्निंग मॉडल सबसे अधिक सटीकता देता है, विशेषकर शोरयुक्त स्कैन पर।

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**डीप‑लर्निंग क्यों?** पारंपरिक रूल‑बेस्ड OCR कम कॉन्ट्रास्ट या विकृत अक्षरों पर फंस सकता है। लाखों ग्लिफ़्स पर प्रशिक्षित डीप‑लर्निंग मॉडल विविधताओं के साथ बेहतर अनुकूल होता है—बिल्कुल वही जो आपको *Python में OCR करने* के लिए चाहिए जब आप फ़ोन कैमरा से ली गई रसीदों पर काम कर रहे हों।

## चरण 3: OCR के लिए इमेज लोड करें

अब हम वास्तव में **OCR के लिए इमेज लोड** करेंगे। Aspose.Imaging PNG, JPEG, BMP, TIFF आदि को सपोर्ट करता है, इसलिए आप इसे किसी भी दस्तावेज़ की तस्वीर पर पॉइंट कर सकते हैं।

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**सामान्य गलती:** इंजन पर इमेज सेट करना भूल जाने से रनटाइम पर `NullReferenceException` आता है। फ़ाइल लोड करने के बाद हमेशा `set_image` कॉल करें।

## चरण 4: OCR करें और टेक्स्ट निकालें

इंजन तैयार और इमेज जुड़ी होने के बाद, हम अंततः **Python में OCR कर** सकते हैं और टेक्स्ट परिणाम प्राप्त कर सकते हैं।

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

`recognize()` मेथड एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें केवल कच्चा टेक्स्ट नहीं, बल्कि कॉन्फिडेंस स्कोर, बाउंडिंग बॉक्स और भाषा जानकारी भी होती है। एक तेज़ **इमेज से टेक्स्ट निकालने** के उपयोग केस के लिए हमें केवल `get_text()` चाहिए।

## चरण 5: पहचाने गए टेक्स्ट को दिखाएँ

आइए देखें कि इंजन ने रसीद से वास्तव में क्या पढ़ा।

```python
print("Recognized text:\n", recognized_text)
```

सामान्य आउटपुट इस प्रकार दिखता है:

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

यदि आउटपुट में गड़बड़ अक्षर दिखें, तो इमेज को OCR इंजन में लोड करने से पहले प्री‑प्रोसेस करने पर विचार करें (जैसे कॉन्ट्रास्ट बढ़ाना या डेस्क्यू फ़िल्टर लगाना)। Aspose.Imaging इमेज‑एन्हांसमेंट टूल्स का पूरा सूट प्रदान करता है जिसे आप एक साथ जोड़ सकते हैं।

## एज केस को संभालना और बेहतर सटीकता के टिप्स

### 1. अत्यधिक शोरयुक्त रसीदों से निपटना
यदि रसीद बहुत अधिक धुंधली है, तो आप तेज़ लेकिन कम सटीक पास के लिए `OcrEngineMode.HIGH_SPEED` मोड पर स्विच कर सकते हैं, फिर साफ़ की गई इमेज पर `DEEP_LEARNING` में दूसरा पास चला सकते हैं।

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. भाषा निर्दिष्ट करना
डिफ़ॉल्ट रूप से Aspose भाषा को ऑटो‑डिटेक्ट करने की कोशिश करता है। अंग्रेज़ी रसीदों के लिए आप इसे फिक्स कर सकते हैं:

```python
ocr_engine.set_language("eng")
```

### 3. मेमोरी मैनेजमेंट
जब लूप में कई इमेज प्रोसेस कर रहे हों, तो स्पष्ट रूप से रिसोर्सेज़ रिलीज़ करें:

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. OCR परिणाम को फ़ाइल में सहेजना
कभी-कभी आपको निकाले गए टेक्स्ट को बाद के विश्लेषण के लिए सहेजना पड़ता है।

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## पूर्ण कार्यशील उदाहरण

नीचे पूरा स्क्रिप्ट दिया गया है जो सभी भागों को जोड़ता है। इसे `receipt_ocr.py` नाम की फ़ाइल में कॉपी‑पेस्ट करें, इमेज पाथ को समायोजित करें, और `python receipt_ocr.py` चलाएँ।

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

स्क्रिप्ट चलाने पर रसीद की सामग्री आपके कंसोल में दिखेगी और साथ ही `receipt_output.txt` फ़ाइल भी उसी डेटा के साथ बन जाएगी।

![Python OCR ट्यूटोरियल – नमूना रसीद आउटपुट](https://example.com/receipt_output.png "python ocr ट्यूटोरियल उदाहरण")

*छवि वैकल्पिक पाठ:* **python ocr ट्यूटोरियल – नमूना रसीद आउटपुट**

## पुनरावलोकन और अगले कदम

हमने अभी एक **python ocr tutorial** पूरा किया जिसमें दिखाया गया कि **OCR के लिए इमेज लोड** कैसे करें, **Python में OCR करें**, और अंत में Aspose का उपयोग करके **रसीद फ़ाइलों से टेक्स्ट पहचानें**। मुख्य बिंदु हैं:

- सही इंजन मोड चुनें (सटीकता के लिए डीप‑लर्निंग)
- `recognize()` कॉल करने से पहले हमेशा इमेज अटैच करें
- `OcrResult` ऑब्जेक्ट का उपयोग करके साफ़ टेक्स्ट निकालें, फिर आवश्यकता अनुसार उसे सहेजें या प्रोसेस करें

अगला क्या? लो‑कॉन्ट्रास्ट स्कैन को सुधारने के लिए Aspose Imaging फ़िल्टर को चेन करने पर विचार करें, या स्क्रिप्ट को Flask API में इंटीग्रेट करें ताकि आप वेब फ़ॉर्म के माध्यम से रसीदें अपलोड कर सकें। आप अकाउंटिंग ऑटोमेशन के लिए OCR डेटा को CSV में एक्सपोर्ट करने का भी अन्वेषण कर सकते हैं।

मल्टी‑पेज PDF या गैर‑लैटिन स्क्रिप्ट्स को संभालने के बारे में सवाल हैं? टिप्पणी छोड़ें—खुशी से मदद करेंगे!

**क्या आप अपने डॉक्यूमेंट ऑटोमेशन को अगले स्तर पर ले जाना चाहते हैं?** कोड प्राप्त करें, विभिन्न इमेज के साथ प्रयोग करें, और OCR इंजन को भारी काम करने दें। कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}