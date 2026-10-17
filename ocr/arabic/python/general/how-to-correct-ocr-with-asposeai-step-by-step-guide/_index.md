---
category: general
date: 2026-02-22
description: كيفية تصحيح OCR باستخدام AsposeAI ونموذج HuggingFace. تعلم تنزيل نموذج
  HuggingFace، ضبط حجم السياق، تحميل صورة OCR وتعيين طبقات GPU في بايثون.
draft: false
keywords:
- how to correct ocr
- download huggingface model
- set context size
- load image ocr
- set gpu layers
language: ar
og_description: كيفية تصحيح OCR بسرعة باستخدام AspizeAI. يوضح هذا الدليل كيفية تنزيل
  نموذج HuggingFace، ضبط حجم السياق، تحميل صورة OCR وتعيين طبقات GPU.
og_title: كيفية تصحيح OCR – دليل AsposeAI الكامل
tags:
- OCR
- Aspose
- AI
- Python
title: كيفية تصحيح OCR باستخدام AsposeAI – دليل خطوة بخطوة
url: /ar/python/general/how-to-correct-ocr-with-asposeai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح OCR – دليل كامل لـ AsposeAI

هل تساءلت يومًا **كيف تصحح OCR** النتائج التي تبدو فوضىً مشوشة؟ لست الوحيد. في العديد من المشاريع الواقعية النص الخام الذي ينتجه محرك OCR مليء بالأخطاء الإملائية، وانقطاع السطور، وأحيانًا لا معنى له. الخبر السار؟ باستخدام معالج ما بعد المعالجة الذكي في Aspose.OCR يمكنك تنظيف ذلك تلقائيًا—دون الحاجة إلى تعقيدات regex يدوية.

في هذا الدليل سنستعرض كل ما تحتاج معرفته **كيف تصحح OCR** باستخدام AsposeAI، نموذج HuggingFace، وبعض إعدادات التكوين المفيدة مثل *set context size* و *set gpu layers*. في النهاية ستحصل على سكريبت جاهز للتنفيذ يقوم بتحميل صورة، تشغيل OCR، وإرجاع نص مصقول ومصحح بالذكاء الاصطناعي. لا إطالة، مجرد حل عملي يمكنك دمجه في قاعدة الشيفرة الخاصة بك.

## ما ستتعلمه

- كيفية **load image ocr** ملفات باستخدام Aspose.OCR في Python.  
- كيفية **download huggingface model** تلقائيًا من Hub.  
- كيفية **set context size** حتى لا يتم قطع المطالبات الطويلة.  
- كيفية **set gpu layers** لتحقيق توازن بين عبء العمل على CPU و GPU.  
- كيفية تسجيل معالج ما بعد المعالجة AI الذي **كيف تصحح OCR** النتائج مباشرةً.  

### المتطلبات المسبقة

- Python 3.8 أو أحدث.  
- حزمة `aspose-ocr` (يمكنك تثبيتها عبر `pip install aspose-ocr`).  
- بطاقة GPU متوسطة (اختياري، لكن يُنصح به لخطوة *set gpu layers*).  
- ملف صورة (`invoice.png` في المثال) تريد تطبيق OCR عليه.

إذا كان أي من ذلك غير مألوف بالنسبة لك، لا تقلق—كل خطوة أدناه تشرح لماذا هي مهمة وتقدم بدائل.

---

## الخطوة 1 – تهيئة محرك OCR و **load image ocr**

قبل أن يمكن أي تصحيح، نحتاج إلى نتيجة OCR خام للعمل عليها. يجعل محرك Aspose.OCR ذلك بسيطًا.

```python
import clr
import aspose.ocr as ocr
import System

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the image you want to process – replace the path with your own file
ocr_engine.set_image(System.Drawing.Image.FromFile(r"YOUR_DIRECTORY/invoice.png"))
```

**لماذا هذا مهم:**  
استدعاء `set_image` يخبر المحرك أي صورة bitmap يجب تحليلها. إذا تخطيت هذا، لن يكون لدى المحرك ما يقرأه وسيرمي استثناء `NullReferenceException`. أيضًا، لاحظ السلسلة الخام (`r"…"`) – فهي تمنع تفسير الشرطات العكسية بنمط Windows كحروف هروب.

> *نصيحة احترافية:* إذا كنت بحاجة لمعالجة صفحة PDF، حوّلها إلى صورة أولًا (مكتبة `pdf2image` تعمل جيدًا) ثم مرّر تلك الصورة إلى `set_image`.

---

## الخطوة 2 – تكوين AsposeAI و **download huggingface model**

AsposeAI هو مجرد غلاف خفيف حول محول HuggingFace. يمكنك توجيهه إلى أي مستودع متوافق، لكن لهذا الدليل سنستخدم النموذج الخفيف `bartowski/Qwen2.5-3B-Instruct-GGUF`.

```python
import aspose.ocr.ai as ocr_ai   # AsposeAI namespace

# Simple logger so we can see what the engine is doing
def console_logger(message):
    print("[AsposeAI] " + message)

# Create the AI engine with our logger
ai_engine = ocr_ai.AsposeAI(console_logger)

# Model configuration – this is where we **download huggingface model**
model_config = ocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"                     # Auto‑download if missing
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"              # Smaller RAM footprint
model_config.gpu_layers = 20                                 # **set gpu layers**
model_config.context_size = 2048                             # **set context size**
model_config.allow_auto_download = "true"

# Initialise the AI engine with the config
ai_engine.initialize(model_config)
```

**لماذا هذا مهم:**  

- **download huggingface model** – ضبط `allow_auto_download` إلى `"true"` يخبر AsposeAI بجلب النموذج في المرة الأولى التي تشغّل فيها السكريبت. لا حاجة لخطوات `git lfs` يدوية.  
- **set context size** – `context_size` يحدد عدد الرموز التي يمكن للنموذج رؤيتها في آن واحد. قيمة أكبر (2048) تسمح لك بإدخال مقاطع OCR أطول دون قطع.  
- **set gpu layers** – بتخصيص أول 20 طبقة من المحول إلى GPU تحصل على زيادة ملحوظة في السرعة مع إبقاء الطبقات المتبقية على CPU، وهو مثالي للبطاقات المتوسطة التي لا تستطيع استيعاب النموذج بالكامل في الذاكرة VRAM.

> *ماذا لو لم يكن لدي GPU؟* فقط اضبط `gpu_layers = 0`؛ سيعمل النموذج بالكامل على CPU، وإن كان أبطأ.

---

## الخطوة 3 – تسجيل معالج ما بعد المعالجة AI حتى يمكنك **كيف تصحح OCR** تلقائيًا

يسمح Aspose.OCR لك بإرفاق دالة معالج ما بعد المعالجة التي تستقبل كائن `OcrResult` الخام. سنرسل تلك النتيجة إلى AsposeAI، الذي سيعيد نسخة منقحة.

```python
import aspose.ocr.recognition as rec

def ai_postprocessor(rec_result: rec.OcrResult):
    """
    Sends the raw OCR text to AsposeAI for correction.
    Returns the same OcrResult object with its `text` field updated.
    """
    return ai_engine.run_postprocessor(rec_result)

# Hook the post‑processor into the OCR engine
ocr_engine.add_post_processor(ai_postprocessor)
```

**لماذا هذا مهم:**  
بدون هذا الخطاف، سيتوقف محرك OCR عند المخرجات الخام. بإدراج `ai_postprocessor`, كل استدعاء لـ `recognize()` سيُطلق تصحيح AI تلقائيًا، مما يعني أنك لن تحتاج لتذكر استدعاء دالة منفصلة لاحقًا. هذه هي أنقى طريقة للإجابة على سؤال **كيف تصحح OCR** في خط أنابيب واحد.

---

## الخطوة 4 – تشغيل OCR ومقارنة النص الخام مع النص المصحح بالذكاء الاصطناعي

الآن يحدث السحر. سيولد المحرك أولاً النص الخام، ثم يمرره إلى AsposeAI، وأخيرًا يعيد النسخة المصححة—كل ذلك في استدعاء واحد.

```python
# Perform OCR – the post‑processor runs behind the scenes
ocr_result = ocr_engine.recognize()

print("Raw OCR text:")
print(ocr_result.text)          # before AI correction (will be overwritten)

print("\nAI‑corrected text:")
print(ocr_result.text)          # after AI correction (post‑processor applied)
```

**الناتج المتوقع (مثال):**

```
Raw OCR text:
Inv0ice No.: 12345
Date: 2023/09/15
Total Amt: $1,2O0.00

AI‑corrected text:
Invoice No.: 12345
Date: 2023/09/15
Total Amt: $1,200.00
```

لاحظ كيف يقوم AI بتصحيح الـ “0” التي قرأتها كـ “O” ويضيف الفاصل العشري المفقود. هذه هي جوهر **كيف تصحح OCR**—النموذج يتعلم من أنماط اللغة ويصحح الأخطاء الشائعة في OCR.

> *حالة حدية:* إذا فشل النموذج في تحسين سطر معين، يمكنك الرجوع إلى النص الخام عبر فحص درجة الثقة (`rec_result.confidence`). حاليًا AsposeAI يعيد نفس كائن `OcrResult`، لذا يمكنك حفظ النص الأصلي قبل تشغيل معالج ما بعد المعالجة إذا احتجت إلى شبكة أمان.

---

## الخطوة 5 – تنظيف الموارد

دائمًا حرّر الموارد الأصلية عند الانتهاء، خاصةً عند التعامل مع ذاكرة GPU.

```python
# Release AI resources (clears the model from GPU/CPU memory)
ai_engine.free_resources()

# Dispose the OCR engine to free the .NET image handle
ocr_engine.dispose()
```

تخطي هذه الخطوة قد يترك مقبضًا معلقًا يمنع السكريبت من الإغلاق بشكل نظيف، أو ما هو أسوأ، يسبب أخطاء نفاد الذاكرة في التشغيلات اللاحقة.

---

## سكريبت كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في ملف باسم `correct_ocr.py`. فقط استبدل `YOUR_DIRECTORY/invoice.png` بالمسار إلى صورتك الخاصة.

```python
import clr
import aspose.ocr as ocr
import aspose.ocr.ai as ocr_ai   # AsposeAI namespace
import aspose.ocr.recognition as rec
import System

# -------------------------------------------------
# Step 1: Initialise the OCR engine and load image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(System.Drawing.Image.FromFile(r"YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# Step 2: Configure AsposeAI – download model, set context & GPU
# -------------------------------------------------
def console_logger(message):
    print("[AsposeAI] " + message)

ai_engine = ocr_ai.AsposeAI(console_logger)

model_config = ocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # set gpu layers
model_config.context_size = 2048     # set context size
ai_engine.initialize(model_config)

# -------------------------------------------------
# Step 3: Register AI post‑processor
# -------------------------------------------------
def ai_postprocessor(rec_result: rec.OcrResult):
    return ai_engine.run_postprocessor(rec_result)

ocr_engine.add_post_processor(ai_postprocessor)

# -------------------------------------------------
# Step 4: Perform OCR and show before/after
# -------------------------------------------------
ocr_result = ocr_engine.recognize()

print("Raw OCR text:")
print(ocr_result.text)

print("\nAI‑corrected text:")
print(ocr_result.text)

# -------------------------------------------------
# Step 5: Release resources
# -------------------------------------------------
ai_engine.free_resources()
ocr_engine.dispose()
```

شغّله باستخدام:

```bash
python correct_ocr.py
```

يجب أن ترى المخرجات الخام متبوعةً بالنسخة المنقحة، مما يؤكد أنك نجحت في تعلم **كيف تصحح OCR** باستخدام AsposeAI.

---

## الأسئلة المتكررة & استكشاف الأخطاء وإصلاحها

### 1. *ماذا لو فشل تحميل النموذج؟*  
تأكد من أن جهازك يستطيع الوصول إلى `https://huggingface.co`. قد يحظر جدار الحماية المؤسسي الطلب؛ في هذه الحالة، قم بتحميل ملف `.gguf` يدويًا من المستودع وضعه في دليل التخزين المؤقت الافتراضي لـ AsposeAI (`%APPDATA%\Aspose\AsposeAI\Cache` على Windows).

### 2. *بطاقة GPU تنفد من الذاكرة مع 20 طبقة.*  
قلل `gpu_layers` إلى قيمة تناسب بطاقتك (مثلاً، `5`). ستعود الطبقات المتبقية تلقائيًا إلى CPU.

### 3. *النص المصحح لا يزال يحتوي على أخطاء.*  
حاول زيادة `context_size` إلى `4096`. السياق الأطول يسمح للنموذج بأخذ المزيد من الكلمات المحيطة في الاعتبار، مما يحسن التصحيح للفواتير متعددة الأسطر.

### 4. *هل يمكنني استخدام نموذج HuggingFace مختلف؟*  
بالتأكيد. فقط استبدل `hugging_face_repo_id` بمستودع آخر يحتوي على ملف GGUF متوافق مع التكميم `int8`. Keep

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}