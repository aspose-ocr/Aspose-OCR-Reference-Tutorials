---
category: general
date: 2026-06-06
description: استخراج النص من ملفات PDF التي تحتوي على صور باستخدام OCR في بايثون.
  تعلم كيفية تحويل المستندات الممسوحة ضوئياً إلى نص بسرعة باستخدام التعرف غير المتزامن
  على دفعات.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: ar
og_description: استخراج النص من صور PDF باستخدام بايثون. يوضح هذا الدليل خطوة بخطوة
  كيفية تحويل المستندات الممسوحة ضوئياً إلى نص باستخدام OCR غير المتزامن.
og_title: استخراج النص من صور PDF – دليل Python OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: استخراج النص من ملفات PDF الصور – دليل بايثون لتحويل المستندات الممسوحة ضوئياً
  إلى نص
url: /ar/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من ملفات PDF التي تحتوي على صور – دليل بايثون لتحويل المستندات الممسوحة ضوئياً إلى نص

هل احتجت يوماً إلى **استخراج النص من ملفات PDF التي تحتوي على صور** دون قضاء ساعات في إعادة الكتابة؟ في هذا الدليل سنوضح لك كيفية **تحويل المستندات الممسوحة ضوئياً إلى نص** باستخدام سير عمل OCR غير متزامن بسيط في بايثون.  

إذا كنت قد حدقت في مجموعة من ملفات PDF الممسوحة وتفكرت، “يجب أن يكون هناك طريقة أسرع”، فأنت في المكان الصحيح. سنستعرض كل سطر من الشيفرة، نشرح لماذا كل جزء مهم، وحتى نتناول بعض الحالات الخاصة التي قد تواجهها.

## ما ستتعلمه

- كيفية تشغيل محرك OCR وتحديد لغة التعرف.  
- آلية تمرير قائمة مختلطة من PNGs و PDFs إلى مُعَرِّف دفعي.  
- تشغيل مهمة OCR بشكل غير متزامن بحيث يبقى تطبيقك مستجيباً.  
- سحب النتائج، ربطها بالملفات المصدر، وطباعة مخرجات نظيفة.  

**المتطلبات المسبقة**: بايثون 3.8+، فهم أساسي لـ `asyncio` أو `concurrent.futures`، ومكتبة OCR توفر فئة `OcrEngine` مشابهة للمثال (مثل Aspose.OCR، أو غلاف Tesseract، أو غلاف مخصص). لا حاجة لإعدادات معقدة—فقط قم بتثبيت المكتبة وستكون جاهزاً.

![استخراج النص من ملفات PDF التي تحتوي على صور](https://example.com/placeholder.png "لقطة شاشة لمخرجات OCR – استخراج النص من ملفات PDF التي تحتوي على صور")

## استخراج النص من ملفات PDF التي تحتوي على صور – إعداد محرك OCR

أول شيء تحتاجه هو نسخة من محرك OCR مُكوَّنة للغة مستنداتك. في مثالنا سنستخدم اللغة الفرنسية، لكن يمكنك استبدالها بأي لغة مدعومة.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**لماذا هذا مهم**: ضبط اللغة مسبقاً يحسّن الدقة بشكل كبير. يستخدم المحرك قواميس ونماذج حروف مخصَّصة للغة؛ تمريره بلغة خاطئة هو سبب شائع للمخرجات المشوَّهة.

## إعداد قائمة الملفات – الصور وPDF معاً

يمكن لمُعَرِّف الدفعات التعامل مع كل من الصور النقطية (`.png`, `.jpg`) وحاويات PDF. ما عليك سوى تمرير قائمة بايثون عادية من مسارات الملفات.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**نصيحة**: احرص على أن تكون القائمة مسطحة؛ سيقوم المحرك داخلياً بفك كل صفحة PDF إلى صور قبل التعرف. إذا كان لديك آلاف الملفات، فكر في تقسيم القائمة إلى دفعات أصغر لتجنب ارتفاع استهلاك الذاكرة.

## بدء التعرف الدفعي غير المتزامن

بدلاً من حجز الخيط الرئيسي، نطلق مهمة OCR في الخلفية. تُعيد الطريقة كائن `Future` سيحمل في النهاية قائمة من كائنات `OcrResult`.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**كيف يعمل**: تحت الغطاء، يُنشئ المحرك مجموعة من الخيوط (أو مهمة غير متزامنة، حسب التنفيذ). هذا يتيح لك متابعة أعمال أخرى—مثل تحديث واجهة المستخدم، جلب ملفات إضافية، أو تسجيل التقدم—بينما يتم تنفيذ الجزء الثقيل في مكان آخر.

## القيام بشيء مفيد أثناء تشغيل OCR

خطأ شائع هو الجلوس بلا فعل واستطلاع الـ `Future` في حلقة ضيقة. بدلاً من ذلك، يمكنك تنفيذ أي عمل غير مرتبط. للعرض، سنطبع سطر حالة بسيط.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## جمع النتائج بمجرد اكتمال الـ Future

عندما تكون جاهزاً لجمع مخرجات OCR، استخدم `as_completed` من `concurrent.futures`. هذا النمط يعمل سواء كان لديك `Future` واحد أو عدة.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**ما ستراه**: مسار كل ملف يليه تمثيل النص المستخرج. بالنسبة لملفات PDF، يحتوي `result.text` على النص المدمج لجميع الصفحات.

### النتيجة المتوقعة (مثال)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

إذا لاحظت فقدان أحرف، تحقق من أن اللغة التي ضبطتها تتطابق مع لغة المستند، وفكّر في معالجة الصور مسبقاً (تصحيح الميل، زيادة التباين) قبل تمريرها إلى المحرك.

## التعامل مع الحالات الخاصة والمشكلات الشائعة

| الحالة | ما يجب فعله |
|-----------|------------|
| **لغات مختلطة** | أجرِ تمريرة لاكتشاف اللغة أولاً، ثم أنشئ محركات منفصلة لكل لغة. |
| **ملفات PDF ضخمة (> 100 ميغابايت)** | قسّم الـ PDF إلى صفحات منفردة على القرص (مثلاً باستخدام `PyPDF2`) ومرّرها كمدخلات منفصلة. |
| **أنظمة كتابة غير لاتينية** | تأكّد من أن مكتبة OCR تتضمن حزمة اللغة المطلوبة؛ بعض المكتبات تحتاج إلى تنزيل ملفات بيانات إضافية. |
| **عنق زجاجة في الأداء** | زد حجم مجموعة الخيوط (`engine.set_thread_pool_size(8)`) أو انتقل إلى خلفية مدعومة بالـ GPU إذا كانت متاحة. |
| **نص مفقود في صور منخفضة الدقة** | عالج الصور باستخدام OpenCV: `cv2.resize`, `cv2.threshold`, و `cv2.medianBlur` لتحسين القابلية للقراءة. |

## مثال كامل يعمل (جاهز للنسخ واللصق)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

احفظه باسم `extract_text_async.py`، استبدل `YOUR_DIRECTORY` بمسار ملفاتك، ثبّت حزمة OCR (`pip install your-ocr-lib`)، ثم شغّل `python extract_text_async.py`. يجب أن ترى مخرجات الكونسول كما هو موضح أعلاه.

## الخطوات التالية – ما بعد الاستخراج الأساسي

- **ما بعد المعالجة**: إزالة الفراغات الزائدة، توحيد Unicode (`unicodedata.normalize`)، أو تشغيل مدقق إملائي لتنظيف ضوضاء OCR.  
- **مخرجات منظمة**: تصدير النتائج إلى CSV أو JSON أو مباشرة إلى قاعدة بيانات للبحث اللاحق.  
- **دفعات متوازية**: إذا كان لديك مئات الملفات، أنشئ عدة `Future` واستخدم طابوراً لإبقاء المعالج مشغولاً دون إغراق الذاكرة.  
- **التكامل مع أطر الويب**: اربط هذا السكربت بنقطة نهاية Flask أو FastAPI لتوفير OCR حسب الطلب كخدمة.

---

### TL;DR

أنت الآن تعرف كيف **استخراج النص من ملفات PDF التي تحتوي على صور** باستخدام سكربت بايثون بسيط يعمل OCR بشكل غير متزامن، مما يتيح لك **تحويل المستندات الممسوحة ضوئياً إلى نص** بينما يظل برنامجك مستجيباً. جرّب ضبط إعدادات اللغة، حجم الدفعات، وتقنيات ما قبل المعالجة للحصول على أقصى دقة ممكنة.

هل لديك طريقة مبتكرة تريد مشاركتها—مثل OCR للملاحظات المكتوبة يدوياً أو خدمة سحابية؟ اترك تعليقاً، ونتمنى لك برمجة سعيدة!

## ما الذي ينبغي أن تتعلمه لاحقاً؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [استخراج النص من الصور باستخدام عملية OCR على المجلدات](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [استخراج النص من الصور باستخدام Aspose.OCR – الأحرف المسموح بها](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}