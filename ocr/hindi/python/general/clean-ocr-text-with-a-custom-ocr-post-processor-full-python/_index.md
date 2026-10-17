---
category: general
date: 2026-06-22
description: Python में OCR पोस्ट‑प्रोसेसर का उपयोग करके OCR टेक्स्ट को साफ़ करना
  सीखें। चरण‑दर‑चरण कोड, व्याख्याएँ और विश्वसनीय संरचित JSON आउटपुट के लिए टिप्स।
draft: false
keywords:
- clean OCR text
- OCR post processor
- Python OCR workflow
- structured JSON OCR
- OCR confidence averaging
language: hi
og_description: OCR पोस्ट‑प्रोसेसर जोड़कर OCR टेक्स्ट को तुरंत साफ़ करें। यह गाइड
  पूरी Python कार्यान्वयन, यह क्यों काम करता है, और इसे कैसे अनुकूलित किया जाए, दिखाता
  है।
og_title: कस्टम OCR पोस्ट प्रोसेसर के साथ OCR टेक्स्ट को साफ़ करें – पायथन ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to clean OCR text using an OCR post processor in Python.
    Step‑by‑step code, explanations, and tips for reliable structured JSON output.
  headline: Clean OCR Text with a Custom OCR Post Processor – Full Python Guide
  type: TechArticle
tags:
- OCR
- Python
- post‑processing
title: कस्टम OCR पोस्ट प्रोसेसर के साथ OCR टेक्स्ट को साफ़ करें – पूर्ण Python गाइड
url: /hi/python/general/clean-ocr-text-with-a-custom-ocr-post-processor-full-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# कस्टम OCR पोस्ट‑प्रोसेसर के साथ OCR टेक्स्ट को साफ़ करें – पूर्ण Python गाइड

क्या आपको कभी **OCR टेक्स्ट को साफ़** करने की ज़रूरत पड़ी है, लेकिन कच्चा आउटपुट लाइन‑ब्रेक, अनावश्यक स्पेस और कम‑विश्वास वाले अक्षरों के कारण परेशान कर रहा था? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया पाइपलाइन में OCR इंजन आपको टेक्स्ट के साथ एक कॉन्फिडेंस स्कोर देता है, और आपको इसे उपयोगी रूप में बदलना पड़ता है।  

अच्छी खबर? एक छोटा **OCR पोस्ट‑प्रोसेसर** परिणाम को व्यवस्थित कर सकता है, औसत कॉन्फिडेंस की गणना कर सकता है, और सब कुछ एक साफ़ JSON स्ट्रिंग में पैक कर सकता है—बिना कोर इंजन को छुए। इस ट्यूटोरियल में हम वह पोस्ट‑प्रोसेसर बनाएँगे, इसे एक सामान्य AI/OCR इंजन के साथ रजिस्टर करेंगे, और हर कोड लाइन को विस्तार से समझेंगे ताकि आप इसे अपने प्रोजेक्ट में कल ही उपयोग कर सकें।

---

## इस ट्यूटोरियल में क्या कवर किया गया है

- एक **clean OCR text** पोस्ट‑प्रोसेसर बनाना जो व्हाइटस्पेस को सामान्य करता है और लाइन‑ब्रेक हटाता है।  
- क्यों **average confidence** की गणना डाउनस्ट्रीम वैलिडेशन के लिए महत्वपूर्ण है।  
- OCR इंजन के साथ प्रोसेसर को रजिस्टर करना (`ai.set_post_processor` पैटर्न)।  
- परिणामस्वरूप संरचित JSON को दिखाना और सामान्य एज केसों का ट्रबलशूटिंग।  

Python स्टैंडर्ड लाइब्रेरी के अलावा कोई बाहरी लाइब्रेरी आवश्यक नहीं है, इसलिए आप इसे किसी भी सिस्टम पर फॉलो कर सकते हैं जो Python 3.8+ चलाता है।  

---

## आवश्यकताएँ

- एक कार्यशील OCR इंजन जो `ocr_result` ऑब्जेक्ट प्रदान करता है, जिसमें `text`, `confidence` (फ़्लोट्स की सूची), और `bounding_boxes` होते हैं।  
- Python फ़ंक्शन और JSON हैंडलिंग की बुनियादी समझ।  
- वैकल्पिक: डिपेंडेंसीज़ को व्यवस्थित रखने के लिए एक वर्चुअल एनवायरनमेंट।  

यदि आप सुनिश्चित नहीं हैं कि आपका इंजन कस्टम पोस्ट‑प्रोसेसर सपोर्ट करता है या नहीं, तो उसकी डॉक्यूमेंटेशन में `set_post_processor` मेथड देखें—अधिकांश आधुनिक AI‑पावर्ड OCR SDKs में यह उपलब्ध होता है।

---

## चरण 1: OCR पोस्ट‑प्रोसेसर परिभाषित करें जो **Clean OCR Text** करता है

सबसे पहले, हम एक फ़ंक्शन लिखते हैं जो कच्चा OCR परिणाम लेता है, टेक्स्ट को सैनिटाइज़ करता है, कॉन्फिडेंस मीट्रिक की गणना करता है, और एक JSON स्ट्रिंग रिटर्न करता है। ध्यान दें कि प्रत्येक ऑपरेशन को जानबूझकर टिप्पणी किया गया है; ये टिप्पणियाँ “क्यों” को दर्शाती हैं, जिसे AI असिस्टेंट अक्सर उद्धृत करते हैं।

```python
import json

def create_structured_json(ocr_result, **kwargs):
    """
    Turn an OCR result into a clean, structured JSON payload.

    Parameters
    ----------
    ocr_result : object
        Must expose .text (raw string), .confidence (list of floats),
        and .bounding_boxes (list of box coordinates).

    Returns
    -------
    str
        JSON string with cleaned text, average confidence, and bounding boxes.
    """
    # 1️⃣ Clean the raw text: replace newlines with spaces and trim excess whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # 2️⃣ Compute the average confidence – useful for quality gating.
    # Guard against division by zero if the engine returns an empty list.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0  # fallback when confidence data is missing

    # 3️⃣ Preserve the original bounding boxes for downstream layout analysis.
    boxes = ocr_result.bounding_boxes

    # 4️⃣ Assemble the dictionary and dump it as a JSON string.
    data = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }

    # ensure_ascii=False keeps Unicode characters intact (think accented letters, emojis, etc.)
    return json.dumps(data, ensure_ascii=False)
```

**यह क्यों काम करता है:**  
- `replace("\n", " ")` मल्टी‑लाइन OCR आउटपुट को एकल, सर्चेबल स्ट्रिंग में बदल देता है—जो अधिकांश पाइपलाइन में “clean OCR text” का अर्थ है।  
- लीडिंग/ट्रेलिंग स्पेस हटाने से फैंटम खाली टोकन नहीं बनते, जो बाद में टोकनाइज़र को तोड़ सकते हैं।  
- औसत कॉन्फिडेंस की गणना करने से आपको एकल क्वालिटी मीट्रिक मिलती है; आप थ्रेशहोल्ड (जैसे 0.85) से नीचे के परिणामों को डेटाबेस में सेव करने से पहले रिजेक्ट कर सकते हैं।  
- बाउंडिंग बॉक्स को जैसा का तैसा रखने से आप मूल लेआउट को अभी भी रेंडर कर सकते हैं, यदि आपको लो‑कॉन्फिडेंस क्षेत्रों को हाईलाइट करना हो।

---

## चरण 2: कस्टम **OCR पोस्ट‑प्रोसेसर** को अपने इंजन के साथ रजिस्टर करें

अधिकांश AI‑पावर्ड OCR SDKs एक मेथड प्रदान करते हैं जिससे आप पोस्ट‑प्रोसेसिंग कॉलबैक जोड़ सकते हैं। नीचे हम मानते हैं कि `ai` (इंजन) नाम का ऑब्जेक्ट `set_post_processor` उपलब्ध कराता है। यदि आपका लाइब्रेरी अलग नाम इस्तेमाल करता है, तो उसे उसी अनुसार बदलें।

```python
# Register the post‑processor; the second argument can hold custom settings.
ai.set_post_processor(create_structured_json, custom_settings={})
```

**टिप:** यदि आपको कभी व्यवहार टॉगल करने की ज़रूरत पड़े (जैसे newline रिमूवल को एनेबल/डिसएबल करना), तो `custom_settings` के माध्यम से कॉन्फ़िगरेशन पास करें। इससे प्रोसेसर कई प्रोजेक्ट्स में पुन: उपयोग योग्य बनता है।

---

## चरण 3: OCR इंजन चलाएँ – अब परिणाम एक JSON स्ट्रिंग है

पोस्ट‑प्रोसेसर संलग्न करने के बाद, `engine.recognize()` (या आपका SDK जो भी मेथड हो) कॉल करने से `create_structured_json` स्वचालित रूप से कॉल होगा। इंजन तब एक ऑब्जेक्ट रिटर्न करता है जिसका `.text` एट्रिब्यूट पहले से ही JSON पेलोड रखता है।

```python
# The engine runs OCR, then our post‑processor formats the output.
structured_result = engine.recognize()
```

> **नोट:** कुछ SDKs एक साधारण स्ट्रिंग रिटर्न कर सकते हैं, न कि `.text` एट्रिब्यूट वाला ऑब्जेक्ट। अगले चरण को उसी अनुसार एडजस्ट करें।

---

## चरण 4: संरचित JSON आउटपुट को प्रदर्शित (या सहेजें)

अंत में, हम JSON को कंसोल पर प्रिंट करते हैं। प्रोडक्शन सेटिंग में आप इसे फ़ाइल, मैसेज क्यू या डेटाबेस में लिखेंगे।

```python
# Show the clean OCR text and additional metadata.
print("Structured JSON:", structured_result.text)
```

**अपेक्षित कंसोल आउटपुट** (पढ़ने में आसान फ़ॉर्मेट):

```json
{
  "clean_text": "The quick brown fox jumps over the lazy dog.",
  "average_confidence": 0.9375,
  "boxes": [
    [0, 0, 120, 30],
    [0, 35, 115, 30],
    ...
  ]
}
```

यदि आपको अनचाहे newline कैरेक्टर या `0.0` कॉन्फिडेंस दिखे, तो सुनिश्चित करें कि आपका OCR इंजन वास्तव में `ocr_result.confidence` को पॉपुलेट कर रहा है। पोस्ट‑प्रोसेसर में मौजूद गार्ड क्लॉज़ `ZeroDivisionError` से बचाता है, लेकिन आपको फिर भी पता होना चाहिए कि कॉन्फिडेंस डेटा क्यों गायब है।

---

## सामान्य एज केसों का हैंडलिंग

| स्थिति | ध्यान देने योग्य बात | त्वरित समाधान |
|-----------|-------------------|-----------|
| **खाली OCR परिणाम** | `ocr_result.text` `""` है और `confidence` सूची खाली है | प्रोसेसर पहले से ही `clean_text` को खाली और `average_confidence` = 0.0 रिटर्न करता है। यदि आप पूरी तरह से JSON जेनरेशन स्किप करना चाहते हैं, तो एक कंडीशनल अर्ली‑रिटर्न जोड़ सकते हैं। |
| **Non‑ASCII कैरेक्टर** | Unicode एस्केप हो रहा है (`\u00e9`) | `ensure_ascii=False` (कोड में पहले से ही है) इस्तेमाल करें ताकि “é” जैसे कैरेक्टर पढ़ने योग्य रहें। |
| **बहुत बड़े दस्तावेज़** | JSON आकार API लिमिट से अधिक हो सकता है | आउटपुट को स्ट्रीम करने या फ़ाइल में लिखने पर विचार करें, बजाय एक ही स्ट्रिंग रिटर्न करने के। |
| **बाउंडिंग बॉक्स गायब** | कुछ OCR इंजन लेआउट डेटा नहीं देते | `boxes` को `None` या खाली सूची सेट करें; डाउनस्ट्रीम कंज्यूमर को अनुपस्थिति को सुगमता से हैंडल करना चाहिए। |

---

## प्रो टिप्स एवं बेस्ट प्रैक्टिसेज

- **बैच प्रोसेसिंग:** यदि आपको सैकड़ों पेज OCR करने हैं, तो रिकग्निशन कॉल को लूप में रैप करें और प्रत्येक JSON पेलोड को एक सूची में इकट्ठा करें। फिर पूरी सूची को एक फ़ाइल में डंप करें ताकि बैच एनालिसिस आसान हो।  
- **कॉन्फिडेंस थ्रेशहोल्ड:** पर्सिस्ट करने से पहले `average_confidence` चेक करें। एक सामान्य नियम: क्रिटिकल डेटा एंट्री टास्क के लिए `0.80` से नीचे के परिणामों को रिजेक्ट करें।  
- **प्रिंट की बजाय लॉगिंग:** प्रोडक्शन में `print()` को स्ट्रक्चर्ड लॉगर (`logging.info(...)`) से बदलें, ताकि आप ट्रैक कर सकें कौन‑सी इमेजेज़ ने लो‑कॉन्फिडेंस परिणाम दिए।  
- **टेस्टिंग:** एक यूनिट टेस्ट लिखें जो ज्ञात टेक्स्ट और कॉन्फिडेंस वैल्यू वाले मॉक `ocr_result` को फीड करे, फिर असर्ट करे कि JSON स्ट्रक्चर अपेक्षित है।  

---

## पूर्ण कार्यशील उदाहरण (सभी चरण एक साथ)

नीचे पूरा स्क्रिप्ट दिया गया है जिसे आप `ocr_cleanup.py` नाम की फ़ाइल में कॉपी‑पेस्ट कर सकते हैं। प्लेसहोल्डर `engine` और `ai` ऑब्जेक्ट को अपने OCR SDK के वास्तविक इंस्टेंस से बदलें।

```python
import json

# ----------------------------------------------------------------------
# Step 1: Define the post‑processor that cleans OCR text and builds JSON.
# ----------------------------------------------------------------------
def create_structured_json(ocr_result, **kwargs):
    """
    Convert raw OCR output into a clean JSON string.
    """
    # Clean the raw text: collapse newlines, trim whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # Safely compute average confidence.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0

    # Keep bounding boxes for layout work.
    boxes = ocr_result.bounding_boxes

    payload = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }
    return json.dumps(payload, ensure_ascii=False)

# ----------------------------------------------------------------------
# Step 2: Register the post‑processor with the OCR engine.
# ----------------------------------------------------------------------
# Replace `ai` with your actual engine/controller instance.
ai.set_post_processor(create_structured_json, custom_settings={})

# ----------------------------------------------------------------------
# Step 3: Run OCR – the result is automatically transformed.
# ----------------------------------------------------------------------
structured_result = engine.recognize()

# ----------------------------------------------------------------------
# Step 4: Output the structured JSON.
# ----------------------------------------------------------------------
print("Structured JSON:", structured_result.text)
```

फ़ाइल सहेजें, `python ocr_cleanup.py` चलाएँ, और आपको एक सुंदर फ़ॉर्मेटेड JSON स्ट्रिंग दिखेगी जिसमें **clean OCR text**, औसत कॉन्फिडेंस स्कोर, और मूल बाउंडिंग बॉक्स शामिल होंगे।

---

## निष्कर्ष

अब आपके पास एक पूर्ण, प्रोडक्शन‑रेडी तरीका है **clean OCR text** प्राप्त करने का, कस्टम **OCR पोस्ट‑प्रोसेसर** के माध्यम से Python में। यह समाधान व्हाइटस्पेस को सामान्य करता है, मिसिंग कॉन्फिडेंस डेटा से बचाव करता है, और एक स्व‑वर्णनात्मक JSON पेलोड रिटर्न करता है जिसे डाउनस्ट्रीम सर्विसेज़ बिना अतिरिक्त पार्सिंग के उपयोग कर सकती हैं।  

अब आप आगे कर सकते हैं:

- प्रोसेसर को **लो‑कॉन्फिडेंस शब्दों** को फ़िल्टर करने के लिए विस्तारित करें, फिर `clean_text` बनाएं।  
- **भाषा डिटेक्शन** जोड़ें ताकि JSON को लोकैल‑स्पेसिफिक पाइपलाइन में रूट किया जा सके।  
- इस पोस्ट‑प्रोसेसर को **स्पेल‑चेकिंग** लाइब्रेरी के साथ मिलाकर अतिरिक्त क्वालिटी लेयर जोड़ें।  

कोड को अपनी ज़रूरतों के अनुसार कस्टमाइज़ करें, विभिन्न कॉन्फिडेंस थ्रेशहोल्ड के साथ प्रयोग करें, या अपने सुधार कमेंट्स में साझा करें। हैप्पी कोडिंग!

## अगला क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और स्टेप‑बाय‑स्टेप एक्सप्लानेशन है, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}