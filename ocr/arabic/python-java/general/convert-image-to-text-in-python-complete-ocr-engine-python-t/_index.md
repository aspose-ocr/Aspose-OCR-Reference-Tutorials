---
category: general
date: 2026-07-05
description: تحويل الصورة إلى نص باستخدام Python OCR – مثال خطوة بخطوة يوضح كيفية
  استخراج النص من الصورة والتعرف على النص من ملف JPG.
draft: false
keywords:
- convert image to text
- extract text from image
- python ocr example
- ocr engine python
- recognize text from jpg
language: ar
og_description: حوّل الصورة إلى نص باستخدام OCR بايثون. اتبع هذا المثال لاستخراج النص
  من الصورة والتعرف على النص من ملف JPG في دقائق.
og_title: تحويل الصورة إلى نص في بايثون – دليل كامل لمحرك OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert image to text with Python OCR – a step‑by‑step python ocr example
    that shows how to extract text from image and recognize text from jpg.
  headline: Convert Image to Text in Python – Complete OCR Engine Python Tutorial
  type: TechArticle
tags:
- ocr
- python
- image-processing
- text-extraction
title: تحويل الصورة إلى نص في بايثون – دليل كامل لمحرك OCR بايثون
url: /ar/python-java/general/convert-image-to-text-in-python-complete-ocr-engine-python-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى نص في بايثون – دليل كامل لمحرك OCR في بايثون

هل احتجت يومًا إلى **convert image to text** لكنك لم تكن متأكدًا من أي مكتبة تثق بها؟ لست وحدك—العديد من المطورين يواجهون هذا التحدي عندما يحاولون استخراج الأحرف من إيصال ممسوح ضوئيًا أو صورة لعلامة. الخبر السار؟ نظام OCR في بايثون يجعل المهمة شبه خالية من المتاعب.

في هذا **python ocr example** سنستعرض سيناريو واقعي: لديك ملف JPEG يحتوي على أحرف سيريليّة، وتريد **extract text from image** بشكل موثوق. في النهاية ستعرف كيف **recognize text from jpg**، ولماذا كل خطوة مهمة، وكيفية تعديل الكود للغات أو صيغ صور أخرى.

## ما ستحتاجه

* Python 3.8+ مثبت (يفضل أحدث إصدار ثابت).
* اتصال إنترنت فعال لتثبيت حزمة OCR.
* ملف صورة (مثال، `cyrillic_sample.jpg`) يحتوي على النص الذي تريد استخراجّه.
* اختياري لكن مفيد: بيئة افتراضية للحفاظ على نظافة الاعتمادات.

لا توجد تبعيات نظام تشغيل ثقيلة، ولا أدوات بناء غامضة—فقط بضع أوامر pip وقليل من أسطر الكود.

## الخطوة 1: تثبيت حزمة محرك OCR لبايثون

أول شيء يجب عليك فعله هو الحصول على محرك OCR يعمل جيدًا مع بايثون. في هذا الدليل سنستخدم الحزمة الوهمية `ocr` لأن واجهتها تشبه العديد من المكتبات الواقعية (مثل `pytesseract` أو `easyocr`). ثبّتها باستخدام:

```bash
pip install ocr
```

> **لماذا هذه الخطوة مهمة:** تثبيت الحزمة يجلب الملفات الثنائية الأصلية وملفات بيانات اللغة التي تقوم بالعمل الفعلي. تخطيها سيتسبب في رفع `ImportError` فور محاولتك `import ocr`.

## الخطوة 2: استيراد الوحدات وإعداد البيئة

الآن بعد أن أصبحت المكتبة على جهازك، استورد الأجزاء التي تحتاجها. سنقوم أيضًا بتكوين السجلات (logging) لتتمكن من رؤية ما يفعله المحرك خلف الكواليس—مفيد عندما تقوم لاحقًا **باستخراج النص من الصورة** للملفات التي ليست نظيفة تمامًا.

```python
import ocr
import logging

# Enable debug output (optional but recommended for first runs)
logging.basicConfig(level=logging.INFO)
```

> **نصيحة احترافية:** إذا كنت تعمل داخل دفتر Jupyter، قد ترغب في ضبط `logging.getLogger().setLevel(logging.DEBUG)` لرؤية تفاصيل أكثر.

## الخطوة 3: إنشاء مثال (Instance) لمحرك OCR

إنشاء المحرك هو الأساس لأي سير عمل **ocr engine python**. فكر فيه كتشغيل الأضواء في غرفة مظلمة؛ بدون ذلك، لا يستطيع باقي الخط الأنابيب رؤية أي شيء.

```python
# Step 3: Instantiate the OCR engine
ocr_engine = ocr.OcrEngine()
```

> **لماذا هذه الخطوة حاسمة:** كائن `OcrEngine` يحمل إعدادات مثل حزم اللغات، خيارات ما قبل المعالجة، وعلامات تسريع العتاد. تعديل أي منها لاحقًا سيؤثر على جميع عمليات التعرف اللاحقة.

## الخطوة 4: اختيار اللغة المناسبة – دعم السيريليّة

إذا كنت تتعامل مع نص سيريلي (أو أي نص غير لاتيني)، تحتاج إلى إخبار المحرك أي نموذج لغة يجب تحميله. وإلا ستحصل على مخرجات مشوشة أو، والأسوأ، سلسلة فارغة.

```python
# Step 4: Set language to Cyrillic (enables Cyrillic block support)
ocr_engine.language = ocr.Language.CYRILLIC
```

> **حالة حافة:** بعض المحركات تتطلب تحميل بيانات اللغة بشكل منفصل. إذا رأيت خطأ مثل `LanguageDataNotFound`، نفّذ `ocr.download_language('CYRILLIC')` قبل تعيين اللغة.

## الخطوة 5: تحميل الصورة التي تريد **تحويل الصورة إلى نص** منها

هنا يبدأ فعلًا تطبيق عبارة **convert image to text**. يعمل محرك OCR على كائن `Image`، وليس على مسار ملف خام، لذا نحتاج أولًا إلى تغليف ملف JPEG.

```python
# Step 5: Load the image containing the text
cyrillic_image = ocr.Image.load("YOUR_DIRECTORY/cyrillic_sample.jpg")
```

> **لماذا هذا مهم:** تحميل الصورة يمنح المحرك فرصة لفحص أبعادها، عمق اللون، وDPI. هذه الخصائص تؤثر على مدى قدرة المحرك على **recognize text from jpg**.

## الخطوة 6: التعرف على النص – جوهر مثال OCR في بايثون

الآن نطلب من المحرك أخيرًا ما صُنع من أجله: تحويل البكسلات إلى أحرف. تُعيد طريقة `recognize` كائن نتيجة يحتوي على السلسلة المستخرجة، درجات الثقة، ومربعات الإحاطة.

```python
# Step 6: Run OCR and capture the result
ocr_result = ocr_engine.recognize(cyrillic_image)
```

> **ما ستحصل عليه:** `ocr_result.text` هي سلسلة بايثون عادية مع الحفاظ على فواصل الأسطر. إذا كنت تحتاج إلى مواضع على مستوى الكلمات، استكشف `ocr_result.boxes`.

## الخطوة 7: إخراج النص المتعرف عليه – تحقق من نجاح **تحويل الصورة إلى نص**

أسهل طريقة لمعرفة ما إذا كنت قد نجحت في **convert image to text** هي طباعة النتيجة. في تطبيق حقيقي ربما تكتبها إلى قاعدة بيانات أو ملف نصي بدلاً من ذلك.

```python
# Step 7: Print the extracted text
print("=== OCR OUTPUT ===")
print(ocr_result.text)
```

### النتيجة المتوقعة

بافتراض أن `cyrillic_sample.jpg` يحتوي على العبارة “Привет, мир!” سيظهر في وحدة التحكم:

```
=== OCR OUTPUT ===
Привет, мир!
```

إذا كان الإخراج فارغًا أو غير مفهوم، تحقق مرة أخرى من إعداد اللغة وجودة الصورة. الصور الضبابية أو ذات التباين المنخفض غالبًا ما تسبب نتائج سيئة في **extract text from image**.

## التعامل مع المشكلات الشائعة

| المشكلة | لماذا يحدث | الحل السريع |
|---------|------------|-------------|
| **سلسلة فارغة** | نموذج اللغة غير محمّل أو الصورة مظلمة جدًا | تأكد من أن `ocr_engine.language` يطابق النص؛ زد تباين الصورة باستخدام `ocr.Image.adjust_contrast()` |
| **حروف غير مفهومة** | لغة خاطئة أو نصوص مختلطة | عيّن `ocr_engine.language = ocr.Language.MULTI` أو نفّذ تمريرين (لاتيني ثم سيريلي) |
| **أداء بطيء على دفعات كبيرة** | المحرك يعالج الصور بشكل متسلسل | فعّل تعدد الخيوط: `ocr_engine.set_threads(4)` |
| **تسرب الذاكرة** | عدم تحرير موارد الصورة | استدعِ `cyrillic_image.close()` بعد التعرف |

> **نصيحة احترافية:** لمعالجة الدفعات، غلف حلقة التعرف داخل كتلة `try/except` لالتقاط استثناءات `ocr.EngineError` العرضية دون إيقاف المهمة بالكامل.

## توسيع المثال – من JPEG إلى PDFs، من السيريلي إلى متعدد اللغات

النمط الذي اتبعناه لـ **convert image to text** ينطبق على أي صيغة نقطية: PNG، BMP، TIFF، وحتى ملفات PDF الممسوحة (فقط استخرج الصفحة كصورة أولًا). إذا كنت بحاجة إلى **extract text from image** لملفات تحتوي على عدة لغات، يمكنك تمرير قائمة:

```python
ocr_engine.language = [ocr.Language.CYRILLIC, ocr.Language.ENGLISH]
```

وإذا كنت تتعامل مع صور عالية الدقة مأخوذة بهاتف ذكي، فكر في خطوة ما قبل المعالجة:

```python
# Denoise and binarize for better OCR accuracy
clean_image = cyrillic_image.filter(ocr.Filter.GAUSSIAN_BLUR, radius=1)
clean_image = clean_image.binarize(threshold=127)
ocr_result = ocr_engine.recognize(clean_image)
```

هذه التعديلات غالبًا ما تحول **python ocr example** متوسط إلى كود جاهز للإنتاج.

## البرنامج الكامل العامل

فيما يلي البرنامج الكامل الجاهز للتنفيذ الذي يجمع جميع الأجزاء معًا. احفظه باسم `convert_image_to_text.py` وشغّله باستخدام `python convert_image_to_text.py`.



## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [تحويل الصورة إلى نص – تنفيذ OCR على صورة من URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [كيفية استخراج النص من الصورة عن طريق إعداد المستطيلات في OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}