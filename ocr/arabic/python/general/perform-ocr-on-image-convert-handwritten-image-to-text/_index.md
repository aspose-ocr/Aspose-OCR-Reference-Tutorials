---
category: general
date: 2026-03-18
description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على الصورة واستخراج النص المكتوب
  بخط اليد من صورة. تعلم كيفية تحويل صورة مكتوبة بخط اليد، استخراج النص من ملف JPG،
  والتعرف على النص من الصورة.
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: ar
og_description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على الصورة لاستخراج النص
  المكتوب بخط اليد من صورة. يوضح هذا الدرس كيفية تحويل صورة مكتوبة بخط اليد والتعرف
  على النص من ملفات JPG.
og_title: إجراء التعرف الضوئي على الحروف في الصورة – دليل شامل للنص المكتوب يدوياً
tags:
- OCR
- Python
- Handwriting Recognition
title: إجراء التعرف الضوئي على الأحرف في الصورة – تحويل الصورة المكتوبة يدويًا إلى
  نص
url: /ar/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على الصورة – استخراج النص المكتوب بخط اليد من الطرف إلى الطرف

هل احتجت يوماً إلى **perform OCR on image** ملفات ولكنك لم تكن متأكدًا ما إذا كان المحرك يستطيع قراءة الخط اليدوي الفوضوي؟ لست وحدك. في العديد من التطبيقات الواقعية—فكر في ماسحات فواتير النفقات أو أدوات تدوين الملاحظات—ستصادف صورًا لكتابات عشوائية تحتاج إلى تحويلها إلى نص عادي.  

في هذا الدليل سنوضح لك كيفية **convert handwritten image** الملفات، **extract text from jpg**، وحتى **recognize text from photo** باستخدام مكتبة صغيرة على نمط Python تسمى `ocr`. بنهاية الدليل ستحصل على سكريبت جاهز للتنفيذ يستخرج كل كلمة من ملاحظة مكتوبة بخط اليد، بغض النظر عن مدى ارتعاش القلم.

## ما ستحتاجه

- Python 3.8+ (الكود يعمل على أي مفسّر حديث)
- حزمة `ocr` الافتراضية – ثبّتها باستخدام `pip install ocr-lib` (استبدلها باسم الحزمة الفعلية التي تستخدمها)
- صورة واضحة لملاحظة مكتوبة بخط اليد محفوظة باسم `note.jpg` (أو بأي صيغة صورة أخرى)
- قدر بسيط من الفضول—لا تحتاج إلى خلفية متقدمة في التعلم الآلي

هذا كل شيء. لا خدمات خارجية، لا مفاتيح API، فقط محرك محلي يمكنه **perform OCR on image** للبيانات.

![perform OCR on image screenshot](example.png)

*نص بديل: لقطة شاشة لإجراء OCR على الصورة تُظهر محرر الشيفرة مع برنامج OCR.*

## تنفيذ خطوة بخطوة

فيما يلي نقسم العملية إلى أجزاء صغيرة. كل عنوان يحتوي على كلمة مفتاحية لتسهيل التصفح السريع، وكل قسم يشرح **لماذا** نقوم بما نقوم به—not just **what**.

### الخطوة 1: تثبيت والتحقق من مكتبة OCR

قبل أن تتمكن من **perform OCR on image** الملفات، يجب أن تكون المكتبة موجودة في بيئتك. افتح الطرفية وشغّل:

```bash
pip install ocr-lib
```

> **نصيحة احترافية:** إذا كنت تعمل في بيئة افتراضية (مستحسن جدًا)، فعّلها أولاً. هذا يحافظ على نظافة الاعتمادات ويتجنب تعارض الإصدارات.

بعد التثبيت، دعنا نتأكد أن Python يستطيع استيراد الحزمة:

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

إذا ظهرت رسالة النجاح، فأنت جاهز لـ **convert handwritten image** البيانات.

### الخطوة 2: إنشاء نسخة من المحرك واختيار وضع الخط اليدوي

معظم محركات OCR تفضّل التعرف على النص المطبوع بشكل افتراضي. بما أننا نريد **extract handwritten text**، يجب أن نغيّر الوضع صراحة. هذه الخطوة حاسمة لأن الخط اليدوي غالبًا ما يتطلب معالجة مسبقة مختلفة (مثل تنعيم الخطوط).

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*لماذا هذا مهم:* الأحرف المكتوبة بخط اليد قد تختلف كثيرًا في الحجم والميول. بتعيين `RecognitionMode.HANDWRITTEN`، يطبق المحرك نموذجًا مدربًا على عينات من الخط المتصل، مما يعزز الدقة بشكل كبير.

### الخطوة 3: تحميل الصورة التي تريد تحليلها

الآن نقوم فعليًا بـ **perform OCR on image** المحتوى. طريقة `load_image` تقبل مسارًا أو كائنًا شبيهًا بملف. للعرض، سنحمّل ملف JPEG، لكن نفس الاستدعاء يعمل مع PNG، BMP، أو حتى صفحات PDF.

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

إذا كانت صورتك مخزنة في سحابة، قم بتحميلها أولاً أو مرّر تدفق `BytesIO`—`ocr` مرن بما يكفي للتعامل مع كلا الحالتين.

### الخطوة 4: تشغيل عملية التعرف

مع تحضير المحرك وتحميل الصورة في الذاكرة، ن finally **perform OCR on image** ونسترجع النص الخام.

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

استدعاء `recognize()` يُعيد سلسلة Unicode عادية. لمعظم الحالات يمكنك كتابة النتيجة مباشرة إلى ملف `.txt`، أو تمريرها إلى خط أنابيب معالجة لغة طبيعية، أو عرضها في واجهة GUI.

### الخطوة 5: اختياري – تنظيف أو ما بعد معالجة المخرجات

التعرف على الخط اليدوي ليس مثاليًا؛ غالبًا ما ستلاحظ فواصل سطر عشوائية أو أحرف مقروءة خطأ. خطوة تنظيف سريعة يمكن أن تحسّن النتائج اللاحقة.

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

لا تتردد في إضافة مدقّقات إملائية، نماذج لغوية، أو تعبيرات regex مخصصة حسب مجال عملك.

### السكريبت الكامل – جاهز للنسخ واللصق

بدمج كل ما سبق، إليك البرنامج الكامل القابل للتنفيذ الذي **extracts handwritten text** من JPEG ويطبع نتيجة منظمة.

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**الناتج المتوقع** (النص الفعلي سيختلف بالطبع):

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

إذا رأيت نصًا غير مفهوم، تحقق مرة أخرى من جودة الصورة (إضاءة جيدة، تشويش قليل) وتأكد أنك في وضع `HANDWRITTEN`. هذان العاملان يفسران معظم أخطاء التعرف.

## الأسئلة المتكررة (FAQ)

| السؤال | الجواب |
|----------|--------|
| **Can I use this to extract text from a PNG?** | بالتأكيد. `engine.load_image("scan.png")` يعمل بنفس الطريقة. |
| **What if my image is a PDF page?** | حوّل الصفحة إلى صورة أولًا (مثلاً باستخدام `pdf2image`) ثم مرّرها إلى المحرك. |
| **Is the library thread‑safe?** | نعم، يمكنك إنشاء كائنات `OcrEngine` منفصلة لكل خيط. |
| **How does this differ from `pytesseract`?** | `ocr` يخفّف الحاجة إلى ملف Tesseract التنفيذي ويضم نموذجًا مدمجًا للخط اليدوي، لذا لا تحتاج لتثبيت برامج خارجية. |
| **What if I need to **extract text from JPG** files in bulk?** | غلف السكريبت داخل حلقة، أو استخدم `engine.load_image` لكل ملف وجمع النتائج في قائمة أو ملف CSV. |

## الحالات الخاصة وأفضل الممارسات

1. **Low‑contrast photos** – زد التباين برمجيًا قبل التحميل، أو استخدم `engine.apply_preprocessing('contrast', level=2)`.
2. **Mixed printed & handwritten** – نفّذ تمريرين: أولاً بـ `HANDWRITTEN`، ثم بـ `PRINTED`، وادمج النتائج.
3. **Large images** – قلل الحجم إلى عرض ~1500 px؛ محركات OCR عادةً ما تكون أسرع مع مخازن أصغر دون فقدان الدقة.
4. **Unicode characters** – المكتبة تُعيد سلاسل UTF‑8، لذا يمكنك التعامل مع الإيموجي، الأحرف ذات اللكنات، أو الرموز الرياضية مباشرة.

## الخلاصة

لقد استعرضنا مثالًا عمليًا لكيفية **perform OCR on image** للملفات، مع التركيز على الملاحظات المكتوبة بخط اليد. عبر تثبيت حزمة `ocr`، ضبط المحرك على وضع `HANDWRITTEN`، تحميل الصورة، واستدعاء `recognize()`، يمكنك **convert handwritten image** البيانات إلى نص نظيف قابل للبحث.  

من هنا قد ترغب في **extract text from jpg** ملفات بكميات كبيرة، أو إمداد المخرجات لتطبيق تدوين ملاحظات، أو دمجها مع تحويل النص إلى كلام لزيادة إمكانية الوصول. السماء هي الحد، والكود أعلاه يمنحك أساسًا قويًا للتجربة.

هل لديك طريقة مختلفة تريد مشاركتها—ربما صيغة ملف أخرى أو حيلة معالجة مسبقة غريبة؟ اترك تعليقًا، ولنستمر في النقاش. برمجة سعيدة، واستمتع بتحويل تلك الخربشات إلى ذهب رقمي!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}