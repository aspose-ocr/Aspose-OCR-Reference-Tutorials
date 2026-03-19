---
category: general
date: 2026-03-18
description: استخراج النص من ملفات PNG باستخدام بايثون و Aspose OCR. تعلّم كيفية تحميل
  الصورة للتعرف الضوئي على الأحرف، تشغيل OCR على ملفات متعددة، وتحقيق معالجة دفعة
  من الصور باستخدام التعرف المتوازي على الصور.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: ar
og_description: استخراج النص من ملفات PNG باستخدام Aspose OCR في بايثون. يوضح هذا
  الدرس كيفية تحميل الصورة للتعرف الضوئي على الأحرف، ومعالجة ملفات OCR متعددة، وتشغيل
  مجموعة من الصور باستخدام التعرف المتوازي على الصور.
og_title: استخراج النص من PNG – دليل OCR المتوازي
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: استخراج النص من PNG – دليل OCR المتوازي للتعرف على الصور على دفعات
url: /ar/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من PNG – دليل OCR المتوازي للتعرف على الصور على دفعات

هل احتجت يومًا إلى **استخراج النص من PNG** لكن شعرت بأنك عالق عندما تستغرق صورة واحدة وقتًا طويلاً للمعالجة؟ لست وحدك. في العديد من المشاريع الواقعية—مثل ماسحات الفواتير، محولات الإيصالات إلى رقمية، أو أدوات الأرشفة—السرعة مهمة، ومعالجة كل PNG واحدةً تلو الأخرى لن تكون كافية.  

في هذا الدليل سنستعرض حلًا كاملًا وجاهزًا للتنفيذ **يحمّل الصورة لـ OCR**، ويُنفّذ **ocr multiple files** بطريقة **batch OCR images**، ويستفيد من **التعرف المتوازي على الصور** باستخدام وحدة `threading` في بايثون. في النهاية ستحصل على سكريبت يستخرج النص من أي عدد من ملفات PNG في ثوانٍ، وليس دقائق.

## ما الذي ستحتاجه

- Python 3.8 أو أحدث (الصياغة المعروضة تعمل على 3.10+ أيضًا).  
- حزمة Aspose OCR لـ Java/​Python (`aspose-ocr`). يمكنك تثبيتها عبر `pip`.  
- مجلد يحتوي على مجموعة من ملفات PNG التي تريد معالجتها.  
- كمية معتدلة من الذاكرة RAM—كل خيط (thread) يحتفظ بنسخة صغيرة من محرك OCR، لذا حتى الحاسوب المحمول يمكنه تشغيل عشرات العمال.

لا خدمات خارجية، لا مفاتيح سحابية، ولا ملفات إعدادات غامضة. مجرد كود بايثون نقي يمكنك نسخه ولصقه وتشغيله.

## لماذا استخراج النص من PNG بشكل متوازي؟

معالجة PNG تعتمد على وحدة المعالجة المركزية (CPU): محرك OCR ينفّذ سلسلة من خوارزميات تحليل الصورة التي تتعامل مع بيانات البكسل. عندما يكون لديك عشرة أو عشرون أو مئة صورة، يصبح إجمالي وقت التنفيذ في الأساس مجموع أوقات كل تشغيل منفرد.  

عن طريق إنشاء خيط (thread) لكل ملف، نسمح لنظام التشغيل بجدولة هذه المهام الثقيلة على وحدة المعالجة بشكل متزامن. على جهاز متعدد النوى، هذا غالبًا ما يقلّص—أو حتى يربع—وقت التنفيذ الفعلي. العيب هو استهلاك قليلًا أكبر من الذاكرة، لكن بالنسبة لمعظم وظائف الدفعات فإن الزيادة في السرعة تستحق ذلك.

> **نصيحة احترافية:** إذا كنت تتعامل مع مئات الميجابايت من الصور، فكر في استخدام `concurrent.futures.ProcessPoolExecutor` بدلاً من `threading`. العمليات تعطيك توازيًا حقيقيًا على مفسر CPython المرتبط بـ GIL، على حساب بعض الزيادة في الحمل.

## الخطوة 1: تثبيت Aspose OCR للبايثون

أولًا وقبل كل شيء—لنقم بتثبيت مكتبة OCR على نظامك.

```bash
pip install aspose-ocr
```

هذا السطر الواحد يجلب أحدث ملفات Aspose OCR الثنائية وربطها ببايثون. إذا واجهت خطأ في الصلاحيات، جرّب إضافة `--user` أو استخدام بيئة افتراضية.

## الخطوة 2: تحميل الصورة لـ OCR – دالة العامل

الآن نعرّف الروتين الأساسي الذي سيُنفّذ في كل خيط. إنه **يحمّل الصورة لـ OCR**، يُجري التعرف، ويطبع معاينة للنص المستخرج.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

بعض النقاط التي يجب ملاحظتها:

- **لماذا إنشاء `OcrEngine` جديد لكل خيط؟** المحرك يحتفظ بذاكرات داخلية؛ مشاركة نسخة واحدة قد تؤدي إلى حالات سباق ومخرجات مشوشة.  
- **لماذا إزالة سطر جديد؟** عندما نسجل إلى وحدة التحكم يبقى السطر مرتبًا.  
- **معالجة الأخطاء؟** في بيئة الإنتاج ستغلف الجسم بـ `try/except` وربما تسجل إلى ملف—سنغطي ذلك لاحقًا.

## الخطوة 3: سرد ملفات PNG التي تريد معالجتها

يمكنك كتابة القائمة يدويًا، لكن نهجًا أكثر مرونة هو فحص دليل. أدناه ندرج يدويًا ثلاثة ملفات للتوضيح؛ استبدل المسارات بمجلدك الخاص.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

إذا كنت تفضّل الاكتشاف التلقائي:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

هذا التعديل الصغير يتيح لك **استخراج النص من PNG** على نطاق واسع دون تعديل الكود المصدر في كل مرة.

## الخطوة 4: إعداد ocr multiple files مع batch OCR images

الآن ننشئ خيطًا لكل صورة. هذا هو جوهر نمط **batch OCR images**.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

تعبير القائمة (list comprehension) يبقي الكود مختصرًا، وكل كائن `Thread` يخزن الدالة المستهدفة ومعاملها (`image_path`).  

> **ملاحظة جانبية:** وحدة `threading` في بايثون تستخدم خيوط نظام التشغيل الأصلية، لذا على لابتوب بأربع نوى عادةً سترى ما يصل إلى أربعة خيوط تعمل فعليًا في آنٍ واحد؛ البقية ستُجدول عندما تصبح النوى متاحة.

## الخطوة 5: تشغيل التعرف المتوازي على الصور

إطلاق العمال بسيط: تكرار عبر القائمة واستدعاء `start()`. بعد ذلك ننتظر انتهاء كل خيط باستخدام `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

عند انتهاء السكريبت، سترى سلسلة من السطور مثل:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

هذا الإخراج يؤكد أن كل PNG تم معالجته والنص المستخرج متاح لمعالجة إضافية (مثل حفظه في قاعدة بيانات أو إمداده إلى خط أنابيب NLP).

## الخطوة 6: التحقق من النتائج ومعالجة الحالات الحدية

### التحقق من النتائج الفارغة

أحيانًا تكون الصورة صاخبة جدًا، أو يفشل محرك OCR في اكتشاف أي أحرف. فحص سريع يمكن أن يحفظك من أخطاء لاحقة.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### تحديد عدد الخيوط المتزامنة

إذا شغلت هذا على جهاز افتراضي محدود، قد يؤدي إنشاء مئات الخيوط إلى إغراق المجدول. يمكنك تحديد الحد الأقصى للتوازي باستخدام semaphore:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### حفظ النتائج إلى ملف

بدلاً من الطباعة، قد ترغب في ملف CSV يحتوي على اسم الملف والنص المستخرج:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

تأكد من فتح ملف CSV **مرة واحدة** خارج دالة الخيط لتجنب حالات السباق؛ كاتب `csv` آمن للاستخدام عبر الخيوط للكتابات البسيطة.

## مثال كامل يعمل

بجمع كل شيء معًا، إليك سكريبت واحد يمكنك وضعه في ملف اسمه `batch_ocr.py` وتشغيله:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}