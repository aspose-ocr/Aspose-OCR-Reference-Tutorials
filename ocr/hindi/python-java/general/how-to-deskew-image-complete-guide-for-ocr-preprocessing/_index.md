---
category: general
date: 2026-07-05
description: इमेज को जल्दी से डेस्क्यू कैसे करें। OCR के लिए इमेज को प्रीप्रोसेस करना
  सीखें, इमेज की रोटेशन को सही करें, और Python के साथ स्कैन को टेक्स्ट में बदलें।
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: hi
og_description: इमेज को डेस्क्यू करने और OCR के लिए इमेज को प्रीप्रोसेस करने का तरीका।
  यह गाइड दिखाता है कि इमेज की रोटेशन को कैसे ठीक किया जाए और पाइथन का उपयोग करके
  इमेज से टेक्स्ट कैसे निकाला जाए।
og_title: छवि को डेस्क्यू कैसे करें – चरण-दर-चरण OCR प्रीप्रोसेसिंग
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: इमेज को डेस्क्यू कैसे करें – OCR प्रीप्रोसेसिंग के लिए संपूर्ण मार्गदर्शिका
url: /hi/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज को डेस्क्यू कैसे करें – OCR प्रीप्रोसेसिंग के लिए पूर्ण गाइड

क्या आपने कभी सोचा है कि **how to deskew image** फ़ाइलें जो एक टेढ़े स्कैनर से ली गई लगती हैं, उन्हें कैसे ठीक किया जाए? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में वह पहला काम जो आपको **extract text from image** करने से पहले करना पड़ता है, वह है उस झुकाव को सीधा करना।  

इस ट्यूटोरियल में हम एक व्यावहारिक, अंत‑से‑अंत उदाहरण के माध्यम से चलेंगे जो **preprocesses image for OCR** करता है, घुमाव को ठीक करता है, और अंत में एक Python OCR लाइब्रेरी का उपयोग करके **converts scan to text** करता है। कोई अस्पष्ट संदर्भ नहीं, बस एक कार्यशील स्क्रिप्ट जिसे आप कॉपी‑पेस्ट कर सकते हैं, साथ ही सामान्य समस्याओं के टिप्स।  

## आप क्या हासिल करेंगे

* किसी भी स्कैन किए गए JPEG या PNG को लोड करें जो थोड़ा झुका हुआ हो।  
* OCR की सटीकता बढ़ाने के लिए एक deskew फ़िल्टर और एक बाइनराइज़ेशन स्टेप लागू करें।  
* OCR इंजन चलाएँ और **extract text from image** विश्वसनीय रूप से प्राप्त करें।  
* समझें कि **correct image rotation** नीचे की प्रक्रिया में टेक्स्ट एक्सट्रैक्शन के लिए क्यों महत्वपूर्ण है।  

### पूर्वापेक्षाएँ

* आपके मशीन पर Python 3.9+ स्थापित हो।  
* `ocr` नेमस्पेस को अनुकरण करने वाला एक pip‑installable OCR पैकेज (उदाहरण के लिए, Tesseract के चारों ओर एक हल्का रैपर) स्थापित करें।  
* Python फ़ंक्शन्स और इमेज प्रोसेसिंग अवधारणाओं की बुनियादी समझ रखें।  

यदि आपके पास ये हैं, तो चलिए आगे बढ़ते हैं।

![how to deskew image example](deskew_before_after.png){alt="how to deskew image – सुधार से पहले और बाद"}

## चरण 1: OCR इंजन सेट अप करें – Python का उपयोग करके इमेज को डेस्क्यू कैसे करें

सबसे पहले: आपको एक OCR इंजन चाहिए जो आपके दस्तावेज़ की भाषा को समझ सके। नीचे दिया गया स्निपेट न्यूनतम बायलरप्लेट दिखाता है जिससे इंजन बनाया जा सके और उसे बताया जा सके कि आप English टेक्स्ट के साथ काम कर रहे हैं।

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Why this matters:*  इंजन की भाषा सेटिंग उस द्वारा उपयोग किए जाने वाले कैरेक्टर सेट और डिक्शनरी को प्रभावित करती है। इस स्टेप को छोड़ने से OCR सामान्य शब्दों को गलत समझ सकता है, विशेषकर जब आप **correct image rotation** करते हैं।

## चरण 2: स्कैन की गई इमेज लोड करें जिसे आप सीधा करना चाहते हैं

अब हम फ़ाइल को मेमोरी में लाते हैं। `"YOUR_DIRECTORY/skewed_scan.jpg"` को अपनी इमेज के पाथ से बदलें।

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

यदि इमेज पहले से ही एक NumPy एरे या OpenCV `Mat` में है, तो आप लोडर को उसी अनुसार अनुकूलित कर सकते हैं – मुख्य बात यह है कि ऑब्जेक्ट को बाद में उपयोग किए जाने वाले `apply_filter` मेथड को एक्सपोज़ करना चाहिए।

## चरण 3: OCR के लिए इमेज को प्रीप्रोसेस करें – Deskew और Binarize

यहीं पर जादू होता है। हम दो फ़िल्टर को क्रम में लगाते हैं:

1. **Deskew** – स्वचालित रूप से प्रमुख टेक्स्ट बेसलाइन का पता लगाता है और इमेज को क्षैतिज में वापस घुमाता है।  
2. **Binarize (Otsu)** – चित्र को शुद्ध काली‑और‑सफ़ेद में बदलता है, जो पहचान दर को काफी बढ़ाता है।  

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Pro tip:*  यदि बाइनराइज़ेशन के बाद भी टेक्स्ट धुंधला दिखता है, तो कंट्रास्ट को समायोजित करने या किसी अलग थ्रेशहोल्डिंग मेथड का उपयोग करने की कोशिश करें। `ocr.Filter` मॉड्यूल अक्सर कठिन मामलों के लिए `adaptive_threshold()` शामिल करता है।

## चरण 4: OCR चलाएँ – इमेज से टेक्स्ट निकालें

एक साफ़, सीधा किया हुआ कैनवास होने पर, हम इमेज को इंजन को देते हैं। परिणाम ऑब्जेक्ट में पहचाना गया स्ट्रिंग, कॉन्फिडेंस स्कोर, और यदि बाद में आवश्यकता हो तो बाउंडिंग बॉक्स भी होते हैं।

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

सामान्य आउटपुट इस प्रकार दिखता है:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

ध्यान दें कि लाइन ब्रेक्स पूरी तरह से संरेखित हैं? यही **correct image rotation** का लाभ है – OCR को अब लाइन की दिशा का अनुमान नहीं लगाना पड़ता।

## चरण 5: सब कुछ एक साथ रखें – स्कैन को टेक्स्ट में बदलने के लिए एक-फ़ाइल स्क्रिप्ट

नीचे पूरा, चलाने योग्य स्क्रिप्ट है जो हमने चर्चा किए सभी भागों को मिलाता है। इसे `deskew_ocr.py` के रूप में सेव करें और `python deskew_ocr.py` चलाएँ।

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### यह क्यों काम करता है

- **Deskew first** – बाइनराइज़ेशन से पहले इमेज को घुमाने से थ्रेशहोल्ड एल्गोरिद्म एक समतल क्षितिज पर काम करता है।  
- **Binarize after deskew** – Otsu की विधि द्विप्रहरी हिस्टोग्राम मानती है; एक झुकी हुई पेज इस मान्यता को बिगाड़ देगी।  
- **English language model** – OCR को बताता है कि कौन से कैरेक्टर की अपेक्षा करनी है, जिससे फॉल्स पॉज़िटिव कम होते हैं।  

यदि आपको अन्य भाषाओं को संभालना है, तो बस `ocr.Language.ENGLISH` को उपयुक्त enum से बदल दें।

## सामान्य प्रश्न और किनारे के केस

| Question | Answer |
|----------|--------|
| *यदि स्कैन उल्टा हो तो क्या करें?* | `deskew()` फ़िल्टर आमतौर पर 180° घुमाव को भी पहचान लेता है। यदि यह विफल हो, तो डेस्क्यू करने से पहले `apply_filter(ocr.Filter.rotate(180))` कॉल करें। |
| *मेरे दस्तावेज़ में रंगीन ग्राफ़िक्स हैं – क्या बाइनराइज़ेशन उन्हें मिटा देगा?* | हां। मिश्रित सामग्री के लिए, केवल `ocr.Filter.deskew()` का उपयोग करने पर विचार करें, फिर रंगीन इमेज पर OCR चलाएँ। आप ग्राफ़िक्स को संरक्षित रखते हुए अभी भी टेक्स्ट निकाल सकते हैं। |
| *क्या मैं फ़ाइलों की एक बैच प्रोसेस कर सकता हूँ?* | लॉजिक को एक लूप में रैप करें, सूची से प्रत्येक फ़ाइल पाथ पढ़ें, और प्रत्येक `result.text` को अलग `.txt` फ़ाइल में सहेजें। |
| *कम‑रिज़ॉल्यूशन स्कैन पर सटीकता कैसे बढ़ाएँ?* | डेस्क्यू करने से **पहले** बाइकोबिक फ़िल्टर से इमेज को अपस्केल करें, फिर शार्पनिंग फ़िल्टर लागू करें। अधिक पिक्सेल OCR इंजन को बेहतर संकेत देते हैं। |

## बोनस: डेस्क्यू का विज़ुअल वेरिफिकेशन

यदि आप पहले‑और‑बाद को साइड बाय साइड देखना चाहते हैं, तो एक तेज़ Matplotlib स्निपेट जोड़ें:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

## निष्कर्ष

हमने **how to deskew image** फ़ाइलों को कवर किया, क्यों **preprocess image for OCR** आवश्यक है, और कैसे **extract text from image** करके अंत में **convert scan to text** किया। कार्यप्रवाह—load → deskew → binarize → recognize—सुनिश्चित करता है कि OCR एक साफ़, सीधा पेज देखे, जिससे उच्च सटीकता और कम मैन्युअल सुधार होते हैं।

आपकी OCR यात्रा में आगे क्या है? इन चीज़ों के साथ प्रयोग करें:

- विभिन्न भाषा पैक्स (`ocr.Language.FRENCH`, आदि)।  
- कॉलम या टेबल का पता लगाने के लिए लेआउट एनालिसिस स्टेप जोड़ना।  
- PDF लाइब्रेरी का उपयोग करके OCR परिणामों को सर्चेबल PDFs में एक्सपोर्ट करना।  

यदि आपको कोई समस्या आती है तो टिप्पणी छोड़ने में संकोच न करें, या विशेष रूप से जिद्दी स्कैन को संभालने के लिए अपने स्वयं के बदलाव साझा करें। कोडिंग का आनंद लें, और आपकी इमेजेस हमेशा पूरी तरह लेवल रहें!

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करती हैं।

- [AspOCR का उपयोग कैसे करें: .NET के लिए इमेज OCR फ़िल्टर को प्रीप्रोसेस करें](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Aspose.OCR का उपयोग करके भाषा चयन के साथ C# में इमेज टेक्स्ट निकालें](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [इमेज को OCR कैसे करें – OCR इमेज रिकग्निशन में इमेज पर OCR करें](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}