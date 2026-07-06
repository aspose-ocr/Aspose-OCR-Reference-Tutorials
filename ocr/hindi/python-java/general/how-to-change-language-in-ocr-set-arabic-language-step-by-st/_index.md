---
category: general
date: 2026-06-22
description: OCR इंजन में भाषा को जल्दी बदलने का तरीका। सरल कोड का उपयोग करके अरबी
  (ar) OCR भाषा सेट करना सीखें और सामान्य समस्याओं से बचें।
draft: false
keywords:
- how to change language
- ocr language arabic
- how to set OCR
- change OCR language
- set language OCR
language: hi
og_description: OCR इंजन में भाषा कैसे बदलें, यह पहली पंक्ति में समझाया गया है। अरबी
  OCR भाषा को तेज़ी से सेट करने के लिए इस ट्यूटोरियल का पालन करें।
og_title: OCR में भाषा कैसे बदलें – पूर्ण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: How to change language in OCR engines quickly. Learn to set Arabic
    (ar) OCR language using simple code and avoid common pitfalls.
  headline: How to Change Language in OCR – Set Arabic Language Step‑by‑Step
  type: TechArticle
- description: How to change language in OCR engines quickly. Learn to set Arabic
    (ar) OCR language using simple code and avoid common pitfalls.
  name: How to Change Language in OCR – Set Arabic Language Step‑by‑Step
  steps:
  - name: '**Grab the OCR engine instance** – this is usually a singleton or a factory‑created
      object.'
    text: '**Grab the OCR engine instance** – this is usually a singleton or a factory‑created
      object.'
  - name: '**Pull the settings object** – most libraries keep language, DPI, and other
      options in a separate config container.'
    text: '**Pull the settings object** – most libraries keep language, DPI, and other
      options in a separate config container.'
  - name: '**Set the language code** – for Arabic the ISO‑639‑2 code is `"ar"`.'
    text: '**Set the language code** – for Arabic the ISO‑639‑2 code is `"ar"`.'
  type: HowTo
tags:
- OCR
- multilingual
- programming
title: OCR में भाषा कैसे बदलें – अरबी भाषा सेट करने की चरण‑दर‑चरण प्रक्रिया
url: /hi/python-java/general/how-to-change-language-in-ocr-set-arabic-language-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR में भाषा कैसे बदलें – पूर्ण प्रोग्रामिंग गाइड

OCR इंजन में भाषा बदलना एक आम बाधा है जब आप बहुभाषी दस्तावेज़ों से निपटना शुरू करते हैं। इस ट्यूटोरियल में हम आपको सटीक चरणों के माध्यम से ले जाएंगे ताकि OCR भाषा को अरबी पर सेट किया जा सके, साथ ही एक चलाने योग्य कोड नमूना और प्रत्येक पंक्ति की व्याख्याएँ हों। यदि आपने कभी सोचा है *“how to set OCR* को किसी अलग लिपि पर बिना पाइपलाइन टूटे सेट करने के बारे में*, तो आप सही जगह पर हैं*।

हम वह सब कवर करेंगे जिसकी आपको जरूरत है: आवश्यक लाइब्रेरीज़, OCR इंजन इंस्टेंस कैसे प्राप्त करें, उसकी सेटिंग्स तक कैसे पहुँचें, और अंत में OCR भाषा को सुरक्षित रूप से कैसे बदलें। अंत तक आप अंग्रेज़ी से अरबी (या किसी अन्य समर्थित भाषा) में एक ही मेथड कॉल से स्विच कर पाएँगे। कोई जादू नहीं, सिर्फ स्पष्ट कोड और कुछ व्यावहारिक टिप्स।

## पूर्वापेक्षाएँ

- Python 3.8+ (या कोई भी नवीनतम संस्करण)
- एक OCR लाइब्रेरी जो सेटिंग्स ऑब्जेक्ट को उजागर करती है – उदाहरण में **pytesseract** को एक छोटे हेल्पर क्लास में रैप किया गया है, लेकिन यही पैटर्न अन्य इंजन जैसे EasyOCR या Microsoft के Computer Vision SDK के लिए भी काम करता है।
- OCR इंजन के लिए अरबी भाषा डेटा स्थापित हो (`ara.traineddata` for Tesseract)।  
  *Pro tip:* Ubuntu पर आप इसे `sudo apt-get install tesseract-ocr-ara` से स्थापित कर सकते हैं।

## OCR में भाषा कैसे बदलें – अवलोकन

भाषा बदलना मूलतः एक तीन‑स्टेप प्रक्रिया है:

1. **Grab the OCR engine instance** – यह आमतौर पर एक सिंगलटन या फ़ैक्टरी‑क्रिएटेड ऑब्जेक्ट होता है।
2. **Pull the settings object** – अधिकांश लाइब्रेरीज़ भाषा, DPI, और अन्य विकल्पों को एक अलग कॉन्फ़िग कंटेनर में रखती हैं।
3. **Set the language code** – अरबी के लिए ISO‑639‑2 कोड `"ar"` है।

नीचे एक न्यूनतम, पूरी तरह चलाने योग्य स्क्रिप्ट है जो इन चरणों को दर्शाती है।

![How to change language in OCR screenshot](image-placeholder.png "How to change language in OCR example")

## चरण 1: OCR इंजन इंस्टेंस बनाएं या प्राप्त करें

पहले हमें एक इंजन चाहिए। वास्तविक प्रोजेक्ट्स में इंजन कहीं और बनाया जा सकता है और पास किया जा सकता है; स्पष्टता के लिए हम इसे यहाँ ही इंस्टैंशिएट करेंगे।

```python
# step1_engine.py
import pytesseract
from PIL import Image

class SimpleOCREngine:
    """A thin wrapper around pytesseract to expose a settings object."""
    def __init__(self):
        # pytesseract itself doesn't expose a mutable settings object,
        # so we store options in a dict that we later pass to image_to_string().
        self._options = {"lang": "eng"}  # default to English

    def get_settings(self):
        """Return a Settings object that can modify OCR options."""
        return OcrSettings(self)

    def recognize(self, image_path: str) -> str:
        """Run OCR on the given image using current options."""
        img = Image.open(image_path)
        return pytesseract.image_to_string(img, config=self._build_config())

    def _build_config(self) -> str:
        """Convert the internal options dict to a Tesseract command line."""
        # Example: '-l eng' or '-l ar+eng' for multiple languages
        lang_option = self._options.get("lang", "eng")
        return f"-l {lang_option}"
```

**Why we wrap the engine** – कई OCR SDKs (जिसमें Tesseract भी शामिल है) प्रत्येक कॉल पर भाषा को स्ट्रिंग के रूप में पास करने की अपेक्षा रखते हैं। विकल्पों को सेटिंग्स ऑब्जेक्ट में एन्कैप्सुलेट करके हमें एक साफ़, *how to set OCR*‑स्टाइल API मिलता है जो आपके द्वारा प्रदान किए गए मूल कोड स्निपेट को प्रतिबिंबित करता है।

## चरण 2: इंजन की सेटिंग्स ऑब्जेक्ट तक पहुंचें

अब जब हमारे पास इंजन है, हम उसकी सेटिंग्स प्राप्त करते हैं। यह मूल उदाहरण की दूसरी पंक्ति (`settings = engine.get_settings()`) को प्रतिबिंबित करता है।

```python
# step2_settings.py
class OcrSettings:
    """Provides getters and setters for OCR configuration."""
    def __init__(self, engine: SimpleOCREngine):
        self._engine = engine

    def set_language(self, lang_code: str):
        """
        Change OCR language.
        :param lang_code: ISO‑639‑2 language code, e.g., 'ar' for Arabic.
        """
        # Validate the language code – a tiny safety net.
        if not isinstance(lang_code, str) or len(lang_code) < 2:
            raise ValueError("Language code must be a non‑empty string.")
        self._engine._options["lang"] = lang_code

    def get_language(self) -> str:
        """Return the currently configured language code."""
        return self._engine._options.get("lang", "eng")
```

यहाँ हम **how to set OCR** भाषा को `set_language` के माध्यम से उजागर करते हैं। यह मेथड एक बुनियादी सैनीटी चेक भी करता है, जो एक अच्छा डिफेंसिव प्रोग्रामिंग अभ्यास है।

## चरण 3: OCR भाषा को अरबी (ocr language arabic) पर सेट करें

अंत में हम मेथड को अरबी कोड `"ar"` के साथ कॉल करते हैं। यह *change OCR language* ऑपरेशन का मूल है।

```python
# step3_change_language.py
from step1_engine import SimpleOCREngine

# Obtain the OCR engine instance (could be a singleton in a larger app)
engine = SimpleOCREngine()

# Access the settings object
settings = engine.get_settings()

# Set the OCR language to Arabic – this is the "how to change language" line.
settings.set_language("ar")

# Optional: verify the change
print("Current OCR language:", settings.get_language())

# Run OCR on a sample Arabic image (replace with your own path)
# result = engine.recognize("sample_arabic.png")
# print("OCR Output:", result)
```

**Expected output**

```
Current OCR language: ar
```

यदि आप `recognize` कॉल को अनकमेंट करते हैं और इसे एक वास्तविक अरबी इमेज़ की ओर इंगित करते हैं, तो आपको कंसोल में अरबी अक्षर प्रिंट होते दिखेंगे (बशर्ते भाषा डेटा स्थापित हो)।

## कई भाषाओं के लिए OCR कैसे सेट करें

कभी‑कभी आपको *ocr language arabic* **plus** अंग्रेज़ी की आवश्यकता होती है, विशेषकर मिश्रित दस्तावेज़ों में। `set_language` मेथड `+`‑सेपरेटेड लिस्ट को स्वीकार कर सकता है:

```python
settings.set_language("ar+eng")
print("Now recognizing both Arabic and English:", settings.get_language())
```

*Edge case*: यदि अनुरोधित भाषा पैक स्थापित नहीं है, तो Tesseract `Error opening language file` जैसी त्रुटि फेंकेगा। क्रैश से बचने के लिए आप एक्सेप्शन को कैच कर डिफ़ॉल्ट भाषा पर फॉल बैक कर सकते हैं।

```python
try:
    settings.set_language("ar")
except Exception as e:
    print("Failed to set Arabic language:", e)
    settings.set_language("eng")  # fallback
```

## रनटाइम पर OCR भाषा को गतिशील रूप से बदलें

कई एप्लिकेशन्स में उपयोगकर्ता ड्रॉपडाउन से भाषा चुनता है। क्योंकि सेटिंग्स इंजन ऑब्जेक्ट के अंदर रहती हैं, आप इंजन को पुनः‑इंस्टैंशिएट किए बिना ऑन‑द‑फ्लाई भाषा स्विच कर सकते हैं।

```python
def switch_language(lang_code: str):
    settings.set_language(lang_code)
    print(f"OCR language switched to {lang_code}")

# Example usage:
switch_language("fr")   # switch to French
switch_language("ar")   # back to Arabic
```

यह पैटर्न *set language OCR* आवश्यकता को पूरा करता है जबकि कोड को साफ़ रखता है।

## सामान्य समस्याएँ और प्रो टिप्स

| Pitfall | What Happens | Fix |
|---------|--------------|-----|
| Language pack missing | Tesseract returns “Failed loading language ‘ar’” | Install the language data (`sudo apt-get install tesseract-ocr-ara` or download from the repo). |
| Using the wrong ISO code | No output or garbled characters | Verify the code (`ar` for Arabic, `eng` for English, `chi_sim` for Simplified Chinese). |
| Forgetting to rebuild config | Engine still uses old language | Always call `engine._build_config()` (handled internally when you call `recognize`). |
| Passing a list instead of a string | TypeError | Use `"ar+eng"` as a single string, not `["ar", "eng"]`. |

## पूर्ण कार्यशील उदाहरण (सभी भाग एक साथ)

```python
# full_example.py
import pytesseract
from PIL import Image

class SimpleOCREngine:
    def __init__(self):
        self._options = {"lang": "eng"}

    def get_settings(self):
        return OcrSettings(self)

    def recognize(self, image_path: str) -> str:
        img = Image.open(image_path)
        return pytesseract.image_to_string(img, config=self._build_config())

    def _build_config(self) -> str:
        return f"-l {self._options.get('lang', 'eng')}"

class OcrSettings:
    def __init__(self, engine: SimpleOCREngine):
        self._engine = engine

    def set_language(self, lang_code: str):
        if not isinstance(lang_code, str) or len(lang_code) < 2:
            raise ValueError("Language code must be a non‑empty string.")
        self._engine._options["lang"] = lang_code

    def get_language(self) -> str:
        return self._engine._options.get("lang", "eng")

# ---------- Usage ----------
engine = SimpleOCREngine()
settings = engine.get_settings()

# Change to Arabic (how to change language)
settings.set_language("ar")
print("Current OCR language:", settings.get_language())

# Uncomment and point to a real Arabic image to test OCR
# output = engine.recognize("sample_arabic.png")
# print("OCR result:", output)
```

स्क्रिप्ट को `python full_example.py` के साथ चलाएँ। यदि सब कुछ सेट अप है, तो आप देखेंगे:

```
Current OCR language: ar
```

…और यदि आप अंतिम दो पंक्तियों को सक्षम करते हैं तो आपके अरबी इमेज़ का OCR आउटपुट प्रदर्शित होगा।

## निष्कर्ष

आप अब जानते हैं **how to change language in OCR** इंजन, विशेष रूप से कैसे एक साफ़, पुन: उपयोग योग्य पैटर्न का उपयोग करके OCR भाषा को अरबी पर सेट किया जाए। गाइड ने इंजन प्राप्त करने, उसकी सेटिंग्स तक पहुँचने, और अंत में भाषा परिवर्तन लागू करने की प्रक्रिया को कवर किया—*ocr language arabic* परिदृश्य और व्यापक *change OCR language* उपयोग केस दोनों को शामिल करते हुए।  

अगले कदम? अधिक भाषाओं के समर्थन को जोड़ें, मल्टी‑लैंग्वेज स्ट्रिंग्स (`"ar+eng"`) के साथ प्रयोग करें, या इस लॉजिक को एक वेब सर्विस में इंटीग्रेट करें जो उपयोगकर्ताओं को किसी भी लिपि में दस्तावेज़ अपलोड करने की अनुमति देती है। यदि आप अन्य लाइब्रेरीज़ (EasyOCR, Google Vision) में *set language OCR* के बारे में जिज्ञासु हैं तो आगे पढ़ें।

## अगला क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर करने में मदद करेंगे।

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract OCR – OCR Configuration](/ocr/english/net/ocr-configuration/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}