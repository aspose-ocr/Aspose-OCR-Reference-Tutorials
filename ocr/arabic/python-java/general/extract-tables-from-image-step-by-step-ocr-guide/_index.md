---
category: general
date: 2026-03-26
description: استخراج الجداول من الصورة وتحويل الصورة إلى جدول بيانات باستخدام OCR
  في بايثون. تعلم كيفية تحميل الصورة للـ OCR، قراءة الجداول واستخراج بيانات الجدول.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: ar
og_description: استخراج الجداول من الصورة باستخدام OCR في بايثون. يوضح هذا الدليل
  كيفية تحميل الصورة للـ OCR، قراءة الجداول، وتحويلها إلى جدول بيانات.
og_title: استخراج الجداول من الصورة – دليل OCR كامل
tags:
- OCR
- Python
- Data Extraction
title: استخراج الجداول من الصورة – دليل OCR خطوة بخطوة
url: /ar/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج الجداول من الصورة – دليل OCR كامل

هل احتجت يوماً إلى **استخراج الجداول من صورة** لكن لم تعرف من أين تبدأ؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتوي ملف PDF أو لقطة شاشة على بيانات جدولة يجب تحويلها إلى صفوف وأعمدة قابلة للتحرير. الخبر السار؟ بضع أسطر من كود Python، مقترنة بمحرك OCR قوي، يمكنها تحويل تلك الصورة إلى جدول بيانات قابل للاستخدام في ثوانٍ.

في هذا الدرس سنستعرض كيفية تحميل صورة للـ OCR، تشغيل محرك التعرف، واستخراج كل جدول صفًا بصف. في النهاية ستتمكن من **تحويل الصورة إلى جدول بيانات**، وسترى أيضًا كيفية **ocr read tables** و **ocr extract table data** للمعالجة اللاحقة. لا سحر مخفي، فقط كود واضح قابل للتنفيذ يمكنك إضافته إلى مشروعك اليوم.

---

## ما ستحتاجه

قبل أن نبدأ، تأكد من توفر ما يلي:

- **Python 3.9+** – أحدث إصدار مستقر هو الأنسب.
- مكتبة **`ocr`** (أو أي SDK OCR متوافق يتيح `OcrEngine`، `Image`، وطرق متعلقة بالجداول). قم بتثبيتها باستخدام `pip install ocr‑sdk` (استبدل باسم الحزمة الفعلي إذا لزم).
- ملف صورة (`.png`، `.jpg`، إلخ) يحتوي على جدول مطبوع بوضوح.  
- اختياري: **pandas** إذا رغبت في كتابة البيانات المستخرجة مباشرة إلى ملف CSV أو Excel (`pip install pandas`).

هل لديك كل شيء؟ رائع—لنبدأ.

---

## الخطوة 1: استيراد SDK الـ OCR وإعداد البيئة

أولاً وقبل كل شيء: نحتاج إلى جلب فئات OCR إلى السكريبت وإعداد مساعد صغير سيحول بيانات الجدول الخام إلى DataFrame لاحقًا.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**لماذا هذا مهم:** استيراد `ocr` يمنحنا الوصول إلى `OcrEngine`، `Imaging.Image`، وكائنات الجداول التي سنقوم بالتنقل بينها. لا يلزم `pandas` للاستخراج، لكنه يجعل جزء **تحويل الصورة إلى جدول بيانات** سهلًا للغاية.

---

## الخطوة 2: تحميل الصورة التي تريد معالجتها

الآن نقوم فعليًا بـ **load image for OCR**. يتوقع SDK كائن `Image`، لذا سنغلف مسار الملف باستخدام الطريقة المساعدة `Image.load()`.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**نصيحة احترافية:** احفظ ملفات الصور في مجلد مخصص (`assets/` أو `data/`) واستخدم مسارات نسبية. بهذه الطريقة يبقى السكريبت قابلًا للنقل بين الأجهزة.

---

## الخطوة 3: تشغيل عملية التعرف

مع إرفاق الصورة، يمكننا أخيرًا إخبار المحرك بـ **ocr read tables**. تعيد الدالة `recognize()` كائن نتيجة يحتوي على كل ما اكتشفه المحرك—كتل النص، الأسطر، والأهم بالنسبة لنا، الجداول.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**لماذا نتحقق:** قد تكون بعض الصور مشوشة أو حدود الجداول باهتة، مما يؤدي إلى عدم اكتشافها. تسجيل تحذير يمنحك ملاحظات مبكرة دون إيقاف السكريبت.

---

## الخطوة 4: استخراج صفوف وخلايا كل جدول

هنا يحدث السحر الحقيقي. سن iterates على كل جدول مكتشف، نستخرج كل صف، ثم نص كل خلية. تجعلنا الـ list comprehension الداخلية الكود مختصرًا، لكننا سنشرح التدفق خطوة بخطوة.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**ما الذي يحدث؟**  

- `enumerate(..., start=1)` يمنحنا رقم جدول صديق للقراءة في السجلات.  
- `row_obj.get_cells()` تُعيد كل كائن خلية؛ `cell.get_text()` يحصل على النص المفكك بواسطة OCR.  
- نخزن الصفوف في `rows_data`، ثم نمررها إلى `pandas.DataFrame` الذي ينسق الأعمدة تلقائيًا.  
- كتلة `print` تعكس **المخرجات الأساسية** المعروضة في المقتطف الأصلي، لتتمكن من التحقق من النتائج فورًا.

**معالجة الحالات الخاصة:** إذا كان للصف عدد خلايا مختلف عن الصفوف الأخرى، سيملأ `pandas` الأماكن الناقصة بـ `NaN`. يمكنك لاحقًا تنظيف الـ DataFrame باستخدام `df.fillna('')` إذا فضلت السلاسل الفارغة.

---

## الخطوة 5: حفظ الجداول المستخرجة إلى جدول بيانات

الآن بعد أن أصبح لدينا قائمة من DataFrames، تحويلها إلى ملف Excel (أو ملفات CSV) أمر سهل. هذا يحقق هدف **تحويل الصورة إلى جدول بيانات**.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**لماذا Excel؟** معظم مستخدمي الأعمال يفضلون `.xlsx`. إذا كنت تفضل CSV، استبدل الحلقة بـ `df.to_csv(f"table_{idx}.csv", index=False)`.

---

## البرنامج الكامل الجاهز للتنفيذ

بجمع كل ما سبق، إليك البرنامج الكامل الذي يمكنك نسخه ولصقه ثم تشغيله.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**المخرجات المتوقعة في الطرفية** (مع جدول بسيط 2×3):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

وستجد ملف `extracted_tables.xlsx` في مجلد السكريبت، كل جدول في ورقة منفصلة.

---

## الأسئلة المتكررة والنصائح

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني استخدام مكتبة OCR مختلفة؟** | بالتأكيد. النمط يبقى نفسه: تحميل الصورة → التعرف → التكرار على `get_tables()`. فقط استبدل الاستيراد وأسماء الكائنات. |
| **ماذا لو كانت صورتي مشوشة؟** | قم بالمعالجة المسبقة باستخدام OpenCV (العتبة، تصحيح الميل) قبل تمريرها إلى محرك OCR. تقليل الضوضاء غالبًا ما يحسن دقة **ocr extract table data**. |
| **هل أحتاج لتثبيت `openpyxl`؟** | نعم، `pandas` يستخدمه خلف الكواليس لإنتاج ملفات Excel. ثبّته عبر `pip install openpyxl`. |
| **كيف أتعامل مع الخلايا المدمجة؟** | بعض SDKs توفر `cell.is_merged()`؛ يمكنك اكتشاف ذلك ونشر القيمة عبر النطاق المدمج يدويًا. |
| **هل هناك طريقة لاستخراج جداول محددة فقط؟** | قم بالفلترة باستخدام `table_obj.get_confidence()` أو بالتحقق من كلمات المفتاح في العناوين قبل المعالجة. |

---

## الخلاصة

أصبحت الآن تمتلك حلًا كاملًا من البداية إلى النهاية لـ **extract tables from image**، تحويل النتيجة إلى جدول بيانات منظم، وحتى التعامل مع جداول متعددة في صورة واحدة. يوضح السكريبت كيفية **load image for OCR**، **ocr read tables**، و **ocr extract table data** مع الحفاظ على مرونة كافية لتناسب المتطلبات الواقعية.

ما الخطوة التالية؟ جرّب إمداد محرك OCR بصفحة PDF محوّلة إلى صورة، أو جرب لغات وخطوط مختلفة. يمكنك أيضًا توجيه الـ DataFrames مباشرة إلى قاعدة بيانات أو أداة تقارير—الخيال هو الحد.

إذا وجدت هذا الدليل مفيدًا، لا تتردد في مشاركته، وضع نجمة على المستودع الذي يستضيف الـ SDK، أو ترك تعليق بأفكارك الخاصة. برمجة سعيدة، ولتكون جداولك دائمًا مُستخرجة بدقة! 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}