---
category: general
date: 2026-06-28
description: Python में ऑटो‑रोटेट, बाइनराइज़ेशन और डीनॉइज़िंग के साथ OCR के लिए छवि
  को प्रीप्रोसेस करें। OCR इंजन का उपयोग करके संरचित JSON आउटपुट प्राप्त करें।
draft: false
keywords:
- preprocess image for OCR
- auto rotate image OCR
- OCR engine Python
- OCR structured JSON output
- image binarization for OCR
- denoise OCR image
language: hi
og_description: Python में ऑटो‑रोटेट, बाइनरीकरण और डीनॉइज़िंग के साथ OCR के लिए छवि
  को पूर्व‑प्रसंस्करण करें। OCR इंजन का उपयोग करके संरचित JSON निकालना सीखें।
og_title: OCR के लिए छवि का पूर्व-प्रसंस्करण – पूर्ण पायथन गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
    text: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
  - name: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
    text: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
  - name: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
    text: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
  - name: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
    text: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
  - name: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
    text: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR के लिए इमेज का प्रीप्रोसेसिंग – पूर्ण पायथन गाइड
url: /hi/python/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR के लिए इमेज प्रीप्रोसेस – पूर्ण Python गाइड

क्या आपने कभी सोचा है कि **preprocess image for OCR** कैसे किया जाए ताकि इंजन वास्तव में वही पढ़े जो आप देखते हैं? आप अकेले नहीं हैं—अधिकांश डेवलपर्स को वही समस्या आती है जब उनके स्कैन किए गए दस्तावेज़ गड़बड़ निकलते हैं। अच्छी खबर? कुछ सही‑से कदम—auto‑rotate, binarization, और denoising—एक गंदे फोटो को साफ़, मशीन‑पठनीय टेक्स्ट में बदल सकते हैं।

इस ट्यूटोरियल में हम एक **Python** वर्कफ़्लो को देखेंगे जो न केवल इमेज को साफ़ करता है बल्कि आपको एक सुंदर संरचित JSON फ़ाइल भी देता है। अंत तक आप जानेंगे कि OCR के लिए इमेज को auto‑rotate कैसे करें, OCR के लिए इमेज binarization कैसे लागू करें, और यहां तक कि OCR इमेज डेटा को denoise करके **OCR engine Python** इंस्टेंस को फीड करने से पहले।

## आपको क्या चाहिए

- Python 3.9+ (कोई भी नवीनतम संस्करण काम करेगा)
- `Pillow` इमेज हैंडलिंग के लिए (`pip install pillow`)
- `ocrutil` – एक काल्पनिक यूटिलिटी लाइब्रेरी जो OCR इंजन को रैप करती है (इंस्टॉल करने के लिए `pip install ocrutil`)
- एक सैंपल skewed इमेज (`skewed.jpg`) जिसे आप किसी फ़ोल्डर में रख सकते हैं

बस इतना ही—कोई भारी फ्रेमवर्क नहीं, कोई GPU जादू नहीं। सिर्फ plain‑vanilla Python और कुछ उपयोगी लाइब्रेरीज़।

## चरण 1: अपनी इमेज लोड करें – OCR के लिए तैयारी

सबसे पहले: हमें एक इमेज ऑब्जेक्ट चाहिए जिसे बाकी पाइपलाइन प्रोसेस कर सके।

```python
from PIL import Image
import ocrutil

# Load the image you want to process
img_path = "YOUR_DIRECTORY/skewed.jpg"
img = Image.open(img_path)          # Pillow gives us a convenient Image object
print(f"Loaded image size: {img.size}")
```

*Why this matters:* Pillow से इमेज लोड करने से हम सभी मूल पिक्सेल डेटा को बरकरार रखते हैं, जो बाद में binarization लागू करने पर बहुत महत्वपूर्ण है। इस चरण को छोड़ देना या कम‑क्वालिटी लोडर का उपयोग करना OCR की सटीकता को पहले ही बिगाड़ सकता है।

## चरण 2: OCR के लिए इमेज को Auto‑rotate करें (auto rotate image OCR)

फ़ोन से ली गई फोटो अक्सर झुकी या उल्टी होती है। `ocrutil.auto_rotate` हेल्पर टेक्स्ट बेसलाइन को पहचानता है और इमेज को उसी अनुसार घुमाता है।

```python
# Automatically correct 90°/180° rotation
img = ocrutil.auto_rotate(img)
print("Auto‑rotation applied.")
```

*Pro tip:* यदि आप जानते हैं कि आपके दस्तावेज़ हमेशा सीधा हैं, तो आप इसे छोड़ सकते हैं, लेकिन वास्तविक परिस्थितियों में “auto rotate image OCR” आपको बहुत सारी मैन्युअल सफ़ाई से बचाता है।

## चरण 3: OCR के लिए इमेज प्रीप्रोसेस – Binarization + Denoising

अब हम मुख्य बात पर आते हैं: **preprocess image for OCR**। दो सबसे प्रभावी ट्रिक्स हैं:

1. **Binarization** – तस्वीर को शुद्ध काली‑और‑सफ़ेद में बदलना, जो कैरेक्टर एज को तेज़ करता है।
2. **Denoising** – उन स्पॉट्स को हटाना जो OCR इंजन द्वारा ग्लीफ़ के रूप में गलत समझे जा सकते हैं।

```python
# Apply preprocessing: binarization + denoising
img = ocrutil.preprocess(img)   # Under the hood: thresholding + median filter
print("Preprocessing completed.")
```

यदि आप इस चरण के बाद इमेज को देखें (जैसे, `img.show()`), तो आपको बैकग्राउंड के साथ तीव्र कंट्रास्ट दिखेगा—बिल्कुल वही जो एक अच्छा OCR इंजन चाहता है।

## चरण 4: OCR इंजन सेट अप करें (OCR engine Python)

साफ़ इमेज हाथ में होने पर, हम OCR इंजन को इंस्टैंशिएट करते हैं। `ocrutil.OcrEngine` क्लास एक लोकप्रिय ओपन‑सोर्स OCR बैकएंड (जैसे Tesseract) को रैप करती है और एक उपयोगकर्ता‑मित्र Python API प्रदान करती है।

```python
# Create and configure the OCR engine
engine = ocrutil.OcrEngine()
engine.set_image(img)           # Feed the preprocessed image
print("Engine ready for recognition.")
```

*Why we do this:* प्रीप्रोसेस्ड इमेज को **OCR engine Python** ऑब्जेक्ट को देना सुनिश्चित करता है कि इंजन आपके द्वारा उपलब्ध कराए गए सबसे उच्च‑गुणवत्ता वाले डेटा के साथ काम करे, जिससे सीधे उच्च सटीकता मिलती है।

## चरण 5: प्लेन‑टेक्स्ट रिकग्निशन (वैकल्पिक लेकिन उपयोगी)

कभी‑कभी आपको केवल कच्चा टेक्स्ट चाहिए होता है। यह चरण वैकल्पिक है क्योंकि ट्यूटोरियल का मुख्य लक्ष्य संरचित आउटपुट है, लेकिन यह त्वरित सत्यापन के लिए उपयोगी है।

```python
# Get plain text (useful for debugging)
plain_text = engine.recognize()
print("Plain‑text output:\n", plain_text[:200])   # Print first 200 chars
```

आपको एक स्ट्रिंग दिखेगी जो मूल दस्तावेज़ जैसी दिखेगी, लेकिन बिना किसी लेआउट जानकारी के। यदि टेक्स्ट गड़बड़ दिखे, तो वापस जाएँ और प्रीप्रोसेसिंग पैरामीटर को समायोजित करें।

## चरण 6: संरचित डेटा निकालें और JSON के रूप में सेव करें (OCR structured JSON output)

आधुनिक OCR इंजनों की असली ताकत उनकी लेआउट जानकारी—टेबल्स, कॉलम्स, और यहाँ तक कि फ़ॉर्म फ़ील्ड्स—वापस देने की क्षमता में है। `engine.recognize_structured()` ठीक वही करता है, और हम परिणाम को एक साफ़ JSON फ़ाइल में डंप करेंगे।

```python
# Recognize structured data (tables, layout) and export to JSON
structured_result = engine.recognize_structured()
output_path = "YOUR_DIRECTORY/out.json"
ocrutil.save_result(structured_result, output_path)
print(f"Structured OCR result saved to {output_path}")
```

JSON का एक स्निपेट इस तरह दिख सकता है:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "type": "text",
          "bbox": [12, 34, 560, 120],
          "text": "Invoice #12345"
        },
        {
          "type": "table",
          "bbox": [15, 130, 580, 400],
          "rows": [
            ["Item", "Qty", "Price"],
            ["Widget A", "2", "$19.99"]
          ]
        }
      ]
    }
  ]
}
```

*What this gives you:* एक मशीन‑पठनीय प्रतिनिधित्व जिसे आप सीधे डेटाबेस, API, या रिपोर्टिंग टूल में फीड कर सकते हैं—अब मैन्युअल कॉपी‑पेस्ट की ज़रूरत नहीं।

## बोनस: विज़ुअल कन्फर्मेशन (Image with Alt Text)

नीचे प्रीप्रोसेसिंग पाइपलाइन की पहले‑और‑बाद की स्नैपशॉट है। देखें कैसे कंट्रास्ट बढ़ता है और शोर गायब हो जाता है।

![OCR के लिए इमेज प्रीप्रोसेस – मूल बनाम साफ़](/images/ocr_preprocess_example.png){: .align-center alt="OCR के लिए इमेज प्रीप्रोसेस उदाहरण"}

*If you’re curious:* `ocrutil.preprocess` को अपने OpenCV रूटीन से बदलें और आप अभी भी वही **preprocess image for OCR** सिद्धांत का पालन करेंगे—threshold, filter, फिर फीड।

## सामान्य गलतियाँ और उन्हें कैसे टालें

- **Over‑binarizing:** थ्रेशोल्ड बहुत अधिक सेट करने से हल्के अक्षर मिट सकते हैं। यदि आप अक्षर गायब देखते हैं, तो `ocrutil.preprocess` में थ्रेशोल्ड कम करें।
- **Wrong DPI:** OCR इंजन प्रिंटेड सामग्री के लिए लगभग 300 dpi मानते हैं। यदि आपकी इमेज कम‑रिज़ॉल्यूशन है, तो प्रीप्रोसेसिंग से पहले अप‑स्केल करने पर विचार करें।
- **Skipping auto‑rotate:** केवल 5‑डिग्री का झुकाव भी लाइन डिटेक्शन को बिगाड़ सकता है। “auto rotate image OCR” चरण सस्ता है और बाद में घंटों की डिबगिंग बचाता है।

## वर्कफ़्लो का विस्तार

अब जब आपके पास एक ठोस बेसलाइन है, आप चाह सकते हैं:

1. **Add language packs** (`engine.set_language('eng+spa')`) मल्टी‑लिंगुअल दस्तावेज़ों के लिए।  
2. **Integrate with Pandas** ताकि JSON टेबल्स को एनालिटिक्स के लिए DataFrames में बदला जा सके।  
3. **Run batch processing** एक फ़ोल्डर की इमेजेज़ पर लूप करके और परिणामों को एक मास्टर JSON फ़ाइल में जोड़कर।

इन सभी एक्सटेंशन का आधार अभी भी यही मुख्य विचार है: **preprocess image for OCR** को इंजन को कॉल करने से पहले करना।

## निष्कर्ष

आपने अभी-अभी Python में **preprocess image for OCR** करना सीख लिया है—auto‑rotate, binarize, denoise, और अंत में साफ़ इमेज को **OCR engine Python** को दिया जो प्लेन टेक्स्ट और समृद्ध **OCR structured JSON output** दोनों देता है। इन चरणों का पालन करके आप पहचान दर को काफी बढ़ा सकते हैं और ऐसा डेटा प्राप्त कर सकते हैं जो डाउनस्ट्रीम प्रोसेसिंग के लिए तैयार है।

अगले स्तर पर जाने के लिए तैयार हैं? बिल्ट‑इन `ocrutil.preprocess` को कस्टम OpenCV पाइपलाइन से बदलें, विभिन्न binarization तकनीकों के साथ प्रयोग करें, या JSON को रिपोर्टिंग डैशबोर्ड में फीड करें। संभावनाएँ असीमित हैं, और जो नींव आपने अभी बनाई है वह आपको फिर से वही इमेज‑क्वालिटी समस्याओं से बचाएगी।

कोडिंग का आनंद लें, और आपके OCR परिणाम हमेशा स्पष्ट रहें!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Aspose OCR के साथ इमेज से टेक्स्ट निकालें – चरण‑दर‑चरण गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [इमेज से टेक्स्ट निकालें – Aspose.OCR for .NET के साथ OCR ऑप्टिमाइज़ेशन](/ocr/english/net/ocr-optimization/)
- [OCR इमेज रिकग्निशन में थ्रेशोल्ड वैल्यू कैसे सेट करें](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}