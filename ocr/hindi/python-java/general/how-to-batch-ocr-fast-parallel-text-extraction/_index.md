---
category: general
date: 2026-03-26
description: Python का उपयोग करके बैच OCR को कुशलतापूर्वक कैसे करें—छवियों और PDF
  से टेक्स्ट निकालना और समानांतर प्रोसेसिंग के साथ OCR रूपांतरण सीखें।
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: hi
og_description: बैच OCR को प्रभावी ढंग से कैसे करें—छवियों से टेक्स्ट निकालने, PDF
  OCR रूपांतरण और Python का उपयोग करके बैच OCR प्रोसेसिंग के लिए चरण‑दर‑चरण गाइड।
og_title: 'बैच OCR कैसे करें: तेज़ समानांतर पाठ निष्कर्षण'
tags:
- OCR
- Python
- Parallel Computing
title: 'बैच OCR कैसे करें: तेज़ समानांतर पाठ निष्कर्षण'
url: /hi/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# बैच OCR कैसे करें: तेज़ समानांतर टेक्स्ट निष्कर्षण

क्या आपने कभी सोचा है **how to batch ocr** जब आपके पास दर्जनों स्कैन किए हुए पेज, स्क्रीनशॉट और PDF फ़ाइलें मौजूद हों? आप अकेले नहीं हैं—ज्यादातर डेवलपर्स इसी समस्या का सामना करते हैं: प्रत्येक फ़ाइल को एक‑एक करके प्रोसेस करना एक दर्दनाक बाधा बन जाता है।  

अच्छी खबर यह है कि आप कुछ वर्कर थ्रेड्स बना सकते हैं, उन्हें सभी फ़ाइलें दे सकते हैं, और देख सकते हैं कि OCR इंजन बैच को समानांतर रूप से कैसे प्रोसेस करता है। इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने‑योग्य उदाहरण के माध्यम से चलेंगे जो **extract text from images** दिखाता है, **pdf ocr conversion** करता है, और गति के लिए **parallel ocr processing** का उपयोग करता है।

> **आपको क्या मिलेगा**  
> * एक पूरी तरह कार्यात्मक Python स्क्रिप्ट जो PNG, TIFF, PDF, और JPG फ़ाइलों की मिश्रित सूची को एक बार में प्रोसेस करती है।  
> * यह समझ कि थ्रेड पूल I/O‑बाउंड OCR कार्यों को क्यों तेज़ बनाता है।  
> * त्रुटियों, बड़े PDFs, और कस्टम थ्रेड काउंट को संभालने के टिप्स।  

## Prerequisites

Before we dive, make sure you have:

| Requirement | Reason |
|-------------|--------|
| Python 3.8+ | आधुनिक सिंटैक्स और `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | `OcrBatchProcessor` और परिणाम ऑब्जेक्ट प्रदान करता है |
| A handful of sample files (PNG, TIFF, PDF, JPG) | **extract text from images** को क्रिया में देखने के लिए |
| Basic familiarity with threads (optional) | उपयोगी लेकिन अनिवार्य नहीं |

यदि आपने अभी तक `ocr` पैकेज इंस्टॉल नहीं किया है, तो चलाएँ:

```bash
pip install ocr-lib   # replace with the actual package name
```

अब पर्यावरण तैयार है, चलिए समस्या को तोड़ते हैं।

## Step 1: Import helpers and instantiate the batch processor

पहली चीज़ जो हमें चाहिए वह है सभी OCR जॉब्स को इकट्ठा करने की जगह। `OcrBatchProcessor` क्लास ठीक यही करती है—काम के आइटम्स को कतारबद्ध करती है और आपको `Future` ऑब्जेक्ट्स की एक सूची देती है।

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Why this matters*: `as_completed` को इम्पोर्ट करने से हम प्रत्येक समाप्त जॉब पर तुरंत प्रतिक्रिया दे सकते हैं, सबसे धीमी फ़ाइल का इंतज़ार करने की बजाय। यह **batch ocr processing** का मूल है।

## Step 2: Tune the worker pool for parallel execution

डिफ़ॉल्ट रूप से प्रोसेसर संभवतः एक ही थ्रेड का उपयोग करता है, जो बैचिंग के उद्देश्य को नष्ट कर देता है। हम स्पष्ट रूप से चार वर्कर मांगते हैं—इसे अपने CPU कोर की संख्या तक बढ़ा सकते हैं।

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Pro tip*: I/O‑बाउंड कार्यों जैसे OCR के लिए, `CPU cores * 2` के बाद अक्सर रिटर्न घटने लगता है। कुछ मान आज़माएँ और सबसे उपयुक्त चुनें।

## Step 3: Queue every file you want to OCR

यहाँ हम इमेज और PDF फ़ाइलों का मिश्रित सेट जोड़ते हैं। `add` मेथड केवल पाथ को रिकॉर्ड करता है; वास्तविक कार्य तब तक शुरू नहीं होता जब तक हम बैच सबमिट नहीं करते।

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

यदि आपको पूरे फ़ोल्डर को प्रोसेस करना है, तो एक तेज़ `glob` लूप काम कर देगा:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Step 4: Fire off the jobs and collect futures

`submit_all` को कॉल करने से प्रोसेसर को हरी बत्ती मिलती है। यह `Future` ऑब्जेक्ट्स की एक सूची लौटाता है—इन्हें परिणामों के प्लेसहोल्डर समझें जो बाद में आएँगे।

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

इस चरण पर OCR इंजन बैकग्राउंड में व्यस्त है, प्रत्येक थ्रेड एक फ़ाइल को प्रोसेस कर रहा है।

## Step 5: Pull results as soon as they finish

`as_completed` का उपयोग करके हम फ्यूचर्स को उनके समाप्त होने के क्रम में इटरेट करते हैं, न कि सबमिट किए गए क्रम में। इससे हमारा स्क्रिप्ट उत्तरदायी रहता है, विशेषकर जब कुछ PDFs साधारण PNGs से अधिक समय लेते हैं।

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Expected output** (संक्षिप्त रूप में):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

प्रत्येक ब्लॉक मूल फ़ाइल के प्लेन‑टेक्स्ट प्रतिनिधित्व से मेल खाता है। यदि आप **pdf ocr conversion** कर रहे हैं, तो टेक्स्ट में प्रत्येक पेज से OCR इंजन द्वारा समझा गया सब कुछ शामिल होगा।

## Handling Edge Cases & Common Pitfalls

| Situation | What to watch for | Quick fix |
|-----------|-------------------|-----------|
| एक भ्रष्ट इमेज | `future.result()` raises `OSError` | `try/except` में लपेटें (ऊपर कोड देखें) |
| बहुत बड़े PDF ( > 100 MB ) | मेमोरी दबाव, धीमे थ्रेड्स | `thread_count` को थोड़ा बढ़ाएँ या पहले PDF को अध्यायों में विभाजित करें |
| मिश्रित भाषा दस्तावेज़ | डिफ़ॉल्ट OCR मॉडल गलत पहचान कर सकता है | यदि लाइब्रेरी समर्थन करती है तो `OcrBatchProcessor` को भाषा संकेत पास करें |
| लेआउट को संरक्षित रखने की आवश्यकता | सादा `get_text()` कॉलम खो देता है | `ocr_result.get_hocr()` या समान लेआउट‑सजग मेथड का उपयोग करें |

### Pro tip: Custom thread count based on file type

यदि आपका अधिकांश कार्यभार PDFs है, तो आप उन पर अधिक थ्रेड्स और छोटे PNGs पर कम थ्रेड्स आवंटित कर सकते हैं। कुछ लाइब्रेरीज़ आपको प्रति‑जॉब `priority` पास करने देती हैं; अन्यथा, आप दो अलग‑अलग बैच बना सकते हैं—एक इमेज के लिए, एक PDFs के लिए—और उन्हें समानांतर चलाएँ।

## Visual Overview (optional)

![बैच OCR वर्कफ़्लो आरेख](https://example.com/ocr-workflow.png "बैच OCR वर्कफ़्लो आरेख")

*यह आरेख फ़ाइल डिस्कवरी → बैच निर्माण → समानांतर निष्पादन → परिणाम एकत्रीकरण के प्रवाह को दर्शाता है।*

## Full Script You Can Copy‑Paste

नीचे पूरा प्रोग्राम है, जिसे आप सीधे `.py` फ़ाइल में पेस्ट कर सकते हैं। इसमें ऊपर के सभी स्निपेट्स शामिल हैं, साथ ही एक छोटा हेल्पर भी है जो डायरेक्टरी में समर्थित फ़ाइलों को स्वचालित रूप से खोजता है।

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

इसे `batch_ocr.py` के रूप में सेव करें, अपने स्कैन वाले फ़ोल्डर की ओर इंगित करें, और देखें कि कंसोल में निकाला गया टेक्स्ट कैसे भरता है।  

### Why this works

* **Thread pool** – OCR मुख्यतः डिस्क I/O और बाहरी इंजन कॉल्स की प्रतीक्षा करता है, इसलिए कई थ्रेड्स CPU को व्यस्त रखते हैं।  
* **`as_completed`** – आप परिणाम तुरंत प्राप्त करते हैं जब वे तैयार हों, जो UI फ़ीडबैक या स्ट्रीमिंग पाइपलाइन के लिए आदर्श है।  
* **Error isolation** – एक खराब फ़ाइल पूरी बैच को नहीं गिराएगी; `try/except` ब्लॉक विफलताओं को अलग करता है।

## Conclusion

संक्षेप में, अब आप **how to batch ocr** को Python के `concurrent.futures` और एक OCR लाइब्रेरी जो बैच प्रोसेसिंग सपोर्ट करती है, के साथ कर सकते हैं। एक उचित थ्रेड पूल कॉन्फ़िगर करके, सभी समर्थित फ़ाइलों को कतारबद्ध करके, और जैसे ही परिणाम तैयार हों उन्हें निकालकर, आप तेज़ **parallel ocr processing** प्राप्त करते हैं बिना विश्वसनीयता खोए।  

अब आप कर सकते हैं:

* आउटपुट को तेज़ दस्तावेज़ पुनःप्राप्ति के लिए सर्च इंडेक्स में जोड़ें।  
* स्क्रिप्ट को विस्तारित करके प्रत्येक परिणाम को मूल फ़ाइल के साथ एक `.txt` फ़ाइल में लिखें।  
* यदि आपका OCR लाइब्रेरी async API देता है तो बिल्ट‑इन थ्रेड पूल को `asyncio` से बदलें।  

प्रयोग जारी रखें—Tesseract, Azure Cognitive Services, या Google Vision को बदलें, और आप वही पैटर्न लागू होते देखेंगे। Happy OCR-ing!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}