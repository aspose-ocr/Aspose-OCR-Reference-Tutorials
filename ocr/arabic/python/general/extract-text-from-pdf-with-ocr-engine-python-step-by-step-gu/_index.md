---
category: general
date: 2026-01-12
description: استخراج النص من ملف PDF باستخدام محرك OCR في بايثون – تعلم كيفية قراءة
  PDF باستخدام OCR، تحميل الصورة للـ OCR، والحصول على نتائج منظمة.
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: ar
og_description: استخراج النص من ملف PDF باستخدام محرك OCR في بايثون. يوضح هذا الدرس
  كيفية قراءة ملف PDF باستخدام OCR، تحميل الصورة للـ OCR، واستخدام محرك OCR في بايثون
  للحصول على نتائج موثوقة.
og_title: استخراج النص من PDF باستخدام محرك OCR بايثون – دليل شامل
tags:
- OCR
- Python
- PDF
- Text Extraction
title: استخراج النص من ملف PDF باستخدام محرك OCR في بايثون – دليل خطوة بخطوة
url: /ar/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من PDF باستخدام محرك OCR في بايثون – دليل كامل

هل احتجت يومًا إلى **استخراج النص من PDF** لكن الملف مجرد صورة ممسوحة ضوئيًا؟ لست وحدك. في العديد من المشاريع الواقعية يكون ملف PDF الذي تستلمه لا يحتوي على نص قابل للتحديد، لذا فإن الطريقة الوحيدة هي **قراءة PDF باستخدام OCR**.  

في هذا الدليل سنستعرض حلًا عمليًا من البداية إلى النهاية يوضح بالضبط كيف **نحمّل صورة للـ OCR**، ونشغّل **محرك OCR في بايثون**، ونستخرج نصًا منظمًا يمكنك إرساله إلى خطوط المعالجة اللاحقة. لا مراجع غامضة، فقط مثال كامل قابل للتنفيذ يمكنك نسخه ولصقه اليوم.

## ما ستتعلمه

- كيفية تثبيت واستيراد مكتبة OCR للبايثون التي تحتاجها.  
- الخطوات الدقيقة **لتحميل صورة للـ OCR** من ملف PDF.  
- كيفية استدعاء طريقة `recognize_structured()` للمحرك والتكرار على الكتل، السطور، والكلمات.  
- نصائح للتعامل مع النتائج ذات الثقة المنخفضة وملفات PDF متعددة الصفحات.  

بنهاية هذا الدرس سيكون لديك سكربت يَستخرج النص من مستندات PDF بثقة، سواء كان يحتوي على صفحة واحدة أو مئة صفحة.

---

![مخطط يوضح محرك OCR وهو يعالج ملف PDF ويخرج نصًا منظمًا.](images/ocr_flow.png "مخطط استخراج النص من pdf")

*نص بديل للصورة: مخطط استخراج النص من pdf يوضح خطوات معالجة OCR.*

## المتطلبات المسبقة

- Python 3.9 أو أحدث (الكود يستخدم f‑strings وتلميحات الأنواع).  
- حزمة OCR قابلة للتثبيت عبر pip وتوفر فئة `OcrEngine` (مثال خيالي: مكتبة `pyocr`).  
- ملف PDF تريد معالجته، محفوظ محليًا (مثال: `form.pdf`).  

إذا كنت تفتقد مكتبة OCR، قم بتثبيتها باستخدام:

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## الخطوة 1: استخراج النص من PDF – إعداد محرك OCR

قبل أن نتمكن من **قراءة PDF باستخدام OCR**، نحتاج إلى إنشاء نسخة من المحرك. فكر في المحرك كالعقل الذي ينظر إلى كل بكسل ويقرر أي حرف يمثل.

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **لماذا هذا مهم:** تهيئة المحرك مرة واحدة تسمح لك بإعادة استخدام حزم اللغات المحمَّلة عبر ملفات متعددة، مما يوفر الوقت والذاكرة.

---

## الخطوة 2: تحميل صورة للـ OCR – تحضير ملف PDF الخاص بك

ملف PDF ليس صورة خام، لذا عادةً ما توفر المكتبة أداة مساعدة لتحويل الصفحة الأولى (أو جميع الصفحات) إلى صورة يستطيع محرك OCR فهمها.

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **نصيحة:** إذا كان PDF يحتوي على صفحات متعددة، تسمح لك العديد من مكتبات OCR بتمرير `page=2` أو التكرار عبر `engine.load_image(pdf_path, page=n)`. للوثائق الكبيرة، فكر في معالجة الصفحات على دفعات لتجنب ارتفاع استهلاك الذاكرة.

---

## الخطوة 3: استخدام OCR Engine Python – التعرف على النص المنظم

الآن يبدأ العمل الجاد. استدعاء `recognize_structured()` يُعيد هيكلية من كتل → سطور → كلمات، كل منها مُعَلَّم باللغة، الثقة، ومربعات الإحاطة.

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **ما ستحصل عليه:**  
> - `structured_result.blocks` – حاويات المستوى الأعلى (غالبًا فقرات أو أعمدة).  
> - كل كتلة تحتوي على `lines`، وكل سطر يحتوي على `words`.  
> - درجات الثقة تتيح لك تصفية النتائج المشكوك فيها.

---

## الخطوة 4: التكرار على النتائج – الوصول إلى الكتل، السطور، والكلمات

فيما يلي حلقة مختصرة تطبع أهم المعلومات. يمكنك توسيعها لكتابة JSON أو CSV أو إدخالها إلى قاعدة بيانات.

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### النتيجة المتوقعة

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **لماذا ستحب هذا:** الهيكلية تعكس طريقة قراءة الإنسان للصفحة، مما يجعل من السهل إعادة بناء الجداول أو التخطيطات العمودية لاحقًا.

---

## الخطوة 5: معالجة الحالات الخاصة – الثقة المنخفضة وملفات PDF متعددة الصفحات

### كلمات ذات ثقة منخفضة

إذا انخفضت ثقة كلمة إلى ما دون، على سبيل المثال `0.70`، قد ترغب في وضع علامة عليها للمراجعة اليدوية:

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### معالجة جميع الصفحات

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **نصيحة احترافية:** خزن الصور الوسيطة كملفات PNG إذا كانت مكتبة OCR تُعيد رسمها في كل مرة—هذا يمكن أن يوفر ثوانٍ عند معالجة دفعات كبيرة.

---

## السكربت الكامل العامل

بدمج كل ما سبق، إليك ملف واحد يمكنك تشغيله فورًا:

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

احفظه باسم `extract_pdf_ocr.py` وشغّله:

```bash
python extract_pdf_ocr.py
```

ستظهر لك تفاصيل المستوى الكتلي في وحدة التحكم، بالإضافة إلى أي تحذيرات ثقة منخفضة.

---

## الخاتمة

لقد غطينا طريقة كاملة وجاهزة للإنتاج **لاستخراج النص من PDF** باستخدام **محرك OCR في بايثون**. بدءًا من تثبيت المكتبة، مرورًا **بتحميل صورة للـ OCR**، إلى **قراءة PDF باستخدام OCR** وأخيرًا التكرار على الإخراج المنظم، أصبح لديك الآن سكربت قابل لإعادة الاستخدام يمكنك تكييفه مع أي مشروع.

خطوات مستقبلية قد ترغب في استكشافها:

- تصدير الهيكلية إلى JSON لخطوط معالجة اللغة الطبيعية اللاحقة.  
- إضافة كشف اللغة لتبديل نماذج OCR تلقائيًا.  
- دمج `pdf2image` للمعالجة المسبقة لملفات PDF التي تحتوي على تخطيطات معقدة.  

جرّبه على دفعة فواتير متعددة الصفحات، عدّل عتبة الثقة، وشاهد مدى السرعة التي يمكنك بها تحويل ملفات PDF الممسوحة إلى نص قابل للبحث والتحرير. إذا واجهت أي صعوبات، اترك تعليقًا أدناه—نتمنى لك تجربة OCR موفقة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}