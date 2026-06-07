---
category: general
date: 2026-06-06
description: Aspose OCR Cloud का उपयोग करके PDF को OCR कैसे करें। PDF से टेक्स्ट निकालना,
  PDF पेज को PNG में बदलना, और Python में PDF पेज इमेज को सहेजना सीखें।
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: hi
og_description: कैसे Aspose OCR Cloud के साथ PDF को OCR करें। यह गाइड दिखाता है कि
  कैसे साधारण टेक्स्ट PDF निकालें, PDF पेज को PNG में बदलें, और PDF पेज की छवियों
  को सहेजें।
og_title: Aspose OCR क्लाउड के साथ PDF को OCR कैसे करें – चरण-दर-चरण
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Aspose OCR Cloud के साथ PDF को OCR कैसे करें – पूर्ण गाइड
url: /hi/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Cloud के साथ PDF को OCR कैसे करें – संपूर्ण गाइड

क्या आपने कभी भारी डेस्कटॉप टूल्स के साथ झगड़े बिना **PDF को OCR कैसे करें** फ़ाइलों के बारे में सोचा है? आप अकेले नहीं हैं—कई डेवलपर्स इस समस्या का सामना करते हैं जब उन्हें स्कैन किए गए दस्तावेज़ों से टेक्स्ट निकालने का तेज़, प्रोग्रामेटिक तरीका चाहिए। अच्छी खबर? Aspose OCR Cloud के साथ आप **PDF से टेक्स्ट निकाल सकते हैं**, प्रत्येक पेज को PNG में बदल सकते हैं, और यहाँ तक कि **PDF पेज इमेजेज़ को सहेज सकते हैं** बाद में उपयोग के लिए, सब कुछ एक साफ़ Python स्क्रिप्ट से।

इस ट्यूटोरियल में हम आपको वह सब कुछ बताएंगे जो आपको जानना आवश्यक है: SDK को इंस्टॉल करने, इंजन को लाइसेंस करने, और मल्टी‑पेज PDF को पहचानने से लेकर प्लेन टेक्स्ट निकालने, पेज को PNG में बदलने, और उन इमेजेज़ को डिस्क पर सहेजने तक। अंत तक आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं जिसे **PDF को OCR कैसे करें** क्षमताओं की आवश्यकता है।

## आप क्या चाहिए

- **Python 3.8+** (कोड 3.10 और उससे नए संस्करणों पर भी काम करता है)  
- एक Aspose OCR Cloud खाता – आपको एक मुफ्त ट्रायल लाइसेंस फ़ाइल (`Aspose.OCR.lic`) मिलेगी  
- `asposeocrcloud` पैकेज (`pip install asposeocrcloud`)  
- एक स्कैन किया हुआ, मल्टी‑पेज PDF जिसे आप प्रोसेस करना चाहते हैं  

बस इतना ही। कोई अतिरिक्त बाइनरी नहीं, कोई नेटिव डिपेंडेंसी नहीं, सिर्फ शुद्ध Python।

## PDF को OCR कैसे करें – सेटअप और लाइसेंस

किसी भी OCR मेथड को कॉल करने से पहले, आपको SDK को बताना होगा कि आप कौन हैं। Aspose एक हल्की लाइसेंस फ़ाइल का उपयोग करता है जिसे आप अपनी स्क्रिप्ट के लिए सुलभ स्थान पर रखते हैं।

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Pro tip:* यदि आप लाइसेंस चरण को छोड़ देते हैं, तो SDK फिर भी काम करेगा लेकिन आउटपुट इमेजेज़ में एक छोटा वॉटरमार्क एम्बेड करेगा। प्रोडक्शन के लिए यह आदर्श नहीं है।

## स्टेप 2: Aspose OCR Cloud Python SDK इंस्टॉल करें

एक टर्मिनल खोलें और चलाएँ:

```bash
pip install asposeocrcloud
```

यह पैकेज सभी आवश्यक डिपेंडेंसीज़ (requests, pillow, आदि) को खींच लेता है, इसलिए आपको कुछ और खोजने की जरूरत नहीं।

## स्टेप 3: OCR इंजन बनाएं और भाषा चुनें

इंजन ऑपरेशन का दिल है। आप Aspose द्वारा समर्थित कोई भी भाषा निर्दिष्ट कर सकते हैं; अधिकांश मामलों में English काम करता है।

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

भाषा क्यों सेट करें? क्योंकि OCR इंजन सटीकता बढ़ाने के लिए भाषा‑विशिष्ट शब्दकोशों का उपयोग करता है। यदि आप फ्रेंच PDF प्रोसेस कर रहे हैं, तो बस `ENGLISH` को `FRENCH` से बदल दें।

## स्टेप 4: अपने मल्टी‑पेज PDF की ओर इशारा करें

इंजन को उस फ़ाइल का पूरा पाथ दें जिसे आप प्रोसेस करना चाहते हैं। रिलेटिव पाथ ठीक हैं जब तक वे स्क्रिप्ट की वर्किंग डायरेक्टरी से हल हो जाते हैं।

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

सुनिश्चित करें कि फ़ाइल पढ़ी जा सकती है; अन्यथा आपको `FileNotFoundError` मिलेगा।

## स्टेप 5: OCR चलाएँ – आपको परिणामों की एक सूची मिलेगी

`recognize_pdf` को कॉल करने से एक सूची मिलती है जहाँ प्रत्येक एलिमेंट स्रोत PDF के एक पेज से मेल खाता है।

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

प्रत्येक `OcrResult` दो उपयोगी प्रॉपर्टीज़ रखता है:

* `text` – पेज का प्लेन‑टेक्स्ट प्रतिनिधित्व ( **extract plain text pdf** के लिए शानदार)
* `image` – रेंडर किए गए पेज का Pillow `Image` ऑब्जेक्ट ( **convert pdf page png** के लिए परफेक्ट)

## स्टेप 6: PDF से टेक्स्ट निकालें और पेज को PNG में बदलें

अब हम परिणामों के माध्यम से लूप करते हैं, निकाले गए टेक्स्ट को प्रिंट करते हैं, और प्रत्येक पेज का PNG संस्करण सहेजते हैं।

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### अपेक्षित कंसोल आउटपुट

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

आपको `page_1.png`, `page_2.png`, … `YOUR_DIRECTORY` में मिलेंगे। ये रास्टराइज़्ड पेज इमेजेज़ हैं जिन्हें आप डाउनस्ट्रीम इमेज‑प्रोसेसिंग पाइपलाइन में फीड कर सकते हैं।

## स्टेप 7: PDF पेज इमेजेज़ सहेजें (वैकल्पिक पोस्ट‑प्रोसेसिंग)

यदि आपको केवल इमेजेज़ चाहिए और टेक्स्ट नहीं, तो आप `print(res.text)` लाइन को स्किप कर सकते हैं। इसके विपरीत, यदि आप टेक्स्ट को अलग `.txt` फ़ाइलों में स्टोर करना चाहते हैं, तो बस एक छोटा राइट‑आउट जोड़ें:

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

यह छोटा जोड़ यह दर्शाता है कि **PDF पेज इमेजेज़ सहेजना** कितना आसान है, साथ ही निकाले गए कंटेंट को भी स्थायी बनाना।

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ रखकर, यहाँ पूरा स्क्रिप्ट है जिसे आप `ocr_pdf.py` में कॉपी‑पेस्ट कर सकते हैं:

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

इसे चलाएँ:

```bash
python ocr_pdf.py
```

आपको प्रत्येक पेज के टेक्स्ट का कंसोल डम्प और PNG फ़ाइलों की एक श्रृंखला दिखनी चाहिए

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}