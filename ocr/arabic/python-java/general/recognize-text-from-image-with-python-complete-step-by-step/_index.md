---
category: general
date: 2026-06-16
description: التعرف على النص من الصورة باستخدام OCR في بايثون. تعلّم كيفية تحميل الصورة
  للـ OCR، وضبط وضع الدقة العالية، وتشغيل التعرف على النص لتحويل الصورة إلى نص.
draft: false
keywords:
- recognize text from image
- convert image to text
- load image for ocr
- run ocr recognition
- set high accuracy mode
language: ar
og_description: التعرف على النص من الصورة في بايثون. يوضح هذا الدليل كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف، وتفعيل وضع الدقة العالية، وتشغيل التعرف الضوئي على الأحرف
  لتحويل الصورة إلى نص.
og_title: التعرف على النص من الصورة – دورة شاملة لتقنية OCR بايثون
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using Python OCR. Learn how to load image
    for OCR, set high accuracy mode, and run OCR recognition to convert image to text.
  headline: recognize text from image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: recognize text from image using Python OCR. Learn how to load image
    for OCR, set high accuracy mode, and run OCR recognition to convert image to text.
  name: recognize text from image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Empty Result
    text: 'Sometimes the engine returns an empty string. This usually means the image
      is too blurry or the text color blends with the background. Try:'
  - name: 2. Non‑Latin Scripts
    text: 'If your picture contains Cyrillic, Chinese, or Arabic characters, you’ll
      need to tell the OCR engine which language pack to use:'
  - name: 3. Large Batches
    text: Processing a folder of images? Wrap the core logic in a loop and reuse the
      same engine instance to avoid repeated initialization overhead.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: التعرف على النص من الصورة باستخدام بايثون – دليل كامل خطوة بخطوة
url: /ar/python-java/general/recognize-text-from-image-with-python-complete-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة – دليل Python OCR الكامل

هل تساءلت يومًا كيف **تتعرف على النص من الصورة** دون الحاجة لدفع مقابل خدمة سحابية؟ لست وحدك. سواء كنت تقوم برقمنة الإيصالات القديمة أو استخراج العناوين من لقطات الشاشة، فإن تحويل الصورة إلى نص قابل للتحرير مهارة مفيدة جدًا.

في هذا الدرس سنستعرض **مثالًا كاملاً قابلاً للتنفيذ** يوضح لك كيفية **تحميل صورة للـ OCR**، **تفعيل وضع الدقة العالية**، و**تشغيل التعرف على النص** بحيث يمكنك **تحويل الصورة إلى نص** في بضع أسطر من Python فقط. لا إطالة، فقط الجزء العملي الذي يمكنك نسخه ولصقه الآن.

## ما ستبنيه

بنهاية هذا الدليل ستحصل على سكربت صغير يقوم بـ:

1. إنشاء محرك OCR.
2. تفعيل علم **set high accuracy mode** للحصول على نتائج أفضل مع الصور منخفضة الدقة.
3. **تحميل صورة للـ OCR** من القرص.
4. **تشغيل التعرف على النص** لت **التعرف على النص من الصورة**.
5. طباعة السلسلة المستخرجة – أي **تحويل الصورة إلى نص** فعليًا.

إذا كان لديك Python 3.8+ وقليل من الفضول، فأنت جاهز للبدء.

## المتطلبات المسبقة

- **Python 3.8 أو أحدث** – يستخدم الكود تلميحات نوع لا تفهمها الإصدارات الأقدم.
- مكتبة OCR توفر وحدة `ocr` (المثال يحاكي غلافًا عامًا؛ استبدله بـ `pytesseract` أو `easyocr` أو أي SDK خاص بمزود تفضله).
- صورة JPEG منخفضة الدقة باسم `low-res.jpg` في مجلد يمكنك التحكم فيه.
- (اختياري) بيئة افتراضية للحفاظ على نظافة الاعتمادات: `python -m venv venv && source venv/bin/activate`.

```bash
# Example installation for a hypothetical `ocr` package
pip install ocr-lib
```

> **نصيحة احترافية:** إذا كنت تستخدم `pytesseract`، فقم بتثبيت محرك Tesseract منفصلًا (`sudo apt-get install tesseract-ocr` على Linux، Homebrew على macOS).

---

## الخطوة 1: التعرف على النص من الصورة – تهيئة محرك OCR

أولًا وقبل كل شيء. نحتاج إلى كائن محرك OCR جديد سيتولى الجزء الثقيل.

```python
# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*لماذا هذا مهم:* فئة `OcrEngine` هي نقطة الدخول لجميع العمليات اللاحقة. فكر فيها كالعقل الذي سيفسر البكسلات التي تزوده بها. إنشاء نسخة جديدة في كل تشغيل يضمن حالة نظيفة، خاصةً عندما تقوم بتبديل إعدادات مثل **set high accuracy mode** لاحقًا.

---

## الخطوة 2: تفعيل وضع الدقة العالية – تحسين نتائج الصور منخفضة الدقة

الصور منخفضة الدقة تشكل تحديًا كبيرًا لمحركات OCR. تفعيل علم الدقة العالية يخبر المحرك بتطبيق معالجة مسبقة إضافية (تكبير، تقليل الضوضاء، إلخ) قبل قراءة الأحرف فعليًا.

```python
# Step 2: Enable high‑accuracy mode for better results
engine.high_accuracy = True   # <-- activates advanced preprocessing
```

> **لماذا تفعله؟** عندما تكون الصورة المصدرية مشوشة أو صغيرة، قد يتخطى الوضع الافتراضي الحروف أو يدمج الكلمات. مسار الدقة العالية يضحي بقليل من السرعة مقابل قفزة ملحوظة في الدقة — مثالي للسكريبتات الفردية التي لا تكون فيها الكمون أمرًا حاسمًا.

---

## الخطوة 3: تحميل صورة للـ OCR – تحضير الملف

الآن نقوم فعليًا **بتحميل صورة للـ OCR**. الدالة المساعدة `ocr.Image.load_from_file` تُجرد خطوات الإدخال/الإخراج وتفكيك الصورة.

```python
# Step 3: Load the low‑resolution image to be processed
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/low-res.jpg")
```

*ما الذي يحدث في الخلفية؟* تقوم المكتبة بقراءة ملف JPEG، تحويله إلى bitmap، وتخزينه داخل كائن المحرك. إذا احتجت للعمل مع صورة موجودة بالفعل في الذاكرة (مثلاً من طلب ويب)، فإن معظم المكتبات توفر أيضًا طريقة `from_bytes` — فقط استبدل الاستدعاء.

---

## الخطوة 4: تشغيل التعرف على النص – الإجراء الأساسي

بعد أن تم تهيئة المحرك ووضع الصورة في مكانها، نصل أخيرًا إلى **تشغيل التعرف على النص**. هذه الخطوة تقوم باستخراج النص فعليًا.

```python
# Step 4: Perform OCR recognition on the image
high_res_result = engine.recognize()
```

طريقة `recognize()` تُعيد كائن نتيجة يحتوي على السلسلة الخام، درجات الثقة، وأحيانًا بيانات الصناديق المحيطة. لغرض **تحويل الصورة إلى نص**، سنركز على الخاصية `text`.

---

## الخطوة 5: إخراج النص المُتعرف عليه – تحويل الصورة إلى نص

النتيجة النهائية للعملية: طباعة السلسلة المستخرجة. هنا تتحول الصورة أخيرًا إلى نص قابل للتحرير.

```python
# Step 5: Output the recognized text
print(high_res_result.text)
```

**الناتج المتوقع** (النص الفعلي سيختلف حسب الصورة):

```
Invoice #12345
Date: 2024‑03‑15
Total: $256.78
Thank you for your business!
```

إذا ظهرت لك أحرف مشوشة، تأكد من أن **set high accuracy mode** فعلاً `True` وأن الصورة ليست مضغوطة بشكل مفرط.

---

## معالجة الحالات الشائعة

### 1. نتيجة فارغة

أحيانًا يُعيد المحرك سلسلة فارغة. هذا يعني عادةً أن الصورة غير واضحة أو أن لون النص يندمج مع الخلفية. جرّب:

- زيادة دقة الصورة قبل التحميل (`PIL.Image.resize`).
- تعديل التباين (`ImageEnhance.Contrast`).

### 2. نصوص غير لاتينية

إذا احتوت الصورة على أحرف سيريالية أو صينية أو عربية، سيتعين عليك إخبار محرك OCR بحزمة اللغة المناسبة:

```python
engine.language = "eng+rus"   # Example for English + Russian
```

### 3. دفعات كبيرة

هل تريد معالجة مجلد من الصور؟ ضع المنطق الأساسي داخل حلقة وأعد استخدام نفس كائن المحرك لتجنب تكلفة التهيئة المتكررة.

```python
import pathlib

engine = ocr.OcrEngine()
engine.high_accuracy = True
engine.language = "eng"

for img_path in pathlib.Path("batch/").glob("*.jpg"):
    engine.image = ocr.Image.load_from_file(str(img_path))
    result = engine.recognize()
    print(f"{img_path.name}: {result.text[:50]}...")
```

---

## مثال كامل يعمل

بجمع كل الأجزاء معًا، إليك سكربت يمكنك وضعه في ملف اسمه `ocr_demo.py` وتشغيله فورًا.

```python
#!/usr/bin/env python3
"""
ocr_demo.py – Recognize text from image using a generic OCR library.
"""

import ocr  # Replace with the actual OCR package you installed

def main():
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.high_accuracy = True          # set high accuracy mode
    engine.language = "eng"              # optional: specify language pack

    # Load image – change the path to your own file
    image_path = "YOUR_DIRECTORY/low-res.jpg"
    engine.image = ocr.Image.load_from_file(image_path)

    # Perform recognition
    result = engine.recognize()

    # Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

احفظه، اجعل له صلاحية التنفيذ (`chmod +x ocr_demo.py`)، ثم شغّله:

```bash
./ocr_demo.py
```

سترى ناتج **تحويل الصورة إلى نص** يُطبع على الشاشة.

---

## نصائح وحيل من الميدان

- **احفظ المحرك في الذاكرة** إذا كنت تعالج الكثير من الصور؛ إنشاء نسخة جديدة لكل ملف قد يضاعف زمن التنفيذ.
- **قم بالمعالجة المسبقة بنفسك** عندما لا يكون وضع الدقة العالية كافيًا: استخدم OpenCV لإزالة الضوضاء (`cv2.fastNlMeansDenoisingColored`) أو لتثبيت الثنائيات (`cv2.threshold`).
- **سجّل درجة الثقة** (`result.confidence`) إذا احتجت لتصفية النتائج منخفضة الجودة تلقائيًا.
- **تجنّب كتابة المسارات صراحة**؛ استخدم `pathlib.Path` لتوافقية عبر الأنظمة.

---

## الخلاصة

لقد تعلمنا الآن **التعرف على النص من الصورة** باستخدام سير عمل Python بسيط: **تحميل صورة للـ OCR**، **تفعيل وضع الدقة العالية**، **تشغيل التعرف على النص**، وأخيرًا **تحويل الصورة إلى نص**. يكتمل هذا الخط الأنابيب في أقل من عشرين سطرًا، لكنه مرن بما يكفي للتعامل مع دفعات، مستندات متعددة اللغات، ومدخلات صاخبة.

مستعد للتحدي التالي؟ جرّب استبدال مكتبة `ocr` العامة بـ `pytesseract` أو `easyocr`، جرب خطوات معالجة إضافية، أو دمج السكربت في API باستخدام Flask لتتمكن من رفع الصور من صفحة ويب والحصول على النصوص مباشرة.

هل لديك أسئلة أو حالة استخدام مميزة؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُكمل التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}