---
category: general
date: 2026-05-31
description: Python के साथ OCR की सटीकता को सुधारें, OCR के लिए छवियों की पूर्व-प्रसंस्करण
  करके। जानें कि इमेज फ़ाइलों से टेक्स्ट कैसे निकालें, PNG से टेक्स्ट कैसे पहचानें,
  और परिणामों को कैसे बढ़ाएँ।
draft: false
keywords:
- improve OCR accuracy
- preprocess image for OCR
- extract text from image
- recognize text from PNG
- image preprocessing for text
language: hi
og_description: Python में इमेज प्रीप्रोसेसिंग लागू करके OCR की सटीकता बढ़ाएँ। इस
  गाइड का पालन करके इमेज फ़ाइलों से टेक्स्ट निकालें और PNG से टेक्स्ट को आसानी से
  पहचानें।
og_title: Python में OCR की सटीकता सुधारें – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  headline: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  name: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Loads the PNG into memory
    text: Loads the PNG into memory
  - name: Applies denoise and deskew based on our settings
    text: Applies denoise and deskew based on our settings
  - name: Runs the neural‑network or classic pattern matcher
    text: Runs the neural‑network or classic pattern matcher
  - name: Packages the output into `recognition_result`
    text: Packages the output into `recognition_result`
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python में OCR की सटीकता बढ़ाएँ – पूर्ण चरण‑दर‑चरण मार्गदर्शिका
url: /hi/python-java/general/improve-ocr-accuracy-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में OCR सटीकता सुधारें – पूर्ण चरण‑दर‑चरण गाइड

क्या आपने कभी **OCR सटीकता सुधारने** की कोशिश की है और फिर भी गड़बड़ आउटपुट मिला है? आप अकेले नहीं हैं। अधिकांश डेवलपर्स को तब समस्या आती है जब मूल छवि शोरयुक्त, तिरछी, या बस कम‑कॉन्ट्रास्ट वाली होती है। अच्छी खबर? कुछ प्री‑प्रोसेसिंग ट्रिक्स धुंधली स्क्रीनशॉट को साफ, मशीन‑पढ़ने योग्य टेक्स्ट में बदल सकती हैं।

इस ट्यूटोरियल में हम एक वास्तविक उदाहरण के माध्यम से चलते हैं जो **OCR के लिए इमेज को प्री‑प्रोसेस** करता है, पहचान इंजन चलाता है, और अंत में **इमेज फ़ाइलों से टेक्स्ट निकालता** है—विशेष रूप से एक PNG। अंत तक आप ठीक‑ठीक जान पाएँगे कि **PNG से टेक्स्ट कैसे पहचानें** उच्च सफलता दर के साथ, और आपके पास एक पुन: उपयोग योग्य कोड स्निपेट होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं।

## आप क्या सीखेंगे

- OCR इंजन के लिए इमेज प्री‑प्रोसेसिंग क्यों महत्वपूर्ण है  
- कौन से प्री‑प्रोसेसिंग मोड (डेनॉइज़, डेस्क्यू) सबसे बड़ा सुधार देते हैं  
- Python में `OcrEngine` इंस्टेंस को कैसे कॉन्फ़िगर करें  
- पूरा, चलाने योग्य स्क्रिप्ट जो **इमेज फ़ाइलों से टेक्स्ट निकालता** है  
- घुमाए गए स्कैन या कम‑रिज़ॉल्यूशन तस्वीरों जैसे एज केस को संभालने के टिप्स  

कोई बाहरी लाइब्रेरी OCR SDK के अलावा आवश्यक नहीं है, लेकिन आपको Python 3.8+ और एक PNG इमेज चाहिए जिसे आप पढ़ना चाहते हैं।

---

![Python में OCR सटीकता सुधारने के चरण दर्शाने वाला आरेख](image.png "OCR सटीकता सुधार कार्यप्रवाह")

*Alt text: Python में OCR सटीकता सुधारने के चरण दर्शाने वाला आरेख, जिसमें प्री‑प्रोसेसिंग और पहचान चरण दिखाए गए हैं।*

## आवश्यकताएँ

- Python 3.8 या उससे नया स्थापित  
- `OcrEngine`, `OcrEngineSettings`, और `ImagePreprocessMode` प्रदान करने वाले OCR SDK तक पहुंच (नीचे दिया गया कोड एक सामान्य API का उपयोग करता है; आवश्यकता पड़ने पर अपने विक्रेता की क्लासेज़ से बदलें)  
- एक PNG इमेज (`input.png`) जिसे आप किसी फ़ोल्डर में रख सकते हैं  

यदि आप वर्चुअल एनवायरनमेंट का उपयोग कर रहे हैं, तो अभी इसे सक्रिय करें—कोई जटिल चीज़ नहीं, बस `python -m venv venv && source venv/bin/activate`।

---

## चरण 1: OCR इंजन इंस्टेंस बनाएं – OCR सटीकता सुधारना शुरू करें

पहली चीज़ जो आपको चाहिए वह है OCR इंजन ऑब्जेक्ट। इसे ऐसे सोचें जैसे वह दिमाग जो बाद में पिक्सेल पढ़ेगा और अक्षर निकालेगा।

```python
# Step 1: Initialise the OCR engine
ocr_engine = OcrEngine()
```

क्यों यह महत्वपूर्ण है: बिना इंजन के आप कोई भी प्री‑प्रोसेसिंग नहीं लगा सकते, और कच्ची इमेज सीधे recogniser को फीड हो जाएगी—आमतौर पर सटीकता के लिए सबसे बुरा परिदृश्य।

---

## चरण 2: लक्ष्य PNG लोड करें – PNG से टेक्स्ट पहचानने के लिए मंच तैयार करें

अब हम इंजन को बताते हैं कि किस फ़ाइल पर काम करना है। PNG lossless है, जो JPEG की तुलना में हमें थोड़ा फायदा देता है।

```python
# Step 2: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/input.png")
```

यदि इमेज कहीं और स्थित है, तो बस पाथ समायोजित करें। इंजन किसी भी समर्थित फ़ॉर्मेट को स्वीकार करता है, लेकिन PNG अक्सर तीखे अक्षर किनारों के लिए आवश्यक बारीक विवरण संरक्षित रखता है।

---

## चरण 3: प्री‑प्रोसेसिंग कॉन्फ़िगर करें – OCR के लिए इमेज प्री‑प्रोसेस करें

यहाँ जादू होता है। हम एक सेटिंग्स ऑब्जेक्ट बनाते हैं, डेनॉइज़िंग को सक्षम करते हैं ताकि धब्बे हट जाएँ, और डेस्क्यू को चालू करते हैं ताकि झुके हुए टेक्स्ट को स्वतः सीधा किया जा सके।

```python
# Step 3: Prepare preprocessing settings to improve accuracy
preprocess_settings = OcrEngineSettings()
preprocess_settings.preprocess_mode = (
    ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
)
```

### डेनॉइज़ + डेस्क्यू क्यों?

- **Denoise**: रैंडम पिक्सेल शोर पैटर्न‑मैचिंग एल्गोरिदम को भ्रमित करता है। इसे हटाने से अक्षर तेज़ हो जाते हैं।  
- **Deskew**: केवल 2‑डिग्री का झुकाव भी confidence स्कोर को काफी घटा सकता है। डेस्क्यू बेसलाइन को संरेखित करता है, जिससे recogniser फ़ॉन्ट को अधिक विश्वसनीय रूप से मिलाता है।  

यदि आपकी इमेज विशेष रूप से डार्क है, तो अतिरिक्त फ़्लैग (जैसे `ImagePreprocessMode.CONTRAST_ENHANCE`) के साथ प्रयोग कर सकते हैं। SDK दस्तावेज़ आमतौर पर सभी उपलब्ध मोड सूचीबद्ध करता है।

---

## चरण 4: सेटिंग्स को इंजन पर लागू करें – प्री‑प्रोसेसिंग को OCR से जोड़ें

सेटिंग्स ऑब्जेक्ट को इंजन को असाइन करें ताकि अगली पहचान रन में हमने परिभाषित ट्रांसफ़ॉर्मेशन उपयोग हों।

```python
# Step 4: Apply the settings to the engine
ocr_engine.settings = preprocess_settings
```

यदि आप इस चरण को छोड़ देते हैं, तो इंजन अपने डिफ़ॉल्ट (अक्सर “कोई प्री‑प्रोसेसिंग नहीं”) पर वापस आ जाएगा, और आप **निचली OCR सटीकता** देखेंगे।

---

## चरण 5: पहचान प्रक्रिया चलाएँ – इमेज से टेक्स्ट निकालें

सब कुछ कनेक्ट हो जाने के बाद, हम अंततः इंजन को उसका काम करने के लिए कहते हैं। कॉल सिंक्रोनस है, जो एक result ऑब्जेक्ट लौटाता है जिसमें पहचाना गया स्ट्रिंग होता है।

```python
# Step 5: Run the recognition process
recognition_result = ocr_engine.recognize()
```

पर्दे के पीछे इंजन अब:

1. PNG को मेमोरी में लोड करता है  
2. हमारी सेटिंग्स के आधार पर डेनॉइज़ और डेस्क्यू लागू करता है  
3. न्यूरल‑नेटवर्क या क्लासिक पैटर्न मैचर चलाता है  
4. आउटपुट को `recognition_result` में पैकेज करता है  

---

## चरण 6: पहचाने गए टेक्स्ट को आउटपुट करें – सुधार की पुष्टि करें

आइए निकाले गए स्ट्रिंग को प्रिंट करें। वास्तविक एप्लिकेशन में आप इसे फ़ाइल, डेटाबेस में लिख सकते हैं, या किसी अन्य सर्विस को पास कर सकते हैं।

```python
# Step 6: Output the recognized text
print(recognition_result.text)
```

### अपेक्षित आउटपुट

यदि इमेज में वाक्य “Hello, OCR World!” है तो आपको यह दिखना चाहिए:

```
Hello, OCR World!
```

ध्यान दें कि टेक्स्ट साफ़ है—कोई अनचाहे प्रतीक या टूटे हुए अक्षर नहीं। यह **टेक्स्ट के लिए इमेज प्री‑प्रोसेसिंग** का सही परिणाम है।

---

## प्रो टिप्स और एज केस

| Situation | What to Adjust | Why |
|-----------|----------------|-----|
| बहुत कम‑रिज़ॉल्यूशन PNG (≤ 72 dpi) | यदि उपलब्ध हो तो `ImagePreprocessMode.SUPER_RESOLUTION` जोड़ें | अपसैंपलिंग recogniser को काम करने के लिए अधिक पिक्सेल दे सकता है |
| टेक्स्ट 5° से अधिक घुमाया हुआ है | डेस्क्यू टॉलरेंस बढ़ाएँ या इंजन को फीड करने से पहले `Pillow` से मैन्युअली घुमाएँ | अत्यधिक कोण कभी‑कभी ऑटोमैटिक डेस्क्यू को बायपास कर देते हैं |
| भारी बैकग्राउंड पैटर्न | `ImagePreprocessMode.BACKGROUND_REMOVAL` सक्षम करें | गैर‑टेक्स्ट अव्यवस्था को हटाता है जो अन्यथा गलत पढ़ी जा सकती थी |
| बहु‑भाषा दस्तावेज़ | `ocr_engine.language = "eng+spa"` (या समान) सेट करें | इंजन सही कैरेक्टर सेट चुनता है, जिससे कुल सटीकता बढ़ती है |

याद रखें, **OCR सटीकता सुधारना** एक‑साइज़‑फिट‑ऑल नहीं है; आपको अपने विशेष डेटासेट के लिए प्री‑प्रोसेसिंग फ़्लैग्स पर पुनरावृति करनी पड़ सकती है।

---

## पूर्ण स्क्रिप्ट – कॉपी और पेस्ट करने के लिए तैयार

नीचे वह पूरा, चलाने योग्य उदाहरण है जिसमें हमने चर्चा किए सभी चरण शामिल हैं। इसे `improve_ocr_accuracy.py` के रूप में सहेजें और `python improve_ocr_accuracy.py` से चलाएँ।

```python
"""
Improve OCR Accuracy in Python – Full Example
Author: Your Name (2026)
Requires: OCR SDK providing OcrEngine, OcrEngineSettings, ImagePreprocessMode
"""

# Import the necessary classes from the OCR SDK
from ocr_sdk import OcrEngine, OcrEngineSettings, ImagePreprocessMode

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the PNG you want to read
    image_path = "YOUR_DIRECTORY/input.png"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure preprocessing: denoise + deskew
    preprocess_settings = OcrEngineSettings()
    preprocess_settings.preprocess_mode = (
        ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
    )

    # 4️⃣ Apply the settings
    ocr_engine.settings = preprocess_settings

    # 5️⃣ Run recognition
    recognition_result = ocr_engine.recognize()

    # 6️⃣ Print the extracted text
    print("=== Recognized Text ===")
    print(recognition_result.text)

if __name__ == "__main__":
    main()
```

इसे चलाएँ, कंसोल देखें, और आप तुरंत **इमेज से टेक्स्ट निकालें** परिणाम देखेंगे। यदि आउटपुट सही नहीं लगता, तो “प्रो टिप्स” तालिका में वर्णित अनुसार `preprocess_mode` फ़्लैग्स को ट्यून करें।

---

## निष्कर्ष

हमने Python का उपयोग करके **OCR सटीकता सुधारने** की एक व्यावहारिक विधि देखी। `OcrEngine` बनाकर, PNG लोड करके, **OCR के लिए इमेज को प्री‑प्रोसेस** करके, और अंत में **PNG से टेक्स्ट पहचान** करके, आप स्रोत चाहे जितना भी अधूरा हो, **इमेज फ़ाइलों से टेक्स्ट निकाल** सकते हैं।  

अगले कदम? इमेज की एक बैच को लूप में फीड करें, प्रत्येक परिणाम को CSV में सहेजें, या कॉन्ट्रास्ट एन्हांसमेंट जैसे अतिरिक्त प्री‑प्रोसेसिंग मोड्स के साथ प्रयोग करें। वही पैटर्न PDFs, स्कैन किए हुए रसीदों, या हाथ से लिखे नोट्स के लिए भी काम करता है—सिर्फ इनपुट बदलें और सेटिंग्स समायोजित करें।  

क्या आपके पास किसी विशेष इमेज प्रकार के बारे में प्रश्न हैं या इसे वेब सर्विस में इंटीग्रेट करने का तरीका जानना चाहते हैं? कमेंट छोड़ें, और हम उन पर साथ में चर्चा करेंगे। Happy coding, और आपकी OCR परिणाम हमेशा क्रिस्टल‑क्लियर रहें!

## आगे आप क्या सीखें?

- [Aspose OCR के साथ इमेज से टेक्स्ट निकालें – चरण‑दर‑चरण गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [इमेज से टेक्स्ट निकालें – Aspose.OCR for .NET के साथ OCR ऑप्टिमाइज़ेशन](/ocr/english/net/ocr-optimization/)
- [OCR में रेक्टेंगल तैयार करके इमेज से टेक्स्ट कैसे निकालें](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}