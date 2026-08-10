---
category: general
date: 2026-06-25
description: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف (OCR) واستخراج النص من
  المستند الممسوح باستخدام بايثون. دليل خطوة بخطوة مع الشيفرة الكاملة.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: ar
og_description: قم بمعالجة الصورة مسبقًا للتعرف الضوئي على الأحرف وتعرف على النص من
  المستند الممسوح باستخدام بايثون. اتبع هذا الدرس التفصيلي القابل للتنفيذ.
og_title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف في بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: معالجة مسبقة للصورة للتعرف الضوئي على الأحرف (OCR) في بايثون – دليل شامل
url: /ar/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف (OCR) في بايثون – دليل شامل

هل تساءلت يومًا كيف **preprocess image for OCR** بحيث يكون النص نظيفًا وموثوقًا؟ لست وحدك—معظم المطورين يواجهون نفس المشكلة عندما تكون الصفحة الممسوحة مائلة أو التباين غير متساوٍ. الخبر السار هو أن بضع أسطر من بايثون يمكنها تصحيح ذلك الفوضى، تحويل الصورة إلى ثنائية، وإعطائك نصًا واضحًا وقابلًا للبحث.

في هذا الدرس سنستعرض الخطوات الدقيقة لـ **preprocess image for OCR** *و* **recognize text from scanned document** باستخدام مكتبة OCR شائعة. في النهاية ستحصل على سكريبت جاهز للتنفيذ، وتفهم لماذا كل إعداد مهم، وتعرف كيف تعدله للتعامل مع الحالات الصعبة.

## ما ستحتاجه

- Python 3.8 أو أحدث (الكود يعمل أيضًا على 3.10+)
- حزمة OCR تُظهر الفئات `OcrEngine` و `ImagePreProcessingOptions` و `Image` (مثال: الوحدة الوهمية `ocr` المستخدمة في المثال)
- مستند ممسوح أو مُصوَّر يكون مائلًا قليلًا أو منخفض التباين
- بيئة التطوير المتكاملة المفضلة لديك أو طرفية بسيطة—لا حاجة لواجهة رسومية ثقيلة

هذا كل شيء. لا ملفات تنفيذية إضافية، ولا تمارين Docker. هيا نبدأ.

## معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف (OCR) – خطوة بخطوة

فيما يلي سير العمل الأساسي مقسَّم إلى خمس مراحل واضحة. كل مرحلة تتضمن **السبب** الذي يجعلنا نفعل ذلك، **الكود** الدقيق، و**شرحًا** قصيرًا لما يحدث خلف الكواليس.

### الخطوة 1: إنشاء مثيل محرك OCR

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*لماذا هذا مهم:*  
كائن `OcrEngine` هو دماغ العملية. يحتفظ بالإعدادات مثل حزم اللغات، عتبات الثقة،—والأهم بالنسبة لنا—علامات معالجة الصورة مسبقًا. إنشاءه أولًا يمنحنا قاعدة نظيفة لتفعيل الحيل التي تلي ذلك.

### الخطوة 2: تمكين التصحيح التلقائي للميل (Deskewing) والتحويل إلى ثنائي (Binarization)

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*لماذا هذا مهم:*  
- **Deskewing** يدور الصورة بحيث تصبح خطوط النص أفقية. تواجه محركات OCR صعوبة عندما يميل خط الأساس بأكثر من بضع درجات.  
- **Binarization** يحول الصورة إلى أبيض وأسود نقي، مما يزيل الضوضاء الخلفية التي قد تشوش مصنّفات الأحرف.  
كلا الخيارين *تلقائيان* في العديد من المكتبات الحديثة، لكن لا يزال عليك تفعيلهما—ومن هنا التعيين الصريح.

> **نصيحة احترافية:** إذا كانت صور المصدر لديك مُحاذاة تمامًا، يمكنك ضبط `auto_deskew=False` لتوفير جزء من الملي ثانية في وقت المعالجة.

### الخطوة 3: تحميل الصورة المائلة التي تريد معالجتها

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*لماذا هذا مهم:*  
طريقة `Image.load` تقرأ الملف إلى الذاكرة وتغلفه في كائن يفهمه محرك OCR. كما تستخرج بيانات التعريف مثل DPI، والتي يمكن أن تؤثر على عامل التحجيم الافتراضي لتصحيح الميل.

> **حالة خاصة:** إذا كانت الصورة ملف TIFF متعدد الصفحات، سيتعين عليك التكرار عبر كل صفحة أو استخدام أداة مساعدة مثل `ocr.MultiPageImage.load`. تُطبق نفس إعدادات المعالجة المسبقة على كل صفحة.

### الخطوة 4: تنفيذ OCR على الصورة المعالجة مسبقًا

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*لماذا هذا مهم:*  
في هذه المرحلة يطبق المحرك خطوات تصحيح الميل والتحويل إلى ثنائي التي فعلناها مسبقًا، ثم يشغل شبكته العصبية (أو خط أنابيب أسلوب Tesseract التقليدي) على البت ماب المنقّاة. عادةً ما يحتوي كائن `result` المُرجع على النص العادي، درجات الثقة، وأحيانًا بيانات الموقع لكل كلمة.

> **ماذا لو ظل النص مشوشًا؟**  
تحقق من دقة الصورة: يعمل OCR بأفضل شكل عند 300 dpi أو أعلى. إذا كان المصدر أقل، فكر في تكبير الصورة قبل التحميل، أو اطلب النسخة الأصلية من مصدر المستند.

### الخطوة 5: إخراج النص المُعترف به

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*لماذا هذا مهم:*  
`result.text` هو تمثيل نصي عادي لكل ما استطاع المحرك قراءته. طباعته مفيدة للتصحيح السريع؛ في تطبيق حقيقي ربما تكتبها إلى ملف `.txt`، قاعدة بيانات، أو تمررها إلى خط أنابيب NLP لاحق.

---

## التعرف على النص من المستند الممسوح – ما بعد الأساسيات

الآن بعد أن عملت خط الأنابيب الأساسي، دعنا نستكشف بعض الاختلافات الشائعة التي قد تواجهها عندما تحاول **recognize text from scanned document** على الصور في الواقع.

### 1. التعامل مع لغات متعددة

إذا كان مستندك يحتوي على الإنجليزية والفرنسية معًا، اضبط المحرك قبل الخطوة 1:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

معظم محركات OCR تقبل رموز ISO‑639‑2؛ تحميل حزم لغات إضافية يضيف حملًا بسيطًا لكنه يحسن الدقة بشكل كبير على الصفحات متعددة اللغات.

### 2. ضبط عتبات التحويل إلى ثنائي بدقة

التحويل إلى ثنائي التلقائي يعمل في معظم الحالات، لكن بعض النسخ الضوئية القديمة تحتاج إلى عتبة مخصصة:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

جرّب القيم بين 120 و 220 حتى يختفي الخلفية دون مسح الأحرف الخفيفة.

### 3. استخراج معلومات التخطيط

أحيانًا تحتاج إلى أكثر من النص الخام—تريد معرفة موقع كل فقرة على الصفحة. العديد من المحركات تعرض مجموعة `result.blocks`:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

هذا لا يقدر بثمن لإعادة بناء الجداول أو الحفاظ على ترتيب الأعمدة.

### 4. معالجة مجموعة من الملفات

إذا كان لديك مجلد مليء بملفات PDF ممسوحة تم تحويلها إلى JPEGs، احطِ كامل التدفق بحلقة:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

تُعيد الحلقة استخدام نفس مثيل `engine`، مما يكون أكثر كفاءة من إنشاءه لكل ملف.

### 5. التعامل مع المسحات منخفضة الدقة

الصور منخفضة الدقة (< 150 dpi) غالبًا ما تنتج أحرفًا غير واضحة. حل سريع هو تكبير الصورة باستخدام خوارزمية عالية الجودة قبل تمريرها إلى محرك OCR:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

تكبير الصورة لن يخلق تفاصيل سحرية، لكن خطوة التحويل إلى ثنائي يمكنها العمل مع حواف أكثر وضوحًا، مما يمنح تحسينًا طفيفًا.

## النتيجة المتوقعة

تشغيل السكريبت الأصلي المكوّن من خمس خطوات على مسح مائل معتدل بدقة 300 dpi يجب أن يطبع شيئًا مشابهًا لـ:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

إذا رأيت أحرفًا مشوشة، تحقق مرة أخرى من علامات المعالجة المسبقة، دقة الصورة، وإعدادات اللغة.

## الخلاصة

لقد غطينا كل ما تحتاجه لـ **preprocess image for OCR** و **recognize text from scanned document** باستخدام بايثون. بدءًا من مثيل محرك جديد، فعلنا التصحيح التلقائي للميل والتحويل إلى ثنائي، حمّلنا صورة مائلة، نفّذنا التعرف، وطبعنا النص النظيف. على طول الطريق استكشفنا دعم اللغات المتعددة، تعديل العتبة يدويًا، استخراج التخطيط، المعالجة الدفعية، وحلول الصور منخفضة الدقة.

جرّب السكريبت على مسحاتك الخاصة—ربما مجموعة من الإيصالات، نموذج مكتوب يدويًا، أو مقطع من صحيفة قديمة. بمجرد أن تشعر بالراحة، حاول إضافة توليد PDF أو تمرير النتيجة إلى فهرس بحث. السماء هي الحد.

**هل أنت مستعد للتحدي التالي؟** اطلع على دروسنا حول *“استخراج الجداول من ملفات PDF الممسوحة باستخدام بايثون”* و *“تدريب نماذج OCR مخصصة باستخدام TensorFlow”* لتوسيع صندوق أدوات أتمتة المستندات الخاص بك.

Happy coding, and may your OCR always be crisp!

## ما يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)
- [كيفية استخدام AspOCR: مرشحات معالجة الصورة لـ OCR في .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}