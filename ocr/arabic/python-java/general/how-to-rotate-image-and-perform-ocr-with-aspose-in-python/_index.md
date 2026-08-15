---
category: general
date: 2026-03-26
description: تعلم كيفية تدوير الصورة وإجراء التعرف الضوئي على الحروف (OCR) في بايثون.
  يوضح هذا الدليل أيضًا كيفية معالجة الصورة مسبقًا للتعرف الضوئي على الحروف واستخراج
  النص من الصورة بكفاءة.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: ar
og_description: كيفية تدوير الصورة بشكل صحيح ثم التعرف على النص من الصورة باستخدام
  Aspose OCR. اتبع هذا الدليل خطوة بخطوة لمعالجة الصورة مسبقًا للتعرف الضوئي على الأحرف
  واستخراج النص من الصورة.
og_title: كيفية تدوير الصورة وإجراء التعرف الضوئي على الأحرف – دليل بايثون الكامل
tags:
- Aspose
- Python
- Image Processing
- OCR
title: كيفية تدوير الصورة وإجراء OCR باستخدام Aspose في بايثون
url: /ar/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تدوير الصورة وإجراء OCR باستخدام Aspose في Python

هل تساءلت يومًا **كيفية تدوير الصورة** بحيث يمكن لمحرك OCR قراءة النص فعليًا؟ ربما قمت بمسح نموذج انتهى به الأمر مائلًا، أو أن صورة الكاميرا تحولت 90° باتجاه عقارب الساعة. في هذه الحالة يبدو النص جيدًا للعين البشرية، لكن محرك OCR يرى فوضى. الخبر السار؟ إنه سهل جدًا تصحيح الاتجاه، قص المنطقة التي تهمك، ثم استخراج النص — كل ذلك ببضع أسطر من Python ومكتبات Aspose.

في هذا البرنامج التعليمي سنستعرض سير العمل بالكامل: من تحميل ملف TIFF مدور، تصحيح اتجاهه، **معالجة الصورة للـ OCR**، وأخيرًا **التعرف على النص من الصورة**. في النهاية ستعرف **كيفية إجراء OCR** على أي صورة وستتمكن من **استخراج النص من ملفات الصورة** بثقة.

## ما ستحتاجه

- Python 3.8+ (الكود يعمل مع أي نسخة حديثة)
- حزم `asposeocrjava` و `asposeimaging` المثبتة عبر `pip`
- صورة عينة تحتاج إلى تدوير (مثال: `rotated_form.tif`)
- قليل من الفضول حول معالجة الصور

لا حاجة لإطارات عمل ضخمة — فقط الحزمتين من Aspose وقليل من منطق Python.

## الخطوة 1: تثبيت حزم Aspose (كيفية إجراء OCR)

قبل أن نتمكن من **تدوير الصورة** أو **التعرف على النص من الصورة**، نحتاج إلى المكتبات التي تقوم بالعمل الفعلي.

```bash
pip install asposeocrjava asposeimaging
```

> **نصيحة احترافية:** إذا كنت خلف بروكسي مؤسسي، أضف `--proxy http://proxy:port` إلى الأمر. الحزم هي مجرد أغطية Python صافية حول نواة Aspose .NET/Java، لذا عادةً ما تكون عملية التثبيت فورية.

## الخطوة 2: تحميل الملف المصدر وتدويره – خطوة “كيفية تدوير الصورة” الأساسية

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **لماذا التدوير؟** معظم محركات OCR تفترض أن النص يقرأ من اليسار إلى اليمين ومن الأعلى إلى الأسفل. إذا تم تحويل البت ماب إلى الجانب، سيعيد المحرك إما نصًا غير مفهوم أو لا شيء على الإطلاق. التدوير يطابق شبكة البكسلات مع ترتيب القراءة المتوقع، مما يحسن الدقة بشكل كبير.

> **حالة حافة:** إذا لم تكن متأكدًا ما إذا كانت الصورة تحتاج إلى تدوير 90°، 180°، أو 270°، يمكنك فحص `source_image.width` مقابل `source_image.height` أو استخدام وسوم توجيه `exif`. طريقة `rotate_flip` في Aspose تدعم أيضًا `ROTATE_180` و `ROTATE_270_CLOCKWISE`.

> **معاينة الصورة (اختياري):**  
> ![مثال على كيفية تدوير الصورة](/assets/rotate-demo.png "كيفية تدوير الصورة – قبل وبعد التدوير")

## الخطوة 3: قص منطقة الاهتمام – معالجة الصورة للـ OCR

غالبًا ما تحتاج فقط إلى جزء صغير من الصفحة — مثل حقل التوقيع أو كتلة من الأرقام. القص يزيل الضوضاء ويسرع **كيفية إجراء OCR**.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **لماذا القص؟** تقليل حجم الصورة يحد من مساحة البحث لمحرك OCR، مما يقلل الإيجابيات الكاذبة ويقلل وقت المعالجة. كما يساعد إذا كان الملف المصدر يحتوي على علامات مائية أو رسومات أخرى قد تربك المحرك.

> **نصيحة:** إذا كنت تتعامل مع حقول متعددة، كرر خطوة القص باستخدام مستطيلات مختلفة وشغّل OCR على كل قطعة على حدة.

## الخطوة 4: تهيئة محرك OCR – جوهر “كيفية إجراء OCR”

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **خلف الكواليس:** يستخدم Aspose OCR مزيجًا من Tesseract وتحليل الصور المملوك. إنشاء المحرك مرة واحدة وإعادة استخدامه لعدة صور أكثر كفاءة من إنشاء كائن جديد في كل مرة.

## الخطوة 5: إمداد الصورة المقطوعة والتعرف على النص – كيفية استخراج النص من الصورة

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### النتيجة المتوقعة

إذا كانت منطقة الاهتمام تحتوي على العبارة “Invoice #12345 – Paid”، سترى شيئًا مثل:

```
Invoice #12345 – Paid
```

إذا واجه OCR صعوبة، قد تحصل على مسافات إضافية أو أحرف مقروءة بشكل خاطئ (مثال: “Invo1ce #I2345 – Pa1d”). هنا تأتي حيل **معالجة الصورة للـ OCR** — مثل تعديل التباين أو تطبيق التثليث — لتلعب دورها. تقدم Aspose فلاتر إضافية يمكنك ربطها قبل الخطوة 5، لكن التدفق الأساسي أعلاه يعمل لمعظم المسحات النظيفة.

## الخطوة 6: اختياري — ضبط إعدادات OCR بدقة (متقدم “كيفية إجراء OCR”)

إذا كنت تحتاج إلى دقة أعلى للغة معينة أو تريد تجاهل أحرف معينة، يمكنك تعديل المحرك:

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **متى تستخدم:** استخدم هذا عندما يحتوي المستند على الكثير من الرموز الزخرفية التي لا تهمك. القائمة السوداء تقلل من الاكتشافات الخاطئة.

## البرنامج الكامل من البداية إلى النهاية

بجمع كل شيء معًا، إليك برنامج جاهز للتنفيذ **كيفية تدوير الصورة**، **معالجة الصورة للـ OCR**، وأخيرًا **التعرف على النص من الصورة**:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

تشغيل هذا البرنامج يطبع النص المعترف به إلى وحدة التحكم ويحفظ صورة مرئية للمنطقة المقطوعة المعالجة باسم `processed_roi.png`. يمكنك فتح هذا PNG للتحقق من أن التدوير والقص تمّا كما هو متوقع.

## أسئلة شائعة ومشكلات محتملة

| السؤال | الجواب |
|----------|--------|
| **ماذا لو كانت الصورة بالفعل في الوضع الصحيح؟** | خطوة التدوير متطابقة—تدوير صورة موجهة بشكل صحيح بزاوية 90° سيكسرها بالطبع، لذا يجب فحص `source_image.width` مقابل `height` أو استخدام بيانات توجيه EXIF قبل استدعاء `rotate_flip`. |
| **نتيجة OCR تحتوي على فواصل سطر إضافية.** | استخدم `result.get_text().replace("\n", " ").strip()` للتنظيف، أو فعّل `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)`. |
| **هل يمكنني معالجة ملفات PDF مباشرةً؟** | نعم — يمكن لـ Aspose Imaging تحميل صفحات PDF كصور (`Image.load("file.pdf")`)، ثم تتبع نفس خطوات التدوير و OCR. |
| **هل هناك طريقة لمعالجة دفعة من الملفات؟** | ضع `ocr_rotated_image` داخل حلقة على دليل، أو استخدم `concurrent.futures` في Python للتوازي. |
| **كيف أتعامل مع لغات غير الإنجليزية؟** | حدد لغة التعرف عبر `ocr_engine.get_recognition_settings().set_recognition_language("fr")` للفرنسية، إلخ. |

## الخلاصة

لقد غطينا **كيفية تدوير الصورة** بشكل صحيح، **معالجة الصورة للـ OCR** عن طريق القص، وأخيرًا **كيفية إجراء OCR** لـ **التعرف على النص من الصورة** و **استخراج النص من الصورة** باستخدام مكتبات Aspose للـ Python. يوضح البرنامج الكامل سير عمل عملي وجاهز للإنتاج يمكنك إدراجه في أي خط أنابيب أتمتة.

إذا كنت جاهزًا للمتابعة، جرب التجربة مع:

- **تحسين الصورة** (التباين، التثليث) قبل OCR
- **استخراج مناطق اهتمام متعددة** للنماذج التي تحتوي على عدة حقول
- **معالجة دفعة** لمجلدات كاملة من المستندات الممسوحة
- **التكامل** مع الأنظمة اللاحقة (مثال: تغذية البيانات المستخرجة إلى قاعدة بيانات)

لا تتردد في تعديل الكود ليناسب حالتك الخاصة، وتمنياتنا لك بالبرمجة السعيدة! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}