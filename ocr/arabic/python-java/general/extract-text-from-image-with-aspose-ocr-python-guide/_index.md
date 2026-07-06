---
category: general
date: 2026-03-28
description: استخراج النص من الصورة باستخدام Aspose OCR في بايثون – تعلم كيفية التعرف
  على النص من PNG، تحويل الصورة إلى نص بايثون، وتحميل الصورة للتعرف الضوئي على الأحرف
  بسرعة.
draft: false
keywords:
- extract text from image
- recognize text from png
- convert image to text python
- load image for ocr
- read text from scanned image
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في بايثون. يوضح هذا الدرس
  كيفية التعرف على النص من PNG، وتحويل الصورة إلى نص باستخدام بايثون، وتحميل الصورة
  للتعرف الضوئي على الأحرف.
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل بايثون
tags:
- OCR
- Python
- Aspose
- Image Processing
title: استخراج النص من الصورة باستخدام Aspose OCR – دليل بايثون
url: /ar/python-java/general/extract-text-from-image-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام Aspose OCR – دليل Python

هل احتجت يومًا إلى **استخراج النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة ستعطيك نتائج موثوقة على مسح PNG؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند التعامل مع ملفات PDF الممسوحة ضوئيًا أو صور الإيصالات. الخبر السار؟ باستخدام Aspose OCR للغة Python يمكنك التعرف على النص من ملفات PNG، تحويل الصورة إلى نص بأسلوب Python، وتحميل الصورة للـ OCR في بضع أسطر فقط.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح بالضبط كيف **استخراج النص من الصورة** باستخدام Aspose OCR. ستتعرف على كيفية تحميل الصورة، تمكين الكشف التلقائي عن اللغة، تشغيل محرك OCR، وأخيرًا قراءة اللغة المكتشفة والنص المستخرج. في النهاية ستتمكن من إدراج هذا الكود في أي مشروع يحتاج إلى قراءة النص من ملفات الصور الممسوحة.

## ما ستتعلمه

- كيفية **تحميل الصورة للـ OCR** باستخدام Aspose Storage.  
- كيفية **التعرف على النص من PNG** وتحديد لغته تلقائيًا.  
- كيفية **تحويل الصورة إلى نص Python** دون الحاجة للتعامل مع بافرات البايت منخفضة المستوى.  
- نصائح للتعامل مع ملفات PDF متعددة الصفحات، الأخطاء الشائعة، وسيناريوهات الحافة.  
- النتيجة المتوقعة وطرق سريعة للتحقق من نجاح الاستخراج.

### المتطلبات المسبقة

- تثبيت Python 3.8 أو أعلى على جهازك.  
- رخصة Aspose OCR للغة Python (أو مفتاح تجربة مجانية) – يمكنك الحصول عليها من موقع Aspose.  
- تثبيت الحزم `aspose-ocr` و `aspose-storage` عبر الأمر `pip install aspose-ocr aspose-storage`.  
- ملف PNG أو أي صورة مدعومة أخرى ترغب في معالجتها.

الآن، لنبدأ.

## الخطوة 1: تحميل الصورة للـ OCR

قبل أن يتمكن محرك OCR من القيام بأي شيء، يحتاج إلى كائن صورة. Aspose Storage يجعل ذلك سهلًا.

```python
# Step 1: Import required Aspose modules
import aspose.ocr as aocr
import aspose.storage as storage

# Step 1.1: Define the path to your image file
input_image_path = "YOUR_DIRECTORY/input_image.png"

# Step 1.2: Load the image – Aspose supports PNG, JPEG, BMP, TIFF, etc.
# The Image class abstracts away file‑system handling.
image = storage.Image.load(input_image_path)
```

*لماذا هذا مهم:* استخدام `storage.Image.load` يخفف عنك تفاصيل تنسيقات الملفات، بحيث يمكنك **التعرف على النص من png** أو JPEG دون كتابة محملات مخصصة. إذا لم يُعثر على الملف، ستطلق Aspose استثناء `FileNotFoundError` واضح يمكنك التقاطه للتعامل مع الخطأ برشاقة.

> **نصيحة احترافية:** حافظ على حجم الصور أقل من 5 ميغابايت لأفضل أداء. يمكن تقليل حجم الملفات الكبيرة باستخدام `image.resize()` قبل الـ OCR.

## الخطوة 2: تهيئة محرك OCR وتمكين اكتشاف اللغة

تأتي Aspose OCR بمحرك قوي `OcrEngine` يستطيع اكتشاف لغة النص تلقائيًا. تشغيل هذا الخيار غالبًا ما يحسن الدقة للوثائق متعددة اللغات.

```python
# Step 2: Initialise the OCR engine
ocr_engine = aocr.OcrEngine()

# Step 2.1: Enable automatic language detection (AUTO mode)
ocr_engine.language_detection = aocr.LanguageDetectionMode.AUTO
```

*لماذا هذا مهم:* عندما **تحول الصورة إلى نص python**، عادةً ما يهمك معرفة اللغة لأنها تؤثر على مجموعة الأحرف والقاموس المستخدم أثناء التعرف. وضع AUTO يسمح للمحرك باختيار الأنسب، سواء كان إنجليزيًا أو إسبانيًا أو صينيًا.

## الخطوة 3: التعرف على النص من PNG واستخراج النتيجة

الآن يحدث الجزء الأكثر تعقيدًا. طريقة `recognize` تشغل خط أنابيب OCR وتعيد كائن نتيجة غني.

```python
# Step 3: Run OCR on the loaded image
ocr_result = ocr_engine.recognize(image)

# Step 3.1: Pull out the detected language and the plain text
detected_lang = ocr_result.detected_language
extracted_text = ocr_result.text
```

إذا كنت تحتاج فقط إلى السلسلة النصية الخام، فـ `ocr_result.text` جاهزة للاستخدام. خاصية `detected_language` تعطيك رمز ISO‑639‑1 (مثال: `"en"` للإنجليزية).

> **حالة حافة:** بالنسبة للماسحات المتضررة بشدة، قد يعيد المحرك سلسلة فارغة. في هذه الحالة، فكر في معالجة الصورة مسبقًا (زيادة التباين، تصحيح الميل) باستخدام مكتبات مثل Pillow قبل تمريرها إلى Aspose.

## الخطوة 4: عرض النتيجة – ما الذي تتوقعه

لنطبع النتائج لتتمكن من التحقق من أن كل شيء يعمل.

```python
# Step 4: Show the detection results
print(f"Detected language: {detected_lang}")
print("Extracted text:")
print(extracted_text)
```

### ناتج تجريبي

```
Detected language: en
Extracted text:
Invoice #12345
Date: 2026‑03‑01
Total: $1,250.00
Thank you for your business!
```

إذا رأيت شيئًا مشابهًا، تهانينا—لقد نجحت في **استخراج النص من الصورة** باستخدام Aspose OCR! إذا كان الناتج مشوشًا، تحقق من جودة الصورة (على الأقل 300 dpi للنص المطبوع).

## الخطوة 5: نصائح متقدمة – التعامل مع ملفات PDF متعددة الصفحات والوثائق الممسوحة

بينما يعمل التدفق الأساسي مع PNG واحد، غالبًا ما تتعامل مع ملفات PDF متعددة الصفحات أو مجموعات TIFF.

1. **تحويل صفحات PDF إلى صور** – يمكن لـ Aspose PDF تصيير كل صفحة إلى PNG، ثم تمريرها إلى حلقة OCR.  
2. **المعالجة الدفعية** – تكرار عبر مجلد من الصور الممسوحة، وتجميع النتائج في قائمة أو كتابتها إلى CSV.  
3. **اختيار لغة مخصص** – إذا كنت تعلم أن المستند دائمًا بالفرنسية، اضبط `ocr_engine.language_detection = aocr.LanguageDetectionMode.FRENCH` لزيادة السرعة.

```python
# Example: Batch processing a folder of PNGs
import os

folder = "scans/"
texts = []
for file_name in os.listdir(folder):
    if file_name.lower().endswith(".png"):
        img = storage.Image.load(os.path.join(folder, file_name))
        result = ocr_engine.recognize(img)
        texts.append({"file": file_name,
                      "lang": result.detected_language,
                      "text": result.text})
```

الآن لديك مجموعة جاهزة يمكنك تصديرها باستخدام `json` أو `pandas`.

## الخطوة 6: الأخطاء الشائعة وكيفية تجنبها

| المشكلة | السبب | الحل |
|---------|-------|------|
| ناتج فارغ | الصورة منخفضة الدقة أو مضغوطة بشدة | رفع الدقة إلى ≥300 dpi، استخدم Pillow للحدّ من الضبابية |
| اكتشاف لغة غير صحيح | صفحات متعددة اللغات | اضبط `language_detection` يدويًا إلى لغة محددة أو عالج كل صفحة على حدة |
| خطأ ذاكرة عند الدفعات الكبيرة | تحميل العديد من الصور عالية الدقة في آن واحد | عالج الصور واحدةً تلو الأخرى، أو استخدم `gc.collect()` بعد كل تكرار |
| أحرف غير متوقعة | الخط غير مدعوم في قاموس OCR | فعّل `ocr_engine.enable_complex_script` إذا كنت تتعامل مع العربية أو الهندية |

## البرنامج الكامل القابل للتنفيذ

فيما يلي السكربت الكامل الذي يمكنك نسخه ولصقه في ملف باسم `extract_text.py`. استبدل `YOUR_DIRECTORY/input_image.png` بالمسار الفعلي لصورتك.

```python
# extract_text.py
# Complete example: extract text from image with Aspose OCR (Python)

import aspose.ocr as aocr
import aspose.storage as storage

def main():
    # 1️⃣ Load the image
    input_image_path = "YOUR_DIRECTORY/input_image.png"
    try:
        image = storage.Image.load(input_image_path)
    except Exception as e:
        print(f"❗ Unable to load image: {e}")
        return

    # 2️⃣ Initialise OCR engine and enable auto language detection
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language_detection = aocr.LanguageDetectionMode.AUTO

    # 3️⃣ Run OCR
    try:
        ocr_result = ocr_engine.recognize(image)
    except Exception as e:
        print(f"❗ OCR failed: {e}")
        return

    # 4️⃣ Output results
    print(f"Detected language: {ocr_result.detected_language}")
    print("Extracted text:")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

شغّله باستخدام:

```bash
python extract_text.py
```

ستظهر لك اللغة المكتشفة متبوعة بالنص المستخرج في سطر الأوامر.

## الخلاصة

أنت الآن تعرف كيف **استخراج النص من الصورة** باستخدام Aspose OCR في Python، من تحميل الملف إلى عرض النص المعترف به. هذا الحل المتكامل يتيح لك **التعرف على النص من png**، **تحويل الصورة إلى نص python** بسهولة، و**تحميل الصورة للـ OCR** في أي خط أنابيب أتمتة.

ما الخطوة التالية؟ جرّب معالجة دفعة من الإيصالات الممسوحة، صدّر النتائج إلى CSV، أو دمج خطوة OCR في سير عمل معالجة مستندات أكبر (مثل ملء قاعدة بيانات تلقائيًا). يمكنك أيضًا استكشاف مكتبة Aspose PDF لتحويل ملفات PDF الممسوحة إلى مستندات قابلة للبحث—وهي خطوة منطقية إذا كنت تتعامل مع **قراءة النص من صورة ممسوحة ضوئيًا** في ملفات PDF.

برمجة سعيدة، ولا تتردد في تجربة إعدادات لغات مختلفة، حيل ما قبل المعالجة للصور، أو حتى دمج Aspose OCR مع Tesseract لنهج هجين. إذا واجهت أي مشكلة، اترك تعليقًا أدناه—دعنا نحلها معًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}