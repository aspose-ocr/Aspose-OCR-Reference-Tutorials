---
category: general
date: 2026-11-20
description: قم بإجراء التعرف الضوئي على الأحرف (OCR) للصورة باستخدام Aspose OCR ثم
  استخراج النص من الصورة باستخدام معالج ما بعد المعالجة الذكي المدمج. تعلم سير عمل
  كامل بلغة بايثون في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
language: ar
lastmod: 2026-11-20
og_description: قم بإجراء التعرف الضوئي على الأحرف (OCR) للصورة باستخدام Aspose OCR،
  ثم استخرج النص من الصورة عبر المعالجة اللاحقة بالذكاء الاصطناعي. اتبع هذا الدليل
  خطوة بخطوة بلغة بايثون.
og_image_alt: Diagram showing how to perform OCR on image and extract text from image
  using Aspose
og_title: إجراء التعرف الضوئي على الأحرف في الصورة واستخراج النص من الصورة باستخدام
  Aspose
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Perform OCR on image with Aspose OCR and then extract text from image
    using the built‑in AI post‑processor. Learn a complete Python workflow in minutes.
  headline: Perform OCR on image and extract text from image with Aspose
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI post‑processing
title: إجراء التعرف الضوئي على الأحرف في الصورة واستخراج النص من الصورة باستخدام Aspose
url: /ar/python/general/perform-ocr-on-image-and-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على الصورة واستخراج النص من الصورة باستخدام Aspose

إذا كنت بحاجة إلى **perform OCR on image** ملفات في Python، يوضح لك هذا الدليل حلاً كاملاً من البداية إلى النهاية. باستخدام Aspose OCR مع معالج Aspose AI اللاحق، يمكنك بثقة **extract text from image** الملفات وتحسين مخرجات OCR الخام باستخدام نموذج لغة خفيف.

في هذا الدرس ستقوم بـ:

* إعداد محرك Aspose OCR.
* تشغيل OCR لـ **extract text from image**.
* اختياريًا تكوين نموذج AI للمعالجة اللاحقة.
* تسجيل دالة معالج لاحق مخصصة.
* إنتاج نص محسّن وتنظيف الموارد.

تعمل الخطوات مع أي صورة نقطية (PNG، JPEG، BMP) وتحتاج فقط إلى حزمة `aspose-ocr`.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أنك تمتلك:

| المتطلب | سبب أهميته |
|-------------|----------------|
| Python 3.8+ | مطلوب من قبل Aspose SDK. |
| `aspose-ocr` pip package | يوفر فئات `AsposeOCR` و `AsposeAI` و model‑configuration. |
| ملف صورة (مثال: `sample_image.png`) | المصدر الذي ستقوم بـ **perform OCR on image**. |
| اختياري: دعم GPU | إذا كنت تخطط لتشغيل نموذج أكبر على GPU، اضبط `gpu_layers` وفقًا لذلك. |

ثبت SDK باستخدام:

```bash
pip install aspose-ocr
```

## الخطوة 1: Perform OCR on image

العملية الأولى هي قراءة الصورة والحصول على النص الخام. هذه هي الخطوة الأساسية **perform OCR on image**.

```python
from aspose.ocr import AsposeOCR

# Initialise the OCR engine
ocr_engine = AsposeOCR()

# Path to the image you want to process
image_path = "YOUR_DIRECTORY/sample_image.png"

# Execute OCR – this returns the plain text extracted from the image
raw_text = ocr_engine.recognize_image(image_path)

print("Raw OCR result:")
print(raw_text)
```

**لماذا هذا يعمل:** `AsposeOCR.recognize_image` يشغّل نموذج التعرف الضوئي على الحروف المدرب مسبقًا والذي تم تحسينه للسرعة والدقة على الخطوط الشائعة. تُرجع الطريقة سلسلة Unicode عادية، وهي الأساس لأي معالجة لاحقة.

> **نصيحة احترافية:** إذا كانت الصورة تحتوي على لغات متعددة، اضبط `ocr_engine.language = "eng+spa"` (أو أي رمز ISO‑639‑2 مدعوم) قبل استدعاء `recognize_image`.

## الخطوة 2: Initialise the AI post‑processor

توفر Aspose AI طبقة معالجة لاحقة خفيفة الوزن يمكنها تنظيف أخطاء OCR، وتصحيح علامات الترقيم، أو تطبيق منطق أعمال مخصص.

```python
from aspose.ocr import AsposeAI

# Initialise the AI post‑processor with default logging
ai_processor = AsposeAI()
```

**لماذا تحتاجه:** غالبًا ما يخطئ OCR الخام في التعرف على الأحرف (مثال: “0” مقابل “O”). خطوة AI تُحسّن المخرجات، مما يجعل نتيجة **extract text from image** أكثر موثوقية للمهام اللاحقة مثل الفهرسة أو التحليل.

## الخطوة 3: (اختياري) Configure the AI model

يمكنك توجيه المعالج إلى نموذج Hugging Face محدد، وتمكين التنزيلات التلقائية، أو فرض تنفيذ على وحدة المعالجة المركزية. هذه الخطوة اختيارية ولكنها مفيدة عندما تريد سلوكًا حتميًا.

```python
from aspose.ocr import AsposeAIModelConfig

# Create a configuration object
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"          # Download model if missing
model_config.hugging_face_repo_id = "openai/gpt2"   # Small, fast model
model_config.gpu_layers = 0                        # Use CPU; set >0 for GPU

# Apply the configuration to the AI processor
ai_processor.configure(model_config)
```

**شرح:**  
* `allow_auto_download` يوفر عليك إدارة النماذج يدويًا.  
* `hugging_face_repo_id` يختار نموذجًا؛ `gpt2` هو توازن جيد بين الحجم والجودة لتصحيح النص القصير.  
* `gpu_layers` يتحكم في عدد طبقات المحول التي تُشغَّل على GPU؛ `0` يفرض تنفيذًا بحتًا على CPU، وهو آمن على جميع الأجهزة.

## الخطوة 4: Register a custom post‑processing function

تتيح لك Aspose AI توصيل أي دالة قابلة للاستدعاء تستقبل سلسلة OCR الخام وتعيد نسخة مُحوَّلة. أدناه مثال بسيط يحول كل شيء إلى أحرف كبيرة.

```python
def my_post_processor(text):
    """
    Custom post‑processor that transforms the OCR result.
    Replace this logic with your own business rules.
    """
    return text.upper()

# Register the function with the AI processor
ai_processor.set_post_processor(my_post_processor, custom_settings=None)
```

**متى تخصص:** استخدم دالة مخصصة عندما تحتاج إلى تنظيف خاص بالمجال، مثل إزالة المعرفات السرية، توحيد التواريخ، أو تطبيق تصحيحات تعتمد على regex. سيعمل نموذج AI *بعد* هذه الدالة، مما يتيح لك دمج القواعد الحتمية مع التحسينات الاحتمالية.

## الخطوة 5: Enhance the OCR result using the AI post‑processor

الآن شغّل خط الأنابيب الكامل: يُمرَّر نص OCR الخام أولاً عبر دالتك المخصصة، ثم عبر نموذج AI، وأخيرًا تحصل على المخرجات المُحسّنة.

```python
# Run the AI post‑processor on the raw OCR text
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("\nOriginal OCR :")
print(raw_text)
print("\nAI‑enhanced   :")
print(enhanced_text)
```

**ما يجب أن تراه:**  
إذا كانت الصورة الأصلية تحتوي على “Hello world”، قد يعرض الطرفية:

```
Original OCR :
Hello world

AI‑enhanced   :
HELLO WORLD
```

في سيناريو واقعي، سيصحح نموذج AI الأخطاء الإملائية، ويضيف علامات الترقيم المفقودة، أو يعيد تنسيق فواصل الأسطر، مما يمنحك نتيجة **extract text from image** أنظف جاهزة للتخزين أو التحليل.

## الخطوة 6: Release resources when finished

كل من محرك OCR ومعالج AI اللاحق يخصصان موارد أصلية. تحريرهما صراحةً يمنع تسرب الذاكرة، خاصةً في الخدمات الطويلة التشغيل.

```python
# Clean up native resources
ai_processor.free_resources()
```

إذا قمت أيضًا بإنشاء `ocr_engine` مع خلفية ثقيلة، يمكنك استدعاء `ocr_engine.dispose()` (إن كان متاحًا) بنفس الطريقة.

## الاختلافات الشائعة وحالات الحافة

| الحالة | التعديل الموصى به |
|-----------|------------------------|
| **ملفات PDF الكبيرة ذات الصفحات المتعددة** | تكرار عبر كل صفحة، استدعاء `recognize_image` لكل صفحة نقطية، وتجميع النتائج. |
| **بيئة مفعّلة بـ GPU** | اضبط `model_config.gpu_layers` على عدد الطبقات التي تريدها على GPU (مثال: `4`). تأكد من تثبيت تعريفات CUDA. |
| **نص غير إنجليزي** | غيّر `ocr_engine.language` إلى رمز اللغة المناسب، وإذا لزم الأمر، اختر نموذج Hugging Face مخصص لتلك اللغة. |
| **مسحات ضوضائية جدًا** | قم بمعالجة مسبقة للصورة باستخدام OpenCV (إزالة الضوضاء، العتبة) قبل استدعاء `recognize_image`. |
| **الحاجة إلى الحفاظ على الحالة الأصلية** | استبدل دالة `my_post_processor` بدالة لا تفعل شيئًا أو قاعدة أكثر دقة بدلاً من `text.upper()`. |

## مثال كامل يعمل

بجمع كل شيء معًا، إليك سكريبت واحد يمكنك تشغيله كما هو (استبدل `YOUR_DIRECTORY/sample_image.png` بمسار ملفك الفعلي):

```python
from aspose.ocr import AsposeOCR, AsposeAI, AsposeAIModelConfig

# 1️⃣ Perform OCR on image
ocr_engine = AsposeOCR()
image_path = "YOUR_DIRECTORY/sample_image.png"
raw_text = ocr_engine.recognize_image(image_path)

# 2️⃣ Initialise the AI post‑processor
ai_processor = AsposeAI()

# 3️⃣ (Optional) Configure the AI model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "openai/gpt2"
model_config.gpu_layers = 0            # CPU execution
ai_processor.configure(model_config)

# 4️⃣ Register a custom post‑processor (example: uppercase)
def my_post_processor(text):
    return text.upper()

ai_processor.set_post_processor(my_post_processor, custom_settings=None)

# 5️⃣ Enhance the OCR result
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("Original OCR :", raw_text)
print("AI‑enhanced   :", enhanced_text)

# 6️⃣ Release resources
ai_processor.free_resources()
```

تشغيل هذا السكريبت يطبع كلًا من مخرجات OCR الخام والإصدار المحسن بالـ AI، موضحًا كيف يمكنك **perform OCR on image** الملفات وبثقة **extract text from image** في سير عمل واحد قابل للتكرار.

## الخلاصة

أنت الآن تعرف كيف **perform OCR on image** الملفات باستخدام Aspose OCR، ثم **extract text from image** باستخدام معالج AI المدمج. يغطي الدليل:

* تهيئة محرك OCR.
* تشغيل OCR للحصول على النص الخام.
* (اختياريًا) تكوين نموذج Hugging Face خفيف الوزن.
* إضافة a

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide](/ocr/english/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/)
- [How to Correct OCR Errors – Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image Python – Complete Aspose OCR Guide](/ocr/english/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}