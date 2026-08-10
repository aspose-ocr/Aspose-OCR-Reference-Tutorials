---
category: general
date: 2026-06-25
description: Python में OCR का उपयोग कैसे करें – जानें कि OCR के लिए छवि कैसे लोड
  करें, क्षेत्र में टेक्स्ट को पहचानें, और क्षेत्र के टेक्स्ट को जल्दी निकालें।
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: hi
og_description: Python में OCR का उपयोग कैसे करें – छवि लोड करने, किसी विशिष्ट क्षेत्र
  में टेक्स्ट पहचानने और इनवॉइस नंबर निकालने के लिए चरण-दर-चरण मार्गदर्शिका।
og_title: 'OCR Python का उपयोग कैसे करें: छवि लोड करें और क्षेत्र का टेक्स्ट निकालें'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'OCR Python का उपयोग कैसे करें: छवि लोड करें और क्षेत्र का टेक्स्ट निकालें'
url: /hi/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Python का उपयोग कैसे करें: इमेज लोड करें और क्षेत्र का टेक्स्ट निकालें

**Python में OCR का उपयोग कैसे करें** उतना ही आसान है जितना आप सोचते हैं। कभी स्कैन की हुई इनवॉइस को देखकर सोचा है कि पूरे पेज को पार्स किए बिना सिर्फ इनवॉइस नंबर कैसे निकाला जाए? आप अकेले नहीं हैं—कई डेवलपर्स को ऑप्टिकल कैरेक्टर रिकग्निशन के साथ पहली बार काम करते समय यही समस्या आती है। इस गाइड में हम इमेज को OCR के लिए लोड करने, एक आयत (rectangle) परिभाषित करने, उस क्षेत्र में टेक्स्ट पहचानने, और अंत में उस क्षेत्र का टेक्स्ट निकालने की प्रक्रिया को चरण‑दर‑चरण देखेंगे। अंत तक आपके पास एक तैयार‑स्क्रिप्ट होगी जो आपको चाहिए हुआ किसी भी टेक्स्ट को अलग‑अलग निकाल सकेगी।

> *Pro tip:* यदि आप PDFs के साथ काम कर रहे हैं, तो पहले प्रत्येक पेज को इमेज में बदलें—ज्यादातर OCR लाइब्रेरी PNG/JPEG को सबसे बेहतर तरीके से संभालती हैं।

## आपको क्या चाहिए

- Python 3.8+ (सबसे नवीन स्थिर रिलीज़ की सलाह दी जाती है)  
- एक OCR लाइब्रेरी जो `OcrEngine` क्लास प्रदान करती है (उदाहरण के लिए **ocr** को `pip install ocr-lib` से इंस्टॉल करें)  
- एक सैंपल इमेज—यहाँ हम `invoice.png` का उपयोग करेंगे, जिसे आप अपनी इच्छित फ़ोल्डर में रखेंगे  
- आयत (x, y, width, height) की बुनियादी समझ  

कोई भारी डिपेंडेंसी नहीं, GPU की जरूरत नहीं—सिर्फ साधारण CPU काम, जिससे यह पोर्टेबल रहता है।

---

## OCR का उपयोग कैसे करें: इंजन इनिशियलाइज़ करें (Step 1)

कोई भी टेक्स्ट पढ़ने से पहले, आपको OCR इंजन का एक इंस्टेंस चाहिए। इसे वह दिमाग समझें जो पिक्सेल पैटर्न का विश्लेषण करेगा।

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*यह क्यों महत्वपूर्ण है:* इंजन को इनिशियलाइज़ करने से भाषा मॉडल लोड होते हैं और डिफ़ॉल्ट कॉन्फ़िगरेशन सेट होते हैं। इस चरण को छोड़ने पर `recognize_region` कॉल करते ही एक एक्सेप्शन फेंका जाएगा।

---

## OCR के लिए इमेज लोड करें (Step 2)

अब जब इंजन तैयार है, हम उसे एक इमेज दें। लाइब्रेरी की `Image.load` मेथड सामान्य फॉर्मैट को संभालती है और बिटमैप को सामान्यीकृत करती है।

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

यदि फ़ाइल नहीं मिलती, तो Python `FileNotFoundError` फेंकेगा। सुनिश्चित करें कि पाथ एब्सोल्यूट है या आपके स्क्रिप्ट की वर्किंग डायरेक्टरी के रिलेटिव है।  

*एज केस:* कुछ OCR इंजन ग्रेस्केल इमेज की अपेक्षा करते हैं। यदि सटीकता कम लग रही है, तो पहले इमेज को ग्रेस्केल में बदलें:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## क्षेत्र में टेक्स्ट पहचानें (Step 3)

क्षेत्र को परिभाषित करना वह जगह है जहाँ आप इंजन को बताते हैं कि *कहाँ* देखना है। `Rectangle` सब‑पिक्सेल प्रिसीजन के लिए फ़्लोटिंग‑पॉइंट वैल्यूज़ लेता है, जो हाई‑रेज़ोल्यूशन स्कैन के साथ काम करते समय उपयोगी होता है।

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – आयत का टॉप‑लेफ़्ट कोना (पिक्सेल में)  
- **width, height** – बॉक्स का आकार  

आप सोच रहे होंगे कि ये नंबर कैसे पता करें। एक तेज़ तरीका है इमेज को किसी भी एडिटर (जैसे GIMP या Paint.NET) में खोलें और सिलेक्शन टूल से कोऑर्डिनेट्स पढ़ें।  

*पूरे पेज को OCR क्यों नहीं करते?* क्षेत्र को सीमित करने से शोर कम होता है, प्रोसेसिंग तेज़ होती है, और इनवॉइस नंबर जैसे छोटे फ़ील्ड की सटीकता में बहुत सुधार आता है।

---

## क्षेत्र का टेक्स्ट निकालें (Step 4)

क्षेत्र सेट हो जाने पर, इंजन से केवल उसी स्लाइस को पहचानने को कहें। परिणाम ऑब्जेक्ट में कच्चा टेक्स्ट और कॉन्फिडेंस स्कोर होते हैं।

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

यदि OCR इंजन कई भाषाओं को सपोर्ट करता है, तो आप वैकल्पिक भाषा कोड भी पास कर सकते हैं:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*आम गलती:* कुछ इंजन शब्दों की लिस्ट लौटाते हैं, न कि एकल स्ट्रिंग। ऐसे में उन्हें जोड़ें:

```python
text = " ".join(region_result.words)
```

---

## निकाला गया इनवॉइस नंबर आउटपुट करें (Step 5)

अंत में, निकाले गए टेक्स्ट को प्रिंट या स्टोर करें। आप स्ट्रिंग को पोस्ट‑प्रोसेस करके अतिरिक्त व्हाइटस्पेस या नॉन‑न्यूमेरिक कैरेक्टर्स हटा भी सकते हैं।

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

सही ढंग से संरेखित आयत के साथ स्क्रिप्ट चलाने पर आपको कुछ इस तरह का आउटपुट मिलेगा:

```
Invoice number: 20231578
```

यदि गड़बड़ कैरेक्टर्स दिखें, तो आयत के कोऑर्डिनेट्स दोबारा जाँचें या इमेज रेज़ोल्यूशन बढ़ाने पर विचार करें।

---

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ मिलाकर, यहाँ एक सेल्फ‑कंटेन्ड स्क्रिप्ट है जिसे आप कॉपी‑पेस्ट करके चला सकते हैं:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

फ़ाइल को `extract_invoice.py` के रूप में सेव करें, `YOUR_DIRECTORY` को वास्तविक फ़ोल्डर पाथ से बदलें, और चलाएँ:

```bash
python extract_invoice.py
```

आपको कंसोल में इनवॉइस नंबर प्रिंट होते दिखना चाहिए।

---

## अक्सर पूछे जाने वाले प्रश्न

**प्र: यदि इनवॉइस नंबर फैंसी फ़ॉन्ट में प्रिंटेड हो तो क्या करें?**  
उ: अधिकांश आधुनिक OCR इंजन विभिन्न फ़ॉन्ट्स को संभालते हैं, लेकिन आप कस्टम लैंग्वेज मॉडल ट्रेन करके या इमेज को प्री‑प्रोसेस (जैसे थ्रेशहोल्ड फ़िल्टर लगाकर) सटीकता बढ़ा सकते हैं।

**प्र: क्या मैं एक साथ कई फ़ील्ड निकाल सकता हूँ?**  
उ: बिल्कुल। `Rectangle` ऑब्जेक्ट्स की एक लिस्ट बनाएं—प्रत्येक फ़ील्ड के लिए एक—और उन पर लूप चलाकर प्रत्येक परिणाम को डिक्शनरी में स्टोर करें।

**प्र: क्या यह मल्टी‑पेज PDFs पर काम करता है?**  
उ: प्रत्येक पेज को पहले इमेज में बदलें (`pdf2image` या समान टूल से), फिर प्रत्येक पेज पर वही रीजन‑बेस्ड एक्सट्रैक्शन लागू करें।

---

## निष्कर्ष

इस ट्यूटोरियल में हमने **Python में OCR का उपयोग कैसे करें** को कवर किया: इमेज लोड करना, एक विशिष्ट क्षेत्र में टेक्स्ट पहचानना, और उस क्षेत्र का टेक्स्ट निकालना—जो स्कैन किए हुए दस्तावेज़ों से इनवॉइस नंबर, ऑर्डर ID, या कोई भी छोटा डेटा स्निपेट निकालने के लिए परफेक्ट है। रुचि के क्षेत्र को अलग करके आप गति, सटीकता, और पोस्ट‑प्रोसेसिंग की झंझट कम कर सकते हैं।

अगला कदम तैयार है? स्क्रिप्ट को इस तरह विस्तारित करें कि वह **OCR के लिए इमेज लोड** को बैच इनवॉइस फ़ोल्डर से करे, या **क्षेत्र में टेक्स्ट पहचानें** को डेट, टोटल जैसे विभिन्न फ़ील्ड्स के लिए प्रयोग करें। पैटर्न वही रहता है—सिर्फ आयत के कोऑर्डिनेट्स बदलें।

यदि आपको कोई समस्या आई या सुधार के लिए आइडिया हैं, तो नीचे कमेंट करें। Happy coding, और आपका OCR पाइपलाइन हमेशा सटीक रहे!

## आगे आप क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [इमेज से टेक्स्ट निकालें Aspose OCR के साथ – चरण‑दर‑चरण गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [OCR में आयतें तैयार करके इमेज से टेक्स्ट निकालें](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [AspOCR का उपयोग: .NET के लिए इमेज OCR फ़िल्टर प्री‑प्रोसेस](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}