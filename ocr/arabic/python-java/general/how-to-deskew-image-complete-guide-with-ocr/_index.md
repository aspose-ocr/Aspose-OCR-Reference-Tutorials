---
category: general
date: 2026-03-26
description: تعلم كيفية تصحيح انحراف الصورة، والتعرف على النص من الصورة، وبناء خط
  أنابيب لمعالجة الصور لإزالة الضوضاء من المسح الضوئي وتحويل الصورة الممسوحة إلى نص.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: ar
og_description: كيفية تصحيح انحراف الصورة وتحويل المسح المائل إلى نص قابل للبحث. اتبع
  هذا الدليل للتعرف على النص من الصورة، وإزالة الضوضاء من المسح، وتحويل الصورة الممسوحة
  إلى نص.
og_title: كيفية تصحيح إمالة الصورة – دليل OCR خطوة بخطوة
tags:
- OCR
- image-processing
- Python
title: كيفية تصحيح ميل الصورة – دليل كامل مع OCR
url: /ar/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تُصحّح انحراف الصورة – دليل كامل مع OCR

هل تساءلت يومًا **كيف تُصحّح انحراف الصورة** التي خرجت من ماسح ضوئي رخيص؟ لست وحدك. الصفحة المائلة تبدو غير احترافية، والأهم من ذلك أن الميل يمكن أن يربك أي محرك OCR يحاول **التعرف على النص من الصورة**.  

في هذا الدرس سنستعرض خط أنابيب **معالجة الصور** الكامل الذي يُصحّح الانحراف، ويُحوّل الصورة إلى ثنائية، ويزيل الضوضاء، ثم يُسلمها إلى محرك OCR حتى تتمكن من **تحويل الصورة الممسوحة إلى نص** بأقل جهد. لا سحر، مجرد بايثون عادي ومكتبة صغيرة تقوم بالعمل الشاق.

## ما ستحتاجه

- Python 3.9+ (الكود يعمل على 3.10 وما فوق)
- حزمة `ocr` (تثبيت عبر `pip install ocr‑toolkit` – استبدلها باسم المكتبة الفعلي لديك)
- صورة JPEG أو PNG ممسوحة تظهر فيها انحراف واضح (مثال: `skewed_scan.jpg`)
- قليل من الفضول حول سبب أهمية كل خطوة من خطوات المعالجة المسبقة

هذا كل شيء. لا توجد تبعيات ثقيلة مثل OpenCV إلا إذا أردت الغوص أعمق لاحقًا.

## الخطوة 1: تحميل الصورة الممسوحة

أول شيء هو جلب الملف إلى الذاكرة. هذه الخطوة بسيطة لكنها حاسمة—إذا كان المسار خاطئًا، سيتعطل كل شيء.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **لماذا؟**  
> تحميل الصورة يمنحنا كائنًا يمكن التلاعب به بحيث يستطيع `ocr.ImagePreprocessor` العمل معه. تخطي هذه الخطوة سيجعل خط الأنابيب غير قادر على الوصول إلى بيانات البكسل الفعلية.

## كيف تُصحّح انحراف الصورة وتجهّزها لـ OCR

الآن بعد أن لدينا الصورة، لنُعيدها إلى وضعها المستقيم. طريقة `deskew()` تُقدّر زاوية الميل وتدوّر الصورة لتصبح أفقية مرة أخرى.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **نصيحة احترافية:** إذا كانت مسحاتك انحرفت قليلًا فقط (≤ 3°)، فإن الخوارزمية الافتراضية عادةً ما تكون دقيقة. للزوايا الشديدة قد تحتاج إلى تعديل المعاملات الداخلية—تحقق من وثائق المكتبة للمتغيّر `max_angle`.

## تحويل الصورة إلى ثنائية – اجعلها أبيض‑أسود

محركات OCR تحب المدخلات ذات التباين العالي. تحويل الصورة إلى تمثيل ثنائي (أبيض‑أسود) يزيل الظلال الدقيقة التي قد تُربك التعرف على الأحرف.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **ما الذي يحدث؟**  
> البكسلات التي قيمتها أعلى من 128 تصبح بيضاء؛ كل ما هو أقل يتحول إلى أسود. عدّل العتبة إذا كانت مسحتك غامقة أو فاتحة بشكل غير عادي.

## إزالة الضوضاء من المسح قبل OCR

حتى الصورة المستقيمة تمامًا قد تحتوي على بقع، غبار، أو تشوهات ضغط. تلك البقع الصغيرة هي عدو أي محرك OCR.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **لماذا نزيل الضوضاء؟**  
> الضوضاء تُنشئ حوافًا زائفة قد يفسرها محرك OCR كحروف. نصف قطر صغير يناسب معظم المسحات؛ زد القيمة للمستندات ذات الضوضاء الشديدة.

## تطبيق خط أنابيب معالجة الصورة

تم ضبط جميع الإعدادات—الآن نشغّل الخط على الصورة الأصلية.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **النتيجة:** `processed_image` هي صورة نقطية (bitmap) مُنظّفة، مستقيمة، وعالية التباين جاهزة لاستخراج النص.

## التعرف على النص من الصورة باستخدام محرك OCR

حان الوقت لقراءة النص فعليًا. نُهيئ محرك OCR، نمرّر له صورتنا المُعالجة، ونطلب السلسلة النصية الخام.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **الناتج المتوقع** (مثال):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

إذا رأيت أحرفًا مشوشة، تحقق من خطوة تصحيح الانحراف أو جرّب قيمة `threshold` مختلفة.

## بناء خط أنابيب معالجة الصورة – السكريبت الكامل

بجمع كل شيء معًا، إليك سكريبت واحد قابل للتنفيذ يمكنك وضعه في ملف `.py` وتشغيله:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **نصيحة:** غلف كل العملية داخل دالة (`def ocr_from_file(path): …`) إذا كنت تخطط لمعالجة ملفات متعددة دفعة واحدة.

## أسئلة شائعة وحالات خاصة

- **ماذا لو كانت الصورة بالفعل في الوضع الصحيح؟**  
  طريقة `deskew()` تكتشف زاوية قريبة من الصفر وتترك الصورة كما هي، لذا يمكنك تشغيلها بأمان على كل ملف.

- **مسحتي ملونة—هل يجب أن أبقيها ملونة؟**  
  اللون لا يضيف قيمة لمعظم مهام OCR. التحويل إلى ثنائي يزيل اللون، يسرّع المعالجة، ويقلل استهلاك الذاكرة.

- **هل يمكن ربط عدة خطوات معالجة؟**  
  بالتأكيد. فئة `ImagePreprocessor` صُممت لتعمل كخط أنابيب؛ يمكنك إضافة `sharpen()`, `contrast_enhance()` أو فلاتر مخصصة قبل استدعاء `apply()`.

- **مخرجات OCR تحتوي على فواصل أسطر غير مرغوبة—كيف أصلح ذلك؟**  
  عالج السلسلة بعد ذلك باستخدام `text.replace("\n", " ").strip()` أو استخدم مكتبة تحليل تخطيط أكثر تقدمًا مثل أوضاع `--psm` في Tesseract.

## الخطوات التالية

الآن بعد أن عرفت **كيف تُصحّح انحراف الصورة** ولديك خط أنابيب **معالجة الصور** قوي، يمكنك استكشاف:

- دمج **التعرف على النص من الصورة** في واجهة Flask API لتحميل المستندات مباشرة.
- استخدام الخط لمعالجة **إزالة الضوضاء من المسح** للوثائق التاريخية حيث تكون الحفظ أمرًا أساسيًا.
- توسيع العملية لمعالجة آلاف الصفحات دفعة واحدة وإنتاج PDF قابل للبحث باستخدام `pdfminer` أو `PyMuPDF`.

لا تتردد في تجربة عتبات مختلفة، نصف قطر إزالة الضوضاء، أو حتى استبدال محرك OCR بـ Tesseract إذا كنت تحتاج دعمًا متعدد اللغات. الأساسيات تبقى نفسها: استقيم، نظّف، ثم اقرأ.

---

*برمجة سعيدة! إذا واجهت أي مشكلة، اترك تعليقًا أدناه—سأكون سعيدًا بمساعدتك على تحسين الخط.*  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}