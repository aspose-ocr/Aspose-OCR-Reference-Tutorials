---
category: general
date: 2026-06-28
description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على الصورة باستخدام Aspose AI
  واستخراج النص العادي من الصورة ببضع أسطر فقط من بايثون. دليل خطوة بخطوة للتكامل
  السريع.
draft: false
keywords:
- perform OCR on image
- extract plain text from image
- Aspose AI OCR
- Python OCR tutorial
- spell‑check post‑processor
- OCR result handling
language: ar
og_description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على الصورة باستخدام Aspose
  AI واستخراج النص العادي من الصورة بسهولة. تعلم سير العمل الكامل في هذا الدرس المختصر.
og_title: إجراء التعرف الضوئي على الأحرف في الصورة باستخدام Aspose AI – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Perform OCR on image using Aspose AI and extract plain text from image
    in just a few lines of Python. Step‑by‑step tutorial for fast integration.
  headline: Perform OCR on Image with Aspose AI – Complete Guide
  type: TechArticle
- questions:
  - answer: Aspose’s OCR engine works best with 300 dpi or higher. If you’re dealing
      with lower quality scans, consider pre‑processing the image (e.g., sharpening,
      binarisation) before feeding it to `engine.set_image`.
    question: What if the image is low‑resolution?
  - answer: Yes. Loop over a list of image files, re‑using the same `engine` and `ai`
      instances. Just remember to call `engine.set_image` for each new file.
    question: Can I process multiple pages?
  - answer: Only on the first run, when the AI model is downloaded. After that, everything
      runs offline from the cached directory you specified.
    question: Do I need an internet connection?
  - answer: 'Pass a language code in the options dictionary, e.g., `ai.set_post_processor(AIProcessor.SpellCheck,
      {"lang": "fr"})` for French.'
    question: How do I change the language of the spell‑check?
  type: FAQPage
tags:
- OCR
- Python
- Aspose
- AI
title: إجراء التعرف الضوئي على الحروف في الصورة باستخدام Aspose AI – دليل شامل
url: /ar/python/general/perform-ocr-on-image-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على الصورة باستخدام Aspose AI – دليل كامل

هل تساءلت يومًا كيف **تُجري OCR على الصورة** دون التعامل مع مكتبات ثقيلة؟ في العديد من التطبيقات الواقعية تحتاج فقط إلى استخراج النص من فاتورة أو إيصال ممسوح ضوئيًا، ثم ربما تنظيفه باستخدام مدقق إملائي. الخبر السار هو أن Aspose AI يجعل ذلك سهلًا للغاية، ويمكنك أيضًا **استخراج النص العادي من الصورة** في سكريبت واحد واضح.

في هذا الدرس سنستعرض كامل سير العمل: تحميل صورة، تشغيل OCR، الحصول على النتائج الخام والمُهيكلة، تطبيق معالج ما بعد التدقيق الإملائي المدمج، وأخيرًا تنظيف الموارد. في النهاية ستحصل على مثال بايثون جاهز للتنفيذ يمكنك إدراجه في مشروعك الخاص.

![مثال على إجراء OCR على الصورة](image.png "مخطط يوضح خط أنابيب OCR – إجراء OCR على الصورة")

## ما ستتعلمه

- كيفية تهيئة محرك Aspose OCR وتزويده بملف صورة.  
- الفرق بين مخرجات السلسلة العادية و`OcrResult` المُهيكلة التي تحتفظ بالتخطيط.  
- كيفية ربط جسر Aspose AI، تحميل النموذج تلقائيًا، وتوجيهه إلى مجلد تخزين مؤقت مخصص.  
- استخدام معالج ما بعد التدقيق الإملائي لاستخراج **النص العادي من الصورة** مع تصحيح الإملاء مع الحفاظ على الصناديق المحيطة.  
- نصائح أفضل الممارسات لتحرير موارد AI وتجنب تسرب الذاكرة.  

لا تحتاج إلى خبرة سابقة مع Aspose—فقط بيئة Python 3 تعمل وصورة من اختيارك. لنبدأ.

## الخطوة 1 – تهيئة محرك OCR وتحميل صورتك

أول شيء تحتاج إلى فعله هو تشغيل محرك OCR وتوجيهه إلى الصورة التي تريد قراءتها. فكر في المحرك كماسح يحول البكسلات إلى أحرف.

```python
# Step 1: Initialise the OCR engine and load the image
engine = OcrEngine()
engine.set_image(Image.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **لماذا هذا مهم:** `OcrEngine()` ينشئ جلسة جديدة، بينما `set_image` يخبر المحرك بالملف الذي يجب تحليله بالضبط. إذا تخطيت هذه الخطوة، فإن استدعاءات `recognize` اللاحقة ستثير استثناءً لأنه لا يوجد شيء لمعالجته.

## الخطوة 2 – إجراء OCR والحصول على النتائج العادية والمُهيكلة

الآن نقوم فعليًا **بإجراء OCR على الصورة**. Aspose يقدم لك نوعين من المخرجات:

1. `plain_text` – سلسلة بسيطة، مثالية عندما تحتاج فقط إلى الكلمات.  
2. `structured` – كائن `OcrResult` يحتفظ بفواصل الأسطر، الصناديق المحيطة، وغيرها من بيانات التخطيط.

```python
# Step 2: Perform OCR – obtain plain text and structured result
plain_text = engine.recognize()                # plain string
structured = engine.recognize_structured()    # OcrResult with layout info
```

> **نصيحة احترافية:** استخدم `plain_text` عندما يهمك فقط الأحرف (مثل البحث في مستند). استخدم `structured` عندما تحتاج إلى ربط النص بموقعه الأصلي، مثل تمييز الأخطاء على المسح الأصلي.

## الخطوة 3 – تهيئة جسر Aspose AI (تحميل النموذج عند الاستخدام الأول)

Aspose AI هو الدماغ الذي يشغل معالج ما بعد التدقيق الإملائي. في المرة الأولى التي تشغّله فيها، سيتم تحميل النموذج تلقائيًا. يمكنك أيضًا توفير مجلد مخصص لتخزين النموذج مؤقتًا، مما يسرّع التشغيلات اللاحقة.

```python
# Step 3: Initialise the Aspose AI bridge (model will be downloaded on first use)
# Optional: specify a custom directory for the cached model
ai_config = AsposeAIModelConfig()
ai_config.directory_model_path = "YOUR_DIRECTORY/models"
ai = AsposeAI(ai_config)
```

> **لماذا هذا مهم:** تخزين النموذج مؤقتًا يجنّب استدعاءات الشبكة المتكررة ويحافظ على استجابة تطبيقك، خاصة في بيئات الإنتاج.

## الخطوة 4 – تسجيل معالج ما بعد التدقيق الإملائي المدمج

Aspose يأتي مع معالج تدقيق إملائي مفيد يعمل على السلاسل العادية وكذلك نتائج OCR المُهيكلة. سجّله مرة واحدة، وستكون جاهزًا لتنظيف أي أخطاء إملائية ناتجة عن OCR.

```python
# Step 4: Register the built‑in spell‑check post‑processor
ai.set_post_processor(AIProcessor.SpellCheck, {})
```

> **ملاحظة:** القاموس الفارغ `{}` هو المكان الذي يمكنك فيه تمرير قواميس مخصصة أو إعدادات لغة إذا احتجت إلى مزيد من التحكم.

## الخطوة 5 – تطبيق التدقيق الإملائي على نص OCR العادي

هنا نُجري **استخراج النص العادي من الصورة** مع تصحيح الأخطاء الإملائية في آنٍ واحد. طريقة `run_postprocessor` تأخذ السلسلة الخام وتعيد نسخة مُنقّحة.

```python
# Step 5: Apply spell‑check to the plain OCR text
corrected_text = ai.run_postprocessor(plain_text)
print("Corrected:", corrected_text)
```

الناتج المتوقع (مثال):

```
Corrected: Invoice Number 2023‑07‑15
Date: 07/15/2023
Total Amount: $1,250.00
```

> **لماذا هذا مهم:** غالبًا ما تُخطئ محركات OCR في التعرف على أحرف مثل “0” مقابل “O” أو “1” مقابل “l”. خطوة التدقيق الإملائي تُصقل هذه الأخطاء، مما يمنحك بيانات أنظف للمعالجة اللاحقة.

## الخطوة 6 – تطبيق التدقيق الإملائي على نتيجة OCR المُهيكلة (يحافظ على الصناديق المحيطة)

إذا كنت بحاجة للحفاظ على التخطيط الأصلي—مثلاً لتسليط الضوء على الكلمات المصححة في المستند الممسوح—يمكنك تمرير النتيجة المُهيكلة إلى نفس المعالج. الكائن المُعاد لا يزال يحتوي على معلومات الأسطر.

```python
# Step 6: Apply spell‑check to the structured OCR result (preserves bounding boxes)
corrected_struct = ai.run_postprocessor(structured)
for line in corrected_struct.Lines:
    print(line.Text)
```

مثال على مخرجات وحدة التحكم:

```
Invoice Number 2023‑07‑15
Date: 07/15/2023
Total Amount: $1,250.00
```

> **نصيحة احترافية:** لأن مجموعة `Lines` تحتفظ بإحداثيات `BoundingBox`، يمكنك الآن وضع النص المصحح فوق الصورة الأصلية باستخدام أي مكتبة رسومية (Pillow، OpenCV، إلخ).

## الخطوة 7 – تحرير موارد AI عند الانتهاء

تسرب الذاكرة هو القاتل الصامت للخدمات طويلة التشغيل. حرّر دائمًا موارد AI بمجرد الانتهاء من العمل.

```python
# Step 7: Release AI resources when done
ai.free_resources()
```

> **لماذا هذا مهم:** `free_resources()` يغلق الخيوط الخلفية ويُفرغ النموذج من الذاكرة، مما يبقي تطبيقك خفيفًا.

## مثال كامل يعمل

بدمج كل ما سبق، إليك السكريبت الكامل الذي يمكنك نسخه ولصقه وتشغيله (فقط استبدل `YOUR_DIRECTORY` بالمسارات الفعلية):

```python
from aspose.ocr import OcrEngine, Image
from aspose.ai import AsposeAI, AsposeAIModelConfig, AIProcessor

# Initialise OCR engine
engine = OcrEngine()
engine.set_image(Image.from_file("YOUR_DIRECTORY/invoice.png"))

# Perform OCR
plain_text = engine.recognize()
structured = engine.recognize_structured()

# Initialise Aspose AI bridge
ai_config = AsposeAIModelConfig()
ai_config.directory_model_path = "YOUR_DIRECTORY/models"
ai = AsposeAI(ai_config)

# Register spell‑check post‑processor
ai.set_post_processor(AIProcessor.SpellCheck, {})

# Correct plain text
corrected_text = ai.run_postprocessor(plain_text)
print("Corrected:", corrected_text)

# Correct structured result
corrected_struct = ai.run_postprocessor(structured)
for line in corrected_struct.Lines:
    print(line.Text)

# Clean up
ai.free_resources()
```

شغّل السكريبت، وسترى الناتج المصحح يُطبع على وحدة التحكم. هذا هو سير عمل **إجراء OCR على الصورة** بالكامل من البداية إلى النهاية.

## أسئلة شائعة وحالات حافة

- **ماذا لو كانت الصورة منخفضة الدقة؟**  
  يعمل محرك OCR الخاص بـ Aspose بأفضل شكل مع 300 dpi أو أعلى. إذا كنت تتعامل مع مسحات ذات جودة أقل، فكر في معالجة الصورة مسبقًا (مثل الشحذ أو التحويل إلى أبيض وأسود) قبل تمريرها إلى `engine.set_image`.

- **هل يمكنني معالجة صفحات متعددة؟**  
  نعم. يمكنك التكرار على قائمة من ملفات الصور، وإعادة استخدام نفس كائنات `engine` و`ai`. فقط تذكّر استدعاء `engine.set_image` لكل ملف جديد.

- **هل أحتاج إلى اتصال بالإنترنت؟**  
  فقط في التشغيل الأول عندما يتم تحميل نموذج AI. بعد ذلك، يعمل كل شيء دون اتصال من الدليل المخزن مؤقتًا الذي حددته.

- **كيف أغيّر لغة التدقيق الإملائي؟**  
  مرّر رمز اللغة في قاموس الخيارات، مثال: `ai.set_post_processor(AIProcessor.SpellCheck, {"lang": "fr"})` للغة الفرنسية.

## الخلاصة

أنت الآن تعرف بالضبط كيفية **إجراء OCR على الصورة** باستخدام Aspose AI وكيفية **استخراج النص العادي من الصورة** مع تصحيح الأخطاء الشائعة تلقائيًا. غطى الدرس تهيئة المحرك، النتائج العادية مقابل المُهيكلة، تخزين النموذج مؤقتًا، دمج التدقيق الإملائي، وتنظيف الموارد بشكل صحيح.

من هنا يمكنك استكشاف إضافة قواميس مخصصة، تمرير النص المصحح إلى خط أنابيب NLP لاحق، أو رسم الصناديق المحيطة مرة أخرى على المسح الأصلي للتحقق البصري. الاحتمالات كثيرة، والقاعدة التي أنشأتها الآن هي أساس قوي.

لا تتردد في التجربة—غيّر الصورة، عدّل إعدادات المعالج، أو ربط وحدات AI إضافية. إذا واجهت أي مشكلة، اترك تعليقًا أدناه؛ برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية استخدام Aspose OCR للحصول على نتيجة JSON في التعرف على الصور](/ocr/english/net/text-recognition/get-result-as-json/)
- [التعرف على نص الصورة باستخدام Aspose OCR لعدة لغات](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}