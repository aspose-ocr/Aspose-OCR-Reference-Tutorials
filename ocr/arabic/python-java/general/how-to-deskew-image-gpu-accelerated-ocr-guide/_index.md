---
category: general
date: 2026-01-02
description: تعلم كيفية تصحيح انحراف الصورة وتعزيز تباينها للحصول على نص عادي بسرعة.
  يتضمن كود بايثون خطوة بخطوة ونصائح لاستخراج النص.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: ar
og_description: كيفية تصحيح انحراف الصورة وتعزيز التباين للحصول على نص عادي. مثال
  كامل بلغة بايثون لاستخراج الجداول وتسريع باستخدام وحدة معالجة الرسومات.
og_title: كيفية تصحيح ميل الصورة – دليل OCR كامل باستخدام GPU
tags:
- OCR
- Python
- Image Processing
title: كيفية تصحيح ميل الصورة – دليل OCR المعزز باستخدام وحدة معالجة الرسومات (GPU)
url: /ar/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تُصحّح انحراف الصورة – دليل OCR مع تسريع GPU

هل تساءلت يومًا **كيف تُصحّح انحراف الصورة** عندما تأتي إيصالاتك بزاوية غريبة؟ لست وحدك؛ الصورة المائلة يمكن أن تحول إيصالًا مقروءًا إلى فوضى غير مفهومة. الخبر السار هو أنه ببضع أسطر من بايثون يمكنك تصحيح الانحراف تلقائيًا، تعزيز التباين، واستخراج نص نظيف—بدون الحاجة إلى فوتوشوب يدوي.

في هذا الدرس سنستعرض مثالًا كاملاً قابلًا للتنفيذ لا يوضح فقط **كيف تُصحّح انحراف الصورة** بل يُظهر أيضًا **كيف تُعزّز التباين**، **كيف تحصل على نص عادي**، وحتى **كيف تستخرج النص** من الجداول التي يكتشفها محرك OCR. في النهاية ستحصل على سكريبت مستقل يمكنك إدراجه في أي مشروع.

## ما الذي ستحتاجه

- تثبيت Python 3.9+ (الكود يستخدم تلميحات الأنواع، لذا يفضَّل مفسّر حديث)
- مكتبة `ocr` التي توفر `OcrEngine`، `EngineMode`، `ImageProcessingOptions`، و `OcrResult` (ثبِّتها عبر `pip install ocr‑sdk` – استبدل باسم الحزمة الفعلي الذي تستخدمه)
- بطاقة GPU مع تعريفات متوافقة إذا أردت الاستفادة من تسريع الأداء (اختياري لكن مُستحسن)
- ملف صورة مائل قليلًا أو منخفض التباين، مثل `receipt_skewed.jpg`

> **نصيحة احترافية:** إذا لم يكن لديك GPU، فقط غيّر `EngineMode.GPU` إلى `EngineMode.CPU` وسيستمر السكريبت في العمل—لكن سيكون أبطأ قليلًا.

## تنفيذ خطوة بخطوة

فيما يلي نقسم الحل إلى أجزاء منطقية. كل جزء يحمل عنوان **H2** وصفي يحتوي إما على الكلمة المفتاحية الأساسية *how to deskew image* أو إحدى الكلمات الثانوية. الكود كامل، مُعلّق، وجاهز للتنفيذ.

### How to Deskew Image with GPU‑Accelerated OCR

أول ما نقوم به هو إخبار محرك OCR بالعمل على الـ GPU وتفعيل ميزة التصحيح التلقائي للانحراف. يقوم Auto‑deskew بتحليل هندسة الصورة ويعيد تدويرها إلى الوضع الصحيح.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **لماذا هذا مهم:** تسريع GPU يمكن أن يقلل زمن المعالجة من ثوانٍ إلى مليثوانٍ، وهو أمر حاسم عندما تتعامل مع عشرات الإيصالات في الدقيقة.

### Boost Image Contrast for Better Recognition

الإيصال منخفض التباين يشكل كابوسًا لأي نظام OCR. من خلال تعزيز التباين نوفر للمحرك حوافًا أوضح للعمل معها.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **كيفية تعزيز التباين:** طريقة `set_contrast_boost` تقبل نسبة مئوية؛ 30 % هي القيمة الافتراضية الآمنة التي تعمل مع معظم الإيصالات الممسوحة. إذا كانت صورك داكنة جدًا، زد النسبة إلى 50 % أو جرّب قيمًا أخرى.

### Get Plain Text from the Processed Image

الآن بعد أن أصبحت الصورة مستقيمة ومضيئة، نمررها إلى المحرك ونطلب نتيجة النص العادي.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**الناتج المتوقع** (مقتطع للوضوح):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **كيفية الحصول على نص عادي:** طريقة `get_text()` تزيل أي معلومات تخطيطية وتعيد سلسلة نصية نظيفة، يمكنك بعدها تخزينها في قاعدة بيانات، إرسالها إلى API، أو تمريرها إلى تحليلات لاحقة.

### How to Extract Text from Detected Tables

غالبًا ما تحتوي الإيصالات على بيانات جدولة (العناصر، الكميات، الأسعار). يمكن لـ OCR SDK اكتشاف الجداول والسماح لك بالتنقل عبر الصفوف والخلايا.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**مثال على ناتج جدول**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **لماذا نستخرج الجداول:** البيانات المهيكلة تجعل حساب الإجماليات، إنشاء التقارير، أو إدخالها في برامج المحاسبة أمرًا بسيطًا.

### Full Working Script

بجمع كل ما سبق، إليك السكريبت الذي يمكنك نسخه إلى `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

شغّله باستخدام:

```bash
python deskew_and_ocr.py
```

سترى النص المنقح وأي جداول مكتشفة تُطبع على سطر الأوامر.

## حالات الحافة الشائعة وكيفية التعامل معها

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **الصورة مقلوبة رأسًا على عقب** | زد من ثقة `set_auto_deskew(True)` عبر استدعاء `set_rotation_correction(True)` إذا كان الـ SDK يدعم ذلك. |
| **تعزيز التباين يجعل الصورة ساطعة جدًا** | قلل النسبة المئوية الممررة إلى `set_contrast_boost` (مثلاً 15 %). |
| **GPU غير متوفر** | غيّر `EngineMode.GPU` إلى `EngineMode.CPU`؛ باقي الخطوات تبقى كما هي. |
| **الجداول لم تُكتشف** | جرّب مسحًا بدقة أعلى أو فعّل `set_table_detection(True)` إذا كانت المكتبة توفر ذلك. |

## الخطوات التالية: من النص العادي إلى البيانات المهيكلة

الآن بعد أن عرفت **كيف تُصحّح انحراف الصورة**، **كيف تُعزّز التباين**، و**كيف تحصل على نص عادي**، قد ترغب في:

- تحليل النص العادي باستخدام تعبيرات نمطية لاستخراج أزواج المفتاح‑القيمة (مثل `total`، `date`).
- تخزين النتائج في قاعدة بيانات SQLite أو PostgreSQL للتقارير المستقبلية.
- ربط السكريبت بوظيفة خالية من الخوادم (AWS Lambda، Azure Functions) لمعالجة التحميلات تلقائيًا.

جميع هذه الإضافات تُبنى على الأساس الذي غطيناه هنا.

## الخلاصة

استعرضنا **كيف تُصحّح انحراف الصورة** باستخدام محرك OCR مسرّع بـ GPU، وأظهرنا **كيف تُعزّز التباين** للحصول على تعرّف أدق، وبيّنّا لك بالضبط **كيف تحصل على نص عادي**، وحتى **كيف تستخرج النص** من الجداول. السكريبت الكامل القابل للتنفيذ يجمع كل ذلك، بحيث يمكنك إدراجه في أي مشروع بايثون والبدء في استخراج بيانات نظيفة من صور مائلة ومنخفضة التباين فورًا.

جرّبه على بعض إيصالاتك، عدّل مستوى التباين، ودع OCR يتولى العمل الشاق. إذا واجهت أي مشاكل، ارجع إلى جدول حالات الحافة أعلاه—معظم القضايا تُحل بتعديل بسيط.

برمجة سعيدة، ولتكن صورك دائمًا مستقيمة ومضيئة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}