---
category: general
date: 2026-09-13
description: دليل دمج نموذج OCR من Hugging Face يوضح كيفية تكوين OCR، إضافة تدقيق
  إملائي للـ OCR، وتحسين الموارد في بايثون.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- hugging face ocr model
- how to configure ocr
- spell check ocr
language: ar
lastmod: 2026-09-13
og_description: 'شرح إعداد نموذج OCR من Hugging Face: تعلم كيفية تكوين OCR، وتمكين
  تدقيق الإملاء في OCR، وإدارة الموارد باستخدام Aspose AI في بايثون.'
og_image_alt: Diagram of Hugging Face OCR model configuration with Aspose AI
og_title: نموذج OCR من Hugging Face مع Aspose AI – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Hugging Face OCR model integration guide shows how to configure OCR,
    add spell check OCR, and optimize resources in Python.
  headline: 'Hugging Face OCR model: configure Aspose AI for Python'
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI
title: 'نموذج OCR من Hugging Face: تكوين Aspose AI للبايثون'
url: /ar/python/general/hugging-face-ocr-model-configure-aspose-ai-for-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نموذج OCR من Hugging Face: إعداد Aspose AI للـ Python

إذا كنت بحاجة إلى العمل مع نموذج OCR من Hugging Face في مشروع Python، يوضح لك هذا الدليل كيفية إعداد OCR، وإرفاق معالج ما بعد المعالجة لتصحيح الأخطاء الإملائية، وإطلاق الموارد بشكل نظيف. ستشاهد مثالًا كاملاً وقابلًا للتنفيذ يدمج مساعد Aspose AI مع محرك OCR.

يغطي الدليل أيضًا الأخطاء الشائعة مثل فقدان ملفات النموذج، اختيار طبقة الـ GPU، وضمان تشغيل معالج ما بعد المعالجة بكفاءة. بنهاية المقال يمكنك تشغيل OCR على صورة، تحسين النص المستخرج باستخدام تصحيح إملائي مدفوع بالذكاء الاصطناعي، وتحرير النموذج عند انتهاء المهمة.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* Python 3.8 أو أحدث مثبت.
* رخصة Aspose OCR (أو مفتاح تجريبي) وحزمة `aspose-ocr` مثبتة عبر `pip install aspose-ocr`.
* اتصال بالإنترنت لتنزيل النموذج من Hugging Face (اختياري).
* بطاقة GPU تدعم CUDA إذا كنت تخطط لتشغيل الطبقات على الـ GPU (اختياري).

لا تحتاج إلى أي مكتبات إضافية لخطوة تصحيح الإملاء لأن النموذج اللغوي الكبير (LLM) المقدم من Hugging Face يقوم بذلك داخليًا.

## الخطوة 1: تثبيت واستيراد الفئات المطلوبة

أولاً قم بتثبيت الـ SDK ثم استورد الفئات التي تدير مساعد AI وتكوين النموذج.

```bash
pip install aspose-ocr
```

```python
# Step 1: Import the Aspose OCR classes
from aspose.ocr import AsposeAI, AsposeAIModelConfig
```

فئة `AsposeAI` تغلف نموذج لغة كبير (LLM) وتوفر أدوات مثل ما بعد المعالجة وإدارة الموارد. كائن `AsposeAIModelConfig` يتيح لك التحكم في مكان تخزين النموذج، ما إذا كان سيُحمَّل تلقائيًا، وعدد الطبقات التي تُشغل على الـ GPU.

## الخطوة 2: تهيئة محرك OCR ومساعد AI

أنشئ نسخة من محرك OCR الذي سيقرأ الصور، ثم أنشئ مساعد AI. يمكنك تمرير مسجل (logger) إلى `AsposeAI` للحصول على تشخيصات مفصلة، لكن المُنشئ الافتراضي يعمل في معظم السيناريوهات.

```python
# Step 2: Initialise the OCR engine (replace with your preferred engine)
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine()          # assumes a default configuration

# Initialise the AI helper – optional logger can be supplied
ai_helper = AsposeAI()            # or AsposeAI(logging=my_logger)
```

محرك OCR ينتج كائن نتيجة يحتوي على `plain_text`. سيتولى مساعد AI تحسين هذا النص لاحقًا.

## الخطوة 3: كيفية تكوين تنزيل نموذج OCR واستخدام الـ GPU

الآن عرّف تكوينًا يشير إلى دليل تخزين مخصص، يفرض التحميل التلقائي للنموذج، يحدد مستودع Hugging Face معين، ويقرر عدد طبقات الـ transformer التي تُشغل على الـ GPU.

```python
# Step 3: Configure model download, cache location, and GPU usage
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # download if missing
    directory_model_path="YOUR_DIRECTORY/models",   # custom cache location
    hugging_face_repo_id="openai/gpt2",             # specific Hugging Face model
    gpu_layers=20                                   # number of layers on GPU
)

# Apply the configuration – the property assignment triggers internal setup
ai_helper.model_config = model_cfg
```

**لماذا هذا مهم:**  
* `allow_auto_download` يمنع الأخطاء أثناء التشغيل عندما لا يكون ملف النموذج موجودًا محليًا.  
* `directory_model_path` يتيح لك الاحتفاظ بملفات النموذج جنبًا إلى جنب مع مشروعك، وهو مفيد للبُنى القابلة لإعادة الإنتاج.  
* `gpu_layers` يوازن بين السرعة والذاكرة؛ ضبط قيمة أقل من إجمالي عدد الطبقات يبقي البقية على الـ CPU، مما يجنب تعطل الذاكرة.

> **نصيحة احترافية:** إذا كانت بطاقة الـ GPU لديك أقل من 8 GB من الذاكرة، ابدأ بـ `gpu_layers=4` وزد القيمة تدريجيًا مع مراقبة استهلاك الذاكرة.

## الخطوة 4: إضافة معالج ما بعد معالجة OCR لتصحيح الإملاء

متطلب شائع هو تصحيح الأخطاء الإملائية التي يولدها OCR. يمكنك تسجيل معالج ما بعد معالجة مخصص يستقبل النص الخام ويعيد نسخة مصححة. طريقة `run_postprocessor` في المساعد تستخدم داخليًا الـ LLM المحمَّل لأداء تصحيح الإملاء.

```python
# Step 4: Register a custom post‑processor that refines OCR text
def postprocess_text(text, settings=None):
    # The LLM corrects spelling and punctuation
    corrected = ai_helper.run_postprocessor(text)
    return corrected

# Attach the post‑processor to the AI helper
ai_helper.set_post_processor(postprocess_text, custom_settings=None)
```

**لماذا يعمل ذلك:**  
طريقة `run_postprocessor` تستفيد من نفس الـ LLM الذي يُشغِّل نموذج OCR من Hugging Face، لذا تحصل على تصحيحات واعية للسياق بدلاً من مجرد بحث في القاموس. هذا النهج يلبي متطلب *تصحيح إملائي لـ OCR* دون إضافة مكتبات تصحيح إملائي من طرف ثالث.

## الخطوة 5: تشغيل OCR وتحسين النتيجة باستخدام وحدة AI

مع جاهزية المحرك ومساعد AI، يمكنك التعرف على صورة ثم تمرير النص المستخرج عبر معالج ما بعد معالجة تصحيح الإملاء.

```python
# Step 5: Run OCR on an image and enhance the plain‑text result
ocr_result = ocr_engine.recognize("YOUR_DIRECTORY/sample_image.png")
enhanced_text = ai_helper.run_postprocessor(ocr_result.plain_text)

print("Original:", ocr_result.plain_text)
print("Enhanced:", enhanced_text)
```

**الناتج المتوقع**

```
Original: Ths is a smple txt with som errrs.
Enhanced: This is a simple text with some errors.
```

يوضح الناتج أن نموذج OCR من Hugging Face يلتقط معظم الأحرف، بينما تصحيح الإملاء المدفوع بالذكاء الاصطناعي يُصحح الأخطاء المتبقية.

### أسئلة شائعة

* **ماذا لو فشل تنزيل النموذج؟**  
  تحقق من أن شبكتك تسمح بحركة مرور HTTPS الصادرة إلى `huggingface.co`. يمكنك أيضًا تنزيل النموذج يدويًا ووضعه في `directory_model_path`.

* **هل يمكنني استخدام مستودع Hugging Face مختلف؟**  
  نعم. استبدل `hugging_face_repo_id` بأي معرف نموذج يدعم توليد النص، مثل `facebook/opt-2.7b`. تأكد من أن رخصة النموذج تسمح بالاستخدام التجاري.

* **هل دعم الـ GPU إلزامي؟**  
  لا. ضبط `gpu_layers=0` يشغِّل النموذج بالكامل على الـ CPU، وهو أبطأ لكنه يعمل على أي جهاز.

## الخطوة 6: تحرير موارد النموذج عند الانتهاء

بعد معالجة جميع الصور، حرّر ذاكرة الـ GPU واحذف الملفات المؤقتة. هذه الخطوة أساسية للخدمات طويلة الأمد التي تُحمِّل نماذج متعددة.

```python
# Step 6: Release model resources when done
ai_helper.free_resources()
```

استدعاء `free_resources` يفرغ أوزان الـ transformer من ذاكرة الـ GPU ويُنظّف الذاكرة المؤقتة إذا قمت بتحديد دليل مؤقت.

## مثال كامل يعمل

جمع كل الأجزاء معًا ينتج سكريبت يمكنك تشغيله فورًا بعد تثبيت الـ SDK.

```python
from aspose.ocr import AsposeAI, AsposeAIModelConfig, OcrEngine

# Initialise OCR engine
ocr_engine = OcrEngine()

# Initialise AI helper
ai_helper = AsposeAI()

# Configure the Hugging Face OCR model
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="models",
    hugging_face_repo_id="openai/gpt2",
    gpu_layers=20
)
ai_helper.model_config = model_cfg

# Register spell‑check post‑processor
def postprocess_text(text, settings=None):
    return ai_helper.run_postprocessor(text)

ai_helper.set_post_processor(postprocess_text)

# Recognise image and enhance text
ocr_result = ocr_engine.recognize("sample_image.png")
enhanced_text = ai_helper.run_postprocessor(ocr_result.plain_text)

print("Original:", ocr_result.plain_text)
print("Enhanced:", enhanced_text)

# Clean up
ai_helper.free_resources()
```

احفظ السكريبت باسم `ocr_with_spellcheck.py` ونفّذه باستخدام `python ocr_with_spellcheck.py`. إذا تم إعداد كل شيء بشكل صحيح، ستظهر مخرجات OCR الأصلية تليها النسخة المصححة.

## الخلاصة

أصبح لديك الآن حل كامل لدمج نموذج OCR من Hugging Face مع Aspose AI في Python، مع تكوين تنزيل النموذج واستخدام الـ GPU، وإضافة معالج ما بعد معالجة لتصحيح الإملاء. يوضح المثال كيفية تشغيل OCR، تحسين الدقة، وتنظيف الموارد—كل ذلك داخل سكريبت واحد مستقل.

من هنا يمكنك استكشاف تحسينات إضافية مثل:

* **المعالجة الدفعية** – تكرار عبر مجلد من الصور وكتابة النتائج إلى ملف CSV.  
* **معالجة ما بعد مخصصة** – إضافة قواعد خاصة بلغة معينة أو دمج معجم متخصص.  
* **تحسين الأداء** – تجربة قيم `gpu_layers` مختلفة أو الانتقال إلى نموذج transformer أكبر للحصول على دقة أعلى.

لا تتردد في تعديل الكود ليناسب سير عملك، ومشاركة أي تحسينات تكتشفها في قسم التعليقات أدناه. برمجة سعيدة!

## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Correct OCR Results with Aspose OCR and Hugging Face – Step‑by‑Step](/ocr/english/python/general/how-to-correct-ocr-results-with-aspose-ocr-and-hugging-face/)
- [Cómo corregir resultados de OCR con Aspose OCR y Hugging Face – Guía paso a](/ocr/spanish/python/general/how-to-correct-ocr-results-with-aspose-ocr-and-hugging-face/)
- [Wie man OCR-Ergebnisse mit Aspose OCR und Hugging Face korrigiert – Schritt‑für‑Schritt‑Anleitung](/ocr/german/python/general/how-to-correct-ocr-results-with-aspose-ocr-and-hugging-face/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}