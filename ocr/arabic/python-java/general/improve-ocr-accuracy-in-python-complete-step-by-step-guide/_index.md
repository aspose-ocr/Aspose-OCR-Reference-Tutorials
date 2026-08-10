---
category: general
date: 2026-05-31
description: حسّن دقة التعرف الضوئي على الأحرف (OCR) باستخدام بايثون عبر معالجة الصور
  مسبقًا للتعرف الضوئي على الأحرف. تعلّم كيفية استخراج النص من ملفات الصور، والتعرف
  على النص من ملفات PNG، وتعزيز النتائج.
draft: false
keywords:
- improve OCR accuracy
- preprocess image for OCR
- extract text from image
- recognize text from PNG
- image preprocessing for text
language: ar
og_description: حسّن دقة التعرف الضوئي على الأحرف في بايثون من خلال تطبيق معالجة مسبقة
  للصور للنص. اتبع هذا الدليل لاستخراج النص من ملفات الصور والتعرف على النص من ملفات
  PNG بسهولة.
og_title: تحسين دقة التعرف الضوئي على الأحرف في بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  headline: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  name: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Loads the PNG into memory
    text: Loads the PNG into memory
  - name: Applies denoise and deskew based on our settings
    text: Applies denoise and deskew based on our settings
  - name: Runs the neural‑network or classic pattern matcher
    text: Runs the neural‑network or classic pattern matcher
  - name: Packages the output into `recognition_result`
    text: Packages the output into `recognition_result`
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: تحسين دقة التعرف الضوئي على الأحرف في بايثون – دليل كامل خطوة بخطوة
url: /ar/python-java/general/improve-ocr-accuracy-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحسين دقة OCR في بايثون – دليل خطوة بخطوة كامل

هل حاولت يومًا **تحسين دقة OCR** ولكنك حصلت على مخرجات مشوشة؟ لست وحدك. يواجه معظم المطورين صعوبة عندما تكون الصورة الأصلية مليئة بالضوضاء، مائلة، أو ذات تباين منخفض ببساطة. الخبر السار؟ مجموعة من حيل ما قبل المعالجة يمكنها تحويل لقطة شاشة غير واضحة إلى نص نظيف يمكن للآلة قراءته.

في هذا البرنامج التعليمي سنستعرض مثالًا واقعيًا **يعالج صورة لـ OCR**، يشغل محرك التعرف، وأخيرًا **يستخرج النص من الصورة** — تحديدًا PNG. بنهاية الدليل ستعرف بالضبط كيف **تتعرف على النص من PNG** بمعدل نجاح أعلى، وستحصل على مقتطف كود قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع.

## ما ستتعلمه

- لماذا تعد معالجة الصورة مهمة لمحركات OCR  
- أي أوضاع ما قبل المعالجة (إزالة الضوضاء، تصحيح الميل) تعطي أكبر تحسين  
- كيفية تكوين كائن `OcrEngine` في بايثون  
- السكريبت الكامل القابل للتنفيذ الذي **يستخرج النص من الصورة**  
- نصائح للتعامل مع الحالات الخاصة مثل المسحات المدوّرة أو الصور منخفضة الدقة  

لا تحتاج إلى مكتبات خارجية غير SDK الخاص بـ OCR، لكنك ستحتاج إلى Python 3.8+ وصورة PNG تريد قراءتها.

---

![مخطط يوضح خطوات تحسين دقة OCR في بايثون](image.png "مخطط تحسين تدفق عمل دقة OCR")

*Alt text: مخطط يوضح خطوات تحسين دقة OCR ومعالجة ما قبل المعالجة وخطوات التعرف.*

## المتطلبات المسبقة

- Python 3.8 أو أحدث مثبت  
- الوصول إلى SDK الخاص بـ OCR الذي يوفر `OcrEngine`، `OcrEngineSettings`، و `ImagePreprocessMode` (الكود أدناه يستخدم API عام؛ استبدله بفئات البائع إذا لزم الأمر)  
- صورة PNG (`input.png`) موجودة في مجلد يمكنك الإشارة إليه  

إذا كنت تستخدم بيئة افتراضية، فعّلها الآن—ليس هناك شيء معقد، فقط `python -m venv venv && source venv/bin/activate`.

---

## الخطوة 1: إنشاء كائن محرك OCR – ابدأ تحسين دقة OCR

الأول الذي تحتاجه هو كائن محرك OCR. فكر فيه كالعقل الذي سيقرأ البكسلات لاحقًا ويُخرج الأحرف.

```python
# Step 1: Initialise the OCR engine
ocr_engine = OcrEngine()
```

لماذا هذا مهم: بدون محرك لا يمكنك تطبيق أي معالجة مسبقة، وستُرسل الصورة الخام مباشرة إلى المُعرّف—عادةً ما يكون ذلك أسوأ سيناريو للدقة.

---

## الخطوة 2: تحميل ملف PNG المستهدف – تهيئة البيئة لتعرف النص من PNG

الآن نخبر المحرك أي ملف سيعمل عليه. PNG غير مضغوط، وهذا يمنحنا ميزة صغيرة على JPEG.

```python
# Step 2: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/input.png")
```

إذا كانت الصورة موجودة في مكان آخر، فقط عدّل المسار. المحرك يقبل أي صيغة مدعومة، لكن PNG غالبًا ما يحافظ على التفاصيل الدقيقة اللازمة لحواف الأحرف الواضحة.

---

## الخطوة 3: تكوين ما قبل المعالجة – معالجة الصورة لـ OCR

هنا يحدث السحر. نُنشئ كائن إعدادات، نفعّل إزالة الضوضاء لمسح البقع، ونُشغّل تصحيح الميل بحيث يُستقيم النص المائل تلقائيًا.

```python
# Step 3: Prepare preprocessing settings to improve accuracy
preprocess_settings = OcrEngineSettings()
preprocess_settings.preprocess_mode = (
    ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
)
```

### لماذا إزالة الضوضاء + تصحيح الميل؟

- **إزالة الضوضاء**: الضوضاء العشوائية في البكسلات تُربك خوارزميات مطابقة الأنماط. إزالتها تُحسّن حدة الحروف.  
- **تصحيح الميل**: حتى ميل قدره درجتين يمكن أن يُخفض درجات الثقة بشكل كبير. تصحيح الميل يُعيد محاذاة الخط الأساسي، مما يسمح للمُعرّف بمطابقة الخطوط بشكل أكثر موثوقية.

يمكنك تجربة علامات إضافية (مثل `ImagePreprocessMode.CONTRAST_ENHANCE`) إذا كانت صورك داكنة جدًا. عادةً ما تُدرج وثائق SDK جميع الأوضاع المتاحة.

---

## الخطوة 4: تطبيق الإعدادات على المحرك – ربط ما قبل المعالجة بـ OCR

نُعيّن كائن الإعدادات إلى المحرك حتى يستخدم التحويلات التي عرّفناها في عملية التعرف التالية.

```python
# Step 4: Apply the settings to the engine
ocr_engine.settings = preprocess_settings
```

إذا تخطيت هذه الخطوة، سيعود المحرك إلى الإعدادات الافتراضية (غالبًا “بدون معالجة مسبقة”)، وستلاحظ **انخفاض دقة OCR**.

---

## الخطوة 5: تشغيل عملية التعرف – استخراج النص من الصورة

مع كل شيء موصول، نطلب من المحرك الآن أداء مهمته. الاستدعاء متزامن، ويُعيد كائن نتيجة يحتوي على السلسلة المعترف بها.

```python
# Step 5: Run the recognition process
recognition_result = ocr_engine.recognize()
```

خلف الكواليس، يقوم المحرك الآن بـ:

1. تحميل PNG إلى الذاكرة  
2. تطبيق إزالة الضوضاء وتصحيح الميل بناءً على إعداداتنا  
3. تشغيل الشبكة العصبية أو مطابقة الأنماط الكلاسيكية  
4. تجميع الناتج في `recognition_result`

---

## الخطوة 6: إخراج النص المعترف به – تحقق من التحسين

لنطبع السلسلة المستخرجة. في تطبيق حقيقي قد تكتبها إلى ملف، قاعدة بيانات، أو تمرّرها إلى خدمة أخرى.

```python
# Step 6: Output the recognized text
print(recognition_result.text)
```

### النتيجة المتوقعة

إذا كانت الصورة تحتوي على الجملة “Hello, OCR World!” يجب أن ترى:

```
Hello, OCR World!
```

لاحظ أن النص نظيف—بدون رموز عشوائية أو أحرف مكسورة. هذا هو نتيجة **معالجة الصورة المناسبة للنص**.

---

## نصائح احترافية وحالات خاصة

| الحالة | ما الذي يجب تعديله | السبب |
|-----------|----------------|-----|
| PNG منخفض الدقة جدًا (≤ 72 dpi) | أضف `ImagePreprocessMode.SUPER_RESOLUTION` إذا كان متاحًا | التكبير يمكن أن يمنح المُعرّف المزيد من البكسلات للعمل معها |
| النص مدوّر > 5° | زد من تحمل تصحيح الميل أو قم بتدوير يدوي باستخدام `Pillow` قبل تمريره للمحرك | الزوايا الشديدة أحيانًا تتجاوز تصحيح الميل التلقائي |
| نمط خلفية كثيف | فعّل `ImagePreprocessMode.BACKGROUND_REMOVAL` | يزيل الفوضى غير النصية التي قد تُقرأ خطأ |
| مستند متعدد اللغات | عيّن `ocr_engine.language = "eng+spa"` (أو ما شابه) | يختار المحرك مجموعة الأحرف الصحيحة، مما يحسّن الدقة العامة |

تذكر، **تحسين دقة OCR** ليس حلًا واحدًا يناسب الجميع؛ قد تحتاج إلى تعديل علامات ما قبل المعالجة وفقًا لمجموعتك الخاصة من البيانات.

---

## السكريبت الكامل – جاهز للنسخ واللصق

فيما يلي المثال الكامل القابل للتنفيذ الذي يدمج كل خطوة ناقشناها. احفظه باسم `improve_ocr_accuracy.py` وشغّله باستخدام `python improve_ocr_accuracy.py`.

```python
"""
Improve OCR Accuracy in Python – Full Example
Author: Your Name (2026)
Requires: OCR SDK providing OcrEngine, OcrEngineSettings, ImagePreprocessMode
"""

# Import the necessary classes from the OCR SDK
from ocr_sdk import OcrEngine, OcrEngineSettings, ImagePreprocessMode

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the PNG you want to read
    image_path = "YOUR_DIRECTORY/input.png"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure preprocessing: denoise + deskew
    preprocess_settings = OcrEngineSettings()
    preprocess_settings.preprocess_mode = (
        ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
    )

    # 4️⃣ Apply the settings
    ocr_engine.settings = preprocess_settings

    # 5️⃣ Run recognition
    recognition_result = ocr_engine.recognize()

    # 6️⃣ Print the extracted text
    print("=== Recognized Text ===")
    print(recognition_result.text)

if __name__ == "__main__":
    main()
```

شغّله، راقب وحدة التحكم، وسترى نتيجة **استخراج النص من الصورة** فورًا. إذا بدت النتيجة غير صحيحة، عدّل علامات `preprocess_mode` كما هو موضح في جدول “نصائح احترافية”.

---

## الخلاصة

لقد استعرضنا وصفة عملية **لتحسين دقة OCR** باستخدام بايثون. من خلال إنشاء `OcrEngine`، تحميل PNG، **معالجة الصورة لـ OCR**، وأخيرًا **التعرف على النص من PNG**، يمكنك استخراج النص من ملفات الصورة حتى عندما لا تكون المصدر مثاليًا.  

ما الخطوة التالية؟ جرّب معالجة مجموعة من الصور داخل حلقة، خزن كل نتيجة في CSV، أو جرّب أوضاع معالجة إضافية مثل تحسين التباين. نفس النمط يعمل مع ملفات PDF، الإيصالات الممسوحة، أو الملاحظات المكتوبة بخط اليد—فقط غير الإدخال واضبط الإعدادات.

هل لديك أسئلة حول نوع صورة معين أو تريد معرفة كيفية دمج هذا في خدمة ويب؟ اترك تعليقًا، وسنستكشف تلك السيناريوهات معًا. برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالكريستال!

## ماذا يجب أن تتعلم بعد ذلك؟

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)
- [كيفية استخراج النص من الصورة عن طريق إعداد المستطيلات في OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}