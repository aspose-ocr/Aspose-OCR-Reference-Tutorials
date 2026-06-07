---
category: general
date: 2026-06-06
description: قم بتشغيل OCR على الصورة باستخدام بايثون وعرض درجات الثقة. تعلّم كيفية
  تصفية الكلمات ذات الثقة المنخفضة، وضبط العتبات، ومعالجة الحالات الخاصة.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: ar
og_description: قم بتشغيل OCR على صورة في بايثون، افحص مستويات الثقة، وقم بتصفية الكلمات
  ذات الثقة المنخفضة. هذا الدرس يوجهك عبر مثال كامل قابل للتنفيذ.
og_title: تشغيل OCR على الصورة باستخدام بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: تشغيل التعرف الضوئي على الأحرف (OCR) على صورة باستخدام بايثون – دليل كامل خطوة
  بخطوة
url: /ar/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على الصورة باستخدام بايثون – دليل خطوة بخطوة كامل

هل احتجت يومًا إلى **run OCR on image** ملفات ولكن لم تكن متأكدًا من كيفية استخراج نص موثوق منها؟ أنت لست وحدك—العديد من المطورين يواجهون نفس المشكلة عندما تبدو الكلمات المستخرجة غير ثابتة وتكون درجة الثقة غامضة.  

في هذا الدليل سنغوص مباشرةً في حل عملي: ستتعرف على كيفية **run OCR on image**، قراءة الثقة العامة، واستخراج أي كلمات ذات ثقة منخفضة قد تحتاج إلى مراجعة يدوية. في النهاية ستحصل على سكريبت قابل لإعادة الاستخدام، وتفهم لماذا كل سطر مهم، وتعرف كيف تعدل عتبة الثقة لمشاريعك الخاصة.

## ما يغطيه هذا الدرس

سنستعرض سير العمل بالكامل—من تحميل الصورة إلى طباعة تقرير منظم للكلمات التي سقطت تحت علامة 80 % من الثقة. على طول الطريق سنناقش:

* اختيار محرك OCR قوي (سنستخدم **EasyOCR**، مكتبة OCR شائعة في بايثون)  
* تفسير خاصية `confidence` التي تُرجعها كل نتيجة OCR  
* تصفية الكلمات باستخدام **عتبة ثقة OCR** مخصصة  
* توسيع السكريبت لمعالجة دفعات أو استخدام محركات بديلة مثل **pytesseract**  

لا تحتاج إلى خبرة سابقة في OCR، فقط إلمام أساسي ببايثون وبيئة عمل (يوصى بـ Python 3.9+).  

هل أنت مستعد لتحويل لقطات الشاشة الضبابية إلى نص نظيف قابل للبحث؟ لنبدأ.

---

## ## كيفية تشغيل OCR على الصورة باستخدام بايثون

قلب الدرس هو مقطع من ثلاث خطوات يعكس الكود الذي رأيته بالفعل. أدناه سنفصل كل سطر، نشرح السبب، ثم نعطيك سكريبت جاهز للنسخ واللصق.

### الخطوة 1: تثبيت واستيراد محرك OCR

أولًا، تأكد من توفر مكتبة OCR. **EasyOCR** يعمل مباشرةً للعديد من اللغات ويعطيك درجة ثقة لكل كلمة.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*لماذا EasyOCR؟* إنه يجمع نموذج تعلم عميق تم تدريبه على مجموعات بيانات متنوعة، لذا عادةً ما تحصل على قيم ثقة أعلى من محرك Tesseract القديم، خاصةً على الصور ذات الجودة المختلطة.

> **نصيحة احترافية:** إذا كنت تعمل في بيئة محدودة (مثل حاوية Docker صغيرة)، قد يكون `pytesseract` أخف وزنًا، لكنك ستفقد بعض الدقة الحديثة التي يوفرها EasyOCR.

### الخطوة 2: تشغيل OCR على الصورة

الآن نقوم فعليًا بـ **run OCR on image**. تم استبدال طريقة `recognize_image` من المثال الأصلي بنداء `readtext` الخاص بـ EasyOCR، والذي يُرجع قائمة من tuples على الشكل `(bbox, text, confidence)`.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

كل عنصر في `ocr_results` يبدو كالتالي:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

العنصر الثالث (`0.92` في المثال) هو درجة الثقة التي تتراوح بين 0 إلى 1.

### الخطوة 3: تلخيص الثقة العامة

على عكس المقتطف السابق الذي طبع خاصية `confidence` واحدة، يقدم EasyOCR ثقة لكل كلمة. للحصول على فكرة عامة، سنحسب المتوسط:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*لماذا المتوسط؟* يمنحك فحصًا سريعًا للصحّة—إذا كانت الثقة العامة أقل من، لنقل، 70 %، فربما تحتاج إلى تحسين الصورة (إضاءة أفضل، معالجة مسبقة، إلخ).

### الخطوة 4: سرد الكلمات ذات الثقة المنخفضة

الآن يأتي الجزء الذي يجيب مباشرةً على طلب “قائمة الكلمات التي تكون ثقتها أقل من العتبة المطلوبة”. سنحدد **عتبة ثقة OCR** بـ 0.80 (80 %) افتراضيًا، لكن يمكنك تعديلها.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

الحلقة تطبع كل كلمة لم تتجاوز العتبة، مع نسبة الثقة الخاصة بها. هذا هو النظير الدقيق لحلقة `for recognized_word in recognition_result.words` الأصلية، لكنه الآن يعمل مع صيغة إخراج EasyOCR.

---

## ## فهم درجات ثقة OCR

الثقة ليست رقمًا سحريًا؛ إنها تقدير النموذج لمدى تأكده من النسخ المعين. إليك بعض الأمور التي يجب مراعاتها:

| الحالة | الثقة المتوقعة | ما الذي يجب فعله |
|-----------|-------------------|------------|
| مسح واضح وعالي الدقة | 0.95 – 1.00 | لا حاجة لأي عمل إضافي |
| ضبابية طفيفة أو إضاءة غير متساوية | 0.80 – 0.94 | فكر في معالجة مسبقة بسيطة (زيادة التباين) |
| ضوضاء شديدة، نص مائل | < 0.70 | طبّق معالجة مسبقة للصورة (تصحيح الميل، إزالة الضوضاء) أو انتقل إلى محرك OCR مختلف |

> **احذر:** بعض اللغات (مثل الخط اليدوي المتصل) تنتج بطبيعتها درجات أقل. عدّل العتبة وفقًا لذلك.

### حالات الحافة والاختلافات

1. **معالجة دفعات** – إذا كنت بحاجة إلى **run OCR on image** لملفات متعددة دفعةً واحدة، غلف المنطق أعلاه بحلقة تتنقل عبر دليل.
2. **لغات متعددة** – مرّر قائمة مثل `['en', 'fr']` إلى `easyocr.Reader` وسيكتشف المحرك كلا اللغتين.
3. **محركات بديلة** – هل تريد تجربة **pytesseract**؟ استبدل كتلة القارئ بـ:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   بعد ذلك ستحتاج إلى تجميع ثقة كل حرف إلى ثقة كلمة—عمل إضافي قليل لكنه ممكن.
4. **حيل المعالجة المسبقة** – تطبيق فلاتر OpenCV (`cv2.threshold`, `cv2.GaussianBlur`) يمكن أن يعزز الثقة للصور المليئة بالضوضاء.  

---

## ## سكريبت كامل جاهز للتنفيذ

فيما يلي ملف بايثون كامل يمكنك وضعه في مشروعك. احفظه باسم `ocr_report.py` وشغّله بـ `python ocr_report.py`. تأكد أن مسار الصورة يشير إلى ملف حقيقي.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**المخرجات المتوقعة** (ستختلف أرقامك):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

إذا تجاوزت كل كلمة عتبة الـ 80 % ستظهر لك الرسالة الودية “All words meet the confidence threshold.” بدلاً من ذلك.

---

## ## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا مع ملفات PDF؟**  
ج: ليس مباشرة. حوّل كل صفحة PDF إلى صورة أولًا (مثلاً باستخدام `pdf2image`) ثم أدخل ملف PNG/JPEG إلى السكريبت.

**س: أرقام الثقة لدي كلها منخفضة — ماذا يمكنني أن أفعل؟**  
ج: جرّب معالجة مسبقة للصورة: زد التباين، أزل الضوضاء الخلفية، أو قم بتدوير الصورة لتصبح أفقية. EasyOCR يقبل أيضًا معامل `contrast_ths` يمكنك ضبطه.

**س: هل يمكنني تصدير النتائج إلى CSV؟**  
ج: بالتأكيد. بعد حلقة الكلمات منخفضة الثقة، اكتب `ocr_results` إلى `csv.DictWriter` حيث يحتوي كل صف على `text`، `confidence`، وإحداثيات المربع المحيط.

**س: هل هناك نسخة مسرعة باستخدام GPU؟**  
ج: EasyOCR يستخدم CUDA تلقائيًا إذا كان هناك GPU متوافق وPyTorch مثبت. تحقق من `torch.cuda.is_available()` قبل تشغيل السكريبت.

---

## الخلاصة

لقد قمنا للتو بـ **run OCR on image** باستخدام بايثون، فحصنا الثقة العامة، وعزلنا أي كلمات ذات ثقة منخفضة تحتاج إلى

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية ضبط قيمة العتبة في التعرف على الصور باستخدام OCR](/ocr/english/net/ocr-settings/set-threshold-value/)
- [كيفية استخدام Aspose OCR للحصول على نتيجة JSON في التعرف على الصور](/ocr/english/net/text-recognition/get-result-as-json/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}