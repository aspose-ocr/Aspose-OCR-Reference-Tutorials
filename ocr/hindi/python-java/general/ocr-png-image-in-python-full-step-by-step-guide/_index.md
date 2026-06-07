---
category: general
date: 2026-06-06
description: Python के साथ OCR PNG इमेज – सीखें कैसे इमेज से टेक्स्ट निकालें, एक Python
  OCR उदाहरण चलाएँ और यहाँ तक कि प्राचीन ग्रीक टेक्स्ट भी आसानी से पढ़ें।
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: hi
og_description: Python में OCR PNG इमेज की व्याख्या। यह गाइड दिखाता है कि कैसे इमेज
  से टेक्स्ट निकाला जाए, Python OCR उदाहरण चलाया जाए और आसानी से प्राचीन ग्रीक पढ़ा
  जाए।
og_title: Python में OCR PNG इमेज – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python में PNG इमेज का OCR – पूर्ण चरण‑दर‑चरण मार्गदर्शिका
url: /hi/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में OCR PNG इमेज – पूर्ण चरण‑दर‑चरण गाइड

क्या आपने कभी सोचा है कि **OCR PNG image** फ़ाइलों को सीधे Python स्क्रिप्ट से कैसे किया जाए? शायद आपके पास स्कैन किए हुए प्राचीन पांडुलिपियों की एक फ़ोल्डर है और आपको **extract text from image** फ़ाइलों को मैन्युअल रूप से टाइप किए बिना निकालना है। अच्छी खबर यह है कि आपको कंप्यूटर विज़न में पीएचडी की जरूरत नहीं है—बस कुछ लाइनों का कोड और सही लाइब्रेरी, और आप सेकंडों में प्राचीन ग्रीक पढ़ पाएँगे।

इस ट्यूटोरियल में हम एक **python OCR example** के माध्यम से चलेंगे जो PNG से टेक्स्ट पहचानता है, भाषा को Greek polytonic पर सेट करता है, और परिणाम प्रिंट करता है। अंत तक आप बिल्कुल जानेंगे कि कैसे **recognize image text** किया जाता है, सामान्य समस्याओं का समाधान करें, और स्क्रिप्ट को अन्य भाषाओं या इमेज फ़ॉर्मेट्स के लिए अनुकूलित किया जा सकता है।

## आप क्या सीखेंगे

- Python OCR लाइब्रेरी (pytesseract + Tesseract OCR) स्थापित और कॉन्फ़िगर करें
- एक OCR इंजन इंस्टेंस बनाएं और PNG फ़ाइल लोड करें
- पहचान भाषा को Greek polytonic पर सेट करें ताकि आप **read ancient greek** कर सकें
- पहचाने गए टेक्स्ट को आउटपुट करें और सामान्य समस्याओं का समाधान करें
- स्क्रिप्ट को कई PNGs को बैच‑प्रोसेस करने या किसी अन्य भाषा में स्विच करने के लिए विस्तारित करें

### आवश्यकताएँ

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | आधुनिक सिंटैक्स और टाइप हिंट्स |
| `pytesseract` package | Tesseract इंजन के चारों ओर का हल्का रैपर |
| Tesseract OCR binaries (≥ 5.0) | वास्तविक इंजन जो भारी काम करता है |
| Greek language data (`grc.traineddata`) | **read ancient greek** के लिए सही रूप से आवश्यक |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | हमारा लक्ष्य **ocr png image** डेमो के लिए |

आप Python पक्ष को इस प्रकार स्थापित कर सकते हैं:

```bash
pip install pytesseract Pillow
```

और Ubuntu/macOS पर आप स्वयं इंजन जोड़ेंगे:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Greek polytonic प्रशिक्षित डेटा डाउनलोड करना न भूलें:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

* (पाथ अलग हो सकता है; यदि आवश्यक हो तो `TESSDATA_PREFIX` समायोजित करें।)*

## OCR PNG इमेज: इंजन इंस्टेंस बनाएं

पहली चीज़ जो हमें चाहिए वह एक ऑब्जेक्ट है जो Tesseract से बात करता है। `pytesseract` में इंजन को मॉड्यूल‑लेवल फ़ंक्शन्स के माध्यम से एक्सेस किया जाता है, लेकिन स्पष्टता के लिए हम इसे एक छोटी क्लास में रैप करेंगे। यह मूल स्निपेट में देखे गए “engine” कॉन्सेप्ट को दर्शाता है।

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**क्यों रैप करें?**  
- सार्वजनिक API को उसी स्निपेट जैसा रखता है जिससे आप शुरू हुए थे, जिससे माइग्रेशन आसान हो जाता है।  
- मुख्य प्रवाह को छुए बिना बाद में लॉगिंग या एरर हैंडलिंग जोड़ने की अनुमति देता है।  
- अच्छा OOP अभ्यास दर्शाता है—जो वरिष्ठ डेवलपर्स सराहते हैं।

## इमेज से टेक्स्ट निकालें: भाषा को Greek Polytonic पर सेट करें

अब जब हमारे पास इंजन है, हमें उसे बताना है कि कौन सी भाषा की अपेक्षा करनी है। Greek polytonic में ऐसे डायाक्रिटिक्स होते हैं जो मानक “greek” डेटा में नहीं होते, इसलिए हम Tesseract को `grc` प्रशिक्षित फ़ाइल की ओर इंगित करते हैं।

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

यदि आप कभी किसी अन्य भाषा में **extract text from image** फ़ाइलें निकालना चाहते हैं, तो बस `"grc"` को `"eng"` (अंग्रेज़ी), `"fra"` (फ़्रेंच) आदि से बदलें। वही लाइन किसी भी स्थापित भाषा के लिए काम करती है।

## इमेज टेक्स्ट पहचानें: PNG पर OCR चलाएँ

भाषा सेट करने के बाद, हम PNG को इंजन में फीड करते हैं। मूल उदाहरण में हार्ड‑कोडेड पाथ उपयोग किया गया था; हम इसे `Path` ऑब्जेक्ट्स का उपयोग करके थोड़ा अधिक लचीला बनाएँगे।

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**टिप्स और किनारे के केस**

- **File not found** – कॉल को `try/except FileNotFoundError` में रैप करें ताकि एक मित्रवत संदेश दिया जा सके।  
- **Low‑resolution PNG** – OCR से पहले Pillow के साथ प्री‑प्रोसेसिंग (जैसे, रिसाइज़िंग, बाइनराइज़ेशन) पर विचार करें।  
- **Non‑Greek text** – Tesseract अभी भी डिकोड करने की कोशिश करेगा, लेकिन सटीकता तेज़ी से घटती है। हमेशा भाषा से मेल रखें।

## पहचाने गए टेक्स्ट को आउटपुट करें

अंत में, हम परिणाम को प्रिंट करते हैं। वास्तविक प्रोजेक्ट में आप इसे डेटाबेस, CSV, या यहाँ तक कि ट्रांसलेशन पाइपलाइन में भी फीड कर सकते हैं।

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

जब आप स्क्रिप्ट को प्राचीन ग्रीक शिलालेख की स्पष्ट स्कैन पर चलाते हैं, तो आपको कुछ इस तरह दिखना चाहिए:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

यदि आउटपुट गड़बड़ दिखता है, तो दोबारा जांचें कि **greek.traineddata** फ़ाइल सही फ़ोल्डर में है और PNG बहुत शोरयुक्त नहीं है।

## पूर्ण कार्यशील उदाहरण (सभी चरण एक स्क्रिप्ट में)

नीचे पूर्ण, तैयार‑चलाने योग्य प्रोग्राम है। इसे `ocr_greek.py` के रूप में सहेजें और `python ocr_greek.py` चलाएँ।

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**अपेक्षित आउटपुट** (संक्षिप्त रूप में):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

यदि आप सही ग्रीक अक्षर देखते हैं, तो बधाई—आपने Python में सफलतापूर्वक **ocr png image** ऑपरेशन किया है!

## सामान्य प्रश्न और प्रो टिप्स

### शोरयुक्त PNG पर सटीकता कैसे बढ़ाएँ?

- इमेज को ग्रेस्केल में बदलें: `img = img.convert('L')`
- बाइनरी थ्रेशोल्ड लागू करें: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)` के साथ अपस्केल करें

ये कदम अक्सर एक **recognize image text** दुःस्वप्न को साफ़ परिणाम में बदल देते हैं।

### क्या मैं PNGs के पूरे फ़ोल्डर को प्रोसेस कर सकता हूँ?

बिल्कुल। `recognize_image` कॉल को `Path.glob("*.png")` पर `for` लूप में रैप करें। प्रत्येक परिणाम को डिक्शनरी में रखें या बाद में विश्लेषण के लिए CSV में लिखें।

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### यदि मुझे केवल संख्याएँ निकालनी हों तो क्या करें?

`image_to_string` को एक कस्टम **config** स्ट्रिंग पास करें:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

इस तरह आप **extract text from image** फ़ाइलें निकाल सकते हैं जिनमें टेबल, सीरियल नंबर, या टाइमस्टैम्प होते हैं।

### क्या कॉन्फिडेंस स्कोर प्राप्त करने का तरीका है?

हाँ—`pytesseract.image_to_data` का उपयोग करें जो प्रत्येक शब्द के कॉन्फिडेंस के साथ TSV लौटाता है। आप अंतिम स्ट्रिंग बनाने से पहले कम‑कॉन्फिडेंस टोकन को फ़िल्टर कर सकते हैं।

## ट्यूटोरियल का विस्तार

अब जब आप बुनियादी बातों में निपुण हो गए हैं, तो इन संबंधित विषयों को देखें:

- **Batch OCR with multiprocessing** – PNGs के बड़े कॉर्पोरा को तेज़ करने के लिए।  
- **Hybrid OCR + NLP pipelines** – निकाले गए प्राचीन ग्रीक को स्वचालित रूप से आधुनिक अंग्रेज़ी में अनुवाद करने के लिए।  
- **Alternative engines** – विशिष्ट उपयोग‑केस के लिए `easyocr` या `opencv`‑आधारित विधियों को आज़माएँ।  
- **Cloud OCR services** – सर्वरलेस स्केलिंग के लिए Google Vision, Azure Computer Vision, या AWS Textract।

इनमें से प्रत्येक हमारे द्वारा कवर किए गए मूल **python ocr example** पर आधारित है, इसलिए आप गहराई में जाने में सहज महसूस करेंगे।

## निष्कर्ष

हमने एक सरल स्निपेट को Python में एक मजबूत **ocr png image** वर्कफ़्लो में बदल दिया है। `OcrEngine` बनाकर, भाषा को Greek polytonic पर सेट करके, PNG फीड करके, और परिणाम प्रिंट करके, अब आप जानते हैं कि **extract text from image** फ़ाइलें, **recognize image text** कैसे करें, और यहाँ तक कि **read ancient greek** भी।

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों की खोज करने में मदद करेंगे।

- [Aspose OCR के साथ इमेज से टेक्स्ट निकालें – चरण‑दर‑चरण गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [OCR इमेज पहचान में थ्रेशोल्ड वैल्यू कैसे सेट करें](/ocr/english/net/ocr-settings/set-threshold-value/)
- [एकाधिक भाषाओं के लिए Aspose OCR के साथ टेक्स्ट इमेज पहचानें](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}