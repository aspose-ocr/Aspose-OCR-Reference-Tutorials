---
category: general
date: 2026-03-26
description: تحويل الصورة إلى نص باستخدام Aspose OCR وتنظيف نص OCR بطريقة بايثونية.
  تعلّم كيفية استخراج نص الصورة ومعالجته لاحقًا في سكريبت واحد.
draft: false
keywords:
- convert image to text
- how to extract image text
- clean ocr text python
- Aspose OCR Python
- AI spell‑checker Python
- post‑process OCR output
language: ar
og_description: حوّل الصورة إلى نص بسرعة. يوضح هذا الدليل كيفية استخراج نص الصورة
  وتنظيف نص OCR بأسلوب بايثون باستخدام Aspose OCR ومدقق إملائي ذكي.
og_title: تحويل الصورة إلى نص باستخدام بايثون – دليل كامل
tags:
- OCR
- Python
- Aspose
- AI
title: تحويل الصورة إلى نص باستخدام بايثون – دليل كامل خطوة بخطوة
url: /ar/python/general/convert-image-to-text-with-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى نص – دليل بايثون كامل

هل احتجت يوماً إلى **تحويل الصورة إلى نص** لكنك حصلت على نتائج فوضوية؟ لست وحدك. يواجه العديد من المطورين مشكلة عندما يكون ناتج OCR مليئاً بالأخطاء الإملائية، الرموز العشوائية، أو فواصل الأسطر الخاطئة. الخبر السار؟ ببضع أسطر من بايثون وAspose OCR يمكنك استخراج نص واضح من أي صورة **و** تنظيفه تلقائياً.

> **ما ستتعلمه**  
> * تثبيت وتكوين Aspose OCR.  
> * التعرف على النص من ملف صورة.  
> * تهيئة نموذج Aspose AI لتصحيح الإملاء.  
> * تطبيق المعالج اللاحق لتنظيف ناتج OCR.  
> * حفظ النتيجة النهائية وتحرير الموارد.  

كل هذا يعمل بنمط **clean OCR text python**—أي أن الكود جاهز للإدماج في أي مشروع دون الحاجة إلى أطر إضافية.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| Python 3.9 أو أحدث | صsyntax حديثة وتلميحات نوع |
| حزمة `asposeocr` (`pip install asposeocr`) | محرك OCR الأساسي |
| اتصال بالإنترنت (في التشغيل الأول) | تنزيل النموذج تلقائياً من Hugging Face |
| صورة PNG/JPEG تريد قراءتها | مصدر الإدخال |

لا يلزم وجود GPU، لكن إذا كان لديك سيستخدمه نموذج AI تلقائياً لتسريع عملية تصحيح الإملاء.

---

## الخطوة 1: تحويل الصورة إلى نص باستخدام Aspose OCR

أول شيء نحتاجه هو محرك OCR موثوق. Aspose OCR مكتبة تجارية، لكنها توفر طبقة مجانية سخية للتطوير. أدناه نقوم بتهيئة المحرك، نحدد اللغة الإنجليزية، ونفعّل تصحيح الانحراف التلقائي للتعامل مع المسحات المائلة.

```python
import asposeocr as ocr

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English   # English language pack
ocr_engine.auto_skew = True                  # Auto‑deskew images
```

> **لماذا نفعّل `auto_skew`؟**  
> العديد من المستندات الممسوحة ليست مسطحة تماماً. يقوم Auto‑skew بتدوير الصورة بالدرجة اللازمة لتحسين التعرف على الأحرف، مما يقلل عدد الكلمات المشوشة التي سيتعين عليك تنظيفها لاحقاً.

الآن نمرّر ملف الصورة إلى المحرك:

```python
# Recognise text from the input image (replace with your own path)
ocr_result = ocr_engine.recognize_image("YOUR_DIRECTORY/input_image.png")
print("Raw OCR output:")
print(ocr_result.text[:200])  # Show first 200 characters for sanity check
```

خاصية `ocr_result.text` تحتوي على السلسلة الخام المستخرجة من الصورة. في هذه المرحلة قد تلاحظ علامات ترقيم عشوائية، مشاكل في فواصل الأسطر، أو حتى بعض الكلمات المكتوبة خطأً—وهي المشكلة التي نهدف إلى حلها.

![convert image to text workflow](image.png){alt="مخطط تحويل الصورة إلى نص"}

---

## الخطوة 2: إعداد مدقق الإملاء AI (Clean OCR Text Python)

تنظيف ناتج OCR يمكن أن يكون بسيطاً كاستبدال regex، لكن للحصول على نص مقروء حقاً سنستخدم Aspose AI مع نموذج LLM خفيف متخصص في تصحيح الإملاء. يتم جلب النموذج من Hugging Face في أول تشغيل للسكريبت، لذا لا تحتاج إلى تنزيل أي شيء يدوياً.

```python
from asposeocr import AsposeAI, AsposeAIModelConfig

# Model configuration – auto‑download enabled
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=30                # Use GPU if available, otherwise CPU fallback
)

# Initialise the AI spell‑checker
spell_checker = AsposeAI()
spell_checker.initialize(model_cfg)
spell_checker.set_post_processor("spell_check")
```

**لماذا هذا النموذج بالتحديد؟**  
`Qwen2.5‑3B‑Instruct‑GGUF` هو نموذج مدمج يضم 3 مليارات معامل ومُدرب على التعليمات، يعمل بسهولة على GPU للابتوب (أو حتى على CPU مع تقليل الدقة إلى int8). إنه سريع بما يكفي لتصحيح الإملاء سطرًا بسطر دون استهلاك كبير للذاكرة.

---

## الخطوة 3: تطبيق تصحيح الإملاء على ناتج OCR

مع وجود نص OCR جاهز والنموذج AI مُعد، نمرّر السلسلة الخام إلى المعالج اللاحق. تُعيد الطريقة نسخة مُنقّحة يمكنك كتابتها مباشرة إلى القرص.

```python
# Run the spell‑checking post‑processor
corrected_text = spell_checker.run_postprocessor(ocr_result.text)

print("\nCleaned OCR output (first 200 chars):")
print(corrected_text[:200])
```

التحسينات النموذجية التي ستلاحظها:

* “teh” → “the”  
* “recieve” → “receive”  
* فقدان المسافات بعد علامات الترقيم – يتم إصلاحها تلقائياً  
* فواصل أسطر غريبة تتحول إلى جمل صحيحة  

إذا احتجت مزيداً من التحكم، يمكنك تمرير موجه مخصص إلى `run_postprocessor`، لكن الإعداد الافتراضي “spell_check” يكفي في معظم الحالات.

---

## الخطوة 4: حفظ النص المنقّح إلى ملف

الآن بعد أن أصبح النص مرتباً، نقوم بحفظه. استخدام UTF‑8 يضمن بقاء أي أحرف خاصة (مثل الحروف المشكّلة) سليمة.

```python
output_path = "YOUR_DIRECTORY/output_text.txt"

with open(output_path, "w", encoding="utf-8") as out_file:
    out_file.write(corrected_text)

print(f"\n✅ Processing complete: input_image.png → {output_path}")
```

يمكنك فتح الملف بأي محرر وسترى وثيقة قابلة للقراءة جاهزة للمعالجة اللاحقة—سواء كان ذلك لتغذية نموذج لغة، فهرسة للبحث، أو مجرد أرشفة.

---

## الخطوة 5: تحرير موارد AI (صيانة جيدة)

Aspose AI يحتفظ بأوزان النموذج في الذاكرة. تحريرها عند الانتهاء يمنع تسرب الذاكرة، خاصة في الخدمات التي تعمل لفترات طويلة.

```python
spell_checker.free_resources()
```

هذا كل شيء! كامل خط الأنابيب—من الصورة إلى النص النظيف—يُنفّذ في أقل من 30 سطرًا من بايثون.

---

## الأسئلة الشائعة والحالات الخاصة

### ماذا لو لم تكن الصورة باللغة الإنجليزية؟

عيّن `ocr_engine.language` إلى التعداد المناسب، مثل `ocr.Language.French`. نموذج تصحيح الإملاء غير معتمد على اللغة للتهجئة الأساسية، لكن قد ترغب في نموذج متعدد اللغات للحصول على أفضل النتائج.

### بطاقة الرسوميات لدي تحتوي على 20 طبقة فقط—هل يمكنني استخدام النموذج؟

بالطبع. فقط قلل `gpu_layers` إلى `20` (أو `0` لاستخدام CPU فقط). المكتبة ستعود تلقائياً إلى CPU للطبقات المتبقية.

### فشل تنزيل النموذج خلف بروكسي مؤسسي؟

مرّر إعدادات البروكسي عبر المتغيرات البيئية (`HTTP_PROXY`, `HTTPS_PROXY`) قبل تشغيل السكريبت. روتين التنزيل يحترم هذه الإعدادات.

### أحتاج فقط إلى تنظيف سريع باستخدام regex، دون AI؟

يمكنك تخطي خطوة AI وتشغيل تنظيف بسيط:

```python
import re
clean = re.sub(r'\s+', ' ', ocr_result.text).strip()
```

لكن تذكر، الـ regex لا يُصلح الأخطاء الإملائية الحقيقية—AI هو الذي يقوم بذلك لك.

---

## السكريبت الكامل القابل للتنفيذ

فيما يلي السكريبت الكامل جاهز للتنفيذ. استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على صورتك ومكان حفظ ملف الإخراج.

```python
import asposeocr as ocr
from asposeocr import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Initialise OCR engine
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
ocr_engine.auto_skew = True

# -------------------------------------------------
# Step 2 – Recognise text from image
# -------------------------------------------------
ocr_result = ocr_engine.recognize_image("YOUR_DIRECTORY/input_image.png")
print("Raw OCR (first 200 chars):")
print(ocr_result.text[:200])

# -------------------------------------------------
# Step 3 – Configure AI spell‑checker
# -------------------------------------------------
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=30
)

spell_checker = AsposeAI()
spell_checker.initialize(model_cfg)
spell_checker.set_post_processor("spell_check")

# -------------------------------------------------
# Step 4 – Clean the OCR output
# -------------------------------------------------
corrected_text = spell_checker.run_postprocessor(ocr_result.text)
print("\nCleaned OCR (first 200 chars):")
print(corrected_text[:200])

# -------------------------------------------------
# Step 5 – Write to file
# -------------------------------------------------
output_path = "YOUR_DIRECTORY/output_text.txt"
with open(output_path, "w", encoding="utf-8") as out_file:
    out_file.write(corrected_text)

print(f"\nProcessing complete: input_image.png → {output_path}")

# -------------------------------------------------
# Step 6 – Free AI resources
# -------------------------------------------------
spell_checker.free_resources()
```

تشغيل هذا السكريبت سينتج ملف `output_text.txt` يحتوي على النص المنقّح لصورتك.

---

## الخلاصة

لقد استعرضنا طريقة عملية **لتحويل الصورة إلى نص** باستخدام Aspose OCR، ثم **تنظيف نص OCR** بأسلوب بايثون مع مدقق إملائي AI. الحل مستقل، يتطلب ملف بايثون واحد فقط، ويعمل على Windows، macOS، أو Linux.

إذا كنت تبحث عن الخطوة التالية، فكر في:

* **كيفية استخراج نص الصورة** من ملفات PDF عبر تحويل الصفحات إلى صور أولاً.  
* تغذية النص المنقّح إلى نموذج تلخيص لتوليد تقارير تلقائية.  
* تخزين النتائج في قاعدة بيانات متجهات للبحث الدلالي.

جرّبه، عدّل معلمات النموذج، ودع خط أنابيب OCR‑to‑text يصبح أداة أساسية في صندوق أدوات استيعاب البيانات الخاص بك. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}