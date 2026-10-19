---
category: general
date: 2026-03-18
description: قم بتشغيل OCR على الصورة بسرعة باستخدام بايثون. تعلّم كيفية التعرف على
  النص من ملفات PNG، تحميل الصورة للـ OCR، واستخراج الكلمات من الصورة في دليل خطوة
  بخطوة.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: ar
og_description: تشغيل OCR على الصورة باستخدام بايثون. يوضح هذا الدرس كيفية التعرف
  على النص من PNG، تحميل الصورة للـ OCR، واستخراج الكلمات من الصورة مع مثال كامل للكود.
og_title: تشغيل OCR على الصورة – دليل بايثون
tags:
- OCR
- Python
- Image Processing
title: تشغيل OCR على الصورة – مثال كامل للـ OCR باستخدام بايثون
url: /ar/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على الصورة – مثال كامل لـ Python OCR

هل احتجت يوماً إلى **run OCR on image** للملفات لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك؛ العديد من المطورين يواجهون هذه المشكلة عندما يبدأون باستخراج النص من المستندات الممسوحة ضوئيًا. في هذا الدرس سنستعرض **Python OCR example** يتيح لك **recognize text from PNG**، **load image for OCR**، و**extract words from image** مع درجات الثقة — كل ذلك في بضع أسطر من الشيفرة فقط.

سنغطي كل ما تحتاجه: المكتبة المطلوبة، كيفية إعداد المحرك، لماذا كل خطوة مهمة، وكيف يبدو الناتج. في النهاية، ستتمكن من وضع هذا المقتطف في مشروعك والبدء في استخراج النص من أي صورة فورًا. لا إطالة، مجرد حل عملي قابل للتنفيذ.

## ما ستحتاجه

- Python 3.8 أو أحدث مثبت  
- حزمة `ocrengine` (أو أي مكتبة توفر فئة `OcrEngine`). يمكنك تثبيتها عبر `pip install ocrengine` – عدّل الاسم إذا كنت تستخدم مكتبة OCR مختلفة مثل `pytesseract`.  
- ملف صورة (PNG، JPG، إلخ) تريد معالجته – في هذا الدليل سنستخدم `invoice.png`.  

هذا كل شيء. لا تبعيات ثقيلة، لا خدمات خارجية، فقط Python نقي.

![مثال تشغيل OCR على صورة يظهر فاتورة ممسوحة](/images/run-ocr-on-image.png)

*نص بديل: مثال تشغيل OCR على صورة – فاتورة ممسوحة يتم معالجتها*

## الخطوة 1 – تثبيت واستيراد مكتبة OCR

أولاً، لنقم بإضافة محرك OCR إلى بيئتنا واستيراده. إذا كنت تستخدم حزمة `ocrengine` الافتراضية، سيبدو الاستيراد هكذا:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**لماذا هذا مهم:** استيراد الفئة الصحيحة يمنحك الوصول إلى الطرق التي سنستدعيها لاحقًا، مثل `setImageFromFile` و `recognize`. إذا تخطيت هذه الخطوة، سيظهر لك خطأ `ModuleNotFoundError` وستعجز عن تحميل أي صورة.

## الخطوة 2 – إنشاء كائن محرك OCR

الآن بعد أن أصبحت المكتبة جاهزة، نحتاج إلى كائن محرك سيحمل الإعدادات والحالة لعملية التعرف.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*نصيحة احترافية:* بعض محركات OCR تسمح لك بتعديل نماذج اللغة أو إعدادات DPI في هذه المرحلة. بالنسبة إلى **python OCR example** أساسي، الإعدادات الافتراضية تعمل جيدًا، لكن إذا كنت تتعامل مع مسحات منخفضة الدقة، فكر في تعديلها هنا.

## الخطوة 3 – تحميل الصورة التي تريد معالجتها

الخطوة المنطقية التالية هي **load image for OCR**. توجه المحرك إلى مسار ملف PNG (أو أي صيغة مدعومة) التي تريد تحليلها.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**ما الذي يحدث تحت الغطاء؟** يقرأ المحرك بيانات البكسل، يحولها إلى صيغة يستطيع خوارزمية التعرف فهمها، ويخزنها داخليًا. إذا كان مسار الملف غير صحيح، ستحصل على `FileNotFoundError`، لذا تأكد من وجود الصورة.

## الخطوة 4 – تشغيل خوارزمية التعرف

بعد تحميل الصورة، ن finally **run OCR on image** لاستخراج المحتوى النصي.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

في هذه المرحلة يقوم المحرك بمسح البت ماب، يطبق مطابقة الأنماط، ويعيد كائن يحتوي على كل كلمة مكتشفة، السطر، ومقياس الثقة.

## الخطوة 5 – التكرار على الكلمات المعترف بها وعرض الثقة

أكثر جزء مفيد في أي سير عمل OCR هو رؤية **the confidence** لكل رمز مستخرج. هذا يخبرك بمدى تأكد المحرك من كل كلمة، مما يسمح لك بتصفية النتائج ذات الثقة المنخفضة إذا لزم الأمر.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**المخرجات المتوقعة** (عينة):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

يمكنك الآن رؤية بالضبط **what words were extracted from the image** ومدى موثوقية كل اكتشاف. هذا هو جوهر أي **extract words from image** pipeline.

## معالجة الحالات الشائعة

### ماذا لو كانت الصورة بتدرج الرمادي؟

بعض محركات OCR تعمل بشكل أفضل مع الصور الملونة. إذا لاحظت ثقة منخفضة عبر جميع الكلمات، جرّب تحويل PNG إلى نسخة ذات تباين أعلى بالأبيض والأسود قبل تمريرها إلى المحرك. يمكن أن تساعدك Pillow في ذلك:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### التعامل مع لغات متعددة

إذا كان مستندك يحتوي على الإنجليزية والإسبانية، ستحتاج إلى **recognize text from PNG** باستخدام نموذج متعدد اللغات. معظم المحركات تسمح لك بتحديد قائمة اللغات أثناء التهيئة:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### تصفية الكلمات ذات الثقة المنخفضة

أحيانًا تحتاج فقط إلى الكلمات التي تكون ثقتها فوق، لنقل، 90 %. يمكن تنفيذ فلتر سريع هكذا:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## سكريبت كامل وجاهز للتنفيذ

بجمع كل شيء معًا، إليك سكريبت واحد يمكنك نسخه ولصقه وتشغيله فورًا (فقط استبدل مسار PNG الخاص بك).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

شغّله باستخدام:

```bash
python run_ocr_on_image.py
```

سترى قائمة الكلمات ونسب الثقة مطبوعة في وحدة التحكم، تمامًا كما هو موضح سابقًا.

## الأسئلة المتكررة

**هل يعمل هذا مع ملفات JPG أو TIFF؟**  
بالتأكيد. طريقة `setImageFromFile` تقبل أي صيغة يمكن للمكتبة الأساسية فك تشفيرها، لذا يمكنك **run OCR on image** للملفات من نوع JPG، TIFF، BMP، إلخ.

**هل يمكنني معالجة صور متعددة في حلقة؟**  
بالطبع. ضع خطوات التحميل والتعرف داخل حلقة `for` على قائمة مسارات الملفات. فقط تذكر إعادة تهيئة المحرك إذا كانت المكتبة تتطلب كائنًا جديدًا لكل صورة.

**ماذا لو احتجت النص كسلسلة واحدة بدلاً من كل كلمة؟**  
معظم كائنات نتيجة OCR توفر طريقة `getText()` التي تُعيد المستند بالكامل. مثال:

```python
full_text = ocr_result.getText()
print(full_text)
```

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن عرفت كيف **run OCR on image**، فكر في استكشاف:

- **Post‑processing**: استخدم التعبيرات النمطية لتنظيف التواريخ، المبالغ، أو المعرفات المستخرجة من الفواتير.  
- **Batch processing**: دمج السكريبت مع `os.listdir()` لمعالجة مجلد كامل من المستندات الممسوحة.  
- **Alternative libraries**: `pytesseract` خيار مفتوح المصدر شائع؛ سير العمل مشابه—فقط استبدل استدعاءات المحرك.  
- **Exporting results**: اكتب الكلمات المستخرجة ودرجات الثقة إلى CSV للتحليل اللاحق.

كل من هذه الإضافات يبني مباشرةً على الأساس الذي وضعناه هنا، مما يتيح لك تحويل بيانات OCR الخام إلى معلومات قابلة للتنفيذ.

---

### TL;DR

عرضنا مثالًا مختصرًا، **python OCR example** يوضح كيفية **load image for OCR**، **run OCR on image**، و**extract words from image** مع الإبلاغ عن الثقة. السكريبت الكامل جاهز للتنفيذ، والآن لديك المعرفة لتكييفه مع أي مشروع يحتاج إلى **recognize text from PNG** (أو صيغ أخرى). جرّبه، عدّل عتبات الثقة، وشاهد تطبيقاتك تصبح واعية للنص في دقائق. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}