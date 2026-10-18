---
category: general
date: 2026-08-12
description: قم بتشغيل OCR على الصورة باستخدام بايثون و Aspose AI لاستخراج النص من
  الصورة وتحسين دقة OCR باستخدام معالج ما بعد المعالجة لتصحيح الإملاء.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: ar
lastmod: 2026-08-12
og_description: قم بتشغيل OCR على الصورة في بايثون واستخراج النص من الصورة فورًا مع
  تحسين دقة OCR باستخدام المعالجة اللاحقة للذكاء الاصطناعي من Aspose.
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: تشغيل OCR على صورة باستخدام بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: تشغيل OCR على صورة باستخدام بايثون – دليل خطوة بخطوة
url: /ar/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على صورة باستخدام Python – دليل خطوة بخطوة

إذا كنت بحاجة إلى **تشغيل OCR على ملفات الصور** في Python، فإن هذا الدليل يرافقك عبر سير العمل بالكامل. ستتعلم كيف **استخراج النص من الصورة**، وتطبيق **تصحيح نص OCR**، و**تحسين دقة OCR** باستخدام بضع أسطر من الشيفرة فقط.

معالجة المستندات الممسوحة، الإيصالات، أو لقطات الشاشة غالبًا ما ينتج عنها نصوص مشوشة. من خلال إرفاق معالج تدقيق إملائي بعد العملية، يمكنك تحويل مخرجات OCR الخام إلى محتوى نظيف وقابل للبحث دون الحاجة إلى أداة منفصلة. يغطي هذا الشرح كل ما تحتاجه—من تحميل الصورة إلى عرض النتيجة المصححة.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* Python 3.9 أو أحدث مثبت.
* الوصول إلى حزم Aspose.OCR و Aspose.AI للـ Python (أو ما يعادلها من أطر مفتوحة المصدر).
* صورة نموذجية (مثلاً `sample.png`) موجودة في دليل معروف.
* إلمام أساسي بدوال Python والبرمجة الكائنية.

يمكنك تثبيت المكتبات المطلوبة باستخدام pip:

```bash
pip install aspose-ocr aspose-ai
```

> **نصيحة احترافية:** استخدم بيئة افتراضية (`python -m venv .venv`) لعزل الاعتمادات.

## الخطوة 1: تشغيل OCR على صورة – إنشاء كائن المحرك

الخطوة الأولى هي إنشاء كائن `OcrEngine`. هذا الكائن يضم إعدادات محرك OCR ويوفر طرقًا لمعالجة الصور والتعرف عليها.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

إنشاء المحرك مرة واحدة وإعادة استخدامه عبر صور متعددة يقلل من زمن بدء التشغيل ويضمن إعدادات متسقة طوال الجلسة.

## الخطوة 2: تحميل الصورة لـ OCR

قبل أن يتم التعرف، يجب على المحرك معرفة أي صورة سيحللها. طريقة `load_image` تقبل مسار ملف أو تدفق ثنائي.

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **لماذا هذا مهم:** تحميل الصورة بشكل صحيح هو الأساس للحصول على OCR دقيق. توفير صورة عالية الدقة (300 dpi أو أعلى) عادةً ما **يحسن دقة OCR** لأن المحرك يستطيع تمييز الأحرف بوضوح أكبر.

## الخطوة 3: استخراج النص من الصورة – إجراء التعرف الأساسي

بعد تحميل الصورة، يمكنك استدعاء `recognize()` للحصول على كائن نتيجة. تحتوي النتيجة على النص الخام، درجات الثقة، وبشكل اختياري مربعات الإحاطة لكل كلمة.

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

في هذه المرحلة تكون قد **شغلت OCR على صورة** واستخرجت الأحرف الخام. ومع ذلك، قد يحتوي النص على أخطاء إملائية، خاصةً في المسحات منخفضة الجودة.

## الخطوة 4: تصحيح نص OCR – إرفاق مدقق إملائي بعد المعالجة

توفر Aspose AI خط أنابيب مرن للمعالجة اللاحقة. من خلال توصيل مدقق إملائي مخصص يمكنك تصحيح الأخطاء الشائعة في OCR (مثل “l” مقابل “1”، “O” مقابل “0”).

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**كيفية عمل المدقق الإملائي:** يجب أن يطبق `MySpellChecker` طريقة `process(text: str) -> str`. داخل هذه الطريقة، يمكنك استخدام مكتبات مثل `pyspellchecker` أو `symspellpy` لاستبدال تسلسلات الكلمات غير المحتملة ببدائل تم التحقق منها في القاموس.

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## الخطوة 5: عرض النص الأصلي والنص المصحح من OCR

أخيرًا، قارن بين المخرجات الخام والمصححة. يساعدك ذلك على التحقق من أن **تصحيح نص OCR** قد **حسن دقة OCR** لحالتك.

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### النتيجة المتوقعة

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

السطر المصحح يُظهر أن المدقق الإملائي استبدل الأخطاء الشائعة في OCR (`Th1s` → `This`, `s4mpl3` → `simple`, `rec3pt` → `receipt`, `som3` → `some`, `err0rs` → `errors`).

## الخطوة 6: تحسين دقة OCR – قائمة مراجعة لأفضل الممارسات

حتى مع المعالجة اللاحقة، يمكنك رفع جودة محرك OCR الأساسية:

| عنصر القائمة | لماذا يساعد |
|--------------|--------------|
| **استخدام صور عالية الدقة (≥300 dpi)** | المزيد من بيانات البكسل يقلل من غموض الأحرف. |
| **تحويل الصور الملونة إلى تدرج الرمادي** | يزيل الضوضاء اللونية التي قد تربك المحرك. |
| **تطبيق تصحيح الميل للصور** | يُستقيم النص المائل، مما يمنع أخطاء تقسيم الأسطر. |
| **تحديد اللغة/الإقليم صراحةً** | يوجه المُعرّف نحو مجموعة الأحرف الصحيحة. |
| **تمكين نموذج اللغة** (إذا كانت المكتبة تدعمه) | يوفر توقعات تعتمد على السياق، مما **يحسن دقة OCR** أكثر. |

يمكنك تنفيذ هذه الخطوات التحضيرية باستخدام Pillow أو OpenCV قبل تمرير الصورة إلى `ocr_engine`.

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## سكريبت كامل قابل للتنفيذ

بجمع كل ما سبق، يصبح السكريبت التالي جاهزًا للنسخ واللصق في ملف اسمه `run_ocr.py` وتشغيله.

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

تشغيل السكريبت يطبع النص الأصلي والنص المصحح، مؤكدًا أنك قد **شغلت OCR على صورة**، **استخرت النص من الصورة**، و**حسّنت دقة OCR** عبر **تصحيح نص OCR**.

## الخلاصة

أنت الآن تعرف كيف **تشغل OCR على صورة** باستخدام Python، تستخرج النص الخام، وتطبق مدقق إملائي بعد المعالجة للحصول على نتائج أنظف. باتباع قائمة المراجعة لـ **تحسين دقة OCR**، يمكنك تكييف هذا سير العمل مع الإيصالات، الفواتير، بطاقات الهوية، أو أي مستند ممسوح ضوئيًا.

### ما التالي؟

* استكشف **قواميس مخصصة للغات** لـ OCR متعدد اللغات.
* دمج الخط الأنابيب مع قاعدة بيانات أو فهرس بحث (مثل Elasticsearch) لجعل النص المستخرج قابلًا للبحث.
* استبدل المدقق الإملائي البسيط بنموذج لغة عصبي (مثل تصحيح قائم على GPT) للحصول على دقة أعلى.

لا تتردد في تجربة تقنيات مختلفة لمعالجة الصور مسبقًا، أو معالجات لاحقة مختلفة، أو محركات OCR بديلة. النمط الأساسي—**تشغيل OCR على صورة → استخراج النص من صورة → تصحيح نص OCR → تحسين دقة OCR**—يبقى هو نفسه، مما يمنحك أساسًا قويًا لأي مشروع رقمنة مستندات.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}