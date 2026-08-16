---
category: general
date: 2026-03-18
description: كيفية استخدام OCR لاستخراج النص من الصور – دليل سريع للتعرف على النص
  من ملفات PNG وتحميل الصور لـ OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: ar
og_description: كيفية استخدام OCR لاستخراج النص من الصور – تعلم التعرف على النص من
  PNG، تحميل الصورة للـ OCR، واستخراج النص باستخدام سكريبت بايثون بسيط.
og_title: 'كيفية استخدام OCR: استخراج النص من الصور في بايثون'
tags:
- OCR
- Python
- Image Processing
title: 'كيفية استخدام OCR: استخراج النص من الصور في بايثون'
url: /ar/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR: استخراج النص من الصور في بايثون

هل تساءلت يومًا **how to use OCR** عندما يكون لديك لقطة شاشة فوضوية أو إيصال ممسوح ضوئيًا؟ لست وحدك—المطورون يحتاجون باستمرار إلى استخراج نص قابل للقراءة من الصور، خاصة ملفات PNG التي تأتي من تطبيقات الهواتف المحمولة أو التحميلات على الويب. في هذا الدرس سنستعرض مثالًا كاملًا وقابلًا للتنفيذ يوضح لك كيفية **extract text from image**، **recognize text from PNG**، وحتى **load image for OCR** باستخدام بضع أسطر فقط من بايثون.

سنغطي كل شيء من تثبيت المكتبة المناسبة إلى التعامل مع المستندات متعددة اللغات، بحيث تعرف في النهاية بالضبط *how to extract text* من أي صورة تُمرّرها إلى المحرك. لا مراجع غامضة، فقط حل واضح خطوة بخطوة يمكنك نسخه ولصقه وتشغيله.

## ما ستتعلمه

في الأقسام القليلة القادمة سنقوم بـ:

1. إعداد محرك OCR خفيف الوزن (بدون تبعيات ثقيلة).  
2. تحميل ملف صورة—تحديدًا PNG—إلى المحرك.  
3. تمكين الكشف التلقائي عن اللغة حتى يتمكن المحرك من معالجة المحتوى متعدد اللغات.  
4. تشغيل عملية التعرف وجلب نتيجة النص العادي.  
5. تعديل سير العمل لحالات الحافة مثل الملفات المفقودة أو الصيغ غير المدعومة.

إذا كنت مرتاحًا مع بايثون الأساسي، فأنت جاهز. لا تحتاج إلى خبرة سابقة في OCR، رغم أن إلقاء نظرة سريعة على توثيق المكتبة لا يضر.

---

![كيفية استخدام OCR على صورة PNG](placeholder.png "كيفية استخدام OCR على صورة PNG – دليل خطوة بخطوة")

## كيفية استخدام OCR – تحميل الصورة والتعرف على النص {#how-to-use-ocr}

### الخطوة 1: تثبيت مكتبة OCR

أولاً، تحتاج إلى حزمة بايثون توفر فئة `OcrEngine`. لغرض هذا الدرس سنستخدم الحزمة الوهمية ولكن التوضيحية **SimpleOCR**، التي يمكنك تثبيتها عبر pip:

```bash
pip install simple-ocr
```

> **Pro tip:** إذا كنت تعمل في بيئة افتراضية (موصى بها بشدة)، فعّلها قبل تشغيل أمر التثبيت. هذا يحافظ على نظافة تبعيات مشروعك.

### الخطوة 2: استيراد المحرك وإنشاء نسخة

إنشاء المحرك سهل كما استدعاء المُنشئ الخاص به. فكر في المحرك كـ “العقل” الذي سيعالج لاحقًا الصورة التي تزوده بها.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

لماذا ننشئ نسخة جديدة في كل مرة؟ العزل. يضمن محرك جديد عدم وجود حالة متبقية من تشغيل سابق تُلوث عملية التعرف الحالية، وهو أمر حاسم عندما تعالج العديد من الملفات دفعة واحدة.

### الخطوة 3: تحميل الصورة التي تريد معالجتها

الآن نقوم فعليًا **load image for OCR**. طريقة `setImageFromFile` تقبل مسارًا لأي صورة نقطية؛ سنشير إليها إلى ملف PNG يُدعى `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

إذا لم يُعثر على الملف، فإن `SimpleOCR` يُطلق استثناء واضح `FileNotFoundError`. يمكنك التقاطه لتقديم رسالة خطأ ودية:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### الخطوة 4: تمكين الكشف التلقائي عن اللغة

معظم محركات OCR الحديثة تأتي مع حزم لغات. بتمرير `"multilingual"` نخبر المحرك بفحص النص واختيار نموذج اللغة المناسب تلقائيًا. هذا مفيد بشكل خاص عندما يحتوي PNG الخاص بك على مزيج من الإنجليزية والإسبانية، على سبيل المثال.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

إذا كنت تعرف اللغة مسبقًا، يمكنك استبدال `"multilingual"` ب locale محدد مثل `"eng"` أو `"spa"` لتسريع المعالجة.

### الخطوة 5: تشغيل عملية التعرف

العمل الشاق يحدث هنا. `recognize()` يمسح الصورة، يطبق التجزئة، يشغل الشبكة العصبية، ويُنشئ مخزن نص داخليًا.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

خلف الكواليس، يقوم المحرك بـ:

- **Pre‑processing** (إزالة الميل، التحويل إلى ثنائي)  
- **Layout analysis** (اكتشاف الأعمدة، الجداول)  
- **Character classification** (باستخدام نموذج تعلم عميق)  

كل ذلك مُجرد، ولهذا تحتاج سطرًا واحدًا فقط.

### الخطوة 6: استرجاع وطباعة النص المُعترف به

أخيرًا، نسترجع كائن النتيجة ونستخرج السلسلة النصية العادية. هذا هو الجزء الذي تقوم فيه فعليًا **extract text from image**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Expected output** (مقتطع للاختصار):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

إذا كانت الصورة لا تحتوي على أحرف قابلة للتعرف، فإن `text` سيكون سلسلة فارغة. يمكنك الحماية من ذلك:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## استخراج النص من الصورة – معالجة الحالات الشائعة

### لغات متعددة في ملف واحد

عندما يخلط المستند بين لغات، عادةً ما يقوم الإعداد `"multilingual"` بالعمل الصحيح. ومع ذلك، إذا لاحظت أخطاء في التعرف، يمكنك تحديد قائمة احتياطية يدويًا:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### صيغ غير PNG

على الرغم من تركيزنا على **recognize text from PNG**، فإن `SimpleOCR` يقبل أيضًا JPEG و BMP و TIFF. فقط غيّر امتداد الملف في `setImageFromFile`. بالنسبة لمجموعات TIFF، قد تحتاج إلى اختيار صفحة محددة:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### الملفات الكبيرة واستخدام الذاكرة

إذا كنت تعالج مسحات جيجابكسل، فكر في تغيير الحجم قبل OCR:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

تغيير الحجم يقلل من ضغط الذاكرة مع الحفاظ على تفاصيل كافية للتعرف الدقيق.

### تصحيح التحميلات الفاشلة

أحيانًا تبدو الصورة جيدة للعين لكنها تالفة داخليًا. فعّل التسجيل التفصيلي لرؤية ما يراه المحرك:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## سكريبت كامل جاهز للتنفيذ

فيما يلي البرنامج الكامل الذي يجمع جميع الأجزاء معًا. انسخه في ملف اسمه `ocr_demo.py`، عدل المتغير `YOUR_DIRECTORY` placeholder، وشغّل `python ocr_demo.py`.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

تشغيل هذا السكريبت يجب أن يُظهر النسخة النصية العادية لأي شيء داخل `mixed_doc.png`. لا تتردد في استبدال الملف بأي صورة أخرى—**how to extract text** يعمل بنفس الطريقة.

---

## الخلاصة

لقد استعرضنا للتو **how to use OCR** في بايثون لاستخراج النص من ملفات **extract text from image**، مع تركيز خاص على **recognize text from PNG** والخطوات العملية لـ **load image for OCR**. المقتطف أعلاه هو حل مستقل: تثبيت الحزمة، إمدادها بملف، تمكين الكشف متعدد اللغات، تشغيل المحرك، والحصول على النتيجة.

من هنا قد:

- دمج السكريبت في خدمة ويب تقبل تحميلات المستخدمين.  
- معالجة مجموعة من ملفات PDF محوّلة إلى PNG دفعةً واحدة.  
- إضافة معالجة لاحقة (مثل تنظيف regex، التدقيق الإملائي) لتحسين الدقة.

تذكر، جودة OCR تعتمد على وضوح الصورة، حزم اللغة المناسبة، وأحيانًا قليل من المعالجة المسبقة—لذا جرب

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}