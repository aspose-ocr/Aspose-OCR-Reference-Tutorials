---
category: general
date: 2026-02-09
description: استخراج النص من ملفات PDF باستخدام OCR عبر Aspose في بايثون. تعلم كيفية
  قراءة PDF باستخدام OCR، تحميل PDF للـ OCR وإتقان استخراج نص PDF بكفاءة.
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load pdf for ocr
- how to extract pdf text
language: ar
og_description: استخراج النص من ملف PDF باستخدام OCR عبر Aspose. يوضح هذا الدليل كيفية
  قراءة PDF باستخدام OCR، وتحميل PDF للـ OCR، والإجابة على كيفية استخراج نص PDF.
og_title: استخراج النص من PDF باستخدام OCR – دليل بايثون
tags:
- OCR
- Python
- PDF processing
title: استخراج النص من PDF باستخدام OCR – دليل بايثون الكامل
url: /ar/python/general/extract-text-from-pdf-with-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من PDF باستخدام OCR – دليل بايثون كامل

هل احتجت يومًا إلى **استخراج النص من PDF** لكن الملف مجرد صورة ممسوحة ضوئيًا؟ لست الوحيد الذي يواجه هذه المشكلة. في العديد من المشاريع الواقعية، ملفات PDF التي تتلقاها تكون صورة فقط، لذا فإن استدعاء “قراءة PDF” العادي لا يُعيد شيئًا. هنا يأتي دور OCR، واليوم سنُظهر لك بالضبط **كيفية استخراج نص PDF** باستخدام Aspose OCR للبايثون.

في هذا الدرس ستتعلم **قراءة PDF باستخدام OCR**، وسترى أفضل طريقة **لتحميل PDF لـ OCR**، وستتبع مثالًا كاملاً يُعيد كل كلمة مع درجة الثقة الخاصة بها. لا مراجع غامضة—فقط سكريبت قابل للتنفيذ، وتفسيرات لأهمية كل سطر، ونصائح يمكنك تطبيقها فورًا.

## ما يغطيه هذا الدليل

سنبدأ بتثبيت حزمة Aspose OCR، ثم إنشاء كائن `OcrEngine`، تحميل PDF، تشغيل التعرف الهيكلي، وأخيرًا استخراج كل كلمة مع درجة ثقتها. بنهاية الدليل ستتمكن من الإجابة على سؤال “**كيفية استخراج نص PDF**?” لأي مستند ممسوح، وستفهم الفروقات بين OCR الهيكلي والعادي.

المتطلبات قليلة: Python 3.8+، مكتبة Aspose OCR قابلة للتثبيت عبر pip، وملف PDF تريد معالجته. إذا كنت مرتاحًا مع الحلقات الأساسية في بايثون، فأنت جاهز للبدء.

لماذا هذا مهم؟ لأن درجات الثقة تتيح لك تصفية النتائج ذات الجودة المنخفضة تلقائيًا، والنص الهيكلي يمنحك تسلسل الصفحات، الكتل، الأسطر، والكلمات—مثالي للتحليلات اللاحقة أو فهارس البحث.

---

![استخراج النص من PDF باستخدام Aspose OCR](https://example.com/placeholder-image.jpg "استخراج النص من pdf")

*نص بديل للصورة: “استخراج النص من pdf باستخدام محرك Aspose OCR في بايثون”*

## الخطوة 1 – تثبيت واستيراد Aspose OCR

قبل تشغيل أي كود تحتاج إلى المكتبة. Aspose OCR تُوزَّع كحزمة wheel خالصة بايثون، لذا أمر `pip` واحد يكفي.

```bash
pip install aspose-ocr
```

الآن استورد الوحدة. قد يبدو سطر الاستيراد غريبًا (`aspose.ocr as aocr`) لكنه يحافظ على نظافة مساحة الاسم.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr
```

*لماذا هذا مهم:* استيراد `aspose.ocr` يمنحك الوصول إلى `OcrEngine`، الفئة الأساسية التي تتعامل مع كل شيء من تحميل الملفات إلى إرجاع النتائج الهيكلية.

## الخطوة 2 – إنشاء كائن محرك OCR

كائن `OcrEngine` يجمع الإعدادات مثل اللغة، وضع التعرف، وإعدادات الأداء. في معظم الحالات الإعدادات الافتراضية تعمل جيدًا، لكن يمكنك تعديلها لاحقًا.

```python
# Step 2: Create an OCR engine instance
ocr_engine = aocr.OcrEngine()
```

> **نصيحة احترافية:** إذا كنت تعلم أن PDF يحتوي على نص إنجليزي فقط، اضبط `ocr_engine.language = aocr.Language.English` لتسريع العملية.

## الخطوة 3 – تحميل PDF لـ OCR

الآن نـ **نحمّل PDF لـ OCR**. طريقة `load_image` تقبل صيغًا متعددة—PDF، JPG، PNG، TIFF—وبالتالي يمكنك إعادة استخدام نفس الكود لمصادر أخرى.

```python
# Step 3: Load the document you want to process
ocr_engine.load_image("YOUR_DIRECTORY/input.pdf")
```

*ما الذي يحدث خلف الكواليس؟* Aspose يحلل كل صفحة إلى صور نقطية، ثم يتعامل محرك OCR معها كصور عادية. لهذا يمكنك تمرير PDF متعدد الصفحات مباشرة؛ سيقوم المحرك بالتكرار داخليًا.

## الخطوة 4 – تنفيذ التعرف الهيكلي

التعرف الهيكلي يُعيد كائن `OcrResult` يحافظ على تسلسل التخطيط (صفحات → كتل → أسطر → كلمات). هذا أغنى بكثير من إخراج النص العادي.

```python
# Step 4: Perform structured recognition to obtain detailed results
ocr_result = ocr_engine.recognize_structured()   # returns an OcrResult object
```

إذا كنت تحتاج فقط إلى النص الخام، يمكنك استدعاء `ocr_engine.recognize()` بدلاً من ذلك، لكنك ستفقد درجات الثقة والبيانات الموضعية—معلومات غالبًا ما تكون حاسمة في خطوط التحقق.

## الخطوة 5 – استخراج الكلمات ودرجات الثقة

هذا هو جوهر **كيفية استخراج نص PDF** مع الحصول على قيم الثقة. الحلقات المتداخلة تتنقل عبر التسلسل الهرمي وتجمع أزواج `(word, confidence)`.

```python
# Step 5: Extract recognized words and their confidence scores
recognized_words = []
for page in ocr_result.structured_text.pages:
    for block in page.blocks:
        for line in block.lines:
            for word in line.words:
                recognized_words.append((word.text, word.confidence))
```

*لماذا نستخدم هذا النوع من الحلقات؟* كل مستوى (صفحة → كتلة → سطر → كلمة) يمنحك سياقًا. على سبيل المثال، يمكنك لاحقًا تجميع الكلمات لتكوين جمل أو تجاهل الكلمات من كتلة عنوان عادةً ما تكون ذات ثقة أقل.

### التعامل مع الحالات الخاصة

- **PDF فارغ:** إذا كان `ocr_result.structured_text.pages` فارغًا، يبقى `recognized_words` فارغًا—عالج ذلك بلطف.
- **ثقة منخفضة:** قد ترغب في تصفية الكلمات التي `confidence < 0.6`. مثال:

```python
high_confidence = [(t, c) for t, c in recognized_words if c >= 0.6]
```

## الخطوة 6 – عرض كلمة نموذجية مع درجة الثقة الخاصة بها

فحص سريع للتأكد هو طباعة الكلمة الأولى مع درجة ثقتها. هذا يؤكد أن المحرك قرأ شيئًا فعليًا.

```python
# Step 6: Show a sample word with its confidence
if recognized_words:
    sample_text, sample_conf = recognized_words[0]
    print(f"{sample_text} (conf: {sample_conf:.2f})")
```

المخرجات النموذجية تكون كالتالي:

```
Invoice (conf: 0.98)
```

إذا رأيت درجة ثقة أقل من 0.5، فكر في تعديل ما قبل معالجة الصورة (مثل تصحيح الميل) قبل تشغيل OCR.

## الخطوة 7 – تلخيص العدد الإجمالي للكلمات التي تم التعرف عليها

أخيرًا، قدم للمستخدم ملخصًا سريعًا. هذا مفيد للتسجيل أو لتغذية واجهة المستخدم.

```python
# Step 7: Summarize the total number of words recognized
print(f"Total words recognized: {len(recognized_words)}")
```

مثال على مخرجات وحدة التحكم:

```
Total words recognized: 1,342
```

## مثال كامل يعمل

بجمع كل ما سبق، إليك السكريبت الكامل الذي يمكنك نسخه ولصقه في ملف باسم `extract_ocr.py`. استبدل `"YOUR_DIRECTORY/input.pdf"` بالمسار إلى ملف PDF الخاص بك.

```python
# extract_ocr.py – Complete example to extract text from PDF with OCR

import aspose.ocr as aocr

def extract_words(pdf_path):
    # Initialize OCR engine
    ocr_engine = aocr.OcrEngine()
    
    # Load PDF (this is the step where we **load PDF for OCR**)
    ocr_engine.load_image(pdf_path)
    
    # Run structured recognition
    ocr_result = ocr_engine.recognize_structured()
    
    # Collect words + confidence
    words = []
    for page in ocr_result.structured_text.pages:
        for block in page.blocks:
            for line in block.lines:
                for word in line.words:
                    words.append((word.text, word.confidence))
    return words

if __name__ == "__main__":
    pdf_file = "YOUR_DIRECTORY/input.pdf"
    recognized = extract_words(pdf_file)
    
    # Show first word as a quick sanity check
    if recognized:
        txt, conf = recognized[0]
        print(f"{txt} (conf: {conf:.2f})")
    
    # Summary
    print(f"Total words recognized: {len(recognized)}")
```

تشغيل هذا السكريبت يطبع كلمة نموذجية مع ثقتها والعدد الكلي—بالضبط ما تحتاجه للتحقق من أن **قراءة PDF باستخدام OCR** نجحت كما هو متوقع.

## أسئلة شائعة ومشكلات محتملة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كان PDF محميًا بكلمة مرور؟* | استدعِ `ocr_engine.load_image("file.pdf", password="secret")`. سيقوم المحرك بفك التشفير قبل تحويله إلى صور نقطية. |
| *هل يمكنني معالجة عدة ملفات PDF دفعة واحدة؟* | بالتأكيد. ضع استدعاء `extract_words` داخل حلقة تمر على قائمة مسارات الملفات. |
| *هل أحتاج لتثبيت حزم لغات إضافية؟* | للـ PDF غير الإنجليزي، ثبّت حزمة اللغة المناسبة (`pip install aspose-ocr‑lang‑<lang>`). |
| *كيف أحسن درجات الثقة المنخفضة؟* | عالج صفحات PDF مسبقًا (زيادة DPI، تطبيق التثبيت الثنائي) قبل التحميل، أو فعّل `ocr_engine.image_preprocessing = True`. |

## الخطوات التالية – ما بعد الاستخراج الأساسي

الآن بعد أن عرفت **كيفية استخراج نص PDF** مع درجات الثقة، يمكنك استكشاف:

- **فهرسة** الكلمات في Elasticsearch للبحث النصي الكامل.
- **تصدير** التسلسل الهرمي الهيكلي إلى JSON للتحليلات اللاحقة.
- **دمج** Aspose OCR مع أدوات تحويل PDF إلى صورة لضبط إعدادات DPI بدقة.
- **دمج** العملية في نقطة نهاية Flask أو FastAPI لتقديم OCR كخدمة.

كل هذه الإضافات تبني على نفس الكود الأساسي الذي غطيناه للتو، لذا يمكنك التكرار بسرعة.

### الخلاصة

لقد استعرضنا حلًا كاملًا من البداية إلى النهاية يتيح لك **استخراج النص من PDF** باستخدام Aspose OCR في بايثون. من خلال تحميل PDF لـ OCR، تنفيذ التعرف الهيكلي، والتنقل عبر الصفحات والكتل والأسطر والكلمات، ستحصل ليس فقط على النص الخام بل أيضًا على درجة ثقة لكل كلمة—وذلك أمر حاسم للتحكم في الجودة.  

لا تتردد في تعديل السكريبت، إضافة ما قبل المعالجة، أو ربطه بسير عمل معالجة مستندات أكبر. إذا واجهت أي صعوبات، اترك تعليقًا أدناه؛ برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}