---
category: general
date: 2026-06-22
description: معالجة مسبقة للصورة لاستخدام OCR لاستخراج النص من الصورة وتحسين دقة OCR
  باستخدام Aspose OCR في بايثون. مثال كامل قابل للتنفيذ مشمول.
draft: false
keywords:
- preprocess image for OCR
- extract text from image
- improve OCR accuracy
language: ar
og_description: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف، استخراج النص من الصورة،
  وتحسين دقة التعرف الضوئي على الأحرف باستخدام Aspose OCR. تعلم سير العمل الكامل في
  بايثون.
og_title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف – دليل بايثون كامل
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  headline: Preprocess Image for OCR – Step‑by‑Step Python Guide
  type: TechArticle
- description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  name: Preprocess Image for OCR – Step‑by‑Step Python Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Aspose OCR’s wheels target modern interpreters. | | `aspose-ocr` package
      (`pip install aspose-ocr`) | Provides the `OcrEngine`, `ImagePreprocessor`,
      and filter classes. | | A sample image (e.g., `noisy-document.jpg`) |'
  - name: – Initialise the OCR Engine and Load Your Source Image
    text: '```python import aspose.ocr as ocr'
  - name: – Build a Preprocessing Chain to Clean the Image
    text: '```python # Initialise the preprocessor – a container for a series of filters
      preprocessor = ocr.ImagePreprocessor()'
  - name: – Attach the Preprocessor to the Engine
    text: '```python # Hook the preprocessing pipeline into the OCR engine ocr_engine.set_preprocessor(preprocessor)
      ```'
  - name: – Run OCR and Extract Text from Image
    text: '```python # Perform the recognition on the pre‑processed image recognition_result
      = ocr_engine.recognize()'
  - name: – Verify the Output and Fine‑Tune for Better Accuracy
    text: '```python # Quick sanity check: print length and a sample snippet print(f"Detected
      {len(extracted_text)} characters.") print("First 200 chars:", extracted_text[:200])
      ```'
  type: HowTo
- questions:
  - answer: Yes. Convert each page to an image (e.g., using `pdf2image`) and feed
      it through the same pipeline in a loop. The same `preprocess image for OCR`
      steps apply per page.
    question: Does this work with multi‑page PDFs?
  - answer: 'Set the language before recognition: `engine.set_language(ocr.Language.FRENCH)`.
      The preprocessing filters stay the same; only the language model changes.'
    question: What if my document is in a language other than English?
  - answer: 'Absolutely. The `ImagePreprocessor` is extensible—just call `add_filter`
      again. For heavy‑dotted backgrounds, `ocr.Filters.MedianFilter(kernel=3)` can
      be useful. --- ## Wrap‑Up We’ve just **preprocess image for OCR**, run Aspose’s
      engine, and **extract text from image** while showcasing several tric'
    question: Can I chain more filters?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف – دليل بايثون خطوة بخطوة
url: /ar/python-java/general/preprocess-image-for-ocr-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة الصورة للتعرف الضوئي على الأحرف – دليل بايثون كامل

إذا كنت بحاجة إلى **معالجة الصورة للتعرف الضوئي على الأحرف**، فمن المحتمل أنك صادفت مسحات ضوضائية، صفحات مائلة، أو صور منخفضة التباين لا تتعاون. هل حاولت استخراج النص من صورة لتجد أنه مشوش؟ هنا يأتي دور سلسلة معالجة مسبقة قوية يمكنها أن تُحدث الفارق بين بضع كلمات قابلة للقراءة وكابوس كامل في النسخ.

في هذا الدليل سنستعرض مثالًا كاملاً من البداية إلى النهاية **يستخرج النص من الصورة** مع إظهار كيفية **تحسين دقة التعرف الضوئي على الأحرف** باستخدام Aspose OCR للبايثون. لا مراجع غامضة—فقط الكود الذي يمكنك نسخه‑لصقه، والتفسير وراء كل سطر، ونصائح لحالات الاستخدام الواقعية.

## ما ستحصل عليه

- سكريبت بايثون جاهز للتنفيذ يحمل مستندًا ضوضائيًا، ينظفه، ويطبع النص المُعترف به.  
- فهم لماذا كل مرشح معالجة مسبقة مهم وكيفية ضبط معاييره.  
- استراتيجيات للتعامل مع المشكلات الشائعة مثل الضوضاء المتناثرة الكثيفة، الدوران الشديد، أو المسحات منخفضة التباين.  

### المتطلبات

| المتطلبات | لماذا يهم |
|-------------|----------------|
| Python 3.8+ | حزم Aspose OCR تستهدف مفسرات حديثة. |
| `aspose-ocr` package (`pip install aspose-ocr`) | توفر `OcrEngine`، `ImagePreprocessor`، وفئات الفلاتر. |
| A sample image (e.g., `noisy-document.jpg`) | صورة نموذجية (مثال: `noisy-document.jpg`) سنستخدم صورة فوضوية عمدًا لتوضيح الفوائد من المعالجة المسبقة. |
| Basic familiarity with Python functions | إلمام أساسي بدوال بايثون يساعدك على تعديل السكريبت ليتناسب مع خط أنابيبك الخاص. |

> **نصيحة محترف:** إذا كنت تستخدم Windows، شغّل السكريبت داخل بيئة افتراضية لتجنب تعارض الإصدارات.

---

## معالجة الصورة للتعرف الضوئي على الأحرف باستخدام Aspose OCR (Python)

فيما يلي جوهر الدليل—تحليل خطوة‑بخطوة للكود الذي ستحتاجه. يشرح كل قسم **ماذا** نفعل *و* **لماذا** نفعل ذلك، حتى تتمكن من تعديل السلسلة لاحقًا دون تخمين.

![preprocess image for OCR](ocr-preprocess.png){alt="معالجة الصورة للتعرف الضوئي على الأحرف"}

### الخطوة 1 – تهيئة محرك OCR وتحميل صورة المصدر

```python
import aspose.ocr as ocr

# Create the OCR engine – the central object that drives recognition
ocr_engine = ocr.OcrEngine()

# Load the raw image file. Using ImageStream lets Aspose handle various formats.
ocr_engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))
```

- **لماذا** `OcrEngine`؟ إنه يضمّ المُعرّف، إعدادات اللغة، (لاحقًا) المعالج المسبق.  
- **لماذا** `ImageStream.from_file`؟ ي abstracts away handling نوع الملف، بحيث يمكنك استبدال JPEG بـ PNG دون تعديل الكود.

### الخطوة 2 – بناء سلسلة معالجة مسبقة لتنظيف الصورة

```python
# Initialise the preprocessor – a container for a series of filters
preprocessor = ocr.ImagePreprocessor()

# 1️⃣ Deskew – corrects any rotation so text lines become horizontal.
preprocessor.add_filter(ocr.Filters.Deskew())

# 2️⃣ Despeckle – removes isolated noise pixels; strength=2 is a good middle ground.
preprocessor.add_filter(ocr.Filters.Despeckle(strength=2))

# 3️⃣ ContrastBoost – lifts faint characters; level=1.5 amplifies contrast without blowing out highlights.
preprocessor.add_filter(ocr.Filters.ContrastBoost(level=1.5))
```

**كيف تُحسّن هذه الفلاتر دقة OCR:**  
- **Deskew** يزيل مشكلة “الصفحة المائلة” التي تُربك تجزئة الأحرف.  
- **Despeckle** يستهدف البقع الناتجة عن الماسحات منخفضة الجودة؛ كلما زادت القوة زاد إزالة الضوضاء لكن قد تُفقد التفاصيل الدقيقة.  
- **ContrastBoost** يجعل النص الداكن يبرز أمام الخلفية الفاتحة، وهو فوز كلاسيكي لمعظم محركات OCR.

> **حالة خاصة:** إذا كان مستندك مستقيمًا تمامًا، يمكنك تخطي `Deskew()` لتوفير بضع مليثانية.

### الخطوة 3 – ربط المعالج المسبق بالمحرك

```python
# Hook the preprocessing pipeline into the OCR engine
ocr_engine.set_preprocessor(preprocessor)
```

الآن في كل مرة تُستدعى فيها `ocr_engine.recognize()`، سيُطبق أولًا الفلاتر الثلاثة بالترتيب المحدد. الترتيب مهم: تريد **إزالة الميل قبل إزالة البقع**، وإلا قد يفسّر مرشح البقع الحواف المائلة كضوضاء.

### الخطوة 4 – تشغيل OCR واستخراج النص من الصورة

```python
# Perform the recognition on the pre‑processed image
recognition_result = ocr_engine.recognize()

# Pull out the plain text string
extracted_text = recognition_result.get_text()
print(extracted_text)
```

- استدعاء `recognize()` يُعيد كائن `RecognitionResult` يحتوي ليس فقط على النص الخام بل أيضًا على درجات الثقة، الصناديق المحيطة، وتفاصيل اللغة.  
- هنا نحتاج فقط إلى السلسلة النصية البسيطة، لكن يمكنك استكشاف `recognition_result.get_confidence()` للحصول على فحص سريع لـ **تحسين دقة OCR**.

### الخطوة 5 – التحقق من الناتج وضبط الإعدادات لمزيد من الدقة

```python
# Quick sanity check: print length and a sample snippet
print(f"Detected {len(extracted_text)} characters.")
print("First 200 chars:", extracted_text[:200])
```

إذا ظل الناتج يحتوي على رموز مشوشة، فكر في التعديلات التالية:

| المشكلة | الإصلاح المقترح |
|-------|----------------|
| النص ما زال غير واضح | زيادة `ContrastBoost(level)` إلى 2.0 أو إضافة `ocr.Filters.GaussianBlur(radius=1)` قبل إزالة البقع. |
| الكثير من الأحرف العشوائية | رفع `Despeckle(strength)` إلى 3، أو إدراج `ocr.Filters.RemoveLines()` لإزالة الخطوط الأفقية. |
| الانحراف لا يزال موجودًا | استدعاء `ocr.Filters.Deskew(max_angle=5)` لتقييد التصحيح إلى دورانات خفيفة. |

---

## سكريبت كامل قابل للتنفيذ

انسخ الكتلة أدناه إلى ملف باسم `ocr_preprocess.py`. استبدل `YOUR_DIRECTORY/noisy-document.jpg` بالمسار الفعلي لصورتك، ثم شغّل `python ocr_preprocess.py`.

```python
import aspose.ocr as ocr

def main():
    # Initialise engine and load image
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))

    # Build preprocessing pipeline
    preproc = ocr.ImagePreprocessor()
    preproc.add_filter(ocr.Filters.Deskew())
    preproc.add_filter(ocr.Filters.Despeckle(strength=2))
    preproc.add_filter(ocr.Filters.ContrastBoost(level=1.5))

    # Attach pipeline
    engine.set_preprocessor(preproc)

    # Recognise and extract text
    result = engine.recognize()
    text = result.get_text()

    # Display results
    print("\n--- OCR Output ---")
    print(text)
    print("\n--- Summary ---")
    print(f"Characters detected: {len(text)}")
    print("Snippet:", text[:200].replace("\n", " "))

if __name__ == "__main__":
    main()
```

تشغيل هذا السكريبت على صورة JPEG ضوضائية ومائلة قليلًا يجب أن ينتج نصًا نظيفًا وقابلًا للقراءة—مُظهرًا كيف أن سلسلة معالجة مسبقة مصممة جيدًا **تحسّن دقة OCR** بشكل كبير.

---

## أسئلة شائعة وإجابات

**س: هل يعمل هذا مع ملفات PDF متعددة الصفحات؟**  
ج: نعم. حوّل كل صفحة إلى صورة (مثال باستخدام `pdf2image`) ومرّرها عبر نفس السلسلة داخل حلقة. تُطبق نفس خطوات **معالجة الصورة للتعرف الضوئي على الأحرف** على كل صفحة.

**س: ماذا لو كان مستندي بلغة غير الإنجليزية؟**  
ج: عيّن اللغة قبل التعرف: `engine.set_language(ocr.Language.FRENCH)`. تبقى فلاتر المعالجة المسبقة كما هي؛ يتغير فقط نموذج اللغة.

**س: هل يمكنني ربط فلاتر إضافية؟**  
ج: بالتأكيد. `ImagePreprocessor` قابل للتوسيع—فقط استدعِ `add_filter` مرة أخرى. للخلفيات ذات النقاط الكثيفة، قد يكون `ocr.Filters.MedianFilter(kernel=3)` مفيدًا.

---

## الخلاصة

لقد قمنا الآن **بمعالجة الصورة للتعرف الضوئي على الأحرف**، تشغيل محرك Aspose، و**استخراج النص من الصورة** مع عرض عدة حيل لـ **تحسين دقة OCR**. المثال الكامل جاهز للإدماج في أي مشروع، وتصميم الفلاتر المعياري يعني أنه يمكنك استبدال، إضافة، أو حذف الخطوات حسب احتياجات بياناتك.

التالي، قد ترغب في استكشاف:

- **معالجة دفعات** لعدة مسحات باستخدام `concurrent.futures`.  
- **معالجة ما بعد** باستخدام مكتبات تدقيق إملائي (مثل `pyspellchecker`) لتنظيف الأخطاء التي يُدخلها OCR.  
- **دمج** السكريبت في خدمة ويب باستخدام Flask أو FastAPI، لتحويله إلى مايكرو‑خدمة OCR عند الطلب.

جرّبه، عدّل قوّة الفلاتر، وشاهد معدلات التعرف ترتفع. إذا واجهت أي مشكلة، اترك تعليقًا—برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية استخدام AspOCR: فلاتر معالجة الصورة للتعرف الضوئي على الأحرف لـ .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [استخراج النص من الصورة – تحسين التعرف الضوئي على الأحرف باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}