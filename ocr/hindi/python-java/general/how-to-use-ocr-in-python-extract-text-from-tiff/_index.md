---
category: general
date: 2026-07-05
description: Python में OCR का उपयोग करके TIFF को जल्दी से टेक्स्ट में बदलना कैसे
  करें। TIFF छवियों से टेक्स्ट निकालने और एक Python OCR इंजन बनाने के लिए OCR लाइब्रेरी
  के Python चरणों को सीखें।
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: hi
og_description: Python में OCR का उपयोग कैसे करें? यह गाइड आपको चरण‑दर‑चरण दिखाता
  है कि कैसे एक Python OCR इंजन और OCR लाइब्रेरी Python का उपयोग करके TIFF को टेक्स्ट
  में बदलें।
og_title: Python में OCR का उपयोग कैसे करें – पूर्ण TIFF टेक्स्ट निष्कर्षण
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Python में OCR का उपयोग कैसे करें – TIFF से टेक्स्ट निकालें
url: /hi/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में OCR का उपयोग कैसे करें – TIFF से टेक्स्ट निकालें

क्या आपने कभी सोचा है **Python में OCR का उपयोग कैसे करें** ताकि स्कैन की गई किताब को संपादन योग्य टेक्स्ट में बदला जा सके? आप अकेले नहीं हैं—डेवलपर्स, शोधकर्ता और शौकीन सभी मल्टी‑पेज TIFF इमेजेज़ के साथ काम करते समय इस समस्या का सामना करते हैं। अच्छी खबर? **ocr library python** के साथ आप एक छोटा OCR इंजन बना सकते हैं, इसे एक TIFF फ़ाइल पर इंगित कर सकते हैं, और कुछ सेकंड में साफ़, खोज योग्य टेक्स्ट प्राप्त कर सकते हैं।

इस ट्यूटोरियल में हम वह सब कवर करेंगे जिसकी आपको ज़रूरत है: सही पैकेज इंस्टॉल करना, मल्टी‑पेज TIFF लोड करना, OCR इंजन चलाना, और अंत में प्रत्येक पेज की सामग्री प्रिंट करना। अंत तक आप **TIFF को टेक्स्ट में बदलना** और **TIFF फ़ाइलों से टेक्स्ट निकालना** अपने Python वातावरण से बाहर निकले बिना कर पाएँगे।

## आवश्यकताएँ

- Python 3.9 या नया (उदाहरण 3.11 पर परीक्षण किया गया था)
- एक नवीनतम संस्करण का `ocr` लाइब्रेरी (या कोई भी संगत `python ocr engine` जो आप पसंद करें)
- एक मल्टी‑पेज TIFF फ़ाइल जिसे आप प्रोसेस करना चाहते हैं (हम इसे `scanned_book.tif` कहेंगे)
- Python स्क्रिप्ट्स और वर्चुअल एनवायरनमेंट्स की बुनियादी समझ

कोई भारी बाहरी टूल्स आवश्यक नहीं—सिर्फ pip और कुछ लाइनों का कोड।

## OCR लाइब्रेरी Python स्थापित करें

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** यदि आप Windows पर हैं और पैकेज नेेटिव बाइनरीज़ पर निर्भर करता है, तो सुनिश्चित करें कि आपके पास उपयुक्त Visual C++ redistributable इंस्टॉल है। इंस्टॉलर आमतौर पर आपको चेतावनी देगा यदि कुछ गायब है।

## Python में OCR इंजन का उपयोग कैसे करें

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**भाषा क्यों सेट करें?**  
अधिकांश OCR इंजन सटीकता बढ़ाने के लिए भाषा मॉडल का उपयोग करते हैं। यदि आप इस चरण को छोड़ देते हैं, तो इंजन एक सामान्य मॉडल पर वापस आ जाता है जो विराम चिह्न या विशेष अक्षरों को गलत पहचान सकता है।

## मल्टी‑पेज TIFF इमेज लोड करें

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Edge case:** यदि आपका TIFF संपीड़न (CCITT Group 4, LZW, आदि) का उपयोग करता है और लाइब्रेरी त्रुटि देती है, तो पहले ImageMagick से इसे अनकम्प्रेस्ड संस्करण में बदलने की कोशिश करें:  
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## सभी पृष्ठों पर OCR चलाएँ – TIFF को टेक्स्ट में बदलें

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**अंदर क्या हो रहा है?**  
`recognize_multi_page` फ़ंक्शन प्रत्येक रास्टराइज़्ड पेज पर इटररेट करता है, न्यूरल‑नेटवर्क रेकग्नाइज़र चलाता है, और प्लेन‑टेक्स्ट आउटपुट को कॉन्फिडेंस स्कोर के साथ पैकेज करता है। यह मूल रूप से एक बैच ऑपरेशन है जो आपको मैन्युअल लूप लिखने से बचाता है।

## परिणामों के माध्यम से इटररेट करें – TIFF से टेक्स्ट निकालें

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### अपेक्षित आउटपुट

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

प्रत्येक `result.text` स्ट्रिंग उस पेज के कच्चे OCR आउटपुट को रखती है। यदि आपको लाइन‑ब्रेक संरक्षित चाहिए, तो अधिकांश इंजन `result.lines` को स्ट्रिंग्स की सूची के रूप में एक्सपोज़ करते हैं।

## बड़े TIFF फ़ाइलों को संभालना – टिप्स और ट्रिक्स

500‑पेज TIFF को प्रोसेस करना मेमोरी‑इंटेंसिव हो सकता है। यहाँ कुछ रणनीतियाँ हैं जो चीज़ों को सुगम रखती हैं:

1. **पेजों को चंक करें** – `recognize_multi_page` के बजाय, एक जेनरेटर के अंदर `engine.recognize(page)` को कॉल करें जो एक समय में एक पेज यील्ड करता है।  
2. **DPI समायोजित करें** – इमेज रेज़ोल्यूशन कम करने (उदा., 300 DPI से 200 DPI) से CPU लोड घटता है जबकि अधिकांश प्रिंटेड टेक्स्ट की सटीकता पर न्यूनतम प्रभाव पड़ता है।  
3. **पैराललाइज़ करें** – यदि आपका OCR इंजन थ्रेड‑सेफ़ है, तो `concurrent.futures.ThreadPoolExecutor` को स्पॉन करके कई पेजों को एक साथ पहचानें।  

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## निकाले गए टेक्स्ट को फ़ाइलों में सहेजें

अधिकांश वास्तविक‑दुनिया पाइपलाइन को स्थायी स्टोरेज की ज़रूरत होती है। नीचे प्रत्येक पेज के टेक्स्ट को अपनी फ़ाइल में डंप करने का संक्षिप्त तरीका दिया गया है, पेज क्रम को संरक्षित रखते हुए।

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

अब आपके पास `.txt` फ़ाइलों की एक साफ़ डायरेक्टरी है, जो इंडेक्सिंग या आगे के NLP प्रोसेसिंग के लिए तैयार है।

## इमेज प्रीव्यू – OCR परिणामों को विज़ुअली कैसे उपयोग करें

यदि आप मूल इमेज पर OCR ओवरले देखना चाहते हैं (डिबगिंग के लिए उपयोगी), तो कई लाइब्रेरी बाउंडिंग बॉक्स ड्रॉ करने की सुविधा देती हैं। यहाँ Pillow का उपयोग करके एक त्वरित उदाहरण है:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![Python में OCR का उपयोग कैसे करें – TIFF पेज पर OCR ओवरले](ocr_overlay_example.png)

*Alt text:* Python में OCR का उपयोग कैसे करें – TIFF पेज पर OCR ओवरले।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| गड़बड़ अक्षर | गलत भाषा मॉडल | सही enum सेट करने के लिए `engine.language` सेट करें |
| पृष्ठ गायब | TIFF संपीड़न समर्थित नहीं है | पहले अनकम्प्रेस्ड TIFF में बदलें |
| धीमी प्रदर्शन | उच्च DPI + सिंगल‑थ्रेडेड प्रोसेसिंग | DPI घटाएँ या मल्टी‑थ्रेडिंग सक्षम करें |
| खाली आउटपुट | इमेज बहुत डार्क/कम कंट्रास्ट है | कॉन्ट्रास्ट स्ट्रेचिंग (`opencv` या `Pillow`) के साथ प्री‑प्रोसेस करें |

इन समस्याओं को शुरुआती चरण में हल करने से बाद में कई घंटे की डिबगिंग बचती है।

## अगले कदम – बेसिक एक्सट्रैक्शन से आगे

अब जब आप **Python में OCR का उपयोग कैसे करें** की बुनियादें समझ चुके हैं, तो आप आगे की चीज़ों को एक्सप्लोर कर सकते हैं:

- **PDF जनरेशन** – निकाले गए टेक्स्ट को `reportlab` के साथ मिलाकर सर्चेबल PDFs बनाएं।  
- **भाषा पहचान** – `langdetect` का उपयोग करके `engine.language` को ऑटो‑स्विच करें।  
- **संरचित डेटा एक्सट्रैक्शन** – रेगुलर एक्सप्रेशन या spaCy का उपयोग करके कच्चे टेक्स्ट से तिथियां, नाम, या टेबल निकालें।  
- **वैकल्पिक OCR बैकएंड्स** – यदि आपको बहुभाषी समर्थन चाहिए तो `ocr` को `pytesseract` या `easyocr` से बदलें।  

इनमें से प्रत्येक विषय स्वाभाविक रूप से द्वितीयक कीवर्ड **ocr library python**, **convert tiff to text**, **extract text from tiff**, और **python ocr engine** से जुड़ता है, जिससे आप अधिक उन्नत प्रोजेक्ट्स के लिए एक ठोस नींव बना सकते हैं।

---

### निष्कर्ष

हमने **Python में OCR का उपयोग कैसे करें** को इंस्टॉलेशन से लेकर मल्टी‑पेज प्रोसेसिंग तक कवर किया, यह दिखाते हुए कि आप कैसे **TIFF को टेक्स्ट में बदलें** और **TIFF से टेक्स्ट निकालें** एक सरल **python OCR engine** का उपयोग करके। ऊपर दिया गया पूर्ण, चलाने योग्य उदाहरण अधिकांश मानक TIFF फ़ाइलों के लिए बॉक्स से बाहर काम करेगा, और प्रदान किए गए टिप्स आपको बड़े दस्तावेज़ों या बड़े पाइपलाइन में OCR को स्केल करने में मदद करेंगे।

अपने स्कैन किए हुए किताबों, रसीदों, या अभिलेखीय इमेजेज़ के साथ इसे आज़माएँ—फिर “अगले कदम” सेक्शन में सूचीबद्ध उन्नत विचारों के साथ प्रयोग करें। Happy coding, और आपके OCR परिणाम हमेशा सटीक रहें!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [Aspose OCR के साथ इमेज से टेक्स्ट निकालें – चरण‑दर‑चरण गाइड](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Java के लिए Aspose.OCR के साथ tiff से टेक्स्ट निकालें](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Aspose OCR का उपयोग करके स्ट्रीम से इमेज टेक्स्ट एक्सट्रैक्शन कैसे करें](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}