---
category: general
date: 2026-04-26
description: AsposeAI OCR पोस्ट‑प्रोसेसिंग का उपयोग करके क्रेडिट कार्ड नंबरों को जल्दी
  से मास्क करें। PCI अनुपालन, रेगुलर एक्सप्रेशन मास्किंग और डेटा सैनिटाइज़ेशन को चरण‑दर‑चरण
  ट्यूटोरियल में सीखें।
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: hi
og_description: AsposeAI के साथ OCR परिणामों में क्रेडिट कार्ड नंबरों को मास्क करें।
  यह ट्यूटोरियल PCI अनुपालन, रेगुलर एक्सप्रेशन मास्किंग और डेटा सैनिटाइज़ेशन को कवर
  करता है।
og_title: क्रेडिट कार्ड नंबरों को मास्क करें – पूर्ण पायथन OCR पोस्ट‑प्रोसेसिंग गाइड
tags:
- OCR
- Python
- security
title: OCR आउटपुट में क्रेडिट कार्ड नंबरों को मास्क करें – पूर्ण पायथन गाइड
url: /hi/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# क्रेडिट कार्ड नंबरों को मास्क करें – पूर्ण Python गाइड

क्या आपको कभी OCR इंजन से सीधे प्राप्त टेक्स्ट में **क्रेडिट कार्ड नंबरों को मास्क करने** की ज़रूरत पड़ी है? आप अकेले नहीं हैं। नियामक उद्योगों में, पूर्ण PAN (Primary Account Number) को उजागर करना PCI अनुपालन ऑडिटरों के साथ बड़ी समस्या बन सकता है। अच्छी खबर यह है कि कुछ ही पंक्तियों के Python कोड और AsposeAI के पोस्ट‑प्रोसेसिंग हुक के साथ, आप मध्य के आठ अंकों को स्वचालित रूप से छिपा सकते हैं और सुरक्षित रह सकते हैं।

इस ट्यूटोरियल में हम एक वास्तविक परिदृश्य पर चलेंगे: रसीद की छवि पर OCR चलाना, फिर एक कस्टम **OCR पोस्ट‑प्रोसेसिंग** फ़ंक्शन लागू करना जो किसी भी PCI डेटा को साफ़ करता है। अंत तक आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जिसे आप किसी भी AsposeAI वर्कफ़्लो में जोड़ सकते हैं, साथ ही किनारे के मामलों को संभालने और समाधान को स्केल करने के लिए कुछ व्यावहारिक टिप्स भी।

## आप क्या सीखेंगे

- **AsposeAI** के साथ एक कस्टम पोस्ट‑प्रोसेसर कैसे रजिस्टर करें।
- क्यों **रेगुलर एक्सप्रेशन मास्किंग** तरीका तेज़ और भरोसेमंद है।
- डेटा सैनिटाइज़ेशन से संबंधित **PCI अनुपालन** की बुनियादी बातें।
- कई कार्ड फ़ॉर्मेट या अंतरराष्ट्रीय नंबरों के लिए पैटर्न को कैसे विस्तारित करें।
- अपेक्षित आउटपुट और यह कैसे सत्यापित करें कि मास्किंग काम कर रहा है।

> **Prerequisites** – आपके पास एक कार्यशील Python 3 वातावरण, Aspose.AI for OCR पैकेज इंस्टॉल (`pip install aspose-ocr`), और एक सैंपल इमेज (जैसे `receipt.png`) होनी चाहिए जिसमें क्रेडिट‑कार्ड नंबर हो। अन्य कोई बाहरी सेवा आवश्यक नहीं है।

---

## Step 1: Define a Post‑Processor that Masks Credit Card Numbers

समाधान का दिल एक छोटे फ़ंक्शन में रहता है जो OCR परिणाम प्राप्त करता है, **रेगुलर एक्सप्रेशन मास्किंग** रूटीन चलाता है, और साफ़ किया हुआ टेक्स्ट लौटाता है।

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Why this works:**  
- रेगुलर एक्सप्रेशन `(\d{4})\d{8}(\d{4})` ठीक 16 लगातार अंकों से मेल खाता है, जो Visa, MasterCard और कई अन्य कार्डों का सामान्य फ़ॉर्मेट है।  
- पहले और आखिरी चार अंकों (`\1` और `\2`) को कैप्चर करके हम डिबगिंग के लिए पर्याप्त जानकारी रखते हैं, जबकि **PCI compliance** नियमों का पालन करते हैं जो पूर्ण PAN को स्टोर करने से रोकते हैं।  
- प्रतिस्थापन `\1****\2` संवेदनशील मध्य के आठ अंकों को छिपा देता है, जिससे `1234567812345678` → `1234****5678` बन जाता है।

> **Pro tip:** यदि आपको 15‑अंकीय American Express नंबरों का समर्थन चाहिए, तो एक दूसरा पैटर्न जैसे `r'(\d{4})\d{6}(\d{5})'` जोड़ें और दोनों रिप्लेसमेंट क्रमिक रूप से चलाएँ।

---

## Step 2: Initialise the AsposeAI Engine

पोस्ट‑प्रोसेसर को अटैच करने से पहले हमें OCR इंजन का एक इंस्टेंस चाहिए। AsposeAI OCR मॉडल और कस्टम प्रोसेसिंग के लिए एक सरल API बंडल करता है।

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Why initialise here?**  
`AsposeAI` ऑब्जेक्ट को एक बार बनाकर कई छवियों में पुन: उपयोग करने से ओवरहेड कम होता है। इंजन भाषा मॉडल को कैश भी करता है, जिससे बाद के कॉल तेज़ होते हैं—जब आप रसीदों के बैच को स्कैन कर रहे हों तो यह उपयोगी है।

---

## Step 3: Register the Custom Masking Function

AsposeAI एक `set_post_processor` मेथड प्रदान करता है जो आपको कोई भी कॉलेबल प्लग‑इन करने देता है। हम अपना `mask_pci` फ़ंक्शन एक वैकल्पिक सेटिंग्स डिक्शनरी (अभी खाली) के साथ पास करते हैं।

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**What’s happening behind the scenes?**  
जब आप बाद में `run_postprocessor` को कॉल करेंगे, AsposeAI कच्चे OCR परिणाम को `mask_pci` को देगा। फ़ंक्शन एक हल्के ऑब्जेक्ट (`data`) प्राप्त करता है जिसमें पहचाना गया टेक्स्ट होता है, और आप एक नया स्ट्रिंग लौटाते हैं। यह डिज़ाइन कोर OCR को अपरिवर्तित रखता है जबकि आपको **डेटा सैनिटाइज़ेशन** नीतियों को एक ही जगह लागू करने देता है।

---

## Step 4: Run OCR on the Receipt Image

अब जब इंजन को आउटपुट साफ़ करने का तरीका पता है, हम उसे एक इमेज देते हैं। इस ट्यूटोरियल के लिए मान लेते हैं कि आपके पास पहले से ही सही भाषा और रिज़ॉल्यूशन सेटिंग्स वाला `engine` ऑब्जेक्ट कॉन्फ़िगर है।

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Tip:** यदि आपके पास प्री‑कॉन्फ़िगर्ड ऑब्जेक्ट नहीं है, तो आप इसे इस तरह बना सकते हैं:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

`recognize_image` कॉल एक ऑब्जेक्ट लौटाता है जिसका `text` एट्रिब्यूट कच्चा, अनमास्क्ड स्ट्रिंग रखता है।

---

## Step 5: Apply the Registered Post‑Processor

कच्चा OCR डेटा हाथ में होने पर, हम उसे AI इंस्टेंस को देते हैं। इंजन स्वचालित रूप से पहले रजिस्टर किए गए `mask_pci` फ़ंक्शन को चलाता है।

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Why use `run_postprocessor` instead of calling the function manually?**  
यह वर्कफ़्लो को सुसंगत रखता है, विशेषकर जब आपके पास कई पोस्ट‑प्रोसेसर (जैसे स्पेल‑चेकिंग, लैंग्वेज डिटेक्शन) हों। AsposeAI उन्हें रजिस्टर किए क्रम में कतारबद्ध करता है, जिससे आउटपुट डिटरमिनिस्टिक रहता है।

---

## Step 6: Verify the Sanitized Output

आख़िर में, साफ़ किया हुआ टेक्स्ट प्रिंट करें और पुष्टि करें कि सभी क्रेडिट‑कार्ड नंबर सही ढंग से मास्क हो गए हैं।

```python
print(final_result.text)
```

**Expected output** (excerpt):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

यदि रसीद में कोई कार्ड नंबर नहीं था, तो टेक्स्ट अपरिवर्तित रहता है—मास्क करने को कुछ नहीं, चिंता करने को कुछ नहीं।

---

## Handling Edge Cases and Common Variations

### Multiple Card Numbers in One Document
यदि रसीद में एक से अधिक PAN (जैसे लॉयल्टी कार्ड + पेमेंट कार्ड) हों, तो रेगुलर एक्सप्रेशन ग्लोबली चलता है और सभी मैचों को स्वचालित रूप से मास्क करता है। अतिरिक्त कोड की आवश्यकता नहीं।

### Non‑Standard Formatting
कभी‑कभी OCR स्पेस या डैश डाल देता है (`1234 5678 1234 5678` या `1234-5678-1234-5678`)। इन कैरेक्टर्स को अनदेखा करने के लिए पैटर्न को विस्तारित करें:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

जोड़ा गया `[ -]?` वैकल्पिक स्पेस या हाइफ़न को डिटेक्ट करता है।

### International Cards
कुछ क्षेत्रों में 19‑अंकीय PAN उपयोग होते हैं; आप पैटर्न को इस तरह विस्तृत कर सकते हैं:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

सिर्फ यह याद रखें कि **PCI compliance** अभी भी मध्य के अंकों को मास्क करने की मांग करता है, चाहे लंबाई कुछ भी हो।

### Logging Masked Values (Optional)
यदि आपको ऑडिट ट्रेल चाहिए, तो `custom_settings` के माध्यम से एक फ़्लैग पास करें और फ़ंक्शन को समायोजित करें:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

फिर इस तरह रजिस्टर करें:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Full Working Example (Copy‑Paste Ready)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

इस स्क्रिप्ट को `4111111111111111` वाले रसीद पर चलाने पर परिणाम होगा:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

यही पूरा पाइपलाइन है—कच्चे OCR से **डेटा सैनिटाइज़ेशन** तक—कुछ साफ़ Python लाइनों में बँधा हुआ।

---

## Conclusion

हमने दिखाया कि कैसे AsposeAI के पोस्ट‑प्रोसेसिंग हुक, एक संक्षिप्त रेगुलर‑एक्सप्रेशन रूटीन, और कुछ सर्वोत्तम‑प्रैक्टिस टिप्स का उपयोग करके OCR परिणामों में **क्रेडिट कार्ड नंबरों को मास्क** किया जा सकता है। समाधान पूरी तरह से स्व-निहित है, किसी भी इमेज के साथ काम करता है जिसे OCR पढ़ सकता है, और अधिक जटिल कार्ड फ़ॉर्मेट या लॉगिंग आवश्यकताओं को कवर करने के लिए विस्तारित किया जा सकता है।

अगला कदम? इस मास्क को एक **डेटाबेस इन्सर्शन** रूटीन के साथ जोड़ें जो केवल आखिरी चार अंक ही स्टोर करे, या एक **बैच प्रोसेसर** बनाएं जो रात भर पूरी फ़ोल्डर की रसीदें स्कैन करे। आप अन्य **OCR पोस्ट‑प्रोसेसिंग** कार्यों जैसे पता मानकीकरण या भाषा पहचान को भी एक्सप्लोर कर सकते हैं—हर एक यहाँ दिखाए गए पैटर्न का पालन करता है।

यदि आपके पास किनारे के मामलों, प्रदर्शन, या कोड को किसी अन्य OCR लाइब्रेरी के लिए अनुकूलित करने के बारे में प्रश्न हैं, तो नीचे टिप्पणी करें, और बातचीत जारी रखें। Happy coding, and stay secure!

![क्रेडिट कार्ड नंबरों को मास्क करने के OCR पाइपलाइन में कैसे काम करता है का चित्रण](https://example.com/images/ocr-mask-flow.png "OCR पोस्ट‑प्रोसेसिंग मास्किंग फ्लो का चित्र")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}