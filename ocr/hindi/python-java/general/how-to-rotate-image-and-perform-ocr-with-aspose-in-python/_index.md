---
category: general
date: 2026-03-26
description: Python में छवि को घुमाना और OCR करना सीखें। यह गाइड यह भी दिखाता है कि
  OCR के लिए छवि को कैसे पूर्व-प्रसंस्करण करें और छवि से प्रभावी ढंग से टेक्स्ट निकालें।
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: hi
og_description: Aspose OCR का उपयोग करके छवि को सही ढंग से घुमाएँ और फिर छवि से टेक्स्ट
  पहचानें। OCR के लिए छवि को पूर्व-प्रसंस्करण करने और छवि से टेक्स्ट निकालने के लिए
  इस चरण‑दर‑चरण ट्यूटोरियल का पालन करें।
og_title: छवि को घुमाना और OCR करना – पूर्ण पायथन गाइड
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Python में Aspose के साथ इमेज को घुमाना और OCR करना
url: /hi/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# कैसे इमेज को घुमाएँ और Aspose के साथ Python में OCR करें

क्या आपने कभी सोचा है **इमेज को कैसे घुमाएँ** ताकि OCR इंजन वास्तव में टेक्स्ट पढ़ सके? शायद आपने कोई फॉर्म स्कैन किया जो साइडवेज़ आया, या कैमरा कैप्चर 90° क्लॉकवाइज़ घुमा हुआ था। ऐसे में टेक्स्ट इंसान की आँखों को ठीक लगता है, लेकिन OCR इंजन को गड़बड़ दिखता है। अच्छी खबर? केवल कुछ ही पंक्तियों के Python और Aspose लाइब्रेरीज़ के साथ ओरिएंटेशन ठीक करना, इच्छित क्षेत्र को क्रॉप करना, और फिर टेक्स्ट निकालना बहुत आसान है।

इस ट्यूटोरियल में हम पूरे वर्कफ़्लो को कवर करेंगे: घुमाई हुई TIFF लोड करना, उसकी ओरिएंटेशन सही करना, **OCR के लिए इमेज प्री‑प्रोसेस** करना, और अंत में **इमेज से टेक्स्ट पहचानना**। अंत तक आप जानेंगे **OCR कैसे किया जाए** किसी भी इमेज पर और **इमेज फ़ाइल से टेक्स्ट निकालना** कैसे किया जाए।

## आपको क्या चाहिए

- Python 3.8+ (कोड किसी भी हालिया संस्करण के साथ काम करता है)
- `asposeocrjava` और `asposeimaging` पैकेज `pip` के माध्यम से इंस्टॉल किए हुए
- एक सैंपल इमेज जिसे घुमाने की ज़रूरत है (जैसे `rotated_form.tif`)
- इमेज प्रोसेसिंग में थोड़ी जिज्ञासा

कोई भारी‑वजन वाले फ्रेमवर्क की ज़रूरत नहीं—सिर्फ दो Aspose पैकेज और थोड़ा Python लॉजिक।

---

## चरण 1: Aspose पैकेज इंस्टॉल करें (OCR कैसे किया जाए)

इमेज को **घुमाने** या **इमेज से टेक्स्ट पहचानने** से पहले हमें वही लाइब्रेरीज़ चाहिए जो असली काम करती हैं।

```bash
pip install asposeocrjava asposeimaging
```

> **प्रो टिप:** यदि आप कॉरपोरेट प्रॉक्सी के पीछे हैं, तो कमांड में `--proxy http://proxy:port` जोड़ें। ये पैकेज Aspose .NET/Java कोर के शुद्ध Python रैपर हैं, इसलिए इंस्टॉलेशन आमतौर पर तुरंत हो जाता है।

---

## चरण 2: स्रोत फ़ाइल लोड करें और उसे घुमाएँ – “इमेज को कैसे घुमाएँ” का मुख्य चरण

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **क्यों घुमाएँ?** अधिकांश OCR इंजन मानते हैं कि टेक्स्ट बाएँ‑से‑दाएँ और ऊपर‑से‑नीचे पढ़ा जाता है। यदि बिटमैप साइडवेज़ है, तो इंजन या तो बकवास रिटर्न करेगा या कुछ नहीं। घुमाने से पिक्सेल ग्रिड अपेक्षित रीडिंग ऑर्डर के साथ संरेखित हो जाता है, जिससे सटीकता में उल्लेखनीय सुधार होता है।

> **एज केस:** यदि आपको नहीं पता कि इमेज को 90°, 180° या 270° घुमाना है, तो `source_image.width` बनाम `source_image.height` देख सकते हैं या `exif` ओरिएंटेशन टैग्स का उपयोग कर सकते हैं। Aspose की `rotate_flip` मेथड `ROTATE_180` और `ROTATE_270_CLOCKWISE` को भी सपोर्ट करती है।

> **इमेज प्रीव्यू (वैकल्पिक):**  
> ![इमेज को घुमाने का उदाहरण](/assets/rotate-demo.png "इमेज को घुमाना – घुमाने से पहले और बाद") 

---

## चरण 3: रुचि के क्षेत्र को क्रॉप करें – OCR के लिए इमेज प्री‑प्रोसेस

अक्सर आपको पेज का केवल छोटा हिस्सा चाहिए—जैसे सिग्नेचर फ़ील्ड या नंबरों का ब्लॉक। क्रॉप करने से शोर हटता है और **OCR कैसे किया जाए** की गति बढ़ती है।

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **क्यों क्रॉप करें?** इमेज साइज घटाने से OCR इंजन का सर्च स्पेस सीमित हो जाता है, जिससे फॉल्स पॉज़िटिव कम होते हैं और प्रोसेसिंग टाइम घटता है। यह तब भी मदद करता है जब स्रोत फ़ाइल में वॉटरमार्क या अन्य ग्राफ़िक्स हों जो इंजन को भ्रमित कर सकते हैं।

> **टिप:** यदि आप कई फ़ील्ड्स के साथ काम कर रहे हैं, तो विभिन्न रेक्टेंगल्स के साथ क्रॉप स्टेप को दोहराएँ और प्रत्येक हिस्से पर अलग‑अलग OCR चलाएँ।

---

## चरण 4: OCR इंजन को इनिशियलाइज़ करें – “OCR कैसे किया जाए” का कोर

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **पर्दे के पीछे:** Aspose OCR Tesseract और प्रोप्राइटरी इमेज एनालिसिस का मिश्रण उपयोग करता है। एक बार इंजन को इंस्टैंशिएट करके कई इमेज पर री‑यूज़ करना, हर बार नया ऑब्जेक्ट बनाने से अधिक कुशल है।

---

## चरण 5: क्रॉप की गई इमेज फीड करें और टेक्स्ट पहचानें – इमेज से टेक्स्ट निकालना

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### अपेक्षित आउटपुट

यदि ROI में “Invoice #12345 – Paid” वाक्य है, तो आपको कुछ इस तरह दिखेगा:

```
Invoice #12345 – Paid
```

यदि OCR संघर्ष करता है, तो आपको अतिरिक्त स्पेस या गलत अक्षर मिल सकते हैं (जैसे “Invo1ce #I2345 – Pa1d”)। यही वह जगह है जहाँ **OCR के लिए इमेज प्री‑प्रोसेस** ट्रिक्स—जैसे कंट्रास्ट एडजस्ट करना या बाइनराइज़ेशन लागू करना—काम आते हैं। Aspose अतिरिक्त फ़िल्टर प्रदान करता है जिन्हें आप चरण 5 से पहले चेन कर सकते हैं, लेकिन ऊपर दिया बेसिक फ्लो अधिकांश साफ़ स्कैन के लिए काम करता है।

---

## चरण 6: वैकल्पिक – OCR सेटिंग्स को फाइन‑ट्यून करें (एडवांस्ड “OCR कैसे किया जाए”)

यदि आपको किसी विशेष भाषा के लिए उच्च सटीकता चाहिए या कुछ कैरेक्टर्स को इग्नोर करना है, तो आप इंजन को ट्यून कर सकते हैं:

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **कब उपयोग करें:** जब दस्तावेज़ में बहुत सारे सजावटी सिंबल हों जिनकी आपको ज़रूरत नहीं है। ब्लैकलिस्टिंग फॉल्स डिटेक्शन को कम करती है।

---

## पूर्ण एंड‑टू‑एंड स्क्रिप्ट

सब कुछ एक साथ जोड़ते हुए, यहाँ एक तैयार‑चलाने‑योग्य स्क्रिप्ट है जो **इमेज को कैसे घुमाएँ**, **OCR के लिए इमेज प्री‑प्रोसेस**, और अंत में **इमेज से टेक्स्ट पहचानें** करती है:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

इस स्क्रिप्ट को चलाने पर पहचान किया गया टेक्स्ट कंसोल में प्रिंट होगा और प्रोसेस्ड ROI की विज़ुअल `processed_roi.png` के रूप में सेव होगी। आप उस PNG को खोलकर पुष्टि कर सकते हैं कि घुमाव और क्रॉप अपेक्षित रूप से हुए हैं।

---

## सामान्य प्रश्न और समस्याएँ

| प्रश्न | उत्तर |
|----------|--------|
| **अगर इमेज पहले से ही सही दिशा में है तो?** | रोटेशन स्टेप इडेम्पोटेंट है—सही ओरिएंटेड इमेज को 90° घुमाने से वह बिगड़ जाएगी, इसलिए `source_image.width` बनाम `height` या EXIF ओरिएंटेशन डेटा को जांचें पहले `rotate_flip` कॉल करने से। |
| **मेरे OCR आउटपुट में अतिरिक्त लाइन ब्रेक्स हैं।** | `result.get_text().replace("\n", " ").strip()` से साफ़ करें, या `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)` एनेबल करें। |
| **क्या मैं सीधे PDFs प्रोसेस कर सकता हूँ?** | हाँ—Aspose Imaging PDF पेजेज़ को इमेज (`Image.load("file.pdf")`) के रूप में लोड कर सकता है, उसके बाद वही रोटेशन और OCR स्टेप्स फॉलो करें। |
| **क्या कई फ़ाइलों को बैच‑प्रोसेस किया जा सकता है?** | `ocr_rotated_image` को किसी डायरेक्टरी के ऊपर लूप में रखें, या Python के `concurrent.futures` का उपयोग करके पैरललाइज़ करें। |
| **अंग्रेज़ी के अलावा अन्य भाषाओं को कैसे हैंडल करें?** | `ocr_engine.get_recognition_settings().set_recognition_language("fr")` जैसे सेटिंग से फ्रेंच आदि भाषा सेट करें। |

---

## निष्कर्ष

हमने **इमेज को कैसे घुमाएँ** सही तरीके से, **OCR के लिए इमेज प्री‑प्रोसेस** (क्रॉपिंग) और अंत में **OCR कैसे किया जाए** ताकि **इमेज से टेक्स्ट पहचानें** और **इमेज फ़ाइल से टेक्स्ट निकालें** Aspose की Python लाइब्रेरीज़ का उपयोग करके पूरा किया। पूर्ण स्क्रिप्ट एक प्रैक्टिकल, प्रोडक्शन‑रेडी वर्कफ़्लो दर्शाती है जिसे आप किसी भी ऑटोमेशन पाइपलाइन में डाल सकते हैं।

यदि आप आगे बढ़ना चाहते हैं, तो इन चीज़ों के साथ प्रयोग करें:

- **इमेज एन्हांसमेंट** (कंट्रास्ट, बाइनराइज़ेशन) OCR से पहले
- **कई ROI एक्सट्रैक्शन** फ़ॉर्म्स में कई फ़ील्ड्स के लिए
- **बैच प्रोसेसिंग** स्कैन किए हुए दस्तावेज़ों के पूरे फ़ोल्डर की
- **डाउन्स्ट्रीम सिस्टम्स** के साथ इंटीग्रेशन (जैसे एक्सट्रैक्टेड डेटा को डेटाबेस में फीड करना)

कोड को अपनी ज़रूरतों के अनुसार एडजस्ट करें, और हैप्पी कोडिंग! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}