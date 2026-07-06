---
category: general
date: 2026-05-03
description: تعلم كيفية تشغيل OCR على الصورة واستخراج النص مع الإحداثيات باستخدام
  التعرف المهيكل على OCR. يتضمن كود بايثون خطوة بخطوة.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: ar
og_description: قم بتشغيل OCR على الصورة واحصل على النص مع الإحداثيات باستخدام التعرف
  على OCR الهيكلي. مثال كامل بلغة بايثون مع الشروحات.
og_title: تشغيل OCR على الصورة – دليل استخراج النص المهيكل
tags:
- OCR
- Python
- Computer Vision
title: تشغيل التعرف الضوئي على الأحرف في الصورة – دليل شامل لاستخراج النص المهيكل
url: /ar/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على الصورة – دليل كامل لاستخراج النص المهيكل

هل احتجت يومًا إلى **تشغيل OCR على ملفات الصورة** لكن لم تكن متأكدًا من كيفية الحفاظ على المواقع الدقيقة لكل كلمة؟ لست وحدك. في العديد من المشاريع—مسح الفواتير، رقمنة النماذج، أو اختبار واجهات المستخدم—تحتاج ليس فقط إلى النص الخام بل أيضًا إلى الصناديق المحيطة التي تخبرك بمكان كل سطر على الصورة.  

يُظهر لك هذا الدرس طريقة عملية لـ *تشغيل OCR على الصورة* باستخدام محرك **aocr**، طلب **التعرف على OCR المهيكل**، ثم معالجة النتيجة مع الحفاظ على الهندسة. بنهاية الدرس ستتمكن من **استخراج النص مع الإحداثيات** في بضع أسطر من بايثون، وستفهم لماذا وضع المهيكلة مهم للمهام اللاحقة.

## ما ستتعلمه

- كيفية تهيئة محرك OCR لـ **التعرف على OCR المهيكل**.  
- كيفية إمداد الصورة واستلام النتائج الخام التي تشمل حدود السطر.  
- كيفية تشغيل معالج لاحق ينظف النص دون فقدان الهندسة.  
- كيفية التكرار على السطور النهائية وطباعة كل قطعة نص مع صندوقها المحيط.  

لا سحر، لا خطوات مخفية—فقط مثال كامل قابل للتنفيذ يمكنك إدراجه في مشروعك الخاص.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من تثبيت ما يلي:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

ستحتاج أيضًا إلى ملف صورة (`input_image.png` أو `.jpg`) يحتوي على نص واضح ومقروء. أي شيء من فاتورة ممسوحة ضوئيًا إلى لقطة شاشة يعمل، طالما أن محرك OCR يستطيع رؤية الأحرف.

---

## الخطوة 1: تهيئة محرك OCR للتعرف المهيكل

أول شيء نقوم به هو إنشاء نسخة من `aocr.Engine()` وإخبارها أننا نريد **التعرف على OCR المهيكل**. وضع المهيكلة يُعيد ليس فقط النص العادي بل أيضًا البيانات الهندسية (مستطيلات محيطة) لكل سطر، وهو أمر أساسي عندما تحتاج إلى ربط النص بالصورة.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **لماذا هذا مهم:**  
> في الوضع الافتراضي قد يعطيك المحرك سلسلة من الكلمات المتصلة فقط. وضع المهيكلة يمنحك هيكلية من صفحات → أسطر → كلمات، كل منها مع إحداثيات، مما يجعل من السهل جدًا وضع النتائج فوق الصورة الأصلية أو تمريرها إلى نموذج واعٍ للتخطيط.

---

## الخطوة 2: تشغيل OCR على الصورة والحصول على النتائج الخام

الآن نمرر الصورة إلى المحرك. استدعاء `recognize` يُعيد كائن `OcrResult` يحتوي على مجموعة من الأسطر، كل سطر له مستطيله المحيط الخاص.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

في هذه المرحلة `raw_result.lines` يحتوي على كائنات ذات خاصيتين مهمتين:

- `text` – السلسلة المعترف بها لهذا السطر.  
- `bounds` – مجموعة قيم مثل `(x, y, width, height)` تصف موقع السطر.

---

## الخطوة 3: معالجة لاحقة مع الحفاظ على الهندسة

مخرجات OCR الخام غالبًا ما تكون صاخبة: أحرف عشوائية، مسافات غير صحيحة، أو مشاكل في فواصل الأسطر. الدالة `ai.run_postprocessor` تنظف النص ولكن **تحافظ على الهندسة الأصلية**، لذا لا يزال لديك إحداثيات دقيقة.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **نصيحة احترافية:** إذا كان لديك مفردات خاصة بمجال معين (مثل رموز المنتجات)، قدم قاموسًا مخصصًا للمعالج اللاحق لتحسين الدقة.

---

## الخطوة 4: استخراج النص مع الإحداثيات – التكرار والعرض

أخيرًا، نمر على الأسطر المنقحة، ونطبع صندوق كل سطر إلى جانب نصه. هذا هو جوهر **استخراج النص مع الإحداثيات**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### النتيجة المتوقعة

بافتراض أن الصورة المدخلة تحتوي على سطرين: “Invoice #12345” و “Total: $89.99”، ستحصل على شيء مشابه لـ:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

القيمة الأولى هي `(x, y, width, height)` للسطر على الصورة الأصلية، مما يتيح لك رسم المستطيلات، تمييز النص، أو تمرير الإحداثيات إلى نظام آخر.

---

## تصور النتيجة (اختياري)

إذا أردت رؤية الصناديق المحيطة مضافة إلى الصورة، يمكنك استخدام Pillow (PIL) لرسم المستطيلات. أدناه مقتطف سريع؛ يمكنك تخطيه إذا كنت تحتاج فقط إلى البيانات الخام.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image example showing bounding boxes](/images/ocr-bounding-boxes.png "run OCR on image – bounding box overlay")

النص البديل أعلاه يحتوي على **الكلمة المفتاحية الأساسية**، لتلبية متطلبات تحسين محركات البحث لسمات alt في الصور.

---

## لماذا التعرف على OCR المهيكل يتفوق على استخراج النص البسيط

قد تتساءل، “أليس بإمكاني فقط تشغيل OCR والحصول على النص؟ لماذا أحتاج إلى الهندسة؟”  

- **السياق المكاني:** عندما تحتاج إلى ربط الحقول في نموذج (مثلاً “التاريخ” بجوار قيمة التاريخ)، تُظهر لك الإحداثيات *أين* يقع البيانات.  
- **تخطيطات متعددة الأعمدة:** النص الخطي البسيط يفقد الترتيب؛ البيانات المهيكلة تحافظ على ترتيب الأعمدة.  
- **دقة المعالجة اللاحقة:** معرفة حجم الصندوق يساعدك على تحديد ما إذا كانت الكلمة عنوانًا، حاشية، أو عنصرًا عشوائيًا.  

باختصار، **التعرف على OCR المهيكل** يمنحك المرونة لبناء خطوط أنابيب أذكى—سواء كنت تُدخل البيانات إلى قاعدة بيانات، تُنشئ ملفات PDF قابلة للبحث، أو تدرب نموذج تعلم آلي يحترم التخطيط.

---

## الحالات الطرفية الشائعة وكيفية التعامل معها

| الحالة | ما يجب مراقبته | الحل المقترح |
|-----------|-------------------|---------------|
| **صور مائلة أو مائلة** | قد تكون الصناديق المحيطة خارج المحور. | عالج مسبقًا باستخدام تصحيح الميل (مثل `warpAffine` في OpenCV). |
| **خطوط صغيرة جدًا** | قد يفوت المحرك الأحرف، مما يؤدي إلى أسطر فارغة. | زيادة دقة الصورة أو استخدام `ocr_engine.set_dpi(300)`. |
| **لغات مختلطة** | نموذج اللغة الخاطئ قد ينتج نصًا مشوشًا. | ضبط `ocr_engine.language = ["en", "de"]` قبل التعرف. |
| **صناديق متداخلة** | قد يدمج المعالج اللاحق سطرين عن غير قصد. | تحقق من `line.bounds` بعد المعالجة؛ اضبط العتبات في `ai.run_postprocessor`. |

معالجة هذه السيناريوهات مبكرًا توفر عليك عناءً كبيرًا لاحقًا، خاصةً عندما توسع الحل إلى مئات المستندات يوميًا.

---

## البرنامج الكامل من البداية إلى النهاية

فيما يلي البرنامج الكامل الجاهز للتنفيذ الذي يجمع جميع الخطوات معًا. انسخه، عدل مسار الصورة، وستكون جاهزًا.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

تشغيل هذا البرنامج سيقوم بـ:

1. **تشغيل OCR على الصورة** بوضع مهيكل.  
2. **استخراج النص مع الإحداثيات** لكل سطر.  
3. إنتاج PNG مشروح اختياريًا يُظهر الصناديق.

---

## الخلاصة

أصبح لديك الآن حل متكامل ومستقل لـ **تشغيل OCR على الصورة** و**استخراج النص مع الإحداثيات** باستخدام **التعرف على OCR المهيكل**. يوضح الكود كل خطوة—من تهيئة المحرك إلى المعالجة اللاحقة والتحقق البصري—حتى تتمكن من تكييفه مع الفواتير، النماذج، أو أي مستند بصري يحتاج إلى تحديد موقع النص بدقة.

ما الخطوة التالية؟ جرّب استبدال محرك `aocr` بمكتبة أخرى (Tesseract، EasyOCR) وانظر كيف تختلف مخرجاتهما المهيكلة. جرب استراتيجيات معالجة لاحقة مختلفة، مثل التدقيق الإملائي أو مرشحات regex مخصصة، لتعزيز الدقة في مجالك. وإذا كنت تبني خط أنابيب أكبر، فكر في تخزين أزواج `(text, bounds)` في قاعدة بيانات للتحليلات المستقبلية.

برمجة سعيدة، ولتكن مشاريع OCR دائمًا دقيقة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}