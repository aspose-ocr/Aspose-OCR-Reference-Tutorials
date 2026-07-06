---
category: general
date: 2026-02-22
description: जानें कि OCR टेक्स्ट को कैसे निकालें और AI पोस्ट‑प्रोसेसिंग के साथ OCR
  की सटीकता को कैसे सुधारें। Python में चरण‑दर‑चरण उदाहरण के साथ OCR टेक्स्ट को आसानी
  से साफ़ करें।
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: hi
og_description: जानेँ कि कैसे OCR टेक्स्ट निकालें, OCR की सटीकता बढ़ाएँ, और AI पोस्ट‑प्रोसेसिंग
  के साथ एक सरल Python वर्कफ़्लो का उपयोग करके OCR टेक्स्ट को साफ़ करें।
og_title: OCR टेक्स्ट कैसे निकालें – चरण‑दर‑चरण गाइड
tags:
- OCR
- AI
- Python
title: OCR टेक्स्ट निकालने का पूर्ण गाइड
url: /hi/python/general/how-to-extract-ocr-text-complete-guide/
---

craft final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR टेक्स्ट निकालने का तरीका – पूर्ण प्रोग्रामिंग ट्यूटोरियल

क्या आपने कभी सोचा है **OCR कैसे निकालें** स्कैन किए गए दस्तावेज़ से, बिना टाइपो और टूटे हुए लाइनों की गड़बड़ी के? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में OCR इंजन का कच्चा आउटपुट एक बिखरा हुआ पैराग्राफ जैसा दिखता है, और उसे साफ़ करना एक झंझट जैसा लगता है।  

अच्छी खबर? इस गाइड को फॉलो करके आप संरचित OCR डेटा निकालने, एक AI पोस्ट‑प्रोसेसर चलाने, और **साफ़ OCR टेक्स्ट** प्राप्त करने का व्यावहारिक तरीका देखेंगे, जो आगे के विश्लेषण के लिए तैयार होगा। हम **OCR की सटीकता सुधारने** की तकनीकों पर भी चर्चा करेंगे ताकि परिणाम पहली बार में ही भरोसेमंद हों।

आने वाले कुछ मिनटों में हम सब कुछ कवर करेंगे: आवश्यक लाइब्रेरीज़, एक पूरी चलाने योग्य स्क्रिप्ट, और सामान्य pitfalls से बचने के टिप्स। कोई अस्पष्ट “डॉक्यूमेंट देखें” शॉर्टकट नहीं—सिर्फ एक पूर्ण, स्व-समावेशी समाधान जिसे आप कॉपी‑पेस्ट करके चला सकते हैं।

## आपको क्या चाहिए

- Python 3.9+ (कोड टाइप हिंट्स का उपयोग करता है लेकिन पुराने 3.x संस्करणों पर भी चलता है)
- एक OCR इंजन जो संरचित परिणाम दे सके (जैसे `pytesseract` के साथ `--psm 1` फ़्लैग वाला Tesseract, या कोई कमर्शियल API जो ब्लॉक/लाइन मेटाडेटा प्रदान करता हो)
- एक AI पोस्ट‑प्रोसेसिंग मॉडल – इस उदाहरण में हम इसे एक साधारण फ़ंक्शन से मॉक करेंगे, लेकिन आप OpenAI के `gpt‑4o-mini`, Claude, या कोई भी LLM जो टेक्स्ट लेता है और साफ़ आउटपुट देता है, का उपयोग कर सकते हैं
- परीक्षण के लिए कुछ नमूना इमेज (PNG/JPG) की लाइन्स

यदि ये सब तैयार है, तो चलिए शुरू करते हैं।

## OCR निकालने का तरीका – प्रारंभिक प्राप्ति

पहला कदम OCR इंजन को कॉल करना और उससे **संरचित प्रतिनिधित्व** माँगना है, न कि साधारण स्ट्रिंग। संरचित परिणाम ब्लॉक, लाइन, और शब्द की सीमाओं को संरक्षित रखते हैं, जिससे बाद की सफ़ाई बहुत आसान हो जाती है।

```python
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List

# Simple data classes mirroring a typical structured OCR response
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

def recognize_structured(image_path: str) -> StructuredResult:
    """
    Run Tesseract with the `--psm 1` layout mode to get block/line info.
    In a real engine you would get JSON directly; here we simulate it.
    """
    img = Image.open(image_path)

    # Tesseract's TSV output includes level, page_num, block_num, par_num, line_num, word_num, text…
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    current_block_idx = -1
    current_line_idx = -1

    for i, level in enumerate(tsv["level"]):
        if level == 3:  # block level
            result.blocks.append(Block())
            current_block_idx += 1
            current_line_idx = -1
        elif level == 4:  # line level
            result.blocks[current_block_idx].lines.append(Line(text=""))
            current_line_idx += 1

        # level 5 is word; concatenate words into the current line
        if level == 5:
            word = tsv["text"][i]
            if word.strip():
                line_obj = result.blocks[current_block_idx].lines[current_line_idx]
                line_obj.text += (word + " ")

    # Trim trailing spaces
    for block in result.blocks:
        for line in block.lines:
            line.text = line.text.strip()
    return result
```

> **क्यों महत्वपूर्ण है:** ब्लॉकों और लाइनों को संरक्षित करके हम पैराग्राफ की शुरुआत का अनुमान लगाने की ज़रूरत नहीं पड़ती। `recognize_structured` फ़ंक्शन हमें एक साफ़ हायरार्की देता है जिसे बाद में AI मॉडल में फीड किया जा सकता है।

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

स्निपेट चलाने पर पहली लाइन ठीक उसी तरह प्रिंट होती है जैसी OCR इंजन ने देखी थी, जिसमें अक्सर “0cr” जैसी गलत पहचानें “OCR” की जगह होती हैं।

## AI पोस्ट‑प्रोसेसिंग के साथ OCR सटीकता सुधारें

अब जब हमारे पास कच्चा संरचित आउटपुट है, चलिए इसे AI पोस्ट‑प्रोसेसर को देते हैं। लक्ष्य **OCR की सटीकता सुधारना** है, सामान्य गलतियों को ठीक करके, विराम चिह्नों को सामान्यीकृत करके, और आवश्यकता पड़ने पर लाइनों को पुनः‑सेगमेंट करके।

```python
import openai  # Example: using OpenAI's API; replace with your provider

def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    """
    Sends each line to an LLM that returns a cleaned version.
    This simple loop can be parallelized for large documents.
    """
    api_key = "YOUR_OPENAI_API_KEY"
    openai.api_key = api_key

    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "You are an OCR cleanup assistant. Fix any spelling, spacing, "
                "or punctuation errors in the following line while preserving the original meaning:\n\n"
                f"\"{line.text}\""
            )
            response = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=200,
            )
            cleaned = response.choices[0].message.content.strip()
            line.text = cleaned
    return structured
```

> **प्रो टिप:** यदि आपके पास LLM की सब्सक्रिप्शन नहीं है, तो कॉल को स्थानीय ट्रांसफ़ॉर्मर (जैसे `sentence‑transformers` + फाइन‑ट्यून्ड करेक्शन मॉडल) या यहाँ तक कि नियम‑आधारित दृष्टिकोण से बदल सकते हैं। मुख्य विचार यह है कि AI प्रत्येक लाइन को अलग‑अलग देखता है, जो आमतौर पर **OCR टेक्स्ट साफ़ करने** के लिए पर्याप्त होता है।

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

अब आपको एक बहुत ही साफ़ वाक्य दिखना चाहिए—टाइपो हटे, अतिरिक्त स्पेस हटे, और विराम चिह्न ठीक हुए।

## बेहतर परिणामों के लिए OCR टेक्स्ट साफ़ करें

AI सुधार के बाद भी आप एक अंतिम सफ़ाई चरण लागू करना चाह सकते हैं: गैर‑ASCII कैरेक्टर्स हटाएँ, लाइन ब्रेक्स को統一 करें, और कई स्पेसेज़ को एक में बदलें। यह अतिरिक्त पास सुनिश्चित करता है कि आउटपुट आगे के कार्यों जैसे NLP या डेटाबेस इन्गेशन के लिए तैयार है।

```python
import re

def final_cleanup(structured: StructuredResult) -> str:
    """
    Flattens the hierarchy into a single string and performs
    additional regex‑based cleaning.
    """
    lines = []
    for block in structured.blocks:
        for line in block.lines:
            # Remove any lingering non‑printable characters
            cleaned = re.sub(r"[^\x20-\x7E]", "", line.text)
            # Collapse multiple spaces
            cleaned = re.sub(r"\s+", " ", cleaned).strip()
            lines.append(cleaned)
    # Join blocks with double newline to preserve paragraph breaks
    return "\n\n".join(lines)

clean_text = final_cleanup(structured_result)
print("\n=== Cleaned OCR Text ===\n")
print(clean_text)
```

`final_cleanup` फ़ंक्शन आपको एक साधारण स्ट्रिंग देता है जिसे आप सीधे सर्च इंडेक्स, भाषा मॉडल, या CSV एक्सपोर्ट में फीड कर सकते हैं। क्योंकि हमने ब्लॉक सीमाओं को बरकरार रखा है, पैराग्राफ की संरचना बनी रहती है।

## एज केस और क्या‑अगर स्थितियाँ

- **मल्टी‑कॉलम लेआउट:** यदि स्रोत में कॉलम हैं, तो OCR इंजन लाइनों को इंटरलीव कर सकता है। आप TSV आउटपुट से कॉलम कोऑर्डिनेट्स निकालकर लाइनों को पुनः‑क्रमित कर सकते हैं, फिर AI को भेजें।
- **नॉन‑लैटिन स्क्रिप्ट्स:** चीनी या अरबी जैसी भाषाओं के लिए, LLM के प्रॉम्प्ट को भाषा‑विशिष्ट सुधार के लिए बदलें, या उस स्क्रिप्ट पर फाइन‑ट्यून्ड मॉडल का उपयोग करें।
- **बड़े दस्तावेज़:** प्रत्येक लाइन को अलग‑अलग भेजना धीमा हो सकता है। लाइनों को बैच करें (जैसे 10 प्रति अनुरोध) और LLM को साफ़ लाइनों की सूची लौटाने दें। टोकन लिमिट का ध्यान रखें।
- **मिसिंग ब्लॉक्स:** कुछ OCR इंजन केवल शब्दों की फ्लैट लिस्ट देते हैं। ऐसे में आप समान `line_num` वाले शब्दों को समूहित करके लाइनों का पुनर्निर्माण कर सकते हैं।

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ मिलाकर, यहाँ एक सिंगल फ़ाइल है जिसे आप एंड‑टू‑एंड चला सकते हैं। प्लेसहोल्डर्स को अपने API की और इमेज पाथ से बदलें।

```python
# ocr_cleanup.py
import re
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List
import openai

# ---------- Data structures ----------
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

# ---------- Step 1: Extract OCR ----------
def recognize_structured(image_path: str) -> StructuredResult:
    img = Image.open(image_path)
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    cur_block = -1
    cur_line = -1

    for i, lvl in enumerate(tsv["level"]):
        if lvl == 3:                # block
            result.blocks.append(Block())
            cur_block += 1
            cur_line = -1
        elif lvl == 4:              # line
            result.blocks[cur_block].lines.append(Line(text=""))
            cur_line += 1
        elif lvl == 5:              # word
            word = tsv["text"][i]
            if word.strip():
                result.blocks[cur_block].lines[cur_line].text += word + " "

    # Trim spaces
    for blk in result.blocks:
        for ln in blk.lines:
            ln.text = ln.text.strip()
    return result

# ---------- Step 2: AI post‑processor ----------
def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    openai.api_key = "YOUR_OPENAI_API_KEY"
    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "Correct OCR errors (spelling, spacing, punctuation) in this line:\n"
                f"\"{line.text}\""
            )
            resp = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=150,
            )
            line.text = resp.choices[0].message.content.strip()
    return structured

# ---------- Step 3: Final cleanup ----------
def final_cleanup(structured: StructuredResult) -> str:
    out = []
    for block in structured.blocks:
        for line in block.lines:
            txt = re.sub(r"[^\x20-\x7E]", "", line.text)   # strip non‑ASCII
            txt = re.sub(r"\s+", " ", txt).strip

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}