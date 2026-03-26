---
category: general
date: 2026-03-26
description: इमेज से टेक्स्ट को जल्दी पहचानें, OCR के लिए इमेज को लोड करना सीखें और
  किसी विशिष्ट क्षेत्र से डेटा निकालें। इस व्यावहारिक गाइड का पालन करें।
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: hi
og_description: Python में OCR के लिए छवि लोड करके, रुचि के क्षेत्र को परिभाषित करके
  और साफ़ टेक्स्ट निकालकर छवि से टेक्स्ट पहचानें। पूरी प्रक्रिया सीखें।
og_title: छवि से पाठ पहचानें – पूर्ण पायथन OCR वॉकथ्रू
tags:
- OCR
- Python
- Image Processing
title: छवि से टेक्स्ट पहचानें – चरण-दर-चरण पायथन OCR ट्यूटोरियल
url: /hi/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज से टेक्स्ट पहचानें – पूर्ण Python OCR वॉकथ्रू

क्या आपको कभी **recognize text from image** करने की ज़रूरत पड़ी है लेकिन आप नहीं जानते थे कि कहाँ से शुरू करें? शायद आपके पास कोई स्कैन किया हुआ फ़ॉर्म, रसीद, या स्क्रीनशॉट है और आप केवल एक विशेष बॉक्स के भीतर शब्द चाहते हैं। अच्छी ख़बर यह है कि कुछ ही Python लाइनों के साथ आप OCR के लिए इमेज लोड कर सकते हैं, एक ही क्षेत्र पर फोकस कर सकते हैं, और आवश्यक सटीक टेक्स्ट निकाल सकते हैं—बिना मैन्युअल कॉपी किए।

इस ट्यूटोरियल में हम पूरी प्रक्रिया को चरण‑दर‑चरण देखेंगे: इमेज लोड करना, ROI (Region of Interest) परिभाषित करना, OCR इंजन चलाना, और परिणाम प्रिंट करना। अंत तक आप इस स्निपेट को किसी भी प्रोजेक्ट में एम्बेड कर सकेंगे जिसे इमेज के किसी विशिष्ट भाग से टेक्स्ट निकालने की आवश्यकता है। कोई भारी‑भाड़ वाला इमेज‑प्रोसेसिंग पाइपलाइन नहीं, बस साफ़, पढ़ने योग्य कोड जो आज ही काम करता है।

## आवश्यकताएँ

- Python 3.8+ स्थापित है  
- `ocr` पैकेज (या कोई भी संगत OCR लाइब्रेरी) – `pip install ocr-lib` के साथ इंस्टॉल करें (अपने उपयोग किए जाने वाले वास्तविक पैकेज नाम से बदलें)  
- एक PNG/JPEG इमेज जिसमें वह फ़ॉर्म हो जिसे आप पढ़ना चाहते हैं  
- Python फ़ंक्शन्स और क्लासेज़ की बुनियादी समझ  

यदि आप पहले से इनसे सहज हैं, तो बढ़िया—आप आगे बढ़ सकते हैं। अन्यथा, एक तेज़ कॉफ़ी लें और सुनिश्चित करें कि ऊपर बताए गए आइटम तैयार हैं; बाद के चरण मानते हैं कि वे उपलब्ध हैं।

## चरण 1: OCR इंजन इंस्टेंस बनाएं – “recognize text from image” कोर

हमें सबसे पहले एक ऑब्जेक्ट चाहिए जो OCR इंजन से बात करना जानता हो। इसे आप उस दिमाग की तरह समझें जो बाद में **recognize text from image** डेटा को पहचानता है।

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **यह क्यों महत्वपूर्ण है:** इंजन को एक बार इनिशियलाइज़ करने से आप सेटिंग्स (जैसे भाषा पैक्स) को कई इमेजेज़ में पुन: उपयोग कर सकते हैं, जिससे प्रदर्शन बेहतर होता है और कोड साफ़ रहता है।

## चरण 2: OCR के लिए इमेज लोड करें – चित्र को मेमोरी में लाना

अब हम वास्तव में **load image for OCR** करते हैं। लाइब्रेरी एक सुविधाजनक स्टैटिक मेथड प्रदान करती है जो फ़ाइल को पढ़ती है और एक ऐसा ऑब्जेक्ट रिटर्न करती है जिसे इंजन समझ सके।

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **Pro tip:** यदि आपकी इमेज बड़ी है, तो लोड करने से पहले उसका आकार बदलने पर विचार करें। छोटी इमेजेज़ OCR को तेज़ करती हैं बिना अधिकांश प्रिंटेड टेक्स्ट की सटीकता को घटाए।

## चरण 3: OCR Region of Interest (ROI) परिभाषित करें

अक्सर आपको पूरे पेज की ज़रूरत नहीं होती—सिर्फ वह विशेष बॉक्स जहाँ उपयोगकर्ता ने डेटा भरा है। **OCR region of interest** को परिभाषित करने से इंजन बाकी सबको अनदेखा कर देता है, जिससे शोर कम होता है और प्रोसेसिंग तेज़ होती है।

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **ROI पर फोकस क्यों?**  
> - **Speed:** इंजन कम पिक्सेल स्कैन करता है।  
> - **Accuracy:** ROI के बाहर की बैकग्राउंड ग्राफ़िक्स कैरेक्टर रिकग्निशन को भ्रमित कर सकती हैं।  
> - **Simplicity:** आपको एक साफ़ स्ट्रिंग मिलती है जो ठीक उसी फ़ील्ड से मेल खाती है जिसकी आपको ज़रूरत है।

## चरण 4: OCR प्रक्रिया चलाएँ – सत्य का क्षण

सब कुछ सेटअप होने के बाद, हम अंततः परिभाषित ROI के भीतर **recognize text from image** करते हैं।

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

यदि इंजन कई क्षेत्रों को सपोर्ट करता है, तो `ocr_result` में एक लिस्ट होगी; हमारे सिंगल‑ROI केस में यह एक सरल ऑब्जेक्ट है जिसमें `get_text()` मेथड है।

## चरण 5: टेक्स्ट निकालें और प्रिंट करें – अंतिम आउटपुट प्राप्त करना

अब हम परिणाम ऑब्जेक्ट से साधारण स्ट्रिंग निकालते हैं और उसे प्रदर्शित करते हैं। यहाँ आप आउटपुट को डेटाबेस, CSV फ़ाइल, या किसी भी डाउनस्ट्रीम लॉजिक में प्लग कर सकते हैं।

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**Expected output** (उदाहरण के लिए भरे हुए नाम फ़ील्ड का):

```
Text inside ROI:
 John Doe
```

यदि OCR इंजन अतिरिक्त व्हाइटस्पेस या लाइन ब्रेक्स रिटर्न करता है, तो आप इसे `.strip()` या रेगुलर एक्सप्रेशन से साफ़ कर सकते हैं।

## सामान्य किनारे के मामलों को संभालना

| स्थिति                              | क्या करें                                                               |
|----------------------------------------|--------------------------------------------------------------------------|
| **Low‑resolution image**               | लोड करने से पहले `Pillow` (`Image.resize`) के साथ अपस्केल करें।                  |
| **Skewed or rotated text**             | `ocr.Imaging.Image.rotate` के साथ रोटेशन सुधार लागू करें।               |
| **Multiple languages**                | इंजन पर भाषा पैक सेट करें: `ocr_engine.set_language('eng+spa')`. |
| **No ROI defined**                     | `add_region_of_interest` को स्किप करें; इंजन पूरे इमेज को प्रोसेस करेगा। |
| **Unexpected characters (e.g., commas)** | स्ट्रिंग को पोस्ट‑प्रोसेस करें: `extracted_text.replace(',', '')`.            |

ये टिप्स आपके **load image for OCR** पाइपलाइन को मजबूत बनाते हैं भले ही स्रोत सामग्री परिपूर्ण न हो।

## पूर्ण कार्यशील उदाहरण – कॉपी, पेस्ट, रन

नीचे पूरा स्क्रिप्ट है जिसे आप `.py` फ़ाइल में डालकर चला सकते हैं। इसमें सभी इम्पोर्ट्स, एरर हैंडलिंग, और एक छोटा हेल्पर शामिल है जो इमेज की मौजूदगी की जाँच करता है।

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

इस स्क्रिप्ट को चलाने से ROI से साफ़ किया गया स्ट्रिंग प्रिंट होगा, जिससे आपको उपयोग के लिए तैयार डेटा मिलेगा।

## निष्कर्ष

अब आपके पास एक स्पष्ट, अंत‑से‑अंत विधि है **recognize text from image** करने की, पहले **load image for OCR** करके, एक सटीक **OCR region of interest** परिभाषित करके, और अंत में साफ़ टेक्स्ट निकालने के लिए। यह तरीका किसी भी Python OCR लाइब्रेरी के साथ काम करता है जो ऊपर दिखाए गए पैटर्न का पालन करती है, और आप इसे आसानी से कई ROI, विभिन्न भाषाओं, या प्री‑प्रोसेसिंग स्टेप्स को संभालने के लिए विस्तारित कर सकते हैं।

अगला, आप खोज सकते हैं:

- **image preprocessing for OCR** (थ्रेशोल्डिंग, डीनॉइज़िंग) ताकि शोरयुक्त स्कैन पर सटीकता बढ़े।  
- **extract text from ROI** परिणाम का उपयोग करके pandas DataFrame को भरना बड़े डेटा विश्लेषण के लिए।  
- स्केल पर अधिक विश्वसनीयता की आवश्यकता होने पर क्लाउड‑आधारित OCR सेवा (Google Vision, Azure Computer Vision) पर स्विच करना।

इसे आज़माएँ, अपने फ़ॉर्म के अनुसार आयताकार निर्देशांक को समायोजित करें, और देखें कि ऑटोमेशन कैसे काम करता है। कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}