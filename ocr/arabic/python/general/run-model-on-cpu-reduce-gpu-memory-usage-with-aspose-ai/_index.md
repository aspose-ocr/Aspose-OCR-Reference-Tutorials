---
category: general
date: 2026-06-22
description: شغّل النموذج على وحدة المعالجة المركزية وتعلم كيفية تقليل استهلاك ذاكرة
  وحدة معالجة الرسومات عن طريق تكوين طبقات GPU في Aspose AI. دليل خطوة بخطوة مع مقاطع
  شفرة.
draft: false
keywords:
- run model on cpu
- reduce gpu memory usage
- limit gpu layers
- configure gpu layers
language: ar
og_description: تشغيل النموذج على وحدة المعالجة المركزية وتقليل استهلاك ذاكرة وحدة
  معالجة الرسومات عن طريق تكوين طبقات الـ GPU. دليل كامل لإعداد نموذج Aspose AI.
og_title: تشغيل النموذج على وحدة المعالجة المركزية – تقليل استهلاك ذاكرة وحدة معالجة
  الرسومات
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  headline: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  type: TechArticle
- description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  name: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  steps:
  - name: Attach any required post‑processors.
    text: Attach any required post‑processors.
  - name: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
    text: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
  - name: Initialize the model with that configuration.
    text: Initialize the model with that configuration.
  - name: Verify placement and run a test inference.
    text: Verify placement and run a test inference.
  type: HowTo
tags:
- AsposeAI
- CPU inference
- GPU optimization
title: تشغيل النموذج على وحدة المعالجة المركزية – تقليل استهلاك ذاكرة وحدة معالجة
  الرسومات باستخدام Aspose AI
url: /ar/python/general/run-model-on-cpu-reduce-gpu-memory-usage-with-aspose-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل النموذج على وحدة المعالجة المركزية – تقليل استهلاك ذاكرة GPU باستخدام Aspose AI

هل تساءلت يومًا كيف **run model on CPU** عندما لا يتوفر لديك GPU في الخادم؟ أو ربما تواجه أخطاء نفاد الذاكرة على GPU محدود وتحتاج إلى **reduce GPU memory usage** دون التضحية بالكثير من السرعة. في هذا الدليل سنستعرض ذلك بالضبط: إرفاق معالج لاحق، تهيئة Aspose AI على وحدة المعالجة المركزية، وضبط عدد طبقات GPU لتقليل البصمة الذاكرية.

سنغطي كل شيء من أول سطر كود حتى التحقق من أن النموذج يستخدم فعلاً الإعدادات التي طلبتها. في النهاية ستتمكن من **run model on CPU**, **limit GPU layers**, و **configure GPU layers** لأي عبء عمل—بدون سحر، مجرد Python عادي.

## المتطلبات المسبقة

- Python 3.8+ مثبت (الكود يستخدم توجيهات النوع لكنه يعمل على الإصدارات الأقدم أيضًا)
- حزمة `asposeai` (قم بالتثبيت عبر `pip install asposeai`)
- إلمام أساسي بمفاهيم استدلال الشبكات العصبية (لا تحتاج إلى دكتوراه، فقط فضول)
- اختياري: جهاز يدعم GPU لاختبار الفرق بين تشغيلات CPU و GPU

إذا كنت تفتقد أيًا من هذه المتطلبات، قم بتثبيت الـ SDK أولًا؛ باقي الدرس يفترض أن الاستيراد يعمل.

![Diagram illustrating how to run model on cpu instead of gpu](run-model-on-cpu-diagram.png)

## الخطوة 1: إرفاق معالج التدقيق الإملائي (لا حاجة لإعدادات مخصصة)

قبل أن نفكر حتى في CPU أو GPU، لنقم بربط معالج التدقيق الإملائي الذي يأتي مع Aspose AI. من العادات الجيدة إرفاق المعالجات اللاحقة مبكرًا حتى تكون جزءًا من كل استدعاء استدلال.

```python
from asposeai import AI, spell_check_processor

# Create the AI client
ai = AI()

# Attach the built‑in spell‑check processor; no custom settings required
ai.set_post_processor(spell_check_processor, custom_settings={})
```

*لماذا هذا مهم:* المعالجات اللاحقة تعمل **بعد** أن ينتج النموذج الرموز الأولية. بربطها الآن، تضمن أن أي نص تولده لاحقًا—سواء على CPU أو GPU—سيتم تنظيفه تلقائيًا. خطوة صغيرة تمنع الأخطاء اللاحقة.

## الخطوة 2: تشغيل النموذج على وحدة المعالجة المركزية – تهيئة Aspose AI بدون GPU

الآن يأتي جوهر الدرس: إخبار Aspose AI بـ **run model on CPU**. يتيح الـ SDK الكائن `AsposeAIModelConfig`، حيث يتحكم المتغير `gpu_layers` في عدد الطبقات التي تبقى على الـ GPU. ضبطه إلى `0` يجبر الشبكة بأكملها على العمل على الـ CPU.

```python
from asposeai import AsposeAIModelConfig

# Initialize the model configuration to use zero GPU layers (i.e., CPU only)
cpu_config = AsposeAIModelConfig(gpu_layers=0)

# Apply the configuration; this will load the model onto the CPU
ai.initialize(cpu_config)

print("✅ Model initialized on CPU – ready for inference.")
```

*ما الذي يحدث خلف الكواليس؟* عندما يكون `gpu_layers=0`، يخصص وقت التشغيل جميع الـ tensors في ذاكرة المضيف. هذا يلغي الحاجة إلى تعريفات CUDA، مما يجعل السكريبت قابلًا للتشغيل على أي خادم تقريبًا. العيب هو انخفاض معدل النقل، لكن للوظائف الدُفعية أو النماذج الأولية منخفضة الكمون البساطة غالبًا ما تفوق السرعة الخام.

## الخطوة 3: تقليل طبقات GPU لتقليل استهلاك ذاكرة GPU

إذا كان لديك GPU لكنه يعاني من نقص في الذاكرة، يمكنك **limit GPU layers** بدلاً من نقل كل شيء إلى الـ CPU. بالحفاظ على عدد قليل فقط من الطبقات الأولية على الـ GPU، لا تزال تستفيد من تسريع العتاد مع تقليل استهلاك الذاكرة بشكل كبير.

```python
# Example: keep only the first 10 layers on the GPU; the rest run on CPU
limited_gpu_config = AsposeAIModelConfig(gpu_layers=10)

ai.initialize(limited_gpu_config)

print("✅ Model initialized with 10 GPU layers – memory usage trimmed.")
```

*لماذا يساعد تقليل طبقات GPU:* نماذج الـ transformer الحديثة تخصّص معظم الذاكرة لكل طبقة. حذف حتى عدد قليل من الطبقات من الـ GPU يمكن أن يحرّر مئات الميجابايت. هذه الطريقة مثالية للوظائف "المقيدة بالذاكرة" حيث لا يزال مطلوبًا تسريع للعمليات الأثقل.

## الخطوة 4: تكوين طبقات GPU لإدارة مرنة للذاكرة

أحيانًا تحتاج إلى نهج أكثر تفصيلاً—ربما تريد **configure GPU layers** بناءً على حجم المهمة المحدد. يتيح الـ SDK قراءة العدد الكلي للطبقات في النموذج وحساب عدد آمن من طبقات الـ GPU أثناء التشغيل.

```python
# Determine total number of layers (this is model‑specific; assume 36 for illustration)
total_layers = ai.model_info.total_layers  

# Choose a safe percentage, e.g., 25% of layers on GPU
gpu_layer_fraction = 0.25
desired_gpu_layers = int(total_layers * gpu_layer_fraction)

# Build the config dynamically
dynamic_config = AsposeAIModelConfig(gpu_layers=desired_gpu_layers)

ai.initialize(dynamic_config)

print(f"✅ Configured {desired_gpu_layers}/{total_layers} layers on GPU.")
```

*نصيحة محترف:* عند التشغيل على خادم مشترك، استعلم عن الذاكرة المتاحة على الـ GPU أولًا (`torch.cuda.get_device_properties(0).total_memory`) واضبط `desired_gpu_layers` وفقًا لذلك. هذه الخطوة الإضافية تضمن عدم تجاوز سعة الـ GPU، مما يمنع حدوث أعطال OOM.

## الخطوة 5: التحقق من الإعدادات واختبار الاستدلال

بعد إعداد التكوين، من الحكمة التحقق مرة أخرى من مكان وجود كل طبقة. يوفر Aspose AI طريقة تشخيصية تُعيد خريطة للطبقات والأجهزة.

```python
# Retrieve the device placement map
placement = ai.get_layer_placement()

cpu_layers = [l for l, dev in placement.items() if dev == "cpu"]
gpu_layers = [l for l, dev in placement.items() if dev == "gpu"]

print(f"Layers on CPU: {len(cpu_layers)}")
print(f"Layers on GPU: {len(gpu_layers)}")
```

بمجرد أن تكون راضيًا، شغّل استدلالًا سريعًا لترى كل شيء يعمل:

```python
input_text = "The quick brown fox jumps over the lazy dog."
output = ai.process(input_text)

print("Model output:", output)
```

إذا طبع السكريبت النص المتوقع وتطابق تقرير التوزيع مع إعداداتك، فقد نجحت في **run model on CPU**, **reduce GPU memory usage**, و **configure GPU layers** لسيناريوك.

## الأخطاء الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| `CUDA out of memory` error | عدد كبير جدًا من طبقات GPU | قلل `gpu_layers` أو غيّر إلى `gpu_layers=0` |
| لا يوجد إخراج من `ai.process` | النموذج غير مهيأ | تأكد من استدعاء `ai.initialize` **بعد** إرفاق معالجات ما بعد المعالجة |
| استدلال بطيء على GPU | جميع الطبقات لا تزال على CPU | تحقق من أن `gpu_layers` > 0 وأن خريطة الأجهزة تُظهر استخدام GPU |
| أخطاء إملائية غير متوقعة | لم يتم إرفاق معالج ما بعد المعالجة | استدعِ `set_post_processor` قبل `initialize` |

## إضافي: التبديل بين CPU و GPU أثناء التشغيل

نظرًا لأن الـ SDK يعيد تهيئة النموذج في كل مرة تستدعي فيها `initialize`، يمكنك التبديل بين CPU و GPU دون إعادة تشغيل السكريبت.

```python
def switch_to_cpu():
    ai.initialize(AsposeAIModelConfig(gpu_layers=0))
    print("🔄 Switched to CPU mode.")

def switch_to_gpu(layers=12):
    ai.initialize(AsposeAIModelConfig(gpu_layers=layers))
    print(f"🔄 Switched to GPU mode with {layers} layers.")
```

ما عليك سوى استدعاء `switch_to_cpu()` عندما تحتاج إلى تشغيل منخفض الذاكرة، و`switch_to_gpu(12)` عندما تكون مستعدًا لتسريع الأداء.

## الخلاصة

لقد استعرضنا مثالًا عمليًا كاملًا حول كيفية **run model on CPU**, **reduce GPU memory usage**, **limit GPU layers**, و **configure GPU layers** باستخدام Aspose AI. الخطوات بسيطة:

1. إرفاق أي معالجات لاحقة مطلوبة.  
2. اختيار التكوين (`gpu_layers=0` للـ CPU فقط، أو عدد معتدل للوضع المختلط).  
3. تهيئة النموذج بهذا التكوين.  
4. التحقق من توزيع الطبقات وتشغيل استدلال تجريبي.  

مع هذه التقنيات يمكنك الحفاظ على خفيفة وزن خطوط أنابيب الاستدلال، تجنب أعطال OOM المكلفة، ولا يزال بإمكانك استخراج أداء من GPU محدود عندما يكون متاحًا. بعد ذلك، قد تستكشف استراتيجيات التجميع، أو التكميم، أو حتى نقل أجزاء من النموذج إلى الـ CPU مع إبقاء رؤوس الانتباه على الـ GPU—كل هذه المواضيع تبنى مباشرة على أساس **configure GPU layers** الذي أتممته الآن.

هل لديك أسئلة حول بنية نموذج محددة أو تحتاج مساعدة في تعديل عدد الطبقات لـ

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [دروس Aspose OCR – التعرف الضوئي على الأحرف](/ocr/english/)
- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية التعرف على نص الصورة باستخدام اللغة مع Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}