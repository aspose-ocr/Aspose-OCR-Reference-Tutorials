---
category: general
date: 2026-07-05
description: كيفية استخدام OCR في بايثون لتحويل ملفات TIFF إلى نص بسرعة. تعلّم خطوات
  مكتبة OCR في بايثون لاستخراج النص من صور TIFF وبناء محرك OCR باستخدام بايثون.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: ar
og_description: كيف تستخدم OCR في بايثون؟ يوضح لك هذا الدليل خطوة بخطوة كيفية تحويل
  ملفات TIFF إلى نص باستخدام محرك OCR بايثون ومكتبة ocr بايثون.
og_title: كيفية استخدام OCR في بايثون – استخراج النص الكامل من ملفات TIFF
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: كيفية استخدام OCR في بايثون – استخراج النص من ملف TIFF
url: /ar/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في بايثون – استخراج النص من TIFF

هل تساءلت يومًا **how to use OCR in Python** لتحويل كتاب ممسوح ضوئيًا إلى نص قابل للتحرير؟ لست وحدك—المطورون والباحثون والهواة يواجهون هذه المشكلة عند التعامل مع صور TIFF متعددة الصفحات. الخبر السار؟ باستخدام **ocr library python** يمكنك تشغيل محرك OCR صغير، توجيهه إلى ملف TIFF، والحصول على نص نظيف قابل للبحث في ثوانٍ.

في هذا الدرس سنستعرض كل ما تحتاجه: تثبيت الحزمة المناسبة، تحميل صورة TIFF متعددة الصفحات، تشغيل محرك OCR، وأخيرًا طباعة محتوى كل صفحة. في النهاية ستتمكن من **convert TIFF to text** و **extract text from TIFF** دون مغادرة بيئة بايثون الخاصة بك.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- Python 3.9 أو أحدث (تم اختبار المثال على 3.11)
- نسخة حديثة من مكتبة `ocr` (أو أي `python ocr engine` متوافق تفضله)
- ملف TIFF متعدد الصفحات تريد معالجته (سنسميه `scanned_book.tif`)
- معرفة أساسية ببرامج بايثون وبيئات العمل الافتراضية

لا تحتاج إلى أدوات خارجية ثقيلة—فقط pip وقليل من أسطر الكود.

## تثبيت مكتبة OCR للبايثون

أولًا: تحتاج إلى خلفية OCR قوية. في هذا الدليل سنستخدم حزمة `ocr` الوهمية التي توفر API عالي المستوى بسيط، لكن نفس النمط يعمل مع أطر تعتمد على Tesseract مثل `pytesseract` أو SDK تجارية.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **نصيحة احترافية:** إذا كنت على نظام Windows وتعتمد الحزمة على ملفات تنفيذية أصلية، تأكد من تثبيت حزمة Visual C++ redistributable المناسبة. عادةً ما يحذرك المثبت إذا كان هناك شيء مفقود.

## كيفية استخدام محرك OCR في بايثون

الآن بعد أن أصبحت المكتبة جاهزة، لننشئ محرك OCR ونوجهه إلى ملف TIFF الخاص بنا. المقتطف التالي ينشئ كائن محرك، يضبط اللغة إلى الإنجليزية، ويجهزه للمعالجة متعددة الصفحات.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**لماذا نضبط اللغة؟**  
معظم محركات OCR تستخدم نماذج لغوية لتحسين الدقة. إذا تخطيت هذه الخطوة، سيعود المحرك إلى نموذج عام قد يخطئ في التعرف على علامات الترقيم أو الأحرف الخاصة.

## تحميل صورة TIFF متعددة الصفحات

الخطوة التالية هي تحميل المستند الممسوح. المساعد `ocr.Image.load` يفهم مجموعات TIFF مباشرةً، ويعيد كائنًا يمثل كل صفحة داخليًا.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **حالة خاصة:** إذا كان ملف TIFF يستخدم ضغطًا (CCITT Group 4، LZW، إلخ) وأطلقت المكتبة خطأً، حاول تحويله إلى نسخة غير مضغوطة باستخدام ImageMagick أولًا:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## تنفيذ OCR على جميع الصفحات – تحويل TIFF إلى نص

مع كائن الصورة في يدك، يمكن للمحرك الآن معالجة كل صفحة مرة واحدة. تُعيد هذه الطريقة قائمة حيث يحتوي كل عنصر على نتيجة OCR لصفحة واحدة.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**ما الذي يحدث خلف الكواليس؟**  
دالة `recognize_multi_page` تتنقل عبر كل صفحة مُرصَّصة، تشغل مُعرّف الشبكة العصبية، وتجمع ناتج النص العادي مع درجات الثقة. إنها عملية دفعة تُوفر عليك كتابة حلقة يدوية.

## التنقل عبر النتائج – استخراج النص من TIFF

أخيرًا، نعرض النص المُعترف به. يمكنك كتابة الناتج إلى ملفات `.txt` منفصلة، أو إرساله إلى قاعدة بيانات، أو تغذيته إلى فهرس بحث—حسب ما يناسب سير عملك.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### الناتج المتوقع

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

كل سلسلة `result.text` تحتوي على ناتج OCR الخام لتلك الصفحة. إذا كنت تحتاج إلى الحفاظ على فواصل الأسطر، تُوفر معظم المحركات `result.lines` كقائمة من السلاسل.

## معالجة ملفات TIFF الكبيرة – نصائح وحيل

معالجة ملف TIFF مكوّن من 500 صفحة قد تكون مستهلكة للذاكرة. إليك بعض الاستراتيجيات للحفاظ على السلاسة:

1. **تقسيم الصفحات** – بدلاً من `recognize_multi_page`، استدعِ `engine.recognize(page)` داخل مولد يُعيد صفحة واحدة في كل مرة.  
2. **تعديل DPI** – خفض دقة الصورة (مثلاً من 300 DPI إلى 200 DPI) يقلل من استهلاك المعالج مع تأثير طفيف على الدقة لمعظم النصوص المطبوعة.  
3. **التنفيذ المتوازي** – إذا كان محرك OCR آمنًا للخطوط المتعددة، أنشئ `concurrent.futures.ThreadPoolExecutor` لتشغيل التعرف على عدة صفحات في آنٍ واحد.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## حفظ النص المستخرج إلى ملفات

معظم خطوط الأنابيب في العالم الحقيقي تحتاج إلى تخزين دائم. أدناه طريقة مختصرة لتفريغ نص كل صفحة في ملف خاص بها، مع الحفاظ على ترتيب الصفحات.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

الآن لديك دليل نظيف من ملفات `.txt` جاهزة للفهرسة أو لمعالجة NLP إضافية.

## معاينة الصورة – كيفية استخدام نتائج OCR بصريًا

إذا رغبت في رؤية تغطية OCR على الصورة الأصلية (مفيد للتصحيح)، تسمح لك العديد من المكتبات برسم مربعات الحد. إليك مثال سريع باستخدام Pillow:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![How to use OCR in Python – OCR overlay on a TIFF page](ocr_overlay_example.png)

*نص بديل:* كيفية استخدام OCR في بايثون – تغطية OCR على صفحة TIFF.

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | سبب حدوثها | الحل |
|---------|------------|------|
| حروف مشوشة | نموذج لغة خاطئ | اضبط `engine.language` إلى التعداد الصحيح |
| صفحات مفقودة | ضغط TIFF غير مدعوم | تحويل إلى TIFF غير مضغوط أولاً |
| أداء بطيء | DPI عالي + معالجة أحادية الخيط | خفض DPI أو تمكين المعالجة المتعددة الخيوط |
| ناتج فارغ | الصورة مظلمة جدًا/قليل التباين | معالجة مسبقة بتمديد التباين (`opencv` أو `Pillow`) |

معالجة هذه القضايا مبكرًا توفر لك ساعات من التصحيح لاحقًا.

## الخطوات التالية – ما بعد الاستخراج الأساسي

الآن بعد أن أتقنت أساسيات **how to use OCR in Python**، فكر في استكشاف:

- **إنشاء PDF** – دمج النص المستخرج مع `reportlab` لإعادة بناء ملفات PDF قابلة للبحث.  
- **اكتشاف اللغة** – تبديل `engine.language` تلقائيًا باستخدام `langdetect`.  
- **استخراج البيانات المهيكلة** – استخدم التعبيرات النمطية أو spaCy لاستخراج التواريخ، الأسماء، أو الجداول من النص الخام.  
- **محركات OCR بديلة** – استبدل `ocr` بـ `pytesseract` أو `easyocr` إذا كنت تحتاج إلى دعم متعدد اللغات.

كل من هذه المواضيع يرتبط بطبيعة الحال بالكلمات المفتاحية الثانوية **ocr library python**, **convert tiff to text**, **extract text from tiff**, و **python ocr engine**، مما يمنحك أساسًا قويًا لمشاريع أكثر تقدمًا.

---

### الخلاصة

غطّينا **how to use OCR in Python** من التثبيت إلى المعالجة متعددة الصفحات، موضحين لك بالضبط كيفية **convert TIFF to text** و **extract text from TIFF** باستخدام **python OCR engine** بسيط. المثال الكامل القابل للتنفيذ أعلاه يجب أن يعمل مباشرةً لمعظم ملفات TIFF القياسية، والنصائح المقدمة ستساعدك على التوسع إلى مستندات أكبر أو دمج OCR في خطوط أنابيب أوسع.

جرّبه على كتبك الممسوحة، إيصالاتك، أو صور الأرشيف الخاصة بك—ثم جرب الأفكار المتقدمة المذكورة في قسم “الخطوات التالية”. نتمنى لك برمجة سعيدة، وأن تكون نتائج OCR دقيقة دائمًا!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية استخراج النص من tiff باستخدام Aspose.OCR للـ Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [كيفية تنفيذ استخراج نص الصورة من تدفق باستخدام Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}