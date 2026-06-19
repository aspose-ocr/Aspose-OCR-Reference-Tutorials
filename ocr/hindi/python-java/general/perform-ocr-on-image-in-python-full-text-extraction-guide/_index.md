---
category: general
date: 2026-06-19
description: Python की OCR लाइब्रेरी का उपयोग करके छवि पर OCR करें। सीखें कि छवि से
  टेक्स्ट कैसे पहचानें, JPEG से टेक्स्ट कैसे डिटेक्ट करें, और स्कैन की गई छवि से टेक्स्ट
  को प्रभावी ढंग से निकालें।
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: hi
og_description: Python के साथ छवि पर OCR करें और स्कैन की गई फ़ाइलों से टेक्स्ट निकालें।
  यह गाइड आपको चरण‑दर‑चरण छवियों को लोड करने, डेस्क्यूइंग करने और टेक्स्ट को पहचानने
  के माध्यम से ले जाता है।
og_title: Python में इमेज पर OCR करें – पूर्ण टेक्स्ट एक्सट्रैक्शन गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Python में इमेज पर OCR करें – पूर्ण टेक्स्ट एक्सट्रैक्शन गाइड
url: /hi/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में इमेज पर OCR करें – पूर्ण टेक्स्ट एक्सट्रैक्शन गाइड

क्या आपको कभी **perform OCR on image** फ़ाइलों को प्रोसेस करना पड़ा लेकिन कोड जटिल लगने के कारण रुकावट आई? आप अकेले नहीं हैं। चाहे आप स्कैन किए हुए रसीदों के ढेर को सर्चेबल PDFs में बदल रहे हों या डेटा‑साइंस प्रोजेक्ट के लिए JPEG से कैप्शन निकाल रहे हों, JPEGs और अन्य फ़ॉर्मैट्स से टेक्स्ट पहचानने की क्षमता आज के किसी भी डेवलपर के लिए अनिवार्य कौशल है।

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे कि आप कैसे **detect text from image** फ़ाइलों, **extract text from scanned image** दस्तावेज़ों को पहचानें, और यहाँ तक कि **load image for OCR** कुछ ही लाइनों में करें। अंत तक, आपके पास एक ठोस, प्रोडक्शन‑रेडी स्निपेट होगा जिसे आप अपने प्रोजेक्ट्स में जोड़ सकते हैं—कोई गायब इम्पोर्ट नहीं, कोई अस्पष्ट “see docs” शॉर्टकट नहीं।

## आप क्या बनाएँगे

- एक छोटा Python स्क्रिप्ट जो OCR इंजन बनाता है, auto‑deskew सक्षम करता है, JPEG (या कोई भी समर्थित फ़ॉर्मैट) लोड करता है, और पहचाने गए टेक्स्ट को प्रिंट करता है।
- **why** प्रत्येक सेटिंग के महत्व की व्याख्या, न कि केवल **how** टाइप करने की।
- मल्टी‑पेज PDFs, गैर‑अंग्रेज़ी भाषाओं, और ब्लरी स्कैन जैसी सामान्य समस्याओं को संभालने के टिप्स।

### आवश्यकताएँ

- Python 3.8+ स्थापित हो (उदाहरण में `ocr` पैकेज का उपयोग किया गया है जो `pip install ocr-lib` के माध्यम से उपलब्ध है – इसे अपने वास्तविक लाइब्रेरी नाम से बदलें)।
- Python फ़ंक्शन्स और वर्चुअल एनवायरनमेंट्स की बुनियादी परिचितता।
- एक इमेज फ़ाइल (JPEG, PNG, TIFF) जिसे आप प्रोसेस करना चाहते हैं; हम `skewed_page.jpg` को प्लेसहोल्डर के रूप में उपयोग करेंगे।

> **Pro tip:** यदि आप Windows पर हैं, तो OCR लाइब्रेरी इंस्टॉल करते समय टर्मिनल को Administrator के रूप में चलाएँ ताकि परमिशन समस्याओं से बचा जा सके।

## इमेज पर OCR करें – सेटअप और कॉन्फ़िगरेशन

सबसे पहले आपको एक साफ़ OCR इंजन इंस्टेंस चाहिए। इसे ऑपरेशन के पीछे दिमाग समझें; उचित कॉन्फ़िगरेशन के बिना, सबसे तेज़ इमेज भी बेतुके परिणाम देगी।

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Why this matters:**  
`engine.language` सेट करने से OCR इंजन द्वारा अपेक्षित कैरेक्टर सेट सीमित हो जाता है, जिससे सटीकता में उल्लेखनीय वृद्धि होती है। यदि आप इसे छोड़ देते हैं, तो इंजन अनुमान लगाने की कोशिश करेगा, अक्सर सरल शब्दों को गलत पढ़ेगा।

## ऑटोमैटिक डेस्क्यू सक्षम करें – टिल्टेड स्कैन को ठीक करें

स्कैन किए हुए पेज़ कभी भी पूरी तरह सपाट नहीं होते। एक हल्का टिल्ट कैरेक्टर सेगमेंटेशन को बिगाड़ सकता है, “Hello” को “H3llo” बना देता है। `auto_deskew` फ़्लैग आपके लिए यह काम करता है।

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Edge case:** यदि आप जानते हैं कि आपकी इमेज पहले से ही सीधी है, तो deskew को डिसेबल करने से प्रोसेसिंग टाइम में कुछ मिलीसेकंड बच सकते हैं—हजारों पेज़ को बैच जॉब में हैंडल करते समय उपयोगी।

## OCR के लिए इमेज लोड करें – JPEG, PNG, TIFF को सपोर्ट करना

अब हम वास्तव में **load image for OCR** करते हैं। `ocr.Image.load` मेथड लचीला है; यह किसी भी समर्थित रास्टर फ़ॉर्मैट का पाथ स्वीकार करता है।

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Why this step is crucial:** लाइब्रेरी फ़ाइल को एक आंतरिक बिटमैप में पढ़ती है, आवश्यक रंग स्थान परिवर्तन लागू करती है। इसे स्किप करके रॉ बाइट स्ट्रीम पास करने से `FileNotFoundError` उठेगा या, बदतर, चुपचाप खाली परिणाम देगा।

यदि आपको विशेष रूप से **recognize text from JPEG** फ़ाइलों की आवश्यकता है, तो बस फ़ाइल एक्सटेंशन `.jpeg` या `.jpg` रखें। वही कॉल PNG (`.png`) या TIFF (`.tif`) के लिए भी बिना बदलाव के काम करता है।

## इमेज पर OCR करें – इंजन चलाना

इंजन तैयार और इमेज मेमोरी में होने के साथ, अब **perform OCR on image** डेटा का समय है। यह एकल लाइन सभी भारी काम करती है: प्री‑प्रोसेसिंग, सेगमेंटेशन, क्लासिफिकेशन, और टेक्स्ट असेंबली।

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**What happens under the hood?**  
- यदि सक्षम हो तो इंजन deskew ट्रांसफ़ॉर्मेशन लागू करता है।  
- यह कैरेक्टर्स पहचानने के लिए न्यूरल नेटवर्क या Tesseract बैकएंड चलाता है।  
- अंत में, यह कैरेक्टर्स को शब्दों और लाइनों में जोड़ता है, एक समृद्ध `result` ऑब्जेक्ट लौटाता है।

## स्कैन की गई इमेज से टेक्स्ट निकालें – परिणाम आउटपुट करें

अंतिम कदम है **extract text from scanned image** करना और उसे प्रदर्शित करना। `result.text` एट्रिब्यूट में प्लेन‑टेक्स्ट प्रतिनिधित्व होता है।

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

सामान्य आउटपुट इस प्रकार दिखता है:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

यदि OCR इंजन कोई कैरेक्टर नहीं ढूँढ पाता, तो `result.text` एक खाली स्ट्रिंग होगी। ऐसे में, इमेज की क्वालिटी दोबारा जांचें या `engine.confidence_threshold` प्रॉपर्टी को समायोजित करने पर विचार करें (यदि आपकी लाइब्रेरी इसे सपोर्ट करती है)।

## सामान्य विविधताओं को संभालना

### JPEG बनाम PNG से टेक्स्ट पहचानना

दोनों फ़ॉर्मैट सपोर्टेड हैं, लेकिन JPEG कम्प्रेशन आर्टिफैक्ट्स पैदा कर सकता है जो इंजन को भ्रमित कर देते हैं। यदि आप अक्सर गलत पहचान देखते हैं, तो पहले JPEG को PNG में कन्वर्ट करने की कोशिश करें:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### कई भाषाओं वाले इमेज से टेक्स्ट डिटेक्ट करना

यदि आपका दस्तावेज़ अंग्रेज़ी और स्पेनिश दोनों को मिलाता है, तो मल्टी‑लैंग्वेज मोड सेट करें:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

इंजन तब पहचान के दौरान दोनों अल्फ़ाबेट्स को ध्यान में रखेगा।

### स्कैन किए हुए PDFs से टेक्स्ट निकालना

PDFs के लिए, आपको पहले प्रत्येक पेज़ को इमेज में रास्टराइज़ करना होगा। `pdf2image` जैसी लाइब्रेरीज़ इसे आसान बनाती हैं:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

## पूरा कार्यशील उदाहरण

नीचे पूरा स्क्रिप्ट है जिसे आप `ocr_demo.py` फ़ाइल में कॉपी‑पेस्ट कर सकते हैं। इसमें एरर हैंडलिंग और एग्जीक्यूशन टाइम मापने के लिए एक छोटा हेल्पर शामिल है।

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Expected output** (मान लेते हैं कि स्कैन स्पष्ट है):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं इसे हेडलेस सर्वर पर चला सकता हूँ?**  
A: बिल्कुल। लाइब्रेरी GUI के बिना काम करती है; बस सुनिश्चित करें कि आवश्यक नेटिव बाइनरीज़ (जैसे, Tesseract) सर्वर पर इंस्टॉल हों।

**Q: अगर इमेज ब्लरी है तो क्या करें?**  
A: `engine.recognize` से पहले शार्पनिंग फ़िल्टर जोड़ने पर विचार करें। कई OCR लाइब्रेरीज़ `image_preprocessing.sharpen = True` एक्सपोज़ करती हैं या आप OpenCV के `cv2.GaussianBlur` को रिवर्स में उपयोग कर सकते हैं।

**Q: क्या स्क्रिप्ट बैच प्रोसेसिंग सपोर्ट करती है?**  
A: हाँ। `perform_ocr` को फ़ाइल पाथ की सूची पर लूप में रैप करें,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}