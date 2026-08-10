---
category: general
date: 2026-06-19
description: استخراج النص من الصور باستخدام OCR في بايثون. تعلم الكشف التلقائي عن
  اللغة، المعالجة المتوازية، والتعرف على النصوص على دفعات في دليل مختصر.
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: ar
og_description: استخراج النص من الصور باستخدام OCR في بايثون. يوضح هذا الدليل الكشف
  التلقائي عن اللغة، المعالجة المتوازية، والتعرف على النصوص على دفعات في دليل واحد.
og_title: استخراج النص من الصور في بايثون – دليل OCR كامل
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: استخراج النص من الصور في بايثون – دليل OCR الكامل
url: /ar/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصور في بايثون – دليل OCR كامل

هل تساءلت يومًا كيف **تستخرج النص من الصور** دون الحاجة إلى كتابة كل كلمة يدويًا؟ لست وحدك. سواء كنت تقوم برقمنة الإيصالات القديمة، أو تبني أرشيفًا مستندًا للبحث، أو مجرد تجربة حيل الذكاء الاصطناعي الرائعة، فإن القدرة على سحب النص من الصور هي مهارة أساسية لأي مطور بايثون اليوم.

في هذا الدرس سنستعرض مثالًا كاملًا جاهزًا للتنفيذ **يستخرج النص من الصور** باستخدام محرك OCR شائع. سنغطي الكشف التلقائي عن اللغة، المعالجة المتوازية للسرعة، والتعرف على دفعات الصور حتى تتمكن من معالجة عشرات الملفات في ثوانٍ. هل يبدو هذا ما تحتاجه؟ لنبدأ.

## ما ستتعلمه

- كيفية إنشاء محرك OCR باستخدام `ocr.OcrEngine`.
- تفعيل **الكشف التلقائي عن اللغة** بحيث يختار المحرك اللغة المناسبة تلقائيًا.
- إعداد **معالجة OCR المتوازية** باستخدام مجموعة خيوط مخصصة.
- تشغيل **التعرف على دفعة من الصور** على قائمة من الملفات.
- طباعة النص المستخرج لكل صورة، جاهز للحفظ أو الفهرسة.

لا حاجة لأي وثائق خارجية—كل ما تحتاجه موجود هنا، والكود يعمل مباشرةً مع حزمة `ocr` (قم بتثبيتها عبر `pip install ocr`).

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

1. Python 3.8 أو أحدث مثبت.
2. حزمة `ocr` (`pip install ocr`).
3. مجلد يحتوي على صور PNG (أو JPG) تريد معالجتها.
4. إلمام أساسي بدوال وحلقات بايثون.

هذا كل ما تحتاجه—بدون تبعيات ثقيلة، بدون سحر الـ GPU، فقط بايثون عادي.

![مثال لاستخراج النص من الصور](https://example.com/ocr-demo.png "لقطة شاشة تُظهر ناتج استخراج النص من الصور")

*نص بديل: مثال لاستخراج النص من الصور*

## الخطوة 1 – إعداد محرك OCR (الكلمة المفتاحية الأساسية في التنفيذ)

أولًا: أنشئ مثالًا لمحرك OCR. فكر في `ocr.OcrEngine()` كالعقل وراء العملية؛ فهو يعرف كيف يقرأ الأحرف، السطور، والفقرات.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

لماذا نحتاج إلى محرك صريح؟ لأن **استخدام ocr.OcrEngine** يمنحك تحكمًا دقيقًا في إعدادات اللغة، الخيوط، وأكثر. إنه أكثر مرونة لاستخراج النص من الصور مقارنةً بالمساعدات ذات السطر الواحد.

## الخطوة 2 – السماح للمحرك بالكشف عن اللغات تلقائيًا

معظم مكتبات OCR تتطلب منك تحديد اللغة التي يبحث عنها. هذا مناسب لمشروع بلغة واحدة، لكنه مرهق لدفعات متعددة اللغات. لحسن الحظ، تدعم حزمة `ocr` **الكشف التلقائي عن اللغة**.

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

ضبط `engine.language` إلى `ocr.Language.Auto` يخبر المحرك بفحص كل صورة واختيار نموذج اللغة المناسب. هذه السطر الصغير يوفر لك ساعات من الإعداد اليدوي عندما تتعامل مع مستندات دولية.

## الخطوة 3 – تسريع العملية باستخدام معالجة OCR المتوازية

إذا كان لديك أربعة نوى CPU أو أكثر، لماذا لا تستفيد منها؟ يمكن للمحرك إنشاء مجموعة خيوط، مما يسمح بمعالجة عدة صور في الوقت نفسه. هنا يبرز **معالجة OCR المتوازية**.

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

يمكنك تعديل العدد `4` وفقًا لجهازك. المزيد من الخيوط → تشغيل دفعات أسرع، لكن تذكر أن كل خيط يستهلك ذاكرة، لذا ابحث عن التوازن المناسب لبيئتك.

## الخطوة 4 – جمع الصور التي تريد معالجتها

الآن نحتاج إلى قائمة بمسارات الملفات. يمكنك بناء هذه القائمة يدويًا، قراءتها من CSV، أو استخدام `glob`. للتوضيح، سنكتب قائمة قصيرة مباشرةً:

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

استبدل `YOUR_DIRECTORY` بالمسار الفعلي على نظامك. إذا كان لديك عشرات الملفات، فإن `glob.glob("*.png")` سيفعل معظم العمل.

## الخطوة 5 – تشغيل التعرف على دفعة من الصور

هذا هو جوهر الدرس: استدعاء واحد يعالج كل صورة في `files` ويعيد قائمة من كائنات النتيجة. هذه هي ميزة **التعرف على دفعة من الصور** التي تجعل OCR على نطاق واسع عمليًا.

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

خلف الكواليس، يوزع المحرك كل ملف على الخيوط الأربعة التي أعددناها مسبقًا، مع الكشف التلقائي عن اللغة لكل صورة. تُعيد الطريقة قائمة حيث يحتوي كل عنصر على النص المستخرج والبيانات الوصفية.

## الخطوة 6 – طباعة (أو تخزين) النص المستخرج

أخيرًا، نمر على النتائج ونطبع النص. في مشروع حقيقي ربما تكتب ذلك إلى قاعدة بيانات أو ملف CSV، لكن الطباعة تبقي المثال بسيطًا.

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**الناتج المتوقع** (مقتطع للوضوح):

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

كل كتلة تُظهر اسم الملف متبوعًا بالسلسلة المستخرجة من OCR. إذا احتوت الصورة على لغات متعددة، سترى الأحرف المناسبة بفضل خطوة **الكشف التلقائي عن اللغة** السابقة.

## نصائح احترافية ومخاطر شائعة

- **جودة الصورة مهمة** – الصور الضبابية أو ذات التباين المنخفض ستنتج نفايات. عالجها مسبقًا باستخدام OpenCV (`cv2.threshold`, `cv2.resize`) إذا لزم الأمر.
- **عدد الخيوط مقابل I/O** – إذا كانت صورك مخزنة على قرص شبكة بطيء، قد لا تساعد زيادة الخيوط. راقب استهلاك CPU باستخدام `top` أو **Task Manager**.
- **معالجة Unicode** – `result.text` هو سلسلة Unicode. عند الكتابة إلى ملفات، افتحها بـ `encoding="utf‑8"` لتجنب `UnicodeEncodeError`.
- **استهلاك الذاكرة** – ملفات PDF الكبيرة قد تستهلك الكثير من RAM. إذا واجهت `MemoryError`، قلل حجم مجموعة الخيوط أو عالج الصور على دفعات أصغر.

## السكريبت الكامل العامل

فيما يلي السكريبت الكامل جاهز للنسخ واللصق والذي يدمج كل خطوة ناقشناها. احفظه باسم `batch_ocr.py` وشغّله بـ `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

شغّله هكذا:

```bash
python batch_ocr.py ./my_images 4
```

سترى كتلة نص منسقة بشكل جميل لكل صورة، مما يثبت أنك تستطيع **استخراج النص من الصور** على نطاق واسع.

## ما التالي؟

الآن بعد أن أتقنت أساسيات **استخراج النص من الصور** باستخدام بايثون، فكر في استكشاف:

- **ما بعد المعالجة**: نظّف مخرجات OCR باستخدام regex أو مكتبات معالجة اللغة الطبيعية.
- **تحويل PDF**: أدخل السلاسل المستخرجة في مولد PDF لإنشاء ملفات PDF قابلة للبحث.
- **خدمات OCR السحابية**: قارن نتائج `ocr` المحلية مع Google Vision أو Azure OCR للحصول على دقة في الحالات الخاصة.
- **واجهة GUI**: أنشئ تطبيقًا صغيرًا بـ Flask أو FastAPI يتيح للمستخدمين رفع الصور ورؤية النص المستخرج فورًا.

كل هذه المواضيع تبني على أساس **مكتبة OCR بايثون** التي أعددتها، وتستفيد جميعها من نفس حيل **معالجة OCR المتوازية** التي استخدمناها هنا.

---

*برمجة سعيدة! إذا واجهت أي صعوبات، اترك تعليقًا أدناه—أنا دائمًا مستعد لمساعدتك في حل مشكلات OCR.*


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}