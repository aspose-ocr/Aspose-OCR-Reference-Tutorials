---
category: general
date: 2026-06-16
description: التعرف على النص من الصورة باستخدام محرك OCR بلغة بايثون – تعلم كيفية
  استخراج النص من الإيصال وتحسين دقة OCR في دقائق.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- improve ocr accuracy
- python ocr tutorial
- image preprocessing for OCR
language: ar
og_description: التعرف على النص من الصورة بسرعة. يوضح هذا الدليل كيفية استخراج النص
  من الإيصال وتحسين دقة OCR باستخدام بايثون.
og_title: التعرف على النص من الصورة باستخدام بايثون OCR – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  headline: recognize text from image with Python OCR – Complete Guide
  type: TechArticle
- description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  name: recognize text from image with Python OCR – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - A sample receipt image (JPEG or PNG) that you want to
      process. - The `ocr` package (the example uses a fictional `ocr` module for
      illustration; replace it with `pytesseract`, `easyocr`, or any library t'
  - name: Expected Output
    text: 'Running the script on a typical grocery receipt yields something like:'
  - name: H3 – Crop to the Receipt Region
    text: 'If your image contains a lot of background (e.g., a photo of a desk), crop
      it first:'
  - name: H3 – Use a Custom Language Pack
    text: 'For receipts that contain foreign characters (e.g., “€” or “¥”), load the
      appropriate language data:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: التعرف على النص من الصورة باستخدام بايثون OCR – دليل كامل
url: /ar/python-java/general/recognize-text-from-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة باستخدام Python OCR – دليل كامل

هل احتجت يومًا إلى **التعرف على النص من الصورة** لكن النتائج كانت غير مفهومة؟ لست وحدك. في العديد من سيناريوهات الأعمال الصغيرة—مثل مسح الفواتير، تحويل الفواتير إلى رقمية، أو استخراج البيانات من بطاقات الهوية—الحصول على مخرجات نظيفة وموثوقة هو الفارق بين سير عمل سلس وصداع رأس.

في هذا الدرس سنستعرض طريقة عملية لـ **التعرف على النص من الصورة** باستخدام مكتبة OCR خفيفة الوزن للـ Python. سنظهر لك أيضًا كيفية **استخراج النص من إيصال** ومشاركة حيل **تحسين دقة OCR** دون الحاجة لشراء برامج باهظة الثمن. جاهز؟ لنبدأ.

## ما ستبنيه

بنهاية هذا الدليل ستحصل على سكربت جاهز للتنفيذ يقوم بـ:

1. إنشاء محرك OCR.  
2. تفعيل المعالجة المسبقة الذكية (تصحيح الميل، إزالة البقع، التحويل إلى ثنائي).  
3. تحميل صورة إيصال مشوشة.  
4. تشغيل خط أنابيب التعرف تلقائيًا.  
5. طباعة نص نظيف قابل للبحث في وحدة التحكم.

بدون خدمات خارجية، بدون مفاتيح API مخفية—فقط كود Python نقي يمكنك تعديله لأي مشروع.

### المتطلبات المسبقة

- Python 3.8+ مثبت على جهازك.  
- إلمام أساسي بـ pip وبيئات virtual.  
- صورة إيصال تجريبية (JPEG أو PNG) تريد معالجتها.  
- حزمة `ocr` (المثال يستخدم وحدة `ocr` خيالية للتوضيح؛ استبدلها بـ `pytesseract` أو `easyocr` أو أي مكتبة توفر API مشابه).

> **نصيحة محترف:** إذا واجهت نقصًا في الاعتماديات، ثبّتها عبر `pip install ocr` (أو اسم الحزمة الفعلي) قبل المتابعة.

## الخطوة 1 – التعرف على النص من الصورة: إعداد المحرك

أولًا وقبل كل شيء. نحتاج إلى كائن يعرف كيف يقرأ بيانات البكسل ويحولها إلى أحرف. فكر في المحرك كعقل العملية؛ كل شيء آخر يزوده بالمعلومات.

```python
import ocr  # Replace with your actual OCR library import

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

لماذا ننشئ المحرك يدويًا؟ بعض المكتبات تسمح لك باستدعاء دالة واحدة، لكن إنشاء نسخة صريحة يمنحك تحكمًا دقيقًا في المعالجة المسبقة—وهو ما نحتاجه **لتحسين دقة OCR** لاحقًا.

## الخطوة 2 – استخراج النص من الإيصال: تفعيل المعالجة المسبقة

الإيصال الممسوح بهاتف عادةً ما يكون غير مثالي. قد يكون مائلًا قليلًا، مغطى ببقع غبار، أو يعاني من إضاءة غير متساوية. تفعيل المعالجة المسبقة يقوم بالعمل الشاق قبل أن ينظر المحرك إلى الأحرف.

```python
# Step 2: Enable preprocessing to improve recognition quality
preprocess = engine.preprocessing
preprocess.deskew = True        # Auto‑rotate slightly tilted pages
preprocess.despeckle = True     # Remove isolated noise pixels
preprocess.binarization = True  # Convert image to pure black‑white
```

*تصحيح الميل* (Deskew) يُستقيم الصفحة، *إزالة البقع* (despeckle) تمسح الشوائب، و*التحويل إلى ثنائي* (binarization) يجعل كل بكسل إما أسود أو أبيض. هذه العلامات الثلاث وحدها يمكن أن **تحسن دقة OCR** بنسبة 20‑30 % على الإيصالات المشوشة.

## الخطوة 3 – تحميل الصورة التي تريد التعرف عليها

الآن نوجه المحرك إلى الملف الفعلي. يمكن أن يكون المسار مطلقًا أو نسبيًا؛ فقط تأكد من وجود الصورة.

```python
# Step 3: Load the scanned receipt image
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")
```

إذا كنت تتساءل ما إذا كان المحرك يدعم ملفات PDF أو TIFF متعددة الصفحات، فإن معظم المكتبات الحديثة تدعم ذلك—فقط راجع الوثائق. بالنسبة لملف JPEG بصفحة واحدة، السطر أعلاه يكفي.

## الخطوة 4 – تشغيل OCR – المحرك يتولى البقية

مع تفعيل المعالجة المسبقة وتحميل الصورة، الاستدعاء التالي يقوم بكل شيء: يسبق المعالجة، يشغل خوارزمية التعرف، ويعيد كائن النتيجة.

```python
# Step 4: Run OCR – the configured preprocessing is applied automatically
ocr_result = engine.recognize()
```

خلف الكواليس قد يستخدم المحرك Tesseract، شبكة عصبية، أو محركًا مملوكًا. لا تحتاج إلى معرفة التفاصيل الداخلية؛ ستحصل فقط على نتيجة نظيفة.

## الخطوة 5 – إخراج النص المعترف به

أخيرًا، نستخرج النص العادي من النتيجة ونطبعه. في تطبيق حقيقي يمكنك كتابة النتيجة إلى قاعدة بيانات، ملف CSV، أو حتى تمريره إلى خط أنابيب تحليلي لاحق.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### النتيجة المتوقعة

تشغيل السكربت على إيصال بقالة نموذجي ينتج شيء مشابه لـ:

```
WALMART STORE #1234
123 Main St.
Anytown, USA

Date: 06/15/2026   Time: 14:32
Cashier: J. Doe

Item                Qty   Price
---------------------------------
Milk                1     2.99
Bread               2     5.48
Eggs                1     3.20
---------------------------------
Subtotal                    11.67
Tax                         0.93
Total                       12.60
```

إذا كان الناتج مشوشًا، تأكد من تفعيل علامات المعالجة المسبقة وأن الصورة ليست مظلمة جدًا. تعديل عتبة التحويل إلى ثنائي (بعض المكتبات تسمح بتحديد قيمة مخصصة) يمكن أن **يحسن دقة OCR** أكثر.

## متقدم: تحسين استخراج النص من الإيصال بسرعة

بينما يعمل سير العمل المكوّن من خمس خطوات لمعظم الحالات، قد ترغب في تسريع العملية عند معالجة مئات الإيصالات كل ليلة. إليك بعض التعديلات الاختيارية:

### H3 – قص إلى منطقة الإيصال

إذا كانت صورتك تحتوي على خلفية كثيرة (مثل صورة مكتب)، قصها أولًا:

```python
engine.image = engine.image.crop((50, 200, 800, 1200))  # left, top, right, bottom
```

### H3 – استخدام حزمة لغة مخصصة

للإيصالات التي تحتوي على أحرف أجنبية (مثل “€” أو “¥”)، حمّل بيانات اللغة المناسبة:

```python
engine.set_language('eng+deu+fra')  # English, German, French
```

كلا الحيلين يساعدان المحرك على **التعرف على النص من الصورة** بشكل أكثر موثوقية، خاصةً عندما يختلف المصدر.

## الأخطاء الشائعة وكيفية تجنبها

- **الخطوط المفقودة:** بعض محركات OCR تحتاج ملفات الخطوط للخطوط المتخصصة في الإيصالات. ثبّت حزم اللغة المناسبة.  
- **الضوضاء الزائدة:** حتى مع `despeckle=True`، قد تُربك الفحوصات ذات الحبيبات الكثيفة المحرك. فلتر يدوي سريع في Pillow (`Image.filter(ImageFilter.MedianFilter)`) قد يساعد.  
- **دقة DPI غير صحيحة:** تفترض محركات OCR حوالي 300 dpi. إذا كانت صورتك أقل، قم بتكبيرها أولًا: `engine.image = engine.image.resize((width*2, height*2))`.

معالجة هذه القضايا مباشرة **تحسن دقة OCR** دون اللجوء إلى خدمات طرف ثالث مكلفة.

## السكربت الكامل – جاهز للتنفيذ

فيما يلي البرنامج الكامل القابل للتنفيذ بلغة Python الذي يدمج كل ما ناقشناه. احفظه باسم `receipt_ocr.py` وشغّله عبر `python receipt_ocr.py`.

```python
import ocr  # Replace with the actual library you use

def main():
    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Enable preprocessing steps
    preprocess = engine.preprocessing
    preprocess.deskew = True
    preprocess.despeckle = True
    preprocess.binarization = True

    # Load the receipt image (change the path to your file)
    engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")

    # Optional: crop out unnecessary background
    # engine.image = engine.image.crop((50, 200, 800, 1200))

    # Run the recognition pipeline
    result = engine.recognize()

    # Print the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

تشغيل هذا السكربت سي **يتعرف على النص من الصورة** ويطبع كتلة منسقة من بيانات الإيصال. لا تتردد في تعديل إحداثيات القص، إعدادات اللغة، أو علامات المعالجة المسبقة لتتناسب مع تخطيطات إيصالاتك الخاصة.

## الخلاصة

لقد استعرضنا طريقة بسيطة لـ **التعرف على النص من الصورة** باستخدام Python، وأظهرنا كيفية **استخراج النص من إيصال**، وتعمقنا في عدة نصائح عملية **لتحسين دقة OCR**. الفكرة الأساسية بسيطة: إعداد محرك OCR، تفعيل المعالجة المسبقة الذكية، تزويده بصورة نظيفة، وترك المكتبة تقوم بالعمل الشاق.

ما الخطوات التالية؟ جرّب معالجة دفعة من الإيصالات داخل حلقة، احفظ كل نتيجة في CSV، أو اربط الناتج بنظام محاسبة. يمكنك أيضًا تجربة مكتبات OCR تعتمد على التعلم العميق مثل `easyocr` للحصول على دقة أعلى مع الخطوط المعقدة.

هل لديك أسئلة حول تنسيق إيصال معين أو تريد معرفة كيفية التعامل مع ملفات PDF متعددة الصفحات؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}