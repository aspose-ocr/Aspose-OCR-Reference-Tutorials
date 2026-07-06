---
category: general
date: 2026-01-12
description: كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) للصور دفعةً واحدة بسرعة واستخراج
  النص من ملفات JPEG باستخدام بايثون. تعلم المعالجة الدفعية خطوة بخطوة مع مثال كامل
  قابل للتنفيذ.
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: ar
og_description: كيفية معالجة مجموعة من الصور عبر OCR واستخراج النص من ملفات JPEG.
  يوضح هذا الدليل خطوة بخطوة حلًا كاملًا وجاهزًا للتنفيذ بلغة بايثون.
og_title: كيفية تنفيذ التعرف الضوئي على الحروف للصور دفعةً واحدة – دليل بايثون سريع
tags:
- OCR
- Python
- image processing
title: كيفية إجراء OCR للصور على دفعات – دليل سريع لاستخراج النص من ملفات JPEG
url: /ar/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية معالجة صور OCR دفعةً – دليل سريع لاستخراج النص من ملفات JPEG

هل تساءلت يومًا **كيف تقوم بمعالجة صور OCR دفعةً** دون كتابة سكريبت منفصل لكل ملف؟ لست وحدك. في العديد من المشاريع—مسح الفواتير، الرقمنة الأرشيفية، أو مراقبة المحتوى—نحتاج إلى استخراج النص من العشرات أو المئات من ملفات JPEG دفعة واحدة. الخبر السار هو أنه يمكنك القيام بذلك ببضع أسطر من بايثون فقط، وستحصل على محرك قابل لإعادة الاستخدام يمكنك إدراجه في أي خط أنابيب.

في هذا الدرس سنوضح لك بالضبط **كيف تقوم بمعالجة صور OCR دفعةً**، ثم نستعرض استخراج النص من ملفات JPEG، ومعالجة الحالات الخاصة، والتحقق من النتيجة. بنهاية الدرس ستحصل على سكريبت مستقل يمكنك تشغيله على أي مجلد يحتوي على صور، وستفهم لماذا تُعد المعالجة الدفعية مهمة للأداء وسهولة الصيانة.

## ما ستتعلمه

- إعداد محرك OCR بسيط وتكوينه للغة الإنجليزية.  
- جمع جميع ملفات JPEG من دليل باستخدام `pathlib`.  
- استدعاء محرك OCR مرة واحدة لمعالجة الدفعة بالكامل.  
- عرض معاينة للنص المُستخرج لكل صورة.  
- نصائح للتعامل مع دفعات كبيرة، لغات مختلفة، ومشكلات شائعة.

**المتطلبات المسبقة**: Python 3.8+، مكتبة `ocr` (أو أي غلاف متوافق)، ومجلد يحتوي على صور JPEG تريد تحليلها. لا تحتاج إلى خدمات خارجية—كل شيء يعمل محليًا.

---

## الخطوة 1: تهيئة محرك OCR – جوهر كيفية معالجة صور OCR دفعةً

قبل أن نتمكن من **معالجة صور OCR دفعةً**، نحتاج إلى محرك يعرف كيف يقرأ النص. في معظم المكتبات تقوم بإنشاء كائن محرك، وتحديد اللغة اختياريًا، ثم تعيد استخدامه لكل ملف.

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*لماذا هذا مهم*: تهيئة المحرك مرة واحدة تجنّب عبء تحميل نماذج اللغة مرارًا. كما يتيح لك تعديل الإعدادات (مثل DPI، أو قائمة الأحرف المسموح بها) في مكان واحد لتطبيقها على الدفعة بأكملها.

> **نصيحة احترافية**: إذا كنت تخطط لمعالجة مستندات متعددة اللغات، غيّر `ocr.Language.ENGLISH` إلى `ocr.Language.MULTI` أو حمّل حزم لغات متعددة قبل بدء الدفعة.

---

## الخطوة 2: جمع جميع ملفات JPEG – جزء “استخراج النص من ملفات JPEG”

الآن بعد أن أصبح المحرك جاهزًا، نحتاج إلى إخباره بأي الصور سيعمل عليها. استخدام `pathlib` يجعل الكود مستقلًا عن النظام ومختصرًا.

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*لماذا هذا مهم*: بجمع قائمة الملفات أولًا، يمكننا تمرير المجموعة كاملة إلى محرك OCR في استدعاء واحد—وهذا ما يعنيه **معالجة صور OCR دفعةً**. إذا كان لديك مجلدات فرعية، يمكنك تعديل `glob("**/*.jpg")` للبحث بصورة متكررة.

> **حالة خاصة**: إذا كانت صورك تحمل امتدادات مختلطة (`.jpeg`, `.JPG`)، وسّع نمط الـ glob إلى: `image_dir.rglob("*.[jJ][pP][eE]?g")`.

---

## الخطوة 3: معالجة الدفعة بالكامل في استدعاء واحد – القوة الحقيقية للمعالجة الدفعية

معظم مكتبات OCR الحديثة توفر طريقة `process_batch` (أو ما شابه) تقبل مجموعة من مسارات الملفات. هذه هي قلب **معالجة صور OCR دفعةً** بكفاءة.

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*لماذا هذا مهم*: استدعاء دفعة واحد يقلل عدد التحولات بين بايثون وC، يبقي نموذج اللغة محملاً في الذاكرة، وغالبًا ما يتيح تنفيذًا متوازيًا داخليًا. النتيجة هي قائمة من الكائنات—كل منها يحتوي على النص المستخرج وتقييمات الثقة.

> **ملاحظة أداء**: للدفعات الضخمة جدًا (آلاف الصور)، فكر في تقسيم القائمة إلى أجزاء أصغر (مثلاً 200 ملف) لتجنب استهلاك الذاكرة الزائد.

---

## الخطوة 4: عرض معاينة للنص المستخرج – تحقق سريع

بعد انتهاء المعالجة الدفعية، من المفيد إلقاء نظرة على أول بضعة أحرف من كل نتيجة. هذا يساعدك على التأكد من أن OCR يَستخرج النص فعلاً من ملفات JPEG.

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*لماذا هذا مهم*: المعاينة القصيرة تتيح لك اكتشاف الأخطاء الواضحة (مثل ناتج فارغ أو أحرف مشوهة) دون فتح كل ملف. إذا لاحظت مشكلات منهجية، يمكنك تعديل إعدادات المحرك وإعادة تشغيل الدفعة.

> **مشكلة شائعة**: نسيان إزالة أحرف السطر الجديد قد يجعل المعاينة فوضوية. السطر `replace("\n", " ")` ينظّف ذلك.

---

## مثال عملي كامل – دمج جميع الخطوات

فيما يلي السكريبت الكامل الذي يمكنك نسخه، تعديل مسار الدليل، وتشغيله. يوضح كامل سير عمل **معالجة صور OCR دفعةً** من البداية إلى النهاية.

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**الناتج المتوقع** (عينة):

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

إذا أظهرت المعاينة نصًا ذا معنى، فقد نجحت في **استخراج النص من ملفات JPEG** باستخدام نهج دفعي.

---

## التعامل مع دفعات كبيرة وسيناريوهات متقدمة

### تقسيم الأحمال الكبيرة
عند التعامل مع آلاف الصور، قد يصبح الذاكرة عنق زجاجة. قسّم القائمة إلى أجزاء أصغر:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### تغيير اللغات
إذا كانت مستنداتك تحتوي على الفرنسية أو الإسبانية، غيّر اللغة قبل بدء الدفعة:

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### حفظ النتائج على القرص
بدلاً من الطباعة، قد ترغب في كتابة كل نتيجة OCR إلى ملف `.txt`:

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## الخلاصة

أنت الآن تعرف **كيف تقوم بمعالجة صور OCR دفعةً** وتستخرج النص من ملفات JPEG باستخدام سكريبت بايثون مختصر. بتهيئة المحرك مرة واحدة، جمع مسارات JPEG، معالجتها في دفعة واحدة، ومعاينة النتائج، تحقق السرعة والبساطة. من هنا يمكنك توسيع سير العمل—إضافة دعم متعدد اللغات، تخزين النتائج في قاعدة بيانات، أو دمج السكريبت في خط أنابيب معالجة مستندات أكبر.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال مكتبة `ocr` بـ Tesseract، جرب معالجة مسبقة مختلفة للصور (مثل العتبة أو تغيير الحجم)، أو أدخل النص المستخرج إلى نموذج معالجة لغة طبيعية لتصنيف تلقائي. السماء هي الحد، ولديك الآن أساس قوي للبناء عليه.

برمجة سعيدة، ولتكن دفعات OCR خالية من الأخطاء دائمًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}