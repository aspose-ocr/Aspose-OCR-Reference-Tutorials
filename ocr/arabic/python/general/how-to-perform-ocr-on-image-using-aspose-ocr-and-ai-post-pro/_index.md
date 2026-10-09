---
category: general
date: 2026-09-25
description: تعلم كيفية إجراء التعرف الضوئي على الأحرف (OCR) على صورة باستخدام Aspose
  OCR، تحميل الصورة للتعرف الضوئي على الأحرف، والتعرف على النص من الفاتورة في مثال
  كامل بلغة بايثون.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- load image for OCR
- recognize text from receipt
- Aspose OCR Python
- AI post‑processor OCR
language: ar
lastmod: 2026-09-25
og_description: قم بإجراء التعرف الضوئي على الحروف (OCR) على الصورة باستخدام Aspose
  OCR في بايثون. يوضح هذا الدليل كيفية تحميل الصورة للتعرف الضوئي على الحروف واستخراج
  النص من الإيصال مع تحسين الذكاء الاصطناعي.
og_image_alt: Screenshot of Python code performing OCR on an image and showing original
  vs AI‑enhanced text
og_title: إجراء التعرف الضوئي على الأحرف (OCR) على الصورة باستخدام Aspose OCR ومعالج
  ما بعد الذكاء الاصطناعي – دليل بايثون
schemas:
- author: Aspose
  dateModified: '2026-09-25'
  description: Learn how to perform OCR on image with Aspose OCR, load image for OCR,
    and recognize text from receipt in a complete Python example.
  headline: How to perform OCR on image using Aspose OCR and AI post‑processor in
    Python
  type: TechArticle
tags:
- OCR
- Python
- Aspose
title: كيفية تنفيذ OCR على صورة باستخدام Aspose OCR ومعالج ما بعد الذكاء الاصطناعي
  في بايثون
url: /ar/python/general/how-to-perform-ocr-on-image-using-aspose-ocr-and-ai-post-pro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إجراء OCR على صورة باستخدام Aspose OCR ومعالج ما بعد المعالجة بالذكاء الاصطناعي في بايثون

إذا كنت بحاجة إلى **إجراء OCR على ملفات الصور** في بايثون، فإن هذا الدليل يوضح لك حلًا كاملًا وجاهزًا للتنفيذ. ستتعلم كيفية **تحميل الصورة للـ OCR**، تشغيل محرك Aspose OCR، و**استخراج النص من إيصالات** مع معالجة ما بعد المعالجة المدعومة بالذكاء الاصطناعي (اختياري).

سنمرّ بكل خطوة، من تثبيت الـ SDK إلى تحرير الموارد، حتى تتمكن من دمج استخراج النص الموثوق به في تطبيقاتك دون فقدان أي تفاصيل.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

- تثبيت Python 3.8+  
- Aspose OCR for Python عبر pip (`pip install aspose-ocr`)  
- اتصال بالإنترنت لتنزيل نموذج الذكاء الاصطناعي الاختياري  
- صورة إيصال تجريبية (`receipt.png`) موجودة في مسار معروف  

لا توجد خدمات خارجية إضافية مطلوبة؛ الكود يعمل محليًا ويستخدم نموذج Qwen2‑3B‑Instruct المجاني عندما تكون طبقات GPU متاحة.

## الخطوة 1: تثبيت الحزم المطلوبة

```bash
pip install aspose-ocr
```

حزمة `aspose-ocr` تحتوي على كل من الفئة `OcrEngine` ومعالج ما بعد المعالجة `AsposeAI` الذي سنستخدمه **لإجراء OCR على صورة**.

## الخطوة 2: إنشاء وتكوين محرك OCR – تحميل الصورة للـ OCR

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # <-- load image for OCR
```

استدعاء `load_image` يخبر المحرك بأي ملف يجب تحليله. يمكنك استبدال المسار بأي ملف PNG أو JPG أو TIFF تحتاج إلى **إجراء OCR على صورة** له.

## الخطوة 3: إعداد معالج AsposeAI الاختياري ما بعد المعالجة

معالج ما بعد المعالجة بالذكاء الاصطناعي يمكنه تصحيح الأخطاء الإملائية، تحسين التنسيق، أو تطبيق منطق مخصص بعد إرجاع نتيجة الـ OCR الخام.

```python
from aspose.ocr import AsposeAI, AsposeAIModelConfig

# Initialise the AI processor (logging is optional)
ai_processor = AsposeAI()   # AsposeAI(logging=my_logger)

# Define which model to use – it will auto‑download if missing
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20                     # use GPU layers when available
)

# Load the model configuration into the processor
ai_processor.initialize(model_config)   # implicit in many examples
```

التكوين يوجه المعالج لتنزيل نموذج Qwen2 الافتراضي، مما يتيح لك **إجراء OCR على صورة** مع فهم لغوي أعلى مستوى.

## الخطوة 4: إرفاق دالة معالجة ما بعد بسيطة

يمكنك ربط أي دالة قابلة للاستدعاء تستقبل النص الخام وتعيد نسخة مصححة. إليك مثالًا بسيطًا يصلح خطأ إملائي شائع:

```python
def simple_spell_check(text, **kwargs):
    """Correct a frequent misspelling in receipt OCR results."""
    return text.replace("reciept", "receipt")

# Register the function with the AI processor
ai_processor.set_post_processor(simple_spell_check, {})
```

نظرًا لأن الدالة مسجلة، في كل مرة تستدعي فيها `run_postprocessor` ستمر مخرجات الـ OCR عبر هذه الخطوة.

## الخطوة 5: تشغيل OCR وتحسين النتيجة – استخراج النص من الإيصال

```python
# Perform the core OCR operation
raw_result = ocr_engine.recognize()          # <-- recognize text from receipt

# Let the AI processor improve the raw output
enhanced_result = ai_processor.run_postprocessor(raw_result)

# Display both versions
print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)
```

استدعاء `recognize` يُعيد كائنًا يحتوي على الخاصية `text` التي تضم الأحرف الخام المستخرجة من صورة الإيصال. الاستدعاء اللاحق لـ `run_postprocessor` يُعيد نتيجة جديدة تم فيها تطبيق تصحيح الإملاء (وأي تحسينات مستندة إلى النموذج).

### النتيجة المتوقعة

```
Original OCR : Total: $23.45\nSubtotl: $20.00\nTax: $3.45\nThank you for your reciept
AI‑enhanced  : Total: $23.45
Subtotal: $20.00
Tax: $3.45
Thank you for your receipt
```

لاحظ كيف أن النص المحسن بالذكاء الاصطناعي يصلح الخطأ الإملائي ويضيف فواصل أسطر لسهولة القراءة—بالضبط ما تحتاجه عندما **تستخرج النص من إيصالات**.

## الخطوة 6: تحرير الموارد

```python
# Release memory held by the AI processor
ai_processor.free_resources()

# Dispose of the OCR engine
ocr_engine.dispose()
```

تحرير الموارد أمر مهم خاصةً عند معالجة العديد من الصور في خدمة طويلة التشغيل.

## البرنامج الكامل القابل للتنفيذ

جمع جميع الأجزاء معًا يمنحك سكريبتًا واحدًا يمكنك نسخه، لصقه، وتنفيذه:

```python
# ocr_receipt.py
from aspose.ocr import AsposeAI, AsposeAIModelConfig, OcrEngine

# 1️⃣ Initialise OCR engine and load the image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # load image for OCR

# 2️⃣ Set up optional AI post‑processor
ai_processor = AsposeAI()
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20
)
ai_processor.initialize(model_config)

# 3️⃣ Register a simple spell‑check function
def simple_spell_check(text, **kwargs):
    return text.replace("reciept", "receipt")
ai_processor.set_post_processor(simple_spell_check, {})

# 4️⃣ Perform OCR and enhance the result
raw_result = ocr_engine.recognize()                # recognize text from receipt
enhanced_result = ai_processor.run_postprocessor(raw_result)

print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)

# 5️⃣ Release resources
ai_processor.free_resources()
ocr_engine.dispose()
```

شغّل السكريبت باستخدام:

```bash
python ocr_receipt.py
```

يجب أن ترى المخرجات الأصلية والمُحسّنة بالذكاء الاصطناعي مطبوعةً في وحدة التحكم.

## نصائح احترافية ومخاطر شائعة

- **جودة الصورة مهمة** – تأكد من أن صورة الإيصال مضاءة جيدًا وغير مضغوطة بشكل مفرط؛ وإلا قد يفوت محرك OCR بعض الأحرف، مما يقلل فائدة ما بعد المعالجة.  
- **توفر GPU** – إذا لم يكن جهازك يحتوي على GPU متوافق، اضبط `gpu_layers=0` لإجبار الاستدلال على CPU؛ سيظل النموذج يعمل، لكن بأداء أبطأ.  
- **معالجات ما بعد المعالجة المخصصة** – يمكنك ربط عدة دوال أو استخدام نموذج لغة أكثر تعقيدًا لإعادة تنسيق التواريخ، المبالغ، أو أسماء البائعين.  
- **المعالجة الدفعية** – أنشئ كائن `AsposeAI` واحدًا وأعد استخدامه عبر العديد من مثيلات `OcrEngine` لتجنب تنزيل النموذج مرارًا وتكرارًا.  

## الخلاصة

أنت الآن تعرف كيفية **إجراء OCR على صورة** باستخدام Aspose OCR، وكيفية **تحميل الصورة للـ OCR**، وكيفية **استخراج النص من إيصال** مع تحسينات مدفوعة بالذكاء الاصطناعي. باتباع الخطوات أعلاه، يمكنك دمج معالجة إيصالات دقيقة وعالية الإنتاجية في أي تطبيق بايثون.

**الخطوات التالية**: استكشف تقنيات ما بعد المعالجة الإضافية مثل تطبيع العملات، دمج النتيجة في قاعدة بيانات، أو الانتقال إلى نموذج أكبر لمعالجة إيصالات متعددة اللغات. للمزيد من التخصيص المتعمق، راجع وثائق Aspose OCR حول حزم اللغات المخصصة ومعالجة الصور المتقدمة مسبقًا.

برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Perform OCR in C# – Extract Text from Image Using Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}