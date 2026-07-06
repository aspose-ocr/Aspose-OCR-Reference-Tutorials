---
category: general
date: 2026-06-22
description: छवि को OCR के लिए पूर्व-प्रसंस्करण करें ताकि छवि से पाठ निकाला जा सके
  और Python में Aspose OCR का उपयोग करके OCR की सटीकता में सुधार किया जा सके। पूर्ण,
  चलाने योग्य उदाहरण शामिल है।
draft: false
keywords:
- preprocess image for OCR
- extract text from image
- improve OCR accuracy
language: hi
og_description: OCR के लिए छवि को पूर्व-प्रसंस्करण करें, छवि से पाठ निकालें, और Aspose
  OCR के साथ OCR की सटीकता बढ़ाएँ। Python में पूर्ण कार्यप्रवाह सीखें।
og_title: OCR के लिए छवि का पूर्व-प्रसंस्करण – पूर्ण पायथन ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  headline: Preprocess Image for OCR – Step‑by‑Step Python Guide
  type: TechArticle
- description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  name: Preprocess Image for OCR – Step‑by‑Step Python Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Aspose OCR’s wheels target modern interpreters. | | `aspose-ocr` package
      (`pip install aspose-ocr`) | Provides the `OcrEngine`, `ImagePreprocessor`,
      and filter classes. | | A sample image (e.g., `noisy-document.jpg`) |'
  - name: – Initialise the OCR Engine and Load Your Source Image
    text: '```python import aspose.ocr as ocr'
  - name: – Build a Preprocessing Chain to Clean the Image
    text: '```python # Initialise the preprocessor – a container for a series of filters
      preprocessor = ocr.ImagePreprocessor()'
  - name: – Attach the Preprocessor to the Engine
    text: '```python # Hook the preprocessing pipeline into the OCR engine ocr_engine.set_preprocessor(preprocessor)
      ```'
  - name: – Run OCR and Extract Text from Image
    text: '```python # Perform the recognition on the pre‑processed image recognition_result
      = ocr_engine.recognize()'
  - name: – Verify the Output and Fine‑Tune for Better Accuracy
    text: '```python # Quick sanity check: print length and a sample snippet print(f"Detected
      {len(extracted_text)} characters.") print("First 200 chars:", extracted_text[:200])
      ```'
  type: HowTo
- questions:
  - answer: Yes. Convert each page to an image (e.g., using `pdf2image`) and feed
      it through the same pipeline in a loop. The same `preprocess image for OCR`
      steps apply per page.
    question: Does this work with multi‑page PDFs?
  - answer: 'Set the language before recognition: `engine.set_language(ocr.Language.FRENCH)`.
      The preprocessing filters stay the same; only the language model changes.'
    question: What if my document is in a language other than English?
  - answer: 'Absolutely. The `ImagePreprocessor` is extensible—just call `add_filter`
      again. For heavy‑dotted backgrounds, `ocr.Filters.MedianFilter(kernel=3)` can
      be useful. --- ## Wrap‑Up We’ve just **preprocess image for OCR**, run Aspose’s
      engine, and **extract text from image** while showcasing several tric'
    question: Can I chain more filters?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: OCR के लिए छवि का पूर्व‑प्रसंस्करण – चरण‑दर‑चरण पायथन गाइड
url: /hi/python-java/general/preprocess-image-for-ocr-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR के लिए इमेज प्रीप्रोसेस – पूर्ण Python ट्यूटोरियल

यदि आपको **preprocess image for OCR** की आवश्यकता है, तो आप संभवतः शोरयुक्त स्कैन, झुके हुए पृष्ठ, या कम‑कॉन्ट्रास्ट फ़ोटो से जूझ रहे होंगे जो सहयोग नहीं करतीं। क्या आपने कभी इमेज से टेक्स्ट निकालने की कोशिश की है और केवल गड़बड़ आउटपुट मिला है? यही वह जगह है जहाँ एक ठोस प्रीप्रोसेसिंग चेन पढ़ने योग्य शब्दों की एक छोटी सी मात्रा और पूरी‑भरी ट्रांसक्रिप्शन दुविधा के बीच अंतर बना सकती है।

इस गाइड में हम एक पूर्ण, एंड‑टू‑एंड उदाहरण के माध्यम से चलेंगे जो **extracts text from image** करता है और साथ ही Aspose OCR for Python का उपयोग करके **improve OCR accuracy** दिखाता है। कोई अस्पष्ट संदर्भ नहीं—सिर्फ वह कोड जिसे आप कॉपी‑पेस्ट कर सकते हैं, प्रत्येक लाइन के पीछे की तर्कशक्ति, और वास्तविक‑दुनिया के एज केसों के लिए टिप्स।

## आप क्या सीखेंगे

- एक तैयार‑चलाने योग्य Python स्क्रिप्ट जो शोरयुक्त दस्तावेज़ को लोड करती है, उसे साफ़ करती है, और पहचाना गया टेक्स्ट प्रिंट करती है।  
- यह समझना कि प्रत्येक प्रीप्रोसेसिंग फ़िल्टर क्यों महत्वपूर्ण है और उसके पैरामीटर कैसे ट्यून करें।  
- भारी स्पेकल शोर, अत्यधिक घुमाव, या कम‑कॉन्ट्रास्ट स्कैन जैसी सामान्य समस्याओं को संभालने की रणनीतियाँ।  

### आवश्यकताएँ

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Aspose OCR के व्हील्स आधुनिक इंटरप्रेटर्स को टार्गेट करते हैं। |
| `aspose-ocr` package (`pip install aspose-ocr`) | `OcrEngine`, `ImagePreprocessor`, और फ़िल्टर क्लासेज़ प्रदान करता है। |
| A sample image (e.g., `noisy-document.jpg`) | हम एक जानबूझकर गंदा चित्र उपयोग करेंगे ताकि प्रीप्रोसेसिंग के लाभ दिखाए जा सकें। |
| Basic familiarity with Python functions | आपको स्क्रिप्ट को अपने पाइपलाइन में अनुकूलित करने में मदद मिलती है। |

> **Pro tip:** यदि आप Windows पर हैं, तो संस्करण टकराव से बचने के लिए स्क्रिप्ट को एक वर्चुअल एनवायरनमेंट के अंदर चलाएँ।

---

## Aspose OCR (Python) के साथ इमेज प्रीप्रोसेस

नीचे ट्यूटोरियल का मुख्य भाग है—कोड का चरण‑दर‑चरण विवरण जो आपको चाहिए। प्रत्येक सेक्शन यह बताता है **what** हम कर रहे हैं *and* **why** हम कर रहे हैं, ताकि आप बाद में पाइपलाइन को बिना अनुमान लगाए बदल सकें।

![preprocess image for OCR example](ocr-preprocess.png){alt="preprocess image for OCR"}

### चरण 1 – OCR इंजन को इनिशियलाइज़ करें और स्रोत इमेज लोड करें

```python
import aspose.ocr as ocr

# Create the OCR engine – the central object that drives recognition
ocr_engine = ocr.OcrEngine()

# Load the raw image file. Using ImageStream lets Aspose handle various formats.
ocr_engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))
```

- **Why** an `OcrEngine`? यह रिकग्नाइज़र, भाषा सेटिंग्स, और (बाद में) प्रीप्रोसेसर को समाहित करता है।  
- **Why** `ImageStream.from_file`? यह फ़ाइल‑टाइप हैंडलिंग को एब्स्ट्रैक्ट करता है, इसलिए आप JPEG को PNG से कोड बदलें बिना बदल सकते हैं।

### चरण 2 – इमेज को साफ़ करने के लिए प्रीप्रोसेसिंग चेन बनाएं

```python
# Initialise the preprocessor – a container for a series of filters
preprocessor = ocr.ImagePreprocessor()

# 1️⃣ Deskew – corrects any rotation so text lines become horizontal.
preprocessor.add_filter(ocr.Filters.Deskew())

# 2️⃣ Despeckle – removes isolated noise pixels; strength=2 is a good middle ground.
preprocessor.add_filter(ocr.Filters.Despeckle(strength=2))

# 3️⃣ ContrastBoost – lifts faint characters; level=1.5 amplifies contrast without blowing out highlights.
preprocessor.add_filter(ocr.Filters.ContrastBoost(level=1.5))
```

**इन फ़िल्टरों से OCR की सटीकता कैसे बढ़ती है:**  
- **Deskew** सामान्य “झुका पृष्ठ” समस्या को समाप्त करता है जो कैरेक्टर सेगमेंटेशन को भ्रमित करती है।  
- **Despeckle** कम‑गुणवत्ता स्कैनरों द्वारा उत्पन्न स्पेकल्स को लक्षित करता है; अधिक स्ट्रेंथ अधिक शोर हटाती है लेकिन बारीक विवरण को घिस सकता है।  
- **ContrastBoost** गहरे टेक्स्ट को हल्के बैकग्राउंड के खिलाफ उभारा जाता है, जो अधिकांश OCR इंजनों के लिए क्लासिक जीत है।

> **Edge case:** यदि आपका दस्तावेज़ पहले से ही पूरी तरह सीधा है, तो `Deskew()` को छोड़ सकते हैं और कुछ मिलीसेकंड बचा सकते हैं।

### चरण 3 – प्रीप्रोसेसर को इंजन से जोड़ें

```python
# Hook the preprocessing pipeline into the OCR engine
ocr_engine.set_preprocessor(preprocessor)
```

अब हर बार जब `ocr_engine.recognize()` चलाया जाएगा, यह पहले हमने परिभाषित तीन फ़िल्टरों को ठीक उसी क्रम में लागू करेगा। क्रम महत्वपूर्ण है: आपको **deskew before despeckling** करना चाहिए, नहीं तो स्पेकल फ़िल्टर घुमा हुआ किनारा शोर समझ सकता है।

### चरण 4 – OCR चलाएँ और इमेज से टेक्स्ट निकालें

```python
# Perform the recognition on the pre‑processed image
recognition_result = ocr_engine.recognize()

# Pull out the plain text string
extracted_text = recognition_result.get_text()
print(extracted_text)
```

- `recognize()` कॉल एक `RecognitionResult` ऑब्जेक्ट लौटाता है जिसमें न केवल कच्चा टेक्स्ट बल्कि कॉन्फिडेंस स्कोर, बाउंडिंग बॉक्स, और भाषा विवरण भी होते हैं।  
- यहाँ हमें केवल साधारण स्ट्रिंग चाहिए, लेकिन आप `recognition_result.get_confidence()` का उपयोग करके एक त्वरित **improve OCR accuracy** जांच कर सकते हैं।

### चरण 5 – आउटपुट की जाँच करें और बेहतर सटीकता के लिए फाइन‑ट्यून करें

```python
# Quick sanity check: print length and a sample snippet
print(f"Detected {len(extracted_text)} characters.")
print("First 200 chars:", extracted_text[:200])
```

यदि आउटपुट अभी भी गड़बड़ प्रतीक दिखाता है, तो इन समायोजनों पर विचार करें:

| Issue | Suggested Fix |
|-------|----------------|
| Still blurry text | Increase `ContrastBoost(level)` to 2.0 or add `ocr.Filters.GaussianBlur(radius=1)` before despeckling. |
| Too many stray characters | Raise `Despeckle(strength)` to 3, or insert `ocr.Filters.RemoveLines()` to strip horizontal rules. |
| Skew persists | Call `ocr.Filters.Deskew(max_angle=5)` to limit correction to mild rotations. |

---

## पूर्ण, चलाने योग्य स्क्रिप्ट

नीचे दिया गया ब्लॉक `ocr_preprocess.py` नाम की फ़ाइल में कॉपी करें। `YOUR_DIRECTORY/noisy-document.jpg` को अपनी इमेज के वास्तविक पाथ से बदलें, फिर `python ocr_preprocess.py` चलाएँ।

```python
import aspose.ocr as ocr

def main():
    # Initialise engine and load image
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))

    # Build preprocessing pipeline
    preproc = ocr.ImagePreprocessor()
    preproc.add_filter(ocr.Filters.Deskew())
    preproc.add_filter(ocr.Filters.Despeckle(strength=2))
    preproc.add_filter(ocr.Filters.ContrastBoost(level=1.5))

    # Attach pipeline
    engine.set_preprocessor(preproc)

    # Recognise and extract text
    result = engine.recognize()
    text = result.get_text()

    # Display results
    print("\n--- OCR Output ---")
    print(text)
    print("\n--- Summary ---")
    print(f"Characters detected: {len(text)}")
    print("Snippet:", text[:200].replace("\n", " "))

if __name__ == "__main__":
    main()
```

इस स्क्रिप्ट को शोरयुक्त, थोड़ा घुमा हुआ JPEG पर चलाने से साफ़, पढ़ने योग्य टेक्स्ट प्राप्त होगा—जो दिखाता है कि एक अच्छी तरह डिज़ाइन किया गया प्रीप्रोसेसिंग चेन **improves OCR accuracy** को नाटकीय रूप से बढ़ाता है।

---

## सामान्य प्रश्न एवं उत्तर

**Q: क्या यह मल्टी‑पेज PDFs के साथ काम करता है?**  
A: हाँ। प्रत्येक पेज को इमेज में बदलें (जैसे `pdf2image` का उपयोग करके) और उसे लूप में उसी पाइपलाइन से पास करें। प्रत्येक पेज पर वही `preprocess image for OCR` कदम लागू होते हैं।

**Q: यदि मेरा दस्तावेज़ अंग्रेज़ी के अलावा किसी अन्य भाषा में है तो क्या करें?**  
A: पहचान से पहले भाषा सेट करें: `engine.set_language(ocr.Language.FRENCH)`। प्रीप्रोसेसिंग फ़िल्टर वही रहते हैं; केवल भाषा मॉडल बदलता है।

**Q: क्या मैं और फ़िल्टर जोड़ सकता हूँ?**  
A: बिल्कुल। `ImagePreprocessor` विस्तारणीय है—बस फिर से `add_filter` कॉल करें। भारी‑डॉटेड बैकग्राउंड के लिए, `ocr.Filters.MedianFilter(kernel=3)` उपयोगी हो सकता है।

---

## निष्कर्ष

हमने अभी **preprocess image for OCR** किया, Aspose का इंजन चलाया, और **extract text from image** किया जबकि कई ट्रिक्स दिखाए जो **improve OCR accuracy** को बढ़ाते हैं। पूरा उदाहरण किसी भी प्रोजेक्ट में डालने के लिए तैयार है, और मॉड्यूलर फ़िल्टर डिज़ाइन का मतलब है कि आप अपनी डेटा की जरूरतों के अनुसार चरणों को बदल, जोड़ या हट सकते हैं।

आगे आप विचार कर सकते हैं:

- `concurrent.futures` के साथ दर्जनों स्कैन की **बैच प्रोसेसिंग**।  
- `pyspellchecker` जैसी स्पेल‑चेक लाइब्रेरीज़ के साथ **पोस्ट‑प्रोसेसिंग** करके OCR‑परिचित टाइपो को साफ़ करना।  
- Flask या FastAPI का उपयोग करके स्क्रिप्ट को एक वेब सर्विस में **इंटीग्रेट** करना, जिससे यह एक ऑन‑डिमांड OCR माइक्रो‑सर्विस बन जाए।

इसे चलाएँ, फ़िल्टर स्ट्रेंथ को समायोजित करें, और देखें कि आपकी पहचान दरें कैसे बढ़ती हैं। यदि कोई समस्या आती है, तो टिप्पणी छोड़ें—हैप्पी कोडिंग!

## आप अगला क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}