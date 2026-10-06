---
category: general
date: 2026-01-12
description: كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) وتحويل الصورة إلى نص بسرعة.
  تعلم التعرف على الأحرف الخاصة، استخراج النص من الصورة، وتحميل الصورة للتعرف الضوئي
  على الأحرف مع مثال كامل بلغة بايثون.
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: ar
og_description: كيفية تنفيذ OCR في بايثون، تحويل الصورة إلى نص، والتعرف على الأحرف
  الخاصة. اتبع هذا الدليل العملي لاستخراج النص من الصور.
og_title: كيفية تنفيذ OCR في بايثون – دليل كامل
tags:
- OCR
- Python
- Image Processing
title: كيفية تنفيذ OCR في بايثون – دليل خطوة بخطوة
url: /ar/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تقوم بإجراء OCR في بايثون – دليل خطوة بخطوة

هل احتجت يومًا إلى **إجراء OCR** على لقطة شاشة تحتوي على أحرف لاتينية وسيريلية؟ لست وحدك. في العديد من المشاريع—سواء كان ذلك لتحويل الإيصالات إلى نص، فهرسة مستندات متعددة اللغات، أو بناء أرشيف قابل للبحث—**كيفية إجراء OCR** تصبح سؤالًا محوريًا بسرعة.  

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح لك كيفية **تحويل الصورة إلى نص**، **التعرف على الأحرف الخاصة**، و**استخراج النص من الصورة** باستخدام مكتبة بايثون بسيطة. في النهاية ستحصل على سكربت جاهز للتنفيذ يحمل صورة للـ OCR، يتعامل مع محتوى متعدد اللغات، ويطبع النتيجة.

## ما الذي ستحتاجه

قبل أن نبدأ، تأكد من توفر المتطلبات التالية:

- تثبيت Python 3.8+ على جهازك.  
- حزمة `ocr` (أو أي مكتبة OCR متوافقة) مُثبتة عبر `pip install ocr`.  
- ملف صورة (`multilingual.png`) يحتوي على أحرف لاتينية وسيريلية.  
- محرر نصوص أو بيئة تطوير متكاملة—VS Code، PyCharm، أو حتى Notepad بسيط سيكفي.  

إذا لم تكن لديك حزمة `ocr`، يمكنك استبدالها بـ `pytesseract` مع بعض التعديلات البسيطة؛ المفاهيم الأساسية تبقى كما هي.

## الخطوة 1: تثبيت واستيراد مكتبة OCR

أولًا، لنجهز محرك OCR. سنستورد المكتبة، ننشئ كائن المحرك، ونكوّنه لدعم اللغات المتعددة.

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**لماذا هذا مهم:**  
إنشاء المحرك هو الأساس—بدونه لا يمكنك **تحميل صورة للـ OCR** لاحقًا. تمكين حزم اللغات يضمن أن المحرك يستطيع التعرف بشكل صحيح على أحرف مثل “Ŀ”، “Ҕ”، و“Ǣ”. إذا تخطيت هذه الخطوة، ستحصل على مخرجات مشوشة للخطوط غير اللاتينية.

## الخطوة 2: تحميل الصورة التي تحتوي على نص متعدد اللغات

الآن نوجه المحرك إلى الملف الذي نريد معالجته. يمكن أن يكون المسار مطلقًا أو نسبيًا؛ فقط تأكد أنه يشير إلى صورة قابلة للقراءة.

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![مثال على كيفية إجراء OCR](/images/ocr-example.png "كيفية إجراء OCR على صورة متعددة اللغات")

**لماذا هذا مهم:**  
نداء `load_image` يقرأ بيانات البكسل إلى الذاكرة، محضرًا إياها لخوارزمية OCR. إذا كانت الصورة كبيرة، قد يقوم المحرك بتقليل حجمها تلقائيًا؛ يمكنك ضبط ذلك لاحقًا باستخدام `engine.set_max_resolution(3000)` للمسحات عالية الدقة.

## الخطوة 3: تشغيل عملية التعرف

بعد أن تم تهيئة المحرك وتحميل الصورة، يمكننا أخيرًا استخراج المحتوى النصي.

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**لماذا هذا مهم:**  
`recognize()` ينفّذ الشبكة العصبية الثقيلة خلف الكواليس. يعيد كائنًا يحتوي على النص الخام، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها لتصحيح بصري.

## الخطوة 4: إخراج النص المُعترف به

لنرى ما وجده المحرك. سنطبع النص على الشاشة، لكن يمكنك أيضًا كتابته إلى ملف أو قاعدة بيانات.

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### النتيجة المتوقعة

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

إذا رأيت شيئًا مشابهًا، تهانينا—لقد نجحت في **تحويل الصورة إلى نص** و**التعرف على الأحرف الخاصة**.

## التعامل مع المشكلات الشائعة

حتى مع سكربت بسيط، قد تواجه بعض العقبات. إليك بعض النصائح العملية من تجربتي.

### 1. عدم وجود حزم اللغة

إذا ظهرت علامات استفهام (`?`) بدلًا من الأحرف السيريلية، تحقق من تثبيت حزم اللغة. للعديد من محركات OCR تحتاج إلى تنزيل ملفات `.traineddata` المقابلة ووضعها في مجلد `tessdata` الخاص بالمحرك.

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. جودة الصورة منخفضة

الصور الضبابية أو ذات التباين المنخفض تُنتج درجات ثقة منخفضة. عالج الصورة مسبقًا باستخدام OpenCV:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. ملفات كبيرة واستهلاك الذاكرة

معالجة صورة بحجم 10 ميغابايت قد ترفع استهلاك الذاكرة. استخدم `engine.set_max_image_size(2000)` لتحديد أقصى دقة، أو قسّم الصورة إلى مربعات وعالج كل مربع على حدة.

### 4. التقاط إطارات الحدود

إذا كنت بحاجة لتسليط الضوء على موقع كل كلمة (مفيد لتراكب الواجهة)، يمكنك الوصول إلى `result.boxes`:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## السكربت الكامل – تنفيذ بنقرة واحدة

بجمع كل ما سبق، إليك ملف واحد يمكنك تشغيله كـ `python ocr_demo.py`. يتضمن معالجة الأخطاء، معالجة مسبقة اختيارية، وتعليقات لتوضيح الفكرة.

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

شغّله باستخدام:

```bash
python ocr_demo.py path/to/multilingual.png
```

سترى نفس النتيجة المعروضة سابقًا، مما يؤكد أنك قد **استخراجت النص من الصورة** بنجاح.

## الخلاصة

غطّينا **كيفية إجراء OCR** في بايثون من البداية إلى النهاية: تثبيت المكتبة، تحميل الصورة، التعرف على محتوى متعدد اللغات، ومعالجة أكثر المشكلات شيوعًا. باتباع هذا الدليل يمكنك الآن **تحويل الصورة إلى نص**، **التعرف على الأحرف الخاصة**، و**استخراج النص من الصورة** في مشاريعك—دون الحاجة إلى النسخ اليدوي.

ما الخطوة التالية؟ جرّب ما يلي:

- إضافة حزم لغة إضافية (مثل `spa` للإسبانية).  
- تصدير النتائج إلى JSON لمعالجة لاحقة.  
- دمج خطوة OCR في واجهة Flask API ليتمكن الخدمات الأخرى من استدعائها.  

إذا صادفت أي صعوبات، فإن مجتمع معظم مكتبات OCR نشط—ابحث عن “ocr library language pack installation” أو اترك تعليقًا أدناه. برمجة سعيدة، واستمتع بتحويل الصور إلى نص قابل للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}