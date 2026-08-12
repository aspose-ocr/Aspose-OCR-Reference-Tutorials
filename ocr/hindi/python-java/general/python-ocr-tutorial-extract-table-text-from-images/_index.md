---
category: general
date: 2026-01-12
description: Python OCR ट्यूटोरियल जो दिखाता है कि कैसे एक छवि से तालिका का टेक्स्ट
  निकाला जाए। छवि से तालिका पढ़ना सीखें और Aspose OCR के साथ चयनित टेक्स्ट निकालें।
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: hi
og_description: Python OCR ट्यूटोरियल जो आपको सिखाता है कि कैसे एक छवि से तालिका का
  टेक्स्ट निकालें, छवि से तालिका पढ़ें और Aspose OCR का उपयोग करके चयनित टेक्स्ट निकालें।
og_title: 'पायथन OCR ट्यूटोरियल: छवियों से तालिका पाठ निकालें'
tags:
- OCR
- Python
- AsposeOCR
title: 'Python OCR ट्यूटोरियल: छवियों से तालिका का पाठ निकालें'
url: /hi/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR ट्यूटोरियल: छवियों से तालिका टेक्स्ट निकालें

क्या आपको कभी ऐसा **python ocr tutorial** चाहिए था जो वास्तव में दिखाए कि स्कैन किए गए फॉर्म से तालिका कैसे निकाली जाए? आप अकेले नहीं हैं। अधिकांश ट्यूटोरियल सामान्य टेक्स्ट एक्सट्रैक्शन पर ही रुक जाते हैं, जिससे आपको वह साफ़ ग्रिड डेटा अलग करने का अंदाज़ा लगाना पड़ता है जिसकी आपको ज़रूरत है।  

इस गाइड में हम एक वास्तविक‑दुनिया परिदृश्य को देखेंगे: छवि से तालिका पढ़ना, केवल आवश्यक चयनित टेक्स्ट निकालना, और अंत में परिणाम प्रिंट करना। साथ ही हम **how to extract table** डेटा को विश्वसनीय रूप से निकालने के टिप्स भी देंगे, ताकि आपको हर बार व्हील को फिर से बनाने की ज़रूरत न पड़े।

## आप क्या सीखेंगे

- Aspose OCR को Python के लिए कैसे सेट‑अप करें।
- तालिका वाले आयताकार क्षेत्र को कैसे परिभाषित करें।
- **extract table text** और **read table from image** के सटीक कदम।
- कई भाषाओं या अनियमित तालिका लेआउट को संभालने के टिप्स।
- एक पूर्ण, चलाने योग्य स्क्रिप्ट जिसे आप आज ही अपने प्रोजेक्ट में डाल सकते हैं।

**Prerequisites**  
- Python 3.8 या नया।  
- OCR अवधारणाओं की बुनियादी समझ (गहरी विशेषज्ञता आवश्यक नहीं)।  
- एक PNG या JPEG छवि जिसमें स्पष्ट तालिका हो (हम इसे `form_with_table.png` कहेंगे)।  

यदि आपके पास ये हैं, तो चलिए शुरू करते हैं—कोई फालतू बात नहीं, सिर्फ़ कार्यात्मक कोड।

![python ocr ट्यूटोरियल तालिका क्षेत्र का उदाहरण](table_region_example.png){alt="python ocr ट्यूटोरियल तालिका क्षेत्र दिखाते हुए उदाहरण"}

## Step 1: Install and Import Aspose OCR

पहले बात: आपको Aspose OCR लाइब्रेरी चाहिए। पैकेज PyPI पर है, इसलिए एक ही `pip` कमांड से हो जाता है।

```bash
pip install aspose-ocr
```

अब मॉड्यूल और आवश्यक हेल्पर्स को इम्पोर्ट करें।

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*Pro tip:* अपनी डिपेंडेंसीज़ को `requirements.txt` फ़ाइल में रखें। इससे पर्यावरण को दोहराना बहुत आसान हो जाता है।

## Step 2: Initialise the OCR Engine (Python OCR Tutorial Core)

इंजन बनाना किसी भी **python ocr tutorial** का दिल है। यहाँ हम डिफ़ॉल्ट भाषा को English सेट करते हैं—बाद में इसे बदलने में स्वतंत्र महसूस करें।

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

भाषा सेट क्यों करें? जब इंजन को पता हो कि कौन से अक्षर अपेक्षित हैं, तो OCR की सटीकता में बहुत बड़ा उछाल आता है। यदि आप बहुभाषी फॉर्म्स के साथ काम कर रहे हैं, तो आप भाषा की सूची सेट कर सकते हैं या प्रत्येक क्षेत्र के लिए ओवरराइड कर सकते हैं (बाद में देखें)।

## Step 3: Load Your Image

Aspose OCR अधिकांश सामान्य इमेज फ़ॉर्मेट्स को सपोर्ट करता है। बस फ़ाइल पाथ पर पॉइंट करें, और आपके पास प्रोसेसिंग के लिए एक `Image` ऑब्जेक्ट तैयार होगा।

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*Edge case:* बड़ी छवियां (5 MB से अधिक) प्रोसेसिंग को धीमा कर सकती हैं। यदि प्रदर्शन समस्या बनती है तो रिसाइज़ या कम्प्रेस करने पर विचार करें।

## Step 4: Define the Table Region (Read Table from Image)

अब मज़ेदार हिस्सा: इंजन को बताना कि तालिका कहाँ है। आप `OcrRegion` को `Rectangle` (x, y, width, height) के साथ प्रदान करते हैं। कॉर्डिनेट्स पिक्सेल‑आधारित होते हैं, इसलिए आपको थोड़ा प्रयोग करना पड़ सकता है।

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

क्षेत्र क्यों उपयोग करें? OCR को केवल तालिका क्षेत्र तक सीमित करके हम **extract selected text** तेज़ी से प्राप्त करते हैं और आसपास के लेबल या ग्राफ़िक्स से शोर को हटाते हैं। यह सटीकता भी बढ़ाता है क्योंकि इंजन एक समान लेआउट पर फोकस कर सकता है।

## Step 5: Run OCR on the Defined Region

क्षेत्र सेट करने के बाद, हम `process_region` को कॉल करते हैं। यह मेथड एक `OcrResult` ऑब्जेक्ट लौटाता है जिसमें कच्चा टेक्स्ट, कॉन्फिडेंस स्कोर, और यदि आवश्यक हो तो बाउंडिंग बॉक्स भी होते हैं।

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

यदि आपको कई तालिकाएँ निकालनी हैं, तो बस विभिन्न आयतों के साथ Steps 4‑5 दोहराएँ।

## Step 6: Output the Extracted Table Text

अंत में, तालिका के टेक्स्टुअल प्रतिनिधित्व को प्रिंट या स्टोर करें। Aspose OCR साधारण टेक्स्ट के साथ लाइन ब्रेक देता है जो आमतौर पर पंक्तियों के साथ मेल खाता है, जिससे पोस्ट‑प्रोसेसिंग सीधा हो जाता है।

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**Expected output** (उदाहरण):

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

अब आप इस स्ट्रिंग को `csv` पार्सर्स, pandas DataFrames, या किसी भी डाउनस्ट्रीम एनालिटिक्स पाइपलाइन में फीड कर सकते हैं।

## Full Working Example

सब कुछ एक साथ मिलाकर, यहाँ पूरा स्क्रिप्ट है जिसे आप तुरंत चला सकते हैं। `YOUR_DIRECTORY/form_with_table.png` को अपनी छवि के वास्तविक पाथ से बदलें।

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

स्क्रिप्ट को `python extract_table.py` के साथ चलाएँ। यदि सब कुछ सही है, तो आपको कंसोल में तालिका प्रिंट होती दिखेगी।

## Common Questions & Edge‑Case Handling

**अगर तालिका पूरी तरह आयताकार नहीं है तो क्या करें?**  
आप तालिका को कई ओवरलैपिंग क्षेत्रों में बाँट सकते हैं या एक बड़ा आयत उपयोग करके पूरे क्षेत्र को कवर कर सकते हैं और फिर टेक्स्ट को पोस्ट‑प्रोसेस कर सकते हैं (जैसे लाइन ब्रेक पर विभाजित करना)।

**क्या मैं केवल विशिष्ट कॉलम निकाल सकता हूँ?**  
पूरा तालिका टेक्स्ट मिलने के बाद, Python के `csv` या `pandas` का उपयोग करके आप उन कॉलम को स्लाइस कर सकते हैं जिनकी आपको ज़रूरत है। OCR चरण स्वयं आयत के भीतर सब कुछ लौटाता है।

**गैर‑English तालिकाओं के साथ कैसे काम करें?**  
`ocr_engine.language` (या `region.language`) को उपयुक्त enum पर सेट करें, जैसे `ocr.Language.FRENCH` या कई भाषाओं को `ocr.Language.ENGLISH | ocr.Language.SPANISH` के साथ संयोजित करें।

**क्या प्रत्येक सेल के लिए बाउंडिंग बॉक्स प्राप्त करना संभव है?**  
Aspose OCR `region_result.words` लौटाता है जहाँ प्रत्येक शब्द में बाउंडिंग बॉक्स शामिल होता है। आपको उन बॉक्सों को ग्रिड में मैप करना होगा—उन्नत लेआउट विश्लेषण के लिए उपयोगी।

## Tips for Better Accuracy

- **Clean the image**: OCR को फ़ीड करने से पहले बाइनराइज़ या कंट्रास्ट बढ़ाएँ। Pillow जैसी लाइब्रेरी मदद कर सकती हैं।  
- **Avoid compression artifacts**: संभव हो तो स्कैन को PNG के रूप में सेव करें।  
- **Mind DPI**: 300 dpi एक आदर्श मान है; कम DPI से कैरेक्टर मिस हो सकते हैं।  
- **Test different rectangle sizes**: थोड़ा बड़ा आयत अक्सर उन स्ट्रे आय कैरेक्टर्स को भी पकड़ लेता है जो तालिका का हिस्सा होते हैं।

## Next Steps

अब जब आप Aspose OCR के साथ **how to extract table** डेटा में निपुण हो गए हैं, तो आप आगे कर सकते हैं:

- निकाले गए टेक्स्ट को Python के `csv` मॉड्यूल से CSV फ़ाइल में बदलना।  
- डेटा को **pandas** DataFrame में फीड करके विश्लेषण करना।  
- हाथ से लिखे फॉर्म पढ़ने के लिए OCR का उपयोग (इसके लिए अलग इंजन या अतिरिक्त ट्रेनिंग की ज़रूरत होगी)।  
- सरल `for` लूप का उपयोग करके दर्जनों स्कैन किए गए फॉर्म की बैच प्रोसेसिंग को ऑटोमेट करना।  

इनमें से प्रत्येक विस्तार इस **python ocr tutorial** में कवर किए गए मूल अवधारणाओं पर आधारित है, इसलिए आप स्केल अप करने के लिए अच्छी तरह तैयार हैं।

---

*हैप्पी कोडिंग! यदि आपको कोई दिक्कत आती है, तो नीचे कमेंट छोड़ें—मैं आपको एक्सट्रैक्शन को फाइन‑ट्यून करने में मदद करने के लिए तैयार हूँ।*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}