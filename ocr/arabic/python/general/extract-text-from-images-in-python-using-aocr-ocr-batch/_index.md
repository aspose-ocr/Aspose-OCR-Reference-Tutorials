---
category: general
date: 2026-06-25
description: استخراج النص من الصور باستخدام مكتبة Python aocr – تعلم التعرف الضوئي
  على الحروف (OCR) الدفعي، ضبط وضعية التعرف على النص المطبوع، وإضافة معالج ما بعد
  الذكاء الاصطناعي.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: ar
og_description: استخراج النص من الصور باستخدام مكتبة Python aocr. يوضح هذا الدرس التعرف
  الضوئي على الحروف (OCR) الدفعي، وضع التعرف على النص المطبوع، ومعالج ما بعد الذكاء
  الاصطناعي الاختياري.
og_title: استخراج النص من الصور في بايثون – دليل كامل لاستخدام aocr دفعي
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: استخراج النص من الصور في بايثون باستخدام aocr OCR Batch
url: /ar/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصور في بايثون باستخدام aocr OCR Batch

هل احتجت يوماً إلى **استخراج النص من الصور** وشعرت بالإرهاق من عشرات الخطوات الصغيرة؟ لست وحدك. سواءً كنت تقوم برقمنة النماذج الممسوحة، أو استخراج البيانات من الإيصالات، أو بناء أرشيف قابل للبحث، فإن الحصول على نتائج OCR موثوقة على نطاق واسع قد يبدو كصعود تلٍّ حاد.

الخبر السار؟ باستخدام مكتبة **aocr** يمكنك إنشاء دفعة OCR كاملة في بايثون ببضع أسطر فقط. في هذا الدليل سنستعرض كيفية إنشاء دفعة OCR، تحميل كل صورة مدعومة من مجلد، اختيار وضع **recognition mode printed** المناسب، وحتى ربط **AI postprocessor** للحصول على دفعة إضافية من الدقة. في النهاية ستحصل على سكريبت جاهز للتنفيذ يستخرج النص من الصور ويخبرك بكمية النص المستخرج لكل ملف.

## ما ستتعلمه

- كيفية تثبيت واستيراد حزمة `aocr`.
- إعداد `OcrBatch` لمعالجة آلاف الملفات تلقائيًا.
- اختيار وضع التعرف الأمثل للمستندات المطبوعة.
- (اختياري) ربط معالج ما بعد الذكاء الاصطناعي لتنظيف النتائج المشوشة.
- عرض مسار كل ملف جنبًا إلى جنب مع طول النص المستخرج منه.
- نصائح للتعامل مع الحالات الخاصة مثل الصيغ غير المدعومة أو الصفحات الفارغة.

### المتطلبات المسبقة

- Python 3.8 أو أحدث مثبت على جهازك.  
- إلمام أساسي ببرمجة بايثون (الحلقات، الاستيراد، إلخ).  
- وجود مجلد يحتوي على صور ممسوحة (PNG, JPG, TIFF, إلخ).  

إذا كان لديك كل ذلك، فلنبدأ—بدون الحاجة إلى خدمات خارجية.

## الخطوة 1: تثبيت مكتبة aocr

أولاً وقبل كل شيء. حزمة `aocr` ليست جزءًا من المكتبة القياسية، لذا ستحتاج إلى سحبها من PyPI.

```bash
pip install aocr
```

> **نصيحة احترافية:** استخدم بيئة افتراضية (`python -m venv .venv`) لعزل الاعتمادات.  

بعد التثبيت، يمكنك استيراد الفئات الأساسية.

```python
# core imports
import aocr
```

## الخطوة 2: إنشاء كائن OcrBatch

`OcrBatch` هو العنصر الأساسي الذي سيزحف في الدليل الخاص بك ويتتبع كل ملف صورة. فكر فيه كحزام ناقل يرسل الصور إلى محرك OCR.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

في هذه المرحلة تكون الدفعة فارغة، لكننا سنملأها في الخطوة التالية.

## الخطوة 3: إضافة جميع الصور المدعومة من مجلد (بشكل متكرر)

من المحتمل أن يكون لديك هيكل مجلدات متداخل—ربما مجلد فرعي لكل عميل أو لكل شهر. طريقة `add_folder` تمشي الشجرة لك، وتضيف كل صورة يعرف كيف يقرأها.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

استبدل `"YOUR_DIRECTORY/scanned_forms/"` بالمسار الفعلي على نظامك. بعد هذا الاستدعاء، يحتوي `ocr_batch.file_paths` على قائمة بأسماء الملفات المطلقة، وتعرف الدفعة بالضبط عدد العناصر التي ستعالجها.

## الخطوة 4: اختيار وضع التعرف للنص المطبوع

محرك `aocr` يدعم عدة أوضاع (يدوي، مطبوع، مختلط). بما أننا نتعامل مع نماذج مطبوعة نظيفة، اضبط الوضع وفقًا لذلك. هذه العلامة الصغيرة يمكن أن تحسن الدقة بشكل كبير لأن المحرك يتخطى الخوارزميات الثقيلة المطلوبة للخطوط المتصلة.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **لماذا يهم:** النص المطبوع يمتلك خطوطًا أساسية وأشكال حروف ثابتة، مما يسمح لنموذج OCR باستخدام قواميس حروف أكثر تحديدًا. إذا تركت الوضع على “auto” قد تحصل على ضوضاء إضافية في المسحات منخفضة الدقة.

## الخطوة 5: (اختياري) ربط معالج ما بعد الذكاء الاصطناعي

إذا كانت مسحاتك تعاني من تشويش، انخفاض التباين، أو خطوط غير مألوفة، يمكن لمعالج ما بعد الذكاء الاصطناعي تنظيف ناتج OCR الخام قبل إرساله إلى الأنظمة اللاحقة. طريقة `set_ai_postprocessor` تتوقع كائنًا يطبق واجهة `process(text: str) -> str`.

فيما يلي مثال بسيط باستخدام فئة خيالية `SimpleCleaner`. عمليًا يمكنك توصيل محول من HuggingFace، نموذج لغة مخصص، أو حتى مدقق إملائي قائم على القواعد.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

إذا تخطيت هذه الخطوة، ستعيد الدفعة سلاسل OCR الخام فقط.

## الخطوة 6: تشغيل OCR على الدفعة بالكامل وجمع النتائج

الآن يبدأ العمل الشاق. طريقة `run` تتكرر على كل ملف، تشغل محرك OCR، تمرّر الناتج عبر معالج AI الاختياري، وتعيد قائمة من السلاسل—واحدة لكل صورة.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

نظرًا لأن الطريقة تُعيد قائمة بايثون عادية، يمكنك التعامل معها كأي مجموعة أخرى—تخزينها، كتابتها إلى CSV، أو إدخالها في قاعدة بيانات.

## الخطوة 7: عرض مسار كل ملف مع طول النص المستخرج

فحص سريع للمنطق هو طباعة عدد الأحرف المستخرجة من كل ملف. إذا كانت الصفحة فارغة أو فشل OCR، سترى طولًا يساوي `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

المخرجات النموذجية تكون كالتالي:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

رؤية علامة `0` تُخبرك فورًا أي الملفات تحتاج مراجعة ثانية (ربما تكون تالفة أو ليست صورة أصلاً).

## التعامل مع الحالات الشائعة

### 1. صيغ الملفات غير المدعومة

يتخطى `aocr` بصمت الملفات التي لا يستطيع فك تشفيرها. إذا كنت تشك بوجود ملفات PDF أو BMP مختلطة، قم بفلترتها مسبقًا:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. دفعات كبيرة واستهلاك الذاكرة

معالجة آلاف المسحات عالية الدقة قد ترفع استهلاك الذاكرة. خفّف ذلك بمعالجة الدفعات على أجزاء:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. صفحات فارغة أو منخفضة التباين

إذا أعطت صفحة أقل من 10 أحرف، قد ترغب في وضع علامة عليها للمراجعة اليدوية:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## مثال كامل يعمل

بتجميع كل ما سبق، إليك سكريبت يمكنك نسخه ولصقه وتشغيله فورًا. احفظه باسم `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**المخرجات المتوقعة** (مقتصرة للعرض):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

شغّله باستخدام:

```bash
python batch_ocr.py
```

إذا تم إعداد كل شيء بشكل صحيح، سترى سطرًا لكل صورة، كل سطر يوضح عدد الأحرف المستخرجة من النص.

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات PDF؟**  
ج: ليس مباشرة. `aocr` يتعامل فقط مع الصور النقطية. حوّل ملفات PDF إلى PNG/TIFF أولًا (مثلاً باستخدام `pdf2image`).

**س: هل يمكنني تغيير وضع التعرف إلى يدوي؟**  
ج: بالتأكيد—استبدل `aocr.RecognitionMode.PRINTED` بـ `aocr.RecognitionMode.HANDWRITTEN`. سيتطلب ذلك وقت تشغيل أطول لكن سيعطي نتائج أفضل على الملاحظات المكتوبة بخط اليد.

**س: ماذا لو احتجت دعمًا متعدد اللغات؟**  
ج: المكتبة تأتي بحزم لغات. ثبّت حزمة اللغة المطلوبة (`pip install aocr-lang-fr` للفرنسية، إلخ) واضبط `ocr_batch.language = "fr"` قبل التشغيل.

## الخطوات التالية والمواضيع ذات الصلة

- **المعالجة المتوازية:** غلف تنفيذ الدفعة في `concurrent.futures.ThreadPoolExecutor` لاستغلال عدة نوى CPU.  
- **تخزين النتائج:** اكتب `ocr_results` إلى CSV أو قاعدة بيانات SQLite للتحليلات اللاحقة.  
- **التكامل مع سحابة AI:** استبدل `SimpleCleaner` بنموذج محول من HuggingFace لتصحيح إملائي متقدم.  
- **تحسين aocr:** إذا كان لديك مجموعة خطوط مخصصة، استكشف `aocr.Trainer` لتحسين دقة وضع الطباعة.

---

هذا كل شيء—الآن لديك أساس قوي


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}