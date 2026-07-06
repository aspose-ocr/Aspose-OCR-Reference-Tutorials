---
category: general
date: 2026-01-02
description: استخراج جدول من مستند باستخدام بايثون. تعلم كيفية قراءة الجداول من ملفات
  PDF وتكرار صفوف الجدول بحل نظيف وقابل لإعادة الاستخدام.
draft: false
keywords:
- extract table from document
- how to read tables from pdf
- how to iterate table rows
- pdf table extraction python
- document layout detection
language: ar
og_description: استخراج جدول من مستند باستخدام بايثون. يوضح هذا الدليل كيفية قراءة
  الجداول من ملف PDF وتكرار صفوف الجدول باستخدام محرك موثوق.
og_title: استخراج جدول من المستند – دليل بايثون الكامل
tags:
- Python
- PDF
- Data Extraction
title: استخراج جدول من المستند – دليل بايثون خطوة بخطوة
url: /ar/python/general/extract-table-from-document-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج جدول من المستند – دليل بايثون كامل

هل احتجت يوماً إلى **استخراج جدول من المستند** لكن لم تعرف من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون نفس المشكلة عند التعامل مع ملفات PDF التي تخفي البيانات داخل الجداول. في هذا الدرس سنستعرض حلاً عمليًا من البداية إلى النهاية يُظهر ليس فقط **كيفية قراءة الجداول من pdf**، بل يوضح أيضًا **كيفية تكرار صفوف الجدول** حتى تتمكن من توجيه البيانات إلى أي مكان تحتاجه.

تخيل أن لديك مجموعة من الفواتير، كل واحدة تحتوي على جدول ملخص للمواد. تريد تلك الصفوف في ملف CSV للتحليلات اللاحقة. بنهاية هذا الدليل ستحصل على قطعة كود قابلة لإعادة الاستخدام تقوم بذلك بالضبط، بالإضافة إلى بعض النصائح لتجنب الأخطاء الشائعة.

## ما ستتعلمه

- اكتشاف تخطيط المستند باستخدام محرك تخطيط.  
- تحسين الاكتشاف الخام باستخدام معالج ما بعد المعالجة للحصول على هياكل جداول أنظف.  
- تكرار كل صف من الجدول المكتشف وطباعة (أو تخزين) محتويات الخلايا.  

بدون خدمات خارجية، بدون صناديق سوداء سحرية—فقط بايثون عادي ومكتبة OCR/تخطيط مشهورة (مثل **pdfplumber**، **pdfminer.six**، أو `engine` مملوك تستخدمه بالفعل). إذا كان لديك كائن `engine` يطبق `recognize_layout()` و `run_postprocessor()`، يمكنك إدراج الكود مباشرة.

> **نصيحة احترافية:** إذا كنت تستخدم SDK تجاريًا، تأكد من تفعيل ميزة “اكتشاف الجداول”؛ وإلا قد يغفل التخطيط الخام الخلايا المدمجة.

---

## الخطوة 1: اكتشاف هيكل الجدول – Extract table from document

أول ما تحتاجه هو تخطيط خام يُظهر لك أين توجد الجداول على الصفحة. معظم مكتبات PDF الحديثة توفر طريقة مثل `recognize_layout()` تُعيد هيكلًا هرميًا من الكتل، الأسطر، والخلايا.

```python
# Step 1 – Detect the document layout using the engine
# ---------------------------------------------------
# `engine` is assumed to be an instantiated object from your PDF library.
# It could be pdfplumber, a custom OCR SDK, or any tool that supports layout detection.
raw_layout = engine.recognize_layout()
```

**لماذا هذا مهم:**  
التخطيط الخام يمنحك إحداثيات كل عنصر نصي، لكنه غالبًا ما يتضمن ضوضاء—رؤوس، تذييلات، أو أحرف عشوائية ليست جزءًا من الجدول. لهذا السبب الخطوة التالية حاسمة.

> **سؤال شائع:** *ماذا لو كان ملف PDF يحتوي على صفحات متعددة؟*  
> عادةً ما تُعيد استدعاء `recognize_layout()` قائمة من كائنات الصفحات. قم بالتكرار عليها وطبق نفس منطق ما بعد المعالجة على كل صفحة.

---

## الخطوة 2: تحسين الاكتشاف – How to read tables from pdf

بعد حصولك على `raw_layout`، ستحتاج إلى تنظيفه. معظم المحركات توفر معالجًا ما بعد المعالجة يدمج الخلايا المجزأة، يزيل النص غير ذي الصلة، ويُنشئ كائن `Table` صحيح.

```python
# Step 2 – Refine the detected layout with the post‑processor
# ----------------------------------------------------------
# The post‑processor returns an enhanced layout where tables are
# represented as a list of rows, each row being a list of Cell objects.
enhanced_layout = engine.run_postprocessor(raw_layout)
```

**لماذا تحتاج هذا:**  
قد يُظهر التخطيط الخام صفًا جدولياً واحدًا كعشرات من القطع الصغيرة. يقوم المعالج ما بعد المعالجة بتجميع تلك القطع إلى خلايا منطقية، مما يجعل تكرارها لاحقًا سهلًا.

> **حالة حافة:** بعض ملفات PDF تستخدم حدودًا غير مرئية. إذا لاحظت فقدان صفوف، فعّل خيار “detect invisible lines” في محركك (إن كان متوفرًا).

---

## الخطوة 3: تكرار صفوف الجدول – How to iterate table rows

الآن بعد أن لديك `enhanced_layout` نظيفًا، استخراج البيانات يصبح سهلًا. في الأسفل نمر على كل صف، نجمع نصوص الخلايا باستخدام علامات تبويب (لتحافظ على محاذاة المخرجات)، ونطبع النتيجة. يمكنك استبدال `print` بأي منطق تخزين—كاتب CSV، إدخال قاعدة بيانات، إلخ.

```python
# Step 3 – Print the table contents row by row
# --------------------------------------------
# `enhanced_layout.table` is expected to be an iterable of rows.
# Each `row` is a list of Cell objects with a `.text` attribute.
for row in enhanced_layout.table:
    # Join each cell's text with a tab to align columns
    print("\t".join(cell.text for cell in row))
```

**المخرجات المتوقعة (مثال):**

```
Item	Qty	Price	Total
Widget A	2	$10.00	$20.00
Widget B	1	$15.00	$15.00
Service C	5	$8.00	$40.00
```

إذا كنت تحتاج إلى CSV بدلاً من عرض مفصول بعلامات تبويب، استبدل `"\t".join(...)` بـ `",".join(...)` واكتب إلى ملف.

---

## مثال كامل يعمل

بدمج كل ما سبق، إليك سكربت مستقل. عدّل الاستيراد وت初始化 المحرك ليتوافق مع المكتبة التي تستخدمها.

```python
# --------------------------------------------------------------
# Full script: extract table from document and iterate rows
# --------------------------------------------------------------
import sys

# -----------------------------------------------------------------
# 1️⃣  Import or instantiate your PDF layout engine.
# Replace the placeholder with the actual library you use.
# -----------------------------------------------------------------
# Example with a fictional `pdf_engine` package:
# from pdf_engine import LayoutEngine
# engine = LayoutEngine(api_key="YOUR_KEY")
# -----------------------------------------------------------------
# For pdfplumber (open‑source) you could do:
# import pdfplumber
# engine = pdfplumber.open("sample.pdf")
# -----------------------------------------------------------------
# We'll keep it generic for the tutorial.
# -----------------------------------------------------------------

def extract_table(engine):
    """
    Detect, refine, and iterate over a table in a PDF document.
    Returns a list of rows, where each row is a list of cell strings.
    """
    # Detect layout
    raw_layout = engine.recognize_layout()

    # Refine layout
    enhanced_layout = engine.run_postprocessor(raw_layout)

    # Collect rows
    rows = []
    for row in enhanced_layout.table:
        rows.append([cell.text for cell in row])
    return rows

def main(pdf_path):
    # Initialise your engine – this will differ per library
    # Below is a stub; replace with real initialization.
    engine = initialize_engine(pdf_path)   # <-- implement this

    try:
        table_rows = extract_table(engine)
        for row in table_rows:
            print("\t".join(row))
    except Exception as e:
        print(f"❌ Extraction failed: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python extract_table.py <path-to-pdf>")
    else:
        main(sys.argv[1])
```

**ما يجب استبداله:**

- `initialize_engine(pdf_path)`: إنشاء كائن المحرك للمكتبة التي اخترتها.  
- `engine.recognize_layout()` / `engine.run_postprocessor()`: استخدم أسماء الطرق الصحيحة إذا كانت مختلفة.

تشغيل السكربت باستخدام `python extract_table.py invoice.pdf` سيطبع جدولًا مفصولًا بعلامات تبويب، جاهزًا للمعالجة اللاحقة.

---

## توضيح بصري

فيما يلي مخطط سريع يوضح ما يبدو عليه خط أنابيب الاكتشاف.  
![extract table from document diagram showing raw layout → post‑processor → clean table]  

*نص بديل:* *مخطط تدفق استخراج جدول من المستند*  

---

## الأسئلة المتكررة وحالات الحافة

| السؤال | الجواب |
|----------|--------|
| **ماذا لو كان PDF يحتوي على جداول متعددة؟** | قد يحتوي `enhanced_layout.table` على الجدول الأول فقط المكتشف. قم بالتكرار عبر `enhanced_layout.tables` (لاحظ الجمع) إذا كانت المكتبة تدعم ذلك، وطبق نفس منطق تكرار الصفوف على كل جدول. |
| **كيف أتعامل مع الخلايا المدمجة؟** | عادةً ما يقوم المعالج ما بعد المعالجة بتوسيع الخلايا المدمجة إلى إدخالات منفصلة. إذا لم يحدث ذلك، تحقق من علم `merge_cells` في المحرك أو قم بدمج الخلايا المتجاورة يدويًا بناءً على إحداثياتها. |
| **هل يمكن استخراج جداول من PDF ممسوح ضوئيًا؟** | نعم، لكن ستحتاج إلى خطوة OCR قبل اكتشاف التخطيط. العديد من SDKs تجمع بين OCR واكتشاف التخطيط في استدعاء واحد (`recognize_layout()` على مستند ممسوح). |
| **هل هناك مخاوف من الأداء عند معالجة دفعات كبيرة؟** | عالج الصفحات بالتوازي (مثلاً باستخدام `concurrent.futures`). الجزء الثقيل هو OCR؛ حافظ على بقاء كائن المحرك فعالًا عبر الملفات لتجنب إعادة تحميل النماذج الثقيلة. |
| **هل أحتاج لتثبيت تبعيات إضافية؟** | إذا استخدمت `pdfplumber`، ثبّتها عبر `pip install pdfplumber`. بالنسبة لـ SDKs التجارية، اتبع دليل التثبيت الخاص بالمورد. |

---

## الخلاصة

لقد أظهرنا لك كيفية **استخراج جدول من المستند** عبر اكتشاف التخطيط، تحسينه، ثم **تكرار صفوف الجدول** للحصول على بيانات نظيفة قابلة للاستخدام. سواء كنت تُغذي مستودع بيانات، تُولّد تقارير، أو ببساطة تُحوّل PDF إلى CSV، يبقى النمط نفسه: اكتشف → نظّف → كرّر.

خطوات قد ترغب في استكشافها لاحقًا:

- **كيفية قراءة الجداول من pdf** مع معلومات تنسيق إضافية (خطوط، ألوان).  
- تصدير مباشرة إلى **pandas DataFrames** للتحليلات.  
- استخدام نفس خط الأنابيب **للكتابة عكسًا** وإضافة جداول إلى PDF جديد (تدفق عكسي).  

جرّب السكربت على بعض ملفات PDF الخاصة بك وشاهد مدى السرعة التي يمكنك بها تحويل الجداول الثابتة إلى بيانات قابلة للتنفيذ. استخراج سعيد!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}