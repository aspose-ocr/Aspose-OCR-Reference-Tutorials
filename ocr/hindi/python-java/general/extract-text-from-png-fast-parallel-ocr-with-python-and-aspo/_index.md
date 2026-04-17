---
category: general
date: 2026-03-28
description: Aspose OCR का उपयोग करके Python में PNG से तेज़ी से टेक्स्ट निकालें।
  उच्च‑प्रदर्शन परिणामों के लिए समानांतर इमेज रिकग्निशन Python के साथ स्कैन किए गए
  पृष्ठों का टेक्स्ट बदलना सीखें।
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: hi
og_description: Python में Aspose OCR का उपयोग करके PNG से तेज़ी से टेक्स्ट निकालें।
  यह गाइड दिखाता है कि कैसे स्कैन किए गए पृष्ठों का टेक्स्ट समानांतर इमेज रिकग्निशन
  Python के साथ बदलें, जिससे उच्च‑गति वाले परिणाम मिलते हैं।
og_title: PNG से टेक्स्ट निकालें – पाइथन के साथ तेज़ समानांतर OCR
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: PNG से टेक्स्ट निकालें – पाइथन और Aspose के साथ तेज़ समानांतर OCR
url: /hi/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG से टेक्स्ट निकालें – तेज़ समानांतर OCR Python के साथ

क्या आपको कभी **PNG से टेक्स्ट निकालने** की ज़रूरत पड़ी लेकिन सिंगल‑थ्रेडेड OCR बहुत धीमा लग रहा था? आप अकेले नहीं हैं। चाहे आप स्कैन किए हुए रसीदों का ढेर डिजिटाइज़ कर रहे हों या लेक्चर स्लाइड्स को सर्चेबल PDF में बदल रहे हों, अक्सर बॉटलनेक OCR चरण ही होता है।

इस ट्यूटोरियल में हम आपको एक पूर्ण, तैयार‑चलाने‑योग्य समाधान दिखाएंगे जो **स्कैन किए हुए पृष्ठों का टेक्स्ट** समानांतर रूप से बदलता है, Aspose OCR के असिंक्रोनस बैच मोड को Python के `ThreadPoolExecutor` के साथ मिलाकर। अंत तक आप **recognize image text python**‑स्टाइल में टेक्स्ट पहचान सकेंगे, और दहाईयों इमेज़ को उस समय में प्रोसेस करेंगे जो एक साधारण लूप लेता।

> **आप क्या सीखेंगे**  
> * एक पूरी तरह कार्यशील स्क्रिप्ट जो PNG इमेज़ से टेक्स्ट को एक साथ निकालती है।  
> * यह समझना कि असिंक्रोनस बैच मोड क्यों तेज़ है।  
> * बड़े वर्कलोड के लिए समाधान को स्केल करने के टिप्स।

## आपको क्या चाहिए

| पूर्वापेक्षा | कारण |
|--------------|--------|
| Python 3.9+ | आधुनिक सिंटैक्स और टाइप हिंट्स। |
| `aspose-ocr` और `aspose-storage` पैकेज | OCR इंजन और इमेज़ लोडर प्रदान करते हैं। |
| PNG फ़ाइलों का फ़ोल्डर (जैसे, स्कैन किए गए पृष्ठ) | वह स्रोत सामग्री जिसे आप प्रोसेस करना चाहते हैं। |
| Python समवर्तीता का बुनियादी ज्ञान | सहायक लेकिन अनिवार्य नहीं; हम सब कुछ समझाएंगे। |

आप Aspose लाइब्रेरीज़ को इस तरह इंस्टॉल कर सकते हैं:

```bash
pip install aspose-ocr aspose-storage
```

> **Pro tip:** अपने पैकेजों को अपडेट रखें (`pip list --outdated`) ताकि नवीनतम प्रदर्शन सुधारों का लाभ मिल सके।

## चरण 1: Aspose OCR इंजन को असिंक्रोनस बैच मोड में इनिशियलाइज़ करें

सबसे पहले हम एक `OcrEngine` इंस्टेंस बनाते हैं और उसे **असिंक्रोनस बैच मोड** में स्विच करते हैं। यह मोड आंतरिक रूप से रिकग्निशन अनुरोधों को कतारबद्ध करता है, जिससे इंजन कई इमेज़ को प्रोसेस कर सकता है बिना आपके Python थ्रेड को ब्लॉक किए।

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*असिंक्रोनस क्यों?*  
जब आप `recognize` को सिंक्रोनस मोड में कॉल करते हैं, तो कॉल तब तक ब्लॉक रहती है जब तक इमेज़ पूरी तरह प्रोसेस नहीं हो जाती। असिंक्रोनस मोड में, इंजन वर्तमान इमेज़ अभी भी डिकोड हो रही हो, तब भी अगले इमेज़ पर काम शुरू कर सकता है, जिससे I/O और CPU कार्य ओवरलैप हो जाता है।

## चरण 2: उन PNG फ़ाइलों की सूची बनाएं जिन्हें आप प्रोसेस करना चाहते हैं

यहाँ हम इमेज़ की कलेक्शन परिभाषित करते हैं। वास्तविक प्रोजेक्ट में आप यह सूची डायनामिकली जेनरेट कर सकते हैं (जैसे, `glob.glob("*.png")`), लेकिन स्पष्ट रूप से लिखने से उदाहरण समझने में आसान रहता है।

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **Note:** `YOUR_DIRECTORY` को उस वास्तविक पाथ से बदलें जहाँ आपके PNG स्कैन स्थित हैं। यदि आपके पास सैकड़ों फ़ाइलें हैं, तो `os.listdir` का उपयोग करके `.png` फ़ाइलों को फ़िल्टर करने पर विचार करें।

## चरण 3: एक हेल्पर लिखें जो इमेज़ लोड करे और उसका टेक्स्ट रिटर्न करे

यह हेल्पर दो‑स्टेप प्रक्रिया को एब्स्ट्रैक्ट करता है: **Aspose Storage** के ज़रिए फ़ाइल लोड करना और फिर उसे OCR इंजन को देना। एक छोटा डॉकस्ट्रिंग जोड़ने से फ़ंक्शन स्वयं‑डॉक्यूमेंटिंग बन जाता है—भविष्य में मेंटेनेंस के लिए उपयोगी।

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*अलग फ़ंक्शन क्यों?*  
यह थ्रेड‑पूल कोड को साफ़ रखता है और हमें लॉजिक को कहीं और (जैसे, Flask एन्डपॉइंट) पुन: उपयोग करने देता है। साथ ही, I/O को अलग करने से डिबगिंग आसान हो जाती है—यदि कोई विशेष फ़ाइल फेल होती है, तो आप एक्सेप्शन ट्रेस में फ़ाइलनाम देखेंगे।

## चरण 4: थ्रेड पूल के साथ समानांतर इमेज़ रिकग्निशन चलाएँ

अब हम `ThreadPoolExecutor` लाते हैं। डिफ़ॉल्ट रूप से हम चार वर्कर बनाते हैं, लेकिन आप `max_workers` को अपने CPU कोर और इमेज़ सेट के आकार के आधार पर ट्यून कर सकते हैं।

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### यह कैसे देता है समानांतर इमेज़ रिकग्निशन Python

* **ThreadPoolExecutor** वर्कर थ्रेड्स का पूल बनाता है जो प्रत्येक `recognize_image` को कॉल करता है।  
* क्योंकि OCR इंजन असिंक्रोनस बैच मोड में है, प्रत्येक थ्रेड काम को इंजन को सौंप सकता है जबकि वह अभी भी रिस्पॉन्सिव रहता है।  
* `as_completed` फ्यूचर को उनके समाप्त होने के क्रम में यील्ड करता है, इसलिए आपको परिणाम तुरंत मिलते हैं—बड़े बैच को स्ट्रीम करने के लिए परफेक्ट।

> **Common pitfall:** `max_workers=1` सेट करने से समानांतरता का उद्देश्य नष्ट हो जाता है। 8‑कोर मशीन पर `max_workers=8` अक्सर सबसे अच्छा थ्रूपुट देता है, लेकिन अपने हार्डवेयर के लिए सही वैल्यू खोजने हेतु कुछ मान आज़माएँ।

## चरण 5: आउटपुट को वेरिफ़ाई करें और एज केस हैंडल करें

जब आप स्क्रिप्ट चलाएंगे, तो आपको प्रत्येक PNG के लिए टेक्स्ट ब्लॉक दिखेगा, जिसके पहले उसका फ़ाइलनाम प्रीफ़िक्स होगा:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

यदि कोई इमेज़ फेल होती है (करप्ट फ़ाइल, असमर्थित फ़ॉर्मेट), तो `except` ब्लॉक एक मददगार एरर मैसेज प्रिंट करेगा और पूरी बैच क्रैश नहीं होगी।

### समाधान को विस्तारित करना

| परिदृश्य | सुझाया गया बदलाव |
|----------|-----------------|
| **हजारों पृष्ठ** | `ProcessPoolExecutor` पर स्विच करें ताकि कई CPU प्रोसेस उपयोग हो सकें, या सूची को चंक्स में बाँट कर क्रमिक रूप से प्रोसेस करें। |
| **विभिन्न इमेज़ फ़ॉर्मेट (JPG, TIFF)** | `storage.Image.load` मेथड फ़ॉर्मेट को ऑटो‑डिटेक्ट करता है, इसलिए फ़ाइलों को `input_images` में जोड़ दें। |
| **परिणाम संग्रहीत करने की ज़रूरत** | `else` ब्लॉक के अंदर `text` को `.txt` फ़ाइल में लिखें या डेटाबेस में इन्सर्ट करें। |
| **परफ़ॉर्मेंस मॉनिटरिंग** | `recognize_image` को टाइमर (`time.perf_counter`) से रैप करें और फ़ाइल‑प्रति अवधि लॉग करें। |

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा स्क्रिप्ट है, जिसे आप `parallel_ocr.py` नाम की फ़ाइल में रख सकते हैं। कोई भाग नहीं छूटा—आपको जो चाहिए वह सब यहाँ है।

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

फ़ाइल को सेव करें, `YOUR_DIRECTORY` प्लेसहोल्डर को एडजस्ट करें, और चलाएँ:

```bash
python parallel_ocr.py
```

आपको प्रत्येक PNG के लिए निकाला गया टेक्स्ट कंसोल में दिखना चाहिए, ठीक उसी तरह जैसा पहले दिखाया गया था।

## निष्कर्ष

हमने यह दिखाया कि **PNG से टेक्स्ट निकालना** कितना कुशल हो सकता है, Aspose OCR के असिंक्रोनस बैच मोड को Python के `ThreadPoolExecutor` के साथ मिलाकर। स्क्रिप्ट स्कैन किए हुए पृष्ठों का टेक्स्ट समानांतर रूप से बदलती है, जिससे आप **recognize image text python**‑स्टाइल को बिना कस्टम थ्रेड‑पूल लिखे स्केलेबल बना सकते हैं।

यदि आप इसे आगे बढ़ाना चाहते हैं, तो कोशिश करें:

* परिणामों को सर्चेबल SQLite डेटाबेस में स्टोर करना।  
* OCR से पहले OpenCV के साथ इमेज़ प्री‑प्रोसेसिंग (डेस्क्यू, डिनॉइज़) जोड़ना।  
* स्क्रिप्ट को Flask या FastAPI एन्डपॉइंट के पीछे माइक्रोसर्विस के रूप में डिप्लॉय करना।

याद रखें, हाई‑परफ़ॉर्मेंस OCR की कुंजी सिर्फ तेज़ इंजन नहीं, बल्कि उस इंजन को इस तरह फ़ीड करना है जो समवर्तीता को अधिकतम करे। यहाँ दिखाए गए पैटर्न से आप दहाईयों या यहाँ तक कि सैकड़ों PNG स्कैन को न्यूनतम कोड बदलाव के साथ हैंडल कर सकते हैं।

Happy coding, और आपके PDFs हमेशा सर्चेबल रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}