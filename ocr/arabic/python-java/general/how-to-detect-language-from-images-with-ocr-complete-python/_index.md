---
category: general
date: 2026-06-22
description: تعلم كيفية اكتشاف اللغة من الصورة واستخراج النص باستخدام OCR في بايثون.
  دليل خطوة بخطوة يغطي الكشف التلقائي عن اللغة واستخراج النص.
draft: false
keywords:
- how to detect language
- detect language from image
- extract text from image
- how to use ocr
- how to extract text
language: ar
og_description: كيف تكتشف اللغة من صورة باستخدام OCR؟ يوضح لك هذا الدليل خطوة بخطوة
  كيفية استخدام OCR في بايثون لاكتشاف اللغة واستخراج النص.
og_title: كيفية اكتشاف اللغة من الصور باستخدام OCR – دليل كامل بلغة بايثون
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  headline: How to Detect Language from Images with OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  name: How to Detect Language from Images with OCR – Complete Python Guide
  steps:
  - name: Expected Output
    text: 'If `sample-multilang.png` contains French text, you might see something
      like:'
  - name: 1. Unsupported Image Formats
    text: 'If you try to load a TIFF file that the OCR library doesn’t recognise,
      `ocr.ImageStream.from_file()` will raise an `OcrUnsupportedFormatError`. Wrap
      the load call in a try/except block:'
  - name: 2. Low‑Resolution Images
    text: 'OCR accuracy drops sharply below ~300 dpi. If you notice poor detection,
      consider pre‑processing the image with Pillow:'
  - name: 3. Multiple Languages in One Image
    text: 'When an image contains text in more than one language, the auto‑detect
      feature will pick the dominant one. To capture all languages, you can disable
      auto‑detect and manually pass a list of languages to the engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: كيفية اكتشاف اللغة من الصور باستخدام OCR – دليل بايثون كامل
url: /ar/python-java/general/how-to-detect-language-from-images-with-ocr-complete-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية اكتشاف اللغة من الصور باستخدام OCR – دليل بايثون الكامل

هل تساءلت يومًا **كيف يتم اكتشاف اللغة** في صورة دون فتحها يدويًا؟ أنت لست الوحيد. في العديد من المشاريع—مثل ماسحات الإيصالات، أرشيفات المستندات متعددة اللغات، أو تطبيق بسيط لتحويل الصور إلى نص—تحتاج إلى معرفة *أي* لغة ينتمي إليها النص قبل أن تتمكن من معالجته أكثر.  

في هذا الدرس سنستعرض مثالًا عمليًا من البداية إلى النهاية يوضح **كيفية اكتشاف اللغة** من صورة ثم استخراج الأحرف الفعلية. في النهاية ستتمكن من تشغيل بضع أسطر من بايثون، توجيه البرنامج إلى أي صورة مدعومة، والحصول على كل من اللغة المكتشفة *والنص المستخرج*. لا إطالة، مجرد حل واضح يمكنك نسخه ولصقه.

## ما ستتعلمه

- تثبيت وإعداد مكتبة OCR خفيفة الوزن في بايثون.  
- تهيئة محرك OCR وتمكين اكتشاف اللغة التلقائي.  
- تحميل صورة (أي صيغة مدعومة) وتشغيل OCR.  
- استرجاع اللغة المكتشفة والنص المستخرج.  
- التعامل مع المشكلات الشائعة مثل الصيغ غير المدعومة أو نتائج اللغة الغامضة.  

إذا تساءلت يومًا **كيف تستخدم OCR** للمستندات متعددة اللغات، فهذا الدليل يغطي ما تحتاجه.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي على جهازك:

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| Python 3.9 أو أحدث | حزمة OCR التي سنستخدمها تستهدف مفسرات حديثة. |
| `pip` (مدير حزم بايثون) | مطلوب لتثبيت مكتبة OCR. |
| صورة نموذجية تحتوي على نص بلغة واحدة على الأقل (مثال: `sample-multilang.png`) | توفر لك شيئًا ملموسًا للاختبار. |
| اختياري: بيئة افتراضية (`venv` أو `conda`) | تحافظ على نظافة الاعتمادات وتجنب تعارض الإصدارات. |

> **نصيحة احترافية:** إذا كنت تعمل داخل بيئة افتراضية، فعّلها قبل تثبيت حزمة OCR للحفاظ على نظافة بايثون العام.

---

## الخطوة 1: تثبيت مكتبة OCR

في هذا الشرح سنستخدم حزمة `ocr` الافتراضية التي تعكس الـ API المعروض في مقطع الشيفرة. في سيناريو واقعي يمكنك استبدالها بـ `pytesseract` أو `easyocr` أو أي مكتبة أخرى تدعم اكتشاف اللغة التلقائي.

```bash
pip install ocr
```

> **ملاحظة:** الحزمة خفيفة الوزن (< 5 ميغابايت) وتعمل على Windows و macOS و Linux. إذا واجهت أخطاء صلاحية، أضف `--user` إلى الأمر.

---

## الخطوة 2: تهيئة محرك OCR – كيفية اكتشاف اللغة

الآن بعد أن أصبحت المكتبة جاهزة، يمكننا إنشاء كائن محرك OCR. هذا هو الكائن الذي سيفحص الصورة فعليًا ويحدد اللغة.

```python
import ocr

# Initialise the OCR engine – this is where we start the language detection pipeline
engine = ocr.OcrEngine()
```

لماذا نبدأ بمحرك؟ فكر في المحرك كعقل نظام OCR؛ فهو يحمل الإعدادات، يحمل نماذج اللغات، ويدير العمليات الثقيلة خلف الكواليس. تهيئته أولًا يضمن أن أي استدعاءات لاحقة (مثل تحميل صورة) لديها سياق للعمل فيه.

---

## الخطوة 3: تحميل صورتك وتمكين اكتشاف اللغة التلقائي

الخطوة التالية هي تمرير الصورة إلى المحرك. سنُفعِّل أيضًا علامة *auto‑detect language* حتى يحاول محرك OCR تخمين اللغة أثناء التشغيل.

```python
# Load the image (any supported format – PNG, JPEG, BMP, etc.)
image_path = "YOUR_DIRECTORY/sample-multilang.png"
image = ocr.ImageStream.from_file(image_path)

# Attach the image to the engine
engine.set_image(image)

# Enable automatic language detection – this is the key for detecting language from image
engine.get_settings().set_auto_detect_language(True)
```

> **لماذا نُفعِّل الاكتشاف التلقائي؟**  
> معظم مكتبات OCR تأتي بلغة افتراضية (غالبًا الإنجليزية). إذا كان مستندك يحتوي على الفرنسية أو اليابانية أو أي نص آخر، سيفوت المحرك ذلك بدون هذا الإعداد. عبر تفعيل `set_auto_detect_language(True)`، نسمح للمحرك بفحص البت ماب، مقارنة إحصاءات شكل الأحرف، واختيار نموذج اللغة الأكثر احتمالًا.

---

## الخطوة 4: تنفيذ OCR – استخراج النص من الصورة

مع تحميل الصورة وتفعيل اكتشاف اللغة، خطوة OCR الفعلية هي مجرد استدعاء طريقة واحدة.

```python
# Run the OCR process – this both detects the language and extracts the text
result = engine.recognize()
```

طريقة `recognize()` تقوم بشيئين في الخلفية:

1. **اكتشاف اللغة:** تشغيل مصنف خفيف الوزن على الصورة لاختيار رمز اللغة (مثال: `en`, `fr`, `es`).  
2. **استخراج النص:** ثم تطبيق النموذج الخاص بتلك اللغة لتحويل الأحرف إلى سلاسل Unicode.

نظرًا لأن الإجراءين يحدثان معًا، ستحصل على كائن `result` واحد يحتوي على كل ما تحتاجه.

---

## الخطوة 5: استرجاع وعرض اللغة المكتشفة والنص المستخرج

أخيرًا، نستخرج رمز اللغة والنص الخام من كائن `result` ونطبعهما على وحدة التحكم.

```python
# Print the detected language and the extracted text
print("Detected language:", result.get_language())
print("Text:", result.get_text())
```

### النتيجة المتوقعة

إذا كانت `sample-multilang.png` تحتوي على نص فرنسي، قد ترى شيئًا مثل:

```
Detected language: fr
Text: Bonjour, ceci est un texte d'exemple.
```

إذا كانت الصورة غامضة أو تحتوي على عدة لغات، سيُعيد المحرك اللغة التي يثق بها أكثر، ويمكنك لاحقًا فحص درجة الثقة (معظم المكتبات توفر طريقة `get_confidence()` للاستخدامات المتقدمة).

---

## التعامل مع الحالات الشائعة

### 1. صيغ الصور غير المدعومة

إذا حاولت تحميل ملف TIFF لا تتعرف عليه مكتبة OCR، سيُطلق `ocr.ImageStream.from_file()` استثناء `OcrUnsupportedFormatError`. غلف استدعاء التحميل بكتلة try/except:

```python
try:
    image = ocr.ImageStream.from_file(image_path)
except ocr.OcrUnsupportedFormatError as e:
    print(f"Unsupported format: {e}")
    raise
```

### 2. الصور منخفضة الدقة

تنخفض دقة OCR بشكل حاد تحت ~300 dpi. إذا لاحظت اكتشافًا ضعيفًا، فكر في معالجة مسبقة للصورة باستخدام Pillow:

```python
from PIL import Image, ImageEnhance

pil_img = Image.open(image_path)
pil_img = pil_img.resize((pil_img.width * 2, pil_img.height * 2), Image.LANCZOS)
pil_img.save("resized.png")
image = ocr.ImageStream.from_file("resized.png")
```

### 3. عدة لغات في صورة واحدة

عندما تحتوي الصورة على نص بأكثر من لغة، ستختار ميزة الاكتشاف التلقائي اللغة السائدة. لالتقاط جميع اللغات، يمكنك تعطيل الاكتشاف التلقائي وتمرير قائمة باللغات يدويًا إلى المحرك:

```python
engine.get_settings().set_auto_detect_language(False)
engine.get_settings().set_languages(["en", "fr", "de"])
```

بهذا سيحاول OCR التعرف على الأحرف باستخدام كل نموذج لغة ويُعيد أفضل تطابق لكل كتلة نصية.

---

## البرنامج الكامل – جميع الخطوات مجتمعة

فيما يلي البرنامج الكامل القابل للتنفيذ في بايثون الذي يجمع كل ما تناولناه. احفظه باسم `detect_language_ocr.py` وشغّله بالأمر `python detect_language_ocr.py`.

```python
# detect_language_ocr.py
# -------------------------------------------------
# How to detect language from image and extract text using OCR
# -------------------------------------------------

import ocr

def main():
    # 1️⃣ Initialise the OCR engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image (any supported format)
    image_path = "YOUR_DIRECTORY/sample-multilang.png"
    try:
        image = ocr.ImageStream.from_file(image_path)
    except ocr.OcrUnsupportedFormatError as err:
        print(f"Error loading image: {err}")
        return

    engine.set_image(image)

    # 3️⃣ Enable automatic language detection
    engine.get_settings().set_auto_detect_language(True)

    # 4️⃣ Perform OCR – this both detects language and extracts text
    try:
        result = engine.recognize()
    except ocr.OcrRecognitionError as err:
        print(f"OCR failed: {err}")
        return

    # 5️⃣ Retrieve and display the detected language and extracted text
    print("Detected language:", result.get_language())
    print("Text:", result.get_text())

if __name__ == "__main__":
    main()
```

**شغّله** وسترى فورًا رمز اللغة متبوعًا بالنص المستخرج. هذا هو الجواب الكامل على **كيفية اكتشاف اللغة** و**كيفية استخراج النص** من صورة باستخدام OCR.

---

## ما التالي؟ – خطوات إضافية ومواضيع ذات صلة

- **تحسين الدقة:** جرب معالجة مسبقة للصور (عَتْمَة، إزالة الضوضاء) باستخدام `opencv-python`.  
- **معالجة دفعات:** ضع البرنامج داخل حلقة للتعامل مع مجلد كامل من الصور.  
- **الدمج مع NLP:** مرّر النص المستخرج إلى مكتبة تحديد اللغة مثل `langdetect` للحصول على رأي ثانٍ.  
- **استكشاف محركات OCR أخرى:** `pytesseract` يوفّر تحكمًا دقيقًا، بينما `easyocr` يدعم أكثر من 80 لغة مباشرةً.  

كل هذه المواضيع ترتبط بكلماتنا المفتاحية الثانوية—*detect language from image*، *extract text from image*، *how to use OCR*، و*how to extract text*—لتستمر في توسيع أدواتك دون الحاجة للبدء من الصفر.

---

## الخلاصة

لقد غطينا **كيفية اكتشاف اللغة** من صورة، استعرضنا الشيفرة الدقيقة المطلوبة، وشرحنا سبب أهمية كل خطوة. عبر تهيئة محرك OCR، تحميل الصورة، تفعيل اكتشاف اللغة التلقائي، وأخيرًا استدعاء `recognize()`، ستحصل على كل من معرف اللغة والنص المستخرج في عملية واحدة نظيفة.

الآن يمكنك دمج هذه المنطق في تطبيقات أكبر—سواء كان خدمة مسح إيصالات، روبوت دردشة متعدد اللغات، أو أداة سطح مكتب بسيطة. الفكرة الأساسية تبقى نفسها: دع محرك OCR يقوم بالعمل الشاق، ثم استخدم النتائج كما تشاء.

هل لديك أسئلة حول الحالات الخاصة، أو تريد مشاركة حالة استخدام مميزة؟ اترك تعليقًا أدناه. برمجة سعيدة، واستمتع بتحويل الصور إلى نص قابل للبحث!  

![كيفية اكتشاف اللغة من الصورة](ocr-demo.png "لقطة شاشة تُظهر كيفية اكتشاف اللغة من الصورة باستخدام OCR بايثون")


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}