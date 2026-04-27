---
category: general
date: 2026-04-26
description: قُم بإخفاء أرقام بطاقات الائتمان بسرعة باستخدام معالجة ما بعد التعرف
  الضوئي على الأحرف AsposeAI. تعلّم الامتثال لمعيار PCI، وإخفاء باستخدام التعبيرات
  النمطية، وتنظيف البيانات في دليل خطوة بخطوة.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: ar
og_description: إخفاء أرقام بطاقات الائتمان في نتائج OCR باستخدام AsposeAI. يغطي هذا
  الدليل الالتزام بمعايير PCI، وإخفاء باستخدام التعبيرات النمطية، وتنظيف البيانات.
og_title: إخفاء أرقام بطاقات الائتمان – دليل كامل لمعالجة ما بعد التعرف الضوئي على
  الحروف باستخدام بايثون
tags:
- OCR
- Python
- security
title: إخفاء أرقام بطاقات الائتمان في مخرجات OCR – دليل بايثون الكامل
url: /ar/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إخفاء أرقام بطاقات الائتمان – دليل بايثون كامل

هل احتجت يومًا إلى **إخفاء أرقام بطاقات الائتمان** في نص يأتي مباشرةً من محرك OCR؟ لست وحدك. في الصناعات المنظمة، كشف رقم PAN الكامل (Primary Account Number) يمكن أن يضعك في مشكلة مع مدققي الامتثال PCI. الخبر السار؟ باستخدام بضع أسطر من بايثون و post‑processing hook الخاص بـ AsposeAI، يمكنك إخفاء الثمانية أرقام الوسطى تلقائيًا والبقاء في الجانب الآمن.

في هذا الدرس سنستعرض سيناريو واقعي: تشغيل OCR على صورة إيصال، ثم تطبيق دالة **معالجة ما بعد OCR** مخصصة تقوم بتنظيف أي بيانات PCI. في النهاية ستحصل على مقطع شفرة قابل لإعادة الاستخدام يمكنك إدراجه في أي سير عمل AsposeAI، بالإضافة إلى مجموعة من النصائح العملية للتعامل مع الحالات الخاصة وتوسيع الحل.

## ما ستتعلمه

- كيفية تسجيل معالج ما بعد مخصص مع **AsposeAI**.
- لماذا نهج **إخفاء باستخدام التعبير النمطي** سريع وموثوق.
- أساسيات **الامتثال PCI** المتعلقة بتنظيف البيانات.
- طرق توسيع النمط لتعدد صيغ البطاقات أو الأرقام الدولية.
- المخرجات المتوقعة وكيفية التحقق من أن الإخفاء تم بنجاح.

> **المتطلبات المسبقة** – يجب أن يكون لديك بيئة Python 3 تعمل، وحزمة Aspose.AI for OCR مثبتة (`pip install aspose-ocr`)، وصورة نموذجية (مثلاً `receipt.png`) تحتوي على رقم بطاقة ائتمان. لا توجد خدمات خارجية أخرى مطلوبة.

---

## الخطوة 1: تعريف معالج ما بعد يُخفي أرقام بطاقات الائتمان

جوهر الحل يكمن في دالة صغيرة تستقبل نتيجة OCR، وتنفذ روتين **إخفاء باستخدام التعبير النمطي**، وتعيد النص المنقّى.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**لماذا يعمل هذا:**  
- التعبير النمطي `(\d{4})\d{8}(\d{4})` يطابق بالضبط 16 رقمًا متتاليًا، وهو الصيغة الشائعة لفيزا، ماستركارد، والعديد غيرها.  
- من خلال التقاط الأربعة أرقام الأولى والأخيرة (`\1` و`\2`) نحافظ على معلومات كافية للتصحيح مع الالتزام بقواعد **PCI compliance** التي تحظر تخزين PAN الكامل.  
- الاستبدال `\1****\2` يخفي الثمانية أرقام الوسطى الحساسة، محولًا `1234567812345678` إلى `1234****5678`.

**نصيحة احترافية:** إذا كنت بحاجة لدعم أرقام American Express ذات 15 رقمًا، أضف نمطًا ثانيًا مثل `r'(\d{4})\d{6}(\d{5})'` وقم بتنفيذ كلا الاستبدالين بالتتابع.

---

## الخطوة 2: تهيئة محرك AsposeAI

قبل أن نتمكن من إرفاق معالج ما بعدنا، نحتاج إلى نسخة من محرك OCR. يجمع AsposeAI نموذج OCR وواجهة API بسيطة للمعالجة المخصصة.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**لماذا نهيئ هنا؟**  
إنشاء كائن `AsposeAI` مرة واحدة وإعادة استخدامه عبر صور متعددة يقلل من الحمل الزائد. كما يقوم المحرك بتخزين نماذج اللغة في الذاكرة المؤقتة، مما يسرّع الاستدعاءات اللاحقة—مفيد عند مسح دفعات من الإيصالات.

---

## الخطوة 3: تسجيل دالة الإخفاء المخصصة

يوفر AsposeAI طريقة `set_post_processor` التي تسمح لك بربط أي callable. نمرر دالة `mask_pci` الخاصة بنا مع قاموس إعدادات اختياري (حالياً فارغ).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**ماذا يحدث خلف الكواليس؟**  
عند استدعاء `run_postprocessor` لاحقًا، سيقوم AsposeAI بتمرير نتيجة OCR الخام إلى `mask_pci`. تستقبل الدالة كائنًا خفيفًا (`data`) يحتوي على النص المعترف به، وتعيد سلسلة جديدة. يضمن هذا التصميم بقاء نواة OCR دون تعديل مع السماح لك بفرض سياسات **تنظيف البيانات** في مكان واحد.

---

## الخطوة 4: تشغيل OCR على صورة الإيصال

الآن بعد أن علم المحرك كيفية تنظيف المخرجات، نمرره صورة. من أجل هذا الدرس نفترض أنك تمتلك كائن `engine` مُعد مسبقًا بالإعدادات الصحيحة للغة والدقة.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**نصيحة:** إذا لم يكن لديك كائن مُعد مسبقًا، يمكنك إنشائه باستخدام:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

نداء `recognize_image` يُعيد كائنًا يحتوي على الخاصية `text` التي تحمل السلسلة الخام غير المخبأة.

---

## الخطوة 5: تطبيق معالج ما بعد المسجل

مع وجود بيانات OCR الخام، نمررها إلى كائن AI. يقوم المحرك تلقائيًا بتنفيذ الدالة `mask_pci` التي سجلناها مسبقًا.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**لماذا نستخدم `run_postprocessor` بدلاً من استدعاء الدالة يدويًا؟**  
يساعد ذلك في الحفاظ على تناسق سير العمل، خاصةً عندما يكون لديك عدة معالجات ما بعد (مثل التدقيق الإملائي، اكتشاف اللغة). يقوم AsposeAI بترتيبها وفقًا لتسجيلك، مما يضمن مخرجات حتمية.

---

## الخطوة 6: التحقق من المخرجات المنقاة

أخيرًا، لنطبع النص المنقّى ونؤكد أن أي أرقام بطاقات ائتمان تم إخفاؤها بشكل صحيح.

```python
print(final_result.text)
```

**المخرجات المتوقعة** (مقتطف):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

إذا لم يحتوي الإيصال على رقم بطاقة، يبقى النص دون تغيير—لا شيء لإخفائه، ولا داعي للقلق.

---

## معالجة الحالات الخاصة والاختلافات الشائعة

### عدة أرقام بطاقات في مستند واحد
إذا كان الإيصال يحتوي على أكثر من PAN (مثلاً بطاقة ولاء بالإضافة إلى بطاقة دفع)، يعمل التعبير النمطي عالميًا، ويخفي جميع التطابقات تلقائيًا. لا حاجة إلى كود إضافي.

### تنسيق غير قياسي
أحيانًا يضيف OCR مسافات أو شرطات (`1234 5678 1234 5678` أو `1234-5678-1234-5678`). قم بتوسيع النمط لتجاهل تلك الأحرف:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

الإضافة `[ -]?` تسمح بوجود مسافات أو شرطات اختيارية بين مجموعات الأرقام.

### بطاقات دولية
لـ PAN بطول 19 رقمًا المستخدمة في بعض المناطق، يمكنك توسيع النمط:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

تذكر فقط أن **PCI compliance** لا يزال يتطلب إخفاء الأرقام الوسطى، بغض النظر عن الطول.

### تسجيل القيم المخفية (اختياري)
إذا كنت بحاجة إلى سجلات تدقيق، مرّر علمًا عبر `custom_settings` وعدّل الدالة:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

ثم سجّل باستخدام:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## مثال كامل جاهز للنسخ واللصق

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

تشغيل هذا السكريبت على إيصال يحتوي على `4111111111111111` سيُنتج:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

هذا هو سير العمل الكامل—من OCR الخام إلى **تنظيف البيانات**—مُغلف ببضع أسطر نظيفة من بايثون.

---

## الخلاصة

لقد أظهرنا لك الآن كيفية **إخفاء أرقام بطاقات الائتمان** في نتائج OCR باستخدام post‑processing hook الخاص بـ AsposeAI، روتين تعبير نمطي مختصر، ومجموعة من النصائح العملية للـ **PCI compliance**. الحل مستقل تمامًا، يعمل مع أي صورة يستطيع محرك OCR قراءتها، ويمكن توسيعه لتغطية صيغ بطاقات أكثر تعقيدًا أو متطلبات التسجيل.

هل أنت مستعد للخطوة التالية؟ جرّب ربط هذا الإخفاء مع دالة **إدخال قاعدة بيانات** تخزن الأربعة أرقام الأخيرة فقط للمرجعية، أو دمج **معالج دفعات** يمسح مجلدًا كاملاً من الإيصالات طوال الليل. يمكنك أيضًا استكشاف مهام **معالجة ما بعد OCR** أخرى مثل توحيد العناوين أو اكتشاف اللغة—كل منها يتبع نفس النمط الذي استخدمناه هنا.

هل لديك أسئلة حول الحالات الخاصة، الأداء، أو كيفية تعديل الكود لمكتبة OCR مختلفة؟ اترك تعليقًا أدناه، ولنستمر في النقاش. برمجة سعيدة، وابق آمنًا!  

![Diagram illustrating how mask credit card numbers works in an OCR pipeline](https://example.com/images/ocr-mask-flow.png "Diagram of OCR post‑processing masking flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}