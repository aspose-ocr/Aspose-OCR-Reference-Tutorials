---
category: general
date: 2026-02-09
description: صحّح أخطاء OCR بسرعة باستخدام Aspose OCR، وضع التعرف على الخط اليدوي،
  ونموذج اللغة من HuggingFace. تعلّم كيفية استخراج النص من الصورة باستخدام المعالجة
  اللاحقة بالذكاء الاصطناعي.
draft: false
keywords:
- correct OCR errors
- extract text from image
- use HuggingFace model
- handwritten recognition mode
- load image for OCR
language: ar
og_description: تصحيح أخطاء OCR باستخدام Aspose OCR ونموذج HuggingFace. احصل على تعليمات
  خطوة بخطوة لاستخراج النص من الصورة وتحسين الدقة.
og_title: تصحيح أخطاء OCR باستخدام Aspose OCR و HuggingFace – دليل كامل
tags:
- OCR
- AI
title: تصحيح أخطاء OCR باستخدام Aspose OCR و HuggingFace – دليل كامل
url: /ar/python/general/correct-ocr-errors-with-aspose-ocr-huggingface-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصحيح أخطاء OCR – دليل كامل لـ Aspose OCR و HuggingFace

هل احتجت إلى **تصحيح أخطاء OCR** وشعرت بالعجز بعد الحصول على المخرجات الأولية؟ لست وحدك. يواجه العديد من المطورين أحرفًا مشوشة عند استخراج النص من المستندات الممسوحة، خاصةً عندما يحتوي المصدر على كتابة يدوية أو خطوط منخفضة التباين.  

في هذا الدليل سنوضح لك بالضبط كيف **استخراج النص من صورة**، وتفعيل **وضع التعرف على الكتابة اليدوية**، ثم **استخدام نموذج HuggingFace** للمعالجة اللاحقة لتنظيف تلك الأخطاء. في النهاية ستحصل على سكريبت جاهز للتنفيذ يقوم بتحميل صورة للـ OCR، تشغيل Aspose OCR، وتصحيح الأخطاء تلقائيًا باستخدام نموذج لغة كبير.

## ما ستتعلمه

- كيفية **تحميل صورة للـ OCR** باستخدام Aspose OCR.
- تفعيل **وضع التعرف على الكتابة اليدوية** للحصول على دقة أعلى للنص المتصل.
- تشغيل المحرك **لاستخراج النص من صورة**.
- إعداد **نموذج HuggingFace** (Qwen 2.5‑3B‑Instruct) لـ **تصحيح أخطاء OCR**.
- التحقق من النتائج قبل/بعد المعالجة وتنظيف الموارد.

لا تحتاج إلى خدمات خارجية بخلاف Aspose OCR و HuggingFace، والكود يعمل على أجهزة CPU‑only (طبقات GPU اختيارية). لنبدأ.

---

## الخطوة 1: تحميل صورة للـ OCR واستخراج النص من الصورة

أولًا—يحتاج سكريبتك إلى صورة bitmap للعمل معها. يستطيع Aspose OCR قراءة PNG، JPEG، TIFF، والعديد من الصيغ الأخرى.

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Create the OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image(r"YOUR_DIRECTORY/sample.png")  # <-- replace with your path
```

> **نصيحة احترافية:** احرص على أن تكون دقة الصورة 300 dpi أو أعلى؛ الدقة المنخفضة تزيد بشكل كبير من فرص الأخطاء في التعرف.

استدعاء `load_image` هو خطوة **تحميل صورة للـ OCR** التي تُجهّز المحرك للمراحل التالية.

---

## الخطوة 2: تفعيل وضع التعرف على الكتابة اليدوية (اختياري لكنه قوي)

إذا كان المصدر يحتوي على أي شكل من أشكال الخط المتصل أو الملاحظات الممسوحة، فإن تشغيل مُعرّف الكتابة اليدوية يمكن أن يُغيّر اللعبة.

```python
# Switch to handwritten mode – this tells Aspose to use a different neural net
ocr_engine.recognizer_mode = aocr.RecognizerMode.HANDWRITTEN
```

لماذا؟ لأن نموذج النص المطبوع الافتراضي غالبًا ما يخلط بين “l” (الحرف L الصغير) و “1” (الرقم واحد) عندما تكون الضربات مائلة. وضع الكتابة اليدوية يستخدم نموذجًا مُدربًا على بيانات القلم، مما يقلل هذه الأخطاء.

---

## الخطوة 3: تشغيل OCR والحصول على النص الخام

الآن نقوم فعليًا بتشغيل المحرك. تُعيد طريقة `recognize()` سلسلة نصية عادية—ما زالت مليئة بأخطاء OCR المعتادة.

```python
# Execute OCR – this returns the raw, uncorrected text
raw_text = ocr_engine.recognize()
print("Raw OCR output:\n", raw_text)
```

قد يبدو الإخراج الخام النموذجي هكذا:

```
Th1s 1s 4 s4mpl3 t3xt w1th s0me OCR err0rs.
```

لاحظ وجود “1” و “4” في أماكن الحروف. هذا هو ما سنصحه في الخطوة التالية.

---

## الخطوة 4: استخدام نموذج HuggingFace لتصحيح أخطاء OCR

هذا هو جزء **استخدام نموذج HuggingFace**. سنستدعي مستودع `Qwen/Qwen2.5-3B-Instruct-GGUF`، نطلب نسخة `int8` مُكمّية للسرعة، ونخصص عددًا قليلًا من طبقات GPU إذا كان لديك بطاقة متوافقة. إذا لم تتوفر لديك، اضبط `gpu_layers=0` وسيعود الكود إلى CPU.

```python
# Configure the AI post‑processor
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # Let the SDK download the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    gpu_layers=20                                   # Adjust based on your GPU; 0 = CPU only
)

# Instantiate the processor
ai_processor = AsposeAI(ai_config)

# Define a simple correction prompt
ai_processor.set_post_processor(
    "llm_correction",
    lambda: {"prompt": "Fix OCR errors in the following text, preserving line breaks and punctuation."}
)

# Run the LLM on the raw OCR output
corrected_text = ai_processor.run_postprocessor(raw_text)

print("\nCorrected OCR output:\n", corrected_text)
```

يتلقى النموذج النص الخام، يطبق الـ prompt، ويعيد نسخة مُنقّحة:

```
This is a sample text with some OCR errors.
```

نظرًا لأننا استخدمنا **نموذج HuggingFace** مُكمٍّ، فإن الاستدلال يتم في أقل من ثانية على GPU متوسط، وحتى على CPU يكتمل بسرعة كافية لمعظم وظائف الدُفعات.

---

## الخطوة 5: مراجعة النتائج، تحرير الموارد، والخطوات التالية

أخيرًا، نقارن بين المخرجات قبل/بعد المعالجة ونحرّر أي موارد أصلية قد يكون SDK خصّصها.

```python
# Display side‑by‑side comparison
print("\nBefore :", raw_text)
print("After  :", corrected_text)

# Clean up – important when processing many files in a loop
ai_processor.free_resources()
```

إذا كنت تخطط لمعالجة مجلد من الصور، غلف التدفق بالكامل داخل حلقة `for` واستدعِ `free_resources()` بعد كل ملف لتجنّب تسرب الذاكرة.

---

![مخطط تدفق تصحيح أخطاء OCR](https://example.com/diagram.png "مخطط يُظهر خط أنابيب تصحيح أخطاء OCR من تحميل الصورة إلى المعالجة اللاحقة بالذكاء الاصطناعي")

*نص بديل للصورة: "نظرة عامة على خط أنابيب تصحيح أخطاء OCR"*

---

## الأسئلة المتكررة والحالات الخاصة

**ماذا لو لم يكن لدي GPU؟**  
اضبط `gpu_layers=0` في `AsposeAIModelConfig`. سيعمل النموذج على CPU؛ تكميم `int8` يحافظ على استهلاك الذاكرة منخفضًا.

**هل يمكنني استخدام نموذج HuggingFace مختلف؟**  
بالطبع. استبدل `hugging_face_repo_id` بأي نموذج GGUF متوافق وعدّل `hugging_face_quantization` وفقًا لذلك. للوثائق الفرنسية، جرّب `bigscience/bloomz-560m`.

**هل سيحافظ النموذج على بنية الجداول في مستنداتي؟**  
الـ prompt الأساسي يركز على الحفاظ على فواصل الأسطر. إذا كنت بحاجة إلى تنسيق الجداول، عزّز الـ prompt بـ: `"Preserve table rows and columns exactly as shown."`

**كيف أتعامل مع ملفات PDF متعددة الصفحات؟**  
حوّل كل صفحة إلى صورة (مثلاً باستخدام `pdf2image`) ومرّرها واحدةً تلو الأخرى إلى نفس الخط الأنابيب. يعمل المعالج اللاحق للذكاء الاصطناعي على كل صفحة على حدة، لذا ستحصل على تصحيح متسق عبر الملف بأكمله.

**هل هناك طريقة للمعالجة الدُفعية دون إعادة تحميل النموذج في كل مرة؟**  
اضبط `allow_auto_download="false"` بعد التشغيل الأول وضع ملفات النموذج في دليل التخزين المؤقت الافتراضي (`~/.aspose/ocr/models`). ستُحمَّل الإصدارات اللاحقة فورًا.

---

## الخاتمة

أصبح لديك الآن حل كامل من البداية للنهاية **لتصحيح أخطاء OCR** باستخدام Aspose OCR، وتفعيل **وضع التعرف على الكتابة اليدوية**، و**استخدام نموذج HuggingFace** للمعالجة اللاحقة المدعومة بالذكاء الاصطناعي. باتباع الخطوات أعلاه يمكنك استخراج النص من صورة، تنظيف المخرجات، ودمج سير العمل في خطوط معالجة مستندات أكبر.

الخطوات التالية قد تشمل:

- تجريب prompts مختلفة لتخصيص أسلوب التصحيح.
- المعالجة الدُفعية لملفات PDF أو الكتب الممسوحة.
- دمج النص المصحح مع مهام NLP لاحقة (تلخيص، استخراج كيانات).

برمجة سعيدة، ولتكن نتائج OCR خالية من الأخطاء!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}