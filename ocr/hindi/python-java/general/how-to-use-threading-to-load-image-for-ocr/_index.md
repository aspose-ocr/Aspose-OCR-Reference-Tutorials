---
category: general
date: 2026-04-26
description: Python में OCR के लिए छवि लोड करने हेतु थ्रेडिंग का उपयोग कैसे करें।
  कॉलबैक, बैकग्राउंड थ्रेड और छवि लोडिंग के साथ असिंक्रोनस OCR प्रोसेसिंग को कुछ ही
  चरणों में सीखें।
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: hi
og_description: Python में OCR के लिए इमेज लोड करने हेतु थ्रेडिंग का उपयोग कैसे करें।
  यह गाइड कॉलबैक्स और बैकग्राउंड निष्पादन के साथ एक पूर्ण, चलाने योग्य उदाहरण दिखाता
  है।
og_title: OCR के लिए इमेज लोड करने हेतु थ्रेडिंग का उपयोग कैसे करें
tags:
- Python
- Threading
- OCR
- Image Processing
title: OCR के लिए इमेज लोड करने हेतु थ्रेडिंग का उपयोग कैसे करें
url: /hi/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# थ्रेडिंग का उपयोग करके OCR के लिए इमेज लोड करना

क्या आपने कभी सोचा है **थ्रेडिंग का उपयोग कैसे करें** OCR के लिए इमेज लोड करने के बारे में, बिना आपके ऐप को फ्रीज़ किए? यह वह स्थिति है जो तब आती है जब आप डेस्कटॉप स्कैनर, वेब सर्विस, या बड़ी तस्वीरों को प्रोसेस करने वाली साधारण स्क्रिप्ट बना रहे हों। अच्छी खबर? कुछ पंक्तियों का Python कोड और सही थ्रेडिंग पैटर्न आपके UI को तेज़ रखेगा जबकि OCR इंजन अपना जादू चलाएगा।

इस ट्यूटोरियल में हम एक पूर्ण, अंत‑से‑अंत उदाहरण के माध्यम से चलेंगे: बड़ी PNG लोड करना, बैकग्राउंड थ्रेड पर OCR शुरू करना, और परिणाम को एक कॉलबैक के साथ हैंडल करना। अंत तक आप न केवल **थ्रेडिंग का उपयोग कैसे करें** बल्कि **OCR के लिए इमेज लोड करना** भी एक साफ़, पुन: उपयोग योग्य तरीके से जानेंगे।

## आपको क्या चाहिए

- Python 3.9+ (हमारा सिंटैक्स किसी भी हालिया संस्करण पर काम करता है)
- `pillow` इमेज हैंडलिंग के लिए (`pip install pillow`)
- `pytesseract` Tesseract OCR के लिए एक हल्का रैपर है (`pip install pytesseract`)
- Tesseract OCR इंजन आपके मशीन पर इंस्टॉल होना चाहिए (डाउनलोड करें [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- एक बड़ी इमेज फ़ाइल जिसे आप प्रोसेस करना चाहते हैं (`large_image.png` इस गाइड में)

कोई अतिरिक्त फ्रेमवर्क नहीं, कोई async/await नहीं—सिर्फ क्लासिक `threading` और एक कॉलबैक।

## चरण 1: थ्रेडिंग मॉड्यूल इम्पोर्ट करें (बैकग्राउंड एक्सिक्यूशन के लिए आवश्यक)

सबसे पहले हम `threading` मॉड्यूल को इम्पोर्ट करते हैं। यह हमें `Thread` क्लास देता है, जो किसी भी फ़ंक्शन को अलग OS थ्रेड में चलाने की अनुमति देता है।

```python
import threading
```

*Why this matters*: यदि आप OCR को मुख्य थ्रेड पर चलाते हैं, तो आपका प्रोग्राम (विशेषकर GUI) OCR समाप्त होने तक फ्रीज़ हो जाएगा। कार्य को बैकग्राउंड थ्रेड को सौंपने से मुख्य थ्रेड UI को अपडेट करने, उपयोगकर्ता इनपुट संभालने, या अन्य कार्य शुरू करने के लिए मुक्त रहता है।

## चरण 2: एक कॉलबैक परिभाषित करें जो OCR समाप्त होने पर कॉल किया जाएगा

एक कॉलबैक बस एक फ़ंक्शन है जिसे कोई अन्य कोड भाग काम समाप्त होने पर कॉल करता है। यहाँ हम पहचाने गए टेक्स्ट को प्रिंट करेंगे, लेकिन आप इसे स्टोर कर सकते हैं, नेटवर्क पर भेज सकते हैं, या UI विजेट को अपडेट कर सकते हैं।

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*Pro tip*: कॉलबैक को हल्का रखें। कॉलबैक के अंदर भारी प्रोसेसिंग थ्रेडिंग के उद्देश्य को नष्ट कर देती है क्योंकि यह अभी भी उस थ्रेड को ब्लॉक कर देगा जो इसे कॉल करता है (अक्सर मुख्य थ्रेड)।

## चरण 3: वह इमेज लोड करें जिसे आप प्रोसेस करना चाहते हैं

इमेज लोड करना OCR से अलग कार्य है, लेकिन यह समग्र वर्कफ़्लो का हिस्सा है। Pillow का उपयोग इसे बहुत आसान बनाता है।

```python
from PIL import Image

def load_image(path: str) -> Image.Image:
    """Loads an image from disk and returns a Pillow Image object."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img
    except Exception as exc:
        raise RuntimeError(f"Failed to load image: {exc}") from exc
```

*Why we do it here*: यदि इमेज बहुत बड़ी है, तो मुख्य थ्रेड पर लोड करने से पहले ही एक झटका लग सकता है। कई वास्तविक‑दुनिया के ऐप्स में आप लोडिंग को भी थ्रेड में ऑफ‑लोड करेंगे, लेकिन स्पष्टता के लिए हम इसे सिंक्रोनस रखते हैं।

## चरण 4: एक छोटा OCR इंजन रैपर बनाएं

मूल स्निपेट ने `engine.process_async` का उपयोग किया था। हम इसे एक छोटे क्लास के साथ नकल करेंगे जो आंतरिक रूप से एक थ्रेड शुरू करता है और समाप्त होने पर प्रदान किए गए कॉलबैक को कॉल करता है।

```python
import pytesseract

class SimpleOcrEngine:
    """A minimal OCR engine that runs pytesseract in a background thread."""

    def __init__(self, image: Image.Image):
        self.image = image

    def _run_ocr(self, callback):
        """Internal method executed in the worker thread."""
        try:
            # pytesseract returns the recognized text as a plain string
            text = pytesseract.image_to_string(self.image)
            callback(text)
        except Exception as exc:
            callback(f"OCR failed: {exc}")

    def process_async(self, callback):
        """Public method to start OCR on a new thread."""
        worker = threading.Thread(target=self._run_ocr, args=(callback,))
        worker.daemon = True          # Daemon so it won’t block program exit
        worker.start()
        print("OCR thread started…")
```

*Explanation*:  
- `_run_ocr` भारी काम करता है।  
- `process_async` एक `Thread` ऑब्जेक्ट बनाता है, इसे डेमन के रूप में मार्क करता है (ताकि इंटरप्रेटर थ्रेड चल रहा हो तो भी बाहर निकल सके), और इसे शुरू करता है।  
- कॉलबैक को या तो OCR टेक्स्ट या एक एरर मैसेज मिलता है।

## चरण 5: सब कुछ जोड़ें और OCR चलते समय अन्य काम करें

अब हम पूरे फ्लो को व्यवस्थित करते हैं: इमेज लोड करना, इंजन को इंस्टैंशिएट करना, async OCR शुरू करना, और मुख्य थ्रेड को कुछ और काम से व्यस्त रखना (यहाँ हम बस एक संदेश प्रिंट करते हैं)।

```python
if __name__ == "__main__":
    # 1️⃣ Load the image you want to OCR
    img_path = "YOUR_DIRECTORY/large_image.png"
    image = load_image(img_path)

    # 2️⃣ Create the OCR engine instance
    engine = SimpleOcrEngine(image)

    # 3️⃣ Start OCR on a background thread, passing our callback
    engine.process_async(callback=ocr_done)

    # 4️⃣ Do other work while OCR runs (simulated with a loop)
    for i in range(5):
        print(f"Main thread doing other work… ({i+1}/5)")
        # In a real app you might update a progress bar, handle UI events, etc.
        threading.Event().wait(0.5)  # Sleep 0.5 s without blocking the OS thread

    # Give the OCR thread a moment to finish before the script exits
    threading.Event().wait(2)
    print("Script finished.")
```

**अपेक्षित आउटपुट (संक्षिप्त रूप में):**

```
Image 'YOUR_DIRECTORY/large_image.png' loaded – size: (3840, 2160)
OCR thread started…
Main thread doing other work… (1/5)
Main thread doing other work… (2/5)
...
--- Async OCR finished ---
The quick brown fox jumps over the lazy dog.
Script finished.
```

यदि OCR विफल हो जाता है, तो कॉलबैक टेक्स्ट के बजाय एक एरर मैसेज प्रिंट करेगा।

---

## यह तरीका साधारण लूप से बेहतर क्यों काम करता है

- **Responsiveness**: मुख्य थ्रेड कभी भी OCR कॉल पर ब्लॉक नहीं होता, जो बड़ी इमेज के लिए सेकंड ले सकता है।
- **Scalability**: आप कई `SimpleOcrEngine` इंस्टेंस बना सकते हैं, प्रत्येक अपने थ्रेड पर, जिससे इमेजों का बैच एक साथ प्रोसेस हो सके।
- **Separation of Concerns**: लोडिंग, प्रोसेसिंग, और परिणाम हैंडलिंग स्पष्ट रूप से अलग हैं, जिससे कोड का परीक्षण और रखरखाव आसान हो जाता है।

## सामान्य pitfalls और उन्हें कैसे टालें

| समस्या | क्या होता है | समाधान |
|---------|--------------|-----|
| थ्रेड को *daemon* के रूप में मार्क करना भूल जाना | मुख्य कार्य समाप्त होने के बाद स्क्रिप्ट लटक जाती है क्योंकि OCR थ्रेड अभी भी जीवित है। | एक्ज़िट करने से पहले `worker.daemon = True` सेट करें **या** थ्रेड को `join()` करें। |
| परिणाम के लिए ग्लोबल वेरिएबल का उपयोग बिना लॉक के | जब कई थ्रेड एक साथ लिखते हैं तो रेस कंडीशन डेटा को भ्रष्ट कर सकती है। | परिणाम को कॉलबैक के माध्यम से पास करें (जैसा हम करते हैं) या `queue.Queue` जैसे थ्रेड‑सेफ़ कंटेनर का उपयोग करें। |
| मुख्य थ्रेड पर बड़ी इमेज लोड करना | बैकग्राउंड OCR शुरू होने से पहले UI फ्रीज़ हो जाता है। | इमेज लोडिंग को भी थ्रेड पर ऑफ‑लोड करें, या लेज़ी लोडिंग तकनीकें उपयोग करें। |
| वर्कर थ्रेड के अंदर एक्सेप्शन को हैंडल न करना | अनहैंडल्ड एक्सेप्शन थ्रेड को चुपचाप समाप्त कर देती है, जिससे आपको कोई परिणाम नहीं मिलता। | `try/except` में OCR लॉजिक को रैप करें और एरर को कॉलबैक तक पहुंचाएँ। |

## इस पैटर्न का विस्तार

- **Progress Reporting**: OCR थ्रेड से मुख्य थ्रेड तक मध्यवर्ती प्रोग्रेस प्रतिशत पुश करने के लिए साझा `queue.Queue` का उपयोग करें।
- **Thread Pool**: बैच प्रोसेसिंग के लिए व्यक्तिगत `Thread` ऑब्जेक्ट्स को `concurrent.futures.ThreadPoolExecutor` से बदलें।
- **GUI Integration**: Tkinter या PyQt ऐप में, कॉलबैक को `after()` (Tkinter) या `QTimer.singleShot` (Qt) के साथ शेड्यूल करें ताकि UI अपडेट मुख्य थ्रेड पर हों।

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

```python
import threading
from PIL import Image
import pytesseract

def ocr_done(result_text: str) -> None:
    """Callback invoked when OCR finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)

def load_image(path: str) -> Image.Image:
    """Load an image and report its size."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}