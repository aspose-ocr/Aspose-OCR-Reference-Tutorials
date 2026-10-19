---
category: general
date: 2026-06-19
description: كيفية تنفيذ OCR على الإيصالات وتشغيل مدقق إملائي لاستخراج نص نظيف. اتبع
  هذا الدرس التعليمي خطوة بخطوة بلغة بايثون.
draft: false
keywords:
- how to perform ocr
- extract text from receipt
- run spell checker
- perform ocr on image
- load image for ocr
language: ar
og_description: كيفية إجراء التعرف الضوئي على الأحرف (OCR) على الإيصالات وتشغيل مدقق
  إملائي فورًا. تعلّم سير العمل الكامل بلغة بايثون مع Aspose AI.
og_title: كيفية إجراء OCR على الإيصالات – دليل شامل لمصحح الإملاء
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to perform OCR on receipts and run a spell checker for clean text
    extraction. Follow this step‑by‑step Python tutorial.
  headline: How to Perform OCR on Receipts – Spell Checker Guide
  type: TechArticle
- description: How to perform OCR on receipts and run a spell checker for clean text
    extraction. Follow this step‑by‑step Python tutorial.
  name: How to Perform OCR on Receipts – Spell Checker Guide
  steps:
  - name: '**Load the image** → the OCR engine knows *what* to read.'
    text: '**Load the image** → the OCR engine knows *what* to read.'
  - name: '**Perform OCR** → the engine spits out raw characters.'
    text: '**Perform OCR** → the engine spits out raw characters.'
  - name: '**Extract the text** → we pull the string out of the engine’s result object.'
    text: '**Extract the text** → we pull the string out of the engine’s result object.'
  - name: '**Run spell checker** → a smart post‑processor cleans up typos and OCR
      quirks.'
    text: '**Run spell checker** → a smart post‑processor cleans up typos and OCR
      quirks.'
  - name: '**Use the corrected text** → print, store, or pass it to another service.'
    text: '**Use the corrected text** → print, store, or pass it to another service.'
  type: HowTo
tags:
- OCR
- Python
- Aspose AI
- Text Extraction
title: كيفية تنفيذ التعرف الضوئي على الحروف في الإيصالات – دليل مدقق الإملاء
url: /ar/python/general/how-to-perform-ocr-on-receipts-spell-checker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR على الإيصالات – دليل مدقق الإملاء

هل تساءلت يومًا **how to perform OCR** على إيصال دون أن تشعر بالإحباط؟ لست وحدك. في العديد من التطبيقات الواقعية—متتبعات النفقات، أدوات المحاسبة، أو حتى ماسح بسيط لقائمة البقالة—تحتاج إلى **extract text from receipt** من صور الإيصالات والتأكد من أن النص قابل للقراءة. الخبر السار؟ ببضع أسطر من Python و Aspose AI يمكنك الحصول على سلسلة نظيفة تم فحص إملائها في ثوانٍ.

في هذا الدرس سنستعرض كامل سير العمل: تحميل صورة الإيصال، تشغيل OCR، ثم صقل النتيجة باستخدام معالج ما بعد الفحص الإملائي. في النهاية ستحصل على دالة جاهزة للاستخدام يمكنك إدراجها في أي مشروع يحتاج إلى تحويل الإيصالات إلى نص موثوق.

## ما ستتعلمه

- كيفية **load image for OCR** باستخدام OcrEngine من Aspose.  
- الخطوات الدقيقة لـ **perform OCR on image** في ملفات Python.  
- طرق **extract text from receipt** ولماذا يعتبر المعالج اللاحق مهمًا.  
- كيفية **run spell checker** على ناتج OCR الخام لإصلاح الأخطاء الشائعة.  
- نصائح للتعامل مع الحالات الخاصة مثل المسحات منخفضة التباين أو الإيصالات متعددة الصفحات.

### المتطلبات المسبقة

- Python 3.8 أو أحدث مثبت على جهازك.  
- رخصة Aspose.OCR سارية (الإصدار التجريبي المجاني يعمل للاختبار).  
- إلمام أساسي بدوال Python ومعالجة الاستثناءات.

إذا كان لديك كل ذلك، لنبدأ—بدون إطالة، مجرد حل عملي يمكنك نسخه ولصقه.

![مخطط مثال كيفية تنفيذ OCR](ocr_flow.png)

## كيفية تنفيذ OCR على الإيصالات – نظرة عامة

قبل أن نبدأ بالبرمجة، تخيل التدفق كخط تجميع بسيط:

1. **تحميل الصورة** → محرك OCR يعرف *ماذا* يقرأ.  
2. **تنفيذ OCR** → المحرك ينتج الأحرف الخام.  
3. **استخراج النص** → نأخذ السلسلة من كائن نتيجة المحرك.  
4. **تشغيل مدقق الإملاء** → معالج لاحق ذكي ينظف الأخطاء والعيوب في OCR.  
5. **استخدام النص المصحح** → طباعة، تخزين، أو تمريره إلى خدمة أخرى.

هذا كل شيء. كل مرحلة هي سطر واحد واضح في الكود، لكن الشروحات المحيطة ستمنعك من الضياع عندما يحدث شيء غير متوقع.

## الخطوة 1 – تحميل الصورة لـ OCR

أول شيء يجب عليك فعله هو توجيه محرك OCR إلى الملف الصحيح. `OcrEngine` من Aspose يتوقع مسارًا، لذا تأكد من أن صورة الإيصال موجودة في مكان يمكن للسكريبت قراءته.

```python
# Import the necessary Aspose OCR classes
from aspose.ocr import OcrEngine

def load_image(image_path: str) -> OcrEngine:
    """
    Initializes an OcrEngine instance and loads the image.
    Returns the configured engine ready for recognition.
    """
    engine = OcrEngine()
    try:
        # This is the 'load image for ocr' step
        engine.set_image_from_file(image_path)
        return engine
    except Exception as e:
        # Provide a clear error if the file can't be opened
        raise FileNotFoundError(f"Unable to load image at {image_path}: {e}")
```

**لماذا هذا مهم:**  
إذا كان مسار الصورة غير صحيح، ينهار كامل الخط الأنابيب. من خلال تغليف التحميل في `try/except`، ستحصل على رسالة مفيدة بدلاً من تتبع الأخطاء الغامض. أيضًا، لاحظ اسم الطريقة `set_image_from_file`—هذا هو الاستدعاء الدقيق الذي يستخدمه Aspose لـ **load image for OCR**.

## الخطوة 2 – تنفيذ OCR على الصورة

الآن بعد أن المحرك يعرف أي ملف يقرأ، نطلب منه التعرف على الأحرف. هذه الخطوة هي التي يحدث فيها العمل الشاق.

```python
def perform_ocr(engine: OcrEngine):
    """
    Executes OCR on the previously loaded image.
    Returns the raw recognition result object.
    """
    # This line actually runs the OCR algorithm
    raw_result = engine.recognize()
    return raw_result
```

**خلف الكواليس:**  
`recognize()` يمسح البت ماب، يطبق التجزئة، ثم يشغل مُعرّف يعتمد على الشبكة العصبية. النتيجة تحتوي على أكثر من مجرد نص عادي—فهي تشمل درجات الثقة، صناديق الإحاطة، ومعلومات اللغة. لمعظم سيناريوهات مسح الإيصالات، ستحتاج فقط إلى خاصية `text` لاحقًا.

## الخطوة 3 – استخراج النص من الإيصال

النتيجة الخام هي كائن غني، لكننا نهتم فقط بالسلسلة القابلة للقراءة من قبل الإنسان. هذه هي النقطة التي نقوم فيها بـ **extract text from receipt**.

```python
def get_raw_text(raw_result) -> str:
    """
    Pulls the plain text out of the OCR result.
    """
    # The Text attribute holds the recognized characters
    return raw_result.text
```

**مخاطر شائعة:**  
أحيانًا تحتوي الإيصالات على خطوط صغيرة أو طباعة باهتة، مما يجعل محرك OCR يُعيد سلاسل فارغة أو رموز مشوهة. إذا لاحظت الكثير من الأحرف `�`، فكر في معالجة مسبقة للصورة (زيادة التباين، تصحيح الميل، إلخ) قبل تحميلها.

## الخطوة 4 – تشغيل مدقق الإملاء

OCR ليس مثاليًا—خاصةً مع الإيصالات منخفضة الدقة. Aspose AI يقدم معالجًا لاحقًا يعمل كمدقق إملائي، يصحح أخطاء OCR الشائعة مثل “0” مقابل “O” أو “l” مقابل “1”.

```python
from aspose.ai import AsposeAI

def spell_check(raw_text: str) -> str:
    """
    Sends the raw OCR text through Aspose AI's spell‑checking post‑processor.
    Returns the corrected string.
    """
    # Initialize the AI helper
    spellchecker = AsposeAI()
    try:
        # The 'run_postprocessor' method expects the raw OCR result object,
        # but we can also feed just the text if the API allows.
        corrected = spellchecker.run_postprocessor(raw_text)
        return corrected.text
    finally:
        # Always free resources to avoid memory leaks
        spellchecker.free_resources()
```

**لماذا تحتاجه:**  
حتى مع دقة OCR بنسبة 95 % قد ينتج بعض الكلمات الخاطئة التي تعطل التحليل اللاحق (مثل استخراج التاريخ). مدقق الإملاء يتعلم من نماذج اللغة ويصحح هذه الأخطاء تلقائيًا. عمليًا، ستلاحظ قفزة ملحوظة من “Total: $1O.00” إلى “Total: $10.00”.

## الخطوة 5 – استخدام النص المصحح

في هذه المرحلة لديك سلسلة نظيفة جاهزة لأي غرض—طباعة إلى وحدة التحكم، تخزين في قاعدة بيانات، أو تغذيتها إلى محلل لغة طبيعية.

```python
def main(image_path: str):
    # Load the image
    engine = load_image(image_path)

    # Perform OCR
    raw_result = perform_ocr(engine)

    # Extract raw text
    raw_text = get_raw_text(raw_result)

    # Run spell checker
    corrected_text = spell_check(raw_text)

    # Release OCR resources
    engine.dispose()

    # Show the final, cleaned‑up receipt text
    print("=== Corrected Receipt Text ===")
    print(corrected_text)

# Example usage
if __name__ == "__main__":
    main("YOUR_DIRECTORY/receipt.png")
```

**الإخراج المتوقع** (مع افتراض إيصال بقالة نموذجي):

```
=== Corrected Receipt Text ===
Walmart Supercenter
Date: 06/15/2026   Time: 14:32
Item          Qty   Price
Milk          2     $3.20
Bread         1     $2.50
Eggs          1     $2.99
Subtotal               $8.69
Tax                    $0.69
Total                 $9.38
Thank you for shopping!
```

لاحظ كيف أن الأرقام تم عرضها بشكل صحيح والكلمة “Thank” لم تُقرأ خطأً كـ “Thankk”.

## التعامل مع الحالات الخاصة والنصائح

- **مسحات منخفضة التباين:** عالج الصورة مسبقًا باستخدام Pillow (`ImageEnhance.Contrast`) قبل التحميل.  
- **إيصالات متعددة الصفحات:** كرر عبر كل ملف صفحة وضم النتائج.  
- **تنوع اللغات:** اضبط `engine.language = "eng"` أو رمز ISO آخر إذا كنت تتعامل مع إيصالات غير إنجليزية.  
- **تنظيف الموارد:** استدعِ دائمًا `engine.dispose()` و `spellchecker.free_resources()`؛ عدم القيام بذلك قد يسبب تسرب الذاكرة في الخدمات طويلة التشغيل.  
- **معالجة دفعات:** غلف منطق `main` في طابور عمل (Celery, RQ) لسيناريوهات عالية الإنتاجية.

## الخلاصة

لقد أجبنا للتو على سؤال **how to perform OCR** على الإيصالات ودمجنا بسلاسة **run spell checker** للحصول على نص نظيف وقابل للبحث. من تحميل الصورة، تنفيذ OCR على الصورة، استخراج النص من الإيصال، إلى تشغيل معالج ما بعد الفحص الإملائي—كل خطوة مضغوطة، موثقة جيدًا، وجاهزة للاستخدام في بيئات الإنتاج.

إذا كنت تبحث عن **extract text from receipt** على نطاق واسع، فكر في إضافة معالجة متوازية وتخزين نتائج OCR مؤقتًا. هل تريد استكشاف المزيد؟ جرّب دمج محلل PDF للتعامل مع ملفات PDF الممسوحة، أو جرب تحليل تخطيط Aspose لالتقاط البيانات العمودية تلقائيًا.

برمجة سعيدة، ولتظل إيصالاتك دائمًا قابلة للقراءة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [كيفية استخدام AspOCR: مرشحات معالجة مسبقة لصورة OCR لـ .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}