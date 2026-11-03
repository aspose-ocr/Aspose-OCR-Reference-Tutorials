---
category: general
date: 2026-05-03
description: استخراج النص من الصورة باستخدام Aspose OCR وفحص الإملاء بالذكاء الاصطناعي.
  تعلم كيفية إجراء OCR على الصورة، تحميل الصورة للـ OCR، التعرف على النص من الفاتورة
  وإطلاق موارد وحدة معالجة الرسوميات.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR وتدقيق إملائي بالذكاء الاصطناعي.
  دليل خطوة بخطوة يغطي كيفية إجراء OCR على الصورة، تحميل الصورة للـ OCR، وإطلاق موارد
  وحدة معالجة الرسومات.
og_title: استخراج النص من الصورة – دليل شامل للتعرف الضوئي على الأحرف وتدقيق الإملاء
tags:
- OCR
- Aspose
- AI
- Python
title: استخراج النص من الصورة – OCR مع تدقيق إملائي AI من Aspose
url: /ar/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة – دليل OCR كامل وتدقيق الإملاء

هل احتجت يومًا إلى **استخراج النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة ستوفر لك السرعة والدقة معًا؟ لست وحدك. في العديد من المشاريع الواقعية—مثل معالجة الفواتير، رقمنة الإيصالات، أو مسح العقود—الحصول على نص نظيف وقابل للبحث من صورة هو العائق الأول.

الخبر السار هو أن Aspose OCR مقترن بنموذج Aspose AI خفيف الوزن يمكنه إنجاز هذه المهمة ببضع أسطر من بايثون. في هذا الدرس سنستعرض **كيفية OCR الصورة**، تحميل الصورة بشكل صحيح، تشغيل معالج تدقيق إملائي مدمج، وأخيرًا **تحرير موارد GPU** حتى يبقى تطبيقك صديقًا للذاكرة.

بنهاية هذا الدليل ستتمكن من **التعرف على النص من صور الفواتير**، تصحيح أخطاء OCR الشائعة تلقائيًا، والحفاظ على نظافة GPU للدفعة التالية.

---

## ما ستحتاجه

- Python 3.9 أو أحدث (الكود يستخدم تلميحات النوع لكنه يعمل على إصدارات 3.x السابقة)
- حزم `aspose-ocr` و `aspose-ai` (التثبيت عبر `pip install aspose-ocr aspose-ai`)
- وجود GPU يدعم CUDA اختياري؛ سيعود السكريبت إلى CPU إذا لم يُعثر على GPU.
- صورة مثال، مثل `sample_invoice.png`، موجودة في مجلد يمكنك الإشارة إليه.

لا أطر عمل ML ثقيلة، ولا تحميل نماذج ضخمة—فقط نموذج Q4‑K‑M مُكمًّى صغير يتناسب بسهولة مع معظم بطاقات GPU.

## الخطوة 1: تهيئة محرك OCR – استخراج النص من الصورة

أول ما تقوم به هو إنشاء كائن `OcrEngine` وتحديد اللغة المتوقعة. هنا نختار الإنجليزية ونطلب إخراج نص عادي، وهو مثالي للمعالجة اللاحقة.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**لماذا هذا مهم:** تحديد اللغة يحد من مجموعة الأحرف، مما يحسن الدقة. وضع النص العادي يزيل معلومات التخطيط التي عادةً لا تحتاجها عندما تريد فقط استخراج النص من الصورة.

## الخطوة 2: تحميل الصورة لـ OCR – كيفية OCR الصورة

الآن نقوم بتمرير صورة فعلية إلى المحرك. الدالة المساعدة `Image.load` تدعم الصيغ الشائعة (PNG، JPEG، TIFF) وتُبسط تفاصيل إدخال/إخراج الملفات.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**نصيحة:** إذا كانت صورك المصدرية كبيرة، فكر في تغيير حجمها قبل إرسالها إلى المحرك؛ الأبعاد الأصغر يمكن أن تقلل من استهلاك ذاكرة GPU دون الإضرار بجودة التعرف.

## الخطوة 3: تكوين نموذج Aspose AI – التعرف على النص من الفاتورة

Aspose AI يأتي بنموذج GGUF صغير يمكنك تنزيله تلقائيًا. يستخدم المثال مستودع `Qwen2.5‑3B‑Instruct‑GGUF`، مُكمًّى إلى `q4_k_m`. كما نخبر وقت التشغيل بتخصيص 20 طبقة على الـ GPU، مما يوازن بين السرعة واستخدام الذاكرة.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**خلف الكواليس:** النموذج المُكمًّى حجمه تقريبًا 1.5 GB على القرص، وهو جزء صغير من نموذج الدقة الكاملة، لكنه لا يزال يلتقط ما يكفي من الفروق اللغوية لتحديد الأخطاء الشائعة في OCR.

## الخطوة 4: تهيئة AsposeAI وإرفاق معالج تدقيق الإملاء بعد المعالجة

Aspose AI يتضمن معالج تدقيق إملائي جاهز بعد المعالجة. بإرفاقه، سيتم تنظيف كل نتيجة OCR تلقائيًا.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**لماذا نستخدم معالج ما بعد المعالجة؟** غالبًا ما يخطئ محرك OCR في قراءة “Invoice” كـ “Invo1ce” أو “Total” كـ “T0tal”. يقوم تدقيق الإملاء بتشغيل نموذج لغة خفيف على السلسلة الأصلية ويصحح تلك الأخطاء دون الحاجة إلى كتابة قاموس مخصص.

## الخطوة 5: تشغيل معالج تدقيق الإملاء على نتيجة OCR

مع ربط كل شيء، استدعاء واحد ينتج النص المصحح. نقوم أيضًا بطباعة النسختين الأصلية والمنقحة لتتمكن من رؤية التحسين.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

قد يبدو الناتج النموذجي لفاتورة كالتالي:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

لاحظ كيف تحولت “Invo1ce” إلى الكلمة الصحيحة “Invoice”. هذه هي قوة تدقيق الإملاء المدمج بالذكاء الاصطناعي.

## الخطوة 6: تحرير موارد GPU – تحرير موارد GPU بأمان

إذا كنت تشغل هذا في خدمة طويلة الأمد (مثل واجهة ويب API تعالج عشرات الفواتير في الدقيقة)، يجب تحرير سياق GPU بعد كل دفعة. وإلا ستواجه تسربات في الذاكرة وفي النهاية أخطاء “CUDA out of memory”.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**نصيحة احترافية:** استدعِ `free_resources()` داخل كتلة `finally` أو مدير سياق لضمان تنفيذه دائمًا، حتى إذا حدث استثناء.

## مثال كامل يعمل

جمع كل الأجزاء معًا يمنحك سكريبتًا مستقلًا يمكنك إدراجه في أي مشروع.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

احفظ الملف، عدل مسار الصورة، وشغّل `python extract_text_from_image.py`. يجب أن ترى نص الفاتورة المنقح يُطبع في وحدة التحكم.

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا على أجهزة لا تحتوي على GPU؟**  
ج: بالتأكيد. إذا لم يتم اكتشاف GPU، فإن Aspose AI ينتقل إلى التنفيذ على CPU، رغم أنه سيكون أبطأ. يمكنك فرض الاستخدام على CPU بتعيين `model_cfg.gpu_layers = 0`.

**س: ماذا لو كانت فواتيري بلغة غير الإنجليزية؟**  
ج: غيّر `ocr_engine.language` إلى القيمة المناسبة من الـ enum (مثلاً `aocr.Language.Spanish`). نموذج تدقيق الإملاء متعدد اللغات، لكن قد تحصل على نتائج أفضل باستخدام نموذج مخصص للغة.

**س: هل يمكنني معالجة صور متعددة في حلقة؟**  
ج: نعم. فقط انقل خطوات التحميل، التعرف، وما بعد المعالجة داخل حلقة `for`. تذكر استدعاء `ocr_ai.free_resources()` بعد الحلقة أو بعد كل دفعة إذا كنت تعيد استخدام نفس نسخة AI.

**س: ما حجم تحميل النموذج؟**  
ج: تقريبًا 1.5 GB للإصدار المُكمًّى `q4_k_m`. يتم تخزينه مؤقتًا بعد التشغيل الأول، لذا فإن التنفيذ اللاحق يكون فوريًا.

## الخلاصة

في هذا الدرس أظهرنا كيفية **استخراج النص من الصورة** باستخدام Aspose OCR، تكوين نموذج AI صغير، تطبيق معالج تدقيق إملائي بعد المعالجة، وتحرير موارد GPU بأمان. يغطي سير العمل كل شيء من تحميل الصورة إلى تنظيف الموارد بعد الانتهاء، مما يمنحك خط أنابيب موثوقًا لسيناريوهات **التعرف على النص من الفاتورة**.

الخطوة التالية؟ جرّب استبدال تدقيق الإملاء بنموذج استخراج كيانات مخصص

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}