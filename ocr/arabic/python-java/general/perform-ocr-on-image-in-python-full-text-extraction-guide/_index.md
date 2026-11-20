---
category: general
date: 2026-06-19
description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على الصورة باستخدام مكتبة OCR
  في بايثون. تعلّم كيفية اكتشاف النص من الصورة، التعرف على النص من ملف JPEG، واستخراج
  النص من الصورة الممسوحة ضوئياً بكفاءة.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: ar
og_description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على الصورة باستخدام بايثون
  واستخراج النص من الملفات الممسوحة ضوئياً. يشرح هذا الدليل خطوة بخطوة كيفية تحميل
  الصور، وتصحيح الميل، والتعرف على النص.
og_title: إجراء التعرف الضوئي على الأحرف (OCR) على صورة في بايثون – دليل استخراج النص
  الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: إجراء OCR على صورة في بايثون – دليل استخراج النص الكامل
url: /ar/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على صورة في بايثون – دليل استخراج النص الكامل

هل احتجت يوماً إلى **perform OCR on image** ملفات لكن واجهت صعوبة لأن الكود كان غامضاً؟ لست وحدك. سواءً كنت تحول مجموعة من الإيصالات الممسوحة إلى ملفات PDF قابلة للبحث أو تستخرج العناوين من صورة JPEG لمشروع علم بيانات، فإن القدرة على التعرف على النص من JPEG وغيرها من الصيغ هي مهارة أساسية لأي مطور اليوم.

في هذا الدرس سنستعرض مثالاً كاملاً قابلاً للتنفيذ يوضح لك كيفية **detect text from image** الملفات، **extract text from scanned image** المستندات، وحتى **load image for OCR** في بضع أسطر فقط. في النهاية ستحصل على مقطع شفرة جاهز للإنتاج يمكنك إدراجه في مشاريعك—بدون استيرادات مفقودة، دون اختصارات “انظر الوثائق”.

## ما ستبنيه

- برنامج بايثون صغير يخلق محرك OCR، يفعّل auto‑deskew، يحمل صورة JPEG (أو أي صيغة مدعومة)، ويطبع النص المُعترف به.
- شروحات حول **why** كل إعداد مهم، وليس فقط **how** تكتبه.
- نصائح للتعامل مع ملفات PDF متعددة الصفحات، اللغات غير الإنجليزية، ومشكلات شائعة مثل الصور الضبابية.

### المتطلبات المسبقة

- تثبيت Python 3.8+ (المثال يستخدم حزمة `ocr` المتوفرة عبر `pip install ocr-lib` – استبدلها باسم المكتبة الفعلي لديك).
- معرفة أساسية بدوال بايثون والبيئات الافتراضية.
- ملف صورة (JPEG, PNG, TIFF) تريد معالجته؛ سنستخدم `skewed_page.jpg` كعنصر نائب.

> **Pro tip:** إذا كنت على نظام Windows، شغّل الطرفية كمسؤول عند تثبيت مكتبة OCR لتجنب مشاكل الأذونات.

---

## إجراء OCR على صورة – الإعداد والتكوين

أول شيء تحتاجه هو نسخة نظيفة من محرك OCR. فكر فيه كالعقل وراء العملية؛ بدون تكوين صحيح، حتى أكثر الصور وضوحاً ستعيد نصاً غير مفهوم.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Why this matters:**  
إعداد `engine.language` يحد من مجموعة الأحرف التي يتوقعها محرك OCR، مما يعزز الدقة بشكل كبير. إذا تخطيت هذا الإعداد، سيحاول المحرك التخمين، وغالباً ما يخطئ في قراءة الكلمات البسيطة.

---

## تمكين التصحيح التلقائي للانحراف – إصلاح المسحات المائلة

الصفحات الممسوحة نادراً ما تكون مسطحة تماماً. الانحراف الطفيف قد يخلّ بتقسيم الأحرف، محوّلاً “Hello” إلى “H3llo”. علم `auto_deskew` يقوم بالعمل الشاق نيابةً عنك.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Edge case:** إذا كنت تعلم أن صورك مستقيمة بالفعل، يمكن إلغاء تفعيل التصحيح لتقليل بضع مليثانية من زمن المعالجة—مفيد عند معالجة آلاف الصفحات في مهمة دفعة.

---

## تحميل صورة للـ OCR – دعم JPEG, PNG, TIFF

الآن نقوم فعلياً بـ **load image for OCR**. طريقة `ocr.Image.load` مرنة؛ تقبل مساراً لأي صيغة نقطية مدعومة.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Why this step is crucial:** المكتبة تقرأ الملف إلى bitmap داخلي، وتطبق أي تحويل ضروري لمساحة الألوان. تخطي هذه الخطوة وتمرير تدفق بايتات خام سيسبّب `FileNotFoundError` أو، الأسوأ، ينتج نتائج فارغة بصمت.

إذا كنت بحاجة إلى **recognize text from JPEG** تحديداً، تأكد فقط من أن امتداد الملف هو `.jpeg` أو `.jpg`. نفس الاستدعاء يعمل مع PNG (`.png`) أو TIFF (`.tif`) دون تعديل.

---

## إجراء OCR على صورة – تشغيل المحرك

مع تحضير المحرك وتحميل الصورة في الذاكرة، حان الوقت لـ **perform OCR on image** البيانات. هذا السطر الواحد يقوم بالمعالجة الكاملة: ما قبل المعالجة، التقسيم، التصنيف، وتجميع النص.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**What happens under the hood?**  
- المحرك يطبق تحويل التصحيح (إذا كان مفعّلاً).  
- يشغّل شبكة عصبية أو محرك Tesseract لتحديد الأحرف.  
- أخيراً، يربط الأحرف لتكوّن كلمات وأسطر، ويعيد كائن `result` غني.

---

## استخراج النص من صورة ممسوحة – إخراج النتائج

الخطوة الأخيرة هي **extract text from scanned image** وعرضه. الخاصية `result.text` تحتوي على تمثيل النص العادي.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

الناتج النموذجي يبدو هكذا:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

إذا فشل محرك OCR في العثور على أي أحرف، ستكون `result.text` سلسلة فارغة. في هذه الحالة، أعد فحص جودة الصورة أو فكر في تعديل خاصية `engine.confidence_threshold` (إذا كانت مكتبتك تدعم ذلك).

---

## معالجة الاختلافات الشائعة

### التعرف على النص من JPEG مقابل PNG

كلا الصيغتين مدعومتان، لكن ضغط JPEG قد يضيف تشويهات تُربك المحرك. إذا لاحظت أخطاءً متكررة في التعرف، جرّب تحويل JPEG إلى PNG أولاً:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### اكتشاف النص من صورة بعدة لغات

إذا كان مستندك يخلط بين الإنجليزية والإسبانية، فعّل وضع متعدد اللغات:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

سيتعامل المحرك حينها مع كلا الأبجديتين أثناء التعرف.

### استخراج النص من ملفات PDF ممسوحة

بالنسبة لملفات PDF، تحتاج إلى تحويل كل صفحة إلى صورة أولاً. مكتبات مثل `pdf2image` تجعل العملية سهلة:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## مثال عملي كامل

فيما يلي السكريبت الكامل الذي يمكنك نسخه‑لصقه في ملف `ocr_demo.py`. يتضمن معالجة الأخطاء ومساعد صغير لقياس زمن التنفيذ.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Expected output** (assuming a clear scan):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## الأسئلة المتكررة

**Q: Can I run this on a headless server?**  
A: بالتأكيد. المكتبة تعمل بدون واجهة رسومية؛ فقط تأكد من تثبيت الثنائيات الأصلية اللازمة (مثل Tesseract) على الخادم.

**Q: What if the image is blurry?**  
A: فكر في إضافة مرشح شحذ قبل `engine.recognize`. العديد من مكتبات OCR تكشف عن `image_preprocessing.sharpen = True` أو يمكنك استخدام `cv2.GaussianBlur` من OpenCV بشكل عكسي.

**Q: Does the script support batch processing?**  
A: نعم. غلف `perform_ocr` داخل حلقة تمر على قائمة مسارات الملفات،

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}