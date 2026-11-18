---
category: general
date: 2026-06-06
description: كيفية معالجة الصور مسبقًا للتعرف الضوئي على الأحرف (OCR) باستخدام بايثون.
  تعلم كيفية تحويل الصورة إلى ثنائية باستخدام طريقة أوتسو، وكيفية تصحيح انحراف المستندات
  الممسوحة ضوئيًا، وتحسين دقة التعرف الضوئي على النص الألماني.
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: ar
og_description: كيفية معالجة الصور مسبقًا للتعرف الضوئي على الأحرف (OCR) في بايثون.
  يوضح هذا الدرس كيفية تحويل الصورة إلى ثنائية باستخدام طريقة أوتسو، وكيفية تصحيح
  ميل المستندات الممسوحة، وكيفية تحسين دقة OCR للصور الألمانية.
og_title: كيفية معالجة الصور مسبقًا للتعرف الضوئي على الأحرف – دليل بايثون كامل
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: كيفية معالجة الصور مسبقًا للتعرف الضوئي على الأحرف – دليل بايثون الكامل
url: /ar/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية معالجة الصور قبل OCR – دليل بايثون كامل

هل تساءلت يومًا **كيف تُعالج الصور قبل OCR** لتظهر النصوص واضحة كالكريستال؟ لست وحدك. المستندات الممسوحة ضوئيًا—وخاصة الصفحات الألمانية المزعجة—يمكن أن تكون كابوسًا لأي محرك OCR. الخبر السار؟ بعض خطوات المعالجة الذكية يمكن أن تحول مسحًا ضبابيًا ومبقعًا إلى صورة نظيفة قابلة للقراءة آليًا.

في هذا الدرس سنستعرض مثالًا عمليًا يوضح **كيف تُعالج الصور قبل OCR** باستخدام بايثون. ستتعلم **تحويل الصورة إلى ثنائية باستخدام Otsu**، **كيفية تصحيح ميل المستندات الممسوحة**، وبشكل عام **كيفية تحسين دقة OCR** عندما تحتاج إلى **استخراج النص من ملفات صورة ألمانية**. لا إطالة، فقط سكريبت يعمل يمكنك نسخه ولصقه اليوم.

## ما الذي ستحتاجه

- **Python 3.9+** (أي نسخة حديثة تعمل)
- مكتبة OCR تُوفر فئة `OcrEngine` – للعرض سنفترض حزمة `ocr` عامة. ثبّتها عبر `pip install ocr-lib`.
- مسح ألماني مشوش (`noisy_german_scan.tif`) تريد اختباره.
- فهم أساسي لدوال بايثون (إذا كتبت `def` من قبل، فأنت جاهز).

> **نصيحة محترف:** إذا كنت تستخدم SDK OCR مختلف (مثال: Tesseract عبر `pytesseract`)، فإن المفاهيم تبقى نفسها—فقط عدّل أسماء الطرق.

## نظرة عامة على الحل

1. **إنشاء كائن محرك OCR.**  
2. **تعيين لغة التعرف إلى الألمانية.**  
3. **بناء خط أنابيب معالجة مخصص** يتضمن تصحيح الميل، إزالة الضوضاء، التحويل إلى ثنائي (Otsu)، وتمديد التباين.  
4. **إرفاق خط الأنابيب بالمحرك** بحيث تمر كل صورة من خلاله تلقائيًا.  
5. **تشغيل OCR** على مسح ألماني مشوش.  
6. **طباعة النص المستخرج** للتحقق من النتيجة.

فيما يلي نُفصِّل كل خطوة، نشرح **لماذا** هي مهمة، ونُظهر الشيفرة الدقيقة التي تحتاجها.

![مثال على كيفية معالجة الصور قبل OCR](image.png "مثال على كيفية معالجة الصور قبل OCR")

## الخطوة 1: إنشاء كائن محرك OCR

أولًا وقبل كل شيء—بدون محرك، لا يحدث شيء. كائن `OcrEngine` هو نقطة الدخول التي تُنسّق جميع المعالجات اللاحقة.

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*لماذا هذا مهم:* تهيئة المحرك تُعد الموارد الداخلية (مثل نماذج اللغة) وتمنحك مساحة نظيفة لإرفاق خط أنابيب مخصص لاحقًا.

## الخطوة 2: تعيين لغة التعرف إلى الألمانية

دقة OCR تعتمد بشكل كبير على اللغة. بإخبار المحرك أن يتوقع الألمانية، تُفعِّل مجموعة الأحرف والنموذج اللغوي المناسب.

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

إذا تخطيت هذه الخطوة، قد يَفترض المحرك اللغة الإنجليزية افتراضيًا، ما يؤدي إلى أخطاء في التعرف على الأحرف المُعقَّدة مثل الـä، الـö، الـü وحرف الـß—وهي مشاكل شائعة عند التعامل مع المستندات الألمانية.

## الخطوة 3: بناء خط أنابيب معالجة مخصص

هذا هو جوهر **كيفية معالجة الصور قبل OCR**. سنسلسلة أربع تحويلات:

| التحويل | ما يفعله | لماذا يساعد |
|---------|----------|--------------|
| **تصحيح الميل** | يدور الصورة لتصبح أفقية (حد أقصى 5°) | المسحات نادراً ما تكون محاذاة تمامًا؛ تصحيح الميل يزيل الانحراف الذي يربك تجزئة الأحرف. |
| **إزالة الضوضاء** | يقلل البقع العشوائية (قوة 0.7) | الضوضاء تُنشئ حواف زائفة قد يفسرها محرك OCR كأحرف. |
| **تحويل إلى ثنائي (Otsu)** | يحول إلى أبيض‑أسود باستخدام طريقة Otsu | الصورة الثنائية النظيفة تُعطي المحرك تباينًا حادًا بين النص (المقدمة) والخلفية. |
| **تمديد التباين** | يوسّع النطاق الديناميكي | يحسّن قابلية قراءة الخطوط الخفيفة، خاصة في المستندات القديمة. |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### كيفية تصحيح ميل المستندات الممسوحة

استدعاء `deskew` أعلاه هو الجواب الملموس على **كيفية تصحيح ميل المستندات الممسوحة**. داخليًا يقدّر زاوية الخط النصي السائدة عبر تحويل Hough ويُدوّر الصورة للعودة إلى الوضع الصحيح. إذا كانت مستنداتك مائلة بأكثر من 5°، زد قيمة `max_angle`، لكن احذر من ظهور تشوهات نتيجة الدوران الزائد.

### تحويل الصورة إلى ثنائية باستخدام Otsu

السطر `binarize(method="otsu")` يجيب مباشرة على الاستفسار **تحويل الصورة إلى ثنائية باستخدام Otsu**. خوارزمية Otsu تحسب عتبة تُقلل التباين داخل الفئات، وهو مثالي للمستندات ذات التوزيع الثنائي (نص داكن مقابل خلفية فاتحة).

## الخطوة 4: إرفاق خط الأنابيب بالمحرك

الآن نخبر محرك OCR بتشغيل كل صورة واردة عبر خط الأنابيب الذي بنيناه للتو.

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*لماذا هذا مهم:* بدون التسجيل، سيعالج المحرك المسح الخام متجاهلًا كل التنظيف الذي أعددناه. هذه الخطوة تضمن **كيفية تحسين دقة OCR** عبر تطبيق نفس المعالجة مسبقًا على كل صورة.

## الخطوة 5: التعرف على النص من مسح ألماني مشوش

حان الوقت لتجميع كل شيء. نمرّر للمحرك صورة ألمانية مشوشة ونتركه يقوم بالعمل الشاق.

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

إذا كنت مهتمًا بالأداء، يمكنك قياس زمن الاستدعاء:

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## الخطوة 6: إخراج النص المعترف به

أخيرًا، نطبع السلسلة المستخرجة. هذا هو الجواب المباشر على **استخراج النص من صورة ألمانية**.

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### النتيجة المتوقعة

باستخدام مسح تجريبي يحتوي على الجملة “Die schnelle braune Füchsin springt über den faulen Hund.” يجب أن ترى شيئًا مشابهًا لـ:

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

إذا ظل الإخراج يحتوي على أحرف مشوشة، ففكّر في تعديل قوة `denoise` أو زيادة `max_angle` لتصحيح الميل.

## الأخطاء الشائعة وكيفية التعامل معها

- **نموذج اللغة مفقود:** نسيان `set_recognition_language(Language.GERMAN)` غالبًا ما يؤدي إلى فقدان الأحرف المُعقَّدة. تحقق من استدعاء الدالة.  
- **إزالة ضوضاء مفرطة:** قوة أعلى من 0.9 قد تمحو الخطوط الرفيعة، خاصة في الخطوط القديمة. حافظ على 0.5‑0.7 في أغلب الحالات.  
- **صيغة ملف غير صحيحة:** بعض محركات OCR لا تتعامل مع ملفات TIFF متعددة الصفحات. إذا كان لديك مستند متعدد الصفحات، قسّمه إلى ملفات صفحة واحدة أولًا.  
- **ترتيب الخط الأنابيب:** الترتيب المعروض (تصحيح الميل → إزالة الضوضاء → تحويل إلى ثنائي → تمديد التباين) مقصود. تحويل الصورة إلى ثنائية قبل إزالة الضوضاء قد يحفظ الضوضاء؛ لذا دائمًا أزل الضوضاء أولًا.

## توسيع خط الأنابيب (ما التالي؟)

الآن بعد أن لديك أساسًا قويًا، قد ترغب في:

- **إضافة فتح مورفولوجي** لتنظيف البقع الصغيرة (`.morph_open(kernel=3)`).  
- **دمج نموذج لغوي** لتصحيح ما بعد المعالجة (`ocr_engine.apply_spellcheck()`).  
- **توازي معالجة الدفعات** للمجموعات الكبيرة باستخدام `concurrent.futures`.

كل هذه توسعات طبيعية تحافظ على فكرة **كيفية معالجة الصور قبل OCR** بينما تعزز **كيفية تحسين دقة OCR** أكثر.

## الخلاصة

لقد غطينا **كيفية معالجة الصور قبل OCR** من البداية حتى النهاية: إنشاء محرك، تعيين اللغة الألمانية، بناء خط أنابيب **يحول الصورة إلى ثنائية باستخدام Otsu**، **كيفية تصحيح ميل المستندات الممسوحة**، وأخيرًا **استخراج النص من صورة ألمانية** بثقة أعلى. باتباع الخطوات الستة أعلاه ستلاحظ قفزة ملحوظة في جودة التعرف—وداعًا للتصحيحات اليدوية المتواصلة.

جرّب السكريبت على مسحاتك الخاصة، العب بالمعاملات، ودع النتائج تتحدث عن نفسها. هل لديك أسئلة حول تعديل معين في المعالجة؟ اترك تعليقًا، وسنغوص أعمق معًا.

برمجة سعيدة، ولتكن OCR دائمًا دقيقة!

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شيفرات تعمل بالكامل وشروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}