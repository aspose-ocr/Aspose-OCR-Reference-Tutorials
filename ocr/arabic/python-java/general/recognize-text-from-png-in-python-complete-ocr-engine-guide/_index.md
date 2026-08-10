---
category: general
date: 2026-06-25
description: 'التعرف على النص من ملف PNG باستخدام بايثون: دليل خطوة بخطوة لإنشاء محرك
  OCR بايثون، تشغيل OCR على مستند تقني واستخراج النص من صورة المستند التقني.'
draft: false
keywords:
- recognize text from png
- ocr image to text python
- create OCR engine python
- extract text from technical document image
- run OCR on technical document
language: ar
og_description: التعرف على النص من ملفات PNG باستخدام بايثون. تعلم كيفية إنشاء محرك
  OCR بايثون، تشغيل OCR على المستندات التقنية واستخراج النص من صورة المستند التقني.
og_title: التعرف على النص من PNG في بايثون – دليل كامل لمحرك OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: 'recognize text from png with Python: step‑by‑step guide to create
    OCR engine python, run OCR on technical document and extract text from technical
    document image.'
  headline: Recognize Text from PNG in Python – Complete OCR Engine Guide
  type: TechArticle
- description: 'recognize text from png with Python: step‑by‑step guide to create
    OCR engine python, run OCR on technical document and extract text from technical
    document image.'
  name: Recognize Text from PNG in Python – Complete OCR Engine Guide
  steps:
  - name: Low‑Resolution Images
    text: 'If the PNG originates from a scanned fax, you might be dealing with 72
      dpi. OCR accuracy drops dramatically below 150 dpi. A quick fix is to upscale
      the image using a bicubic algorithm before recognition:'
  - name: Rotated Pages
    text: 'Technical manuals sometimes come scanned at an angle. The engine can auto‑deskew,
      but you can also pre‑rotate:'
  - name: Multi‑Page Documents
    text: 'When you need to **run OCR on technical document** PDFs that have been
      exported to PNG per page, wrap the logic in a loop:'
  - name: Language Selection
    text: 'Aspose OCR defaults to English, but you can switch to other languages (e.g.,
      German) by loading the appropriate language pack:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: التعرف على النص من PNG في بايثون – دليل شامل لمحرك OCR
url: /ar/python-java/general/recognize-text-from-png-in-python-complete-ocr-engine-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من PNG في بايثون – دليل كامل لمحرك OCR

هل احتجت يومًا إلى **التعرف على النص من PNG** ولكن لم تكن متأكدًا أي مكتبة بايثون تختار؟ لست الوحيد. سواءً كنت تقوم برقمنة الأدلة الممسوحة ضوئيًا، أو استخراج أرقام السيريال من ملصقات المنتجات، أو استخراج البيانات من صورة مستند تقني، فإن خط أنابيب OCR موثوق يمكنه توفير ساعات من النسخ واللصق اليدوي.

في هذا الدرس سنستعرض مثالًا عمليًا يوضح لك كيفية **إنشاء محرك OCR بايثون**، وإعطائه ملف PNG، و**استخراج النص من صورة مستند تقني** ببضع أسطر من الشيفرة فقط. في النهاية ستعرف أيضًا كيفية **تشغيل OCR على مستند تقني** بملفات ذات جودة مختلفة، وستحصل على سكربت قابل لإعادة الاستخدام لمشروعك التالي.

## ما ستتعلمه

- تثبيت وإعداد مكتبة OCR لبايثون (يتم استخدام Aspose OCR، لكن الخطوات تنطبق على معظم حزم OCR الحديثة).  
- **إنشاء محرك OCR بايثون** وتكوين قاموس مخصص للمصطلحات الخاصة بالمجال.  
- تحميل صورة PNG، تشغيل OCR، و**التعرف على النص من png** بكفاءة.  
- معالجة المشكلات الشائعة مثل الدقة المنخفضة، الصفحات المائلة، والخلفيات الضوضائية.  
- توسيع السكربت لمعالجة دفعات من مستندات تقنية متعددة.

> **المتطلبات المسبقة** – يجب أن يكون لديك Python 3.8+ مثبتًا، وإلمام أساسي بـ pip، وصورة PNG تحتوي على نص قابل للقراءة آليًا. لا تحتاج إلى خبرة سابقة في OCR.

---

## الخطوة 1: تثبيت مكتبة OCR (إنشاء محرك OCR بايثون)

أولاً وقبل كل شيء: نحتاج إلى مكتبة تقوم بالعمل الشاق فعليًا. Aspose OCR لبايثون عبر .NET هو خيار تجاري يقدم دقة عالية مباشرةً، لكن النمط نفسه يعمل مع بدائل مفتوحة المصدر مثل `pytesseract`. للحفاظ على المثال مستقلًا، سنستخدم Aspose OCR.

```bash
pip install aspose-ocr
```

> **نصيحة احترافية:** إذا واجهت أخطاء أذونات على Windows، شغّل الأمر من PowerShell بامتيازات إدارية أو أضف `--user` في النهاية.

بعد التثبيت، يمكنك استيراد الوحدة وإنشاء محرك:

```python
import aspose.ocr as ocr
```

سطر الاستيراد الواحد هذا يمنحك الوصول إلى الفئة `OcrEngine`، وهي الأساس لـ **إنشاء محرك OCR بايثون**.

## الخطوة 2: تهيئة محرك OCR وضبطه (تشغيل OCR على مستند تقني)

الآن سنقوم بإنشاء نسخة من المحرك وربما نزوده بقاموس مخصص. القاموس المخصص هو قائمة من الكلمات التي يجب على OCR اعتبارها صالحة — مثالي للمصطلحات التقنية، رموز المنتجات، أو الاختصارات الداخلية.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: define a custom dictionary for domain‑specific terms
engine.custom_dictionary = [
    "AsposeOCR", "OCRSDK", "Invoice#2026", "SKU-12345"
]
```

لماذا نهتم بالقاموس؟ تخيل مسح دليل صيانة يذكر مرارًا وتكرارًا “SKU‑12345”. بدون القاموس قد يقرأ OCR ذلك كـ “SKU‑12345” أو حتى “S K U‑12345”. بإضافة المصطلح إلى `custom_dictionary`، تحسن بشكل كبير دقة **ocr image to text python** لهذا المستند المحدد.

## الخطوة 3: تحميل صورة PNG (استخراج النص من صورة مستند تقني)

بعد ذلك، نقوم بتحميل PNG التي تحتوي على النص الذي نريد **التعرف على النص من png**. يدعم Aspose OCR مجموعة متنوعة من صيغ الصور، لكن PNG خيار جيد لأنه يحافظ على الجودة غير المضغوطة.

```python
# Step 3: Load the image file
image_path = "YOUR_DIRECTORY/technical_doc.png"
image = ocr.Image.load(image_path)
```

إذا كانت PNG الخاصة بك كبيرة بشكل غير عادي (مثلاً مخططًا مسحوبًا)، قد ترغب في تقليل حجمها قبل OCR للحفاظ على استهلاك الذاكرة ضمن حدود معقولة:

```python
# Optional downscale for huge images
max_dim = 2000  # pixels
if max(image.width, image.height) > max_dim:
    scale = max_dim / max(image.width, image.height)
    image = image.resize(int(image.width * scale), int(image.height * scale))
```

## الخطوة 4: تنفيذ OCR (OCR Image to Text Python)

مع جاهزية المحرك وتحميل الصورة، يكون التعرف الفعلي استدعاء طريقة واحدة:

```python
# Step 4: Run OCR on the loaded image
result = engine.recognize(image)
```

في الخلفية، تقوم `engine.recognize` بتنفيذ سلسلة من خطوات ما قبل المعالجة — التثليث، تصحيح الميل، تحليل التخطيط — قبل تمرير الصورة المنقحة إلى الشبكة العصبية. لهذا السبب يمكن لسطر واحد فقط **تشغيل OCR على مستند تقني** ملفات قد تُربك السكربتات البسيطة.

## الخطوة 5: إخراج النص المُتعرف عليه (التعرف على النص من PNG)

أخيرًا، نطبع النص المستخرج. يمكنك أيضًا كتابته إلى ملف، أو إدخاله في قاعدة بيانات، أو تمريره إلى خطوط معالجة لغة طبيعية لاحقة.

```python
# Step 5: Output the recognized text
print("=== OCR Result ===")
print(result.text)
```

إذا شغّلت السكربت مع PNG صالحة، سترى شيئًا مثل:

```
=== OCR Result ===
Invoice #2026
Product: AsposeOCR SDK
SKU-12345
Total: $1,299.00
```

> **مثال على الصورة**  
> ![recognize text from png output](images/ocr_result.png)  
> *نص بديل:* *التعرف على النص من png – مثال نتيجة OCR معروضة في وحدة التحكم.*

تُظهر لقطة الشاشة استخراجًا نظيفًا حيث ضَمَن القاموس المخصص أن يبقى رمز المنتج سليماً.

---

## الغوص أعمق: التعامل مع الحالات الطرفية الشائعة

### صور منخفضة الدقة

إذا كانت PNG مصدرها فاكس ممسوح، قد تتعامل مع 72 dpi. تنخفض دقة OCR بشكل كبير تحت 150 dpi. حل سريع هو تكبير الصورة باستخدام خوارزمية بيكوبيك قبل التعرف:

```python
if image.dpi < 150:
    image = image.resize(image.width * 2, image.height * 2, interpolation=ocr.InterpolationMode.BICUBIC)
```

### صفحات مائلة

أحيانًا تُمسح الأدلة التقنية بزاوية. يمكن للمحرك تصحيح الميل تلقائيًا، لكن يمكنك أيضًا تدوير مسبقًا:

```python
# Detect and correct rotation
angle = engine.auto_rotate(image)
if angle != 0:
    image = image.rotate(-angle)
```

### مستندات متعددة الصفحات

عندما تحتاج إلى **تشغيل OCR على مستند تقني** ملفات PDF تم تصديرها إلى PNG لكل صفحة، ضع المنطق داخل حلقة:

```python
import glob

for png_path in sorted(glob.glob("pages/*.png")):
    img = ocr.Image.load(png_path)
    txt = engine.recognize(img).text
    with open("output.txt", "a", encoding="utf-8") as f:
        f.write(f"--- Page {png_path} ---\n{txt}\n\n")
```

### اختيار اللغة

يُفترض Aspose OCR اللغة الإنجليزية، لكن يمكنك التبديل إلى لغات أخرى (مثل الألمانية) بتحميل حزمة اللغة المناسبة:

```python
engine.language = ocr.Language.German
```

هذا مفيد عندما يتضمن **استخراج النص من صورة مستند تقني** جداول أو مواصفات متعددة اللغات.

## سكربت كامل يعمل

فيما يلي السكربت الكامل الجاهز للتنفيذ الذي يجمع كل شيء معًا. احفظه باسم `ocr_technical_doc.py` واستبدل `YOUR_DIRECTORY/technical_doc.png` بمسار PNG الخاص بك.



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية استخراج نص الصورة من تدفق باستخدام Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [تحويل الصورة إلى نص – تنفيذ OCR على صورة من URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}