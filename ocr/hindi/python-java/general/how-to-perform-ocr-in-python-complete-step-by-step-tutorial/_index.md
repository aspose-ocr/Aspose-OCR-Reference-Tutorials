---
category: general
date: 2026-03-26
description: Python में OCR कैसे करें और इमेज फ़ाइलों से टेक्स्ट को पहचानें, यह सीखें।
  यह गाइड दिखाता है कि PNG से टेक्स्ट कैसे निकालें और इमेज को जल्दी से टेक्स्ट में
  बदलें।
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: hi
og_description: Python में OCR कैसे करें? इस गाइड का पालन करें ताकि आप इमेज से टेक्स्ट
  पहचान सकें, PNG से टेक्स्ट निकाल सकें, और ट्रायल लाइसेंस के साथ इमेज को टेक्स्ट
  में बदल सकें।
og_title: Python में OCR कैसे करें – पूर्ण ट्यूटोरियल
tags:
- OCR
- Python
- Image Processing
title: Python में OCR कैसे करें – पूर्ण चरण‑दर‑चरण ट्यूटोरियल
url: /hi/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में OCR कैसे करें – पूर्ण चरण‑दर‑चरण ट्यूटोरियल  

क्या आपने कभी सोचा है कि **OCR कैसे करें** उस तस्वीर पर जो आपने अभी अपने फोन से ली है? आप अकेले नहीं हैं—दुनिया भर के डेवलपर्स को जटिल नेटिव लाइब्रेरीज़ से जूझे बिना इमेज फ़ाइलों से टेक्स्ट पहचानने का भरोसेमंद तरीका चाहिए।  

इस ट्यूटोरियल में हम एक व्यावहारिक उदाहरण के माध्यम से दिखाएंगे कि **OCR कैसे करें**, **इमेज से टेक्स्ट कैसे पहचानें**, और **PNG से टेक्स्ट कैसे निकालें** एक हल्के Python रैपर का उपयोग करके। अंत तक आप केवल कुछ लाइनों के कोड से **इमेज को टेक्स्ट में बदल** सकेंगे, और लाइसेंसिंग की झंझटों की चिंता नहीं होगी क्योंकि हम बिल्ट‑इन ट्रायल मोड का उपयोग करेंगे।

## आप क्या सीखेंगे  

* OCR इंजन के लिए ट्रायल लाइसेंस कैसे सेट करें (फ़ाइल पाथ की जरूरत नहीं)।  
* **इमेज से टेक्स्ट पहचानने** के लिए कॉल्स का सटीक क्रम।  
* **PNG फ़ाइलों से टेक्स्ट निकालने** के तरीके और फ़ॉन्ट न मिलने जैसी सामान्य समस्याओं का समाधान।  
* ट्रायल से प्रोडक्शन लाइसेंस पर स्विच करते समय समाधान को स्केल करने के टिप्स।  

**Prerequisites** – आपको Python 3.8+ और `ocr` पैकेज (इंस्टॉल करने के लिए `pip install ocr`) चाहिए। अन्य कोई बाहरी टूल आवश्यक नहीं है।

---  

![OCR करने का उदाहरण](https://example.com/ocr-demo.png "Python में OCR – पहचाना गया टेक्स्ट प्रदर्शित")  

*छवि वैकल्पिक पाठ: Python में OCR – नमूना आउटपुट*  

## Step 1 – Activate a Trial License (No File Path Needed)  

इंजन कुछ भी पढ़ने से पहले उसे एक वैध लाइसेंस चाहिए। ट्रायल मोड प्रयोगों और छोटे प्रोजेक्ट्स के लिए एकदम उपयुक्त है।

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Why this matters:* लाइसेंस ऑब्जेक्ट OCR लाइब्रेरी को बताता है कि आप एक सैंडबॉक्स में काम कर रहे हैं। यदि आप इस चरण को छोड़ देते हैं, तो `recognize()` कॉल करने के तुरंत बाद इंजन `LicenseError` फेंकेगा।  

**Pro tip:** जब आप पेड लाइसेंस पर जाएँ, तो ऊपर की दो लाइनों को `ocr.License("path/to/your/license.key").apply()` से बदल दें।

## Step 2 – Create the OCR Engine Instance  

अब जब ट्रायल सक्रिय है, हम मुख्य इंजन को इंस्टैंशिएट करते हैं। इसे ऐसे समझें जैसे “ब्रेन” जो इमेज को देखेगा और तय करेगा कि कौन‑से कैरेक्टर कहाँ हैं।

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Why this matters:* `OcrEngine` भाषा पैक्स और DPI सेटिंग्स जैसी कॉन्फ़िगरेशन रखता है। आप बाद में इन्हें बदल सकते हैं, लेकिन डिफ़ॉल्ट अधिकांश English‑only PNG के लिए काम करता है।

## Step 3 – Load the PNG You Want to Process  

यहीं पर हम **इमेज से टेक्स्ट पहचानते** हैं। `ocr.Imaging.Image.load()` मेथड PNG, JPEG, BMP और कुछ अन्य फ़ॉर्मेट्स को सपोर्ट करता है।

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Edge case:* यदि आपका PNG इंडेक्स्ड पैलेट (स्क्रीनशॉट्स में आम) उपयोग करता है, तो लोडर इसे स्वचालित रूप से 24‑bit RGB बफ़र में बदल देगा। यह परिवर्तन थोड़ा प्रदर्शन पर असर डाल सकता है, लेकिन सटीक OCR परिणाम सुनिश्चित करता है।

## Step 4 – Run the OCR and Grab the Text  

अंत में, हम इंजन को अपना काम करने को कहते हैं और फिर प्लेन‑टेक्स्ट परिणाम निकालते हैं।

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Expected output** (उदाहरण के लिए एक साधारण इमेज जिसमें “Hello World” लिखा है):

```
Hello World
```

यदि इमेज में कई लाइनें हैं, तो आउटपुट लाइन ब्रेक को बरकरार रखेगा, जिससे CSV पार्सर या NLP पाइपलाइन जैसे डाउनस्ट्रीम प्रोसेस में आसानी होगी।

## Optional: Fine‑Tuning for Better Accuracy  

* **Language packs:** `ocr_engine.set_language("eng")` (डिफ़ॉल्ट) या फ़्रेंच के लिए `"fra"`।  
* **DPI scaling:** `ocr_engine.set_dpi(300)` कम‑रिज़ॉल्यूशन स्कैन पर परिणाम सुधार सकता है।  
* **Pre‑processing:** `ocr.Imaging.Image.threshold()` के साथ बाइनरी थ्रेशहोल्ड लागू करने से `set_image` से पहले शोरयुक्त बैकग्राउंड में साफ़ टेक्स्ट मिलता है।  

ये ट्यूनिंग तब उपयोगी होती हैं जब आप एक त्वरित डेमो से प्रोडक्शन‑ग्रेड **ocr tutorial python** पर जाते हैं जो रोज़ाना सैकड़ों फ़ाइलें प्रोसेस करता है।

## Full Script – Ready to Copy & Paste  

नीचे पूरा, चलाने योग्य स्क्रिप्ट है जो ऊपर बताए गए सभी चरणों को जोड़ता है। इसे `run_ocr.py` के रूप में सेव करें और `YOUR_DIRECTORY/sample1.png` को अपनी PNG फ़ाइल के पाथ से बदलें।

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

कमांड लाइन से चलाएँ:

```bash
python run_ocr.py
```

आपको कंसोल में निकाला गया टेक्स्ट प्रिंट होता दिखेगा। यदि आपको खाली स्ट्रिंग मिलती है, तो दोबारा जांचें कि इमेज में स्पष्ट, हाई‑कॉन्ट्रास्ट टेक्स्ट है और ट्रायल लाइसेंस बिना त्रुटि के लागू हुआ है।

## Common Questions & Gotchas  

* **“क्या यह JPEG के साथ काम करता है?”** – बिल्कुल। `load()` मेथड फ़ॉर्मेट को ऑटो‑डिटेक्ट करता है, इसलिए आप कोड में बदलाव किए बिना PNG को JPEG से बदल सकते हैं।  
* **“अगर इमेज घुमा हुआ है तो क्या करें?”** – इंजन ऑटो‑डिटेक्ट ओरिएंटेशन कर सकता है, लेकिन बेहतर परिणामों के लिए आप `input_image.rotate(90)` के साथ पहले से घुमा सकते हैं, फिर `set_image` कॉल करें।  
* **“क्या मैं लूप में कई इमेज प्रोसेस कर सकता हूँ?”** – हाँ। बस लोडिंग और `recognize()` कॉल को `for` लूप के अंदर रखें; वही `ocr_engine` इंस्टेंस पुनः उपयोग किया जा सकता है, जिससे थोड़ा ओवरहेड बचता है।  

## Next Steps – From Demo to Production  

अब जब आप **OCR कैसे करें** जानते हैं, तो इन फॉलो‑अप टॉपिक्स पर विचार करें:

* **Batch processing** – इस स्क्रिप्ट को `os.listdir()` के साथ मिलाकर **PNG फ़ाइलों से टेक्स्ट निकालें** बड़े पैमाने पर।  
* **Integrate with PDF** – `pdf2image` का उपयोग करके PDF पेज को PNG में बदलें, फिर उसी पाइपलाइन में फीड करें।  
* **Post‑processing** – रेगएक्स या फज़ी मैचिंग लागू करके सामान्य OCR गलतियों (जैसे “0” बनाम “O”) को साफ़ करें।  

इनमें से प्रत्येक **इमेज को टेक्स्ट में बदल** की मूल अवधारणा पर आधारित है और आपके OCR वर्कफ़्लो की उपयोगिता को बढ़ाता है।

---  

### TL;DR  

हमने वह सब कवर किया जो आपको Python में **OCR कैसे करें** जानने के लिए चाहिए: ट्रायल लाइसेंस सक्रिय करें, इंजन बनाएं, PNG लोड करें, पहचान चलाएँ, और परिणाम प्रिंट करें। कुछ ही लाइनों से आप **इमेज से टेक्स्ट पहचान**, **PNG से टेक्स्ट निकालें**, और **इमेज को टेक्स्ट में बदल** सकते हैं किसी भी डाउनस्ट्रीम एप्लिकेशन के लिए।  

इसे आज़माएँ, DPI या भाषा सेटिंग्स को ट्यून करें, और इंजन को भारी काम करने दें। हैप्पी कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}