---
category: general
date: 2026-04-29
description: जानिए कैसे अपने स्कैन पर OCR चलाएँ, Hugging Face मॉडल को स्वचालित रूप
  से उपयोग करें, और Aspose OCR के साथ मिनटों में स्कैन से टेक्स्ट पहचानें।
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: hi
og_description: Aspose OCR का उपयोग करके स्कैन पर OCR कैसे चलाएँ, स्वचालित रूप से
  Hugging Face मॉडल डाउनलोड करें, और साफ़, विराम चिह्नों वाला टेक्स्ट प्राप्त करें।
og_title: Aspose और Hugging Face के साथ OCR कैसे चलाएँ – पूर्ण गाइड
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: Aspose और Hugging Face के साथ OCR कैसे चलाएँ – पूर्ण मार्गदर्शिका
url: /hi/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose और Hugging Face के साथ OCR कैसे चलाएँ – पूर्ण गाइड

क्या आपने कभी सोचा है कि सेटिंग्स को घंटों तक समायोजित किए बिना स्कैन किए गए दस्तावेज़ों के ढेर पर **OCR कैसे चलाएँ**? आप अकेले नहीं हैं। कई प्रोजेक्ट्स में, डेवलपर्स को जल्दी से **स्कैन से टेक्स्ट पहचानना** होता है, फिर भी वे मॉडल डाउनलोड और पोस्ट‑प्रोसेसिंग में फँस जाते हैं।  

अच्छी खबर: यह ट्यूटोरियल आपको एक तैयार‑से‑चलाने वाला समाधान दिखाता है जो **Hugging Face मॉडल का उपयोग करता है**, इसे स्वचालित रूप से डाउनलोड करता है, और विराम चिह्न जोड़ता है ताकि आउटपुट ऐसा लगे जैसे इंसान ने लिखा हो। अंत तक, आपके पास एक स्क्रिप्ट होगी जो फ़ोल्डर में प्रत्येक इमेज को प्रोसेस करती है और प्रत्येक स्कैन के बगल में एक साफ़ `.txt` फ़ाइल रख देती है।

## आपको क्या चाहिए

- Python 3.8+ (कोड f‑strings का उपयोग करता है, इसलिए पुराने संस्करण काम नहीं करेंगे)
- `aspose-ocr` पैकेज (इंस्टॉल करने के लिए `pip install aspose-ocr`)
- पहली बार मॉडल डाउनलोड के लिए इंटरनेट एक्सेस  
- इमेज स्कैन का फ़ोल्डर (`.png`, `.jpg`, या `.tif`)

बस इतना ही—कोई अतिरिक्त बाइनरी नहीं, कोई मैन्युअल मॉडल सेटिंग नहीं। चलिए शुरू करते हैं।

![how to run OCR example](https://example.com/ocr-demo.png "how to run OCR example")

## चरण 1: Aspose OCR क्लासेस इम्पोर्ट करें और वातावरण सेट अप करें

हम Aspose OCR लाइब्रेरी से आवश्यक क्लासेस को इम्पोर्ट करके शुरू करते हैं। सभी चीज़ों को पहले से इम्पोर्ट करने से स्क्रिप्ट साफ़ रहती है और लापता डिपेंडेंसीज़ को ढूँढ़ना आसान हो जाता है।

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*क्यों यह महत्वपूर्ण है*: `OcrEngine` भारी काम करता है, जबकि `AsposeAI` हमें बड़े भाषा मॉडल को प्लग‑इन करके smarter post‑processing करने देता है। यदि आप इम्पोर्ट छोड़ देते हैं, तो बाकी कोड भी कंपाइल नहीं होगा—इसलिए इसे मत भूलें।

## चरण 2: GPU‑सजग Hugging Face मॉडल कॉन्फ़िगर करें  

अब हम Aspose को बताते हैं कि मॉडल कहाँ से लाना है और कितनी लेयर्स GPU पर चलनी चाहिए। `allow_auto_download="true"` फ़्लैग आपके लिए **मॉडल को स्वचालित रूप से डाउनलोड** करता है।

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **प्रो टिप**: यदि आपके पास GPU नहीं है, तो `gpu_layers=0` सेट करें। मॉडल CPU पर फॉल बैक हो जाएगा, जो धीमा है लेकिन फिर भी काम करता है।

### Hugging Face मॉडल क्यों चुनें?

Hugging Face एक विशाल संग्रह में तैयार‑से‑उपयोग LLMs रखता है। `Qwen/Qwen2.5-3B-Instruct-GGUF` की ओर इशारा करके, आपको एक कॉम्पैक्ट, इंस्ट्रक्शन‑ट्यून्ड मॉडल मिलता है जो विराम चिह्न जोड़ सकता है, स्पेसिंग सही कर सकता है, और छोटे OCR त्रुटियों को भी ठीक कर सकता है। यह व्यावहारिक रूप से **use hugging face model** का सार है।

## चरण 3: AI इंजन को इनिशियलाइज़ करें और विराम चिह्न पोस्ट‑प्रोसेसिंग सक्षम करें  

AI इंजन सिर्फ फैंसी चैट के लिए नहीं है—यहाँ हम एक *punctuation adder* जोड़ते हैं जो कच्चे OCR आउटपुट को साफ़ करता है।

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*क्या हो रहा है?* `set_post_processor` कॉल एक बिल्ट‑इन पोस्ट‑प्रोसेसर को रजिस्टर करता है जो OCR इंजन समाप्त होने के बाद चलता है। यह कच्ची स्ट्रिंग लेता है और जहाँ‑जहाँ आवश्यक हो, कॉमा, पीरियड और बड़े अक्षर डालता है, जिससे अंतिम टेक्स्ट बहुत अधिक पठनीय बन जाता है।

## चरण 4: OCR इंजन बनाएं और AI इंजन को अटैच करें  

AI इंजन को OCR इंजन से जोड़ने से हमें एक ही ऑब्जेक्ट मिलता है जो अक्षरों को पढ़ सकता है और परिणाम को पॉलिश भी कर सकता है।

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

यदि आप इस चरण को छोड़ देते हैं, तो OCR फिर भी काम करेगा, लेकिन आपको विराम चिह्न का बूस्ट नहीं मिलेगा—इसलिए आउटपुट शब्दों की धारा जैसा दिखेगा।

## चरण 5: फ़ोल्डर में प्रत्येक इमेज को प्रोसेस करें  

यह ट्यूटोरियल का मुख्य भाग है। हम प्रत्येक इमेज पर लूप करते हैं, OCR चलाते हैं, पोस्ट‑प्रोसेसर लागू करते हैं, और साफ़ किया हुआ टेक्स्ट साइड‑बाय‑साइड `.txt` फ़ाइल में लिखते हैं।

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### क्या उम्मीद करें

स्क्रिप्ट चलाने पर कुछ इस तरह का आउटपुट मिलता है:

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

प्रत्येक लाइन आपको confidence स्कोर बताती है (एक त्वरित हेल्थ चेक) और `invoice_001.png.txt`, `receipt_2024.tif.txt` आदि बनाती है, जिसमें विराम चिह्नित, मानव‑पठनीय टेक्स्ट होता है।

### एज केस और वैरिएशन्स

- **Non‑English scans**: `hugging_face_repo_id` को एक मल्टीलेंग्वेज मॉडल (जैसे, `microsoft/Multilingual-LLM-GGUF`) में बदलें।
- **Large batches**: लूप को `concurrent.futures.ThreadPoolExecutor` में रैप करें ताकि पैरलल प्रोसेसिंग हो, लेकिन GPU मेमोरी लिमिट का ध्यान रखें।
- **Custom post‑processing**: यदि आपको डोमेन‑स्पेसिफिक क्लीनअप चाहिए (जैसे, इनवॉइस नंबर हटाना), तो `"punctuation_adder"` को अपनी स्क्रिप्ट से बदलें।

## चरण 6: संसाधनों को साफ़ करें  

जब जॉब समाप्त हो जाता है, संसाधनों को मुक्त करने से मेमोरी लीक रोकता है, विशेषकर यदि आप इसे एक लंबी अवधि की सर्विस के अंदर चला रहे हैं।

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

इस चरण को नजरअंदाज करने से GPU मेमोरी लटक सकती है, जो बाद की रन को बाधित कर देगा।

## पुनरावलोकन: OCR को एंड‑टू‑एंड कैसे चलाएँ  

सिर्फ कुछ लाइनों में, हमने दिखाया है **OCR कैसे चलाएँ** स्कैन के फ़ोल्डर पर, **Hugging Face मॉडल का उपयोग करें** जो पहली बार खुद डाउनलोड हो जाता है, और **स्कैन से टेक्स्ट पहचानें** जिसमें स्वचालित रूप से विराम चिह्न जोड़े जाते हैं। पूरा स्क्रिप्ट कॉपी‑पेस्ट, अपने पाथ्स समायोजित करने और चलाने के लिए तैयार है।

## अगले कदम और संबंधित विषय  

- **Batch post‑processing**: तेज़ बुल्क हैंडलिंग के लिए `ocr_engine.run_batch_postprocessor` को एक्सप्लोर करें।  
- **Alternative models**: यदि आपको OCR के साथ स्पीच‑टू‑टेक्स्ट चाहिए तो `openai/whisper` फ़ैमिली आज़माएँ।  
- **Integration with databases**: निकाले गए टेक्स्ट को SQLite या Elasticsearch में स्टोर करें ताकि सर्चेबल आर्काइव बन सके।  

बिल्कुल प्रयोग करें—मॉडल बदलें, `gpu_layers` को ट्यून करें, या अपना पोस्ट‑प्रोसेसर जोड़ें। Aspose OCR की लचीलापन और Hugging Face के मॉडल हब का संयोजन इसे किसी भी दस्तावेज़‑डिजिटलीकरण प्रोजेक्ट के लिए एक बहुमुखी आधार बनाता है।

---

*हैप्पी कोडिंग! यदि आपको कोई समस्या आती है, तो नीचे कमेंट करें या गहरी कॉन्फ़िगरेशन विकल्पों के लिए Aspose OCR दस्तावेज़ देखें।*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}