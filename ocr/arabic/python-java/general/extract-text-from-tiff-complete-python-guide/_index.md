---
category: general
date: 2026-03-28
description: استخراج النص من ملفات TIFF باستخدام Aspose OCR في بايثون. تعلّم كيفية
  تحويل TIFF إلى نص بسرعة وموثوقية.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
language: ar
og_description: استخراج النص من ملفات TIFF باستخدام Aspose OCR في بايثون. يوضح هذا
  الدليل كيفية تحويل TIFF إلى نص خطوة بخطوة.
og_title: استخراج النص من ملف TIFF – دليل بايثون الكامل
tags:
- OCR
- Python
- Aspose
title: استخراج النص من ملف TIFF – دليل بايثون الكامل
url: /ar/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من TIFF – دليل بايثون كامل

هل تحتاج إلى **استخراج النص من صور TIFF** في مشروع بايثون الخاص بك؟ يوضح لك هذا الدليل كيفية **تحويل TIFF إلى نص** باستخدام مكتبة Aspose OCR، ويقوم بذلك بطريقة يمكن للمبتدئ حتى اتباعها.  

إذا سبق لك أن حدقت في ملف TIFF متعدد الصفحات وتساءلت كيف تحصل على الكلمات دون كتابة يدوية، فأنت في المكان الصحيح. سنستعرض العملية بالكامل — من تثبيت الحزمة إلى التعامل مع الحالات الخاصة مثل الملفات المشفرة — حتى تتمكن من التركيز على بناء الميزات التي تهمك.

## ما ستتعلمه

في هذا الدرس ستكتشف:

* كيفية إعداد Aspose OCR للبايثون.
* الشيفرة الدقيقة اللازمة لقراءة كل صفحة من TIFF متعدد الصفحات.
* طرق التعامل مع المشكلات الشائعة مثل الخطوط المفقودة أو الصفحات الفاسدة.
* نصائح لتحسين الدقة والأداء عند **استخراج النص من ملفات TIFF** على نطاق واسع.

بنهاية الدرس، ستحصل على سكريبت جاهز للتنفيذ يحول أي ملف TIFF إلى نص عادي، جاهز للفهرسة أو البحث أو إدخاله في خطوط معالجة اللغة الطبيعية اللاحقة.

### المتطلبات المسبقة

* Python 3.8 أو أحدث (المكتبة تدعم 3.7+).
* رخصة صالحة لـ Aspose OCR — أو يمكنك البدء بالتجربة المجانية (الشيفرة تعمل في وضع التقييم، مع علامة مائية على الناتج).
* إلمام أساسي ببيئات افتراضية في بايثون (اختياري لكن يُنصح به).

---

## الخطوة 1 – تثبيت حزمة Aspose OCR

أولاً: تحتاج إلى حزمة `aspose-ocr`. هي مستضافة على PyPI، لذا يكفي أمر `pip` لتثبيتها.

```bash
pip install aspose-ocr
```

> **نصيحة احترافية:** استخدم بيئة افتراضية (`python -m venv venv`) لعزل الاعتمادات. هذا يمنع تعارض الإصدارات مع مشاريع أخرى قد تكون تديرها.

> **لماذا هذا مهم:** تثبيت الحزمة يجلب ملفات الـ OCR الأصلية التي تقوم بالمعالجة الفعلية. بدونها، لن تتوفر طريقة `recognize_from_tiff`، وستواجه `ImportError`.

---

## الخطوة 2 – استيراد المكتبة وإنشاء محرك OCR

الآن بعد أن صارت المكتبة على جهازك، استوردها وأنشئ كائن `OcrEngine`. هذا الكائن هو العامل الأساسي الذي سيعالج بيانات الصورة.

```python
# Step 2: Import the Aspose OCR library and create an engine instance
import aspose.ocr as aocr

# Initialize the OCR engine – you can optionally pass a license file here
ocr_engine = aocr.OcrEngine()
```

*فئة `OcrEngine` تضم جميع إعدادات OCR، مثل اللغة، الدقة، وخيارات ما قبل المعالجة. سنقوم بتعديل بعضها لاحقًا لتحسين الدقة.*

---

## الخطوة 3 – تحديد مسار ملف TIFF متعدد الصفحات

تحتاج إلى مسار الـ TIFF الذي تريد قراءته. المكتبة تدعم المسارات المطلقة أو النسبية، لكن المسارات المطلقة تتجنب المفاجآت عندما يُنفّذ السكريبت من دليل عمل مختلف.

```python
# Step 3: Define the path to the TIFF file
tiff_file_path = "YOUR_DIRECTORY/input.tif"
```

> **خطأ شائع:** نسيان هروب الشرط المائل في نظام Windows (`C:\\Images\\file.tif`). استخدم السلاسل الخام (`r"C:\Images\file.tif"`) أو الشرط المائل للأمام لتفادي المشكلة.

---

## الخطوة 4 – التعرف على النص من جميع الصفحات

هذا هو جوهر الدرس: استدعاء `recognize_from_tiff`. تُعيد الطريقة قائمة من كائنات `OcrResult` — واحدة لكل صفحة — بحيث يمكنك التنقل بينها بشكل فردي.

```python
# Step 4: Extract text from every page of the TIFF
ocr_pages = ocr_engine.recognize_from_tiff(tiff_file_path)

# Verify we got results
if not ocr_pages:
    raise RuntimeError("No pages were recognized. Check the file path and format.")
```

**لماذا يعمل هذا:** تقوم Aspose OCR داخليًا بتقسيم TIFF إلى إطاراته المكوّنة، وتشغيل محرك OCR على كل إطار، ثم تجميع النتائج. هذا أكثر موثوقية من محاولة فصل الصفحات يدويًا باستخدام Pillow أو ImageMagick.

---

## الخطوة 5 – التكرار على النتائج وإخراج النص

أخيرًا، قم بالتكرار على قائمة `OcrResult` واطبع (أو احفظ) النص المستخرج. يمكنك أيضًا كتابة كل صفحة في ملف `.txt` منفصل إذا كان ذلك يناسب سير عملك.

```python
# Step 5: Print or save the extracted text
for page_index, page_result in enumerate(ocr_pages):
    print(f"--- TIFF Page {page_index + 1} ---")
    print(page_result.text)
    # Optional: write each page to a separate file
    with open(f"page_{page_index + 1}.txt", "w", encoding="utf-8") as f:
        f.write(page_result.text)
```

**الناتج المتوقع** (مقتطع للوضوح):

```
--- TIFF Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- TIFF Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
```

> **معالجة الحالات الخاصة:** إذا كانت الصفحة لا تحتوي على نص قابل للتعرف، فستكون قيمة `page_result.text` سلسلة فارغة. قد ترغب في تسجيل تلك الصفحات للمراجعة اليدوية لاحقًا.

---

## إضافي – تعديل إعدادات OCR لتحسين الدقة

أحيانًا لا تكون الإعدادات الافتراضية كافية، خاصةً مع المسحات منخفضة الدقة أو الخطوط غير المعتادة. إليك بعض الإعدادات التي يمكنك تعديلها:

```python
# Set language (default is English)
ocr_engine.language = aocr.Language.English

# Increase image resolution before OCR (helps with blurry scans)
ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
    sharpen=True,
    contrast=1.2
)

# Enable deskew to straighten rotated pages
ocr_engine.deskew = True
```

*هذه الخيارات اختيارية، لكنها غالبًا ما تُحدث الفارق بين مخرجات مشوشة ونص نظيف قابل للبحث.*

---

## المشكلات الشائعة وكيفية تجنّبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| لا يوجد ناتج لأي صفحة | مسار ملف غير صحيح أو ضغط TIFF غير مدعوم | تحقق من المسار، وتأكد أن TIFF يستخدم ضغطًا مدعومًا (مثل LZW أو PackBits). |
| أحرف مشوهة (مثال: �) | إعداد لغة غير صحيح أو نقص في ملفات الخطوط | اضبط `ocr_engine.language` إلى اللغة المناسبة؛ ثبّت الخطوط المطلوبة على نظام التشغيل. |
| بطء المعالجة على TIFF كبير | الوضع الافتراضي أحادي الخيط | استخدم `ocr_engine.recognize_from_tiff(..., parallel=True)` إذا كانت نسخة المكتبة تدعم ذلك. |
| تحذير الترخيص | استخدام النسخة التجريبية بدون ملف ترخيص | قدّم مفتاح الترخيص عبر `aocr.License().set_license("Aspose.OCR.lic")`. |

---

## السكريبت الكامل – جاهز للتنفيذ

فيما يلي السكريبت الكامل المتكامل الذي يجمع جميع الخطوات والتعديلات الاختيارية التي نوقشت أعلاه. انسخه إلى ملف باسم `extract_tiff_text.py` ثم نفّذه بالأمر `python extract_tiff_text.py`.

```python
#!/usr/bin/env python3
"""
extract_tiff_text.py

A complete example that extracts text from a multi‑page TIFF using Aspose OCR.
It demonstrates how to:
- Install and import the library
- Initialize the OCR engine
- Configure optional preprocessing
- Iterate over each page and save the results

Author: Your Name
Date: 2026‑03‑28
"""

import aspose.ocr as aocr
import os
import sys

def main(tiff_path: str, output_dir: str = "output"):
    # Ensure output directory exists
    os.makedirs(output_dir, exist_ok=True)

    # Initialize the OCR engine
    ocr_engine = aocr.OcrEngine()

    # Optional: fine‑tune OCR settings for better accuracy
    ocr_engine.language = aocr.Language.English
    ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
        sharpen=True,
        contrast=1.2
    )
    ocr_engine.deskew = True

    # Perform OCR on the TIFF
    try:
        ocr_pages = ocr_engine.recognize_from_tiff(tiff_path)
    except Exception as e:
        sys.exit(f"Failed to process {tiff_path}: {e}")

    if not ocr_pages:
        sys.exit("No pages were recognized. Check the file path and format.")

    # Iterate over results
    for idx, result in enumerate(ocr_pages, start=1):
        page_text = result.text or "[No recognizable text]"
        print(f"--- TIFF Page {idx} ---")
        print(page_text[:200] + ("..." if len(page_text) > 200 else ""))  # preview

        # Save each page's text
        out_file = os.path.join(output_dir, f"page_{idx}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

    print(f"\nAll pages processed. Text files saved in '{output_dir}'.")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        sys.exit("Usage: python extract_tiff_text.py <path_to_tiff>")
    tiff_file = sys.argv[1]
    main(tiff_file)
```

**تشغيل السكريبت**

```bash
python extract_tiff_text.py /path/to/your/input.tif
```

ستظهر لك معاينة في وحدة التحكم لكل صفحة ومجلد باسم `output` يحتوي على `page_1.txt`، `page_2.txt`، إلخ.

---

## الخلاصة

لقد غطينا كل ما تحتاجه **لاستخراج النص من ملفات TIFF** باستخدام بايثون وAspose OCR. من تثبيت الحزمة إلى معالجة المستندات متعددة الصفحات، تعديل الإعدادات للدقة، وحفظ النتائج — الآن لديك سير عمل كامل بين يديك.  

إذا كنت ترغب في **تحويل TIFF إلى نص** في خط إنتاج، فكر في تجميع الملفات، تشغيل OCR بشكل متوازي، وتخزين الناتج في فهرس قابل للبحث مثل Elasticsearch. للمغامرين، جرّب لغات أخرى (`aocr.Language.Spanish`) أو مرّر نتائج OCR الخام إلى مكتبة تدقيق إملائي لتنقية الضوضاء.

هل لديك أسئلة حول التوسيع، الترخيص، أو التكامل مع التخزين السحابي؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة! 

---

![Diagram showing the OCR flow from TIFF file to extracted text](https://example.com/placeholder-image.png "استخراج النص من TIFF باستخدام بايثون")

*نص بديل الصورة: استخراج النص من TIFF باستخدام بايثون*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}