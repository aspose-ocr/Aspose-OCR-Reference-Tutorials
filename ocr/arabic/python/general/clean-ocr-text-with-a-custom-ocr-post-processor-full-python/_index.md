---
category: general
date: 2026-06-22
description: تعلم كيفية تنظيف نص OCR باستخدام معالج ما بعد OCR في بايثون. كود خطوة
  بخطوة، شروحات، ونصائح للحصول على مخرجات JSON منظمة وموثوقة.
draft: false
keywords:
- clean OCR text
- OCR post processor
- Python OCR workflow
- structured JSON OCR
- OCR confidence averaging
language: ar
og_description: نظّف نص OCR فورًا بإضافة معالج ما بعد OCR. يوضح هذا الدليل التنفيذ
  الكامل بلغة Python، ولماذا يعمل، وكيفية تكييفه.
og_title: تنظيف نص OCR باستخدام معالج ما بعد OCR مخصص – دليل بايثون
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to clean OCR text using an OCR post processor in Python.
    Step‑by‑step code, explanations, and tips for reliable structured JSON output.
  headline: Clean OCR Text with a Custom OCR Post Processor – Full Python Guide
  type: TechArticle
tags:
- OCR
- Python
- post‑processing
title: تنظيف نص OCR باستخدام معالج ما بعد OCR مخصص – دليل بايثون كامل
url: /ar/python/general/clean-ocr-text-with-a-custom-ocr-post-processor-full-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنظيف نص OCR باستخدام معالج ما بعد OCR مخصص – دليل Python كامل

هل احتجت يوماً إلى **تنظيف نص OCR** لكن المخرجات الخام كانت مليئة بفواصل الأسطر، والمسافات العشوائية، والأحرف ذات الثقة المنخفضة؟ لست وحدك. في العديد من خطوط الأنابيب الواقعية، يمنحك محرك OCR كتلة نصية مع درجة الثقة، وتبقى لك مهمة تحويلها إلى شيء مفيد.  

الخبر السار؟ معالج **ما بعد OCR** صغير يمكنه ترتيب النتيجة، حساب متوسط الثقة، وحتى تجميع كل شيء في سلسلة JSON مرتبة — كل ذلك دون لمس محرك OCR الأساسي. في هذا الدرس سنبني ذلك المعالج، نسجله مع محرك AI/OCR عام، ونستعرض كل سطر من الشيفرة حتى تتمكن من إضافته إلى مشروعك غداً.

---

## ما يغطيه هذا الدرس

- كيفية إنشاء معالج **نص OCR نظيف** يقوم بتطبيع الفراغات وإزالة فواصل الأسطر.  
- لماذا حساب **متوسط الثقة** مفيد للتحقق اللاحق.  
- تسجيل المعالج مع محرك OCR (نمط `ai.set_post_processor`).  
- عرض الـ JSON الهيكلي الناتج ومعالجة الحالات الطرفية الشائعة.  

لا تحتاج إلى مكتبات خارجية غير مكتبة Python القياسية، لذا يمكنك المتابعة على أي نظام يدعم Python 3.8+.

---

## المتطلبات المسبقة

- محرك OCR يعمل ويُظهر كائن `ocr_result` يحتوي على `text`، `confidence` (قائمة من القيم العشرية)، و`bounding_boxes`.  
- إلمام أساسي بدوال Python ومعالجة JSON.  
- اختياريًا: بيئة افتراضية للحفاظ على الاعتمادات مرتبة.  

إذا لم تكن متأكدًا ما إذا كان محركك يدعم معالجات ما بعد مخصصة، تحقق من وثائقه للعثور على طريقة `set_post_processor` — معظم SDKs الحديثة المدعومة بالذكاء الاصطناعي توفر ذلك.

---

## الخطوة 1: تعريف معالج ما بعد OCR **تنظيف نص OCR**

أولًا، نكتب دالة تستقبل نتيجة OCR الخام، تنظف النص، تحسب مقياس الثقة، وتعيد سلسلة JSON. لاحظ كيف تم التعليق على كل عملية؛ هذه التعليقات هي “السبب” الذي يحب المساعدون الذكائيون الإشارة إليه.

```python
import json

def create_structured_json(ocr_result, **kwargs):
    """
    Turn an OCR result into a clean, structured JSON payload.

    Parameters
    ----------
    ocr_result : object
        Must expose .text (raw string), .confidence (list of floats),
        and .bounding_boxes (list of box coordinates).

    Returns
    -------
    str
        JSON string with cleaned text, average confidence, and bounding boxes.
    """
    # 1️⃣ Clean the raw text: replace newlines with spaces and trim excess whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # 2️⃣ Compute the average confidence – useful for quality gating.
    # Guard against division by zero if the engine returns an empty list.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0  # fallback when confidence data is missing

    # 3️⃣ Preserve the original bounding boxes for downstream layout analysis.
    boxes = ocr_result.bounding_boxes

    # 4️⃣ Assemble the dictionary and dump it as a JSON string.
    data = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }

    # ensure_ascii=False keeps Unicode characters intact (think accented letters, emojis, etc.)
    return json.dumps(data, ensure_ascii=False)
```

**لماذا يعمل هذا:**  
- `replace("\n", " ")` يحول مخرجات OCR متعددة الأسطر إلى سلسلة واحدة قابلة للبحث — وهذا ما يعنيه “نص OCR نظيف” في معظم خطوط الأنابيب.  
- إزالة الفراغات في البداية والنهاية تتجنب الرموز الفارغة الوهمية التي قد تُعطل المحللات لاحقًا.  
- حساب متوسط الثقة يمنحك مقياس جودة واحد؛ يمكنك رفض النتائج التي تقل عن عتبة معينة (مثلاً 0.85) قبل حفظها في قاعدة البيانات.  
- ترك صناديق الحدود (bounding boxes) دون تعديل يعني أنه لا يزال بإمكانك عرض التخطيط الأصلي إذا احتجت لتسليط الضوء على المناطق منخفضة الثقة.

---

## الخطوة 2: تسجيل **معالج ما بعد OCR** المخصص مع محركك

معظم SDKs المدعومة بالذكاء الاصطناعي توفر طريقة لتوصيل دالة ما بعد المعالجة. فيما يلي نفترض وجود كائن اسمه `ai` (المحرك) يقدم `set_post_processor`. إذا كانت مكتبتك تستخدم اسمًا مختلفًا، استبدله وفقًا لذلك.

```python
# Register the post‑processor; the second argument can hold custom settings.
ai.set_post_processor(create_structured_json, custom_settings={})
```

**نصيحة:** مرّر الإعدادات عبر `custom_settings` إذا احتجت يومًا لتبديل سلوكيات (مثل تمكين/تعطيل إزالة فواصل الأسطر). هذا يجعل المعالج قابلًا لإعادة الاستخدام عبر المشاريع.

---

## الخطوة 3: تشغيل محرك OCR – النتيجة الآن سلسلة JSON

مع ربط المعالج، استدعاء `engine.recognize()` (أو أي طريقة يستخدمها SDK الخاص بك) سيستدعي تلقائيًا `create_structured_json`. ثم يُعيد المحرك كائنًا يحتوي على الخاصية `.text` التي تضم حزمة JSON بالفعل.

```python
# The engine runs OCR, then our post‑processor formats the output.
structured_result = engine.recognize()
```

> **ملاحظة:** قد تُعيد بعض SDKs سلسلة نصية عادية بدلاً من كائن يحتوي على خاصية `.text`. عدّل الخطوة التالية وفقًا لذلك.

---

## الخطوة 4: عرض (أو حفظ) مخرجات JSON الهيكلية

أخيرًا، نطبع الـ JSON على وحدة التحكم. في بيئة الإنتاج قد تفضّل كتابة ذلك إلى ملف، أو طابور رسائل، أو قاعدة بيانات.

```python
# Show the clean OCR text and additional metadata.
print("Structured JSON:", structured_result.text)
```

**الناتج المتوقع على وحدة التحكم** (منسق للقراءة):

```json
{
  "clean_text": "The quick brown fox jumps over the lazy dog.",
  "average_confidence": 0.9375,
  "boxes": [
    [0, 0, 120, 30],
    [0, 35, 115, 30],
    ...
  ]
}
```

إذا لاحظت وجود أحرف سطر جديدة عشوائية أو قيمة ثقة `0.0`، تحقق من أن محرك OCR يملأ فعليًا `ocr_result.confidence`. جملة الحماية في المعالج ستحميك من `ZeroDivisionError`، لكنك ما زلت بحاجة لمعرفة سبب فقدان بيانات الثقة.

---

## معالجة الحالات الطرفية الشائعة

| الحالة | ما يجب مراقبته | الحل السريع |
|-----------|-------------------|-----------|
| **نتيجة OCR فارغة** | `ocr_result.text` يساوي `""` وقائمة `confidence` فارغة | المعالج يُعيد بالفعل `clean_text` فارغ و`average_confidence` = 0.0. يمكنك إضافة إرجاع مبكر إذا رغبت بتخطي توليد JSON تمامًا. |
| **حروف غير ASCII** | Unicode يتم هروبه (`\u00e9`) | استخدم `ensure_ascii=False` (موجود بالفعل في الشيفرة) للحفاظ على حروف مثل “é” قابلة للقراءة. |
| **وثائق طويلة جدًا** | قد يتجاوز حجم JSON حدود API | فكر في بث الإخراج أو كتابة إلى ملف بدلاً من إرجاع سلسلة واحدة. |
| **صناديق الحدود مفقودة** | بعض محركات OCR لا تُصدر بيانات التخطيط | عيّن `boxes` إلى `None` أو قائمة فارغة؛ يجب على المستهلكين اللاحقين التعامل مع الغياب بأريحية. |

---

## نصائح احترافية وأفضل الممارسات

- **المعالجة الدفعية:** إذا كنت تحتاج إلى OCR لمئات الصفحات، ضع استدعاء التعرف داخل حلقة واجمع كل حزمة JSON في قائمة. ثم صُد القائمة إلى ملف واحد لتسهيل التحليل الدفعي.  
- **عتبات الثقة:** قبل الحفظ، افحص `average_confidence`. قاعدة عامة: ارفض أي نتيجة أقل من `0.80` للمهام الحرجة لإدخال البيانات.  
- **التسجيل بدلاً من الطباعة:** في الإنتاج، استبدل `print()` بمسجل منظم (`logging.info(...)`) لتتبع أي صور أنتجت نتائج منخفضة الثقة.  
- **الاختبار:** اكتب اختبار وحدة يزوّد `ocr_result` مزيفًا بنص معروف وقيم ثقة، ثم يتحقق من أن بنية JSON تتطابق مع التوقعات.  

---

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي السكربت الكامل الذي يمكنك نسخه إلى ملف باسم `ocr_cleanup.py`. تأكد من استبدال الكائنات النائبة `engine` و`ai` بالنسخ الفعلية من SDK OCR الخاص بك.

```python
import json

# ----------------------------------------------------------------------
# Step 1: Define the post‑processor that cleans OCR text and builds JSON.
# ----------------------------------------------------------------------
def create_structured_json(ocr_result, **kwargs):
    """
    Convert raw OCR output into a clean JSON string.
    """
    # Clean the raw text: collapse newlines, trim whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # Safely compute average confidence.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0

    # Keep bounding boxes for layout work.
    boxes = ocr_result.bounding_boxes

    payload = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }
    return json.dumps(payload, ensure_ascii=False)

# ----------------------------------------------------------------------
# Step 2: Register the post‑processor with the OCR engine.
# ----------------------------------------------------------------------
# Replace `ai` with your actual engine/controller instance.
ai.set_post_processor(create_structured_json, custom_settings={})

# ----------------------------------------------------------------------
# Step 3: Run OCR – the result is automatically transformed.
# ----------------------------------------------------------------------
structured_result = engine.recognize()

# ----------------------------------------------------------------------
# Step 4: Output the structured JSON.
# ----------------------------------------------------------------------
print("Structured JSON:", structured_result.text)
```

احفظ الملف، شغّله بـ `python ocr_cleanup.py`، وسترى سلسلة JSON منسقة بشكل جميل تحتوي على **نص OCR نظيف**، متوسط درجة الثقة، وصناديق الحدود الأصلية.

---

## الخلاصة

أصبح لديك الآن طريقة جاهزة للإنتاج **لتنظيف نص OCR** باستخدام معالج ما بعد OCR مخصص في Python. الحل يطبع الفراغات، يحمي من نقص بيانات الثقة، ويعيد حزمة JSON ذاتية الوصف يمكن للخدمات اللاحقة استهلاكها دون الحاجة إلى معالجة إضافية.  

من هنا يمكنك:

- توسيع المعالج لت **تصفية الكلمات منخفضة الثقة** قبل بناء `clean_text`.  
- إضافة **كشف اللغة** لتوجيه الـ JSON إلى خطوط أنابيب مخصصة حسب اللغة.  
- دمج هذا المعالج مع مكتبات **التدقيق الإملائي** للحصول على طبقة جودة إضافية.  

لا تتردد في تعديل الشيفرة، تجربة عتبات ثقة مختلفة، أو مشاركة تحسيناتك في التعليقات. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}