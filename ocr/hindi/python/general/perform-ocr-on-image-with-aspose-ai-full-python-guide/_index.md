---
category: general
date: 2026-06-19
description: Aspose OCR और AI पोस्ट‑प्रोसेसर का उपयोग करके Python में छवि पर OCR कैसे
  करें, सीखें। इसमें ऑटो‑डाउनलोडेड मॉडल, वर्तनी जांच, और GPU त्वरण शामिल हैं।
draft: false
keywords:
- perform OCR on image
- Aspose OCR Python
- AI post‑processor
- auto‑downloaded model
- spellcheck post‑processor
- GPU acceleration
language: hi
og_description: Aspose OCR और AI पोस्ट‑प्रोसेसर का उपयोग करके छवि पर OCR करें। ऑटो‑डाउनलोडेड
  मॉडल, स्पेलचेक और GPU एक्सेलेरेशन के साथ चरण‑दर‑चरण गाइड।
og_title: छवि पर OCR करें – पूर्ण पायथन ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  headline: perform OCR on image with Aspose AI – Full Python Guide
  type: TechArticle
- description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  name: perform OCR on image with Aspose AI – Full Python Guide
  steps:
  - name: Initializes the Aspose OCR engine and loads a sample invoice image.
    text: Initializes the Aspose OCR engine and loads a sample invoice image.
  - name: Runs a basic OCR pass and prints the raw text.
    text: Runs a basic OCR pass and prints the raw text.
  - name: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
    text: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
  - name: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
    text: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
  - name: Releases all resources cleanly.
    text: Releases all resources cleanly.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Aspose AI के साथ छवि पर OCR करें – पूर्ण Python गाइड
url: /hi/python/general/perform-ocr-on-image-with-aspose-ai-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज पर OCR करें – पूर्ण Python ट्यूटोरियल

क्या आपने कभी सोचा है कि **इमेज फ़ाइलों पर OCR कैसे किया जाए** बिना दर्जनों लाइब्रेरीज़ के साथ झंझट किए? मेरे अनुभव में मुख्य समस्या अक्सर कच्चे OCR इंजन को संभालना और फिर शोरयुक्त आउटपुट को साफ़ करना होती है। सौभाग्य से, Aspose OCR for Python अपने AI पोस्ट‑प्रोसेसर के साथ पूरी पाइपलाइन को आसान बना देता है।

इस गाइड में हम एक व्यावहारिक, एंड‑टू‑एंड उदाहरण के माध्यम से दिखाएंगे कि **इमेज डेटा पर OCR कैसे किया जाए**, ऑटो‑डाउनलोडेड मॉडल से सटीकता कैसे बढ़ाई जाए, स्पेल‑चेक कैसे सक्षम किया जाए, और जब उपलब्ध हो तो GPU एक्सेलेरेशन का उपयोग कैसे किया जाए। इस प्रक्रिया को पूरा करने के बाद आपके पास एक पुन: उपयोग योग्य स्क्रिप्ट होगी जिसे आप किसी भी इनवॉइसिंग, रसीद‑स्कैनिंग, या डॉक्यूमेंट‑डिजिटलीज़ेशन प्रोजेक्ट में डाल सकते हैं।

## What You’ll Build

हम एक छोटा Python प्रोग्राम बनाएँगे जो:

1. Aspose OCR इंजन को इनिशियलाइज़ करता है और एक सैंपल इनवॉइस इमेज लोड करता है।  
2. बेसिक OCR चलाता है और रॉ टेक्स्ट प्रिंट करता है।  
3. **Aspose AI** को **ऑटो‑डाउनलोडेड मॉडल** के साथ कॉन्फ़िगर करता है जो Hugging Face से आता है।  
4. **AI पोस्ट‑प्रोसेसर** (जिसमें **स्पेल‑चेक पोस्ट‑प्रोसेसर** भी शामिल है) को चलाकर OCR आउटपुट को साफ़ करता है।  
5. सभी रिसोर्सेज़ को साफ़ तरीके से रिलीज़ करता है।

कोई बाहरी सर्विसेज़ नहीं, कोई API की नहीं—सिर्फ कुछ लाइनों का Python और Aspose की शक्ति।

> **Pro tip:** यदि आपके मशीन में एक उचित GPU है, तो `gpu_layers` सेट करने से पोस्ट‑प्रोसेसिंग स्टेप में सेकंड्स बच सकते हैं।

## Prerequisites

- Python 3.8 या उससे नया (कोड में टाइप हिंट्स हैं लेकिन वैकल्पिक हैं)।  
- `aspose-ocr` और `aspose-ai` पैकेज `pip` के माध्यम से इंस्टॉल किए हुए।  
  ```bash
  pip install aspose-ocr aspose-ai
  ```  
- एक सैंपल इमेज (PNG, JPG, या TIFF) जिसे आप रेफ़रेंस कर सकें, जैसे `sample_invoice.png`।  
- (वैकल्पिक) CUDA‑सक्षम GPU और उपयुक्त ड्राइवर्स यदि आप **GPU एक्सेलेरेशन** चाहते हैं।

अब जब बुनियादी सेटअप तैयार है, चलिए कोड में डुबकी लगाते हैं।

![इमेज पर OCR करने का उदाहरण](image.png)

## perform OCR on image – Step 1: Initialise the OCR engine and load the image

सबसे पहले हमें एक OCR इंजन इंस्टेंस चाहिए। Aspose OCR एक साफ़, ऑब्जेक्ट‑ओरिएंटेड API प्रदान करता है जो लो‑लेवल इमेज प्री‑प्रोसेसिंग को एब्स्ट्रैक्ट करता है।

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()
ocr_engine.Language = "en"                     # English; change as needed

# Load the image you want to analyse
ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")
```

**यह क्यों महत्वपूर्ण है:**  
भाषा को पहले सेट करने से इंजन को पता चलता है कि किस कैरेक्टर सेट की उम्मीद करनी है, जिससे पहचान की गति और सटीकता दोनों में सुधार हो सकता है। यदि आप बहुभाषी दस्तावेज़ों से निपट रहे हैं, तो `"en"` को `"fr"` या `"de"` में बदल दें।

## Step 2: Perform basic OCR and view the raw text

अब हम वास्तव में पहचान चलाते हैं। रिज़ल्ट ऑब्जेक्ट में रॉ टेक्स्ट, कॉन्फिडेंस स्कोर, और यदि आवश्यक हो तो बाउंडिंग बॉक्स भी होते हैं।

```python
# Run OCR
ocr_result = ocr_engine.Recognize()

# Show the unprocessed output
print("Raw OCR output:")
print(ocr_result.Text)
```

आम तौर पर आउटपुट कुछ इस तरह दिख सकता है (ध्यान दें कभी‑कभी गलत पढ़े गए कैरेक्टर्स):

```
Raw OCR output:
Inv0ice N0: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00
```

आप देख सकते हैं कि जहाँ इंजन ने “O” देखा, वहाँ `0` (ज़ीरो) आया है। यही वह जगह है जहाँ **AI पोस्ट‑प्रोसेसर** चमकता है।

## Configure Aspose AI – auto‑downloaded model and spellcheck

रॉ OCR परिणाम को AI लेयर में भेजने से पहले, हमें Aspose AI को बताना होगा कि कौन सा मॉडल उपयोग करना है। लाइब्रेरी स्वचालित रूप से Hugging Face से मॉडल डाउनलोड कर सकती है, इसलिए आपको बड़े `.bin` फ़ाइलों से जूझना नहीं पड़ेगा।

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

# Create a model configuration that auto‑downloads the Qwen2.5‑3B‑Instruct model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"   # reduces RAM usage
model_config.gpu_layers = 20                      # use GPU if available

# Initialise the AI engine with the config
ai_engine = AsposeAI(model_config)

# Enable the built‑in spellcheck post‑processor
ai_engine.set_post_processor("spellcheck", None)
```

**सेटिंग्स की व्याख्या**

| Setting | What it does | When to adjust |
|---------|--------------|----------------|
| `allow_auto_download` | पहली बार रन पर Aspose को मॉडल ऑटोमैटिकली फ़ेच करने देता है। | ऑफ़लाइन उपयोग के लिए पहले से डाउनलोड न करने पर `true` रखें। |
| `hugging_face_repo_id` | Hugging Face पर मॉडल की पहचानकर्ता। | यदि आपको डोमेन‑स्पेसिफिक मॉडल चाहिए तो इसे बदलें। |
| `hugging_face_quantization` | क्वांटाइज़ेशन लेवल चुनता है (`int8`, `float16`, आदि)। | कम मेमोरी वाले वातावरण में `int8` उपयोग करें; उच्च सटीकता के लिए `float16`। |
| `gpu_layers` | GPU पर चलने वाले ट्रांसफ़ॉर्मर लेयर्स की संख्या। | CPU‑केवल के लिए `0` रखें, या मॉडल की कुल लेयर्स (जैसे Qwen2.5‑3B के लिए 20) तक कोई भी वैल्यू सेट करें। |

## Run the AI post‑processor on the OCR result

इंजन तैयार होने पर, हम बस रॉ OCR आउटपुट को AI पाइपलाइन में फीड करते हैं। बिल्ट‑इन **स्पेल‑चेक पोस्ट‑प्रोसेसर** स्पष्ट टाइपो को ठीक करेगा, जबकि भाषा मॉडल आगे री‑फ़्रेज़ या मिसिंग जानकारी भर सकता है यदि आप बाद में अतिरिक्त प्रोसेसर सक्षम करते हैं।

```python
# Enhance the OCR result using the AI post‑processor
enhanced_result = ai_engine.run_postprocessor(ocr_result)

# Display the cleaned‑up text
print("\nAI‑enhanced OCR output:")
print(enhanced_result.Text)
```

स्पेल‑चेक स्टेप के बाद अपेक्षित आउटपुट:

```
AI‑enhanced OCR output:
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

ध्यान दें कि ज़ीरो को सही अक्षरों में बदल दिया गया है, और गलत लिखा “Am0unt” अब “Amount” हो गया है। **AI पोस्ट‑प्रोसेसर** रॉ टेक्स्ट को चयनित मॉडल के माध्यम से भेजता है, जो अपने प्रशिक्षण के आधार पर एक परिष्कृत संस्करण लौटाता है।

### Edge Cases & Tips

- **Low‑resolution images**: यदि OCR इंजन संघर्ष करता है, तो पहले इमेज को अप‑स्केल करने पर विचार करें (`Pillow` मदद कर सकता है) या `ocr_engine.ImagePreprocessingOptions` बढ़ाएँ।  
- **Non‑Latin scripts**: `ocr_engine.Language` को उपयुक्त ISO कोड में बदलें (`"zh"` चीनी के लिए, `"ar"` अरबी के लिए)।  
- **GPU not detected**: `gpu_layers` सेटिंग स्वचालित रूप से CPU पर फ़ॉल्बैक हो जाती है यदि कोई संगत GPU नहीं मिलता, इसलिए अतिरिक्त एरर हैंडलिंग की ज़रूरत नहीं।  
- **Model size limits**: Qwen2.5‑3B मॉडल लगभग 4 GB कंप्रेस्ड है; ऑटो‑डाउनलोड के लिए सुनिश्चित करें कि डिस्क में पर्याप्त जगह हो।

## Release resources – clean shutdown

Aspose ऑब्जेक्ट्स में नेटिव हैंडल्स होते हैं, इसलिए काम खत्म होने पर उन्हें फ्री करना अच्छा अभ्यास है। यह विशेषकर लम्बे‑चलने वाले सर्विसेज़ में मेमोरी लीक को रोकता है।

```python
# Free AI resources
ai_engine.free_resources()

# Dispose of the OCR engine
ocr_engine.Dispose()
```

यदि आप स्पष्ट क्लीन‑अप चाहते हैं तो पूरे स्क्रिप्ट को `try…finally` ब्लॉक में रैप कर सकते हैं।

## Full Script – copy‑paste ready

नीचे पूरा प्रोग्राम दिया गया है, जिसे आप `YOUR_DIRECTORY` को अपनी इमेज के पाथ से बदलने के बाद चला सकते हैं।

```python
# -*- coding: utf-8 -*-
"""
Full example: perform OCR on image using Aspose OCR + AI post‑processor.
Author: Your Name
Date: 2026‑06‑19
"""

from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.Language = "en"
    ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Basic OCR
    ocr_result = ocr_engine.Recognize()
    print("Raw OCR output:")
    print(ocr_result.Text)

    # 3️⃣ Configure Aspose AI with auto‑downloaded model
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "int8"
    model_cfg.gpu_layers = 20   # GPU acceleration if available

    ai_engine = AsposeAI(model_cfg)
    ai_engine.set_post_processor("spellcheck", None)   # enable spellcheck

    # 4️⃣ AI post‑processing
    enhanced = ai_engine.run_postprocessor(ocr_result)
    print("\nAI‑enhanced OCR output:")
    print(enhanced.Text)

    # 5️⃣ Clean up
    ai_engine.free_resources()
    ocr_engine.Dispose()

if __name__ == "__main__":
    main()
```

इसे इस तरह चलाएँ:

```bash
python perform_ocr_on_image.py
```

आपको कंसोल में रॉ और क्लीन्ड दोनों आउटपुट प्रिंट होते दिखेंगे।

## Conclusion


## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का पता लगा सकें।

- [Aspose OCR के साथ इमेज से टेक्स्ट निकालें – चरण‑दर‑चरण गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose.OCR का उपयोग करके भाषा चयन के साथ C# में इमेज टेक्स्ट निकालें](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [इमेज को टेक्स्ट में बदलें – URL से इमेज पर OCR करें](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}