---
category: general
date: 2026-06-16
description: OCR में रुचि के क्षेत्र (ROI) को परिभाषित करें ताकि आईडी कार्ड से स्पेनिश
  टेक्स्ट निकाला जा सके। जानें कि OCR के लिए इमेज कैसे लोड करें और ROI को प्रभावी
  ढंग से कैसे निर्दिष्ट करें।
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: hi
og_description: आईडी कार्ड से स्पेनिश टेक्स्ट निकालने के लिए OCR में रुचि के क्षेत्र
  को परिभाषित करें। छवियों को लोड करने और ROI निर्दिष्ट करने के चरण-दर-चरण मार्गदर्शक।
og_title: OCR में रुचि के क्षेत्र को परिभाषित करें – पूर्ण पायथन ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: OCR में रुचि के क्षेत्र को परिभाषित करें – पूर्ण पायथन ट्यूटोरियल
url: /hi/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR में रुचि का क्षेत्र निर्धारित करें – पूर्ण Python ट्यूटोरियल

क्या आपने कभी सोचा है कि **define region of interest in OCR** कैसे निर्धारित करें ताकि आप केवल उस भाग को पढ़ें जिसकी आपको वास्तव में जरूरत है? इस ट्यूटोरियल में हम आपको ठीक वही दिखाएंगे, साथ ही दिखाएंगे कि **load image for OCR** कैसे करें और कुछ ही Python लाइनों में एक ID कार्ड से स्पेनिश टेक्स्ट निकालें।  

यदि आप कभी शोरयुक्त स्कैन को देखते‑देखते सोचते रहे हैं, “नाम फ़ील्ड को निकालने का कोई साफ़ तरीका होना चाहिए,” तो आप सही जगह पर हैं। अंत तक आप बैकग्राउंड के अव्यवस्था से बचते हुए वह ID कार्ड टेक्स्ट निकाल पाएँगे जिसकी आपको ज़रूरत है।

## आप क्या सीखेंगे

- क्यों आपको OCR चलाने से पहले **define region of interest** करना चाहिए।  
- लोकप्रिय Python OCR रैपर का उपयोग करके **load image for OCR** करने के सटीक चरण।  
- पिक्सेल निर्देशांक के साथ **how to specify ROI** कैसे करें।  
- **extract id card text** को विश्वसनीय रूप से निकालने के तरीके, भले ही स्रोत भाषा स्पेनिश हो।  
- घुमाए हुए कार्ड या कम‑कॉन्ट्रास्ट स्कैन जैसे एज केस को संभालने के टिप्स।  

कोई पूर्व OCR विशेषज्ञता आवश्यक नहीं—बस एक कार्यशील Python 3 वातावरण और एक JPEG ID कार्ड की फ़ाइल चाहिए जिसे आप परीक्षण करना चाहते हैं।

---

![Define region of interest illustration](placeholder.png){alt="रुचि के क्षेत्र का उदाहरण, जिसमें ID कार्ड छवि पर हाइलाइटेड आयत दिखाया गया है"}

## चरण 1: OCR लाइब्रेरी स्थापित करें और इम्पोर्ट करें

सबसे पहले, आपको एक ऐसी लाइब्रेरी चाहिए जो आपके द्वारा देखे गए स्निपेट जैसा `OcrEngine` क्लास प्रदान करे। इस गाइड में हम काल्पनिक `ocr` पैकेज का उपयोग करेंगे, लेकिन वही अवधारणाएँ `pytesseract`, `easyocr`, या किसी भी रैपर पर लागू होती हैं जो आपको भाषा और ROI सेट करने देती हैं।

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Pro tip:* यदि आप `pytesseract` उपयोग कर रहे हैं, तो `Rectangle` क्लास एक साधा ट्यूपल `(left, top, width, height)` बन जाता है। बाकी प्रवाह समान रहता है।

## चरण 2: OCR के लिए इमेज लोड करें

अब हम **load image for OCR** करेंगे। इंजन को एक `ocr.Image` ऑब्जेक्ट चाहिए, इसलिए हम इसे उस फ़ाइल की ओर इंगित करते हैं जिसमें ID कार्ड है। पथ को पूर्ण या स्क्रिप्ट की कार्यशील डायरेक्टरी के सापेक्ष रखें।

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

यदि इमेज बहुत बड़ी है, तो पहले उसका आकार बदलने पर विचार करें; OCR इंजन 1500 px से कम चौड़ाई वाली इमेज पर तेज़ काम करता है।

## चरण 3: ROI कैसे निर्दिष्ट करें (Define Region of Interest)

यह ट्यूटोरियल का मुख्य भाग है: **how to specify ROI**। ROI बस एक आयत है जो OCR इंजन को बताती है, “केवल इन पिक्सेल सीमाओं के भीतर देखो।” इसे ID कार्ड पर नाम फ़ील्ड के चारों ओर बॉक्स खींचने जैसा समझें।

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

ये संख्याएँ क्यों? हमारे नमूना इमेज में नाम लगभग बाएँ किनारे से 120 px और ऊपर से 80 px पर स्थित है। इन्हें अपने कार्ड लेआउट के अनुसार समायोजित करें।  

*Edge case:* यदि कार्ड 90° घुमा हुआ है, तो `width` और `height` को बदलें और `left`/`top` को उसी अनुसार समायोजित करें, या इंजन को फीड करने से पहले Pillow से इमेज को प्री‑रोटेट करें।

## चरण 4: ROI के भीतर OCR निष्पादित करें

ROI निर्धारित होने पर, इंजन आयत के बाहर की सभी चीज़ों को नजरअंदाज़ करेगा। इससे प्रोसेसिंग तेज़ होती है और बैकग्राउंड ग्राफ़िक्स के कारण होने वाले फ़ॉल्स पॉज़िटिव कम होते हैं।

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

`recognize()` कॉल एक ऑब्जेक्ट लौटाता है जिसमें पहचाना गया टेक्स्ट, कॉन्फिडेंस स्कोर, और प्रत्येक शब्द के बाउंडिंग बॉक्स शामिल होते हैं।

## चरण 5: ID कार्ड टेक्स्ट निकालें (और स्पेनिश आउटपुट सत्यापित करें)

अंत में, हम **extract id card text** को ROI परिणाम से निकालते हैं और प्रिंट करते हैं। क्योंकि हमने पहले भाषा को स्पेनिश सेट किया था, OCR इंजन भाषा‑विशिष्ट शब्दकोश लागू करेगा, जिससे “ñ” या “á” जैसे अक्षरों की सटीकता बढ़ेगी।

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### अपेक्षित आउटपुट

```
ROI text: JUAN PÉREZ GARCÍA
```

यदि आपको गड़बड़ अक्षर दिखें, तो दोबारा जांचें कि इमेज वास्तव में स्पेनिश में है और OCR लाइब्रेरी के भाषा डेटा फ़ाइलें स्थापित हैं।

## सामान्य समस्याएँ और उनके समाधान

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| खाली स्ट्रिंग लौटाई गई | ROI किसी भी टेक्स्ट से नहीं मिलता | इमेज व्यूअर से निर्देशांक सत्यापित करें; यदि उपलब्ध हो तो `engine.debug_draw_roi()` उपयोग करें। |
| बहुत सारे ग़ैर‑अक्षर | गलत भाषा पैक | स्पेनिश भाषा डेटा को पुनः‑इंस्टॉल करें या `ocr.Language.AUTO` पर स्विच करें। |
| कम कॉन्फिडेंस स्कोर | इमेज धुंधली या कम‑कॉन्ट्रास्ट है | OpenCV से प्री‑प्रोसेस करें – `cv2.GaussianBlur` और `cv2.threshold` लागू करें। |
| ROI के बावजूद OCR पूरी इमेज पर चलता है | पुराना लाइब्रेरी संस्करण उपयोग किया गया | नवीनतम `ocr` पैकेज में अपग्रेड करें; पुराने संस्करण ROI को अनदेखा करते थे। |

## उदाहरण का विस्तार: कई ROI

कभी‑कभी आपको एक से अधिक फ़ील्ड निकालनी पड़ती है (जैसे नाम और ID नंबर)। पैटर्न वही रहता है: `engine.region_of_interest` बदलें और फिर से `recognize()` कॉल करें।

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

यदि लाइब्रेरी समर्थन देती है, तो आप आयतों की सूची को बैच‑प्रोसेस भी कर सकते हैं, जिससे OCR इंजन को कई बार कॉल करने की आवश्यकता नहीं रहती।

## पूर्ण कार्यशील स्क्रिप्ट

सब कुछ एक साथ रखते हुए, यहाँ एक तैयार‑चलाने‑योग्य स्क्रिप्ट है जो **defines region of interest**, **loads image for OCR**, और **extracts Spanish text** को एक ID कार्ड से निकालती है।

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

स्क्रिप्ट चलाएँ और आपको कंसोल में नाम प्रिंट होता दिखेगा। अन्य फ़ील्ड को लक्ष्य बनाने के लिए आयत मान बदलें, और आपके पास किसी भी ID‑कार्ड‑प्रकार दस्तावेज़ के लिए पुन: उपयोग योग्य यूटिलिटी होगी।

## अगले कदम

- **बैच प्रोसेसिंग:** ID कार्डों के फ़ोल्डर पर लूप चलाएँ और प्रत्येक निकाले गए नाम को CSV फ़ाइल में सहेजें।  
- **भाषा पहचान:** उपयोगकर्ता को भाषा गतिशील रूप से चुनने दें; `ocr.Language.AUTO` उपयोगी हो सकता है।  
- **पोस्ट‑प्रोसेसिंग:** सामान्य OCR त्रुटियों को साफ़ करने के लिए रेगएक्स पैटर्न लागू करें (उदाहरण: नामों में “0” को “O” से बदलें)।  

**define region of interest** को मास्टर करके आपने तेज़ और सटीक **extract id card text** का एक शक्तिशाली तरीका खोल दिया है, विशेष रूप से स्पेनिश‑भाषी दस्तावेज़ों के साथ काम करते समय।

---

### TL;DR

हमने आपको दिखाया कि **define region of interest in OCR**, **load image for OCR**, और **how to specify ROI** का उपयोग करके ID कार्ड से **extract spanish text image** कैसे किया जाता है। पूरा उदाहरण एक मिनट से कम समय में चलता है और कुछ ही निर्देशांक बदलावों से किसी भी लेआउट के लिए अनुकूलित किया जा सकता है। इसे आज़माएँ, आयत को समायोजित करें, और OCR को लेज़र की तरह फोकस होते देखें।

कोडिंग का आनंद लें!

## आप आगे क्या सीखेंगे?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API सुविधाओं में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}