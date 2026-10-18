---
category: general
date: 2026-01-02
description: تعلم كيفية تسجيل الذكاء الاصطناعي باستخدام Aspose OCR مع مسجل مخصص. يغطي
  هذا الدليل مثالًا على مسجل مخصص، وكيفية استيراد Aspose OCR وتعيين مسجل مخصص.
draft: false
keywords:
- how to log ai
- use custom logger
- custom logger example
- import aspose ocr
- set custom logger
language: ar
og_description: تعلم كيفية تسجيل الذكاء الاصطناعي باستخدام Aspose OCR مع مسجل مخصص.
  اتبع الدليل خطوة بخطوة لاستيراد Aspose OCR، وتعيين مسجل مخصص، ورؤية النتيجة.
og_title: كيفية تسجيل الذكاء الاصطناعي باستخدام Aspose OCR – مثال على مسجل مخصص
tags:
- Aspose OCR
- Python
- Logging
title: كيفية تسجيل الذكاء الاصطناعي باستخدام Aspose OCR – مثال على مسجل مخصص
url: /ar/python/general/how-to-log-ai-with-aspose-ocr-custom-logger-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تسجيل AI باستخدام Aspose OCR – مثال على مسجل مخصص

هل تساءلت يومًا **كيف تسجل AI** عندما تلعب بـ Aspose OCR؟ ربما جرّبت مسجل وحدة التحكم الافتراضي وفكرت، “هذا جيد، لكن هل يمكنني جعله أكثر جاذبية أو إرسال السجلات إلى ملف؟” لست وحدك. في هذا الدرس سنستعرض مثالًا كاملًا على **مسجل مخصص**، نُظهر لك الشيفرة الدقيقة التي تحتاجها، ونشرح *لماذا* كل جزء مهم.

بنهاية هذا الدليل ستتمكن من:

* **استيراد Aspose OCR** في بايثون دون أي مشاكل.  
* **تعيين مسجل مخصص** يلتقط كل رسالة يصدرها محرك AI.  
* التحقق من المخرجات وتكييف المسجل مع إطار التسجيل الخاص بك.

لا حاجة لأي وثائق خارجية—كل ما تحتاجه موجود هنا.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

| المتطلب | السبب |
|-------------|--------|
| Python 3.8+ | حزمة `asposeocr` تستهدف إصدارات بايثون الحديثة. |
| مكتبة `asposeocr` مثبتة (`pip install asposeocr`) | توفر وحدة `asposeocr.ai` التي سنستخدمها. |
| إلمام أساسي بالدوال والقابلات (callables) | مطلوب لإنشاء مسجل مخصص. |

إذا كان أي من هذه غير متوفر، قم بتثبيت المكتبة الآن:

```bash
pip install asposeocr
```

---

## الخطوة 1 – استيراد Aspose OCR ووحدة AI

أول شيء تقوم به عندما تريد **استيراد Aspose OCR** هو سحب مساحة الاسم `asposeocr.ai`. هذا يمنحك الوصول إلى الفئة `AsposeAI`، وهي نقطة الدخول لجميع عمليات OCR المدعومة بالذكاء الاصطناعي.

```python
# Step 1: Import the Aspose OCR AI module
import asposeocr.ai as ai
```

*لماذا هذا مهم:* استيراد الوحدة الصحيحة يضمن أنك تتواصل مع الواجهة الخلفية المناسبة. إذا فاتك استيراد الوحدة الفرعية `.ai` ستحصل فقط على API OCR التقليدي، الذي لا يوفّر نقاط الربط الخاصة بالتسجيل التي نحتاجها.

---

## الخطوة 2 – إنشاء محرك AI الافتراضي (مسجل وحدة التحكم)

يأتي Aspose OCR مع مسجل مدمج يكتب مباشرة إلى `stdout`. لنشغله حتى تتمكن من رؤية السلوك الأساسي.

```python
# Step 2: Create an AI engine that logs to the console by default
default_engine = ai.AsposeAI()
```

عند تشغيل أي عملية OCR باستخدام `default_engine`، ستظهر لك رسائل مثل:

```
[INFO] AsposeAI initialized – version 23.10
[DEBUG] Loading language model...
```

هذه الرسائل مفيدة للتصحيح السريع، لكنها ليست مرنة بما يكفي لبيئات الإنتاج. لذلك ننتقل إلى الخطوة التالية.

---

## الخطوة 3 – تعريف مسجل مخصص (أي callable يقبل سلسلة)

**المسجل المخصص** يمكن أن يكون أي callable في بايثون يأخذ معاملًا واحدًا من نوع `str`. المثال الأدنى يضيف بادئة `[AI LOG]` إلى كل رسالة. يمكنك استبدال `print` بـ `logging.info`، أو الكتابة إلى ملف، أو إرسالها إلى خدمة مراقبة.

```python
# Step 3: Define a custom logger (any callable that accepts a string)
def custom_logger(message: str):
    # You could replace this with `logging.info(message)` or any other sink.
    print("[AI LOG]", message)
```

*لماذا هذا يعمل:* مُنشئ `AsposeAI` يبحث عن معامل `logging` يطبق بروتوكول “استدعاء‑مع‑سلسلة”. بتوفير دالة تتطابق مع هذا التوقيع، تمنحك السيطرة الكاملة على طريقة معالجة كل سطر سجل.

---

## الخطوة 4 – إنشاء محرك AI يستخدم المسجل المخصص

الآن نجمع كل شيء معًا. مرّر `custom_logger` إلى مُنشئ `AsposeAI` عبر معامل `logging`. سيقوم المحرك بتمرير كل رسالة داخلية إلى دالتك.

```python
# Step 4: Create an AI engine that uses the custom logger
engine_with_custom_logger = ai.AsposeAI(logging=custom_logger)
```

### المخرجات المتوقعة

تشغيل استدعاء OCR بسيط (مثل `engine_with_custom_logger.recognize("sample.png")`) سيولد مخرجات مشابهة لـ:

```
[AI LOG] AsposeAI initialized – version 23.10
[AI LOG] Loading language model...
[AI LOG] Model loaded successfully.
[AI LOG] Starting OCR on sample.png
[AI LOG] OCR completed – 98% confidence.
```

لاحظ كيف أن كل سطر يبدأ الآن بـ `[AI LOG]`، تمامًا كما عرّفنا في `custom_logger`. هذا يثبت أن **كيفية تسجيل AI** تحت سيطرتك بالكامل.

---

## مثال كامل يعمل – من الاستيراد إلى التنفيذ

فيما يلي السكربت الكامل الذي يمكنك نسخه‑لصقه في ملف اسمه `custom_logger_demo.py`. يوضح التدفق الكامل، من استيراد Aspose OCR إلى إجراء طلب OCR بسيط باستخدام المسجل المخصص.

```python
# custom_logger_demo.py
# -------------------------------------------------
# Demonstrates how to log AI using Aspose OCR
# with a user‑defined logger.
# -------------------------------------------------

import asposeocr.ai as ai

def custom_logger(message: str):
    """A tiny logger that prefixes messages."""
    print("[AI LOG]", message)

def main():
    # Use the custom logger when creating the AI engine
    ocr_engine = ai.AsposeAI(logging=custom_logger)

    # Path to an image you want to process (replace with your own)
    image_path = "sample.png"

    # Perform OCR – this will trigger the logger
    try:
        result = ocr_engine.recognize(image_path)
        print("\n--- OCR RESULT ---")
        print(result.text)  # Assuming the result object has a `text` attribute
    except Exception as e:
        print("[AI LOG] Error during OCR:", e)

if __name__ == "__main__":
    main()
```

**ما المتوقع عند تشغيله**

```bash
python custom_logger_demo.py
```

```
[AI LOG] AsposeAI initialized – version 23.10
[AI LOG] Loading language model...
[AI LOG] Model loaded successfully.
[AI LOG] Starting OCR on sample.png
[AI LOG] OCR completed – 98% confidence.

--- OCR RESULT ---
Hello world! This is the extracted text.
```

إذا رغبت في **تعيين مسجل مخصص** إلى ملف، ما عليك سوى استبدال `print` في `custom_logger` بشيء مثل:

```python
def file_logger(message: str):
    with open("ocr.log", "a", encoding="utf-8") as f:
        f.write(message + "\n")
```

وتمرير `logging=file_logger` عند إنشاء `AsposeAI`.

---

## أسئلة شائعة وحالات حافة

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني استخدام وحدة `logging` القياسية؟* | بالتأكيد. فقط قم بتهيئة كائن مسجل ومرّر `logger.info(message)` داخل الدالة القابلة للاستدعاء. |
| *ماذا لو ألقى مسجلي استثناءً؟* | SDK يلتقط أي استثناء من المسجل ويستمر، لكنك ستفقد تلك الرسالة المحددة. حافظ على البساطة. |
| *هل يتلقى المسجل رسائل مستوى DEBUG أيضًا؟* | نعم. محرك AI يرسل **جميع** الرسائل الداخلية (INFO، DEBUG، WARN). يمكنك الفلترة داخل الدالة إذا أردت مستويات معينة فقط. |
| *هل معامل `logging` اختياري؟* | إذا تُرك، يعود المحرك إلى المسجل المدمج في وحدة التحكم. |
| *هل سيعمل هذا مع الكود غير المتزامن (async)؟* | المسجل نفسه متزامن؛ إذا احتجت إلى معالجة غير متزامنة، غلف الاستدعاء داخل coroutine `asyncio` واستخدم `await` حسب الحاجة. |

---

## نصائح احترافية – جعل مسجلك جاهزًا للإنتاج

1. **الكتابة على دفعات** – فتح وإغلاق الملف لكل رسالة بطيء. استخدم `logging.FileHandler` مع التخزين المؤقت.  
2. **إضافة طوابع زمنية** – أضف `datetime.now().isoformat()` إلى البادئة لتسهيل عملية التصحيح.  
3. **مستويات السجل** – إذا احتجت إلى دقة أكبر، غيّر التوقيع ليقبل زوجًا مثل `(level, message)` وعدّل استدعاء SDK (حاليًا يمرر سلسلة فقط، لذا يمكنك تحليل كلمات المستوى يدويًا).  
4. **مركزية الإعدادات** – احتفظ بتعريف المسجل في وحدة منفصلة (`my_logging.py`) واستوردها أينما تحتاج إلى إنشاء كائن `AsposeAI`.  

هذه الحيل تساعدك على الإجابة ليس فقط على *كيفية تسجيل AI*، بل على *كيفية تسجيل AI بفعالية* في الخدمات الواقعية.

---

## الخلاصة

غطّينا **كيفية تسجيل AI** باستخدام Aspose OCR من البداية إلى النهاية: استيراد المكتبة، إنشاء محرك افتراضي، كتابة **مثال على مسجل مخصص**، وأخيرًا ربط ذلك المسجل بمحرك AI. الشيفرة كاملة، قابلة للتنفيذ، ويمكن تعديلها لتتناسب مع أي نظام تسجيل تفضله.

إذا كنت مستعدًا للخطوة التالية، جرّب استبدال المسجل القائم على `print` بوحدة `logging` في بايثون، أو أرسل السجلات إلى خدمة سحابية مثل Datadog، أو حتى أصدر JSON منظم للتحليل اللاحق. النمط يبقى نفسه—**استخدم مسجلًا مخصصًا** و**عيّن مسجلًا مخصصًا** عند إنشاء `AsposeAI`.

برمجة سعيدة، ولتكن سجلاتك دائمًا واضحة كما نتائج OCR الخاصة بك!

---

![how to log ai screenshot](image.png "how to log ai example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}