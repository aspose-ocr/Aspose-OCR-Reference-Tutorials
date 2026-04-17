---
category: general
date: 2026-03-28
description: تعلم كيفية تحويل ملفات PDF إلى نص باستخدام OCR وPython بسرعة. يوضح لك
  هذا الدليل كيفية استخراج النص من ملفات PDF، والتعرف على النص في ملفات PDF، وتحويل
  ملفات PDF الممسوحة ضوئياً إلى نص باستخدام Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: ar
og_description: تعلّم كيفية التعرف الضوئي على الأحرف (OCR) لملفات PDF باستخدام بايثون.
  استخرج النص من PDF، تعرف على النص داخل PDF، وحوّل ملفات PDF الممسوحة ضوئياً إلى
  نص خلال دقائق.
og_title: كيفية التعرف الضوئي على النص في ملفات PDF باستخدام بايثون – دليل كامل
tags:
- PDF
- OCR
- Python
- Aspose
title: كيفية التعرف الضوئي على النص في ملفات PDF باستخدام بايثون – دليل خطوة بخطوة
url: /ar/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على النص في ملفات PDF باستخدام بايثون – دليل خطوة بخطوة

هل تساءلت يومًا **how to OCR PDF** عندما يكون الملف مجرد صورة لصفحة؟ لست وحدك. في هذا الدرس سنستعرض الخطوات الدقيقة للتعرف الضوئي على النص في ملفات PDF، استخراج النص من PDF، وتحويل PDF الممسوح ضوئيًا إلى نص قابل للبحث—كل ذلك باستخدام كود بايثون بسيط.

سنغطي كل شيء من تثبيت مكتبة Aspose OCR إلى استخراج النص المعترف به من كل صفحة. في النهاية ستكون قادرًا على **OCR PDF with Python**، **extract text from PDF**، و**convert scanned PDF to text** دون الحاجة للبحث في وثائق متفرقة. لا إطالة، مجرد مثال عملي يمكنك نسخه ولصقه.

## ما ستحتاجه

قبل أن نبدأ، تأكد من توفر ما يلي:

* Python 3.8+ (أحدث إصدار مستقر هو الأفضل)  
* رخصة Aspose OCR for Python أو مفتاح تجربة مجانية – يمكنك الحصول عليه من موقع Aspose.  
* ملف PDF ممسوح ضوئيًا تريد معالجته (سنسميه `input.pdf`).  

إذا كان لديك كل ذلك، رائع—لنبدأ. إذا لم يكن كذلك، تثبيت الحزمة سهل وسنوضح لك الطريقة.

## كيفية التعرف الضوئي على النص في PDF – إعداد البيئة

أول شيء عليك فعله هو الحصول على وحدة Aspose OCR على جهازك. الحزمة تسمى `aspose-ocr`، ويمكنك تثبيتها عبر pip:

```bash
pip install aspose-ocr
```

> **نصيحة احترافية:** استخدم بيئة افتراضية (`python -m venv venv`) لتبقى تبعياتك منظمة.

بعد تثبيت الحزمة، يمكنك استيرادها وبدء تشغيل محرك OCR. هذا هو الأساس لكل سير عمل **ocr pdf with python** ستبنيه لاحقًا.

## OCR PDF with Python – استيراد Aspose OCR

الآن بعد أن المكتبة متاحة، لنقم بإدخالها في السكريبت. سنضبط أيضًا المحرك للعمل في *وضع PDF المباشر*، الذي يخبر Aspose بقراءة بايتات PDF مباشرة من الملف بدلاً من تحويل كل صفحة إلى صورة أولاً.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

لماذا نستخدم `PdfMode.DIRECT`؟ لأنه يتخطى خطوة الرستر الإضافية، مما يجعل العملية أسرع ويحافظ على التخطيط الأصلي—مفيد جدًا عندما تحتاج إلى **recognize text from PDF** بدقة.

## التعرف على النص من PDF – تشغيل المحرك

مع جاهزية المحرك، وجهه إلى ملفك الممسوح. طريقة `recognize_from_pdf` تقوم بكل العمل الشاق: تحلل كل صفحة، تشغل خوارزمية OCR، وتعيد كائن `OcrResult` يحتوي على مجموعة من كائنات `Page`.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

إذا كنت تتساءل عما إذا كان هذا يعمل مع ملفات PDF المشفرة—نعم، طالما زودت كلمة المرور عبر `ocr_engine.password = "secret"` قبل استدعاء `recognize_from_pdf`. هذه حالة حافة يتجاهلها كثير من الدروس، لكنها مفيدة في خطوط الأنابيب الواقعية.

## استخراج النص من PDF – الوصول إلى نتائج الصفحات

قائمة `ocr_result.pages` تحتفظ بإدخال واحد لكل صفحة. كل كائن `Page` يمتلك خاصية `.text` التي تحتوي على تمثيل النص العادي للصفحة الممسوحة. لنقم بالتكرار عبرها وطباعة النتائج لتتمكن من رؤية ما تم استخراجها بالضبط.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

تشغيل السكريبت سيظهر شيئًا مشابهًا لـ:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

هذا الإخراج يثبت أنك نجحت في **extract text from PDF** و**recognize text from PDF** باستخدام Aspose OCR. الآن يمكنك تمرير السلاسل إلى قاعدة بيانات، فهرس بحث، أو أي خط أنابيب NLP لاحق.

![how to ocr pdf example](placeholder-image.png "how to ocr pdf example")

*نص بديل للصورة:* **how to ocr pdf example** – يُظهر مخرجات وحدة التحكم للنص المعترف به لكل صفحة.

## تحويل PDF الممسوح إلى نص – حفظ الناتج

معظم المطورين لا يرغبون فقط في رؤية النص على وحدة التحكم؛ هم بحاجة إلى ملف دائم. أدناه مثال صغير يكتب نص كل صفحة إلى ملف `.txt` منفصل، مما يحقق **convert scanned PDF to text** في مجلد يُسمى `output`.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

بعد انتهاء السكريبت ستحصل على دليل منظم:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

الآن قد أتممت **convert scanned PDF to text** ويمكنك إمداد تلك الملفات إلى أي عملية لاحقة—بحث، تحليلات، أو حتى أمر `grep` بسيط.

## أسئلة شائعة وحالات خاصة

**ماذا لو كان PDF يحتوي على صور مختلطة مع نص حقيقي؟**  
سوف يحاول Aspose OCR التعرف على كل شيء، لكن يمكنك تسريع العملية بتعطيل OCR للصفحات التي تحتوي بالفعل على نص قابل للتحديد. اضبط `ocr_engine.auto_detect_page_orientation = True` ثم استدعِ `ocr_engine.recognize_from_pdf(..., detect_text=False)` للصفحات المعروفة.

**هل يمكنني التحكم في نموذج اللغة؟**  
بالطبع. اضبط `ocr_engine.language = aocr.Language.English` (أو أي لغة مدعومة) قبل استدعاء `recognize_from_pdf`. هذا يحسن الدقة للوثائق غير الإنجليزية.

**كيف أتعامل مع ملفات PDF ضخمة (أكثر من 100 صفحة)؟**  
عالجها على دفعات. طريقة `recognize_from_pdf` تقبل معامل `page_range`، مثال: `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. كرر على النطاقات للحفاظ على استهلاك الذاكرة منخفضًا.

## مثال كامل يعمل

نجمع كل ما سبق في سكريبت واحد يمكنك وضعه في ملف اسمه `ocr_pdf.py` وتشغيله:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

شغّله باستخدام:

```bash
python ocr_pdf.py
```

سترى مخرجات وحدة التحكم التي تؤكد نص كل صفحة وموقع ملفات `.txt` المحفوظة.

## الخلاصة

غطّينا **how to OCR PDF** باستخدام بايثون، عرضنا طريقة نظيفة لـ **ocr pdf with python**، أظهرنا لك كيفية **extract text from PDF**، شرحنا آلية **recognize text from PDF**، وأخيرًا قدمنا مقتطفًا جاهزًا لـ **convert scanned PDF to text**. العملية بأكملها مغلفة

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}