---
category: general
date: 2026-07-05
description: Python OCR का उपयोग करके छवि से टेक्स्ट निकालें। जानें कि OCR के लिए
  छवि कैसे लोड करें, क्षेत्र से टेक्स्ट पढ़ें, और कुछ लाइनों के कोड से इनवॉइस से टेक्स्ट
  निकालें।
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: hi
og_description: Python OCR के साथ छवि से टेक्स्ट निकालें। यह गाइड दिखाता है कि OCR
  के लिए छवि कैसे लोड करें, क्षेत्र से टेक्स्ट पढ़ें, और जल्दी से इनवॉइस से टेक्स्ट
  निकालें।
og_title: छवि से टेक्स्ट निकालें – OCR का उपयोग करके क्षेत्र से टेक्स्ट पढ़ें
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: छवि से पाठ निकालें – OCR का उपयोग करके क्षेत्र से पाठ पढ़ें
url: /hi/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज से टेक्स्ट निकालें – रीजन‑आधारित OCR के साथ टेक्स्ट पढ़ें

क्या आपको कभी **इमेज से टेक्स्ट निकालना** पड़ा है लेकिन केवल एक विशेष भाग ही मायने रखता है—जैसे इनवॉइस पर कुल राशि? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में आपको **रीजन से टेक्स्ट पढ़ना** पड़ता है, पूरी तस्वीर को पार्स करने की बजाय। सौभाग्य से, कुछ ही पंक्तियों के Python कोड से आप इमेज को OCR के लिए लोड कर सकते हैं, एक ROI (Region of Interest) निर्धारित कर सकते हैं, और बिल्कुल वही अक्षर निकाल सकते हैं जो आपको चाहिए।

इस ट्यूटोरियल में हम एक पूर्ण, चलने योग्य उदाहरण के माध्यम से दिखाएंगे कि **OCR के लिए इमेज लोड करना**, ROI सेट करना, और अंत में **इनवॉइस से टेक्स्ट निकालना** कैसे किया जाता है। अंत तक आपके पास एक तैयार‑स्निपेट होगा जो किसी भी लोकप्रिय OCR लाइब्रेरी के साथ काम करेगा जो रीजन‑बेस्ड रिकग्निशन को सपोर्ट करती है।

---

## आपको क्या चाहिए

- Python 3.8+ (कोड 3.10 पर भी काम करता है)  
- एक OCR पैकेज जो `OcrEngine` क्लास प्रदान करता हो (डेमो के लिए हम एक काल्पनिक `ocr` मॉड्यूल इस्तेमाल करेंगे; इसे `pytesseract`, `easyocr` या किसी भी लाइब्रेरी से बदलें जो ROI सपोर्ट देती हो)  
- एक सैंपल इमेज—जैसे `invoice.png`—जिसमें स्पष्ट, प्रिंटेड टेक्स्ट हो  
- Python फ़ंक्शन और क्लास की बेसिक समझ (डीप लर्निंग की आवश्यकता नहीं)

यदि आपके पास ये सब है, तो चलिए शुरू करते हैं। यदि नहीं, तो python.org से नवीनतम Python डाउनलोड करें और `pip install your-ocr-lib` कमांड से OCR पैकेज इंस्टॉल करें।

---

![इमेज से टेक्स्ट निकालें उदाहरण](extract-text-from-image.png "इमेज से टेक्स्ट निकालें – रीजन‑आधारित OCR डेमो")

*ऊपर की तस्वीर में वह रीजन (लाल आयत) दिखाया गया है जिसे हम **इमेज से टेक्स्ट निकालने** के लिए टार्गेट करेंगे।*

---

## चरण 1: OCR लाइब्रेरी इंस्टॉल और इम्पोर्ट करें

सबसे पहले, सुनिश्चित करें कि OCR लाइब्रेरी आपके एनवायरनमेंट में उपलब्ध है। नीचे दिया गया इम्पोर्ट पैटर्न अधिकांश पैकेजों के लिए काम करता है जो हाई‑लेवल `OcrEngine` क्लास प्रदान करते हैं।

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **प्रो टिप:** यदि आप `pytesseract` इस्तेमाल कर रहे हैं, तो आपको Tesseract बाइनरी अलग से इंस्टॉल करनी होगी और `pytesseract.pytesseract.tesseract_cmd` को उसके पाथ पर सेट करना होगा।

---

## चरण 2: OCR इंजन बनाएं और भाषा सेट करें

इंजन बनाना सीधा है, लेकिन भाषा निर्दिष्ट करने से सटीकता में काफी सुधार होता है, विशेषकर उन इनवॉइस के लिए जिनमें नंबर और अंग्रेज़ी शब्द होते हैं।

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

हम यह क्यों करते हैं? OCR इंजन भाषा मॉडल का उपयोग करके अक्षर प्रेडिक्ट करता है; इसे इंग्लिश की उम्मीद बताने से “0” को “O” पढ़ने जैसी गलतियों से बचा जा सकता है।

---

## चरण 3: OCR के लिए इमेज लोड करें

अब हम वास्तव में **OCR के लिए इमेज लोड** करेंगे। अधिकांश लाइब्रेरी फ़ाइल पाथ या Pillow इमेज ऑब्जेक्ट को स्वीकार करती हैं। यहाँ हम सरलता के लिए लाइब्रेरी के बिल्ट‑इन लोडर का उपयोग कर रहे हैं।

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

सुनिश्चित करें कि पाथ सही डायरेक्टरी की ओर इशारा कर रहा है; एक आम गलती relative path को भूल जाना है जब स्क्रिप्ट अलग वर्किंग डायरेक्टरी से चलती है।

---

## चरण 4: ROI (Region of Interest) परिभाषित करें

ROI परिभाषित करना **रीजन से टेक्स्ट पढ़ने** का मुख्य हिस्सा है। इसे ऐसे समझें जैसे आप इनवॉइस के उस हिस्से के चारों ओर एक आयत खींच रहे हैं जहाँ कुल राशि लिखी होती है।

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` और `top` आयत के ऊपर‑बाएँ कोने के X और Y कोऑर्डिनेट दर्शाते हैं।  
- `width` और `height` बॉक्स का आकार निर्धारित करते हैं।  
- आप विभिन्न मानों के साथ प्रयोग कर सकते हैं, ऐसे इमेज व्यूअर का उपयोग करके जो पिक्सेल कोऑर्डिनेट दिखाता हो।

> **ROI क्यों महत्वपूर्ण है:** पूरे पेज पर OCR चलाने से CPU साइकिल बर्बाद होते हैं और अक्सर अनावश्यक टेक्स्ट, टेबल या ग्राफ़िक्स से शोर उत्पन्न होता है। रीजन पर फोकस करने से परिणाम साफ़ और प्रोसेसिंग तेज़ होती है।

---

## चरण 5: निर्दिष्ट रीजन पर OCR चलाएँ

सब कुछ सेट हो जाने के बाद, हम अंततः **इमेज से टेक्स्ट निकालेंगे**—लेकिन केवल उस ROI के भीतर जिसे हमने परिभाषित किया है।

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

`recognize` मेथड आमतौर पर एक ऑब्जेक्ट रिटर्न करता है जिसमें रॉ स्ट्रिंग, कॉन्फिडेंस स्कोर, और कभी‑कभी प्रत्येक शब्द के बाउंडिंग बॉक्स होते हैं। हमारे उद्देश्य के लिए हमें केवल प्लेन टेक्स्ट चाहिए।

---

## चरण 6: निकाले गए टेक्स्ट को आउटपुट करें

आइए परिणाम को प्रिंट करें और देखें कि हमें क्या मिला। यह चरण वास्तविक‑दुनिया परिदृश्य में **इनवॉइस से टेक्स्ट निकालने** को दर्शाता है।

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### अपेक्षित आउटपुट

```
Text inside ROI:
Total Amount: $1,245.67
```

यदि आपका इनवॉइस अलग लेआउट वाला है, तो आप आयत के भीतर मौजूद कोई भी टेक्स्ट देखेंगे—शायद इनवॉइस नंबर, डेट, या PO रेफ़रेंस।

---

## चरण 7: पुन: उपयोग योग्य फ़ंक्शन में रैप करें (वैकल्पिक)

समाधान को कई इनवॉइस पर पुन: उपयोग योग्य बनाने के लिए, लॉजिक को एक फ़ंक्शन में एन्कैप्सुलेट करें। यह भी **ROI पर OCR** को एक जनरिक यूटिलिटी के रूप में दर्शाता है।

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

अब आप इस फ़ंक्शन को किसी भी इनवॉइस के साथ कॉल कर सकते हैं:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## सामान्य समस्याएँ और उनके समाधान

| समस्या | क्यों होता है | समाधान |
|--------|--------------|--------|
| **खाली आउटपुट** | ROI वास्तव में किसी टेक्स्ट को कवर नहीं करता (गलत कोऑर्डिनेट)। | इमेज एडिटर से पिक्सेल वैल्यू दोबारा चेक करें; विज़ुअल डिबग ओवरले जोड़ें। |
| **गड़बड़ अक्षर** | कम रिज़ॉल्यूशन या खराब कॉन्ट्रास्ट वाली इमेज। | इमेज को प्री‑प्रोसेस करें: ग्रेस्केल में बदलें, थ्रेशोल्ड लागू करें (`cv2.threshold`)। |
| **गलत भाषा** | इंजन डिफ़ॉल्ट रूप से ऐसी भाषा उपयोग करता है जिसमें आवश्यक कैरेक्टर सेट नहीं है। | स्पष्ट रूप से `ocr_engine.language` को `ENGLISH` या उपयुक्त लोकेल पर सेट करें। |
| **परफ़ॉर्मेंस लैग** | बड़े इमेज पर बार‑बार OCR चलाना। | इमेज को रीसाइज़ करें या पहले ROI को क्रॉप करके प्रोसेस करें। |

---

## उदाहरण का विस्तार: कई ROIs

कभी‑कभी एक इनवॉइस में कई फ़ील्ड्स होते हैं जिन्हें निकालना होता है—जैसे **इनवॉइस से टेक्स्ट निकालना** कुल राशि और इनवॉइस डेट दोनों के लिए। आप आयतों की एक लिस्ट पर लूप कर सकते हैं:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

यह पैटर्न कोड को साफ़ रखता है और बाद में अधिक रीजन जोड़ना आसान बनाता है।

---

## निष्कर्ष

हमने अभी-अभी Python OCR का उपयोग करके **इमेज से टेक्स्ट निकालने** की पूरी एंड‑टू‑एंड वर्कफ़्लो को कवर किया, विशेष रीजन पर फोकस करते हुए। **OCR के लिए इमेज लोड** करके, **ROI** परिभाषित करके, और इंजन को कॉल करके आप भरोसेमंद रूप से **रीजन से टेक्स्ट पढ़ सकते** हैं—इनवॉइस से टोटल निकालने, रसीद से डेट निकालने, या किसी भी लोकलाइज़्ड डेटा के लिए परफेक्ट।

बिना झिझक प्रयोग करें

## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Aspose OCR के साथ इमेज से टेक्स्ट निकालें – स्टेप‑बाय‑स्टेप गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [इमेज से टेक्स्ट निकालें – .NET के लिए Aspose.OCR के साथ OCR ऑप्टिमाइज़ेशन](/ocr/english/net/ocr-optimization/)
- [OCR में रेक्टेंगल तैयार करके इमेज से टेक्स्ट निकालने का तरीका](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}