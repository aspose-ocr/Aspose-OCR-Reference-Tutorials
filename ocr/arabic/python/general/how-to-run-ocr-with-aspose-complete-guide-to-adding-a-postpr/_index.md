---
category: general
date: 2026-02-22
description: تعلم كيفية تشغيل تقنية التعرف الضوئي على الحروف (OCR) على الصور باستخدام
  Aspose وكيفية إضافة معالج لاحق للحصول على نتائج محسّنة بالذكاء الاصطناعي. دليل بايثون
  خطوة بخطوة.
draft: false
keywords:
- how to run OCR
- how to add postprocessor
language: ar
og_description: اكتشف كيفية تشغيل OCR باستخدام Aspose وكيفية إضافة معالج لاحق للحصول
  على نص أنظف. مثال كامل على الشيفرة ونصائح عملية.
og_title: كيفية تشغيل OCR مع Aspose – إضافة معالج لاحق في بايثون
tags:
- Aspose OCR
- Python
- AI post‑processing
title: كيفية تشغيل OCR باستخدام Aspose – دليل شامل لإضافة معالج ما بعد المعالجة
url: /ar/python/general/how-to-run-ocr-with-aspose-complete-guide-to-adding-a-postpr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR باستخدام Aspose – دليل كامل لإضافة معالج لاحق

هل تساءلت يومًا **كيف تشغل OCR** على صورة دون الحاجة إلى التعامل مع عشرات المكتبات؟ لست وحدك. في هذا الدرس سنستعرض حلًا بلغة Python لا يقتصر فقط على تشغيل OCR بل يوضح أيضًا **كيف تضيف معالجًا لاحقًا** لتحسين الدقة باستخدام نموذج AI من Aspose.  

سنغطي كل شيء من تثبيت SDK إلى تحرير الموارد، بحيث يمكنك نسخ‑لصق برنامج يعمل ورؤية النص المصحح في ثوانٍ. لا خطوات مخفية، فقط شروحات واضحة باللغة الإنجليزية وقائمة كاملة بالكود.

## ما الذي ستحتاجه

| المتطلبات المسبقة | لماذا يهم |
|------------------|-----------|
| Python 3.8+ | مطلوب لجسر `clr` وحزم Aspose |
| `pythonnet` (pip install pythonnet) | يتيح التفاعل مع .NET من Python |
| Aspose.OCR for .NET (download from Aspose) | محرك OCR الأساسي |
| اتصال بالإنترنت (التشغيل الأول) | يسمح للنموذج AI بالتحميل التلقائي |
| صورة نموذجية (`sample.jpg`) | الملف الذي سنمرره إلى محرك OCR |

إذا كان أي من هذه غير مألوف لك، لا تقلق—تثبيتها سهل وسنذكر الخطوات الأساسية لاحقًا.

## الخطوة 1: تثبيت Aspose OCR وإعداد جسر .NET  

لتشغيل **OCR** تحتاج إلى ملفات DLL الخاصة بـ Aspose OCR وجسر `pythonnet`. نفّذ الأوامر التالية في الطرفية:

```bash
pip install pythonnet
# Download the Aspose.OCR for .NET zip from https://downloads.aspose.com/ocr/python-net
# Unzip it and note the folder path, e.g., C:\Aspose\OCR\Net
```

بعد أن تكون ملفات DLL على القرص، أضف المجلد إلى مسار CLR حتى يتمكن Python من العثور عليها:

```python
import sys, os, clr

# Adjust this path to where you extracted the Aspose OCR binaries
aspose_path = r"C:\Aspose\OCR\Net"
sys.path.append(aspose_path)

# Load the main assembly
clr.AddReference("Aspose.OCR")
clr.AddReference("Aspose.OCR.AI")
```

> **نصيحة احترافية:** إذا حصلت على استثناء `BadImageFormatException`، تأكد من أن مفسّر Python يطابق بنية DLL (كلاهما 64‑bit أو كلاهما 32‑bit).

## الخطوة 2: استيراد المساحات الاسمية وتحميل صورتك  

الآن يمكننا جلب فئات OCR إلى النطاق وتوجيه المحرك إلى ملف الصورة:

```python
import System
import aspose.ocr as ocr
import aspose.ocr.ai as ocr_ai
import System.Drawing

# Create the OCR engine instance
ocr_engine = ocr.OcrEngine()

# Load the image you want to process
image_path = r"YOUR_DIRECTORY/sample.jpg"
ocr_engine.set_image(System.Drawing.Image.FromFile(image_path))
```

دالة `set_image` تقبل أي صيغة يدعمها GDI+، لذا PNG أو BMP أو TIFF تعمل بنفس كفاءة JPG.

## الخطوة 3: تكوين نموذج Aspose AI للمعالجة اللاحقة  

هنا نجيب على **كيف تضيف معالجًا لاحقًا**. نموذج AI موجود في مستودع Hugging Face ويمكن تحميله تلقائيًا عند الاستخدام الأول. سنقوم بتكوينه ببعض الإعدادات المنطقية:

```python
# A silent logger – Aspose AI expects a callable, we give it a no‑op lambda
logger = lambda msg: None

# Initialise the AI processor
ai_processor = ocr_ai.AsposeAI(logger)

# Build the model configuration
model_cfg = ocr_ai.AsposeAIModelConfig()
model_cfg.allow_auto_download = "true"
model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_cfg.hugging_face_quantization = "int8"
model_cfg.gpu_layers = 20          # Use GPU if available; otherwise falls back to CPU
model_cfg.context_size = 2048

# Apply the configuration
ai_processor.initialize(model_cfg)
```

> **لماذا هذا مهم:** المعالج اللاحق AI ينظف الأخطاء الشائعة في OCR (مثل “1” مقابل “l”، أو الفواصل المفقودة) باستخدام نموذج لغة كبير. ضبط `gpu_layers` يسرّع الاستنتاج على وحدات معالجة الرسوميات الحديثة لكنه ليس إلزاميًا.

## الخطوة 4: ربط المعالج اللاحق بمحرك OCR  

مع جاهزية نموذج AI، نربطه بمحرك OCR. طريقة `add_post_processor` تتوقع دالة قابلة للاستدعاء تستقبل نتيجة OCR الخام وتعيد نسخة مصححة.

```python
# Hook the AI post‑processor into the OCR pipeline
ocr_engine.add_post_processor(lambda result: ai_processor.run_postprocessor(result))
```

من الآن فصاعدًا، كل استدعاء لـ `recognize()` سيمرّر النص الخام تلقائيًا عبر نموذج AI.

## الخطوة 5: تشغيل OCR واسترجاع النص المصحح  

حان وقت الحقيقة—لنقم فعليًا **بتشغيل OCR** ونرى المخرجات المحسّنة بواسطة AI:

```python
# Perform recognition
ocr_result = ocr_engine.recognize()

# The .text property holds the corrected string
print("Corrected text:", ocr_result.text)
```

المخرجات النموذجية تكون هكذا:

```
Corrected text: The quick brown fox jumps over the lazy dog.
```

إذا كانت الصورة الأصلية تحتوي على ضوضاء أو خطوط غير مألوفة، ستلاحظ أن نموذج AI يصلح الكلمات المشوهة التي فشل المحرك الخام في التعرف عليها.

## الخطوة 6: تنظيف الموارد  

كلا من محرك OCR ومعالج AI يخصصان موارد غير مُدارة. تحريرهما يمنع تسرب الذاكرة، خاصة في الخدمات التي تعمل لفترات طويلة:

```python
# Release the AI model first
ai_processor.free_resources()

# Then dispose of the OCR engine
ocr_engine.dispose()
```

> **حالة حدية:** إذا كنت تخطط لتشغيل OCR بشكل متكرر داخل حلقة، احتفظ بالمحرك فعالًا واستدعِ `free_resources()` فقط عند الانتهاء. إعادة تهيئة نموذج AI في كل دورة يضيف عبئًا ملحوظًا.

## البرنامج الكامل – جاهز بنقرة واحدة  

فيما يلي البرنامج الكامل القابل للتنفيذ والذي يدمج جميع الخطوات السابقة. استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على `sample.jpg`.

```python
# ------------------------------------------------------------
# How to Run OCR with Aspose and How to Add Postprocessor
# ------------------------------------------------------------
import sys, clr, System, os
import aspose.ocr as ocr
import aspose.ocr.ai as ocr_ai
import System.Drawing

# ----------------------------------------------------------------
# 1️⃣  Set up CLR paths – adjust to your local Aspose folder
# ----------------------------------------------------------------
aspose_path = r"C:\Aspose\OCR\Net"   # <--- change this!
sys.path.append(aspose_path)
clr.AddReference("Aspose.OCR")
clr.AddReference("Aspose.OCR.AI")

# ----------------------------------------------------------------
# 2️⃣  Create OCR engine and load image
# ----------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
image_file = r"YOUR_DIRECTORY/sample.jpg"   # <--- your image here
ocr_engine.set_image(System.Drawing.Image.FromFile(image_file))

# ----------------------------------------------------------------
# 3️⃣  Initialise the AI post‑processor
# ----------------------------------------------------------------
logger = lambda msg: None                # silent logger
ai_processor = ocr_ai.AsposeAI(logger)

model_cfg = ocr_ai.AsposeAIModelConfig()
model_cfg.allow_auto_download = "true"
model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_cfg.hugging_face_quantization = "int8"
model_cfg.gpu_layers = 20
model_cfg.context_size = 2048
ai_processor.initialize(model_cfg)

# ----------------------------------------------------------------
# 4️⃣  Hook the AI processor into the OCR pipeline
# ----------------------------------------------------------------
ocr_engine.add_post_processor(lambda result: ai_processor.run_postprocessor(result))

# ----------------------------------------------------------------
# 5️⃣  Run OCR and print corrected text
# ----------------------------------------------------------------
ocr_result = ocr_engine.recognize()
print("Corrected text:", ocr_result.text)

# ----------------------------------------------------------------
# 6️⃣  Release resources
# ----------------------------------------------------------------
ai_processor.free_resources()
ocr_engine.dispose()
```

شغّل البرنامج باستخدام `python ocr_with_postprocess.py`. إذا تم إعداد كل شيء بشكل صحيح، سيظهر النص المصحح في وحدة التحكم خلال بضع ثوانٍ فقط.

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا على Linux؟**  
ج: نعم، طالما تم تثبيت بيئة تشغيل .NET (عن طريق SDK `dotnet`) والملفات الثنائية المناسبة لـ Aspose على Linux. سيتعين عليك تعديل فواصل المسارات (`/` بدلاً من `\`) والتأكد من أن `pythonnet` مُجمّع ضد نفس بيئة التشغيل.

**س: ماذا لو لم يكن لدي GPU؟**  
ج: اضبط `model_cfg.gpu_layers = 0`. سيعمل النموذج على CPU؛ توقع استنتاج أبطأ لكنه لا يزال فعالًا.

**س: هل يمكنني استبدال مستودع Hugging Face بنموذج آخر؟**  
ج: بالطبع. فقط استبدل `model_cfg.hugging_face_repo_id` بمعرف المستودع المطلوب واضبط `quantization` إذا لزم الأمر.

**س: كيف أتعامل مع ملفات PDF متعددة الصفحات؟**  
ج: حوّل كل صفحة إلى صورة (مثلاً باستخدام `pdf2image`) ومرّرها تسلسليًا إلى نفس `ocr_engine`. يعمل المعالج اللاحق AI على كل صورة على حدة، لذا ستحصل على نص نظيف لكل صفحة.

## الخلاصة  

في هذا الدليل غطينا **كيفية تشغيل OCR** باستخدام محرك Aspose .NET من Python وأظهرنا **كيفية إضافة معالج لاحق** لتنظيف المخرجات تلقائيًا. البرنامج الكامل جاهز للنسخ، اللصق، والتنفيذ—بدون خطوات مخفية أو تنزيلات إضافية بخلاف تحميل النموذج الأولي.  

من هنا يمكنك استكشاف:

- إمداد النص المصحح إلى خط أنابيب NLP لاحق.
- تجربة نماذج Hugging Face مختلفة لمفردات متخصصة.
- توسيع الحل باستخدام نظام طابور لمعالجة دفعات من آلاف الصور.

جرّبه، عدّل المعلمات، ودع AI يتولى الأعمال الشاقة لمشاريع OCR الخاصة بك. Happy coding!  

![مخطط يوضح محرك OCR يمرّر صورة، ثم يرسل النتائج الخام إلى معالج AI اللاحق، وأخيرًا ينتج نصًا مصححًا – كيفية تشغيل OCR مع Aspose ومعالجته لاحقًا](https://example.com/ocr-postprocess-diagram.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}