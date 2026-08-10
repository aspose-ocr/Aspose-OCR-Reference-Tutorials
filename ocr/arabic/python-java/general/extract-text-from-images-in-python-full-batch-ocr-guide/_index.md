---
category: general
date: 2026-06-19
description: استخراج النص من الصور في بايثون باستخدام محرك OCR بسيط. تعلم كيفية تحويل
  الصور الممسوحة ضوئياً إلى نص، التعرف على النص من الصور، وقائمة ملفات الصور في بايثون
  بكفاءة.
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: ar
og_description: استخراج النص من الصور باستخدام بايثون ومحرك OCR خفيف الوزن. يوضح لك
  هذا الدليل كيفية تحويل الصور الممسوحة ضوئياً إلى نص، والتعرف على النص من الصور،
  وإدراج ملفات الصور في بايثون في بضع خطوات.
og_title: استخراج النص من الصور في بايثون – دليل OCR شامل للدفعات
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: استخراج النص من الصور في بايثون – دليل كامل لتقنية OCR الدفعي
url: /ar/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصور باستخدام بايثون – دليل OCR شامل للدفعات

هل احتجت يوماً إلى **استخراج النص من الصور** لكن لم تعرف من أين تبدأ؟ لست وحدك—المطورون يواجهون باستمرار تحدي تحويل ملفات PDF الممسوحة ضوئياً، الإيصالات المصورة، أو لقطات الشاشة إلى نص قابل للبحث. في هذا الدرس سنستعرض مثالاً كاملاً جاهزاً للتنفيذ يوضح كيفية **تحويل الصور الممسوحة إلى نص**، التعرف على النص من الصور، وحتى **قائمة ملفات الصور بأسلوب بايثون**. في النهاية ستحصل على سكريبت قابل لإعادة الاستخدام يعالج مجلدًا كاملاً دفعة واحدة.

سنغطي كل ما تحتاجه: المكتبات المطلوبة، لماذا كل خطوة مهمة، التعامل مع الحالات الخاصة، وبعض النصائح لحل المشكلات. لا حاجة للبحث في وثائق خارجية؛ الكود أدناه مكتمل، والشروحات تجيب على سؤال "كيف" *و* "لماذا". افتح بيئة التطوير المفضلة لديك، ولنبدأ.

---

## ما ستبنيه

- تهيئة محرك OCR (سنستخدم حزمة `ocr` للتوضيح).
- مسح دليل وإ **قائمة ملفات الصور بأسلوب بايثون**، مع تصفية PNG، JPG، و TIFF.
- تشغيل عملية **OCR دفعي** على جميع الصور المكتشفة.
- طباعة النص المستخرج لكل ملف مع تسمية واضحة.

> **نصيحة محترف:** إذا لم تكن مكتبة `ocr` مثبتة لديك، يمكنك استبدالها بـ `pytesseract` مع بعض التعديلات البسيطة—المنطق الأساسي يبقى كما هو.

---

## المتطلبات المسبقة

- Python 3.8+ (السكريبت يستخدم f‑strings وتلميحات الأنواع).
- مكتبة OCR توفر `OcrEngine` مع `recognize_batch`. في هذا الدليل نفترض وجود حزمة خيالية `ocr`، لكن النمط يعمل مع المكتبات الحقيقية.
- مجلد يحتوي على ملفات صور تريد معالجتها (`.png`, `.jpg`, `.tif`).

---

## الخطوة 1 – تثبيت واستيراد الوحدات المطلوبة

أولاً، تأكد من توفر حزمة OCR. إذا كنت تستخدم مكتبة حقيقية مثل `pytesseract`، استبدل الاستيراد وفقًا لذلك.

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **لماذا هذا مهم:** استيراد `os` يمنحنا معالجة مسارات متوافقة مع جميع الأنظمة، بينما `typing.List` يساعد في إكمال الكود في IDE ويجعل الكود مستقبليًا.

---

## الخطوة 2 – **استخراج النص من الصور**: تهيئة محرك OCR

إنشاء المحرك هو الخطوة الأولى لأي عمل OCR. نضبط اللغة على الكشف التلقائي حتى يتمكن المحرك من التعامل مع المستندات متعددة اللغات.

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **شرح:** من خلال تغليف إنشاء المحرك في دالة نحافظ على modularity الكود. إذا احتجت لاحقًا لتعديل DPI أو وضع OCR، يمكنك تعديل هذا المكان فقط.

---

## الخطوة 3 – **قائمة ملفات الصور بايثون**: جمع الملفات من دليل

الآن نحتاج إلى تحديد كل صورة نريد معالجتها. تعبير القائمة التالي يعكس نمط “قائمة ملفات الصور بايثون” الشائع.

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **معالجة الحالات الخاصة:** تتجاهل الدالة المجلدات الفرعية (يمكنك إضافة التكرار لاحقًا) وتستبعد الملفات المخفية تلقائيًا لأنها عادةً لا تنتهي بالامتدادات المدعومة.

---

## الخطوة 4 – **تحويل الصور الممسوحة إلى نص**: تشغيل OCR دفعي

معظم مكتبات OCR توفر طريقة دفعية أسرع بكثير من معالجة صورة واحدة في كل مرة. إليك كيفية استدعائها.

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **لماذا الدفعة؟** إرسال جميع الصور مرة واحدة يقلل من الحمل الزائد (مثل تحميل نموذج OCR مرارًا) وغالبًا ما يحسن استغلال CPU/GPU.

---

## الخطوة 5 – **التعرف على النص من الصور**: عرض النتائج

أخيرًا، نمر على أزواج أسماء الملفات ونتائج OCR، ونطبع عنوانًا واضحًا لكل صورة.

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **نصيحة:** `strip()` يزيل المسافات الزائدة في البداية والنهاية التي يضيفها OCR غالبًا.

---

## السكريبت الكامل – جمع كل الأجزاء معًا

فيما يلي البرنامج الكامل القابل للتنفيذ. احفظه باسم `batch_ocr.py` وشغّله باستخدام `python batch_ocr.py <your_folder>`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### النتيجة المتوقعة

با افتراض أن المجلد يحتوي على `invoice1.png` و `receipt.jpg`، قد ترى ما يلي:

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

كل كتلة مُعلمة بوضوح، مما يجعل المعالجة اللاحقة (مثل الحفظ في قاعدة بيانات) سهلة.

---

## معالجة المشكلات الشائعة

| المشكلة | لماذا تحدث | الحل السريع |
|---------|------------|------------|
| **لا يظهر نص** | لغة OCR غير مكتشفة أو الصورة ذات تباين منخفض. | فرض لغة (`engine.language = ocr.Language.English`) أو تحسين الصور (زيادة التباين). |
| **خطأ ذاكرة في دفعات كبيرة** | المحرك يحاول تحميل جميع الصور مرة واحدة. | قسّم `image_files` إلى أجزاء (`batch_size = 20`) واستدعِ `recognize_batch` بشكل متكرر. |
| **صيغة ملف غير مدعومة** | أضفت `.gif` أو `.bmp`. | وسّع مجموعة `supported_exts` أو حوّل الصور إلى PNG/JPG مسبقًا. |
| **تشويه Unicode** | OCR يُعيد بايتات بدلاً من سلاسل. | تأكد من أن مكتبة OCR تُخرج Unicode (`result.text.decode('utf‑8')` إذا لزم). |

---

## توسيع سير العمل

الآن بعد أن أصبحت قادرًا على **استخراج النص من الصور**، فكر في الخطوات التالية:

- **تصدير إلى CSV** – كتابة كل اسم ملف والنص المستخرج إلى جدول للتحاليل.
- **معالجة متوازية** – استخدم `concurrent.futures.ThreadPoolExecutor` لمعالجة دفعات متعددة في آن واحد.
- **الدمج مع OCR سحابي** – استبدل المحرك المحلي بـ Google Vision أو Azure OCR للحصول على دقة أعلى في التخطيطات المعقدة.
- **إضافة معالجة مسبقة للصور** – مكتبات مثل Pillow أو OpenCV يمكنها تصحيح الميل، إزالة الضوضاء، أو تطبيق عتبة قبل OCR، مما يحسن النتائج.

كل هذه الأفكار تعتمد على نفس الدوال الأساسية التي بنيناها، لذا لن تحتاج للبدء من الصفر.

---

## الخلاصة

لقد استعرضنا حلًا كاملاً لـ **استخراج النص من الصور** باستخدام بايثون، بدءًا من **قائمة ملفات الصور بايثون** إلى **التعرف على النص من الصور** وأخيرًا **تحويل الصور الممسوحة إلى نص** في دفعة منظمة. السكريبت بسيط لكنه مرن بما يكفي ليكون أساسًا لمشروعات أكبر—سواءً كنت تُرقم إيصالات، تبني أرشيفًا قابلاً للبحث، أو تشغّل خط أنابيب لاستخراج البيانات.

جرّبه، عدّل خطوات المعالجة المسبقة، وشاهد تحسين دقة OCR. إذا واجهت أي عوائق، راجع جدول “معالجة المشكلات الشائعة”؛ غالبًا ما تُحل القضايا بتغييرات إعدادات بسيطة.

هل أنت مستعد للتحدي التالي؟ جرّب إضافة خطوة تحويل PDF إلى صور باستخدام `pdf2image`، ثم مرر تلك الصور إلى نفس الخط الأنابيب. السماء هي الحد عندما تجمع OCR مع نظام بايثون الغني.

برمجة سعيدة، ولتكن نصوصك دائمًا مقروءة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [استخراج نص الصور – أساسيات OCR مع Aspose.OCR للـ Java](/ocr/english/java/ocr-basics/)
- [كيفية استخراج النص من صورة عبر URL باستخدام Aspose.OCR للـ Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}