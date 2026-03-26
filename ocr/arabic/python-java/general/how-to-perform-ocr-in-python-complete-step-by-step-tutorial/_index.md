---
category: general
date: 2026-03-26
description: تعلّم كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) في بايثون والتعرف على
  النص من ملفات الصور. يوضح هذا الدليل كيفية استخراج النص من ملفات PNG وتحويل الصورة
  إلى نص بسرعة.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: ar
og_description: كيف تقوم بتنفيذ OCR في بايثون؟ اتبع هذا الدليل للتعرف على النص من
  الصورة، استخراج النص من PNG، وتحويل الصورة إلى نص باستخدام ترخيص تجريبي.
og_title: كيفية تنفيذ التعرف الضوئي على الأحرف في بايثون – دليل كامل
tags:
- OCR
- Python
- Image Processing
title: كيفية تنفيذ OCR في بايثون – دليل كامل خطوة بخطوة
url: /ar/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في بايثون – دليل خطوة بخطوة كامل  

هل تساءلت يومًا **كيف تقوم بتنفيذ OCR** على صورة التقطتها لتوك على هاتفك؟ لست وحدك—فالمطورون في كل مكان يحتاجون إلى طريقة موثوقة للتعرف على النص من ملفات الصور دون التعامل مع مكتبات أصلية معقدة.  

في هذا الدرس سنستعرض مثالًا عمليًا يوضح **كيفية تنفيذ OCR**، **التعرف على النص من الصورة**، و**استخراج النص من PNG** باستخدام غلاف خفيف الوزن لبايثون. في النهاية ستتمكن من **تحويل الصورة إلى نص** في بضع أسطر من الشيفرة، ولن تحتاج للقلق بشأن مشاكل الترخيص لأننا سنستخدم وضع التجربة المدمج.  

## ما ستتعلمه  

* كيفية إعداد ترخيص تجريبي لمحرك OCR (بدون الحاجة إلى مسار ملف).  
* التسلسل الدقيق لاستدعاءات **التعرف على النص من الصورة**.  
* طرق **استخراج النص من PNG** ومعالجة المشكلات الشائعة مثل الخطوط المفقودة.  
* نصائح لتوسيع الحل عندما تنتقل من ترخيص تجريبي إلى ترخيص إنتاج.  

**المتطلبات المسبقة** – تحتاج إلى Python 3.8+ وحزمة `ocr` (يمكن تثبيتها عبر `pip install ocr`). لا توجد أدوات خارجية أخرى مطلوبة.  

---  

![كيفية تنفيذ OCR في بايثون – مثال على النتيجة](https://example.com/ocr-demo.png "كيفية تنفيذ OCR في بايثون – النص المعترف به معروض")  

*نص بديل للصورة: كيفية تنفيذ OCR في بايثون – مثال على النتيجة*  

## الخطوة 1 – تفعيل ترخيص تجريبي (بدون مسار ملف)  

قبل أن يتمكن المحرك من قراءة أي شيء، يحتاج إلى ترخيص صالح. وضع التجربة مثالي للتجارب والمشاريع الصغيرة.  

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*لماذا هذا مهم:* كائن الترخيص يخبر مكتبة OCR أنك تعمل في بيئة تجريبية. إذا تخطيت هذه الخطوة، سيطلق المحرك خطأ `LicenseError` فور استدعاء `recognize()`.  

**نصيحة احترافية:** عندما تنتقل إلى ترخيص مدفوع، استبدل السطرين أعلاه بـ `ocr.License("path/to/your/license.key").apply()`.

## الخطوة 2 – إنشاء نسخة من محرك OCR  

الآن بعد تفعيل التجربة، نقوم بإنشاء نسخة من المحرك الرئيسي. فكر فيه كـ “العقل” الذي سيُمعن النظر في الصورة ويحدد مكان كل حرف.  

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*لماذا هذا مهم:* `OcrEngine` يحتفظ بإعدادات مثل حزم اللغات وإعدادات DPI. يمكنك تعديلها لاحقًا، لكن الإعداد الافتراضي يعمل مع معظم ملفات PNG الإنجليزية فقط.  

## الخطوة 3 – تحميل ملف PNG الذي تريد معالجته  

هنا نبدأ **التعرف على النص من الصورة**. تدعم طريقة `ocr.Imaging.Image.load()` صيغ PNG، JPEG، BMP، وبعض الصيغ الأخرى.  

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*حالة خاصة:* إذا كان ملف PNG الخاص بك يستخدم لوحة ألوان مفهرسة (شائع في لقطات الشاشة)، سيقوم المحمل تلقائيًا بتحويله إلى مخزن 24‑bit RGB. قد يضيف هذا التحويل قليلًا من الحمل على الأداء، لكنه يضمن نتائج OCR دقيقة.  

## الخطوة 4 – تشغيل OCR واستخراج النص  

أخيرًا، نطلب من المحرك تنفيذ مهمته ثم نستخرج النتيجة كنص عادي.  

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**الناتج المتوقع** (مثال لصورة بسيطة تحتوي على “Hello World”):  

```
Hello World
```

إذا احتوت الصورة على عدة أسطر، سيحافظ الناتج على فواصل الأسطر، مما يسهل تمريره إلى عمليات لاحقة مثل محللات CSV أو خطوط أنابيب NLP.  

## اختياري: تحسين الدقة عبر الضبط الدقيق  

* **حزم اللغات:** `ocr_engine.set_language("eng")` (الافتراضي) أو `"fra"` للفرنسية.  
* **تحجيم DPI:** `ocr_engine.set_dpi(300)` يمكن أن يحسن النتائج على المسحات منخفضة الدقة.  
* **المعالجة المسبقة:** تطبيق عتبة ثنائية (`ocr.Imaging.Image.threshold()`) قبل `set_image` غالبًا ما ينتج نصًا أنظف على خلفيات صاخبة.  

هذه التعديلات مفيدة عندما تنتقل من عرض تجريبي سريع إلى دليل **ocr tutorial python** إنتاجي يعالج مئات الملفات يوميًا.  

## السكريبت الكامل – جاهز للنسخ واللصق  

فيما يلي السكريبت الكامل القابل للتنفيذ الذي يجمع جميع الخطوات السابقة. احفظه باسم `run_ocr.py` واستبدل `YOUR_DIRECTORY/sample1.png` بالمسار إلى ملف PNG الخاص بك.  

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

شغّله من سطر الأوامر:  

```bash
python run_ocr.py
```

ستظهر لك النصوص المستخرجة مطبوعة في وحدة التحكم. إذا حصلت على سلسلة فارغة، تحقق مرة أخرى من أن الصورة تحتوي على نص واضح وعالي التباين وأن الترخيص التجريبي تم تطبيقه دون أخطاء.  

## أسئلة شائعة ومشكلات محتملة  

* **“هل يعمل مع JPEG?”** – بالتأكيد. طريقة `load()` تكتشف الصيغة تلقائيًا، لذا يمكنك استبدال PNG بـ JPEG دون تعديل الشيفرة.  
* **“ماذا لو كانت الصورة مائلة?”** – يمكن للمحرك اكتشاف الاتجاه تلقائيًا، لكن للحصول على أفضل النتائج يمكنك تدوير الصورة مسبقًا باستخدام `input_image.rotate(90)` قبل `set_image`.  
* **“هل يمكن معالجة عدة صور داخل حلقة?”** – نعم. فقط انقل عمليات التحميل واستدعاء `recognize()` داخل حلقة `for`؛ يمكن إعادة استخدام نفس نسخة `ocr_engine`، مما يوفر قليلًا من الحمل.  

## الخطوات التالية – من العرض التجريبي إلى الإنتاج  

الآن بعد أن عرفت **كيفية تنفيذ OCR**، فكر في المواضيع التالية:  

* **المعالجة الدفعية** – دمج هذا السكريبت مع `os.listdir()` لـ **استخراج النص من PNG** على نطاق واسع.  
* **التكامل مع PDF** – استخدم `pdf2image` لتحويل صفحات PDF إلى PNG، ثم مررها إلى نفس خط الأنابيب.  
* **المعالجة اللاحقة** – طبّق تعبيرات regex أو مطابقة تقريبية لتنظيف الأخطاء الشائعة في OCR (مثل “0” مقابل “O”).  

كل من هذه الأفكار يبني على الفكرة الأساسية لـ **تحويل الصورة إلى نص** ويزيد من فائدة سير عمل OCR الخاص بك.  

---  

### TL;DR  

لقد غطينا كل ما تحتاج معرفته لـ **كيفية تنفيذ OCR** في بايثون: تفعيل ترخيص تجريبي، إنشاء محرك، تحميل PNG، تشغيل التعرف، وطباعة النتيجة. ببضع أسطر فقط يمكنك **التعرف على النص من الصورة**، **استخراج النص من PNG**، و**تحويل الصورة إلى نص** لأي تطبيق لاحق.  

جرّبه، عدّل إعدادات DPI أو اللغة، ودع المحرك يتولى الجزء الصعب. برمجة سعيدة!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}