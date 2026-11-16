---
category: general
date: 2026-06-25
description: معالجة OCR دفعةً في بايثون بسهولة. تعلّم كيفية استخراج النص من مجموعة
  الصور وإتقان استخراج نص الصور دفعةً باستخدام الخيوط المتوازية.
draft: false
keywords:
- batch OCR processing
- extract text from image batch
- batch image text extraction
language: ar
og_description: معالجة OCR الدفعي في بايثون تتيح لك استخراج النص من دفعة الصور بسرعة.
  هذا الدليل يشرح لك OCR المتوازي مع أمثلة شفرة واضحة.
og_title: معالجة OCR دفعيّة في بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  headline: Batch OCR Processing in Python – Complete Programming Guide
  type: TechArticle
- description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  name: Batch OCR Processing in Python – Complete Programming Guide
  steps:
  - name: Missing or Corrupt Images
    text: If an image can’t be opened, most OCR libraries raise an exception that
      aborts the whole batch. Wrap the call in a `try/except` inside the batch function
      or filter out problematic files beforehand (see the sanity check in Step 1).
  - name: Language & DPI Settings
    text: For multilingual documents, pass a `langs` parameter (e.g., `langs=['en',
      'de']`). If your scans are low‑resolution, consider pre‑processing with `Pillow`
      to upscale to 300 DPI before OCR—this often boosts accuracy.
  - name: Memory Constraints
    text: 'Eight threads can eat RAM, especially with large images. If you hit memory
      errors, lower `max_threads` or process the list in smaller chunks:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: معالجة OCR الدفعية في بايثون – دليل برمجي شامل
url: /ar/python-java/general/batch-ocr-processing-in-python-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة دفعة OCR في بايثون – دليل برمجة شامل

هل احتجت إلى **معالجة دفعة OCR** لكن لم تكن متأكدًا من كيفية تشغيلها بكفاءة على العشرات من الصفحات الممسوحة ضوئيًا؟ لست وحدك—غالبًا ما يواجه المطورون صعوبة عندما يحاولون استخراج النص من مجموعة صور دون أن يثقلوا وحدة المعالجة المركزية.

في هذا الدليل سنظهر لك طريقة مباشرة لـ **استخراج النص من مجموعة صور** باستخدام محرك OCR في بايثون، تشغيل العملية على ما يصل إلى ثمانية خيوط، وأخيرًا معرفة عدد الأحرف التي ساهمت بها كل صورة. بنهاية القراءة ستحصل على سكريبت قابل لإعادة الاستخدام يتعامل مع **استخراج نص الصور دفعةً** كالمحترفين.

## ما يغطيه هذا الدرس

سنستعرض ثلاث خطوات عملية:

1. بناء قائمة بملفات الصور التي تريد التعرف عليها.  
2. تشغيل محرك OCR بالتوازي مع `max_threads=8`.  
3. التكرار على النتائج وطباعة ملخص مختصر.

بدون خدمات خارجية، بدون مكتبات غامضة—فقط بايثون عادي وواجهة OCR نموذجية (مثلاً `ocr` من `easyocr` أو غلاف مخصص). إذا كان لديك Python 3.8+ وحزمة OCR مثبتة، فأنت جاهز للنسخ‑اللصق والتشغيل.

---

## الخطوة 1: إعداد قائمة بملفات الصور لمعالجة دفعة OCR

أول شيء تحتاجه هو مجموعة من مسارات الصور. فكر فيها كقائمة تسوق لمحرك OCR؛ كل إدخال يشير إلى ملف PNG أو JPEG أو TIFF يحتوي على النص الذي تريد قراءته.

```python
# Step 1: Prepare a list of image files to be recognized
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png",
    "YOUR_DIRECTORY/page4.png",
    "YOUR_DIRECTORY/page5.png"
]

# Quick sanity check – make sure the files exist
import os
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"These files are missing: {missing}")
```

**لماذا هذا مهم:**  
إنشاء القائمة مسبقًا يسمح لمحرك OCR بالعمل في وضع الدفعة الحقيقي. كما يمنحك مكانًا واحدًا لإضافة أو إزالة ملفات دون تعديل منطق المعالجة لاحقًا. فحص الصحة يمنع حدوث تعطل “الملف غير موجود” في منتصف تشغيل طويل.

---

## الخطوة 2: تشغيل OCR على الدفعة باستخدام خيوط متوازية (استخراج نص من مجموعة صور)

الآن نمرر القائمة إلى محرك OCR. معظم أغطية OCR الحديثة توفر طريقة `recognize_batch` التي تقبل معامل `max_threads`. بتعيينه إلى `8` نخبر المكتبة بإنشاء ثمانية خيوط عمل، مما يمكن أن يقلل زمن المعالجة بشكل كبير على معالج رباعي النوى مع تقنية Hyper‑Threading.

```python
# Step 2: Run OCR on the batch, allowing up to 8 parallel threads
# Assuming `ocr` is a module that provides OcrEngine with recognize_batch()
import ocr

batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# batch_results is a list of Result objects, each with a .text attribute
```

**لماذا يساعد التوازي:**  
OCR يستهلك وحدة المعالجة المركزية؛ كل صورة تُمرَّر عبر شبكة عصبية أو محرك قديم. تشغيلها واحدةً تلو الأخرى قد يكون بطيئًا جدًا، خاصةً للماسحات ذات الدقة العالية. الخيوط المتوازية تبقي جميع الأنوية مشغولة، محوّلة مهمة تستغرق 5 دقائق إلى دقيقة واحدة على الأجهزة العادية.

**نصيحة:** إذا كنت تستخدم `easyocr`، فإن الاستدعاء يكون كالتالي `reader.readtext(image_path, detail=0)` داخل حلقة. تجريدنا `recognize_batch` يخفي هذه التعقيدات، لكن يمكنك دائمًا استبداله بـ `ThreadPoolExecutor` إذا لم توفر المكتبة دعمًا للدفعات.

---

## الخطوة 3: التكرار عبر النتائج وتلخيص استخراج نص الصور دفعةً

بعد انتهاء OCR، ستحصل على قائمة من كائنات النتائج. لنقم بدمج مسارات الملفات الأصلية مع مخرجات OCR المقابلة ونطبع سطرًا أنيقًا لكل صورة يوضح عدد الأحرف التي تم التعرف عليها.

```python
# Step 3: Iterate through the results and display character counts
for file_path, result in zip(image_files, batch_results):
    # result.text holds the raw extracted string
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**ما ستراه:**  

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

**لماذا هذه الخطوة مفيدة:**  
عدد الأحرف السريع يعطيك نظرة سريعة على ما إذا كانت الصورة قد عولجت بشكل صحيح. عدد منخفض غير متوقع قد يشير إلى مسح ضبابي، إعداد لغة خاطئ، أو ملف تالف—مشكلات يمكنك معالجتها قبل الانتقال إلى التحليل اللاحق.

---

## إضافي: التعامل مع الحالات الحدية والمشكلات الشائعة

### صور مفقودة أو تالفة  
إذا تعذّر فتح صورة، فإن معظم مكتبات OCR تُطلق استثناءً يوقف الدفعة بالكامل. احط الاستدعاء بـ `try/except` داخل دالة الدفعة أو استبعد الملفات المسببة للمشكلات مسبقًا (انظر فحص الصحة في الخطوة 1).

### إعدادات اللغة و DPI  
للمستندات متعددة اللغات، مرّر معامل `langs` (مثال: `langs=['en', 'de']`). إذا كانت مسحاتك ذات دقة منخفضة، فكر في ما قبل المعالجة باستخدام `Pillow` لتكبيرها إلى 300 DPI قبل OCR—هذا غالبًا ما يحسن الدقة.

### قيود الذاكرة  
ثمانية خيوط قد تستهلك ذاكرة RAM، خاصةً مع صور كبيرة. إذا واجهت أخطاء ذاكرة، قلل `max_threads` أو عالج القائمة على دفعات أصغر:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(image_files, 3):  # process three images at a time
    results = ocr.OcrEngine.recognize_batch(chunk, max_threads=3)
    # handle results...
```

---

## السكريبت الكامل العامل

بجمع كل ما سبق، إليك مثال كامل جاهز للتنفيذ. استبدل `"YOUR_DIRECTORY"` بمسار المجلد الذي يحتوي على ملفات PNG وتأكد من تثبيت وحدة `ocr`.

```python
#!/usr/bin/env python3
"""
Batch OCR Processing Script
Extracts text from an image batch using parallel threads and prints character counts.
"""

import os
import ocr  # Replace with your OCR library import, e.g., from easyocr import Reader

# -------------------------------------------------
# Step 1: Define the list of image files
# -------------------------------------------------
image_dir = "YOUR_DIRECTORY"
image_files = [
    os.path.join(image_dir, f"page{i}.png") for i in range(1, 6)
]

# Verify that all files exist
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"Missing image files: {missing}")

# -------------------------------------------------
# Step 2: Run OCR in parallel (max 8 threads)
# -------------------------------------------------
# The OcrEngine is a placeholder – adapt to your library's API
batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# -------------------------------------------------
# Step 3: Report how many characters each image yielded
# -------------------------------------------------
for file_path, result in zip(image_files, batch_results):
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**الناتج المتوقع** (ستختلف أرقامك):

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

شغِّل السكريبت باستخدام `python batch_ocr.py` وسترى الطرفية تمتلئ بالإحصاءات المختصرة.

---

## نظرة بصرية عامة

![Batch OCR processing flow diagram](image-placeholder.png "Diagram illustrating batch OCR processing steps")

*نص بديل للصورة:* *مخطط تدفق معالجة دفعة OCR يوضح إنشاء قائمة الملفات، تنفيذ OCR المتوازي، وتلخيص النتائج.*

---

## الخلاصة

أصبح لديك الآن أساس قوي لـ **معالجة دفعة OCR** في بايثون. من خلال إعداد قائمة نظيفة من الصور، واستخدام خيوط متوازية لاستخراج النص من مجموعة صور، وتلخيص النتائج، يمكنك تحويل مهمة يدوية شاقة إلى خط أنابيب سريع وقابل لإعادة الاستخدام.

من هنا يمكنك:

- حفظ كل `result.text` في ملف `.txt` للتحليل اللغوي اللاحق.  
- دمج عدد الأحرف مع درجات الثقة لتصفية الصفحات ذات الجودة المنخفضة.  
- دمج السكريبت في سير عمل أكبر لاستهلاك المستندات، وربما إمداده إلى فهرس بحث.

سواء كنت تقوم برقمنة أرشيفات، أو بناء تطبيق مسح فواتير، أو إعداد بيانات تدريب لنموذج لغة، فإن المفاهيم التي تم تناولها هنا يمكن توسيعها لتشمل مئات أو آلاف الملفات بأقل تعديل.

هل لديك أسئلة حول إعدادات اللغة، أو ما قبل معالجة الصور، أو نشر هذا في السحابة؟ اترك تعليقًا أو اطلع على الدروس ذات الصلة حول *معالجة الصور في بايثون* و *OCR غير المتزامن باستخدام asyncio*. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة‑بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية معالجة دفعة صور OCR باستخدام List في Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [استخراج النص من صورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}