---
category: general
date: 2026-07-05
description: تعلم كيفية تحميل النموذج من Hugging Face باستخدام Aspose AI وتعيين طبقات
  GPU لتسريع الاستدلال. مثال كامل بلغة Python مع شرح خطوة بخطوة.
draft: false
keywords:
- how to load model from hugging face
- set gpu layers
- Aspose AI configuration
- Python AI inference
- Hugging Face model loading
language: ar
og_description: كيفية تحميل نموذج من Hugging Face باستخدام Aspose AI وتعيين طبقات
  GPU لأداء مثالي. اتبع هذا الدليل الكامل.
og_title: كيفية تحميل نموذج من Hugging Face باستخدام Aspose AI
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to load model from Hugging Face with Aspose AI and set GPU
    layers for faster inference. Full Python example with step‑by‑step explanation.
  headline: How to Load Model from Hugging Face with Aspose AI
  type: TechArticle
- description: Learn how to load model from Hugging Face with Aspose AI and set GPU
    layers for faster inference. Full Python example with step‑by‑step explanation.
  name: How to Load Model from Hugging Face with Aspose AI
  steps:
  - name: Create the Aspose AI configuration object
    text: '```python import aocr'
  - name: Tell Aspose AI how many layers should live on the GPU
    text: '```python # Step 2: set gpu layers – we’ll run the first 30 layers on the
      GPU cfg.gpu_layers = 30 ```'
  - name: Point to the Hugging Face repository
    text: '```python # Step 3: Specify the Hugging Face repo that holds the model
      cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF" ```'
  - name: Instantiate the Aspose AI engine
    text: '```python # Step 4: Create the engine instance ai = aocr.AsposeAI() ```'
  - name: Initialize the engine with the prepared config
    text: '```python # Step 5: Wire everything together ai.initialize(cfg) ```'
  - name: Verify that the GPU layers are active
    text: '```python # Step 6: Quick sanity check – print the active GPU layer count
      print("GPU layers active:", cfg.gpu_layers) ```'
  - name: Expected Output
    text: '``` GPU layers active: 30'
  type: HowTo
tags:
- Aspose AI
- Hugging Face
- GPU
title: كيفية تحميل نموذج من Hugging Face باستخدام Aspose AI
url: /ar/python/general/how-to-load-model-from-hugging-face-with-aspose-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحميل نموذج من Hugging Face باستخدام Aspose AI

هل تساءلت يومًا **كيفية تحميل نموذج من Hugging Face** عندما تعمل مع Aspose AI؟ لست وحدك. في العديد من المشاريع، تكون أكبر نقطة احتكاك هي جلب ذلك النموذج البعيد إلى وحدة معالجة الرسومات المحلية دون أن تشعر بالإحباط.  

في هذا الدليل سنستعرض الخطوات الدقيقة لتحميل نموذج من Hugging Face، **تعيين طبقات GPU**، والتحقق من أن كل شيء يعمل بسلاسة. في النهاية ستحصل على قطعة كود Python قابلة لإعادة الاستخدام يمكنك وضعها في أي تطبيق مدعوم بـ Aspose AI.

> **ملخص سريع:** سننشئ كائن تكوين، نوجهه إلى مستودع Hugging Face، نخبر Aspose AI بعدد الطبقات التي يجب تشغيلها على GPU، وأخيرًا نشغل المحرك. لا أسرار، فقط كود واضح.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* Python 3.8 + مثبت.
* حزمة `aocr` (Aspose OCR/AI) – تثبيت عبر `pip install aocr`.
* وحدة معالجة رسومات تدعم CUDA (اختياري ولكن يُنصح به بشدة للسرعة).
* اتصال بالإنترنت حتى يتم جلب النموذج من Hugging Face.

إذا كان أي من هذه مفقودًا، احصل عليه الآن – سيفترض باقي الدرس أنه موجود.

## كيفية تحميل نموذج من Hugging Face باستخدام Aspose AI

جوهر **كيفية تحميل نموذج من Hugging Face** يكمن في ثلاث أسطر صغيرة من الكود. لنفصلها.

### الخطوة 1: إنشاء كائن تكوين Aspose AI

```python
import aocr

# Step 1: Build a fresh configuration container
cfg = aocr.AsposeAIModelConfig()
```

*لماذا هذا مهم:* كائن `AsposeAIModelConfig` هو المصدر الوحيد للحقائق لكل ما يحتاجه المحرك – مسار النموذج، إعدادات GPU، خيارات الـ tokenizer، وما إلى ذلك. بدءًا بتكوين نظيف يمنع وجود حالة مخفية من تشغيلات سابقة.

### الخطوة 2: إخبار Aspose AI بعدد الطبقات التي يجب أن تعيش على GPU

```python
# Step 2: set gpu layers – we’ll run the first 30 layers on the GPU
cfg.gpu_layers = 30
```

هنا نقوم **بتعيين طبقات GPU**. عادةً ما تكون أول 30 طبقة من المحول هي الأكثر استهلاكًا للمعالجة، لذا نقلها إلى GPU يمنح أكبر تسريع مع إبقاء البقية على CPU للبقاء ضمن حدود VRAM.

> **نصيحة احترافية:** إذا واجهت خطأ نفاد الذاكرة، قلل هذا الرقم (مثلاً `cfg.gpu_layers = 20`). وعلى العكس، إذا كان لديك GPU قوي، يمكنك رفعه إلى `40` أو أكثر.

### الخطوة 3: توجيه إلى مستودع Hugging Face

```python
# Step 3: Specify the Hugging Face repo that holds the model
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

هذا هو قلب **كيفية تحميل نموذج من Hugging Face**. من خلال توفير معرف المستودع، سيقوم Aspose AI تلقائيًا بتحميل ملفات النموذج في المرة الأولى التي تشغل فيها السكربت، ويخزنها مؤقتًا محليًا، ويعيد استخدامها في التشغيلات اللاحقة.

> **حالة خاصة:** بعض المستودعات تتطلب مصادقة. إذا حصلت على خطأ 401، أنشئ رمزًا (Token) من Hugging Face وضعه في `cfg.hugging_face_token = "<YOUR_TOKEN>"`.

### الخطوة 4: إنشاء كائن محرك Aspose AI

```python
# Step 4: Create the engine instance
ai = aocr.AsposeAI()
```

المحرك هو البيئة التي تنفذ الاستدلال فعليًا. يبقى خفيفًا حتى تستدعي `initialize`.

### الخطوة 5: تهيئة المحرك باستخدام التكوين المُعد

```python
# Step 5: Wire everything together
ai.initialize(cfg)
```

أثناء `initialize`، يقوم Aspose AI بجلب النموذج من المستودع (إذا لزم الأمر)، ويحمل عدد الطبقات المحدد على GPU، ويستعد لتلقي الطلبات.

### الخطوة 6: التحقق من أن طبقات GPU نشطة

```python
# Step 6: Quick sanity check – print the active GPU layer count
print("GPU layers active:", cfg.gpu_layers)
```

يجب أن ترى:

```
GPU layers active: 30
```

إذا كان الرقم يطابق ما قمت بتعيينه، فقد نجحت في **تعيين طبقات GPU** والنموذج جاهز للاستدلال.

## مثال عملي كامل

فيما يلي السكربت الكامل القابل للتنفيذ الذي يجمع كل الأجزاء معًا. انسخه إلى ملف باسم `load_hf_model.py` وشغّله بالأمر `python load_hf_model.py`.

```python
import aocr

# ------------------------------------------------------------
# 1️⃣ Create configuration object
# ------------------------------------------------------------
cfg = aocr.AsposeAIModelConfig()

# ------------------------------------------------------------
# 2️⃣ Set how many layers run on the GPU
# ------------------------------------------------------------
cfg.gpu_layers = 30          # adjust based on your GPU memory

# ------------------------------------------------------------
# 3️⃣ Point to the Hugging Face repository
# ------------------------------------------------------------
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# (Optional) If your repo is private, uncomment the line below:
# cfg.hugging_face_token = "hf_XXXXXXXXXXXXXXXXXXXXXXXX"

# ------------------------------------------------------------
# 4️⃣ Create the Aspose AI engine
# ------------------------------------------------------------
ai = aocr.AsposeAI()

# ------------------------------------------------------------
# 5️⃣ Initialize with the config
# ------------------------------------------------------------
ai.initialize(cfg)

# ------------------------------------------------------------
# 6️⃣ Verify GPU layer activation
# ------------------------------------------------------------
print("GPU layers active:", cfg.gpu_layers)

# ------------------------------------------------------------
# 7️⃣ Quick inference test (optional)
# ------------------------------------------------------------
prompt = "Explain the difference between supervised and unsupervised learning."
response = ai.infer(prompt)   # returns a string with the model's answer
print("\nModel response:\n", response)
```

### النتيجة المتوقعة

```
GPU layers active: 30

Model response:
 Supervised learning uses labeled data...
```

الصياغة الدقيقة للاستجابة قد تختلف حسب نسخة النموذج، لكن السكربت يجب أن ينتهي دون رمي استثناء.

## تعيين طبقات GPU – نصائح متقدمة

بينما يعمل السطر الأساسي **set gpu layers** (`cfg.gpu_layers = 30`) في معظم الحالات، قد تواجه بعض السيناريوهات:

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **نقص VRAM** (مثلاً GPU بسعة 8 GB) | قلل `gpu_layers` إلى 20 أو أقل. |
| **وجود عدة GPUs** | استخدم `cfg.gpu_id = 1` لاستهداف الـ GPU الثاني، ثم أبقِ `gpu_layers` بأعلى مستوى تسمح به الذاكرة. |
| **الاعتماد على CPU فقط** | اضبط `cfg.gpu_layers = 0`. سيعمل المحرك بالكامل على CPU، وهو أبطأ لكنه آمن. |
| **الدقة المختلطة** | فعّل `cfg.use_fp16 = True` لتقليل استهلاك الذاكرة إلى النصف على الأجهزة الداعمة. |

هذه التعديلات تسمح لك بضبط التوازن بين السرعة واستهلاك الذاكرة.

## نظرة بصرية عامة

![How to load model from hugging face diagram](image.png)

*نص بديل:* مخطط يوضح **كيفية تحميل نموذج من Hugging Face** باستخدام Aspose AI وأماكن تطبيق طبقات GPU.

## أسئلة شائعة

**س: هل أحتاج إلى تحميل النموذج يدويًا؟**  
لا. يتولى Aspose AI عملية التحميل تلقائيًا بمجرد تزويده بمعرف المستودع.

**س: ماذا لو لم يكن تنسيق النموذج هو GGUF؟**  
يدعم Aspose AI حاليًا تنسيقي GGUF و ONNX. بالنسبة للتنسيقات الأخرى، يجب تحويلها أولاً أو استخدام محمل مختلف.

**س: هل يمكنني تغيير عدد طبقات GPU بعد التهيئة؟**  
ليس دون إعادة تهيئة المحرك. استدعِ `ai.shutdown()` (إن كان متاحًا)، عدّل `cfg.gpu_layers`، ثم شغّل `initialize` مرة أخرى.

## الخطوات التالية

الآن بعد أن عرفت **كيفية تحميل نموذج من Hugging Face** و**تعيين طبقات GPU**، قد ترغب في:

* استكشاف **الاستدلال الدفعي** لزيادة الإنتاجية.
* ربط المحرك بنقطة نهاية FastAPI لتقديم خدمات في الوقت الحقيقي.
* تجربة **النماذج الكمّية** لاستخراج أداء أكبر من VRAM المحدود.

كل من هذه المواضيع يبني على الأساس الذي غطيناه للتو، لذا ستجد الانتقال سلسًا.

## الخلاصة

لقد استعرضنا مثالًا عمليًا كاملًا حول **كيفية تحميل نموذج من Hugging Face** باستخدام Aspose AI، وأظهرنا لك بالضبط كيف **تعيين طبقات GPU** لتحقيق الأداء المثالي. السكربت جاهز للإدماج في أي مشروع، والنصائح الإضافية ستساعدك على تجنب المشكلات الشائعة.  

جرّبه الآن،

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Set Aspose OCR License and Verify It in Java](/ocr/english/java/ocr-basics/set-license/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}