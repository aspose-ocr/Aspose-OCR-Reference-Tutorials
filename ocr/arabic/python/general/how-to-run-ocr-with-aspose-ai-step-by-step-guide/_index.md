---
category: general
date: 2026-02-09
description: كيفية تشغيل OCR باستخدام Aspose AI ونموذج Hugging Face – تعلم تنزيل نموذج
  Hugging Face، تصحيح أخطاء OCR وتحرير ذاكرة GPU.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: ar
og_description: كيفية تشغيل OCR باستخدام Aspose AI موضحة في الفقرة الأولى – اكتشف
  كيفية تنزيل نموذج Hugging Face، وتصحيح أخطاء OCR، وتحرير ذاكرة GPU.
og_title: كيفية تشغيل OCR باستخدام Aspose AI – الدليل الكامل
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: كيفية تشغيل OCR باستخدام Aspose AI – دليل خطوة بخطوة
url: /ar/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR باستخدام Aspose AI – دليل كامل

هل تساءلت يومًا **how to run OCR** على فاتورة ممسوحة ضوئيًا وتحصل على أرقام نظيفة تمامًا دون قضاء ساعات في تصحيح الأخطاء؟ لست وحدك. في العديد من المشاريع الواقعية لا يزال النص الخام الناتج عن محرك OCR التقليدي يحتوي على أحرف عشوائية، رموز عملة مكسورة، أو أرقام مشوشة—خاصة عندما تكون الصورة المصدرية صاخبة.  

الخبر السار هو أنك يمكنك ربط نموذج LLM بـ Aspose OCR، تنزيل نموذج Hugging Face أثناء التشغيل، والسماح للذكاء الاصطناعي بتحسين النتيجة لك. في هذا الدليل سنستعرض كامل سير العمل، بدءًا من جلب النموذج (نعم، سنوضح لك كيفية **download hugging face model** تلقائيًا) وحتى تحرير موارد GPU عندما تنتهي. في النهاية ستحصل على سكريبت قابل لإعادة الإنتاج **corrects OCR errors**، يعمل بسرعة على GPU متوسط، وينظف نفسه لتجنب إهدار الذاكرة.

## ما ستتعلمه

- إعداد Aspose AI لجلب نموذج **Qwen2.5‑3B‑Instruct‑GGUF** من Hugging Face.
- تشغيل محرك Aspose OCR القياسي على ملف صورة.
- استخدام موجه LLM مخصص يحافظ على الأرقام ورموز العملة دون تغيير.
- تحرير ذاكرة GPU باستخدام الروتين المدمج **free gpu memory**.
- تعديل سير العمل لحالات الحافة مثل ملفات PDF متعددة الصفحات أو GPUs منخفضة الأداء.

> **المتطلبات الأساسية** – Python 3.9+, حزمة `aspose-ocr`، اتصال بالإنترنت لتحميل النموذج الأول، وGPU بسعة لا تقل عن 4 GB VRAM (اختياري لكن موصى به). إذا لم يكن لديك GPU، سيعود السكريبت تلقائيًا إلى CPU للطبقات المتبقية.

---

## كيفية تشغيل OCR وتحسين النتائج

فيما يلي سكريبت Python كامل وجاهز للتنفيذ. احفظه باسم `ocr_with_ai.py` واستبدل مسارات العناصر النائبة بملفاتك الخاصة.

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **نصيحة احترافية:** يتيح لك معامل `gpu_layers` تحديد عدد طبقات الـ transformer التي تبقى على الـ GPU. إذا واجهت أخطاء نفاد الذاكرة، قلل هذا الرقم وستعمل البقية على CPU – ستظل قادرًا على **free gpu memory** لاحقًا باستخدام `ai.free_resources()`.

### النتيجة المتوقعة

تشغيل السكريبت على فاتورة نموذجية ينتج شيئًا مشابهًا لـ:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

لاحظ كيف قام الذكاء الاصطناعي بتصحيح حرف “O” في `$1O0.00` إلى صفر صحيح مع الحفاظ على علامة الدولار. هذا هو جوهر **correct OCR errors** للمستندات المالية.

---

## تنزيل نموذج Hugging Face – ما يحدث خلف الكواليس؟

عند ضبط `allow_auto_download="true"`، يتحقق غلاف Aspose AI من `directory_model_path`. إذا لم تكن ملفات النموذج موجودة، يتواصل مع Hugging Face Hub، ويسحب النسخة **int8‑quantized** من `Qwen2.5‑3B‑Instruct‑GGUF`، ويحفظها محليًا. هذا التنزيل لمرة واحدة عادةً يكون أقل من 2 GB، مما يجعله ممكنًا حتى على SSDs متوسطة.

> **لماذا int8?** يقلل التحويل إلى 8‑bit من استهلاك الذاكرة بشكل كبير—وهذا أمر حاسم عندما تريد أيضًا **free gpu memory** بعد المعالجة. المقايضة هي انخفاض طفيف في الدقة، لكن بالنسبة لمعالجة نص OCR لاحقًا فإن التأثير ضئيل.

إذا كنت تفضل استضافة النموذج بنفسك، ما عليك سوى وضع ملفات `.gguf` في `YOUR_DIRECTORY/Models` وسيتعرف عليها Aspose دون الحاجة إلى الاتصال بالإنترنت مرة أخرى.

---

## كيفية تحرير GPU – أفضل الممارسات

موارد GPU هي مورد مشترك في العديد من محطات العمل. ترك الـ tensors حية بعد انتهاء السكريبت قد يسبب أخطاء “CUDA out of memory” للمهام اللاحقة. استدعاء `ai.free_resources()` يقوم بثلاثة أشياء:

1. **Disposes the underlying transformer** – يتم تحرير جميع الأوزان المقيمة على الـ GPU.
2. **Clears the PyTorch cache** – يتم استدعاء `torch.cuda.empty_cache()` داخليًا.
3. **Deletes temporary files** – يتم حذف أي ملفات مؤقتة على القرص تم إنشاؤها أثناء التنزيل.

يمكنك أيضًا استدعاء `torch.cuda.empty_cache()` يدويًا إذا كنت تمزج Aspose AI مع أحمال عمل PyTorch أخرى، لكن الطريقة المدمجة عادةً ما تكون كافية.

---

## دليل خطوة بخطوة (H2s مع كلمات مفتاحية ثانوية)

### تنزيل نموذج Hugging Face تلقائيًا

يخفي مُنشئ `AsposeAIModelConfig` تعقيد التعامل مع واجهة Hugging Face API. فقط تأكد من وجود اتصال بالإنترنت في المرة الأولى التي تشغّل فيها السكريبت. بعد ذلك، يعيش النموذج في `YOUR_DIRECTORY/Models`، وتبدأ التشغيلات اللاحقة فورًا.

### تحرير ذاكرة GPU بعد الاستدلال

إذا كنت تشغّل هذا داخل خدمة طويلة التشغيل (مثل Flask API)، استدعِ `ai.free_resources()` بعد كل طلب. هذا يمنع تسرب الذاكرة ويضمن أن الطلب التالي يمكنه إعادة استخدام نفس الـ GPU دون مشاكل.

### تصحيح أخطاء OCR باستخدام موجه مخصص

ترجع دالتنا `financial_prompt` قاموسًا يحتوي على مفتاح واحد `prompt`. يمكنك تعديل ذلك لأي مجال:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

غيّر اسم الدالة في `ai.set_post_processor(...)` وستحصل على خط أنابيب **correct OCR errors** لسجلات طبية.

### كيفية تشغيل OCR على ملفات PDF متعددة الصفحات

يمكن لـ Aspose OCR التعامل مع ملفات PDF مباشرةً:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

بعد حصولك على السلسلة الخام، سيقوم نفس معالج الـ LLM بتنظيف نص كل صفحة. لا حاجة لكود إضافي.

### عندما لا تملك GPU – كيفية تحرير GPU (حتى بدون واحد)

حتى على الأجهزة التي تعمل بالـ CPU فقط، استدعاء `ai.free_resources()` لا ضرر فيه. فهو ببساطة يفرغ الذاكرات الداخلية، مما يمكن أن يحرر RAM أيضًا. لذا فإن نصيحة **how to free gpu** تنطبق عالميًا: دائمًا نظّف بعد الانتهاء.

---

## المشكلات الشائعة وكيف حلّناها

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **Out‑of‑Memory on GPU** | تم ضبط `gpu_layers` أعلى من قدرة بطاقتك | قلل `gpu_layers` إلى 10 أو 5، ودع البقية تعمل على CPU |
| **Model never downloads** | جدار الحماية المؤسسي يحظر HTTPS إلى huggingface.co | حمّل النموذج يدويًا عبر شبكة مختلفة، ثم وجه `directory_model_path` إلى المجلد المحلي |
| **Numbers get corrupted** | الموجه غير واضح بما يكفي بشأن الحفاظ على الأرقام | أضف العبارة “preserve all numeric values and currency symbols exactly as they appear” إلى الموجه |
| **`free_resources` raises an exception** | استخدام نسخة قديمة من Aspose OCR | حدّث إلى أحدث حزمة `aspose-ocr` (pip install --upgrade aspose-ocr) |

---

## ملخص المثال الكامل

إليك السكريبت مرة أخرى، هذه المرة مع تعليقات داخلية تشرح كل سطر للرجوع إليه مستقبلاً:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

---

## الخلاصة

لقد غطينا **how to run OCR** باستخدام Aspose، تنزيل نموذج Hugging Face عند الطلب، صياغة موجه **corrects OCR errors**، وأخيرًا **free gpu memory** لتبقى محطة عملك سريعة الاستجابة. يتكامل سير العمل بالكامل في ملف Python واحد مستقل—بدون سكريبتات خارجية، بدون معالجة يدوية للنموذج، وبدون تخصيصات GPU متبقية.

الخطوة التالية؟ جرّب استبدال `financial_prompt` بـ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}