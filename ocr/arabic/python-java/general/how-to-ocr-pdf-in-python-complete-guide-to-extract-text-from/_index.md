---
category: general
date: 2026-06-22
description: تعلم كيفية التعرف الضوئي على النص (OCR) لملفات PDF باستخدام بايثون، استخراج
  النص من PDF، وتحويل PDF إلى نص باستخدام نهج يعتمد على التدفق. خطوات بسيطة لمعالجة
  ملفات PDF الممسوحة ضوئياً.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: ar
og_description: كيف تقوم بعملية OCR لملفات PDF في بايثون؟ اتبع هذا الدليل لاستخراج
  النص من PDF، وتحويل PDF إلى نص، ومعالجة PDF الممسوح ضوئياً باستخدام تدفق.
og_title: كيفية التعرف الضوئي على النص في ملفات PDF باستخدام بايثون – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: كيفية إجراء OCR لملف PDF في بايثون – دليل شامل لاستخراج النص من ملفات PDF
url: /ar/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على الحروف (OCR) لملفات PDF في بايثون – دليل شامل لاستخراج النص من ملفات PDF

هل تساءلت يومًا **كيفية التعرف الضوئي على الحروف (OCR) لملفات PDF** دون التعامل مع أدوات سطح المكتب الضخمة؟ لست وحدك. في العديد من المشاريع الواقعية—مثل أتمتة الفواتير أو رقمنة المسحات الأرشيفية—تحتاج إلى طريقة موثوقة لتحويل ملف PDF ممسوح ضوئيًا إلى نص قابل للبحث والتحرير.

في هذا الدرس سنستعرض مثالًا نظيفًا وشاملًا ي **يستخرج النص من صفحات PDF** باستخدام محرك OCR خفيف الوزن في بايثون. بنهاية الدرس ستعرف بالضبط **كيفية تحويل PDF إلى نص**، **كيفية تحميل PDF من تدفق**، و**كيفية معالجة PDF الممسوح** بكفاءة. لا سحر، مجرد كود بايثون بسيط يمكنك إضافته إلى مشروعك اليوم.

## ما ستتعلمه

- تثبيت وتكوين مكتبة OCR بايثون تدعم إدخال PDF.  
- تمكين وضع التعرف على PDF وتحديد صيغة الإخراج كنص عادي.  
- تحميل PDF متعدد الصفحات من تدفق ملف (نمط “تحميل PDF من تدفق” الكلاسيكي).  
- تشغيل OCR على جميع الصفحات واسترجاع المحتوى النصي.  
- طباعة أو تخزين النتائج للمعالجة اللاحقة.

**المتطلبات المسبقة**  
- Python 3.8+ مثبت على جهازك.  
- إلمام أساسي بـ pip وبيئات الافتراضية.  
- ملف PDF ممسوح ضوئيًا (اسمه `multipage.pdf` في المثال) موجود في دليل معروف.

إذا كان أي من ذلك غير مألوف لك، لا تقلق—كل خطوة مشروحة بلغة بسيطة، وسنقدم لك الأوامر الدقيقة التي تحتاجها.

---

## الخطوة 1: تثبيت محرك OCR (كيفية التعرف الضوئي على الحروف لملفات PDF)

أولًا وقبل كل شيء—تحتاج إلى محرك OCR يمكنه التعامل مع إدخال PDF. في هذا الدليل سنستخدم الحزمة الافتراضية `ocr` (واجهة البرمجة تشبه SDKs التجارية الشهيرة، لكن نفس النمط يعمل مع Tesseract‑OCR، ABBYY، أو Google Vision عند تغليفه بشكل مناسب).

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **نصيحة احترافية:** إذا كنت تستخدم Windows وواجهت أخطاء أذونات، جرّب `pip install --user ocr` بدلاً من ذلك.

بعد تثبيت الحزمة، يمكنك استيرادها في سكريبتك وإنشاء نسخة من المحرك—هذا هو جوهر **كيفية التعرف الضوئي على الحروف لملفات PDF**.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

كائن `OcrEngine` يحتوي على جميع الإعدادات التي سنضبطها لاحقًا، مثل اللغة، DPI،—والأهم—وضع PDF.

## الخطوة 2: تمكين التعرف على PDF واختيار الإخراج (استخراج النص من PDF)

بشكل افتراضي، تفترض العديد من SDKs الخاصة بـ OCR أنك تزودها بصور. لجعل المحرك يتعامل مع التدفق الوارد كملف PDF، نقوم بتمكين علامة التعرف على PDF ونطلب إخراج نص عادي.

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

لماذا نحتاج لتحديد صيغة الإخراج؟ لأن بعض المحركات يمكنها إرجاع PDF بطبقة نص مخفية، أو PDF قابل للبحث، أو JSON يحتوي على إطارات الحدود. بالنسبة لمعظم خطوط استخراج البيانات، **استخراج النص من PDF** كسلاسل نصية هو أنظف تنسيق للمعالجة اللاحقة.

## الخطوة 3: تحميل PDF من تدفق ملف (تحميل PDF من تدفق)

تحميل PDF من تدفق هو نمط فعال من حيث الذاكرة—تتجنب تحميل الملف بالكامل إلى RAM مرة واحدة. هذا مفيد بشكل خاص عند التعامل مع مستندات متعددة الصفحات كبيرة الحجم.

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **ماذا لو كان الملف على S3 أو دلو سحابي آخر؟**  
> ببساطة استبدل `from_file` بطريقة تقبل مخزن بايتات (مثلاً `ImageStream.from_bytes(s3_object.read())`). يبقى باقي خط الأنابيب كما هو.

## الخطوة 4: تشغيل OCR على جميع الصفحات (معالجة PDF الممسوح)

الآن يبدأ العمل الجاد. سيقوم المحرك بالتكرار عبر كل صفحة، تشغيل محرك التعرف، وإرجاع قائمة من كائنات الصفحات—كل منها يتيح الوصول إلى محتواه النصي.

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

خلف الكواليس، تقوم مكتبة OCR بفك ضغط كل صفحة PDF، تحويلها إلى صورة raster بدقة DPI المحددة، وتمرير البت ماب عبر نموذج الشبكة العصبية الخاص بها. النتيجة؟ مجموعة من كائنات `Page` جاهزة للاستخراج.

## الخطوة 5: استرجاع وعرض النص المعترف به (تحويل PDF إلى نص)

أخيرًا، نمر على الصفحات المسترجعة ونطبع النص المعترف به. هذه هي اللحظة التي يحدث فيها **تحويل PDF إلى نص** فعليًا.

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### النتيجة المتوقعة

إذا كان `multipage.pdf` يحتوي على ثلاث صفحات ممسوحة، سترى شيئًا مشابهًا لـ:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

لاحظ الفصل الواضح بين الصفحات—مفيد إذا كنت تحتاج لتخزين نص كل صفحة في قاعدة بيانات أو إرساله إلى نموذج NLP لاحق.

## معالجة الحالات الشائعة

### 1. ملفات PDF ذات طبقات صورة ونص مختلطة
بعض ملفات PDF تحتوي بالفعل على طبقة نص مخفية (مثلاً تم تصديرها من Word). إذا أردت أن يتجاهل محرك OCR **النص الموجود** ويعيد معالجة الصورة، اضبط:

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. ملفات كبيرة تتجاوز حدود الذاكرة
عند العمل مع ملفات PDF بحجم جيجابايت، فكر في المعالجة على دفعات:

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. دعم اللغة والخط
إذا كانت مستنداتك الممسوحة ضوئيًا بالفرنسية أو تحتوي على أحرف خاصة، أخبر المحرك أي نموذج لغة يستخدم:

```python
settings.set_language("fr")   # or "en", "de", etc.
```

## السكريبت الكامل – جاهز للتنفيذ

فيما يلي المثال الكامل القابل للتنفيذ الذي يجمع كل الأجزاء معًا. احفظه باسم `ocr_pdf.py` وشغّله باستخدام `python ocr_pdf.py`.

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**تشغيل السكريبت** سيطبع نص كل صفحة إلى وحدة التحكم، تمامًا كما هو موضح في قسم “النتيجة المتوقعة”. من هنا يمكنك توجيه الإخراج إلى ملف:

```bash
python ocr_pdf.py > extracted_text.txt
```

## الخلاصة

لقد غطينا للتو **كيفية التعرف الضوئي على الحروف لملفات PDF** في بايثون من البداية إلى النهاية. من خلال تكوين المحرك، تحميل المستند عبر تدفق، والتكرار على كل صفحة معترف بها، يمكنك **استخراج النص من PDF**، **تحويل PDF إلى نص**، و**معالجة PDF الممسوح** ببضع أسطر فقط. النهج قابل للتوسع من الفواتير ذات الصفحتين الصغيرة إلى أرشيفات مئات الصفحات الضخمة.

ما الخطوة التالية؟ جرّب إمداد السلاسل المستخرجة إلى فهرس بحث، ملخص نموذج لغة، أو خط أنابيب للتحقق من البيانات. يمكنك أيضًا تجربة صيغ إخراج مثل JSON للاحتفاظ ببيانات الموقع لتحليل المستندات المتقدم.

هل لديك أسئلة حول التعامل مع ملفات PDF المشفرة أو التكامل مع التخزين السحابي؟ اترك تعليقًا أدناه—برمجة سعيدة! 

![مخطط يوضح سير عمل OCR للـ PDF – كيفية التعرف الضوئي على PDF، تحميل PDF من تدفق، التعرف على الصفحات، واستخراج النص](ocr-pdf-workflow.png "مخطط سير عمل كيفية التعرف الضوئي على PDF")

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية التعرف الضوئي على PDF في .NET باستخدام Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [كيفية استخراج النص من صورة باستخدام Aspose.OCR لـ .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [كيفية استخراج النص من أرشيفات ZIP باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}