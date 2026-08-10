---
category: general
date: 2026-04-26
description: OCR परिणामों को पोस्ट‑प्रोसेस कैसे करें और निर्देशांक के साथ टेक्स्ट
  निकालें। संरचित आउटपुट और AI सुधार का उपयोग करके चरण‑दर‑चरण समाधान सीखें।
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: hi
og_description: OCR परिणामों को पोस्ट‑प्रोसेस कैसे करें और कोऑर्डिनेट्स के साथ टेक्स्ट
  निकालें। विश्वसनीय वर्कफ़्लो के लिए इस व्यापक ट्यूटोरियल का पालन करें।
og_title: OCR को पोस्ट‑प्रोसेस कैसे करें – पूर्ण गाइड
tags:
- OCR
- Python
- AI
- Text Extraction
title: OCR को पोस्ट‑प्रोसेस कैसे करें – पाइथन में निर्देशांक के साथ टेक्स्ट निकालें
url: /hi/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR को पोस्ट‑प्रोसेस कैसे करें – Python में कॉर्डिनेट्स के साथ टेक्स्ट निकालें

क्या आपको कभी **how to post‑process OCR** परिणामों की जरूरत पड़ी है क्योंकि कच्चा आउटपुट शोरयुक्त या गलत‑संरेखित था? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स—इनवॉइस स्कैनिंग, रसीद डिजिटाइज़ेशन, या यहाँ तक कि AR अनुभवों को बढ़ाने में—OCR इंजन आपको कच्चे शब्द देता है, लेकिन आपको उन्हें साफ़ करना पड़ता है और यह ट्रैक रखना पड़ता है कि प्रत्येक शब्द पेज पर कहाँ स्थित है। यही वह जगह है जहाँ एक structured output मोड और AI‑ड्रिवेन पोस्ट‑प्रोसेसर मिलकर चमकते हैं।

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य Python पाइपलाइन के माध्यम से जाएंगे जो एक इमेज से **extracts text with coordinates** निकालता है, AI‑आधारित सुधार चरण चलाता है, और प्रत्येक शब्द को उसके (x, y) स्थान के साथ प्रिंट करता है। कोई गायब इम्पोर्ट नहीं, कोई अस्पष्ट “see the docs” शॉर्टकट नहीं—बस एक स्व-निहित समाधान जिसे आप आज ही अपने प्रोजेक्ट में डाल सकते हैं।

> **Pro tip:** यदि आप कोई अलग OCR लाइब्रेरी उपयोग कर रहे हैं, तो “structured” या “layout” मोड देखें; अवधारणाएँ वही रहती हैं।

---

## आवश्यकताएँ

शुरू करने से पहले, सुनिश्चित करें कि आपके पास है:

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | आधुनिक सिंटैक्स और टाइप हिंट्स |
| `ocr` library that supports `OutputMode.STRUCTURED` (e.g., a fictional `myocr`) | बाउंडिंग‑बॉक्स डेटा के लिए आवश्यक |
| An AI post‑processing module (could be OpenAI, HuggingFace, or a custom model) | OCR के बाद सटीकता में सुधार करता है |
| An image file (`input.png`) in your working directory | वह स्रोत जिसे हम पढ़ेंगे |

यदि इनमें से कोई भी अपरिचित लग रहा है, तो बस प्लेसहोल्डर पैकेज `pip install myocr ai‑postproc` से इंस्टॉल करें। नीचे दिया गया कोड भी फॉलबैक स्टब्स शामिल करता है ताकि आप वास्तविक लाइब्रेरीज़ के बिना फ्लो का परीक्षण कर सकें।

## चरण 1: OCR इंजन के लिए Structured Output मोड सक्षम करें  

पहला काम हम OCR इंजन को यह बताना है कि वह हमें केवल साधारण टेक्स्ट से अधिक दे। Structured output प्रत्येक शब्द को उसके बाउंडिंग बॉक्स और कॉन्फिडेंस स्कोर के साथ लौटाता है, जो बाद में **extract text with coordinates** के लिए आवश्यक है।

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*Why this matters:* बिना structured मोड के आपको केवल एक लंबी स्ट्रिंग मिलेगी, और आप वह स्पैशियल जानकारी खो देंगे जो इमेज पर टेक्स्ट ओवरले करने या डाउनस्ट्रीम लेआउट विश्लेषण के लिए आवश्यक है।

## चरण 2: इमेज को पहचानें और शब्द, बॉक्स, तथा कॉन्फिडेंस कैप्चर करें  

अब हम इमेज को इंजन में फीड करते हैं। परिणाम एक ऑब्जेक्ट है जिसमें शब्द ऑब्जेक्ट्स की सूची होती है, प्रत्येक `text`, `x`, `y`, `width`, `height`, और `confidence` को एक्सपोज़ करता है।

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*Edge case:* यदि इमेज खाली या पढ़ने योग्य नहीं है, तो `structured_result.words` एक खाली सूची होगी। इसे जांचना और सुगमता से हैंडल करना अच्छा अभ्यास है।

## चरण 3: स्थितियों को संरक्षित रखते हुए AI‑आधारित पोस्ट‑प्रोसेसिंग चलाएँ  

भले ही सबसे अच्छे OCR इंजन भी गलतियाँ करते हैं—जैसे “O” बनाम “0” या लापता डायक्रिटिक्स। डोमेन‑स्पेसिफिक टेक्स्ट पर प्रशिक्षित AI मॉडल उन त्रुटियों को सुधार सकता है। महत्वपूर्ण बात यह है कि हम मूल कॉर्डिनेट्स को रखते हैं ताकि स्पैशियल लेआउट अपरिवर्तित रहे।

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*Why we preserve coordinates:* कई डाउनस्ट्रीम टास्क (जैसे PDF जेनरेशन, AR लेबलिंग) सटीक प्लेसमेंट पर निर्भर करते हैं। AI केवल `text` फील्ड को बदलता है, `x`, `y`, `width`, `height` को अपरिवर्तित छोड़ता है।

## चरण 4: सुधारे गए शब्दों पर इटरेट करें और उनके टेक्स्ट को कॉर्डिनेट्स के साथ दिखाएँ  

अंत में, हम सुधारे गए शब्दों पर लूप लगाते हैं और प्रत्येक शब्द को उसके टॉप‑लेफ़्ट कोने `(x, y)` के साथ प्रिंट करते हैं। यह **extract text with coordinates** लक्ष्य को पूरा करता है।

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**अपेक्षित आउटपुट (उदाहरण):**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

प्रत्येक लाइन सुधारे गए शब्द और मूल इमेज पर उसका सटीक स्थान दिखाती है।

## पूर्ण कार्यशील उदाहरण  

नीचे एक एकल स्क्रिप्ट है जो सब कुछ जोड़ती है। आप इसे कॉपी‑पेस्ट कर सकते हैं, इम्पोर्ट स्टेटमेंट्स को अपनी वास्तविक लाइब्रेरीज़ के अनुसार समायोजित कर सकते हैं, और सीधे चला सकते हैं।

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**स्क्रिप्ट चलाना**

```bash
python ocr_postprocess_demo.py
```

यदि आपके पास वास्तविक लाइब्रेरीज़ इंस्टॉल हैं, तो स्क्रिप्ट आपके `input.png` को प्रोसेस करेगी। अन्यथा, स्टब इम्प्लीमेंटेशन आपको कोई बाहरी डिपेंडेंसी बिना अपेक्षित फ्लो और आउटपुट देखने देती है।

## अक्सर पूछे जाने वाले प्रश्न (FAQ)

| Question | Answer |
|----------|--------|
| *क्या यह Tesseract के साथ काम करता है?* | Tesseract स्वयं बॉक्स से बाहर कोई structured मोड प्रदान नहीं करता, लेकिन `pytesseract.image_to_data` जैसे रैपर्स बाउंडिंग बॉक्स लौटाते हैं जिन्हें आप उसी AI पोस्ट‑प्रोसेसर में फीड कर सकते हैं। |
| *यदि मुझे टॉप‑लेफ़्ट के बजाय बॉटम‑राइट कोना चाहिए तो?* | प्रत्येक शब्द ऑब्जेक्ट `width` और `height` भी प्रदान करता है। विपरीत कोना पाने के लिए `x2 = x + width` और `y2 = y + height` गणना करें। |
| *क्या मैं कई इमेजेज को बैच‑प्रोसेस कर सकता हूँ?* | बिल्कुल। चरणों को `for image_path in Path("folder").glob("*.png"):` लूप में रैप करें और प्रत्येक फ़ाइल के परिणाम एकत्र करें। |
| *सुधार के लिए मैं कौन सा AI मॉडल चुनूँ?* | सामान्य टेक्स्ट के लिए, OCR त्रुटियों पर फाइन‑ट्यून किया गया छोटा GPT‑2 काम करता है। डोमेन‑स्पेसिफिक डेटा (जैसे, मेडिकल प्रिस्क्रिप्शन) के लिए, शोर‑साफ़ डेटा पर पेयर्ड सीक्वेंस‑टू‑सीक्वेंस मॉडल ट्रेन करें। |
| *AI सुधार के बाद कॉन्फिडेंस स्कोर उपयोगी है?* | आप डिबगिंग के लिए अभी भी मूल कॉन्फिडेंस रख सकते हैं, लेकिन यदि मॉडल समर्थन करता है तो AI अपना स्वयं का कॉन्फिडेंस आउटपुट कर सकता है। |

## किनारे के मामले और सर्वोत्तम प्रथाएँ  

1. **खाली या भ्रष्ट इमेजेज** – आगे बढ़ने से पहले हमेशा सत्यापित करें कि `structured_result.words` खाली नहीं है।  
2. **नॉन‑लैटिन स्क्रिप्ट्स** – सुनिश्चित करें कि आपका OCR इंजन लक्ष्य भाषा के लिए कॉन्फ़िगर किया गया है; AI पोस्ट‑प्रोसेसर को उसी स्क्रिप्ट पर प्रशिक्षित होना चाहिए।  
3. **परफॉर्मेंस** – AI सुधार महंगा हो सकता है। यदि आप वही इमेज पुनः उपयोग करेंगे तो परिणामों को कैश करें, या AI चरण को असिंक्रोनस चलाएँ।  
4. **कोऑर्डिनेट सिस्टम** – OCR लाइब्रेरीज़ विभिन्न मूल बिंदु (टॉप‑लेफ़्ट बनाम बॉटम‑लेफ़्ट) उपयोग कर सकती हैं। PDF या कैनवस पर ओवरले करते समय तदनुसार समायोजित करें।  

## निष्कर्ष  

अब आपके पास **how to post‑process OCR** और विश्वसनीय रूप से **extract text with coordinates** के लिए एक ठोस, एंड‑टू‑एंड रेसिपी है। Structured output को सक्षम करके, परिणाम को AI सुधार लेयर से गुजारकर, और मूल बाउंडिंग बॉक्स को संरक्षित रखकर, आप शोरयुक्त OCR स्कैन को साफ़, स्पैशियल‑अवेयर टेक्स्ट में बदल सकते हैं जो PDF जेनरेशन, डेटा एंट्री ऑटोमेशन, या ऑगमेंटेड‑रियलिटी ओवरले जैसे डाउनस्ट्रीम टास्क के लिए तैयार है।

अगले कदम के लिए तैयार? स्टब AI को OpenAI `gpt‑4o‑mini` कॉल से बदलें, या पाइपलाइन को FastAPI में इंटीग्रेट करें।

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}