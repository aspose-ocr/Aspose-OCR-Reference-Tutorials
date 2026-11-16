---
category: general
date: 2026-07-05
description: تحويل PDF إلى نص باستخدام OCR في بايثون. تعلّم كيفية استخراج النص من
  PDF، إجراء معالجة OCR على دفعات، وتحميل PDF للـ OCR في بضع خطوات سهلة.
draft: false
keywords:
- convert pdf to text
- extract text from pdf
- batch ocr processing
- load pdf for ocr
- recognize scanned pdf
language: ar
og_description: تحويل PDF إلى نص بسرعة. يوضح هذا الدرس كيفية استخراج النص من PDF،
  وتشغيل معالجة OCR دفعةً واحدة، والتعرف على ملفات PDF الممسوحة ضوئياً باستخدام بايثون.
og_title: تحويل PDF إلى نص باستخدام OCR في بايثون – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  headline: Convert PDF to Text with Python OCR – Complete Guide
  type: TechArticle
- description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  name: Convert PDF to Text with Python OCR – Complete Guide
  steps:
  - name: '**Chunked Loading** – Some libraries let you load a range of pages:'
    text: '**Chunked Loading** – Some libraries let you load a range of pages:'
  - name: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
    text: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
  - name: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
    text: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
  - name: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
    text: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
  - name: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
    text: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
  type: HowTo
tags:
- OCR
- Python
- PDF
title: تحويل PDF إلى نص باستخدام OCR في بايثون – دليل كامل
url: /ar/python-java/general/convert-pdf-to-text-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل PDF إلى نص باستخدام Python OCR – دليل كامل

هل تساءلت يوماً كيف **convert PDF to text** دون عناء؟ ربما لديك مجموعة من العقود الممسوحة ضوئياً، الفواتير، أو الأوراق البحثية وتحتاج إلى نسخة نصية صافية للفهرسة أو التحليل. الخبر السار هو أن بضع أسطر من Python يمكنها القيام بالعمل الشاق نيابةً عنك.

في هذا الدرس سنستعرض حلاً عملياً لا يقتصر فقط على **convert pdf to text**، بل يوضح لك أيضاً كيفية **extract text from pdf**، إعداد **batch OCR processing**، وتحميل **pdf for OCR** بشكل صحيح. في النهاية ستحصل على سكريبت جاهز للتنفيذ يمكنه **recognize scanned pdf** في خطوة واحدة.

## ما ستتعلمه

- تثبيت وتكوين مكتبة OCR للـ Python (سنستخدم حزمة `ocr` عامة للتوضيح).  
- تحميل ملف PDF متعدد الصفحات وإرساله إلى محرك OCR.  
- التكرار عبر النتائج لطباعة أو حفظ النص المستخرج.  
- التعامل مع الحالات الشائعة مثل الملفات الكبيرة، ملفات PDF المشفرة، والوثائق متعددة اللغات.  

بدون أدوات GUI ثقيلة، بدون نسخ يدوي—فقط كود نقي يمكنك إدراجه في خط أنابيب CI أو أداة سطح مكتب.

![تحويل PDF إلى نص باستخدام Python OCR](https://example.com/images/convert-pdf-to-text.png "تحويل PDF إلى نص باستخدام Python OCR")

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| Python 3.9+ | صsyntax حديث، تلميحات نوع، وأداء أفضل. |
| مكتبة `ocr` (أو غلاف حول Tesseract) | توفر الفئات `OcrEngine`، `Language`، و `Image` المستخدمة في المثال. |
| PDF ممسوح ضوئياً متعدد الصفحات (مثال: `contract.pdf`) | هذا هو المصدر الذي ستقوم بـ **load pdf for OCR**. |
| إلمام أساسي بسطر الأوامر | لتثبيت الحزم وتشغيل السكريبت. |

إذا كنت تستخدم Tesseract تحت الغطاء، قم بتثبيته عبر مدير حزم نظام التشغيل الخاص بك (`apt-get install tesseract-ocr` على Linux، `brew install tesseract` على macOS). ثم أضف الغلاف الخاص بـ Python:

```bash
pip install ocr  # replace with the actual package name, e.g., pytesseract-wrapper
```

## الخطوة 1: إنشاء محرك OCR وتحديد لغة التعرف

أولاً، نحتاج إلى إنشاء كائن محرك OCR. تعيين اللغة إلى الإنجليزية هو الإعداد الافتراضي الشائع، لكن يمكنك التبديل إلى لغات أخرى مدعومة لاحقاً.

```python
import ocr  # hypothetical import; replace with your actual OCR package

# Initialize the OCR engine
engine = ocr.OcrEngine()

# Choose the language for recognition – ENGLISH works for most contracts
engine.language = ocr.Language.ENGLISH
```

**لماذا هذا مهم:** المحرك هو الدماغ الذي يفسر بيانات البكسل. عبر تعريف `engine.language` صراحةً، تتجنب عبء اكتشاف اللغة في كل صفحة، مما يسرّع **batch OCR processing** بشكل كبير.

## الخطوة 2: تحميل مستند PDF لـ OCR

الآن نقوم بتحميل ملف PDF إلى الذاكرة. طريقة `ocr.Image.load` يمكنها قبول مسار الملف وتعيد كائناً يفهمه المحرك.

```python
# Path to your scanned PDF; adjust as needed
pdf_path = "YOUR_DIRECTORY/contract.pdf"

# Load the PDF – this step **load pdf for OCR**
pdf_document = ocr.Image.load(pdf_path)
```

**نصيحة احترافية:** إذا كان ملف PDF محمياً بكلمة مرور، تسمح معظم المكتبات بتمرير معامل `password`. معالجة ذلك مبكراً يمنع ظهور خطأ غامض “cannot open file” لاحقاً.

## الخطوة 3: تشغيل OCR على جميع الصفحات – **recognize scanned pdf** في نداء واحد

تشغيل OCR صفحةً بصفحة قد يكون بطيئاً، خاصةً للوثائق الكبيرة. طريقة `recognize_multi_page` تقوم بـ **batch OCR processing** داخلياً، باستخدام عدة خيوط عندما يكون ذلك ممكناً.

```python
# Execute OCR across every page; returns a list of OcrResult objects
page_results = engine.recognize_multi_page(pdf_document)  # List<OcrResult>
```

**ما الذي يحدث خلف الكواليس؟** يقوم المحرك ببث كل صفحة إلى محرك OCR الأساسي (مثل Tesseract)، يجمع النص، ويغلفه في كائن `OcrResult`. هذا النهج يقلل من عبء الإدخال/الإخراج ويمنحك طريقة نظيفة لـ **extract text from pdf** لاحقاً.

## الخطوة 4: التكرار عبر النتائج وإخراج النص المعترف به

أخيراً، نمر على كل `OcrResult` ونطبع النص. يمكنك أيضاً كتابة كل صفحة إلى ملف `.txt` منفصل أو دمجها في مستند واحد.

```python
for page_number, result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(result.text)
    # Optional: save to a file
    # with open(f"page_{page_number}.txt", "w", encoding="utf-8") as f:
    #     f.write(result.text)
```

**لماذا نستخدم enumerate؟** استخدام `enumerate(..., start=1)` يمنحك رقم صفحة مقروء للبشر، وهو مفيد عندما تحتاج لاحقاً للإشارة إلى قسم معين من PDF الأصلي.

### النتيجة المتوقعة

تشغيل السكريبت على عقد مكوّن من 3 صفحات قد ينتج ما يلي:

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed...
```

إذا كانت صفحة لا تحتوي على نص قابل للتعرف، فإن `result.text` سيكون سلسلة فارغة—مما يسهل اكتشاف الصفحات الفارغة أو التي تحتوي على صورة فقط.

## التعامل مع ملفات PDF الكبيرة وقيود الذاكرة

معالجة PDF مكوّن من 500 صفحة قد تستنزف الذاكرة إذا قمت بتحميل كل شيء دفعة واحدة. إليك استراتيجيتان:

1. **تحميل مقسّم** – تسمح بعض المكتبات بتحميل نطاق من الصفحات:

   ```python
   for start in range(0, total_pages, 50):  # process 50 pages at a time
       chunk = pdf_document.select_pages(start, start + 49)
       chunk_results = engine.recognize_multi_page(chunk)
       # handle chunk_results as before
   ```

2. **البث إلى القرص** – اكتب نص كل صفحة مباشرة إلى ملف بدلاً من الاحتفاظ بالقائمة بالكامل في الذاكرة.

كلا التقنيتين تحافظان على قابلية توسيع سير عمل **convert pdf to text**.

## معالجة الأخطاء والحالات الطرفية

- **PDF مشفر** – مرّر كلمة المرور إلى `Image.load`:

  ```python
  pdf_document = ocr.Image.load(pdf_path, password="mySecret")
  ```

- **لغات مختلطة** – غيّر اللغة لكل صفحة إذا اكتشفت نصاً بلغة مختلفة:

  ```python
  if detect_spanish(result.text):
      engine.language = ocr.Language.SPANISH
  ```

- **مسحات منخفضة الدقة** – عالج الصور مسبقاً باستخدام مكتبة مثل `Pillow` لزيادة التباين قبل OCR. هذا يمكن أن يحسّن بشكل كبير خطوة **recognize scanned pdf**.

## السكريبت الكامل: تحويل PDF إلى نص في تشغيل واحد

فيما يلي السكريبت الكامل الجاهز للتنفيذ الذي يجمع كل شيء معاً. احفظه باسم `pdf_to_text.py` وشغّله بالأمر `python pdf_to_text.py`.

```python
#!/usr/bin/env python3
"""
convert_pdf_to_text.py

A self‑contained script that demonstrates how to convert PDF to text using
Python OCR. It covers loading the PDF, batch processing, and handling common
edge cases.
"""

import os
import ocr  # Replace with your actual OCR package

def convert_pdf_to_text(pdf_path: str, output_dir: str = "output"):
    """Convert a scanned PDF into plain‑text files, one per page."""
    if not os.path.isfile(pdf_path):
        raise FileNotFoundError(f"PDF not found: {pdf_path}")

    os.makedirs(output_dir, exist_ok=True)

    # Step 1 – create engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – load PDF (supports password argument if needed)
    pdf_document = ocr.Image.load(pdf_path)

    # Step 3 – run batch OCR
    page_results = engine.recognize_multi_page(pdf_document)

    # Step 4 – write each page's text to a file
    for page_number, result in enumerate(page_results, start=1):
        page_text = result.text.strip()
        out_file = os.path.join(output_dir, f"page_{page_number}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

        # Also echo to console for quick sanity check
        print(f"--- Page {page_number} ---")
        print(page_text[:200] + ("…" if len(page_text) > 200 else ""))

if __name__ == "__main__":
    # Example usage – adjust the path to your PDF file
    PDF_PATH = "YOUR_DIRECTORY/contract.pdf"
    convert_pdf_to_text(PDF_PATH)
```

**تشغيل السكريبت** سيخلق مجلد `output` يحتوي على `page_1.txt`، `page_2.txt`، إلخ، مما يحقق **extract text from pdf** بطريقة منظمة.

## اختبار الحل

1. **التحقق الأساسي** – افتح ملف `.txt` تم إنشاؤه وتأكد من أن السطور القليلة الأولى تطابق عنوان المستند الأصلي.  
2. **اختبار الأداء** – قس زمن تشغيل السكريبت على PDF مكوّن من 100 صفحة باستخدام أمر `time`. إذا استغرق وقتاً أطول من المتوقع، ففكّر في تمكين خيار تعدد الخيوط في المكتبة (غالباً `engine.set_threads(4)`).  
3. **ضمان الجودة** – قارن مخرجات OCR مع مقتطف مكتوب يدوياً باستخدام أداة diff. استهدف دقة حرفية >95 % للمسحات النظيفة.

## الخطوات التالية والمواضيع ذات الصلة

- **تحسين الدقة**: جرّب ضبط `engine.dpi = 300` أو تطبيق معالجة مسبقة للصور (تصحيح الميل، إزالة الضوضاء) قبل OCR.  
- **PDF قابل للبحث**: استخدم مكتبة PDF (مثل `PyPDF2` أو `pdfplumber`) لإدراج النص المستخرج مرة أخرى في PDF الأصلي، مما يجعله قابلاً للبحث.  
- **معالجة اللغة الطبيعية**: مرّر النص المستخرج إلى spaCy أو NLTK لاستخراج الكيانات، تحليل المشاعر، أو وضع العلامات على الكلمات المفتاحية.  
- **خطوط الأنابيب الأوتوماتيكية**: اجمع هذا السكريبت مع `watchdog` لمراقبة مجلد وتفعيل **convert pdf to text** تلقائياً كلما ظهر ملف جديد.

بإتقان هذه الأنماط، ستتمكن من

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}