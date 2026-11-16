---
category: general
date: 2026-05-03
description: Aspose OCR और AI स्पेल‑चेक का उपयोग करके छवि से टेक्स्ट निकालें। सीखें
  कि कैसे छवि को OCR करें, OCR के लिए छवि लोड करें, इनवॉइस से टेक्स्ट पहचानें और GPU
  संसाधनों को रिलीज़ करें।
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: hi
og_description: Aspose OCR और AI वर्तनी‑जाँच के साथ छवि से टेक्स्ट निकालें। चरण‑दर‑चरण
  गाइड जिसमें छवि को OCR करने, OCR के लिए छवि लोड करने और GPU संसाधनों को रिलीज़ करने
  की प्रक्रिया शामिल है।
og_title: छवि से टेक्स्ट निकालें – पूर्ण OCR और स्पेल‑चेक गाइड
tags:
- OCR
- Aspose
- AI
- Python
title: छवि से पाठ निकालें – Aspose AI स्पेल‑चेक के साथ OCR
url: /hi/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# छवि से टेक्स्ट निकालें – Complete OCR & Spell‑Check Guide

क्या आपको कभी **छवि से टेक्स्ट निकालें** की जरूरत पड़ी है लेकिन आप सुनिश्चित नहीं थे कि कौन सी लाइब्रेरी आपको गति और सटीकता दोनों देगी? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में—जैसे इनवॉइस प्रोसेसिंग, रसीद डिजिटाइज़ेशन, या अनुबंध स्कैनिंग—एक तस्वीर से साफ़, खोजने योग्य टेक्स्ट प्राप्त करना पहला बाधा है।

अच्छी खबर यह है कि Aspose OCR को एक हल्के Aspose AI मॉडल के साथ जोड़ने से यह काम कुछ ही पायथन लाइनों में किया जा सकता है। इस ट्यूटोरियल में हम **छवि को OCR कैसे करें**, चित्र को सही तरीके से लोड करना, बिल्ट‑इन स्पेल‑चेक पोस्ट‑प्रोसेसर चलाना, और अंत में **GPU संसाधनों को रिलीज़ करें** ताकि आपका ऐप मेमोरी‑फ्रेंडली बना रहे।

इस गाइड के अंत तक आप **इनवॉइस से टेक्स्ट पहचानने** वाली छवियों को पहचान सकेंगे, सामान्य OCR त्रुटियों को स्वचालित रूप से सुधारेंगे, और अगली बैच के लिए अपना GPU साफ़ रखेंगे।

## आपको क्या चाहिए

- Python 3.9 या नया (कोड टाइप हिंट्स का उपयोग करता है लेकिन पहले के 3.x संस्करणों पर भी काम करता है)
- `aspose-ocr` और `aspose-ai` पैकेज (इंस्टॉल करने के लिए `pip install aspose-ocr aspose-ai`)
- CUDA‑सक्षम GPU वैकल्पिक है; यदि नहीं मिला तो स्क्रिप्ट CPU पर फ़ॉल बैक हो जाएगी।
- एक उदाहरण छवि, जैसे `sample_invoice.png`, को किसी फ़ोल्डर में रखें जिसे आप संदर्भित कर सकें।

कोई भारी ML फ्रेमवर्क नहीं, कोई बड़े मॉडल डाउनलोड नहीं—सिर्फ एक छोटा Q4‑K‑M क्वांटाइज़्ड मॉडल जो अधिकांश GPUs पर आराम से फिट हो जाता है।

## चरण 1: OCR इंजन को इनिशियलाइज़ करें – छवि से टेक्स्ट निकालें

सबसे पहले आप एक `OcrEngine` इंस्टेंस बनाते हैं और उसे बताते हैं कि आप कौन सी भाषा अपेक्षित है। यहाँ हम अंग्रेज़ी चुनते हैं और प्लेन‑टेक्स्ट आउटपुट का अनुरोध करते हैं, जो डाउनस्ट्रीम प्रोसेसिंग के लिए आदर्श है।

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**यह क्यों महत्वपूर्ण है:** भाषा सेट करने से कैरेक्टर सेट सीमित हो जाता है, जिससे सटीकता बढ़ती है। प्लेन‑टेक्स्ट मोड लेआउट जानकारी को हटाता है जो आमतौर पर आपको तब नहीं चाहिए जब आप सिर्फ छवि से टेक्स्ट निकालना चाहते हैं।

## चरण 2: OCR के लिए छवि लोड करें – छवि को OCR कैसे करें

अब हम इंजन को एक वास्तविक चित्र देते हैं। `Image.load` हेल्पर सामान्य फ़ॉर्मैट (PNG, JPEG, TIFF) को समझता है और फ़ाइल‑IO की जटिलताओं को एब्स्ट्रैक्ट करता है।

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**टिप:** यदि आपके स्रोत चित्र बड़े हैं, तो उन्हें इंजन को भेजने से पहले रीसाइज़ करने पर विचार करें; छोटे आकार GPU मेमोरी उपयोग को कम कर सकते हैं बिना पहचान की गुणवत्ता को नुकसान पहुँचाए।

## चरण 3: Aspose AI मॉडल को कॉन्फ़िगर करें – इनवॉइस से टेक्स्ट पहचानें

Aspose AI एक छोटे GGUF मॉडल के साथ आता है जिसे आप ऑटो‑डownload कर सकते हैं। उदाहरण में `Qwen2.5‑3B‑Instruct‑GGUF` रिपॉजिटरी का उपयोग किया गया है, जो `q4_k_m` में क्वांटाइज़्ड है। हम रनटाइम को भी बताते हैं कि GPU पर 20 लेयर आवंटित करे, जो गति और VRAM उपयोग के बीच संतुलन बनाता है।

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**पर्दे के पीछे:** क्वांटाइज़्ड मॉडल डिस्क पर लगभग 1.5 GB का है, जो फुल‑प्रिसिजन मॉडल का एक छोटा हिस्सा है, फिर भी यह सामान्य OCR गलतियों को पहचानने के लिए पर्याप्त भाषाई बारीकियों को पकड़ता है।

## चरण 4: AsposeAI को इनिशियलाइज़ करें और स्पेल‑चेक पोस्ट‑प्रोसेसर संलग्न करें

Aspose AI में एक तैयार‑निर्मित स्पेल‑चेक पोस्ट‑प्रोसेसर शामिल है। इसे संलग्न करने से, हर OCR परिणाम स्वचालित रूप से साफ़ हो जाएगा।

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**पोस्ट‑प्रोसेसर क्यों उपयोग करें?** OCR इंजन अक्सर “Invoice” को “Invo1ce” या “Total” को “T0tal” पढ़ लेते हैं। स्पेल‑चेक एक हल्के भाषा मॉडल को कच्ची स्ट्रिंग पर चलाता है और उन त्रुटियों को ठीक करता है बिना आपको कस्टम डिक्शनरी लिखे।

## चरण 5: OCR परिणाम पर स्पेल‑चेक पोस्ट‑प्रोसेसर चलाएँ

सब कुछ कनेक्ट हो जाने पर, एक ही कॉल से सुधरा हुआ टेक्स्ट मिलता है। हम मूल और साफ़ किए गए दोनों संस्करण प्रिंट करते हैं ताकि आप सुधार देख सकें।

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

इनवॉइस के लिए सामान्य आउटपुट कुछ इस प्रकार दिख सकता है:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

ध्यान दें कि “Invo1ce” सही शब्द “Invoice” में बदल गया। यही बिल्ट‑इन AI स्पेल‑चेक की शक्ति है।

## चरण 6: GPU संसाधनों को रिलीज़ करें – GPU संसाधनों को सुरक्षित रूप से रिलीज़ करें

यदि आप इसे एक दीर्घकालिक सेवा में चला रहे हैं (जैसे, एक वेब API जो प्रति मिनट दर्जनों इनवॉइस प्रोसेस करता है), तो प्रत्येक बैच के बाद GPU कॉन्टेक्स्ट को फ्री करना आवश्यक है। अन्यथा आपको मेमोरी लीक दिखेगा और अंततः “CUDA out of memory” त्रुटियां मिलेंगी।

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**प्रो टिप:** `free_resources()` को एक `finally` ब्लॉक या कंटेक्स्ट मैनेजर के अंदर कॉल करें ताकि यह हमेशा चले, चाहे कोई अपवाद हो या न हो।

## पूर्ण कार्यशील उदाहरण

सभी हिस्सों को मिलाकर आपको एक स्व-निहित स्क्रिप्ट मिलती है जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं।

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

फ़ाइल को सेव करें, अपनी छवि का पाथ समायोजित करें, और `python extract_text_from_image.py` चलाएँ। आपको कंसोल में साफ़ किया गया इनवॉइस टेक्स्ट प्रिंट होता दिखेगा।

## अक्सर पूछे जाने वाले प्रश्न (FAQ)

**प्रश्न:** क्या यह केवल CPU वाले मशीनों पर काम करता है?  
**उत्तर:** बिल्कुल। यदि कोई GPU नहीं मिलता, तो Aspose AI CPU निष्पादन पर फ़ॉल बैक हो जाता है, हालांकि यह धीमा होगा। आप `model_cfg.gpu_layers = 0` सेट करके CPU को मजबूर कर सकते हैं।

**प्रश्न:** यदि मेरे इनवॉइस अंग्रेज़ी के अलावा किसी अन्य भाषा में हैं तो?  
**उत्तर:** `ocr_engine.language` को उपयुक्त enum वैल्यू (जैसे, `aocr.Language.Spanish`) में बदलें। स्पेल‑चेक मॉडल बहुभाषी है, लेकिन भाषा‑विशिष्ट मॉडल के साथ बेहतर परिणाम मिल सकते हैं।

**प्रश्न:** क्या मैं कई छवियों को लूप में प्रोसेस कर सकता हूँ?  
**उत्तर:** हाँ। लोडिंग, पहचान, और पोस्ट‑प्रोसेसिंग स्टेप्स को `for` लूप के अंदर रखें। यदि आप वही AI इंस्टेंस पुनः उपयोग कर रहे हैं तो लूप के बाद या प्रत्येक बैच के बाद `ocr_ai.free_resources()` कॉल करना याद रखें।

**प्रश्न:** मॉडल डाउनलोड का आकार कितना है?  
**उत्तर:** क्वांटाइज़्ड `q4_k_m` संस्करण के लिए लगभग 1.5 GB। यह पहली बार चलाने के बाद कैश हो जाता है, इसलिए बाद के निष्पादन तुरंत होते हैं।

## निष्कर्ष

इस ट्यूटोरियल में हमने दिखाया कि कैसे Aspose OCR का उपयोग करके **छवि से टेक्स्ट निकालें**, एक छोटा AI मॉडल कॉन्फ़िगर करें, स्पेल‑चेक पोस्ट‑प्रोसेसर लागू करें, और सुरक्षित रूप से **GPU संसाधनों को रिलीज़ करें**। यह वर्कफ़्लो चित्र लोड करने से लेकर स्वयं को साफ़ करने तक सब कुछ कवर करता है, जिससे आपको **इनवॉइस से टेक्स्ट पहचानने** के परिदृश्यों के लिए एक विश्वसनीय पाइपलाइन मिलती है।

अगला कदम? स्पेल‑चेक को एक कस्टम एंटिटी‑एक्सट्रैक्शन मॉडल से बदलने का प्रयास करें

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}