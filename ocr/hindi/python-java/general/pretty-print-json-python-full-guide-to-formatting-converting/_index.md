---
category: general
date: 2026-06-16
description: JSON को Python में जल्दी से प्रीटी प्रिंट करें और सीखें कि JSON को dict
  में कैसे बदलें या डेटा मैनिपुलेशन के लिए JSON स्ट्रिंग को Python में कैसे लोड करें।
  चरण‑दर‑चरण ट्यूटोरियल।
draft: false
keywords:
- pretty print json python
- convert json to dict
- load json string python
language: hi
og_description: JSON को सुंदर रूप से प्रिंट करें Python में और तुरंत देखें कि JSON
  को dict में कैसे बदलें या JSON स्ट्रिंग को Python में कैसे लोड करें। मिनटों में
  JSON हैंडलिंग में निपुण बनें।
og_title: Python में JSON को सुंदर रूप से प्रिंट करना – पूर्ण फ़ॉर्मेटिंग और रूपांतरण
  गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Pretty print JSON Python quickly and learn how to convert JSON to dict
    or load JSON string Python for data manipulation. Step‑by‑step tutorial.
  headline: Pretty Print JSON Python – Full Guide to Formatting & Converting
  type: TechArticle
tags:
- python
- json
- data‑processing
title: प्रिटी प्रिंट JSON पायथन – फॉर्मेटिंग और रूपांतरण की पूरी गाइड
url: /hi/python-java/general/pretty-print-json-python-full-guide-to-formatting-converting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pretty Print JSON Python – फ़ॉर्मेटिंग और कन्वर्ज़न के लिए पूर्ण गाइड

क्या आपको कभी **pretty print JSON Python** करने की ज़रूरत पड़ी है और आश्चर्य हुआ कि आउटपुट हमेशा एक ही, पढ़ने योग्य नहीं लाइन जैसा क्यों दिखता है? आप अकेले नहीं हैं। कई प्रोजेक्ट्स में कच्चा JSON स्ट्रिंग एक उलझा हुआ गड़बड़ होता है, जिससे डिबगिंग ऐसा महसूस होती है जैसे घास के ढेर में सुई ढूँढना।  

अच्छी खबर? कुछ बिल्ट‑इन फ़ंक्शन्स के साथ आप उस अराजक ब्लॉब को एक सुन्दर इंडेंटेड व्यू में बदल सकते हैं, और फिर **convert JSON to dict** करके सुगम डाउनस्ट्रीम प्रोसेसिंग कर सकते हैं। इस ट्यूटोरियल में हम हर कदम को समझेंगे—Python में JSON स्ट्रिंग लोड करने से लेकर उसके डेटा पर इटरेट करने तक—ताकि आप फ़ॉर्मेटिंग से जूझने के बजाय लॉजिक पर ध्यान दे सकें।

## इस ट्यूटोरियल में क्या कवर किया गया है

- कैसे `json.dumps` के साथ `indent` आर्ग्यूमेंट का उपयोग करके **pretty print JSON Python** किया जाए।  
- सही तरीका जिससे **load JSON string Python** को एक नेटिव डिक्शनरी में लोड किया जा सके।  
- परिणामी डिक्शनरी को उपयोगी Python ऑब्जेक्ट्स में बदलना, जिसमें एक व्यावहारिक उदाहरण शामिल है जो प्रत्येक शब्द को उसकी confidence स्कोर के साथ प्रिंट करता है।  
- आम समस्याएँ (जैसे non‑ASCII कैरेक्टर्स को हैंडल करना) और त्वरित समाधान।  
- एक पूर्ण, चलने योग्य स्क्रिप्ट जिसे आप तुरंत कॉपी‑पेस्ट करके अनुकूलित कर सकते हैं।  

इस गाइड के अंत तक आप किसी भी JSON पेलोड को मानव‑पठनीय फ़ॉर्मेट में बदल सकेंगे और उसे शुद्ध Python के साथ मैनिपुलेट कर सकेंगे—कोई बाहरी लाइब्रेरी आवश्यक नहीं।

---

## पूर्वापेक्षाएँ

- Python 3.8 या उससे नया ( `json` मॉड्यूल स्टैंडर्ड लाइब्रेरी का हिस्सा है)।  
- डिक्शनरी और लूप्स की बुनियादी समझ।  
- वैकल्पिक रूप से, एक OCR इंजन या कोई भी सर्विस जो JSON रिटर्न करती है—हमारा उदाहरण एक मॉक `engine.recognize()` कॉल का उपयोग करता है, लेकिन आप इसे अपने डेटा स्रोत से बदल सकते हैं।

---

## चरण 1: OCR (या कोई भी JSON‑जनरेटिंग) रिकग्निशन करें

सबसे पहले, आपको एक JSON‑संगत परिणाम चाहिए। कई कंप्यूटर‑विजन वर्कफ़्लोज़ में OCR इंजन एक स्ट्रक्चर्ड ऑब्जेक्ट आउटपुट करता है जिसे JSON में सीरियलाइज़ किया जा सकता है। यहाँ एक न्यूनतम प्लेसहोल्डर है:

```python
# Step 1: Simulate an OCR engine that returns a result object
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    # The real engine would have a .to_json() method; we mimic it
    def to_json(self, indent=None):
        import json
        return json.dumps({"words": self.words}, indent=indent)

# Imagine `engine` is your pre‑configured OCR engine
engine = MockResult()
result = engine  # In real code: result = engine.recognize()
```

> **इस चरण का महत्व:**  
> भले ही आप OCR नहीं कर रहे हों, आप अक्सर API, फ़ाइल, या मैसेज क्व्यू से डेटा प्राप्त करेंगे। ऑब्जेक्ट को **pretty print** करने से पहले JSON में सीरियलाइज़ेबल होना चाहिए।

---

## चरण 2: Pretty Print JSON Python

अब हम कच्चे डेटा को एक सुन्दर इंडेंटेड स्ट्रिंग में बदलते हैं। `indent` पैरामीटर इस काम को संभालता है।

```python
# Step 2: Serialize the result with pretty printing
json_str = result.to_json(indent=2)  # <-- pretty print JSON Python
print("🔍 Pretty‑printed JSON output:")
print(json_str)   # optional: view the raw JSON output
```

आउटपुट इस प्रकार दिखेगा:

```json
{
  "words": [
    {
      "text": "Hello",
      "confidence": 0.98
    },
    {
      "text": "World",
      "confidence": 0.95
    }
  ]
}
```

> **प्रो टिप:** यदि आप अधिक स्पेसिंग चाहते हैं तो `indent=4` उपयोग करें, या कुंजियों को वर्णक्रमानुसार क्रमबद्ध करने के लिए `sort_keys=True` जोड़ें।

---

## चरण 3: Load JSON String Python → नेटिव डिक्शनरी

एक pretty‑printed स्ट्रिंग मनुष्यों के लिए बढ़िया है, लेकिन वास्तविक काम के लिए Python डिक्शनरी को पसंद करता है। यहाँ हम **load JSON string Python** को एक नेटिव स्ट्रक्चर में लोड करते हैं।

```python
# Step 3: Convert the JSON string to a Python dict
import json

result_dict = json.loads(json_str)   # <-- load json string python
print("\n✅ Loaded dict type:", type(result_dict))
```

आपको यह दिखेगा:

```
✅ Loaded dict type: <class 'dict'>
```

> **हम यह क्यों करते हैं:**  
> डिक्शनरी आपको O(1) लुक‑अप, म्यूटेबल डेटा, और Python इकोसिस्टम के बाकी हिस्सों के साथ सहज इंटीग्रेशन देती है। सीधे JSON स्ट्रिंग के साथ काम करने से आपको जटिल स्ट्रिंग पार्सिंग करनी पड़ेगी।

---

## चरण 4: पहचाने गए शब्दों पर इटरेट करें – एक वास्तविक‑दुनिया का उपयोग केस

आइए प्रत्येक शब्द और उसकी confidence स्कोर निकालें। यह **convert json to dict** (जो डिक्शनरी हमारे पास पहले से है) और व्यावहारिक इटरेशन दोनों को दर्शाता है।

```python
# Step 4: Display each word with its confidence score
print("\n🗣️ Recognized words and confidence values:")
for word in result_dict["words"]:
    # f‑string gives us a clean, readable line
    print(f'{word["text"]} (conf: {word["confidence"]})')
```

अपेक्षित आउटपुट:

```
🗣️ Recognized words and confidence values:
Hello (conf: 0.98)
World (conf: 0.95)
```

> **एज केस टिप:** यदि JSON में `"words"` कुंजी गायब हो सकती है, तो `KeyError` से बचें:

```python
for word in result_dict.get("words", []):
    # safe iteration even when "words" is absent
    print(f'{word.get("text", "<unknown>")} (conf: {word.get("confidence", 0)})')
```

---

## चरण 5: Non‑ASCII कैरेक्टर्स को हैंडल करना (Unicode सपोर्ट)

OCR इंजन अक्सर “é” या “ü” जैसे कैरेक्टर्स रिटर्न करते हैं। डिफ़ॉल्ट `json.dumps` उन्हें `\u00e9` के रूप में एस्केप करता है। उन्हें पढ़ने योग्य रखने के लिए `ensure_ascii=False` पास करें।

```python
# Example with non‑ASCII text
result.words.append({"text": "café", "confidence": 0.92})
json_str_utf8 = result.to_json(indent=2)
json_str_utf8 = json.dumps(json.loads(json_str_utf8), indent=2, ensure_ascii=False)

print("\n🌍 Pretty‑printed JSON with Unicode:")
print(json_str_utf8)
```

अब आउटपुट में एस्केप्ड संस्करण के बजाय **café** दिखेगा। यह तब आवश्यक है जब आप बाद में **convert json to dict** करेंगे; डिक्शनरी में उचित Unicode स्ट्रिंग्स होंगी।

---

## चरण 6: Pretty‑Printed JSON को सेव और रीलोड करना (वैकल्पिक)

कभी-कभी आप फॉर्मेटेड JSON को फ़ाइल में सहेजना चाहते हैं बाद में निरीक्षण के लिए।

```python
# Step 6: Write pretty JSON to a file
with open("ocr_result_pretty.json", "w", encoding="utf-8") as f:
    f.write(json_str_utf8)

# Later you can read it back and still have a dict
with open("ocr_result_pretty.json", "r", encoding="utf-8") as f:
    loaded_dict = json.load(f)   # <-- load json string python from file
print("\n📂 Loaded back from file, type:", type(loaded_dict))
```

फ़ाइल में सुन्दर इंडेंटेड JSON होगा, और `json.load` इसे स्वचालित रूप से डिक्शनरी में पार्स कर देगा।

---

## चरण 7: सब कुछ एक साथ रखना – एक-फ़ाइल समाधान

नीचे एक स्व-निहित स्क्रिप्ट है जो चर्चा किए गए सभी चरणों को शामिल करती है। इसे `pretty_json_demo.py` नाम की फ़ाइल में डालें और चलाएँ।

```python
#!/usr/bin/env python3
"""
Complete example: pretty print JSON Python, convert JSON to dict,
and load JSON string Python for further processing.
"""

import json

# ----------------------------------------------------------------------
# Mock OCR engine – replace with your real engine when ready
# ----------------------------------------------------------------------
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    def to_json(self, indent=None, ensure_ascii=True):
        # Produce a JSON string; indent triggers pretty printing
        return json.dumps({"words": self.words}, indent=indent, ensure_ascii=ensure_ascii)

# ----------------------------------------------------------------------
# Main workflow
# ----------------------------------------------------------------------
def main():
    # Step 1: Get the result object (real code would call engine.recognize())
    result = MockResult()

    # Step 2: Pretty print JSON Python
    json_str = result.to_json(indent=2)          # pretty print JSON Python
    print("🔍 Pretty‑printed JSON:")
    print(json_str)

    # Step 3: Load JSON string Python → dict
    result_dict = json.loads(json_str)          # load json string python
    print("\n✅ Dictionary type:", type(result_dict))

    # Step 4: Iterate over words
    print("\n🗣️ Words with confidence:")
    for word in result_dict.get("words", []):
        print(f'{word.get("text", "<missing>")} (conf: {word.get("confidence", 0)})')

    # Step 5: Demonstrate Unicode handling
    result.words.append({"text": "café", "confidence": 0.92})
    json_utf8 = result.to_json(indent=2, ensure_ascii=False)
    print("\n🌍 Unicode‑friendly pretty JSON:")
    print(json_utf8)

    # Step 6: Save to file and reload
    with open("pretty_output.json", "w", encoding="utf-8") as f:
        f.write(json_utf8)

    with open("pretty_output.json", "r", encoding="utf-8") as f:
        reloaded = json.load(f)                 # load json string python from file
    print("\n📂 Reloaded dict, size:", len(reloaded.get("words", [])))

if __name__ == "__main__":
    main()
```

चलाएँ:

```bash
python pretty_json_demo.py
```

आपको pretty‑printed JSON, डिक्शनरी टाइप, प्रत्येक शब्द उसका confidence के साथ, और `pretty_output.json` में सहेजा गया Unicode‑friendly संस्करण दिखेगा।  

**यही पूरी कहानी है**—कच्चे OCR आउटपुट से लेकर एक साफ़, मैनिपुलेटेबल Python डिक्शनरी तक।

---

## अक्सर पूछे जाने वाले प्रश्न (FAQs)

| प्रश्न | उत्तर |
|----------|--------|
| **क्या मुझे बाहरी लाइब्रेरी की जरूरत है?** | नहीं। बिल्ट‑इन `json` मॉड्यूल दोनों pretty printing और loading को संभालता है। |
| **अगर मेरा JSON बहुत बड़ा हो तो?** | `json.dump` को फ़ाइल हैंडल के साथ उपयोग करें ताकि सब कुछ मेमोरी में लोड न करना पड़े; आप अभी भी pretty फ़ाइल के लिए `indent` सेट कर सकते हैं। |
| **क्या मैं कुंजियों को सॉर्ट कर सकता हूँ?** | हाँ—डिटर्मिनिस्टिक ऑर्डरिंग के लिए `json.dumps` में `sort_keys=True` जोड़ें, जो diff‑आधारित टेस्टिंग में मदद करता है। |
| **मैं खराब JSON को कैसे हैंडल करूँ?** | `json.loads` को `try/except json.JSONDecodeError` ब्लॉक में रैप करें और समस्या वाली स्ट्रिंग को लॉग करें। |
| **क्या कोई तेज़ विकल्प है?** | बड़े पेलोड्स के लिए, `orjson` या `ujson` जैसी लाइब्रेरीज़ तेज़ हैं, लेकिन वे `indent` को सपोर्ट नहीं करतीं। |

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [इमेज रिकग्निशन में JSON परिणाम के लिए Aspose OCR का उपयोग कैसे करें](/ocr/english/net/text-recognition/get-result-as-json/)
- [इमेज रिकग्निशन में JSON परिणाम प्राप्त करने के लिए Aspose OCR का उपयोग कैसे करें](/ocr/spanish/net/text-recognition/get-result-as-json/)
- [इमेज रिकग्निशन में JSON‑परिणामों के लिए Aspose OCR का उपयोग कैसे करें](/ocr/german/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}