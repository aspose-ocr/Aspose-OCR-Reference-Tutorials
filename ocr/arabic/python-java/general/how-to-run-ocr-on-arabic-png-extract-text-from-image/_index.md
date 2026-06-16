---
category: general
date: 2026-03-26
description: تعلم كيفية تشغيل OCR على صور PNG العربية واستخراج النص العربي بسرعة.
  يوضح هذا الدليل تحويل الصورة إلى نص باستخدام كود بايثون خطوة بخطوة.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: ar
og_description: كيف تشغّل OCR على صور PNG العربية؟ اتبع هذا الدليل الكامل لاستخراج
  النص العربي، والتعرف على النص العربي، وتحويل الصورة إلى نص باستخدام بايثون.
og_title: كيفية تشغيل OCR على صورة PNG عربية – استخراج النص من الصورة
tags:
- OCR
- Python
- Arabic
title: كيفية تشغيل OCR على صورة PNG عربية – استخراج النص من الصورة
url: /ar/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR على PNG عربي – استخراج النص من الصورة

هل تساءلت يومًا **كيف تشغّل OCR** على صورة تحتوي على نص عربي؟ ربما لديك إيصالًا ممسوحًا، مخطوطة تاريخية، أو مجرد لقطة شاشة لمنشور على وسائل التواصل الاجتماعي وتحتاج النص بصيغة قابلة للبحث. لست وحدك—المطورون حول العالم يواجهون هذه المشكلة عند التعامل مع اللغات من اليمين إلى اليسار.

في هذا الدرس سنستعرض مثالًا كاملًا وقابلاً للتنفيذ يوضح **كيف تشغّل OCR** على ملف PNG، استخراج النص العربي، وطباعة النتيجة في وحدة التحكم. لا روابط غامضة “انظر الوثائق”؛ فقط الكود الذي يمكنك نسخه‑لصقه، بالإضافة إلى شرح سبب أهمية كل سطر. في النهاية ستكون قادرًا على **تحويل الصورة إلى نص** بثقة، حتى عندما تكون الصورة PNG عربية صعبة.

> **ما ستتعلمه**
> - إعداد محرك OCR في بايثون للغة العربية  
> - تحميل صورة PNG ومعالجة المشكلات الشائعة  
> - التعرف على النص العربي والتحقق من الناتج  
> - نصائح **لاستخراج النص العربي** من صور ذات جودة مختلفة  

قبل أن نبدأ، تأكد من تثبيت بايثون 3.8+ وإصدار حديث من مكتبة `ocr` (المستخدمة في المقتطف). إذا كنت تستخدم بيئة افتراضية، فعّلها الآن—هذا يحافظ على نظافة الاعتمادات.

## المتطلبات المسبقة

- بايثون 3.8 أو أحدث  
- حزمة `ocr` (`pip install ocr‑engine` – استبدل بالاسم الفعلي للحزمة)  
- صورة PNG عربية (`arabic_doc.png`) موجودة في مسار يمكنك الإشارة إليه  
- معرفة أساسية بدوال وفئات بايثون  

هذا كل شيء. لا أطر عمل ثقيلة، لا حاويات Docker—فقط بايثون عادي.

## الخطوة 1: تثبيت واستيراد مكتبة OCR

أولًا وقبل كل شيء. نحتاج إلى محرك OCR نفسه. المكتبة التي سنستخدمها توفر فئة `OcrEngine` بواجهة برمجة تطبيقات بسيطة.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*لماذا نستورد `Imaging` بشكل منفصل؟* وحدة `Imaging` الفرعية توفر طريقة `Image.load` المريحة التي تدعم PNG و JPEG و TIFF مباشرة. تخطي هذه الخطوة يجبرك على التعامل مع البايتات الخام بنفسك، وهو أمر غير ضروري لمعظم الاستخدامات.

## الخطوة 2: إنشاء نسخة من محرك OCR

الآن ننشئ نسخة من المحرك. فكر في هذا الكائن كـ “العقل” الذي سيعالج الصورة.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **نصيحة احترافية:** إذا كنت تخطط لمعالجة العديد من الصور على التوالي، أعد استخدام نفس نسخة `ocr_engine`. فهي تخزن نماذج اللغات في الذاكرة، مما يسرّع عمليات التعرف اللاحقة.

## الخطوة 3: ضبط اللغة إلى العربية

العربية ليست لاتينية؛ لها مجموعة أحرف خاصة، اتجاه من اليمين إلى اليسار، وتشكيل سياقي. لهذا نحتاج إلى إخبار المحرك صراحةً أي نموذج لغة يجب تحميله.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

إذا نسيت هذا السطر، سيعود المحرك إلى اللغة الإنجليزية افتراضيًا وستحصل على ناتج مشوش—شيء رأيته يحدث كثيرًا.

## الخطوة 4: تحميل صورة PNG الخاصة بك

هنا يبدأ الجزء الفعلي من **تحويل الصورة إلى نص**. سنحمّل ملف PNG الذي يحتوي على النص العربي.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### حالات الحافة الشائعة

| المشكلة | العَرَض | الحل |
|-------|---------|-----|
| الصورة مظلمة جدًا | الناتج يحتوي على فراغات كثيرة | المعالجة المسبقة باستخدام Pillow (`ImageEnhance.Brightness`) |
| PNG يحتوي على قناة ألفا | بعض محركات OCR تقرأ البكسلات الشفافة بشكل خاطئ | تحويل إلى RGB (`image.convert("RGB")`) قبل التحميل |
| النص مائل | النص المعترف به مقلوب | تدوير الصورة (`image.rotate(90, expand=True)`) قبل تمريرها إلى المحرك |

## الخطوة 5: تشغيل عملية التعرف

بعد إعداد كل شيء، نطلب من المحرك الآن أداء مهمته.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

طريقة `recognize` تُعيد كائنًا يحتوي على السلسلة النصية Unicode الخام، درجات الثقة، ومربعات الإحاطة. بالنسبة لمعظم المطورين، النص العادي هو كل ما تحتاجه.

## الخطوة 6: إخراج النص العربي المُعترف به

الآن نطبع النتيجة. في تطبيق حقيقي قد تكتبها إلى ملف، قاعدة بيانات، أو تُرسلها إلى واجهة ترجمة.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

عند تشغيل السكريبت، يجب أن ترى الأحرف العربية تُعرض في وحدة التحكم (تأكد من أن الطرفية تدعم Unicode). إذا ظهرت علامات استفهام أو سلاسل فارغة، راجع إعداد اللغة وجودة الصورة.

### الناتج المتوقع

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

إذا كان الناتج مشابهًا للسطر أعلاه، تهانينا—لقد نجحت في **استخراج النص العربي** من PNG!

## مثال كامل يعمل

فيما يلي السكريبت بالكامل، جاهز للنسخ‑اللصق. استبدل `YOUR_DIRECTORY/arabic_doc.png` بالمسار إلى ملفك الخاص.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

شغّله باستخدام `python run_ocr.py` (أو أي اسم أعطيته للملف). إذا تم تثبيت كل شيء بشكل صحيح، سترى الجملة العربية مطبوعة في الطرفية.

## كيفية تشغيل OCR على صيغ صور مختلفة

نفس الكود يعمل مع JPEG أو TIFF أو BMP—فقط غير امتداد الملف. طريقة `Image.load` تكتشف الصيغة تلقائيًا، لذا يمكنك **تحويل الصورة إلى نص** دون أي كود إضافي.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

تذكر أن جودة الصورة المصدر تؤثر بشكل كبير على دقة خطوة **التعرف على النص العربي**. الصور عالية الدقة ومنخفضة الضغط تعطي أفضل النتائج.

## استخراج النص من PNG: نصائح لتحسين الدقة

1. **الدقة مهمة** – استهدف على الأقل 300 dpi. الدقة الأقل غالبًا ما تؤدي إلى فقدان الأحرف.  
2. **التباين هو الملك** – استخدم أدوات معالجة الصور (مثل OpenCV) لزيادة التباين قبل تمرير الصورة إلى محرك OCR.  
3. **إزالة الضوضاء** – البقع الصغيرة قد تشوش النموذج؛ الترشيح المتوسط يساعد.  

إليك مقتطف سريع باستخدام Pillow لتحسين PNG قبل OCR:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## الأسئلة المتكررة

**س: هل يعمل هذا مع لغات من اليمين إلى اليسار غير العربية؟**  
ج: بالتأكيد. فقط غير رمز اللغة (`"ar"` → `"he"` للعبري، `"fa"` للفارسية) وسيحمّل المحرك النموذج المناسب.

**س: ماذا لو أردت استخراج النص من عدة PNGs في مجلد؟**  
ج: قم بالتكرار على الملفات، أعد استخدام نفس نسخة `ocr_engine`، واجمع النتائج في قائمة أو اكتب كل واحدة في ملف `.txt` منفصل.

**س: هل يمكنني الحصول على درجات الثقة لكل كلمة؟**  
ج: نعم. غالبًا ما يوفر `ocr_result` طريقة `get_confidences()`. اربط كل درجة بال كلمة المقابلة للتحكم في الجودة.

## الخطوات التالية

الآن بعد أن عرفت **كيف تشغّل OCR** على PNGs عربية، فكر في الأفكار التالية:

- **المعالجة الدفعية:** دمج السكريبت مع `os.listdir` لـ **استخراج النص العربي** من دليل كامل.  
- **ما بعد المعالجة:** استخدم مكتبات `arabic_reshaper` و `python-bidi` لعرض النص من اليمين إلى اليسار بشكل صحيح في ملفات PDF.  
- **التكامل:** أدخل النص المستخرج إلى فهرس بحث (مثل Elasticsearch) لجعل المستندات الممسوحة قابلة للبحث.  

كل من هذه المواضيع يبني على الأساسيات التي غطيناها هنا، وستساعدك على تحويل سكريبت **تحويل الصورة إلى نص** بسيط إلى خط أنابيب جاهز للإنتاج.

---

![how to run OCR on Arabic PNG](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}