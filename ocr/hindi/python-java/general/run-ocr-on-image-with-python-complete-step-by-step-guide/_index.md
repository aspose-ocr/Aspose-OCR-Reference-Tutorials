---
category: general
date: 2026-06-06
description: Python का उपयोग करके छवि पर OCR चलाएँ और विश्वास स्कोर देखें। सीखें कि
  कम‑विश्वास वाले शब्दों को कैसे फ़िल्टर करें, थ्रेशोल्ड सेट करें, और किनारी मामलों
  को कैसे संभालें।
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: hi
og_description: Python में छवि पर OCR चलाएँ, विश्वास स्तरों की जाँच करें, और कम‑विश्वास
  वाले शब्दों को फ़िल्टर करें। यह ट्यूटोरियल आपको एक पूर्ण, चलाने योग्य उदाहरण के
  माध्यम से ले जाता है।
og_title: Python के साथ छवि पर OCR चलाएँ – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Python के साथ छवि पर OCR चलाएँ – पूर्ण चरण‑दर‑चरण गाइड
url: /hi/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python के साथ इमेज पर OCR चलाएँ – पूर्ण चरण‑दर‑चरण गाइड

क्या आपको कभी **run OCR on image** फ़ाइलों को चलाने की ज़रूरत पड़ी है लेकिन यह नहीं पता था कि उनसे विश्वसनीय टेक्स्ट कैसे प्राप्त करें? आप अकेले नहीं हैं—कई डेवलपर्स इसी समस्या का सामना करते हैं जब निकाले गए शब्द अस्थिर लगते हैं और confidence स्कोर रहस्य बन जाता है।  

इस गाइड में हम सीधे एक कार्यशील समाधान में डुबकी लगाएंगे: आप देखेंगे कि **run OCR on image** कैसे किया जाता है, समग्र confidence कैसे पढ़ा जाता है, और किसी भी low‑confidence शब्द को कैसे निकाला जाए जिसे मैन्युअल समीक्षा की आवश्यकता हो सकती है। अंत तक आपके पास एक पुन: उपयोग योग्य स्क्रिप्ट होगी, आप समझेंगे कि प्रत्येक पंक्ति क्यों महत्वपूर्ण है, और अपने प्रोजेक्ट्स के लिए confidence थ्रेशोल्ड को कैसे समायोजित किया जाए।

## इस ट्यूटोरियल में क्या कवर किया गया है

हम पूरे वर्कफ़्लो को चरण‑दर‑चरण देखेंगे—इमेज लोड करने से लेकर उन शब्दों की साफ़ रिपोर्ट प्रिंट करने तक जो 80 % confidence सीमा से नीचे गिरते हैं। इस दौरान हम चर्चा करेंगे:

* एक ठोस OCR इंजन चुनना (हम **EasyOCR**, एक लोकप्रिय Python OCR लाइब्रेरी का उपयोग करेंगे)  
* `confidence` एट्रिब्यूट की व्याख्या करना जो हर OCR परिणाम लौटाता है  
* कस्टम **OCR confidence threshold** के साथ शब्दों को फ़िल्टर करना  
* बैच प्रोसेसिंग या **pytesseract** जैसे वैकल्पिक इंजनों के लिए स्क्रिप्ट को विस्तारित करना  

कोई पूर्व OCR अनुभव आवश्यक नहीं है, बस Python की बुनियादी समझ और एक कार्यशील वातावरण (Python 3.9+ की सिफारिश) चाहिए।  

धुंधली स्क्रीनशॉट्स को साफ़, खोजने योग्य टेक्स्ट में बदलने के लिए तैयार हैं? चलिए शुरू करते हैं।

---

## ## Python के साथ इमेज पर OCR कैसे चलाएँ

ट्यूटोरियल का मुख्य भाग एक तीन‑स्टेप स्निपेट है जो आपने पहले देखा कोड को प्रतिबिंबित करता है। नीचे हम प्रत्येक पंक्ति को तोड़ेंगे, कारण समझाएंगे, और फिर आपको एक पूर्ण, कॉपी‑एंड‑पेस्ट‑तैयार स्क्रिप्ट देंगे।

### चरण 1: OCR इंजन स्थापित और इम्पोर्ट करें

सबसे पहले, सुनिश्चित करें कि OCR लाइब्रेरी उपलब्ध है। **EasyOCR** कई भाषाओं के लिए तुरंत काम करता है और आपको प्रत्येक शब्द के लिए confidence स्कोर देता है।

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Why EasyOCR?* यह एक डीप‑लर्निंग मॉडल को बंडल करता है जो विविध डेटासेट पर प्रशिक्षित है, इसलिए आप आमतौर पर पुराने Tesseract इंजन की तुलना में उच्च confidence मान प्राप्त करते हैं, विशेषकर मिश्रित‑गुणवत्ता वाली इमेज पर।

> **Pro tip:** यदि आप सीमित वातावरण (जैसे, एक छोटा Docker कंटेनर) में हैं, तो `pytesseract` हल्का हो सकता है, लेकिन आप EasyOCR द्वारा प्रदान की गई कुछ आधुनिक सटीकता खो देंगे।

### चरण 2: इमेज पर OCR चलाएँ

अब हम वास्तव में **run OCR on image** करते हैं। मूल उदाहरण की `recognize_image` मेथड को EasyOCR की `readtext` कॉल से बदल दिया गया है, जो `(bbox, text, confidence)` ट्यूपल की सूची लौटाती है।

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

`ocr_results` में प्रत्येक एंट्री इस प्रकार दिखती है:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

तीसरा तत्व (`0.92` उदाहरण में) confidence स्कोर है जो 0 से 1 तक रहता है।

### चरण 3: समग्र confidence का सारांश

पहले के स्निपेट के विपरीत जो एकल `confidence` एट्रिब्यूट प्रिंट करता था, EasyOCR प्रत्येक शब्द के लिए confidence देता है। समग्र समझ पाने के लिए, हम उनका औसत निकालेंगे:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Why average?* यह आपको एक त्वरित स्वास्थ्य जांच देता है—यदि समग्र confidence, उदाहरण के लिए, 70 % से नीचे है, तो आपको संभवतः इमेज को सुधारना होगा (बेहतर प्रकाश, प्री‑प्रोसेसिंग, आदि)।

### चरण 4: कम‑confidence वाले शब्दों की सूची बनाएँ

अब वह भाग आता है जो सीधे “उन शब्दों की सूची बनाता है जिनका confidence वांछित थ्रेशोल्ड से नीचे है” की आवश्यकता को पूरा करता है। हम डिफ़ॉल्ट रूप से **OCR confidence threshold** को 0.80 (80 %) पर सेट करेंगे, लेकिन आप इसे समायोजित कर सकते हैं।

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

यह लूप प्रत्येक शब्द को प्रिंट करता है जो कट नहीं हुआ, उसके प्रतिशत confidence के साथ। यह मूल `for recognized_word in recognition_result.words` लूप का सटीक समकक्ष है, लेकिन अब EasyOCR के आउटपुट फ़ॉर्मेट के साथ काम करता है।

---

## ## OCR confidence स्कोर को समझना

Confidence कोई जादुई संख्या नहीं है; यह मॉडल का अनुमान है कि वह किसी विशेष ट्रांसक्रिप्शन के बारे में कितना आश्वस्त है। यहाँ कुछ बातें हैं जिन्हें ध्यान में रखना चाहिए:

| स्थिति | सामान्य confidence | क्या करें |
|-----------|-------------------|------------|
| स्पष्ट, उच्च‑रिज़ॉल्यूशन स्कैन | 0.95 – 1.00 | कोई अतिरिक्त काम आवश्यक नहीं |
| हल्का धुंधलापन या असमान प्रकाश | 0.80 – 0.94 | हल्का प्री‑प्रोसेसिंग (कॉन्ट्रास्ट बढ़ाना) पर विचार करें |
| भारी शोर, घुमा हुआ टेक्स्ट | < 0.70 | इमेज प्री‑प्रोसेसिंग (डेस्क्यू, डीनॉइज़) लागू करें या किसी अन्य OCR इंजन पर स्विच करें |

> **Watch out:** कुछ भाषाएँ (जैसे, कर्सिव हस्तलेख) स्वाभाविक रूप से कम स्कोर देती हैं। थ्रेशोल्ड को उसी अनुसार समायोजित करें।

### एज केस और विविधताएँ

1. **Batch Processing** – यदि आपको बड़े पैमाने पर **run OCR on image** फ़ाइलें चलानी हैं, तो ऊपर की लॉजिक को एक लूप में लपेटें जो किसी डायरेक्टरी पर इटररेट करता है।  
2. **Multiple Languages** – `easyocr.Reader` को `['en', 'fr']` जैसी सूची पास करें और इंजन दोनों को पहचान लेगा।  
3. **Alternative Engines** – क्या आप **pytesseract** आज़माना चाहते हैं? रीडर ब्लॉक को इस से बदलें:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   फिर आपको प्रति‑अक्षर confidence को प्रति‑शब्द मानों में एकत्रित करना होगा—थोड़ा अधिक काम है लेकिन संभव है।

4. **Pre‑processing Tricks** – OpenCV फ़िल्टर (`cv2.threshold`, `cv2.GaussianBlur`) लागू करने से शोरयुक्त स्कैन की confidence बढ़ सकती है।  

---

## ## पूर्ण, तैयार‑चलाने‑योग्य स्क्रिप्ट

नीचे पूरा Python फ़ाइल है जिसे आप अपने प्रोजेक्ट में डाल सकते हैं। इसे `ocr_report.py` के रूप में सहेजें और `python ocr_report.py` चलाएँ। सुनिश्चित करें कि इमेज पाथ वास्तविक फ़ाइल की ओर इशारा करता है।

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Expected output** (आपके नंबर अलग हो सकते हैं):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

यदि हर शब्द 80 % की सीमा को पार करता है तो आपको मैत्रीपूर्ण “All words meet the confidence threshold.” संदेश दिखेगा।

---

## ## अक्सर पूछे जाने वाले प्रश्न (FAQ)

**Q: क्या यह PDFs के साथ काम करता है?**  
A: सीधे नहीं। प्रत्येक PDF पेज को पहले इमेज में बदलें (जैसे, `pdf2image` से) और फिर PNG/JPEG को स्क्रिप्ट में फीड करें।

**Q: मेरे confidence नंबर सभी कम हैं—मैं क्या करूँ?**  
A: इमेज प्री‑प्रोसेसिंग आज़माएँ: कॉन्ट्रास्ट बढ़ाएँ, बैकग्राउंड शोर हटाएँ, या इमेज को क्षैतिज बेसलाइन पर घुमाएँ। EasyOCR एक `contrast_ths` पैरामीटर भी स्वीकार करता है जिसे आप समायोजित कर सकते हैं।

**Q: क्या मैं परिणामों को CSV में एक्सपोर्ट कर सकता हूँ?**  
A: बिल्कुल। लो‑confidence लूप के बाद, `ocr_results` को `csv.DictWriter` में लिखें जहाँ प्रत्येक पंक्ति में `text`, `confidence`, और बाउंडिंग‑बॉक्स कॉर्डिनेट्स हों।

**Q: क्या कोई GPU‑त्वरित संस्करण है?**  
A: EasyOCR स्वचालित रूप से CUDA का उपयोग करता है यदि संगत GPU और PyTorch स्थापित हैं। स्क्रिप्ट चलाने से पहले `torch.cuda.is_available()` से जांचें।

---

## निष्कर्ष

हमने अभी **run OCR on image** Python का उपयोग करके किया, समग्र confidence की जांच की, और किसी भी low‑confidence शब्द को अलग किया जिसे 

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}