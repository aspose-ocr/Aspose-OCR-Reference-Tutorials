---
category: general
date: 2026-07-18
description: تشغيل التعرف الضوئي على الأحرف على الصورة باستخدام Aspose OCR في بايثون.
  تعلم استخراج النص العادي من الصورة، تطبيق المعالجة اللاحقة بالذكاء الاصطناعي، والحصول
  على نتائج نظيفة بسرعة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract plain text from image
- Aspose OCR Python
- AI post‑processor OCR
- image text extraction
language: ar
lastmod: 2026-07-18
og_description: قم بتشغيل OCR على الصورة باستخدام Aspose OCR وPython. يوضح هذا الدليل
  كيفية استخراج النص العادي من الصورة وتعزيز الدقة باستخدام معالج ما بعد الذكاء الاصطناعي.
og_image_alt: Screenshot showing run OCR on image results in Python console
og_title: تشغيل OCR على الصورة – دليل بايثون كامل مع Aspose AI
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Run OCR on image using Aspose OCR in Python. Learn to extract plain
    text from image, apply AI post‑processing, and get clean results fast.
  headline: Run OCR on Image with Aspose AI – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI
title: تشغيل OCR على الصورة باستخدام Aspose AI – دليل بايثون كامل
url: /ar/python/general/run-ocr-on-image-with-aspose-ai-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على صورة باستخدام Aspose AI – دليل Python كامل

هل تساءلت يومًا كيف **تشغل OCR على صورة** دون الحاجة إلى التعامل مع واجهات برمجة تطبيقات منخفضة المستوى؟ لست وحدك. في العديد من المشاريع—معالجة الفواتير، مسح الإيصالات، أو رقمنة المستندات القديمة—الحصول على نص نظيف وقابل للبحث من صورة هو الخطوة الأولى، وغالبًا الأصعب.

في هذا الدليل سنستعرض مثالًا عمليًا لا يقتصر فقط على **تشغيل OCR على صورة** بل يوضح أيضًا كيفية **استخراج نص عادي من صورة** باستخدام محرك OCR من Aspose، ثم تحسين النتيجة بمعالج AI صغير. بنهاية الدليل ستحصل على سكريبت جاهز للتنفيذ، وفهم واضح لكل جزء، وبعض النصائح لتجنب المشكلات الشائعة.

![Run OCR on Image example](/images/run-ocr-on-image.png){: .align-center alt="مخرجات وحدة التحكم لتشغيل OCR على صورة تُظهر النص الأصلي والنص المحسن بالذكاء الاصطناعي"}

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

- Python 3.8+ مثبت (الكود يعمل على Windows، macOS، وLinux).
- رخصة نشطة لـ Aspose OCR for Python أو تجربة مجانية (الحزمة هي `aspose-ocr` على PyPI).
- ملف صورة تجريبي (مثل فاتورة أو إيصال ممسوح) محفوظ محليًا.
- اختياري: جهاز يدعم GPU إذا كنت تخطط لتغيير إعداد `gpu_layers` لاحقًا.

هذا كل ما تحتاجه—بدون محركات OCR ثقيلة، دون استدعاءات سحابية خارجية، مجرد تثبيت واحد عبر pip وعدة أسطر من الكود.

## الخطوة 1: تثبيت حزمة Aspose OCR

افتح الطرفية واكتب:

```bash
pip install aspose-ocr
```

الحزمة تجلب محرك OCR الأساسي بالإضافة إلى مساحة الاسم الخفيفة `aspose.ocr` التي سنستخدمها طوال الدليل.

## الخطوة 2: استيراد الفئات المطلوبة

نبدأ باستيراد الفئتين الرئيسيتين: `AsposeAI` للمعالجة اللاحقة المدعومة بالذكاء الاصطناعي و`OcrEngine` لاستخراج النص الفعلي.

```python
# Step 1: Import required classes
from aspose.ocr import AsposeAI, OcrEngine
```

*لماذا هذا مهم*: `OcrEngine` يتولى الجزء الثقيل من التعرف على الحروف، بينما يتيح لنا `AsposeAI` ربط منطق مخصص—مثل تحويل كل كلمة إلى حرف كبير—دون الحاجة لإعادة كتابة نواة OCR.

## الخطوة 3: إنشاء كائن AsposeAI (مسجل اختياري)

إذا رغبت في سجل تفصيلي يمكنك تمرير مسجل مخصص، لكن الإعداد الافتراضي يكفي في معظم الحالات.

```python
# Step 2: Create an AsposeAI instance (optional custom logger can be supplied)
ai = AsposeAI()
```

## الخطوة 4: تعديل النموذج الأساسي (اختياري)

تأتي Aspose OCR بنموذج لغة افتراضي، لكن يمكنك توجيهه إلى مستودع HuggingFace أو إجبار التنفيذ على CPU. أدناه نفعّل التحميل التلقائي ونختار النموذج الصغير `gpt2`—فقط لتوضيح الخيارات المتاحة.

```python
# Step 3: (Optional) Adjust the underlying model configuration
ai.config.allow_auto_download = "true"          # permit automatic model download
ai.config.hugging_face_repo_id = "openai/gpt2"   # specify the HuggingFace model
ai.config.gpu_layers = 0                        # force CPU execution
```

> **نصيحة محترف:** إذا كان لديك GPU يدعم CUDA، زد قيمة `gpu_layers` إلى `1` أو `2` للحصول على تسريع ملحوظ.

## الخطوة 5: تسجيل معالج ما بعد بسيط

هدفنا هو **استخراج نص عادي من صورة** ثم تحسين مظهره. إليك دالة صغيرة تحول كل كلمة إلى حرف كبير. يمكنك استبدالها بتصحيح إملائي، كشف لغة، أو حتى استدعاء نموذج LLM كامل.

```python
# Step 4: Register a simple post‑processor that capitalizes each word
def capitalize_words(text, settings):
    """Capitalize every word in the OCR output."""
    return " ".join(word.capitalize() for word in text.split())

# Attach the processor to the AsposeAI instance
ai.set_post_processor(capitalize_words, custom_settings={})
```

القاموس `custom_settings` يتيح لك تمرير معلمات إضافية لاحقًا—مفيد عندما تطور المعالج.

## الخطوة 6: تحميل صورة وتشغيل OCR

الآن نصل أخيرًا إلى **تشغيل OCR على صورة**. سنستخرج نوعين من المخرجات:

1. **نص عادي** – سلسلة خام بدون معلومات تخطيط.
2. **نص منظم** – يحافظ على التخطيط، بما في ذلك الأعمدة والجداول.

```python
# Step 5: Load an image and obtain OCR results (plain and layout‑aware)
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()                     # raw text
structured_text = ocr_engine.recognize_structured()    # layout‑aware text
```

> **لماذا كلاهما؟** `plain_text` مثالي للبحث السريع، بينما `structured_text` يبرز عندما تحتاج إلى إعادة بناء الجداول أو الحفاظ على محاذاة الأعمدة.

## الخطوة 7: تحسين مخرجات OCR باستخدام معالج AI ما بعد

مع نتائج OCR في يدنا، نمررها إلى `AsposeAI.run_postprocessor`. هنا يتم تشغيل الدالة `capitalize_words` التي عرفناها سابقًا.

```python
# Step 6: Enhance the OCR outputs using the AI post‑processor
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)
```

إذا قررت لاحقًا استبدال معالج ما بعد بـ شيء أكثر تعقيدًا—مثل مصحح قواعد—فقط استبدل الدالة في الخطوة 5 وستظل بقية الخطوات كما هي.

## الخطوة 8: عرض النتائج

دعنا نطبع كل شيء جنبًا إلى جنب لتتمكن من مقارنة OCR الخام مع النسخة المحسنة بالذكاء الاصطناعي.

```python
# Step 7: Display original and enhanced texts
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)
```

### المخرجات المتوقعة

```
Original plain text: invoice #12345 date 01/02/2024 total $123.45
AI‑enhanced plain text: Invoice #12345 Date 01/02/2024 Total $123.45

Original structured text: invoice #12345
date 01/02/2024
total $123.45
AI‑enhanced structured text: Invoice #12345
Date 01/02/2024
Total $123.45
```

لاحظ كيف حول معالج AI ما بعد الكلمات كلها بأحرف صغيرة إلى أحرف كبيرة، مما جعل النص أكثر قابلية للقراءة. يمكنك تطبيق أي تحويل تريده—هذا مجرد إثبات مفهوم.

## الخطوة 9: تنظيف الموارد

يقوم Aspose بتحميل ملفات نماذج ضخمة في الذاكرة. عند الانتهاء، حرّرها لتجنب تسرب الذاكرة، خاصة في الخدمات طويلة التشغيل.

```python
# Step 8: Release model resources when done
ai.free_resources()
```

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني تشغيل OCR على عدة صور داخل حلقة؟** | بالتأكيد. أنشئ كائن `OcrEngine` مرة واحدة، استدعِ `load_image` داخل الحلقة، وأعد استخدام نفس كائن `AsposeAI` للمعالجة اللاحقة. |
| **ماذا لو كانت الصورة منخفضة الدقة؟** | عالجها مسبقًا باستخدام OpenCV (مثلاً `cv2.resize` و `cv2.threshold`) قبل تمريرها إلى `OcrEngine`. |
| **هل أحتاج إلى GPU؟** | ليس ضروريًا. وضع CPU الافتراضي يعمل جيدًا لمعظم المستندات. اضبط `ai.config.gpu_layers` > 0 فقط إذا كان لديك GPU متوافق وتحتاج إلى سرعة أعلى. |
| **كيف أستخرج نص عادي من صورة بلغات أخرى؟** | غيّر `ocr_engine.language = "fr"` (أو أي رمز ISO‑639‑1) قبل استدعاء `recognize`. سيستمر المعالج اللاحق في العمل، لكن قد تحتاج إلى منطق خاص باللغة. |

## السكريبت الكامل العامل

بتجميع كل ما سبق، إليك البرنامج الكامل الجاهز للتنفيذ:

```python
# Full script: run OCR on image, extract plain text, and apply AI post‑processing

from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Initialize AsposeAI
ai = AsposeAI()
ai.config.allow_auto_download = "true"
ai.config.hugging_face_repo_id = "openai/gpt2"
ai.config.gpu_layers = 0   # set >0 for GPU

# 2️⃣ Register post‑processor (capitalizes each word)
def capitalize_words(text, settings):
    return " ".join(word.capitalize() for word in text.split())

ai.set_post_processor(capitalize_words, custom_settings={})

# 3️⃣ Load image and run OCR
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()
structured_text = ocr_engine.recognize_structured()

# 4️⃣ Enhance outputs
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)

# 5️⃣ Print results
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)

# 6️⃣ Clean up
ai.free_resources()
```

احفظه باسم `run_ocr_on_image.py`، استبدل مسار الصورة بالمسار الفعلي لديك، ثم نفّذ الأمر `python run_ocr_on_image.py`. يجب أن ترى مخرجات قبل/بعد كما في المثال أعلاه.

## الخلاصة

لقد نجحنا في **تشغيل OCR على صورة** باستخدام Aspose OCR، وأظهرنا كيفية **استخراج نص عادي من صورة**، وقدمنا طريقة خفيفة لتحسين قابلية القراءة باستخدام معالج AI ما بعد. النمط الأساسي—OCR

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج نص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [استخراج نص صورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [استخراج نص من صورة – تحسين OCR مع Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}