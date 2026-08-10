---
category: general
date: 2026-05-31
description: OCR के रुचि क्षेत्र (ROI) का उपयोग करके OCR के लिए छवि लोड करना और आयत
  से टेक्स्ट निकालना सीखें, बिल पर राशि पहचानने के लिए एकदम उपयुक्त।
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: hi
og_description: OCR के लिए इमेज लोड करने हेतु ROI (रुचि का क्षेत्र) को मास्टर करें,
  आयत से टेक्स्ट निकालें और एक ही ट्यूटोरियल में इनवॉइस से टेक्स्ट पहचानें।
og_title: OCR रुचि क्षेत्र – चरण-दर-चरण पाइथन गाइड
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR रुचि क्षेत्र – पाइथन में आयत से टेक्स्ट निकालें
url: /hi/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Region of Interest – आयत से टेक्स्ट निकालें Python में

क्या आपने कभी सोचा है कि स्कैन किए गए इनवॉइस के किसी विशिष्ट भाग को **ocr region of interest** कैसे किया जाए बिना पूरी पेज को इंजन में फीड किए? आप पहले व्यक्ति नहीं हैं जो धुंधली रसीद को देखकर सोचते हैं, “निचले दाएँ कोने में मौजूद राशि को कैसे निकालूँ?” अच्छी खबर यह है कि आप OCR लाइब्रेरी को ठीक वही बता सकते हैं जहाँ देखना है, जिससे गति और सटीकता दोनों में काफी सुधार होता है।

इस गाइड में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे कि कैसे **load image for OCR** करें, **region of interest** को परिभाषित करें, और फिर **extract text from rectangle** करके अंत में **recognize text from invoice** करें और क्लासिक “how to extract amount” सवाल का उत्तर दें। कोई अस्पष्ट संदर्भ नहीं—सिर्फ ठोस कोड, स्पष्ट व्याख्याएँ, और कुछ प्रो टिप्स जो आप पहले जानना चाहते थे।

---

## What You’ll Build

## आप क्या बनाएँगे

1. डिस्क से इनवॉइस इमेज लोड करता है।  
2. एक आयताकार ROI को चिह्नित करता है जहाँ कुल राशि स्थित है।  
3. केवल उस ROI के भीतर OCR चलाता है।  
4. साफ़ किया गया राशि स्ट्रिंग प्रिंट करता है।  

---

## Prerequisites

## आवश्यकताएँ

- Python 3.8+ स्थापित हो (`python --version` कमांड ≥3.8 दिखाना चाहिए)।  
- एक pip‑installable OCR पैकेज (उदा., `pip install simpleocr`)।  
- एक इनवॉइस इमेज (PNG या JPEG) जिसे आप किसी फ़ोल्डर में रख सकते हैं।  
- Python फ़ंक्शन्स और क्लासेज़ की बुनियादी परिचितता (कुछ भी जटिल नहीं)।  

यदि आपके पास ये सब है, बढ़िया—आइए शुरू करें। यदि नहीं, पहले इमेज प्राप्त करें; बाकी कदम फ़ाइल की वास्तविक सामग्री से स्वतंत्र हैं।

---

## Step 1: Load Image for OCR

## चरण 1: OCR के लिए इमेज लोड करें

किसी भी OCR वर्कफ़्लो को सबसे पहले एक बिटमैप चाहिए जिससे पढ़ा जा सके। अधिकांश लाइब्रेरी एक सरल `load_image` मेथड प्रदान करती हैं जो फ़ाइल पाथ को स्वीकार करती है। यहाँ हमारे `SimpleOCR` इंजन के साथ यह कैसे किया जाता है:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** स्क्रिप्ट को अलग कार्य निर्देशिका से चलाते समय “file not found” जैसी आश्चर्यजनक त्रुटियों से बचने के लिए absolute paths या `os.path.join` का उपयोग करें।

---

## Step 2: Define OCR Region of Interest

## चरण 2: OCR Region of Interest परिभाषित करें

पूरे पेज को स्कैन करने के बजाय, हम इंजन को *बिल्कुल* बताते हैं कि राशि कहाँ स्थित है। यही **ocr region of interest** चरण है, और यह विश्वसनीय निष्कर्षण की कुंजी है, विशेषकर जब दस्तावेज़ में शोरयुक्त हेडर या फुटर हों।

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

इन संख्याओं का क्या मतलब है? `x` और `y` पिक्सेल ऑफ़सेट हैं जो शीर्ष‑बाएँ कोने से मापे जाते हैं, जबकि `width` और `height` बॉक्स का आकार दर्शाते हैं। यदि आप अनिश्चित हैं, तो इमेज को किसी भी एडिटर में खोलें, रूलर सक्षम करें, और निर्देशांक नोट करें। कई IDEs कर्सर की स्थिति को होवर करते समय भी दिखा सकते हैं।

---

## Step 3: Extract Text from Rectangle

## चरण 3: आयत से टेक्स्ट निकालें

अब ROI सेट हो गया है, हम इंजन से **recognize text from invoice** करने को कहते हैं लेकिन केवल उसी आयत तक सीमित जो हमने अभी जोड़ी है। यह कॉल एक रिज़ल्ट ऑब्जेक्ट लौटाता है जिसमें आमतौर पर कच्चा स्ट्रिंग, confidence स्कोर, और कभी‑कभी बाउंडिंग बॉक्स होते हैं।

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

पर्दे के पीछे, `recognize()` प्रत्येक ROI पर इटररेट करता है, उस स्लाइस को क्रॉप करता है, OCR मॉडल चलाता है, और परिणामों को जोड़ता है। इसलिए एक सटीक **extract text from rectangle** क्षेत्र परिभाषित करने से बैच जॉब्स के प्रोसेसिंग समय में सेकंड बच सकते हैं।

---

## Step 4: How to Extract Amount – Clean the Output

## चरण 4: राशि निकालें – आउटपुट साफ़ करें

OCR पूर्ण नहीं है; अक्सर आपको अतिरिक्त स्पेस, लाइन फ़ीड, या गलत‑पढ़े अक्षर (जैसे “S” बनाम “5”) मिलते हैं। एक तेज़ `strip()` और छोटा रेगेक्स आमतौर पर मौद्रिक मानों के लिए काम करता है।

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Why this matters:** यदि आप राशि को डेटाबेस या पेमेंट गेटवे में फीड करने की योजना बनाते हैं, तो आपको एक पूर्वानुमेय फ़ॉर्मेट चाहिए। व्हाइटस्पेस हटाने और गैर‑संख्यात्मक अक्षरों को फ़िल्टर करने से डाउनस्ट्रीम त्रुटियों से बचा जा सकता है।

---

## Step 5: Recognize Text from Invoice – Full Script

## चरण 5: इनवॉइस से टेक्स्ट पहचानें – पूर्ण स्क्रिप्ट

सब कुछ एक साथ मिलाकर, यहाँ पूर्ण, तैयार‑चलाने‑योग्य स्क्रिप्ट है। इसे `extract_amount.py` के रूप में सेव करें और `python extract_amount.py` चलाएँ।

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Expected Output

### अपेक्षित आउटपुट

```
Amount: 1,245.67
```

यदि ROI गलत संरेखित है, तो आप `Amount: 1245.6S` जैसा कुछ देख सकते हैं—ध्यान दें stray “S” को। आयत के निर्देशांक को समायोजित करें और आउटपुट साफ़ दिखने तक पुनः चलाएँ।

---

## Common Pitfalls & Edge Cases

## सामान्य कठिनाइयाँ और किनारे के मामले

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **ROI बहुत छोटा** | राशि का टेक्स्ट कट जाता है, जिससे आंशिक पहचान होती है। | `width`/`height` को लगभग 10‑20 % बढ़ाएँ और पुनः‑परीक्षण करें। |
| **गलत DPI** | कम‑रिज़ॉल्यूशन स्कैन (≤150 dpi) OCR की सटीकता घटाते हैं। | इमेज को लोड करने से पहले 300 dpi पर री‑सैंपल करें, या स्कैनर से उच्च DPI माँगें। |
| **एकाधिक मुद्राएँ** | रेगेक्स पहला संख्यात्मक समूह लेता है, जो इनवॉइस नंबर हो सकता है। | रेगेक्स को मुद्रा प्रतीकों (`$`, `€`, `£`) के सामने खोजने के लिए सुधारें। |
| **घुमाए हुए इनवॉइस** | OCR इंजन मानते हैं कि टेक्स्ट सीधा है; घुमे पेज पहचान बिगड़ते हैं। | ROI जोड़ने से पहले रोटेशन सुधार (`ocr_engine.rotate(90)`) लागू करें। |
| **पृष्ठभूमि में शोर** | छायाएँ या स्टैम्प मॉडल को भ्रमित करते हैं। | सरल थ्रेशोल्ड (`cv2.threshold`) या डिनॉइज़िंग फ़िल्टर से प्री‑प्रोसेस करें। |

## Pro Tips for Real‑World Projects

## वास्तविक‑दुनिया प्रोजेक्ट्स के लिए प्रो टिप्स

- **बैच प्रोसेसिंग:** इनवॉइस के फ़ोल्डर पर लूप करें, ROI को डायनामिक रूप से (जैसे टेम्पलेट डिटेक्शन के आधार पर) गणना करें, और परिणाम CSV में सहेजें।  
- **टेम्पलेट मिलान:** यदि आप कई इनवॉइस लेआउट संभालते हैं, तो `template_id → ROI coordinates` का JSON मानचित्र रखें। तेज़ लेआउट क्लासिफायर के आधार पर ROI बदलें।  
- **समांतर निष्पादन:** कई OCR इंस्टेंस को एक साथ चलाने के लिए `concurrent.futures.ThreadPoolExecutor` का उपयोग करें—उच्च‑वॉल्यूम बैक‑ऑफ़िस पाइपलाइन के लिए उत्कृष्ट।  
- **विश्वास फ़िल्टरिंग:** अधिकांश OCR परिणामों में एक confidence स्कोर होता है। थ्रेशोल्ड (जैसे 85 %) से नीचे के परिणामों को हटाएँ और मैन्युअल रिव्यू के लिए फ़्लैग करें।  

---

## Conclusion

## निष्कर्ष

हमने सब कुछ कवर किया है जो आपको **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, और अंत में **recognize text from invoice** करने के लिए चाहिए, ताकि क्लासिक **how to extract amount** सवाल का उत्तर मिल सके। स्क्रिप्ट कॉम्पैक्ट है, फिर भी विभिन्न दस्तावेज़ फ़ॉर्मेट, भाषाएँ, और OCR बैक‑एंड के साथ अनुकूलित की जा सकती है।

अब जब आपने बुनियादी बातों में महारत हासिल कर ली है, तो वर्कफ़्लो को विस्तारित करने पर विचार करें: बारकोड स्कैनिंग जोड़ें, PDF पार्सर के साथ एकीकृत करें, या निकाली गई राशि को अकाउंटिंग API में पुश करें। संभावनाएँ असीमित हैं, और एक अच्छी‑परिभाषित ROI के साथ आप हमेशा तेज़, साफ़ परिणाम पाएँगे।

यदि कोई समस्या आती है, तो नीचे टिप्पणी करें—हैप्पी OCRing!

![ocr region of interest example](https://example.com/ocr_roi_example.png "ocr region of interest example")

## What Should You Learn Next?

## आगे आप क्या सीखें?

- [OCR में आयतें तैयार करके इमेज से टेक्स्ट निकालना कैसे करें](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Aspose.OCR डिटेक्ट एरिया मोड के साथ जावा में इमेज से टेक्स्ट निकालें](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [इमेज से टेक्स्ट निकालें – .NET के लिए Aspose.OCR के साथ OCR ऑप्टिमाइज़ेशन](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}