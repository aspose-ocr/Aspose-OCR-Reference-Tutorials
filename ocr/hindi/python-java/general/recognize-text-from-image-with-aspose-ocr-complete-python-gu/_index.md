---
category: general
date: 2026-06-28
description: Aspose OCR for Python का उपयोग करके छवि से टेक्स्ट पहचानना और OCR करना
  सीखें। इसमें OCR भाषा सेट करने और कॉन्फिडेंस स्कोर निकालने के चरण शामिल हैं।
draft: false
keywords:
- recognize text from image
- perform ocr on image
- how to set OCR language
language: hi
og_description: Aspose OCR का उपयोग करके Python में छवि से पाठ को पहचानें। यह गाइड
  दिखाता है कि OCR भाषा कैसे सेट करें, छवि पर OCR कैसे करें, और विश्वसनीयता स्तर कैसे
  पढ़ें।
og_title: छवि से पाठ पहचानें – पूर्ण पायथन OCR ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  headline: recognize text from image with Aspose OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  name: recognize text from image with Aspose OCR – Complete Python Guide
  steps:
  - name: What if my image contains multiple languages?
    text: 'Aspose OCR supports multi‑language detection, but you need to pass a **combined
      language flag**. For example, to handle both Latin and Cyrillic:'
  - name: How do I improve accuracy on low‑resolution images?
    text: '- **Pre‑process** the image: increase contrast, apply binarization, or
      upscale using a library like Pillow. - **Set the correct DPI** if you know it;
      Aspose respects the image metadata. - **Choose the right language**—the more
      specific you are, the better the model performs.'
  - name: Can I extract only certain regions of the image?
    text: Yes. Use the `recognizeRegion` method (not shown in the basic example) and
      pass a rectangle object defining the area of interest. This is handy when you
      only need a table or a specific block of text.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Aspose OCR के साथ छवि से टेक्स्ट पहचानें – पूर्ण पाइथन गाइड
url: /hi/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-python-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज से टेक्स्ट पहचानें Aspose OCR के साथ – पूर्ण Python गाइड

क्या आपको कभी **इमेज से टेक्स्ट पहचानने** की जरूरत पड़ी है लेकिन यह नहीं पता था कि कौन सी लाइब्रेरी आपको गति और सटीकता दोनों देगी? आप अकेले नहीं हैं। दस्तावेज़ ऑटोमेशन की दुनिया में, **इमेज पर OCR करने** की क्षमता एक दैनिक आवश्यकता है—चाहे आप रसीदों को डिजिटल बना रहे हों, पासपोर्ट स्कैन कर रहे हों, या बहुभाषी संकेतों से डेटा निकाल रहे हों।

इस ट्यूटोरियल में हम एक व्यावहारिक उदाहरण के माध्यम से दिखाएंगे कि Aspose OCR for Python का उपयोग करके **इमेज से टेक्स्ट कैसे पहचानें**, और साथ ही **OCR भाषा कैसे सेट करें** ताकि इंजन को पता हो कि वह लैटिन, सिरिलिक या किसी अन्य लिपि से निपट रहा है। अंत तक आपके पास एक तैयार‑चलाने‑योग्य स्क्रिप्ट होगी जो पूरा टेक्स्ट, लाइन‑बाय‑लाइन कॉन्फिडेंस, और प्रत्येक शब्द के बाउंडिंग बॉक्स को प्रिंट करेगी।

## आपको क्या चाहिए

- **Python 3.8+** (कोड किसी भी हालिया संस्करण पर काम करता है)
- **Aspose.OCR for Python via Java** पैकेज – इसे `pip install aspose-ocr` से इंस्टॉल करें
- एक इमेज फ़ाइल (जैसे, `mixed_script.png`) जिसमें वह टेक्स्ट हो जिसे आप निकालना चाहते हैं
- एक बेसिक IDE या एडिटर—VS Code, PyCharm, या यहाँ तक कि साधारण टेक्स्ट एडिटर भी चलेगा

कोई भारी डिपेंडेंसी नहीं, कोई नेटिव बाइनरी नहीं जिसे कंपाइल करना पड़े। सिर्फ एक pip इंस्टॉल और आप तैयार हैं।

## Step 1: Install and Import the OCR Engine

पहले लाइब्रेरी को अपने मशीन पर इंस्टॉल करें और आवश्यक क्लासेज़ को इम्पोर्ट करें।

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

# Import the OCR engine and the language enumeration
from asposeocrjava import OcrEngine, Language
```

> **Pro tip:** यदि आप कॉर्पोरेट प्रॉक्सी के पीछे हैं, तो pip कमांड में `--proxy` फ़्लैग जोड़ें। यह बाद में बहुत सिरदर्द बचाता है।

## Step 2: Create the Engine and **how to set OCR language**

`OcrEngine` का एक इंस्टेंस बनाना इतना सरल है जितना उसके कंस्ट्रक्टर को कॉल करना, लेकिन असली शक्ति तब आती है जब आप इंजन को बताते हैं कि किस भाषा की अपेक्षा है। यही वह भाग है जो “**OCR भाषा कैसे सेट करें**” सवाल का जवाब देता है।

```python
# Instantiate the OCR engine
ocr_engine = OcrEngine()

# Tell the engine we’re dealing with Latin script (you can pick others like Language.Cyrillic)
ocr_engine.setLanguage(Language.Latin)
```

यह क्यों महत्वपूर्ण है? OCR एल्गोरिदम भाषा‑विशिष्ट कैरेक्टर मॉडल का उपयोग करते हैं; सही भाषा सेट करने से सटीकता में काफी सुधार होता है, विशेषकर उन स्क्रिप्ट्स में जहाँ समान ग्लिफ़ होते हैं (जैसे लैटिन में “0” बनाम “O” और सिरिलिक में “О”)।

## Step 3: **perform OCR on image** – Recognize the Text

अब हम इंजन को इमेज पाथ देते हैं और उसे अपना जादू करने देते हैं। यह मेथड एक `RecognitionResult` ऑब्जेक्ट रिटर्न करता है जिसमें आपको चाहिए सब कुछ होता है।

```python
# Path to the image you want to process
image_path = "YOUR_DIRECTORY/mixed_script.png"

# Run the OCR operation
recognition_result = ocr_engine.recognizeImage(image_path)
```

यदि फ़ाइल नहीं मिलती, तो Aspose `FileNotFoundError` उठाएगा। प्रोडक्शन कोड में कॉल को `try/except` ब्लॉक में रैप करें—अनहैंडल्ड एक्सेप्शन आपके सर्विस को क्रैश कर सकता है।

## Step 4: Output the Full Recognized Text

सबसे आम अनुरोध बस “मुझे टेक्स्ट दो” होता है। `getText()` मेथड सभी डिटेक्टेड लाइनों को एक सिंगल स्ट्रिंग में जोड़ देता है।

```python
# Print the complete text extracted from the image
print("Full text:", recognition_result.getText())
```

आपको कुछ इस तरह दिखेगा:

```
Full text: Hello World!
This is a sample mixed‑script image.
```

यही है **इमेज से टेक्स्ट पहचानने** का मूल—एक-लाइनर जो इंजन द्वारा डिकोड किया गया पूरा टेक्स्ट रिटर्न करता है।

## Step 5: (Optional) Show Confidence for Each Detected Line

कॉन्फिडेंस स्कोर आपको विश्वसनीयता का अंदाज़ा देते हैं। 0.70 से नीचे की स्कोर वाली लाइनों को मानव समीक्षा की ज़रूरत पड़ सकती है।

```python
print("\n--- Line‑by‑Line Confidence ---")
for line in recognition_result.getLines():
    # Each line object provides its text and a confidence value between 0 and 1
    print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")
```

आम आउटपुट:

```
Line: 'Hello World!'  Confidence: 0.98
Line: 'This is a sample mixed‑script image.'  Confidence: 0.85
```

## Step 6: (Optional) Retrieve Bounding Boxes for Each Word – Great for UI Highlighting

यदि आप ऐसा व्यूअर बना रहे हैं जहाँ यूज़र किसी शब्द पर क्लिक करके उसका OCR डेटा देख सके, तो बाउंडिंग बॉक्स कॉर्डिनेट्स बहुत काम आते हैं।

```python
print("\n--- Word Bounding Boxes ---")
for word in recognition_result.getWords():
    bbox = word.getBoundingBox()   # Returns (x, y, width, height)
    print(f"Word '{word.getText()}' at {bbox}")
```

सैंपल आउटपुट:

```
Word 'Hello' at (12, 34, 58, 20)
Word 'World' at (78, 34, 60, 20)
```

ये कॉर्डिनेट्स पिक्सेल में होते हैं और मूल इमेज के सापेक्ष होते हैं, इसलिए आप उन्हें सीधे कैनवास पर ओवरले कर सकते हैं।

## Full Working Script

सब कुछ मिलाकर, यहाँ एक तैयार‑चलाने‑योग्य स्क्रिप्ट है जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं। बस `YOUR_DIRECTORY/mixed_script.png` को अपनी इमेज के वास्तविक पाथ से बदलें।

```python
# ocr_demo.py
from asposeocrjava import OcrEngine, Language

def main(image_path: str, language: Language = Language.Latin):
    """
    Recognize text from an image using Aspose OCR.
    Parameters:
        image_path (str): Full path to the image file.
        language (Language): OCR language to use (default: Latin).
    """
    # Create the OCR engine and set the desired language
    ocr_engine = OcrEngine()
    ocr_engine.setLanguage(language)

    try:
        # Perform OCR
        result = ocr_engine.recognizeImage(image_path)

        # Full text output
        print("Full text:", result.getText())

        # Optional: line confidence
        print("\n--- Line‑by‑Line Confidence ---")
        for line in result.getLines():
            print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")

        # Optional: word bounding boxes
        print("\n--- Word Bounding Boxes ---")
        for word in result.getWords():
            bbox = word.getBoundingBox()
            print(f"Word '{word.getText()}' at {bbox}")

    except FileNotFoundError:
        print(f"Error: Image file not found at {image_path}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    # Change the path below to point at your own test image
    IMAGE_PATH = "YOUR_DIRECTORY/mixed_script.png"
    main(IMAGE_PATH, Language.Latin)
```

Run it with:

```bash
python ocr_demo.py
```

आपको कंसोल में पूरा एक्सट्रैक्टेड टेक्स्ट, कॉन्फिडेंस स्कोर, और बाउंडिंग बॉक्स प्रिंट होते दिखेंगे।

## Common Questions & Edge Cases

### What if my image contains multiple languages?

Aspose OCR मल्टी‑लैंग्वेज डिटेक्शन को सपोर्ट करता है, लेकिन आपको एक **कंबाइंडेड लैंग्वेज फ्लैग** पास करना होगा। उदाहरण के लिए, लैटिन और सिरिलिक दोनों को हैंडल करने के लिए:

```python
ocr_engine.setLanguage(Language.Latin | Language.Cyrillic)
```

पाइप (`|`) ऑपरेटर एनेम्स को मर्ज करता है। यह मल्टी‑लैंग्वेज परिदृश्यों के लिए “**इमेज पर OCR करना**” की आवश्यकता को पूरा करता है।

### How do I improve accuracy on low‑resolution images?

- **इमेज को प्री‑प्रोसेस** करें: कंट्रास्ट बढ़ाएँ, बाइनराइज़ेशन लागू करें, या Pillow जैसी लाइब्रेरी से अपस्केल करें।
- यदि आप DPI जानते हैं तो **सही DPI सेट** करें; Aspose इमेज मेटाडेटा को मानता है।
- **सही भाषा चुनें**—जितनी विशिष्ट आप होंगे, मॉडल उतना ही बेहतर प्रदर्शन करेगा।

### Can I extract only certain regions of the image?

हाँ। `recognizeRegion` मेथड (बेसिक उदाहरण में नहीं दिखाया गया) का उपयोग करें और एक रेक्टैंगल ऑब्जेक्ट पास करें जो रुचि के क्षेत्र को परिभाषित करता है। यह तब उपयोगी होता है जब आपको केवल टेबल या किसी विशेष टेक्स्ट ब्लॉक की ज़रूरत हो।

## Conclusion

हमने अभी-अभी Aspose OCR for Python का उपयोग करके **इमेज से टेक्स्ट पहचानने** का एक पूर्ण, एंड‑टू‑एंड उदाहरण देखा। अब आप जानते हैं कि **इमेज पर OCR कैसे करें**, **OCR भाषा** सही तरीके से सेट करें, और कॉन्फिडेंस स्कोर तथा शब्द‑स्तर बाउंडिंग बॉक्स दोनों को कैसे प्राप्त करें ताकि आगे के UI कार्यों में उपयोग किया जा सके।

अब आप आगे कर सकते हैं:

- अन्य भाषाओं (`Language.Arabic`, `Language.Japanese`, आदि) के साथ प्रयोग करें
- स्क्रिप्ट को वेब सर्विस (Flask/Django) में इंटीग्रेट करें ताकि OCR को API के रूप में प्रदान किया जा सके
- बाउंडिंग‑बॉक्स डेटा को फ्रंट‑एंड कैनवास के साथ मिलाकर यूज़र्स को टेक्स्ट हाईलाइट करने की सुविधा दें

संभावनाएँ उतनी ही विस्तृत हैं जितनी दस्तावेज़ जिन्हें आपको डिजिटल बनाना है। कोई कठिन इमेज है जो सहयोग नहीं कर रही? कमेंट करें, हम साथ में ट्रबलशूट करेंगे। Happy coding! 

![इमेज से टेक्स्ट पहचानने का उदाहरण](/images/ocr_example.png "इमेज से टेक्स्ट पहचानें – Aspose OCR आउटपुट")

## आगे आप क्या सीख सकते हैं?

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}