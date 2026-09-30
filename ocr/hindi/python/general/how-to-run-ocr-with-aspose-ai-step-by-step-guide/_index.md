---
category: general
date: 2026-02-09
description: Aspose AI और Hugging Face मॉडल का उपयोग करके OCR कैसे चलाएँ – Hugging
  Face मॉडल डाउनलोड करना सीखें, OCR त्रुटियों को सुधारें और GPU मेमोरी मुक्त करें।
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: hi
og_description: Aspose AI के साथ OCR चलाने की विधि पहले पैराग्राफ में समझाई गई है
  – जानिए कैसे Hugging Face मॉडल डाउनलोड करें, OCR त्रुटियों को सुधारें और GPU मेमोरी
  मुक्त करें।
og_title: Aspose AI के साथ OCR कैसे चलाएँ – पूर्ण मार्गदर्शिका
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: Aspose AI के साथ OCR कैसे चलाएँ – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

to preserve markdown formatting exactly.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose AI के साथ OCR चलाने का तरीका – पूर्ण गाइड

क्या आपने कभी **OCR कैसे चलाएँ** स्कैन किए गए इनवॉइस पर और बिना टाइपो सुधारने में घंटों खर्च किए साफ़ नंबर प्राप्त करने के बारे में सोचा है? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में क्लासिक OCR इंजन से निकला कच्चा टेक्स्ट अभी भी अनचाहे अक्षर, टूटे हुए मुद्रा प्रतीक, या गड़बड़ अंकों को रखता है—विशेषकर जब स्रोत छवि शोरयुक्त हो।  

अच्छी खबर यह है कि आप एक LLM को Aspose OCR से जोड़ सकते हैं, Hugging Face मॉडल को ऑन‑द‑फ़्लाई डाउनलोड कर सकते हैं, और AI को आउटपुट को आपके लिए पॉलिश करने दे सकते हैं। इस ट्यूटोरियल में हम पूरे पाइपलाइन को कवर करेंगे, मॉडल को पुल करने से (हाँ, हम आपको दिखाएंगे कि **download hugging face model** कैसे स्वचालित रूप से किया जाता है) लेकर GPU संसाधनों को मुक्त करने तक जब आप काम समाप्त कर लें। अंत तक आपके पास एक पुनरुत्पादक स्क्रिप्ट होगी जो **corrects OCR errors** करती है, मध्यम GPU पर तेज़ चलती है, और खुद को साफ़ करती है ताकि आप मेमोरी बर्बाद न करें।

## आप क्या सीखेंगे

- Aspose AI को कॉन्फ़िगर करें ताकि वह Hugging Face से **Qwen2.5‑3B‑Instruct‑GGUF** मॉडल को फ़ेच कर सके।
- एक इमेज फ़ाइल पर मानक Aspose OCR इंजन चलाएँ।
- एक कस्टम LLM प्रॉम्प्ट उपयोग करें जो नंबर और मुद्रा प्रतीकों को अपरिवर्तित रखे।
- बिल्ट‑इन **free gpu memory** रूटीन के साथ GPU मेमोरी रिलीज़ करें।
- मल्टी‑पेज PDFs या लो‑एंड GPUs जैसे एज केसों के लिए वर्कफ़्लो को ट्यून करें।

> **Prerequisites** – Python 3.9+, `aspose-ocr` पैकेज, पहली बार मॉडल डाउनलोड के लिए इंटरनेट एक्सेस, और कम से कम 4 GB VRAM वाला GPU (वैकल्पिक लेकिन अनुशंसित)। यदि आपके पास GPU नहीं है, तो स्क्रिप्ट शेष लेयर्स के लिए स्वचालित रूप से CPU पर फ़ॉल बैक हो जाएगी।

---

## OCR कैसे चलाएँ और परिणाम सुधारें

नीचे पूर्ण, तैयार‑चलाने योग्य Python स्क्रिप्ट दी गई है। इसे `ocr_with_ai.py` के रूप में सेव करें और प्लेसहोल्डर पाथ्स को अपनी फ़ाइलों से बदलें।

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Pro tip:** `gpu_layers` पैरामीटर आपको यह तय करने देता है कि कितनी ट्रांसफ़ॉर्मर लेयर्स GPU पर रहेंगी। यदि आप आउट‑ऑफ़‑मेमोरी त्रुटियों का सामना कर रहे हैं, तो इस संख्या को कम करें और बाकी CPU पर चलेंगे – आप बाद में `ai.free_resources()` के साथ **free gpu memory** अभी भी कर पाएँगे।

### अपेक्षित आउटपुट

स्क्रिप्ट को एक नमूना इनवॉइस पर चलाने पर कुछ इस तरह का परिणाम मिलता है:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

ध्यान दें कि AI ने `$1O0.00` में “O” को सही शून्य में बदल दिया जबकि डॉलर साइन को बरकरार रखा। यही वित्तीय दस्तावेज़ों के लिए **correct OCR errors** का सार है।

## Hugging Face मॉडल डाउनलोड – पर्दे के पीछे क्या होता है?

जब आप `allow_auto_download="true"` सेट करते हैं, तो Aspose AI रैपर `directory_model_path` की जाँच करता है। यदि मॉडल फ़ाइलें वहाँ नहीं हैं, तो यह Hugging Face हब से कनेक्ट होकर **int8‑quantized** संस्करण का `Qwen2.5‑3B‑Instruct‑GGUF` खींचता है और स्थानीय रूप से स्टोर करता है। यह एक‑बार का डाउनलोड आमतौर पर 2 GB से कम होता है, जिससे यह मामूली SSDs पर भी संभव बनता है।

> **Why int8?** 8‑बिट क्वांटाइज़ेशन मेमोरी उपयोग को नाटकीय रूप से घटाता है—जब आप प्रोसेसिंग के बाद **free gpu memory** भी चाहते हैं तो यह महत्वपूर्ण है। ट्रेड‑ऑफ़ सटीकता में एक छोटा सा नुकसान है, लेकिन OCR टेक्स्ट के पोस्ट‑प्रोसेसिंग पर इसका प्रभाव नगण्य है।

यदि आप मॉडल को स्वयं होस्ट करना चाहते हैं, तो बस `.gguf` फ़ाइलों को `YOUR_DIRECTORY/Models` में डालें और Aspose बिना फिर से इंटरनेट पर जाए इन्हें ले लेगा।

## GPU कैसे मुक्त करें – सर्वोत्तम प्रैक्टिसेज़

GPU संसाधन कई वर्कस्टेशनों पर साझा होते हैं। आपका स्क्रिप्ट समाप्त होने के बाद टेन्सर्स को जीवित छोड़ना “CUDA out of memory” त्रुटियों का कारण बन सकता है। `ai.free_resources()` कॉल तीन काम करता है:

1. **Disposes the underlying transformer** – सभी GPU‑रेज़िडेंट वज़न रिलीज़ हो जाते हैं।
2. **Clears the PyTorch cache** – `torch.cuda.empty_cache()` आंतरिक रूप से कॉल किया जाता है।
3. **Deletes temporary files** – डाउनलोड के दौरान बनाए गए किसी भी ऑन‑डिस्क कैश को हटा दिया जाता है।

यदि आप Aspose AI को अन्य PyTorch वर्कलोड्स के साथ मिला रहे हैं, तो आप मैन्युअली `torch.cuda.empty_cache()` भी कॉल कर सकते हैं, लेकिन बिल्ट‑इन मेथड आमतौर पर पर्याप्त होता है।

## चरण‑दर‑चरण वॉक‑थ्रू (H2s with Secondary Keywords)

### Hugging Face मॉडल ऑटोमैटिकली डाउनलोड करें

`AsposeAIModelConfig` कंस्ट्रक्टर Hugging Face API की जटिलता को छिपाता है। बस यह सुनिश्चित करें कि स्क्रिप्ट पहली बार चलाते समय आपके पास इंटरनेट एक्सेस हो। उसके बाद मॉडल `YOUR_DIRECTORY/Models` में रहता है, और बाद के रन तुरंत शुरू हो जाते हैं।

### इनफ़रेंस के बाद GPU मेमोरी रिलीज़ करें

यदि आप इसे एक लंबी‑चलने वाली सर्विस (जैसे Flask API) के अंदर चला रहे हैं, तो प्रत्येक अनुरोध के बाद `ai.free_resources()` कॉल करें। यह मेमोरी लीक्स को रोकता है और सुनिश्चित करता है कि अगला अनुरोध बिना रुकावट के वही GPU पुनः उपयोग कर सके।

### कस्टम प्रॉम्प्ट के साथ OCR त्रुटियों को सुधारें

हमारा `financial_prompt` फ़ंक्शन एक डिक्शनरी लौटाता है जिसमें एक ही कुंजी `prompt` होती है। आप इसे किसी भी डोमेन के अनुसार कस्टमाइज़ कर सकते हैं:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

`ai.set_post_processor(...)` में फ़ंक्शन नाम बदल दें और आपके पास मेडिकल रिकॉर्ड्स के लिए एक **correct OCR errors** पाइपलाइन तैयार है।

### मल्टी‑पेज PDFs पर OCR कैसे चलाएँ

Aspose OCR बॉक्स से बाहर PDFs को हैंडल कर सकता है:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

कच्ची स्ट्रिंग मिलने के बाद, वही LLM पोस्ट‑प्रोसेसर प्रत्येक पेज के टेक्स्ट को साफ़ कर देगा। अतिरिक्त कोड की आवश्यकता नहीं।

### जब आपके पास GPU न हो – GPU कैसे मुक्त करें (भले ही न हो)

CPU‑केवल मशीनों पर भी `ai.free_resources()` कॉल करना हानिरहित है। यह केवल आंतरिक कैश को साफ़ करता है, जिससे RAM भी मुक्त हो सकती है। इसलिए **how to free gpu** सलाह सार्वभौमिक रूप से लागू होती है: हमेशा अपने बाद सफ़ाई करें।

## सामान्य समस्याएँ एवं उनके समाधान

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| **Out‑of‑Memory on GPU** | `gpu_layers` आपके कार्ड के लिए बहुत अधिक सेट है | `gpu_layers` को 10 या 5 तक घटाएँ, बाकी CPU पर चलाएँ |
| **Model never downloads** | कॉरपोरेट फ़ायरवॉल huggingface.co पर HTTPS ब्लॉक करता है | मॉडल को किसी अन्य नेटवर्क पर मैन्युअली डाउनलोड करें, फिर `directory_model_path` को स्थानीय फ़ोल्डर की ओर इंगित करें |
| **Numbers get corrupted** | प्रॉम्प्ट पर्याप्त स्पष्ट नहीं है कि अंक रखे जाएँ | प्रॉम्प्ट में “preserve all numeric values and currency symbols exactly as they appear” जोड़ें |
| **`free_resources` raises an exception** | पुराना Aspose OCR संस्करण उपयोग में है | नवीनतम `aspose-ocr` पैकेज में अपग्रेड करें (pip install --upgrade aspose-ocr) |

## पूर्ण उदाहरण सारांश

यहाँ स्क्रिप्ट फिर से दी गई है, इस बार इनलाइन कमेंट्स के साथ जो भविष्य में प्रत्येक लाइन को समझाते हैं:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

## निष्कर्ष

हमने **how to run OCR** को Aspose के साथ कवर किया, ऑन‑डिमांड Hugging Face मॉडल डाउनलोड किया, एक प्रॉम्प्ट तैयार किया जो **corrects OCR errors** करता है, और अंत में **free gpu memory** किया ताकि आपका वर्कस्टेशन उत्तरदायी बना रहे। पूरा वर्कफ़्लो एक ही, स्व-निहित Python फ़ाइल में फिट हो जाता है—कोई बाहरी स्क्रिप्ट नहीं, कोई मैन्युअल मॉडल हैंडलिंग नहीं, और कोई लटकी हुई GPU अलोकेशन नहीं।

अगले कदम? `financial_prompt` को किसी अन्य प्रॉम्प्ट से बदलकर देखें

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}