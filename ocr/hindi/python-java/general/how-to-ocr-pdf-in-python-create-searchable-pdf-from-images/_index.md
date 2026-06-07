---
category: general
date: 2026-06-06
description: Python का उपयोग करके PDF को OCR कैसे करें और छवियों से खोज योग्य PDF
  फ़ाइलें बनाएं। मिनटों में खोज योग्य टेक्स्ट जोड़ना और छवि को PDF/A में बदलना सीखें।
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: hi
og_description: स्टेप‑बाय‑स्टेप PDF को OCR करने का तरीका। सरल Python स्क्रिप्ट का
  उपयोग करके खोज योग्य टेक्स्ट जोड़ना और इमेज को PDF/A में बदलना सीखें।
og_title: PDF को OCR कैसे करें – खोज योग्य PDFs बनाने के लिए त्वरित गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: Python में PDF को OCR कैसे करें – छवियों से खोज योग्य PDF बनाएं
url: /hi/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF को OCR कैसे करें – स्कैन किए गए चित्रों को खोज योग्य PDF में बदलें

क्या आपने कभी सोचा है **PDF को OCR कैसे किया जाए** जब आपके पास केवल इनवॉइस या रसीद की स्कैन की हुई छवि है? आप अकेले नहीं हैं। कई कार्यालयों में आने वाले कागजात PNG या JPEG के रूप में आते हैं, और अगला कदम—उस सामग्री को खोज योग्य बनाना—एक ब्लैक‑बॉक्स जैसा लगता है।

अच्छी खबर? सिर्फ कुछ पंक्तियों के Python कोड से आप **searchable PDF** फ़ाइलें बना सकते हैं, **searchable text** जोड़ सकते हैं, और यहाँ तक कि **image को PDF/A** में बदल सकते हैं दीर्घकालिक अभिलेखीयकरण के लिए। इस ट्यूटोरियल में हम प्रत्येक चरण को समझेंगे, क्यों यह महत्वपूर्ण है, और आपको एक तैयार‑स्क्रिप्ट देंगे जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं।

> **Pro tip:** यह ही तरीका मल्टी‑पेज स्कैन पर भी काम करता है; बस फ़ाइलों पर लूप लगाएँ और इंजन बाकी काम खुद कर देगा।

---

## What You’ll Need

डुबकी लगाने से पहले, सुनिश्चित करें कि आपके मशीन पर निम्नलिखित मौजूद हैं:

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9 or newer | आधुनिक सिंटैक्स और बेहतर लाइब्रेरी समर्थन |
| `pdfium`‑based OCR engine (e.g., `pdfocr` or a commercial SDK) | इमेज पहचान और PDF/A जेनरेशन दोनों को संभालता है |
| An image file (PNG, JPEG, TIFF) you want to turn into a searchable PDF | वह स्रोत जहाँ से टेक्स्ट निकाला जाएगा |
| Write permission to the output folder | ताकि स्क्रिप्ट नया PDF सहेज सके |

यदि आपने अभी तक OCR SDK इंस्टॉल नहीं किया है, तो चलाएँ:

```bash
pip install pdfocr   # replace with your vendor's package name
```

बस इतना ही—कोई जटिल सिस्टम डिपेंडेंसी नहीं, सिर्फ एक pip install।

---

## How to OCR PDF – Overview

ऊपर से देखा जाए तो प्रक्रिया तीन सरल कार्यों में विभाजित है:

1. **Recognize** छवि के भीतर का टेक्स्ट पढ़ें जबकि मूल ग्राफ़िक्स को बरकरार रखें।  
2. **Export** OCR परिणाम को मूल छवि के साथ **searchable PDF/A** (अभिलेखीय‑अनुकूल PDF फ़्लेवर) के रूप में निर्यात करें।  
3. **Validate** यह सुनिश्चित करें कि परिणामी फ़ाइल में मूल चित्र के ऊपर चयन योग्य, खोज योग्य टेक्स्ट लेयर मौजूद है।

नीचे आप प्रत्येक चरण को कोड में देखेंगे, साथ ही कमांड्स के *क्यों* की व्याख्या भी।

---

## Step 1: Recognize Text from the Image

पहले हम OCR इंजन को पिक्सेल पढ़ने और एक result ऑब्जेक्ट लौटाने को कहते हैं, जिसमें कच्ची छवि और निकाला गया टेक्स्ट दोनों होते हैं। इसे ऐसे समझें जैसे इंजन आपके लिए इनवॉइस “पढ़” रहा हो।

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### Why this matters

- **Preserving graphics** का मतलब है कि विज़ुअल लेआउट (टेबल, लोगो, स्टैम्प) स्कैनर द्वारा कैप्चर किए गए रूप में ही रहता है।  
- `result` ऑब्जेक्ट आमतौर पर एक छिपी हुई टेक्स्ट लेयर रखता है जिसे हम बाद में PDF में एम्बेड करेंगे।  
- `recognize_image` का उपयोग `recognize_pdf` की बजाय करने से अतिरिक्त रूपांतरण चरण हट जाता है, जिससे सिंगल‑पेज इमेज की प्रोसेसिंग तेज़ होती है।

#### Common variations

- यदि आपके पास **multi‑page TIFF** है, तो फ़ाइल पाथ सीधे पास करें; अधिकांश इंजन प्रत्येक पेज को अलग इमेज मानेंगे।  
- उन PDFs के लिए जिनमें पहले से इमेज हैं, आप `engine.recognize_pdf("file.pdf")` कॉल कर सकते हैं और इस चरण को पूरी तरह छोड़ सकते हैं।

---

## Step 2: Export OCR Result as Searchable PDF/A

अब हम चरण 1 के `result` को लेते हैं और इंजन को नई फ़ाइल लिखने के लिए कहते हैं। यहाँ मुख्य फ़्लैग *PDF/A* है—PDF का ISO‑स्टैंडर्ड संस्करण जो दीर्घकालिक संरक्षण के लिए बनाया गया है।

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### Why this matters

- **Searchable PDF**: आउटपुट फ़ाइल में एक छिपी, चयन योग्य टेक्स्ट लेयर होती है। अब आप दस्तावेज़ में Ctrl + F कर सकते हैं।  
- **PDF/A compliance**: कुछ संस्थाएँ (क़ानूनी, वित्तीय) ऑडिट ट्रेल के लिए PDF/A की मांग करती हैं; यह चरण वह नियम स्वचालित रूप से पूरा करता है।  
- यह मेथड **searchable text** जोड़ता है बिना इमेज को फ्लैटन किए, इसलिए विज़ुअल फ़िडेलिटी पूरी रहती है।

#### Edge case: Need a regular PDF instead?

यदि आपको PDF/A की ज़रूरत नहीं है, तो `save_as_pdfa` को `save_as_pdf` से बदल दें। बाकी वर्कफ़्लो वही रहता है।

---

## Step 3: Verify the Searchable PDF

एक त्वरित sanity check आपको बाद में अजीब बग्स से बचाता है। उत्पन्न फ़ाइल को किसी भी PDF व्यूअर में खोलें, कोई शब्द चुनें, और सर्च फ़ंक्शन इस्तेमाल करें।

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### Expected output

जब आप स्क्रिप्ट चलाते हैं, तो कंसोल पर यह प्रिंट होता है:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

फ़ाइल खोलने पर आपको मूल इनवॉइस इमेज के साथ एक हल्की, अदृश्य टेक्स्ट लेयर दिखेगी। किसी भी शब्द को हाईलाइट करें और आप देखेंगे कि वह चयन योग्य है—**यही वह searchable text है** जो आपने अभी जोड़ी है।

---

## Adding Searchable Text to Existing PDFs (Bonus)

कभी‑कभी आपके पास पहले से एक PDF होता है लेकिन आपको उस पर **searchable text** जोड़ना होता है। वही इंजन OCR परिणाम को मौजूदा PDF पर ओवरले कर सकता है:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

यहाँ `apply_to` छिपी लेयर को मूल पेजों के साथ मर्ज करता है, जिससे आप **searchable PDF** बना सकते हैं बिना फिर से स्कैन किए।

---

## Common Pitfalls and Tips

| Pitfall | How to avoid it |
|---------|-----------------|
| **Low‑resolution source images** (< 150 dpi) | अपस्केल करें या उच्च‑रिज़ॉल्यूशन स्कैन का अनुरोध करें; 150 dpi से नीचे OCR की सटीकता काफी घट जाती है। |
| **Missing language data** | अपने OCR इंजन के लिए उपयुक्त भाषा पैक्स इंस्टॉल करें (`pip install pdfocr[eng,spa]`)। |
| **Output folder not writable** | स्क्रिप्ट को पर्याप्त अनुमतियों के साथ चलाएँ या कोई अलग डायरेक्टरी चुनें। |
| **PDF/A validation fails** | सुनिश्चित करें कि आप असमर्थित फ़ॉन्ट्स या JavaScript एम्बेड नहीं कर रहे हैं; अधिकांश SDK `save_as_pdfa` उपयोग करने पर इसे स्वचालित रूप से संभाल लेते हैं। |

---

## Full Script – One‑File Solution

नीचे एक स्व-समाहित स्क्रिप्ट है जो सब कुछ जोड़ती है। कॉपी‑पेस्ट करें, प्लेसहोल्डर पाथ बदलें, और आप **image को PDF/A में बदलने** के लिए तैयार हैं।

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**What this script does:**  
1. OCR इंजन लोड करता है।  
2. चुनी गई इमेज पढ़ता है और टेक्स्ट निकालता है।  
3. एक **searchable PDF/A** लिखता है जिसे आप तुरंत वितरित या अभिलेखित कर सकते हैं।  

इसे फ़ंक्शन में रैप करके पूरे फ़ोल्डर को प्रोसेस करने के लिए `os.listdir()` पर इटररेट करें और प्रत्येक फ़ाइल के लिए तीन चरण दोहराएँ।

---

## Next Steps & Related Topics

अब जब आप **how to OCR PDF** में महारत हासिल कर चुके हैं, तो इन आगे के विचारों को देखें:

- **Batch processing:** `concurrent.futures` का उपयोग करके दर्जनों इनवॉइस को समानांतर में OCR करें।  
- **Metadata injection:** आसान इंडेक्सिंग के लिए PDF मेटाडेटा में निर्माण तिथि या इनवॉइस नंबर जोड़ें।  
- **Hybrid PDFs:** मूल इमेज के साथ searchable text को मिलाकर “डिजिटल ट्विन” बनाएं।  
- **Alternative outputs:** यदि डाउनस्ट्रीम सिस्टम को एडिटेबल फ़ॉर्मेट चाहिए तो **DOCX** या **HTML** में एक्सपोर्ट करें।

इनमें से प्रत्येक आपके द्वारा अभी सीखे गए मूल सिद्धांतों—recognize, export, verify—पर आधारित है।

---

## Wrap‑Up

संक्षेप में, अब आप **how to OCR PDF** फ़ाइलों को सिर्फ तीन पंक्तियों के Python से **searchable PDF/A** में बदलना जानते हैं। स्क्रिप्ट भारी काम संभालती है, मूल ग्राफ़िक्स को बरकरार रखती है, और आपको एक मानक‑अनुपालन दस्तावेज़ देती है जिसे आप खोज, अभिलेख या साझा कर सकते हैं।  

अपने इनवॉइस, रसीद या स्कैन किए हुए कॉन्ट्रैक्ट के साथ इसे आज़माएँ। यदि कोई समस्या आती है, तो नीचे टिप्पणी छोड़ें या SDK की आधिकारिक डॉक्यूमेंटेशन देखें—वहाँ अक्सर अतिरिक्त उदाहरण होते हैं। Happy coding, और अब किसी भी इमेज को तुरंत खोज योग्य बनाने की नई क्षमता का आनंद लें! 

![PDF को OCR करने का उदाहरण, मूल इमेज और searchable PDF ओवरले दिखाते हुए](placeholder.png "PDF को OCR करने का उदाहरण")

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}