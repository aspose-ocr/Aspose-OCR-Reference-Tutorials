---
category: general
date: 2026-03-18
description: تتيح لك موارد الذكاء الاصطناعي المجانية استخراج النص من صور PNG باستخدام
  Aspose OCR Python. تعلم كيفية تنزيل نموذج من Hugging Face وتنظيف النتائج.
draft: false
keywords:
- free ai resources
- how to extract text
- download hugging face model
- recognize text from png
- aspose ocr python
language: ar
og_description: تتيح لك الموارد المجانية للذكاء الاصطناعي استخراج النص من صور PNG
  باستخدام Aspose OCR Python. تعلم كيفية تنزيل نموذج من Hugging Face وتنظيف النتائج.
og_title: 'موارد AI المجانية: نص OCR من PNG باستخدام Aspose Python'
tags:
- OCR
- Python
- AI
title: 'موارد الذكاء الاصطناعي المجانية: استخراج النص من PNG باستخدام Aspose Python'
url: /ar/python/general/free-ai-resources-ocr-text-from-png-using-aspose-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# موارد الذكاء الاصطناعي المجانية: استخراج نص من PNG باستخدام Aspose Python

هل تساءلت يومًا كيف تستخرج النص من ملف PNG دون دفع مقابل خدمة سحابية؟ **موارد الذكاء الاصطناعي المجانية** تجعل ذلك ممكنًا، ومع Aspose OCR Python يمكنك القيام بذلك محليًا في بضع أسطر فقط. في هذا الدليل سنستعرض كامل الخطوات — التعرف على النص من PNG، تنزيل نموذج من Hugging Face، وتحرير موارد الذكاء الاصطناعي عندما تنتهي.

سنغطي كل ما تحتاج إلى معرفته: الحزم المطلوبة، الكود خطوة بخطوة، لماذا كل جزء مهم، وبعض النصائح التي لن تجدها في الوثائق الرسمية. في النهاية ستحصل على سكريبت جاهز للتنفيذ يحول أي صورة إلى نص نظيف خالٍ من الأخطاء الإملائية.

## ما ستحتاجه

- **Python 3.9+** – يستخدم الكود إرشادات النوع لكنه يعمل على إصدارات 3.x السابقة أيضًا.  
- **Aspose.OCR for Python** (`pip install aspose-ocr`) – محرك OCR الأساسي.  
- **Internet access** في المرة الأولى التي تشغل فيها السكريبت – يقوم بتنزيل النموذج من Hugging Face.  
- وحدة **GPU** (اختياري) – سنضبط `gpu_layers=20` لتسريع تشغيل النموذج إذا كان لديك CUDA.

لا اشتراك مدفوع، ولا رسوم مخفية—فقط موارد ذكاء اصطناعي مجانية تتحكم فيها بنفسك.

---

![رسم توضيحي لموارد الذكاء الاصطناعي المجانية يظهر حاسوبًا محمولًا يعالج صورة PNG](/images/free-ai-resources.png "موارد الذكاء الاصطناعي المجانية")

## موارد الذكاء الاصطناعي المجانية: استخدام Aspose OCR Python

هذا القسم يوضح التدفق عالي المستوى. فكر فيه كالوصفة: تقوم بتحميل صورة، تطلب من Aspose التعرف على الأحرف الخام، تسلم تلك الأحرف إلى نموذج AI ينظفها، ثم تحرر الموارد. **الهدف الأساسي** هو إظهار كيفية استخراج النص من PNG مع الحفاظ على كل شيء محليًا.

### الخطوة 1: كيفية استخراج نص من صورة PNG

Aspose OCR يتولى الجزء الثقيل من تحويل البكسل إلى حرف. طريقة `recognize()` تُعيد نصًا عاديًا، غالبًا ما يكون صاخبًا (يفتقد المسافات، أحرف خاطئة). أدناه الكود الأدنى للحصول على هذا الإخراج الخام.

```python
import aspose.ocr as ocr

# Load the image you want to process
ocr_engine = ocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/input.png")

# Run OCR – this is where we recognize text from PNG
raw_text = ocr_engine.recognize()          # plain text output
print("🔎 Raw OCR output:")
print(raw_text)
```

**لماذا هذا مهم:**  
- `load_image` يدعم PNG, JPEG, TIFF، والعديد من الصيغ الأخرى — لذا فإن “recognize text from PNG” هو مجرد حالة استخدام واحدة.  
- السلسلة الخام غالبًا ما تحتوي على أخطاء إملائية، وفواصل أسطر مكسورة، ورموز عشوائية؛ لذلك نحتاج إلى معالج لاحق.

#### نصيحة سريعة
إذا كانت صورة PNG تحتوي على الكثير من الضوضاء، استدعِ `ocr_engine.preprocess_image()` قبل `recognize()`. يمكن أن يعزز الدقة دون أي تكلفة إضافية.

### الخطوة 2: تنزيل نموذج Hugging Face للمعالجة اللاحقة للذكاء الاصطناعي

Aspose يوفر غلافًا خفيفًا حول أي نموذج من Hugging Face. في مثالنا نقوم بسحب **Qwen/Qwen2.5-3B-Instruct‑GGUF** مع تقليل الكمية إلى int8 — حجم صغير لا يزال يقدم تدقيق إملائي وتصحيح قواعدي قوي.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",   # small footprint, ideal for free AI resources
    gpu_layers=20                       # use GPU if available, otherwise fall back to CPU
)

# The model is downloaded automatically on first run
ai_helper = AsposeAI(model_cfg)

# Enable the built‑in spell‑check post‑processor
ai_helper.set_post_processor("spellcheck")
print("✅ Model downloaded and post‑processor configured.")
```

**لماذا نقوم بتنزيل نموذج:**  
- النموذج يضيف الفهم السياقي الذي يفتقر إليه OCR البحت.  
- استخدام **free AI resource** مثل نموذج GGUF مفتوح المصدر يعني أنك تتجنب واجهات برمجة التطبيقات المكلفة.  
- `int8` تقليل الكمية يقلل من استهلاك الذاكرة RAM إلى أقل من 4 GB، وهو مناسب لمعظم الحواسيب المحمولة.

#### نصيحة احترافية
إذا كنت على جهاز يعمل بالـ CPU فقط، اضبط `gpu_layers=0`. سيظل الكود يعمل؛ لكنه لن يكون سريعًا كما هو.

### الخطوة 3: تطبيق المعالج اللاحق لتنظيف مخرجات OCR

الآن نمرر السلسلة الخام إلى نموذج AI. طريقة `run_postprocessor()` تُعيد نسخة مُنقّاة — تُصحّح الأخطاء الإملائية، تُضيف المسافات المفقودة، ويصبح النص جاهزًا للمهام اللاحقة.

```python
# Clean the OCR result with the AI post‑processor
cleaned_text = ai_helper.run_postprocessor(raw_text)

print("\n✨ Cleaned OCR output:")
print(cleaned_text)
```

**ما ستراه:**  
- “Ths is a smple txt” → “This is a simple text”  
- “2023/09/01” يبقى دون تغيير، لأن النموذج يحترم الأرقام.

### الخطوة 4: تحرير موارد الذكاء الاصطناعي المجانية عند الانتهاء

عند الانتهاء، استدعِ `free_resources()` لإلغاء تحميل النموذج من الذاكرة وإغلاق أي سياق GPU. نسيان هذه الخطوة قد يترك ذاكرة GPU معلقة، وهو فخ شائع للمطورين الجدد على استدلال AI.

```python
# Free up memory and GPU resources
ai_helper.free_resources()
print("\n🧹 Resources released – your free AI resources are back to idle.")
```

### المشكلات الشائعة وحالات الحافة

| المشكلة | سبب حدوثها | الحل |
|------|----------------|-----|
| **توقف تحميل النموذج** | انتهاء مهلة الشبكة أو جدار الحماية يمنع CDN الخاص بـ Hugging Face. | استخدم VPN أو قم بتنزيل النموذج يدويًا (`git lfs pull`) ووجه `AsposeAIModelConfig` إلى المسار المحلي. |
| **نفاد ذاكرة GPU** | `gpu_layers` عالي جدًا بالنسبة لبطاقتك. | قلل `gpu_layers` إلى 10 أو اضبطه إلى 0 لاستخدام CPU فقط. |
| **حروف غير مرغوب فيها** | الصورة PNG تحتوي على خلفية شفافة تُربك OCR. | قم بالمعالجة المسبقة باستخدام `ocr_engine.preprocess_image()` أو حوّل PNG إلى BMP أولاً. |
| **التدقيق الإملائي يزيل المصطلحات الخاصة بالمجال** | المعالج اللاحق المدمج غير مدرك للمصطلحات الخاصة بك. | قدّم قاموسًا مخصصًا عبر `ai_helper.set_custom_vocab(["MyProduct", "XYZ123"])`. |

### مثال كامل يعمل

بدمج كل شيء معًا، إليك سكريبت واحد يمكنك نسخه ولصقه وتشغيله. يفترض أن تكون قد ثبتت `aspose-ocr` وأن لديك PNG في `input.png`.

```python
import aspose.ocr as ocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

def main():
    # -------------------------------------------------
    # Step 1: Load image and run OCR (recognize text from PNG)
    # -------------------------------------------------
    engine = ocr.OcrEngine()
    engine.load_image("input.png")
    raw = engine.recognize()
    print("🔎 Raw OCR output:")
    print(raw)

    # -------------------------------------------------
    # Step 2: Download and configure the Hugging Face model
    # -------------------------------------------------
    cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20
    )
    ai = AsposeAI(cfg)
    ai.set_post_processor("spellcheck")
    print("\n✅ Model ready for post‑processing.")

    # -------------------------------------------------
    # Step 3: Clean the OCR result
    # -------------------------------------------------
    cleaned = ai.run_postprocessor(raw)
    print("\n✨ Cleaned OCR output:")
    print(cleaned)

    # -------------------------------------------------
    # Step 4: Release free AI resources
    # -------------------------------------------------
    ai.free_resources()
    print("\n🧹 All resources freed.")

if __name__ == "__main__":
    main()
```

**الإخراج المتوقع (مثال):**

```
🔎 Raw OCR output:
Ths is a smple txt frm a png img.

✅ Model ready for post‑processing.

✨ Cleaned OCR output:
This is a simple text from a PNG image.

🧹 All resources freed.
```

لاحظ كيف تتحول العبارة “recognize text from PNG” إلى نص قابل للقراءة تمامًا بعد المعالج اللاحق للذكاء الاصطناعي.

## الخطوات التالية: توسيع خط الأنابيب

- **Batch processing:** تكرار عبر مجلد من PNGs، وتجميع النتائج في ملف CSV.  
- **Custom post‑processors:** استبدال `"spellcheck"` بـ `"summarize"` للحصول على ملخص جملة واحدة لكل صورة.  
- **Integrate with FastAPI:** عرض نقطة النهاية OCR كخدمة مصغرة، مع الاستمرار في استخدام موارد الذكاء الاصطناعي المجانية فقط.  

إذا كنت curious about **how to extract text** من PDFs بدلاً من PNGs

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}