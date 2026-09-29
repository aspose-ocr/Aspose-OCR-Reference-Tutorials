---
category: general
date: 2026-01-12
description: كيفية تعيين اللغة في Aspose OCR Python واستخراج النص من الصورة باستخدام
  قاموس مخصص. دليل خطوة بخطوة للمطورين.
draft: false
keywords:
- how to set language
- extract text from image
- how to extract text
- how to add dictionary
- how to process image
language: ar
og_description: كيفية تعيين اللغة في Aspose OCR Python واستخراج النص من الصورة باستخدام
  قاموس مخصص. تعلم سير العمل الكامل في دقائق.
og_title: كيفية ضبط اللغة في Aspose OCR Python – دليل كامل
tags:
- OCR
- Python
- Aspose
- Image Processing
title: كيفية تعيين اللغة في Aspose OCR Python – دليل كامل
url: /ar/python-java/general/how-to-set-language-in-aspose-ocr-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تعيين اللغة في Aspose OCR Python – دليل كامل

هل تساءلت يومًا **كيفية تعيين اللغة** عند استخدام Aspose OCR في Python؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما لا يتعرف نموذج اللغة الإنجليزية الافتراضي على رموز المنتجات، أرقام السيريال، أو النصوص متعددة اللغات. الخبر السار هو أن الحل بسيط وقوي في آنٍ واحد. في هذا الدرس سنستعرض كيفية ضبط اللغة، إضافة قاموس مخصص، استخراج النص من صورة، وأخيرًا معالجة الصورة للحصول على أفضل نتائج OCR.

سنغطي كل ما تحتاج معرفته: من تثبيت المكتبة إلى تشغيل مثال كامل يطبع النص المستخرج. في النهاية ستتمكن من **استخراج النص من صورة** بثقة، حتى عندما يحتوي المحتوى على رموز غير عادية أو لغات مختلطة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* Python 3.8+ مثبت (الكود يستخدم f‑strings، لذا الإصدارات الأقدم لن تعمل).
* رخصة Aspose OCR for Python سارية أو مفتاح تجربة مجانية.
* حزمة `asposeocr` مثبتة عبر `pip install asposeocr`.
* صورة نموذجية (`product_label.png`) تحتوي على النص الذي تريد قراءته.

إذا كان لديك كل هذه العناصر، رائع—لننتقل إلى الخطوة التالية. إذا لم يكن كذلك، احصل على نسخة التجربة المجانية من موقع Aspose وشغّل أمر التثبيت؛ سيستغرق الأمر دقيقة واحدة فقط.

## الخطوة 1: استيراد وحدة Aspose OCR

الخطوة الأولى هي جلب فئات OCR إلى سكريبتك. هذا هو الأساس لـ **كيفية تعيين اللغة** لاحقًا.

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr
```

> **نصيحة احترافية:** ضع عمليات الاستيراد في أعلى الملف. هذا يجعل قراءة السكريبت أسهل، خاصةً عندما تعود إليه لاحقًا.

## الخطوة 2: كيفية تعيين اللغة

بشكل افتراضي، تفترض Aspose OCR أن النص إنجليزي. إذا كانت صورتك تحتوي على الفرنسية أو الألمانية أو أي لغة أخرى، عليك إخبار المحرك باللغة التي يجب استخدامها. هنا يبرز المفتاح الأساسي.

```python
# Step 2: Create an OCR engine and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # change to ocr.Language.FRENCH, etc.
```

لماذا هذا مهم؟ تعتمد محركات OCR على نماذج أحرف مخصصة للغة. توفير اللغة الصحيحة يحسن الدقة بشكل كبير—خاصةً للأحرف ذات اللكنات أو الروابط الخاصة باللغات.

> **ملاحظة:** إذا كنت بحاجة لدعم لغات متعددة في آنٍ واحد، يمكنك تمرير قائمة مثل `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

## الخطوة 3: كيفية إضافة قاموس (كلمات معرفة من قبل المستخدم)

أحيانًا يخطئ محرك OCR في قراءة رموز المنتجات مثل “AB‑1234”. يمكنك زيادة الثقة بتزويده بقاموس مخصص. هذا يجيب مباشرةً على **كيفية إضافة القاموس** في Aspose OCR.

```python
# Step 3: Supply product codes that must be recognized with higher confidence
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])
```

يتعامل المحرك مع هذه الكلمات كـ “معروفة” ويفضلها على الأحرف المتشابهة. هذا مفيد جدًا لأرقام SKU، رموز السيريال، أو أسماء العلامات التجارية التي لا تنتمي إلى لغة طبيعية.

## الخطوة 4: كيفية معالجة الصورة

بعد ضبط المحرك، تحتاج إلى تحميل الصورة التي تريد تحليلها. هذا يوضح **كيفية معالجة الصورة** بطريقة نظيفة وقابلة لإعادة الاستخدام.

```python
# Step 4: Load the image containing the product label
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")
```

إذا كنت تتعامل مع ملفات PDF، يمكنك تحويل كل صفحة إلى صورة أولاً—Aspose OCR يدعم ذلك مباشرة.

## الخطوة 5: كيفية استخراج النص من الصورة

مع إعداد كل شيء، الخطوة الأخيرة هي تشغيل OCR واسترجاع النص. هذا هو جوهر **كيفية استخراج النص** من صورة.

```python
# Step 5: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)

# Step 6: Print the extracted text
print(ocr_result.text)
```

عند تشغيل السكريبت، يجب أن ترى شيئًا مشابهًا لـ:

```
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

إذا كان الإخراج مشوشًا، تحقق مرة أخرى من أنك ضبطت اللغة الصحيحة وأن القاموس المخصص يحتوي على السلاسل الدقيقة التي تتوقعها.

## مثال عملي كامل

بجمع كل ما سبق، إليك السكريبت الكامل الذي يمكنك نسخه ولصقه في ملف باسم `extract_label.py`. تأكد من استبدال `YOUR_DIRECTORY` بالمسار الفعلي لصورتك.

```python
import asposeocr as ocr

# Create OCR engine and set language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # Change if needed

# Add custom dictionary entries
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])

# Load the target image
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")

# Perform OCR
ocr_result = ocr_engine.process(image)

# Output the result
print("=== OCR Extraction Result ===")
print(ocr_result.text)
```

### النتيجة المتوقعة

```
=== OCR Extraction Result ===
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

إذا رأيت الرموز الدقيقة التي أضفتها إلى القاموس، فقد نجحت في إتقان **كيفية تعيين اللغة**، **كيفية إضافة القاموس**، و**كيفية استخراج النص من صورة** باستخدام Aspose OCR.

## التعامل مع الحالات الشائعة

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **الصورة غير واضحة** | قم بالمعالجة المسبقة باستخدام `ocr.Image.apply_filter()` لتوضيح الصورة قبل استدعاء `process()`. |
| **عدة لغات في صورة واحدة** | اضبط `ocr_engine.language = ocr.Language.ENGLISH | ocr.Language.SPANISH`. |
| **ملفات PDF كبيرة** | كرر العملية لكل صفحة، حوّلها إلى `ocr.Image`، واستدعِ `process()` لكل صفحة. |
| **حروف غير متوقعة** | أضفها إلى قائمة الكلمات المعرفة من قبل المستخدم؛ Aspose OCR يتعامل معها كرموز ذات ثقة عالية. |

هذه النصائح تحافظ على قوة خط أنابيب OCR الخاص بك، حتى عندما لا تكون المدخلات مثالية.

## مرجع بصري

![كيفية تعيين اللغة في مثال Aspose OCR](image.png "لقطة شاشة توضح كيفية تعيين اللغة في مثال Aspose OCR Python")

*نص بديل:* **كيفية تعيين اللغة** لقطة شاشة توضح تعيين خاصية اللغة في بيئة تطوير Python.

## الخلاصة

أنت الآن تعرف **كيفية تعيين اللغة** في Aspose OCR Python، وكيفية **إضافة القاموس**، والخطوات الدقيقة **لاستخراج النص من صورة** و**معالجة الصورة** للحصول على أفضل النتائج. يمكن إدراج المثال الكامل أعلاه في أي مشروع، وتعديله للغات مختلفة، وتوسيعه لمعالجة دفعات أو إدخال ملفات PDF.

هل أنت مستعد للتحدي التالي؟ جرّب استبدال `ocr.Language.ENGLISH` بـ `ocr.Language.FRENCH` ولاحظ تحسين الدقة على الملصقات الفرنسية. أو جرب طريقة `set_user_defined_words` لتضمين كتالوج كامل من المنتجات—سيعامل محرك OCR كل إدخال كمطابقة ذات ثقة عالية.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالكريستال!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}