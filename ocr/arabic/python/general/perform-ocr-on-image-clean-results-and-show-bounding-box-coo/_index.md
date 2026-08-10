---
category: general
date: 2026-03-28
description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على الصورة واحصل على نص نظيف
  مع إحداثيات الصناديق المحيطة. تعلم كيفية استخراج النص من OCR، تنظيفه، وعرض النتائج
  خطوة بخطوة.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: ar
og_description: نفّذ OCR على الصورة، نظّف النتيجة، واعرض إحداثيات الصناديق المحيطة
  في دليل مختصر.
og_title: تنفيذ التعرف الضوئي على الأحرف في الصورة – نتائج نظيفة ومربعات الإحاطة
tags:
- OCR
- Computer Vision
- Python
title: إجراء التعرف الضوئي على الأحرف في الصورة – نتائج نظيفة وعرض إحداثيات الصندوق
  المحيط
url: /ar/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على الصورة – تنظيف النتائج وعرض إحداثيات الصناديق المحيطة

هل احتجت يوماً إلى **إجراء OCR على ملفات الصور** لكنك حصلت على نص فوضوي ولا تعرف أين يقع كل كلمة في الصورة؟ لست وحدك. في العديد من المشاريع—رقمنة الفواتير، مسح الإيصالات، أو استخراج النص البسيط—الحصول على مخرجات OCR الخام هو مجرد العائق الأول. الخبر السار؟ يمكنك تنظيف تلك المخرجات ورؤية إحداثيات الصناديق المحيطة لكل منطقة فوراً دون كتابة الكثير من الشيفرة المتكررة.

في هذا الدليل سنستعرض **كيفية استخراج OCR**، تشغيل **معالج لاحق لتنظيف OCR**، وأخيراً **عرض إحداثيات الصناديق المحيطة** لكل منطقة تم تنظيفها. في النهاية ستحصل على سكريبت واحد قابل للتنفيذ يحول صورة غير واضحة إلى نص منظم ومهيكل جاهز للمعالجة اللاحقة.

## ما ستحتاجه

- Python 3.9+ (الصياغة أدناه تعمل على 3.8 وما فوق)
- محرك OCR يدعم `recognize(..., return_structured=True)` – على سبيل المثال مكتبة خيالية `engine` مستخدمة في المقتطف. استبدلها بـ Tesseract أو EasyOCR أو أي SDK يُعيد بيانات المناطق.
- إلمام أساسي بدوال Python والحلقات
- ملف صورة تريد مسحه (PNG، JPG، إلخ)

> **نصيحة احترافية:** إذا كنت تستخدم Tesseract، فإن الدالة `pytesseract.image_to_data` تُعطيك الصناديق المحيطة بالفعل. يمكنك تغليف نتيجتها بمحول صغير يحاكي واجهة `engine.recognize` الموضحة أدناه.

---

![مثال على إجراء OCR على الصورة](image-placeholder.png "مثال على إجراء OCR على الصورة")

*نص بديل: مخطط يوضح كيفية إجراء OCR على الصورة وتصور إحداثيات الصناديق المحيطة*

## الخطوة 1 – إجراء OCR على الصورة والحصول على المناطق المهيكلة

الخطوة الأولى هي طلب من محرك OCR أن يُعيد ليس فقط النص العادي بل قائمة مهيكلة من مناطق النص. تحتوي هذه القائمة على السلسلة النصية الخام والمستطيل الذي يحيط بها.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**لماذا هذا مهم:**  
عند طلب النص العادي فقط تفقد السياق المكاني. البيانات المهيكلة تتيح لك لاحقاً **عرض إحداثيات الصناديق المحيطة**، محاذاة النص مع الجداول، أو تمرير المواقع الدقيقة إلى نموذج لاحق.

## الخطوة 2 – كيفية تنظيف مخرجات OCR باستخدام معالج لاحق

محركات OCR جيدة في التعرف على الأحرف، لكنها غالباً ما تترك مسافات زائدة، قطع سطر غير مرغوب فيها، أو رموز تم التعرف عليها خطأً. المعالج اللاحق يُطبع النص، يُصحح الأخطاء الشائعة في OCR، ويزيل الفراغات الزائدة.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

إذا كنت تبني منظفك الخاص، فكر في:

- إزالة الأحرف غير ASCII (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- دمج مسافات متعددة إلى مسافة واحدة
- تطبيق مدقق إملائي مثل `pyspellchecker` لتصحيح الأخطاء الواضحة

**لماذا يجب أن تهتم:**  
السلسلة النظيفة تجعل البحث، الفهرسة، وسلاسل معالجة اللغة الطبيعية اللاحقة أكثر موثوقية. بعبارة أخرى، **كيفية تنظيف OCR** غالباً ما تكون الفارق بين مجموعة بيانات صالحة وصداع رأس.

## الخطوة 3 – عرض إحداثيات الصناديق المحيطة لكل منطقة تم تنظيفها

الآن بعد أن أصبح النص مرتباً، نمر على كل منطقة، نطبع مستطيلها والنص المنظف. هذه هي الخطوة التي نُظهر فيها أخيراً **إحداثيات الصناديق المحيطة**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**نموذج الإخراج**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

يمكنك الآن تمرير تلك الإحداثيات إلى مكتبة رسم (مثل OpenCV) لتغطية الصناديق على الصورة الأصلية، أو تخزينها في قاعدة بيانات لاستعلامات لاحقة.

## البرنامج الكامل الجاهز للتنفيذ

فيما يلي البرنامج الكامل الذي يجمع بين الخطوات الثلاث. استبدل استدعاءات `engine` الوهمية بـ SDK OCR الفعلي الخاص بك.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### كيفية التشغيل

```bash
python perform_ocr.py sample_invoice.jpg
```

سترى قائمة بالصناديق المحيطة مقترنة بالنص المنظف، تماماً كما هو موضح في نموذج الإخراج أعلاه.

## الأسئلة المتكررة والحالات الخاصة

| السؤال | الجواب |
|----------|--------|
| **ماذا لو لم يدعم محرك OCR الخاص بـ `return_structured`؟** | اكتب غلافًا خفيفًا يحول مخرجات المحرك الخام (عادةً قائمة كلمات مع إحداثيات) إلى كائنات تحتوي على خصائص `text` و `bounding_box`. |
| **هل يمكنني الحصول على درجات الثقة؟** | العديد من SDKs تُظهر مقياس الثقة لكل منطقة. أضفه إلى جملة الطباعة: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **كيف أتعامل مع النص المدور؟** | عالج الصورة مسبقًا باستخدام `cv2.minAreaRect` من OpenCV لتصحيح الانحراف قبل استدعاء `recognize`. |
| **ماذا لو احتجت المخرجات بصيغة JSON؟** | سَلّس `processed_result.regions` باستخدام `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **هل هناك طريقة لتصور الصناديق؟** | استخدم OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` داخل الحلقة، ثم `cv2.imwrite("annotated.jpg", img)`. |

## الخلاصة

لقد تعلمت الآن **كيفية إجراء OCR على الصورة**، تنظيف المخرجات الخام، و**عرض إحداثيات الصناديق المحيطة** لكل منطقة. تدفق الخطوات الثلاث—التعرف → المعالجة اللاحقة → التكرار—هو نمط قابل لإعادة الاستخدام يمكنك دمجه في أي مشروع Python يحتاج إلى استخراج نص موثوق.

### ما التالي؟

- **استكشاف محركات OCR مختلفة** (Tesseract، EasyOCR، Google Vision) ومقارنة الدقة.
- **دمج مع قاعدة بيانات** لتخزين بيانات المناطق لأرشفة قابلة للبحث.
- **إضافة كشف لغة** لتوجيه كل منطقة إلى مدقق إملائي مناسب.
- **تغطية الصناديق على الصورة الأصلية** للتحقق البصري (انظر مقتطف OpenCV أعلاه).

إذا صادفتك أية مشاكل، تذكر أن أكبر فائدة تأتي من خطوة المعالجة اللاحقة القوية؛ النص المنظف أسهل بكثير في التعامل منه إلى تفريغ عشوائي من الأحرف.

برمجة سعيدة، ولتكن خطوط أنابيب OCR الخاصة بك دائماً مرتبة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}