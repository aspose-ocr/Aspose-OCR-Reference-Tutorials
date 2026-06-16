---
category: general
date: 2026-03-26
description: كيفية استخراج نص PDF باستخدام OCR. تعلم كيفية تحميل PDF كصورة، التعرف
  على نص PDF واستخراج النص من PDF باستخدام مثال بسيط بلغة بايثون.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: ar
og_description: كيفية استخراج نص PDF باستخدام OCR. يوضح لك هذا الدليل كيفية تحميل
  PDF كصورة، التعرف على نص PDF واستخراج النص من PDF باستخدام بايثون.
og_title: كيفية استخراج نص PDF باستخدام OCR – دليل كامل
tags:
- OCR
- Python
- PDF processing
title: كيفية استخراج نص PDF باستخدام OCR – دليل خطوة بخطوة كامل
url: /ar/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج نص PDF باستخدام OCR – دليل خطوة‑بخطوة كامل

هل تساءلت يومًا **كيف تستخرج PDF** التي هي في الواقع مجرد صور ممسوحة ضوئيًا؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يحتاجون إلى محتوى قابل للبحث لكن لديهم فقط ملفات PDF تحتوي على صور. الخبر السار؟ بضع أسطر من الشيفرة ومكتبة OCR قوية يمكنها تحويل تلك ملفات PDF المصورة إلى نص عادي في لحظة.  

في هذا الدرس سنستعرض **كيفية استخدام OCR** لتحميل PDF كصورة، التعرف على نص PDF، وأخيرًا **استخراج النص من PDF** لأي طول. في النهاية ستحصل على سكريبت قابل للتنفيذ، شرح واضح لكل خطوة، وبعض النصائح لتجنب المشكلات الشائعة.

## ما ستحتاجه

- Python 3.9 أو أحدث (الكود يعمل على 3.10+ أيضًا)  
- حزمة Python `ocr` (أو أي مكتبة OCR متوافقة تُظهر `OcrEngine`، `OcrEngineMode`، و `Imaging.Image`)  
- ملف PDF متعدد الصفحات تريد معالجته (للتجربة سنسميه `multi_page.pdf`)  
- إلمام أساسي بالبيئات الافتراضية (اختياري لكن يُنصح به)

> **نصيحة احترافية:** إذا كنت على Windows، فكر في استخدام Anaconda Prompt؛ على macOS/Linux، أمر بسيط `python -m venv venv && source venv/bin/activate` ينجز المهمة.

## الخطوة 1: تثبيت مكتبة OCR

أولاً، احصل على حزمة OCR من PyPI. المثال أدناه يستخدم حزمة `ocr` خيالية تحاكي الـ API المعروض في مقتطف الشيفرة، لكن معظم المكتبات الواقعية (مثل `pytesseract` + `pdf2image`) تتبع نفس النمط.

```bash
pip install ocr
```

إذا كنت تستخدم محركًا مختلفًا، استبدل `ocr` بالاسم المناسب (مثال: `pip install pytesseract pdf2image`).

## الخطوة 2: تهيئة محرك OCR

إنشاء مثال للمحرك هو أساس **كيفية استخراج نص PDF**. فكر في المحرك كالعقل الذي سيفسر البكسلات داخل كل صفحة PDF.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **لماذا هذا مهم:** `set_engine_mode` يتيح لك الموازنة بين السرعة والدقة. `DEFAULT` خيار متوازن؛ إذا كنت بحاجة إلى دقة أعلى، غيّر إلى `HIGH_ACCURACY` (إذا كانت المكتبة تدعم ذلك).

## الخطوة 3: تحميل PDF ككائن صورة

OCR يعمل على الصور، وليس على حاويات PDF، لذا يجب تحويل PDF إلى تمثيل صورة أولاً. طريقة `Imaging.Image.load` تتعامل مع ملفات PDF متعددة الصفحات تلقائيًا.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **حالة خاصة:** بعض المكتبات تقبل صورة صفحة واحدة فقط. في هذه الحالة، ستحتاج إلى التكرار عبر كل صفحة باستخدام `pdf2image.convert_from_path`. استدعاء `load` لدينا يج abstracts ذلك، مما يجعل **load pdf as image** سطرًا واحدًا.

## الخطوة 4: التعرف على النص في جميع الصفحات

الآن يأتي جوهر **recognize PDF text**. المحرك يمسح كل صفحة، ويعيد قائمة من كائنات النتيجة—واحدة لكل صفحة.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

كل `page_result` يحتوي على طرق مثل `get_text()` (نص عادي) و `get_confidence()` (مقياس جودة اختياري).  

> **نصيحة:** إذا كنت تحتاج فقط الصفحة الأولى، استدعِ `recognize(pdf_image[0])` بدلاً من المساعد متعدد الصفحات.

## الخطوة 5: التكرار عبر النتائج وإخراج النص المستخرج

أخيرًا، نكرر عبر النتائج، ونطبع نص كل صفحة. هذا يكمل سير عمل **extract text from PDF**.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### النتيجة المتوقعة

إذا كان `multi_page.pdf` يحتوي على ثلاث صفحات بالكلمات “Hello”، “World”، و “Python”، سترى:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

هذا كل شيء—ملف PDF الخاص بك الآن قابل للبحث بالكامل والنص جاهز للمعالجة اللاحقة (الفهرسة، تحليل المشاعر، إلخ).

## الخطوة 6: التعامل مع المشكلات الشائعة

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **إخراج فارغ** | صفحات PDF ممسوحة بدقة DPI منخفضة، مما يجعل الأحرف غير قابلة للتمييز. | قم بزيادة حجم الصورة قبل OCR: `pdf_image = pdf_image.resize(300)` (300 DPI هو الخيار المثالي). |
| **حروف غير مفهومة** | الأبجديات غير اللاتينية تحتاج إلى حزم لغات. | حمّل نموذج اللغة المناسب: `ocr_engine.load_language('spa')` للإسبانية، إلخ. |
| **استهلاك الذاكرة عند ملفات PDF الكبيرة** | تحميل جميع الصفحات مرة واحدة يستهلك الذاكرة. | عالج الصفحات على دفعات: `for img in pdf_image.split(batch=10): …` (شفرة تمثيلية). |
| **أداء بطيء** | استخدام `DEFAULT` على مستند ضخم قد يكون بطيئًا. | غيّر إلى وضع `FAST` أو شغّل OCR بالتوازي باستخدام `concurrent.futures`. |

## إضافي: حفظ النص المستخرج إلى ملف

معظم خطوط الأنابيب الواقعية تحتاج إلى حفظ النص. إليك أداة صغيرة تكتب كل شيء إلى `output.txt`.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

الآن يمكنك إدخال `output.txt` إلى محرك بحث، قاعدة بيانات، أو أي نموذج معالجة لغة طبيعية.

## تجميع كل شيء معًا – السكريبت الكامل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه، عدل مسارات الملفات، وستكون جاهزًا.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

شغّله:

```bash
python extract_pdf_ocr.py
```

يجب أن ترى محتوى كل صفحة يُطبع في وحدة التحكم، متبوعًا بتأكيد أن الملف `extracted_text.txt` تم إنشاؤه.

## الخاتمة

لقد غطينا **كيفية استخراج نص PDF** من المستندات التي تحتوي على صور فقط باستخدام محرك OCR، بدءًا من تثبيت المكتبة إلى التعامل مع نتائج متعددة الصفحات وحفظ المخرجات. الآن تعرف **كيفية استخدام OCR**، وكيفية **تحميل PDF كصورة**، وكيفية **recognize PDF text** بثقة.  

ما الخطوات التالية؟ جرّب تبديل وضع المحرك الافتراضي إلى إعداد عالي الدقة، جرب حزم اللغات لملفات PDF متعددة اللغات، أو مرّر النص المستخرج إلى فهرس بحث نص كامل مثل Elasticsearch. السماء هي الحد عندما تتقن أساسيات استخراج النص من ملفات PDF.

---

![how to extract pdf example](images/ocr_flowchart.png){alt="مخطط سير عمل استخراج PDF"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}