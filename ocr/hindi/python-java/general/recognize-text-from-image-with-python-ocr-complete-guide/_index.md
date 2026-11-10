---
category: general
date: 2026-06-16
description: Python OCR इंजन का उपयोग करके छवि से टेक्स्ट पहचानें – रसीद से टेक्स्ट
  निकालना सीखें और मिनटों में OCR की सटीकता सुधारें।
draft: false
keywords:
- recognize text from image
- extract text from receipt
- improve ocr accuracy
- python ocr tutorial
- image preprocessing for OCR
language: hi
og_description: छवि से जल्दी टेक्स्ट पहचानें। यह गाइड दिखाता है कि रसीद से टेक्स्ट
  कैसे निकालें और पाइथन का उपयोग करके OCR की सटीकता कैसे सुधारें।
og_title: Python OCR के साथ छवि से पाठ पहचानें – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  headline: recognize text from image with Python OCR – Complete Guide
  type: TechArticle
- description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  name: recognize text from image with Python OCR – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - A sample receipt image (JPEG or PNG) that you want to
      process. - The `ocr` package (the example uses a fictional `ocr` module for
      illustration; replace it with `pytesseract`, `easyocr`, or any library t'
  - name: Expected Output
    text: 'Running the script on a typical grocery receipt yields something like:'
  - name: H3 – Crop to the Receipt Region
    text: 'If your image contains a lot of background (e.g., a photo of a desk), crop
      it first:'
  - name: H3 – Use a Custom Language Pack
    text: 'For receipts that contain foreign characters (e.g., “€” or “¥”), load the
      appropriate language data:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python OCR के साथ छवि से पाठ को पहचानें – पूर्ण गाइड
url: /hi/python-java/general/recognize-text-from-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज से टेक्स्ट पहचानें Python OCR – पूर्ण गाइड

क्या आपको कभी **इमेज से टेक्स्ट पहचानने** की ज़रूरत पड़ी है लेकिन परिणाम बकवास जैसा दिखे? आप अकेले नहीं हैं। कई छोटे‑व्यवसाय परिदृश्यों में—जैसे रसीदें स्कैन करना, इनवॉइस को डिजिटल बनाना, या आईडी कार्ड से डेटा निकालना—साफ़, विश्वसनीय आउटपुट प्राप्त करना सुगम कार्यप्रवाह और सिरदर्द के बीच का अंतर है।

इस ट्यूटोरियल में हम एक हल्के Python OCR लाइब्रेरी का उपयोग करके **इमेज से टेक्स्ट पहचानने** का व्यावहारिक तरीका दिखाएंगे। हम यह भी बताएंगे कि **रसीद से टेक्स्ट निकालें** फ़ाइलों से कैसे निकालें और महंगे सॉफ़्टवेयर खरीदे बिना **OCR सटीकता सुधारने** के ट्रिक्स साझा करेंगे। तैयार हैं? चलिए शुरू करते हैं।

## आप क्या बनाएँगे

1. एक OCR इंजन को इंस्टैंशिएट करता है।  
2. स्मार्ट प्री‑प्रोसेसिंग (डेस्क्यू, डेस्पेकल, बाइनरीज़ेशन) सक्षम करता है।  
3. एक शोरयुक्त रसीद इमेज लोड करता है।  
4. पहचान पाइपलाइन को स्वचालित रूप से चलाता है।  
5. कंसोल में साफ़, खोजने योग्य टेक्स्ट प्रिंट करता है।

कोई बाहरी सेवाएँ नहीं, कोई छिपी API कुंजियाँ नहीं—सिर्फ शुद्ध Python कोड जिसे आप किसी भी प्रोजेक्ट में अनुकूलित कर सकते हैं।

### आवश्यकताएँ

- आपके मशीन पर Python 3.8+ स्थापित हो।  
- pip और वर्चुअल एनवायरनमेंट्स की बुनियादी जानकारी।  
- एक नमूना रसीद इमेज (JPEG या PNG) जिसे आप प्रोसेस करना चाहते हैं।  
- `ocr` पैकेज (उदाहरण में एक काल्पनिक `ocr` मॉड्यूल का उपयोग किया गया है; इसे `pytesseract`, `easyocr`, या किसी भी लाइब्रेरी से बदलें जो समान API प्रदान करती है)।

> **Pro tip:** यदि आपको डिपेंडेंसीज़ गायब मिलें, तो आगे बढ़ने से पहले `pip install ocr` (या वास्तविक पैकेज नाम) के साथ उन्हें इंस्टॉल करें।

## चरण 1 – इमेज से टेक्स्ट पहचानें: इंजन सेट अप करें

सबसे पहले हमें एक ऐसा ऑब्जेक्ट चाहिए जो पिक्सेल डेटा पढ़े और उसे अक्षरों में बदल सके। इंजन को ऑपरेशन का दिमाग समझें; बाकी सब उसे जानकारी देता है।

```python
import ocr  # Replace with your actual OCR library import

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

इंजन को मैन्युअली क्यों बनाते हैं? कुछ लाइब्रेरी आपको एक ही फ़ंक्शन कॉल करने देती हैं, लेकिन एक स्पष्ट इंस्टेंस आपको प्री‑प्रोसेसिंग पर सूक्ष्म नियंत्रण देता है—बिल्कुल वही जो बाद में **OCR सटीकता सुधारने** के लिए हमें चाहिए।

## चरण 2 – रसीद से टेक्स्ट निकालें: प्री‑प्रोसेसिंग सक्षम करें

फ़ोन कैमरे से स्कैन की गई रसीद अक्सर परिपूर्ण नहीं होती। यह थोड़ा टिल्टेड हो सकती है, धूल के धब्बों से भरी हो सकती है, या असमान रोशनी से ग्रस्त हो सकती है। प्री‑प्रोसेसिंग को सक्षम करने से इंजन को अक्षर देखे से पहले ही भारी काम हो जाता है।

```python
# Step 2: Enable preprocessing to improve recognition quality
preprocess = engine.preprocessing
preprocess.deskew = True        # Auto‑rotate slightly tilted pages
preprocess.despeckle = True     # Remove isolated noise pixels
preprocess.binarization = True  # Convert image to pure black‑white
```

*Deskew* पेज को सीधा करता है, *despeckle* बिखरे धब्बों को मिटाता है, और *binarization* हर पिक्सेल को या तो काला या सफ़ेद बनाता है। ये तीन फ़्लैग अकेले शोरयुक्त रसीदों पर **OCR सटीकता को 20‑30 %** तक सुधार सकते हैं।

## चरण 3 – वह इमेज लोड करें जिसे आप पहचानना चाहते हैं

अब हम इंजन को वास्तविक फ़ाइल की ओर इंगित करते हैं। पाथ एब्सोल्यूट या रिलेटिव हो सकता है; बस सुनिश्चित करें कि इमेज मौजूद है।

```python
# Step 3: Load the scanned receipt image
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")
```

यदि आप सोच रहे हैं कि इंजन PDFs या मल्टी‑पेज TIFFs को सपोर्ट करता है या नहीं, तो अधिकांश आधुनिक लाइब्रेरी करती हैं—डॉक्यूमेंटेशन देखें। एक सिंगल‑पेज JPEG के लिए ऊपर की लाइन ही पर्याप्त है।

## चरण 4 – OCR चलाएँ – इंजन बाकी सब करता है

प्री‑प्रोसेसिंग कॉन्फ़िगर हो गई और इमेज लोड हो गई, अगला कॉल सब कुछ करता है: यह प्री‑प्रोसेस करता है, पहचान एल्गोरिद्म चलाता है, और एक रिज़ल्ट ऑब्जेक्ट लौटाता है।

```python
# Step 4: Run OCR – the configured preprocessing is applied automatically
ocr_result = engine.recognize()
```

पर्दे के पीछे इंजन Tesseract, एक न्यूरल नेटवर्क, या कोई प्रोप्राइटरी इंजन उपयोग कर रहा हो सकता है। आपको आंतरिक कार्यप्रणाली जानने की ज़रूरत नहीं; आपको सिर्फ़ एक साफ़ परिणाम मिलता है।

## चरण 5 – पहचाने गए टेक्स्ट को आउटपुट करें

अंत में हम रिज़ल्ट से प्लेन‑टेक्स्ट निकालते हैं और उसे प्रिंट करते हैं। वास्तविक एप्लिकेशन में आप इसे डेटाबेस, CSV फ़ाइल, या यहाँ तक कि डाउनस्ट्रीम एनालिटिक्स पाइपलाइन में भी भेज सकते हैं।

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### अपेक्षित आउटपुट

एक सामान्य ग्रॉसरी रसीद पर स्क्रिप्ट चलाने से कुछ इस तरह का परिणाम मिलता है:

```
WALMART STORE #1234
123 Main St.
Anytown, USA

Date: 06/15/2026   Time: 14:32
Cashier: J. Doe

Item                Qty   Price
---------------------------------
Milk                1     2.99
Bread               2     5.48
Eggs                1     3.20
---------------------------------
Subtotal                    11.67
Tax                         0.93
Total                       12.60
```

यदि आउटपुट गड़बड़ दिखे, तो दोबारा जांचें कि प्री‑प्रोसेसिंग फ़्लैग ऑन हैं और इमेज बहुत डार्क नहीं है। बाइनरीज़ेशन थ्रेशहोल्ड को ट्यून करना (कुछ लाइब्रेरी आपको कस्टम वैल्यू सेट करने देती हैं) **OCR सटीकता को और भी सुधार सकता** है।

## उन्नत: रसीद से टेक्स्ट तेज़ी से निकालने के लिए फाइन‑ट्यूनिंग

जब आप रात में सैकड़ों रसीदें प्रोसेस कर रहे हों, तो आप गति बढ़ाना चाह सकते हैं। यहाँ दो वैकल्पिक ट्यूनिंग हैं:

### H3 – रसीद क्षेत्र को क्रॉप करें

यदि आपकी इमेज में बहुत बैकग्राउंड है (जैसे डेस्क की फोटो), तो पहले उसे क्रॉप करें:

```python
engine.image = engine.image.crop((50, 200, 800, 1200))  # left, top, right, bottom
```

### H3 – कस्टम लैंग्वेज पैक उपयोग करें

यदि रसीद में विदेशी अक्षर (जैसे “€” या “¥”) हों, तो उपयुक्त भाषा डेटा लोड करें:

```python
engine.set_language('eng+deu+fra')  # English, German, French
```

दोनों ट्रिक्स इंजन को **इमेज से टेक्स्ट पहचानने** में अधिक भरोसेमंद बनाते हैं, खासकर जब स्रोत सामग्री विविध हो।

## सामान्य समस्याएँ और उन्हें कैसे टालें

- **Missing Fonts:** कुछ OCR इंजन को विशेष रसीद फ़ॉन्ट्स के लिए फ़ॉन्ट फ़ाइलों की आवश्यकता होती है। उपयुक्त भाषा पैक इंस्टॉल करें।  
- **Too Much Noise:** `despeckle=True` के साथ भी, अत्यधिक ग्रेनी स्कैन इंजन को भ्रमित कर सकते हैं। Pillow में एक त्वरित मैनुअल फ़िल्टर (`Image.filter(ImageFilter.MedianFilter)`) मदद कर सकता है।  
- **Incorrect DPI:** OCR इंजन लगभग 300 dpi मानते हैं। यदि आपकी इमेज कम है, तो पहले उसका आकार बदलें: `engine.image = engine.image.resize((width*2, height*2))`।

इन मुद्दों को सीधे संबोधित करने से **OCR सटीकता** महंगे थर्ड‑पार्टी सर्विसेज़ के बिना सुधरती है।

## पूर्ण स्क्रिप्ट – चलाने के लिए तैयार

नीचे वह पूरा, चलाने योग्य Python प्रोग्राम है जिसमें हमने चर्चा किए सभी तत्व शामिल हैं। इसे `receipt_ocr.py` के रूप में सेव करें और `python receipt_ocr.py` चलाएँ।

```python
import ocr  # Replace with the actual library you use

def main():
    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Enable preprocessing steps
    preprocess = engine.preprocessing
    preprocess.deskew = True
    preprocess.despeckle = True
    preprocess.binarization = True

    # Load the receipt image (change the path to your file)
    engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")

    # Optional: crop out unnecessary background
    # engine.image = engine.image.crop((50, 200, 800, 1200))

    # Run the recognition pipeline
    result = engine.recognize()

    # Print the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

इस स्क्रिप्ट को चलाने से **इमेज से टेक्स्ट पहचानें** और रसीद डेटा का एक सुगठित ब्लॉक प्रिंट होगा। अपने रसीद लेआउट के अनुसार क्रॉपिंग कोऑर्डिनेट्स, भाषा सेटिंग्स, या प्री‑प्रोसेसिंग फ़्लैग को अनुकूलित करने में संकोच न करें।

## निष्कर्ष

हमने अभी-अभी Python का उपयोग करके **इमेज से टेक्स्ट पहचानने** का सीधा तरीका कवर किया, दिखाया कि **रसीद से टेक्स्ट निकालें** फ़ाइलों से कैसे निकालें, और कई व्यावहारिक टिप्स के साथ **OCR सटीकता सुधारने** के उपाय बताए। मुख्य विचार सरल है: एक OCR इंजन सेट अप करें, स्मार्ट प्री‑प्रोसेसिंग सक्षम करें, उसे एक साफ़ इमेज दें, और लाइब्रेरी को भारी काम करने दें।

अगले कदम? रसीदों की एक बैच को लूप में फीड करें, प्रत्येक परिणाम को CSV में स्टोर करें, या आउटपुट को बही‑खाता सिस्टम में जोड़ें। आप `easyocr` जैसे डीप‑लर्निंग आधारित OCR लाइब्रेरीज़ के साथ भी प्रयोग कर सकते हैं ताकि जटिल फ़ॉन्ट्स पर और भी उच्च सटीकता मिल सके।

किसी विशेष रसीद फ़ॉर्मेट के बारे में सवाल हैं या मल्टी‑पेज PDFs को कैसे हैंडल करें देखना चाहते हैं? नीचे कमेंट करें, और हैप्पी कोडिंग!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Aspose OCR के साथ इमेज से टेक्स्ट निकालें – चरण‑दर‑चरण गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [OCR में आयतें तैयार करके इमेज से टेक्स्ट कैसे निकालें](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [इमेज से टेक्स्ट निकालें – .NET के लिए Aspose.OCR के साथ OCR ऑप्टिमाइज़ेशन](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}