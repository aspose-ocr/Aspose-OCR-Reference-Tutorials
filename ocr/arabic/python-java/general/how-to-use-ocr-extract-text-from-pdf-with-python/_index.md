---
category: general
date: 2026-04-26
description: كيفية استخدام تقنية OCR على ملفات PDF الممسوحة ضوئياً، استخراج النص من
  PDF، تشغيل OCR على PDF، وتحويل PDF الممسوح إلى ملفات قابلة للبحث في بضع خطوات.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: ar
og_description: 'كيفية استخدام OCR في بايثون: تعلم كيفية استخراج النص من ملفات PDF،
  تشغيل OCR على ملفات PDF، وتحويل ملفات PDF الممسوحة ضوئياً إلى مستندات قابلة للبحث.'
og_title: كيفية استخدام OCR – دليل سريع لاستخراج النص من PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: كيفية استخدام OCR – استخراج النص من PDF باستخدام بايثون
url: /ar/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR – استخراج النص من PDF باستخدام Python

هل تساءلت يومًا **كيف تستخدم OCR** لاستخراج النص من عقد ممسوح ضوئيًا أو إيصال أو كتاب إلكتروني؟ لست وحدك. في العديد من المشاريع الواقعية يكون ملف PDF الذي تتلقاه مجرد صورة، وبدون OCR لا يمكنك البحث أو الفهرسة أو تحليل محتوياته.  

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح **كيف تستخدم OCR**، وكيف **استخراج النص من PDF**، ولماذا قد ترغب في **تحويل PDF الممسوح** إلى مستندات قابلة للبحث. سنغطي أيضًا فن **تحميل PDF كصورة** حتى يتمكن محرك OCR من رؤية كل صفحة بوضوح.

> **معاينة سريعة:** في النهاية ستحصل على سكريبت يحمل PDF متعدد الصفحات، يُجري OCR على كل صفحة، ويطبع النص المُعترف به – دون الحاجة إلى خدمات خارجية.

## ما ستحتاجه

- Python 3.9+ (أي نسخة حديثة تعمل)
- حزمة `aocr` (أو أي مكتبة OCR متوافقة توفر `OcrEngine` و `Image.load`)
- ملف PDF ممسوح ضوئيًا تريد معالجته (مثال: `contract.pdf`)
- كمية معتدلة من الذاكرة (≈ 200 ميغابايت لكل 100 صفحة عادةً ما تكون كافية)

إذا لم تقم بتثبيت مكتبة OCR بعد، نفّذ:

```bash
pip install aocr
```

> **نصيحة احترافية:** استخدم بيئة افتراضية للحفاظ على تنظيم الاعتمادات.

## الخطوة 1: تحميل PDF كصورة – القطعة الأولى من اللغز

قبل أن يحدث أي OCR، يجب تمثيل PDF كصورة. هنا يأتي دور الكلمة المفتاحية الثانوية **load pdf as image**.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*لماذا هذا مهم:* `aocr.Image.load` تقوم داخليًا بتحويل كل صفحة PDF إلى صورة نقطية يستطيع محرك OCR فهمها. إذا تخطيت هذه الخطوة ومررت ملف PDF الأصلي، سيظهر خطأ لأن المحرك يتوقع بيانات بكسل، وليس بيانات متجهية.

> **ملاحظة:** يمكن أن يكون المسار مطلقًا أو نسبيًا. تأكد من أن الملف قابل للقراءة؛ وإلا ستحصل على `FileNotFoundError`.

## الخطوة 2: تشغيل OCR على PDF – تحويل البكسلات إلى أحرف

الآن بعد أن أصبح PDF صورة، يمكننا أخيرًا **run OCR on PDF**. المقتطف التالي يعالج جميع الصفحات دفعة واحدة:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*ما الذي يحدث خلف الكواليس؟* `process_all_pages` يمر عبر الصفحات المحوّلة، يطبق نموذج OCR، ويعيد قائمة من كائنات النتيجة — واحدة لكل صفحة. كل نتيجة تحتوي على النص المعترف به، درجات الثقة، ومربعات الإحاطة (إذا احتجتها لاحقًا).

## الخطوة 3: استخراج النص من PDF – سحب السلاسل النصية

مع نتائج OCR في المتناول، يصبح استخراج النص العادي أمرًا بسيطًا. سن iterates عبر الصفحات ونطبع النتيجة، مظهرين الكلمة المفتاحية الثانوية **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**الناتج المتوقع** (مقتطع للاختصار):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

إذا كنت تحتاج النص في سلسلة واحدة، ما عليك سوى دمجه:

```python
full_text = "\n".join(r.text for r in page_results)
```

الآن لقد نجحت في **extracted text from PDF** باستخدام OCR.

## الخطوة 4: تحويل PDF ممسوح – جعله قابلًا للبحث

العديد من الأدوات اللاحقة (مثل Elasticsearch أو SharePoint) تتوقع PDF قابلًا للبحث بدلاً من تفريغ نصي عادي. يمكنك دمج ناتج OCR مرة أخرى في PDF الأصلي، وبالتالي **convert scanned PDF** إلى نسخة قابلة للبحث.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*لماذا ذلك؟* PDF القابل للبحث يحتفظ بالتخطيط الأصلي والصور مع السماح باختيار النص وفهرسته — فوز للإنسان والآلة معًا.

## المشكلات الشائعة والحالات الخاصة

### ملفات PDF متعددة الصفحات أكبر من الذاكرة

إذا كان PDF يحتوي على مئات الصفحات، قد يستهلك تحميل كل شيء مرة واحدة كل الذاكرة. مكتبة `aocr` تدعم التحميل الكسول:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

ثم عالج الصفحات واحدةً تلو الأخرى:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### مسحات منخفضة الجودة

دقة OCR تنخفض بشكل كبير مع الصور الضبابية أو ذات التباين المنخفض. قبل تمرير الصورة إلى المحرك، فكر في المعالجة المسبقة:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### دعم اللغات

بشكل افتراضي، يفترض المحرك أن اللغة إنجليزية. لت **run OCR on PDF** بلغة أخرى، عيّن رمز اللغة:

```python
ocr_engine.language = "spa"  # Spanish
```

تأكد من تثبيت نموذج اللغة المقابل.

## مثال كامل يعمل

بجمع كل ما سبق، إليك سكريبت مستقل يمكنك وضعه في ملف اسمه `ocr_pdf.py` وتشغيله فورًا:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

شغّله هكذا:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

سترى النص يُطبع على وحدة التحكم، وإذا أضفت الخيار `-o`، سيظهر PDF قابل للبحث بجوار الملف الأصلي.

## نصائح احترافية وأفضل الممارسات

- **معالجة دفعات:** عند التعامل مع عشرات ملفات PDF، غلف المنطق أعلاه في حلقة وسجّل نجاح/فشل كل ملف.
- **تصفية الثقة:** كل `page_result` يتضمن مقياس ثقة. احذف أو علم الصفحات ذات الثقة المنخفضة للمراجعة اليدوية.
- **التوازي:** إذا كان معالجك متعدد النوى، فكر في استخدام `concurrent.futures` لمعالجة الصفحات بشكل متوازي — مع مراعاة استهلاك الذاكرة.
- **قفل الإصدار:** واجهة `aocr` قد تتطور. قم بتثبيت نسخة محددة في `requirements.txt` (مثال: `aocr==2.3.1`) لتجنب التغييرات المفاجئة.

## الخلاصة

استعرضنا **how to use OCR** لـ **extract text from PDF**، **run OCR on PDF**، **load PDF as image**، وحتى **convert scanned PDF** إلى صيغة قابلة للبحث. الكود كامل، والشروحات تغطي الـ *what* والـ *why*، والآن لديك نمط قابل لإعادة الاستخدام لأي مشروع يتعامل مع PDFs مبنية على الصور.

ما التالي؟ جرّب إمداد النص المستخرج إلى خط أنابيب معالجة لغة طبيعية، أو فهرسة PDFs القابلة للبحث باستخدام Elasticsearch، أو تجربة محركات OCR مختلفة مثل Tesseract أو Azure Computer Vision. السماء هي الحد، والأدوات بين يديك.

برمجة سعيدة، ولتكن ملفات PDF الخاصة بك دائمًا قابلة للبحث! 

![مثال على كيفية استخدام OCR](/images/ocr_workflow.png "كيفية استخدام OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}