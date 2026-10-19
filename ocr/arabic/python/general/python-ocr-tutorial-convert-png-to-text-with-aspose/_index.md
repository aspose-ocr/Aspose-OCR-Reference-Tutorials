---
category: general
date: 2026-09-19
description: يظهر دليل Python OCR كيفية تحويل PNG إلى نص باستخدام Aspose OCR. تعلم
  استخراج النصوص باستخدام OCR في بايثون واستخراج النص من الصور الممسوحة ضوئياً.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- python OCR tutorial
- convert PNG to text
- OCR text extraction python
- extract text image python
- extract text scanned image
language: ar
lastmod: 2026-09-19
og_description: يُرشدك برنامج تعليمي للـ OCR بلغة بايثون إلى تحويل ملفات PNG إلى نص
  باستخدام Aspose OCR. اتقن استخراج النصوص باستخدام OCR في بايثون واستخراج النص من
  الصور الممسوحة ضوئياً.
og_image_alt: Screenshot of Python OCR code extracting text from a PNG image
og_title: دورة OCR بايثون – تحويل PNG إلى نص باستخدام Aspose
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  headline: 'Python OCR tutorial: convert PNG to text with Aspose'
  type: TechArticle
- description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  name: 'Python OCR tutorial: convert PNG to text with Aspose'
  steps:
  - name: Expected output
    text: 'If `sample.png` contains the sentence “Hello, world!”, the console will
      show:'
  - name: 1. Non‑PNG formats
    text: Even though this tutorial focuses on **convert PNG to text**, you might
      receive JPEG or TIFF files. The same code works; just change the file extension
      in `load_image`.
  - name: 2. Low‑resolution images
    text: 'OCR accuracy drops below 150 dpi. If you encounter poor results, upscale
      the image first using Pillow:'
  - name: 3. Extracting text from a scanned image with multiple languages
    text: 'Set a comma‑separated list of language codes:'
  - name: 4. Large documents
    text: 'Processing many pages in a single run can exhaust memory. Process each
      page individually:'
  type: HowTo
tags:
- python
- OCR
- image processing
title: 'دورة OCR بايثون: تحويل PNG إلى نص باستخدام Aspose'
url: /ar/python/general/python-ocr-tutorial-convert-png-to-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل OCR بلغة Python: تحويل PNG إلى نص باستخدام Aspose

إذا كنت بحاجة إلى **دليل OCR بلغة Python** يحول صورة PNG إلى نص قابل للتحرير، فإن هذا الدليل يقدم لك حلًا كاملاً جاهزًا للتنفيذ. ستتعرف على كيفية تثبيت مكتبة Aspose OCR، تحميل الصورة، تشغيل محرك التعرف، وطباعة النتائج—كل ذلك في بضع خطوات مختصرة.

مسح المستند واستخراج النص قد يبدو مرهقًا، خاصةً عندما تتعامل مع صيغ الصور وإعدادات اللغة. يزيل هذا الدليل التخمينات من خلال إظهار الطرق التي يجب استدعاؤها ولماذا هي مهمة، حتى تتمكن من التركيز على دمج OCR في تطبيقاتك الخاصة.

ستتعلم أيضًا **كيفية تحويل PNG إلى نص**، التعامل مع المشكلات الشائعة، وتكييف الكود لأنواع صور أخرى مثل JPEG أو TIFF. في النهاية، ستكون قادرًا على استخراج النص من أي صورة ممسوحة بثقة.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* Python 3.8 أو أحدث مثبت.
* اتصال بالإنترنت لتنزيل حزمة Aspose OCR.
* صورة PNG (أو أي صيغة مدعومة) تحتوي على نص قابل للقراءة.

أنت **لست بحاجة** إلى محرك OCR منفصل أو ملفات تنفيذية خارجية—Aspose OCR يضم كل ما تحتاجه.

## الخطوة 1: تثبيت حزمة Aspose OCR

الخطوة الأولى هي إضافة المكتبة إلى بيئتك. توفر Aspose حزمة Python صافية يمكن تثبيتها عبر pip.

```bash
pip install aspose-ocr
```

> **نصيحة احترافية:** استخدم بيئة افتراضية (`python -m venv venv`) لعزل الاعتمادات عن المشاريع الأخرى.

تثبيت الحزمة يجعل وحدة `aspose.ocr` متاحة، والتي تحتوي على الفئة `OcrEngine` المستخدمة طوال هذا الدليل.

## الخطوة 2: استيراد فئة محرك OCR

الآن بعد أن أصبحت الحزمة موجودة، استورد الفئة التي تدير عملية التعرف.

```python
# Step 2: Import the OCR engine class
from aspose.ocr import OcrEngine
```

`OcrEngine` تُغلف كل المنطق الخاص بتحميل الصور، ضبط اللغة، واستخراج النص. استيرادها في أعلى الملف يتماشى مع الممارسات القياسية في Python ويحافظ على تنظيم السكريبت.

## الخطوة 3: إنشاء نسخة من محرك OCR

إنشاء نسخة يمنحك محركًا جديدًا بإعدادات افتراضية. يمكنك لاحقًا تخصيص خصائص مثل اللغة أو ما قبل معالجة الصورة.

```python
# Step 3: Create an instance of the OCR engine
engine = OcrEngine()
```

كائن `engine` الجديد يمثل جلسة OCR واحدة. إعادة استخدام نفس النسخة لعدة صور يمكن أن يحسن الأداء لأن الموارد الداخلية تُخزن مؤقتًا.

## الخطوة 4: تحميل الصورة التي تريد معالجتها

حدد المسار إلى ملف PNG الذي تريد تحويله. طريقة `load_image` تقبل أي صيغة تدعمها Aspose OCR، لذا يمكنك أيضًا تمرير ملفات JPEG أو BMP أو TIFF.

```python
# Step 4: Load the image you want to process
engine.load_image("YOUR_DIRECTORY/sample.png")
```

إذا تعذر العثور على الملف، فإن `load_image` تُثير استثناء `FileNotFoundError`. احرص على وضع الاستدعاء داخل كتلة try/except في الكود الإنتاجي لتقديم رسالة خطأ ودية.

## الخطوة 5: تنفيذ OCR لاستخراج النص من الصورة

استدعاء `recognize` يُشغل خط أنابيب التعرف ويُعيد السلسلة المستخرجة. الطريقة تتعامل تلقائيًا مع تحليل التخطيط، تجزئة الأحرف، واكتشاف اللغة (اللغة الافتراضية هي الإنجليزية).

```python
# Step 5: Perform OCR to extract text from the image
text = engine.recognize()
```

يمكنك تغيير اللغة قبل استدعاء `recognize`:

```python
engine.language = "fr"   # for French text
```

هذه المرونة مفيدة عندما تحتاج إلى **استخراج نص OCR باستخدام Python** للوثائق متعددة اللغات.

## الخطوة 6: إخراج النص المعترف به

أخيرًا، اطبع أو احفظ النتيجة. للتحقق السريع، يعرض `print` السلسلة الخام في وحدة التحكم.

```python
# Step 6: Output the recognized text
print(text)
```

### النتيجة المتوقعة

إذا كان `sample.png` يحتوي على الجملة “Hello, world!”، فستظهر وحدة التحكم:

```
Hello, world!
```

قد يتضمن الإخراج فواصل أسطر أو مسافات إضافية حسب التخطيط الأصلي. يمكنك معالجة السلسلة لاحقًا باستخدام `str.strip()` أو تعبيرات نمطية لتنظيفها.

## معالجة الحالات الشائعة

### 1. صيغ غير PNG

على الرغم من تركيز هذا الدليل على **تحويل PNG إلى نص**، قد تستلم ملفات JPEG أو TIFF. الكود نفسه يعمل؛ فقط غيّر امتداد الملف في `load_image`.

```python
engine.load_image("scanned_page.tiff")
```

### 2. صور منخفضة الدقة

تنخفض دقة OCR تحت 150 dpi. إذا واجهت نتائج ضعيفة، قم بزيادة حجم الصورة أولاً باستخدام Pillow:

```python
from PIL import Image

img = Image.open("sample.png")
high_res = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
high_res.save("sample_high_res.png")
engine.load_image("sample_high_res.png")
```

### 3. استخراج نص من صورة ممسوحة بعدة لغات

حدد قائمة مفصولة بفواصل من رموز اللغات:

```python
engine.language = "en,es,de"
```

ستحاول Aspose OCR التعرف على الأحرف من جميع اللغات المذكورة.

### 4. مستندات كبيرة

معالجة العديد من الصفحات في تشغيل واحد قد تستنزف الذاكرة. عالج كل صفحة على حدة:

```python
for page_path in ["page1.png", "page2.png", "page3.png"]:
    engine.load_image(page_path)
    print(engine.recognize())
```

## سكريبت كامل قابل للتنفيذ

جمع كل خطوة معًا ينتج برنامجًا مستقلاً يمكنك نسخه، لصقه، وتشغيله.

```python
# python_ocr_tutorial.py
# Complete script for extracting text from a PNG image using Aspose OCR

# Install the library first:
# pip install aspose-ocr

from aspose.ocr import OcrEngine

def extract_text(image_path: str) -> str:
    """
    Loads an image and returns the recognized text.
    Parameters:
        image_path: Path to the PNG (or other supported) image.
    Returns:
        Recognized text as a string.
    """
    engine = OcrEngine()          # Create OCR engine instance
    engine.load_image(image_path) # Load the target image
    return engine.recognize()     # Perform OCR and return result

if __name__ == "__main__":
    # Replace with the actual path to your image
    path = "YOUR_DIRECTORY/sample.png"
    try:
        result = extract_text(path)
        print("=== Recognized Text ===")
        print(result)
    except Exception as e:
        print(f"Error during OCR processing: {e}")
```

شغّل السكريبت باستخدام:

```bash
python python_ocr_tutorial.py
```

يجب أن ترى النص المستخرج يُطبع في وحدة التحكم.

## الخلاصة

هذا **الدليل OCR بلغة Python** أوضح كيفية **تحويل PNG إلى نص** باستخدام Aspose OCR، متضمنًا التثبيت، تحميل الصورة، التعرف، ومعالجة الإخراج. الآن لديك نمط موثوق لـ **استخراج نص OCR باستخدام Python**، ويمكنك تكييف الكود لـ **استخراج نص من صورة باستخدام Python** لأي مستند ممسوح.

من هنا، يمكنك التفكير في:

* دمج السكريبت في خدمة ويب (مثل Flask) لتوفير OCR كواجهة API.
* تخزين النص المستخرج في قاعدة بيانات لأرشفة قابلة للبحث.
* تجربة إعدادات لغات مختلفة للتعامل مع مسوحات متعددة اللغات.

برمجة سعيدة، واستمتع بتحويل الصور إلى نص قابل للبحث والتحرير!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Python OCR Tutorial: Extract Table Text from Images](/ocr/english/python-java/general/python-ocr-tutorial-extract-table-text-from-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}