---
category: general
date: 2026-06-16
description: Python OCR का उपयोग करके TIFF फ़ाइलों से टेक्स्ट निकालें। चरण‑दर‑चरण
  सीखें कि कैसे TIFF को टेक्स्ट में बदलें, और बहु‑पृष्ठ दस्तावेज़ों को आसानी से संभालें।
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: hi
og_description: Python OCR के साथ TIFF फ़ाइलों से टेक्स्ट निकालें। इस गाइड का पालन
  करके TIFF को टेक्स्ट में बदलें, मल्टी‑पेज स्कैन को संभालें, और साफ़ परिणाम प्राप्त
  करें।
og_title: TIFF से टेक्स्ट निकालें – पूर्ण पायथन गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: TIFF से टेक्स्ट निकालें – पूर्ण पायथन गाइड
url: /hi/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF से टेक्स्ट निकालें – पूर्ण Python गाइड

क्या आपको **TIFF से टेक्स्ट निकालने** की ज़रूरत पड़ी है लेकिन शुरुआत नहीं पता थी? आप अकेले नहीं हैं—कई डेवलपर्स स्कैन किए गए अभिलेखों या लेगेसी दस्तावेज़ों के साथ काम करते समय इस समस्या का सामना करते हैं। अच्छी खबर? कुछ ही लाइनों के Python कोड से आप **TIFF को टेक्स्ट में बदल** सकते हैं, चाहे फ़ाइल में दर्जनों पेज हों।

इस ट्यूटोरियल में हम एक वास्तविक उदाहरण के माध्यम से चलेंगे: एक मल्टी‑पेज TIFF लोड करना, OCR भाषा को फ़्रेंच सेट करना, और प्रत्येक पेज से पहचाना गया टेक्स्ट निकालना। अंत तक आपके पास चलाने योग्य स्क्रिप्ट होगी, आप समझेंगे कि प्रत्येक कदम क्यों महत्वपूर्ण है, और जानेंगे कि इसे अन्य भाषाओं या इमेज फ़ॉर्मेट्स के लिए कैसे अनुकूलित करें।

## आवश्यकताएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

- Python 3.8 या उससे नया स्थापित हो।
- `ocr` पैकेज (या कोई भी संगत OCR लाइब्रेरी जो `OcrEngine` क्लास प्रदान करती हो)। इसे `pip install ocr-lib` से इंस्टॉल कर सकते हैं—अपने उपयोग में आने वाले वास्तविक पैकेज नाम से बदलें।
- एक मल्टी‑पेज TIFF फ़ाइल (जैसे `french-scans.tif`) जिसे आप प्रोसेस करना चाहते हैं।
- Python स्क्रिप्टिंग की बुनियादी समझ।

कोई भारी डिपेंडेंसी नहीं, कोई बाहरी सर्विस नहीं—सिर्फ शुद्ध Python और एक OCR इंजन।

---

## चरण 1: OCR इंजन सेट अप करें **TIFF से टेक्स्ट निकालने** के लिए

सबसे पहले—हमें एक OCR इंजन इंस्टेंस चाहिए और हमें उसे बताना होगा कि कौन सी भाषा उपयोग करनी है। हमारे केस में स्रोत सामग्री फ़्रेंच है, इसलिए हम भाषा को उसी अनुसार सेट करेंगे।

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**यह क्यों महत्वपूर्ण है:**  
भाषा सेटिंग सटीकता को बहुत बढ़ा देती है। फ़्रेंच अक्षर जैसे “é” या “ç” को इंग्लिश डिफ़ॉल्ट पर सामान्य प्रतीकों के रूप में पढ़ा जाता। फ़्रेंच को स्पष्ट रूप से चुनकर हम इंजन को सही कैरेक्टर मैप देते हैं।

> **प्रो टिप:** यदि आप कई भाषाओं में दस्तावेज़ प्रोसेस कर रहे हैं, तो आप प्रत्येक `recognize()` कॉल से पहले `engine.language` को ऑन‑द‑फ़्लाई बदल सकते हैं।

---

## चरण 2: वह मल्टी‑पेज TIFF लोड करें जिसे आप **TIFF को टेक्स्ट में बदलना** चाहते हैं

एक TIFF कई फ्रेम रख सकता है—हर फ्रेम को एक अलग पेज मानें। OCR लाइब्रेरी हमारे लिए इसे एब्स्ट्रैक्ट करती है, इसलिए हम बस फ़ाइल की ओर इशारा करते हैं।

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**एज केस अलर्ट:**  
यदि फ़ाइल पाथ गलत है या TIFF करप्ट है, तो `load_from_file` मेथड एक एक्सेप्शन उठाएगा। प्रोडक्शन कोड के लिए इसे `try/except` ब्लॉक में रैप करें:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## चरण 3: पूरे दस्तावेज़ पर OCR चलाएँ – **TIFF से टेक्स्ट निकालने** का कोर

अब हम इंजन को अपना जादू करने देते हैं। `recognize()` कॉल एक बार में हर पेज प्रोसेस करता है और एक रिच रिज़ल्ट ऑब्जेक्ट लौटाता है।

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**अंदर क्या हो रहा है?**  
इंजन प्रत्येक फ्रेम पर इटररेट करता है, प्री‑प्रोसेसिंग (डेस्क्यूइंग, बाइनराइज़ेशन) लागू करता है, न्यूरल नेटवर्क चलाता है, और आउटपुट को एग्रीगेट करता है। क्योंकि हमने `recognize()` केवल एक बार कॉल किया, लाइब्रेरी पेजों के बीच रिसोर्सेज़ शेयर कर सकती है, जो मैन्युअल लूपिंग से तेज़ है।

---

## चरण 4: JSON रिज़ल्ट से पहचाना गया टेक्स्ट निकालें – **TIFF को टेक्स्ट में बदलना** पेज दर पेज

रिज़ल्ट ऑब्जेक्ट को JSON में सीरियलाइज़ किया जा सकता है। उस JSON के अंदर आपको `pages` एरे मिलेगा, जिसमें प्रत्येक में एक `text` फ़ील्ड होगा।

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

अब हमारे पास एक साफ़ Python लिस्ट है जहाँ हर एलिमेंट एक पेज के OCR आउटपुट से मेल खाता है।

---

## चरण 5: प्रत्येक पेज का टेक्स्ट प्रिंट या सेव करें – **TIFF से टेक्स्ट निकालने** का अंतिम टुकड़ा

आइए पेजों के माध्यम से लूप करें और निकाला गया टेक्स्ट दिखाएँ। आप चाहें तो प्रत्येक पेज को अलग `.txt` फ़ाइल में भी लिख सकते हैं।

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### अपेक्षित आउटपुट (उदाहरण)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

यदि OCR सफल रहा, तो आपको प्रत्येक पेज के लिए फ़्रेंच वाक्यों का साफ़ ब्लॉक दिखेगा। यदि गड़बड़ अक्षर दिखें, तो भाषा सेटिंग दोबारा जाँचें या OCR से पहले इमेज रेज़ोल्यूशन बढ़ाने पर विचार करें।

---

## सामान्य समस्याओं का समाधान जब आप **TIFF को टेक्स्ट में बदलते** हैं

| समस्या | क्यों होता है | त्वरित समाधान |
|-------|----------------|-----------|
| **खाली `pages` एरे** | TIFF सही से लोड नहीं हुआ या उसमें कोई फ्रेम नहीं है। | फ़ाइल पाथ जाँचें और सुनिश्चित करें कि TIFF एक सिंगल‑पेज PNG नहीं है जो TIFF के रूप में दिख रहा हो। |
| **गड़बड़ अक्षर** | भाषा का मिलान न होना या इमेज क्वालिटी कम होना। | सही `engine.language` सेट करें और इमेज को प्री‑प्रोसेस करें (जैसे DPI बढ़ाएँ)। |
| **बड़े TIFF पर मेमोरी ब्लो‑अप** | सभी पेज एक साथ लोड करने से RAM ख़त्म हो जाता है। | चंक्स में प्रोसेस करें: एक फ्रेम लोड करें, पहचानें, फिर अगले पर जाने से पहले डिस्कार्ड करें। |
| **प्रिंट करते समय Unicode एरर** | कंसोल एन्कोडिंग एक्सेंटेड कैरेक्टर्स को सपोर्ट नहीं करती। | `print(page["text"].encode('utf-8').decode('utf-8'))` उपयोग करें या टर्मिनल को UTF‑8 के लिए कॉन्फ़िगर करें। |

---

## स्क्रिप्ट को विस्तारित करना: **TIFF से टेक्स्ट निकालने** से बैच प्रोसेसिंग तक

अब जब आपके पास ठोस आधार है, तो इन अगले कदमों पर विचार करें:

1. **बैच कन्वर्ज़न** – पूरे फ्लो को `def ocr_tiff(path):` फ़ंक्शन में रैप करें और TIFF फ़ाइलों की डायरेक्टरी पर इटररेट करें।
2. **फ़ाइलों में आउटपुट** – प्रिंट करने के बजाय प्रत्येक पेज का टेक्स्ट `page_{i}.txt` में लिखें या सबको एक ही डॉक्यूमेंट में कंकैट करें।
3. **वैकल्पिक OCR इंजन** – यदि आपको अधिक सटीकता चाहिए, तो `ocr.OcrEngine()` को Tesseract (`pytesseract`) या Azure Cognitive Services से बदलें—बस वही “TIFF से टेक्स्ट निकालने” लॉजिक रखें।
4. **पोस्ट‑प्रोसेसिंग** – स्पेल‑चेक, भाषा डिटेक्शन, या रेगेक्स क्लीन‑अप चलाएँ ताकि कच्चा OCR आउटपुट साफ़ हो जाए।

---

## पूर्ण, तैयार‑से‑चलाने वाली स्क्रिप्ट

नीचे पूरा कोड दिया गया है, कॉपी‑पेस्ट के लिए तैयार। इसमें बेसिक एरर हैंडलिंग और वैकल्पिक रूप से प्रत्येक पेज का टेक्स्ट अलग फ़ाइलों में सेव करने की सुविधा शामिल है।

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

इस स्क्रिप्ट को चलाएँ, `tiff_file` को अपने दस्तावेज़ की ओर इंगित करें, और कंसोल में साफ़ फ़्रेंच वाक्य देखिए। यदि आप `out_folder` प्रदान करते हैं, तो आपको `page_#.txt` फ़ाइलों की एक श्रृंखला भी मिल जाएगी, जो आगे की प्रोसेसिंग के लिए तैयार होगी।

---

## निष्कर्ष

हमने एक सरल Python OCR वर्कफ़्लो का उपयोग करके **TIFF फ़ाइलों से टेक्स्ट निकाला** है, और आप अब भरोसेमंद रूप से **TIFF को टेक्स्ट में बदल** सकते हैं। सही भाषा के साथ इंजन इनिशियलाइज़ करने से लेकर प्रत्येक पेज के JSON रिज़ल्ट पर लूप करने तक, हर कदम का “क्यों” समझाया गया है, ताकि आप इसे अन्य भाषाओं, इमेज फ़ॉर्मेट्स, या बड़े बैच जॉब्स के लिए अनुकूलित कर सकें।

अगला क्या? OCR बैकएंड को Tesseract से बदलें, विभिन्न भाषा पैक्स के साथ प्रयोग करें, या आउटपुट को सर्चेबल डेटाबेस में इंटीग्रेट करें। जब आप स्कैन किए गए इमेज को सर्चेबल टेक्स्ट में बदल सकते हैं, तो संभावनाएँ असीमित हैं।

यदि आपको कोई समस्या आती है या आगे के सुधारों के बारे में विचार हैं, तो कमेंट करें। Happy coding!

## अब आपको क्या सीखना चाहिए?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}