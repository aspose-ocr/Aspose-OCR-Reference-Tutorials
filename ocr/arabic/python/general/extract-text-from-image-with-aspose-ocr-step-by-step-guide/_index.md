---
category: general
date: 2025-12-27
description: استخراج النص من الصورة باستخدام Aspose OCR وتصحيح أخطاء OCR. تعلم كيفية
  تحميل الصورة للتعرف الضوئي على الأحرف وإصلاح الأخطاء بسرعة.
draft: false
keywords:
- extract text from image
- load image for ocr
- how to correct ocr errors
- Aspose OCR Python
- OCR post‑processing
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR وتصحيح أخطاء OCR فورًا.
  اتبع هذا الدليل لتحميل الصورة للـ OCR وتنظيف النتائج.
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل كامل
tags:
- OCR
- Python
- Aspose
- Text Extraction
title: استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة
url: /ar/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة

هل احتجت يومًا إلى **استخراج النص من صورة** لكن واجهت مخرجات OCR فوضوية؟ لست وحدك. في العديد من مشاريع الأتمتة—مثل معالجة الفواتير، مسح الإيصالات، أو رقمنة المستندات القديمة—العقبة الأولى هي الحصول على نص نظيف وقابل للبحث من الصورة.  

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح لك كيفية **تحميل الصورة لـ OCR**، تشغيل التعرف، ثم **تصحيح أخطاء OCR** باستخدام معالج التدقيق الإملائي المدعوم بالذكاء الاصطناعي من Aspose. في النهاية ستحصل على سكريبت واحد يحول ملف PNG لفاتورة إلى نص مصقول وقابل للبحث جاهز لأي سير عمل لاحق.

## ما ستتعلمه

- كيفية تثبيت واستيراد مكتبات Aspose OCR والذكاء الاصطناعي في Python.  
- الكود الدقيق المطلوب **لتحميل الصورة لـ OCR** (بدون تخمين).  
- كيفية تشغيل محرك OCR والحصول على السلسلة الخام.  
- لماذا ينتج عن OCR غالبًا أخطاء إملائية وكيف يمكن للمعالج المدمج لتدقيق الإملاء **تصحيح أخطاء OCR** تلقائيًا.  
- نصائح للتعامل مع الحالات الخاصة مثل ملفات PDF متعددة الصفحات أو المسحات منخفضة الدقة.

> **المتطلبات المسبقة:** Python 3.8+، رخصة صالحة لـ Aspose OCR (أو نسخة تجريبية مجانية)، وملف صورة (مثال: `invoice.png`) تريد معالجته.

---

## استخراج النص من صورة – إعداد Aspose OCR

قبل أن نتمكن من فعل أي شيء، نحتاج إلى الحزم الصحيحة. توزع Aspose محرك OCR الخاص بها كوحدة يمكن تثبيتها عبر pip.

```bash
pip install aspose-ocr
```

إذا كنت تريد أيضًا معالج الذكاء الاصطناعي بعد التعرف، ثبت الحزمة المرافقة:

```bash
pip install aspose-ocr-ai
```

> **نصيحة احترافية:** حافظ على تحديث الحزم. في وقت كتابة هذا الدليل أحدث الإصدارات هي `aspose-ocr 23.12` و `aspose-ocr-ai 23.12`.

بعد أن تصبح المكتبات على نظامك، استورد الفئات التي ستستخدمها:

```python
# Step 1: Import the OCR and AI classes
from aspose.ocr import OcrEngine, AsposeAI
```

> **لماذا هذا مهم:** استيراد الفئات المحددة يحافظ على نظافة مساحة الاسم ويجعل من الواضح أي المكونات مسؤولة عن التعرف وأيها عن المعالجة اللاحقة.

---

## تحميل الصورة لـ OCR – تحضير صورة الفاتورة PNG

الخطوة المنطقية التالية هي توجيه المحرك إلى الملف الذي تريد قراءته. هنا يبرز دور كلمة المفتاح **load image for OCR**.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 3: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **شرح:** `OcrEngine()` ينشئ محركًا جديدًا بإعدادات افتراضية (اللغة الإنجليزية، التدوير التلقائي، إلخ). طريقة `load_image()` تقبل مسار ملف، أو تدفق، أو حتى مصفوفة بايت—وبالتالي يمكنك إمداد الصور من القرص، أو الويب، أو ذاكرة مؤقتة.

### الأخطاء الشائعة عند تحميل الصور

| المشكلة | العرض | الحل |
|-------|---------|-----|
| DPI منخفض (<300) | أحرف مشوشة، أرقام مفقودة | أعد تحجيم الصورة إلى 300 dpi أو أعلى قبل التحميل |
| وضع اللون غير صحيح (CMYK) | أشكال أحرف غير صحيحة | حوّل إلى RGB باستخدام Pillow (`Image.convert("RGB")`) |
| PDF متعدد الصفحات | يتم معالجة الصفحة الأولى فقط | حوّل كل صفحة إلى صورة وكرر العملية عليها |

---

## تنفيذ OCR والحصول على النص الخام

الآن بعد أن علم المحرك مكان الصورة، يمكنه قراءتها فعليًا.

```python
# Step 4: Perform OCR to extract raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)
```

استدعاء `recognize()` يُعيد سلسلة نصية عادية في Python. في العديد من السيناريوهات الواقعية سيحتوي الناتج على مسافات زائدة، أحرف مقروءة خطأ، أو فواصل أسطر مكسورة—خاصة مع الإيصالات التي تستخدم خطوطًا مكثفة.

> **لماذا نلتقط raw_text أولًا:** يمنحك ذلك أساسًا للمقارنة مع النسخة المنقحة لاحقًا، وهو مفيد للتصحيح أو التدقيق.

---

## كيفية تصحيح أخطاء OCR – باستخدام تدقيق إملائي AI من Aspose

توفر Aspose غلافًا خفيفًا للذكاء الاصطناعي يمكنه تشغيل معالج تدقيق إملائي على الناتج الخام. هذا يجيب مباشرة على سؤال **how to correct OCR errors**.

```python
# Step 5: Initialise the AI post‑processor and choose a spell‑check processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")
```

يمكنك استبدال `"spell_check"` بمعالجات أخرى مثل `"grammar_check"` أو `"named_entity_recognition"` إذا تطلبت حالتك ذلك.

```python
# Step 6: Clean the OCR output using the selected post‑processor
clean_text = ai_processor.run_postprocessor(raw_text)

# Step 7: Output the corrected text
print("\nCorrected OCR output:")
print(clean_text)
```

### ما يفعله تدقيق الإملاء خلف الكواليس

1. **التقطيع** – يقسم السلسلة الخام إلى كلمات وعلامات ترقيم.  
2. **البحث في القاموس** – يقارن كل كلمة بقاموس إنجليزي (أو قاموس مخصص يمكنك توفيره).  
3. **التقييم السياقي** – يستخدم نموذج لغة صغير لتحديد ما إذا كان التصحيح يناسب الكلمات المحيطة.  
4. **الاستبدال** – يُعيد سلسلة جديدة مع تطبيق أكثر التصحيحات احتمالًا.

> **حالة خاصة:** إذا لم تكن اللغة المصدر إنجليزية، مرّر رمز اللغة المناسب عند إنشاء `AsposeAI()` (مثال: `AsposeAI(language="fr")`).

---

## التحقق من النص المنقح واستخدامه

في هذه المرحلة لديك متغيران: `raw_text` (النص الأصلي من OCR) و `clean_text` (النسخة المدققة). أيهما تحتفظ به يعتمد على احتياجاتك اللاحقة.

```python
# Example: Save the cleaned text to a .txt file for later indexing
with open("invoice_extracted.txt", "w", encoding="utf-8") as f:
    f.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

إذا كنت تُدخل النتيجة في محرك بحث، قاعدة بيانات، أو نموذج تعلم آلي، يُفضَّل دائمًا النسخة **المنقحة**—وإلا ستنشر ضوضاء OCR عبر خط أنابيبك.

---

## مثال كامل يعمل

فيما يلي السكريبت الكامل الذي يمكنك نسخه إلى ملف باسم `extract_invoice.py`. يفترض أنك قد ثبت الحزمتين من Aspose مسبقًا وأن لديك صورة في `YOUR_DIRECTORY/invoice.png`.

```python
# extract_invoice.py
# -------------------------------------------------------------
# Complete example: extract text from image and correct OCR errors
# -------------------------------------------------------------

# 1️⃣ Import required classes
from aspose.ocr import OcrEngine, AsposeAI

# 2️⃣ Create OCR engine and load the target image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

# 3️⃣ Run OCR – get raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)

# 4️⃣ Initialise AI spell‑check post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")

# 5️⃣ Clean the OCR output
clean_text = ai_processor.run_postprocessor(raw_text)

# 6️⃣ Show the corrected result
print("\nCorrected OCR output:")
print(clean_text)

# 7️⃣ Persist the cleaned text for later use
with open("invoice_extracted.txt", "w", encoding="utf-8") as out_file:
    out_file.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

شغّله باستخدام:

```bash
python extract_invoice.py
```

سترى المخرجات الخام متبوعةً بالنسخة الأكثر ترتيبًا، وسيظهر ملف باسم `invoice_extracted.txt` في نفس المجلد.

---

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا مع ملفات PDF؟**  
ج: ليس مباشرة. حوّل كل صفحة PDF إلى صورة (مثال باستخدام `pdf2image`) وكرر السكريبت على ملفات PNG الناتجة.

**س: لغتي ليست الإنجليزية—هل يمكنني استخدام تدقيق الإملاء؟**  
ج: نعم. مرّر رمز اللغة المطلوب إلى `AsposeAI(language="de")` للألمانية، `"es"` للإسبانية، إلخ.

**س: ماذا لو كان محرك OCR يخطئ في اكتشاف تخطيط الجدول؟**  
ج: يوفر Aspose OCR خيار `set_layout_analysis(True)`. تفعيل هذا يحسّن اكتشاف الجداول لكنه قد يزيد من زمن المعالجة.

**س: كيف أتعامل مع دفعات ضخمة جدًا؟**  
ج: ضع المنطق الأساسي داخل دالة واستخدم مجموعة خيوط (thread pool) أو IO غير متزامن (async IO) لتوزيع العمل على عدة نوى أو آلات.

---

## الخاتمة

لقد عرضنا كيفية **استخراج النص من صورة** باستخدام Aspose OCR، وكيفية **تحميل الصورة لـ OCR**، وأبسط طريقة **لتصحيح أخطاء OCR** باستخدام تدقيق إملائي AI المدمج. السكريبت الكامل القابل للتنفيذ يُظهر سير العمل من تحميل صورة الفاتورة PNG إلى حفظ ملف `.txt` نظيف وقابل للبحث.

لا تتردد في التجربة: استبدل تدقيق الإملاء بتصحيح القواعد، أو أدخل الناتج إلى مصنف NLP، أو دمج العملية في نظام إدارة مستندات أكبر. السماء هي الحد عندما تحصل على نص موثوق ومصحح.

هل لديك المزيد من الأسئلة حول OCR، Aspose، أو أتمتة Python؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة! 

---

![مثال على استخراج النص من صورة](extract_text_image.png "Extract text from image with Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}