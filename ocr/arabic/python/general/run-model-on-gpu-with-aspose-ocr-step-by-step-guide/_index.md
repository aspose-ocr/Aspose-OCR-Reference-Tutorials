---
category: general
date: 2026-03-26
description: تشغيل النموذج على وحدة معالجة الرسومات باستخدام Aspose OCR. تعلّم كيفية
  تنزيل مستودع Hugging Face، ضبط طبقات GPU، استيراد Aspose OCR وتحميل نموذج Qwen2.5
  في دقائق.
draft: false
keywords:
- run model on gpu
- download hugging face repo
- import aspose ocr
- set gpu layers
- load qwen2.5 model
language: ar
og_description: تشغيل النموذج على وحدة معالجة الرسومات باستخدام Aspose OCR. يوضح هذا
  الدرس كيفية تنزيل مستودع Hugging Face، ضبط طبقات الـ GPU، استيراد Aspose OCR وتحميل
  نموذج Qwen2.5.
og_title: تشغيل النموذج على وحدة معالجة الرسومات باستخدام Aspose OCR – دليل كامل
tags:
- Aspose OCR
- GPU acceleration
- Hugging Face
- Python AI
title: تشغيل النموذج على وحدة معالجة الرسومات باستخدام Aspose OCR – دليل خطوة بخطوة
url: /ar/python/general/run-model-on-gpu-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل النموذج على GPU باستخدام Aspose OCR – دليل كامل

هل تساءلت يوماً كيف **run model on GPU** دون الحاجة إلى التعامل مع شفرة CUDA منخفضة المستوى؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى تسريع نموذج لغة كبير لكنهم لا يزالون يرغبون في بساطة مكتبة عالية المستوى. الخبر السار؟ Aspose OCR يأتي بمحرك AI سهل الاستخدام يمكنه سحب نموذج مباشرة من Hugging Face، وتحويله إلى صيغة مضغوطة، ونقل أول عشر طبقات إلى وحدة معالجة الرسومات الخاصة بك—كل ذلك في بضع أسطر من Python.

في هذا الدليل سنستعرض العملية بالكامل: **download Hugging Face repo**، **import Aspose OCR**، ضبط **GPU layers**، وأخيراً **load the Qwen2.5 model**. في النهاية ستحصل على محرك OCR جاهز للاستخدام يعمل بالفعل على بطاقة الرسومات الخاصة بك، وستفهم لماذا كل إعداد مهم.

## ما ستحتاجه

- Python 3.9 أو أحدث (الكود يستخدم type hints و f‑strings)
- بطاقة GPU متوافقة مع CUDA (اختياري لكن يُنصح به للسرعة)
- اتصال بالإنترنت لسحب النموذج من Hugging Face
- حزمة `asposeocr` (`pip install asposeocr`)  

لا توجد تبعيات خارجية أخرى مطلوبة—Aspose OCR يتولى كل الأعمال الثقيلة نيابةً عنك.

## الخطوة 1: تحميل مستودع Hugging Face واستيراد Aspose OCR

أول شيء يجب القيام به هو التأكد من أن ملفات النموذج متاحة محليًا. يمكن لـ `AsposeAIModelConfig` في Aspose OCR جلب المستودع تلقائيًا من Hugging Face، لذا لا تحتاج إلى استنساخ أي شيء يدويًا.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
from asposeocr import AsposeAI, AsposeAIModelConfig
```

**لماذا هذا مهم:** استيراد الحزمة يمنحك الوصول إلى فئة `AsposeAI`، التي تغلف نموذج الـ transformer الأساسي. كائن `AsposeAIModelConfig` هو المكان الذي تخبر فيه المحرك *من أين* يحصل على النموذج و*كيف* يتعامل معه (مثلًا، quantization، تخصيص GPU).

> **نصيحة احترافية:** إذا كنت خلف بروكسي مؤسسي، قم بتعيين متغير البيئة `HTTPS_PROXY` قبل تشغيل السكريبت—Aspose OCR يحترم إعدادات البروكسي القياسية في Python.

## الخطوة 2: ضبط طبقات GPU لأداء مثالي

تشغيل نموذج على GPU ليس مجرد مفتاح “تشغيل/إيقاف”. يمكنك تحديد عدد الطبقات المبكرة من الـ transformer التي تبقى على GPU بينما تعود البقية إلى CPU. هذا النهج المختلط مفيد عندما تكون ذاكرة GPU محدودة.

```python
# Step 2: Define the model configuration
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # automatically pull repo if missing
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # int8 reduces memory footprint
    gpu_layers=20                                   # first 20 layers run on GPU
)
```

**لماذا 20 طبقة؟** نموذج Qwen2.5‑3B يحتوي على 32 كتلة transformer. تخصيص أول 20 إلى GPU يمنحك زيادة ملحوظة في السرعة مع الحفاظ على استهلاك الذاكرة تحت السيطرة على بطاقة 12 GB. يمكنك تعديل `gpu_layers` وفقًا لمواصفات جهازك—تعيينه إلى `0` يجبر التنفيذ على CPU فقط، بينما `32` يحاول وضع كل شيء على GPU (قد يسبب OOM على البطاقات ذات الذاكرة المحدودة).

## الخطوة 3: إنشاء محرك AI وتحميل نموذج Qwen2.5

الآن نقوم بإنشاء المحرك ونمرره إلى التكوين الذي أعددناه للتو. استدعاء `initialize` الصريح اختياري—Aspose OCR سيقوم بالتهيئة بشكل كسول عند الاستخدام الأول—لكن استدعاؤه مسبقًا يجعل فحص الجاهزية أوضح.

```python
# Step 3: Create and initialize the AI engine with the configuration
ocr_engine = AsposeAI()
ocr_engine.initialize(model_config)   # explicit call for clarity
```

**ماذا يحدث خلف الكواليس؟**  
1. Aspose OCR يتواصل مع Hugging Face، ويحمل ملف GGUF (إذا لم يكن مخزنًا مؤقتًا).  
2. يتم تحويل الملف إلى صيغة يفهمها وقت التشغيل الداخلي.  
3. أول `gpu_layers` من الكتل تُنقل إلى ذاكرة CUDA؛ البقية تبقى على CPU.  
4. المحرك يعلّم نفسه كـ *initialized*، ويمكنك الاستعلام عن ذلك باستخدام `is_initialized()`.

## الخطوة 4: التحقق من أن النموذج جاهز للتشغيل على GPU

فحص سريع يضمن لك تجنب الأخطاء الغامضة في وقت التشغيل لاحقًا. طريقة `is_initialized()` تُعيد قيمة Boolean، مما يسمح لك بالتأكد من أن التحميل، التحويل، وتخصيص GPU نجحوا.

```python
# Step 4: Confirm that the engine is ready
print("AI ready:", ocr_engine.is_initialized())
```

عند سير الأمور بسلاسة يجب أن ترى:

```
AI ready: True
```

إذا حصلت على `False`، تحقق من أن تعريفات CUDA محدثة وأن GPU لديها ذاكرة كافية للطبقات الـ 20 التي طلبتها.

## اختياري: تشغيل استدلال OCR سريع لرؤية GPU قيد العمل

بينما يركز هذا الدليل على تحميل النموذج، سيتجه معظم القراء قريبًا لتشغيل OCR فعليًا. إليك مثالًا بسيطًا يعالج صورة محلية (`sample.png`) ويطبع النص المكتشف.

```python
# Optional: Perform a single OCR inference
image_path = "sample.png"
result = ocr_engine.recognize_image(image_path)

print("Detected text:")
print(result.text)
```

**لماذا نشغل هذا الآن؟** لأن الاستدلال الأول غالبًا ما يُفعّل تجميع JIT لنوى CUDA. إذا قست الوقت باستخدام `time.perf_counter()`، ستلاحظ أن التشغيل الثاني أسرع بكثير—دليل واضح على أن النموذج يعمل فعليًا على GPU.

## المشكلات الشائعة وكيفية إصلاحها

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| `RuntimeError: CUDA out of memory` | `gpu_layers` set too high for your card | Decrease `gpu_layers` (e.g., to 12) or switch to `int8` quantization (already done). |
| `OSError: Unable to download repository` | No internet or proxy blocking | Set `HTTPS_PROXY`/`HTTP_PROXY` env vars or download the GGUF file manually and point `hugging_face_repo_id` to a local path. |
| `AttributeError: 'AsposeAI' object has no attribute 'recognize_image'` | Using an older version of `asposeocr` | Upgrade via `pip install --upgrade asposeocr`. |
| `False` from `is_initialized()` | CUDA driver mismatch | Verify `nvidia-smi` shows the driver version compatible with your CUDA toolkit. |

## ملخص بصري

![Run model on GPU diagram](run-model-on-gpu.png "Diagram showing model download, GPU layer allocation, and inference flow")

*Alt text:* *مخطط تشغيل النموذج على وحدة معالجة الرسومات يوضح تحميل مستودع Hugging Face، تخصيص طبقات GPU، وتدفق الاستدلال.*

## خلاصة – ما أنجزناه

- **استوردنا Aspose OCR** وفئات المساعدة الخاصة بالذكاء الاصطناعي.  
- **حمّلنا مستودع Hugging Face** تلقائيًا، بفضل `allow_auto_download`.  
- **حددنا طبقات GPU** (`gpu_layers=20`) لنقل أكثر الأجزاء حسابيًا إلى بطاقة الرسومات.  
- **حمّلنا نموذج Qwen2.5‑3B‑Instruct** مع quantization إلى int8، مما قلل استهلاك الذاكرة بشكل كبير.  
- **تحققنا** من أن المحرك جاهز (`is_initialized()` تُعيد `True`).  

كل ذلك تم في أقل من 30 سطرًا من Python—بدون الحاجة إلى كتابة نوى CUDA مخصصة.

## الخطوات التالية والمواضيع ذات الصلة

1. **جرب تقنيات quantization مختلفة** (`float16`, `bfloat16`) لتقييم التوازن بين السرعة والدقة.  
2. **قم بترقية النماذج إلى أكبر حجم** (مثل Qwen2.5‑7B) عبر تعديل `gpu_layers` والتأكد من وجود VRAM كافية.  
3. **معالجة OCR على دفعات**: مرّر قائمة من مسارات الصور إلى `ocr_engine.recognize_images()` لزيادة الإنتاجية.  
4. **دمج مع FastAPI** لإنشاء نقطة نهاية REST تُجري OCR على الملفات الواردة—مثالي للخدمات المصغرة.  

إذا كنت مهتمًا بمزيد من تحسينات GPU المتقدمة، اطلع على دليل الأداء الرسمي لـ Aspose OCR أو وثائق CUDA Toolkit للمتغيرات البيئية مثل `CUDA_VISIBLE_DEVICES`.

---

*برمجة سعيدة! إذا ساعدك هذا الدليل في تشغيل نموذج على GPU، أخبرنا في التعليقات أو شارك تعديلاتك. كلما جربنا معًا، أسرع تتعلم المجتمع.*  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}