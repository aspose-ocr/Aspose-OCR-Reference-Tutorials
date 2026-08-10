---
category: general
date: 2026-07-05
description: كيفية تعيين اللغة في Aspose OCR باستخدام بايثون. تعلم كيفية استخدام OCR،
  وكيفية استخراج النص من صور PNG، وتحويل الصورة إلى نص بايثون في دقائق.
draft: false
keywords:
- how to set language
- how to use ocr
- how to extract text
- extract text png
- image to text python
language: ar
og_description: كيفية تعيين اللغة في Aspose OCR باستخدام Python. يوضح هذا الدليل كيفية
  استخدام OCR، استخراج النص من ملفات PNG، وإجراء تحويلات الصورة إلى نص باستخدام Python.
og_title: كيفية تعيين اللغة في Aspose OCR باستخدام بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to set language in Aspose OCR using Python. Learn how to use OCR,
    how to extract text from PNG images, and convert image to text python in minutes.
  headline: How to Set Language in Aspose OCR with Python – Full Guide
  type: TechArticle
- description: How to set language in Aspose OCR using Python. Learn how to use OCR,
    how to extract text from PNG images, and convert image to text python in minutes.
  name: How to Set Language in Aspose OCR with Python – Full Guide
  steps:
  - name: Alternative Language Options
    text: 'If your image contains **Cyrillic** or **Arabic**, just swap the enum:'
  - name: Expected Output
    text: 'Assuming `input.png` contains the phrase “Hello, World!” you’ll see:'
  - name: 1. Blurry Images Yield Garbage
    text: '- **Solution:** Pre‑process the image (increase contrast, sharpen). Aspose
      OCR offers built‑in filters, e.g., `engine.image_preprocessing = ocr.ImagePreprocessing.AUTO`.'
  - name: 2. Wrong Language Produces Missing Accents
    text: '- **Solution:** Double‑check that you called `engine.language = ocr.Language.LATIN_EXTENDED`
      **before** calling `recognize`. Changing the language after recognition has
      no effect.'
  - name: 3. License Not Found → Evaluation Watermark
    text: '- **Solution:** Verify the path to `Aspose.OCR.Java.lic`. Use an absolute
      path or `os.path.join(os.getcwd(), "license", "Aspose.OCR.Java.lic")` to avoid
      relative‑path surprises.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: كيفية تعيين اللغة في Aspose OCR باستخدام بايثون – دليل كامل
url: /ar/python-java/general/how-to-set-language-in-aspose-ocr-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تعيين اللغة في Aspose OCR باستخدام Python – دليل كامل

تعيين اللغة في Aspose OCR باستخدام Python غالبًا ما يكون الخطوة الأولى للحصول على نتائج دقيقة. في هذا الدرس سنرشدك إلى كيفية تعيين اللغة، وكيفية استخدام OCR، وكيفية استخراج النص من صورة PNG — كل ذلك في سكريبت واحد قابل للتنفيذ.

إذا سبق لك أن حدقت في لقطة شاشة غير واضحة وتساءلت إذا كان بإمكانك تحويلها سحريًا إلى نص قابل للتحرير، فأنت في المكان الصحيح. سنغطي كل شيء من ترخيص المكتبة إلى طباعة النص المُعترف به، وسنضيف نصائح عملية لتجنب المشكلات الشائعة.

## المتطلبات المسبقة — ما ستحتاجه قبل البدء

- **Python 3.8+** (أي نسخة حديثة تعمل)
- **pip** لتثبيت حزمة `aspose-ocr`
- ملف **رخصة Aspose OCR** (اختياري لكنه مُوصى به للإنتاج)
- صورة **PNG** تحتوي على النص الذي تريد قراءته  
  (سنسميها `input.png` طوال الشرح)

لا أطر ثقيلة، لا حاويات Docker — مجرد Python عادي ومكتبة Aspose OCR.

## الخطوة 1: تثبيت وترخيص Aspose OCR

أولًا، تحتاج إلى وجود المكتبة على جهازك. افتح الطرفية ونفّذ:

```bash
pip install aspose-ocr
```

إذا كان لديك رخصة، ضع الملف `Aspose.OCR.Java.lic` (نعم، رخصة Java تعمل مع Python) في مكان آمن وحمّله هكذا:

```python
import asposeocr as ocr

# Load your Aspose OCR license (optional but removes evaluation limits)
ocr.License().set_license("YOUR_DIRECTORY/Aspose.OCR.Java.lic")
```

> **نصيحة محترف:** احتفظ بملف الرخصة خارج مجلد التحكم في المصدر لتجنب الالتزام العرضي.

## الخطوة 2: إنشاء كائن محرك OCR

الآن نقوم بإنشاء المحرك الذي سيقوم بالمعالجة الفعلية.

```python
# Create an OCR engine instance
engine = ocr.OcrEngine()
```

كائن `engine` هو بوابتك إلى جميع ميزات OCR التي تقدمها Aspose — التعرف، اختيار اللغة، معالجة الصورة مسبقًا، وما إلى ذلك.

## الخطوة 3: كيفية تعيين اللغة — تهيئة Latin Extended

هنا يبرز المفتاح الأساسي. للحصول على أعلى دقة يجب إخبار المحرك بمجموعة اللغة المتوقعة. تدعم Aspose OCR عشرات اللغات، لكن للعديد من النصوص الأوروبية الغربية ستحتاج إلى **Latin Extended**.

```python
# How to set language: configure the engine to recognize Latin Extended characters
engine.language = ocr.Language.LATIN_EXTENDED
```

لماذا هذا مهم؟ تعيين اللغة يحد من مجموعة الأحرف التي يبحث عنها المحرك، مما يقلل بشكل كبير من الإيجابيات الكاذبة. إذا تخطيت هذه الخطوة، قد تحصل على مخرجات مشوشة، خاصةً مع الأحرف ذات اللكنات.

### خيارات لغات بديلة

إذا كانت صورتك تحتوي على **Cyrillic** أو **Arabic**، فقط استبدل الـ enum:

```python
engine.language = ocr.Language.CYRILLIC      # For Russian, Bulgarian, etc.
engine.language = ocr.Language.ARABIC        # For Arabic script
```

يمكنك حتى دمج عدة لغات بتمرير قائمة، لكن تذكر أن كل لغة مضافة تبطئ المعالجة قليلًا.

## الخطوة 4: تحميل الصورة التي تريد تحويلها (استخراج نص PNG)

الجزء التالي هو إمداد المحرك ببيتماب. يمكن لـ Aspose OCR قراءة العديد من الصيغ، لكننا سنركز على **PNG** لأنها غير مضغوطة ومستخدمة على نطاق واسع.

```python
# Load the image that contains the text you want to recognize
image = ocr.Image.load("YOUR_DIRECTORY/input.png")
```

إذا كنت تتساءل كيف تستخرج النص من **PNG** موجود على الويب، يمكنك تحميله أولًا باستخدام `requests` ثم تمرير المصفوفة البايتية إلى `ocr.Image.from_bytes()`.

```python
import requests
response = requests.get("https://example.com/sample.png")
image = ocr.Image.from_bytes(response.content)
```

## الخطوة 5: تنفيذ OCR وطباعة النتيجة (كيفية استخدام OCR)

الآن يأتي لحظة الحقيقة — تشغيل المحرك والحصول على النص.

```python
# Perform OCR and output the recognised text
result = engine.recognize(image)

print("Recognised text:")
print(result.text)
```

خاصية `result.text` تحتفظ بمخرجات تحويل **image to text python**. إنها سلسلة نصية عادية، لذا يمكنك كتابتها إلى ملف، تمريرها إلى chatbot، أو حتى إجراء تحليل مشاعر عليها.

### النتيجة المتوقعة

بافتراض أن `input.png` يحتوي على العبارة “Hello, World!” ستظهر لك:

```
Recognised text:
Hello, World!
```

إذا كانت الصورة تشمل عدة أسطر، فستُفصل بينها أحرف السطر الجديد (`\n`). يمكنك تقسيمها باستخدام `result.text.splitlines()` لمزيد من المعالجة.

## الخطوة 6: المشكلات الشائعة وكيفية إصلاحها

### 1. الصور الضبابية تُنتج نفايات

- **الحل:** عالج الصورة مسبقًا (زيادة التباين، الشحذ). توفر Aspose OCR فلاتر مدمجة، مثل `engine.image_preprocessing = ocr.ImagePreprocessing.AUTO`.

### 2. اللغة الخاطئة تُفقد اللكنات

- **الحل:** تأكد من أنك استدعيت `engine.language = ocr.Language.LATIN_EXTENDED` **قبل** استدعاء `recognize`. تغيير اللغة بعد التعرف لا يؤثر.

### 3. عدم العثور على الرخصة → علامة مائية للتقييم

- **الحل:** تحقق من مسار `Aspose.OCR.Java.lic`. استخدم مسارًا مطلقًا أو `os.path.join(os.getcwd(), "license", "Aspose.OCR.Java.lic")` لتجنب مفاجآت المسارات النسبية.

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي السكريبت الكامل الذي يمكنك نسخه ولصقه في `ocr_demo.py` وتشغيله:

```python
import asposeocr as ocr
import os

# -------------------------------------------------
# 1️⃣ Load license (optional)
# -------------------------------------------------
license_path = os.path.join("YOUR_DIRECTORY", "Aspose.OCR.Java.lic")
if os.path.exists(license_path):
    ocr.License().set_license(license_path)
    print("License loaded successfully.")
else:
    print("License not found – running in evaluation mode.")

# -------------------------------------------------
# 2️⃣ Create OCR engine
# -------------------------------------------------
engine = ocr.OcrEngine()

# -------------------------------------------------
# 3️⃣ How to set language – Latin Extended for accented chars
# -------------------------------------------------
engine.language = ocr.Language.LATIN_EXTENDED

# -------------------------------------------------
# 4️⃣ Load PNG image (extract text png)
# -------------------------------------------------
image_path = os.path.join("YOUR_DIRECTORY", "input.png")
image = ocr.Image.load(image_path)

# -------------------------------------------------
# 5️⃣ Perform OCR – how to use OCR
# -------------------------------------------------
result = engine.recognize(image)

# -------------------------------------------------
# 6️⃣ Output – how to extract text / image to text python
# -------------------------------------------------
print("\n--- Recognised text ---")
print(result.text)
```

احفظ الملف، استبدل `YOUR_DIRECTORY` بالمجلد الفعلي، ثم نفّذ:

```bash
python ocr_demo.py
```

سترى النص المُعترف به يُطبع في وحدة التحكم.

## إضافي: حفظ النتيجة في ملف نصي

إذا كنت تفضّل ملفًا دائمًا بدلاً من الإخراج على الشاشة:

```python
output_path = os.path.join("YOUR_DIRECTORY", "output.txt")
with open(output_path, "w", encoding="utf-8") as f:
    f.write(result.text)
print(f"Text saved to {output_path}")
```

الآن أتممت **كيفية تعيين اللغة**، **كيفية استخدام OCR**، و**كيفية استخراج النص** من PNG — كل ذلك باستخدام Python.

---

## الخلاصة

لقد عرضنا **كيفية تعيين اللغة** في Aspose OCR باستخدام Python، وأظهرنا **كيفية استخدام OCR** لقراءة الصور، وشرحنا **كيفية استخراج النص** من ملف PNG — أي تحويل صورة إلى نص قابل للتحرير باستخدام تقنيات **image to text python**. السكريبت الكامل جاهز للتنفيذ، ويمكنك تعديله للغات أو صيغ صور أخرى بتغيير سطر واحد فقط.

هل أنت مستعد للخطوة التالية؟ جرّب معالجة مجموعة من الصور داخل حلقة، جرب إعدادات لغات مختلفة، أو دمج النتيجة في خط أنابيب معالجة مستندات أكبر. السماء هي الحد عندما تتقن الأساسيات.

هل لديك أسئلة حول لغة معينة أو تحتاج مساعدة في تصحيح صورة صعبة؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}