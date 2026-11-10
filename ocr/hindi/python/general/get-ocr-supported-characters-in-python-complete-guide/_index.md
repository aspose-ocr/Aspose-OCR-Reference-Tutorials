---
category: general
date: 2026-06-25
description: aocr लाइब्रेरी का उपयोग करके OCR समर्थित अक्षर जल्दी प्राप्त करें। जानें
  कि OCR अक्षरों की सूची कैसे बनाएं, भाषाएँ कैसे सेट करें, और Python में अपने OCR
  इंजन को डिबग करें।
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: hi
og_description: aocr के साथ OCR समर्थित अक्षर प्राप्त करें। यह गाइड आपको दिखाता है
  कि OCR अक्षरों की सूची कैसे बनाएं, भाषाएँ कैसे चुनें, और Python में किनारे के मामलों
  को कैसे संभालें।
og_title: Python में OCR समर्थित अक्षर प्राप्त करें – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Python में OCR समर्थित अक्षर प्राप्त करें – पूर्ण मार्गदर्शिका
url: /hi/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में OCR समर्थित अक्षर प्राप्त करें – पूर्ण गाइड

क्या आप कभी यह सोचते रहे हैं कि **OCR समर्थित अक्षर** किसी विशेष भाषा के लिए कैसे प्राप्त करें जब आप OCR इंजन के साथ प्रयोग कर रहे हों? आप अकेले नहीं हैं। चाहे आप रसीद स्कैनर बना रहे हों या बहुभाषी दस्तावेज़ पार्सर, यह जानना कि आपका इंजन कौन‑से glyphs पहचान सकता है, बहुत मददगार होता है। इस ट्यूटोरियल में हम पूरी प्रक्रिया—लाइब्रेरी स्थापित करना, भाषा कॉन्फ़िगर करना, और अंत में उन अक्षरों की सूची बनाना—परिचित कराएंगे, ताकि आप अपने OCR पाइपलाइन को मिनटों में डिबग और फाइन‑ट्यून कर सकें।

हम **aocr** लाइब्रेरी का उपयोग करेंगे, जो एक हल्का Python OCR इंजन है और भाषा क्षमताओं को क्वेरी करना बेहद आसान बनाता है। इस गाइड के अंत तक आप **OCR अक्षरों की सूची** बना पाएँगे, **समर्थित OCR भाषाओं** के बीच स्विच कर पाएँगे, और उत्पादन में समस्याएँ पैदा करने से पहले कवरेज में गैप्स भी पहचान सकेंगे।

---

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* Python 3.8 या नया (aocr पैकेज 3.7 के समर्थन को हटा देता है)
* इंटरनेट कनेक्शन वाला टर्मिनल या कमांड प्रॉम्प्ट
* Python स्क्रिप्टिंग की बुनियादी समझ (यदि आपने पहले `print()` लिखा है, तो आप तैयार हैं)

कोई भारी बाहरी निर्भरताएँ नहीं—सिर्फ `aocr` pip पैकेज।

---

## aocr लाइब्रेरी (OCR Engine Python) स्थापित करें

सबसे पहले आपको एक कार्यशील **OCR engine Python** इंस्टॉलेशन चाहिए। aocr पैकेज PyPI पर उपलब्ध है, इसलिए एक ही pip कमांड से काम चल जाएगा:

```bash
pip install aocr
```

यदि आप वर्चुअल एनवायरनमेंट (बहुत अनुशंसित) का उपयोग कर रहे हैं, तो पहले उसे सक्रिय करें:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Pro tip:** संस्करण को पिन करें (`pip install aocr==1.2.4`) ताकि बाद में अप्रत्याशित API बदलावों से बचा जा सके।

---

## भाषा चुनें (Supported OCR Languages)

aocr कुछ बिल्ट‑इन भाषा पैक्स के साथ आता है। प्रत्येक पैक उन Unicode कोड पॉइंट्स का सेट परिभाषित करता है जिन्हें इंजन पहचान सकता है। इन पैक्स को क्वेरी करने के लिए आपको इंजन इंस्टेंस पर `language` एट्रिब्यूट सेट करना होगा।

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

आप `aocr.Language.ENGLISH` को किसी भी अन्य enum वैल्यू (`FRENCH`, `GERMAN`, आदि) से बदल सकते हैं। यदि आप ऐसी भाषा असाइन करने की कोशिश करते हैं जो बंडल नहीं है, तो aocr `ValueError` उठाता है। इसलिए पहले **supported OCR languages** की सूची जांचना अच्छा रहता है:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## अक्षरों का सेट प्राप्त करें (Get OCR Supported Characters)

अब ट्यूटोरियल का मुख्य भाग: वास्तव में **OCR समर्थित अक्षर** प्राप्त करना। इंजन एक उपयोगी मेथड `get_supported_characters()` प्रदान करता है जो सिंगल‑कैरेक्टर स्ट्रिंग्स की सूची लौटाता है।

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

पर्दे के पीछे, aocr भाषा पैक के साथ बंडल किए गए JSON फ़ाइल को पढ़ता है और प्रत्येक Unicode कोड पॉइंट को Python स्ट्रिंग में बदलता है। परिणाम निर्धारक (deterministic) है, यानी आप समान भाषा संस्करण पर स्क्रिप्ट चलाने पर हर बार वही सूची पाएँगे।

---

## कितने अक्षर समर्थित हैं, दिखाएँ

काउंट जानने से कवरेज की व्यापकता जल्दी समझ में आती है। अंग्रेज़ी के लिए आमतौर पर कुछ हजार अक्षर (विराम चिह्न और अंक सहित) दिखते हैं।

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

`len()` कॉल O(1) है क्योंकि Python सूची की लंबाई को आंतरिक रूप से संग्रहीत करता है, इसलिए बड़े अल्फाबेट्स के लिए भी कोई प्रदर्शन दंड नहीं होता।

---

## पहले 100 समर्थित अक्षर देखें

एक त्वरित विज़ुअल चेक से पता चल सकता है कि इंजन में वह प्रतीक है या नहीं जिसकी आपको ज़रूरत है (जैसे Euro चिन्ह या स्मार्ट कोट्स)। चलिए पहले सौ अक्षर प्रिंट करते हैं:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

`join` ऑपरेशन स्लाइस को एक सिंगल स्ट्रिंग में जोड़ता है, जो Python सूची को प्रिंट करने की तुलना में अधिक पठनीय बनाता है।

---

## पूर्ण स्क्रिप्ट – सभी चरण एक जगह

नीचे पूरा, चलाने योग्य उदाहरण है जो सभी चीज़ों को जोड़ता है। इसे `list_supported_chars.py` के रूप में सेव करें और टर्मिनल से `python list_supported_chars.py` चलाएँ।

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**अपेक्षित आउटपुट (संक्षिप्त):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

सटीक काउंट aocr संस्करण के अनुसार थोड़ा बदल सकता है, लेकिन आप हमेशा एक लंबा अल्फाबेट और सामान्य विराम चिह्न देखेंगे।

---

## एज केसों का संचालन

### अगर भाषा पैक मौजूद नहीं है तो क्या?

यदि आप ऐसी भाषा का अनुरोध करते हैं जो बंडल नहीं है, तो `aocr.Language` में वह enum नहीं होगा, और आपको `AttributeError` मिलेगा। इसे एक सरल चेक से बचा सकते हैं:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### खाली अक्षर सूची

कुछ दुर्लभ भाषाओं में यदि अंतर्निहित प्रशिक्षण डेटा अधूरा है तो खाली सूची मिल सकती है। ऐसे में आप डिफ़ॉल्ट (जैसे English) पर फॉल्बैक कर सकते हैं या चेतावनी दे सकते हैं:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Unicode सामान्यीकरण

सूची में संयुक्त अक्षर (जैसे “é” को `e` + acute accent) हो सकते हैं। यदि आपका डाउनस्ट्रीम प्रोसेसिंग प्री‑कम्पोज़्ड glyphs की अपेक्षा करता है, तो एक सामान्यीकरण चरण चलाएँ:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## वास्तविक‑दुनिया प्रोजेक्ट्स के लिए प्रो टिप्स

* **अक्षर सूची को कैश करें** – यदि आप हजारों इमेज प्रोसेस कर रहे हैं, तो हर इटरेशन में `get_supported_characters()` कॉल करने से अनावश्यक ओवरहेड बढ़ता है। सूची को मॉड्यूल‑लेवल वेरिएबल में रखें या बाद में पुनः उपयोग के लिए JSON में सीरियलाइज़ करें।
* **क्रॉस‑लैंग्वेज वैलिडेशन** – जब आप एक ही ऐप में कई भाषाएँ सपोर्ट करते हैं, तो character sets का इंटरसेक्ट निकालें ताकि एक सामान्य उपसेट मिल सके। इससे UI एलिमेंट्स को विभिन्न लोकल्स में सुसंगत रखने में मदद मिलती है।
* **OCR फेल्योर डिबगिंग** – यदि इंजन किसी glyph को गलत वर्गीकृत करता है, तो `list_supported_chars` के आउटपुट से उस अक्षर की तुलना करें। यदि वह लिस्ट में नहीं है, तो आपने एक कवरेज गैप पहचान लिया है जिसे कस्टम ट्रेनिंग की ज़रूरत हो सकती है।
* **कस्टम फ़ॉन्ट्स के साथ संयोजन** – aocr Unicode रेंज का सम्मान करता है, लेकिन रेंडरिंग क्वालिटी फ़ॉन्ट पर निर्भर करती है। प्रोडक्शन में उपयोग किए जाने वाले फ़ॉन्ट के साथ अपने समर्थित अक्षरों का परीक्षण करें ताकि आश्चर्यजनक समस्याओं से बचा जा सके।

---

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या यह aocr संस्करण 2.x के साथ काम करता है?**  
उत्तर: हाँ, `get_supported_characters()` मेथड 1.x और 2.x दोनों में स्थिर है। केवल परिवर्तन यह है कि भाषा enums को `aocr.languages` में स्थानांतरित किया गया है।

**प्रश्न: क्या मैं प्रत्येक अक्षर का Unicode कोड पॉइंट प्राप्त कर सकता हूँ?**  
उत्तर: बिल्कुल। सूची समझ में `ord(ch)` का उपयोग करें:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**प्रश्न: दाएँ‑से‑बाएँ स्क्रिप्ट्स जैसे Arabic के बारे में क्या?**  
उत्तर: aocr में `ARABIC` enum शामिल है। अक्षर सूची में Arabic glyphs होंगे, लेकिन आपको अपने डाउनस्ट्रीम UI में RTL रेंडरिंग सक्षम करनी पड़ सकती है।

---

## निष्कर्ष

अब आप **aocr लाइब्रेरी** का उपयोग करके Python में **OCR समर्थित अक्षर** कैसे प्राप्त करें, **समर्थित OCR भाषाओं** के बीच कैसे स्विच करें, और मजबूत टेक्स्ट‑रिकग्निशन पाइपलाइन के लिए **OCR अक्षरों की सूची** बनाना क्यों आवश्यक है, यह सब जानते हैं। पूर्ण स्क्रिप्ट और ऊपर दिए गए टिप्स के साथ, आप जल्दी से भाषा कवरेज की जाँच, गायब glyphs को डिबग, और अधिक स्मार्ट OCR‑ड्रिवन एप्लिकेशन बना सकते हैं।

अगला कदम क्या है? इस अक्षर सूची को कस्टम शब्द‑सूची फ़िल्टर के साथ जोड़ें, या किसी अन्य OCR इंजन (Tesseract, EasyOCR) के साथ प्रयोग करें और परिणामों की तुलना करें। जितना अधिक आप एक्सप्लोर करेंगे, उतनी ही बेहतर आपकी OCR समाधान बनेंगे।

हैप्पी कोडिंग, और आपके अक्षर सेट हमेशा पूर्ण रहें!

## अगला क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोचेज़ को एक्सप्लोर कर सकें।

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}