---
category: general
date: 2026-03-26
description: كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) على دفعات بكفاءة باستخدام
  بايثون — تعلم استخراج النص من الصور وتحويل ملفات PDF إلى OCR باستخدام المعالجة المتوازية.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: ar
og_description: كيفية تنفيذ OCR دفعيًا بكفاءة—دليل خطوة بخطوة لاستخراج النص من الصور،
  تحويل PDF إلى OCR ومعالجة OCR دفعيًا باستخدام بايثون.
og_title: 'كيفية تنفيذ OCR دفعيًا: استخراج نص سريع ومتوازي'
tags:
- OCR
- Python
- Parallel Computing
title: 'كيفية تنفيذ OCR دفعةً: استخراج نص سريع ومتوازي'
url: /ar/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعة: استخراج نص سريع ومتوازي

هل تساءلت يومًا **كيف تقوم بعمل OCR دفعة** عندما يكون لديك العشرات من الصفحات الممسوحة ضوئيًا، لقطات الشاشة، وملفات PDF متراكمة؟ لست وحدك—معظم المطورين يواجهون نفس المشكلة: معالجة كل ملف على حدة تصبح عنق زجاجة مؤلم.

الخبر السار هو أنه يمكنك تشغيل عدد من خيوط العمل، إطعامها بجميع ملفاتك، ومشاهدة محرك OCR يستهلك الدفعة بشكل متوازي. في هذا الدرس سنستعرض مثالًا كاملاً جاهزًا للتنفيذ يُظهر **استخراج النص من الصور**، تنفيذ **تحويل PDF إلى OCR**، والاستفادة من **معالجة OCR المتوازية** للسرعة.

> **ما ستحصل عليه**  
> * برنامج Python كامل الوظائف يعالج قائمة مختلطة من ملفات PNG وTIFF وPDF وJPG دفعة واحدة.  
> * فهم لماذا يسرّع تجمّع الخيوط مهام OCR التي تعتمد على الإدخال/الإخراج.  
> * نصائح للتعامل مع الأخطاء، ملفات PDF الكبيرة، وعدد الخيوط المخصص.  

## المتطلبات المسبقة

قبل أن نغوص، تأكد من وجود ما يلي:

| المتطلب | السبب |
|-------------|--------|
| Python 3.8+ | الصياغة الحديثة و`concurrent.futures` |
| مكتبة `ocr` (أو أي غلاف OCR متوافق) | توفر `OcrBatchProcessor` وكائنات النتيجة |
| مجموعة من الملفات التجريبية (PNG, TIFF, PDF, JPG) | لرؤية **استخراج النص من الصور** عمليًا |
| إلمام أساسي بالخيوط (اختياري) | مفيد لكنه ليس إلزاميًا |

إذا لم تقم بتثبيت حزمة `ocr` بعد، نفّذ:

```bash
pip install ocr-lib   # replace with the actual package name
```

الآن بعد أن أصبح البيئة جاهزة، لنقسم المشكلة إلى خطوات.

## الخطوة 1: استيراد المساعدات وإنشاء معالج الدفعة

أول شيء نحتاجه هو مكان لجمع جميع وظائف OCR. فئة `OcrBatchProcessor` تقوم بذلك بالضبط—تُرتب عناصر العمل وتعيد لك قائمة من كائنات `Future`.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*لماذا هذا مهم*: استيراد `as_completed` يتيح لنا الاستجابة لكل وظيفة مكتملة فورًا، بدلاً من الانتظار لأبطأ ملف. هذا هو جوهر **معالجة OCR دفعة**.

## الخطوة 2: ضبط مجموعة العاملين للتنفيذ المتوازي

بشكل افتراضي قد يستخدم المعالج خيطًا واحدًا، مما يُبطل فائدة التجميع. نطلب صراحةً أربعة عمال—يمكنك زيادة هذا العدد إلى عدد نوى المعالج لديك.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*نصيحة محترف*: للمهام التي تعتمد على الإدخال/الإخراج مثل OCR، غالبًا ما تتناقص الفائدة بعد `عدد نوى CPU * 2`. جرّب عدة قيم واختر الأنسب.

## الخطوة 3: إضافة كل ملف تريد تحويله إلى OCR

هنا نضيف مجموعة مختلطة من ملفات الصور وPDF. طريقة `add` تسجل المسار فقط؛ العمل الفعلي لن يبدأ حتى نُرسل الدفعة.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

إذا كنت بحاجة لمعالجة مجلد كامل، حلقة `glob` سريعة تقوم بالمهمة:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## الخطوة 4: إطلاق الوظائف وجمع الـ futures

استدعاء `submit_all` يمنح المعالج الإشارة للبدء. يُعيد قائمة من كائنات `Future`—تخيلها كحاملات للنتائج التي ستظهر لاحقًا.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

في هذه المرحلة يكون محرك OCR مشغولًا في الخلفية، كل خيط يلتهم ملفًا.

## الخطوة 5: سحب النتائج فور انتهائها

باستخدام `as_completed` نمر على الـ futures بترتيب انتهائها، وليس بترتيب إرسالها. هذا يبقي البرنامج مستجيبًا، خاصةً عندما تستغرق بعض ملفات PDF وقتًا أطول من PNG البسيطة.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**الناتج المتوقع** (مقتطع للوضوح):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

كل كتلة تمثل النص العادي للملف الأصلي. إذا كنت تقوم بـ **تحويل PDF إلى OCR**، سيتضمن النص كل ما استطاع محرك OCR استخراجه من كل صفحة.

## التعامل مع الحالات الخاصة والمشكلات الشائعة

| الحالة | ما يجب مراقبته | الحل السريع |
|-----------|-------------------|-----------|
| صورة تالفة | `future.result()` يرفع `OSError` | غلفها بـ `try/except` (انظر الكود أعلاه) |
| ملفات PDF ضخمة ( > 100 MB ) | ضغط على الذاكرة، بطء الخيوط | زد `thread_count` بشكل معتدل أو قسّم PDF إلى فصول أولًا |
| مستندات متعددة اللغات | النموذج الافتراضي قد يخطئ في التعرف | مرّر تلميحات اللغة إلى `OcrBatchProcessor` إذا كانت المكتبة تدعم ذلك |
| الحاجة للحفاظ على التخطيط | `get_text()` العادي يفقد الأعمدة | استخدم `ocr_result.get_hocr()` أو طريقة مماثلة تدعم التخطيط |

### نصيحة محترف: عدد خيوط مخصص حسب نوع الملف

إذا كنت تعلم أن معظم عبء العمل هو PDF، يمكنك تخصيص خيوط أكثر لتلك الملفات وأقل للـ PNG الصغيرة. بعض المكتبات تسمح بتمرير `priority` لكل وظيفة؛ وإلا يمكنك إنشاء دفعتين منفصلتين—واحدة للصور، وأخرى للـ PDF—وتشغيلهما متوازيًا.

## نظرة بصرية (اختياري)

![how to batch ocr workflow diagram](https://example.com/ocr-workflow.png "how to batch ocr workflow")

*الرسم البياني يوضح التدفق من اكتشاف الملفات → إنشاء الدفعة → التنفيذ المتوازي → تجميع النتائج.*

## البرنامج الكامل يمكنك نسخه ولصقه

فيما يلي البرنامج بالكامل، جاهزًا للنسخ إلى ملف `.py`. يتضمن جميع المقاطع أعلاه، بالإضافة إلى أداة مساعدة صغيرة تكتشف تلقائيًا الملفات المدعومة في دليل.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

احفظه باسم `batch_ocr.py`، وجهه إلى مجلد يحتوي على مسحاتك، وشاهد وحدة التحكم تمتلئ بالنص المستخرج.  

### لماذا هذا يعمل

* **مجمع الخيوط** – OCR يعتمد في الغالب على انتظار عمليات الإدخال/الإخراج واستدعاءات المحرك الخارجي، لذا الخيوط المتعددة تبقي المعالج مشغولًا.  
* **`as_completed`** – تحصل على النتائج فور جاهزيتها، وهو مثالي لتغذية واجهة المستخدم أو خطوط الأنابيب المتدفقة.  
* **عزل الأخطاء** – ملف سيء واحد لا يوقف الدفعة بأكملها؛ كتلة `try/except` تعزل الفشل.

## الخلاصة

باختصار، الآن تعرف **كيف تقوم بعمل OCR دفعة** باستخدام `concurrent.futures` في بايثون مع مكتبة OCR تدعم المعالجة الدفعية. من خلال تكوين مجموعة خيوط معتدلة، تجميع كل ملف مدعوم، وسحب النتائج فور انتهائها، ستحقق **معالجة OCR متوازية** سريعة دون التضحية بالموثوقية.  

من هنا يمكنك:

* ربط الناتج بفهرس بحث لتسهيل استرجاع المستندات.  
* توسيع البرنامج لكتابة كل نتيجة إلى ملف `.txt` بجانب الأصل.  
* استبدال مجموعة الخيوط المدمجة بـ `asyncio` إذا كانت مكتبة OCR توفر واجهات غير متزامنة.  

استمر في التجربة—استبدل Tesseract، Azure Cognitive Services، أو Google Vision، وستلاحظ أن النمط نفسه ينطبق. نتمنى لك OCR موفقًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}