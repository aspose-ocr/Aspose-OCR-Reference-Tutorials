---
category: general
date: 2026-03-18
description: इमेज पर OCR करके जल्दी से टेक्स्ट निकालें। जानिए OCR के लिए इमेज कैसे
  लोड करें, OCR इंजन कैसे बनाएं, और भाषा विकल्पों के साथ OCR की सटीकता कैसे बढ़ाएँ।
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: hi
og_description: इस विस्तृत गाइड के साथ छवि पर OCR करें। OCR के लिए छवि लोड करना सीखें,
  OCR इंजन बनाएं, और विश्वसनीय टेक्स्ट निष्कर्षण के लिए OCR की सटीकता सुधारें।
og_title: छवि पर OCR करें – पूर्ण प्रोग्रामिंग ट्यूटोरियल
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: छवि पर OCR करें – चरण-दर-चरण मार्गदर्शिका
url: /hi/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज पर OCR करें – पूर्ण प्रोग्रामिंग ट्यूटोरियल

क्या आपको कभी **perform OCR on image** करने की ज़रूरत पड़ी, लेकिन यह नहीं पता था कि कौन‑सी लाइब्रेरी चुनें या भरोसेमंद परिणाम कैसे प्राप्त करें? आप अकेले नहीं हैं। इस गाइड में हम **extract text from image** करने के लिए आवश्यक सभी चीज़ों को कवर करेंगे, चित्र लोड करने से लेकर भाषा विकल्पों को ट्यून करने तक, ताकि आप हर कदम पर **improve OCR accuracy** कर सकें।

हम बताएँगे कि **load image for OCR** कैसे किया जाता है, **create OCR engine** कैसे बनाते हैं, और प्रत्येक सेटिंग क्यों महत्वपूर्ण है। अंत में आपके पास एक तैयार‑स्क्रिप्ट होगी जो पहचाने गए टेक्स्ट को प्रिंट करेगी, और आप प्रत्येक लाइन के पीछे का “क्यों” समझ पाएँगे—कोई अस्पष्ट “डॉक्यूमेंट देखें” शॉर्टकट नहीं। चलिए शुरू करते हैं।

## What You’ll Need

- Python 3.8+ (कोड f‑strings और type hints का उपयोग करता है)
- काल्पनिक `ocr_lib` पैकेज – `pip install ocr_lib` से इंस्टॉल करें
- स्पष्ट, प्रिंटेड टेक्स्ट वाली इमेज फ़ाइल (जैसे `lab_report.png`)
- एक बेसिक टेक्स्ट एडिटर या IDE (VS Code, PyCharm, या जो भी आपको पसंद हो)

यदि आपके पास ये सब है, तो बढ़िया—आप तैयार हैं। यदि नहीं, तो python.org से Python डाउनलोड करें और pip कमांड चलाएँ; यह सिर्फ एक मिनट लेता है।

![perform OCR on image example](/images/ocr-example.png)

*Alt text: इमेज पर OCR – निकाले गए टेक्स्ट का नमूना आउटपुट।*

## Step 1: Create OCR Engine – How to **create OCR engine** in Python

पहले किसी भी पहचान को करने से पहले, लाइब्रेरी को एक engine ऑब्जेक्ट चाहिए जो कॉन्फ़िगरेशन और रन‑टाइम स्टेट को रखे। इसे ऑपरेशन का दिमाग समझें।

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Why this matters:** इंजन को पहले इंस्टैंशिएट करने से बाद में आप भाषा विकल्प जोड़ सकते हैं, और यह आंतरिक मॉडल को कैश करके बाद के कॉल्स को तेज़ बनाता है।

## Step 2: Load Image for OCR – The correct way to **load image for OCR**

अब जब हमारे पास इंजन है, हमें उसे पढ़ने के लिए कुछ देना होगा। `setImageFromFile` मेथड एक फ़ाइल‑सिस्टम पाथ लेता है; पाथ एब्सोल्यूट या स्क्रिप्ट की वर्किंग डायरेक्टरी के रिलेटिव हो सकता है।

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Pro tip:** एब्सोल्यूट पाथ या `os.path.join` का उपयोग करें ताकि स्क्रिप्ट अलग फ़ोल्डर से चलने पर “file not found” की समस्या न आए।

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Step 3: Improve OCR Accuracy – Tweaking **language options** to **improve OCR accuracy**

आउट‑ऑफ़‑द‑बॉक्स OCR काम करता है, लेकिन डोमेन‑स्पेसिफिक शब्दावली (जैसे लैब जार्गन) अक्सर इसे भ्रमित कर देती है। कस्टम डिक्शनरी और ब्लैकलिस्ट जोड़ने से “0” को “O” के साथ ग़लत पहचानने जैसी समस्याएँ कम होती हैं।

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Why this helps:** डिक्शनरी OCR मॉडल को बताती है कि “HPLC” एक वैध टोकन है, जिससे शब्द को बेतुके टुकड़ों में नहीं तोड़ता। ब्लैकलिस्ट मॉडल को अस्पष्ट प्रतीकों को शोर मानने के लिए कहती है, जो सीधे **improve OCR accuracy** करता है।

## Step 4: Perform OCR on Image – The core **perform OCR on image** call

इंजन तैयार और इमेज अटैच हो जाने के बाद, अब टेक्स्ट को पहचानने का समय है। यह स्टेप एक `OcrResult` ऑब्जेक्ट रिटर्न करता है, जिससे आप रॉ टेक्स्ट, कॉन्फिडेंस स्कोर, या बाउंडिंग बॉक्स क्वेरी कर सकते हैं।

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

यदि इमेज धुंधली है, तो परिणाम में कम कॉन्फिडेंस नंबर दिखेंगे। यह संकेत है कि इमेज को प्री‑प्रोसेस (जैसे कंट्रास्ट बढ़ाना) करना चाहिए इससे पहले कि आप इसे इंजन को दें।

## Step 5: Extract Text from Image – Pulling the final string out

अंत में, हम `OcrResult` से उसका टेक्स्ट प्राप्त करते हैं। `getText()` मेथड एक प्लेन‑टेक्स्ट स्ट्रिंग रिटर्न करता है, जिसे आप फ़ाइल में सेव कर सकते हैं, डेटाबेस में डाल सकते हैं, आदि।

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Expected output:** मान लीजिए `lab_report.png` में एक साधारण टेबल है, तो आउटपुट कुछ इस तरह दिख सकता है:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

यही **extract text from image** का भाग है।

## Full Working Example – Put It All Together

नीचे एक सिंगल स्क्रिप्ट है जो पिछले सेक्शन की सभी हिस्सों को जोड़ती है। आप इसे `run_ocr.py` में कॉपी‑पेस्ट करके `python run_ocr.py` चला सकते हैं।

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Quick verification checklist

| ✅ | Item |
|---|------|
| ✔️ | Engine is created (`create OCR engine`) |
| ✔️ | Image is loaded (`load image for OCR`) |
| ✔️ | Language options are set (`improve OCR accuracy`) |
| ✔️ | OCR is performed (`perform OCR on image`) |
| ✔️ | Text is extracted (`extract text from image`) |

स्क्रिप्ट चलाएँ और कंसोल देखें। यदि आपको “OCR Output” ब्लॉक में अपनी रिपोर्ट की सामग्री दिखती है, तो आपने सफलतापूर्वक **performed OCR on image** कर लिया है।

## Common Pitfalls & How to Avoid Them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Blurry input** | OCR मॉडल अक्षरों को अलग नहीं कर पाता | OpenCV से प्री‑प्रोसेस करें: `cv2.GaussianBlur` या DPI बढ़ाएँ |
| **Wrong language** | डिफ़ॉल्ट भाषा अंग्रेज़ी के अलावा कुछ और सेट हो सकती है | `engine.setLanguage("eng")` को `recognize()` से पहले कॉल करें |
| **Missing dictionary terms** | डोमेन‑स्पेसिफिक शब्द गड़बड़ हो जाते हैं | Step 3 में दिखाए अनुसार `setDictionary` से जोड़ें |
| **Blacklisted characters cause** |  |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}