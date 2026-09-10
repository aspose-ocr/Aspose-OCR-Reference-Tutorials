---
category: general
date: 2026-01-12
description: كيفية تنفيذ OCR بسرعة ودقة. تعلم تشغيل OCR على المستند، استخراج النص
  من ملف TIFF، تحميل الصورة للـ OCR وتعيين لغة OCR في بايثون.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: ar
og_description: كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) في بايثون. يوضح لك هذا
  الدليل كيفية تشغيل OCR على المستند، استخراج النص من ملف TIFF، تحميل الصورة للتعرف
  الضوئي على الأحرف وتحديد لغة OCR.
og_title: كيفية تنفيذ OCR على مستند TIFF – دليل شامل
tags:
- OCR
- Python
- Image Processing
title: كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) في مستند TIFF – دليل خطوة بخطوة
url: /ar/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إجراء OCR على مستند TIFF – دليل كامل

هل تساءلت يومًا **كيف تقوم بإجراء OCR** على ملف TIFF ممسوح ضوئيًا دون قضاء ساعات في البحث عن المكتبة المناسبة؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى استخراج النص من صور TIFF، خاصة عندما تكون الأداء وإعدادات اللغة مهمة.

في هذا الدرس سنستعرض كل ما تحتاج معرفته: من تثبيت حزمة OCR، تحميل الصورة لإجراء OCR، ضبط لغة OCR، وحتى **تشغيل OCR على المستند** واستخراج نص نظيف. بنهاية الدرس ستحصل على سكريبت جاهز للتنفيذ يمكنك إدراجه في أي مشروع.

> **نصيحة احترافية:** بينما يستخدم المثال وحدة `ocr` عامة، فإن نفس المفاهيم تنطبق على Tesseract، EasyOCR، أو أي محرك OCR حديث يقدم واجهة برمجة تطبيقات Python.

## ما ستحتاجه

- Python 3.8+ (أي نسخة حديثة تعمل)
- مكتبة OCR توفر فئة `OcrEngine` (العينة تستخدم حزمة `ocr` خيالية؛ استبدلها بالحزمة الفعلية التي تستخدمها)
- ملف TIFF متعدد الصفحات تريد معالجته (سنسميه `big_document.tif`)
- جهاز يحتوي على الأقل على 4 نوى CPU إذا كنت تخطط لتحديد عدد الخيوط

بدون خدمات خارجية، بدون مفاتيح سحابة—فقط كود محلي يعمل في ثوانٍ.

![كيفية إجراء OCR على مستند TIFF – معاينة للنص المستخرج](/images/ocr-example.png "كيفية إجراء OCR على مستند TIFF")

*نص بديل للصورة: كيفية إجراء OCR على مستند TIFF – معاينة للنص المستخرج.*

## الخطوة 1: تثبيت واستيراد مكتبة OCR

أولًا: احصل على المكتبة على جهازك. معظم حزم OCR موجودة على PyPI، لذا فإن أمر `pip install` البسيط يكفي.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

الآن استورد الفئات التي ستحتاجها. إذا كنت تستخدم Tesseract، فإن سطر الاستيراد سيختلف، لكن باقي الكود يبقى كما هو.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*لماذا هذا مهم:* استيراد الرموز الصحيحة مبكرًا يمنع تصادم الأسماء لاحقًا ويجعل السكريبت أسهل للقراءة.

## الخطوة 2: إنشاء وتكوين محرك OCR (ضبط لغة OCR)

تكوين المحرك هو المكان الذي **تضبط فيه لغة OCR** للحصول على التعرف الدقيق. الإنجليزية هي الافتراضية، لكن يمكنك التبديل إلى الفرنسية أو الألمانية أو حتى وضع متعدد اللغات بسطر واحد.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **لماذا 4 خيوط؟** معظم الحواسيب المحمولة الحديثة تحتوي على أربعة نوى على الأقل، وتحديد عدد الخيوط يمنع عملية OCR من استهلاك كامل موارد الجهاز—مفيد خصوصًا عندما يعمل السكريبت على خادم مشترك.

إذا كنت بحاجة إلى لغة أخرى، فقط استبدل `ocr.Language.ENGLISH` بـ `ocr.Language.FRENCH` أو `ocr.Language.SPANISH`، إلخ.

## الخطوة 3: تحميل الصورة لإجراء OCR (Load Image for OCR)

الآن نقوم **بتحميل الصورة لإجراء OCR**. طريقة `Image.load` تقرأ ملف TIFF إلى الذاكرة، وتتعامل مع المستندات متعددة الصفحات تلقائيًا.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*حالة حافة:* إذا كان الملف كبيرًا، قد تنفد الذاكرة RAM. في هذه الحالة، فكر في تحميل صفحة واحدة في كل مرة باستخدام `Image.load_page(page_number)` (إذا كانت المكتبة تدعم ذلك).

## الخطوة 4: تشغيل OCR على المستند

مع جاهزية المحرك وتحميل الصورة، حان الوقت لـ **تشغيل OCR على المستند**. طريقة `process` تقوم بالعمل الشاق وتعيد كائن نتيجة.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

خلف الكواليس، يقوم المحرك بتقسيم الصورة إلى كتل نصية، تشغيل نموذج التعرف، وتجميع النتائج معًا. الاستدعاء حجب (blocking)، مما يعني أن السكريبت ينتظر حتى يتم معالجة كامل ملف TIFF—مثالي للمهام الدفعية.

## الخطوة 5: استخراج النص من TIFF والتحقق من المخرجات

أخيرًا، نقوم **باستخراج النص من TIFF** عبر الوصول إلى خاصية `text` في النتيجة. لنطبع أول 200 حرف كفحص سريع.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**الناتج المتوقع (مثال):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

إذا كنت بحاجة إلى النص الكامل، استخدم ببساطة `ocr_result.text`. للمعالجة اللاحقة قد ترغب في كتابة النص إلى ملف `.txt`:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

## مثال كامل يعمل

بجمع كل ذلك معًا، إليك سكريبت جاهز للتنفيذ. استبدل اسم الحزمة النائب بالاسم الذي قمت بتثبيته فعليًا.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

شغّل السكريبت باستخدام:

```bash
python ocr_tiff_example.py
```

يجب أن ترى معاينة مطبوعة في وحدة التحكم وملفًا باسم `extracted_text.txt` يحتوي على النص الكامل.

## أسئلة شائعة وحالات حافة

- **ماذا لو كان TIFF يحتوي على عدة صفحات؟**  
  معظم محركات OCR تتعامل مع كل صفحة كصورة منفصلة داخليًا. `ocr_result.text` سيحتوي على سطر جديد بين الصفحات. إذا كنت تحتاج إلى معالجة كل صفحة على حدة، استخدم حلقة مع `Image.load_page(page_number)`.

- **هل يمكنني معالجة PNG أو JPEG بدلاً من TIFF؟**  
  بالتأكيد. طريقة `Image.load` عادةً ما تقبل أي صيغة يدعمها Pillow أو المكتبة الأساسية. فقط غيّر امتداد الملف.

- **النص مشوّه—هل يجب أن أغير اللغة؟**  
  نعم. خطوة **ضبط لغة OCR** ضرورية للوثائق غير الإنجليزية. تأكد من تثبيت حزمة اللغة (مثلاً `tesseract‑lang‑fra` للفرنسية).

- **نفاد الذاكرة؟**  
  قلل `set_memory_limit` أو عالج الصفحات واحدةً تلو الأخرى. بعض المحركات تسمح أيضًا بتقليل حجم الصورة قبل التعرف.

## الخاتمة

ها قد حصلت على دليل مختصر وعامل بالكامل حول **كيفية إجراء OCR** على ملف TIFF باستخدام Python. غطينا كل شيء من تثبيت المكتبة، تكوين المحرك (بما في ذلك **ضبط لغة OCR**)، **تحميل الصورة لإجراء OCR**، **تشغيل OCR على المستند**، وأخيرًا **استخراج النص من TIFF**.  

لا تتردد في التجربة: عدّل عدد الخيوط، غيّر اللغات، أو أدخل مخرجات OCR في خط أنابيب معالجة اللغة الطبيعية. السماء هي الحد عندما تتقن الأساسيات.

هل لديك أسئلة أخرى؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}