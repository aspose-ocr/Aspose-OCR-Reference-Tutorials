---
category: general
date: 2026-06-28
description: قم بمعالجة الصورة مسبقًا للتعرف الضوئي على الأحرف باستخدام بايثون لتعزيز
  الدقة. تعلم خط أنابيب كامل لمعالجة الصور مسبقًا، حسّن نتائج التعرف الضوئي على الأحرف،
  واستخرج النص من الصور السيريالية.
draft: false
keywords:
- preprocess image for OCR
- how to improve OCR accuracy
- python OCR with preprocessing
- image preprocessing pipeline python
- extract text from Cyrillic image
language: ar
og_description: قم بمعالجة الصورة مسبقًا للتعرف الضوئي على الأحرف (OCR) باستخدام بايثون
  وتعلم كيفية تحسين دقة OCR. يوضح لك هذا الدليل خطوة بخطوة خط أنابيب معالجة مسبقة
  كامل واستخراج النص من الصور السيريالية.
og_title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف – دورة بايثون كاملة
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with Python to boost accuracy. Learn a full
    image preprocessing pipeline, improve OCR results, and extract text from Cyrillic
    images.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with Python to boost accuracy. Learn a full
    image preprocessing pipeline, improve OCR results, and extract text from Cyrillic
    images.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the code works on 3.10+ as well). - Basic familiarity
      with Python packages and virtual environments. - An OCR library that provides
      `OcrEngine`, `Language`, and `ImagePreprocessor` classes (e.g., a wrapper around
      Tesseract or a commercial SDK). - A sample Cyrillic image (`cyri'
  - name: Why These Three Steps?
    text: 1. **Deskew** – OCR engines assume left‑to‑right (or top‑to‑bottom) alignment.
      A few degrees of rotation can drop accuracy by 30 % or more. 2. **Binarize**
      – Converting to a binary image reduces the data the OCR engine must analyze,
      sharpening character edges. 3. **Denoise** – Small specks or compre
  - name: How This Improves OCR Accuracy
    text: '- By feeding a **clean, deskewed, binarized** image, the engine can focus
      on character shapes rather than fighting noise. - Specifying `Language.Cyrillic`
      activates the correct character set and language model, which is a key factor
      in **how to improve OCR accuracy** for non‑Latin scripts.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف – دليل بايثون الكامل
url: /ar/python-java/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة الصورة للتعرف الضوئي على الحروف – دليل بايثون كامل

هل تساءلت يوماً كيف **preprocess image for OCR** بحيث يكون النص واضحاً كالكريستال؟ لست وحدك—الكثير من المطورين يواجهون مشكلة عندما تُخرج محركات OCR أحرفاً مشوشة، خاصةً مع مسحات سيريليكية مائلة أو صاخبة. الخبر السار؟ أن خط أنابيب معالجة الصورة المصمم جيداً يمكنه رفع معدلات التعرف بشكل كبير.

في هذا الدرس سنغوص مباشرةً في حل **Python OCR with preprocessing** يتعامل مع تصحيح الميل، التحويل إلى ثنائي، وإزالة الضوضاء، ثم يوضح لك كيفية **extract text from Cyrillic image**. بنهاية الدرس ستحصل على سكريبت قابل لإعادة الاستخدام، وتفهم **how to improve OCR accuracy**، وستكون جاهزاً لتكييف خط الأنابيب لأي لغة أو مصدر صورة.

## ما ستتعلمه

- المنطق وراء كل خطوة معالجة ولماذا هي مهمة للتعرف الضوئي.
- كيفية تجميع **image preprocessing pipeline python** يمكن إعادة استخدامها عبر المشاريع.
- مثال كامل قابل للتنفيذ يُنشئ محرك OCR، يعالج صورة سيريليكية، ويطبع النص المُستخرج.
- نصائح للتعامل مع الحالات الخاصة مثل الميل الشديد، التباين المنخفض، أو المستندات متعددة اللغات.
- أفكار للخطوات التالية مثل المعالجة الدفعية، حزم اللغات المخصصة، وتكامل مع خدمات OCR السحابية.

### المتطلبات المسبقة

- Python 3.8 أو أحدث (الكود يعمل أيضاً على 3.10+).
- إلمام أساسي بحزم بايثون والبيئات الافتراضية.
- مكتبة OCR توفر الفئات `OcrEngine`، `Language`، و `ImagePreprocessor` (مثل غلاف حول Tesseract أو SDK تجاري).  
- صورة سيريليكية تجريبية (`cyrillic_skewed.jpg`) موجودة في مجلد يمكنك التحكم فيه.

> **نصيحة محترف:** إذا لم يكن لديك غلاف OCR جاهز، تفقد حزمة المصدر المفتوح `pytesseract` واستخدمها مع `opencv-python`. المفاهيم في هذا الدليل تُترجم مباشرة.

---

## الخطوة 1: تثبيت واستيراد الحزم المطلوبة

أولاً، لننتهي من الاعتمادات. سنستخدم مكتبة افتراضية `ocr_lib` التي تجمع بين المحرك وأدوات المعالجة. إذا كنت تستخدم `pytesseract` + OpenCV، استبدل الاستيرادات وفقاً لذلك.

```python
# Install the (fictional) OCR library – replace with your actual package manager command
# pip install ocr-lib

from ocr_lib import OcrEngine, Language, ImagePreprocessor
import os
```

> **لماذا هذا مهم:** استيراد الفئات الصحيحة يضمن فصل واضح بين محرك OCR (التعرف) ومعالج الصورة (التحسين). دمجهما قد يؤدي إلى كود متشابك يصعب تصحيح الأخطاء.

---

## الخطوة 2: بناء خط أنابيب **Preprocess Image for OCR**

الآن سننشئ قلب الدرس: خط أنابيب يقوم بتصحيح الميل، التحويل إلى ثنائي، وإزالة الضوضاء من المدخل. كل تحويل يستهدف ضعفاً محدداً في محركات OCR.

```python
# Step 2: Initialise the pre‑processing chain
preprocessor = ImagePreprocessor()

# Deskew – correct rotation so text lines are horizontal
preprocessor = preprocessor.deskew()

# Binarize – convert to pure black‑and‑white using a threshold (180 works well for most scans)
preprocessor = preprocessor.binarize(threshold=180)

# Remove noise – apply a mild median filter (strength=2) to smooth speckles
preprocessor = preprocessor.removeNoise(strength=2)
```

### لماذا هذه الخطوات الثلاث؟

1. **Deskew** – تفترض محركات OCR أن النص مُحاذٍ من اليسار إلى اليمين (أو من الأعلى إلى الأسفل). بضع درجات من الدوران يمكن أن تُخفض الدقة بأكثر من 30 ٪.
2. **Binarize** – تحويل الصورة إلى ثنائية يقلل البيانات التي يجب على محرك OCR تحليلها، ويُحسّن حواف الأحرف.
3. **Denoise** – البقع الصغيرة أو عيوب الضغط قد تُخطئ المحرك باعتبارها علامات ترقيم أو علامات تشكيل، خاصةً في السيريليكية حيث تشبه العديد من الحروف بعضها البعض.

> **ملاحظة حالة حافة:** إذا كانت صور المصدر نظيفة بالفعل، يمكنك تخطي `removeNoise` أو تقليل معامل `strength`. إزالة الضوضاء المفرطة قد تمحو تفاصيل دقيقة مثل نقاط التشكيل.

---

## الخطوة 3: تحميل الصورة وتطبيق خط الأنابيب

مع جاهزية خط الأنابيب، نمرره إلى مسار ملف. تُعيد طريقة `apply` كائن صورة مُعالجة يمكن لمحرك OCR استهلاكه مباشرة.

```python
# Path to the original Cyrillic image (adjust as needed)
image_path = os.path.join("YOUR_DIRECTORY", "cyrillic_skewed.jpg")

# Run the preprocessing pipeline
processed_image = preprocessor.apply(image_path)
```

إذا أردت معاينة النتيجة، يمكنك حفظها على القرص:

```python
# Optional: save the preprocessed image for visual verification
processed_image.save("preprocessed_cyrillic.jpg")
print("Preprocessed image saved – check the file to confirm deskewing and binarization.")
```

> **لماذا المعاينة؟** رؤية الصورة المُحوَّلة تساعدك على ضبط العتبات. أحياناً يكون العتبة 180 قاسية جداً؛ خفضها إلى 150 قد يحافظ على الخطوط الخفيفة.

---

## الخطوة 4: إعداد محرك OCR واستخراج النص

الآن ننتقل إلى جزء OCR الفعلي. سنُعدّ المحرك لاستخدام حزمة اللغة السيريليكية، وهو أمر أساسي لـ **extract text from Cyrillic image**.

```python
# Initialise the OCR engine
engine = OcrEngine()

# Tell the engine we’re working with Cyrillic text
engine.setLanguage(Language.Cyrillic)

# Perform recognition on the preprocessed image
ocr_result = engine.recognizeImage(processed_image)

# Extract plain text from the OCR result object
recognized_text = ocr_result.getText()
print("=== Recognized Text ===")
print(recognized_text)
```

### كيف يُحسّن هذا دقة OCR

- بإطعام صورة **نظيفة، مُصححة الميل، ومُثنائية**، يستطيع المحرك التركيز على أشكال الأحرف بدلاً من مكافحة الضوضاء.
- تحديد `Language.Cyrillic` يُفعّل مجموعة الأحرف والنموذج اللغوي الصحيح، وهو عامل رئيسي في **how to improve OCR accuracy** للغات غير اللاتينية.

---

## الخطوة 5: تجميع كل شيء في دالة قابلة لإعادة الاستخدام (اختياري)

إذا كنت تخطط لمعالجة ملفات متعددة، فإن تغليف المنطق يجعل الكود أنظف وأسهل صيانة.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Preprocess an image and extract Cyrillic text using the OCR engine.

    Parameters
    ----------
    image_path : str
        Full path to the source image.

    Returns
    -------
    str
        Recognized Cyrillic text.
    """
    # Build the preprocessing pipeline (could be cached for performance)
    preprocessor = (ImagePreprocessor()
                    .deskew()
                    .binarize(threshold=180)
                    .removeNoise(strength=2))

    processed = preprocessor.apply(image_path)

    engine = OcrEngine()
    engine.setLanguage(Language.Cyrillic)

    result = engine.recognizeImage(processed)
    return result.getText()


# Example usage
if __name__ == "__main__":
    sample_path = os.path.join("YOUR_DIRECTORY", "cyrillic_skewed.jpg")
    text = extract_cyrillic_text(sample_path)
    print("Extracted Cyrillic text:")
    print(text)
```

> **لماذا الدالة؟** تعزل منطق المعالجة، مما يجعل من السهل استبدال لغة مختلفة أو تعديل المعاملات دون إعادة كتابة السكريبت بالكامل.

---

## الأخطاء الشائعة وكيفية التعامل معها

| المشكلة | العرض | الحل |
|-------|----------|-----|
| **ميل شديد (>15°)** | النص يظهر مشوشاً أو مفقوداً | زيادة صلابة `deskew()` أو تدوير يدوي باستخدام `getRotationMatrix2D` في OpenCV. |
| **تباين منخفض** | التحويل إلى ثنائي يجعل كل شيء أبيض | خفض قيمة `threshold` أو تطبيق خطوة تمدد التباين قبل `binarize()`. |
| **حجم خط صغير** | الأحرف تلتصق بعد التحويل إلى ثنائي | استخدم صورة مصدر ذات دقة أعلى أو طبّق تمويه غاوسي خفيف قبل العتبة. |
| **لغات متعددة** | الأحرف السيريليكية تصبح غير قابلة للقراءة | اضبط `engine.setLanguage([Language.Cyrillic, Language.English])` إذا كانت المكتبة تدعم وضع متعدد اللغات. |
| **صيغة صورة غير مدعومة** | `apply()` يطرح خطأ | حوّل الصورة إلى PNG أو JPEG مسبقاً باستخدام Pillow (`Image.open().convert('RGB')`). |

---

## توسيع نهج **Image Preprocessing Pipeline Python**

1. **معالجة دفعية** – تكرار عبر مجلد من الصور، وتخزين كل نتيجة في ملف CSV.
2. **تنفيذ متوازي** – استخدم `concurrent.futures.ThreadPoolExecutor` لتسريع الأحمال الكبيرة.
3. **مرشحات مخصصة** – أضف عمليات شكلية (`erode`, `dilate`) للنماذج المطبوعة.
4. **تكامل OCR سحابي** – استبدل `OcrEngine` بعميل API (Google Vision, Azure Computer Vision) مع الحفاظ على خطوات المعالجة نفسها.

```python
# Example of batch processing with ThreadPoolExecutor
from concurrent.futures import ThreadPoolExecutor, as_completed

def batch_extract(folder: str):
    files = [os.path.join(folder, f) for f in os.listdir(folder) if f.lower().endswith('.jpg')]
    results = {}

    with ThreadPoolExecutor(max_workers=4) as executor:
        future_to_file = {executor.submit(extract_cyrillic_text, f): f for f in files}
        for future in as_completed(future_to_file):
            file_path = future_to_file[future]
            try:
                results[file_path] = future.result()
            except Exception as exc:
                results[file_path] = f"Error: {exc}"
    return results
```

---

## ملخص بصري

![preprocess image for OCR example](/images/ocr_preprocess_example.png "Diagram showing the preprocess image for OCR pipeline: deskew → binarize → denoise → OCR engine")

*يوضح المخطط كل مرحلة من سير عمل **preprocess image for OCR**، من المسح الخام إلى النص النهائي المستخرج.*

---

## الخاتمة

لقد استعرضنا حلًا كاملاً لـ **preprocess image for OCR** باستخدام بايثون، بدءًا من تثبيت الحزم المناسبة إلى بناء خط أنابيب **image preprocessing pipeline python** قوي، وأخيرًا **extract text from Cyrillic image**. عبر تطبيق تصحيح الميل، التحويل إلى ثنائي، وإزالة الضوضاء قبل تمرير الصورة إلى محرك OCR، ستلاحظ تحسنًا ملحوظًا في **how to improve OCR accuracy**، خاصةً مع النصوص السيريليكية الصعبة.

هل أنت مستعد للتحدي التالي؟ جرّب استبدال نموذج اللغة إلى العربية، جرب العتبة التكيفية، أو اربط الخط الأنابيب بواجهة Flask لمعالجة المستندات في الوقت الفعلي. السماء هي الحد، ومع هذا الأساس أنت مجهّز لتحويل المسحات الفوضوية إلى نصوص قابلة للبحث ونظيفة.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالكريستال!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Calculate Skew Angle for OCR Image Preprocessing](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}