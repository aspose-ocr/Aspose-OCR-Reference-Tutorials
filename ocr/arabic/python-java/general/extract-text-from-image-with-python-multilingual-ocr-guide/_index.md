---
category: general
date: 2026-04-26
description: استخراج النص من الصورة باستخدام Aspose OCR في بايثون. تعلم كيفية استخراج
  النص، تحويل الصورة إلى نص، وتحميل الصورة للتعرف الضوئي على الأحرف مع دعم متعدد اللغات.
draft: false
keywords:
- extract text from image
- how to extract text
- convert image to text
- load image for ocr
- multilingual ocr python
language: ar
og_description: استخراج النص من الصورة فورًا. يوضح هذا الدليل كيفية استخراج النص،
  تحويل الصورة إلى نص، وتحميل الصورة للتعرف الضوئي على الأحرف باستخدام Aspose OCR
  في بايثون.
og_title: استخراج النص من الصورة باستخدام بايثون – دليل OCR متعدد اللغات الكامل
tags:
- OCR
- Python
- Aspose
title: استخراج النص من الصورة باستخدام بايثون – دليل OCR متعدد اللغات
url: /ar/python-java/general/extract-text-from-image-with-python-multilingual-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام بايثون – دليل OCR متعدد اللغات

هل احتجت يوماً إلى **استخراج النص من صورة** لكن لم تكن متأكدًا أي مكتبة يمكنها التعامل مع صفحات متعددة اللغات؟ لست وحدك. في العديد من التطبيقات الواقعية—مثل معالجة الفواتير، مراقبة وسائل التواصل الاجتماعي، أو أرشفة المستندات متعددة اللغات—ستصادف صورًا تحتوي على أحرف لاتينية وسيريلية معًا.

الخبر السار؟ مع Aspose OCR للبايثون يمكنك **استخراج النص**، **تحويل الصورة إلى نص**، و**تحميل الصورة لـ OCR** في بضع أسطر فقط، مع السماح للمحرك باكتشاف اللغة تلقائيًا. في هذا الدرس سنستعرض مثالًا كاملاً قابلًا للتنفيذ، نشرح لماذا كل خطوة مهمة، ونغطي بعض الحالات الخاصة التي قد تواجهها.

> **ما ستستفيده**  
> * برنامج جاهز للتنفيذ يقرأ النص من صورة PNG متعددة اللغات.  
> * فهم كيفية ضبط OCR متعدد اللغات في بايثون.  
> * نصائح للتعامل مع الملفات الكبيرة، صيغ الصور المختلفة، وتصحيح الأخطاء الشائعة.  

## المتطلبات المسبقة

- بايثون 3.8 أو أحدث (الكود يستخدم f‑strings).  
- حزمة `asposeocr` مثبتة (`pip install asposeocr`).  
- ملف صورة (مثال: `mixed_lang.png`) يحتوي على نص بأكثر من نظام كتابة.  
- معرفة أساسية باستيراد بايثون وواجهات برمجة التطبيقات الكائنية.  

لا توجد تبعيات ثقيلة، ولا خدمات خارجية—فقط تثبيت واحد عبر pip وستكون جاهزًا.

---

## الخطوة 1 – تثبيت واستيراد مكتبة Aspose OCR  

قبل أن نتمكن من **تحميل الصورة لـ OCR**، نحتاج إلى المكتبة نفسها. الحزمة تتضمن محرك OCR الأساسي ومحمّل صور خفيف الوزن.

```python
# Install the package (run once in your environment)
# pip install asposeocr

# Import the required classes
import asposeocr as aocr
from asposeocr import OcrEngine, OcrConfig, Language
```

*لماذا هذا مهم*: استيراد الفئات المحددة يبقي مساحة الأسماء منظمة ويجعل الكود اللاحق أكثر وضوحًا. إذا استوردت فقط `asposeocr`، سيتعين عليك تأهيل كل استدعاء (`aocr.OcrEngine()`)، مما يضيف ضوضاء.

---

## الخطوة 2 – إنشاء محرك OCR وتمكين الكشف متعدد اللغات  

يمكن لـ Aspose OCR تخمين اللغة (اللغات) الموجودة في الصورة تلقائيًا. ضبط `Language.AUTO` يغطي اللاتينية، السيريلية، العربية، والعديد غيرها.

```python
# Initialize the OCR engine
ocr_engine = OcrEngine()

# Enable automatic language detection (covers Latin, Cyrillic, etc.)
ocr_engine.config.language = Language.AUTO
```

*نصيحة محترف*: إذا كنت تعرف مجموعة اللغات مسبقًا، يمكنك تعيين `Language.ENGLISH` أو `Language.RUSSIAN` للحصول على تحسين طفيف في الأداء. لكن بالنسبة للمستندات المختلطة حقًا، فإن `AUTO` هو الخيار الأكثر أمانًا.

---

## الخطوة 3 – تحميل الصورة التي تريد معالجتها  

هنا نـ **نحمّل الصورة لـ OCR**. يدعم Aspose صيغ PNG، JPEG، BMP، TIFF، وحتى صفحات PDF التي تُعامل كصور.

```python
# Path to the image containing mixed‑language text
image_file_path = "YOUR_DIRECTORY/mixed_lang.png"

# Load the image into the OCR engine
ocr_engine.image = aocr.Image.load(image_file_path)
```

> **نصيحة**: إذا كانت صورتك أكبر من 2 ميغابايت، فكر في تصغير حجمها مسبقًا. الصور الكبيرة تستهلك ذاكرة أكثر ويمكن أن تبطئ خطوة الكشف.

---

## الخطوة 4 – تشغيل عملية OCR والتقاط النتيجة  

استدعاء `process()` يقوم بالعمل الشاق: كشف النص، تحليل التخطيط، وفك تشفير اللغة.

```python
# Execute the OCR operation
ocr_result = ocr_engine.process()
```

كائن `ocr_result` المعاد يحتوي على عدة خصائص مفيدة:

| الخاصية | الوصف |
|----------|-------------|
| `text`   | سلسلة نصية عادية للنص المعترف به (ما ستستخدمه في الأغلب). |
| `confidence` | درجة الثقة العامة (0‑100). |
| `lines`  | قائمة كائنات `OcrLine` مع بيانات الموقع (مفيد للـ PDFs). |

---

## الخطوة 5 – عرض النص المستخرج  

أخيرًا، نطبع النتيجة. في تطبيق حقيقي قد تكتبها إلى قاعدة بيانات أو تمررها إلى واجهة برمجة تطبيقات ترجمة.

```python
print("Recognized Text:")
print(ocr_result.text)
```

**الناتج المتوقع** (مثال لصورة متعددة اللغات):

```
Recognized Text:
Hello world!
Привет мир!
```

إذا ظهرت رموز غير مفهومة، تحقق من أن الصورة غير تالفة وأنك تستخدم أحدث نسخة من `asposeocr` (v23.7 في وقت كتابة هذا الدليل).

---

## الخطوة 6 – السكريبت الكامل يمكنك نسخه ولصقه  

جمع كل الأجزاء معًا يزيل الالتباس حول "من أين يبدأ الكود؟". احفظ هذا الملف باسم `multilingual_ocr.py` وشغّله من سطر الأوامر.

```python
# multilingual_ocr.py
# -------------------------------------------------
# Complete example: extract text from image (multilingual)
# -------------------------------------------------

import asposeocr as aocr
from asposeocr import OcrEngine, Language

def extract_text(image_path: str) -> str:
    """
    Loads an image, runs Aspose OCR with auto language detection,
    and returns the recognized text.
    """
    engine = OcrEngine()
    engine.config.language = Language.AUTO
    engine.image = aocr.Image.load(image_path)
    result = engine.process()
    return result.text

if __name__ == "__main__":
    # Adjust this path to point at your own image file
    img_path = "YOUR_DIRECTORY/mixed_lang.png"
    text = extract_text(img_path)
    print("Recognized Text:")
    print(text)
```

شغّله:

```bash
python multilingual_ocr.py
```

يجب أن ترى السلاسل المستخرجة مطبوعة في وحدة التحكم. هذا كل شيء—**تحويل الصورة إلى نص** ببضع أسطر فقط.

---

## أسئلة شائعة ومعالجة الحالات الخاصة  

### ماذا لو كانت صورتي تحتوي على كتابة يدوية؟  
Aspose OCR مخصص للنص المطبوع. النصوص المكتوبة يدويًا غالبًا ما تحتاج نموذجًا مخصصًا (مثل Azure Read أو Google Vision). يمكنك تجربة `Language.AUTO`، لكن توقع ثقة أقل.

### كيف أحسن الدقة في المسحات الضوضائية؟  
1. عالج الصورة مسبقًا (تحويل إلى أبيض-أسود، إزالة البقع).  
2. زد DPI إلى ما لا يقل عن 300 ppi قبل تمريرها للمحرك.  
3. اضبط `ocr_engine.config.deskew = True` إذا كانت الصورة مائلة.

```python
ocr_engine.config.deskew = True
```

### هل يمكن استخراج النص من PDF دون تحويله إلى صورة أولًا؟  
نعم—Aspose OCR يمكنه فتح صفحات PDF مباشرة:

```python
ocr_engine.image = aocr.Image.load("document.pdf", page_number=1)
```

تذكر أن كل صفحة تُعامل كصورة داخليًا، لذا تنطبق نفس اعتبارات الجودة.

---

## الخلاصة  

أصبح لديك الآن وصفة شاملة من البداية إلى النهاية **لاستخراج النص من الصورة** باستخدام Aspose OCR في بايثون، مع دعم متعدد اللغات. يوضح السكريبت كيفية **تحميل الصورة لـ OCR**، **تحويل الصورة إلى نص**، وكيفية التعامل مع أكثر المشكلات شيوعًا.

من هنا يمكنك:

- دمج الدالة في خدمة ويب تستقبل تحميلات المستخدمين.  
- ربط النص المستخرج بمكتبة كشف لغة لتوجيهه إلى محرك الترجمة المناسب.  
- تجربة خيارات `ocr_engine.config` (مثل `max_recognition_time`، `text_orientation`) لضبط الأداء بدقة.

برمجة سعيدة، ولتكن خطوط OCR دائمًا دقيقة!  

---  

![Screenshot of extracted multilingual text – extract text from image example](image-placeholder.png "extract text from image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}