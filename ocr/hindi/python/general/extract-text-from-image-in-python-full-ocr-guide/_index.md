---
category: general
date: 2026-06-25
description: Python OCR का उपयोग करके छवि से टेक्स्ट निकालें। जानें कि OCR के लिए
  छवि कैसे लोड करें, Python में OCR कैसे करें, और कुछ सरल चरणों में रसीद को JSON में
  कैसे परिवर्तित करें।
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: hi
og_description: Python OCR का उपयोग करके छवि से टेक्स्ट निकालें। यह ट्यूटोरियल आपको
  OCR के लिए छवि लोड करने, Python में OCR करने, और रसीद को JSON में बदलने की प्रक्रिया
  दिखाता है।
og_title: Python में इमेज से टेक्स्ट निकालें – पूर्ण OCR गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Python में छवि से टेक्स्ट निकालें – पूर्ण OCR गाइड
url: /hi/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज से टेक्स्ट निकालें Python में – पूर्ण OCR गाइड

क्या आपको कभी **इमेज से टेक्स्ट निकालने** की ज़रूरत पड़ी है लेकिन आप नहीं जानते थे कि कहाँ से शुरू करें? इस ट्यूटोरियल में हम आपको दिखाएंगे कि कैसे **OCR के लिए इमेज लोड करें**, **Python में OCR करें**, और **रसीद को JSON में बदलें**—सिर्फ कुछ लाइनों के कोड से।

यदि आपने कभी रसीद‑स्कैनिंग ऐप, खर्च‑ट्रैकर बनाया है, या सिर्फ डेटा एंट्री को ऑटोमेट करना चाहते हैं, तो आप देखेंगे कि इस फ्लो में महारत हासिल करना क्यों गेम‑चेंजर है। अंत तक आपके पास एक कार्यशील स्क्रिप्ट होगी जो रसीद की तस्वीर पढ़ती है और एक साफ़ JSON पेलोड आउटपुट करती है, जिसे डाउनस्ट्रीम सर्विसेज़ में इस्तेमाल किया जा सकता है।

## आप क्या सीखेंगे

हम `aocr` लाइब्रेरी को इंस्टॉल करने से लेकर रॉ रिज़ल्ट को हैंडल करने तक हर कदम को कवर करेंगे। विशेष रूप से आप सीखेंगे:

1. **OCR इंजन इंस्टेंस बनाएं** – सभी पहचान कार्यों का प्रवेश बिंदु।  
2. **OCR के लिए इमेज लोड करें** – इंजन को बताएं कि कौन सी फ़ाइल पढ़नी है।  
3. **निर्यात फ़ॉर्मेट चुनें** – JSON या XML, हम JSON चुनेंगे क्योंकि इसे उपयोग करना आसान है।  
4. **पहचान चलाएँ** – वास्तव में Python में OCR करें।  
5. **परिणाम प्रिंट या स्टोर करें** – रसीद को JSON में बदलें और आउटपुट देखें।

OCR का कोई पूर्व अनुभव आवश्यक नहीं है; बस एक बेसिक Python सेटअप और एक इमेज फ़ाइल (रसीद, फ्लायर, जो भी चाहिए) चाहिए।  

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="Python OCR का उपयोग करके इमेज से टेक्स्ट निकालने की प्रक्रिया का डायग्राम"}

## इमेज से टेक्स्ट निकालें – चरण‑दर‑चरण Python OCR

नीचे पूरा, तैयार‑चलाने‑योग्य स्क्रिप्ट दिया गया है। इसे `receipt_ocr.py` नाम की फ़ाइल में कॉपी‑पेस्ट करें और `python receipt_ocr.py` चलाएँ।

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### यह क्यों काम करता है

- **इंजन इंस्टेंस** – `aocr.OcrEngine()` सभी भारी काम (मॉडल लोडिंग, प्री‑प्रोसेसिंग, आदि) को समेटे रहता है।  
- **इमेज लोड करना** – `engine.load_image()` लाइब्रेरी को ठीक‑ठीक बताता है कि कौन सा बिटमैप विश्लेषण करना है; आप JPEG, PNG, या यहाँ तक कि मल्टी‑पेज PDFs भी फीड कर सकते हैं।  
- **निर्यात फ़ॉर्मेट** – `engine.export_format` को `aocr.ExportFormat.JSON` सेट करने से परिणाम एक संरचित स्ट्रिंग बन जाता है, जो JSON की अपेक्षा रखने वाले API के लिए परफ़ेक्ट है।  
- **पहचान कॉल** – `engine.recognize()` पर्दे के पीछे न्यूरल नेट इन्फ़रेंस चलाता है; यह एक JSON स्ट्रिंग रिटर्न करता है जिसमें डिटेक्टेड टेक्स्ट ब्लॉक्स, कॉन्फिडेंस स्कोर, और लेआउट जानकारी होती है।  

---

## aocr के साथ OCR के लिए इमेज लोड करें

यदि आप सोच रहे हैं कि इमेज को किसी विशेष प्री‑प्रोसेसिंग की ज़रूरत है या नहीं, तो छोटा जवाब **नहीं** है—`aocr` अधिकांश सामान्य मामलों (कॉन्ट्रास्ट एडजस्टमेंट, डेस्क्यूइंग) को स्वचालित रूप से संभालता है। फिर भी, आप सटीकता को बढ़ा सकते हैं:

- सुनिश्चित करें कि इमेज कम से कम 300 dpi की हो।  
- अनावश्यक बॉर्डर को क्रॉप करें।  
- फ़ीड करने से पहले ग्रेस्केल में बदलें (वैकल्पिक, `engine.load_image()` आपके लिए यह कर देगा)।

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*प्रो टिप:* यदि रसीद में बहुत शोर है, तो ऊपर दिया गया अतिरिक्त कदम **Python में OCR करने** की सटीकता को उल्लेखनीय रूप से बढ़ा सकता है।

---

## निर्यात फ़ॉर्मेट चुनें और रसीद को JSON में बदलें

आप पूछ सकते हैं, “सिर्फ प्लेन टेक्स्ट क्यों नहीं ले लेते?” क्योंकि JSON पदानुक्रमित संरचना (लाइन, शब्द, बाउंडिंग बॉक्स) को संरक्षित रखता है। इससे बाद में *कुल राशि* या *तारीख* जैसे फ़ील्ड को मैप करना बहुत आसान हो जाता है।

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

जब आप स्क्रिप्ट चलाते हैं, `json_result` कुछ इस तरह दिखेगा (संक्षिप्त रूप में):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

अब आपके पास एक **रसीद को JSON में बदलें** पेलोड है जिसे आप सीधे डेटाबेस, REST एन्डपॉइंट, या मशीन‑लर्निंग मॉडल में फीड कर सकते हैं।

---

## पहचान चलाएँ और परिणाम प्राप्त करें

अंतिम कदम—वास्तव में OCR करना—`recognize()` को कॉल करने जितना सरल है। लाइब्रेरी पर्दे के पीछे:

1. इमेज को प्री‑ट्रेन्ड कॉन्वॉल्यूशनल नेटवर्क से गुज़रती है।  
2. नेटवर्क आउटपुट को पढ़ने योग्य कैरेक्टर्स में डिकोड करती है।  
3. सब कुछ चुने हुए फ़ॉर्मेट (हमारे केस में JSON) में पैकेज कर देती है।

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

यदि आपको आउटपुट को प्रिंट करने के बजाय स्टोर करना है, तो बस इसे फ़ाइल में लिख दें:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*एज केस:* कुछ रसीदों में नॉन‑ASCII कैरेक्टर्स (जैसे “€” ) होते हैं। ऊपर दिखाए अनुसार फ़ाइल को UTF‑8 एन्कोडिंग के साथ खोलें, ताकि टेक्स्ट गड़बड़ न हो।

---

## पूर्ण कार्यशील उदाहरण (सभी चरण एक स्क्रिप्ट में)

सब कुछ एक साथ जोड़ते हुए, यहाँ अंतिम स्क्रिप्ट है जिसे आप एंड‑टू‑एंड चला सकते हैं:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

इसे इस तरह चलाएँ:

```bash
python receipt_ocr.py
```

आपको एक कन्फ़र्मेशन लाइन दिखेगी और उसी फ़ोल्डर में `receipt_output.json` फ़ाइल मिलेगी जिसमें संरचित डेटा होगा।

---

## निष्कर्ष

अब आप जानते हैं **इमेज से टेक्स्ट कैसे निकालें** Python का उपयोग करके, **OCR के लिए इमेज कैसे लोड करें**, **Python में OCR कैसे करें**, और **रसीद को JSON में कैसे बदलें** डाउनस्ट्रीम उपयोग के लिए। यह एंड‑टू‑एंड फ्लो हल्का है, केवल `aocr` पैकेज की आवश्यकता है, और इसे किसी भी ऑटोमेशन पाइपलाइन में डाला जा सकता है।

अब आगे क्या? निर्यात फ़ॉर्मेट को XML में बदलें, विभिन्न इमेज प्री‑प्रोसेसिंग तकनीकों के साथ प्रयोग करें, या एक छोटा Flask API बनाएं जो अपलोड की गई रसीद ले और तुरंत JSON पेलोड रिटर्न करे। बुनियादी बातें समझने के बाद संभावनाएँ अनंत हैं।

कोई सवाल या समस्या है? नीचे कमेंट करें, और हैप्पी कोडिंग!

## आगे आप क्या सीखें

यह गाइड में दिखाए गए तकनीकों पर आधारित निकट‑संबंधित ट्यूटोरियल्स हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Aspose OCR के साथ इमेज से टेक्स्ट निकालें – चरण‑दर‑चरण गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [इमेज से टेक्स्ट निकालें – Aspose.OCR for .NET के साथ OCR अनुकूलन](/ocr/english/net/ocr-optimization/)
- [Aspose.OCR for .NET का उपयोग करके इमेज से टेबल निकालें](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}