---
category: general
date: 2026-04-26
description: كيفية إنشاء OCR بسرعة وبشكل موثوق. تعلم استخراج النص من الصورة، تحميل
  الصورة للـ OCR، وتشغيل OCR على ملف PNG باستخدام قاموس مخصص.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: ar
og_description: كيفية إنشاء OCR في بايثون واستخراج النص من الصورة. يوضح هذا الدليل
  كيفية تحميل الصورة للتعرف الضوئي على الأحرف، تشغيل OCR على ملفات PNG، واستخدام قاموس
  مخصص.
og_title: كيفية إنشاء OCR في بايثون – استخراج النص بسرعة
tags:
- OCR
- Python
- Image Processing
title: كيفية إنشاء OCR في بايثون – استخراج النص من الصورة
url: /ar/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء OCR في بايثون – دليل خطوة بخطوة

هل تساءلت يومًا **كيف تنشئ OCR** يمكنه قراءة ملفات PDF الممسوحة ضوئيًا، لقطات الشاشة، أو الملاحظات المكتوبة يدويًا؟ لست وحدك. في العديد من المشاريع الواقعية نحتاج إلى *استخراج النص من ملفات الصورة*، لكن المحركات الجاهزة غالبًا ما تتعثر مع الكلمات المتخصصة.  

في هذا الدرس سترى مثالًا كاملًا وقابلًا للتنفيذ يقوم بتحميل صورة للـ OCR، يطبق قاموسًا مخصصًا، وأخيرًا **تشغيل OCR على ملفات PNG**. بحلول النهاية ستتمكن من استخراج النص من أي صورة وتكييف المحرك مع مصطلحاتك الخاصة.

## ما يغطيه هذا الدرس

* تثبيت حزمة `aocr` الصغيرة ولكن القوية (أو أي مكتبة متوافقة).  
* تكوين **قاموس مخصص** بحيث يتم التعرف على مصطلحات مثل `aspocorp` أو `licensekey`.  
* **تحميل صورة للـ OCR**، سواء كانت PNG أو JPEG أو صفحة PDF ممسوحة.  
* تشغيل عملية الـ OCR وطباعة النتيجة.  

لا روابط توثيق خارجية، مجرد حل مستقل يمكنك نسخه‑ولصقه وتشغيله اليوم.

### المتطلبات المسبقة

* Python 3.8 أو أحدث (الكود يستخدم f‑strings).  
* إلمام أساسي بسطر الأوامر – ستكتب بضع أوامر `pip install`.  
* ملف صورة (`technical_doc.png` في المثال) موجود في مكان يمكنك الإشارة إليه.  

إذا استوفيت هذه العناصر الثلاثة، فأنت جاهز للبدء.  

---

## الخطوة 1: تثبيت مكتبة OCR

أولاً، نحتاج إلى محرك OCR يدعم كائن تكوين قابل للبرمجة. حزمة `aocr` هي غلاف خفيف الوزن حول محرك OCR أصلي وتعمل جيدًا للعرض.

```bash
# Install the library (run once)
pip install aocr
```

> **نصيحة احترافية:** إذا كنت على نظام Windows وصادفت خطأ تجميع، جرّب `pip install aocr‑binary` الذي يوفّر حزمًا مسبقة البناء.

### لماذا تثبيت هذه المكتبة؟

`aocr` يوفّر لنا وصولًا مباشرًا إلى كائن `config` حيث يمكننا حقن **قاموس مخصص**. هذه هي الصلصة السرية لتحسين الدقة في المفردات المتخصصة.

---

## الخطوة 2: إنشاء مثيل محرك OCR وإضافة قاموس مخصص

الآن نقوم بتشغيل المحرك ونخبره بالكلمات التي يجب أن يعتبرها معروفة.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### لماذا القاموس المخصص مهم

نماذج OCR القياسية تُدرب على مجموعات نصية عامة. عندما يرى النموذج كلمة “aspocorp”، قد يقسمها إلى “aspo corp” أو يحذف حروفًا تمامًا. من خلال تزويد القائمة المخصصة، نُوجه المُعرّف نحو التهجئة الدقيقة التي نحتاجها، مما يقلل بشكل كبير من جهد ما بعد المعالجة.

---

## الخطوة 3: تحميل الصورة التي تريد معالجتها

هنا نُحمِّل **الصورة للـ OCR**. طريقة `Image.load` تقبل سلسلة مسار وتحدد نوع الملف تلقائيًا.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **حالة خاصة:** إذا كان المصدر ملف PDF متعدد الصفحات، حوِّل كل صفحة إلى PNG أولاً (مثلاً باستخدام `pdf2image`) وقدمها واحدةً تلو الأخرى إلى المحرك.

### نصائح لتحسين جودة الصورة

* حافظ على الدقة على الأقل 300 dpi.  
* تأكد من أن الصورة في وضعية صحيحة؛ قم بالتدوير باستخدام `Pillow` إذا لزم الأمر.  
* حوِّل المسحات الملونة إلى تدرج الرمادي لتقليل الضوضاء.

---

## الخطوة 4: تشغيل عملية OCR على ملف PNG

مع تكوين المحرك وتحميل الصورة، نُنفّذ أخيرًا **OCR على PNG**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

نداء `process()` يُعيد كائنًا يحتوي على النص المُعترف به، درجات الثقة، ومربعات الإحاطة لكل كلمة.

---

## الخطوة 5: إخراج النص المُعترف به

أسهل طريقة لرؤية ما وجده المحرك هي طباعة الخاصية `text`.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### النتيجة المتوقعة

إذا كان ملف `technical_doc.png` يحتوي على الجملة *“The Aspocorp licensekey expires on 2025‑12‑31.”*، يجب أن يعرض الطرفية:

```
The Aspocorp licensekey expires on 2025-12-31.
```

لاحظ كيف حافظ القاموس المخصص على اسم العلامة التجارية دون تعديل—شيء قد يُشوّه في OCR العادي.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي السكريبت الكامل، جاهز للحفظ كملف `run_ocr.py`. فقط استبدل مسار العنصر النائب بموقع صورتك.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

شغّله من الطرفية:

```bash
python run_ocr.py
```

يجب أن ترى النص المستخرج يُطبع في الطرفية، تمامًا كما هو موضح في المثال السابق.

---

## الأسئلة المتكررة (FAQ)

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني استخراج النص من PDF ممسوح ضوئيًا؟** | نعم. حوّل كل صفحة إلى PNG (أو TIFF) أولاً، ثم قدّم الصور إلى نفس السكريبت. |
| **ماذا لو كانت صورتي JPEG بدلاً من PNG؟** | طريقة `Image.load` تدعم JPEG و BMP و TIFF و PNG مباشرة. فقط غيّر امتداد الملف. |
| **كيف أحسن الدقة في المسحات منخفضة التباين؟** | قم بالمعالجة المسبقة باستخدام `Pillow` – زيادة التباين، تطبيق التثنائي، أو استخدم `opencv` لتصحيح الميل. |
| **هل هناك طريقة للحصول على درجات الثقة لكل كلمة؟** | `ocr_result` يتضمن `words` – كل كلمة لها خاصية `confidence` يمكنك التكرار عليها. |
| **هل يمكن تشغيل هذا على خادم بدون واجهة رسومية؟** | بالطبع. `aocr` لا يعتمد على واجهة رسومية، مما يجعله مثاليًا لأنابيب CI. |

---

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن عرفت **كيفية إنشاء OCR** و **استخراج النص من ملفات الصورة**، فكر في استكشاف:

* **تقنيات ما قبل المعالجة** – `load image for OCR` هي الخطوة الأولى فقط؛ استخدم `opencv` لإزالة الضوضاء أو تحسين الحدة.  
* **المعالجة الدفعية** – تكرار عبر مجلد PNGs لإنشاء أرشيف قابل للبحث.  
* **دعم متعدد اللغات** – أضف حزم اللغة إلى المحرك إذا كنت بحاجة لقراءة مستندات بالفرنسية أو الألمانية.  
* **التكامل مع Elasticsearch** – فهرسة النص المستخرج للبحث النصي الكامل عبر الأصول الممسوحة.  

كل من هذه الإضافات يبنى على النمط الأساسي الذي غطيناه، لذا ستجد الانتقال سهلًا.

---

## الخلاصة

في بضع دقائق أجبنا على **كيفية إنشاء OCR** الذي يستخرج النص من ملفات الصورة بشكل موثوق، خاصة PNGs، وأظهرنا لك كيفية **تحميل صورة للـ OCR**، تطبيق **قاموس مخصص**، و **تشغيل OCR على PNG** دون أي خدمات خارجية.  

جرّب السكريبت، عدّل القاموس ليتناسب مع مصطلحاتك، وستحصل على أساس قوي لأي مشروع رقمنة مستندات.  

إذا واجهت أي مشاكل، اترك تعليقًا أدناه—سعيد بالمساعدة. ولا تنس مشاركة قصص نجاحك؛ المجتمع يتعلم أفضل من الأمثلة الواقعية.  

**هل أنت مستعد لأتمتة أوراقك؟** احصل على الكود، عدّله، وابدأ بتحويل البكسلات إلى نص قابل للبحث اليوم!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}