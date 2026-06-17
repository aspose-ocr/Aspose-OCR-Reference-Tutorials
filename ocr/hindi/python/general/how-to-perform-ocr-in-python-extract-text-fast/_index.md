---
category: general
date: 2026-03-26
description: Python में OCR कैसे करें और आसानी से इमेज से टेक्स्ट निकालें, स्कैन से
  टेक्स्ट पढ़ें, या एक सरल OcrEngine का उपयोग करके इनवॉइस से टेक्स्ट निकालें, यह सीखें।
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: hi
og_description: Python में OCR कैसे करें? यह गाइड आपको दिखाता है कि कैसे इमेज से टेक्स्ट
  निकालें, स्कैन से टेक्स्ट पढ़ें, और मिनटों में इनवॉइस से टेक्स्ट निकालें।
og_title: Python में OCR कैसे करें – तेज़ी से टेक्स्ट निकालें
tags:
- OCR
- Python
- Image Processing
title: Python में OCR कैसे करें – तेज़ी से टेक्स्ट निकालें
url: /hi/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में OCR कैसे करें – तेज़ी से टेक्स्ट निकालें

क्या आपने कभी स्कैन किए हुए रसीद या धुंधली PDF पर **how to perform OCR** करने के बारे में सोचा है? आप अकेले नहीं हैं। कई प्रोजेक्ट्स में **extract text from image** की आवश्यकता जल्दी ही सामने आती है, और सामान्य “हाथ से सब टाइप करो” वाला तरीका स्केलेबल नहीं है।  

इस ट्यूटोरियल में आप एक पूर्ण, तैयार‑चलाने‑योग्य उदाहरण देखेंगे जो **how to use OCR** को दिखाता है ताकि स्कैन से टेक्स्ट पढ़ा जा सके, इनवॉइस से डेटा निकाला जा सके, और यहाँ तक कि ऑटोमैटिक स्क्यू करेक्शन को भी संभाला जा सके—सिर्फ कुछ ही पंक्तियों के Python कोड से।

## आप क्या सीखेंगे

* आवश्यक सटीक डिपेंडेंसीज़ और इम्पोर्ट्स।
* `OcrEngine` इंस्टेंस को कैसे बनाएं और कॉन्फ़िगर करें।
* एक ही इंजन का उपयोग करके **extract text from image**, **read text from scan**, और **extract text from invoice** करने के तरीके।
* आम समस्याएँ (गलत भाषा, फाइलें नहीं मिलना, बड़ी इमेजेज) और उन्हें कैसे टालें।
* अपेक्षित आउटपुट ताकि आप सत्यापित कर सकें कि OCR सफल रहा।

कोई बाहरी डाक्यूमेंटेशन लिंक की आवश्यकता नहीं है—सब कुछ स्व-निहित है, इसलिए आप कोड को कॉपी‑पेस्ट करके तुरंत परिणाम देख सकते हैं।

## पूर्वापेक्षाएँ

Before we dive in, make sure you have:

* Python 3.8+ स्थापित हो ( `ocr` पैकेज किसी भी नवीनतम संस्करण के साथ काम करता है)।
* `ocr` लाइब्रेरी उपलब्ध हो (`pip install ocr‑engine` – यदि अलग हो तो वास्तविक पैकेज नाम से बदलें)।
* एक इमेज फ़ाइल जिसे आप प्रोसेस करना चाहते हैं – डेमो के लिए हम `invoice.png` का उपयोग करेंगे जो `YOUR_DIRECTORY` नामक फ़ोल्डर में स्थित है।

बस इतना ही। यदि आपके पास ये सब हैं, तो आप शुरू करने के लिए तैयार हैं।

## चरण 1: OCR मॉड्यूल स्थापित करें और इम्पोर्ट करें

सबसे पहले: हमें OCR लाइब्रेरी चाहिए। यदि आपने अभी तक इसे स्थापित नहीं किया है, तो अपने टर्मिनल में निम्न कमांड चलाएँ:

```bash
pip install ocr-engine
```

अब हम अपने स्क्रिप्ट में मॉड्यूल को इम्पोर्ट करेंगे।

```python
# Step 1: Import the OCR module
import ocr
```

> **Pro tip:** अपना वर्चुअल एनवायरनमेंट साफ़ रखें; इससे बाद में अन्य इमेज‑प्रोसेसिंग पैकेज जोड़ने पर संस्करण टकराव नहीं होते।

## चरण 2: OCR इंजन बनाएं और कॉन्फ़िगर करें

इंजन बनाना उसके कंस्ट्रक्टर को कॉल करने जितना सरल है, लेकिन वास्तविक शक्ति सही तरीके से कॉन्फ़िगर करने में है। हम भाषा को English सेट करेंगे और ऑटोमैटिक स्क्यू करेक्शन को चालू करेंगे, जो स्कैन किए हुए इनवॉइस को प्रोसेस करने के समय आवश्यक है जब वे पूरी तरह से संरेखित नहीं होते।

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

`auto_skew` को क्यों सक्षम करें? कई स्कैनर ऐसी इमेजेज बनाते हैं जो कुछ डिग्री झुकी होती हैं। बिना सुधार के इंजन अक्षर मिस कर सकता है, जिससे एक पूरी तरह पढ़ी जा सकने वाली इनवॉइस बकवास में बदल सकती है।

## चरण 3: अपने लक्ष्य इमेज पर OCR लागू करें

अब हम इमेज फ़ाइल को इंजन में फीड करते हैं। `recognize_image` मेथड एक ऑब्जेक्ट लौटाता है जिसमें कच्चा टेक्स्ट और कॉन्फिडेंस स्कोर (यदि लाइब्रेरी प्रदान करती है) होते हैं।

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

यदि आप **read text from scan** परिदृश्य में काम कर रहे हैं, तो बस पाथ को स्कैन किए हुए PDF को PNG या JPEG में बदलकर रखें। वही कॉल किसी भी इमेज फ़ॉर्मेट के लिए काम करता है जिसे बेस लाइब्रेरी सपोर्ट करती है।

## चरण 4: निकाले गए टेक्स्ट की जाँच करें और उपयोग करें

आइए कच्चा OCR आउटपुट प्रिंट करें। वास्तविक‑दुनिया के इनवॉइस‑प्रोसेसिंग पाइपलाइन में आप संभवतः इस स्ट्रिंग को पार्स करेंगे, लाइन आइटम्स, टोटल्स और डेट्स निकालेंगे, लेकिन अभी के लिए एक त्वरित नज़र OCR की सफलता की पुष्टि करेगी।

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**अपेक्षित आउटपुट (संक्षिप्त):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

यदि आउटपुट गड़बड़ दिखता है, तो दोबारा जांचें कि इमेज स्पष्ट है और `engine.language` दस्तावेज़ की भाषा से मेल खाता है।

## चरण 5: सामान्य किनारे के मामलों को संभालना

### बड़ी इमेजेज

5000 × 5000 पिक्सेल स्कैन को प्रोसेस करना मेमोरी‑गहन हो सकता है। इसे कम करने का एक त्वरित तरीका है कि इंजन को भेजने से पहले इमेज को डाउनस्केल करें:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### कई भाषाएँ

यदि आपको ऐसी **extract text from image** चाहिए जिसमें English और Spanish दोनों हों, तो आप भाषाओं की सूची सेट कर सकते हैं:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

इंजन दोनों सेटों के अक्षरों को पहचानने की कोशिश करेगा।

### त्रुटि संभालना

कभी भी यह न मानें कि फ़ाइल मौजूद है। कॉल को try‑except ब्लॉक में रैप करें ताकि एक दोस्ताना संदेश दिखाया जा सके:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## दृश्य संदर्भ

नीचे डेमो में उपयोग किए गए सैंपल इनवॉइस की स्क्रीनशॉट है। हल्की झुकाव पर ध्यान दें—बिल्कुल वही जिसे `auto_skew` ठीक करता है।

![ऑटोमैटिक स्क्यू करेक्शन दिखाते हुए इनवॉइस इमेज पर OCR कैसे करें](/images/ocr-example.png)

## पूर्ण, चलाने योग्य उदाहरण

सब कुछ मिलाकर, यहाँ एक सिंगल स्क्रिप्ट है जिसे आप कमांड लाइन से चला सकते हैं। यह इंस्टॉलेशन, कॉन्फ़िगरेशन, त्रुटि संभालना, और एक सरल पोस्ट‑प्रोसेसिंग स्टेप को कवर करता है जो निकाले गए टेक्स्ट को `output.txt` नामक फ़ाइल में लिखता है।

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

`python full_ocr_demo.py` चलाने से निकाला गया टेक्स्ट कंसोल में प्रिंट होगा और `output.txt` में सहेजा जाएगा। वहाँ से आप रेगुलर एक्सप्रेशन, CSV राइटर्स, या कोई भी लॉजिक लागू कर सकते हैं जो **extract text from invoice** ऑटोमेशन के लिए आवश्यक है।

## निष्कर्ष

अब आपके पास Python में **how to perform OCR** का एक ठोस, एंड‑टू‑एंड उत्तर है। `OcrEngine` बनाकर, भाषा और स्क्यू करेक्शन कॉन्फ़िगर करके, और कुछ व्यावहारिक किनारे के मामलों को संभालकर, आप विश्वसनीय रूप से **extract text from image**, **read text from scan**, और **extract text from invoice** कर सकते हैं बिना बिखरे हुए डाक्यूमेंटेशन की खोज किए।

अगला क्या? फ़ाइलों के बैच को लूप में फीड करने की कोशिश करें, विभिन्न भाषाओं के साथ प्रयोग करें, या आउटपुट को PDF जेनरेशन लाइब्रेरी में प्लग करके सर्चेबल PDFs बनाएं। संभावनाएँ असीमित हैं, और आपने जो कोड देखा वह एक मजबूत लॉन्चपैड है।

क्या आपके पास किसी विशेष फ़ाइल फ़ॉर्मेट के बारे में सवाल हैं या कॉन्फिडेंस थ्रेशोल्ड को ट्यून करने में मदद चाहिए? नीचे कमेंट डालें—हम आपके OCR पाइपलाइन को फाइन‑ट्यून करने में मदद करने के लिए खुश हैं!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}