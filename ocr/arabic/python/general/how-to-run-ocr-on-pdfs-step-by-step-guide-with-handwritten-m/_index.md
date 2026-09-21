---
category: general
date: 2026-01-12
description: كيفية تشغيل OCR على ملفات PDF باستخدام Aspose OCR، تحميل OCR للـ PDF،
  تمكين وضع OCR للخط اليدوي ودمج نموذج OCR من Hugging Face للمعالجة اللاحقة.
draft: false
keywords:
- how to run OCR
- load pdf OCR
- handwritten OCR mode
- hugging face OCR model
language: ar
og_description: كيفية تشغيل التعرف الضوئي على الأحرف (OCR) على ملفات PDF باستخدام
  Aspose OCR، وتفعيل وضع التعرف على الخط اليدوي، وتعزيز الدقة باستخدام نموذج OCR من
  Hugging Face.
og_title: كيفية تشغيل OCR على ملفات PDF – دليل كامل
tags:
- OCR
- Python
- Aspose
- Hugging Face
title: كيفية تشغيل OCR على ملفات PDF – دليل خطوة بخطوة مع وضع الخط اليدوي
url: /ar/python/general/how-to-run-ocr-on-pdfs-step-by-step-guide-with-handwritten-m/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR على ملفات PDF – دليل كامل

هل تساءلت يومًا **كيف تشغّل OCR** على ملف PDF متعدد اللغات يحتوي على خط يد فوضوي؟ لست وحدك. في العديد من المشاريع الواقعية—مثل رقمنة الفواتير أو أرشفة الرسائل التاريخية—استخراج النص العادي ليس كافيًا. يوضح لك هذا الدليل بالضبط كيفية تشغيل OCR على ملفات PDF، تحميل PDF OCR، التبديل إلى وضع OCR للخط اليدوي، ثم تحسين النتائج باستخدام **نموذج OCR من Hugging Face** لتصحيح الإملاء والقواعد.

سنستعرض كل ما تحتاجه: من تثبيت Aspose OCR Cloud SDK، إلى تكوين تسريع GPU، إلى ربط نموذج Qwen الخفيف من Hugging Face. في النهاية ستحصل على سكريبت جاهز للتنفيذ يمكنك إدراجه في أي مشروع Python.

> **المتطلبات المسبقة**  
> • Python 3.9 أو أحدث  
> • رخصة Aspose OCR Cloud (محددة كمتغيّر بيئي)  
> • اختياري: GPU متوافق مع CUDA لتسريع الاستدلال  

---

## ما يغطيه هذا الدليل

- تفعيل رخصة Aspose OCR من المتغيّر البيئي  
- تحميل PDF باستخدام `load_pdf OCR` وتمكين **وضع OCR للخط اليدوي**  
- تشغيل OCR منظم للحصول على نص على مستوى الكتلة وبيانات اللغة  
- إعداد **نموذج OCR من Hugging Face** (Qwen 2.5‑3B‑Instruct) للمعالجة اللاحقة  
- تطبيق تدقيق إملائي وتصحيح نحوي كتلةً بكتلة  
- تنظيف موارد الذكاء الاصطناعي لتجنب تسرب الذاكرة  

إذا جربت محرك OCR عادي وحصلت على نص غير مفهوم في الملاحظات المكتوبة بخط اليد، فإن علمية **وضع OCR للخط اليدوي** هي ما كنت تفتقده. وبفضل نموذج Hugging Face، ستحصل أيضًا على صقل احترافي دون مغادرة بيئة Python الخاصة بك.

---

![مخطط سير عمل تشغيل OCR](https://example.com/ocr-workflow.png "مخطط سير عمل تشغيل OCR")

*نص بديل للصورة: مخطط سير عمل تشغيل OCR*

---

## الخطوة 1: تثبيت الحزم المطلوبة

أولًا، تأكد من تثبيت Aspose OCR Cloud SDK ومكتبة `transformers`. نفّذ الأمر التالي في الطرفية:

```bash
pip install aspose-ocr-cloud transformers huggingface-hub
```

> **نصيحة احترافية:** إذا كنت تخطط لاستخدام تسريع GPU، قم أيضًا بتثبيت `torch` مع دعم CUDA (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`).

---

## الخطوة 2: تفعيل رخصة Aspose OCR

تفعيل الرخصة من متغيّر بيئي يبقي مفتاحك بعيدًا عن التحكم في المصدر. عيّن `ASPOSE_OCR_LICENSE` في الصدفة، ثم استدعِ `activate_from_env()`:

```python
import asposeocrcloud as ocr

# Pull the license string from the ASPOSE_OCR_LICENSE environment variable
ocr.activate_from_env()
```

> لماذا هذا مهم: بدون رخصة صالحة يعود SDK إلى وضع التجربة الذي يحدّ من عدد الصفحات ويعطّل استخدام GPU.

---

## الخطوة 3: تهيئة محرك OCR في وضع الخط اليدوي

ننشئ `OcrEngine`، نفعّل GPU (إن وجد)، ونطلب صراحةً **وضع OCR للخط اليدوي**. هذا الوضع يضبط الشبكة العصبية الأساسية لتتعامل بشكل أفضل مع الضربات المتصلة.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Enable GPU acceleration – optional but speeds up large PDFs dramatically
ocr_engine.set_use_gpu(True)

# Switch to handwritten recognition mode for better accuracy on cursive text
ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)
```

> **ملاحظة:** إذا لم يتوفر لديك GPU، فإن `set_use_gpu(False)` سيظل يعمل؛ سيعود المحرك إلى CPU.

---

## الخطوة 4: تحميل ملف PDF وتشغيل OCR منظم

الآن نقوم فعليًا بـ **تحميل PDF OCR**. طريقة `load_image` تقبل PDF، TIFF، JPG، إلخ. يُعيد OCR المنظم كتلًا تحتوي على النص الخام واللغة المكتشفة.

```python
# Replace the path with your own PDF location
pdf_path = "YOUR_DIRECTORY/multilingual_handwritten.pdf"
ocr_engine.load_image(pdf_path)

# Perform structured OCR – returns a hierarchy of blocks
structured_result = ocr_engine.recognize_structured()
```

قائمة `structured_result.blocks` قد تبدو هكذا (مقتطف للعرض):

```python
[
    Block(text="Bonjour le monde", language="fr"),
    Block(text="Hello world", language="en"),
    Block(text="こんにちは世界", language="ja")
]
```

---

## الخطوة 5: تكوين نموذج OCR من Hugging Face للمعالجة اللاحقة

سنستخدم نموذج **Qwen 2.5‑3B‑Instruct** من Hugging Face، مُكمًّن إلى `int8` لتقليل استهلاك الذاكرة. يغلف `AsposeAIModelConfig` إعدادات تحميل وتشغيل النموذج للمعالج اللاحق من Aspose AI.

```python
from asposeocrcloud import AsposeAI, AsposeAIModelConfig

model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25,                # Number of transformer layers to keep on GPU
    allow_auto_download="true"   # Auto‑download the model if not cached
)

spell_corrector = AsposeAI()
spell_corrector.set_post_processor("spell_corrector", model_cfg)
```

> **لماذا هذا النموذج؟** يوازن Qwen 2.5‑3B‑Instruct بين السرعة والجودة. تقليل الدقة إلى `int8` يخفض استهلاك RAM إلى ~4 GB، مما يجعله مناسبًا لمعظم الحواسيب المحمولة الحديثة.

---

## الخطوة 6: تطبيق التدقيق الإملائي كتلةً بكتلة

نمر على كل كتلة OCR، نمررها إلى المعالج اللاحق للذكاء الاصطناعي، ونطبع النص المصحح مع اللغة المكتشفة. هذا هو جوهر خط أنابيب **load PDF OCR → post‑process**.

```python
for block in structured_result.blocks:
    # Run the correction; `run_postprocessor` returns an object with a .text attribute
    corrected = spell_corrector.run_postprocessor(block)
    print(f"[{block.language}] {corrected.text}")
```

### النتيجة المتوقعة

```
[fr] Bonjour le monde
[en] Hello world
[ja] こんにちは世界
```

إذا كان OCR الأصلي يحتوي على أخطاء إملائية مثل “Helllo wrold”، سيُخرج النموذج النسخة المصححة.

---

## الخطوة 7: تنظيف موارد الذكاء الاصطناعي

دائمًا حرّر ذاكرة GPU عند الانتهاء. استدعاء `free_resources()` يزيل النموذج ويُفرغ ذاكرة CUDA.

```python
spell_corrector.free_resources()
```

---

## المشكلات الشائعة وكيفية تجنّبها

| المشكلة | العَرَض | الحل |
|-------|----------|-----|
| **عدم اكتشاف GPU** | `set_use_gpu(True)` يعود صامتًا إلى CPU | تحقق من تعريفات CUDA (`nvidia-smi`) وتثبيت حزمة `torch` المناسبة |
| **فشل تحميل النموذج** | `allow_auto_download` يُظهر خطأ شبكة | تأكد من السماح بالاتصالات الصادرة عبر HTTPS، أو قم بتحميل ملف GGUF يدويًا وتوجيه `hugging_face_repo_id` إلى المسار المحلي |
| **النص المكتوب بخط اليد لا يزال مشوشًا** | درجات ثقة منخفضة في `structured_result` | زيادة `set_recognition_mode` إلى `HANDWRITTEN` (تم ذلك بالفعل) وفكّر في معالجة ما قبل OCR للـ PDF باستخدام تحسين الصورة (`opencv`) |
| **نفاد الذاكرة على GPU** | `RuntimeError: CUDA out of memory` | تقليل `gpu_layers` (مثلاً إلى 10) أو التحويل استدلال على CPU (`set_use_gpu(False)`) |

---

## توسيع سير العمل

- **المعالجة الدفعية:** غلف السكريبت بالكامل في دالة تقبل قائمة مسارات PDF وتكتب المخرجات المصححة إلى ملفات `.txt` منفصلة.  
- **قواميس مخصصة:** إذا كان مجالك يستخدم مصطلحات متخصصة (مثل الاختصارات الطبية)، قم بتدريب نموذج Hugging Face على مجموعة بيانات صغيرة.  
- **نماذج بديلة:** استبدل `Qwen/Qwen2.5-3B-Instruct-GGUF` بـ `mistralai/Mistral-7B-Instruct-v0.2` إذا كنت تحتاج إلى نافذة سياق أوسع.

---

## الخلاصة

أنت الآن تعرف **كيفية تشغيل OCR** على ملفات PDF، تحميل PDF OCR، تمكين **وضع OCR للخط اليدوي**، وتعزيز الدقة باستخدام **نموذج OCR من Hugging Face**. يغطي السكريبت الكامل—تفعيل الرخصة، محرك مدعوم بـ GPU، OCR منظم، معالجة لاحقة بالذكاء الاصطناعي، وتنظيف الموارد—كل خطوة يطرحها المطور عادةً، من “ماذا لو لم يكن لدي GPU?” إلى “كيف أحرّر الموارد؟”. 

جرّبه مع مستنداتك الخاصة، جرّب نماذج مختلفة، أو دمج الأنابيب في خدمة معالجة مستندات أكبر. السماء هي الحدّ عندما تتقن الجمع بين Aspose OCR و Hugging Face AI.

---

**الخطوات التالية**

- جرّب نفس سير العمل على الصور الممسوحة (`.png`, `.jpg`) لتلاحظ كيف يتكيف المحرك.  
- استكشف ميزات **تحليل تخطيط** Aspose OCR لاستخراج الجداول.  
- تعمّق في تقنيات تقليل حجم النماذج في Hugging Face لتصغير حجم النموذج أكثر.

تمنياتنا لك ببرمجة OCR ممتعة!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}