---
category: general
date: 2026-06-25
description: تعلم كيفية إجراء التعرف الضوئي على الأحرف (OCR) باستخدام بايثون واكتشف
  أفضل طريقة لتحميل الصورة للتعرف الضوئي على الأحرف، ثم عزّز الدقة باستخدام المعالجة
  اللاحقة للذكاء الاصطناعي من Aspose.
draft: false
keywords:
- how to perform OCR
- load image for OCR
- Aspose OCR Python
- AI post‑processor OCR
- OCR accuracy improvement
- Python image processing OCR
language: ar
og_description: كيف تقوم بتنفيذ OCR في بايثون؟ اتبع هذا الدليل لتحميل الصورة للـ OCR،
  وتشغيل التعرف الأساسي، وتعزيز النتائج باستخدام المعالجة اللاحقة للذكاء الاصطناعي
  من Aspose.
og_title: كيفية تنفيذ OCR في بايثون – دليل كامل لـ Aspose OCR والذكاء الاصطناعي
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  headline: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  type: TechArticle
- description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  name: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  steps:
  - name: Expected Output
    text: '``` === Raw OCR === Inv0ice #12345 Date: 2023-08-15 Total: $1,23O'
  - name: What if I don’t have a GPU?
    text: Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size`
      to 2048 for better CPU performance. The model will run slower, but you still
      get the same quality of correction.
  - name: My image is rotated—will `load_image` handle it?
    text: 'Aspose OCR automatically detects orientation, but for extremely skewed
      scans you may want to pre‑rotate using Pillow:'
  - name: How do I process multiple files in a folder?
    text: Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in
      a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()`
      **once** after the loop, not after each file—re‑initialising the model repeatedly
      is wasteful.
  - name: Can I swap the language model?
    text: Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible
      model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization
      setting consistent with your hardware.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: كيفية تنفيذ OCR في بايثون – دليل Aspose الكامل للتعرف الضوئي على الأحرف والذكاء
  الاصطناعي
url: /ar/python/general/how-to-perform-ocr-in-python-complete-aspose-ocr-ai-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إجراء OCR في بايثون – دليل Aspose OCR و AI الكامل

هل تساءلت يومًا **كيفية إجراء OCR** في بايثون دون التعقيد مع حيل الصور منخفضة المستوى؟ لست وحدك. في هذا الدرس سنستعرض تحميل صورة لإجراء OCR، واستخراج النص العادي، ثم تحسين النتيجة باستخدام معالج Aspose AI اللاحق. في النهاية ستحصل على سكريبت جاهز للاستخدام يحول المسحات الضوضائية إلى نص نظيف قابل للبحث—بدون الحاجة إلى خدمات إضافية.

سنغطي كل شيء من تثبيت SDK إلى تحرير الموارد في التطبيقات طويلة التشغيل. إذا سبق لك أن حاولت **تحميل صورة لإجراء OCR** وحصلت على نص مشوش، فهذا الدليل هو الحل. ستلاحظ لماذا الجمع بين OCR التقليدي ونموذج اللغة ينتج نتائج تبدو كأنها مكتوبة يدويًا.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- Python 3.9 أو أحدث (الكود يستخدم type hints التي لا تتقبلها المترجمات القديمة)
- ترخيص Aspose OCR نشط أو نسخة تجريبية مجانية (إصدار المجتمع يعمل للتقييم)
- بطاقة رسومية GPU بسعة لا تقل عن 4 GB VRAM إذا رغبت في تسريع نموذج AI (اختياري لكن مفيد)
- صورة نموذجية، مثلاً `sample_invoice.png`، موجودة في مسار يمكنك الإشارة إليه

إذا كان أي من هذه غير مألوف لك، لا تقلق—تثبيت SDK يتم بأمر واحد، ويمكن إيقاف إعدادات GPU لاحقًا.

## الخطوة 1: تثبيت Aspose OCR والاعتمادات

افتح الطرفية واكتب:

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

الحزمة الأولى تزودك بـ `aspose.ocr`، والثانية تضيف أدوات معالج AI اللاحق. كلاهما عجلات Python صافية، لذا لن تحتاج إلى تجميع أي شيء بنفسك.

## الخطوة 2: تحميل صورة لإجراء OCR وتهيئة المحرك

الآن سنقوم **بتحميل صورة لإجراء OCR** باستخدام `OcrEngine` من Aspose. فكر في ذلك كأنك تسلم ورقة إلى موظف دؤوب يقرأ كل حرف.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Initialise the basic OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# Perform a plain OCR scan – this returns a raw string
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)
```

> **لماذا هذا مهم:** استدعاء `load_image` هو الجسر بين نظام الملفات ومحرك OCR. إذا كان المسار غير صحيح، ستحصل على `FileNotFoundError` قبل أن يبدأ أي تعريف. تأكد دائمًا من فواصل الدلائل، خاصةً بين Windows و macOS/Linux.

## الخطوة 3: إعداد معالج Aspose AI اللاحق

يمكن لـ Aspose AI تنزيل نموذج لغة من Hugging Face، تخزينه مؤقتًا محليًا، وتشغيل الاستدلال على GPU (أو CPU). أدناه نضبط نموذجًا خفيفًا بـ 3 مليارات معامل يناسب معظم الحواسيب المحمولة الحديثة.

```python
# Initialise the AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()

# Allow the SDK to fetch the model automatically
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"

# Use half of the GPU layers – balances speed and VRAM usage
model_config.gpu_layers = 20
model_config.context_size = 1024

# Load (or download) the model now
ocr_ai.initialize(model_config)
```

> **نصيحة:** إذا كنت تعمل على جهاز CPU‑only، عيّن `gpu_layers = 0`. سيستمر النموذج في العمل، لكنه سيكون أبطأ قليلًا. التكميم `int8` يحافظ على حجم الذاكرة صغيرًا مع الحفاظ على معظم دقة النموذج.

## الخطوة 4: تسجيل معالج لاحق مخصص

يحتاج نموذج AI إلى موجه يوضح له ما يجب فعله. هنا نطلب منه أن يعمل كمدقق OCR، يصحح الأخطاء الإملائية، يدمج الكلمات المقطوعة، ويزيل الشوائب.

```python
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    # Temperature 0.0 makes the output deterministic
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

# Hook the custom processor into the AI pipeline
ocr_ai.set_post_processor(correction_processor, custom_settings=None)
```

> **لماذا معالج مخصص؟** المعالج الافتراضي قد يضيف شروحات أو تنسيقات لا تحتاجها. عبر توفير دالتنا الخاصة، نحافظ على أن يكون الناتج نصًا نظيفًا فقط، وهو مثالي للفهرسة اللاحقة أو التخزين في قاعدة بيانات.

## الخطوة 5: تشغيل خط أنابيب OCR المدعوم بالذكاء الاصطناعي

الآن نمرر ناتج OCR الخام إلى طبقة AI. سيستدعي المحرك `correction_processor` الخاص بنا، والذي بدوره يتواصل مع نموذج اللغة.

```python
# Apply the AI post‑processor to the raw OCR result
enhanced_text = ocr_ai.run_postprocessor(raw_text)

print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)
```

ستلاحظ تحسينًا واضحًا: تُستعاد الأحرف المفقودة، وتُصحح الأخطاء الشائعة مثل “0” بدلاً من “O”، وتصبح فواصل الأسطر أكثر منطقية.

## الخطوة 6: التنظيف – تحرير الموارد

إذا كنت تخطط لتشغيل هذا داخل خدمة ويب أو عملية daemon طويلة، فإن تحرير ذاكرة GPU أمر حاسم. نسيان استدعاء `free_resources` قد يؤدي إلى تعطل “out‑of‑memory” بعد بضع مئات من الطلبات.

```python
ocr_ai.free_resources()
```

هذا كل شيء—خط أنابيب OCR الكامل الآن جاهز للإنتاج.

## ملخص السكريبت الكامل

فيما يلي المثال الكامل القابل للتنفيذ. انسخه إلى ملف باسم `ocr_with_ai.py`، عدل مسار الصورة، ثم شغّله بـ `python ocr_with_ai.py`.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Step 1: Load image for OCR and perform basic recognition
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)

# Step 2: Initialise the Aspose AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # half of GPU layers
model_config.context_size = 1024
ocr_ai.initialize(model_config)

# Step 3: Register custom correction processor
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

ocr_ai.set_post_processor(correction_processor, custom_settings=None)

# Step 4: Run AI post‑processor on raw OCR output
enhanced_text = ocr_ai.run_postprocessor(raw_text)
print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)

# Step 5: Release resources (important for long‑running apps)
ocr_ai.free_resources()
```

### النتيجة المتوقعة

```
=== Raw OCR ===
Inv0ice #12345
Date: 2023-08-15
Total: $1,23O

=== AI‑enhanced OCR ===
Invoice #12345
Date: 2023-08-15
Total: $1,230
```

لاحظ كيف يتحول “Inv0ice” إلى “Invoice” وتختفي الحرف الزائد “O” بعد المبلغ. هذا هو AI الذي يقوم بسحره.

## الأسئلة الشائعة والحالات الخاصة

### ماذا لو لم يكن لدي GPU؟

عيّن `model_config.gpu_layers = 0` ويمكنك زيادة `model_config.context_size` إلى 2048 لتحسين أداء CPU. سيعمل النموذج أبطأ، لكنك ستحصل على نفس جودة التصحيح.

### صورتي مائلة—هل سيتعامل `load_image` معها؟

Aspose OCR يكتشف الاتجاه تلقائيًا، ولكن للماسحات المائلة بشدة قد تحتاج إلى تدوير مسبق باستخدام Pillow:

```python
from PIL import Image
img = Image.open("sample.png")
rotated = img.rotate(90, expand=True)
rotated.save("rotated.png")
ocr_engine.load_image("rotated.png")
```

### كيف أعالج ملفات متعددة في مجلد؟

لفّ الخط الأنابيب بالكامل داخل حلقة `for` واحفظ كل `enhanced_text` في قائمة أو اكتبها مباشرة إلى CSV. تذكر استدعاء `ocr_ai.free_resources()` **مرة واحدة** بعد انتهاء الحلقة، وليس بعد كل ملف—إعادة تهيئة النموذج في كل مرة مضيعة للموارد.

```python
import os

for filename in os.listdir("invoices"):
    if filename.lower().endswith(".png"):
        ocr_engine.load_image(os.path.join("invoices", filename))
        raw = ocr_engine.recognize()
        clean = ocr_ai.run_postprocessor(raw)
        # Save or index `clean`
```

### هل يمكنني استبدال نموذج اللغة؟

بالطبع. فقط غيّر `model_config.hugging_face_repo_id` إلى أي نموذج متوافق مع GGUF على Hugging Face (مثال: `Meta/Llama-3.2-1B-Instruct-GGUF`). حافظ على إعدادات التكميم متناسقة مع عتادك.

## نصائح احترافية ومخاطر

- **نصيحة احترافية:** عيّن `temperature=0.0` للحصول على تصحيحات حتمية. درجات الحرارة الأعلى قد تُدخل تغييرات إبداعية لكنها غير صحيحة.
- **احذر من:** المستندات الطويلة جدًا (> 5000 حرف). نافذة سياق النموذج محدودة إلى 1024 رمز في المثال؛ قسّم النص إلى فقرات قبل إرساله إلى AI.
- **ملاحظة أمان:** إذا كنت تشغل هذا في بيئة منظمة، تأكد من أن رابط تحميل النموذج مُدرج في القائمة البيضاء. يمكن لعلامة `allow_auto_download` أن

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية استخدام AspOCR: مرشحات تحسين صورة OCR لـ .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [استخراج نص الصورة بـ C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}