---
category: general
date: 2026-06-16
description: كيفية استخدام OCR في بايثون لاستخراج النص من ملفات الصور مثل PNG. تعلم
  تحويل الصورة إلى نص خطوة بخطوة باستخدام Aspose OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- read text from png
- convert image to text
- ocr image to text python
language: ar
og_description: كيفية استخدام OCR في بايثون لاستخراج النص من الصور. يشرح هذا الدليل
  كيفية تحويل ملفات PNG إلى نص قابل للبحث باستخدام Aspose OCR.
og_title: كيفية استخدام OCR في بايثون – استخراج النص من الصور
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  headline: How to Use OCR in Python – Extract Text from Images
  type: TechArticle
- description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  name: How to Use OCR in Python – Extract Text from Images
  steps:
  - name: Expected Output
    text: '``` Detected language: English Recognized text: Hello, world! This is a
      multi‑language test. こんにちは世界 ```'
  - name: 1. License Not Found
    text: If you see an error like `License file not found`, double‑check the path
      you passed to `set_license`. Using a raw string (`r"..."`) helps avoid escape‑character
      mishaps on Windows.
  - name: 2. Blank Output
    text: 'A blank `ocr_result.text` usually means the image is too noisy or the text
      is too faint. Try increasing the image contrast:'
  - name: 3. Wrong Language Detection
    text: 'If the auto‑detect picks the wrong language, you can force a specific one:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Aspose
title: كيفية استخدام OCR في بايثون – استخراج النص من الصور
url: /ar/python-java/general/how-to-use-ocr-in-python-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في بايثون – استخراج النص من الصور

هل تساءلت يومًا **كيف تستخدم OCR** في مشروع بايثون؟ لست الوحيد. سواء كنت تبني ماسحًا للإيصالات، أو مؤرشفًا للوثائق، أو مجرد فضولي حول تحويل لقطة شاشة إلى نص قابل للتحرير، فإن القدرة على **استخراج النص من صورة** هي تغيير جذري.

في هذا الدرس سنستعرض العملية بالكامل — من تثبيت مكتبة Aspose OCR إلى قراءة النص من ملف PNG — حتى تتمكن من **تحويل الصورة إلى نص** ببضع أسطر من الشيفرة فقط. في النهاية، ستعرف بالضبط كيف **تقرأ النص من PNG** وحتى كيف تتعامل مع محتوى متعدد اللغات تلقائيًا.

> **نصيحة احترافية:** اكتشاف اللغة التلقائي في Aspose OCR يعني أنك لا تحتاج لتخمين اللغة مسبقًا — مثالي للتطبيقات العالمية.

## ما ستحتاجه

- Python 3.8+ (أحدث إصدار ثابت يكفي)
- ملف ترخيص Aspose OCR صالح (`Aspose.OCR.lic`). النسخة التجريبية المجانية تعمل للاختبار، لكن الترخيص الصحيح يزيل حدود التقييم.
- حزمة Aspose OCR مثبتة عبر `pip`:

```bash
pip install aspose-ocr
```

- ملف صورة تريد معالجته — لنستخدم `sample-multi-lang.png` كعرض توضيحي.

وجود هذه المتطلبات سيساعد على سير العملية بسلاسة وتجنب مفاجآت “module not found” لاحقًا.

![كيفية استخدام OCR في بايثون - مخطط سير العمل](https://example.com/ocr-workflow.png "كيفية استخدام OCR في بايثون – توضيح خطوة بخطوة")

*نص بديل للصورة: مخطط يوضح كيفية استخدام OCR في بايثون لاستخراج النص من صورة.*

## الخطوة 1: تطبيق ترخيص Aspose OCR (مطلوب مرة واحدة لكل تطبيق)

أول شيء يقوم به أي مشروع OCR جاد هو تحميل الترخيص. بدون ذلك، سيظهر تحذير من Aspose ويقيد عدد الصفحات التي يمكنك معالجتها.

```python
# Import the license class
from aspose.ocr import License

# Create a License object and point it to your .lic file
ocr_license = License()
ocr_license.set_license(r"C:\Path\To\Your\Aspose.OCR.lic")
```

> **لماذا هذا مهم:** تحميل الترخيص مسبقًا يضمن أن محرك **ocr image to text python** يعمل بأقصى سرعة وبدون علامات مائية. فكر فيه كفتح الميزات المميزة قبل بدء التحويل.

## الخطوة 2: إنشاء محرك OCR وتمكين اكتشاف اللغة التلقائي

الآن نقوم بإنشاء المحرك الأساسي. تمكين `language_auto_detect` أمر حاسم عندما لا تعرف ما إذا كانت الصورة تحتوي على الإنجليزية أو الإسبانية أو الصينية أو مزيج من اللغات.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine
ocr_engine = OcrEngine()

# Turn on auto‑language detection – it works for over 60 languages
ocr_engine.language_auto_detect = True
```

إذا *كنت* تعرف اللغة مسبقًا، يمكنك تعيين `ocr_engine.language = "English"` (أو أي رمز ISO مدعوم) لتسريع العملية قليلًا. لكن لأداة عامة “قراءة النص من PNG”، فإن الاكتشاف التلقائي هو الخيار الأكثر أمانًا.

## الخطوة 3: تحميل الصورة التي تريد معالجتها

يعمل Aspose OCR مع مجموعة متنوعة من الصيغ — PNG, JPEG, BMP, TIFF، وما إلى ذلك. لنحمّل ملف PNG يحتوي على عدة لغات.

```python
from aspose.ocr import Image

# Load the image from disk (replace with your actual path)
ocr_image = Image.load_from_file(r"C:\Path\To\sample-multi-lang.png")

# Assign the image to the engine
ocr_engine.image = ocr_image
```

> **حالة حافة:** إذا كانت الصورة ضخمة (أكثر من عدة ميغابايت)، قد ترغب في تقليل حجمها أولًا لتحسين الأداء. يوفر Aspose الدالة `ocr_image.resize(width, height)` لهذا الغرض.

## الخطوة 4: تنفيذ التعرف الضوئي على الأحرف (OCR)

مع إعداد كل شيء، استخراج النص يصبح استدعاءً واحدًا للدالة. كائن النتيجة يمنحك كلًا من النص المعترف به واللغة التي تم اكتشافها.

```python
# Run the recognition process
ocr_result = ocr_engine.recognize()
```

خلف الكواليس، يقوم Aspose بتشغيل شبكات عصبية متطورة وخوارزميات مطابقة الأنماط لتحويل كل مجموعة بكسلات إلى أحرف. كل العمل الشاق يتم في الكود الأصلي، لذا ستحصل على **OCR سريع ودقيق** حتى على أجهزة محدودة.

## الخطوة 5: عرض اللغة المكتشفة والنص المعترف به

أخيرًا، لنطبع ما حصلنا عليه. خاصية `detected_language` تخبرك أي لغة خمنها Aspose، و`text` يحتوي على النص الكامل.

```python
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

### النتيجة المتوقعة

```
Detected language: English
Recognized text:
 Hello, world!
 This is a multi‑language test.
 こんにちは世界
```

إذا شغلت السكريبت على صورة تحتوي على الإنجليزية واليابانية معًا، ستلاحظ تبدل اللغة تلقائيًا — بفضل ميزة الاكتشاف التلقائي التي فعلناها سابقًا.

## معالجة المشكلات الشائعة

### 1. عدم العثور على الترخيص

إذا رأيت خطأ مثل `License file not found`، تحقق مرة أخرى من المسار الذي مررته إلى `set_license`. استخدام سلسلة خام (`r"..."`) يساعد على تجنب مشاكل أحرف الهروب على نظام Windows.

### 2. ناتج فارغ

عادةً ما يعني `ocr_result.text` الفارغ أن الصورة صاخبة جدًا أو أن النص باهت. جرّب زيادة التباين في الصورة:

```python
ocr_image = Image.load_from_file("sample.png")
ocr_image = ocr_image.adjust_contrast(1.5)  # Boost contrast by 50%
ocr_engine.image = ocr_image
```

### 3. اكتشاف لغة خاطئ

إذا اختار الاكتشاف التلقائي لغة غير صحيحة، يمكنك فرض لغة معينة:

```python
ocr_engine.language = "Japanese"  # ISO code or language name
```

## توسيع المثال: معالجة دفعة من ملفات PNG

غالبًا ما ترغب في **تحويل الصورة إلى نص** لمجلد كامل، وليس ملفًا واحدًا فقط. إليك حلقة سريعة تعالج كل ملفات PNG في دليل:

```python
import os
from pathlib import Path

input_folder = Path(r"C:\Images")
output_folder = Path(r"C:\OCR_Output")
output_folder.mkdir(exist_ok=True)

for png_path in input_folder.glob("*.png"):
    # Load and assign image
    ocr_image = Image.load_from_file(str(png_path))
    ocr_engine.image = ocr_image

    # Recognize
    result = ocr_engine.recognize()

    # Write result to a .txt file with the same base name
    txt_path = output_folder / (png_path.stem + ".txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(f"Detected language: {result.detected_language}\n")
        f.write(result.text)

    print(f"Processed {png_path.name} → {txt_path.name}")
```

هذا المقتطف يوضح طريقة عملية **لاستخراج النص من صورة** على نطاق واسع، وهو مطلب شائع في خطوط أنابيب رقمنة المستندات.

## السكريبت الكامل العامل

لنجمع كل ما سبق، إليك ملف واحد يمكنك تشغيله من البداية إلى النهاية:

```python
# ocr_demo.py
import os
from aspose.ocr import License, OcrEngine, Image

# -------------------------------------------------
# 1️⃣ Apply license (replace with your own path)
# -------------------------------------------------
license_path = r"C:\Path\To\Aspose.OCR.lic"
ocr_license = License()
ocr_license.set_license(license_path)

# -------------------------------------------------
# 2️⃣ Create engine and enable auto‑detect
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.language_auto_detect = True

# -------------------------------------------------
# 3️⃣ Load image (change to your PNG file)
# -------------------------------------------------
image_path = r"C:\Path\To\sample-multi-lang.png"
ocr_image = Image.load_from_file(image_path)
ocr_engine.image = ocr_image

# -------------------------------------------------
# 4️⃣ Recognize and output results
# -------------------------------------------------
ocr_result = ocr_engine.recognize()
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

احفظه باسم `ocr_demo.py`، شغّله باستخدام `python ocr_demo.py`، وسترى اللغة والنص يُطبعان في وحدة التحكم.

## الخلاصة

غطّينا **كيفية استخدام OCR** في بايثون من البداية حتى النهاية، موضحين لك كيف **استخراج النص من صورة**، **قراءة النص من PNG**، وبشكل عام **تحويل الصورة إلى نص** باستخدام محرك Aspose القوي. بتحميل الترخيص، وتمكين اكتشاف اللغة التلقائي، وإدخال الصورة في `OcrEngine`، ستحصل على نص نظيف وقابل للبحث خلال ثوانٍ.

ما الخطوة التالية؟ جرّب استبدال Aspose ببديل مفتوح المصدر مثل Tesseract لمقارنة الدقة، أو تجربة إدخال ملفات PDF، أو دمج خطوة OCR في واجهة Flask API لمعالجة الصور مباشرة. السماء هي الحد عندما تتقن أساسيات **ocr image to text python**.

هل لديك أسئلة حول التعامل مع الخطوط الصعبة، تحسين الأداء، أو الترخيص؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [استخراج النص من صورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)
- [استخراج نص الصورة بلغة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}