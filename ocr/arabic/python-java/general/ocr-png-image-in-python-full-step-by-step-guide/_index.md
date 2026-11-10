---
category: general
date: 2026-06-06
description: التعرف الضوئي على الأحرف (OCR) لصورة PNG باستخدام بايثون – تعلم كيفية
  استخراج النص من الصورة، تشغيل مثال OCR بايثون، وحتى قراءة النص اليوناني القديم بسهولة.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: ar
og_description: شرح OCR لصورة PNG في بايثون. يوضح هذا الدليل كيفية استخراج النص من
  الصورة، تشغيل مثال OCR بايثون، وقراءة اليونانية القديمة بسهولة.
og_title: التعرف الضوئي على الأحرف لصورة PNG في بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: التعرف الضوئي على الأحرف (OCR) لصورة PNG في بايثون – دليل كامل خطوة بخطوة
url: /ar/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# صورة PNG OCR في بايثون – دليل خطوة بخطوة كامل

هل تساءلت يومًا كيف يمكنك **OCR PNG image** مباشرةً من سكريبت بايثون؟ ربما لديك مجلد مليء بالمخطوطات القديمة الممسوحة وتحتاج إلى **extract text from image** دون كتابة كل شيء يدويًا. الخبر السار هو أنك لا تحتاج إلى دكتوراه في رؤية الحاسوب—فقط بضع أسطر من الكود والمكتبة المناسبة، وستتمكن من قراءة اليونانية القديمة في ثوانٍ.

في هذا الدرس سنستعرض **python OCR example** يتعرف على النص من ملف PNG، يضبط اللغة إلى اليونانية البوليتونية، ويطبع النتيجة. بنهاية الدرس ستعرف بالضبط كيف **recognize image text**، وكيفية التعامل مع المشكلات الشائعة، وكيفية تعديل السكريبت للغات أو صيغ صور أخرى.

## ما ستتعلمه

- تثبيت وتكوين مكتبة OCR لبايثون (pytesseract + Tesseract OCR)
- إنشاء نسخة من محرك OCR وتحميل ملف PNG
- ضبط لغة التعرف إلى اليونانية البوليتونية لتتمكن من **read ancient greek**
- إخراج النص المُتعرف عليه وحل المشكلات النموذجية
- توسيع السكريبت لمعالجة دفعات متعددة من PNGs أو تغيير اللغة

### المتطلبات المسبقة

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| Python 3.8+ | الصياغة الحديثة وتلميحات الأنواع |
| حزمة `pytesseract` | غلاف خفيف حول محرك Tesseract |
| ملفات ثنائية لـ Tesseract OCR (≥ 5.0) | المحرك الفعلي الذي يقوم بالمعالجة |
| بيانات اللغة اليونانية (`grc.traineddata`) | ضرورية لـ **read ancient greek** بشكل صحيح |
| صورة PNG تريد تحليلها (مثال: `ancient_greek.png`) | هدفنا لتجربة **ocr png image** |

يمكنك تثبيت الجانب الخاص ببايثون باستخدام:

```bash
pip install pytesseract Pillow
```

وعلى Ubuntu/macOS يمكنك إضافة المحرك نفسه:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

لا تنس تحميل بيانات التدريب للغة اليونانية البوليتونية:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(قد يختلف المسار؛ عدل `TESSDATA_PREFIX` إذا لزم الأمر.)*

---

## OCR PNG Image: إنشاء نسخة المحرك

أول شيء نحتاجه هو كائن يتواصل مع Tesseract. في `pytesseract` يتم الوصول إلى المحرك عبر دوال على مستوى الوحدة، لكن لتوضيح الفكرة سنغلفه داخل فئة صغيرة. هذا يعكس مفهوم “المحرك” الذي رأيته في المقتطف الأصلي.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**لماذا نغلفه؟**  
- يحافظ على واجهة برمجة التطبيقات العامة كما في المقتطف الأصلي، مما يجعل الانتقال سهلًا.  
- يتيح لنا إضافة سجلات أو معالجة أخطاء لاحقًا دون تعديل التدفق الرئيسي.  
- يوضح ممارسات OOP الجيدة—وهو ما يقدره المطورون ذوو الخبرة.

---

## استخراج النص من الصورة: ضبط اللغة إلى اليونانية البوليتونية

الآن بعد أن لدينا محركًا، نحتاج إلى إخبارها أي لغة نتوقعها. اليونانية البوليتونية تستخدم علامات تشكيل لا تغطيها بيانات “greek” القياسية، لذا نوجه Tesseract إلى ملف التدريب `grc`.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

إذا أردت **extract text from image** بلغة أخرى، ما عليك سوى استبدال `"grc"` بـ `"eng"` للإنجليزية، `"fra"` للفرنسية، إلخ. نفس السطر يعمل مع أي لغة تم تثبيتها.

---

## التعرف على نص الصورة: تشغيل OCR على PNG

بعد ضبط اللغة، نمرر ملف PNG إلى المحرك. المثال الأصلي استخدم مسارًا ثابتًا؛ سنجعل الأمر أكثر مرونة باستخدام كائنات `Path`.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**نصائح وحالات خاصة**

- **الملف غير موجود** – غلف الاستدعاء بـ `try/except FileNotFoundError` لتقديم رسالة ودية.  
- **PNG منخفض الدقة** – فكر في ما قبل المعالجة (مثل تغيير الحجم، التحويل إلى ثنائي) باستخدام Pillow قبل OCR.  
- **نص غير يوناني** – سيحاول Tesseract التعرف لكنه سيقلّ الدقة بشكل كبير. احرص دائمًا على مطابقة اللغة.

---

## إخراج النص المتعرف عليه

أخيرًا، نطبع النتيجة. في مشروع حقيقي قد تكتبها إلى قاعدة بيانات، ملف CSV، أو حتى تمررها إلى خط أنابيب ترجمة.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

عند تشغيل السكريبت على مسح واضح لنقش يوناني قديم، يجب أن ترى شيئًا مثل:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

إذا كان الإخراج مشوشًا، تحقق من أن ملف **greek.traineddata** موجود في المجلد الصحيح وأن PNG ليس صاخبًا جدًا.

---

## مثال كامل يعمل (كل الخطوات في سكريبت واحد)

فيما يلي البرنامج الكامل الجاهز للتنفيذ. احفظه باسم `ocr_greek.py` وشغّله باستخدام `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**الإخراج المتوقع** (مقتطع للوضوح):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

إذا رأيت الأحرف اليونانية الصحيحة، تهانينا—لقد نجحت في إجراء عملية **ocr png image** باستخدام بايثون!

---

## أسئلة شائعة ونصائح احترافية

### كيف أحسن الدقة على PNG صاخب؟

- حول الصورة إلى تدرج رمادي: `img = img.convert('L')`
- طبق عتبة ثنائية: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- قم بتكبير الصورة: `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

هذه الخطوات غالبًا ما تحول كابوس **recognize image text** إلى نتيجة نظيفة.

### هل يمكنني معالجة مجلد كامل من PNGs؟

بالتأكيد. غلف استدعاء `recognize_image` داخل حلقة `for` على `Path.glob("*.png")`. خزن كل نتيجة في قاموس أو اكتبها إلى CSV للتحليل لاحقًا.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### ماذا لو أردت استخراج الأرقام فقط؟

مرّر سلسلة **config** مخصصة إلى `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

بهذه الطريقة يمكنك **extract text from image** التي تحتوي على جداول أو أرقام تسلسلية أو طوابع زمنية.

### هل يمكن الحصول على درجات الثقة؟

نعم—استخدم `pytesseract.image_to_data` الذي يُرجع ملف TSV يحتوي على الثقة لكل كلمة. يمكنك تصفية الكلمات ذات الثقة المنخفضة قبل تجميع السلسلة النهائية.

---

## توسيع الدرس

الآن بعد أن أتقنت الأساسيات، فكر في استكشاف المواضيع ذات الصلة:

- **Batch OCR مع multiprocessing** – تسريع معالجة مجموعات كبيرة من PNGs.  
- **خطوط OCR + NLP هجينة** – ترجمة النص اليوناني القديم تلقائيًا إلى الإنجليزية الحديثة.  
- **محركات بديلة** – جرّب `easyocr` أو طرق تعتمد على `opencv` لحالات استخدام محددة.  
- **خدمات OCR سحابية** – Google Vision، Azure Computer Vision، أو AWS Textract للتوسع بدون خوادم.

كل هذه تبني على **python ocr example** الذي غطيناه، لذا ستشعر بالراحة في الغوص أعمق.

---

## الخلاصة

قمنا بأخذ مقتطف بسيط وتحويله إلى سير عمل **ocr png image** قوي في بايثون. بإنشاء `OcrEngine`، ضبط اللغة إلى اليونانية البوليتونية، تمرير PNG، وطباعة النتيجة، أصبحت الآن تعرف كيف **extract text from image**، **recognize image text**، وحتى **read ancient greek**.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}