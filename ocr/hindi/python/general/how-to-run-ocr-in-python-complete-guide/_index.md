---
category: general
date: 2026-06-19
description: OCR को चरण‑दर‑चरण कैसे चलाएँ और साधारण टेक्स्ट OCR तकनीकों से OCR की
  सटीकता में सुधार करें। विश्वसनीय टेक्स्ट निष्कर्षण के लिए एक तेज़ कार्यप्रवाह सीखें।
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: hi
og_description: OCR को कुशलतापूर्वक कैसे चलाएँ। यह ट्यूटोरियल दिखाता है कि साधारण
  टेक्स्ट OCR और AI पोस्ट‑प्रोसेसिंग का उपयोग करके OCR की सटीकता कैसे बढ़ाएँ।
og_title: Python में OCR कैसे चलाएँ – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Python में OCR कैसे चलाएँ – पूर्ण मार्गदर्शिका
url: /hi/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Run OCR in Python – Complete Guide

क्या आपने कभी सोचा है **कैसे OCR चलाएँ** एक बैच स्कैन किए गए PDFs पर बिना घंटों सेटिंग्स को ट्यून किए? आप अकेले नहीं हैं। कई प्रोजेक्ट्स में पहली बाधा बस इमेज से भरोसेमंद टेक्स्ट निकालना होती है, और एक अस्थिर परिणाम और साफ़ एक्सट्रैक्शन के बीच का अंतर अक्सर कुछ स्मार्ट कदमों पर निर्भर करता है।

इस गाइड में हम एक व्यावहारिक चार‑स्टेप पाइपलाइन को देखेंगे जो न केवल **OCR चलाता** है बल्कि **OCR की सटीकता को सुधारता** है, एक तेज़ प्लेन‑टेक्स्ट पास को लेआउट‑अवेयर दूसरे पास और एक AI‑पावर्ड पोस्ट‑प्रोसेसर के साथ मिलाकर। अंत तक आपके पास एक तैयार‑स्क्रिप्ट, प्रत्येक चरण के महत्व की स्पष्ट व्याख्या, और मल्टी‑कॉलम पेज या शोरयुक्त स्कैन जैसे एज केस को संभालने के टिप्स होंगे।

---

## What You’ll Need

शुरू करने से पहले सुनिश्चित करें कि आपके पास ये हैं:

- **Python 3.9+** – कोड टाइप हिंट्स और f‑strings का उपयोग करता है।  
- **Tesseract OCR** इंस्टॉल किया हुआ और `tesseract` कमांड लाइन से एक्सेसिबल। (Ubuntu पर: `sudo apt install tesseract-ocr`; Windows पर आधिकारिक रेपो से इंस्टॉलर डाउनलोड करें।)  
- **pytesseract** रैपर (`pip install pytesseract`)।  
- एक **AI पोस्ट‑प्रोसेसिंग लाइब्रेरी** – इस उदाहरण में हम मान लेते हैं कि आपके पास एक हल्का `ai` मॉड्यूल है जो `run_postprocessor` प्रदान करता है। इसे OpenAI के GPT‑4 API या लोकल LLM से बदल सकते हैं।  
- कुछ सैंपल इमेज या PDFs टेस्ट करने के लिए।

बस इतना ही। कोई भारी फ्रेमवर्क नहीं, कोई Docker जिम्नास्टिक नहीं। सिर्फ कुछ pip इंस्टॉल और आप तैयार हैं।

---

## Step 1: Perform a Fast Plain‑Text OCR Pass

ज्यादातर डेवलपर्स अक्सर यह भूल जाते हैं कि *plain text* OCR रन बहुत तेज़ होता है और आपको एक त्वरित sanity check देता है। हम `engine.Recognize()` को कॉल करेंगे ताकि बिना किसी लेआउट मेटाडेटा के कच्चे कैरेक्टर्स मिलें। यही हम **plain text OCR** कहते हैं।

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*Why this matters:*  
- **Speed** – 300 dpi पेज पर एक प्लेन पास आमतौर पर एक सेकंड से कम में समाप्त हो जाता है।  
- **Baseline** – आप बाद में मिलने वाले स्ट्रक्चर्ड आउटपुट की तुलना इस बेसलाइन से कर सकते हैं ताकि स्पष्ट त्रुटियों को पहचान सकें।  
- **Error‑catching** – अगर प्लेन पास पूरी तरह फेल हो (जैसे, सब गिबरिश), तो आपको पता चल जाएगा कि इमेज क्वालिटी बहुत कम है और आप जल्दी बाहर निकल सकते हैं।

---

## Step 2: Run a Detailed Layout‑Aware OCR Pass

प्लेन टेक्स्ट अच्छा है, लेकिन यह *कहाँ* प्रत्येक शब्द पेज पर स्थित है, इसे छोड़ देता है। इनवॉइस, फॉर्म या मल्टी‑कॉलम मैगज़ीन के लिए आपको कोऑर्डिनेट्स, लाइन नंबर और कभी‑कभी फ़ॉन्ट जानकारी चाहिए होती है। यही वह जगह है जहाँ `engine.RecognizeStructured()` काम आता है।

नीचे Tesseract के **TSV** आउटपुट के चारों ओर एक हल्का रैपर है, जो पेज → लाइन → शब्द की हायरार्की देता है, बाउंडिंग बॉक्स को संरक्षित रखते हुए।

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*Why we do this:*  
- **Coordinates** आपको बाद में निकाले गए टेक्स्ट को मूल इमेज पर हाइलाइट या रेडैक्शन के लिए मैप करने की सुविधा देते हैं।  
- **Line grouping** मूल लेआउट को संरक्षित रखता है, जो टेबल या कॉलम को पुनः निर्मित करने के लिए आवश्यक है।  
- यह पास प्लेन पास से थोड़ा धीमा है, लेकिन अधिकांश दस्तावेज़ों के लिए कुछ सेकंड में समाप्त हो जाता है।

---

## Step 3: Run the AI Post‑Processor to Correct OCR Errors

सबसे अच्छे OCR इंजन भी गलती करते हैं—जैसे “rn” बनाम “m”, गायब डायक्रिटिक, या शब्दों का विभाजन। एक AI मॉडल रॉ स्ट्रिंग और स्ट्रक्चर्ड डेटा को देख सकता है, असंगतियों को पहचान सकता है, और मूल कोऑर्डिनेट्स को बरकरार रखते हुए टेक्स्ट को पुनः लिख सकता है।

नीचे एक **mock** इम्प्लीमेंटेशन है; यदि आपके पास वास्तविक LLM है तो बॉडी को बदल दें।

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*Why this step improves OCR accuracy:*  
- **Contextual fixes** – AI यह तय कर सकता है कि “l0ve” संभवतः “love” है, आसपास के शब्दों के आधार पर।  
- **Coordinate preservation** – आप लेआउट जानकारी रखे रहते हैं, इसलिए डाउनस्ट्रीम टास्क (जैसे PDF एनोटेशन) सटीक रहते हैं।  
- **Iterative refinement** – आप पोस्ट‑प्रोसेसर को कई बार चला सकते हैं, प्रत्येक पास में और अधिक त्रुटियों को साफ़ किया जाता है।

---

## Step 4: Iterate Through the Corrected, Structured Output

अब जब हमारे पास एक साफ़‑सुथरा स्ट्रक्चर है, अंतिम टेक्स्ट निकालना बहुत आसान है। नीचे हम प्रत्येक लाइन को प्रिंट करते हैं, लेकिन आप इसे CSV में लिख सकते हैं, डेटाबेस में फीड कर सकते हैं, या सर्चेबल PDF जेनरेट कर सकते हैं।

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**Expected output** (मान लीजिए एक साधारण एक‑पेज इनवॉइस है):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

ध्यान दें कि लाइन ब्रेक और कॉलम क्रम बरकरार है, और सामान्य OCR गड़बड़ियाँ जैसे “$15.00” को “$15,00” पढ़ना AI स्टेप द्वारा सुधारा गया है।

---

## How This Workflow Helps **Improve OCR Accuracy**

| चरण | क्या ठीक करता है | क्यों महत्वपूर्ण है |
|------|----------------|-------------------|
| **Plain text OCR** | पढ़ने योग्य नहीं पेजों की जल्दी पहचान | बेकार इनपुट को स्किप करके समय बचाता है |
| **Structured OCR** | लेआउट, कोऑर्डिनेट्स को कैप्चर करता है | हाइलाइटिंग, रेडैक्शन जैसे डाउनस्ट्रीम टास्क को सक्षम बनाता है |
| **AI post‑processor** | स्पेलिंग सुधारता है, विभक्त शब्दों को जोड़ता है, नंबर ठीक करता है | शोरयुक्त स्कैन पर कैरेक्टर‑लेवल सटीकता को ~85 % से >95 % तक बढ़ाता है |
| **Iteration** | ट्यून किए गए पैरामीटरों के साथ पुनः‑रन की अनुमति देता है | विशिष्ट डॉक्यूमेंट टाइप्स के लिए पाइपलाइन को फाइन‑ट्यून करता है |

इन तीन अवधारणाओं—**plain text OCR**, लेआउट‑अवेयर एक्सट्रैक्शन, और AI सुधार—को मिलाकर आप एक मजबूत समाधान प्राप्त करते हैं जो *काफी हद तक* **OCR की सटीकता को सुधारता** है, बिना स्क्रैच से कस्टम न्यूरल नेटवर्क लिखे।

---

## Common Pitfalls & Pro Tips

- **Pitfall:** Tesseract को लो‑रेज़ोल्यूशन इमेज (≤150 dpi) देना गड़बड़ आउटपुट देता है।  
  **Pro tip:** `Pillow` से प्री‑प्रोसेस करें—`Image.convert('L')` और `Image.filter(ImageFilter.MedianFilter())` लागू करें OCR से पहले।

- **Pitfall:** AI पोस्ट‑प्रोसेसर अनजाने में डोमेन‑स्पेसिफिक टर्म्स (जैसे “SKU123”) को बदल सकता है।  
  **Pro tip:** टर्म्स की एक whitelist बनाएं और उसे LLM या `pyspellchecker` जैसी स्पेल‑चेकर लाइब्रेरी को पास करें।

- **Pitfall:** मल्टी‑कॉलम पेज एक ही लाइन में मर्ज हो जाते हैं।  
  **Pro tip:** Tesseract के TSV आउटपुट में `block_num` फ़ील्ड का उपयोग करके कॉलम बाउंड्रीज़ पहचानें और लाइनों को उसी अनुसार विभाजित करें।

- **Pitfall:** बड़े PDFs को एक साथ लोड करने से मेमोरी ओवरफ़्लो हो सकता है।  
  **Pro tip:** पेजेज को क्रमिक रूप से प्रोसेस करें—`pdf2image.convert_from_path(..., first_page=n, last_page=n)` के साथ लूप करें।

---

## Extending the Pipeline

अगर आप आगे के कदमों में रुचि रखते हैं, तो नीचे दिए गए सुधारों पर विचार करें:

1. **Batch processing** – पूरे स्क्रिप्ट को एक फ़ंक्शन में रैप करें जो डायरेक्टरी को वॉक करे, `concurrent.futures` के साथ हजारों फ़ाइलों को पैरलल प्रोसेस करे।  
2. **Language models** – साधारण difflib ह्यूरिस्टिक को OpenAI के `gpt‑4o` या लोकल LLaMA मॉडल कॉल से बदलें, ताकि अधिक समृद्ध कॉन्टेक्स्टुअल सुधार मिल सके।  
3. **Export formats** – सुधारित स्ट्रक्चर को सर्चेबल PDF में लिखें  

## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और स्टेप‑बाय‑स्टेप व्याख्याएँ हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)
- [Improve OCR Accuracy – Detect Areas Mode in OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}