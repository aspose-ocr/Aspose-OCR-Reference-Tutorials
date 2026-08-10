---
category: general
date: 2026-05-03
description: Python OCR ट्यूटोरियल जो दिखाता है कि PNG इमेज फ़ाइलें कैसे लोड करें,
  छवि से टेक्स्ट पहचानें और बैच OCR प्रोसेसिंग के लिए मुफ्त AI संसाधन प्रदान करता
  है।
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: hi
og_description: Python OCR ट्यूटोरियल आपको PNG छवियों को लोड करने, छवि से टेक्स्ट
  पहचानने और बैच OCR प्रोसेसिंग के लिए मुफ्त AI संसाधनों को संभालने के चरणों से परिचित
  कराता है।
og_title: Python OCR ट्यूटोरियल – मुफ्त AI संसाधनों के साथ तेज़ बैच OCR
tags:
- OCR
- Python
- AI
title: पायथन OCR ट्यूटोरियल – बैच OCR प्रोसेसिंग को आसान बनाना
url: /hi/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR ट्यूटोरियल – बैच OCR प्रोसेसिंग आसान बनाएं

क्या आपको कभी ऐसा **python ocr tutorial** चाहिए था जो वास्तव में आपको सैकड़ों PNG फ़ाइलों पर OCR चलाने दे बिना सिर दर्द के? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में आपको **load png image** फ़ाइलें लोड करनी पड़ती हैं, उन्हें इंजन में फीड करना होता है, और काम खत्म होने पर AI संसाधनों को साफ़ करना होता है।

इस गाइड में हम एक पूर्ण, तुरंत चलने योग्य उदाहरण के माध्यम से दिखाएंगे कि कैसे **recognize text from image** फ़ाइलों को बैच में प्रोसेस किया जाए और अंतर्निहित AI मेमोरी को मुक्त किया जाए। अंत तक आपके पास एक स्व-समाहित स्क्रिप्ट होगी जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं—कोई अतिरिक्त झंझट नहीं, सिर्फ़ आवश्यक बातें।

## What You’ll Need

- Python 3.10 या नया (यहाँ उपयोग किया गया सिंटैक्स f‑strings और type hints पर निर्भर करता है)  
- एक OCR लाइब्रेरी जो `engine.recognize` मेथड प्रदान करती हो – डेमो के लिए हम एक काल्पनिक `aocr` पैकेज मानेंगे, लेकिन आप इसे Tesseract, EasyOCR आदि से बदल सकते हैं  
- कोड स्निपेट में दिखाया गया `ai` हेल्पर मॉड्यूल (यह मॉडल इनिशियलाइज़ेशन और रिसोर्स क्लीनअप संभालता है)  
- वह फ़ोल्डर जिसमें आप प्रोसेस करना चाहते हैं कई PNG फ़ाइलें हों  

यदि आपके पास `aocr` या `ai` स्थापित नहीं है, तो आप उन्हें स्टब्स के साथ मॉक कर सकते हैं – अंत में “Optional Stubs” सेक्शन देखें।

## Step 1: Initialize the AI Engine (Free AI Resources)

कोई भी इमेज OCR पाइपलाइन में फीड करने से पहले, अंतर्निहित मॉडल तैयार होना चाहिए। केवल एक बार इनिशियलाइज़ करने से मेमोरी बचती है और बैच जॉब्स तेज़ होते हैं।

```python
# step_1_initialize.py
import ai                # hypothetical helper that wraps the AI model
import aocr               # OCR library

def init_engine(config_path: str = "config.yaml"):
    """
    Initialize the AI engine if it hasn't been set up yet.
    This uses free AI resources – the engine will be released later.
    """
    if not ai.is_initialized():
        ai.initialize(config_path)   # auto‑initialize with the provided configuration
    else:
        print("Engine already initialized.")
```

**क्यों यह महत्वपूर्ण है:**  
`ai.initialize` को प्रत्येक इमेज के लिए बार‑बार कॉल करने से GPU मेमोरी बार‑बार अलोकेट होगी, अंत में स्क्रिप्ट क्रैश हो जाएगी। `ai.is_initialized()` की जाँच करके हम एक ही अलोकेशन सुनिश्चित करते हैं – यही “free AI resources” सिद्धांत है।

## Step 2: Load PNG Image Files for Batch OCR Processing

अब हम सभी PNG फ़ाइलें इकट्ठा करते हैं जिन्हें OCR के माध्यम से चलाना है। `pathlib` का उपयोग कोड को OS‑अग्नॉस्टिक रखता है।

```python
# step_2_load_images.py
from pathlib import Path
from typing import List

def collect_png_paths(directory: str) -> List[Path]:
    """
    Scan `directory` and return a list of Path objects pointing to PNG files.
    """
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files
```

**एज केस:**  
यदि फ़ोल्डर में गैर‑PNG फ़ाइलें (जैसे JPEG) हों तो उन्हें अनदेखा किया जाएगा, जिससे `engine.recognize` किसी असमर्थित फ़ॉर्मेट पर अटक नहीं पाएगा।

## Step 3: Run OCR on Each Image and Apply Post‑Processing

इंजन तैयार है और फ़ाइल सूची तैयार है, अब हम इमेजेज़ पर लूप कर सकते हैं, कच्चा टेक्स्ट निकाल सकते हैं, और उसे पोस्ट‑प्रोसेसर को दे सकते हैं जो सामान्य OCR आर्टिफैक्ट्स (जैसे अनावश्यक लाइन ब्रेक) को साफ़ करता है।

```python
# step_3_ocr_batch.py
import aocr
import ai
from pathlib import Path
from typing import List

def ocr_batch(image_paths: List[Path]) -> List[str]:
    """
    Perform OCR on each PNG image and return a list of cleaned strings.
    """
    results = []
    for image_path in image_paths:
        # Load the image – aocr.Image.load abstracts away Pillow/OpenCV details
        img = aocr.Image.load(str(image_path))
        
        # Recognize raw text
        raw_text = engine.recognize(img)
        
        # Refine the raw OCR output using the AI post‑processor
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters extracted.")
    
    return results
```

**हम लोडिंग को रिकग्निशन से अलग क्यों करते हैं:**  
`aocr.Image.load` लेज़ी डिकोडिंग कर सकता है, जो बड़े बैच के लिए तेज़ है। लोड स्टेप को स्पष्ट रखने से बाद में JPEG या TIFF फ़ाइलों को संभालने के लिए किसी अलग इमेज लाइब्रेरी में स्विच करना आसान हो जाता है।

## Step 4: Clean Up – Free AI Resources After the Batch

बैच पूरा होने के बाद, हमें मॉडल को रिलीज़ करना चाहिए ताकि मेमोरी लीक्स न हों, विशेषकर GPU‑सक्षम मशीनों पर।

```python
# step_4_cleanup.py
import ai

def release_resources():
    """
    Free any allocated AI resources. Safe to call multiple times.
    """
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources have been released.")
    else:
        print("No AI resources were allocated.")
```

## Putting It All Together – The Complete Script

नीचे एक सिंगल फ़ाइल है जो चारों स्टेप्स को एक सुसंगत वर्कफ़्लो में जोड़ती है। इसे `batch_ocr.py` के रूप में सेव करें और कमांड लाइन से चलाएँ।

```python
# batch_ocr.py
"""
Python OCR tutorial – end‑to‑end batch OCR processing.
Loads PNG images, runs OCR, post‑processes results, and frees AI resources.
"""

import sys
from pathlib import Path
import ai
import aocr

# ----------------------------------------------------------------------
# Helper functions (copied from the steps above)
# ----------------------------------------------------------------------
def init_engine(cfg: str = "config.yaml"):
    if not ai.is_initialized():
        ai.initialize(cfg)
    else:
        print("Engine already initialized.")

def collect_png_paths(directory: str):
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files

def ocr_batch(image_paths):
    results = []
    for image_path in image_paths:
        img = aocr.Image.load(str(image_path))
        raw_text = engine.recognize(img)
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters.")
    return results

def release_resources():
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources released.")
    else:
        print("No resources to release.")

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-png>")
        sys.exit(1)

    image_dir = sys.argv[1]

    try:
        init_engine()
        png_paths = collect_png_paths(image_dir)
        texts = ocr_batch(png_paths)

        # Optional: write results to a single text file
        output_file = Path("ocr_results.txt")
        with output_file.open("w", encoding="utf-8") as f:
            for path, txt in zip(png_paths, texts):
                f.write(f"--- {path.name} ---\n")
                f.write(txt + "\n\n")
        print(f"All results saved to {output_file.resolve()}")
    finally:
        release_resources()
```

### Expected Output

तीन PNG फ़ाइलों वाले फ़ोल्डर के खिलाफ स्क्रिप्ट चलाने पर यह आउटपुट दे सकता है:

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

`ocr_results.txt` फ़ाइल प्रत्येक इमेज के लिए एक स्पष्ट डिलिमिटर के साथ साफ़ किया गया OCR टेक्स्ट रखेगी।

## Optional Stubs for aocr & ai (If You Don’t Have Real Packages)

यदि आप भारी OCR लाइब्रेरीज़ को इम्पोर्ट किए बिना फ्लो टेस्ट करना चाहते हैं, तो आप न्यूनतम मॉक मॉड्यूल बना सकते हैं:

```python
# aocr/__init__.py
class Image:
    @staticmethod
    def load(path):
        return f"ImageObject({path})"

def dummy_recognize(image):
    return "Raw OCR output for " + str(image)

engine = type("Engine", (), {"recognize": dummy_recognize})()
```

```python
# ai/__init__.py
_state = {"initialized": False}

def is_initialized():
    return _state["initialized"]

def initialize(cfg):
    print(f"Initializing AI engine with {cfg}")
    _state["initialized"] = True

def run_postprocessor(text):
    # Very naive cleanup: strip extra spaces
    return " ".join(text.split())

def free_resources():
    print("Freeing AI resources")
    _state["initialized"] = False
```

इन फ़ोल्डरों को `batch_ocr.py` के बगल में रखें और स्क्रिप्ट चलाएगी, मॉक परिणाम प्रिंट करेगी।

## Pro Tips & Common Pitfalls

- **Memory spikes:** यदि आप हजारों हाई‑रिज़ॉल्यूशन PNG प्रोसेस कर रहे हैं, तो OCR से पहले उनका आकार बदलने पर विचार करें। `aocr.Image.load` अक्सर `max_size` आर्ग्यूमेंट स्वीकार करता है।  
- **Unicode handling:** हमेशा आउटपुट फ़ाइल को `encoding="utf-8"` के साथ खोलें; OCR इंजन गैर‑ASCII कैरेक्टर्स भी आउटपुट कर सकते हैं।  
- **Parallelism:** CPU‑बाउंड OCR के लिए आप `ocr_batch` को `concurrent.futures.ThreadPoolExecutor` में रैप कर सकते हैं। बस यह याद रखें कि एक ही `ai` इंस्टेंस रखें – कई थ्रेड्स जो प्रत्येक `ai.initialize` कॉल करते हैं, “free AI resources” लक्ष्य को नष्ट कर देते हैं।  
- **Error resilience:** प्रति‑इमेज लूप को `try/except` ब्लॉक में रखें ताकि एक ही करप्ट PNG पूरी बैच को रोक न सके।

## Conclusion

अब आपके पास एक **python ocr tutorial** है जो दिखाता है कैसे **load png image** फ़ाइलें लोड करें, **batch OCR processing** करें, और जिम्मेदारी से **free AI resources** मैनेज करें। पूर्ण, रन करने योग्य उदाहरण ठीक‑ठीक दिखाता है कैसे **recognize text from image** ऑब्जेक्ट्स को प्रोसेस किया जाए और बाद में क्लीन‑अप किया जाए, ताकि आप इसे अपने प्रोजेक्ट्स में कॉपी‑पेस्ट कर सकें बिना किसी हिस्से की कमी की तलाश किए।

अगले कदम के लिए तैयार हैं? स्टब्ड `aocr` और `ai` मॉड्यूल को वास्तविक लाइब्रेरीज़ जैसे `pytesseract` और `torchvision` से बदलें। आप स्क्रिप्ट को JSON आउटपुट, डेटाबेस में परिणाम पुश करना, या क्लाउड स्टोरेज बकेट के साथ इंटीग्रेट करने के लिए भी विस्तारित कर सकते हैं। संभावनाएँ अनंत हैं—हैप्पी कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}