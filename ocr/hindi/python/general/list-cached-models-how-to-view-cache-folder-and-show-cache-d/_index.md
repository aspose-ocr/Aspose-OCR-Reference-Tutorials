---
category: general
date: 2026-02-22
description: जानें कैसे कैश किए गए मॉडल की सूची बनाएं और अपने कंप्यूटर पर कैश डायरेक्टरी
  को जल्दी से दिखाएं। इसमें कैश फ़ोल्डर को देखने और स्थानीय AI मॉडल स्टोरेज को प्रबंधित
  करने के चरण शामिल हैं।
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: hi
og_description: कैश किए गए मॉडल को सूचीबद्ध करना, कैश डायरेक्टरी दिखाना और कैश फ़ोल्डर
  को कुछ आसान चरणों में देखना जानें। पूर्ण पायथन उदाहरण शामिल है।
og_title: कैश्ड मॉडलों की सूची – कैश डायरेक्टरी देखने के लिए त्वरित गाइड
tags:
- AI
- caching
- Python
- development
title: कैश्ड मॉडल सूची – कैश फ़ोल्डर कैसे देखें और कैश डायरेक्टरी दिखाएँ
url: /hi/python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# सूचीबद्ध कैश्ड मॉडल – कैश डायरेक्टरी देखने के लिए त्वरित गाइड

क्या आपने कभी सोचा है कि **list cached models** को अपने वर्कस्टेशन पर बिना अजीब फ़ोल्डरों में खोदे कैसे देखें? आप अकेले नहीं हैं। कई डेवलपर्स को यह पता लगाने में दिक्कत होती है कि कौन‑से AI मॉडल पहले से ही स्थानीय रूप से संग्रहीत हैं, ख़ासकर जब डिस्क स्पेस कम हो। अच्छी खबर? कुछ ही लाइनों के कोड से आप **list cached models** और **show cache directory** दोनों कर सकते हैं, जिससे आपको अपने कैश फ़ोल्डर की पूरी दृश्यता मिलती है।

इस ट्यूटोरियल में हम एक स्व‑निर्भर Python स्क्रिप्ट के माध्यम से यही करेंगे। अंत तक आप जानेंगे कि कैश फ़ोल्डर को कैसे देखें, विभिन्न OS पर कैश कहाँ रहता है, और डाउनलोड किए गए प्रत्येक मॉडल की साफ‑सुथरी सूची कैसे प्रिंट करें। कोई बाहरी डॉक्यूमेंटेशन नहीं, कोई अनुमान नहीं—सिर्फ स्पष्ट कोड और व्याख्याएँ जिन्हें आप अभी कॉपी‑पेस्ट कर सकते हैं।

## What You’ll Learn

- कैसे एक AI क्लाइंट (या स्टब) को इनिशियलाइज़ करें जो कैशिंग यूटिलिटीज़ प्रदान करता है।  
- **list cached models** और **show cache directory** के लिए सटीक कमांड्स।  
- Windows, macOS, और Linux पर कैश कहाँ रहता है, ताकि आप मैन्युअली नेविगेट कर सकें।  
- खाली कैश या कस्टम कैश पाथ जैसी एज केसों को संभालने के टिप्स।  

**Prerequisites** – आपको Python 3.8+ और एक pip‑installable AI क्लाइंट चाहिए जो `list_local()`, `get_local_path()`, और वैकल्पिक रूप से `clear_local()` को इम्प्लीमेंट करता हो। अगर आपके पास अभी तक नहीं है, तो उदाहरण में एक मॉक `YourAIClient` क्लास का उपयोग किया गया है जिसे आप वास्तविक SDK (जैसे `openai`, `huggingface_hub` आदि) से बदल सकते हैं।  

Ready? चलिए शुरू करते हैं।

## Step 1: Set Up the AI Client (or a Mock)

यदि आपके पास पहले से ही क्लाइंट ऑब्जेक्ट है, तो इस ब्लॉक को स्किप करें। अन्यथा, एक छोटा स्टैंड‑इन बनाएं जो कैशिंग इंटरफ़ेस की नकल करता हो। इससे स्क्रिप्ट वास्तविक SDK के बिना भी चल सकेगी।

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **Pro tip:** यदि आपके पास पहले से ही वास्तविक क्लाइंट है (जैसे `from huggingface_hub import HfApi`), तो `YourAIClient()` कॉल को `HfApi()` से बदल दें और सुनिश्चित करें कि `list_local` और `get_local_path` मेथड्स मौजूद हों या उसी अनुसार रैप किए गए हों।

## Step 2: **list cached models** – retrieve and display them

अब क्लाइंट तैयार है, हम इसे स्थानीय रूप से उपलब्ध सभी मॉडल्स की सूची देने के लिए कह सकते हैं। यही हमारा **list cached models** ऑपरेशन है।

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**Expected output** (with the dummy data from step 1):

```
Cached models:
 - model_1
 - model_2
 - model_3
```

यदि कैश खाली है तो आपको यह दिखेगा:

```
Cached models:
```

यह खाली लाइन बताती है कि अभी तक कुछ भी संग्रहीत नहीं है—स्क्रिप्ट‑क्लीन‑अप रूटीन लिखते समय यह उपयोगी है।

## Step 3: **show cache directory** – where does the cache live?

पाथ जानना अक्सर आधा काम होता है। विभिन्न ऑपरेटिंग सिस्टम्स कैश को अलग‑अलग डिफ़ॉल्ट लोकेशन में रखते हैं, और कुछ SDK पर्यावरण वेरिएबल्स के ज़रिए इसे ओवरराइड करने की अनुमति देते हैं। नीचे दिया गया स्निपेट एब्सोल्यूट पाथ प्रिंट करता है ताकि आप `cd` करके या फ़ाइल एक्सप्लोरर में खोल सकें।

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**Typical output** on a Unix‑like system:

```
Cache directory: /home/youruser/.ai_cache
```

Windows पर आपको कुछ इस तरह दिख सकता है:

```
Cache directory: C:\Users\YourUser\.ai_cache
```

अब आप किसी भी प्लेटफ़ॉर्म पर **how to view cache folder** बिल्कुल जानते हैं।

## Step 4: Put It All Together – a single runnable script

नीचे पूरा, तैयार‑से‑चलाने वाला प्रोग्राम है जो तीनों स्टेप्स को जोड़ता है। इसे `view_ai_cache.py` के रूप में सेव करें और `python view_ai_cache.py` चलाएँ।

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

चलाएँ और आपको तुरंत दोनों—कैश्ड मॉडल्स की सूची **और** कैश डायरेक्टरी का लोकेशन—दिखाई देगा।

## Edge Cases & Variations

| Situation | What to Do |
|-----------|------------|
| **Empty cache** | स्क्रिप्ट “Cached models:” प्रिंट करेगी लेकिन कोई एंट्री नहीं होगी। आप एक कंडीशनल वार्निंग जोड़ सकते हैं: `if not models: print("⚠️ No models cached yet.")` |
| **Custom cache path** | क्लाइंट बनाते समय पाथ पास करें: `YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`। `get_local_path()` कॉल उस कस्टम लोकेशन को दर्शाएगा। |
| **Permission errors** | प्रतिबंधित मशीनों पर क्लाइंट `PermissionError` उठा सकता है। इनिशियलाइज़ेशन को `try/except` ब्लॉक में रैप करें और यूज़र‑राइटेबल डायरेक्टरी पर फॉलबैक करें। |
| **Real SDK usage** | `YourAIClient` को वास्तविक क्लाइंट क्लास से बदलें और मेथड नाम मिलते हों यह सुनिश्चित करें। कई SDK सीधे `cache_dir` एट्रिब्यूट प्रदान करते हैं जिसे आप पढ़ सकते हैं। |

## Pro Tips for Managing Your Cache

- **Periodic cleanup:** यदि आप अक्सर बड़े मॉडल डाउनलोड करते हैं, तो एक cron जॉब शेड्यूल करें जो `shutil.rmtree(ai.get_local_path())` को कॉल करे, बशर्ते आप अब उन्हें न चाहते हों।  
- **Disk usage monitoring:** Linux/macOS पर `du -sh $(ai.get_local_path())` या PowerShell में `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum` का उपयोग करके आकार पर नज़र रखें।  
- **Versioned folders:** कुछ क्लाइंट्स मॉडल वर्ज़न के अनुसार सबफ़ोल्डर बनाते हैं। जब आप **list cached models** करेंगे, तो प्रत्येक वर्ज़न अलग एंट्री के रूप में दिखेगा—पुरानी रिवीजन को प्रून करने के लिए इसका उपयोग करें।  

## Visual Overview

![list cached models screenshot](https://example.com/images/list-cached-models.png "list cached models – console output showing models and cache path")

*Alt text:* *list cached models – कंसोल आउटपुट जिसमें कैश्ड मॉडल नाम और कैश डायरेक्टरी पाथ दिखाया गया है।*

## Conclusion

हमने वह सब कवर किया जो आपको **list cached models**, **show cache directory**, और सामान्यतः **how to view cache folder** किसी भी सिस्टम पर करने के लिए चाहिए। यह छोटा स्क्रिप्ट एक पूर्ण, runnable समाधान दिखाता है, प्रत्येक स्टेप के महत्व को समझाता है, और वास्तविक‑दुनिया के उपयोग के लिए प्रैक्टिकल टिप्स देता है।  

अगला कदम आप **कैश को प्रोग्रामेटिकली क्लियर करने** के बारे में देख सकते हैं, या इन कॉल्स को बड़े डिप्लॉयमेंट पाइपलाइन में इंटीग्रेट कर सकते हैं जो इनफ़रेंस जॉब्स शुरू करने से पहले मॉडल उपलब्धता को वैलिडेट करता है। चाहे जो भी हो, अब आपके पास स्थानीय AI मॉडल स्टोरेज को आत्मविश्वास के साथ मैनेज करने की नींव है।

किसी विशेष AI SDK के बारे में सवाल हैं? नीचे कमेंट करें, और हैप्पी कैशिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}