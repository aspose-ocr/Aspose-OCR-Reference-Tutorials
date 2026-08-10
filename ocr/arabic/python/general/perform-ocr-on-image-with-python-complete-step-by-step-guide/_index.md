---
category: general
date: 2026-07-05
description: تنفيذ التعرف الضوئي على الأحرف (OCR) على صورة باستخدام بايثون. تعلم كيفية
  تحويل الصورة إلى نص بايثون، تحميل الصورة للتعرف الضوئي على الأحرف واستخراج النص
  السيريلي من الصورة في دقائق.
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: ar
og_description: قم بتنفيذ التعرف الضوئي على الأحرف (OCR) على صورة باستخدام بايثون.
  يوضح لك هذا الدليل كيفية تحويل الصورة إلى نص بايثون، تحميل الصورة للتعرف الضوئي
  على الأحرف واستخراج النص السيريلي من الصورة بسرعة.
og_title: إجراء التعرف الضوئي على الأحرف في الصورة باستخدام بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: إجراء التعرف الضوئي على الحروف (OCR) على صورة باستخدام بايثون – دليل كامل خطوة
  بخطوة
url: /ar/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على صورة باستخدام بايثون – دليل خطوة بخطوة كامل

هل تساءلت يومًا كيف **perform OCR on image** الملفات دون تسليمها إلى خدمة طرف ثالث؟ لست وحدك. في العديد من المشاريع—ماسحات جوازات السفر، محولات الإيصالات، أو أدوات الأرشفة—الحصول على النص الخام من صورة هو العائق الأول.  

في هذا الدليل سنستعرض مثالًا عمليًا ي **converts image to text python** النمط، يوضح لك كيفية **load image for OCR**، وأخيرًا **extract Cyrillic text from image** باستخدام مكتبة `aocr` المفتوحة المصدر. في النهاية ستتمكن من **recognize Cyrillic text** في أي صورة تضعها أمامه.

> **ما ستحصل عليه:** سكريبت جاهز للتنفيذ، شروحات واضحة لكل خطوة، ونصائح للتعامل مع المشكلات الشائعة (مثل المسحات الضبابية أو الخطوط غير المتوقعة). لا APIs خارجية، فقط بايثون نقي.

---

## المتطلبات المسبقة

- Python 3.8 أو أحدث مثبت.
- طرفية أو موجه أوامر تشعر بالراحة في استخدامه.
- حزمة `aocr` (قابلة للتثبيت عبر `pip install aocr`).
- ملف صورة يحتوي على أحرف سيريليّة (مثال: جواز سفر روسي ممسوح ضوئيًا).  

إذا كان أي من هذه غير مألوف لك، لا تقلق—سيتم تغطية كل نقطة من النقاط بإيجاز أثناء المتابعة.

## الخطوة 1: إجراء OCR على صورة – إعداد البيئة

أول شيء نحتاجه هو بيئة بايثون نظيفة حيث توجد مكتبة OCR. استخدام بيئة افتراضية يعزل الاعتمادات ويمنع تعارض الإصدارات.

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**لماذا؟**  
بيئة مخصصة تضمن أن حزمة `aocr` والملفات الثنائية الأصلية الخاصة بها لا تتداخل مع مشاريع أخرى. كما تجعل إمكانية إعادة الإنتاج سهلة—يمكن لشخص آخر استنساخ المستودع الخاص بك وتشغيل نفس أمر `pip install -r requirements.txt`.

> **نصيحة احترافية:** جمد الاعتمادات الخاصة بك باستخدام `pip freeze > requirements.txt` حتى تعرف دائمًا بالضبط أي الإصدارات تم استخدامها.

---

## الخطوة 2: تحميل الصورة لـ OCR – الاستيراد وتحضير الملف

الآن بعد أن المكتبة جاهزة، نحتاج إلى **load image for OCR**. طريقة `aocr.Image.from_file` تتعامل مع معظم الصيغ الشائعة (PNG, JPEG, TIFF). إليك كيف تقوم بذلك:

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**ما الذي يحدث هنا؟**  
`aocr.Image.from_file` يقرأ البيانات الثنائية، يفكّ تشفيرها، ويخزنها في كائن يمكن لمحرك OCR فهمه. إذا لم يتم العثور على الملف، سيُطلق بايثون استثناء `FileNotFoundError`، والذي يمكنك التقاطه لاحقًا إذا احتجت إلى معالجة الأخطاء بشكل أنيق.

> **حالة خاصة:** بعض الماسحات الضوئية تنتج ملفات TIFF متعددة الصفحات. في هذه الحالة، ستحتاج إلى تقسيم الصفحات أولاً—توفر `aocr` الدالة `Image.from_tiff_pages()` لهذا.

## الخطوة 3: تكوين محرك OCR – فرض التعرف على السيريليّة

افتراضيًا، العديد من محركات OCR تحاول تخمين اللغة، مما قد يؤدي إلى مخرجات مشوشة للخطوط غير اللاتينية. لت **recognize Cyrillic text** بشكل موثوق، نحدد صراحةً اللغة إلى “cyrillic”.

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**لماذا فرض اللغة؟**  
الأحرف السيريليّة تشترك في تشابه بصري مع الأحرف اللاتينية (مثال: “A” مقابل “А”). إخبار المحرك بتوقع السيريليّة يقلل من الأخطاء في التعرف بشكل كبير، خاصةً في المسحات منخفضة الدقة.

## الخطوة 4: إجراء OCR على صورة – تشغيل التعرف

مع تحميل الصورة وضبط المحرك، ن finally **perform OCR on image**. طريقة `recognize` تُعيد كائن `OcrResult` يحتوي على النص المستخرج وتقييمات الثقة.

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**ماذا يقدم لك `ocr_result`؟**  
- `text`: السلسلة النصية العادية للأحرف التي تم التعرف عليها.  
- `confidence`: عدد عشري (0‑1) يوضح مستوى الثقة العام.  
- `lines`: قائمة كائنات السطر إذا كنت بحاجة إلى تحكم دقيق.  

> **سؤال شائع:** *ماذا لو كان النص مقلوبًا رأسًا على عقب؟*  
> `aocr` يمكنه تدوير الصور تلقائيًا؛ فقط اضبط `ocr_engine.auto_rotate = True` قبل استدعاء `recognize`.

## الخطوة 5: تحويل الصورة إلى نص بايثون – معالجة النتيجة بعد الاستخراج

السلسلة الخام قد تحتوي على مسافات زائدة أو فواصل سطرية غير مرغوبة. لت **convert image to text python** النمط، سننظفها ببضع خطوات بسيطة:

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**لماذا العناء؟**  
المخرجات المنقحة أسهل في إدخالها إلى خطوط المعالجة اللاحقة—سواءً كنت تخزنها في قاعدة بيانات، أو تُرسلها إلى API ترجمة، أو تُجري بحثًا باستخدام regex لأرقام الجوازات.

## الخطوة 6: استخراج النص السيريلي من الصورة – تجميع كل شيء معًا

لنقم بدمج كل شيء في دالة واحدة قابلة لإعادة الاستخدام. هذا يجعل **extract Cyrillic text from image** سطرًا واحدًا في مشاريعك الخاصة.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**النتيجة التي يجب أن تراها (مثال):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

إذا كانت الصورة واضحة والخط يتطابق مع نموذج OCR، ستحصل على نسخ شبه كامل.

## استكشاف الأخطاء وإصلاحها & نصائح

| المشكلة | السبب المحتمل | الحل |
|-------|--------------|-----|
| أحرف مشوشة | إعداد لغة خاطئ | تأكد من `ocr_engine.language = "cyrillic"` |
| مخرجات فارغة | الصورة مظلمة جدًا أو منخفضة الدقة | عالج مسبقًا باستخدام `opencv` لزيادة التباين |
| اتجاه خاطئ | الصورة مدارة 90° | اضبط `ocr_engine.auto_rotate = True` |
| أداء بطيء | صورة كبيرة ( >5 MP ) | غيّر الحجم باستخدام `aocr.Image.resize(width=1024)` قبل التعرف |

![مثال على إجراء OCR على صورة](ocr_example.png "مثال على إجراء OCR على صورة")

*نص بديل: “مثال على إجراء OCR على صورة يُظهر كود بايثون يستخرج النص السيريلي من مسح جواز سفر.”*

## الخلاصة

لقد قمنا للتو **perform OCR on image** للملفات باستخدام بايثون نقي، وتعلمنا كيفية **load image for OCR**، فرضنا على المحرك **recognize Cyrillic text**، وأخيرًا **extract Cyrillic text from image** باستخدام دالة مساعدة منظمة. كامل خط الأنابيب—من تثبيت `aocr` إلى تنظيف النتيجة—يُناسب بضع عشرات من أسطر الكود ويمكن دمجه في أي مشروع يحتاج إلى **convert image to text python**.

## ما التالي؟

- **معالجة دفعات:** تكرار عبر مجلد من المسحات وتخزين النتائج في SQLite.
- **كشف اللغة:** دمج `langdetect` مع `aocr` للتبديل التلقائي بين السيريليّة واللاتينية.
- **معالجة مسبقة متقدمة:** استخدام `opencv` لتصحيح الميل، إزالة الضوضاء، أو تحويل الصور إلى ثنائية لزيادة الدقة.
- **التكامل مع FastAPI:** إظهار دالة `extract_cyrillic_text` كواجهة REST لتطبيقات الويب.

لا تتردد في التجربة—غيّر اللغة إلى “latin” لجوازات السفر الإنجليزية، أو جرّب محرك OCR مختلف تمامًا. المفاهيم تبقى نفسها، والكود مرن بما يكفي للتكيف.

برمجة سعيدة، ولتظل صورك دائمًا قابلة للقراءة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}