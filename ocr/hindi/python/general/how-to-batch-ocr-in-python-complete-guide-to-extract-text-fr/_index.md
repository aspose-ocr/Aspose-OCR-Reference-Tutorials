---
category: general
date: 2026-06-28
description: Python में बैच OCR कैसे करें—छवियों से टेक्स्ट निकालें और स्कैन किए गए
  पृष्ठों को बैच OCR प्रोसेसिंग का उपयोग करके टेक्स्ट में बदलें।
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: hi
og_description: Python में बैच OCR कैसे करें, छवियों से टेक्स्ट निकालें, और स्कैन
  किए गए पृष्ठों को कुशल बैच OCR प्रोसेसिंग के साथ टेक्स्ट में बदलना सीखें।
og_title: Python में बैच OCR कैसे करें – चरण-दर-चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python में बैच OCR कैसे करें – छवियों से टेक्स्ट निकालने के लिए पूर्ण गाइड
url: /hi/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में बैच OCR कैसे करें – छवियों से टेक्स्ट निकालने के लिए पूर्ण गाइड

यदि आप सोच रहे हैं **how to batch OCR in Python**, तो आप सही जगह पर हैं। यह ट्यूटोरियल आपको **extract text from images** और **convert scanned pages to text** करने का एक तेज़ तरीका दिखाता है, एक ही OCR इंजन इंस्टेंस का उपयोग करके। अब एक‑एक फ़ाइल को कॉपी‑पेस्ट करने की ज़रूरत नहीं—कोड को ही भारी काम करने दें।

हम आपको वह सब दिखाएंगे जो आपको चाहिए: लाइब्रेरी इंस्टॉल करना, स्कैन की पूरी फ़ोल्डर लोड करना, बैच OCR प्रोसेसिंग चलाना, और परिणामों को सहजता से संभालना। अंत तक आपके पास एक पुन: उपयोग योग्य स्क्रिप्ट होगी जो PNGs या JPEGs की स्टैक को सेकंडों में सर्चेबल टेक्स्ट फ़ाइलों में बदल देती है।

## आपको क्या चाहिए

* Python 3.9+ स्थापित हो (कोड 3.8 पर भी काम करता है, लेकिन 3.9+ आपको नवीनतम टाइपिंग फीचर देता है)।
* एक आधुनिक OCR लाइब्रेरी—यहाँ हम **Aspose.OCR for Python via .NET** का उपयोग करते हैं, जो मूल स्निपेट में दिखाए गए `OcrEngine` क्लास को एक्सपोज़ करता है।  
  ```bash
  pip install aspose-ocr
  ```
* स्कैन किए हुए पेजों की एक फ़ोल्डर (`page1.png`, `page2.png`, …)। जो भी Pillow खोल सकता है, वह काम करेगा, इसलिए PDFs, TIFFs, या BMPs भी ठीक हैं।
* थोड़ी सी जिज्ञासा—यदि आपने पहले कभी image‑to‑text ऑटोमेट नहीं किया है, तो आप देखेंगे कि बैच OCR क्यों एक गेम‑चेंजर है।

> **Pro tip:** यदि आप एक शुद्ध‑Python लाइब्रेरी पसंद करते हैं, तो `OcrEngine` को `pytesseract.image_to_string` से बदल दें। आसपास की लॉजिक समान रहती है।

## Python में बैच OCR कैसे करें – चरण‑दर‑चरण गाइड

नीचे पूर्ण, चलाने योग्य स्क्रिप्ट है। हर लाइन पर टिप्पणी की गई है ताकि आप देख सकें *क्यों* प्रत्येक भाग महत्वपूर्ण है, न कि केवल *क्या* करता है।

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### अपेक्षित आउटपुट

तीन PNG स्कैन वाली फ़ोल्डर पर स्क्रिप्ट चलाने से कुछ इस तरह का आउटपुट मिलता है:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

प्रिव्यू प्रत्येक पेज के पहले 200 अक्षर दिखाता है, और पूरा टेक्स्ट `ocr_output` डायरेक्टरी में रहता है।

## एक ही इंजन का उपयोग करके छवियों से टेक्स्ट निकालना

हम **एक** `OcrEngine` बनाते हैं और उसे पुन: उपयोग क्यों करते हैं? इंजन को इंस्टैंसिएट करना महंगा हो सकता है क्योंकि यह भाषा पैक्स और नेटिव DLLs लोड करता है। बैच में एक ही इंस्टेंस साझा करके, आप:

* **Save memory** – केवल एक सेट रिसोर्स RAM में रहता है।
* **Boost speed** – इंजन गर्म रहता है, बार‑बार इनिशियलाइज़ेशन से बचता है।
* **Maintain consistency** – समान रिकॉग्निशन सेटिंग्स हर पेज पर लागू होती हैं, जो तब आवश्यक है जब आप **extract text from images** करना चाहते हैं जिनका लेआउट समान हो।

यदि आपको रिकॉग्निशन को ट्यून करना है (जैसे, स्पेल‑चेक सक्षम करना या भाषा बदलना), तो इसे `recognize_batch` कॉल करने से *पहले* करें। सभी बाद के पेज स्वचालित रूप से उन सेटिंग्स को विरासत में ले लेंगे।

## स्कैन किए हुए पेजों को टेक्स्ट में प्रभावी रूप से बदलना

समस्या का मूल—**convert scanned pages to text**—`engine.recognize_batch(images)` द्वारा हल किया जाता है। अंदर से लाइब्रेरी प्रत्येक इमेज को बैकग्राउंड थ्रेड पूल में प्रोसेस करती है, इसलिए मल्टी‑कोर मशीनों पर लगभग रैखिक स्केलिंग मिलती है। ध्यान रखने योग्य कुछ बातें:

* **Image quality matters** – 300 dpi या उससे अधिक सबसे अच्छे परिणाम देते हैं। यदि आपके स्कैन कम‑रिज़ॉल्यूशन हैं, तो उन्हें इंजन को देने से पहले Pillow से अप‑सैंपल करने पर विचार करें।
* **Color vs. grayscale** – OCR इंजन आमतौर पर 8‑bit ग्रेस्केल पर तेज़ काम करते हैं। आप एक प्री‑प्रोसेसिंग स्टेप जोड़ सकते हैं:
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Language support** – Aspose.OCR 40 से अधिक भाषाओं का समर्थन करता है। यदि आप अंग्रेज़ी के अलावा कोई भाषा उपयोग कर रहे हैं, तो बैच कॉल से पहले `engine.language = "eng"` या `"fra"` सेट करें।

## बैच OCR प्रोसेसिंग के सर्वोत्तम अभ्यास

हालाँकि ऊपर का कोड पहले से ही संक्षिप्त है, प्रोडक्शन‑ग्रेड बैच OCR अक्सर कुछ अतिरिक्त सुरक्षा उपायों की आवश्यकता रखता है:

| चिंता | सिफ़ारिश किया गया तरीका |
|---------|----------------------|
| **बड़े बैच (> 500 फ़ाइलें)** | मेमोरी उपयोग को कम रखने के लिए 100–200 इमेज के चंक्स में विभाजित करें। |
| **क्षतिग्रस्त या असमर्थित फ़ाइलें** | `load_images` हेल्पर पहले से ही एक्सेप्शन पकड़ लेता है और एक चेतावनी लॉग करता है; आप बुरी फ़ाइलों को स्किप या मूव करने के लिए एक फॉलबैक भी लिख सकते हैं। |
| **प्रोग्रेस मॉनिटरिंग** | यदि लाइब्रेरी प्रति‑इमेज कॉलबैक प्रदान करती है, तो `recognize_batch` को एक लूप में रैप करें जो प्रत्येक इमेज के बाद यील्ड करे। |
| **पोस्ट‑प्रोसेसिंग** | परिणामी स्ट्रिंग्स पर स्पेल‑चेक या रेगेक्स क्लीनअप चलाएँ ताकि डाउनस्ट्रीम सर्चेबिलिटी में सुधार हो। |
| **पैरेललिज़्म** | यदि आपके पास मल्टी‑नोड सेटअप है, तो फ़ोल्डर्स को वर्कर्स में वितरित करें और अंत में `.txt` आउटपुट को मर्ज करें। |

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं इसे सीधे PDFs के साथ उपयोग कर सकता हूँ?**  
A: बिल्कुल। प्रत्येक PDF पेज को पहले इमेज में बदलें (उदाहरण के लिए `pdf2image` का उपयोग करके) और प्राप्त सूची को `recognize_batch` को दें। पाइपलाइन का बाकी हिस्सा अपरिवर्तित रहता है।

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर करने में मदद करेंगे।

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}