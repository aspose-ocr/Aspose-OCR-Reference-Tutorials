---
category: general
date: 2026-01-12
description: Python में तेज़ी से बैच OCR इमेजेज कैसे करें और JPEG फ़ाइलों से टेक्स्ट
  निकालें। एक पूर्ण चलाने योग्य उदाहरण के साथ चरण‑दर‑चरण बैच प्रोसेसिंग सीखें।
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: hi
og_description: कैसे बैच में OCR इमेजेज़ को प्रोसेस करें और JPEG फ़ाइलों से टेक्स्ट
  निकालें। यह गाइड आपको एक पूर्ण, तुरंत चलाने योग्य Python समाधान के माध्यम से ले
  जाता है।
og_title: कैसे बैच में OCR छवियों को प्रोसेस करें – त्वरित पायथन ट्यूटोरियल
tags:
- OCR
- Python
- image processing
title: बैच में OCR इमेज कैसे करें – JPEG फ़ाइलों से टेक्स्ट निकालने के लिए तेज़ गाइड
url: /hi/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# बैच OCR इमेजेज कैसे करें – JPEG फ़ाइलों से टेक्स्ट निकालने के लिए तेज़ गाइड

क्या आपने कभी **बैच OCR इमेजेज** करने के बारे में सोचा है बिना प्रत्येक फ़ाइल के लिए अलग स्क्रिप्ट लिखे? आप अकेले नहीं हैं। कई प्रोजेक्ट्स—इनवॉइस स्कैनिंग, अभिलेख डिजिटलीकरण, या कंटेंट मॉडरेशन—में हमें एक ही बार में दर्जनों या सैकड़ों JPEG फ़ाइलों से टेक्स्ट निकालना पड़ता है। अच्छी खबर यह है कि आप इसे कुछ ही पंक्तियों के Python कोड से कर सकते हैं, और आपके पास एक पुन: उपयोग योग्य इंजन होगा जिसे आप किसी भी पाइपलाइन में डाल सकते हैं।

इस ट्यूटोरियल में हम आपको बिल्कुल **बैच OCR इमेजेज** कैसे करें दिखाएंगे, फिर JPEG फ़ाइलों से टेक्स्ट निकालने, एज केस संभालने, और आउटपुट की पुष्टि करने की प्रक्रिया बताएंगे। अंत तक आपके पास एक स्व-समाहित स्क्रिप्ट होगी जिसे आप किसी भी इमेज फ़ोल्डर पर चला सकते हैं, और आप समझेंगे कि बैच प्रोसेसिंग प्रदर्शन और मेंटेनबिलिटी के लिए क्यों महत्वपूर्ण है।

## आप क्या सीखेंगे

- एक सरल OCR इंजन सेट अप करना और इसे अंग्रेज़ी के लिए कॉन्फ़िगर करना।
- `pathlib` के साथ किसी डायरेक्टरी से सभी JPEG फ़ाइलें एकत्र करना।
- OCR इंजन को एक बार कॉल करके पूरे बैच को प्रोसेस करना।
- प्रत्येक इमेज के लिए पहचाने गए टेक्स्ट का प्रीव्यू दिखाना।
- बड़े बैच, विभिन्न भाषाओं, और सामान्य pitfalls को संभालने के टिप्स।

**Prerequisites**: Python 3.8+, `ocr` लाइब्रेरी (या कोई भी संगत रैपर), और JPEG इमेजों का एक फ़ोल्डर जिसे आप विश्लेषण करना चाहते हैं। कोई बाहरी सर्विस आवश्यक नहीं—सब कुछ लोकली चलता है।

---

## Step 1: Initialise the OCR Engine – The Core of How to Batch OCR Images

**बैच OCR इमेजेज** करने से पहले हमें एक ऐसा इंजन चाहिए जो टेक्स्ट पढ़ना जानता हो। अधिकांश लाइब्रेरीज़ में आप एक इंजन ऑब्जेक्ट बनाते हैं, वैकल्पिक रूप से भाषा सेट करते हैं, और फिर इसे हर फ़ाइल के लिए पुन: उपयोग करते हैं।

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*Why this matters*: इंजन को एक बार इनिशियलाइज़ करने से भाषा मॉडल को बार‑बार लोड करने का ओवरहेड बचता है। यह आपको सेटिंग्स (जैसे DPI, कैरेक्टर व्हाइटलिस्ट) को एक ही जगह पर ट्यून करने की सुविधा भी देता है जो पूरे बैच पर लागू होगी।

> **Pro tip**: यदि आप बहुभाषी दस्तावेज़ प्रोसेस करने की योजना बना रहे हैं, तो `ocr.Language.ENGLISH` को `ocr.Language.MULTI` में बदलें या बैच शुरू होने से पहले कई भाषा पैक लोड करें।

---

## Step 2: Gather All JPEG Files – The “Extract Text from JPEG Files” Part

अब जब इंजन तैयार है, हमें इसे बताना है कि कौन‑सी इमेजेज़ पर काम करना है। `pathlib` का उपयोग कोड को प्लेटफ़ॉर्म‑इंडिपेंडेंट और संक्षिप्त बनाता है।

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*Why this matters*: फ़ाइल सूची को पहले इकट्ठा करके, हम पूरे कलेक्शन को OCR इंजन को एक कॉल में दे सकते हैं—यही वह चीज़ है जो “बैच OCR इमेजेज” का मूल सिद्धांत है। यदि आपके पास सब‑फ़ोल्डर हैं, तो आप `glob("**/*.jpg")` को रीकर्सिव सर्च के लिए बदल सकते हैं।

> **Edge case**: यदि आपकी इमेजेज़ में मिश्रित एक्सटेंशन (`.jpeg`, `.JPG`) हैं, तो ग्लॉब पैटर्न को इस प्रकार विस्तारित करें: `image_dir.rglob("*.[jJ][pP][eE]?g")`।

---

## Step 3: Process the Whole Batch in One Call – The Real Power of Batch OCR

आधुनिक OCR लाइब्रेरीज़ अक्सर एक `process_batch` (या समान नाम) मेथड प्रदान करती हैं जो फ़ाइल पाथ्स के इटेरेबल को स्वीकार करती है। यही **बैच OCR इमेजेज** को प्रभावी ढंग से करने का दिल है।

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*Why this matters*: एकल बैच कॉल Python‑to‑C ट्रांज़िशन की संख्या घटाता है, भाषा मॉडल को मेमोरी में लोड रखता है, और अक्सर आंतरिक पैरललाइज़ेशन को सक्षम करता है। परिणाम एक ऑब्जेक्ट्स की सूची होती है—प्रत्येक में पहचाना गया टेक्स्ट और कॉन्फिडेंस स्कोर होते हैं।

> **Performance note**: बहुत बड़े बैच (हज़ारों इमेजेज़) के लिए, सूची को छोटे चंक्स (जैसे 200 फ़ाइलें) में विभाजित करने पर विचार करें ताकि मेमोरी ओवरहेड कम रहे।

---

## Step 4: Show a Preview of the Extracted Text – Quick Validation

बैच समाप्त होने के बाद, प्रत्येक परिणाम के पहले कुछ अक्षरों को देखना उपयोगी होता है। यह आपको पुष्टि करने में मदद करता है कि OCR वास्तव में आपके JPEG फ़ाइलों से टेक्स्ट निकाल रहा है।

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*Why this matters*: एक छोटा प्रीव्यू आपको स्पष्ट फेल्यर्स (जैसे खाली आउटपुट, गड़बड़ अक्षर) को हर फ़ाइल खोलने की ज़रूरत बिना पहचानने देता है। यदि आप सिस्टमेटिक समस्याएँ देखते हैं, तो इंजन सेटिंग्स को समायोजित करके बैच को फिर से चला सकते हैं।

> **Common pitfall**: नई लाइन कैरेक्टर को स्ट्रिप करना भूलने से प्रीव्यू गंदा दिख सकता है। `replace("\n", " ")` लाइन इसे साफ़ कर देती है।

---

## Full Working Example – All Steps Combined

नीचे पूरा स्क्रिप्ट दिया गया है जिसे आप कॉपी‑पेस्ट कर सकते हैं, डायरेक्टरी पाथ को समायोजित कर सकते हैं, और चला सकते हैं। यह **बैच OCR इमेजेज** वर्कफ़्लो को शुरू से अंत तक प्रदर्शित करता है।

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**Expected output** (sample):

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

यदि प्रीव्यू में अर्थपूर्ण टेक्स्ट दिखता है, तो आपने सफलतापूर्वक **JPEG फ़ाइलों से टेक्स्ट निकाला** है बैच एप्रोच का उपयोग करके।

---

## Handling Large Batches and Advanced Scenarios

### Chunking Large Workloads
हज़ारों इमेजेज़ से निपटते समय मेमोरी एक बाधा बन सकती है। सूची को छोटे चंक्स में विभाजित करें:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### Switching Languages
यदि आपके दस्तावेज़ों में फ़्रेंच या स्पेनिश है, तो बैच से पहले भाषा बदलें:

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### Saving Results to Disk
प्रिंट करने के बजाय, आप प्रत्येक OCR परिणाम को `.txt` फ़ाइल में लिखना चाह सकते हैं:

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## Conclusion

अब आप जानते हैं **बैच OCR इमेजेज** कैसे करें और एक कॉम्पैक्ट Python स्क्रिप्ट का उपयोग करके **JPEG फ़ाइलों से टेक्स्ट** विश्वसनीय रूप से निकाल सकते हैं। इंजन को एक बार इनिशियलाइज़ करके, सभी JPEG पाथ इकट्ठा करके, उन्हें एकल बैच में प्रोसेस करके, और आउटपुट का प्रीव्यू लेकर, आप गति और सरलता दोनों हासिल करते हैं। अब आप वर्कफ़्लो को विस्तारित कर सकते हैं—बहुभाषी समर्थन जोड़ें, परिणामों को डेटाबेस में स्टोर करें, या स्क्रिप्ट को बड़े डॉक्यूमेंट‑प्रोसेसिंग पाइपलाइन में इंटीग्रेट करें।

अगले कदम के लिए तैयार हैं? `ocr` लाइब्रेरी को Tesseract से बदलें, विभिन्न इमेज प्री‑प्रोसेसिंग (थ्रेशहोल्डिंग, रिसाइज़िंग) के साथ प्रयोग करें, या निकाले गए टेक्स्ट को एक नेचुरल‑लैंग्वेज‑प्रोसेसिंग मॉडल में फीड करके ऑटोमैटिक कैटेगराइज़ेशन करें। संभावनाएँ असीमित हैं, और आपके पास निर्माण के लिए एक ठोस आधार है।

हैप्पी कोडिंग, और आपके OCR बैच हमेशा त्रुटि‑मुक्त रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}