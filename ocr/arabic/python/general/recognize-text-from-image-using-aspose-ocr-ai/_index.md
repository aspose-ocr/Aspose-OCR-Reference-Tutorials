---
category: general
date: 2026-06-06
description: التعرف على النص من الصورة باستخدام Aspose OCR – تعلم كيفية تحميل الصورة
  للتعرف الضوئي على الحروف وتنفيذ التعرف الضوئي على الحروف على الصورة باستخدام المعالجة
  اللاحقة بالذكاء الاصطناعي في بايثون.
draft: false
keywords:
- recognize text from image
- perform ocr on image
- load image for ocr
language: ar
og_description: التعرف على النص من الصورة بسرعة. يوضح هذا الدليل كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف، إجراء التعرف الضوئي على الأحرف على الصورة، وتعزيز النتائج
  باستخدام المعالجة اللاحقة بالذكاء الاصطناعي.
og_title: التعرف على النص من الصورة باستخدام Aspose OCR والذكاء الاصطناعي
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text from image with Aspose OCR – learn how to load image
    for OCR and perform OCR on image using AI post‑processing in Python.
  headline: recognize text from image using Aspose OCR & AI
  type: TechArticle
- description: recognize text from image with Aspose OCR – learn how to load image
    for OCR and perform OCR on image using AI post‑processing in Python.
  name: recognize text from image using Aspose OCR & AI
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer - `asposeocr` package (`pip install asposeocr`) -
      An image file (e.g., `doc.png`) that contains printed or handwritten text -
      Optional: a GPU for faster LLM inference (the script works on CPU too)'
  - name: Install and import the required modules
    text: '```python # Install the library (run once in your environment) # pip install
      asposeocr'
  - name: Create the OCR engine and enable handwritten text recognition
    text: '```python # Initialise the OCR engine ocr_engine = ocr.OcrEngine()'
  - name: Load the image for OCR
    text: '```python # Point the engine at the file you want to process ocr_engine.load_image("YOUR_DIRECTORY/doc.png")
      ```'
  - name: Run the raw OCR pass
    text: '```python # Execute the recognition pipeline and capture the raw result
      raw_result = ocr_engine.recognize() ```'
  - name: Configure the Aspose AI model for LLM post‑processing
    text: '```python ai_config = AsposeAIModelConfig( allow_auto_download="true",
      # Pull the model if missing hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
      hugging_face_quantization="int8", # Reduce RAM usage gpu_layers=20, # Use 20
      GPU layers if a GPU is present directory_model_path="YOUR_DIRECTORY/mo'
  - name: Initialise the AI processor and attach it as a post‑processor
    text: '```python # Instantiate the AI processor with the configuration above ai_processor
      = AsposeAI() ai_processor.initialize(ai_config)'
  - name: Run the post‑processor to enhance the OCR output
    text: '```python # Apply AI‑driven post‑processing enhanced_result = ocr_engine.run_postprocessor(raw_result)'
  - name: Release resources
    text: '```python # Free GPU/CPU memory held by the AI model ai_processor.free_resources()'
  type: HowTo
- questions:
  - answer: No. The script falls back to CPU, but inference will be slower.
    question: Do I need a GPU?
  - answer: Absolutely—just change `hugging_face_repo_id` and adjust `gpu_layers`
      accordingly.
    question: Can I use a different LLM?
  - answer: Resize it first (e.g., using Pillow) to keep memory usage reasonable.
    question: What if my image is huge?
  - answer: You can toggle `enable_handwritten_recognition` depending on your workload.
    question: Is handwritten recognition always on?
  type: FAQPage
tags:
- OCR
- Aspose
- Python
title: التعرف على النص من الصورة باستخدام Aspose OCR والذكاء الاصطناعي
url: /ar/python/general/recognize-text-from-image-using-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة باستخدام Aspose OCR & AI

هل احتجت يوماً إلى التعرف على النص من صورة لكنك لم تكن متأكدًا أي مكتبة ستوفر لك السرعة والدقة معًا؟ لست وحدك. في هذا الدليل سنستعرض مثالًا كاملاً من البداية إلى النهاية يوضح **كيفية تحميل الصورة للـ OCR**، **إجراء الـ OCR على الصورة**، ثم تحسين النتيجة باستخدام معالج Aspose AI. في النهاية ستحصل على سكريبت جاهز للتنفيذ يحول ملف PNG إلى نص نظيف وقابل للبحث.

## ما ستتعلمه

سنغطي كل شيء بدءًا من تثبيت حزمة Aspose OCR حتى تحرير الموارد في نهاية التنفيذ. ستعرف لماذا يهم تمكين التعرف على النص المكتوب يدويًا، وكيفية ضبط نموذج Qwen 2.5 LLM للمعالجة اللاحقة، وما هو شكل المخرجات النهائية. لا تحتاج إلى مراجع خارجية—فقط انسخ، الصق، وشغّل.

### المتطلبات المسبقة

- Python 3.8 أو أحدث  
- حزمة `asposeocr` (`pip install asposeocr`)  
- ملف صورة (مثال: `doc.png`) يحتوي على نص مطبوع أو مكتوب يدويًا  
- اختياري: وحدة معالجة رسومية (GPU) لتسريع استدلال الـ LLM (السكريبت يعمل على CPU أيضًا)

---

## التعرف على النص من الصورة – خطوة بخطوة

أسفل كل كتلة شفرة ستجد شرحًا قصيرًا **لماذا** نقوم بهذا الإجراء، وليس مجرد **ماذا** تفعل السطر.

### الخطوة 1: تثبيت واستيراد الوحدات المطلوبة

```python
# Install the library (run once in your environment)
# pip install asposeocr

import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig
```

*لماذا؟* استيراد `asposeocr` يزودنا بفئة `OcrEngine`، بينما يوفر الموديل الفرعي `ai` معالجًا قائمًا على الـ LLM يحسن بشكل كبير مخرجات الـ OCR الخام.

### الخطوة 2: إنشاء محرك OCR وتمكين التعرف على النص المكتوب يدويًا

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Turn on handwritten‑text support – useful for notes, signatures, etc.
ocr_engine.ocr_settings.enable_handwritten_recognition = True
```

تمكين التعرف على النص المكتوب يدويًا يوسع مجموعة الأحرف في المحرك، لذا لن تفقد الكتابات المتعرجة عندما **تجري OCR على ملفات الصور** التي تحتوي على نص مطبوع ومكتوب يدويًا معًا.

### الخطوة 3: تحميل الصورة للـ OCR

```python
# Point the engine at the file you want to process
ocr_engine.load_image("YOUR_DIRECTORY/doc.png")
```

استدعاء `load_image` هو اللحظة التي **تحمل فيها الصورة للـ OCR**؛ إذا كان المسار غير صحيح، سيطرح المحرك استثناءً توضيحيًا، مما يحفظك من أخطاء غامضة لاحقًا.

### الخطوة 4: تشغيل مرحلة الـ OCR الخام

```python
# Execute the recognition pipeline and capture the raw result
raw_result = ocr_engine.recognize()
```

في هذه المرحلة تحصل على كائن `RecognitionResult` يحتوي على النص غير المصفى، درجات الثقة، وبيانات تخطيط الصفحة. غالبًا ما يكون النص مشوشًا—ولهذا نحتاج إلى التنظيف المدعوم بالذكاء الاصطناعي.

### الخطوة 5: ضبط نموذج Aspose AI للمعالجة اللاحقة باستخدام LLM

```python
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # Pull the model if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Reduce RAM usage
    gpu_layers=20,                                  # Use 20 GPU layers if a GPU is present
    directory_model_path="YOUR_DIRECTORY/models/ocr_ai"
)
```

لماذا نهتم بهذه الإعدادات؟  
- **auto‑download** يضمن توفر النموذج عند أول تشغيل.  
- **int8 quantization** يقلل استهلاك الذاكرة دون خسارة كبيرة في الدقة.  
- **gpu_layers** يسمح لك بالاستفادة من GPU متوافق لتسريع الاستدلال.

### الخطوة 6: تهيئة معالج AI وربطه كمعالج لاحق

```python
# Instantiate the AI processor with the configuration above
ai_processor = AsposeAI()
ai_processor.initialize(ai_config)

# Hook the AI processor into the OCR engine
ocr_engine.set_post_processor(ai_processor, None)
```

ربط المعالج يعني أنه في كل مرة تستدعي فيها `run_postprocessor`، سيقوم الـ LLM بتنظيف الإملاء، دمج الكلمات المتقطعة، وحتى استنتاج علامات الترقيم المفقودة.

### الخطوة 7: تشغيل المعالج اللاحق لتحسين مخرجات الـ OCR

```python
# Apply AI‑driven post‑processing
enhanced_result = ocr_engine.run_postprocessor(raw_result)

# Print the polished text
print(enhanced_result.text)
```

عادةً ما يكون `enhanced_result.text` أكثر قابلية للقراءة من السلسلة الخام—فكر فيه كمدقق إملائي يفهم السياق أيضًا.

### الخطوة 8: تحرير الموارد

```python
# Free GPU/CPU memory held by the AI model
ai_processor.free_resources()

# Dispose of the OCR engine to close file handles, etc.
ocr_engine.dispose()
```

تنظيف الموارد أمر حاسم في الخدمات طويلة التشغيل؛ وإلا ستسرب ذاكرة الـ GPU وتتعرض لتعطل التطبيق في النهاية.

---

## السكريبت الكامل الذي يمكنك تشغيله اليوم

```python
import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Initialise OCR engine with handwritten support
ocr_engine = ocr.OcrEngine()
ocr_engine.ocr_settings.enable_handwritten_recognition = True

# 2️⃣ Load the image you want to analyse
ocr_engine.load_image("YOUR_DIRECTORY/doc.png")   # <-- replace with your path

# 3️⃣ Perform the basic OCR pass
raw_result = ocr_engine.recognize()

# 4️⃣ Set up the AI model for smarter output
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    directory_model_path="YOUR_DIRECTORY/models/ocr_ai"
)

# 5️⃣ Initialise and attach the AI post‑processor
ai_processor = AsposeAI()
ai_processor.initialize(ai_config)
ocr_engine.set_post_processor(ai_processor, None)

# 6️⃣ Enhance the OCR result with the LLM
enhanced_result = ocr_engine.run_postprocessor(raw_result)

# 7️⃣ Show the final, cleaned‑up text
print("=== Enhanced OCR Output ===")
print(enhanced_result.text)

# 8️⃣ Clean up
ai_processor.free_resources()
ocr_engine.dispose()
```

**المخرجات المتوقعة** (مثال على صورة فاتورة بسيطة):

```
=== Enhanced OCR Output ===
Invoice #12345
Date: 2024‑04‑01
Total Amount: $1,250.00
Thank you for your business!
```

لاحظ كيف صحّح طبقة AI كلمة “Inv0ice” → “Invoice” وأضاف علامات الترقيم المفقودة.

---

## الأسئلة المتكررة (وأجوبة سريعة)

- **هل أحتاج إلى GPU؟** لا. السكريبت ينتقل إلى CPU إذا لم يتوفر GPU، لكن الاستدلال سيكون أبطأ.  
- **هل يمكنني استخدام نموذج LLM مختلف؟** بالطبع—فقط غيّر `hugging_face_repo_id` واضبط `gpu_layers` وفقًا لذلك.  
- **ماذا لو كانت صورتي ضخمة؟** قم بتصغيرها أولًا (مثلاً باستخدام Pillow) لتقليل استهلاك الذاكرة.  
- **هل التعرف على النص المكتوب يدويًا مفعل دائمًا؟** يمكنك تشغيل أو إيقاف `enable_handwritten_recognition` حسب احتياجاتك.

---

## الخلاصة

أصبحت الآن تعرف كيف **تتعرف على النص من الصورة** باستخدام Aspose OCR، وكيف **تحمل الصورة للـ OCR**، وكيف **تجري OCR على الصورة** مع معالجة لاحقة محسنة بالذكاء الاصطناعي. المثال الكامل القابل للتنفيذ أعلاه يمنحك أساسًا قويًا لدمج OCR في أي مشروع بايثون—سواء كان مسح إيصالات، رقمنة عقود، أو استخراج بيانات من نماذج مكتوبة يدويًا.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال نموذج Qwen بنموذج أكبر، جرب مخططات تقليل مختلفة، أو ربط عدة صور معًا للمعالجة الدفعة. الاحتمالات لا حصر لها، والكود الذي أنشأته سيتعامل معها بسلاسة.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالكريستال!  

![Screenshot of Python console showing enhanced OCR output](/images/ocr_output.png){alt="لقطة شاشة تُظهر كيفية التعرف على النص من الصورة باستخدام Aspose OCR"}

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [تحويل الصورة إلى نص – إجراء OCR على صورة من URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [استخراج نص الصورة بلغة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}