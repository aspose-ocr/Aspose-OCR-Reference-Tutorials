---
category: general
date: 2026-07-05
description: استخراج النص من الصورة باستخدام OCR في بايثون. تعلّم كيفية التعرف على
  النص من الصورة، تحميل الصورة للـ OCR، وتعيين لغة الـ OCR في بضع أسطر فقط.
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: ar
og_description: استخراج النص من الصورة باستخدام OCR في بايثون. يوضح هذا الدليل كيفية
  التعرف على النص من الصورة، تحميل الصورة للـ OCR، إنشاء محرك OCR بأسلوب بايثون، وتحديد
  لغة الـ OCR.
og_title: استخراج النص من الصورة في بايثون – التعرف على النص بسرعة
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: استخراج النص من الصورة في بايثون – التعرف على النص بسرعة
url: /ar/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام بايثون – التعرف على النص بسرعة

هل احتجت يوماً إلى **استخراج النص من صورة** لكن لم تعرف أي مكتبة تختار؟ إذا تساءلت يوماً *كيف يمكن التعرف على النص من صورة* دون الاعتماد على أدوات خارجية، فأنت في المكان الصحيح. في هذا الدرس سننشئ محرك OCR صغير، نوجهه إلى صورة، ونستخرج النص—لا أكثر ولا أقل.

سنمرّ بكل خطوة: **إنشاء محرك OCR بايثون**، **تحديد لغة OCR**، **تحميل الصورة للـ OCR**، تشغيل التعرف بشكل غير متزامن، وأخيراً قراءة النتيجة. في النهاية ستحصل على سكريبت مستقل يمكنك إدراجه في أي مشروع، سواء كان برنامجاً لتحويل المستندات إلى نص أو شات بوت يقرأ الميمات.

## ما ستحتاجه

- Python 3.8+ (الكود يعمل على 3.10 وما بعده أيضاً)  
- حزمة `ocr` (غلاف خفيف حول Tesseract – تثبيت عبر `pip install ocr` أو أي فرع مفضل لديك)  
- ملف صورة (`.jpg`, `.png`, إلخ) يحتوي على نص قابل للقراءة  
- قليل من الصبر للجزء غير المتزامن (سريع، وعد)

## الخطوة 1: إنشاء محرك OCR – القلب لاستخراج النص

أولاً: تحتاج إلى كائن محرك يعرف كيف يتواصل مع محرك OCR الأساسي. فكر فيه كـ “العقل” الذي سيعالج الصورة لاحقاً.

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*لماذا هذا مهم*: بدون محرك لا يوجد سياق لإعدادات اللغة أو إمكانيات الـ async. فئة `OcrEngine` تُجرد استدعاءات سطر الأوامر منخفضة المستوى إلى Tesseract، وتوفر لك واجهة Python نظيفة.

## الخطوة 2: تحديد لغة OCR – أخبر المحرك بما يتوقعه

إذا كان مستندك بالإنجليزية، يمكنك ترك الإعداد الافتراضي، لكن من الأفضل تحديده صراحة. هذا يوضح أيضاً كيفية **تحديد لغة OCR** للغات أخرى.

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **نصيحة احترافية**: للملفات PDF متعددة اللغات، يمكنك تمرير قائمة مثل `[ocr.Language.ENGLISH, ocr.Language.FRENCH]`. سيحاول المحرك كلا اللغتين تلقائياً.

## الخطوة 3: تحميل الصورة للـ OCR – جلب الصورة إلى الذاكرة

الآن نقوم فعلياً **بتحميل الصورة للـ OCR**. يدعم الغلاف التحميل الكسول، لذا لا يتم قراءة الملف إلا عندما يحتاجه المحرك.

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*حالة خاصة*: إذا كانت الصورة ضخمة (أكثر من 5 ميغابايت)، فكر في تصغيرها أولاً لتسريع عملية التعرف. يمكنك فعل ذلك باستخدام Pillow:

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## الخطوة 4: بدء التعرف غير المتزامن – لا تحجب تطبيقك

تشغيل OCR قد يستغرق ثانية أو اثنتين، خاصةً مع المسحات الكبيرة. طريقة `recognize_async` تُعيد كائن Future يمكنك الاستعلام عنه لاحقاً، مما يتيح لك **أداء أعمال أخرى بينما يعمل OCR في الخلفية**.

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

لماذا الـ async؟ في خادم ويب لا تريد أن يتوقف طلب واحد كل مجموعة العاملين. كائن Future يمنحك التحكم: يمكنك `await` له في كود غير متزامن أو حظره فقط عندما تحتاج النتيجة فعلاً.

## الخطوة 5: استرجاع النتيجة – احجز الحظر فقط عند الضرورة

عندما تحتاج النص، استدعِ `future.get()`. هذا الاستدعاء **يحجز الحظر فقط هنا**، مما يعني أن باقي برنامجك يبقى مستجيباً حتى ينتهي OCR.

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

إذا كنت داخل حلقة `asyncio`، يمكنك بدلاً من ذلك `await future` – الغلاف يدعم كلا الأسلوبين.

## الخطوة 6: استخدام النص المستخرج – بياناتك جاهزة

الآن بعد أن لديك كائن `result`، استخراج السلسلة النصية بسيط. لنطبعها ونظهر أيضاً كيف يمكن كتابة النص إلى ملف.

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**الناتج المتوقع** (مقتطع للاختصار):

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

إذا لم تحتوي الصورة على نص، فإن `result.text` سيكون سلسلة فارغة—عالج هذه الحالة بلطف.

## مثال كامل يعمل – جميع الخطوات في سكريبت واحد

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه، عدل مسار `image_path`، وستكون جاهزاً.

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **ملاحظة**: استبدل `"YOUR_DIRECTORY/large_document.jpg"` بالمسار الفعلي لصورتك. يعمل السكريبت على Windows و macOS و Linux طالما تم تثبيت Tesseract وإتاحته في `PATH`.

## المشكلات الشائعة وكيفية تجنّبها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| **حروف غير مفهومة** | لغة خاطئة أو ملفات بيانات اللغة مفقودة. | تأكد من أن `engine.language` تتطابق مع النص وأن ملف `.traineddata` المقابل موجود في مجلد `tessdata` الخاص بـ Tesseract. |
| **بطء الأداء على الصور الكبيرة** | OCR يزداد تعقيداً مع عدد البكسلات. | صغّر أو قلل الدقة قبل تمرير الصورة إلى المحرك (انظر مقتطف Pillow). |
| **Future لا يكتمل أبداً** | ملف الصورة تالف أو غير قابل للقراءة. | ضع `future.get()` داخل كتلة try/except وتأكد من صحة `image.is_valid()` قبل التعرف. |
| **فقدان Unicode** |  |

## ماذا تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [تحويل الصورة إلى نص – تنفيذ OCR على صورة من URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose OCR لـ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}