---
category: general
date: 2026-06-22
description: Python का उपयोग करके कुछ ही पंक्तियों में छवि पर OCR करें। जानें कि OCR
  के लिए छवि कैसे लोड करें, PNG से टेक्स्ट कैसे पहचानें, और OCR इंजन को प्रभावी ढंग
  से कैसे उपयोग करें।
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: hi
og_description: Python के साथ छवि पर तेज़ी से OCR करें। यह ट्यूटोरियल दिखाता है कि
  OCR के लिए छवि कैसे लोड करें, PNG से टेक्स्ट कैसे पहचानें, और भरोसे के साथ OCR इंजन
  का उपयोग कैसे करें।
og_title: Python में इमेज पर OCR करें – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python में इमेज पर OCR करें – पूर्ण गाइड
url: /hi/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में इमेज पर OCR करें – पूर्ण गाइड

क्या आपको कभी **इमेज पर OCR करना** पड़ा लेकिन कोड की पहली पंक्ति पर अटक गए? आप अकेले नहीं हैं। इस walkthrough में हम आपको बिल्कुल दिखाएंगे कि कैसे **OCR के लिए इमेज लोड करें**, एक हल्का **OCR engine** सेट अप करें, और अंत में **PNG से टेक्स्ट पहचानें** कुछ ही कमांड्स से।

हम लाइब्रेरी को इंस्टॉल करने से लेकर व्हाइटलिस्ट को ट्यून करने तक सब कुछ कवर करेंगे ताकि केवल अंक और बड़े अक्षर ही स्कैन में बचें। अंत तक आपके पास एक तैयार‑से‑चलाने वाला स्क्रिप्ट होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं—कोई रहस्य नहीं, कोई अतिरिक्त फ़्लफ़ नहीं।

## आप क्या सीखेंगे

- Python में प्रोग्रामेटिक रूप से **OCR engine का उपयोग** कैसे करें।  
- स्थानीय फ़ोल्डर से **OCR के लिए इमेज लोड** करने के सटीक चरण।  
- कस्टम कैरेक्टर सेट तक पहचान को सीमित करने का कारण और तरीका।  
- **PNG से टेक्स्ट पहचानें** और परिणाम को सुरक्षित रूप से हैंडल करें।  

**Prerequisites:** Python 3.7+ इंस्टॉल हो, एक टर्मिनल जिससे आप सहज हों, और एक इमेज (जैसे `serial-number.png`) जिसे आप पढ़ना चाहते हैं। पहले से OCR का कोई अनुभव आवश्यक नहीं।

---

## Perform OCR on Image – Initialize the OCR Engine

पहला काम OCR engine का एक इंस्टेंस बनाना है। इंजन को उस दिमाग़ की तरह सोचें जो पिक्सेल्स का विश्लेषण करेगा और उन्हें अक्षरों में बदल देगा।

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Why this matters:* बिना इंजन के इमेज प्रोसेस करने के लिए कुछ नहीं है। `OcrEngine` क्लास सभी भारी‑काम—pre‑processing, segmentation, और character classification—को एक ही ऑब्जेक्ट में बंडल कर देती है जिसे आप पुनः उपयोग कर सकते हैं।

---

## Load Image for OCR – Provide the PNG File

अब जब इंजन मौजूद है, आपको वह तस्वीर फीड करनी होगी जिसे आप पढ़ना चाहते हैं। लाइब्रेरी एक `ImageStream` ऑब्जेक्ट की अपेक्षा करती है, जिसे आप सीधे फ़ाइल पाथ से बना सकते हैं।

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Pro tip:* इमेज को हाई‑कॉन्ट्रास्ट फॉर्मेट (सफ़ेद बैकग्राउंड पर काली टेक्स्ट) में रखें और कम्प्रेशन आर्टिफैक्ट्स से बचें; ये OCR एल्गोरिद्म को गड़बड़ कर सकते हैं।

---

## Restrict Characters – Whitelist Digits and Uppercase Letters

अक्सर आपको केवल कुछ ही कैरेक्टर्स की ज़रूरत होती है—जैसे, एक सीरियल नंबर जिसमें केवल A‑Z और 0‑9 हों। व्हाइटलिस्ट सेट करके आप इंजन को बाकी सबको इग्नोर करने को कहते हैं, जिससे सटीकता में काफी सुधार होता है।

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*What’s happening under the hood?* इंजन एक फ़िल्टर बनाता है जो व्हाइटलिस्ट में न मौजूद किसी भी glyph को अंतिम क्लासिफिकेशन स्टेज से पहले डिस्कार्ड कर देता है। यह तब बहुत काम आता है जब इमेज में शोर या अनावश्यक सजावटी टेक्स्ट हो।

---

## Recognize Text from PNG – Run the OCR Process

इंजन तैयार और इमेज लोड हो जाने के बाद, आप अंततः **इमेज पर OCR कर सकते** हैं। `recognize()` कॉल पूरी पाइपलाइन चलाता है और एक result ऑब्जेक्ट रिटर्न करता है।

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

यदि आप परफ़ॉर्मेंस के बारे में जिज्ञासु हैं, तो यह मेथड आमतौर पर आधुनिक लैपटॉप पर 300 × 200 px PNG के लिए कुछ सौ मिलीसेकंड में समाप्त हो जाता है।

---

## Output and Verify – Get the Recognized Text

अंतिम कदम result ऑब्जेक्ट से प्लेन टेक्स्ट निकालना है। व्हाइटलिस्ट से मेल न खाने वाला कोई भी कैरेक्टर स्वचालित रूप से हटाया जाता है, इसलिए आपको एक साफ़ स्ट्रिंग मिलती है जो आगे की प्रोसेसिंग के लिए तैयार होती है।

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Typical output:* `AB12C3D4E5` (मान लेते हैं कि इमेज में वही सीरियल नंबर था)।  

यदि आउटपुट खाली या गड़बड़ है, तो इमेज क्वालिटी और व्हाइटलिस्ट को दोबारा चेक करें; एक आम गलती यह है कि आवश्यक कैरेक्टर्स को अनजाने में छोड़ दिया गया हो।

---

## Edge Cases & Common Gotchas

| Situation | What to Check | Suggested Fix |
|-----------|---------------|---------------|
| **File not found** | Path typo or missing file | Use `os.path.abspath` to verify the full path before calling `set_image`. |
| **Low contrast image** | Text blends with background | Apply a simple threshold (`Pillow` or `OpenCV`) before feeding the image to the engine. |
| **Unexpected characters** | Whitelist too restrictive | Add the missing characters to the whitelist string. |
| **Large images** | Slow recognition | Resize the image to a maximum of 1024 px width; OCR quality usually stays high. |

---

## Full Script – Ready to Run

नीचे पूरा, स्व-समाहित स्क्रिप्ट है जो सभी हिस्सों को जोड़ता है। इसे `ocr_demo.py` के रूप में सेव करें, `YOUR_DIRECTORY` को वास्तविक फ़ोल्डर से बदलें, और `python ocr_demo.py` चलाएँ।

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Expected console output* (when the PNG contains `SN12345`):

```
Recognized text: SN12345
```

---

## निष्कर्ष

अब आप बिल्कुल जानते हैं कि Python में **इमेज पर OCR कैसे करें**, **OCR के लिए इमेज लोड** करने से लेकर **PNG से टेक्स्ट पहचानें** तक, और अंत में एक कस्टमाइज़ेबल **OCR engine** का उपयोग करके साफ़ परिणाम निकालें। यह तरीका सीधा, विस्तार योग्य, और अधिकांश सीरियल‑नंबर‑स्टाइल स्कैन के लिए बॉक्स‑से‑बाहर काम करता है।

अगला क्या? व्हाइटलिस्ट को लोअरकेस लेटर्स के लिए बदलें, विभिन्न इमेज फॉर्मेट्स (JPEG, BMP) के साथ प्रयोग करें, या स्क्रिप्ट को बैच‑प्रोसेसिंग पाइपलाइन में इंटीग्रेट करें। वही पैटर्न—engine → image → settings → recognize → output—लगभग हर OCR टास्क में लागू होता है।

कोई सवाल या अजीब इमेज जो सहयोग नहीं कर रही? नीचे कमेंट करें, और Happy Coding!

![इमेज पर OCR करने के चरणों को दर्शाता डायग्राम Python के साथ OCR इंजन का उपयोग करके](https://example.com/ocr-flow.png "इमेज पर OCR करने के चरणों को दिखाता डायग्राम Python OCR इंजन के साथ")

## आगे आप क्या सीख सकते हैं?

यहाँ कुछ ट्यूटोरियल्स हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं और संबंधित विषयों को गहराई से कवर करते हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}