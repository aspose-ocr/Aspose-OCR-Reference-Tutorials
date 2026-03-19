---
category: general
date: 2026-03-18
description: Python के साथ छवि पर OCR तेज़ी से चलाएँ। PNG से टेक्स्ट पहचानना, OCR
  के लिए छवि लोड करना, और चरण‑दर‑चरण गाइड में छवि से शब्द निकालना सीखें।
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: hi
og_description: Python का उपयोग करके छवि पर OCR चलाएँ। यह ट्यूटोरियल दिखाता है कि
  PNG से टेक्स्ट कैसे पहचाना जाए, OCR के लिए छवि कैसे लोड की जाए, और पूर्ण कोड उदाहरण
  के साथ छवि से शब्द कैसे निकाले जाएँ।
og_title: छवि पर OCR चलाएँ – पायथन गाइड
tags:
- OCR
- Python
- Image Processing
title: इमेज पर OCR चलाएँ – पूर्ण पायथन OCR उदाहरण
url: /hi/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज पर OCR चलाएँ – पूर्ण Python OCR उदाहरण

क्या आपको कभी **run OCR on image** फ़ाइलों को प्रोसेस करना पड़ा लेकिन शुरुआत नहीं पता थी? आप अकेले नहीं हैं; कई डेवलपर्स पहली बार स्कैन किए गए दस्तावेज़ों से टेक्स्ट निकालते समय इस समस्या से जूझते हैं। इस ट्यूटोरियल में हम एक **Python OCR example** के माध्यम से दिखाएंगे कि कैसे **recognize text from PNG** फ़ाइलों, **load image for OCR**, और **extract words from image** को कॉन्फिडेंस स्कोर के साथ कुछ ही लाइनों के कोड में किया जा सकता है।

हम वह सब कवर करेंगे जिसकी आपको ज़रूरत है: आवश्यक लाइब्रेरी, इंजन सेटअप, प्रत्येक चरण का महत्व, और आउटपुट कैसा दिखेगा। अंत तक आप इस स्निपेट को अपने प्रोजेक्ट में डालकर तुरंत किसी भी इमेज से टेक्स्ट निकाल सकेंगे। कोई फालतू बात नहीं, सिर्फ़ एक व्यावहारिक, चलाने योग्य समाधान।

## What You’ll Need

- Python 3.8 या उससे नया स्थापित हो  
- `ocrengine` पैकेज (या कोई भी लाइब्रेरी जो `OcrEngine` क्लास प्रदान करती हो)। इसे `pip install ocrengine` से इंस्टॉल कर सकते हैं – यदि आप कोई अलग OCR लाइब्रेरी जैसे `pytesseract` उपयोग कर रहे हैं तो नाम बदलें।  
- एक इमेज फ़ाइल (PNG, JPG, आदि) जिसे आप प्रोसेस करना चाहते हैं – इस गाइड के लिए हम `invoice.png` का उपयोग करेंगे।  

बस इतना ही। कोई भारी डिपेंडेंसी नहीं, कोई बाहरी सेवा नहीं, सिर्फ़ शुद्ध Python।

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Alt text: run OCR on image example – स्कैन किया गया इनवॉइस प्रोसेस हो रहा है*

## Step 1 – Install and Import the OCR Library

सबसे पहले, OCR इंजन को अपने वातावरण में लाएँ और इसे इम्पोर्ट करें। यदि आप काल्पनिक `ocrengine` पैकेज का उपयोग कर रहे हैं, तो इम्पोर्ट इस प्रकार दिखेगा:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Why this matters:** सही क्लास को इम्पोर्ट करने से आपको उन मेथड्स तक पहुँच मिलती है जिन्हें हम बाद में कॉल करेंगे, जैसे `setImageFromFile` और `recognize`। यदि आप इस चरण को छोड़ देते हैं, तो Python `ModuleNotFoundError` फेंकेगा, और आप इमेज लोड करने से पहले ही अटक जाएंगे।

## Step 2 – Create an OCR Engine Instance

अब लाइब्रेरी तैयार है, हमें एक इंजन ऑब्जेक्ट चाहिए जो पहचान प्रक्रिया के लिए कॉन्फ़िगरेशन और स्टेट को रखे।

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Pro tip:* कुछ OCR इंजन इस चरण में भाषा मॉडल या DPI सेटिंग्स को ट्यून करने की अनुमति देते हैं। एक बेसिक **python OCR example** के लिए डिफ़ॉल्ट्स ठीक काम करेंगे, लेकिन यदि आप लो‑रेज़ोल्यूशन स्कैन से निपट रहे हैं, तो यहाँ इन्हें समायोजित करने पर विचार करें।

## Step 3 – Load the Image You Want to Process

अगला तार्किक कदम **load image for OCR** है। आप इंजन को उस PNG (या किसी भी समर्थित फ़ॉर्मेट) के फ़ाइल पाथ की ओर इशारा करते हैं जिसे आप विश्लेषण करना चाहते हैं।

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**What’s happening under the hood?** इंजन पिक्सेल डेटा पढ़ता है, उसे उस फ़ॉर्मेट में बदलता है जिसे पहचान एल्गोरिदम समझ सके, और उसे आंतरिक रूप से स्टोर करता है। यदि फ़ाइल पाथ गलत है, तो आपको `FileNotFoundError` मिलेगा, इसलिए इमेज मौजूद है या नहीं, दोबारा जाँचें।

## Step 4 – Run the Recognition Algorithm

इमेज लोड हो जाने के बाद, हम अंततः **run OCR on image** करके टेक्स्टुअल कंटेंट निकालते हैं।

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

इस बिंदु पर इंजन बिटमैप को स्कैन करता है, पैटर्न मैचिंग लागू करता है, और एक ऑब्जेक्ट रिटर्न करता है जिसमें प्रत्येक डिटेक्टेड शब्द, लाइन, और कॉन्फिडेंस मेट्रिक शामिल होते हैं।

## Step 5 – Iterate Over Recognized Words and Display Confidence

किसी भी OCR वर्कफ़्लो का सबसे उपयोगी हिस्सा है **the confidence** को प्रत्येक एक्सट्रैक्टेड टोकन के लिए देखना। यह बताता है कि इंजन प्रत्येक शब्द के बारे में कितना निश्चित है, जिससे आप आवश्यकता पड़ने पर लो‑कॉन्फिडेंस परिणामों को फ़िल्टर कर सकते हैं।

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Expected output** (sample):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

अब आप ठीक‑ठीक देख सकते हैं **what words were extracted from the image** और प्रत्येक डिटेक्शन कितनी विश्वसनीय है। यह किसी भी **extract words from image** पाइपलाइन का मूल है।

## Handling Common Edge Cases

### What If the Image Is Grayscale?

कुछ OCR इंजन कलर इमेज पर बेहतर काम करते हैं। यदि आप पूरे बोर्ड पर कम कॉन्फिडेंस देखते हैं, तो PNG को उच्च‑कॉन्ट्रास्ट ब्लैक‑एंड‑व्हाइट संस्करण में बदलकर इंजन को फ़ीड करने की कोशिश करें। Pillow मदद कर सकता है:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Dealing With Multiple Languages

यदि आपके दस्तावेज़ में अंग्रेज़ी और स्पेनिश दोनों हैं, तो आपको **recognize text from PNG** के लिए मल्टीलिंगुअल मॉडल की आवश्यकता होगी। अधिकांश इंजन आपको इनिशियलाइज़ेशन के दौरान भाषा सूची सेट करने की अनुमति देते हैं:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Filtering Low‑Confidence Words

कभी‑कभी आपको केवल उन शब्दों की ज़रूरत होती है जिनकी कॉन्फिडेंस 90 % से ऊपर हो। एक त्वरित फ़िल्टर इस प्रकार दिखता है:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Full, Ready‑to‑Run Script

सब कुछ एक साथ जोड़ते हुए, यहाँ एक सिंगल स्क्रिप्ट है जिसे आप कॉपी‑पेस्ट करके तुरंत चला सकते हैं (बस अपने PNG का पाथ बदलें)।

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

इसे इस तरह चलाएँ:

```bash
python run_ocr_on_image.py
```

आपको कंसोल में शब्दों की सूची और कॉन्फिडेंस प्रतिशत प्रिंट होते हुए दिखेंगे, बिल्कुल वही जैसा कि पहले दिखाया गया था।

## Frequently Asked Questions

**Does this work with JPG or TIFF files?**  
बिल्कुल। `setImageFromFile` मेथड किसी भी फ़ॉर्मेट को स्वीकार करता है जिसे अंडरलाइनिंग लाइब्रेरी डिकोड कर सके, इसलिए आप **run OCR on image** फ़ाइलों को JPG, TIFF, BMP आदि प्रकारों में प्रोसेस कर सकते हैं।

**Can I process multiple images in a loop?**  
हां, बिल्कुल। लोडिंग और पहचान चरणों को `for` लूप में फ़ाइल पाथ की सूची के ऊपर रैप कर दें। बस यह याद रखें कि यदि लाइब्रेरी को प्रति इमेज नया इंस्टेंस चाहिए तो इंजन को फिर से इनिशियलाइज़ करें।

**What if I need the text in a single string instead of per‑word?**  
अधिकांश OCR रिज़ल्ट ऑब्जेक्ट्स एक `getText()` मेथड एक्सपोज़ करते हैं जो पूरे दस्तावेज़ को रिटर्न करता है। उदाहरण:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Next Steps and Related Topics

अब जब आप **run OCR on image** करना जानते हैं, तो निम्नलिखित विषयों को एक्सप्लोर करें:

- **Post‑processing**: रेगुलर एक्सप्रेशन का उपयोग करके इनवॉइस से निकाले गए डेट, अमाउंट या IDs को साफ़ करें।  
- **Batch processing**: स्क्रिप्ट को `os.listdir()` के साथ मिलाकर स्कैन किए गए दस्तावेज़ों के पूरे फ़ोल्डर को हैंडल करें।  
- **Alternative libraries**: `pytesseract` एक लोकप्रिय ओपन‑सोर्स विकल्प है; वर्कफ़्लो समान है—बस इंजन कॉल्स को बदल दें।  
- **Exporting results**: एक्सट्रैक्टेड शब्दों और कॉन्फिडेंस स्कोर को CSV में लिखें ताकि डाउनस्ट्रीम एनालिसिस किया जा सके।  

इनमें से प्रत्येक एक्सटेंशन सीधे उस फाउंडेशन पर बना है जो हमने यहाँ स्थापित किया है, जिससे आप रॉ OCR डेटा को actionable जानकारी में बदल सकते हैं।

---

### TL;DR

हमने एक संक्षिप्त, **python OCR example** दिखाया है जो बताता है कैसे **load image for OCR**, **run OCR on image**, और **extract words from image** करते हुए कॉन्फिडेंस रिपोर्ट किया जाता है। पूरा स्क्रिप्ट चलाने के लिए तैयार है, और अब आपके पास वह ज्ञान है जिससे आप इसे किसी भी प्रोजेक्ट में एडेप्ट कर सकते हैं जिसे **recognize text from PNG** (या अन्य फ़ॉर्मेट) की ज़रूरत है। इसे आज़माएँ, कॉन्फिडेंस थ्रेशोल्ड को ट्यून करें, और देखें कि आपके एप्लिकेशन मिनटों में टेक्स्ट‑अवेयर कैसे बनते हैं। Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}