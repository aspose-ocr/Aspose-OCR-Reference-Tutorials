---
category: general
date: 2026-03-28
description: Aspose OCR का उपयोग करके Python में TIFF फ़ाइलों से टेक्स्ट निकालें।
  जानिए कैसे TIFF को तेज़ी और भरोसेमंद तरीके से टेक्स्ट में बदलें।
draft: false
keywords:
- extract text from tiff
- convert tiff to text
language: hi
og_description: Aspose OCR का उपयोग करके Python में TIFF फ़ाइलों से टेक्स्ट निकालें।
  यह गाइड दिखाता है कि कैसे चरण‑दर‑चरण TIFF को टेक्स्ट में परिवर्तित किया जाए।
og_title: TIFF से टेक्स्ट निकालें – पूर्ण पायथन गाइड
tags:
- OCR
- Python
- Aspose
title: TIFF से टेक्स्ट निकालें – पूर्ण पायथन गाइड
url: /hi/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF से टेक्स्ट निकालें – पूर्ण Python गाइड

क्या आपको अपने Python प्रोजेक्ट में **TIFF से टेक्स्ट निकालना** है? यह गाइड आपको Aspose OCR लाइब्रेरी का उपयोग करके **TIFF को टेक्स्ट में बदलना** दिखाता है, और यह ऐसा तरीके से करता है जिसे एक शुरुआती भी आसानी से समझ सके।  

यदि आपने कभी एक मल्टी‑पेज TIFF को देखा है और सोचा है कि बिना मैन्युअली टाइप किए शब्द कैसे निकालें, तो आप सही जगह पर हैं। हम पूरी प्रक्रिया को समझाएंगे—पैकेज को इंस्टॉल करने से लेकर एन्क्रिप्टेड फ़ाइलों जैसे एज केस को हैंडल करने तक—ताकि आप महत्वपूर्ण फीचर्स बनाने पर ध्यान दे सकें।

## आप क्या सीखेंगे

* Aspose OCR को Python के लिए सेट अप करने का तरीका।
* मल्टी‑पेज TIFF के प्रत्येक पेज को पढ़ने के लिए आवश्यक सटीक कोड।
* गुम फ़ॉन्ट्स या करप्ट पेजेज जैसी सामान्य समस्याओं को संभालने के तरीके।
* जब आप बड़े पैमाने पर **TIFF से टेक्स्ट निकालते** हैं, तो सटीकता और प्रदर्शन सुधारने के टिप्स।

### पूर्वापेक्षाएँ

* Python 3.8 या नया (लाइब्रेरी 3.7+ को सपोर्ट करती है)।
* एक वैध Aspose OCR लाइसेंस—या आप फ्री ट्रायल से शुरू कर सकते हैं (कोड इवैल्यूएशन मोड में काम करता है, केवल आउटपुट पर वॉटरमार्क के साथ)।
* Python के वर्चुअल एनवायरनमेंट्स की बुनियादी जानकारी (वैकल्पिक लेकिन अनुशंसित)।

---

## चरण 1 – Aspose OCR पैकेज इंस्टॉल करें

सबसे पहले: आपको `aspose-ocr` पैकेज चाहिए। यह PyPI पर होस्टेड है, इसलिए एक साधारण `pip` इंस्टॉल पर्याप्त है।

```bash
pip install aspose-ocr
```

> **Pro tip:** एक वर्चुअल एनवायरनमेंट (`python -m venv venv`) का उपयोग करें ताकि डिपेंडेंसीज़ अलग रहें। यह अन्य प्रोजेक्ट्स के साथ संस्करण टकराव को रोकता है।

> **Why this matters:** पैकेज इंस्टॉल करने से नेेटिव OCR इंजन बाइनरीज़ शामिल हो जाती हैं जो वास्तविक कार्य करती हैं। इनके बिना, `recognize_from_tiff` मेथड मौजूद नहीं रहेगा, और आपको `ImportError` मिलेगा।

## चरण 2 – लाइब्रेरी इम्पोर्ट करें और OCR इंजन बनाएं

अब जब लाइब्रेरी आपके मशीन पर है, इसे इम्पोर्ट करें और एक `OcrEngine` बनाएं। यह ऑब्जेक्ट वह कार्यकर्ता है जो इमेज डेटा प्रोसेस करेगा।

```python
# Step 2: Import the Aspose OCR library and create an engine instance
import aspose.ocr as aocr

# Initialize the OCR engine – you can optionally pass a license file here
ocr_engine = aocr.OcrEngine()
```

`OcrEngine` क्लास सभी OCR सेटिंग्स को समेटे हुए है, जैसे भाषा, रिज़ॉल्यूशन, और प्रीप्रोसेसिंग विकल्प। हम बाद में सटीकता बढ़ाने के लिए उनमें से कुछ को समायोजित करेंगे।

## चरण 3 – अपने मल्टी‑पेज TIFF फ़ाइल की ओर संकेत करें

आपको उस TIFF का पाथ चाहिए जिसे आप पढ़ना चाहते हैं। लाइब्रेरी एब्सोल्यूट या रिलेटिव पाथ दोनों को सपोर्ट करती है, लेकिन एब्सोल्यूट पाथ स्क्रिप्ट के अलग वर्किंग डायरेक्टरी से चलने पर आश्चर्य से बचाते हैं।

```python
# Step 3: Define the path to the TIFF file
tiff_file_path = "YOUR_DIRECTORY/input.tif"
```

> **Common mistake:** Windows पर बैकस्लैश को एस्केप करना भूल जाना (`C:\\Images\\file.tif`)। रॉ स्ट्रिंग्स (`r"C:\Images\file.tif"`) या फॉरवर्ड स्लैश का उपयोग करने से यह समस्या नहीं आती।

## चरण 4 – सभी पेजों से टेक्स्ट पहचानें

यह ट्यूटोरियल का मुख्य भाग है: `recognize_from_tiff` को कॉल करना। यह मेथड `OcrResult` ऑब्जेक्ट्स की एक लिस्ट रिटर्न करता है—प्रत्येक पेज के लिए एक—जिसे आप व्यक्तिगत रूप से इटररेट कर सकते हैं।

```python
# Step 4: Extract text from every page of the TIFF
ocr_pages = ocr_engine.recognize_from_tiff(tiff_file_path)

# Verify we got results
if not ocr_pages:
    raise RuntimeError("No pages were recognized. Check the file path and format.")
```

**Why this works:** Aspose OCR आंतरिक रूप से TIFF को उसके फ्रेम्स में विभाजित करता है, प्रत्येक पर OCR इंजन चलाता है, और परिणामों को बंडल करता है। यह Pillow या ImageMagick से मैन्युअली पेजेज को अलग करने की तुलना में बहुत अधिक विश्वसनीय है।

## चरण 5 – परिणामों पर इटररेट करें और टेक्स्ट आउटपुट करें

अंत में, `OcrResult` लिस्ट पर लूप चलाएँ और निकाले गए टेक्स्ट को प्रिंट (या सेव) करें। यदि आपके वर्कफ़्लो के अनुसार उपयुक्त हो तो आप प्रत्येक पेज को अलग `.txt` फ़ाइल में भी लिख सकते हैं।

```python
# Step 5: Print or save the extracted text
for page_index, page_result in enumerate(ocr_pages):
    print(f"--- TIFF Page {page_index + 1} ---")
    print(page_result.text)
    # Optional: write each page to a separate file
    with open(f"page_{page_index + 1}.txt", "w", encoding="utf-8") as f:
        f.write(page_result.text)
```

**Expected output** (संक्षिप्त रूप में):

```
--- TIFF Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- TIFF Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
```

> **Edge case handling:** यदि किसी पेज में कोई पहचान योग्य टेक्स्ट नहीं है, तो `page_result.text` एक खाली स्ट्रिंग होगी। आप बाद में मैन्युअल रिव्यू के लिए उन पेजेज को लॉग करना चाह सकते हैं।

## बोनस – बेहतर सटीकता के लिए OCR सेटिंग्स को ट्यून करना

कभी‑कभी डिफ़ॉल्ट कॉन्फ़िगरेशन पर्याप्त नहीं होती, विशेषकर लो‑रेज़ॉल्यूशन स्कैन या असामान्य फ़ॉन्ट्स के साथ। नीचे कुछ सेटिंग्स दी गई हैं जिन्हें आप समायोजित कर सकते हैं:

```python
# Set language (default is English)
ocr_engine.language = aocr.Language.English

# Increase image resolution before OCR (helps with blurry scans)
ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
    sharpen=True,
    contrast=1.2
)

# Enable deskew to straighten rotated pages
ocr_engine.deskew = True
```

ये विकल्प वैकल्पिक हैं, लेकिन अक्सर गड़बड़ आउटपुट और साफ़, सर्चेबल ट्रांसक्रिप्ट के बीच अंतर बनाते हैं।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| सभी पेजों के लिए खाली आउटपुट | गलत फ़ाइल पाथ या असमर्थित TIFF कंप्रेशन | पाथ की जाँच करें, सुनिश्चित करें कि TIFF समर्थित कंप्रेशन (जैसे LZW, PackBits) का उपयोग करता है। |
| गड़बड़ अक्षर (जैसे �) | गलत भाषा सेटिंग या फ़ॉन्ट फ़ाइलें गायब | `ocr_engine.language` को सही लोकैल सेट करें; होस्ट OS पर आवश्यक फ़ॉन्ट्स इंस्टॉल करें। |
| बड़े TIFF पर धीमी प्रोसेसिंग | डिफ़ॉल्ट सिंगल‑थ्रेडेड मोड | यदि लाइब्रेरी संस्करण समर्थन करता है तो `ocr_engine.recognize_from_tiff(..., parallel=True)` का उपयोग करें। |
| लाइसेंस चेतावनी | लाइसेंस फ़ाइल के बिना ट्रायल का उपयोग | `aocr.License().set_license("Aspose.OCR.lic")` के माध्यम से लाइसेंस की प्रदान करें। |

## पूर्ण स्क्रिप्ट – चलाने के लिए तैयार

नीचे पूर्ण, स्व-निहित स्क्रिप्ट है जो ऊपर चर्चा किए गए सभी चरणों और वैकल्पिक ट्यूनिंग को सम्मिलित करती है। इसे `extract_tiff_text.py` नाम की फ़ाइल में कॉपी‑पेस्ट करें और `python extract_tiff_text.py` चलाएँ।

```python
#!/usr/bin/env python3
"""
extract_tiff_text.py

A complete example that extracts text from a multi‑page TIFF using Aspose OCR.
It demonstrates how to:
- Install and import the library
- Initialize the OCR engine
- Configure optional preprocessing
- Iterate over each page and save the results

Author: Your Name
Date: 2026‑03‑28
"""

import aspose.ocr as aocr
import os
import sys

def main(tiff_path: str, output_dir: str = "output"):
    # Ensure output directory exists
    os.makedirs(output_dir, exist_ok=True)

    # Initialize the OCR engine
    ocr_engine = aocr.OcrEngine()

    # Optional: fine‑tune OCR settings for better accuracy
    ocr_engine.language = aocr.Language.English
    ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
        sharpen=True,
        contrast=1.2
    )
    ocr_engine.deskew = True

    # Perform OCR on the TIFF
    try:
        ocr_pages = ocr_engine.recognize_from_tiff(tiff_path)
    except Exception as e:
        sys.exit(f"Failed to process {tiff_path}: {e}")

    if not ocr_pages:
        sys.exit("No pages were recognized. Check the file path and format.")

    # Iterate over results
    for idx, result in enumerate(ocr_pages, start=1):
        page_text = result.text or "[No recognizable text]"
        print(f"--- TIFF Page {idx} ---")
        print(page_text[:200] + ("..." if len(page_text) > 200 else ""))  # preview

        # Save each page's text
        out_file = os.path.join(output_dir, f"page_{idx}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

    print(f"\nAll pages processed. Text files saved in '{output_dir}'.")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        sys.exit("Usage: python extract_tiff_text.py <path_to_tiff>")
    tiff_file = sys.argv[1]
    main(tiff_file)
```

**स्क्रिप्ट चलाना**

```bash
python extract_tiff_text.py /path/to/your/input.tif
```

आप प्रत्येक पेज का कंसोल प्रीव्यू और `output` नामक फ़ोल्डर देखेंगे जिसमें `page_1.txt`, `page_2.txt`, आदि फ़ाइलें होंगी।

## निष्कर्ष

हमने अभी वह सब कुछ कवर किया है जो आपको Python और Aspose OCR का उपयोग करके **TIFF फ़ाइलों से टेक्स्ट निकालने** के लिए चाहिए। पैकेज इंस्टॉल करने से लेकर मल्टी‑पेज दस्तावेज़ों को हैंडल करने, सटीकता के लिए सेटिंग्स ट्यून करने, और परिणाम सेव करने तक, पूरा वर्कफ़्लो अब आपके हाथ में है।  

यदि आप प्रोडक्शन पाइपलाइन में **TIFF को टेक्स्ट में बदलने** की सोच रहे हैं, तो फ़ाइलों को बैच करने, OCR कॉल्स को पैरललाइज़ करने, और आउटपुट को Elasticsearch जैसे सर्चेबल इंडेक्स में स्टोर करने पर विचार करें। साहसी लोगों के लिए, अन्य भाषाओं (`aocr.Language.Spanish`) के साथ प्रयोग करें या कच्चे OCR परिणामों को स्पेल‑चेकिंग लाइब्रेरी में फीड करके OCR शोर को साफ़ करें।  

स्केलिंग, लाइसेंसिंग, या क्लाउड स्टोरेज के साथ इंटीग्रेशन के बारे में सवाल हैं? नीचे कमेंट करें, और कोडिंग का आनंद लें!  

![TIFF फ़ाइल से निकाले गए टेक्स्ट तक OCR फ्लो दिखाता डायग्राम](https://example.com/placeholder-image.png "Python का उपयोग करके TIFF से टेक्स्ट निकालें")

*Image alt text: TIFF फ़ाइल से निकाले गए टेक्स्ट तक OCR फ्लो दिखाता डायग्राम*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}