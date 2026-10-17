---
category: general
date: 2026-05-03
description: استخراج النص من صورة باستخدام بايثون و Aspose OCR. تعلم دليل OCR خطوة
  بخطوة للبايثون مع دعم مختلط للغات اللاتينية والسيريلية.
draft: false
keywords:
- extract text from image python
- Aspose OCR Python
- image to text conversion
- mixed language OCR
- Python OCR tutorial
language: ar
og_description: استخراج النص من الصورة باستخدام بايثون بسرعة. يوضح هذا الدليل كيفية
  استخدام Aspose OCR في بايثون للصور المختلطة من اللاتينية والسيريلية.
og_title: استخراج النص من صورة باستخدام بايثون – دليل كامل لاستخدام Aspose OCR
tags:
- OCR
- Python
- Aspose
title: استخراج النص من صورة بايثون – دليل Aspose OCR الكامل
url: /ar/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة باستخدام Python – دليل Aspose OCR الكامل

هل احتجت يومًا إلى **extract text from image python** لكن لم تكن متأكدًا أي مكتبة يمكنها التعامل مع مزيج من الأحرف اللاتينية والسيريلية؟ لست وحدك—المطورون يواجهون هذه المشكلة باستمرار عند إجراء OCR على لقطات شاشة متعددة اللغات.  

الخبر السار هو أن Aspose OCR for Python يجعل العملية بأكملها شبه خالية من المتاعب. في هذا الدرس سنستعرض تثبيت الحزمة، تطبيق الترخيص، تحميل صورة متعددة اللغات، وأخيرًا استخراج النص المعترف به ببضع أسطر من الشيفرة. بنهاية الدرس ستحصل على سكريبت جاهز للتنفيذ يمكنك إدراجه في أي مشروع.

## ما ستتعلمه

- كيفية إعداد **Aspose OCR Python** في بيئة افتراضية.  
- لماذا يؤدي توجيه اللغات (مثل اللاتينية والسيريلية) إلى تسريع الكشف.  
- الشيفرة الدقيقة المطلوبة لـ **extract text from image python** باستدعاء دالة واحدة.  
- الأخطاء الشائعة عند التعامل مع OCR متعدد اللغات وكيفية تجنبها.  

### المتطلبات المسبقة

- Python 3.8 أو أحدث مثبت على جهازك.  
- ملف ترخيص Aspose OCR (`Aspose.OCR.Java.lic`). النسخة التجريبية المجانية تكفي للاختبار، لكن ملف الترخيص يزيل العلامات المائية.  
- صورة PNG/JPEG تحتوي على كل من الأحرف اللاتينية والسيريلية (سنطلق عليها `mixed_latin_cyrillic.png`).  

إذا كان لديك كل ما سبق، فأنت جاهز للبدء—لا تحتاج إلى أطر عمل إضافية أو تبعيات ثقيلة.

---

## الخطوة 1 – استخراج النص من صورة Python: تثبيت Aspose OCR

أولاً: احصل على المكتبة من PyPI وتأكد من أن بيئتك تستطيع العثور على ملف الترخيص.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the Aspose OCR package
pip install asposeocrcloud
```

> **نصيحة محترف:** إذا واجهت خطأ في الصلاحيات، أضف `--user` إلى أمر `pip install` أو شغّل الطرفية كمسؤول.

الآن بعد أن تم تثبيت الحزمة على نظامك، سنستوردها ونوجه المحرك إلى الترخيص الخاص بنا.

```python
import asposeocrcloud as ocr   # the library we just installed

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Apply your license – replace the path with the actual location of your .lic file
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")
```

لماذا نحتاج إلى ترخيص في هذه المرحلة؟ بدون الترخيص يعمل المحرك في **وضع التقييم**، مما يحد من عدد الصفحات ويضيف علامة مائية إلى الناتج. توفير الترخيص مسبقًا يضمن أن استدعاء `recognize` لاحقًا يُعيد نصًا نظيفًا.

---

## الخطوة 2 – تحميل صورتك ذات المحتوى اللاتيني‑السيريلي المختلط

بعد ذلك، نقوم بتحميل الصورة إلى الذاكرة. Aspose OCR يعمل مع فئة `Image` الخاصة به، التي تُجرد تفاصيل تنسيق الملف الأساسي.

```python
# Load the image that contains both Latin and Cyrillic characters
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")
```

إذا كنت تتساءل ما إذا كانت الصيغ الأخرى تعمل—نعم، JPEG، BMP، TIFF، وحتى PDF مدعومة. فقط غيّر امتداد الملف وستتعامل طريقة `from_file` مع البقية.

---

## الخطوة 3 – توجيه اللغات لتسريع الكشف (اختياري لكن مفيد)

عندما تعرف اللغات الموجودة في الصورة، يمكنك إعطاء المحرك إشارة مسبقة. هذا ليس إلزاميًا، لكنه **يقلل بشكل كبير من زمن المعالجة** ويحسن الدقة في OCR متعدد اللغات.

```python
# Provide language hints: Latin and Cyrillic
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]
```

قائمة التوجيه تقبل أي لغة يدعمها Aspose OCR (مثل `"Arabic"`، `"Japanese"`). إذا تخطيت هذه الخطوة، سيحاول المحرك كل لغة مدمجة، مما قد يكون أبطأ في الدفعات الكبيرة.

---

## الخطوة 4 – تشغيل محرك OCR واستخراج النص

الآن لحظة الحقيقة: التعرف الفعلي على الأحرف. طريقة `recognize` تُعيد كائن `OcrResult` يحتوي على النص العادي، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها لاحقًا.

```python
# Perform OCR on the loaded image
ocr_result = ocr_engine.recognize(input_image)

# The recognised text is available via the .text attribute
extracted_text = ocr_result.text
```

> **لماذا يعمل هذا:** تحت الغطاء، يجمع Aspose OCR بين كاشف نصوص يعتمد على الشبكات العصبية ومصنفات مخصصة لكل لغة. بتمرير كائن `Image`، تتجاوز الحاجة إلى أي معالجة يدوية مثل التثنيم.

---

## الخطوة 5 – عرض النص المستخرج

أخيرًا، لنطبع النتيجة على وحدة التحكم. في تطبيق حقيقي قد تكتبها إلى ملف، أو تدفعها إلى قاعدة بيانات، أو تُغذيها إلى واجهة برمجة تطبيقات ترجمة.

```python
print("Recognised text:")
print(extracted_text)
```

عند تشغيل السكريبت، يجب أن ترى شيئًا مثل:

```
Recognised text:
Hello мир! This is a test.
```

هذا الناتج يؤكد أننا نجحنا في **extract text from image python**، مع معالجة كل من الأحرف اللاتينية والسيريلية في تمريرة واحدة.

---

## مثال كامل يعمل

فيما يلي السكريبت الكامل الذي يمكنك نسخه‑ولصقه في ملف يُسمى `extract_ocr.py`. استبدل مسارات العناصر النائبة بالمسارات الفعلية لديك.

```python
import asposeocrcloud as ocr   # package installed via pip

# ------------------------------------------------------------
# Step 1 – Initialise engine and apply license
# ------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")   # path to your license file

# ------------------------------------------------------------
# Step 2 – Load the image (mixed Latin‑Cyrillic)
# ------------------------------------------------------------
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")

# ------------------------------------------------------------
# Step 3 – (Optional) Hint the languages present
# ------------------------------------------------------------
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]

# ------------------------------------------------------------
# Step 4 – Run OCR
# ------------------------------------------------------------
ocr_result = ocr_engine.recognize(input_image)

# ------------------------------------------------------------
# Step 5 – Display the recognised text
# ------------------------------------------------------------
print("Recognised text:")
print(ocr_result.text)
```

احفظ الملف، فعّل بيئتك الافتراضية، وشغّله:

```bash
python extract_ocr.py
```

يجب أن ترى النص المعترف به مطبوعًا، مما يؤكد أن السكريبت يعمل من البداية إلى النهاية.

---

## الأسئلة المتكررة والحالات الخاصة

**ماذا لو كانت الصورة ضبابية؟**  
Aspose OCR يتضمن أدوات لتصحيح الانحراف وتقليل الضوضاء، لكن للصور المتدهورة بشدة قد ترغب في المعالجة المسبقة باستخدام OpenCV (مثلاً تطبيق تمويه غاوسي وعامل عتبة). فئة `Image` يمكنها أيضًا قبول مصفوفة NumPy، لذا يمكنك ربط مرشحات مخصصة قبل استدعاء `recognize`.

**هل يمكنني معالجة مجلد كامل من الصور؟**  
بالطبع. غلف المنطق داخل حلقة `for`، غيّر `from_file` لقراءة كل اسم ملف، وخزن النتائج في قاموس. تذكر احترام حدود معدل الاستدعاءات إذا كنت تستخدم النسخة السحابية.

**هل أحتاج إلى ترخيص منفصل لكل لغة؟**  
لا، ترخيص Aspose OCR واحد يغطي جميع اللغات المدعومة. قائمة `language_hints` هي مجرد توجيه للأداء.

**ماذا عن إدخال PDF؟**  
استبدل `Image.from_file` بـ `ocr.Image.from_file("document.pdf")`. سيقوم محرك OCR تلقائيًا بتحويل كل صفحة إلى صورة وإرجاع النص المدمج.

---

## الخاتمة

لقد عرضنا طريقة مختصرة وجاهزة للإنتاج لـ **extract text from image python** باستخدام Aspose OCR. الخطوات—التثبيت، الترخيص، التحميل، توجيه اللغات، التعرف، والعرض—تغطي كل ما تحتاجه للحصول على نتائج موثوقة لمحتوى لاتيني‑سيريلي مختلط.  

من هنا يمكنك استكشاف مواضيع متقدمة مثل **تحويل الصورة إلى نص** للمعالجة الدفعة، دمج الناتج مع **Python OCR tutorial** في معالجة اللغة الطبيعية، أو تجربة توجيهات لغات أخرى للمستندات متعددة اللغات. السماء هي الحد، والشيفرة بين يديك.

هل لديك حالة استخدام مختلفة أو واجهت مشكلة؟ اترك تعليقًا، شارك تجربتك، ولنستمر في النقاش. برمجة سعيدة!  

![مثال لاستخراج النص من صورة باستخدام Python](/images/extract-text-from-image-python.png "لقطة شاشة تُظهر ناتج OCR – extract text from image python")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}