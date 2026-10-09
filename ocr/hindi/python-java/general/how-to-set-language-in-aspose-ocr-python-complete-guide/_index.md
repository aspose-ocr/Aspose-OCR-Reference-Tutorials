---
category: general
date: 2026-01-12
description: Aspose OCR Python में भाषा कैसे सेट करें और कस्टम शब्दकोश का उपयोग करके
  छवि से टेक्स्ट निकालें। डेवलपर्स के लिए चरण‑दर‑चरण ट्यूटोरियल।
draft: false
keywords:
- how to set language
- extract text from image
- how to extract text
- how to add dictionary
- how to process image
language: hi
og_description: Aspose OCR Python में भाषा कैसे सेट करें और कस्टम शब्दकोश के साथ छवि
  से टेक्स्ट निकालें। कुछ ही मिनटों में पूरी प्रक्रिया सीखें।
og_title: Aspose OCR Python में भाषा कैसे सेट करें – पूर्ण गाइड
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Aspose OCR Python में भाषा कैसे सेट करें – पूर्ण गाइड
url: /hi/python-java/general/how-to-set-language-in-aspose-ocr-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Python में भाषा कैसे सेट करें – पूर्ण गाइड

क्या आपने कभी **भाषा कैसे सेट करें** के बारे में सोचा है जब आप Python में Aspose OCR का उपयोग करते हैं? आप अकेले नहीं हैं—कई डेवलपर्स इस समस्या का सामना करते हैं जब डिफ़ॉल्ट अंग्रेज़ी मॉडल प्रोडक्ट कोड, सीरियल नंबर या बहुभाषी टेक्स्ट को पहचान नहीं पाता। अच्छी खबर यह है कि समाधान सरल और शक्तिशाली दोनों है। इस ट्यूटोरियल में हम भाषा को कॉन्फ़िगर करने, कस्टम डिक्शनरी जोड़ने, इमेज से टेक्स्ट निकालने, और अंत में सर्वोत्तम OCR परिणामों के लिए इमेज प्रोसेस करने की प्रक्रिया को चरण‑बद्ध तरीके से देखेंगे।

हम सब कुछ कवर करेंगे: लाइब्रेरी इंस्टॉल करने से लेकर एक पूरा उदाहरण चलाने तक जो निकाले गए टेक्स्ट को प्रिंट करता है। अंत तक आप **इमेज से टेक्स्ट निकालना** आत्मविश्वास के साथ कर पाएँगे, चाहे कंटेंट में अजीब कोड या मिश्रित भाषाएँ हों।

## आवश्यकताएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* Python 3.8+ इंस्टॉल हो (कोड f‑strings का उपयोग करता है, इसलिए पुराने संस्करण काम नहीं करेंगे)।
* एक सक्रिय Aspose OCR for Python लाइसेंस या फ्री ट्रायल की।
* `asposeocr` पैकेज `pip install asposeocr` के ज़रिए इंस्टॉल किया हुआ हो।
* एक सैंपल इमेज (`product_label.png`) जिसमें वह टेक्स्ट हो जिसे आप पढ़ना चाहते हैं।

अगर आपके पास ये सब है, तो बढ़िया—आगे बढ़ते हैं। अगर नहीं, तो Aspose की वेबसाइट से फ्री ट्रायल लें और इंस्टॉल कमांड चलाएँ; इसमें एक मिनट से कम समय लगेगा।

## चरण 1: Aspose OCR मॉड्यूल इम्पोर्ट करें

सबसे पहले आपको OCR क्लासेज़ को अपने स्क्रिप्ट में लाना होगा। यही **भाषा कैसे सेट करें** के बाद के कदमों की नींव है।

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr
```

> **Pro tip:** इम्पोर्ट्स को फ़ाइल के शीर्ष पर रखें। इससे स्क्रिप्ट को स्कैन करना आसान हो जाता है, खासकर जब आप बाद में वापस आते हैं।

## चरण 2: भाषा कैसे सेट करें

डिफ़ॉल्ट रूप से, Aspose OCR अंग्रेज़ी मानता है। यदि आपकी इमेज में फ़्रेंच, जर्मन या कोई अन्य भाषा है, तो आपको इंजन को बताना होगा कि कौन सी भाषा उपयोग करनी है। यही वह जगह है जहाँ मुख्य कीवर्ड काम आता है।

```python
# Step 2: Create an OCR engine and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # change to ocr.Language.FRENCH, etc.
```

यह क्यों महत्वपूर्ण है? OCR इंजन भाषा‑विशिष्ट कैरेक्टर मॉडल पर निर्भर करते हैं। सही भाषा प्रदान करने से सटीकता में बहुत सुधार आता है—विशेषकर एक्सेंटेड कैरेक्टर्स या भाषा‑विशिष्ट लिगेचर के लिए।

> **Note:** यदि आपको एक साथ कई भाषाओं का समर्थन करना है, तो आप `ocr.Language.ENGLISH | ocr.Language.SPANISH` जैसी लिस्ट पास कर सकते हैं।

## चरण 3: डिक्शनरी (उपयोगकर्ता‑परिभाषित शब्द) कैसे जोड़ें

कभी‑कभी OCR इंजन “AB‑1234” जैसे प्रोडक्ट कोड को गलत पढ़ लेता है। आप कस्टम डिक्शनरी फीड करके कॉन्फिडेंस बढ़ा सकते हैं। यह सीधे **डिक्शनरी कैसे जोड़ें** का उत्तर देता है।

```python
# Step 3: Supply product codes that must be recognized with higher confidence
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])
```

इंजन इन शब्दों को “ज्ञात” मानता है और समान दिखने वाले कैरेक्टर्स की तुलना में इन्हें प्राथमिकता देता है। यह SKU नंबर, सीरियल कोड, या ब्रांड नामों के लिए बहुत उपयोगी है जो सामान्य भाषा का हिस्सा नहीं होते।

## चरण 4: इमेज कैसे प्रोसेस करें

अब जब इंजन कॉन्फ़िगर हो गया है, आपको उस इमेज को लोड करना होगा जिसे आप विश्लेषण करना चाहते हैं। यह **इमेज कैसे प्रोसेस करें** को साफ़ और दोहराने योग्य तरीके से संबोधित करता है।

```python
# Step 4: Load the image containing the product label
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")
```

यदि आप PDFs के साथ काम कर रहे हैं, तो आप प्रत्येक पेज को पहले इमेज में बदल सकते हैं—Aspose OCR यह सुविधा बॉक्स से बाहर प्रदान करता है।

## चरण 5: इमेज से टेक्स्ट कैसे निकालें

सब कुछ सेट हो जाने के बाद, अंतिम कदम OCR चलाना और टेक्स्ट प्राप्त करना है। यही **इमेज से टेक्स्ट कैसे निकालें** का मुख्य भाग है।

```python
# Step 5: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)

# Step 6: Print the extracted text
print(ocr_result.text)
```

जब आप स्क्रिप्ट चलाएँगे, तो आपको कुछ इस तरह दिखना चाहिए:

```
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

यदि आउटपुट गड़बड़ दिखे, तो दोबारा जांचें कि आपने सही भाषा सेट की है और आपकी कस्टम डिक्शनरी में वही स्ट्रिंग्स हैं जो आप अपेक्षित कर रहे हैं।

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ मिलाकर, यहाँ पूरा स्क्रिप्ट है जिसे आप `extract_label.py` नाम की फ़ाइल में कॉपी‑पेस्ट कर सकते हैं। `YOUR_DIRECTORY` को अपनी इमेज के वास्तविक पाथ से बदलें।

```python
import asposeocr as ocr

# Create OCR engine and set language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # Change if needed

# Add custom dictionary entries
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])

# Load the target image
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")

# Perform OCR
ocr_result = ocr_engine.process(image)

# Output the result
print("=== OCR Extraction Result ===")
print(ocr_result.text)
```

### अपेक्षित आउटपुट

```
=== OCR Extraction Result ===
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

यदि आप डिक्शनरी में जोड़े गए कोड्स को ठीक‑ठीक देखते हैं, तो आपने सफलतापूर्वक **भाषा कैसे सेट करें**, **डिक्शनरी कैसे जोड़ें**, और **इमेज से टेक्स्ट कैसे निकालें** को Aspose OCR के साथ महारत हासिल कर ली है।

## सामान्य किनारी मामलों का समाधान

| स्थिति | क्या करें |
|-----------|------------|
| **इमेज धुंधली है** | `ocr.Image.apply_filter()` से शार्पन करके `process()` से पहले प्री‑प्रोसेस करें। |
| **एक इमेज में कई भाषाएँ** | `ocr_engine.language = ocr.Language.ENGLISH | ocr.Language.SPANISH` सेट करें। |
| **बड़ी PDFs** | प्रत्येक पेज पर लूप चलाएँ, उसे `ocr.Image` में बदलें, और हर पेज के लिए `process()` कॉल करें। |
| **अप्रत्याशित कैरेक्टर्स** | उन्हें उपयोगकर्ता‑परिभाषित शब्दों की लिस्ट में जोड़ें; Aspose OCR उन्हें हाई‑कॉन्फिडेंस टोकन मानता है। |

इन टिप्स से आपका OCR पाइपलाइन मजबूत बना रहेगा, भले ही इनपुट परिपूर्ण न हो।

## दृश्य संदर्भ

![how to set language in Aspose OCR example](image.png "Screenshot showing how to set language in Aspose OCR Python example")

*Alt text:* **भाषा कैसे सेट करें** स्क्रीनशॉट जो Python IDE में भाषा प्रॉपर्टी असाइनमेंट को दर्शाता है।

## निष्कर्ष

अब आप जानते हैं कि Aspose OCR Python में **भाषा कैसे सेट करें**, **डिक्शनरी कैसे जोड़ें**, और **इमेज से टेक्स्ट कैसे निकालें** तथा **इमेज कैसे प्रोसेस करें** के लिए कौन‑से कदम उठाने हैं ताकि सर्वोत्तम परिणाम मिलें। ऊपर दिया गया पूर्ण उदाहरण किसी भी प्रोजेक्ट में डाला जा सकता है, विभिन्न भाषाओं के लिए समायोजित किया जा सकता है, और बैच प्रोसेसिंग या PDF इनपुट को संभालने के लिए विस्तारित किया जा सकता है।

अगली चुनौती के लिए तैयार हैं? `ocr.Language.ENGLISH` को `ocr.Language.FRENCH` से बदलें और फ़्रेंच‑भाषी लेबल्स पर सटीकता में सुधार देखें। या `set_user_defined_words` मेथड के साथ पूरे प्रोडक्ट कैटलॉग को शामिल करने का प्रयोग करें—आपका OCR इंजन हर एंट्री को हाई‑कॉन्फिडेंस मैच मान लेगा।

हैप्पी कोडिंग, और आपके OCR परिणाम हमेशा क्रिस्टल‑क्लियर रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}