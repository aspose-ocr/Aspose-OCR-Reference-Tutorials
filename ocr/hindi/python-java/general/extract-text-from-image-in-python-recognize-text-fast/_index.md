---
category: general
date: 2026-07-05
description: Python OCR का उपयोग करके छवि से टेक्स्ट निकालें। सीखें कि कैसे छवि से
  टेक्स्ट पहचाना जाए, OCR के लिए छवि लोड करें, और कुछ ही पंक्तियों में OCR भाषा सेट
  करें।
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: hi
og_description: Python OCR के साथ छवि से टेक्स्ट निकालें। यह गाइड दिखाता है कि छवि
  से टेक्स्ट कैसे पहचाना जाए, OCR के लिए छवि कैसे लोड करें, Python शैली में OCR इंजन
  कैसे बनाएं, और OCR भाषा कैसे सेट करें।
og_title: Python में छवि से टेक्स्ट निकालें – तेज़ी से टेक्स्ट पहचानें
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python में छवि से टेक्स्ट निकालें – तेज़ी से टेक्स्ट पहचानें
url: /hi/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में इमेज से टेक्स्ट निकालें – तेज़ी से टेक्स्ट पहचानें

क्या आपको कभी **इमेज से टेक्स्ट निकालने** की ज़रूरत पड़ी है लेकिन नहीं पता था कि कौन सी लाइब्रेरी चुनें? अगर आपने कभी खुद से *इमेज से टेक्स्ट कैसे पहचानें* पूछा है बिना बाहरी टूल्स के झंझट के, तो आप सही जगह पर हैं। इस ट्यूटोरियल में हम एक छोटा OCR इंजन बनाएँगे, उसे एक तस्वीर पर लगाएँगे, और टेक्स्ट निकालेंगे—बस इतना ही।

हम हर कदम को विस्तार से देखेंगे: **create OCR engine python**, **set OCR language**, **load image for OCR**, असिंक्रोनस रूप से पहचान चलाएँगे, और अंत में परिणाम पढ़ेंगे। अंत तक आपके पास एक स्व-निहित स्क्रिप्ट होगी जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं, चाहे वह दस्तावेज़‑डिजिटाइज़र हो या मेम्स पढ़ने वाला चैटबॉट।

## आपको क्या चाहिए

- Python 3.8+ (कोड 3.10 और नए संस्करणों पर भी काम करता है)  
- `ocr` पैकेज (Tesseract का हल्का रैपर – `pip install ocr` या अपनी पसंदीदा फ़ोर्क से इंस्टॉल करें)  
- एक इमेज फ़ाइल (`.jpg`, `.png`, आदि) जिसमें पढ़ने योग्य टेक्स्ट हो  
- असिंक्रोनस भाग के लिए थोड़ा धैर्य (यह तेज़ है, वादा)

बस इतना ही—कोई भारी डिपेंडेंसी नहीं, कोई नेटिव बिल्ड नहीं। यदि आपके सिस्टम पर पहले से Tesseract स्थापित है, तो `ocr` रैपर इसे स्वचालित रूप से ढूँढ लेगा।

## चरण 1: OCR इंजन बनाएं – एक्सट्रैक्शन का दिल

सबसे पहले: आपको एक इंजन ऑब्जेक्ट चाहिए जो अंतर्निहित OCR इंजन से बात करना जानता हो। इसे उस “दिमाग” की तरह समझें जो बाद में तस्वीर को प्रोसेस करेगा।

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*क्यों यह महत्वपूर्ण है*: बिना इंजन के आपके पास भाषा सेटिंग्स या असिंक्रोनस क्षमताओं का संदर्भ नहीं होगा। `OcrEngine` क्लास Tesseract के लो‑लेवल कमांड‑लाइन कॉल्स को एब्स्ट्रैक्ट करती है, जिससे आपको एक साफ़ Python API मिलती है।

## चरण 2: OCR भाषा सेट करें – इंजन को बताएं कि क्या अपेक्षा है

यदि आपका दस्तावेज़ अंग्रेज़ी है, तो आप डिफ़ॉल्ट छोड़ सकते हैं, लेकिन स्पष्ट रूप से सेट करना अच्छा अभ्यास है। यह दिखाता है कि अन्य लोकेल्स के लिए **set OCR language** कैसे सेट करें।

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **प्रो टिप**: मल्टी‑लिंगुअल PDFs के लिए, आप एक सूची जैसे `[ocr.Language.ENGLISH, ocr.Language.FRENCH]` पास कर सकते हैं। इंजन दोनों भाषाओं को स्वचालित रूप से आज़माएगा।

## चरण 3: OCR के लिए इमेज लोड करें – अपनी तस्वीर को मेमोरी में लाएँ

अब हम वास्तव में **load image for OCR** करेंगे। रैपर लेज़ी लोडिंग को सपोर्ट करता है, इसलिए फ़ाइल तभी पढ़ी जाती है जब इंजन को इसकी ज़रूरत होती है।

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*एज केस*: यदि इमेज बहुत बड़ी है (5 MB से अधिक), तो पहचान को तेज़ करने के लिए पहले उसका आकार बदलने पर विचार करें। आप यह Pillow से कर सकते हैं:

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## चरण 4: असिंक्रोनस रिकग्निशन शुरू करें – अपने ऐप को ब्लॉक न करें

OCR चलाने में एक‑दो सेकंड लग सकते हैं, विशेषकर बड़े स्कैन पर। `recognize_async` मेथड एक फ्यूचर रिटर्न करता है जिसे आप बाद में पोल कर सकते हैं, जिससे आप **OCR बैकग्राउंड में चलते समय अन्य काम कर सकते हैं**।

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

असिंक्रोनस क्यों? वेब सर्वर में आप नहीं चाहते कि एक ही अनुरोध पूरी वर्कर पूल को रोक दे। फ्यूचर ऑब्जेक्ट आपको नियंत्रण देता है: आप इसे async कोड में `await` कर सकते हैं या केवल तब ब्लॉक करें जब आपको वास्तव में परिणाम चाहिए।

## चरण 5: परिणाम प्राप्त करें – केवल आवश्यक होने पर ही ब्लॉक करें

जब आपको अंत में टेक्स्ट चाहिए, तो `future.get()` कॉल करें। यह कॉल **केवल यहाँ ब्लॉक करती है**, जिसका मतलब है कि आपका बाकी प्रोग्राम OCR समाप्त होने तक प्रतिक्रियाशील रहता है।

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

यदि आप `asyncio` लूप के अंदर हैं, तो आप `await future` भी कर सकते हैं – रैपर दोनों स्टाइल को सपोर्ट करता है।

## चरण 6: पहचाने गए टेक्स्ट का उपयोग करें – आपका डेटा तैयार है

अब जब आपके पास `result` ऑब्जेक्ट है, साधारण स्ट्रिंग निकालना बहुत आसान है। चलिए इसे प्रिंट करते हैं और दिखाते हैं कि इसे फ़ाइल में कैसे लिख सकते हैं।

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**अपेक्षित आउटपुट** (संक्षिप्त रूप में):

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

यदि इमेज में कोई टेक्स्ट नहीं है, तो `result.text` एक खाली स्ट्रिंग होगी—इस केस को सहजता से हैंडल करें।

## पूर्ण कार्यशील उदाहरण – एक स्क्रिप्ट में सभी चरण

नीचे पूरा, तैयार‑चलाने योग्य प्रोग्राम है। कॉपी‑पेस्ट करें, `image_path` को समायोजित करें, और आप तैयार हैं।

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **नोट**: `"YOUR_DIRECTORY/large_document.jpg"` को अपनी इमेज के वास्तविक पथ से बदलें। स्क्रिप्ट Windows, macOS, और Linux पर काम करती है जब तक Tesseract स्थापित है और आपके `PATH` में उपलब्ध है।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **गड़बड़ अक्षर** | गलत भाषा या भाषा डेटा फ़ाइलें अनुपलब्ध। | सुनिश्चित करें कि `engine.language` टेक्स्ट से मेल खाता है और संबंधित .traineddata फ़ाइल Tesseract के `tessdata` फ़ोल्डर में मौजूद है। |
| **बड़ी इमेज पर धीमी प्रदर्शन** | OCR पिक्सेल संख्या के साथ लगभग स्केल करता है। | इंजन को फीड करने से पहले आकार बदलें या डाउन‑सैंपल करें (Pillow स्निपेट देखें)। |
| **फ्यूचर कभी रिजॉल्व नहीं होता** | इमेज फ़ाइल भ्रष्ट या अपठनीय। | `future.get()` को try/except ब्लॉक में रखें और पहचान से पहले `image.is_valid()` की जाँच करें। |
| **Unicode हानि** |  |  |

## अब आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच खोजने में मदद करेंगे।

- [Aspose OCR के साथ इमेज से टेक्स्ट निकालें – चरण‑दर‑चरण गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [इमेज को टेक्स्ट में बदलें – URL से इमेज पर OCR करें](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [इमेज से टेक्स्ट निकालें – .NET के लिए Aspose OCR के साथ OCR ऑप्टिमाइज़ेशन](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}