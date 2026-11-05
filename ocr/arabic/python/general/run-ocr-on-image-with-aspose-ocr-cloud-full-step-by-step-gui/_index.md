---
category: general
date: 2026-03-28
description: تعلم كيفية تشغيل OCR على الصورة، تنزيل نموذج Hugging Face تلقائيًا، تنظيف
  نص OCR وتكوين نموذج LLM في بايثون باستخدام Aspose OCR Cloud.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: ar
og_description: قم بتشغيل OCR على الصورة وتنظيف المخرجات باستخدام نموذج Hugging Face
  يتم تنزيله تلقائيًا. يوضح هذا الدليل كيفية تكوين نموذج LLM في بايثون.
og_title: تشغيل OCR على الصورة – دليل Aspose OCR Cloud الكامل
tags:
- OCR
- Python
- LLM
- HuggingFace
title: تشغيل OCR على الصورة باستخدام Aspose OCR Cloud – دليل كامل خطوة بخطوة
url: /ar/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على الصورة – دليل Aspose OCR Cloud الكامل

هل احتجت يوماً لتشغيل OCR على ملفات الصور لكن المخرجات الأولية كانت تبدو فوضىً غير مفهومة؟ في تجربتي، أكبر نقطة ألم ليست في عملية التعرف نفسها—بل في عملية التنظيف. لحسن الحظ، يتيح لك Aspose OCR Cloud إرفاق معالج ما بعد‑الـLLM يمكنه *تنظيف نص OCR* تلقائيًا. في هذا الدرس سنستعرض كل ما تحتاجه: من **تنزيل نموذج Hugging Face** إلى تكوين الـLLM، تشغيل محرك OCR، وأخيرًا صقل النتيجة.

بحلول نهاية هذا الدليل ستحصل على سكريبت جاهز للتنفيذ يقوم بـ:

1. سحب نموذج Qwen 2.5 المدمج من Hugging Face (تم تنزيله تلقائيًا لك).  
2. تكوين النموذج لتشغيل جزء من الشبكة على الـGPU والباقي على الـCPU.  
3. تنفيذ محرك OCR على صورة ملاحظة مكتوبة بخط اليد.  
4. استخدام الـLLM لتنظيف النص المُعترف به، مما يمنحك مخرجات قابلة للقراءة البشرية.

> **المتطلبات المسبقة** – Python 3.8+، حزمة `asposeocrcloud`، بطاقة GPU بسعة لا تقل عن 4 GB VRAM (اختياري لكن يُنصح به)، واتصال إنترنت لتنزيل النموذج الأول.

---

## ما ستحتاجه

- **Aspose OCR Cloud SDK** – تثبيت عبر `pip install asposeocrcloud`.  
- **صورة نموذجية** – مثال: `handwritten_note.jpg` موجودة في مجلد محلي.  
- **دعم GPU** – إذا كان لديك GPU يدعم CUDA، سيقوم السكريبت بتحميل 30 طبقة؛ وإلا سيعود تلقائيًا إلى الـCPU.  
- **صلاحية كتابة** – يقوم السكريبت بتخزين النموذج مؤقتًا في `YOUR_DIRECTORY`؛ تأكد من وجود المجلد.

---

## الخطوة 1 – تكوين نموذج الـLLM (تنزيل نموذج Hugging Face)

أول ما نفعله هو إخبار Aspose AI من أين يجلب النموذج. تتولى فئة `AsposeAIModelConfig` عملية التنزيل التلقائي، والكمّية، وتخصيص طبقات الـGPU.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**لماذا هذا مهم** – تحويل النموذج إلى `int8` يقلل استهلاك الذاكرة بشكل كبير (≈ 4 GB مقابل 12 GB). تقسيم النموذج بين الـGPU والـCPU يتيح لك تشغيل LLM بحدود 3 مليار معامل حتى على RTX 3060 متوسط القدرة. إذا لم يكن لديك GPU، اضبط `gpu_layers=0` وسيتولى الـSDK تشغيل كل شيء على الـCPU.

> **نصيحة:** التشغيل الأول سيقوم بتنزيل حوالي 1.5 GB، لذا امنحه بضع دقائق واتصالًا مستقرًا.

---

## الخطوة 2 – تهيئة محرك الذكاء الاصطناعي باستخدام تكوين النموذج

الآن نقوم بتشغيل محرك Aspose AI ونمرره إلى التكوين الذي أنشأناه للتو.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**ما الذي يحدث خلف الكواليس؟** يتحقق الـSDK من `directory_model_path` للعثور على نموذج موجود. إذا وجد نسخة مطابقة، يقوم بتحميلها فورًا؛ وإلا سيقوم بتنزيل ملف GGUF من Hugging Face، فك ضغطه، وإعداد خط أنابيب الاستدلال.

---

## الخطوة 3 – إنشاء محرك OCR وإرفاق معالج ما بعد‑الـAI

يقوم محرك OCR بالعمل الشاق للتعرف على الأحرف. عبر إرفاق `ocr_ai.run_postprocessor` نُمكّن **تنظيف نص OCR** تلقائيًا بعد عملية التعرف.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**لماذا نستخدم معالج ما بعد‑الـAI؟** غالبًا ما يحتوي OCR الخام على فواصل أسطر في أماكن غير صحيحة، علامات ترقيم خاطئة، أو رموز عشوائية. يستطيع الـLLM إعادة صياغة المخرجات إلى جمل صحيحة، تصحيح الأخطاء الإملائية، وحتى استنتاج الكلمات المفقودة—مما يحول النص الخام إلى نص منقح.

---

## الخطوة 4 – تشغيل OCR على ملف صورة

مع ربط جميع المكونات، حان الوقت لتغذية صورة إلى المحرك.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**حالة خاصة:** إذا كانت الصورة كبيرة (> 5 MP)، قد ترغب في تصغير حجمها أولاً لتسريع المعالجة. يقبل الـSDK كائن Pillow `Image`، لذا يمكنك التحضير مسبقًا باستخدام `PIL.Image.thumbnail()` إذا لزم الأمر.

---

## الخطوة 5 – السماح للـAI بتنظيف النص المُعترف به وعرض النسختين

أخيرًا نستدعي معالج ما بعد‑الـAI الذي أرفقناه مسبقًا. تُظهر هذه الخطوة الفارق بين *قبل* و*بعد* التنظيف.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### المخرجات المتوقعة

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

لاحظ كيف قام الـLLM بـ:

- تصحيح الأخطاء الشائعة في OCR (`Th1s` → `This`).  
- إزالة الرموز العشوائية (`&` → `and`).  
- تحويل فواصل الأسطر إلى جمل صحيحة.

---

## 🎨 نظرة بصرية (سير عمل تشغيل OCR على الصورة)

![Run OCR on image workflow](run_ocr_on_image_workflow.png "Diagram showing the run OCR on image pipeline from model download to cleaned output")

تلخّص الصورة أعلاه الخطوات الكاملة: **تنزيل نموذج Hugging Face → تكوين الـLLM → تهيئة AI → محرك OCR → معالج ما بعد‑الـAI → تنظيف نص OCR**.

---

## أسئلة شائعة ونصائح احترافية

### ماذا لو لم يكن لدي GPU؟

اضبط `gpu_layers=0` في `AsposeAIModelConfig`. سيعمل النموذج بالكامل على الـCPU، وهو أبطأ لكنه لا يزال فعالًا. يمكنك أيضًا الانتقال إلى نموذج أصغر (مثل `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`) لتقليل زمن الاستدلال.

### كيف أغيّر النموذج لاحقًا؟

ما عليك سوى تحديث `hugging_face_repo_id` وإعادة تشغيل `ocr_ai.initialize(model_config)`. سيكتشف الـSDK تغيير الإصدار، ينزل النموذج الجديد، ويستبدل الملفات المخزنة مؤقتًا.

### هل يمكن تخصيص موجه معالج ما بعد‑الـAI؟

نعم. مرّر قاموسًا إلى `custom_settings` يحتوي على مفتاح `prompt_template`. مثال:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### هل يجب تخزين النص المنقح في ملف؟

بالتأكيد. بعد التنظيف يمكنك كتابة النتيجة إلى ملف `.txt` أو `.json` لمعالجة لاحقة:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## الخلاصة

لقد أظهرنا لك كيفية **تشغيل OCR على الصور** باستخدام Aspose OCR Cloud، مع **تنزيل نموذج Hugging Face** تلقائيًا، وتكوين إعدادات **نموذج الـLLM** بدقة، وأخيرًا **تنظيف نص OCR** باستخدام معالج ما بعد‑الـLLM قوي. العملية بأكملها تتضمن سكريبت Python واحد سهل التشغيل وتعمل على الأجهزة التي تدعم GPU أو على الـCPU فقط.

إذا شعرت بالراحة مع هذا الخط الأنابيب، فكر في التجربة مع:

- **نماذج LLM مختلفة** – جرّب `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` للحصول على نافذة سياق أوسع.  
- **معالجة دفعات** – كرّر العملية على مجلد من الصور واجمع النتائج المنقحة في ملف CSV.  
- **موجهات مخصصة** – عدّل الـAI ليتناسب مع مجالك (وثائق قانونية، ملاحظات طبية، إلخ).

لا تتردد في تعديل قيمة `gpu_layers`، أو استبدال النموذج، أو إدخال موجهك الخاص. السماء هي الحد، والكود الموجود الآن هو منصة الإطلاق.

برمجة سعيدة، ولتكن مخرجات OCR دائمًا نظيفة! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}