---
category: general
date: 2026-01-07
description: كيفية تصحيح مخرجات OCR وتشغيل OCR على صورة باستخدام Aspose OCR، ثم استخدام
  نموذج Hugging Face لإصلاح الأخطاء. تعلم كيفية التعرف على النص وتحميل الصورة للـ
  OCR.
draft: false
keywords:
- how to correct ocr
- how to recognize text
- use hugging face model
- run ocr on image
- load image for ocr
language: ar
og_description: كيفية تصحيح مخرجات OCR في بايثون باستخدام Aspose OCR ونموذج Hugging
  Face. دليل خطوة بخطوة يغطي كيفية التعرف على النص، تشغيل OCR على الصورة، وتحميل الصورة
  لـ OCR.
og_title: كيفية تصحيح نتائج OCR – دليل شامل لـ Aspose و Hugging Face
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: كيفية تصحيح نتائج OCR باستخدام Aspose OCR و Hugging Face – دليل خطوة بخطوة
url: /ar/python/general/how-to-correct-ocr-results-with-aspose-ocr-and-hugging-face/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح نتائج OCR باستخدام Aspose OCR و Hugging Face – دليل خطوة بخطوة

هل تساءلت يومًا **how to correct OCR** عن مخرجات OCR التي لا تزال تبدو كخربشة بعد المرور الأول؟ لست وحدك. الملاحظات المكتوبة يدويًا، المسحات ذات التباين المنخفض، أو صور الهواتف الرخيصة غالبًا ما تترك محرك OCR في حالة تخمين، ويمكن أن تكون النتيجة الأولية مليئة بالأخطاء الإملائية. في هذا الدرس سنستعرض حلًا كاملاً يقوم **runs OCR on an image**، يستخدم Aspose OCR لاستخراج النص الخام، ثم يستفيد من **Hugging Face model** لتنظيف الإملاء والقواعد – وبالتالي يجيب على سؤال “how to correct OCR”.

سنغطي أيضًا **how to recognize text** من المصادر المكتوبة يدويًا، ونظهر خطوة **load image for OCR**، ونضيف بعض النصائح العملية التي تحميك من المشكلات الشائعة. في النهاية ستحصل على سكريبت واحد يمكنك إدراجه في أي مشروع Python والبدء في تصحيح نتائج OCR فورًا.

> **نصيحة احترافية:** إذا كنت قد ثبتت بالفعل `asposeocr` وتتوفر لديك وحدة معالجة رسومية، اضبط `gpu_layers` > 0 للحصول على تسريع في السرعة. المثال أدناه يعمل بشكل ممتاز على الأجهزة التي لا تحتوي على GPU أيضًا.

---

## ما ستحتاجه

قبل أن نبدأ، تأكد من توفر ما يلي:

- Python 3.9 أو أحدث.
- حزمة `asposeocr` (`pip install asposeocr`).
- اتصال بالإنترنت للتشغيل الأول – سيتم تنزيل نموذج Hugging Face تلقائيًا.
- صورة مكتوبة يدويًا (مثال: `handwritten_note.jpg`) موجودة في مجلد يمكنك الإشارة إليه.

لا توجد مكتبات إضافية مطلوبة؛ حيث يتولى غلاف Aspose AI تنزيل Hugging Face لك.

---

## الخطوة 1: تحميل الصورة لـ OCR وتهيئة المحرك

أول شيء عليك القيام به هو **load image for OCR**. يوفر Aspose OCR طريقة مريحة `Image.load` التي تقبل مسار ملف أو تدفق.

```python
import asposeocr as ocr

# Initialize the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the handwritten image – replace with your own path
ocr_engine.image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
```

> **لماذا هذا مهم:** تحميل الصورة مبكرًا يسمح للمحرك بفحص الدقة، DPI، وعمق اللون، وهي عوامل حاسمة لاستخراج نص دقيق. تخطي هذه الخطوة أو إمداد صورة تالفة هو سبب شائع للحصول على نتائج **how to recognize text** ضعيفة.

---

## الخطوة 2: ضبط وضعية التعرف إلى يدوي وتشغيل OCR

يدعم Aspose أوضاعًا متعددة للتعرف. بما أننا نتعامل مع ملاحظة مكتوبة بالقلم، نقوم بتمكين وضعية اليدوي.

```python
# Enable handwritten recognition mode
ocr_engine.recognition_mode = ocr.RecognitionMode.HANDWRITTEN

# Run the OCR process
ocr_engine.recognize()
raw_handwritten_text = ocr_engine.recognized_text

print("Handwritten raw output:")
print(raw_handwritten_text)
```

استدعاء `recognize()` **runs OCR on image** ويملأ المتغير `recognized_text`. في هذه المرحلة ستحصل على سلسلة مليئة بالحروف المفقودة، المسافات الزائدة، أو الكلمات المشوشة – وهو بالضبط النوع من المخرجات التي نريد تصحيحها.

---

## الخطوة 3: تكوين نموذج Hugging Face للمعالجة اللاحقة

الآن يأتي الجزء الممتع: استخدام **use hugging face model** لتنظيف النص. يوفر Aspose AI غلافًا خفيفًا لأي نموذج متوافق مع GGUF مستضاف على Hugging Face. في مثالنا نختار النموذج الخفيف `Qwen/Qwen2.5-3B-Instruct-GGUF` – مثالي لأجهزة CPU.

```python
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# Model configuration – auto‑download on first run
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    gpu_layers=0,                # Set >0 if you have a supported GPU
)

# Initialize the AI engine with the config
ai_engine = AsposeAI()
ai_engine.initialize(ai_config)
```

> **لماذا هذا النموذج؟** يوازن بين الحجم وقدرة اتباع التعليمات، مما يجعله مثاليًا للتصحيح الفوري دون الحاجة إلى GPU ضخمة.

---

## الخطوة 4: كتابة موجه تصحيح بسيط

يحتاج الذكاء الاصطناعي إلى تعليم واضح. نغلف مخرجات OCR الخام في موجه يطلب من النموذج “Fix any spelling/grammar errors”. هنا يلتقي **how to correct OCR** بمعالجة اللغة الطبيعية.

```python
def correct_handwritten(text):
    prompt = f"Fix any spelling/grammar errors in this handwritten OCR result:\n{text}"
    return ai_engine.run_prompt(prompt)

# Register the post‑processor with the AI engine
ai_engine.set_post_processor(correct_handwritten, None)
```

استدعاء `set_post_processor` يخبر Aspose AI باستدعاء `correct_handwritten` كلما استدعينا لاحقًا `run_postprocessor`.

---

## الخطوة 5: تطبيق المعالج اللاحق ورؤية النتيجة المنقحة

أخيرًا نمرر سلسلة OCR الخام إلى المعالج اللاحق. يعيد النموذج نسخة مصقولة تبدو كأنها مكتوبة يدويًا.

```python
# Apply correction
corrected_text = ai_engine.run_postprocessor(raw_handwritten_text)

print("\nCorrected handwritten output:")
print(corrected_text)
```

**الناتج المتوقع** (مثال):

```
Handwritten raw output:
Ths is a smple note wth some erors.

Corrected handwritten output:
This is a simple note with some errors.
```

لاحظ كيف قام الذكاء الاصطناعي بتصحيح الحرف “i” المفقود، وإضافة “l” المفقودة، وتصحيح “wth” إلى “with”. هذا هو جوهر **how to correct OCR** – نموذج لغة خفيف يعمل كمدقق إملائي ومصحح قواعد.

---

## الخطوة 6: تنظيف الموارد (ممارسة جيدة)

كائنات Aspose تحتفظ بموارد أصلية، لذا من الأدب تحريرها عندما تنتهي.

```python
# Free AI resources
ai_engine.free_resources()

# Dispose the OCR engine
ocr_engine.dispose()
```

تخطي عملية التنظيف قد يؤدي إلى تسرب الذاكرة، خاصة إذا شغلت السكريبت في خدمة طويلة العمر.

---

## حالات خاصة ونصائح قد لا تكون قد فكرت فيها

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **صورة ذات دقة منخفضة جدًا** (مثال: 72 dpi) | قم بزيادة الدقة باستخدام `Pillow` قبل التحميل، أو اطلب من محرك OCR تطبيق مرشح ثنائي (`ocr_engine.image.apply_binarization()`). |
| **نص مختلط بين مطبوع ومكتوب يدويًا** | نفّذ تمريرين: أولاً بـ `RecognitionMode.PRINTED`، ثم بـ `HANDWRITTEN`، وادمج النتائج قبل المعالجة اللاحقة. |
| **فشل تحميل النموذج** | اضبط `allow_auto_download="false"` وحمّل ملف GGUF يدويًا من Hugging Face، ثم وجه `hugging_face_repo_id` إلى المسار المحلي. |
| **وجود GPU لكن `gpu_layers` مضبوطة على 0** | زد `gpu_layers` إلى عدد الطبقات التي تريد تفريغها – القيم النموذجية تتراوح بين 10‑20 لنموذج 3 B. |
| **مفردات متخصصة** (مثال: مصطلحات طبية) | أضف “تلميح مفردات” قصير في نهاية الموجه: “Use the following terms: …”. النموذج يحترم القوائم البسيطة. |

هذه الفروق الدقيقة تجعل خط أنابيب **how to recognize text** قويًا عبر بيانات العالم الحقيقي.

---

## السكريبت الكامل (جاهز للنسخ واللصق)

فيما يلي السكريبت بالكامل، جاهز للتنفيذ بعد استبدال مسار الصورة.

```python
import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# 1️⃣ Load image for OCR
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")

# -------------------------------------------------
# 2️⃣ Run OCR in handwritten mode
# -------------------------------------------------
ocr_engine.recognition_mode = ocr.RecognitionMode.HANDWRITTEN
ocr_engine.recognize()
raw_handwritten_text = ocr_engine.recognized_text
print("Handwritten raw output:")
print(raw_handwritten_text)

# -------------------------------------------------
# 3️⃣ Configure Hugging Face model
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    gpu_layers=0,                # Change >0 for GPU acceleration
)
ai_engine = AsposeAI()
ai_engine.initialize(ai_config)

# -------------------------------------------------
# 4️⃣ Define correction prompt
# -------------------------------------------------
def correct_handwritten(text):
    prompt = f"Fix any spelling/grammar errors in this handwritten OCR result:\n{text}"
    return ai_engine.run_prompt(prompt)

ai_engine.set_post_processor(correct_handwritten, None)

# -------------------------------------------------
# 5️⃣ Apply post‑processor
# -------------------------------------------------
corrected_text = ai_engine.run_postprocessor(raw_handwritten_text)
print("\nCorrected handwritten output:")
print(corrected_text)

# -------------------------------------------------
# 6️⃣ Clean up
# -------------------------------------------------
ai_engine.free_resources()
ocr_engine.dispose()
```

احفظه باسم `correct_ocr.py` وشغّله باستخدام `python correct_ocr.py`. إذا تم إعداد كل شيء بشكل صحيح، سترى النص الخام والنص المصحح يُطبعان في وحدة التحكم.

---

## الخلاصة

في هذا الدليل أظهرنا **how to correct OCR** عبر ربط Aspose OCR بـ **use hugging face model** للمعالجة اللاحقة الذكية. بدءًا من تحميل الصورة، **run OCR on image**، و**how to recognize text**، مررنا بكل خطوة، شرحنا أهميتها، وقدمنا لك سكريبت جاهز للتنفيذ.  

الآن يمكنك بثقة تنظيف الملاحظات المكتوبة يدويًا، الإيصالات، أو أي مسح منخفض الجودة دون الحاجة إلى تعديل كل سطر يدويًا. هل تريد التقدم أكثر؟ جرّب استبدال نموذج Qwen بنموذج LLaMA أكبر، أو دمج السكريبت في واجهة Flask API حتى يتمكن تطبيق الويب الخاص بك من تصحيح OCR في الوقت الفعلي.  

هل لديك أسئلة حول **load image for OCR**، تعديل الموجه، أو توسيع الحل؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}