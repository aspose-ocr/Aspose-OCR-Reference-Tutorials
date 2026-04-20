---
category: general
date: 2026-03-18
description: Python में OCR त्रुटियों को जल्दी ठीक करें। जानें OCR को कैसे साफ़ करें,
  OCR टेक्स्ट को कैसे साफ़ करें, शून्य को O से बदलें, और Python OCR पोस्ट‑प्रोसेसिंग
  लागू करें।
draft: false
keywords:
- fix OCR errors
- how to clean OCR
- clean OCR text python
- replace zero with O
- python OCR post processing
language: hi
og_description: Python में OCR त्रुटियों को जल्दी ठीक करें। जानें कैसे OCR को साफ़
  करें, शून्य को O से बदलें, और एक ही ट्यूटोरियल में Python OCR पोस्ट‑प्रोसेसिंग का
  उपयोग करें।
og_title: Python में OCR त्रुटियों को ठीक करें – OCR टेक्स्ट को साफ़ करने की गाइड
tags:
- OCR
- Python
- Text Cleaning
title: Python में OCR त्रुटियों को ठीक करें – OCR टेक्स्ट को साफ़ करने की गाइड
url: /hi/python/general/fix-ocr-errors-in-python-clean-ocr-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में OCR त्रुटियों को ठीक करें – OCR टेक्स्ट को साफ़ करने का गाइड

क्या आपने कभी स्कैन किए हुए इनवॉइस को देखा है और सोचा है, *“डेटाबेस में डालने से पहले OCR त्रुटियों को कैसे ठीक करूँ?”* आप अकेले नहीं हैं। दस्तावेज़ ऑटोमेशन की दुनिया में, एक ही गलत पढ़ा गया अक्षर पूरी पाइपलाइन को तोड़ सकता है, इसलिए **how to clean OCR** आउटपुट सीखना आवश्यक है।  

इस ट्यूटोरियल में आप एक व्यावहारिक, अंत‑से‑अंत तरीका देखेंगे **fix OCR errors** को ठीक करने का, जिसमें एक छोटा पोस्ट‑प्रोसेसर उपयोग किया गया है जो अंक “0” को अक्षर “O” से बदलता है—उत्पाद कोड में आम समस्या। अंत तक, आप इस समाधान को किसी भी Python OCR वर्कफ़्लो में जोड़ सकेंगे और साफ़, अधिक विश्वसनीय टेक्स्ट का आनंद ले सकेंगे।

> **आपको क्या मिलेगा:** एक पूर्ण, चलाने योग्य Python स्क्रिप्ट, प्रत्येक पंक्ति के महत्व की व्याख्याएँ, लॉजिक को विस्तारित करने के टिप्स, और अपेक्षित आउटपुट की त्वरित sanity‑check।

## आवश्यकताएँ — शुरू करने से पहले आपको क्या चाहिए

- Python 3.8 या नया (सिंटैक्स सभी हालिया रिलीज़ पर काम करता है)।  
- एक बुनियादी OCR लाइब्रेरी (जैसे, `pytesseract` के माध्यम से Tesseract) जो कच्ची स्ट्रिंग्स लौटाती है।  
- Python में फ़ंक्शन्स और ऑब्जेक्ट्स की न्यूनतम परिचितता।  

यदि आपके पास पहले से ही एक OCR चरण है जो स्ट्रिंग आउटपुट करता है, तो आप तैयार हैं—पोस्ट‑प्रोसेसिंग भाग के लिए कोई अतिरिक्त इंस्टॉलेशन आवश्यक नहीं है।

## चरण 1: एक न्यूनतम AI‑जैसा रैपर सेट अप करें (हमें इसकी आवश्यकता क्यों है)

कई प्रोजेक्ट्स में OCR इंजन एक बड़े “AI” क्लास के अंदर रहता है जो प्री‑प्रोसेसिंग, इनफ़रेंस, और पोस्ट‑प्रोसेसिंग को संभालता है। उदाहरण को स्व-निहित रखने के लिए हम एक छोटा `AIProcessor` क्लास बनाएँगे जो इस पैटर्न की नकल करता है। इससे कोड को मौजूदा कोड‑बेस में बिना किसी पुनर्लेखन के डालना आसान हो जाता है।

```python
# ai_wrapper.py
class AIProcessor:
    """
    Simple wrapper that stores a post‑processing callable.
    In real projects this could be a full‑fledged model class.
    """
    def __init__(self):
        self._post_processor = None

    def set_post_processor(self, func):
        """Register a function that will clean OCR output."""
        if not callable(func):
            raise TypeError("Post‑processor must be callable")
        self._post_processor = func

    def run_postprocessor(self, text):
        """Apply the registered post‑processor to raw OCR text."""
        if self._post_processor is None:
            raise RuntimeError("No post‑processor has been set")
        return self._post_processor(text)
```

**Why this matters:** पोस्ट‑प्रोसेसर को OCR इंजन से अलग रखकर सिंगल‑रेस्पॉन्सिबिलिटी प्रिंसिपल का सम्मान होता है और आप क्लीनिंग लॉजिक को OCR कोड को छुए बिना बदल सकते हैं।

## चरण 2: वह फ़ंक्शन लिखें जो **Fixes OCR Errors** करता है

अब हम ट्यूटोरियल का मुख्य भाग बनाते हैं: एक फ़ंक्शन जो **fixes OCR errors** करता है, अंक “0” को अक्षर “O” से बदलकर। यह पैटर्न प्रोडक्ट कोड, सीरियल नंबर, और किसी भी अल्फ़ान्यूमेरिक पहचानकर्ता को कवर करता है जहाँ OCR इंजन अक्सर इन दो अक्षरों को भ्रमित करता है।

```python
# post_processors.py
def correct_ocr_errors(text: str) -> str:
    """
    Replace common OCR mis‑reads.
    Example: change digit "0" to letter "O" in product codes.
    """
    # You could add more rules here, e.g.:
    # text = text.replace('1', 'I')
    # text = text.replace('5', 'S')
    return text.replace("0", "O")
```

**Why we replace 0 with O:** कई फ़ॉन्ट्स में शून्य और बड़े अक्षर O एक जैसे दिखते हैं, इसलिए OCR अक्सर गलत अनुमान लगाता है। इसे जल्दी सुधारने से, डाउनस्ट्रीम वैलिडेशन (जैसे regex चेक) इच्छित रूप से काम करता है।

## चरण 3: पोस्ट‑प्रोसेसर को AI इंस्टेंस में जोड़ें

रैपर और क्लीनिंग फ़ंक्शन तैयार होने पर, हम उन्हें एक साथ जोड़ते हैं। यह दर्शाता है कि आप प्रोडक्शन पाइपलाइन में एक कस्टम पोस्ट‑प्रोसेसर कैसे रजिस्टर करेंगे।

```python
# main.py
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Create the AI‑like object
ai = AIProcessor()

# Register our OCR‑fixing function
ai.set_post_processor(correct_ocr_errors)
```

यदि आपको कभी किसी अलग भाषा या डेटा फ़ॉर्मेट के लिए **how to clean OCR** आउटपुट की आवश्यकता हो, तो बस एक और फ़ंक्शन लिखें और `set_post_processor` को फिर से कॉल करें—पाइपलाइन के बाकी हिस्से को छूने की जरूरत नहीं।

## चरण 4: कच्चा OCR टेक्स्ट फीड करें और साफ़ परिणाम प्राप्त करें

आइए एक कच्ची OCR स्ट्रिंग का सिमुलेशन करें जिसमें उत्पाद कोड में डरावना “0” शामिल है। वास्तविक परिदृश्य में आप प्लेसहोल्डर को `pytesseract.image_to_string(image)` या समान कॉल से बदलेंगे।

```python
# Simulated OCR output (replace with your own OCR call)
raw_text = "Product code: 10A0B"

# Run the post‑processor to obtain cleaned text
cleaned_text = ai.run_postprocessor(raw_text)

print("Before cleaning :", raw_text)
print("After cleaning  :", cleaned_text)
```

**अपेक्षित आउटपुट**

```
Before cleaning : Product code: 10A0B
After cleaning  : Product code: 1OAOB
```

ध्यान दें कि शून्य अब बड़े O में बदल गए हैं, जिससे हमें एक स्ट्रिंग मिलती है जो अधिकांश इन्वेंटरी सिस्टम के अपेक्षित फ़ॉर्मेट से मेल खाती है।

## चरण 5: लॉजिक को विस्तारित करें – वास्तविक‑विश्व विविधताएँ

ऊपर दिया गया सरल प्रतिस्थापन एक सीमित केस को हल करता है, लेकिन प्रोडक्शन में आप अन्य अजीबताओं का सामना करेंगे:

| सामान्य गलती | उदाहरण OCR | इच्छित सुधार | कैसे जोड़ें |
|----------------|------------|-------------|------------|
| “1” को “I” पढ़ा गया | `I23` | `123` | `text = text.replace('I', '1')` |
| “5” को “S” पढ़ा गया | `S9` | `59` | `text = text.replace('S', '5')` |
| अतिरिक्त व्हाइटस्पेस | `  ABC  ` | `ABC` | `text = text.strip()` |
| मिश्रित‑केस भ्रम | `oRder` | `Order` | `text.title()` |

आप `correct_ocr_errors` को इन नियमों में से किसी के साथ विस्तारित कर सकते हैं। बस प्रत्येक ट्रांसफ़ॉर्मेशन को **idempotent** रखें (दो बार चलाने पर परिणाम नहीं बदलना चाहिए) ताकि आकस्मिक डेटा करप्शन से बचा जा सके।

```python
def correct_ocr_errors(text: str) -> str:
    text = text.replace("0", "O")
    text = text.replace("I", "1")
    text = text.replace("S", "5")
    return text.strip()
```

**Pro tip:** यदि आपके पास वैध कोडों का ज्ञात कैटलॉग है, तो साफ़ किए गए स्ट्रिंग को regex या लुकअप टेबल के विरुद्ध वैलिडेट करने पर विचार करें। यह अतिरिक्त कदम उन शेष OCR त्रुटियों को पकड़ता है जो सरल कैरेक्टर स्वैप्स नहीं पकड़ पाते।

## चरण 6: वास्तविक OCR इंजन के साथ एकीकृत करें (वैकल्पिक)

नीचे एक त्वरित उदाहरण है कि आप `pytesseract` का उपयोग करके पोस्ट‑प्रोसेसर को वास्तविक OCR फ्लो में कैसे प्लग करेंगे। यह भाग वैकल्पिक है लेकिन अंत‑से‑अंत पाइपलाइन दिखाता है।

```python
import pytesseract
from PIL import Image
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Initialize AI wrapper and register the cleaner
ai = AIProcessor()
ai.set_post_processor(correct_ocr_errors)

# Load an image containing a product label
image = Image.open("sample_label.png")

# Perform OCR (this returns raw text)
raw_ocr = pytesseract.image_to_string(image)

# Clean the OCR output
cleaned = ai.run_postprocessor(raw_ocr)

print("Raw OCR   :", raw_ocr)
print("Cleaned   :", cleaned)
```

> **Note:** `pytesseract` को आपके सिस्टम पर Tesseract OCR इंस्टॉल होना चाहिए। ऊपर दिया गया स्निपेट Windows, macOS, और Linux पर काम करता है जब तक बाइनरी आपके PATH में हो।

## चरण 7: परिणामों को प्रोग्रामेटिकली सत्यापित करें

जब आप बड़े बैचों को ऑटोमेट करते हैं, तो यह उपयोगी होता है कि क्लीनिंग स्टेप ने अपेक्षित रूप से काम किया है, यह सुनिश्चित किया जाए। एक त्वरित यूनिट टेस्ट बाद में घंटों की डिबगिंग बचा सकता है।

```python
def test_correct_ocr_errors():
    assert correct_ocr_errors("0O0") == "OOO"
    assert correct_ocr_errors(" 10A0B ") == "1OAOB"
    print("All tests passed!")

test_correct_ocr_errors()
```

इस टेस्ट को चलाने से पुष्टि होती है कि फ़ंक्शन **fixes OCR errors** लगातार ठीक करता है, यहाँ तक कि अतिरिक्त स्पेस छिपकर आएँ।

## छवि चित्रण

नीचे पाइपलाइन का एक दृश्य स्केच दिया गया है (मुख्य कीवर्ड alt टेक्स्ट में SEO के लिए दिखाई देता है)।

![OCR त्रुटियों को ठीक करने की पाइपलाइन आरेख – दिखाता है कच्चा OCR एक पोस्ट‑प्रोसेसर में जाता है जो शून्य को O से बदलता है]()

## निष्कर्ष – हमने क्या हासिल किया

हमने एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाया है कि Python में **how to clean OCR** आउटपुट कैसे किया जाए, विशेष रूप से **zero को O से बदलना** और **fix OCR errors** को एक मॉड्यूलर पोस्ट‑प्रोसेसर का उपयोग करके कैसे किया जाए। क्लीनिंग लॉजिक को OCR इंजन से अलग करके, आपको लचीलापन, परीक्षणयोग्यता, और भविष्य के नियम जोड़ने के लिए एक स्पष्ट स्थान मिलता है जैसे *how to clean OCR* अन्य कैरेक्टर भ्रमों के लिए।

अगले कदम के लिए तैयार हैं? प्रोडक्ट कोड के लिए regex वैलिडेटर जोड़ने का प्रयास करें, शोरयुक्त टेक्स्ट के लिए फज़ी मैचिंग के साथ प्रयोग करें, या `ocrmypdf` जैसी पूर्ण‑फ़ीचर लाइब्रेरी देखें जो पहले से ही पोस्ट‑प्रोसेसिंग हुक्स को बंडल करती है। हमने जो पैटर्न कवर किया है वह अच्छी तरह स्केल करता है, चाहे आप कुछ इनवॉइस संभाल रहे हों या लाखों स्कैन किए हुए दस्तावेज़।

---

*कोडिंग का आनंद लें, और आपकी OCR पाइपलाइन त्रुटि‑मुक्त रहे!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}