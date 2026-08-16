---
category: general
date: 2026-03-18
description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على الصورة لاستخراج النص من
  الصورة بسرعة. تعلم كيفية تحميل الصورة للتعرف الضوئي على الأحرف، وإنشاء محرك OCR،
  وتحسين دقة OCR باستخدام خيارات اللغة.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: ar
og_description: قم بتنفيذ التعرف الضوئي على الأحرف (OCR) على الصورة باستخدام هذا الدليل
  التفصيلي. تعلّم كيفية تحميل الصورة للتعرف الضوئي على الأحرف، وإنشاء محرك OCR، وتحسين
  دقة التعرف الضوئي على الأحرف للحصول على استخراج نص موثوق.
og_title: إجراء التعرف الضوئي على الحروف في الصورة – دليل برمجة كامل
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: تنفيذ التعرف الضوئي على الأحرف في الصورة – دليل خطوة بخطوة
url: /ar/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على الصورة – دليل برمجة كامل

هل احتجت يوماً إلى **perform OCR on image** لكنك لم تكن متأكدًا أي مكتبة تختار أو كيف تحصل على نتائج موثوقة؟ لست وحدك. في هذا الدليل سنستعرض كل ما تحتاجه **extract text from image**، من تحميل الصورة إلى تعديل خيارات اللغة حتى تتمكن من **improve OCR accuracy** في كل خطوة.

سنغطي كيفية **load image for OCR**، وكيفية **create OCR engine**، ولماذا كل إعداد مهم. في النهاية ستحصل على سكربت جاهز للتنفيذ يطبع النص المُعترف به، وستفهم “السبب” وراء كل سطر—دون اختصارات “انظر الوثائق”. هيا نبدأ.

## ما ستحتاجه

- Python 3.8+ (الكود يستخدم f‑strings وتلميحات النوع)
- الحزمة الافتراضية `ocr_lib` – تثبيت عبر `pip install ocr_lib`
- ملف صورة يحتوي على نص واضح مطبوع (مثال: `lab_report.png`)
- محرر نصوص أو بيئة تطوير (VS Code، PyCharm، أو أي شيء تفضله)

إذا كان لديك كل ذلك، ممتاز—أنت جاهز. إذا لا، احصل على بايثون من python.org وشغّل أمر الـ pip؛ الأمر لا يستغرق سوى دقيقة.

![مثال على إجراء OCR على الصورة](/images/ocr-example.png)

*نص بديل: إجراء OCR على الصورة – عينة من الإخراج تُظهر النص المستخرج.*

## الخطوة 1: إنشاء محرك OCR – كيفية **create OCR engine** في بايثون

قبل أن يحدث أي تعرف، تحتاج المكتبة إلى كائن محرك يحمل الإعدادات وحالة التشغيل. فكر في المحرك كالعقل وراء العملية.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Why this matters:** إنشاء المحرك مبكرًا يتيح لك إرفاق خيارات اللغة لاحقًا، كما أنه يخزن النماذج الداخلية مؤقتًا لتسريع الاستدعاءات اللاحقة.

## الخطوة 2: تحميل الصورة لـ OCR – الطريقة الصحيحة لـ **load image for OCR**

الآن بعد أن لدينا محركًا، يجب أن نزوده بشيء يقرأه. طريقة `setImageFromFile` تقبل مسار نظام الملفات؛ يمكن أن يكون المسار مطلقًا أو نسبيًا لدليل عمل السكربت.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Pro tip:** استخدم مسارًا مطلقًا أو `os.path.join` لتجنب مفاجآت “الملف غير موجود” عندما يُشغَّل السكربت من مجلد مختلف.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## الخطوة 3: تحسين دقة OCR – تعديل **language options** إلى **improve OCR accuracy**

OCR الجاهز يعمل، لكن المفردات المتخصصة (مثل المصطلحات المختبرية) غالبًا ما تُربكه. عبر إرفاق قاموس مخصص وقائمة حظر، تقلل الأخطاء مثل الخلط بين “0” و“O”.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Why this helps:** القاموس يخبر نموذج OCR أن “HPLC” رمز صالح، مما يمنع تفكيك الكلمة إلى حروف غير مفهومة. قائمة الحظر تجعل النموذج يتعامل مع الرموز الغامضة كضوضاء، وهذا يُـ**improves OCR accuracy** مباشرة.

## الخطوة 4: إجراء OCR على الصورة – الاستدعاء الأساسي لـ **perform OCR on image**

مع تحضير المحرك وإرفاق الصورة، حان الوقت لتعرف النص فعليًا. تُعيد هذه الخطوة كائن `OcrResult` يمكنك الاستعلام عنه للحصول على النص الخام، درجات الثقة، أو الصناديق المحيطة.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

إذا كانت الصورة غير واضحة، ستلاحظ أرقام ثقة أقل في النتيجة. هذا إشارة لمعالجة الصورة مسبقًا (مثلاً زيادة التباين) قبل إرفاقها بالمحرك.

## الخطوة 5: Extract Text from Image – سحب السلسلة النهائية

أخيرًا، نطلب من `OcrResult` تمثيله النصي. طريقة `getText()` تُعيد سلسلة نصية جاهزة للمعالجة اللاحقة (حفظها في ملف، إدخالها في قاعدة بيانات، إلخ).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Expected output:** بافتراض أن `lab_report.png` يحتوي على جدول بسيط، قد ترى شيئًا مثل:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

هذا هو الجزء المتعلق بـ **extract text from image** تم إنجازه.

## مثال كامل يعمل – جمع كل الأجزاء معًا

فيما يلي سكربت واحد يربط القطع من الأقسام السابقة. يمكنك نسخه إلى `run_ocr.py` وتشغيله عبر `python run_ocr.py`.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### قائمة التحقق السريعة

| ✅ | العنصر |
|---|------|
| ✔️ | تم إنشاء المحرك (`create OCR engine`) |
| ✔️ | تم تحميل الصورة (`load image for OCR`) |
| ✔️ | تم ضبط خيارات اللغة (`improve OCR accuracy`) |
| ✔️ | تم إجراء OCR (`perform OCR on image`) |
| ✔️ | تم استخراج النص (`extract text from image`) |

شغّل السكربت وراقب وحدة التحكم. إذا رأيت كتلة “OCR Output” بمحتويات تقريرك، فقد نجحت في **performed OCR on image**.

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | سبب حدوثها | الحل |
|-------|----------------|-----|
| **Blurry input** | نموذج OCR لا يستطيع تمييز الأحرف | معالجة مسبقة باستخدام OpenCV: `cv2.GaussianBlur` أو زيادة DPI |
| **Wrong language** | قد تكون اللغة الافتراضية مضبوطة على شيء غير الإنجليزية | استدعِ `engine.setLanguage("eng")` قبل `recognize()` |
| **Missing dictionary terms** | الكلمات المتخصصة في المجال تصبح مشوشة | أضفها عبر `setDictionary` كما هو موضح في الخطوة 3 |
| **Blacklisted characters cause

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}