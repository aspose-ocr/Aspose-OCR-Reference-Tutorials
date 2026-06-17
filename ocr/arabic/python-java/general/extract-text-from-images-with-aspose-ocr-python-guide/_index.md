---
category: general
date: 2026-03-18
description: تعلم كيفية استخراج النص من الصور وتحويل نص الصور الممسوحة ضوئياً إلى
  سلاسل قابلة للتحرير باستخدام Aspose OCR في بايثون. يتضمن كودًا خطوة بخطوة.
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: ar
og_description: استخراج النص من الصور باستخدام Aspose OCR في بايثون. يوضح هذا الدرس
  كيفية تحويل نص الصور الممسوحة ضوئياً في بضع أسطر من الشيفرة فقط.
og_title: استخراج النص من الصور باستخدام Aspose OCR – دليل بايثون
tags:
- OCR
- Python
- Aspose
- Image Processing
title: استخراج النص من الصور باستخدام Aspose OCR – دليل بايثون
url: /ar/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصور باستخدام Aspose OCR – دليل بايثون

هل احتجت يومًا إلى **استخراج النص من الصور** لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—المطورون يواجهون باستمرار مشكلة تحويل ملفات PDF الممسوحة، لقطات الشاشة المشوشة، أو الإيصالات المصورة إلى سلاسل نصية قابلة للبحث والتحرير.  

الخبر السار؟ مع Aspose OCR للبايثون يمكنك **تحويل نص الصور الممسوحة** على نطاق واسع، كل ذلك دون مغادرة بيئة التطوير المتكاملة الخاصة بك. في هذا الدليل سنستعرض مثالًا كاملاً جاهزًا للتنفيذ يوضح بالضبط كيفية القيام بذلك، لماذا كل خطوة مهمة، وما الذي يجب الانتباه إليه.

## ما ستتعلمه

- إعداد مكتبة Aspose OCR في بيئة بايثون.  
- تحضير قائمة بملفات الصور (PNG، JPG، TIFF، إلخ).  
- تشغيل OCR على دفعات باستخدام استدعاء طريقة واحد.  
- الوصول إلى النص المستخرج وعرضه لكل ملف.  
- معالجة المشكلات الشائعة مثل الصيغ غير المدعومة واستخدام الذاكرة للملفات الكبيرة.  

في النهاية، ستحصل على سكريبت قابل لإعادة الاستخدام يمكنه **استخراج النص من الصور** عند الطلب—مثالي لأتمتة إدخال البيانات، فهرسة المستندات، أو تغذية خطوط أنابيب NLP اللاحقة.

---

![مثال على استخراج النص من الصور](/images/ocr-extract-text.png "استخراج النص من الصور")

*نص بديل للصورة: “استخراج النص من الصور باستخدام Aspose OCR في بايثون”*

## المتطلبات المسبقة

- Python 3.8 أو أحدث (الكود يستخدم f‑strings).  
- رخصة صالحة لـ Aspose OCR للبايثون أو مفتاح تجربة مجانية.  
- الصور التي تريد معالجتها مخزنة محليًا (أي مزيج من PNG أو JPG أو TIFF).  

إذا كان لديك بيئة افتراضية بالفعل، فهذا رائع—وإذا لم يكن كذلك، أنشئ واحدة باستخدام:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

الآن أنت جاهز لتثبيت SDK.

## الخطوة 1: تثبيت Aspose OCR SDK

Aspose توزع محرك OCR الخاص بها عبر PyPI، لذا أمر `pip` واحد يكفي:

```bash
pip install aspose-ocr
```

> **نصيحة احترافية:** قم بتثبيت نسخة محددة (مثال، `aspose-ocr==22.12`) لتجنب تغييرات غير متوقعة لاحقًا.

## الخطوة 2: استيراد فئة محرك OCR

الفئة الأساسية التي ستتعامل معها هي `OcrEngine`. استوردها في أعلى السكريبت الخاص بك:

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *لماذا هذا مهم:* استيراد ما تحتاجه فقط يحافظ على زمن بدء منخفض، خاصةً عندما تقوم لاحقًا بدمج السكريبت في تطبيق أكبر.

## الخطوة 3: تعريف ملفات الصور للمعالجة

أنشئ قائمة بايثون تحتوي على المسارات الكاملة لكل صورة تريد مسحها. استبدل `YOUR_DIRECTORY` بالمسار الفعلي للمجلد.

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **حالة حافة:** إذا كان لديك مئات الملفات، فكر في توليد هذه القائمة برمجيًا باستخدام `glob.glob('*.png')` لتجنب التعديلات اليدوية.

## الخطوة 4: تشغيل OCR على جميع الصور مرة واحدة

Aspose OCR يوفر طريقة مريحة `processMultiple` تُعيد قائمة من كائنات `OcrResult`—واحد لكل ملف مدخل.

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *لماذا المعالجة على دفعات؟* إرسال كل صورة على حدة يضيف عبءً إضافيًا (تهيئة المحرك، تحميل المكتبات الأصلية). استدعاء الدفعة يقلل من استهلاك المعالج ويسرّع المهمة ككل.

### التعامل مع الأخطاء برفق

إذا لم يتمكن البرنامج من قراءة صورة (ملف تالف، صيغة غير مدعومة)، فإن `processMultiple` سيُطلق استثناء. غلف الاستدعاء داخل كتلة `try/except` للحفاظ على استمرار السكريبت:

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## الخطوة 5: إخراج النص المستخرج لكل ملف

قم بالتكرار على النتائج، مقترنًا كل `OcrResult` باسم ملفه الأصلي. طريقة `getText()` تُعيد السلسلة المعترف بها.

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### النتيجة المتوقعة

تشغيل السكريبت الكامل على ثلاث لقطات شاشة بسيطة قد ينتج شيئًا مثل:

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

إذا احتوت صورة على لا أحرف يمكن التعرف عليها، سترى سلسلة فارغة—لا يحدث أي عطل، ويمكنك اتخاذ قرار بوضع علامة على هذا الملف للمراجعة اليدوية.

## إضافي: تحسين دقة OCR

Aspose OCR يقدم عدة إعدادات اختيارية قد ترغب في تجربتها:

| الإعداد | ما يفعله | متى يستخدم |
|---------|--------------|-------------|
| `ocr_engine.setLanguage('eng')` | يفرض نموذج اللغة الإنجليزية (يقلل الإيجابيات الكاذبة). | معظم المستندات الإنجليزية. |
| `ocr_engine.setResolution(300)` | يحسن الدقة في المسحات ذات الدقة المنخفضة (dpi). | المسحات أقل من 200 dpi. |
| `ocr_engine.setPageSegMode('single_block')` | يتعامل مع الصورة بأكملها ككتلة نص واحدة. | الإيصالات البسيطة أو بطاقات الهوية. |

يمكنك إضافة هذه الأسطر مباشرة بعد إنشاء `ocr_engine`:

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## المشكلات الشائعة وكيفية تجنبها

1. **مجموعات TIFF الكبيرة** – يمكن لملف TIFF متعدد الصفحات أن يستهلك عدة جيجابايت من الذاكرة عند تحميله بالكامل مرة واحدة. قسّم الملف إلى صور صفحة واحدة قبل تمريره إلى `processMultiple`.  
2. **الخطوط غير اللاتينية** – إذا كنت بحاجة إلى **استخراج النص من الصور** التي تحتوي على أحرف سيريالية أو عربية أو صينية، غيّر رمز اللغة وفقًا لذلك (`'rus'`, `'ara'`, `'chi_sim'`).  
3. **مسافات في مسارات الملفات** – قد تتسبب مسارات Windows التي تحتوي على مسافات في حدوث `FileNotFoundError`. غلف كل مسار بسلاسل خام (`r"C:\My Folder\image.png"`) أو استخدم `os.path.abspath`.  

معالجة هذه القضايا مسبقًا توفر عليك أخطاء تشغيلية غامضة لاحقًا.

## مثال عملي كامل

فيما يلي السكريبت الكامل الذي يمكنك نسخه‑لصقه في ملف يُسمى `batch_ocr.py`. يتضمن جميع تحسينات الممارسات الجيدة التي نوقشت أعلاه.

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

احفظه، فعّل بيئتك الافتراضية، وشغّله:

```bash
python batch_ocr.py
```

سترى السلاسل المستخرجة مطبوعة على وحدة التحكم، جاهزة لمزيد من المعالجة (مثل حفظها في قاعدة بيانات أو تغذية نموذج لغة طبيعية).

## الخلاصة

في هذا الدليل أظهرنا كيفية **استخراج النص من الصور** باستخدام Aspose OCR للبايثون، مع تغطية كل شيء من التثبيت إلى المعالجة على دفعات ومعالجة الأخطاء. السكريبت مدمج، وظيفي بالكامل، وسهل التوسيع—سواء كنت بحاجة إلى **تحويل نص الصور الممسوحة** إلى ملفات CSV، أو تغذية فهرس بحث، أو ببساطة أتمتة إدخال البيانات.

هل أنت مستعد للخطوة التالية؟ فكر في ربط خط أنابيب OCR هذا مع أداة دمج PDF لإنشاء ملفات PDF قابلة للبحث، أو ربطه بمشغل تخزين سحابي بحيث يتم معالجة كل مسح مرفوع فورًا. السماء هي الحد، وأنت الآن تمتلك أساسًا قويًا للبناء عليه.

هل لديك أسئلة أو أفكار للتحسين؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}