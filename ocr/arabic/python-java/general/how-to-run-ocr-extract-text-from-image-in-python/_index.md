---
category: general
date: 2026-03-26
description: كيفية تشغيل OCR على ملف PNG واستخراج النص من الصورة باستخدام قاموس مخصص
  لتحسين دقة OCR. تعلم كيفية تحميل الصورة لـ OCR بسرعة.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: ar
og_description: كيفية تشغيل OCR على ملف PNG واستخراج النص من الصورة باستخدام قاموس
  مخصص لتحسين دقة OCR. دليل خطوة بخطوة.
og_title: كيفية تشغيل OCR – استخراج النص من الصورة في بايثون
tags:
- OCR
- Python
- Image Processing
title: كيفية تشغيل OCR – استخراج النص من الصورة في بايثون
url: /ar/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR – استخراج النص من صورة في بايثون

هل تساءلت يومًا **كيف تشغّل OCR** على فاتورة ممسوحة أو لقطة شاشة وتحصل على نص نظيف وقابل للبحث؟ لست وحدك. في كثير من المشاريع، العائق الأساسي هو ببساطة تحميل الصورة لـ OCR ثم إقناع المحرك بفهم الكلمات الخاصة بالمجال.

في هذا الدرس سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ **يستخرج النص من ملفات الصور**، يوضح لك كيف **تتعرف على النص من PNG**، ويظهر حيلًا **لتحسين دقة OCR** باستخدام قواميس مخصصة وأحرف خاصة. في النهاية ستحصل على سكريبت مستقل يمكنك إدراجه في أي مشروع بايثون.

## ما ستحتاجه

- Python 3.8+ (الكود يستخدم توجيهات النوع لكنه يعمل على إصدارات 3.x السابقة)
- مكتبة `ocr` التي تأتي مع محرك OCR المستهدف (قم بالتثبيت عبر `pip install ocr‑engine` – استبدل باسم الحزمة الفعلي)
- ملف صورة (`input.png`) ترغب في معالجته
- اختياري: ملف نص عادي (`invoice_terms.txt`) يحتوي على كلمات خاصة بالمجال، كلمة واحدة في كل سطر

لا توجد تبعيات خارجية ثقيلة، ولا مفاتيح API سحابية، فقط محرك OCR محلي.

---

## الخطوة 1: تثبيت واستيراد مكتبة OCR

أولًا، تأكد من تثبيت حزمة OCR. إذا كنت تستخدم الحزمة الافتراضية `ocr-engine`، نفّذ:

```bash
pip install ocr-engine
```

الآن استورد الفئات التي ستحتاجها:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **نصيحة احترافية:** إذا كنت تستخدم بيئة افتراضية، فعّلها قبل التثبيت للحفاظ على نظافة بايثون العامة.

## الخطوة 2: إنشاء كائن محرك OCR

إنشاء كائن المحرك هو نقطة الدخول لكل مهمة OCR. فكر فيه كتشغيل جهاز الماسح الضوئي في البرمجيات.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

لماذا هذا مهم: المحرك يحتفظ بالإعدادات مثل حزم اللغات، أوضاع التعرف، وأي موارد مخصصة ستضيفها لاحقًا. بدون هذا الكائن لا يمكنك **تحميل صورة لـ OCR** أو تشغيل خط أنابيب التعرف.

## الخطوة 3: تحميل الصورة التي تريد التعرف عليها

هنا نقوم فعليًا **بتحميل صورة لـ OCR**. طريقة `Imaging.Image.load()` تقرأ الملف وتحوّله إلى تنسيق البت ماب الداخلي الذي يتوقعه المحرك.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

إذا كان لديك ملف JPEG أو TIFF، تعمل نفس الطريقة—فقط غيّر الامتداد. المحرك يكتشف الصيغة تلقائيًا.

> **حالة حافة:** الصور الكبيرة جدًا (أكثر من 5 MP) قد تتسبب في ارتفاع استهلاك الذاكرة. فكر في تقليل الحجم باستخدام Pillow قبل التحميل إذا واجهت مشاكل أداء.

## الخطوة 4: توفير قاموس مخصص لتعزيز الدقة

معظم محركات OCR تأتي بنماذج لغة عامة. بالنسبة للفواتير، الإيصالات، أو المستندات القانونية غالبًا ما تُفقد كلمات. توفير قائمة كلمات مخصصة يخبر المحرك أن “هذه المصطلحات صحيحة، تعامل معها كصحيحة”.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

قد تكون الإدخالات النموذجية مثل:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

إضافة هذه تُحسّن مقياس **تحسين دقة OCR** بشكل كبير—خاصةً للرموز غير ASCII.

## الخطوة 5: إضافة أحرف خاصة غير مغطاة في المجموعة الافتراضية

إذا كان مجالك يستخدم رموزًا مثل علامة اليورو (€) أو الحرف الإسكندنافي Ø، يمكنك إضافتها صراحةً:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

سيتعامل المحرك الآن مع هذه الرموز كصحيحة أثناء مرحلة التعرف، مما يقلل من احتمال الحصول على مخرجات “نفاية”.

## الخطوة 6: تشغيل عملية OCR واسترجاع النص

أخيرًا، استدعِ أداة التعرف واحصل على النتيجة النصية الصافية. استدعاء `recognize()` يُعيد كائنًا غنيًا؛ نحتاج فقط إلى السلسلة الخام لمعظم الحالات.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**الناتج المتوقع** (مقتطع للاختصار):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

إذا كان الناتج غير واضح، تحقق مرة أخرى من تحميل القاموس المخصص والأحرف الخاصة بشكل صحيح.

---

## نظرة بصرية

![how to run OCR diagram](ocr-workflow.png){alt="مخطط كيفية تشغيل OCR"}

المخطط أعلاه يوضح التدفق من تحميل الصورة إلى الحصول على نص نظيف، مع إبراز الأماكن التي يمكنك فيها حقن القواميس المخصصة ومجموعات الأحرف.

---

## أسئلة شائعة ومشكلات محتملة

### هل يعمل هذا مع ملفات PDF متعددة الصفحات؟

نعم—فقط حوّل كل صفحة إلى PNG (باستخدام `pdf2image` أو ما شابه) ومرّرها بالتتابع إلى نفس كائن `ocr_engine`. المعالج يتعامل مع كل صورة بشكل مستقل، ستحصل على قائمة سلاسل يمكنك دمجها.

### ماذا لو كانت الصورة مائلة؟

معظم محركات OCR الحديثة تكتشف الاتجاه تلقائيًا، لكن يمكنك فرض تدوير باستخدام:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### كيف تتعامل مع لغات غير الإنجليزية؟

بدّل نموذج اللغة قبل تحميل الصورة:

```python
ocr_engine.set_language("de")  # German
```

تأكد من تثبيت حزمة اللغة المقابلة.

---

## البرنامج الكامل – جاهز للنسخ واللصق

فيما يلي البرنامج بالكامل، جاهز للتنفيذ بعد استبدال مسارات الملفات النائبة.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

نفّذه باستخدام:

```bash
python run_ocr.py
```

سترى النص المستخرج يُطبع في وحدة التحكم. من هناك يمكنك كتابته إلى ملف، إدخاله في قاعدة بيانات، أو تمريره إلى خطوط معالجة NLP لاحقة.

---

## ملخص وخطوات قادمة

غطّينا **كيفية تشغيل OCR** على PNG، **كيفية استخراج النص من صورة**، وأظهرنا طرقًا عملية **للتعرف على النص من PNG** مع **تحسين دقة OCR** باستخدام القواميس والأحرف المخصصة.

بعد ذلك، فكر في:

- **المعالجة الدفعية:** التكرار عبر مجلد من الصور.
- **المعالجة اللاحقة:** استخدم تعبيرات regex لاستخراج أرقام الفواتير أو التواريخ.
- **التكامل:** ربط السكريبت بواجهة Flask API لتقديم خدمات OCR عند الطلب.

إذا كنت مهتمًا بمواضيع أكثر تقدمًا، اطلع على دروس حول **تحميل صورة لـ OCR** باستخدام تمهيد OpenCV، أو استكشف نماذج OCR المعتمدة على التعلم العميق مثل Tesseract 4+ مع طبقات LSTM.

---

### استمر في التجربة!

جرّب استبدال `invoice_terms.txt` بقائمة من المصطلحات الطبية، أضف أحرفًا يونانية، أو قدّم للمحرك صورة منخفضة الدقة لترى إلى أي مدى يمكن أن تمتد الدقة. كلما لعبت أكثر، كلما فهمت أفضل التوازنات بين التمهيد المسبق، القواميس المخصصة، وإعدادات المحرك.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}