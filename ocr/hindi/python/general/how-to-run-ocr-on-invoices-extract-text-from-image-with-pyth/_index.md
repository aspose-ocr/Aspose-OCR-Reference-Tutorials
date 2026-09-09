---
category: general
date: 2026-01-07
description: इनवॉइस प्रोसेसिंग के लिए OCR चलाने और छवि से टेक्स्ट निकालने का तरीका।
  OCR की सटीकता बढ़ाने, OCR के लिए छवि लोड करने और इनवॉइस OCR को कुशलतापूर्वक प्रोसेस
  करने के बारे में सीखें।
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: hi
og_description: इनवॉइस पर OCR चलाने का चरण‑दर‑चरण तरीका। छवि से टेक्स्ट निकालें, OCR
  की सटीकता बढ़ाएँ, और Aspose AI का उपयोग करके OCR के लिए छवि लोड करें।
og_title: इनवॉइस पर OCR कैसे चलाएँ – पूर्ण पायथन गाइड
tags:
- OCR
- Python
- Image Processing
title: इनवॉइस पर OCR कैसे चलाएँ – पायथन के साथ इमेज से टेक्स्ट निकालें
url: /hi/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इनवॉइस पर OCR चलाने का तरीका – Python के साथ इमेज से टेक्स्ट निकालें

क्या आप कभी सोचे हैं **how to run OCR** स्कैन किए गए इनवॉइस पर और साफ़, खोज योग्य टेक्स्ट प्राप्त करने के बारे में? आप अकेले नहीं हैं। कई डेवलपर्स को समस्या होती है जब कच्चा OCR आउटपुट वर्तनी त्रुटियों, टूटे हुए लाइन ब्रेक और अनुपस्थित विराम चिह्नों से भर जाता है। इस ट्यूटोरियल में हम एक फुल‑स्टैक समाधान दिखाएंगे जो न केवल **extracts text from image** करता है बल्कि **improves OCR accuracy** भी Aspose AI मॉडल के पोस्ट‑प्रोसेसिंग से करता है।

आप देखेंगे कैसे **load image for OCR** किया जाता है, बिल्ट‑इन इंजन चलाया जाता है, और फिर एक हल्का स्पेल‑चेक लागू किया जाता है जो परिणाम को डाउनस्ट्रीम एनालिटिक्स के लिए तैयार करता है। अंत तक, आपके पास एक पुन: उपयोग योग्य स्क्रिप्ट होगी जिसे किसी भी इनवॉइस‑प्रोसेसिंग पाइपलाइन में डाला जा सकता है।

> **आपको क्या चाहिए**  
> * Python 3.9 या नया  
> * `aspose-ocr` और `aspose-ai` पैकेज ( `pip` के माध्यम से इंस्टॉल किए गए)  
> * एक इनवॉइस इमेज (PNG, JPEG, या TIFF) – हम उदाहरण के लिए `sample_invoice.png` का उपयोग करेंगे  
> * वैकल्पिक: कम से कम 4 GB VRAM वाला GPU तेज़ मॉडल इन्फ़रेंस के लिए (स्क्रिप्ट CPU पर भी काम करती है)

---

## चरण 1: आवश्यक पैकेज इंस्टॉल करें और पर्यावरण तैयार करें

**load image for OCR** करने से पहले, हमें सुनिश्चित करना होगा कि आवश्यक लाइब्रेरी उपलब्ध हैं। Aspose OCR इंजन एक सरल Python रैपर के साथ आता है, जबकि AI पोस्ट‑प्रोसेसर Hugging Face क्वांटाइज़्ड मॉडल पर निर्भर करता है।

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Pro tip:** यदि आप GPU एक्सेलेरेशन उपयोग करने की योजना बना रहे हैं, तो `torch` को CUDA सपोर्ट के साथ इंस्टॉल करें (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## चरण 2: इनवॉइस इमेज लोड करें

इमेज लोड करना सीधा है, लेकिन यह उल्लेख करना योग्य है कि हम पाथ को स्पष्ट रूप से रॉ स्ट्रिंग (`r"..."`) के रूप में सेट क्यों करते हैं। यह विंडोज पाथ पर आकस्मिक एस्केप‑कैरेक्टर त्रुटियों से बचाता है।

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*यह क्यों महत्वपूर्ण है:* `ocr.Image.load` का उपयोग करने से यह सुनिश्चित होता है कि इमेज Aspose के इष्टतम डिफ़ॉल्ट के अनुसार प्री‑प्रोसेस (बाइनरीज़ेशन, डेस्क्यू) हो गई है, जो पहले से ही **improves OCR accuracy** करता है, किसी भी AI जादू से पहले।

---

## चरण 3: बिल्ट‑इन OCR इंजन चलाएँ

अब हम वास्तव में **run OCR** करते हैं और कच्चा टेक्स्ट कैप्चर करते हैं। यह चरण वह सामान्य आउटपुट दिखाता है जो आप एक साधारण OCR रन से प्राप्त करेंगे—अक्सर लाइन ब्रेक का गड़बड़ और कभी‑कभी वर्तनी त्रुटियों का मिश्रण।

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Typical raw output** (संक्षिप्तता के लिए ट्रंकेटेड):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

आप देख सकते हैं कि “Invoice” “Invo1ce” के रूप में दिख रहा है या विराम चिह्न गायब हैं। यही वह जगह है जहाँ AI पोस्ट‑प्रोसेसर काम आता है।

---

## चरण 4: Aspose AI मॉडल कॉन्फ़िगर करें

हम जिस AI मॉडल का उपयोग करेंगे वह **Qwen2.5‑3B‑Instruct‑GGUF** है, एक हल्का instruction‑tuned LLM जो मिड‑रेंज GPU पर आराम से चलता है। नीचे दिया गया कॉन्फ़िगरेशन Aspose को बताता है कि मॉडल कहाँ से प्राप्त करना है, GPU पर कितनी लेयर्स रखनी हैं, और लंबी पैराग्राफ़ संभालने के लिए कॉन्टेक्स्ट साइज क्या होना चाहिए।

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **यह कॉन्फ़िग क्यों?**  
> * `gpu_layers=30` गति और मेमोरी के बीच संतुलन बनाता है—अधिकांश इन्फ़रेंस GPU पर होता है, जबकि शेष लेयर्स CPU पर रहती हैं ताकि OOM त्रुटियों से बचा जा सके।  
> * `context_size=4096` सुनिश्चित करता है कि मॉडल एक बार में पूरा इनवॉइस देख सके, जिससे महत्वपूर्ण फ़ील्ड्स का ट्रंकेशन रोका जा सके।

---

## चरण 5: एक सरल Spell‑Check पोस्ट‑प्रोसेसर बनाएं

हम AI कॉल को एक छोटे फ़ंक्शन `simple_spell_check` में रैप करेंगे। प्रॉम्प्ट जानबूझकर संक्षिप्त है: “Correct spelling and punctuation:” उसके बाद कच्चा OCR टेक्स्ट। मॉडल एक साफ़ किया हुआ संस्करण लौटाता है।

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**How it works:** `ai.run_prompt` प्रॉम्प्ट को स्थानीय रूप से लोड किए गए LLM को भेजता है, जो फिर एक सिंगल स्ट्रिंग लौटाता है जिसमें सही वर्तनी, उचित विराम चिह्न, और अधिक प्राकृतिक लाइन‑ब्रेक लेआउट होता है।

---

## चरण 6: कच्चे OCR टेक्स्ट पर पोस्ट‑प्रोसेसर लागू करें

अब जादू होता है। हम कच्चे OCR आउटपुट को अपने पोस्ट‑प्रोसेसर में फीड करते हैं और सुधरा हुआ परिणाम प्रिंट करते हैं।

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Sample enhanced output**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

ध्यान दें सुधरी हुई “Invoice” वर्तनी, उचित कोलन उपयोग, और सुसंगत लाइन ब्रेक—बिल्कुल वही जो विश्वसनीय डाउनस्ट्रीम पार्सिंग के लिए चाहिए।

---

## चरण 7: संसाधनों को साफ़ करें

OCR इंजन और AI मॉडल दोनों मूल संसाधन आवंटित करते हैं। जब आप समाप्त हो जाएँ, विशेषकर लंबी‑चलने वाली सर्विसेज़ में, उन्हें मुक्त करना अच्छा अभ्यास है।

```python
ai.free_resources()
engine.dispose()
```

---

## पूर्ण स्क्रिप्ट – पेस्ट करने के लिए तैयार

नीचे पूर्ण, चलाने योग्य स्क्रिप्ट है जो हर चरण को जोड़ती है। इसे `invoice_ocr.py` के रूप में सेव करें, `YOUR_DIRECTORY` को उस फ़ोल्डर से बदलें जिसमें आपका इनवॉइस इमेज है, और `python invoice_ocr.py` के साथ चलाएँ।

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

स्क्रिप्ट चलाएँ और आप दोनों, शोरयुक्त कच्चा OCR डम्प और पॉलिश्ड, **improved OCR accuracy** संस्करण, साइड बाय साइड देखेंगे।

---

## अक्सर पूछे जाने वाले प्रश्न और किनारे के केस

### 1. यदि मेरा इनवॉइस इमेज मल्टी‑पेज PDF है तो क्या?

Aspose OCR सीधे PDF पेज लोड कर सकता है। इमेज लोड लाइन को इस प्रकार बदलें:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

`page_index` को इटरेट करके प्रत्येक पेज को क्रमिक रूप से प्रोसेस करें।

### 2. मेरा GPU मेमोरी समाप्त हो गया—क्या मैं केवल CPU उपयोग कर सकता हूँ?

बिल्कुल। `AsposeAIModelConfig` में `gpu_layers=0` सेट करें। मॉडल पूरी तरह CPU पर चलेगा, जो धीमा है लेकिन लो‑एंड हार्डवेयर के लिए सुरक्षित है।

### 3. गैर‑अंग्रेज़ी इनवॉइस को कैसे हैंडल करें?

मॉडल रिपॉज़िटरी ID को भाषा‑विशिष्ट मॉडल से बदलें, उदाहरण के लिए, मल्टी‑लिंगुअल सपोर्ट के लिए `"mistralai/Mistral-7B-Instruct-v0.2"`। पाइपलाइन का बाकी हिस्सा अपरिवर्तित रहता है।

### 4. क्या मैं कई पोस्ट‑प्रोसेसर चेन कर सकता हूँ (जैसे, डेट फॉर्मेट, टोटल एक्सट्रैक्ट करना)?

हां। `ai.set_post_processor` कॉलेबल्स की सूची स्वीकार करता है। उदाहरण के लिए:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

आउटपुट पहले स्पेल‑चेक होगा, फिर टोटल्स एक्सट्रैक्ट किए जाएंगे।

---

## प्रदर्शन टिप्स और सर्वोत्तम प्रैक्टिसेज़

| Tip | Why it Helps |
|-----|---------------|
| **एक साथ कई इनवॉइस बैच करें** – उन्हें एक सूची में लोड करें और लूप में प्रोसेस करें। | Python इंटरप्रेटर ओवरहेड को कम करता है और AI मॉडल को मेमोरी में वार्म रखता है। |
| **मॉडल को कैश करें** – वेब सर्विस में `initialize` को बार‑बार कॉल करने से बचें। | मॉडल लोडिंग में लगभग 30 सेकंड लग सकते हैं; कैशिंग से तुरंत प्रतिक्रिया मिलती है। |
| **बड़ी इमेज को रीसाइज़ करें** OCR से पहले 1500 px चौड़ाई तक। | छोटी इमेज OCR और AI इन्फ़रेंस दोनों को तेज़ करती है, बिना सटीकता घटाए। |
| **प्रोडक्शन में `allow_auto_download="false"` सेट करें** – मॉडल को अपने डिप्लॉयमेंट के साथ शिप करें। | निर्धारित स्टार्टअप टाइम्स सुनिश्चित करता है और नेटवर्क समस्याओं से बचाता है। |

---

## निष्कर्ष

हमने इनवॉइस पर **how to run OCR** को कवर किया है, इमेज लोड करने से लेकर AI‑ड्रिवेन स्पेल‑चेक से परिणाम को पॉलिश करने तक। इन चरणों का पालन करके आप विश्वसनीय रूप से **extract text from image**, **improve OCR accuracy**, और किसी भी Python‑आधारित वर्कफ़्लो में सहजता से **process invoice OCR** कर सकते हैं।

इसे कुछ विभिन्न इनवॉइस लेआउट्स के साथ चलाएँ—शायद एक हस्तलेखित रसीद या स्कैन किया हुआ कॉन्ट्रैक्ट। वही पाइपलाइन न्यूनतम बदलावों के साथ अनुकूलित होती है, यह साबित करता है कि एक अच्छी‑संरचित OCR + AI कॉम्बो किसी भी दस्तावेज़‑ऑटोमेशन प्रोजेक्ट के लिए एक बहुमुखी टूल है।

यदि आपको यह गाइड उपयोगी लगा, तो इसे अपने टीममेट्स के साथ शेयर करने या Aspose पैकेजों को होस्ट करने वाले रिपॉज़िटरी को स्टार करने पर विचार करें।

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}