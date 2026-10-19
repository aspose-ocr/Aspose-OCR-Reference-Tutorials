---
category: general
date: 2026-03-26
description: छवि को डेस्क्यू करना, छवि से पाठ को पहचानना और स्कैन से शोर हटाने तथा
  स्कैन की गई छवि को पाठ में बदलने के लिए एक इमेज प्रीप्रोसेसिंग पाइपलाइन बनाना सीखें।
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: hi
og_description: इमेज को डेस्क्यू कैसे करें और विकृत स्कैन को खोज योग्य टेक्स्ट में
  बदलें। इस गाइड का पालन करके इमेज से टेक्स्ट पहचानें, स्कैन से शोर हटाएँ, और स्कैन
  की गई इमेज को टेक्स्ट में परिवर्तित करें।
og_title: छवि को डेस्क्यू कैसे करें – चरण-दर-चरण OCR गाइड
tags:
- OCR
- image-processing
- Python
title: इमेज को डेस्क्यू कैसे करें – OCR के साथ पूर्ण गाइड
url: /hi/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज को डेस्क्यू कैसे करें – OCR के साथ पूर्ण गाइड

क्या आपने कभी सोचा है कि सस्ते स्कैनर से निकली **how to deskew image** को कैसे डेस्क्यू किया जाए? आप अकेले नहीं हैं। एक तिरछा पृष्ठ अनपेशेवर दिखता है, और सबसे महत्वपूर्ण बात, झुकाव किसी भी OCR इंजन को **recognize text from image** करने में बाधा डाल सकता है।  

इस ट्यूटोरियल में हम एक पूर्ण **image preprocessing pipeline** के माध्यम से चलेंगे जो स्कैन को डेस्क्यू, बाइनराइज़ और डीनॉइज़ करता है, फिर इसे OCR इंजन को देता है ताकि आप **convert scanned image to text** न्यूनतम झंझट के साथ कर सकें। कोई जादू नहीं, सिर्फ सादा‑सादा Python और एक छोटी लाइब्रेरी जो भारी काम करती है।

## आपको क्या चाहिए

- Python 3.9+ (कोड 3.10 और उससे नए संस्करणों पर भी काम करता है)
- `ocr` पैकेज (इंस्टॉल करने के लिए `pip install ocr‑toolkit` – अपने वास्तविक लाइब्रेरी नाम से बदलें)
- एक स्कैन किया हुआ JPEG या PNG जो स्पष्ट रूप से तिरछा हो (उदाहरण के लिए `skewed_scan.jpg`)
- यह जानने की थोड़ी जिज्ञासा कि प्रत्येक प्रीप्रोसेसिंग स्टेप क्यों महत्वपूर्ण है

बस इतना ही। OpenCV जैसी भारी डिपेंडेंसीज़ की जरूरत नहीं है जब तक आप बाद में गहराई में जाना न चाहें।

## चरण 1: स्कैन की गई इमेज लोड करें

पहला काम फ़ाइल को मेमोरी में लाना है। यह स्टेप सीधा है लेकिन बहुत ज़रूरी—अगर पाथ गलत है, तो बाकी सब क्रैश हो जाएगा।

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Why?**  
> इमेज को लोड करने से हमें एक ऐसा ऑब्जेक्ट मिलता है जिसे `ocr.ImagePreprocessor` के साथ मैनीपुलेट किया जा सकता है। इस स्टेप को छोड़ने से पाइपलाइन वास्तविक पिक्सेल डेटा से अनभिज्ञ रह जाएगी।

## इमेज को डेस्क्यू कैसे करें और OCR के लिए तैयार करें

अब जब हमारे पास इमेज है, चलिए इसे सीधा करते हैं। `deskew()` मेथड झुकाव का एंगल अनुमान लगाता है और चित्र को क्षैतिज में वापस घुमा देता है।

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Pro tip:** यदि आपके स्कैन केवल थोड़ा ही झुके हुए हैं (≤ 3°), तो डिफ़ॉल्ट एल्गोरिद्म आमतौर पर एकदम सही होता है। अत्यधिक एंगल के लिए आपको आंतरिक पैरामीटर समायोजित करने पड़ सकते हैं—`max_angle` के लिए लाइब्रेरी डॉक्यूमेंटेशन देखें।

## इमेज को बाइनराइज़ करें – इसे ब्लैक‑एंड‑व्हाइट बनाएं

OCR इंजन उच्च कंट्रास्ट वाले इनपुट को पसंद करते हैं। चित्र को बाइनरी (ब्लैक‑एंड‑व्हाइट) रूप में बदलने से वह सूक्ष्म शेड्स हट जाता है जो कैरेक्टर पहचान को भ्रमित कर सकते हैं।

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **What’s happening?**  
> 128 से अधिक उज्ज्वल पिक्सेल सफ़ेद हो जाते हैं; बाकी सब काला बन जाता है। यदि आपका स्कैन असामान्य रूप से डार्क या लाइट है तो थ्रेशहोल्ड को समायोजित करें।

## OCR से पहले स्कैन से शोर हटाएँ

भले ही इमेज पूरी तरह से डेस्क्यू हो, उसमें स्पीकल्स, धूल या कम्प्रेशन आर्टिफैक्ट्स हो सकते हैं। ये छोटे ब्लॉब्स किसी भी OCR इंजन के लिए बड़ी समस्या बनते हैं।

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Why remove noise?**  
> शोर झूठी किनारें बनाता है जिन्हें OCR इंजन कैरेक्टर समझ सकता है। अधिकांश स्कैन के लिए छोटा रेडियस पर्याप्त होता है; बहुत ग्रेनी दस्तावेज़ों के लिए इसे बढ़ाएँ।

## इमेज प्रीप्रोसेसिंग पाइपलाइन लागू करें

सभी कॉन्फ़िगरेशन सेट हो गया है—अब हम मूल इमेज पर पाइपलाइन चलाते हैं।

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Result:** `processed_image` एक साफ़‑सुथरी, सीधी, हाई‑कंट्रास्ट बिटमैप है जो टेक्स्ट एक्सट्रैक्शन के लिए तैयार है।

## OCR इंजन के साथ इमेज से टेक्स्ट पहचानें

अब असली टेक्स्ट पढ़ने का समय है। हम OCR इंजन को इनिशियलाइज़ करते हैं, उसे हमारी पॉलिश्ड इमेज देते हैं, और रॉ स्ट्रिंग माँगते हैं।

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Expected output** (sample):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

यदि आपको गड़बड़ अक्षर दिखें, तो डेस्क्यूइंग स्टेप को दोबारा जांचें या अलग `threshold` वैल्यू के साथ प्रयोग करें।

## इमेज प्रीप्रोसेसिंग पाइपलाइन बनाना – पूर्ण स्क्रिप्ट

सब कुछ एक साथ जोड़ते हुए, यहाँ एक सिंगल, रन करने योग्य स्क्रिप्ट है जिसे आप `.py` फ़ाइल में डालकर चला सकते हैं:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Tip:** यदि आप कई फ़ाइलों को बैच में प्रोसेस करने की योजना बना रहे हैं तो पूरे कोड को एक फ़ंक्शन (`def ocr_from_file(path): …`) में रैप कर दें।

## सामान्य प्रश्न और किनारे के मामले

- **What if the image is already upright?**  
  `deskew()` मेथड लगभग शून्य एंगल का पता लगाता है और चित्र को जैसा है वैसा ही छोड़ देता है, इसलिए आप इसे हर फ़ाइल पर सुरक्षित रूप से चला सकते हैं।

- **My scan is in color—should I keep it?**  
  अधिकांश OCR कार्यों के लिए रंग का कोई मूल्य नहीं होता। बाइनराइज़ेशन इसे हटा देता है, प्रोसेसिंग तेज़ होती है और मेमोरी उपयोग घटता है।

- **Can I chain multiple preprocessing steps?**  
  बिल्कुल। `ImagePreprocessor` क्लास पाइपलाइन के लिए डिज़ाइन की गई है; आप `apply()` से पहले `sharpen()`, `contrast_enhance()` या कस्टम फ़िल्टर जोड़ सकते हैं।

- **The OCR output has stray line breaks—how to fix?**  
  स्ट्रिंग को `text.replace("\n", " ").strip()` से पोस्ट‑प्रोसेस करें या टेसरैक्ट के `--psm` मोड जैसे अधिक उन्नत लेआउट एनालिसिस लाइब्रेरी का उपयोग करें।

## अगले कदम

अब जब आप **how to deskew image** जानते हैं और आपके पास एक ठोस **image preprocessing pipeline** है, आप आगे खोज सकते हैं:

- **recognize text from image** को Flask API में इंटीग्रेट करना ताकि ऑन‑द‑फ्लाई डॉक्यूमेंट अपलोड हो सके।
- ऐतिहासिक दस्तावेज़ों की स्कैन में **remove noise from scan** का उपयोग करना जहाँ संरक्षण महत्वपूर्ण है।
- `pdfminer` या `PyMuPDF` का उपयोग करके हजारों पेज़ को बैच‑प्रोसेस करके सर्चेबल PDF आउटपुट बनाना।

विभिन्न थ्रेशहोल्ड, डीनॉइज़ रेडियस के साथ प्रयोग करने या मल्टीलिंगुअल सपोर्ट के लिए OCR बैकएंड को टेसरैक्ट में बदलने में संकोच न करें। मूल सिद्धांत वही रहता है: सीधा करें, साफ़ करें, फिर पढ़ें।

---

*हैप्पी कोडिंग! यदि आपको कोई समस्या आती है, तो नीचे कमेंट छोड़ें—मैं पाइपलाइन को फाइन‑ट्यून करने में मदद करने के लिए खुश रहूँगा।*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}