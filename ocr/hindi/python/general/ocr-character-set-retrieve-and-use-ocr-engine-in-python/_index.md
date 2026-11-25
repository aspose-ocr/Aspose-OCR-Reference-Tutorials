---
category: general
date: 2026-06-06
description: 'OCR कैरेक्टर सेट गाइड: जानिए कैसे OCR इंजन का उपयोग करके लैटिन और सिरिलिक
  लिपियों के लिए समर्थित अक्षरों की सूची बनाएं, पूर्ण Python उदाहरणों के साथ।'
draft: false
keywords:
- ocr character set
- use OCR engine
- supported OCR characters
- script detection OCR
- OCR library Python
language: hi
og_description: 'OCR कैरेक्टर सेट गाइड: जानें कि Python में OCR इंजन का उपयोग करके
  विभिन्न लिपियों के लिए समर्थित अक्षरों की सूची कैसे बनाएं, कोड और टिप्स के साथ पूर्ण।'
og_title: OCR कैरेक्टर सेट – OCR इंजन को प्राप्त करें और उपयोग करें
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: 'OCR character set guide: learn how to use OCR engine to list supported
    characters for Latin and Cyrillic scripts with full Python examples.'
  headline: OCR Character Set – Retrieve and Use OCR Engine in Python
  type: TechArticle
tags:
- OCR
- Python
- Character Sets
title: OCR कैरेक्टर सेट – पाइथन में OCR इंजन प्राप्त करें और उपयोग करें
url: /hi/python/general/ocr-character-set-retrieve-and-use-ocr-engine-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR कैरेक्टर सेट – Python में OCR इंजन को प्राप्त करें और उपयोग करें

क्या आप जानना चाहते हैं कि आपका लाइब्रेरी कौन सा **ocr character set** सपोर्ट करता है? इस ट्यूटोरियल में हम आपको दिखाएंगे कि **use OCR engine** का उपयोग करके विभिन्न स्क्रिप्ट्स के लिए समर्थित कैरेक्टर्स को कैसे क्वेरी करें, और यह वास्तविक‑दुनिया के प्रोजेक्ट्स के लिए क्यों महत्वपूर्ण है।

यदि आपने कभी खाली स्क्रीन पर घूरते हुए सोचा हो कि OCR प्रोसेसिंग के बाद कुछ अक्षर क्यों नहीं दिखते, तो आप अकेले नहीं हैं। उत्तर अक्सर उस कैरेक्टर सेट में छिपा होता है जिसे इंजन जानता है। इस गाइड के अंत तक आप सक्षम होंगे:

* किसी दिए गए स्क्रिप्ट के लिए OCR इंजन द्वारा पहचाने जा सकने वाले सभी कैरेक्टर्स की सूची बनाना।  
* उन मामलों को संभालना जहाँ स्क्रिप्ट समर्थित नहीं है।  
* कैरेक्टर‑सेट जानकारी को डाउनस्ट्रीम वैलिडेशन या UI लॉजिक में इंटीग्रेट करना।

कोई जादुई ब्लैक‑बॉक्स ट्रिक्स नहीं—सिर्फ साधारण Python, कुछ लाइनों का कोड, और थोड़ी सी व्याख्या।

---

## आवश्यकताएँ

शुरू करने से पहले, सुनिश्चित करें कि आपके पास है:

* Python 3.8+ स्थापित (कोड f‑strings का उपयोग करता है)।  
* वह OCR लाइब्रेरी जो `ocr.OcrEngine` प्रदान करती है—इस उदाहरण के लिए हम मानेंगे कि `ocr` नामक पैकेज पहले से `pip install ocr-lib` के माध्यम से स्थापित है।  
* Python के इम्पोर्ट सिस्टम और प्रिंटिंग की बुनियादी समझ।

यदि आपके पास लाइब्रेरी नहीं है, तो चलाएँ:

```bash
pip install ocr-lib
```

बस इतना ही—बुनियादी कैरेक्टर‑सेट क्वेरीज़ के लिए कोई अतिरिक्त बाइनरी या नेटिव डिपेंडेंसीज़ की आवश्यकता नहीं है।

---

## चरण 1: OCR इंजन इंस्टेंस को इनिशियलाइज़ करें

एक इंजन ऑब्जेक्ट बनाना वह पहला कदम है जब आप **use OCR engine** फ़ंक्शनलिटी का उपयोग करते हैं। इसे एक स्कैनर को ऑन करने के रूप में सोचें; इसके बिना आप कोई प्रश्न नहीं पूछ सकते।

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

`OcrEngine` क्लास अंतर्निहित रिकग्निशन इंजन के चारों ओर एक हल्का रैपर है। यह तब तक भारी प्रोसेसिंग नहीं शुरू करता जब तक आप कुछ अनुरोध नहीं करते, इसलिए स्टार्टअप लागत नगण्य है।

> **Pro tip:** यदि आपका एप्लिकेशन कई इंजन इंस्टेंस बनाता है, तो एक ही को पुन: उपयोग करें। यह मेमोरी बचाता है और इनिशियलाइज़ेशन लेटेंसी को कम करता है।

---

## चरण 2: किसी विशिष्ट स्क्रिप्ट के लिए OCR कैरेक्टर सेट को क्वेरी करें

अब जब हमारे पास एक इंजन है, हम उससे पूछ सकते हैं कि वह किसी विशेष लेखन प्रणाली के लिए कौन से कैरेक्टर्स जानता है। मेथड `get_supported_characters(script_name)` Python `list` के रूप में यूनिकोड कैरेक्टर्स लौटाता है।

```python
# Step 2: Get the list of characters the engine can recognize for the Latin script
latin_chars = engine.get_supported_characters("Latin")
print(f"Supported Latin chars ({len(latin_chars)}): {latin_chars}")
```

ऊपर दिया गया स्निपेट चलाने पर कुछ इस तरह का आउटपुट मिलता है:

```
Supported Latin chars (26): ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
```

सटीक आउटपुट OCR लाइब्रेरी के संस्करण पर निर्भर करता है, लेकिन आपको हमेशा कैरेक्टर्स की एक फ्लैट लिस्ट मिलेगी। यदि आपको अपरकेस और लोअरकेस दोनों चाहिए, तो बस `"Latin"` स्क्रिप्ट का अनुरोध करें और प्रत्येक एलिमेंट पर `.lower()` लागू करें, या यदि लाइब्रेरी उन्हें अलग करती है तो अलग `"Latin‑lower"` स्क्रिप्ट को क्वेरी करें।

### यह क्यों महत्वपूर्ण है?

जब आप किसी इमेज में असामान्य डायाक्रिटिक्स (जैसे “ñ” या “ø”) देते हैं, तो OCR इंजन उन्हें चुपचाप प्लेसहोल्डर से बदल सकता है या पूरी तरह हटा सकता है। पहले से **ocr character set** को जानना आपको इनपुट को पूर्व‑वैलिडेट करने, उपयोगकर्ताओं को चेतावनी देने, या किसी अन्य इंजन पर फॉल बैक करने में मदद करता है।

---

## चरण 3: किसी अन्य स्क्रिप्ट के लिए कैरेक्टर्स प्राप्त करें – Cyrillic उदाहरण

इसी मेथड का उपयोग किसी भी स्क्रिप्ट के लिए किया जा सकता है जिसे इंजन सपोर्ट करता है। चलिए देखते हैं Cyrillic के साथ क्या होता है।

```python
# Step 3: Get the list of characters the engine can recognize for the Cyrillic script
cyrillic_chars = engine.get_supported_characters("Cyrillic")
print(f"Supported Cyrillic chars ({len(cyrillic_chars)}): {cyrillic_chars}")
```

सामान्य आउटपुट:

```
Supported Cyrillic chars (33): ['А', 'Б', 'В', 'Г', 'Д', 'Е', 'Ё', 'Ж', 'З', 'И', 'Й', 'К', 'Л', 'М', 'Н', 'О', 'П', 'Р', 'С', 'Т', 'У', 'Ф', 'Х', 'Ц', 'Ч', 'Ш', 'Щ', 'Ъ', 'Ы', 'Ь', 'Э', 'Ю', 'Я']
```

यदि इंजन अनुरोधित स्क्रिप्ट को **सपोर्ट** नहीं करता, तो आमतौर पर यह `ValueError` उठाता है (या इम्प्लीमेंटेशन के अनुसार खाली लिस्ट लौटाता है)। चलिए इसके लिए सुरक्षा लागू करते हैं।

```python
def safe_get_characters(engine, script):
    try:
        chars = engine.get_supported_characters(script)
        if not chars:
            print(f"No characters returned for script '{script}'.")
        else:
            print(f"Supported {script} chars ({len(chars)}): {chars}")
        return chars
    except Exception as e:
        print(f"Error retrieving characters for script '{script}': {e}")
        return []

# Example usage:
safe_get_characters(engine, "Arabic")   # Might trigger the error branch
```

---

## चरण 4: OCR कैरेक्टर सेट को विज़ुअलाइज़ करें (वैकल्पिक)

कभी‑कभी एक त्वरित विज़ुअल मदद करता है, विशेषकर जब आपको स्टेकहोल्डर्स को दिखाना हो कि कौन से कैरेक्टर्स कवर किए गए हैं। नीचे `matplotlib` का उपयोग करके कैरेक्टर्स का ग्रिड रेंडर करने का एक न्यूनतम उदाहरण है।

```python
import matplotlib.pyplot as plt

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14, ha='center', va='center')
    plt.title(title)
    plt.show()

# Visualize Latin characters
plot_character_grid(latin_chars, title="Latin OCR Character Set")
```

> **Image alt text:** ![OCR कैरेक्टर सेट डायग्राम](ocr_character_set.png){alt="OCR कैरेक्टर सेट का अवलोकन"}

डायग्राम कोर समाधान के लिए आवश्यक नहीं है, लेकिन यह दर्शाता है कि आप **use OCR engine** मेटाडेटा को साधारण प्रिंटिंग से आगे कैसे उपयोग कर सकते हैं।

---

## चरण 5: वास्तविक‑दुनिया के वर्कफ़्लो में कैरेक्टर सेट को इंटीग्रेट करें

अब जब हम **ocr character set** को प्राप्त कर सकते हैं, चलिए एक व्यावहारिक परिदृश्य देखते हैं: डेटाबेस में सहेजने से पहले OCR आउटपुट को वैलिडेट करना।

```python
def validate_ocr_output(text, allowed_chars):
    """Return True if every character in `text` exists in `allowed_chars`."""
    invalid = [c for c in text if c not in allowed_chars]
    if invalid:
        print(f"Invalid characters found: {invalid}")
        return False
    return True

# Suppose we ran OCR on an image and got this result:
ocr_result = "HELLO WORLD!"

# Use the previously fetched Latin set for validation:
if validate_ocr_output(ocr_result, set(latin_chars)):
    print("All characters are supported – safe to store.")
else:
    print("Result contains unsupported symbols – consider manual review.")
```

यह पैटर्न गार्बेज डेटा को डाउनस्ट्रीम पाइपलाइन में प्रवेश करने से रोकता है, जो बहुभाषी दस्तावेज़ों के साथ काम करते समय एक आम समस्या है।

---

## सामान्य समस्याएँ और किनारे के केस

| समस्या | क्यों होता है | कैसे बचें |
|---------|----------------|--------------|
| **स्क्रिप्ट नाम टाइपो** (जैसे `"Cyrillic "` ट्रेलिंग स्पेस के साथ) | इंजन स्ट्रिंग को लिटरली लेता है और स्क्रिप्ट नहीं ढूँढ पाता। | `script.strip()` करके व्हाइटस्पेस हटाएँ, फिर `get_supported_characters` कॉल करें। |
| **खाली कैरेक्टर लिस्ट** | कुछ इंजन स्क्रिप्ट दिखाते हैं लेकिन भाषा मॉडल अभी लोड नहीं किया है। | यदि लाइब्रेरी ऐसा मेथड देती है तो `engine.load_language_model(script)` कॉल करें, या सुनिश्चित करें कि मॉडल फ़ाइलें मौजूद हैं। |
| **Unicode सामान्यीकरण समस्याएँ** | “é” जैसे कैरेक्टर्स कंपोज़्ड (`\u00E9`) या डी-कम्पोज़्ड (`e\u0301`) रूप में हो सकते हैं। | वैलिडेशन से पहले `unicodedata.normalize('NFC', text)` से स्ट्रिंग्स को नॉर्मलाइज़ करें। |
| **बड़ी स्क्रिप्ट्स पर प्रदर्शन** (जैसे Chinese) | हजारों कैरेक्टर्स को रिट्रीव करना धीमा हो सकता है। | पहली कॉल के बाद परिणाम को कैश करें; अधिकांश एप्लिकेशन को लिस्ट केवल एक बार चाहिए। |

---

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ मिलाकर, यहाँ एक सिंगल स्क्रिप्ट है जिसे आप कॉपी‑पेस्ट करके चला सकते हैं:



## अब आप क्या सीखें?

- [Aspose OCR ट्यूटोरियल – ऑप्टिकल कैरेक्टर रिकग्निशन](/ocr/english/)
- [OCR पोस्ट प्रोसेसिंग – कैरेक्टर विकल्प प्राप्त करें](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [OCR इमेज रिकग्निशन में थ्रेशहोल्ड वैल्यू कैसे सेट करें](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}