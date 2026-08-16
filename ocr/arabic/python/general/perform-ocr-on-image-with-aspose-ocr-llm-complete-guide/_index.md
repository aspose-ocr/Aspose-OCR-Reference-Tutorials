---
category: general
date: 2026-06-06
description: قم بإجراء التعرف الضوئي على الحروف (OCR) على الصورة باستخدام Aspose OCR
  ونموذج من Hugging Face. تعلم كيفية تنزيل نموذج Hugging Face، استخراج النص من الفاتورة،
  وتحرير موارد وحدة معالجة الرسومات.
draft: false
keywords:
- perform OCR on image
- download Hugging Face model
- extract text from invoice
- free GPU resources
- load image for OCR
language: ar
og_description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على الصورة باستخدام Aspose
  OCR ونموذج Hugging Face. يوضح هذا الدرس كيفية تنزيل النموذج، استخراج النص من الفاتورة،
  وتحرير موارد وحدة معالجة الرسومات.
og_title: إجراء التعرف الضوئي على الأحرف في الصورة باستخدام Aspose OCR و LLM – دليل
  كامل
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Perform OCR on image using Aspose OCR and a Hugging Face model. Learn
    how to download Hugging Face model, extract text from invoice, and free GPU resources.
  headline: Perform OCR on Image with Aspose OCR & LLM – Complete Guide
  type: TechArticle
tags:
- OCR
- Aspose
- Python
- AI
- HuggingFace
title: إجراء التعرف الضوئي على الأحرف في الصورة باستخدام Aspose OCR و LLM – دليل شامل
url: /ar/python/general/perform-ocr-on-image-with-aspose-ocr-llm-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنفيذ OCR على الصورة باستخدام Aspose OCR و LLM – دليل كامل

هل رغبت يومًا في **perform OCR on image** للملفات لكن شعرت بالحيرة عند سؤال “من أين أبدأ؟”؟ لست وحدك—العديد من المطورين يواجهون هذا العائق عندما يتعاملون لأول مرة مع أتمتة المستندات. الخبر السار هو أنه باستخدام Aspose OCR و LLM خفيف الوزن من Hugging Face، يمكنك تحويل مسح ضوئي خام لفاتورة إلى نص نظيف وقابل للبحث في بضع أسطر من بايثون فقط.

في هذا الدرس سنستعرض كل ما تحتاجه: من **loading image for OCR**، إلى **downloading the Hugging Face model**، إلى **extracting text from invoice**، وأخيرًا **free GPU resources** حتى يبقى تطبيقك خفيفًا. بنهاية الدرس ستحصل على سكريبت مستقل يمكنك إدراجه في أي مشروع.

---

## ما ستتعلمه

- كيف تقوم بـ **perform OCR on image** باستخدام `OcrEngine` من Aspose.
- الخطوات الدقيقة لـ **download Hugging Face model** تلقائيًا.
- تقنيات لـ **extract text from invoice** من ملفات PDF أو PNG باستخدام معالجة ما بعد الذكاء الاصطناعي.
- أفضل الممارسات لـ **free GPU resources** بعد الاستدلال.
- نصائح لـ **load image for OCR** بفعالية وتجنب الأخطاء الشائعة.

لا حاجة لأي وثائق خارجية—كل ما تحتاجه موجود هنا، مع الشيفرة الكاملة، الشروحات، والناتج المتوقع.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

| المتطلب | السبب |
|-------------|--------|
| Python 3.9+ | بنية حديثة وتلميحات نوع |
| حزمة `asposeocr` (`pip install asposeocr`) | محرك OCR الأساسي |
| الوصول إلى GPU (اختياري لكن يُنصح به) | يسرّع معالج ما بعد الـ LLM |
| صورة فاتورة (`sample_invoice.png`) | حالة اختبار واقعية |

إذا كان أي من هذه غير متوفر، قم بتثبيته الآن؛ سيقوم السكريبت أيضًا **download Hugging Face model** تلقائيًا، لذا لن تحتاج للبحث عن الملفات يدويًا.

---

## الخطوة 1: Perform OCR on Image – إنشاء المحرك

أول شيء تحتاج إلى فعله هو تشغيل محرك OCR من Aspose. فكر فيه كقماش فارغ سيتحول فيه الصورة إلى نص لاحقًا.

```python
import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# Step 1: Initialize the OCR engine
engine = ocr.OcrEngine()
```

> **لماذا هذا مهم:** `OcrEngine` يختصر كل عمليات ما قبل المعالجة منخفضة المستوى، لتتمكن من التركيز على سير العمل عالي المستوى. كما يوفر طريقة `set_post_processor` التي ستسمح لنا لاحقًا بربط LLM للحصول على مخرجات أذكى.

---

## الخطوة 2: Load Image for OCR – اختيار الملف المناسب

الآن بعد أن تم إنشاء المحرك، نحتاج إلى **load image for OCR**. يدعم Aspose صيغ PNG، JPG، TIFF، وعدد قليل من الصيغ الأخرى. تأكد أن المسار إما مطلق أو نسبى لموقع السكريبت.

```python
# Step 2: Load the image you want to process
engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **نصيحة:** إذا كانت الصورة كبيرة، فكر في تصغير حجمها مسبقًا لتقليل الضغط على الذاكرة. يستطيع محرك OCR التعامل مع مسحات عالية الدقة، لكن صورة بدقة 300 DPI عادةً ما تكون مثالية للفواتير.

---

## الخطوة 3: Perform Raw OCR and View the Extracted Text

مع تحميل الصورة، يمكننا الآن **perform OCR on image** ورؤية ما ينتجه المحرك الخام. هذه الخطوة تعطيك قاعدة قبل إضافة سحر الذكاء الاصطناعي.

```python
# Step 3: Run the built‑in OCR and capture raw results
raw_result = engine.recognize()
print("Raw text:")
print(raw_result.text)
```

**الناتج المتوقع (مقتطع):**

```
Raw text:
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

غالبًا ما يحتوي الناتج الخام على فواصل أسطر، أحرف غير صحيحة، أو حقول مفقودة—وهذا بالضبط السبب في أننا سنستدعي نموذج اللغة في الخطوة التالية.

---

## الخطوة 4: Download Hugging Face Model – إعداد معالج ما بعد الـ LLM

هنا يبرز دور خطوة **download Hugging Face model**. يمكن لـ Aspose AI سحب نموذج تلقائيًا من مستودع Hugging Face إذا لم يكن موجودًا على القرص. سنستخدم نموذج Qwen2.5‑3B‑Instruct‑GGUF، الذي يوازن بين الدقة وحجم الذاكرة.

```python
# Step 4: Set up the AI model configuration
ai_cfg = AsposeAIModelConfig(
    allow_auto_download="true",               # automatically fetch model if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",         # int8 quantization cuts RAM usage dramatically
    gpu_layers=20,                            # first 20 layers run on GPU, rest on CPU
    directory_model_path="YOUR_DIRECTORY/asp_ocr_models"
)
```

> **لماذا يعمل ذلك:** `allow_auto_download` يوفر عليك تحميل ملف `.gguf` يدويًا. التقليل الكمي (`int8`) يقلل حجم النموذج إلى حوالي 3 GB، مما يجعله قابلًا للتشغيل على معظم بطاقات الرسوميات الاستهلاكية. عدّل `gpu_layers` وفقًا لمواصفات جهازك—المزيد من الطبقات على الـ GPU يعني استدلال أسرع.

---

## الخطوة 5: Extract Text from Invoice Using AI‑Enhanced Post‑Processing

الآن نرفق الـ LLM بمحرك OCR وننفذ **post‑processor** ينظف الناتج الخام، يصحح أخطاء OCR، ويُنسق حقول الفاتورة بشكل جميل.

```python
# Step 5: Initialize the AI engine and bind it to the OCR engine
ai_engine = AsposeAI()
ai_engine.initialize(ai_cfg)                 # implicit when using set_post_processor in newer versions
engine.set_post_processor(ai_engine)

# Run the AI‑enhanced post‑processor
enhanced_result = engine.run_postprocessor(raw_result)
print("\nEnhanced text:")
print(enhanced_result.text)
```

**نموذج ناتج مُحسّن:**

```
Enhanced text:
Invoice Number: 12345
Date: 2024-04-01
Bill To: Acme Corp.
Amount Due: $1,250.00
Status: Paid
```

> **ماذا حدث؟** تعرف الـ LLM أن “Invoice #12345” يجب أن تكون “Invoice Number: 12345”، صحّح تنسيق التاريخ، وحتى استنتج حقل “Bill To” الذي فاته المحرك الخام. هذا هو جوهر أتمتة **extract text from invoice**.

---

## الخطوة 6: Free GPU Resources – تنظيف بعد المعالجة

إذا كنت تشغل هذا في خدمة طويلة العمر (مثل Flask API)، يجب عليك **free GPU resources** بعد كل استدلال لتجنب تعطل الذاكرة. توفر Aspose AI طريقة مباشرة لذلك.

```python
# Step 6: Release GPU memory and dispose of the engine
ai_engine.free_resources()   # frees GPU layers and model tensors
engine.dispose()             # cleans up internal buffers
```

> **نصيحة احترافية:** استدعِ `free_resources()` داخل كتلة `finally:` إذا كنت تغلف استدعاء OCR بـ `try/except`. هذا يضمن التنظيف حتى في حال حدوث استثناء.

---

## الخطوة 7: Full Script – جمع كل الأجزاء معًا

فيما يلي السكريبت الكامل الجاهز للتنفيذ. انسخه، عدّل المسارات حسب حاجتك، وستكون جاهزًا.

```python
import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Load image for OCR
engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# 3️⃣ Raw OCR
raw_result = engine.recognize()
print("Raw text:")
print(raw_result.text)

# 4️⃣ Download Hugging Face model (auto‑download enabled)
ai_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    directory_model_path="YOUR_DIRECTORY/asp_ocr_models"
)

# 5️⃣ Attach AI post‑processor and enhance text
ai_engine = AsposeAI()
ai_engine.initialize(ai_cfg)          # optional in newer versions
engine.set_post_processor(ai_engine)

enhanced_result = engine.run_postprocessor(raw_result)
print("\nEnhanced text:")
print(enhanced_result.text)

# 6️⃣ Free GPU resources
ai_engine.free_resources()
engine.dispose()
```

شغّل السكريبت وشاهد التحول من OCR صاخب إلى بيانات فاتورة نظيفة ومهيكلة. 🎉

---

## أسئلة شائعة وحالات طرفية

| السؤال | الجواب |
|----------|--------|
| **ماذا لو فشل تحميل النموذج؟** | تأكد من أن جهازك متصل بالإنترنت وأن `hugging_face_repo_id` صحيح. يمكنك أيضًا تحميل الملف يدويًا. |
| **هل يمكن تشغيل النموذج بدون GPU؟** | نعم، لكن الأداء سيكون أبطأ؛ يمكنك ضبط `gpu_layers` إلى 0 لاستخدام CPU فقط. |
| **كيف أتعامل مع صور متعددة الصفحات؟** | كرّر عملية **load image for OCR** لكل صفحة، ثم اجمع النتائج قبل تمريرها إلى الـ LLM. |
| **هل يدعم Aspose OCR لغات أخرى؟** | يدعم العديد من اللغات؛ استخدم `set_language` لتحديد اللغة المطلوبة قبل الاستدلال. |

---

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}