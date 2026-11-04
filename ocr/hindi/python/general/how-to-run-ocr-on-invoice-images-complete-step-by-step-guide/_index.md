---
category: general
date: 2026-01-12
description: Aspose OCR और एक हल्के Hugging Face मॉडल का उपयोग करके इनवॉइस छवियों
  से OCR चलाने और टेक्स्ट निकालने का तरीका। मॉडल डाउनलोड करना, OCR त्रुटियों को सुधारना,
  और छवि पर OCR करना सीखें।
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: hi
og_description: इनवॉइस छवियों पर OCR चलाने, टेक्स्ट निकालने और Hugging Face LLM के
  साथ त्रुटियों को ठीक करने का तरीका। बेजोड़ परिणामों के लिए इस पूर्ण गाइड का पालन
  करें।
og_title: इनवॉइस छवियों पर OCR कैसे चलाएँ – पूर्ण ट्यूटोरियल
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: इनवॉइस इमेजेज़ पर OCR कैसे चलाएँ – पूर्ण चरण-दर-चरण गाइड
url: /hi/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इनवॉइस इमेजेज़ पर OCR चलाने का पूरा चरण‑दर‑चरण गाइड

क्या आपने कभी सोचा है **कैसे OCR चलाएँ** किसी स्कैन किए गए इनवॉइस पर और साफ़, सर्चेबल टेक्स्ट प्राप्त करें बिना घंटों तक सफ़ाई किए? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में कच्चा OCR आउटपुट अक्सर गलत पहचान से भरा होता है—जैसे “O” को “0”, “l” को “1”, या यहाँ‑तक कि पूरे शब्द गड़बड़। अच्छी खबर? कुछ ही पंक्तियों के Python कोड से आप न सिर्फ **इमेज पर OCR कर सकते** हैं बल्कि Hugging Face के हल्के मॉडल का उपयोग करके **OCR त्रुटियों को स्वचालित रूप से सुधार** भी सकते हैं।

इस ट्यूटोरियल में हम सब कुछ कवर करेंगे: इनवॉइस इमेज लोड करने से लेकर कच्चा टेक्स्ट निकालना, क्वांटाइज़्ड मॉडल डाउनलोड करना, और परिणाम को पॉलिश करना ताकि आपको एक परिपूर्ण ट्रांसक्रिप्शन मिले जो आगे की प्रोसेसिंग के लिए तैयार हो। अंत तक आप **इनवॉइस PDFs या PNGs से टेक्स्ट निकाल** सकेंगे एक ही, दोहराने योग्य स्क्रिप्ट से।

## आवश्यकताएँ और सेटअप

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | आधुनिक सिंटैक्स और टाइप हिंट्स |
| `aspose-ocr` पैकेज | उदाहरण में उपयोग किया गया `ocr.OcrEngine` प्रदान करता है |
| `aspose-ai` पैकेज | `AsposeAI` पोस्ट‑प्रोसेसर उपलब्ध कराता है |
| GPU तक पहुँच (वैकल्पिक) | LLM लेयर्स को तेज़ करता है; अन्यथा CPU भी ठीक है |
| इंटरनेट कनेक्शन (पहली बार) | **Hugging Face मॉडल डाउनलोड** करने के लिए आवश्यक |

आप आवश्यक लाइब्रेरीज़ इस तरह इंस्टॉल कर सकते हैं:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro tip:** यदि आप GPU पर LLM चलाने की योजना बना रहे हैं, तो CUDA सपोर्ट के साथ `torch` इंस्टॉल करें (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`)।

अब जब पर्यावरण तैयार है, चलिए कोड की ओर बढ़ते हैं।

---

## चरण 1 – OCR इंजन को इनिशियलाइज़ करें और अपनी इनवॉइस इमेज लोड करें

सबसे पहले आपको Aspose के OCR इंजन का एक इंस्टेंस बनाना है और उसे उस फ़ाइल की ओर इंगित करना है जिसे आप प्रोसेस करना चाहते हैं। यह चरण **कैसे OCR चलाएँ** किसी भी इमेज पर, इसका आधार है।

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Why this matters:** `load_image` PNG, JPEG, TIFF, और यहाँ तक कि PDF पेजेज़ को भी स्वीकार करता है, जिससे आप **इमेज पर OCR** डेटा किसी भी फ़ॉर्मेट में कर सकते हैं।

---

## चरण 2 – बेसिक OCR चलाएँ और कच्चा टेक्स्ट कैप्चर करें

इमेज लोड हो जाने के बाद, इंजन एक कच्ची ट्रांसक्रिप्शन बना सकता है। यह आउटपुट अक्सर शोरयुक्त होता है, इसलिए हम बाद में एक सुधार चरण चलाएंगे।

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

आम तौर पर कच्चा आउटपुट इस तरह दिख सकता है:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

ध्यान दें जहाँ शून्य (`0`) दिख रहा है, जबकि अंक “O” होना चाहिए? यही वह गलती है जिसे हम बाद में ठीक करेंगे।

---

## चरण 3 – हल्के LLM के साथ AI पोस्ट‑प्रोसेसर कॉन्फ़िगर करें

अब हम एक **download Hugging Face model** लाते हैं जो हार्डवेयर पर चलने के लिए पर्याप्त छोटा है, लेकिन इनवॉइस भाषा को समझने के लिए पर्याप्त शक्तिशाली है। उदाहरण में Qwen 2.5 3B‑Instruct GGUF मॉडल का उपयोग किया गया है, जिसे `int8` में क्वांटाइज़ किया गया है ताकि मेमोरी फुटप्रिंट छोटा रहे।

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Why this model?** `int8` क्वांटाइज़ेशन फ़ाइल को ~1.2 GB तक घटा देता है, जिससे यह अधिकांश लैपटॉप पर संभव हो जाता है। GPU लेयर्स इन्फ़रेंस को तेज़ करते हैं, लेकिन कोड GPU न मिलने पर स्वचालित रूप से CPU पर फ़ॉल्बैक करता है।

---

## चरण 4 – कच्चे OCR परिणाम पर LLM‑आधारित सुधार चलाएँ

मॉडल तैयार होने के बाद, हम कच्चा टेक्स्ट पोस्ट‑प्रोसेसर में फीड करते हैं। LLM ट्रांसक्रिप्शन को पुनः लिखेगा, सामान्य OCR गड़बड़ियों को ठीक करेगा और नंबरों को सामान्य करेगा।

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

अपेक्षित साफ़ किया हुआ आउटपुट:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

आप देख सकते हैं कि शून्य फिर से अक्षर “O” में बदल गया है, और “Am0unt” अब “Amount” हो गया है। यही **OCR त्रुटियों को स्वचालित रूप से सुधार** का मूल है।

---

## चरण 5 – रिसोर्सेज़ रिलीज़ करें और क्लीन‑अप करें

बड़े भाषा मॉडल GPU मेमोरी को पकड़ सकते हैं, इसलिए काम खत्म होने पर रिसोर्सेज़ को मुक्त करना अच्छा अभ्यास है।

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

यदि आप बैच में कई इनवॉइस प्रोसेस करने की योजना बनाते हैं, तो आप मॉडल को लोडेड रख सकते हैं और स्क्रिप्ट के अंत में ही उसे फ्री कर सकते हैं।

---

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ मिलाकर, यहाँ एक सिंगल स्क्रिप्ट है जिसे आप `.py` फ़ाइल में रखकर चला सकते हैं:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

स्क्रिप्ट चलाने पर “AI‑corrected” ब्लॉक जैसा आउटपुट मिलेगा। इमेज पाथ को किसी भी अन्य इनवॉइस या रसीद से बदलें ताकि **इनवॉइस फ़ाइलों से टेक्स्ट निकाल** सकें बड़े पैमाने पर।

---

## अक्सर पूछे जाने वाले प्रश्न और एज केस

### अगर मेरे पास GPU नहीं है तो क्या करें?

`gpu_layers` पैरामीटर वैकल्पिक है। इसे `0` सेट करें या छोड़ दें, और मॉडल पूरी तरह CPU पर चलेगा। अपेक्षा रखें कि इन्फ़रेंस धीमा होगा—आधुनिक लैपटॉप पर प्रति पेज लगभग 2–3 सेकंड।

### मेरे इनवॉइस मल्टी‑पेज PDFs हैं। मैं उन्हें कैसे हैंडल करूँ?

हर पेज को अलग इमेज में कन्वर्ट करें (जैसे `pdf2image` का उपयोग करके) और उसी स्क्रिप्ट के साथ पेजेज़ पर लूप चलाएँ। OCR इंजन प्रत्येक इमेज को स्वतंत्र रूप से प्रोसेस कर सकता है, और LLM प्रत्येक टेक्स्ट ब्लॉक को सुधार देगा।

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### फ़ायरवॉल के पीछे मॉडल डाउनलोड फेल हो रहा है?

मॉडल को मैन्युअली Hugging Face मॉडल हब से डाउनलोड करें, उसे अनज़िप करके लोकल फ़ोल्डर में रखें, और `hugging_face_repo_id` को लोकल पाथ की ओर पॉइंट करें:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### सुधार की सटीकता कितनी है?

आमतौर पर अंग्रेज़ी‑भाषी इनवॉइस के लिए, LLM सामान्य OCR गलतियों का >95 % ठीक कर देता है। जटिल हस्तलिखित नोट्स को अभी भी मैन्युअल रिव्यू की जरूरत पड़ सकती है।

---

## प्रोडक्शन उपयोग के लिए टिप्स और ट्रिक्स

- **बैच प्रोसेसिंग:** चरण 2‑4 को एक फ़ंक्शन में रैप करें और फ़ाइल पाथ की लिस्ट को फीड करें। मॉडल को री‑लोड करने से बचने के लिए वही `AsposeAI` इंस्टेंस पुनः‑उपयोग करें।
- **लॉगिंग:** `print` को Python के `logging` मॉड्यूल से बदलें ताकि ऑडिट ट्रेल के लिए कच्चा और सुधरा हुआ दोनों आउटपुट कैप्चर हो सके।
- **एरर हैंडलिंग:** OCR कॉल को `try/except` ब्लॉक्स में रखें। यदि कोई इमेज फेल हो, तो फ़ाइलनाम को लॉग करें और प्रोसेस जारी रखें।
- **परफ़ॉर्मेंस ट्यूनिंग:** `gpu_layers` के साथ प्रयोग करें। अधिक लेयर्स GPU पर इन्फ़रेंस को तेज़ करेंगे लेकिन VRAM उपयोग बढ़ाएंगे।

---

## निष्कर्ष

हमने **इनवॉइस इमेजेज़ पर OCR चलाने** की पूरी प्रक्रिया को कवर किया, दिखाया कि कैसे **इमेज पर OCR** करें, **Hugging Face मॉडल डाउनलोड** करें, और **OCR त्रुटियों को स्वचालित रूप से सुधार**ें। पूरा स्क्रिप्ट एक व्यावहारिक वर्कफ़्लो दर्शाता है जिसे आप किसी भी Python‑आधारित ऑटोमेशन पाइपलाइन में डाल सकते हैं।

अगला कदम? पाइपलाइन को **मुख्य फ़ील्ड्स निकालने** (इनवॉइस नंबर, तारीख, कुल) के लिए रेगुलर एक्सप्रेशन के साथ विस्तारित करें, या साफ़ आउटपुट को डेटाबेस में डालें ताकि सर्चेबल रिकॉर्ड बन सकें। यदि आपको अलग भाषा या डोमेन‑स्पेसिफिक ज्ञान चाहिए, तो Hugging Face के अन्य हल्के LLMs के साथ प्रयोग कर सकते हैं।

कोडिंग का आनंद लें, और आपकी OCR परिणाम हमेशा क्रिस्टल‑क्लियर रहें! 

![इनवॉइस इमेज पर OCR चलाने का उदाहरण](ocr_invoice_example.png "इनवॉइस पर OCR चलाने का उदाहरण")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}