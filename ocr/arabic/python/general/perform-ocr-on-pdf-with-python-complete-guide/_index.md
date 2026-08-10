---
category: general
date: 2026-06-25
description: إجراء التعرف الضوئي على الأحرف (OCR) لملف PDF باستخدام بايثون — تعلم
  كيفية تحميل ملف PDF للتعرف الضوئي على الأحرف، استخراج النص من صفحات PDF، ومعاينة
  النص المُعترف به بكفاءة.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: ar
og_description: إجراء التعرف الضوئي على الحروف (OCR) لملف PDF باستخدام بايثون. يوضح
  هذا الدليل كيفية تحميل ملف PDF للتعرف الضوئي على الحروف، استخراج النص من صفحات PDF،
  ومعاينة النص المعترف به بسرعة.
og_title: تنفيذ التعرف الضوئي على الحروف في ملفات PDF باستخدام بايثون – دليل خطوة
  بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: إجراء التعرف الضوئي على الحروف في ملفات PDF باستخدام بايثون – دليل شامل
url: /ar/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على ملفات PDF باستخدام Python – دليل شامل

هل احتجت يومًا إلى **perform OCR on PDF** لكن لم تكن متأكدًا من أين تبدأ؟ ربما لديك جبل من العقود الممسوحة ضوئيًا، أو دليل واحد ضخم يرفض التعاون مع أداة استخراج النصوص المعتادة لديك. باختصار، تريد **load PDF for OCR**، استخراج النص، والحصول على معاينة سريعة—كل ذلك دون استهلاك ذاكرة جهازك.

حسنًا، أنت في المكان الصحيح. في هذا الدرس سنستعرض سكريبت Python كامل الوظائف يقوم **extracts text from PDF pages**، يوضح لك كيفية **preview recognized text**، ويتعامل أيضًا مع المشكلة الكلاسيكية لـ **how to OCR large PDF** بشكل فعال.

بنهاية الدرس ستحصل على برنامج جاهز للتنفيذ، وفهم واضح لكل إعدادات التكوين، ومجموعة من النصائح لتجنب الأخطاء الشائعة التي تصطدم بها المبتدئات.

---

## ما ستتعلمه

- كيفية **load PDF for OCR** باستخدام مكتبة `aocr`.
- الخطوات الدقيقة لـ **perform OCR on PDF** صفحةً بصفحة.
- طرق **extract text from PDF pages** مع الحفاظ على استهلاك الذاكرة تحت السيطرة.
- كيفية **preview recognized text** للتحقق من صحة النتائج.
- استراتيجيات التعامل مع **large PDFs** دون استنزاف الذاكرة RAM.

> **Tip:** يفترض هذا الدليل أنك مثبت Python 3.9+ وتملك معرفة أساسية بالبيئات الافتراضية. إذا كنت جديدًا على Python، قم بإعداد virtualenv أولاً—ثق بي، سيوفر عليك الصداع لاحقًا.

## المتطلبات المسبقة

| المتطلبات | لماذا يهم |
|-------------|----------------|
| `aocr` حزمة Python (أو أي محرك OCR متوافق) | توفر الفئة `OcrEngine` المستخدمة في جميع أجزاء السكريبت. |
| `pip` وبيئة افتراضية | تحافظ على عزل الاعتمادات عن Python النظامي الخاص بك. |
| مساحة قرص كافية لاستخراج الصور المؤقتة | بعض محركات OCR تكتب صور الصفحات إلى القرص قبل المعالجة. |
| اختياري: `tqdm` لأشرطة التقدم | تحسن تجربة المستخدم عند التعامل مع مهام **how to OCR large PDF**. |

ثبت الأساسيات باستخدام:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

إذا كان ملف PDF محميًا بكلمة مرور، ستحتاج إلى توفير كلمة المرور لاحقًا—انظر قسم “Edge Cases”.

## الخطوة 1: Perform OCR on PDF – إعداد المحرك

أولًا، نحتاج إلى نسخة من محرك OCR. فكر به كالعقل الذي سيقرأ صورة كل صفحة ويُخرج النص العادي.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **لماذا ضبط `max_memory_mb`؟**  
> محركات OCR غالبًا ما تخزن صور الصفحات في الذاكرة RAM. من خلال تحديد حد للذاكرة، تمنع تعطل السكريبت عند معالجة عقد مكوّن من 500 صفحة.

## الخطوة 2: Load PDF for OCR وتكوين الإعدادات

الآن نقوم فعليًا بـ **load PDF for OCR**. يمكن أن يكون المسار مطلقًا أو نسبيًا؛ فقط تأكد من وجود الملف.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

إذا كان ملف PDF مشفرًا، عادةً ما يرفع `engine.load_pdf` استثناءً. في هذه الحالة يمكنك استدعاء `engine.load_pdf(pdf_path, password="secret")`—المزيد حول ذلك لاحقًا.

## الخطوة 3: Extract Text from PDF Pages – الحلقة الأساسية

هنا حيث نقوم بـ **perform OCR on PDF** صفحةً بصفحة. سنقوم أيضًا بـ **preview recognized text** لأول بضع مئات من الأحرف لتتمكن من التحقق من أن كل شيء يعمل.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **نصيحة احترافية:** شريط التقدم `tqdm` يمنحك إشارة بصرية، وهو مفيد بشكل خاص عند التعامل مع مستندات **how to OCR large PDF** التي تستغرق دقائق للمعالجة.

## الخطوة 4: تجميع كل شيء – سكريبت جاهز للتنفيذ

فيما يلي المثال الكامل القابل للتنفيذ. احفظه باسم `pdf_ocr.py` وشغله باستخدام `python pdf_ocr.py path/to/your/file.pdf`.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### النتيجة المتوقعة (مقتطف)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

سترى معاينة قصيرة لكل صفحة، تليها تأكيد نهائي بأن ملف النص المدمج قد تم كتابته.

## الحالات الخاصة والنصائح العملية

| الموقف | ما الذي يجب فعله |
|-----------|------------|
| **Encrypted PDF** | مرّر كلمة المرور: `engine.load_pdf(pdf_path, password="mySecret")`. |
| **Very large PDF (> 1000 pages)** | قم بزيادة `max_memory_mb` بحذر، أو عالج الملف على دفعات (مثلاً 200 صفحة في كل مرة). |
| **Mixed content (printed + handwritten)** | غيّر `engine.recognition_mode` إلى `aocr.RecognitionMode.MIXED` إذا كانت المكتبة تدعم ذلك. |
| **Missing fonts or poor scan quality** | قم بمعالجة الصفحات مسبقًا باستخدام مكتبة تحسين الصور (مثل Pillow) قبل استدعاء `recognize()`. |
| **Out‑of‑memory crashes** | قلل `preview_len` أو اكتب نص كل صفحة مباشرة إلى القرص بدلاً من الاحتفاظ بها جميعًا في قائمة. |

## كيفية OCR ملفات PDF الكبيرة بفعالية – استراتيجيات متقدمة

عند التعامل مع **how to OCR large PDF**، تصبح السرعة والاستقرار أمرين حاسمين. إليك بعض الحيل التي يمكنك إضافتها إلى السكريبت:

1. **Parallelize per page** – استخدم `concurrent.futures.ThreadPoolExecutor` إذا كان محرك OCR يدعم الخيوط بأمان.
2. **Cache intermediate images** – تسمح بعض المحركات بتخزين الصفحات المرسومة على SSD، مما يقلل بشكل كبير من حمل المعالج عند إعادة التشغيل.
3. **Batch write output** – بدلاً من الإضافة إلى قائمة Python، افتح ملف الإخراج مرة واحدة واكتب نص كل صفحة فور جاهزته.
4. **Adjust DPI** – خفض DPI أثناء التحويل يقلل الذاكرة لكنه قد يؤثر على الدقة؛ ابحث عن القيمة المثلى (عادةً 200‑300 DPI).

فيما يلي مقتطف سريع يوضح كيف يمكنك تنفيذ التوازي لخطوة OCR (اختياري، ألغِ التعليق لاستخدامه):

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

تذكر: التوازي قد يزيد من استهلاك المعالج، لذا راقب درجة حرارة نظامك أثناء التشغيل الطويل.

## الأسئلة المتكررة

**س: هل يمكنني استخدام هذا السكريبت مع مكتبات OCR أخرى مثل Tesseract؟**  
A: بالطبع. استبدل استدعاءات `aocr` بـ `pytesseract.image_to

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية OCR ملفات PDF في .NET باستخدام Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [كيفية استخراج نص الصورة من تدفق باستخدام Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [كيفية استخراج النص من صورة عبر URL باستخدام Aspose.OCR للـ Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}