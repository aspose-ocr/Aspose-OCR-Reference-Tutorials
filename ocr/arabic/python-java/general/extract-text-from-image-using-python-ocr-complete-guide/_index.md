---
category: general
date: 2026-06-06
description: استخراج النص من الصورة باستخدام OCR في بايثون خلال دقائق. اكتشف OCR للصور
  متعددة اللغات، واكتشاف اللغة تلقائيًا، وكيفية استخراج نص OCR بدقة.
draft: false
keywords:
- extract text from image
- how to extract OCR text
- multilingual image OCR
- detect language OCR
- auto detect language OCR
language: ar
og_description: استخراج النص من الصورة باستخدام OCR في بايثون بسرعة. تعلم OCR للصور
  متعددة اللغات، واكتشاف اللغة تلقائيًا، وكيفية استخراج نص OCR خطوة بخطوة.
og_title: استخراج النص من الصورة باستخدام بايثون OCR – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  headline: Extract Text from Image Using Python OCR – Complete Guide
  type: TechArticle
- description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  name: Extract Text from Image Using Python OCR – Complete Guide
  steps:
  - name: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
    text: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
  - name: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
    text: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
  - name: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
    text: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Multilingual
title: استخراج النص من الصورة باستخدام بايثون OCR – دليل كامل
url: /ar/python-java/general/extract-text-from-image-using-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة باستخدام Python OCR – دليل كامل

هل احتجت يوماً إلى **استخراج النص من صورة** لكن لم تكن متأكدًا أي مكتبة يمكنها التعامل مع عدة لغات تلقائيًا؟ لست وحدك—المطورون يسألون باستمرار *كيفية استخراج نص OCR* عند التعامل مع مستندات دولية، إيصالات، أو منشورات ممسوحة. في هذا الدرس سنستعرض مثالًا عمليًا بلغة Python لا يقتصر على استخراج النص من الصورة فحسب، بل **يكشف اللغة** تلقائيًا، مما يجعل OCR للصور متعددة اللغات سهلًا للغاية.

سنغطي كل شيء بدءًا من تثبيت حزمة OCR إلى تمكين **auto detect language OCR**، تشغيل المحرك على صورة تجريبية، وأخيرًا طباعة كل من اللغة المكتشفة والسلسلة المستخرجة. بنهاية الدرس ستحصل على مقتطف يمكن إعادة استخدامه في أي مشروع، سواء كنت تبني خط أنابيب ترجمة أو خدمة استيعاب بيانات.

## إعداد البيئة لاستخراج النص من الصورة

قبل الغوص في الكود، تأكد أن جهازك يلبي المتطلبات الدنيا التالية:

- Python 3.8 أو أحدث (المكتبة تستخدم type hints التي تتجاهلها الإصدارات القديمة)
- `pip` لإدارة الحزم
- ملف صورة يحتوي على نص على الأقل بلغتين مختلفتين (مثال: الإنجليزية + الإسبانية)

ستحتاج أيضًا إلى مكتبة OCR التي تشغل هذا المثال. من أجل هذا الدليل سنستخدم الحزمة الوهمية `ocr`، التي تحاكي الأدوات الواقعية الشهيرة مثل Tesseract أو EasyOCR لكنها تقدم واجهة Python نظيفة.

```bash
# Install the OCR package and its optional image dependencies
pip install ocr[image]
```

> **نصيحة احترافية:** إذا واجهت أخطاء صلاحية، أضف `python -m` قبل الأمر أو استخدم بيئة افتراضية—هذا يحافظ على حزم الموقع العامة مرتبة.

## إنشاء كائن محرك OCR

الآن بعد أن أصبحت المكتبة جاهزة، الخطوة المنطقية الأولى هي **إنشاء كائن محرك OCR**. فكر في المحرك كماسح ذكي يمكنك ضبطه قبل تغذيته بالصور.

```python
import ocr

# Step 1: Initialize the OCR engine
engine = ocr.OcrEngine()
```

لماذا ننشئ كائن المحرك منفصلًا بدلاً من استدعاء طريقة ثابتة؟ كائن المحرك يحتفظ بحالة التكوين (مثل تفضيلات اللغة) التي قد ترغب في إعادة استخدامها عبر عدة صور، مما يوفر عليك عبء إعادة تهيئته في كل مرة.

## تمكين وضع الكشف التلقائي للغة OCR

معظم أدوات OCR تتطلب منك تحديد رمز اللغة—`eng` للإنجليزية، `spa` للإسبانية، وهكذا. التخمين اليدوي للغة يُفقدك هدف **OCR للصور متعددة اللغات**. لحسن الحظ، حزمة `ocr` تقدم وضع *auto detect language OCR* الذي يفحص الصورة ويختار نموذج اللغة الأنسب خلف الكواليس.

```python
# Step 2: Turn on automatic language detection
engine.set_recognition_language(ocr.Language.AUTO_DETECT)
```

تمكين **detect language OCR** بهذه الطريقة يعني أنك لن تحتاج إلى الحفاظ على قائمة طويلة من رموز اللغات. سيحاول المحرك مطابقة الخط الذي يراه—Latin، Cyrillic، Han، إلخ—ويحمّل النموذج المناسب تلقائيًا.

## تنفيذ OCR للصور متعددة اللغات

بعد تهيئة المحرك، حان الوقت فعليًا **لاستخراج النص من الصورة**. الطريقة `recognize_image` تستقبل مسار الملف وتعيد كائن نتيجة يحتوي على كل من النص الخام واللغة التي تم اكتشافها.

```python
# Step 3: Run OCR on a multilingual image
image_path = "YOUR_DIRECTORY/multilang_page.png"
result = engine.recognize_image(image_path)
```

إذا كنت تتساءل *كيف تستخرج نص OCR* من ملف PDF بدلًا من PNG، فإن نفس المحرك يقدم `recognize_pdf`—فقط غيّر اسم الطريقة. منطق الكشف الأساسي يبقى هو نفسه، لذا ستحصل على نفس ميزة **auto detect language OCR**.

## عرض اللغة المكتشفة والنص المستخرج

أخيرًا، نطبع ما اكتشفه المحرك. كائن النتيجة يوفّر `detected_language` (علامة BCP‑47 مثل `en` أو `es`) و`text`، الذي يحمل ناتج OCR الخام.

```python
# Step 4: Show the language and the extracted string
print(f"Detected language: {result.detected_language}")
print("Extracted text:")
print(result.text)
```

تشغيل السكريبت على صورتنا التجريبية يجب أن ينتج شيئًا مشابهًا لـ:

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

لاحظ كيف حدد المحرك الإنجليزية كلغة أساسية، لكنه لا يزال يلتقط السطر الإسباني—تمامًا ما تتوقعه من حل **OCR للصور متعددة اللغات** قوي.

### ماذا لو فشل الكشف؟

أحيانًا قد يلجأ محرك OCR إلى لغة افتراضية (عادةً الإنجليزية) إذا كانت الصورة غير واضحة أو الخط غريب جدًا. في تلك الحالات يمكنك فرض قائمة لغات:

```python
engine.set_recognition_language([ocr.Language.ENGLISH, ocr.Language.SPANISH])
```

لكن تذكر، فرض اللغات يُفقدك راحة **auto detect language OCR**، لذا استخدمه فقط عندما تكون على علم بمجموعة لغات محددة.

## الأخطاء الشائعة وكيفية استخراج نص OCR بثقة

حتى مع الكشف التلقائي، قد تواجه بعض العقبات:

1. **صور منخفضة الدقة** – تنخفض دقة OCR بشكل حاد تحت 150 dpi. قم بزيادة الدقة أو اطلب مسحًا عالي الدقة.
2. **الضوضاء وعيوب الضغط** – طبّق مرشح عتبة بسيط (`opencv` أو `Pillow`) قبل تمرير الصورة إلى المحرك.
3. **خطوط مختلطة في صفحة واحدة** – بعض المحركات تكافح مع الأحرف اللاتينية وCJK معًا. قسّم الصفحة إلى مناطق وشغّل التعرف بشكل منفصل إذا لزم الأمر.

معالجة هذه القضايا تحسّن بشكل كبير جودة عملية **استخراج النص من صورة**، خاصةً عند التعامل مع مستندات متعددة اللغات في العالم الحقيقي.

## مثال كامل جاهز للتنفيذ

فيما يلي السكريبت الكامل الجاهز للتنفيذ الذي يجمع كل الخطوات التي ناقشناها. احفظه باسم `multilingual_ocr.py` وشغّله من سطر الأوامر.

```python
import ocr

def main():
    # Initialize engine with auto language detection
    engine = ocr.OcrEngine()
    engine.set_recognition_language(ocr.Language.AUTO_DETECT)

    # Path to your multilingual image
    image_path = "YOUR_DIRECTORY/multilang_page.png"

    # Perform OCR
    result = engine.recognize_image(image_path)

    # Output results
    print(f"Detected language: {result.detected_language}")
    print("Extracted text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

**الناتج المتوقع** (مع افتراض أن الصورة التجريبية تحتوي على نص إنجليزي وإسباني):

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

لا تتردد في استبدال `multilang_page.png` بأي صورة تحتوي نصًا بلغات أخرى—بفضل **auto detect language OCR**، سيظل السكريبت يعطك علامة لغة منطقية والنص المقابل.

![مثال لاستخراج النص من صورة](https://example.com/ocr-sample.png "استخراج النص من صورة")

## الخلاصة

أنت الآن تعرف بالضبط **كيفية استخراج نص OCR** من صورة، وكيفية تمكين **auto detect language OCR**، وكيفية التعامل مع سيناريوهات **OCR للصور متعددة اللغات** بأقل قدر من الكود. بإنشاء كائن محرك OCR، وتفعيل الكشف التلقائي للغة، واستدعاء `recognize_image`، يمكنك سحب كل من معرف اللغة والنص الخام بثقة.

ما الخطوة التالية؟ جرّب تمرير السلاسل المستخرجة إلى واجهة برمجة تطبيقات ترجمة، احفظها في قاعدة بيانات قابلة للبحث، أو اجمع عدة صفحات في تقرير PDF واحد. يمكنك أيضًا تجربة محركات OCR مختلفة (Tesseract، EasyOCR، Google Vision) مع الحفاظ على نفس سير العمل عالي المستوى—بفضل واجهة **detect language OCR** المتسقة.

إذا صادفت أي شذوذ، راجع قسم “الأخطاء الشائعة” أو عدّل خطوات ما قبل معالجة الصورة. برمجة سعيدة، ولتكن مشاريعك القادمة مليئة بنصوص مكتشفة بشكل صحيح ومستخرجة بدقة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}