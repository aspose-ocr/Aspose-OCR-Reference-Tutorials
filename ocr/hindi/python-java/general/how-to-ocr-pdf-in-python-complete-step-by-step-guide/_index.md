---
category: general
date: 2026-06-06
description: Python का उपयोग करके PDF को OCR कैसे करें, PDF से टेक्स्ट निकालें, स्कैन
  किए गए PDF टेक्स्ट को बदलें, और कुछ ही लाइनों के कोड में OCR भाषा बदलें।
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: hi
og_description: 'Python के साथ PDF को OCR कैसे करें: एक व्यावहारिक गाइड जो आपको दिखाता
  है कि PDF से टेक्स्ट कैसे निकालें, स्कैन किए गए PDF टेक्स्ट को कैसे बदलें, और OCR
  भाषा को आसानी से कैसे बदलें।'
og_title: Python में PDF को OCR कैसे करें – पूर्ण प्रोग्रामिंग ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Python में PDF को OCR कैसे करें – पूर्ण चरण‑दर‑चरण मार्गदर्शिका
url: /hi/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में PDF को OCR कैसे करें – पूर्ण चरण‑दर‑चरण गाइड

क्या आपने कभी **how to OCR PDF** फ़ाइलों को महंगे SaaS टूल्स के बिना करने के बारे में सोचा है? आप अकेले नहीं हैं। चाहे आप पुरानी किताबों को डिजिटल बना रहे हों, इनवॉइस से डेटा निकाल रहे हों, या सिर्फ स्कैन किए गए रिपोर्ट से खोज योग्य टेक्स्ट चाहिए, Python में PDF OCR में महारत हासिल करने से आप मैन्युअल कॉपी‑पेस्ट में घंटों बचा सकते हैं।

इस ट्यूटोरियल में हम एक संक्षिप्त, कार्यशील उदाहरण के माध्यम से चलेंगे जो **extracts text from PDF** करता है, आपको दिखाता है कि **convert scanned PDF text** को संपादन योग्य स्ट्रिंग्स में कैसे बदलें, और यहां तक कि यह भी दर्शाता है कि **change OCR language** कैसे करें यदि आपका दस्तावेज़ अंग्रेज़ी में नहीं है। अंत तक आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं।

## आवश्यकताएँ और सेटअप

Before we dive in, make sure you have:

- Python 3.8+ स्थापित हो (कोड 3.9, 3.10 और नए संस्करणों पर काम करता है)
- `ocr` पैकेज जो `OcrEngine` क्लास प्रदान करता है (आप इसे `pip install ocr-lib` के माध्यम से इंस्टॉल कर सकते हैं – इसे अपने वास्तविक पैकेज नाम से बदलें)
- एक PDF फ़ाइल जिसे आप प्रोसेस करना चाहते हैं; डेमो के लिए हम `high_res_book.pdf` का उपयोग करेंगे जो `YOUR_DIRECTORY` नामक फ़ोल्डर में रखी होगी

If you’re using a virtual environment (highly recommended), activate it first:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **Pro tip:** अपने PDF फ़ाइलों को एक समर्पित `data/` डायरेक्टरी में रखें ताकि बाद में पाथ‑संबंधी समस्याओं से बचा जा सके।

## चरण 1: OCR इंजन इंस्टेंस बनाएं (How to OCR PDF – Initialization)

जब आप **perform OCR on PDF** फ़ाइलों पर OCR करना चाहते हैं, तो आपको सबसे पहला काम इंजन को इंस्टैंशिएट करना है। इंजन को आप मस्तिष्क की तरह सोचें जो प्रत्येक पेज को पढ़ेगा, ग्लिफ़्स की व्याख्या करेगा, और आपको साधारण टेक्स्ट वापस देगा।

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

यह क्यों महत्वपूर्ण है: बिना इंजन के आपके पास भाषा सेटिंग्स, रेंडरिंग विकल्प, या PDF हैंडलिंग के लिए कोई संदर्भ नहीं होगा। `OcrEngine` ऑब्जेक्ट इन सभी डिफ़ॉल्ट्स को रखता है और आपको बाद में उन्हें समायोजित करने देता है।

## चरण 2: पहचान भाषा सेट करें (Change OCR Language)

अधिकांश OCR लाइब्रेरीज़ डिफ़ॉल्ट रूप से अंग्रेज़ी का उपयोग करती हैं, लेकिन अगर आपका दस्तावेज़ फ्रेंच, जर्मन, या यहाँ तक कि जापानी में है तो क्या? भाषा बदलना इतना सरल है जितना `set_recognition_language` को कॉल करना। यह **change OCR language** आवश्यकता को पूरा करता है और उच्च सटीकता सुनिश्चित करता है।

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **Why you might need this:** एक बहुभाषी अभिलेखागार अक्सर मिश्रित‑भाषा वाले पेज़ रखता है। भाषा को तुरंत बदलने से “ß” या “ñ” जैसे अक्षरों की गलत पहचान से बचा जा सकता है।

## चरण 3: PDF रेंडरिंग विकल्प कॉन्फ़िगर करें (Convert Scanned PDF Text Effectively)

स्कैन किए गए PDFs से निपटते समय, रिज़ॉल्यूशन और कलर मोड OCR गुणवत्ता को बहुत प्रभावित करते हैं। अधिकांश दस्तावेज़ों के लिए 300 DPI पर ग्रेस्केल में रेंडर करना एक आदर्श बिंदु है—विवरण पकड़ने के लिए पर्याप्त उच्च, लेकिन मेमोरी उपयोग को उचित रखने के लिए पर्याप्त कम।

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

चेन किए गए कॉल्स दिखने में फैंसी लग सकते हैं, लेकिन वे केवल एक फ्लुएंट API हैं जो हर बार वही ऑप्शन ऑब्जेक्ट रिटर्न करता है। यदि आपको रंग चाहिए (जैसे रंगीन डायग्राम के लिए), तो `"grayscale"` को `"color"` से बदल दें।

## चरण 4: PDF को पहचानें और पहले पेज का टेक्स्ट प्राप्त करें (Extract Text from PDF)

अब **how to OCR PDF** का मूल भाग आता है: इंजन को फ़ाइल पाथ देना और पहचाने गए टेक्स्ट को निकालना। यह मेथड पेज परिणामों की एक सूची लौटाता है; प्रत्येक परिणाम में एक `text` एट्रिब्यूट होता है।

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

यदि आपको पूरा दस्तावेज़ चाहिए, तो `results` पर इटररेट करें:

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### यदि PDF एन्क्रिप्टेड है तो क्या करें?

कुछ PDFs पासवर्ड‑सुरक्षित होते हैं। ऐसे में आप पासवर्ड को `recognize_pdf` में पास कर सकते हैं:

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

इंजन OCR करने से पहले तुरंत डिक्रिप्ट कर देगा—कोई अतिरिक्त कदम आवश्यक नहीं।

## चरण 5: निकाले गए टेक्स्ट की पोस्ट‑प्रोसेसिंग (Fine‑Tuning Extract Text from PDF)

कच्चा OCR आउटपुट अक्सर लाइन ब्रेक, अतिरिक्त स्पेस, या कभी‑कभी गलत पहचाने गए अक्षर रखता है। एक त्वरित क्लीन‑अप रूटीन निकाले गए स्ट्रिंग को डाउनस्ट्रीम प्रोसेसिंग (सर्च इंडेक्सिंग, डेटाबेस स्टोरेज, आदि) के लिए तैयार करता है।

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

अब आप सुरक्षित रूप से **extract text from PDF** कर सकते हैं और इसे किसी भी NLP पाइपलाइन, सर्च इंजन, या साधारण `open(...).write()` ऑपरेशन में फीड कर सकते हैं।

## बोनस: कई PDFs की बैच प्रोसेसिंग (Scaling Perform OCR on PDF)

यदि आपके पास स्कैन किए गए PDFs से भरा फ़ोल्डर है, तो लॉजिक को एक लूप में रैप करें:

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

यह स्निपेट दिखाता है कि कैसे **perform OCR on PDF** फ़ाइलों को बड़े पैमाने पर किया जाए, जो डिजिटलाइजेशन प्रोजेक्ट्स की आम आवश्यकता है।

## अपेक्षित आउटपुट

सिंगल‑पेज उदाहरण (चरण 4) चलाने पर कुछ इस तरह का आउटपुट प्रिंट होना चाहिए:

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

यदि आपने मल्टी‑पेज बुक प्रोसेस की, तो कंसोल प्रत्येक पेज के साफ़ किए गए टेक्स्ट को दिखाएगा, और बैच स्क्रिप्ट हर PDF के बगल में एक `.txt` फ़ाइल छोड़ देगी।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| समस्या | लक्षण | समाधान |
|-------|----------|-----|
| कम‑रिज़ॉल्यूशन स्रोत PDF | गड़बड़ अक्षर, गायब शब्द | DPI बढ़ाएँ (`set_dpi(400)` या अधिक) |
| गलत भाषा सेट | बहुत सारे अज्ञात प्रतीक, विशेषकर उच्चारण वाले अक्षर | उपयोग करें `engine.set_recognition_language(ocr.Language.FRENCH)` या उपयुक्त enum |
| बड़ी PDF से मेमोरी त्रुटि | `MemoryError` या कुछ पेज़ के बाद क्रैश | पेज़ को चंक्स में प्रोसेस करें (`engine.recognize_pdf(..., max_pages=10)`) |
| PDF में फ़ॉन्ट्स गायब | कुछ पेज़ के लिए खाली आउटपुट | सुनिश्चित करें कि PDF वास्तव में रास्टर इमेजेज़ रखता है; कुछ PDFs केवल वेक्टर होते हैं और अलग हैंडलिंग की आवश्यकता होती है |

## छवि चित्रण

नीचे वर्कफ़्लो का एक त्वरित दृश्य दिया गया है। alt टेक्स्ट जानबूझकर SEO‑फ़्रेंडली है।

![how to ocr pdf कार्यप्रवाह आरेख जिसमें इंजन इनिशियलाइज़ेशन, भाषा सेटिंग, रेंडरिंग विकल्प, पहचान, और टेक्स्ट एक्सट्रैक्शन](/images/ocr-workflow.png)

*यह आरेख कोड चलाने के लिए आवश्यक नहीं है, लेकिन यह विज़ुअल लर्नर्स को दिखाता है कि प्रत्येक चरण कहाँ फिट होता है।*

## निष्कर्ष

हमने Python में **how to OCR PDF** फ़ाइलों को शुरू से अंत तक कवर किया: OCR इंजन बनाना, **changing OCR language**, रेंडरिंग को **convert scanned PDF text** के लिए कॉन्फ़िगर करना, और अंत में **extracting text from PDF** को आगे उपयोग के लिए निकालना। पूर्ण, चलाने योग्य उदाहरण किसी भी प्रोजेक्ट में डालने के लिए तैयार है, और वैकल्पिक बैच स्क्रिप्ट दिखाती है कि समाधान को कैसे स्केल किया जाए।

Next, you might want to explore:

- बहुभाषी अभिलेखागार के लिए भाषा सूची पर लूप करके **perform OCR on PDF** जोड़ना।
- निकाले गए टेक्स्ट को Elasticsearch के साथ इंटीग्रेट करके पूर्ण‑टेक्स्ट सर्च करना।
- OCR का उपयोग करके मूल फ़ाइल में टेक्स्ट लेयर एम्बेड करके खोज योग्य PDFs बनाना (कई लाइब्रेरीज़ `save_as_searchable_pdf` मेथड प्रदान करती हैं)।

बिना झिझक प्रयोग करें, DPI सेटिंग्स को समायोजित करें, या किसी अलग OCR बैकएंड पर स्विच करें। मूल बातें वही रहती हैं, और अब आपके पास निर्माण के लिए एक ठोस नींव है।

कोडिंग का आनंद लें, और आपके स्कैन किए गए दस्तावेज़ अंततः खोज योग्य बन जाएँ!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोचेज़ को एक्सप्लोर करने में मदद करती हैं।

- [PDF टेक्स्ट को पहचानें – OCR ऑपरेशन्स with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Aspose.OCR का उपयोग करके भाषा के साथ इमेज टेक्स्ट को OCR कैसे करें](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [.NET में Aspose.OCR के साथ PDF को OCR कैसे करें](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}