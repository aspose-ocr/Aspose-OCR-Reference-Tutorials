---
category: general
date: 2026-01-12
description: AsposeAI से जानकारी प्रदर्शित करना सीखें, स्थानीय मॉडलों की सूची बनाकर,
  मॉडल का नाम, आकार और अंतिम उपयोग का टाइमस्टैम्प स्पष्ट Python उदाहरण में दिखाते
  हुए।
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: hi
og_description: 'AsposeAI से जानकारी कैसे प्रदर्शित करें: स्थानीय मॉडल सूचीबद्ध करें,
  मॉडल का नाम, आकार और अंतिम उपयोग किए गए टाइमस्टैम्प को पूर्ण Python walkthrough
  के साथ दिखाएँ।'
og_title: सूचना कैसे प्रदर्शित करें – स्थानीय मॉडल, नाम, आकार, अंतिम उपयोग।
tags:
- AsposeAI
- Python
- Model Management
title: जानकारी कैसे दिखाएँ – स्थानीय मॉडल, नाम, आकार, अंतिम उपयोग
url: /hi/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जानकारी कैसे दिखाएँ – स्थानीय मॉडल सूचीबद्ध करें, नाम, आकार, अंतिम उपयोग

क्या आपने कभी सोचा है कि **जानकारी कैसे दिखाएँ** अपने AsposeAI इंस्टॉलेशन से बिना लॉग या UI देखे? आप अकेले नहीं हैं। कई डेटा‑साइंस पाइपलाइनों में सबसे पहले आपको यह जल्दी से देखना होता है कि कौन से मॉडल आपके मशीन पर हैं, उनका नाम क्या है, उनका आकार कितना है, और आप ने उन्हें आखिरी बार कब छुआ था।

इसी बात को हम कवर करेंगे: एक संक्षिप्त, एंड‑टू‑एंड Python स्निपेट जो **स्थानीय मॉडल सूचीबद्ध करता है**, फिर **मॉडल का नाम दिखाता है**, **मॉडल का आकार दिखाता है**, और **अंतिम उपयोग** टाइमस्टैम्प दिखाता है। कोई बाहरी लाइब्रेरी नहीं, कोई छिपा जादू नहीं—सिर्फ वह AsposeAI क्लाइंट जो आपके पास पहले से है।

इस ट्यूटोरियल के अंत तक आप कोड को किसी भी स्क्रिप्ट में डाल सकते हैं, चलाएँ, और तुरंत अपने स्थानीय रूप से कैश किए गए मॉडलों की एक साफ़ टेबल प्राप्त कर सकते हैं। यह पर्यावरण की सैनीटी‑चेकिंग, हेल्थ डैशबोर्ड बनाने, या सिर्फ डिस्क पर क्या छिपा है, इस जिज्ञासा को संतुष्ट करने के लिए परफेक्ट है।

## Prerequisites

- Python 3.8 या नया (उदाहरण में f‑strings उपयोग किए गए हैं, इसलिए 3.6+ आवश्यक है)
- `asposeai` पैकेज इंस्टॉल किया हुआ (`pip install asposeai`)
- एक वैध AsposeAI लाइसेंस या ट्रायल की (क्लाइंट पर्यावरण वेरिएबल्स या कॉन्फ़िग फ़ाइल से क्रेडेंशियल्स लेगा)

यदि आप इन सभी बिंदुओं को पहले ही चेक कर चुके हैं, तो बढ़िया—आइए शुरू करते हैं।

## Step 1: जानकारी कैसे दिखाएँ – AsposeAI क्लाइंट को इनिशियलाइज़ करें

स्थानीय मॉडल **सूचीबद्ध** करने से पहले, हमें एक क्लाइंट ऑब्जेक्ट चाहिए जो AsposeAI रनटाइम से बात करे। यह कदम बुनियादी है; इसके बिना बाकी कोड `NameError` फेंकेगा।

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Why this matters*: क्लाइंट को इनिशियलाइज़ करने से स्थानीय इनफ़रेंस इंजन के साथ एक सत्र स्थापित होता है, आवश्यक नेटिव लाइब्रेरीज़ लोड होती हैं। यह यह भी वैरिफ़ाई करता है कि आपका लाइसेंस सक्रिय है, जिससे बाद में मॉडल क्वेरी करते समय अस्पष्ट एरर से बचा जा सके।

> **Pro tip**: यदि आप इसे CI सर्वर पर चला रहे हैं, तो `ASPOSEAI_LICENSE` को पर्यावरण में सेट करें ताकि क्लाइंट इंटरैक्टिव प्रॉम्प्ट के बिना शुरू हो सके।

## Step 2: स्थानीय मॉडल सूचीबद्ध करें – उपलब्ध मॉडलों को प्राप्त करें

अब क्लाइंट तैयार है, हम **स्थानीय मॉडल सूचीबद्ध** कर सकते हैं। `list_local()` मेथड ऑब्जेक्ट्स का एक कलेक्शन रिटर्न करता है, जिनमें `name`, `size_mb`, और `last_used` जैसी प्रॉपर्टीज़ होती हैं।

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*What’s happening under the hood*: `list_local()` उस डायरेक्टरी को स्कैन करता है जहाँ AsposeAI मॉडल फ़ाइलें कैश करता है (`~/.asposeai/models` डिफ़ॉल्ट रूप से) और हल्के मेटाडाटा ऑब्जेक्ट बनाता है। यह तेज़ है क्योंकि यह मॉडल वेट्स नहीं लोड करता—सिर्फ एक छोटा JSON मैनिफेस्ट पढ़ता है।

यदि आप कभी यह जानना चाहते हैं कि कोई विशेष मॉडल पहले से कैश है या नहीं, यह कॉल सबसे तेज़ तरीका है।

## Step 3: मॉडल का नाम दिखाएँ, मॉडल का आकार दिखाएँ, और अंतिम उपयोग दिखाएँ

मॉडल हाथ में होने पर, हम अंततः **जानकारी दिखाते** हैं, कलेक्शन पर इटररेट करके प्रत्येक एट्रिब्यूट प्रिंट करते हैं। यही वह जगह है जहाँ हम **मॉडल का नाम दिखाते** हैं, **मॉडल का आकार दिखाते** हैं, और **अंतिम उपयोग** को एक ही साफ़ लाइन में प्रदर्शित करते हैं।

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Expected output** (आपके टाइमस्टैम्प अलग होंगे):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Why we format it this way*: डैश (`–`) फ़ील्ड्स को पढ़ने में आसान बनाता है, और हेडर लाइन कंसोल आउटपुट को स्कैन‑फ्रेंडली बनाती है। यदि बाद में आपको मशीन‑रीडेबल फ़ॉर्मेट चाहिए (CSV, JSON), तो आप आसानी से `print` कॉल को `writer.writerow` या `json.dump` से बदल सकते हैं।

### Handling Edge Cases

- **कोई मॉडल कैश नहीं** – `list_local()` एक खाली लिस्ट रिटर्न करता है। लूप बस स्किप हो जाएगा, और आपको केवल हेडर मिलेगा। आप एक गार्ड जोड़ना चाहेंगे:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **गुम शर्तें** – दुर्लभ मामलों में मैनिफेस्ट करप्ट हो सकता है। `model_info.last_used` एक्सेस करने से `AttributeError` फेंका जा सकता है। यदि आप ऐसी समस्याओं की उम्मीद करते हैं तो प्रिंट को `try/except` में रैप करें।

- **बड़ी मॉडल डायरेक्टरी** – यदि आपके पास सैकड़ों मॉडल हैं, तो आउटपुट को पेजिंग करने या कंसोल पर प्रिंट करने के बजाय फ़ाइल में लिखने पर विचार करें।

## Visual Summary (Optional)

यदि आप एक त्वरित विज़ुअल संकेत पसंद करते हैं, तो नीचे दिया गया आरेख क्लाइंट इनिशियलाइज़ेशन से लेकर अंतिम डिस्प्ले तक का फ्लो दर्शाता है।  

![AsposeAI क्लाइंट से जानकारी कैसे दिखाएँ का आरेख](/images/how-to-display-info.png "जानकारी कैसे दिखाएँ आरेख")

*Alt text*: **how to display info** – AsposeAI क्लाइंट इनिशियलाइज़ेशन, मॉडल लिस्टिंग, और जानकारी डिस्प्ले का स्कीमैटिक।

## Full Working Script

सब कुछ मिलाकर, यहाँ पूरा, तैयार‑टू‑रन स्क्रिप्ट है:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

इसे `list_models.py` के रूप में सेव करें, executable बनाएं (`chmod +x list_models.py`), और चलाएँ:

```bash
./list_models.py
```

आपको पहले दिखाए गए साफ़ लिस्ट दिखाई देगा।

## Conclusion

हमने **जानकारी कैसे दिखाएँ** को **स्थानीय मॉडल सूचीबद्ध** करके, फिर **मॉडल का नाम दिखाकर**, **मॉडल का आकार दिखाकर**, और **अंतिम उपयोग** टाइमस्टैम्प दिखाकर समझाया। यह तरीका हल्का है, केवल मानक `asposeai` पैकेज की आवश्यकता है, और इसे किसी भी ऑटोमेशन पाइपलाइन या डिबगिंग सत्र में डाला जा सकता है।

अब आप आगे कर सकते हैं:

- आउटपुट को CSV में एक्सपोर्ट करके स्प्रेडशीट विश्लेषण करें (`csv` मॉड्यूल)।
- टाइमस्टैम्प को मॉनिटरिंग डैशबोर्ड में फीड करके पुराने मॉडल पर अलर्ट सेट करें।
- इस स्क्रिप्ट को `aspose_ai.download()` के साथ मिलाकर उन मॉडलों को स्वचालित रूप से रिफ्रेश करें जो लंबे समय से उपयोग नहीं हुए हैं।

याद रखें, अपने मॉडल इन्वेंट्री की स्पष्ट दृश्यता समय बचाती है, स्टोरेज ब्लोट कम करती है, और आपके AI सर्विसेज़ को सुचारू रूप से चलाती है। स्क्रिप्ट को चलाएँ, फ़ॉर्मेटिंग को अपनी पसंद के अनुसार बदलें, और इसे अपने टूलबॉक्स में एक मुख्य भाग बनाएं।

Happy coding, and may your models always be fresh!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}