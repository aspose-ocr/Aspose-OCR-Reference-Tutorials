---
category: general
date: 2026-06-19
description: تحسين دقة OCR في بايثون باستخدام Aspose OCR. تعلم كيفية تعيين لغة OCR،
  تحميل الصورة للـ OCR، واستخراج النص من الصورة باستخدام قاموس مخصص.
draft: false
keywords:
- improve OCR accuracy
- extract text from image
- perform OCR on image
- load image for OCR
- set OCR language
language: ar
og_description: تحسين دقة OCR في بايثون عن طريق ضبط لغة OCR، تحميل صورة للـ OCR، واستخراج
  النص من الصورة باستخدام قاموس مخصص.
og_title: تحسين دقة التعرف الضوئي على الأحرف في بايثون – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Improve OCR accuracy in Python using Aspose OCR. Learn how to set OCR
    language, load image for OCR, and extract text from image with a custom dictionary.
  headline: Improve OCR Accuracy in Python – Complete Guide
  type: TechArticle
- description: Improve OCR accuracy in Python using Aspose OCR. Learn how to set OCR
    language, load image for OCR, and extract text from image with a custom dictionary.
  name: Improve OCR Accuracy in Python – Complete Guide
  steps:
  - name: '**Pre‑processing** – Apply contrast enhancement or binarization with Pillow
      before feeding the image to Aspose OCR.'
    text: '**Pre‑processing** – Apply contrast enhancement or binarization with Pillow
      before feeding the image to Aspose OCR.'
  - name: '**Multiple Languages** – Set `engine.language = ocr.Language.English |
      ocr.Language.French` to enable bilingual recognition.'
    text: '**Multiple Languages** – Set `engine.language = ocr.Language.English |
      ocr.Language.French` to enable bilingual recognition.'
  - name: '**Region‑Based OCR** – If you only need a specific area (e.g., a table),
      crop the image first to reduce noise.'
    text: '**Region‑Based OCR** – If you only need a specific area (e.g., a table),
      crop the image first to reduce noise.'
  - name: '**Confidence Filtering** – `result.confidence` gives a per‑character score;
      you can discard low‑confidence results programmatically.'
    text: '**Confidence Filtering** – `result.confidence` gives a per‑character score;
      you can discard low‑confidence results programmatically.'
  - name: '**Setting the OCR language** to match your document.'
    text: '**Setting the OCR language** to match your document.'
  - name: '**Loading the image correctly** so the engine sees the right pixels.'
    text: '**Loading the image correctly** so the engine sees the right pixels.'
  - name: '**Performing OCR on the image** with a single method call.'
    text: '**Performing OCR on the image** with a single method call.'
  - name: '**Extracting text from the image** and confirming the result.'
    text: '**Extracting text from the image** and confirming the result.'
  - name: '**Adding a custom dictionary** to lock in domain‑specific terms.'
    text: '**Adding a custom dictionary** to lock in domain‑specific terms.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: تحسين دقة OCR في بايثون – دليل كامل
url: /ar/python-java/general/improve-ocr-accuracy-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحسين دقة OCR في بايثون – دليل شامل

هل تساءلت يومًا كيف **تحسن دقة OCR** عندما يحتوي النص الذي تقوم بمسحه على رموز غريبة أو رموز منتجات أو أسماء علامات تجارية؟ لست وحدك. في العديد من المشاريع ينتج المحرك الافتراضي نصًا غير مفهوم، وهذا يقتل الإنتاجية حقًا.

في هذا الدرس سنستعرض مثالًا عمليًا من البداية إلى النهاية يوضح لك كيفية **تحديد لغة OCR**، **تحميل الصورة للـ OCR**، **إجراء OCR على الصورة**، وأخيرًا **استخراج النص من الصورة** باستخدام قاموس مخصص يعزز معدلات التعرف. في النهاية ستحصل على سكريبت جاهز للتنفيذ يمكنك إدراجه في أي مشروع بايثون.

## ما ستستفيده

- سكريبت بايثون كامل الوظائف يستخدم Aspose OCR لقراءة ملف PNG.
- القدرة على **تحسين دقة OCR** من خلال تكوين اللغة وقائمة كلمات مخصصة.
- شروحات واضحة لأسباب أهمية كل إعداد، بالإضافة إلى نصائح للتعامل مع الحالات الخاصة مثل الأحرف غير اللاتينية.
- قائمة مراجعة سريعة لاستكشاف الأخطاء الشائعة في OCR.

### المتطلبات المسبقة

- Python 3.8 أو أحدث مثبت على جهازك.  
- حزمة `aspose-ocr` (تثبيت عبر `pip install aspose-ocr`).  
- صورة نموذجية (`technical_doc.png`) تحتوي على النص الذي تريد قراءته.  
- إلمام أساسي ببايثون—لا شيء معقد مطلوب.

> **نصيحة احترافية:** إذا كنت تعمل في بيئة افتراضية، فعّلها قبل تثبيت الحزمة. هذا يحافظ على نظافة الاعتمادات ويتجنب تعارض الإصدارات.

---

## الخطوة 1: تثبيت واستيراد Aspose OCR

أولًا، لنقم بإضافة المكتبة إلى بيئتنا واستيراد المكونات التي نحتاجها.

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

import aspose.ocr as ocr
```

مساحة الاسم `aspose.ocr` تمنحك الوصول إلى الفئة `OcrEngine`، وهي قلب عملية OCR. استيرادها هنا يبقي باقي السكريبت نظيفًا وسهل القراءة.

---

## الخطوة 2: إنشاء محرك OCR و **تحديد لغة OCR**

لماذا اللغة مهمة؟ تعتمد محركات OCR على نماذج مخصصة للغة لتعرف أشكال الأحرف وأنماط الكلمات. إذا أخبرت المحرك أنك تمسح نصًا إنجليزيًا، سيتجاهل الحروف السيريلية ويركز على الأبجدية اللاتينية، مما يؤدي إلى **تحسين دقة OCR** بشكل ملحوظ.

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Set the recognition language to English (you can pick other languages too)
engine.language = ocr.Language.English
```

> **ملاحظة:** يدعم Aspose OCR أكثر من 50 لغة. استبدل `ocr.Language.English` بـ `ocr.Language.Spanish` أو `ocr.Language.French` وغيرها إذا لم يكن مستندك إنجليزيًا.

---

## الخطوة 3: تعريف **قاموس مخصص** لتعزيز الدقة

تخيل أنك تمسح فواتير تحتوي على كلمة “AsposeOCR” أو رموز منتجات مثل “SKU12345”. المحرك لا يعرف هذه المصطلحات، فيخمنها بشكل غير صحيح. توفير قائمة كلمات مخصصة يخبر المحرك: *“هذه السلاسل صحيحة—لا تحاول تصحيحها.”* وهذا يُعد فوزًا سريعًا لـ **تحسين دقة OCR**.

```python
# Step 3: Create a list of domain‑specific words
custom_word_list = [
    "AsposeOCR",   # brand name
    "InvoiceID",   # field label
    "SKU12345",    # product code
    "β‑cell"       # Greek character example
]

# Attach the custom dictionary to the engine
engine.text_processing.custom_dictionary = custom_word_list
```

يمكنك تحميل هذه القائمة من ملف أو قاعدة بيانات إذا كان لديك مئات الإدخالات—فقط احتفظ بها في قائمة بايثون للتبسيط.

---

## الخطوة 4: **تحميل الصورة للـ OCR**

الآن نحتاج إلى صورة. طريقة `Image.load` تقبل مسارًا لأي تنسيق نقطي مدعوم (PNG، JPEG، BMP، إلخ). إذا تعذر العثور على الملف، يرمي المحرك استثناءً، لذا سنحمي الكود من ذلك.

```python
import os

image_path = "YOUR_DIRECTORY/technical_doc.png"

if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found: {image_path}")

# Step 4: Load the image into memory
image = ocr.Image.load(image_path)
```

> **لماذا هذه الخطوة مهمة:** تحميل الصورة بشكل صحيح يضمن أن المحرك يعمل على بيانات البكسل الدقيقة التي تريد تحليلها. الملفات التالفة أو المسارات الخاطئة هي مصدر شائع للإحباط.

---

## الخطوة 5: **إجراء OCR على الصورة** واستخراج النتائج

مع تكوين المحرك وتحضير الصورة، يصبح التعرف الفعلي استدعاء طريقة واحدة. يحتوي كائن النتيجة على النص الخام، درجات الثقة، وحتى معلومات التخطيط إذا احتجت إليها لاحقًا.

```python
# Step 5: Run OCR
result = engine.recognize(image)

# The recognized text is stored in result.text
recognized_text = result.text
```

إذا أردت **استخراج النص من الصورة** سطرًا بسطر، يمكنك التقسيم بناءً على أحرف السطر الجديد:

```python
lines = recognized_text.splitlines()
for idx, line in enumerate(lines, start=1):
    print(f"{idx:02d}: {line}")
```

---

## الخطوة 6: التحقق من المخرجات – هل حقًا **تحسن دقة OCR**؟

لنطبع النتيجة ونرى إذا ما كان القاموس المخصص قد أحدث فرقًا.

```python
print("\n--- OCR Output ---")
print(recognized_text)
```

المخرجات النموذجية للصورة التجريبية قد تبدو هكذا:

```
--- OCR Output ---
InvoiceID: 2023‑07‑15
Customer: AsposeOCR Ltd.
Product: β‑cell Therapy Kit
SKU: SKU12345
```

لاحظ كيف يظهر اسم العلامة التجارية، الحرف اليوناني، ورمز المنتج تمامًا كما عرّفناها. بدون القاموس المخصص، كان المحرك سيحاول “تصحيح” هذه العناصر، غالبًا ما ينتج شيء مثل “Aspose OCR” أو “SKU 1234”.

---

## المشكلات الشائعة وكيفية التعامل معها

| المشكلة | السبب | الحل |
|-------|----------------|-----|
| **حروف غير مفهومة** | تعيين لغة خاطئة أو صورة منخفضة الدقة | تأكد من أن `engine.language` يطابق لغة المصدر واستخدم مسحًا بدقة عالية (300 dpi أو أعلى). |
| **تجاهل الكلمات المخصصة** | القاموس غير مرفق أو هناك خطأ إملائي في اسم الخاصية | راجع `engine.text_processing.custom_dictionary = …`. |
| **الملف غير موجود** | مسار غير صحيح أو أذونات ملف مفقودة | استخدم `os.path.abspath()` للتحقق من المسار المطلق؛ شغّل السكريبت بأذونات مناسبة. |
| **بطء المعالجة** | صور كبيرة أو صفحات متعددة | عالج الصورة مسبقًا (قص، تغيير حجم) أو استخدم `engine.recognize(image, max_threads=4)` للتنفيذ المتوازي. |

---

## التعمق: تحسينات متقدمة لـ **تحسين دقة OCR**

1. **المعالجة المسبقة** – طبّق تحسين التباين أو التحويل إلى أبيض وأسود باستخدام Pillow قبل تمرير الصورة إلى Aspose OCR.  
2. **عدة لغات** – عيّن `engine.language = ocr.Language.English | ocr.Language.French` لتمكين التعرف الثنائي اللغة.  
3. **OCR قائم على المنطقة** – إذا كنت تحتاج فقط إلى جزء محدد (مثل جدول)، قص الصورة أولًا لتقليل الضوضاء.  
4. **تصفية الثقة** – `result.confidence` يعطي درجة ثقة لكل حرف؛ يمكنك استبعاد النتائج ذات الثقة المنخفضة برمجيًا.

---

## السكريبت الكامل القابل للتنفيذ

فيما يلي السكريبت الكامل جاهز للنسخ واللصق والذي يدمج كل خطوة ناقشناها. احفظه باسم `improve_ocr_accuracy.py` وشغّله من سطر الأوامر.

```python
# improve_ocr_accuracy.py
# Complete example that shows how to improve OCR accuracy with Aspose OCR in Python.

import os
import aspose.ocr as ocr

def main():
    # ---------- Step 1: Initialize engine and set language ----------
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English          # set OCR language

    # ---------- Step 2: Attach custom dictionary ----------
    custom_word_list = [
        "AsposeOCR",
        "InvoiceID",
        "SKU12345",
        "β‑cell"
    ]
    engine.text_processing.custom_dictionary = custom_word_list

    # ---------- Step 3: Load the image ----------
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    image = ocr.Image.load(image_path)               # load image for OCR

    # ---------- Step 4: Perform OCR ----------
    result = engine.recognize(image)                 # perform OCR on image
    recognized_text = result.text

    # ---------- Step 5: Output the recognized text ----------
    print("\n--- OCR Output ---")
    print(recognized_text)

    # Optional: print line numbers for easier debugging
    print("\n--- Line‑by‑Line View ---")
    for idx, line in enumerate(recognized_text.splitlines(), start=1):
        print(f"{idx:02d}: {line}")

if __name__ == "__main__":
    main()
```

شغّله:

```bash
python improve_ocr_accuracy.py
```

سترى المخرجات المنسقة بشكل جميل التي عرضناها سابقًا.

---

## الخلاصة

لقد غطينا طريقة بسيطة لـ **تحسين دقة OCR** في بايثون من خلال:

1. **تحديد لغة OCR** لتطابق مستندك.  
2. **تحميل الصورة بشكل صحيح** حتى يرى المحرك البكسلات المطلوبة.  
3. **إجراء OCR على الصورة** باستدعاء طريقة واحدة.  
4. **استخراج النص من الصورة** وتأكيد النتيجة.  
5. **إضافة قاموس مخصص** لتثبيت المصطلحات الخاصة بالمجال.

هذا هو سير العمل الكامل—from الصورة الخام إلى نص نظيف قابل للبحث—معبأ في سكريبت قابل لإعادة الاستخدام.

إذا كنت مستعدًا للتحدي التالي، جرّب تجربة المعالجة المسبقة للصور (التباين، تصحيح الميل) أو انتقل إلى إعداد متعدد اللغات باستخدام `ocr.Language.English | ocr.Language.German`. نفس المبادئ تنطبق، وستستمر في **تحسين دقة OCR** عبر مجموعة أوسع من المستندات.

هل لديك أسئلة أو حالة خاصة غريبة؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

![improve OCR accuracy


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}