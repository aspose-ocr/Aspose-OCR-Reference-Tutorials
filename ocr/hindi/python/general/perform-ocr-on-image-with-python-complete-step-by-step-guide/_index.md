---
category: general
date: 2026-07-05
description: Python का उपयोग करके छवि पर OCR करें। सीखें कि कैसे छवि को टेक्स्ट में
  बदलें, OCR के लिए छवि लोड करें और कुछ ही मिनटों में छवि से सिरिलिक टेक्स्ट निकालें।
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: hi
og_description: Python में छवि पर OCR करें। यह गाइड आपको दिखाता है कि कैसे छवि को
  टेक्स्ट में बदलें, OCR के लिए छवि लोड करें और जल्दी से छवि से सिरिलिक टेक्स्ट निकालें।
og_title: Python के साथ इमेज पर OCR करें – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: Python के साथ इमेज पर OCR करें – पूर्ण चरण‑दर‑चरण मार्गदर्शिका
url: /hi/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज पर OCR करने के लिए Python – पूर्ण चरण‑दर‑चरण गाइड

क्या आपने कभी सोचा है कि **इमेज फ़ाइलों पर OCR** कैसे किया जाए बिना उन्हें किसी थर्ड‑पार्टी सर्विस को भेजे? आप अकेले नहीं हैं। कई प्रोजेक्ट्स—पासपोर्ट स्कैनर, रसीद डिजिटाइज़र, या आर्काइव टूल्स—में तस्वीर से कच्चा टेक्स्ट निकालना पहला कदम होता है।  

इस ट्यूटोरियल में हम एक व्यावहारिक उदाहरण के माध्यम से **इमेज को टेक्स्ट python** शैली में बदलना, **OCR के लिए इमेज लोड करना**, और अंत में open‑source `aocr` लाइब्रेरी का उपयोग करके **इमेज से सिरिलिक टेक्स्ट निकालना** दिखाएंगे। अंत तक आप किसी भी तस्वीर में **सिरिलिक टेक्स्ट पहचानने** में सक्षम हो जाएंगे।

> **आप क्या सीखेंगे:** एक तैयार‑चलाने‑योग्य स्क्रिप्ट, प्रत्येक चरण की स्पष्ट व्याख्याएँ, और सामान्य समस्याओं (जैसे धुंधली स्कैन या अनपेक्षित फ़ॉन्ट) को संभालने के टिप्स। कोई बाहरी API नहीं, सिर्फ शुद्ध Python।

---

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

- Python 3.8 या उससे नया संस्करण स्थापित हो।
- एक टर्मिनल या कमांड प्रॉम्प्ट जिससे आप सहज हों।
- `aocr` पैकेज (इसे `pip install aocr` से इंस्टॉल किया जा सकता है)।
- एक इमेज फ़ाइल जिसमें सिरिलिक अक्षर हों (जैसे, स्कैन किया हुआ रूसी पासपोर्ट)।  

यदि इनमें से कोई भी चीज़ अपरिचित लग रही है, तो घबराएँ नहीं—हम प्रत्येक बिंदु को संक्षेप में आगे कवर करेंगे।

---

## चरण 1: इमेज पर OCR करना – वातावरण सेट‑अप करना

सबसे पहले हमें एक साफ़ Python वातावरण चाहिए जहाँ OCR लाइब्रेरी मौजूद हो। वर्चुअल एनवायरनमेंट का उपयोग करने से डिपेंडेंसीज़ अलग रहती हैं और संस्करण टकराव से बचा जा सकता है।

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**क्यों?**  
एक समर्पित वातावरण यह सुनिश्चित करता है कि `aocr` पैकेज और उसकी नेटिव बाइनरीज़ अन्य प्रोजेक्ट्स के साथ टकराएँ नहीं। यह पुनरुत्पादन को भी आसान बनाता है—कोई भी आपका रेपो क्लोन करके वही `pip install -r requirements.txt` कमांड चला सकता है।

> **प्रो टिप:** `pip freeze > requirements.txt` के साथ अपनी डिपेंडेंसीज़ को फ्रीज़ कर लें ताकि आप हमेशा ठीक‑वही संस्करणों को जान सकें।

---

## चरण 2: OCR के लिए इमेज लोड करना – इम्पोर्ट और फ़ाइल तैयार करना

अब लाइब्रेरी तैयार है, हमें **OCR के लिए इमेज लोड** करनी होगी। `aocr.Image.from_file` मेथड अधिकांश सामान्य फ़ॉर्मैट (PNG, JPEG, TIFF) को संभालता है। इसे इस तरह उपयोग करें:

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**यहाँ क्या हो रहा है?**  
`aocr.Image.from_file` बाइनरी डेटा पढ़ता है, उसे डिकोड करता है, और एक ऑब्जेक्ट में स्टोर करता है जिसे OCR इंजन समझ सके। यदि फ़ाइल नहीं मिलती, तो Python `FileNotFoundError` उठाएगा, जिसे आप बाद में एरर हैंडलिंग के लिए पकड़ सकते हैं।

> **एज केस:** कुछ स्कैनर मल्टी‑पेज TIFF आउटपुट करते हैं। ऐसे में आपको पहले पेज़ विभाजित करने होंगे—`aocr` `Image.from_tiff_pages()` प्रदान करता है।

---

## चरण 3: OCR इंजन कॉन्फ़िगर करना – सिरिलिक पहचान को मजबूर करना

डिफ़ॉल्ट रूप से, कई OCR इंजन भाषा का अनुमान लगाने की कोशिश करते हैं, जिससे गैर‑लैटिन स्क्रिप्ट्स के लिए आउटपुट गड़बड़ हो सकता है। **सिरिलिक टेक्स्ट** को भरोसेमंद रूप से पहचानने के लिए हम भाषा को स्पष्ट रूप से “cyrillic” सेट करते हैं।

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**भाषा को मजबूर क्यों करें?**  
सिरिलिक अक्षर लैटिन अक्षरों से दृश्य रूप में मिलते‑जुलते होते हैं (जैसे “A” बनाम “А”)। इंजन को सिरिलिक की उम्मीद बताने से गलत पहचान काफी घटती है, विशेषकर लो‑रेज़ोल्यूशन स्कैन पर।

---

## चरण 4: इमेज पर OCR करना – पहचान चलाना

इमेज लोड हो गई और इंजन ट्यून हो गया, अब हम अंततः **इमेज पर OCR** करेंगे। `recognize` मेथड एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें निकाला गया टेक्स्ट और कॉन्फिडेंस स्कोर होते हैं।

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**`ocr_result` आपको क्या देता है?**  
- `text`: पहचाने गए अक्षरों की साधारण स्ट्रिंग।  
- `confidence`: एक फ्लोट (0‑1) जो कुल भरोसे को दर्शाता है।  
- `lines`: लाइन ऑब्जेक्ट्स की सूची, यदि आपको अधिक ग्रैन्युलर कंट्रोल चाहिए।

> **सामान्य प्रश्न:** *अगर टेक्स्ट उल्टा है तो क्या करें?*  
> `aocr` इमेज को ऑटो‑रोटेट कर सकता है; बस `ocr_engine.auto_rotate = True` सेट करें `recognize` कॉल करने से पहले।

---

## चरण 5: इमेज को टेक्स्ट python में बदलना – आउटपुट की पोस्ट‑प्रोसेसिंग

कच्ची स्ट्रिंग में अनावश्यक व्हाइटस्पेस या लाइन‑ब्रेक आर्टिफैक्ट हो सकते हैं। **इमेज को टेक्स्ट python** शैली में बदलने के लिए हम कुछ सरल कदमों से इसे साफ़ करेंगे:

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**ऐसा क्यों करें?**  
साफ़ आउटपुट को डाउनस्ट्रीम पाइपलाइन में फीड करना आसान होता है—चाहे आप इसे डेटाबेस में स्टोर कर रहे हों, ट्रांसलेशन API को भेज रहे हों, या पासपोर्ट नंबर के लिए रेगेक्स सर्च चला रहे हों।

---

## चरण 6: इमेज से सिरिलिक टेक्स्ट निकालना – सबको एक साथ जोड़ना

आइए सब कुछ एक पुन: उपयोग योग्य फ़ंक्शन में बाँधें। इससे **इमेज से सिरिलिक टेक्स्ट निकालना** आपके प्रोजेक्ट्स में एक‑लाइनर बन जाता है।

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**आपको जो परिणाम दिखना चाहिए (उदाहरण):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

यदि इमेज स्पष्ट है और फ़ॉन्ट OCR मॉडल से मेल खाता है, तो आपको लगभग‑परिपूर्ण ट्रांसक्रिप्शन मिलेगा।

---

## troubleshooting & Tips

| Issue | Likely Cause | Fix |
|-------|--------------|-----|
| Garbled characters | Wrong language setting | Ensure `ocr_engine.language = "cyrillic"` |
| Empty output | Image too dark or low‑resolution | Preprocess with `opencv` to increase contrast |
| Wrong orientation | Image rotated 90° | Set `ocr_engine.auto_rotate = True` |
| Slow performance | Large image ( >5 MP ) | Resize with `aocr.Image.resize(width=1024)` before recognition |

---

![perform OCR on image example](ocr_example.png "perform OCR on image example")

*Alt text: “इमेज पर OCR का उदाहरण, जिसमें Python कोड पासपोर्ट स्कैन से सिरिलिक टेक्स्ट निकाल रहा है।”*

---

## निष्कर्ष

हमने शुद्ध Python का उपयोग करके **इमेज पर OCR** किया, **OCR के लिए इमेज लोड** करना सीखा, इंजन को **सिरिलिक टेक्स्ट पहचानने** के लिए मजबूर किया, और अंत में एक साफ़ हेल्पर फ़ंक्शन के साथ **इमेज से सिरिलिक टेक्स्ट निकालना** पूरा किया। `aocr` को इंस्टॉल करने से लेकर परिणाम को साफ़ करने तक पूरी पाइपलाइन कुछ ही दर्जन लाइनों के कोड में समा जाती है और किसी भी प्रोजेक्ट में डाली जा सकती है जिसे **इमेज को टेक्स्ट python** शैली में बदलने की जरूरत है।

---

## आगे क्या?

- **बैच प्रोसेसिंग:** स्कैन की फ़ोल्डर पर लूप चलाएँ और परिणाम SQLite में स्टोर करें।  
- **भाषा पहचान:** `langdetect` को `aocr` के साथ मिलाकर सिरिलिक और लैटिन के बीच ऑटो‑स्विच करें।  
- **एडवांस्ड प्री‑प्रोसेसिंग:** उच्च सटीकता के लिए `opencv` से डेस्क्यू, डीनॉइज़ या बाइनराइज़ करें।  
- **FastAPI के साथ इंटीग्रेशन:** `extract_cyrillic_text` फ़ंक्शन को REST एन्डपॉइंट के रूप में एक्सपोज़ करें वेब ऐप्स के लिए।

इसे आज़माएँ—इंग्लिश पासपोर्ट के लिए भाषा “latin” में बदलें, या पूरी तरह अलग OCR बैकएंड आज़माएँ। अवधारणाएँ वही रहती हैं, और कोड लचीला है।

हैप्पी कोडिंग, और आपकी इमेजेस हमेशा पठनीय रहें!

## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}