---
category: general
date: 2026-05-03
description: كيفية معالجة مجموعة من الصور باستخدام تقنية OCR من Aspose وتدقيق إملائي
  بالذكاء الاصطناعي. تعلّم استخراج النص من الصور، تطبيق التدقيق الإملائي، الاستفادة
  من موارد الذكاء الاصطناعي المجانية وتصحيح أخطاء OCR.
draft: false
keywords:
- how to batch ocr
- extract text from images
- free ai resources
- apply spell check
- correct ocr errors
language: ar
og_description: كيفية معالجة مجموعة من الصور باستخدام Aspose OCR وفحص الإملاء بالذكاء
  الاصطناعي. اتبع دليلًا خطوة بخطوة لاستخراج النص من الصور، وتطبيق فحص الإملاء، واستخدام
  موارد الذكاء الاصطناعي المجانية وتصحيح أخطاء OCR.
og_title: كيفية تنفيذ OCR دفعيًا باستخدام Aspose OCR – دليل بايثون الكامل
tags:
- OCR
- Python
- AI
- Aspose
title: كيفية تنفيذ OCR دفعيًا باستخدام Aspose OCR – دليل بايثون الكامل
url: /ar/python/general/how-to-batch-ocr-with-aspose-ocr-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعيًا باستخدام Aspose OCR – دليل Python كامل

هل تساءلت يومًا **كيف تقوم بعمل OCR دفعيًا** لمجلد كامل من ملفات PDF أو الصور الممسوحة ضوئيًا دون كتابة سكريبت منفصل لكل ملف؟ أنت لست وحدك. في العديد من خطوط الأنابيب الواقعية تحتاج إلى **استخراج النص من الصور**، تصحيح الأخطاء الإملائية، وأخيرًا تحرير أي موارد AI قد خصصتها. يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose OCR، معالج AI خفيف الوزن، وبعض أسطر Python.

سنستعرض عملية تهيئة محرك OCR، ربط مدقق إملائي AI، التكرار عبر دليل الصور، وتنظيف النموذج بعد ذلك. في النهاية ستحصل على سكريبت جاهز للتشغيل يقوم **بتصحيح أخطاء OCR** تلقائيًا ويحرر **موارد AI مجانية** بحيث يبقى GPU الخاص بك سعيدًا.

## ما ستحتاجه

- Python 3.9+ (الكود يستخدم type‑hints لكنه يعمل على إصدارات 3.x السابقة)
- حزمة `asposeocr` (`pip install asposeocr`) – توفر محرك OCR.
- الوصول إلى نموذج Hugging Face `bartowski/Qwen2.5-3B-Instruct-GGUF` (يتم تنزيله تلقائيًا).
- وحدة معالجة رسومية (GPU) بذاكرة VRAM لا تقل عن بضع جيجابايت (السكريبت يحدد `gpu_layers = 30`، يمكنك تقليلها إذا لزم الأمر).

لا توجد خدمات خارجية، ولا واجهات برمجة تطبيقات مدفوعة – كل شيء يعمل محليًا.

---

## الخطوة 1: إعداد محرك OCR – **كيف تقوم بعمل OCR دفعيًا** بفعالية

قبل أن نتمكن من معالجة ألف صورة نحتاج إلى محرك OCR قوي. يتيح لنا Aspose OCR اختيار اللغة ووضعية التعرف في استدعاء واحد.

```python
# Step 1: Initialize the OCR engine for English plain‑text output
def init_ocr() -> aocr.OcrEngine:
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English          # English language pack
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Returns raw string, no layout
    return ocr_engine
```

**لماذا هذا مهم:** ضبط `recognize_mode` إلى `Plain` يحافظ على خفة الناتج، وهو مثالي عندما تخطط لتشغيل مدقق إملائي لاحقًا. إذا كنت بحاجة إلى معلومات التخطيط، يمكنك التحويل إلى `Layout`، لكن ذلك يضيف عبئًا قد لا ترغب به في وظيفة دفعية.

> **نصيحة احترافية:** إذا كنت تتعامل مع مسحات متعددة اللغات، يمكنك تمرير قائمة مثل `ocr_engine.language = [aocr.Language.English, aocr.Language.Spanish]`.

---

## الخطوة 2: تهيئة معالج AI بعد‑المعالجة – **تطبيق التدقيق الإملائي** على ناتج OCR

يأتي Aspose AI مع معالج بعد‑معالجة مدمج يمكنه تشغيل أي نموذج تريده. هنا نقوم بجلب نموذج Qwen 2.5 مضغوط من Hugging Face وربط روتين التدقيق الإملائي.

```python
# Step 2: Configure and start the AI post‑processor
def init_ai() -> aocr.ai.AsposeAI:
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 30          # Adjust based on your GPU memory
    ai_processor = AsposeAI()
    ai_processor.initialize(model_cfg)

    # Attach the built‑in spell‑check post‑processor
    ai_processor.set_post_processor(ai_processor.postprocessor_spell_check, {})
    return ai_processor
```

**لماذا هذا مهم:** النموذج مضغوط (`q4_k_m`)، مما يقلل استهلاك الذاكرة مع الحفاظ على فهم لغوي جيد. باستدعاء `set_post_processor` نخبر Aspose AI بتنفيذ خطوة **تطبيق التدقيق الإملائي** تلقائيًا على أي سلسلة نمررها.

> **احذر:** إذا لم تستطع وحدة GPU الخاصة بك التعامل مع 30 طبقة، قلل العدد إلى 15 أو حتى 5 – سيظل السكريبت يعمل، لكنه سيكون أبطأ قليلاً.

---

## الخطوة 3: تشغيل OCR و**تصحيح أخطاء OCR** على صورة واحدة

الآن بعد أن أصبح كل من محرك OCR ومدقق الإملائي AI جاهزين، نجمعهما. هذه الدالة تحمل صورة، تستخرج النص الخام، ثم تشغل معالج AI بعد‑المعالجة لتنظيفه.

```python
# Step 3: OCR an image and run the spell‑check post‑processor
def ocr_and_correct(image_path: str,
                    ocr_engine: aocr.OcrEngine,
                    ai_processor: aocr.ai.AsposeAI) -> str:
    image = aocr.Image.load(image_path)               # Load any supported format
    raw_text = ocr_engine.recognize(image)           # Plain string from OCR
    corrected_text = ai_processor.run_postprocessor(raw_text)
    return corrected_text
```

**لماذا هذا مهم:** إدخال سلسلة OCR الخام مباشرة إلى نموذج AI يمنحنا خطوة **تصحيح أخطاء OCR** **دون كتابة أي تعبيرات regex أو قواميس مخصصة**. النموذج يفهم السياق، لذا يمكنه تصحيح “recieve” → “receive” وحتى الأخطاء الأكثر دقة.

---

## الخطوة 4: **استخراج النص من الصور** بالجملة – الحلقة الفعلية للمعالجة الدفعية

هنا يبرز سحر **كيفية تنفيذ OCR دفعيًا**. نقوم بالتكرار عبر دليل، نتخطى الملفات غير المدعومة، ونكتب كل ناتج مصحح إلى ملف `.txt`.

```python
# Step 4: Process an entire folder of images
if __name__ == "__main__":
    # Initialize once – reuse for every file
    ocr_engine = init_ocr()
    ai_processor = init_ai()

    input_dir = "YOUR_DIRECTORY/input_images"
    output_dir = "YOUR_DIRECTORY/output_text"
    os.makedirs(output_dir, exist_ok=True)

    for file_name in os.listdir(input_dir):
        # Only handle common image extensions
        if not file_name.lower().endswith(('.png', '.jpg', '.jpeg', '.tif', '.tiff')):
            continue

        image_path = os.path.join(input_dir, file_name)
        corrected = ocr_and_correct(image_path, ocr_engine, ai_processor)

        txt_path = os.path.join(output_dir,
                                os.path.splitext(file_name)[0] + ".txt")
        with open(txt_path, "w", encoding="utf-8") as txt_file:
            txt_file.write(corrected)

        print(f"Processed {file_name}")

    # Step 5: Release **free AI resources** after the batch finishes
    ai_processor.free_resources()
```

### الناتج المتوقع

لصورة تحتوي على الجملة *“The quick brown fox jumps over the lazzy dog.”* سترى ملف نصي يحتوي على:

```
The quick brown fox jumps over the lazy dog.
```

لاحظ أن الحرف “z” المزدوج تم تصحيحه تلقائيًا – هذا هو تدقيق الإملائي AI في العمل.

**لماذا هذا مهم:** بإنشاء كائنات OCR وAI **مرة واحدة** وإعادة استخدامها، نتجنب عبء تحميل النموذج لكل ملف. هذه هي الطريقة الأكثر كفاءة لـ **كيفية تنفيذ OCR دفعيًا** على نطاق واسع.

---

## الخطوة 5: التنظيف – **تحرير موارد AI** بشكل صحيح

عند الانتهاء، استدعاء `free_resources()` يحرر ذاكرة GPU، وسياقات CUDA، وأي ملفات مؤقتة أنشأها النموذج.

```python
# Step 5: Explicitly free GPU and model memory
ai_processor.free_resources()
```

تجاوز هذه الخطوة قد يترك تخصيصات GPU معلقة، مما قد يتسبب في تعطل عمليات Python اللاحقة أو استهلاك VRAM. فكر فيها كجزء “إطفاء الأنوار” في وظيفة دفعية.

---

## المشكلات الشائعة والنصائح الإضافية

| المشكلة | ما الذي يجب البحث عنه | الحل |
|-------|------------------|-----|
| **أخطاء نفاد الذاكرة** | GPU ينفد بعد بضع عشرات من الصور | قلل `gpu_layers` أو انتقل إلى CPU (`model_cfg.gpu_layers = 0`). |
| **حزمة اللغة مفقودة** | OCR يُرجع سلاسل فارغة | تأكد من أن نسخة `asposeocr` تشمل بيانات اللغة الإنجليزية؛ أعد التثبيت إذا لزم الأمر. |
| **ملفات غير صورة** | السكريبت يتعطل عند وجود ملف `.pdf` عشوائي | الحارس `if not file_name.lower().endswith(...)` يتخطى هذه الملفات بالفعل. |
| **التدقيق الإملائي غير مطبق** | الناتج يبدو مطابقًا لـ OCR الخام | تحقق من استدعاء `ai_processor.set_post_processor` قبل الحلقة. |
| **بطء سرعة المعالجة الدفعية** | يستغرق أكثر من 5 ثوانٍ لكل صورة | فعّل `model_cfg.allow_auto_download = "false"` بعد التشغيل الأول، حتى لا يتم إعادة تنزيل النموذج في كل مرة. |

**نصيحة احترافية:** إذا كنت بحاجة إلى **استخراج النص من الصور** بلغة غير الإنجليزية، ببساطة غير `ocr_engine.language` إلى الـ enum المناسب (مثال: `aocr.Language.French`). سيستمر نفس معالج AI بعد‑المعالجة في تطبيق التدقيق الإملائي، لكن قد ترغب في نموذج مخصص للغة للحصول على أفضل النتائج.

---

## ملخص وخطوات قادمة

لقد غطينا كامل خط الأنابيب لـ **كيفية تنفيذ OCR دفعيًا**:

1. **تهيئة** محرك OCR نص عادي للإنجليزية.  
2. **تكوين** نموذج تدقيق إملائي AI وربطه كمعالج بعد‑معالجة.  
3. **تشغيل** OCR على كل صورة والسماح للـ AI **بتصحيح أخطاء OCR** تلقائيًا.  
4. **التكرار** عبر دليل لـ **استخراج النص من الصور** بالجملة.  
5. **تحرير موارد AI** بمجرد انتهاء المهمة.

من هنا يمكنك:

- تمرير النص المصحح إلى خط أنابيب NLP لاحق (تحليل المشاعر، استخراج الكيانات، إلخ).
- استبدال معالج التدقيق الإملائي بمعالج تلخيص مخصص عبر استدعاء `ai_processor.set_post_processor(your_custom_func, {})`.
- موازاة حلقة المجلد باستخدام `concurrent.futures.ThreadPoolExecutor` إذا كان GPU الخاص بك يستطيع التعامل مع تدفقات متعددة.

---

## أفكار نهائية

ليس من الضروري أن تكون معالجة OCR دفعيًا مهمة شاقة. من خلال الاستفادة من Aspose OCR مع نموذج AI خفيف الوزن، تحصل على **حل شامل** يـ **يستخرج النص من الصور**، **يطبق التدقيق الإملائي**، **يصّح أخطاء OCR**، و**يحرّر موارد AI** بنظافة. جرّب السكريبت على مجلد اختبار، اضبط عدد طبقات GPU ليتناسب مع عتادك، وستحصل على خط أنابيب جاهز للإنتاج في دقائق.

هل لديك أسئلة حول تعديل النموذج، معالجة ملفات PDF، أو دمجه في خدمة ويب؟ اترك تعليقًا أدناه أو راسلني على GitHub. برمجة سعيدة، ولتكن OCR دائمًا دقيقة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}