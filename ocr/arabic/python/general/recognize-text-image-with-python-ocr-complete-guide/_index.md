---
category: general
date: 2026-06-28
description: تعرّف على كيفية التعرف على صور النص باستخدام OCR في بايثون، استخراج ملفات
  PNG النصية، وطباعة النص المُعترف به مع معالجة أخطاء قوية.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: ar
og_description: دليل خطوة بخطوة للتعرف على صورة نصية في بايثون، استخراج النص من ملف
  PNG، وطباعة النص المُتعرف عليه بأمان.
og_title: التعرف على نص الصورة باستخدام Python OCR – دليل شامل
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: التعرف على النص في الصورة باستخدام بايثون OCR – دليل شامل
url: /ar/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على نص الصورة باستخدام Python OCR – دليل كامل

هل تساءلت يومًا كيف **تتعرف على نص الصورة** في سكريبت بايثون دون استدعاء إطار عمل ضخم؟ لست وحدك. يحتاج العديد من المطورين إلى طريقة سريعة لـ *load image OCR* لقطة شاشة، أو إيصال ممسوح، أو ملف PNG بسيط والحصول على النص مرة أخرى.  

في هذا الدرس سنقوم بتهيئة محرك OCR بسيط، وإرفاق مسجل مخصص، **load image OCR**، تشغيل **process image OCR**، وأخيرًا **print recognized text**. بنهاية الدرس ستحصل على سكريبت مستقل يمكنه أيضًا **extract text png** حسب الطلب.

## ما ستحصل عليه

- مقتطف بايثون كامل الوظيفة ينشئ محرك OCR، ويسجل كل خطوة، ويتعامل مع الأخطاء بسلاسة.  
- شروحات واضحة عن *لماذا* كل سطر مهم—حتى تتمكن من تعديل الكود ليتوافق مع Tesseract أو EasyOCR أو أي خلفية أخرى.  
- نصائح حول المشكلات الشائعة (خطوط مفقودة، PNGs تالفة) وكيفية تصحيحها.  

### المتطلبات المسبقة

- تثبيت Python 3.8+  
- مكتبة OCR تُظهر فئة `OcrEngine` (المثال يستخدم API خيالي لكنه شائع؛ استبدله بـ `pytesseract`، `easyocr`، إلخ).  
- صورة PNG تريد تحليلها، محفوظة كـ `input.png` في مجلد تملكه.  

> **نصيحة احترافية:** إذا كنت تستخدم `pytesseract`، قم بتثبيت ملف Tesseract الثنائي للنظام أولًا (`sudo apt install tesseract-ocr` على لينكس) ثم نفّذ `pip install pytesseract pillow`.

---

## ## التعرف على نص الصورة: إعداد المسجل

المسجل الجيد هو البطل غير المعلن في أي خط أنابيب OCR. يخبرك *متى* بدأ المحرك، *ما* الملف الذي فتحه، و*لماذا* قد يكون فشل.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*لماذا هذا مهم:*  
المسجل يفصل مخرجات التشخيص عن نواة OCR، مما يجعل من السهل توجيه السجلات إلى ملف، أو خدمة مراقبة، أو حتى واجهة مستخدم لاحقًا.  

---

## ## تحميل صورة OCR: تزويد المحرك بملف PNG

قبل أن يتمكن المحرك من **process image OCR**، يحتاج إلى كائن صورة مناسب. معظم المكتبات تقبل كائن `Image` من Pillow.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*نقاط رئيسية:*  

- **load image ocr** – `Image.from_file` يخفِّي تفاصيل فك ترميز PNG.  
- احرص على جعل المسار قابلًا للتكوين؛ التثبيت الصلب يجعل السكريبت هشًا.  
- استدعاء المسجل يؤكد أن الصورة تم قراءتها بنجاح، وهو مفيد عندما يكون الملف مفقودًا أو تالفًا.  

---

## ## معالجة صورة OCR: التعرف على النص

الآن يبدأ العمل الشاق. يقوم المحرك بمسح البت ماب، ويطبق الشبكات العصبية أو الخوارزميات، ويُنتج سلسلة Unicode.

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*لماذا نغلفه بـ `try/except`:*  
يمكن أن يتعطل OCR عند PNGs منخفضة الدقة، أو مساحات ألوان غير مدعومة، أو بيانات لغة مفقودة. التقاط `OcrException` يتيح لك **print recognized text** فقط عندما يكون موجودًا فعليًا، متجنبًا تتبعات الأخطاء الغامضة للمستخدم النهائي.

---

## ## طباعة النص المعترف به واستخراج نص PNG

إذا نجح التعرف، نعرض النتيجة وربما نكتبها إلى ملف `.txt` يطابق اسم PNG الأصلي.

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*ما ستحصل عليه:*  

- **print recognized text** – رد فعل بصري فوري في الطرفية.  
- ملف `.txt` بجانب الصورة يتيح **extract text png** للمعالجة اللاحقة (فهرسة البحث، إدخال البيانات، إلخ).  

---

## ## الحالات الحدية الشائعة وكيفية التعامل معها

| الحالة | العَرَض | الحل |
|-----------|---------|-----|
| PNG أحادي اللون فقط | OCR يُعيد سلسلة فارغة | تحويل إلى RGB (`Image.convert("RGB")`) قبل إمداد المحرك. |
| اللغة غير مدعومة | `OcrException` مع الكود `LANG_NOT_FOUND` | قم بتثبيت حزمة اللغة (مثال: `tesseract‑lang‑fra` للفرنسية) واضبط `ocr_engine.language = "fra"`. |
| صورة كبيرة جدًا ( > 5 MB ) | تعرف بطيء أو خطأ في الذاكرة | تقليل الحجم باستخدام `image.thumbnail((2000, 2000))` قبل `set_image`. |
| حروف غير متوقعة | مخرجات مشوشة | تأكد أن الصورة هي PNG فعلًا؛ بعض الملفات تتنكر كـ PNG لكنها JPEG في الواقع. استخدم `Image.verify()` للتحقق. |

---

## ## مثال كامل يعمل (جاهز للنسخ واللصق)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**الناتج المتوقع في الطرفية (المسار السعيد):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

إذا حدث خطأ ما، سترى سطرًا واضحًا `[ERROR]` مع السبب، بفضل المسجل المخصص.

---

## ## الخطوات التالية والمواضيع ذات الصلة

- **extract text png** من دفعات: غلف السكريبت داخل حلقة `for` تتجول في شجرة الدليل.  
- **process image ocr** مع تمهيد مسبق (إزالة الميل، تعزيز التباين) باستخدام OpenCV قبل إمداد المحرك.  
- التحويل إلى خدمة OCR سحابية (Google Vision، Azure Read) عن طريق استبدال تنفيذ `OcrEngine`—يبقى الكود المحيط نفسه.  
- تعلم كيفية **print recognized text** إلى ملفات PDF باستخدام `reportlab` لتوليد تقارير آلية.  

---

## الخلاصة

لقد استعرضنا للتو طريقة مختصرة وجاهزة للإنتاج **recognize text image** في بايثون، بدءًا من تحميل PNG إلى **print recognized text** وحفظ النتيجة. من خلال إضافة مسجل صغير، ومعالجة الاستثناءات، وحفظ المخرجات اختياريًا، يصبح السكريبت جاهزًا لكل من التجارب السريعة والتكامل في خطوط أنابيب أكبر.

جرّبه مع لقطات الشاشة الخاصة بك، وجرب تمهيد الصور، وستتمكن قريبًا من استخراج النص من أي PNG تضعه أمامه. هل لديك أسئلة؟ اترك تعليقًا—نتمنى لك OCR سعيد!  

![مثال على التعرف على نص الصورة](placeholder.png)


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية استخراج نص الصورة من تدفق باستخدام Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [تحويل الصورة إلى نص – تنفيذ OCR على صورة من URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}