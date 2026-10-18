---
category: general
date: 2026-03-18
description: قم بإصلاح أخطاء OCR في بايثون بسرعة. تعلّم كيفية تنظيف OCR، وكيفية تنظيف
  نص OCR، واستبدال الصفر بـ O، وتطبيق معالجة ما بعد OCR باستخدام بايثون.
draft: false
keywords:
- fix OCR errors
- how to clean OCR
- clean OCR text python
- replace zero with O
- python OCR post processing
language: ar
og_description: إصلاح أخطاء OCR في بايثون بسرعة. تعلم كيفية تنظيف OCR، استبدال الصفر
  بـ O، واستخدام معالجة ما بعد OCR في بايثون في درس واحد.
og_title: إصلاح أخطاء OCR في بايثون – دليل تنظيف نص OCR
tags:
- OCR
- Python
- Text Cleaning
title: إصلاح أخطاء OCR في بايثون – دليل تنظيف نص OCR
url: /ar/python/general/fix-ocr-errors-in-python-clean-ocr-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إصلاح أخطاء OCR في بايثون – دليل تنظيف نص OCR

هل سبق لك أن نظرت إلى فاتورة ممسوحة ضوئياً وفكرت، *“كيف أصلح أخطاء OCR قبل أن أدخلها إلى قاعدة البيانات الخاصة بي؟”* لست وحدك. في عالم أتمتة المستندات، حرف واحد غير مقروء يمكن أن يعرقل كامل الخط الإنتاجي، لذا فإن تعلم **كيفية تنظيف مخرجات OCR** أمر أساسي.  

في هذا الدرس ستشاهد طريقة عملية من البداية إلى النهاية **لإصلاح أخطاء OCR** باستخدام معالج بسيط يستبدل الرقم “0” بالحرف “O”—خطأ شائع في رموز المنتجات. في النهاية، ستتمكن من دمج الحل في أي سير عمل OCR ببايثون والاستمتاع بنص أنظف وأكثر موثوقية.

> **ما ستحصل عليه:** سكريبت بايثون كامل وقابل للتنفيذ، شرح لماذا كل سطر مهم، نصائح لتوسيع المنطق، وفحص سريع للنتيجة المتوقعة.

## المتطلبات المسبقة — ما تحتاجه قبل البدء

- بايثون 3.8 أو أحدث (الصياغة تعمل على جميع الإصدارات الحديثة).  
- مكتبة OCR أساسية (مثل Tesseract عبر `pytesseract`) تُعيد سلاسل نصية خام.  
- إلمام بسيط بالدوال والكائنات في بايثون.  

إذا كان لديك بالفعل خطوة OCR تُعيد سلسلة نصية، فأنت جاهز—لا تحتاج إلى تثبيت إضافي لجزء ما بعد المعالجة.

## الخطوة 1: إعداد غلاف بسيط شبيه بالذكاء الاصطناعي (لماذا نحتاجه)

في كثير من المشاريع، يعمل محرك OCR داخل فئة “AI” أكبر تتعامل مع ما قبل المعالجة، الاستدلال، وما بعد المعالجة. لجعل المثال مستقلاً سننشئ فئة صغيرة `AIProcessor` تحاكي هذا النمط. هذا يجعل من السهل إدخال الكود في قاعدة موجودة دون إعادة كتابة أي شيء.

```python
# ai_wrapper.py
class AIProcessor:
    """
    Simple wrapper that stores a post‑processing callable.
    In real projects this could be a full‑fledged model class.
    """
    def __init__(self):
        self._post_processor = None

    def set_post_processor(self, func):
        """Register a function that will clean OCR output."""
        if not callable(func):
            raise TypeError("Post‑processor must be callable")
        self._post_processor = func

    def run_postprocessor(self, text):
        """Apply the registered post‑processor to raw OCR text."""
        if self._post_processor is None:
            raise RuntimeError("No post‑processor has been set")
        return self._post_processor(text)
```

**لماذا هذا مهم:** إبقاء معالج ما بعد المعالجة منفصلًا عن محرك OCR يحترم مبدأ المسؤولية الواحدة ويسمح لك بتبديل منطق التنظيف دون لمس كود OCR.

## الخطوة 2: كتابة الدالة التي **تُصلح أخطاء OCR**

الآن نُنشئ جوهر الدرس: دالة **تُصلح أخطاء OCR** عن طريق استبدال الرقم “0” بالحرف “O”. هذا النمط يغطي رموز المنتجات، الأرقام التسلسلية، وأي معرف أبجدي رقمي حيث يخلط محرك OCR بين الحرفين كثيرًا.

```python
# post_processors.py
def correct_ocr_errors(text: str) -> str:
    """
    Replace common OCR mis‑reads.
    Example: change digit "0" to letter "O" in product codes.
    """
    # You could add more rules here, e.g.:
    # text = text.replace('1', 'I')
    # text = text.replace('5', 'S')
    return text.replace("0", "O")
```

**لماذا نستبدل 0 بـ O:** في العديد من الخطوط يبدو الصفر والحرف الكبير O متطابقين، لذا غالبًا ما يخطئ OCR. بتصحيح ذلك مبكرًا، تعمل عمليات التحقق اللاحقة (مثل تعبيرات regex) كما هو متوقع.

## الخطوة 3: ربط معالج ما بعد المعالجة مع كائن AI

بعد أن أصبح الغلاف ودالة التنظيف جاهزين، نربطهما معًا. هذا يعكس كيفية تسجيل معالج ما بعد معالجة مخصص في خط إنتاج حقيقي.

```python
# main.py
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Create the AI‑like object
ai = AIProcessor()

# Register our OCR‑fixing function
ai.set_post_processor(correct_ocr_errors)
```

إذا احتجت يومًا **كيفية تنظيف OCR** لمخرجات بلغة أو تنسيق بيانات مختلف، فقط اكتب دالة أخرى واستدعِ `set_post_processor` مرة أخرى—دون الحاجة لتعديل باقي الخط.

## الخطوة 4: إدخال نص OCR الخام والحصول على النتيجة المنقحة

لنحاكي سلسلة OCR خام تحتوي على “0” المزعجة في رمز المنتج. في سيناريو حقيقي ستستبدل العنصر النائب بـ `pytesseract.image_to_string(image)` أو استدعاء مشابه.

```python
# Simulated OCR output (replace with your own OCR call)
raw_text = "Product code: 10A0B"

# Run the post‑processor to obtain cleaned text
cleaned_text = ai.run_postprocessor(raw_text)

print("Before cleaning :", raw_text)
print("After cleaning  :", cleaned_text)
```

**الناتج المتوقع**

```
Before cleaning : Product code: 10A0B
After cleaning  : Product code: 1OAOB
```

لاحظ كيف تحولت الأصفار إلى حرف O كبير، مما يمنحنا سلسلة تتطابق مع الصيغة المتوقعة لمعظم أنظمة المخزون.

## الخطوة 5: توسيع المنطق – تنوعات واقعية

الاستبدال البسيط أعلاه يحل حالة ضيقة، لكن في الإنتاج ستواجه شذوذات أخرى:

| الخطأ الشائع | مثال OCR | التصحيح المطلوب | كيفية الإضافة |
|--------------|----------|----------------|----------------|
| قراءة “1” كـ “I” | `I23` | `123` | `text = text.replace('I', '1')` |
| قراءة “5” كـ “S” | `S9` | `59` | `text = text.replace('S', '5')` |
| مسافات زائدة | `  ABC  ` | `ABC` | `text = text.strip()` |
| ارتباك الأحرف المختلطة | `oRder` | `Order` | `text = text.title()` |

يمكنك توسيع `correct_ocr_errors` بأي من هذه القواعد. احرص على أن تكون كل تحويلة **متجانسة** (تشغيلها مرتين لا يغيّر النتيجة) لتجنب فساد البيانات غير المقصود.

```python
def correct_ocr_errors(text: str) -> str:
    text = text.replace("0", "O")
    text = text.replace("I", "1")
    text = text.replace("S", "5")
    return text.strip()
```

**نصيحة احترافية:** إذا كان لديك كتالوج معروف للرموز الصالحة، فكر في التحقق من السلسلة المنقحة باستخدام regex أو جدول بحث. هذه الخطوة الإضافية تلتقط أي أخطاء OCR متبقية لا تغطيها الاستبدالات البسيطة.

## الخطوة 6: دمج مع محرك OCR فعلي (اختياري)

فيما يلي توضيح سريع لكيفية ربط معالج ما بعد المعالجة بتدفق OCR حقيقي باستخدام `pytesseract`. هذا الجزء اختياري لكنه يُظهر الخط الكامل من البداية إلى النهاية.

```python
import pytesseract
from PIL import Image
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Initialize AI wrapper and register the cleaner
ai = AIProcessor()
ai.set_post_processor(correct_ocr_errors)

# Load an image containing a product label
image = Image.open("sample_label.png")

# Perform OCR (this returns raw text)
raw_ocr = pytesseract.image_to_string(image)

# Clean the OCR output
cleaned = ai.run_postprocessor(raw_ocr)

print("Raw OCR   :", raw_ocr)
print("Cleaned   :", cleaned)
```

> **ملاحظة:** `pytesseract` يتطلب تثبيت Tesseract OCR على نظامك. المقتطف أعلاه يعمل على Windows و macOS و Linux طالما أن الملف التنفيذي موجود في PATH.

## الخطوة 7: التحقق من النتائج برمجيًا

عند أتمتة دفعات كبيرة، من المفيد التأكد أن خطوة التنظيف تعمل كما هو متوقع. اختبار وحدة بسيط يمكن أن يوفر ساعات من التصحيح لاحقًا.

```python
def test_correct_ocr_errors():
    assert correct_ocr_errors("0O0") == "OOO"
    assert correct_ocr_errors(" 10A0B ") == "1OAOB"
    print("All tests passed!")

test_correct_ocr_errors()
```

تشغيل هذا الاختبار يؤكد أن الدالة **تُصلح أخطاء OCR** باستمرار، حتى عندما تتسلل مسافات إضافية.

## توضيح بصري

فيما يلي مخطط بصري للخط (الكلمة المفتاحية الأساسية تظهر في نص alt لأغراض SEO).

![مخطط تدفق إصلاح أخطاء OCR – يُظهر OCR الخام يُغذى إلى معالج ما بعد المعالجة الذي يستبدل الصفر بـ O]()

## الخلاصة – ما أنجزناه

لقد استعرضنا مثالًا كاملاً وقابلًا للتنفيذ يُظهر **كيفية تنظيف مخرجات OCR** في بايثون، وتحديدًا **استبدال الصفر بـ O** و**إصلاح أخطاء OCR** باستخدام معالج ما بعد معالجة معياري. بفصل منطق التنظيف عن محرك OCR، تحصل على مرونة، قابلية اختبار، ومكان واضح لإضافة قواعد مستقبلية مثل *كيفية تنظيف OCR* لأخطاء أحرف أخرى.

هل أنت مستعد للخطوة التالية؟ جرّب إضافة مُتحقق regex لرموز المنتجات، جرب التطابق الضبابي للنصوص المشوشة، أو استكشف مكتبة متكاملة مثل `ocrmypdf` التي تتضمن بالفعل وصلات ما بعد المعالجة. النمط الذي غطيناه يتوسع بسهولة، سواء كنت تتعامل مع عدد قليل من الفواتير أو ملايين المستندات الممسوحة.

---

*برمجة سعيدة، ولتظل خطوط OCR خالية من الأخطاء!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}