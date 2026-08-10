---
category: general
date: 2026-06-28
description: كيفية تنفيذ OCR على دفعات باستخدام بايثون. تعلم إجراء OCR لعدة صور، استخراج
  النص من ملفات PNG، وتحويل الصورة إلى نص من خلال دورة شاملة لتعليم OCR باستخدام بايثون.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: ar
og_description: كيفية تنفيذ التعرف الضوئي على الحروف (OCR) على دفعات في بايثون موضح
  في الجملة الأولى. اتبع هذا الدرس التعليمي للتعرف الضوئي على الحروف باستخدام بايثون
  لاستخراج النص من ملفات PNG بكفاءة.
og_title: كيفية تنفيذ OCR على دفعات في بايثون – دليل برمجة كامل
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: كيفية تنفيذ التعرف الضوئي على الحروف (OCR) دفعيًا في بايثون – دليل كامل خطوة
  بخطوة
url: /ar/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعيًا في بايثون – دليل خطوة‑بخطوة كامل

هل تساءلت يومًا **كيف تقوم بعمل OCR دفعي** لمجموعة من الصفحات الممسوحة ضوئيًا دون كتابة حلقة تحجب واجهة المستخدم؟ لست وحدك. معالجة عشرات ملفات PNG واحدةً تلو الأخرى قد تشبه مشاهدة جفاف الطلاء، خاصةً عندما تستغرق كل صورة ثانية أو اثنتين لتُفكّ شيفرتها.  

في هذا الدرس سنُظهر لك طريقة نظيفة غير محجوبة **لـ OCR عدة صور** في آنٍ واحد، **لاستخراج النص من ملفات PNG**، و**تحويل الصورة إلى نص** باستخدام محرك OCR حديث لبايثون. بنهاية الدرس ستحصل على سكريبت جاهز للتنفيذ يمكنك وضعه في أي مشروع – مثالي لتعليم *python ocr tutorial* سريع أو لمهمة إنتاجية دفعية.

## ما ستبنيه

- تهيئة محرك OCR وتحديد لغته إلى Latin (أو أي لغة تحتاجها).  
- تمرير قائمة بمسارات الصور (PNG في مثالنا) إلى المحرك.  
- تشغيل عملية دفعية تُعيد كائنًا شبيهًا بـ Future.  
- سحب جميع النتائج بشكل متزامن باستخدام ThreadPool، مع إبقاء الخيط الرئيسي حرًا.  
- طباعة النص المُعترف به لكل صفحة، مع فواصل واضحة.

لا سحر مخفي، مجرد بايثون عادي ومكتبة OCR طرف ثالث (سنستخدم حزمة `pyocr` الخيالية للتوضيح).  

**المتطلبات المسبقة**  
- Python 3.8+ مُثبت.  
- إلمام أساسي بدوال بايثون و`concurrent.futures`.  
- إمكانية الوصول إلى مكتبة OCR تُعرّف فئة `OcrEngine` (مثال: `pip install pyocr`).  

إذا كان أي من هذه غير متوفر، احصل عليه الآن – الأمر أسهل مما تتصور.

---

## كيف تقوم بعمل OCR دفعي في بايثون – المفاهيم الأساسية

قبل الغوص في الكود، دعنا نجيب على سؤال “لماذا” وراء كل خطوة.

1. **لماذا تحديد اللغة؟**  
   دقة OCR ترتفع بشكل كبير عندما يعرف المحرك الأحرف المتوقعة. Latin يناسب الإنجليزية، الفرنسية، الإسبانية، إلخ. غيّر إلى `Language.Japanese` أو `Language.Arabic` إذا لزم الأمر.

2. **لماذا استخدام عملية دفعية؟**  
   استدعاء دفعي يسمح للمحرك بجدولة العمل داخليًا، غالبًا باستخدام خيوط أصلية أو تسريع GPU. يُعيد مقبضًا يمكنك الاستعلام عنه لاحقًا، مما يعني أنك لا تحجب أثناء معالجة كل صورة.

3. **لماذا ThreadPoolExecutor؟**  
   كائن Future الذي نحصل عليه *كسول* – يبدأ بسحب النتائج فقط عندما نطلب ذلك. بإعطاء ThreadPool إلى `getAll`، نسمح لبايثون بجلب نص كل صفحة بشكل متوازي، مما يقلل زمن التنفيذ الكلي بشكل كبير.

4. **لماذا تعداد النتائج؟**  
   ترتيب النتائج يطابق ترتيب مسارات الإدخال، لذا يمكننا تسمية رقم الصفحة بأمان.

فهم هذه النقاط “لماذا” يساعدك على تعديل النمط لملحقات أخرى أو لمجموعات بيانات أكبر.

---

## الخطوة 1: تثبيت واستيراد الحزم المطلوبة

أولًا، تأكد من تثبيت مكتبة OCR. المثال يستخدم حزمة `pyocr` عامة؛ استبدلها بالمكتبة الفعلية التي تفضلها (مثال: `pytesseract`، `easyocr`).

```bash
pip install pyocr
```

الآن استورد كل ما نحتاجه.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **نصيحة احترافية:** استخدام `Path` من `pathlib` يجعل سكريبتك متوافقًا مع أنظمة تشغيل متعددة وأسهل في القراءة.

---

## الخطوة 2: إنشاء محرك OCR وتحديد اللغة

إنشاء المحرك سهل جدًا. سنقفل اللغة على Latin لهذا العرض.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

استدعاء `setLanguage` اختياري لبعض المحركات، لكنه عادةً عادة جيدة. فهو يخبر نموذج OCR بالتركيز على مجموعة الأحرف التي تهمك، مما يحسّن كلًا من السرعة والدقة.

---

## الخطوة 3: سرد ملفات الصور للمعالجة (استخراج النص من PNG)

اجمع جميع ملفات PNG التي تريد تحويلها. استخدام `Path.glob` يتيح لك إسقاط مجلد كامل دون تعديل السكريبت.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **لماذا هذا مهم:** بفضل الفرز، نضمن ترتيبًا حتميًا، وهو ما يطابق لاحقًا كل نتيجة مع رقم الصفحة الصحيح.

---

## الخطوة 4: تشغيل عملية OCR دفعية (تحويل الصورة إلى نص)

الآن نمرر القائمة إلى المحرك. الطريقة تُعيد حاوية شبيهة بـ Future سنستعلم عنها لاحقًا.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

في الخلفية قد يُنشئ المحرك خيوط عمل خاصة به أو حتى خط أنابيب GPU. كل ما يهمنا هو أن لدينا مقبضًا (`batch_future`) يعرف كيف يجلب النتائج الفردية.

---

## الخطوة 5: استرجاع جميع النتائج بشكل متزامن (OCR عدة صور)

هنا نُجري العملية الفعلية *دفعيًا*. بإعطاء `ThreadPoolExecutor` إلى `getAll`، يُجلب نص كل صفحة في خيطه الخاص.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

يمكنك ضبط `max_workers` بناءً على عدد نوى المعالج أو توصيات مكتبة OCR. المزيد من العمال لا يعني دائمًا أسرع – راقب استهلاك المعالج.

---

## الخطوة 6: إخراج النص المُعترف به (ختام درس Python OCR)

أخيرًا، اطبع نص كل صفحة. كائن `Result` يُظهر `getText()` – عدّل إذا استخدمت مكتبة باسم طريقة مختلف.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**الناتج المتوقع (عينة)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

إذا فشلت أي صورة، تُعيد معظم المحركات سلسلة فارغة أو تُطلق استثناء – يمكنك تغليف الحلقة بـ `try/except` للتعامل مع الحالات الطرفية بأناقة.

---

## السكريبت الكامل – جاهز للتنفيذ

فيما يلي السكريبت الكامل المستقل. انسخه إلى ملف باسم `batch_ocr.py`، عدّل `YOUR_DIRECTORY`، ثم نفّذ `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

احفظه، شغّله، وشاهد وحدة التحكم تمتلئ بالنص المستخرج. بسيط، سريع، ومُنفّذ بالكامل بشكل غير متزامن.

---

## المشكلات الشائعة وكيفية تجنّبها

| المشكلة | لماذا تحدث | الحل |
|-------|------------|-----|
| **لا توجد مخرجات** – سلاسل فارغة | لم يتمكن محرك OCR من العثور على نص (الصورة صاخبة جدًا) | عالج الصور مسبقًا: ثنٍّ، تصحيح الميل، أو زيادة DPI |
| **`FileNotFoundError`** | مسار المجلد غير صحيح أو ملفات PNG مفقودة | تحقق من `YOUR_DIRECTORY` وتأكد من أن الملفات تنتهي بـ `.png` |
| **استهلاك عالي للمعالج** | ضبط `max_workers` أعلى من قدرة الجهاز | قلل `max_workers` أو فعّل تسريع GPU إذا كان مدعومًا |
| **تشويش Unicode** | المحرك استخدم لغة مختلفة افتراضيًا | استدعِ `engine.setLanguage(Language.Latin)` (أو اللغة المناسبة) قبل تشغيل OCR الدفعي |

معالجة هذه القضايا مبكرًا سيوفر لك ساعات من التصحيح.

---

## توسيع الدرس – الخطوات التالية

- **OCR لصور متعددة** بصيغ أخرى (JPEG، TIFF) – فقط غيّر نمط الـ glob.  
- **استخراج النص من PNG** وإدخاله في فهرس بحث (مثل Elasticsearch).  
- **تحويل الصورة إلى نص** لإنشاء PDF باستخدام `reportlab` أو `PyPDF2`.  
- **التوازي عبر آلات متعددة** باستخدام `multiprocessing` أو طابور مهام مثل Celery للبيانات الضخمة.  

كل من هذه المواضيع يبني بشكل طبيعي على **python ocr tutorial** الذي أتممته للتو.

---

## الخلاصة

استعرضنا **كيفية تنفيذ OCR دفعي** لمجموعة من ملفات PNG، وأظهرنا قوة واجهة برمجة تطبيقات تدعم الدفعات، وبيّنّا لك كيفية **استخراج النص من PNG** باستخدام نهج Thread‑Pool. السكريبت الكامل أعلاه جاهز للإنتاج، وأنت الآن تمتلك أساسًا قويًا لأي مشروع بايثون يعتمد على OCR.

جرّبه، عدّل إعدادات اللغة، وربما استبدل `pyocr` بـ `pytesseract` – النمط يبقى نفسه. هل لديك أسئلة أو تريد مشاركة حالة استخدام مميزة؟ اترك تعليقًا، ولنستمر في الحوار.

*برمجة سعيدة!*

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُكمل التقنيات التي تم استعراضها في هذا الدليل. كل مورد يحتوي على أمثلة شاملة مع شروحات خطوة‑بخطوة لتساعدك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}