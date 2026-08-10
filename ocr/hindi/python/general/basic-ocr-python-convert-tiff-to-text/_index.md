---
category: general
date: 2026-03-18
description: बेसिक OCR पायथन ट्यूटोरियल दिखाता है कि कैसे TIFF को टेक्स्ट में बदलें,
  इमेज OCR लोड करें, GPU लेयर्स सेट करें, और Aspose AI के साथ लीडिंग ज़ीरो को ठीक
  करें।
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: hi
og_description: बेसिक OCR पायथन ट्यूटोरियल आपको TIFF फ़ाइलों को साफ़ टेक्स्ट में बदलने,
  इमेज लोड करने, GPU लेयर्स सेट करने और लीडिंग ज़ीरो को ठीक करने के माध्यम से ले जाता
  है।
og_title: बेसिक ओसीआर पायथन – TIFF को टेक्स्ट में बदलें
tags:
- OCR
- Python
- AI
- Aspose
title: बेसिक OCR पायथन – TIFF को टेक्स्ट में बदलें
url: /hi/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – TIFF को टेक्स्ट में बदलें AI पोस्ट‑प्रोसेसिंग के साथ

क्या आप अपने स्कैन किए गए दस्तावेज़ों पर **basic ocr python** करने का तरीका ढूँढ़ रहे हैं? इस गाइड में हम Aspose OCR और एक AI पोस्ट‑प्रोसेसर का उपयोग करके TIFF फ़ाइल को साफ़, खोज योग्य टेक्स्ट में बदलने की प्रक्रिया दिखाएंगे।  

यदि आप कभी **convert TIFF to text** करने में कठिनाई महसूस कर चुके हैं क्योंकि कच्चा आउटपुट टाइपो या अजीब प्रतीकों से भरा होता है, तो आप अकेले नहीं हैं। हम आपको यह भी दिखाएंगे कि कैसे **load image OCR** किया जाए, इंजन को **set GPU layers** के लिए समायोजित किया जाए, और यहाँ तक कि इनवॉइस नंबरों में अक्सर दिखाई देने वाले **fix leading zeroes** को कैसे ठीक किया जाए।  

## आप क्या सीखेंगे

- प्रिंटेड दस्तावेज़ों के लिए Aspose OCR इंजन को प्रारंभ करने का तरीका।  
- TIFF फ़ाइल से **load image OCR** करने और कच्चा टेक्स्ट प्राप्त करने के सटीक चरण।  
- AI मॉडल को कॉन्फ़िगर करना, उसे स्वचालित रूप से डाउनलोड करना, और तेज़ इन्फ़रेंस के लिए **setting GPU layers**।  
- बिल्ट‑इन स्पेल‑चेक जोड़ना और एक कस्टम फ़ंक्शन जो **fixes leading zeroes**।  
- OCR परिणाम को साफ़ करना और संसाधनों को सही ढंग से रिलीज़ करना।  

इस ट्यूटोरियल के अंत तक आपके पास एक एकल, पुन: उपयोग योग्य Python स्क्रिप्ट होगी जो किसी भी TIFF को परिष्कृत, खोज योग्य टेक्स्ट में बदल देती है—बिना मैन्युअल कॉपी‑पेस्टिंग के।  

### आवश्यकताएँ

- आपके मशीन पर Python 3.8+ स्थापित हो।  
- `aspose-ocr` पैकेज (`pip install aspose-ocr`)।  
- वैकल्पिक: कम से कम 4 GB VRAM वाला GPU यदि आप **set GPU layers** चाहते हैं; अन्यथा कोड स्वचालित रूप से CPU पर वापस जाता है।  

---

## basic ocr python – इमेज लोड करें और टेक्स्ट पहचानें

सबसे पहले हमें **load image OCR** करना है ताकि इंजन पिक्सेल पढ़ सके। Aspose का `OcrEngine` कई फ़ॉर्मेट संभालता है, लेकिन यहाँ हम TIFF पर ध्यान दे रहे हैं क्योंकि यह स्कैन किए गए इनवॉइस के लिए सबसे आम है।

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro tip:** यदि आप मल्टी‑पेज TIFFs से निपट रहे हैं, तो Aspose प्रत्येक पेज को क्रम में स्वचालित रूप से प्रोसेस करता है, इसलिए आपको अतिरिक्त लूप की आवश्यकता नहीं है।

अब जब इमेज लोड हो गई है, चलिए एक बेसिक रिकग्निशन पास चलाते हैं।

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

आपको कुछ इस तरह दिखेगा:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

अक्षरों से पहले के *zeroes* पर ध्यान दें? यह एक क्लासिक OCR आर्टिफैक्ट है जिसे हम बाद में साफ़ करेंगे।

![basic ocr python workflow](/images/ocr-workflow.png "basic ocr python workflow diagram")

---

## चरण 2: TIFF को टेक्स्ट में बदलें – AI पोस्ट‑प्रोसेसर तैयार करें

कच्चा OCR उपयोगी है, लेकिन अधिकांश प्रोडक्शन पाइपलाइन को एक परिष्कृत संस्करण चाहिए। Aspose एक `AsposeAI` रैपर प्रदान करता है जो Hugging Face से मॉडल डाउनलोड कर सकता है, GPU पर चलाता है, और स्वचालित रूप से स्पेल‑चेक लागू करता है।

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### क्यों `set GPU layers` महत्वपूर्ण है

`gpu_layers` पैरामीटर अंतर्निहित GGUF मॉडल को बताता है कि GPU पर कितनी ट्रांसफ़ॉर्मर लेयर्स रखनी हैं। अधिक लेयर्स = तेज़ इन्फ़रेंस लेकिन अधिक VRAM उपयोग। यदि आप एक साधारण लैपटॉप पर हैं, तो मान को `10` तक घटा दें या पूरी तरह से छोड़ दें ताकि CPU पर रह सकें।

---

## चरण 3: स्पेलचेक लागू करें और **fix leading zeroes**

Aspose AI में एक बिल्ट‑इन स्पेल‑चेकर शामिल है, जो अधिकांश अंग्रेज़ी गलतियों को पकड़ता है। हालांकि, डोमेन‑विशिष्ट सुधार—जैसे इनवॉइस कोड में अग्रणी `0` को `O` में बदलना—के लिए एक कस्टम पोस्ट‑प्रोसेसर की आवश्यकता होती है।

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Why this works:** रेगुलर एक्सप्रेशन शब्द सीमा (`\b`), एक शून्य, फिर ठीक तीन बड़े अक्षर खोजता है। फिर यह शून्य को अक्षर “O” से बदल देता है। आप अन्य विचित्रताओं के लिए पैटर्न को विस्तारित कर सकते हैं (उदा., `0[0-9]{2}` गलत पढ़े गए नंबरों के लिए)।

---

## चरण 4: AI पोस्ट‑प्रोसेसर के साथ OCR परिणाम को साफ़ करें

अब हम सब कुछ मिलाते हैं: **basic ocr python** से प्राप्त कच्चा स्ट्रिंग, स्पेल‑चेक, और हमारा zero‑fix। `run_postprocessor` मेथड एक साफ़ संस्करण लौटाता है जो डाउनस्ट्रीम सिस्टम के लिए तैयार है।

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

पोस्ट‑प्रोसेसर के बाद का सामान्य आउटपुट:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

आप देख सकते हैं कि अग्रणी शून्य `O` में बदल गया है, और सामान्य गलतियों को सुधारा गया है। अब टेक्स्ट सर्च इंजन में इंडेक्सिंग या डेटा‑एक्सट्रैक्शन पाइपलाइन में फीड करने के लिए उपयुक्त है।

---

## चरण 5: AI संसाधनों को रिलीज़ करें – अपने GPU को खुश रखें

यदि आप एक लंबे‑चलने वाले सर्विस में कई OCR जॉब्स चला रहे हैं, तो काम समाप्त होने पर मॉडल की GPU मेमोरी को मुक्त करना अच्छा अभ्यास है।

```python
ocr_ai.free_resources()
```

इस चरण को छोड़ने से बाद के कॉल्स में “out‑of‑memory” त्रुटियाँ आ सकती हैं, विशेष रूप से जब **set GPU layers** को उच्च मान पर सेट किया गया हो।

---

## वैकल्पिक विविधताएँ और किनारे के केस

| स्थिति | क्या बदलें |
|-----------|----------------|
| **हस्तलिखित दस्तावेज़** | `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` का उपयोग करें `PRINTED` के बजाय। |
| **GPU उपलब्ध नहीं** | `gpu_layers=0` सेट करें या आर्ग्यूमेंट को छोड़ दें; मॉडल CPU पर चलेगा (धीमा लेकिन सुरक्षित)। |
| **विभिन्न भाषा** | Hugging Face रेपो ID को एक भाषा‑विशिष्ट मॉडल से बदलें, उदाहरण के लिए `microsoft/Florence-2-base`। |
| **बैच प्रोसेसिंग** | स्टेप्स को `for file in glob("*.tif"):` लूप में रैप करें और परिणामों को सूची या CSV में इकट्ठा करें। |
| **और जटिल शून्य पैटर्न** | `invoice_fix` को अतिरिक्त रेगेक्स के साथ विस्तारित करें, जैसे `r"\b0+([A-Z]{2,})\b"` कई अग्रणी शून्य के लिए। |

---

## निष्कर्ष

हमने अभी-अभी एक **basic ocr python** पाइपलाइन पूरी की है जो TIFF को लोड करती है, कच्चा टेक्स्ट निकालती है, और फिर प्रदर्शन के लिए **setting GPU layers** के साथ AI मॉडल का उपयोग करके इसे साफ़ करती है। कस्टम पोस्ट‑प्रोसेसर दिखाता है कि कैसे **fix leading zeroes** किया जाए, एक छोटा लेकिन अक्सर अनदेखा किया गया विवरण जो डाउनस्ट्रीम एनालिटिक्स को बिगाड़ सकता है।  

बिना झिझक प्रयोग करें: अलग क्वांटाइज़ेशन (`float16` उच्च सटीकता के लिए) आज़माएँ, स्पेल‑चेक को डोमेन‑विशिष्ट शब्दकोश से बदलें, या कई कस्टम फिक्स को एक साथ जोड़ें। पैटर्न वही रहता है—लोड करें, पहचानें, AI कॉन्फ़िगर करें, पोस्ट‑प्रोसेस करें, और साफ़ करें।  

**अगले कदम** जिन पर आप विचार कर सकते हैं:

- साफ़ आउटपुट को डेटाबेस या Elasticsearch इंडेक्स के साथ इंटीग्रेट करना।  
- मल्टी‑लैंग्वेज PDFs के लिए **convert TIFF to text** करने के लिए वही तरीका उपयोग करना।  
- Flask या FastAPI के साथ एक UI जोड़ना ताकि गैर‑तकनीकी उपयोगकर्ता फ़ाइलें अपलोड कर सकें और तुरंत साफ़ टेक्स्ट प्राप्त कर सकें।  

कोडिंग का आनंद लें, और आपके OCR परिणाम हमेशा स्पष्ट और शून्य‑मुक्त रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}