---
category: general
date: 2026-06-28
description: دليل OCR للنص المنظم يُظهر كيفية إجراء OCR على صورة، تحميل OCR للصورة،
  تنفيذ معالجة ما بعد OCR، واستخدام Aspose OCR Python للحصول على نتائج دقيقة.
draft: false
keywords:
- structured text ocr
- how to ocr image
- ocr post processing
- aspose ocr python
- load image ocr
language: ar
og_description: التعرف الضوئي على النص المهيكل باستخدام Aspose OCR Python. تعلّم كيفية
  إجراء التعرف الضوئي على الصورة، تحميل الصورة للتعرف الضوئي، وتطبيق معالجة ما بعد
  التعرف الضوئي في دليل خطوة بخطوة.
og_title: التعرف الضوئي على النص المنظم في بايثون – دليل Aspose OCR الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Structured text OCR tutorial showing how to OCR image, load image OCR,
    perform OCR post processing, and use Aspose OCR Python for accurate results.
  headline: Structured Text OCR in Python with Aspose – Complete Guide
  type: TechArticle
- description: Structured text OCR tutorial showing how to OCR image, load image OCR,
    perform OCR post processing, and use Aspose OCR Python for accurate results.
  name: Structured Text OCR in Python with Aspose – Complete Guide
  steps:
  - name: '**Load image OCR** with auto‑rotate and preprocessing.'
    text: '**Load image OCR** with auto‑rotate and preprocessing.'
  - name: '**Run OCR** while preserving layout (`recognize_structured`).'
    text: '**Run OCR** while preserving layout (`recognize_structured`).'
  - name: '**Apply OCR post processing** via AI spell‑checking.'
    text: '**Apply OCR post processing** via AI spell‑checking.'
  - name: '**Save** the corrected result as JSON (and optionally CSV).'
    text: '**Save** the corrected result as JSON (and optionally CSV).'
  - name: '**Extend** the workflow into NLP or downstream analytics.'
    text: '**Extend** the workflow into NLP or downstream analytics.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: التعرف الضوئي على النص المنظم في بايثون باستخدام أسبوز – دليل كامل
url: /ar/python/general/structured-text-ocr-in-python-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف الضوئي على النصوص المهيكلة في بايثون – دليل كامل

هل تساءلت يومًا كيف تقوم بـ **structured text OCR** لملاحظة مكتوبة يدويًا دون قضاء ساعات في تعديل الإعدادات؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحاولون **load image OCR** والحفاظ على تنسيق الصفحة الأصلي. الخبر السار؟ Aspose OCR for Python يجعل الأمر سهلًا، ويمكنك حتى إضافة تدقيق إملائي مدفوع بالذكاء الاصطناعي كخطوة **OCR post processing** نظيفة.

في هذا الدرس سنستعرض كامل خط الأنابيب — من تحميل الصورة إلى الحصول على ملف JSON يحافظ على فواصل الأسطر والأعمدة. في النهاية، ستحصل على سكريبت جاهز للتنفيذ يُظهر *بالضبط* كيفية **OCR image**، تشغيل ما بعد المعالجة، وإخراج نص مهيكل ونظيف.

---

## ما ستحتاجه

- **Python 3.8+** – أي نسخة حديثة تعمل.  
- **Aspose.OCR for .NET** (متاح للبايثون عبر `pythonnet`). قم بتثبيته باستخدام `pip install pythonnet` ثم أضف ملفات Aspose OCR DLL إلى مشروعك.  
- صورة نموذجية (مثال: `sample_handwritten.jpg`). من الأفضل أن تكون صفحة ممسوحة ضوئيًا ذات صفوف وأعمدة واضحة.  
- اختياري: اتصال بالإنترنت إذا كنت تريد أن يستدعي مدقق الإملاء AI خدمات Aspose AI.  

> **نصيحة احترافية:** احرص على أن تكون الصورة أصغر من 2 ميغابايت لتسريع مرحلة ما قبل المعالجة؛ الملفات الكبيرة قد تتسبب في توقف خطوة التدوير التلقائي.

---

## الخطوة 1 – تحميل الصورة وتحضيرها للتعرف الضوئي (OCR)

أول ما تقوم به عند **load image OCR** هو جلب الملف إلى الذاكرة وتطبيق بعض الأدوات المفيدة: التدوير التلقائي وتقليل الضوضاء. تجمع Aspose OCR هذه المساعدات في `OcrUtil`.

```python
import clr
clr.AddReference("Aspose.OCR")
from Aspose.Ocr import Image, OcrUtil, OcrEngine, AsposeAI, AIProcessor

# Load the image from disk
image_path = "YOUR_DIRECTORY/sample_handwritten.jpg"
image = Image.from_file(image_path)

# Automatic rotation (detects portrait vs. landscape)
image = OcrUtil.auto_rotate(image)

# Pre‑process to improve contrast and remove background speckles
image = OcrUtil.preprocess(image)
```

**لماذا هذا مهم:**  
إذا كانت الصورة مائلة، سيقرأ محرك OCR كل حرف مقلوبًا. استدعاء `auto_rotate` يوفر عليك تدوير الملفات يدويًا. خطوة `preprocess` تعزز دقة التعرف، خاصةً على الملاحظات الممسوحة التي لا يكون الخلفية فيها بيضاء صافية.

---

## الخطوة 2 – تشغيل محرك OCR والحفاظ على التخطيط

الآن بعد أن أصبحت الصورة مرتبة، نمررها إلى محرك OCR الأساسي. الطريقة الرئيسية هنا هي `recognize_structured()`، التي تُعيد `StructuredResult` تحافظ على الصفوف والأعمدة والمسافات البادئة — بالضبط ما تحتاجه لـ **structured text OCR**.

```python
# Initialise the OCR engine
engine = OcrEngine()
engine.set_image(image)

# Perform OCR while preserving the original layout
raw_result = engine.recognize_structured()
```

**ما ستحصل عليه:**  
`raw_result` يحتوي على هيكلية `Pages → Lines → Words`. كل سطر يعرف إحداثياته الأصلية X/Y، لذا يمكنك إعادة بناء الجداول أو النماذج لاحقًا إذا رغبت.

---

## الخطوة 3 – تطبيق تدقيق إملائي مدفوع بالذكاء الاصطناعي (معالجة ما بعد OCR)

مخرجات OCR الخام غالبًا ما تكون مليئة بالكلمات غير الصحيحة، خاصةً مع الخطوط المتصلة. تقدم Aspose AI معالجًا مريحًا يندمج مباشرةً مع كائن النتيجة.

```python
# Initialise Aspose AI for spell‑checking
ai = AsposeAI()
ai.set_post_processor(AIProcessor.SpellCheck, {})

# Run spell‑check on the structured OCR result
corrected_result = ai.run_postprocessor(raw_result)
```

**لماذا تدقيق الإملاء يُغيّر اللعبة:**  
حتى دقة 85 % متواضعة يمكن رفعها إلى أكثر من 95 % بتمرير القاموس. معالج `SpellCheck` يحترم التخطيط، لذا تظل فواصل الأسطر كما هي بينما تُصحح الكلمات الفردية.

---

## الخطوة 4 – حفظ المخرجات المهيكلة والمصححة

تفضل معظم الأنظمة اللاحقة JSON أو CSV أو نصًا عاديًا. أداة `save_result` في Aspose OCR تكتب كامل `StructuredResult` إلى ملف مع الحفاظ على الهيكلية.

```python
# Persist the corrected result as JSON
output_path = "YOUR_DIRECTORY/result.json"
OcrUtil.save_result(corrected_result, output_path)

# Print each line to the console for quick verification
for line in corrected_result.Lines:
    print(line.Text)
```

**مخرجات وحدة التحكم المتوقعة (مثال):**

```
Dear John,
Please find the attached invoice for March.
Total amount: $1,250.00
Thank you,
Acme Corp.
```

لاحظ كيف تتطابق فواصل الأسطر مع المسح الأصلي، وكيف تُصحح الأخطاء الشائعة مثل “March” → “Marrh” تلقائيًا.

---

## الخطوة 5 – (اختياري) تصدير إلى CSV لتدفقات العمل في الجداول

إذا كنت تحتاج إلى بيانات جدولة، فإن تحويل النتيجة المهيكلة إلى CSV سهل للغاية. إليك دالة مساعدة يمكنك إضافتها إلى سكريبتك.

```python
import csv

def export_to_csv(structured_result, csv_path):
    """
    Writes each line of the OCR result to a CSV row.
    Columns are inferred from whitespace gaps.
    """
    with open(csv_path, mode="w", newline="", encoding="utf-8") as file:
        writer = csv.writer(file)
        for line in structured_result.Lines:
            # Split on multiple spaces to guess column boundaries
            columns = [col.strip() for col in line.Text.split("  ") if col]
            writer.writerow(columns)

csv_output = "YOUR_DIRECTORY/result.csv"
export_to_csv(corrected_result, csv_output)
print(f"CSV exported to {csv_output}")
```

الآن لديك ملف CSV جاهز للاستيراد يعكس تخطيط الصفحة الأصلي — مناسب تمامًا للمحاسبة أو خطوط إدخال البيانات.

---

## المشكلات الشائعة وكيفية تجنّبها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| **إخراج فارغ** | عدم تحميل الصورة بشكل صحيح (مسار خاطئ) | تحقق من `image_path` وتأكد من وجود الملف. |
| **حروف غير مفهومة** | تخطي `preprocess` على مسحات منخفضة التباين | احرص دائمًا على استدعاء `OcrUtil.preprocess`. |
| **فقدان التخطيط** | استخدام `engine.recognize()` بدلاً من `recognize_structured()` | التزم بالطريقة المهيكلة للحفاظ على التخطيط. |
| **فشل تدقيق الإملاء** | عدم وجود إنترنت أو بيانات اعتماد Aspose AI غير صالحة | تأكد من أن بيئتك تستطيع الوصول إلى خدمات Aspose AI أو استخدم قواميس غير متصلة. |

---

## توسيع خط الأنابيب: من OCR المهيكل إلى معالجة اللغة الطبيعية (NLP)

بمجرد حصولك على نص نظيف ومهيكل، الخطوة المنطقية التالية هي إرساله إلى نموذج NLP (مثل spaCy) لاستخراج الكيانات. بما أن التخطيط محفوظ، يمكنك ربط الكيانات المكتشفة بمواقعها الأصلية — ميزة قيمة للذكاء الاصطناعي القائم على المستندات.

```python
import spacy

nlp = spacy.load("en_core_web_sm")
doc = nlp("\n".join([line.Text for line in corrected_result.Lines]))

for ent in doc.ents:
    print(ent.text, ent.label_)
```

هذا المقتطف يستخرج التواريخ والقيم المالية وأسماء الأشخاص، محولًا إيصالًا ممسوحًا إلى بيانات قابلة للتنفيذ.

---

## ملخص

غطيْنا جميع جوانب **structured text OCR** باستخدام Aspose OCR for Python:

1. **Load image OCR** مع التدوير التلقائي وما قبل المعالجة.  
2. **Run OCR** مع الحفاظ على التخطيط (`recognize_structured`).  
3. **Apply OCR post processing** عبر تدقيق إملائي مدفوع بالذكاء الاصطناعي.  
4. **Save** النتيجة المصححة كملف JSON (واختياريًا CSV).  
5. **Extend** سير العمل إلى NLP أو تحليلات لاحقة.

كل ذلك في سكريبت واحد متكامل يمكنك إدراجه في أي مشروع بايثون.

---

## ما التالي؟

- **جرب لغات مختلفة** – يدعم Aspose OCR أكثر من 60 لغة؛ فقط اضبط `engine.Language = "fra"` للفرنسية.  
- **اضبط ما قبل المعالجة** – عدّل معلمات `OcrUtil.preprocess` للوصلات الضوضائية.  
- **دمج مع Azure Functions** – حوّل السكريبت إلى API بدون خادم يعالج التحميلات فورًا.  

إذا كنت مهتمًا بـ **how to OCR image** دفعةً، فكر في حلقة تمر عبر دليل وتضيف كل نتيجة JSON إلى ملف رئيسي. نفس النمط يعمل مع ملفات PDF — فقط حوّل كل صفحة إلى صورة أولًا.

---

![مخطط خط أنابيب OCR المهيكل – يظهر تحميل الصورة OCR، ما قبل المعالجة، محرك OCR، ما بعد المعالجة بالذكاء الاصطناعي، والإخراج](/images/structured_ocr_pipeline.png "structured text ocr pipeline")

*نص بديل الصورة: توضيح مخطط خط أنابيب OCR المهيكل*

---

### ترميز سعيد!

إذا واجهت أي مشكلة، اترك تعليقًا أدناه أو راجع الوثائق الرسمية لـ Aspose للحصول على أحدث التعديلات في الـ API. تذكر، المفتاح للحصول على OCR موثوق هو إدخال نظيف ومعالجة ما بعد ذكية — بمجرد إتقان هذين الأمرين، يبقى ما هو متبقٍ مجرد كود ربط.

---

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم استعراضها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية استخدام Aspose OCR للحصول على نتيجة JSON في التعرف على الصور](/ocr/english/net/text-recognition/get-result-as-json/)
- [كيفية التعرف على نص الصورة باستخدام اللغة عبر Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}