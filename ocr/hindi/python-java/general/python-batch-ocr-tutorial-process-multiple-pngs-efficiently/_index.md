---
category: general
date: 2026-06-22
description: पायथन बैच OCR ट्यूटोरियल जो टेस्सरैक्ट और pathlib का उपयोग करके PNG छवियों
  के फ़ोल्डर पर मल्टीथ्रेडेड OCR चलाने का तरीका दिखाता है। पायथन में तेज़ बैच इमेज
  OCR सीखें।
draft: false
keywords:
- python batch ocr tutorial
- multithreaded OCR in Python
- tesseract OCR batch processing
- pathlib image handling
- OCR thread count optimization
language: hi
og_description: पायथन बैच OCR ट्यूटोरियल आपको एक पूर्ण, चलाने योग्य स्क्रिप्ट के माध्यम
  से ले जाता है जो कई PNG फ़ाइलों को टेस्सरैक्ट के साथ कई थ्रेड्स का उपयोग करके प्रोसेस
  करता है।
og_title: पायथन बैच OCR ट्यूटोरियल – PNG इमेजेज़ के लिए तेज़ मल्टीथ्रेडेड OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  headline: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  type: TechArticle
- description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  name: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  steps:
  - name: '**Collects** every PNG with **pathlib image handling**.'
    text: '**Collects** every PNG with **pathlib image handling**.'
  - name: '**Spins up** a **multithreaded OCR in Python** worker pool.'
    text: '**Spins up** a **multithreaded OCR in Python** worker pool.'
  - name: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
    text: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
  - name: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
    text: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
  type: HowTo
tags:
- OCR
- Python
- Batch Processing
title: 'पायथन बैच OCR ट्यूटोरियल: कई PNG फ़ाइलों को कुशलतापूर्वक प्रोसेस करें'
url: /hi/python-java/general/python-batch-ocr-tutorial-process-multiple-pngs-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# python batch ocr tutorial – PNG छवियों के लिए तेज़ मल्टीथ्रेडेड OCR

क्या आपने कभी सोचा है कि **python batch ocr tutorial** का उपयोग करके सैकड़ों PNG स्क्रीनशॉट्स को CPU को गरम हुए देखे बिना कैसे प्रोसेस किया जाए? आप अकेले नहीं हैं। चाहे आप स्कैन किए हुए फॉर्म को डिजिटल बना रहे हों, रसीदों से टेक्स्ट निकाल रहे हों, या एक सर्चेबल आर्काइव बना रहे हों, एक ठोस बैच OCR पाइपलाइन आपको घंटों की बचत कराती है।

इस गाइड में हम एक छोटा लेकिन शक्तिशाली स्क्रिप्ट बनाएँगे जो किसी फ़ोल्डर में सभी `*.png` फ़ाइलों को इकट्ठा करता है, उन्हें मल्टीथ्रेडेड प्रोसेसर के माध्यम से Tesseract को देता है, और साधारण‑टेक्स्ट परिणामों को एक साफ़ आउटपुट डायरेक्टरी में रखता है। कोई रहस्यमय लाइब्रेरी नहीं—सिर्फ `pathlib`, `concurrent.futures`, और भरोसेमंद `pytesseract`। अंत तक आपके पास एक **python batch ocr tutorial** होगा जिसे आप किसी भी प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं।

## आप क्या सीखेंगे

- **pathlib image handling** से इमेज फ़ाइलें कैसे इकट्ठा करें  
- **multithreaded OCR in Python** वर्कर पूल कैसे सेट‑अप करें  
- आपके CPU कोर के अनुसार **OCR thread count optimization** को कैसे ट्यून करें  
- बाद में खोज के लिए स्पष्ट नामकरण योजना के साथ प्रत्येक परिणाम को कैसे सहेजें  
- पूरे प्रोसेस को एकल, स्व‑निर्भर स्क्रिप्ट के रूप में कैसे चलाएँ  

## पूर्वापेक्षाएँ (आपको पहले क्या चाहिए)

| आवश्यकता | क्यों महत्वपूर्ण है |
|-------------|----------------|
| Python 3.9+ | आधुनिक सिंटैक्स (`pathlib`, f‑strings) |
| Tesseract 5.x स्थापित और `PATH` में उपलब्ध | `pytesseract` के पीछे का OCR इंजन |
| `pytesseract` (`pip install pytesseract`) | Tesseract के लिए Python रैपर |
| `Pillow` (`pip install pillow`) | Tesseract के लिए इमेज लोडिंग |
| वह फ़ोल्डर जिसमें आप प्रोसेस करना चाहते हैं PNG फ़ाइलें | हमारा **tesseract OCR batch processing** लक्ष्य |

> **Pro tip:** यदि आप Windows पर हैं, तो `C:\Program Files\Tesseract-OCR` को अपने सिस्टम `PATH` में जोड़ें ताकि `pytesseract` स्वचालित रूप से एक्सिक्यूटेबल को ढूँढ सके।

---

## चरण 1 – सभी PNG इमेज इकट्ठा करें (pathlib का उपयोग करके)

सबसे पहले हमें उन सभी इमेजों की सूची चाहिए जिन पर हम OCR चलाने वाले हैं। `pathlib` इसे एक‑लाइनर बनाता है और कोड को OS‑अग्नोस्टिक रखता है।

```python
import pathlib

# Adjust the path to point at your source folder
source_dir = pathlib.Path("YOUR_DIRECTORY/batch_images")
image_files = list(source_dir.glob("*.png"))

print(f"Found {len(image_files)} PNG files to process.")
```

*`pathlib` क्यों?* यह Windows बैकस्लैश और Unix स्लैश के अंतर को छुपा देता है, जिससे वही स्क्रिप्ट हर जगह चलती है। यह हमारे ट्यूटोरियल में **pathlib image handling** का मूल स्तंभ है।

---

## चरण 2 – एक सरल बैच OCR प्रोसेसर क्लास परिभाषित करें

नीचे एक हल्का रैपर है जो थ्रेडिंग बायलरप्लेट को छुपाता है। यह वही स्यूडो‑कोड दिखाता है जो आपने पहले देखा था, लेकिन पूरी तरह कार्यात्मक है।

```python
import concurrent.futures
import pytesseract
from PIL import Image
import os

class BatchOcrProcessor:
    """Encapsulates multithreaded OCR logic."""

    def __init__(self):
        self.thread_count = os.cpu_count() or 4  # sensible default
        self.output_folder = pathlib.Path("ocr_results")
        self.output_folder.mkdir(parents=True, exist_ok=True)

    def set_thread_count(self, count: int):
        """Adjust the number of worker threads (OCR thread count optimization)."""
        if count < 1:
            raise ValueError("Thread count must be at least 1")
        self.thread_count = count
        print(f"Thread pool size set to {self.thread_count}")

    def set_output_folder(self, folder: str):
        """Where each OCR result will be saved (tesseract OCR batch processing)."""
        self.output_folder = pathlib.Path(folder)
        self.output_folder.mkdir(parents=True, exist_ok=True)
        print(f"Output folder set to {self.output_folder}")

    def _process_single(self, image_path: pathlib.Path):
        """Run OCR on a single image and write the text file."""
        try:
            img = Image.open(image_path)
            text = pytesseract.image_to_string(img)
            out_file = self.output_folder / f"{image_path.stem}.txt"
            out_file.write_text(text, encoding="utf-8")
            return f"✅ {image_path.name} → {out_file.name}"
        except Exception as exc:
            return f"❌ {image_path.name} failed: {exc}"

    def process(self, image_paths):
        """Run OCR on the entire batch using a thread pool."""
        print("🚀 Starting batch OCR...")
        with concurrent.futures.ThreadPoolExecutor(max_workers=self.thread_count) as executor:
            results = list(executor.map(self._process_single, image_paths))
        for line in results:
            print(line)
        print("🏁 Batch OCR completed.")
```

**मुख्य विकल्पों की व्याख्या**

- **ThreadPoolExecutor** हमें I/O‑बाउंड टास्क जैसे फ़ाइल पढ़ना और बाहरी Tesseract बाइनरी को कॉल करने के लिए वास्तविक मल्टीथ्रेडिंग देता है।  
- `set_thread_count` मेथड वह जगह है जहाँ आप **OCR thread count optimization** के साथ प्रयोग कर सकते हैं; अधिक थ्रेड अक्सर तेज़ थ्रूपुट देते हैं जब तक आपका CPU कोर संतृप्त न हो जाए।  
- प्रत्येक इमेज एक `.txt` फ़ाइल बनाती है जिसका नाम मूल PNG के समान होता है—बाद में इंडेक्सिंग या सर्च के लिए एकदम उपयुक्त।

---

## चरण 3 – सब कुछ आपस में जोड़ें

अब हम प्रोसेसर को इंस्टैंशिएट करते हैं, थ्रेड काउंट को ट्यून करते हैं, आउटपुट फ़ोल्डर सेट करते हैं, और अंत में इमेजों की सूची को पास करते हैं।

```python
if __name__ == "__main__":
    # 1️⃣ Gather PNGs (already done above)
    # 2️⃣ Create processor instance
    ocr_processor = BatchOcrProcessor()

    # 3️⃣ Configure thread pool – feel free to change 8 → your core count
    ocr_processor.set_thread_count(8)   # multithreaded OCR in Python

    # 4️⃣ Choose where results land
    ocr_processor.set_output_folder("YOUR_DIRECTORY/ocr_results")

    # 5️⃣ Run the batch – this call blocks until everything is done
    ocr_processor.process(image_files)

    # 6️⃣ All done – a friendly console message
    print("✅ All images processed. Check the ocr_results folder.")
```

स्क्रिप्ट चलाने पर आपको इस प्रकार का आउटपुट मिलेगा:

```
Found 42 PNG files to process.
Thread pool size set to 8
Output folder set to YOUR_DIRECTORY/ocr_results
🚀 Starting batch OCR...
✅ invoice_001.png → invoice_001.txt
✅ receipt_2023-04-15.png → receipt_2023-04-15.txt
...
🏁 Batch OCR completed.
✅ All images processed. Check the ocr_results folder.
```

प्रत्येक `.txt` में कच्चा OCR आउटपुट होता है। कोई भी फ़ाइल खोलें और आप निकाले गए टेक्स्ट को इंडेक्सिंग, सेंटिमेंट एनालिसिस, या अगली प्रक्रिया के लिए तैयार देखेंगे।

---

## चरण 4 – सामान्य समस्याएँ और उनके समाधान

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| खाली `.txt` फ़ाइलें | Tesseract भाषा डेटा नहीं पा रहा या इमेज बहुत डार्क है | भाषा पैकेज (`tesseract-ocr-eng`) इंस्टॉल करें और इमेज को प्री‑प्रोसेस करें (कॉन्ट्रास्ट बढ़ाएँ)। |
| परिणाम पढ़ते समय `UnicodeDecodeError` | आउटपुट में non‑UTF‑8 कैरेक्टर हैं | फ़ाइलों को `encoding="utf-8"` के साथ लिखें (कोड में पहले से है) या जल्दी‑समाधान के लिए `errors="ignore"` उपयोग करें। |
| CPU स्पाइक, गति नहीं बढ़ रही | थ्रेड काउंट भौतिक कोर से अधिक है | `set_thread_count` को `os.cpu_count()` या उससे कम पर घटाएँ। |
| इमेज खोलते समय `FileNotFoundError` | Windows पर पाथ में non‑ASCII कैरेक्टर हैं | स्ट्रिंग को `r` प्रीफ़िक्स दें या सीधे `pathlib` ऑब्जेक्ट्स का उपयोग करें (जैसा हम करते हैं)। |

---

## चरण 5 – ट्यूटोरियल का विस्तार (आगे के कदम)

- **OpenCV (`cv2`)** के साथ इमेज प्री‑प्रोसेसिंग जोड़ें ताकि OCR की सटीकता बढ़े (जैसे, डेस्क्यू, थ्रेशहोल्ड)।  
- **multiprocessing** या RabbitMQ जैसी टास्क क्यू का उपयोग करके मशीन‑स्तर पर पैराललाइज़ करें, बड़े वर्कलोड के लिए।  
- **Elasticsearch** जैसे सर्च इंजन के साथ इंटीग्रेट करें ताकि निकाला गया टेक्स्ट रियल‑टाइम में सर्चेबल हो।  
- यदि आप हाथ‑लिखित टेक्स्ट पर उच्च सटीकता चाहते हैं, तो **Google Vision**, **Azure Computer Vision** जैसी क्लाउड OCR API के साथ Tesseract को बदलें।

इन सभी विचारों का आधार वही है जो आपके पास अब है: एक साफ़, **python batch ocr tutorial** जो बॉक्स से बाहर काम करता है।

---

## निष्कर्ष

आपने अभी एक पूर्ण **python batch ocr tutorial** बनाया है जो:

1. **pathlib image handling** से हर PNG इकट्ठा करता है।  
2. **multithreaded OCR in Python** वर्कर पूल को स्पिन‑अप करता है।  
3. आपके हार्डवेयर के अनुसार थ्रेड्स की संख्या को **OCR thread count optimization** के साथ अनुकूलित करता है।  
4. प्रत्येक परिणाम को एक समर्पित फ़ोल्डर में लिखता है (**tesseract OCR batch processing**)।  

यह स्क्रिप्ट किसी भी पाइपलाइन में डालने के लिए तैयार है—चाहे आप रसीदें, कानूनी दस्तावेज़, या स्क्रीनशॉट्स की पहाड़ी प्रोसेस कर रहे हों। थ्रेड काउंट के साथ प्रयोग करें, इमेज प्री‑प्रोसेसिंग जोड़ें, या आउटपुट को डेटाबेस से कनेक्ट करें—आपका चयन।

कोई प्रश्न हैं? नीचे टिप्पणी करें, और कोडिंग का आनंद लें!

![Workflow diagram of python batch ocr tutorial processing multiple PNG files in parallel](/images/python-batch-ocr-workflow.png){.center width=600 alt="python batch ocr tutorial workflow"}

---


## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकें।

- [Aspose OCR Tutorial – Optical Character Recognition](/ocr/english/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}