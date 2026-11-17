---
category: general
date: 2026-06-25
description: Python में OCR इंजन को इनिशियलाइज़ करें ताकि कस्टम डिक्शनरीज़, भाषा सेटिंग्स
  और क्षेत्र लक्ष्यीकरण का उपयोग करके मल्टी‑पेज PDFs से टेक्स्ट निकाला जा सके।
draft: false
keywords:
- initialize OCR engine
- configure OCR language
- OCR image preprocessing
- OCR custom dictionary
- recognize multi-page PDF
language: hi
og_description: Python में OCR इंजन को प्रारंभ करें ताकि वियतनामी PDFs को विश्वसनीय
  रूप से पढ़ा जा सके, भाषा, पूर्व-प्रसंस्करण और सटीक परिणामों के लिए कस्टम शब्दकोश
  को कॉन्फ़िगर करें।
og_title: OCR इंजन प्रारंभ करें – चरण‑दर‑चरण PDF निष्कर्षण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  headline: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  type: TechArticle
- description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  name: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed. - An OCR library that exposes an `OcrEngine` class
      (the sample uses a hypothetical `ocr` package; replace with your actual SDK).
      - A sample multi‑page PDF (`sample.pdf`) placed in a known directory. - Basic
      familiarity with Python dictionaries and loops.'
  - name: Pro tip
    text: If you ever need to support multiple languages in the same run, you can
      switch `ocr_engine.language` on the fly before processing each page. Just remember
      to re‑initialize any heavy models if the SDK requires it.
  - name: Expected Output
    text: 'Running the script against a three‑page invoice PDF might produce:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: OCR इंजन को प्रारंभ करें – PDF टेक्स्ट निष्कर्षण के लिए पूर्ण गाइड
url: /hi/python-java/general/initialize-ocr-engine-complete-guide-for-pdf-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR इंजन को इनिशियलाइज़ करें – PDF टेक्स्ट एक्सट्रैक्शन के लिए पूरा गाइड

क्या आपको कभी **OCR इंजन को इनिशियलाइज़** करना पड़ा है वियतनामी इनवॉइस की एक बैच के लिए, लेकिन आप नहीं जानते थे कहाँ से शुरू करें? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में पहला बाधा यह है कि OCR लाइब्रेरी को आपके PDF के साथ कैसे जोड़ा जाए, ख़ासकर जब आपको भाषा, प्री‑प्रोसेसिंग, या कस्टम डिक्शनरी को ट्यून करना पड़े।  

इस गाइड में हम एक पूर्ण, रन करने योग्य उदाहरण के माध्यम से दिखाएंगे कि कैसे **OCR इंजन को इनिशियलाइज़** करें, भाषा कॉन्फ़िगर करें, स्मार्ट इमेज प्री‑प्रोसेसिंग सक्षम करें, कस्टम डिक्शनरी जोड़ें, और अंत में मल्टी‑पेज PDF के हर पेज से संरचित डेटा निकालें। अंत तक आपके पास एक सेल्फ‑कंटेन्ड स्क्रिप्ट होगी जिसे आप अपने प्रोजेक्ट में ड्रॉप कर सकते हैं—कोई लापता हिस्से नहीं, कोई “डॉक्यूमेंट देखें” शॉर्टकट नहीं।

## आप क्या सीखेंगे

- कैसे **OCR इंजन को इनिशियलाइज़** करें वियतनामी भाषा सपोर्ट के साथ।  
- क्यों **OCR भाषा को कॉन्फ़िगर** करना सटीकता के लिए महत्वपूर्ण है।  
- **OCR इमेज प्री‑प्रोसेसिंग** विकल्पों जैसे auto‑deskew और auto‑binarize का उपयोग।  
- डोमेन‑स्पेसिफिक टर्म्स की पहचान बढ़ाने के लिए **OCR कस्टम डिक्शनरी** जोड़ना।  
- **मल्टी‑पेज PDF** फ़ाइलों को पहचानना और एक विशिष्ट क्षेत्र (जैसे, कुल राशि) निकालना।  
- रॉ परिणामों को एक साफ़ JSON‑जैसे स्ट्रक्चर में बदलना ताकि डाउनस्ट्रीम प्रोसेसिंग आसान हो।

### प्री‑रिक्विज़िट्स

- Python 3.8+ इंस्टॉल किया हुआ।  
- एक OCR लाइब्रेरी जो `OcrEngine` क्लास एक्सपोज़ करती है (सैंपल में एक काल्पनिक `ocr` पैकेज इस्तेमाल किया गया है; इसे अपने वास्तविक SDK से बदलें)।  
- एक सैंपल मल्टी‑पेज PDF (`sample.pdf`) जिसे ज्ञात डायरेक्टरी में रखें।  
- Python डिक्शनरीज़ और लूप्स की बेसिक समझ।

यदि आपके पास ये सब है, तो चलिए शुरू करते हैं।

---

## चरण 1: Python में OCR इंजन को कैसे इनिशियलाइज़ करें

सबसे पहला काम जो आपको करना है वह है **OCR इंजन को इनिशियलाइज़** करना। इसे ऐसे समझें जैसे मशीन को ऑन करना और उसे बताना कि आप कौन सी भाषा फीड करेंगे।

```python
import ocr  # Replace with your actual OCR package

# Create the engine instance
ocr_engine = ocr.OcrEngine()

# Set the language to Vietnamese – this tells the engine which character set to expect
ocr_engine.language = ocr.Language.Vietnamese
```

> **यह क्यों महत्वपूर्ण है:**  
> अधिकांश OCR इंजन जेनरिक लैंग्वेज पैक्स के साथ आते हैं। `ocr_engine.language` को स्पष्ट रूप से सेट करके आप इंजन को गलत कैरेक्टर्स गेस करने से रोकते हैं, जो वियतनामी में सामान्य डाइअक्रिटिक के लिए मिस‑रिकग्निशन को काफी घटा देता है।

### प्रो टिप
यदि आपको एक ही रन में कई भाषाओं को सपोर्ट करना है, तो आप प्रत्येक पेज प्रोसेस करने से पहले `ocr_engine.language` को ऑन‑द‑फ्लाई बदल सकते हैं। बस याद रखें कि यदि SDK आवश्यक करता है तो किसी भी हेवी मॉडल को री‑इनिशियलाइज़ करना पड़ेगा।

---

## चरण 2: OCR इमेज प्री‑प्रोसेसिंग विकल्प सक्षम करें

रॉ स्कैन अक्सर परफेक्ट नहीं होते। स्क्यूड पेज, अनियमित लाइटिंग, या लो कॉन्ट्रास्ट सबसे अच्छे रिकग्नाइज़र को भी फेल कर सकते हैं। इसलिए हम **OCR इमेज प्री‑प्रोसेसिंग** को इनिशियलाइज़ेशन के तुरंत बाद कॉन्फ़िगर करते हैं।

```python
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,      # Auto‑rotate to correct tilt
    auto_binarize=True    # Convert to black‑and‑white for sharper edges
)
```

ये दो फ्लैग्स अक्सर अधिकांश स्कैन किए गए इनवॉइस को साफ़ करने के लिए पर्याप्त होते हैं। यदि आपके सोर्स PDF पहले से हाई‑क्वालिटी हैं, तो आप इन्हें बंद करके प्रति पेज कुछ मिलीसेकंड बचा सकते हैं।

---

## चरण 3: OCR कस्टम डिक्शनरी जोड़ें

डोमेन‑स्पेसिफिक टर्म्स—जैसे ऑर्डर कोड, प्रोडक्ट आईडी, या लीगल एब्रीविएशन—जेनरिक लैंग्वेज मॉडल में अक्सर नहीं होते। एक **OCR कस्टम डिक्शनरी** फीड करके आप इंजन को एक चीट शीट दे रहे हैं।

```python
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]
```

> **अंदर क्या हो रहा है?**  
> इंजन इस लिस्ट में मौजूद किसी भी शब्द के लिए कॉन्फिडेंस स्कोर को बढ़ा देता है, जिससे वह किसी अन्य शब्द के रूप में मिस‑रीड होने की संभावना बहुत कम हो जाती है।

---

## चरण 4: मल्टी‑पेज PDF को पहचानें – सभी टेक्स्ट एक साथ निकालें

अब जब इंजन पूरी तरह कॉन्फ़िगर हो गया है, हम **मल्टी‑पेज PDF** फ़ाइलों को पहचान सकते हैं। `recognize_multi_page` मेथड एक लिस्ट रिटर्न करता है जहाँ प्रत्येक एलिमेंट एक सिंगल पेज को दर्शाता है, जो पहले से OCR‑प्रोसेस्ड है।

```python
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)
```

यदि आप सैकड़ों पेज वाले बड़े PDF से निपट रहे हैं, तो मेमोरी उपयोग कम रखने के लिए उन्हें चंक्स में प्रोसेस करने पर विचार करें। अधिकांश SDK इस परिदृश्य के लिए स्ट्रीमिंग API प्रदान करते हैं।

---

## चरण 5: हर पेज से एक विशिष्ट क्षेत्र निकालें

अधिकांश इनवॉइस में “Total Amount” फ़ील्ड एक ही जगह पर रहता है। पूरे पेज टेक्स्ट को पार्स करने की बजाय, हम इंजन को एक रेक्टैंगल पर फोकस करने के लिए कह सकते हैं।

```python
from ocr import Rectangle  # Adjust import based on your SDK

for page_index, page in enumerate(pages, start=1):
    # Define the rectangle (x, y, width, height) that encloses the total amount
    total_region = Rectangle(400, 650, 200, 50)

    # Run OCR only on that region
    region_result = ocr_engine.recognize_region(page.image, total_region)
```

> **किसी क्षेत्र को टार्गेट करने का कारण?**  
> OCR को छोटे एरिया तक सीमित करने से प्रोसेसिंग तेज़ होती है और फॉल्स पॉज़िटिव्स कम होते हैं, ख़ासकर जब बाकी पेज शोरयुक्त हो।

---

## चरण 6: प्रत्येक पेज के लिए JSON‑जैसी डिक्शनरी बनाएं

रॉ टेक्स्ट होना अच्छा है, लेकिन डाउनस्ट्रीम सिस्टम आमतौर पर स्ट्रक्चर्ड डेटा की उम्मीद करते हैं। नीचे हम एक साफ़ डिक्शनरी बनाते हैं जो पेज नंबर, पूरा पेज टेक्स्ट, निकाली गई टोटल, और सभी पहचान किए गए शब्दों के कॉन्फिडेंस स्कोर को कैप्चर करती है।

```python
    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    # Step 7: Output the result for the current page
    print(page_output)
```

स्क्रिप्ट चलाने पर यह डिक्शनरी की एक श्रृंखला आउटपुट करेगी—प्रति पेज एक—जो इस तरह दिखेगी:

```json
{
  "page": 1,
  "full_text": "....",
  "total_amount": "1,250,000 VND",
  "words": [
    {"text": "MãĐơnHàng", "conf": 0.98},
    {"text": "KháchHàng", "conf": 0.96},
    ...
  ]
}
```

आप आसानी से आउटपुट को फ़ाइल (`> results.jsonl`) में रीडायरेक्ट कर सकते हैं ताकि बाद में बैच प्रोसेसिंग की जा सके।

---

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ मिलाकर, यहाँ पूरा स्क्रिप्ट है जिसे आप कॉपी‑पेस्ट करके चला सकते हैं:

```python
import ocr
from ocr import Rectangle

# -------------------------------------------------
# 1️⃣ Initialize the OCR engine and configure it
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.Vietnamese
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]

# -------------------------------------------------
# 2️⃣ Recognize all pages of a multi‑page PDF
# -------------------------------------------------
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)

# -------------------------------------------------
# 3️⃣ Iterate through each page, extract region, and build output
# -------------------------------------------------
for page_index, page in enumerate(pages, start=1):
    total_region = Rectangle(400, 650, 200, 50)          # region of interest
    region_result = ocr_engine.recognize_region(page.image, total_region)

    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    print(page_output)   # Replace with logging or file write as needed
```

### अपेक्षित आउटपुट

तीन‑पेज इनवॉइस PDF के खिलाफ स्क्रिप्ट चलाने पर यह आउटपुट हो सकता है:

```
{'page': 1, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.99}, ...]}
{'page': 2, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.98}, ...]}
{'page': 3, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.97}, ...]}
```

इसे `jq` या किसी भी JSON पार्सर में पाइप करके स्ट्रक्चर वेरिफ़ाई कर सकते हैं।

---

## सामान्य प्रश्न और एज केस

| प्रश्न | उत्तर |
|----------|--------|
| **अगर मेरा PDF पासवर्ड‑प्रोटेक्टेड है तो?** | अधिकांश SDK आपको `recognize_multi_page` कॉल में `password` आर्ग्यूमेंट पास करने की अनुमति देते हैं। बस कॉल में `password="mySecret"` जोड़ दें। |
| **मेरी स्कैन ग्रेस्केल में हैं, ब्लैक‑एंड‑व्हाइट नहीं।** | `auto_binarize` विकल्प इसे संभाल लेगा, लेकिन आप `recognize_region` को इमेज फीड करने से पहले `Pillow` से मैन्युअली भी कन्वर्ट कर सकते हैं। |
| **कुल राशि कभी‑कभी अलग कोऑर्डिनेट पर आती है।** | या तो रेक्टैंगल को डायनामिकली कंप्यूट करें (जैसे टेम्प्लेट मैचिंग से) या पूरा‑पेज OCR चलाएँ और फिर `r'\d{1,3}(,\d{3})* VND'` जैसी रेगेक्स से टेक्स्ट सर्च करें। |
| **500‑पेज PDF पर परफॉर्मेंस स्लो है।** | पेजों को बैच में प्रोसेस करें: 50 पेज प्रोसेस करें, रिज़ल्ट लिखें, फिर मेमोरी फ्री करने के लिए `pages` लिस्ट को क्लियर करें। यदि स्कैन पहले से स्ट्रेट हैं तो `auto_deskew` को डिसेबल करें। |
| **भविष्य में अन्य भाषाओं को कैसे हैंडल करें?** | बस `ocr_engine.language = ocr.Language.English` (या कोई भी सपोर्टेड एनोम) को `recognize_multi_page` कॉल से पहले बदल दें। बाकी पाइपलाइन वैसी ही रहेगी। |

---

## प्रोडक्शन‑रेडी डिप्लॉयमेंट के टिप्स

1. **एरर हैंडलिंग** – OCR कॉल को `try/except` ब्लॉक्स में रैप करें; फेल होने पर पेज इंडेक्स लॉग करें ताकि बाद में रिट्राई किया जा सके।  
2. **लॉगिंग** – `print` की बजाय Python के `logging` मॉड्यूल का उपयोग करें ताकि वर्बोसिटी फ्लेक्सिबल रहे।  
3. **पैरालेलिज़्म** – यदि आपका OCR लाइब्रेरी थ्रेड‑सेफ़ है, तो `ThreadPoolExecutor` स्पॉन करके पेजों को एक साथ प्रोसेस करें।  
4. **कॉन्फ़िग फ़ाइल** – भाषा, डिक्शनरी, और रेक्टैंगल कोऑर्डिनेट्स को एक JSON/YAML फ़ाइल में स्टोर करें; इससे स्क्रिप्ट कई प्रोजेक्ट्स में री‑यूज़ेबल बनती है।  
5. **टेस्टिंग** – ज्ञात PDF के साथ एक छोटा टेस्ट सूट बनाएं और एसेर्ट करें कि निकाला गया `total_amount` अपेक्षित वैल्यू से मेल खाता है।  

---

## निष्कर्ष

आपने अभी **

## आगे क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और स्टेप‑बाय‑स्टेप एक्सप्लानेशन शामिल है, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}