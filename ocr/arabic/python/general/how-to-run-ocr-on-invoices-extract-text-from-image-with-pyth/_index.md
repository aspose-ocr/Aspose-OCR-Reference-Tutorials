---
category: general
date: 2026-01-07
description: كيفية تشغيل OCR واستخراج النص من الصورة لمعالجة الفواتير. تعلم تحسين
  دقة OCR، تحميل الصورة لـ OCR، ومعالجة OCR للفواتير بكفاءة.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: ar
og_description: كيفية تشغيل OCR على الفواتير خطوة بخطوة. استخراج النص من الصورة، تحسين
  دقة OCR، وتحميل الصورة لـ OCR باستخدام Aspose AI.
og_title: كيفية تشغيل OCR على الفواتير – دليل بايثون الكامل
tags:
- OCR
- Python
- Image Processing
title: كيفية تشغيل OCR على الفواتير – استخراج النص من الصورة باستخدام بايثون
url: /ar/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR على الفواتير – استخراج النص من الصورة باستخدام بايثون

هل تساءلت يومًا **كيفية تشغيل OCR** على فاتورة ممسوحة ضوئيًا والحصول على نص نظيف وقابل للبحث؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يكون ناتج OCR الخام مليئًا بالأخطاء الإملائية، وانقطاع أسطر، وفقدان علامات الترقيم. في هذا الدرس سنستعرض حلًا متكاملًا لا يقتصر فقط على **استخراج النص من الصورة** بل أيضًا **تحسين دقة OCR** من خلال معالجة ما بعد باستخدام نموذج Aspose AI.

سترى كيف **تحمّل صورة للـ OCR**، وتشغّل المحرك المدمج، ثم تطبق فحص إملائي خفيف يجعل النتيجة جاهزة للتحليلات اللاحقة. في النهاية ستحصل على سكريبت قابل لإعادة الاستخدام يمكن إدراجه في أي خط أنابيب لمعالجة الفواتير.

> **ما ستحتاجه**  
> * Python 3.9 أو أحدث  
> * `aspose-ocr` و `aspose-ai` (تم تثبيتها عبر `pip`)  
> * صورة فاتورة (PNG، JPEG، أو TIFF) – سنستخدم `sample_invoice.png` كمثال  
> * اختياري: وحدة معالجة رسومية (GPU) بذاكرة VRAM لا تقل عن 4 GB لتسريع استنتاج النموذج (السكريبت يعمل على CPU أيضًا)

## الخطوة 1: تثبيت الحزم المطلوبة وإعداد البيئة

قبل أن نتمكن من **تحميل الصورة للـ OCR**، يجب أن نتأكد من توفر المكتبات اللازمة. محرك Aspose OCR يأتي مع غلاف بسيط لبايثون، بينما يعتمد معالج AI ما بعد المعالجة على نموذج مُكمًّص من Hugging Face.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> نصيحة احترافية: إذا كنت تخطط لاستخدام تسريع GPU، ثبّت `torch` بدعم CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

## الخطوة 2: تحميل صورة الفاتورة

تحميل الصورة سهل، لكن يجدر الإشارة إلى سبب تعيين المسار كسلسلة خام صريحة (`r"..."`). هذا يمنع حدوث أخطاء غير مقصودة في أحرف الهروب على مسارات Windows.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*لماذا هذا مهم:* استخدام `ocr.Image.load` يضمن أن الصورة تم معالجتها مسبقًا (تحويل إلى ثنائي، تصحيح الميل) وفقًا للإعدادات الافتراضية المثلى من Aspose، والتي بالفعل **تحسن دقة OCR** قبل أي سحر AI.

## الخطوة 3: تشغيل محرك OCR المدمج

الآن نقوم فعليًا **بتشغيل OCR** والتقاط النص الخام. تُظهر هذه الخطوة النتيجة النموذجية التي ستحصل عليها من تشغيل OCR عادي — غالبًا ما تكون فوضى من فواصل الأسطر وبعض الأخطاء الإملائية.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**الناتج الخام النموذجي** (مقتطع للاختصار):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

قد تلاحظ أن كلمة “Invoice” تظهر كـ “Invo1ce” أو أن علامات الترقيم مفقودة. هنا يأتي دور معالج AI ما بعد المعالجة.

## الخطوة 4: تكوين نموذج Aspose AI

نموذج AI الذي سنستخدمه هو **Qwen2.5‑3B‑Instruct‑GGUF**، نموذج LLM خفيف مُضبط للتعليمات يعمل بسهولة على GPU متوسط المستوى. التكوين أدناه يخبر Aspose من أين يجلب النموذج، وعدد الطبقات التي تُبقى على GPU، وحجم السياق لمعالجة الفقرات الطويلة.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **لماذا هذا التكوين؟**  
> * `gpu_layers=30` يوازن بين السرعة والذاكرة — معظم الاستنتاج يحدث على الـ GPU، بينما تبقى الطبقات المتبقية على الـ CPU لتجنب أخطاء الذاكرة (OOM).  
> * `context_size=4096` يضمن أن النموذج يمكنه رؤية الفاتورة بالكامل مرة واحدة، مما يمنع تقصير الحقول المهمة.

## الخطوة 5: إنشاء معالج ما بعد المعالجة لتصحيح الإملاء بسيط

سنغلف استدعاء AI في دالة صغيرة تسمى `simple_spell_check`. الموجه (prompt) مختصر عمدًا: “Correct spelling and punctuation:” متبوعًا بالنص الخام من OCR. النموذج يُعيد نسخة مُنقّاة.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**كيف يعمل:** `ai.run_prompt` يرسل الموجه إلى الـ LLM المحمّل محليًا، ثم يُعيد سلسلة واحدة مع إملاء مصحّح، علامات ترقيم صحيحة، وتنسيق أسطر أكثر طبيعية.

## الخطوة 6: تطبيق معالج ما بعد المعالجة على النص الخام من OCR

الآن يحدث السحر. نُدخل ناتج OCR الخام إلى معالجنا ما بعد المعالجة ونطبع النتيجة المحسّ.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**نموذج للنتيجة المحسّنة**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

لاحظ تصحيح إملاء كلمة “Invoice”، واستخدام النقطتين بشكل صحيح، وتناسق فواصل الأسطر — بالضبط ما تحتاجه لتحليل موثوق في المراحل اللاحقة.

## الخطوة 7: تنظيف الموارد

كلا من محرك OCR والنموذج AI يخصصان موارد أصلية. من الممارسات الجيدة تحريرها عند الانتهاء، خاصة في الخدمات التي تعمل لفترات طويلة.

```python
ai.free_resources()
engine.dispose()
```

## السكريبت الكامل – جاهز للنسخ

فيما يلي السكريبت الكامل القابل للتنفيذ الذي يربط جميع الخطوات معًا. احفظه باسم `invoice_ocr.py`، استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على صورة الفاتورة، وشغّله باستخدام `python invoice_ocr.py`.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

شغّل السكريبت وسترى كلًا من تفريغ OCR الخام المزعج والنسخة المصقولة، **دقة OCR المحسّنة** جنبًا إلى جنب.

## الأسئلة المتكررة والحالات الخاصة

### 1. ماذا لو كانت صورة الفاتورة متعددة الصفحات (PDF)؟

يمكن لـ Aspose OCR تحميل صفحات PDF مباشرة. استبدل سطر تحميل الصورة بـ:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

قم بتكرار `page_index` لمعالجة كل صفحة على التوالي.

### 2. نفدت ذاكرة GPU — هل يمكنني استخدام CPU فقط؟

بالطبع. اضبط `gpu_layers=0` في `AsposeAIModelConfig`. سيعمل النموذج بالكامل على CPU، وهو أبطأ لكنه آمن للأجهزة منخفضة المواصفات.

### 3. كيف أتعامل مع الفواتير غير الإنجليزية؟

استبدل معرف مستودع النموذج بنموذج مخصص للغة، مثل `"mistralai/Mistral-7B-Instruct-v0.2"` لدعم متعدد اللغات. باقي خط الأنابيب يبقى دون تغيير.

### 4. هل يمكنني ربط عدة معالجات ما بعد المعالجة (مثل تنسيق التواريخ، استخراج الإجماليات)؟

نعم. `ai.set_post_processor` يقبل قائمة من الدوال القابلة للاستدعاء. على سبيل المثال:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

سيتم أولاً تصحيح الإملاء في الناتج، ثم استخراج الإجماليات.

## نصائح الأداء وأفضل الممارسات

| النصيحة | لماذا يساعد |
|-----|---------------|
| **معالجة دفعة من الفواتير** – حمّلها في قائمة وعالجها داخل حلقة. | يقلل من عبء مفسّر بايثون ويحافظ على جاهزية نموذج AI في الذاكرة. |
| **تخزين النموذج في الذاكرة المؤقتة** – تجنّب استدعاء `initialize` بشكل متكرر في خدمة ويب. | تحميل النموذج قد يستغرق ~30 ثانية؛ التخزين المؤقت يوفّر استجابات فورية. |
| **تغيير حجم الصور الكبيرة** إلى عرض 1500 بكسل قبل OCR. | الصور الأصغر تُسرّع كلًا من OCR واستنتاج AI دون التضحية بالدقة. |
| **ضبط `allow_auto_download="false"` في بيئة الإنتاج** – قم بتضمين النموذج مع عملية النشر. | يضمن أوقات بدء تشغيل محددة ويتجنّب مشاكل الشبكة. |

## الخلاصة

لقد غطينا **كيفية تشغيل OCR** على الفواتير، من تحميل الصورة إلى صقل النتيجة باستخدام فحص إملائي مدفوع بالـ AI. باتباع هذه الخطوات يمكنك بثقة **استخراج النص من الصورة**، **تحسين دقة OCR**، ومعالجة OCR للفواتير بسلاسة في أي سير عمل مبني على بايثون.

جرّبه مع عدة تنسيقات فواتير مختلفة — ربما إيصال مكتوب يدويًا أو عقد ممسوح. نفس خط الأنابيب يتكيف مع تعديلات قليلة، مما يثبت أن الجمع بين OCR و AI هو أداة متعددة الاستخدامات لأي مشروع أتمتة مستندات.

إذا وجدت هذا الدليل مفيدًا، فكر في مشاركته مع زملائك أو وضع نجمة على المستودع الذي يستضيف حزم Aspose

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}