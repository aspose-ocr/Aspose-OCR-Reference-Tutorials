---
category: general
date: 2026-07-05
description: استخراج جدول من صورة باستخدام OCR في بايثون. تعلم كيفية استخراج الجدول،
  تحويل الصورة إلى TSV، وإتقان تقنيات OCR للجدول باستخدام بايثون.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: ar
og_description: استخراج جدول من صورة باستخدام OCR في بايثون. يوضح هذا الدليل كيفية
  استخراج الجدول، تحويل الصورة إلى TSV، واستخدام أدوات OCR للجدول في بايثون.
og_title: استخراج جدول من صورة – تحويل الصورة إلى TSV باستخدام بايثون
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: استخراج جدول من صورة – تحويل الصورة إلى TSV باستخدام بايثون
url: /ar/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج جدول من صورة – تحويل الصورة إلى TSV باستخدام بايثون

هل تساءلت يومًا كيف تستخرج جدولًا من صورة دون أن تفقد أعصابك؟ في هذا الدرس سنستعرض **كيفية استخراج بيانات الجدول** من صورة باستخدام مكتبة `aocr`، ثم نحول تلك البيانات إلى ملف TSV منظم. لا سحر، مجرد بضع أسطر من بايثون وقليل من المعالجة اللاحقة المدعومة بالذكاء الاصطناعي.

إذا حاولت يومًا نسخ‑لصق جدول من فاتورة ممسوحة ضوئيًا أو لقطة شاشة وانتهى بك الأمر بملف فوضوي، ستقدّر لماذا يستحق نهج OCR‑المستند إتقانًا. في النهاية، ستتمكن من تمرير أي صورة لجدول إلى بايثون والحصول على قيم مفصولة بجدولة جاهزة للجداول أو قواعد البيانات.

---

## ما ستحتاجه

قبل أن نغوص، تأكد من أن لديك ما يلي على جهازك:

| المتطلبات | لماذا يهم |
|-------------|----------------|
| Python 3.9+ | حزمة `aocr` تستهدف إصدارات بايثون الحديثة. |
| مكتبة `aocr` (`pip install aocr`) | توفر محرك OCR ومعالج AI اللاحق الذي سنستخدمه. |
| ملف صورة يحتوي على جدول (PNG, JPG, إلخ) | البيانات المصدر التي سنستخرجها. |
| اختياري: بيئة افتراضية | تحافظ على عزل الاعتمادات — يُنصح بها بشدة. |

وجود هذه العناصر جاهزة يوفر عليك الانقطاعات في منتصف الدليل.

---

## تثبيت الاعتمادات

أولًا، لنقم بتثبيت أدوات OCR. افتح الطرفية ونفّذ:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **نصيحة احترافية:** إذا واجهت أخطاء في الأذونات، أضف `--user` إلى أمر `pip install` أو استخدم `pipx` للتثبيت عالميًا.

---

## الخطوة 1 – تهيئة محرك OCR

المحرك هو قلب العملية. فكر فيه كـ “العقل” الذي ينظر إلى كل بكسل ويقرر أي حرف ينتمي إلى أي مكان.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

لماذا ننشئ كائن محرك بدلاً من استدعاء دالة واحدة؟ كائن المحرك يتيح لنا إرفاق معالجات لاحقة مخصصة لاحقًا، مما يمنحنا تحكمًا دقيقًا في المخرجات — وهو أمر أساسي عندما تحتاج إلى دقة **ocr table image python**.

---

## الخطوة 2 – إرفاق معالج AI اللاحق

تأتي `aocr` مع معالج AI خفيف الوزن ينظف نتائج OCR الخام مع الحفاظ على حدود الخلايا. لا توجد وسائط إضافية مطلوبة، مما يبقي الشيفرة مرتبة.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

إذا تخطيت هذه الخطوة، ستحصل على نص خام، لكن بنية الجدول ستكون مشوشة — تخيل جدول بيانات حيث كل خلية لغز. المعالج اللاحق يقوم بالعمل الشاق لتنسيق النص مع الشبكة الأصلية.

---

## الخطوة 3 – تحميل صورة الجدول الخاصة بك

يمكنك تحميل صورة من أي مسار، لكن للتوضيح سنشير إلى دليل نائب. استبدل `"YOUR_DIRECTORY/invoice_table.png"` بالمسار الفعلي لملفك.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **ملاحظة:** `aocr.Image` يكتشف تنسيق الصورة تلقائيًا ويُعادي قنوات اللون، لذا لا تحتاج إلى معالجة مسبقة للملف إلا إذا كان متدهورًا بشدة.

---

## الخطوة 4 – تنفيذ OCR مُنظم

الآن يقوم المحرك بمسح الصورة ويعيد كائن جدول خام. يحتوي هذا الكائن على صفوف وأعمدة والنص الخام لكل خلية.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

لماذا نستخدم `recognize_structured` بدلاً من استدعاء عام `recognize`؟ النسخة المُنظمة تحاول استنتاج حدود الصفوف/الأعمدة، مما يمنحك نتيجة شبيهة بالمصفوفة أسهل بكثير للتحويل إلى TSV لاحقًا.

---

## الخطوة 5 – تنظيف البيانات باستخدام معالج AI اللاحق

تشغيل المعالج اللاحق يُنقّح المخرجات الخام: يزيل الأحرف العشوائية، يدمج القطع المتفرقة، ويضمن أن نص كل خلية مُحاذى بشكل صحيح.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

إذا فحصت `processed_table.table`، ستلاحظ قائمة من الصفوف، كل صف هو قائمة من كائنات `Cell`. كل `Cell` يحتوي على خاصية `.text` التي تحمل السلسلة المنقّحة.

---

## الخطوة 6 – تصدير الجدول كملف TSV

الخطوة الأخيرة هي تحويل البيانات المُعالجة إلى ملف قيم مفصولة بجدولة (TSV) — بالضبط ما تحتاجه عندما تريد **convert image to TSV** لبرنامج Excel أو Google Sheets.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

تشغيل السكريبت يطبع كل صف على وحدة التحكم (إذا رغبت) ويكتب ملف TSV نظيف يمكنك فتحه في أي برنامج جدول بيانات.

### التحقق السريع

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

يجب أن ترى أعمدة مُحاذاة بشكل أنيق، مثل:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

إذا ظهر الإخراج مشوشًا، تحقق مرة أخرى من جودة الصورة (الحدة، التباين) وفكّر في تعديل إعدادات محرك OCR — `engine.set_config(...)` يتيح لك ضبط نماذج اللغة وع thresholds الثقة.

---

## معالجة الحالات الشائعة

| الحالة | الحل المقترح |
|-----------|---------------|
| **صورة مائلة** | أعد تدويرها مسبقًا باستخدام `Pillow` (`Image.rotate`) قبل تمريرها إلى `aocr`. |
| **تباين منخفض** | طبّق موازنة التدرج (`cv2.equalizeHist`) لتعزيز قابلية القراءة. |
| **خلايا مدمجة** | عالج TSV لاحقًا لتقسيم الخلايا بناءً على فواصل معروفة أو استخدم العلامة `merge_cells=False` إذا كانت متاحة. |
| **ملفات PDF متعددة الصفحات** | حوّل كل صفحة إلى صورة أولًا (`pdf2image`) وشغّل الخطوات في حلقة. |

هذه التعديلات تحافظ على سير عمل **ocr table image python** قوي عبر مواد مصدرية متنوعة.

---

## السكريبت الكامل – حل شامل

فيما يلي السكريبت الكامل الجاهز للتنفيذ والذي يجمع كل خطوة نوقشت. احفظه باسم `extract_table.py` ونفّذ `python extract_table.py`.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُبنى على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية استخراج جدول من صورة باستخدام Aspose.OCR لـ .NET](/ocr/english/net/text-recognition/recognize-table/)
- [كيفية استخراج النص من صورة عبر إعداد المستطيلات في OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}