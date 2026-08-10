---
category: general
date: 2026-06-25
description: OCR के लिए छवि लोड करें और aocr का उपयोग करके PNG पर चरण‑दर‑चरण Python
  ट्यूटोरियल के साथ OCR करें। डिबगिंग, लॉगिंग और सर्वोत्तम प्रथाएँ सीखें।
draft: false
keywords:
- load image for OCR
- perform OCR on PNG
- aocr logging setup
- OCR debugging Python
- image preprocessing OCR
language: hi
og_description: OCR के लिए छवि लोड करें और aocr का उपयोग करके PNG पर OCR करें। यह
  गाइड आपको लॉगिंग, छवि लोड करने और पूर्ण कोड के साथ पहचान प्रक्रिया के माध्यम से
  ले जाता है।
og_title: OCR के लिए छवि लोड करें – चरण‑दर‑चरण पायथन ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Load image for OCR and perform OCR on PNG with a step‑by‑step Python
    tutorial using aocr. Learn debugging, logging, and best practices.
  headline: Load Image for OCR – Complete Guide to Perform OCR on PNG Files
  type: TechArticle
- questions:
  - answer: Usually not. `aocr` handles PNG natively, but if the image is huge (>10
      MP) you might want to downscale first to speed up processing.
    question: Do I need to convert the PNG to another format?
  - answer: Rotate the log after each run or limit the level to `INFO` once you’re
      confident the pipeline works.
    question: What if the logger file grows too large?
  - answer: Absolutely. Just call `ocr_png` for each file; the function creates a
      fresh logger each time, keeping logs isolated.
    question: Can I process multiple images in a loop?
  - answer: Yes – `engine.result` also contains `boxes` and `confidences`. Explore
      the `aocr` docs for `result.boxes` if you need layout information.
    question: Is there a way to get bounding boxes instead of plain text?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: OCR के लिए इमेज लोड करें – PNG फ़ाइलों पर OCR करने के लिए पूर्ण मार्गदर्शिका
url: /hi/python/general/load-image-for-ocr-complete-guide-to-perform-ocr-on-png-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR के लिए इमेज लोड करें – PNG फ़ाइलों पर OCR करने की पूर्ण गाइड

क्या आपको कभी **load image for OCR** करने की ज़रूरत पड़ी है लेकिन सही डिबगिंग सेटअप नहीं पता था? आप अकेले नहीं हैं। कई प्रोजेक्ट्स में पहला बाधा यह है कि PNG को इंजन में लोड किया जाए जबकि यह देखा जा सके कि अंदर क्या हो रहा है।  

इस ट्यूटोरियल में हम आपको वह सब कुछ दिखाएंगे जो आपको `aocr` लाइब्रेरी का उपयोग करके **perform OCR on PNG** फ़ाइलों के लिए चाहिए – विस्तृत आउटपुट के लिए लॉगर सेटअप करने से लेकर वास्तविक टेक्स्ट पहचान तक। अंत तक आपके पास एक पुन: उपयोग योग्य स्क्रिप्ट होगी जिसे आप किसी भी Python प्रोजेक्ट में जोड़ सकते हैं, और आप समझेंगे कि प्रत्येक भाग क्यों महत्वपूर्ण है।

## आप क्या सीखेंगे

- कैसे `aocr` लॉगर को इनिशियलाइज़ करें ताकि आप हर कदम को ट्रेस कर सकें।
- `aocr.OcrEngine` के साथ **load image for OCR** करने के लिए सटीक कोड।
- डिटेल्ड डिबग जानकारी पाने के लिए लॉगिंग लेवल को कैसे कॉन्फ़िगर करें।
- इंजन को चलाकर **perform OCR on PNG** और परिणाम प्राप्त करना।
- गुम फ़ाइलों या असमर्थित फ़ॉर्मेट जैसी सामान्य समस्याओं को संभालने के टिप्स।

`aocr` का कोई पूर्व अनुभव आवश्यक नहीं है; बस एक कार्यशील Python 3 इंस्टॉलेशन और वह इमेज जिसे आप पढ़ना चाहते हैं। चलिए शुरू करते हैं।

![OCR के लिए इमेज लोड करने का उदाहरण](assets/load-image-ocr.png "Python में OCR के लिए इमेज लोड करने का चित्रण")

## आवश्यकताएँ

| आवश्यकता | क्यों महत्वपूर्ण है |
|-------------|----------------|
| Python 3.8+ | `aocr` आधुनिक इंटरप्रेटर्स को टार्गेट करता है और टाइप हिंट्स का उपयोग करता है। |
| `aocr` लाइब्रेरी स्थापित (`pip install aocr`) | पैकेज के बिना हम जिन क्लासेज़ का उपयोग करते हैं वे मौजूद नहीं होंगी। |
| एक PNG इमेज जिसे आप पढ़ना चाहते हैं | ट्यूटोरियल **perform OCR on PNG** पर केंद्रित है, इसलिए PNG आवश्यक है। |
| लॉग डायरेक्टरी में लिखने की अनुमति | लॉगर को `ocr_debug.log` बनाना आवश्यक है। |

यदि इनमें से कोई भी कमी है, तो अभी इंस्टॉल करें – यह केवल एक मिनट लेता है।

```bash
pip install aocr
```

## चरण 1: OCR के लिए इमेज लोड करें – लॉगिंग इनिशियलाइज़ करें

इमेज को छूने से पहले, एक लॉगर सेट करें। OCR को डिबग करना एक दुःस्वप्न हो सकता है यदि आप नहीं जानते कि इंजन क्या कर रहा है। `aocr.Logging` क्लास सब कुछ फ़ाइल में लिखती है, और लेवल को `DEBUG` सेट करने पर आप हर आंतरिक कॉल देख पाएंगे।

```python
import aocr

# Create a logger instance
ocr_logger = aocr.Logging()
# Choose where the log file will live – adjust the path to suit your project
ocr_logger.set_output_file("logs/ocr_debug.log")

# DEBUG gives you the most detail; you can switch to INFO for less noise
ocr_logger.set_level(aocr.LoggingLevel.DEBUG)
```

**क्यों यह महत्वपूर्ण है:**  
यदि OCR इंजन फ़ाइल नहीं ढूँढ़ पाता है या इमेज फ़ॉर्मेट असमर्थित है, तो लॉगर एक्सेप्शन स्टैक ट्रेस को कैप्चर करेगा। यह आपको बाद में अनंत अनुमान‑कार्य से बचाता है।

## चरण 2: PNG पर OCR करें – इंजन को कॉन्फ़िगर करें

अब जब लॉगर तैयार है, इसे OCR इंजन से जोड़ें। यह कदम दोनों को जोड़ता है ताकि हर इंजन कार्रवाई रिकॉर्ड हो।

```python
# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
# Plug the logger into the engine
ocr_engine.logging = ocr_logger
```

**प्रो टिप:**  
आप कई इमेज के लिए वही `ocr_engine` इंस्टेंस पुन: उपयोग कर सकते हैं। बस बैच प्रोसेस करते समय किसी भी पूर्व स्थिति को साफ़ करना याद रखें।

## चरण 3: OCR के लिए इमेज लोड करें – PNG फ़ाइल को फीड करें

यह ट्यूटोरियल का मुख्य भाग है: वास्तव में **load image for OCR**। `load_image` मेथड एक फ़ाइल पाथ लेता है; यह आंतरिक रूप से PNG को बिटमैप में डिकोड करेगा जिसे इंजन समझ सकेगा।

```python
# Path to the PNG you want to read
image_path = "samples/invoice.png"

# Load the image – this is where we “load image for OCR”
ocr_engine.load_image(image_path)
```

### ध्यान देने योग्य किनारे के केस

1. **फ़ाइल नहीं मिली** – यदि पाथ गलत है, तो `aocr` `FileNotFoundError` उठाता है। लॉगर इसे नोट करेगा, लेकिन आप इसे पकड़ भी सकते हैं:

   ```python
   try:
       ocr_engine.load_image(image_path)
   except FileNotFoundError as e:
       print(f"❌ Could not locate {image_path}: {e}")
       raise
   ```

2. **असमर्थित फ़ॉर्मेट** – यद्यपि PNG व्यापक रूप से समर्थित है, एक भ्रष्ट फ़ाइल `UnsupportedFormatError` ट्रिगर कर सकती है। ऐसे में, लोड करने से पहले Pillow के साथ इमेज को साफ़ PNG में बदलने पर विचार करें।

## चरण 4: PNG पर OCR करें – पहचान चलाएँ

अब जब इमेज मेमोरी में है, आप अंततः **perform OCR on PNG** कर सकते हैं। `recognize` मेथड इंजन की पाइपलाइन (प्री‑प्रोसेसिंग, सेगमेंटेशन, क्लासिफिकेशन) को लॉन्च करता है और परिणाम ऑब्जेक्ट को भरता है।

```python
# Execute the OCR process
ocr_engine.recognize()
```

इस कॉल के बाद, इंजन पहचाना गया टेक्स्ट रखता है। आप इसे `result` एट्रिब्यूट के माध्यम से एक्सेस कर सकते हैं:

```python
# Retrieve the plain text output
recognized_text = ocr_engine.result.text
print("📝 OCR Result:")
print(recognized_text)
```

**आपको परिणाम जांचना क्यों चाहिए:**  
कुछ OCR इंजन कम‑कॉन्ट्रास्ट इमेज के लिए खाली स्ट्रिंग लौटाते हैं। परिणाम तुरंत देखना आपको यह तय करने देता है कि पुनः चलाने से पहले आपको प्री‑प्रोसेस (जैसे कॉन्ट्रास्ट बढ़ाना) करना चाहिए या नहीं।

## चरण 5: सब कुछ समेटें – एक पुन: उपयोग योग्य फ़ंक्शन

सभी भागों को एक फ़ंक्शन में जोड़ने से इसे अन्य स्क्रिप्ट्स या वेब सर्विस से कॉल करना आसान हो जाता है। यह यह भी दर्शाता है कि कैसे **load image for OCR** और **perform OCR on PNG** को एक साफ़ पैकेज में किया जाए।

```python
def ocr_png(image_path: str, log_dir: str = "logs") -> str:
    """
    Load a PNG image, run aocr OCR, and return the extracted text.
    
    Parameters
    ----------
    image_path : str
        Full path to the PNG file.
    log_dir : str, optional
        Directory where the debug log will be written.
    
    Returns
    -------
    str
        The plain‑text OCR result.
    """
    import os
    import aocr

    # Ensure the log directory exists
    os.makedirs(log_dir, exist_ok=True)

    # ---------- Logging ----------
    logger = aocr.Logging()
    logger.set_output_file(os.path.join(log_dir, "ocr_debug.log"))
    logger.set_level(aocr.LoggingLevel.DEBUG)

    # ---------- Engine ----------
    engine = aocr.OcrEngine()
    engine.logging = logger

    # ---------- Load Image ----------
    try:
        engine.load_image(image_path)
    except Exception as exc:
        logger.error(f"Failed to load image {image_path}: {exc}")
        raise

    # ---------- Recognize ----------
    engine.recognize()
    return engine.result.text

# Example usage
if __name__ == "__main__":
    txt = ocr_png("samples/invoice.png")
    print("\n--- Extracted Text ---\n")
    print(txt)
```

स्क्रिप्ट चलाने पर `logs` फ़ोल्डर में एक विस्तृत `ocr_debug.log` बनेगा, फिर पहचाना गया टेक्स्ट कंसोल में प्रिंट होगा। अब आपके पास एक **perform OCR on PNG** यूटिलिटी है जिसे आप कहीं भी इम्पोर्ट कर सकते हैं।

## सामान्य प्रश्न और गड़बड़ियां

- **क्या मुझे PNG को किसी अन्य फ़ॉर्मेट में बदलना चाहिए?**  
  आमतौर पर नहीं। `aocr` PNG को मूल रूप से संभालता है, लेकिन यदि इमेज बहुत बड़ी है (>10 MP) तो प्रोसेसिंग तेज़ करने के लिए पहले उसे डाउनस्केल करना चाह सकते हैं।

- **यदि लॉगर फ़ाइल बहुत बड़ी हो जाए तो क्या करें?**  
  प्रत्येक रन के बाद लॉग को रोटेट करें या जब आपको पाइपलाइन काम करती दिखे तो लेवल को `INFO` तक सीमित करें।

- **क्या मैं लूप में कई इमेज प्रोसेस कर सकता हूँ?**  
  बिल्कुल। प्रत्येक फ़ाइल के लिए `ocr_png` को कॉल करें; फ़ंक्शन हर बार एक नया लॉगर बनाता है, जिससे लॉग अलग रहते हैं।

- **क्या साधारण टेक्स्ट के बजाय बाउंडिंग बॉक्स प्राप्त करना संभव है?**  
  हाँ – `engine.result` में `boxes` और `confidences` भी होते हैं। यदि आपको लेआउट जानकारी चाहिए तो `aocr` डॉक्यूमेंटेशन में `result.boxes` देखें।

## निष्कर्ष

अब आप जानते हैं कि `aocr` लाइब्रेरी का उपयोग करके **load image for OCR** और **perform OCR on PNG** कैसे किया जाता है, साथ ही एक मजबूत लॉगिंग सेटअप जो डिबगिंग को आसान बनाता है। उदाहरण फ़ंक्शन पूरे वर्कफ़्लो को समेटे हुए है, इसलिए आप इसे किसी भी प्रोजेक्ट में डाल सकते हैं और तुरंत टेक्स्ट निकालना शुरू कर सकते हैं।

अगले कदम? इंजन को विभिन्न इमेज प्रकार (JPEG, TIFF) दें और देखें कि सटीकता कैसे बदलती है, या थ्रेशहोल्डिंग जैसी प्री‑प्रोसेसिंग तकनीकों के साथ प्रयोग करके शोरयुक्त स्कैन पर परिणाम बढ़ाएँ। और यदि आप संरचित डेटा (टेबल, फ़ॉर्म) निकालने में रुचि रखते हैं, तो `aocr` के लेआउट एनालिसिस सेक्शन देखें – ये आपके बनाए हुए के साथ अच्छी तरह मेल खाते हैं।

कोडिंग का आनंद लें, और आपकी OCR पाइपलाइन हमेशा त्रुटि‑मुक्त रहे!

## आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण करने में मदद करेंगे।

- [Aspose OCR के साथ इमेज से टेक्स्ट निकालें – चरण‑दर‑चरण गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [इमेज को OCR कैसे करें – OCR इमेज रिकग्निशन में इमेज पर OCR करें](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [इमेज से टेक्स्ट निकालें – .NET के लिए Aspose.OCR के साथ OCR ऑप्टिमाइज़ेशन](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}