---
category: general
date: 2026-06-19
description: كيفية استخراج PDF باستخدام OCR في بايثون – دليل خطوة بخطوة يغطي استخراج
  النص من PDF، التعرف على النص من الصورة، ومثال على OCR باستخدام بايثون.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: ar
og_description: كيفية استخراج ملفات PDF باستخدام OCR في بايثون. تعلم استخراج النص
  من PDF، التعرف على النص من الصورة، وشاهد مثالًا كاملاً على OCR باستخدام بايثون.
og_title: كيفية استخراج نص PDF باستخدام OCR في بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: كيفية استخراج نص PDF باستخدام OCR في بايثون – دليل شامل
url: /ar/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج نص PDF باستخدام OCR في بايثون – دليل كامل

هل تساءلت يومًا **كيف تستخرج محتوى PDF** عندما يكون الملف مجرد صورة ممسوحة ضوئيًا؟ لست وحدك. في العديد من المشاريع الواقعية—مثل العقود، الفواتير، أو الأرشيفات التاريخية—الـ PDF الذي تستلمه لا يحتوي على نص قابل للتحديد. الخبر السار؟ بضع أسطر من بايثون يمكنها تحويل تلك الصفحات التي لا تحتوي على نص إلى نص قابل للبحث والتحرير.

في هذا الدرس سنستعرض مثالًا عمليًا **OCR Python** يقرأ PDF، يُحوِّل صفحته الأولى إلى صورة، ثم **يستخرج النص من PDF** باستخدام محرك OCR. بنهاية الدرس ستعرف بالضبط **كيفية قراءة PDF باستخدام OCR**، لماذا كل خطوة مهمة، وكيفية تعديل الكود للتعامل مع مستندات متعددة الصفحات أو لغات مختلفة.

## ما ستتعلمه

- تثبيت وإعداد مكتبة OCR موثوقة لبايثون.  
- تحويل صفحات PDF إلى صور مناسبة لـ OCR.  
- **التعرف على النص من الصورة** واستخراج سلاسل Unicode نظيفة.  
- المشكلات الشائعة (PDF منخفض الدقة، الصفحات المائلة) وكيفية تجنبها.  
- توسيع السكربت لمعالجة صفحات متعددة أو دفعات.

**المتطلبات المسبقة**: بايثون 3.8+، pip، وفهم أساسي للبيئات الافتراضية. لا تحتاج إلى خبرة سابقة في OCR—فقط اتبع الخطوات.

---

## ## كيفية استخراج نص PDF باستخدام OCR في بايثون

هذا العنوان H2 يحتوي على الكلمة المفتاحية الأساسية حيث تحب محركات البحث رؤيتها. لنبدأ مباشرةً بالكود.

### الخطوة 1 – تثبيت الحزم المطلوبة

أولًا، نحتاج إلى محرك OCR. المثال أدناه يستخدم حزمة **ocr** الشهيرة (غلاف خفيف حول Tesseract). إذا كنت تفضّل خلفية مختلفة، تبقى المفاهيم نفسها.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **نصيحة احترافية:** على لينكس، ستحتاج أيضًا إلى ملف Tesseract الثنائي: `sudo apt-get install tesseract-ocr`. يمكن لمستخدمي macOS الحصول عليه عبر Homebrew: `brew install tesseract`.

### الخطوة 2 – تهيئة محرك OCR وتحديد اللغة

الآن نقوم بتشغيل المحرك ونخبره بالبحث عن الأحرف الإنجليزية. يمكنك استبدال `ocr.Language.English` بأي رمز لغة مدعوم.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**لماذا هذا مهم:** تحديد اللغة يحسّن الدقة بشكل كبير لأن المحرك يستطيع تطبيق القواميس والنماذج الخاصة بتلك اللغة.

### الخطوة 3 – تحميل صفحة PDF كصورة

يعمل OCR على الصور النقطية، وليس على كائنات PDF. الدالة `ocr.Image.from_pdf` تُحوِّل الصفحة المختارة إلى بت ماب. عدّل `page_number` للصفحات الأخرى (فهرسة تبدأ من 0).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **حالة حدية:** إذا كان PDF يحتوي على رسومات متجهية بدلاً من صور ممسوحة، قد تحصل على رسم واضح. بالنسبة للماسحات منخفضة الدقة، فكر في زيادة DPI: `ocr.Image.from_pdf(..., dpi=300)`.

### الخطوة 4 – التعرف على النص من الصورة المُحوَّلة

هذا هو جوهر **ocr python example**. المحرك يعالج البت ماب ويعيد كائنًا يحتوي على السلسلة المستخرجة.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

الخاصية `ocr_result.text` تحتفظ بالنص العادي، مع الحفاظ على فواصل الأسطر حيثما أمكن.

### الخطوة 5 – طباعة أو حفظ النص المستخرج

أخيرًا، نعرض النتيجة. في تطبيق حقيقي ربما تكتب إلى ملف أو قاعدة بيانات.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

تشغيل السكربت يجب أن يُظهر شيئًا مثل:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

هذا هو سير عمل كامل **استخراج النص من pdf** باستخدام OCR.

---

## ## التعرف على النص من الصورة – تحسين الدقة

إذا كنت مهتمًا فقط بـ **التعرف على النص من الصورة** (مثل صورة JPEG لإيصال)، يمكنك تخطي خطوة تحويل PDF:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**نصائح للحصول على نتائج أفضل:**

- **معالجة مسبقة** للصورة: تحويلها إلى تدرج رمادي، تطبيق العتبة، أو تصحيح الميل. مكتبة Pillow تجعل ذلك سهلًا.  
- **زيادة DPI** أثناء تحويل PDF: الدقة الأعلى تعطي محرك OCR تفاصيل أكثر.  
- **تمكين إعدادات محرك OCR** لتقسيم الصفحة (`ocr_engine.config = "--psm 6"` للكتل المتجانسة).

---

## ## قراءة PDF باستخدام OCR – معالجة صفحات متعددة

معظم العقود تمتد لعدة صفحات. التكرار على كل صفحة سهل:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

هذه الدالة **تقرأ PDF باستخدام OCR**، تُدمج المخرجات، وتضيف علامة فاصل صفحة واضحة. يمكنك بعد ذلك تمرير `full_text` إلى فهرس بحث أو حفظه كملف `.txt`.

---

## ## المشكلات الشائعة وكيفية إصلاحها

| العرض | السبب المحتمل | الحل |
|---------|--------------|-----|
| أحرف مشوشة، الكثير من `?` | لغة خاطئة أو ملفات بيانات لغة مفقودة | تثبيت حزمة لغة Tesseract الصحيحة (`tesseract-ocr-<lang>`) وتعيين `ocr_engine.language`. |
| سطور مفقودة أو كلمات مقطوعة | DPI منخفض (أقل من 150) | تحويل PDF بدقة 300 DPI أو أعلى (`dpi=300`). |
| النص مائل أو مقلوب | الصفحة الممسوحة غير موجهة بشكل صحيح | استخدم `ocr.Image.deskew(page_image)` قبل التعرف. |
| معالجة بطيئة على ملفات PDF كبيرة | معالجة الصفحات تسلسليًا على خيط واحد | استخدم `concurrent.futures.ThreadPoolExecutor` للتوازي. |

---

## ## توسيع مثال OCR Python

- **تصدير إلى PDF/A**: بعد الاستخراج، يمكنك دمج النص مرة أخرى في PDF قابل للبحث باستخدام `reportlab` أو `pypdf2`.  
- **اكتشاف اللغة**: استخدم `langdetect` على ناتج OCR لتبديل `ocr_engine.language` تلقائيًا.  
- **معالجة دفعات**: استعرض دليلًا باستخدام `os.listdir` وطبق `extract_all_pages` على كل ملف.

---

## ## النتيجة المتوقعة والتحقق

عند تشغيل السكربت على مسح واضح باللغة الإنجليزية، يجب أن ترى كتلة نصية نظيفة مع علامات ترقيم صحيحة. للتحقق:

1. قارن بضع أسطر مع الصورة الممسوحة الأصلية.  
2. نفّذ عدّ كلمات بسيط (`len(ocr_result.text.split())`) للتأكد من أن المخرجات ليست فارغة.  
3. اختياريًا، مرّر النتيجة إلى مدقق إملائي مثل `pyspellchecker` لاكتشاف أخطاء OCR.

---

## الخلاصة

غطّينا **كيفية استخراج محتوى PDF** عندما يفشل التحليل التقليدي، وعرضنا مثالًا كاملًا **ocr python example**، وشرحنا كيف **نتعرف على النص من الصورة** و**نقرأ PDF باستخدام OCR** للصفحات الفردية والمتعددة. باستخدام مقتطفات الكود أعلاه يمكنك الآن تحويل أي PDF ممسوح إلى نص قابل للبحث والتحرير—دون الحاجة لإعادة كتابة يدوية.

الخطوات التالية؟ جرّب تغيير اللغة إلى الإسبانية (`ocr.Language.Spanish`) أو جرب تقنيات المعالجة المسبقة للصور لتعزيز الدقة. إذا كنت تبني نظام إدارة مستندات، فكر في فهرسة النص المستخرج باستخدام Elasticsearch للبحث الفائق السرعة.

هل لديك أسئلة أو صادفت PDF غريب؟ اترك تعليقًا، وتمنياتنا لك ببرمجة سعيدة!  

![How to extract PDF using OCR in Python](image.png "How to extract PDF using OCR in Python")


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}