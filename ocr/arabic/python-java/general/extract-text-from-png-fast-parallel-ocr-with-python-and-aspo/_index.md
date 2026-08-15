---
category: general
date: 2026-03-28
description: استخراج النص من ملفات PNG بسرعة باستخدام Aspose OCR في بايثون. تعلم تحويل
  نص الصفحات الممسوحة ضوئياً باستخدام التعرف المتوازي على الصور في بايثون للحصول على
  نتائج عالية الأداء.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: ar
og_description: استخراج النص من ملفات PNG بسرعة باستخدام Aspose OCR في بايثون. يوضح
  هذا الدليل كيفية تحويل نص الصفحات الممسوحة ضوئياً باستخدام التعرف المتوازي على الصور
  في بايثون، مع تحقيق نتائج عالية السرعة.
og_title: استخراج النص من PNG – OCR سريع ومتوازي باستخدام بايثون
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: استخراج النص من PNG – OCR سريع ومتوازي باستخدام بايثون و Aspose
url: /ar/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من PNG – OCR متوازي سريع باستخدام بايثون

هل احتجت يوماً إلى **استخراج النص من ملفات PNG** لكن وجدت أن OCR أحادي الخيط بطيء جداً؟ لست وحدك. سواء كنت تقوم برقمنة مجموعة من الإيصالات الممسوحة ضوئياً أو تحويل شرائح المحاضرات إلى ملفات PDF قابلة للبحث، فإن عنق الزجاجة عادةً ما يكون خطوة OCR نفسها.

في هذا الدرس سنعرض لك حلاً كاملاً وجاهزاً للتنفيذ **يحوّل نص الصفحات الممسوحة** بشكل متوازي، باستخدام وضع الدفعة غير المتزامن في Aspose OCR مع `ThreadPoolExecutor` في بايثون. بحلول النهاية ستكون قادرًا على **التعرف على نص الصورة بأسلوب بايثون**، ومعالجة العشرات من الصور في جزء صغير من الوقت الذي تستغرقه حلقة بسيطة.

> **ما ستحصل عليه**  
> * برنامج نصي كامل الوظيفة يَستخرج النص من صور PNG بشكل متزامن.  
> * فهم لماذا يسرّع وضع الدفعة غير المتزامن العملية.  
> * نصائح لتوسيع الحل لتعامل مع أحمال عمل أكبر.

## ما ستحتاجه

| المتطلبات المسبقة | السبب |
|--------------|--------|
| Python 3.9+ | الصياغة الحديثة وتلميحات الأنواع. |
| `aspose-ocr` and `aspose-storage` packages | توفر محرك OCR ومحمّل الصور. |
| A folder of PNG files (e.g., scanned pages) | مجلد يحتوي على ملفات PNG (مثل الصفحات الممسوحة) |
| Basic knowledge of Python concurrency | مفيد لكن غير إلزامي؛ سنشرح كل شيء. |

يمكنك تثبيت مكتبات Aspose باستخدام:

```bash
pip install aspose-ocr aspose-storage
```

> **نصيحة احترافية:** حافظ على تحديث حزمك (`pip list --outdated`) للاستفادة من أحدث تحسينات الأداء.

## الخطوة 1: تهيئة محرك Aspose OCR في وضع الدفعة غير المتزامن

أول شيء نقوم به هو إنشاء نسخة من `OcrEngine` وتحويلها إلى **وضع الدفعة غير المتزامن**. هذا الوضع يضع طلبات التعرف في طابور داخليًا، مما يسمح للمحرك بمعالجة صور متعددة دون حجز خيط بايثون الخاص بك.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*لماذا غير المتزامن؟*  
عند استدعاء `recognize` في الوضع المتزامن، يتوقف التنفيذ حتى يتم معالجة الصورة بالكامل. في الوضع غير المتزامن، يمكن للمحرك البدء في العمل على الصورة التالية بينما لا تزال الحالية تُفكّ الشفرة، مما يدمج عمل الإدخال/الإخراج مع وحدة المعالجة.

## الخطوة 2: سرد ملفات PNG التي تريد معالجتها

هنا نحدد مجموعة الصور. في مشروع حقيقي قد تُنشئ هذه القائمة ديناميكيًا (مثلاً `glob.glob("*.png")`)، لكن إبقاؤها صريحة يجعل المثال سهل المتابعة.

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **ملاحظة:** استبدل `YOUR_DIRECTORY` بالمسار الفعلي حيث توجد مسحات PNG الخاصة بك. إذا كان لديك مئات الملفات، فكر في استخدام `os.listdir` وتصفية `.png`.

## الخطوة 3: كتابة دالة مساعدة تقوم بتحميل الصورة وتعيد نصها

الدالة المساعدة تُجرد عملية الخطوتين لتحميل ملف عبر **Aspose Storage** ثم إرساله إلى محرك OCR. إضافة سطر توثيقي صغير يجعل الدالة ذات توثيق ذاتي—مفيد للصيانة المستقبلية.

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*لماذا دالة منفصلة؟*  
تحافظ على نظافة كود مجموعة الخيوط وتتيح لنا إعادة استخدام المنطق في أماكن أخرى (مثل نقطة نهاية Flask). أيضًا، عزل الإدخال/الإخراج يجعل عملية تصحيح الأخطاء أسهل—إذا فشل ملف معين، سترى اسم الملف في تتبع الاستثناء.

## الخطوة 4: تشغيل التعرف المتوازي على الصور في بايثون باستخدام مجموعة خيوط

الآن نستدعي `ThreadPoolExecutor`. بشكل افتراضي نُنشئ أربعة عمال، لكن يمكنك ضبط `max_workers` بناءً على عدد نوى المعالج وحجم مجموعة الصور.

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### كيف يوفّر لك هذا التعرف المتوازي على الصور في بايثون

* **ThreadPoolExecutor** ينشئ مجموعة من خيوط العمل التي تستدعي كل منها `recognize_image`.  
* لأن محرك OCR في وضع الدفعة غير المتزامن، يمكن لكل خيط تسليم العمل إلى المحرك مع البقاء مستجيبًا.  
* `as_completed` يُعيد الـ futures بترتيب الانتهاء، لذا تحصل على النتائج فور جاهزتها—مثالي لتدفق دفعات كبيرة.

> **مشكلة شائعة:** استخدام `max_workers=1` يُبطل هدف التوازي. على جهاز بثمانية نوى، غالبًا ما يعطي `max_workers=8` أعلى معدل نقل، لكن جرّب عدة قيم لتحديد الإعداد المثالي لجهازك.

## الخطوة 5: التحقق من المخرجات ومعالجة الحالات الخاصة

عند تشغيل السكريبت، يجب أن ترى كتلة نص لكل PNG، مسبوقة باسم ملفه:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

إذا فشلت أي صورة (ملف تالف، صيغة غير مدعومة)، سيطبع قسم `except` رسالة خطأ مفيدة بدلاً من إيقاف الدفعة بالكامل.

### توسيع الحل

| السيناريو | التعديل المقترح |
|----------|-----------------|
| **آلاف الصفحات** | التبديل إلى `ProcessPoolExecutor` لاستغلال عمليات CPU متعددة، أو تقسيم القائمة ومعالجة الدفعات بشكل متسلسل. |
| **صيغ صور مختلفة (JPG, TIFF)** | طريقة `storage.Image.load` تكتشف الصيغة تلقائيًا، لذا فقط أضف الملفات إلى `input_images`. |
| **الحاجة لتخزين النتائج** | اكتب `text` إلى ملف `.txt` أو أدخله في قاعدة بيانات داخل قسم `else`. |
| **مراقبة الأداء** | غلف `recognize_image` بمؤقت (`time.perf_counter`) وسجّل مدة التنفيذ لكل ملف. |

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي السكريبت الكامل، جاهز للإدراج في ملف اسمه `parallel_ocr.py`. لا توجد أجزاء مفقودة—كل ما تحتاجه موجود هنا.

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

احفظ الملف، عدل المتغيّر `YOUR_DIRECTORY`، ثم شغّله:

```bash
python parallel_ocr.py
```

يجب أن ترى النص المستخرج لكل PNG يظهر في وحدة التحكم، كما هو موضح سابقًا.

## الخلاصة

لقد عرضنا للتو كيفية **استخراج النص من ملفات PNG** بكفاءة من خلال دمج وضع الدفعة غير المتزامن في Aspose OCR مع `ThreadPoolExecutor` في بايثون. يقوم السكريبت بتحويل نص الصفحات الممسوحة بشكل متوازي، مما يمنحك طريقة قابلة للتوسع لـ **التعرف على نص الصورة بأسلوب بايثون** دون الحاجة لكتابة مجموعة خيوط مخصصة من الصفر.

إذا كنت مستعدًا لتطوير هذا أكثر، جرّب:

* تخزين النتائج في قاعدة بيانات SQLite قابلة للبحث.  
* إضافة معالجة مسبقة للصور (إزالة الميل، إزالة الضوضاء) باستخدام OpenCV قبل OCR.  
* نشر السكريبت كخدمة مصغرة خلف نقطة نهاية Flask أو FastAPI.

تذكر، المفتاح للحصول على OCR عالي الأداء ليس مجرد محرك أسرع—بل أيضًا حول إمداد ذلك المحرك بالعمل بطريقة تعظم التوازي. باستخدام النمط الموضح هنا، يمكنك معالجة العشرات أو حتى مئات من مسحات PNG بأقل تغييرات في الكود.

برمجة سعيدة، ولتكن ملفات PDF الخاصة بك دائمًا قابلة للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}