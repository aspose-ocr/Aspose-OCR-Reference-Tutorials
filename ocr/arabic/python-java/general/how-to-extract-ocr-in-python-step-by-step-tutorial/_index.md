---
category: general
date: 2026-04-26
description: كيفية استخراج OCR من الصور باستخدام بايثون – مثال على OCR في بايثون يوضح
  كيفية تحميل الصورة لاستخدام OCR واستخراج النص من الفاتورة.
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: ar
og_description: كيفية استخراج OCR من الصور باستخدام بايثون. تعلّم مثال OCR بايثون،
  حمّل صورة للـ OCR، واستخراج النص من الفاتورة في دقائق.
og_title: كيفية استخراج OCR في بايثون – دليل كامل
tags:
- OCR
- Python
- Image Processing
title: كيفية استخراج OCR في بايثون – دليل خطوة بخطوة
url: /ar/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج OCR في بايثون – دليل كامل

هل تساءلت يومًا **كيفية استخراج OCR** من إيصال غير واضح أو فاتورة ممسوحة ضوئيًا؟ لست وحدك — المطورون يواجهون صعوبة مستمرة عندما يحتاجون إلى نص نظيف وقابل للقراءة آليًا من الصور. الخبر السار؟ ببضع أسطر فقط من بايثون يمكنك تحويل صورة إيصال إلى نص عالي الثقة وقابل للبحث.

في هذا الدرس سنستعرض **مثال python ocr** يوضح **كيفية تحميل صورة للـ OCR**، تشغيل المحرك، والاحتفاظ فقط بالحروف التي تتجاوز عتبة الثقة بنسبة 85 ٪. في النهاية ستكون قادرًا على **استخراج النص من إيصالات** دون الحاجة للبحث في الوثائق أو تخمين معلمات الـ API.

## ما ستحتاجه

- Python 3.9 أو أحدث (الصياغة التي نستخدمها تعمل على 3.8+)
- حزمة `aocr` (أو أي مكتبة OCR توفر فئة `OcrEngine`). قم بتثبيتها باستخدام:

```bash
pip install aocr
```

- صورة إيصال نموذجية (`receipt.png`) موجودة في مجلد يمكنك الإشارة إليه.
- محرر نصوص أو بيئة تطوير متكاملة — VS Code، PyCharm، أو حتى دفتر ملاحظات بسيط يكفي.

هذا كل شيء. لا أطر عمل ثقيلة، لا خدمات خارجية، فقط بايثون نقي.

![نتيجة OCR عالية الثقة – كيفية استخراج OCR من إيصال](/images/ocr-high-confidence.png)

*نص بديل للصورة: كيفية استخراج OCR من إيصال باستخدام Python OCR*

## الخطوة 1 – إنشاء مثيل محرك OCR (كيفية استخراج OCR)

أول شيء نقوم به هو تشغيل محرك OCR. فكر فيه كالعقل الذي سيقرأ البكسلات لنا.

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**لماذا؟** إنشاء كائن `OcrEngine` يمنحك كائن إعدادات جديد. يمكنك لاحقًا تعديل نماذج اللغة، إعدادات DPI، أو خطوات ما قبل المعالجة — كل ذلك دون لمس حلقة المعالجة الأساسية.

## الخطوة 2 – تحميل الصورة للـ OCR

بعد ذلك نوجه المحرك إلى الصورة التي نريد تحليلها. هنا يأتي دور كلمة **load image for ocr**.

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **نصيحة احترافية:** إذا كانت صورتك موجودة في دليل مختلف، استخدم `os.path.join` لإنشاء مسار مستقل عن النظام.

**لماذا تحميل الصورة بهذه الطريقة؟** أداة المساعدة `Image.load` تقرأ الملف إلى صيغة يفهمها المحرك، وتتعامل تلقائيًا مع الصيغ الشائعة (PNG، JPEG، TIFF). تخطي هذه الخطوة أو تمرير بايتات خام سيؤدي إلى رفع `ValueError`.

## الخطوة 3 – تشغيل عملية OCR

الآن نقوم فعليًا بتشغيل OCR. طريقة `process` تُعيد كائن نتيجة غني يحتوي على الرموز المُعترف بها، درجات الثقة، ومربعات الإحاطة.

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**ماذا يحتوي `ocr_result`؟** في معظم المكتبات يتضمن:

- `text`: السلسلة المجمعة الخام.
- `symbol_confidences`: قائمة من أزواج `(char, confidence)`.
- `boxes`: إحداثيات كل حرف (مفيدة لتصحيح الأخطاء بصريًا).

الوصول إلى ثقة كل حرف ضروري للخطوة التالية.

## الخطوة 4 – الاحتفاظ فقط بالرموز عالية الثقة (≥ 85 %)

غالبًا ما يحتوي الإيصال على بقع، طباعة باهتة، أو ضوضاء خلفية. من خلال تصفية الرموز ذات الثقة المنخفضة نحسن بشكل كبير عملية التحليل اللاحقة.

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**لماذا 85 %؟** تجريبيًا، عتبة حوالي 0.85 توازن بين الاستدعاء والدقة لمعظم الإيصالات المطبوعة. إذا لاحظت أرقامًا مفقودة، خفّض العتبة؛ إذا حصلت على نص غير مفهوم، ارتقِ بها.

## الخطوة 5 – إخراج النص المستخرج عالي الثقة

أخيرًا، نطبع (أو نخزن) السلسلة المنقحة. هذا هو جوهر سير عمل **extract text from receipt** الخاص بنا.

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

المخرجات النموذجية تبدو هكذا:

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

يمكنك الآن تمرير هذه السلسلة إلى كاتب CSV، قاعدة بيانات، أو أي خط أنابيب تحليلي لاحق.

## البرنامج الكامل الجاهز للتنفيذ

فيما يلي مقتطف الكود الكامل الذي يمكنك نسخه ولصقه في `ocr_receipt.py` وتشغيله فورًا.

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

احفظ الملف، تأكد من وجود `receipt.png`، ثم نفّذ:

```bash
python ocr_receipt.py
```

يجب أن ترى نص الإيصال المنقح يُطبع على وحدة التحكم.

## الحالات الخاصة وسيناريوهات ماذا‑لو

| الحالة | الإصلاح المقترح |
|-----------|----------------|
| **ثقة منخفضة جدًا في جميع العناصر** | معالجة مسبقة للصورة: زيادة التباين، تحويل إلى تدرج الرمادي، أو تطبيق مرشح إزالة الضوضاء (`cv2.GaussianBlur`). |
| **حروف غير لاتينية** | تمرير نموذج لغة إلى `OcrEngine` (مثال: `ocr_engine.language = "spa"` للغة الإسبانية). |
| **إيصالات متعددة في صورة واحدة** | تشغيل OCR على الصورة بالكامل، ثم تقسيم النتيجة باستخدام تعبيرات نمطية تكتشف `\n\n+` (فواصل سطر مزدوجة). |
| **الحاجة إلى النص الأصلي للـ OCR أيضًا** | الاحتفاظ بـ `ocr_result.text` إلى جانب النسخة المصفاة للتصحيح. |

## الأخطاء الشائعة (وكيفية تجنبها)

- **نسيان تثبيت المكتبة** – يجب أن ينجح `pip install aocr` قبل الاستيراد.
- **استخدام فاصل المسار الخطأ** على Windows (`\` مقابل `/`). استخدم `os.path.join`.
- **تحديد عتبة الثقة بشكل ثابت** دون اختبار – دائمًا قم بإجراء فحص بصري سريع على بعض الإيصالات أولاً.
- **تجاهل تطبيع Unicode** – بعض الإيصالات تحتوي على أحرف شرطة خاصة؛ شغّل `unicodedata.normalize('NFKC', text)` إذا كنت تخطط لتخزين النتيجة.

## الخطوات التالية – التقدم إلى ما بعد الأساسيات

الآن بعد أن عرفت **كيفية استخراج OCR** من إيصال واحد، قد ترغب في:

1. **معالجة مجموعة من الإيصالات في مجلد** – تكرار جميع ملفات PNG/JPG وكتابة كل نتيجة إلى CSV.
2. **التكامل مع قاعدة بيانات** – تخزين `high_confidence_text` في SQLite للبحث السريع.
3. **تطبيق التحليل اللغوي الطبيعي** – استخدم regex أو `dateutil` لاستخراج التواريخ، الإجماليات، ومبالغ الضرائب.
4. **تجربة مكتبات بديلة** – `pytesseract`، `easyocr`، أو خدمات سحابية (Google Vision، Azure OCR) إذا كنت تحتاج إلى دعم متعدد اللغات أو دقة أعلى.

كل من هذه المواضيع يدمج بطبيعية كلماتنا المفتاحية الثانوية: *python ocr example*، *extract text from receipt*، *load image for ocr*، و *how to use OCR*.

## الخلاصة

لقد استعرضنا للتو مثالًا كاملًا **python ocr example** يوضح **كيفية استخراج OCR** من صورة إيصال، تصفية الرموز ذات الثقة المنخفضة، وإخراج نتائج نظيفة. الخطوات بسيطة، الكود مستقل، والنهج مرن بما يكفي للتكيف مع مشاريع أكبر.

جرّبه على إيصالاتك الخاصة، عدّل عتبة الثقة، ثم قم بالتوسع إلى معالجة دفعات. إذا صادفت مشاكل — مثل شعار باهت أو خط غير مألوف — تذكّر نصائح الحالات الخاصة أعلاه. برمجة سعيدة، ولتكن خطوط أنابيب OCR دقيقة دائمًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}