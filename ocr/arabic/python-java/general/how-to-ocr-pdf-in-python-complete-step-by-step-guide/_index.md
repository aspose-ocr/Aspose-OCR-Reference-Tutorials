---
category: general
date: 2026-06-06
description: كيفية إجراء التعرف الضوئي على الأحرف (OCR) لملف PDF باستخدام بايثون،
  استخراج النص من PDF، تحويل نص PDF الممسوح ضوئياً، وتغيير لغة OCR في بضع أسطر من
  الشيفرة فقط.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: ar
og_description: 'كيفية التعرف الضوئي على النص في ملفات PDF باستخدام بايثون: دليل عملي
  يوضح لك كيفية استخراج النص من ملفات PDF، تحويل نص PDF الممسوح ضوئياً، وتغيير لغة
  التعرف الضوئي بسهولة.'
og_title: كيفية إجراء OCR لملف PDF في بايثون – دليل برمجة كامل
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: كيفية تحويل PDF إلى نص باستخدام OCR في بايثون – دليل كامل خطوة بخطوة
url: /ar/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على النص في ملفات PDF باستخدام بايثون – دليل خطوة بخطوة كامل

هل تساءلت يومًا **كيف تقوم بالتعرف الضوئي على النص في ملفات PDF** دون دفع تكاليف أدوات SaaS باهظة؟ لست وحدك. سواء كنت تقوم برقمنة الكتب القديمة، أو استخراج البيانات من الفواتير، أو تحتاج فقط إلى نص قابل للبحث من تقرير ممسوح ضوئيًا، فإن إتقان التعرف الضوئي على النص في PDF باستخدام بايثون يمكن أن يوفر لك ساعات من النسخ اليدوي.

في هذا الدرس سنستعرض مثالًا مختصرًا وعاملاً ي **يستخرج النص من PDF**، ويظهر لك كيفية **تحويل نص PDF الممسوح ضوئيًا** إلى سلاسل قابلة للتحرير، بل ويظهر أيضًا كيفية **تغيير لغة التعرف الضوئي** إذا لم يكن مستندك باللغة الإنجليزية. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع.

## المتطلبات المسبقة والإعداد

- Python 3.8+ مثبت (الكود يعمل على 3.9، 3.10، والإصدارات الأحدث)
- حزمة `ocr` التي توفر الفئة `OcrEngine` (يمكنك تثبيتها عبر `pip install ocr-lib` – استبدل باسم الحزمة الحقيقي الذي تستخدمه)
- ملف PDF تريد معالجته؛ في العرض التجريبي سنستخدم `high_res_book.pdf` الموجود في مجلد يسمى `YOUR_DIRECTORY`

إذا كنت تستخدم بيئة افتراضية (موصى بها بشدة)، فقم بتنشيطها أولاً:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **نصيحة احترافية:** احفظ ملفات PDF الخاصة بك في دليل مخصص `data/` لتجنب مشاكل المسارات لاحقًا.

## الخطوة 1: إنشاء مثيل محرك التعرف الضوئي (كيفية التعرف الضوئي على PDF – التهيئة)

أول شيء تحتاج إلى القيام به عندما تريد **إجراء التعرف الضوئي على PDF** هو إنشاء مثيل للمحرك. فكر في المحرك كالعقل الذي سيقرأ كل صفحة، يفسر الرموز، ويعيد لك نصًا عاديًا.

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

لماذا هذا مهم: بدون محرك لا يكون لديك سياق لإعدادات اللغة، خيارات العرض، أو معالجة PDF. كائن `OcrEngine` يحتفظ بكل هذه الإعدادات الافتراضية ويسمح لك بتعديلها لاحقًا.

## الخطوة 2: تعيين لغة التعرف (تغيير لغة OCR)

معظم مكتبات OCR تكون افتراضيًا باللغة الإنجليزية، ولكن ماذا لو كان مستندك بالفرنسية أو الألمانية أو حتى اليابانية؟ تغيير اللغة يكون بسيطًا كاستدعاء `set_recognition_language`. هذا يلبي متطلبات **تغيير لغة OCR** ويضمن دقة أعلى.

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **لماذا قد تحتاج هذا:** غالبًا ما يحتوي أرشيف متعدد اللغات على صفحات مختلطة اللغات. تبديل اللغات أثناء التشغيل يمنع الأخطاء في التعرف على أحرف مثل “ß” أو “ñ”.

## الخطوة 3: تكوين خيارات عرض PDF (تحويل نص PDF الممسوح بفعالية)

عند التعامل مع ملفات PDF الممسوحة، تؤثر الدقة ووضع اللون بشكل كبير على جودة OCR. العرض بدقة 300 DPI بالأبيض‑الأسود هو النقطة المثالية لمعظم المستندات—عالية بما يكفي لالتقاط التفاصيل ولكن منخفضة بما يكفي للحفاظ على استهلاك الذاكرة معقولًا.

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

قد تبدو الاستدعاءات المتسلسلة فاخرة، لكنها مجرد API سلسة تُعيد نفس كائن الخيارات في كل مرة. إذا كنت تحتاج إلى اللون (مثلاً للرسوم البيانية الملونة)، استبدل `"grayscale"` بـ `"color"`.

## الخطوة 4: التعرف على PDF واستخراج نص الصفحة الأولى (استخراج النص من PDF)

الآن يأتي جوهر **كيفية التعرف الضوئي على PDF**: تمرير مسار الملف إلى المحرك واستخراج النص المعترف به. تُعيد الطريقة قائمة بنتائج الصفحات؛ كل نتيجة تحتوي على خاصية `text`.

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

إذا كنت تحتاج المستند بالكامل، قم بالتكرار على `results`:

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### ماذا لو كان PDF مشفرًا؟

بعض ملفات PDF محمية بكلمة مرور. في هذه الحالة يمكنك تمرير كلمة المرور إلى `recognize_pdf`:

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

سيقوم المحرك بفك التشفير أثناء التشغيل قبل إجراء OCR—لا خطوات إضافية مطلوبة.

## الخطوة 5: ما بعد معالجة النص المستخرج (تحسين استخراج النص من PDF)

غالبًا ما يحتوي ناتج OCR الخام على فواصل أسطر، مسافات إضافية، أو أحرف تم التعرف عليها بشكل خاطئ أحيانًا. روتين تنظيف سريع يجعل السلسلة المستخرجة جاهزة للمعالجة اللاحقة (فهرسة البحث، تخزين قاعدة البيانات، إلخ).

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

يمكنك الآن بأمان **استخراج النص من PDF** وإدخاله في أي خط أنابيب NLP، محرك بحث، أو عملية بسيطة `open(...).write()`.

## إضافي: معالجة دفعة متعددة من ملفات PDF (توسيع أداء OCR على PDF)

إذا كان لديك مجلد مليء بملفات PDF الممسوحة، قم بلف المنطق داخل حلقة:

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

هذا المقتطف يوضح كيفية **إجراء OCR على PDF** بشكل جماعي، وهو احتياج شائع لمشاريع الرقمنة.

## النتيجة المتوقعة

تشغيل مثال الصفحة الواحدة (الخطوة 4) يجب أن يطبع شيئًا مشابهًا لـ:

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

إذا قمت بمعالجة كتاب متعدد الصفحات، سيعرض الطرفية النص المنظف لكل صفحة، وستترك سكريبت الدفعة ملف `.txt` بجانب كل PDF.

## المشكلات الشائعة وكيفية تجنبها

| Issue | Symptoms | Fix |
|-------|----------|-----|
| PDF مصدر منخفض الدقة | حروف مشوشة، كلمات مفقودة | زيادة DPI (`set_dpi(400)` أو أعلى) |
| إعداد لغة خاطئ | العديد من الرموز غير المعروفة، خاصة الأحرف ذات اللكنات | استخدم `engine.set_recognition_language(ocr.Language.FRENCH)` أو التعداد المناسب |
| PDF كبير يسبب خطأ في الذاكرة | `MemoryError` أو تعطل بعد بضع صفحات | معالجة الصفحات على دفعات (`engine.recognize_pdf(..., max_pages=10)`) |
| خطوط مفقودة في PDF | ناتج فارغ لبعض الصفحات | تأكد من أن PDF يحتوي فعليًا على صور نقطية؛ بعض ملفات PDF هي فقط متجهية وتحتاج إلى معالجة مختلفة |

## توضيح الصورة

فيما يلي تصور سريع لسير العمل. نص alt مكتوب عمدًا ليتوافق مع تحسين محركات البحث.

![مخطط سير عمل كيفية التعرف الضوئي على PDF يوضح تهيئة المحرك، إعداد اللغة، خيارات العرض، التعرف، واستخراج النص](/images/ocr-workflow.png)

*المخطط غير مطلوب لتشغيل الكود، لكنه يساعد المتعلمين البصريين على رؤية موضع كل خطوة.*

## الخلاصة

لقد غطينا **كيفية التعرف الضوئي على PDF** باستخدام بايثون من البداية إلى النهاية: إنشاء محرك OCR، **تغيير لغة OCR**، تكوين العرض لتحويل **نص PDF الممسوح**، وأخيرًا **استخراج النص من PDF** للاستخدام لاحقًا. المثال الكامل القابل للتنفيذ جاهز للإدراج في أي مشروع، والسكريبت الاختياري للدفعة يوضح لك كيفية توسيع الحل.

Next, you might want to explore:

- إضافة **إجراء OCR على PDF** لأرشيفات متعددة اللغات عبر التكرار على قائمة اللغات.
- دمج النص المستخرج مع Elasticsearch للبحث النصي الكامل.
- استخدام OCR لإنشاء ملفات PDF قابلة للبحث عن طريق تضمين طبقة النص مرة أخرى في الملف الأصلي (العديد من المكتبات توفر طريقة `save_as_searchable_pdf`).

لا تتردد في التجربة، تعديل إعدادات DPI، أو التحويل إلى محرك OCR مختلف. الأساسيات تبقى كما هي، والآن لديك أساس قوي للبناء عليه.

برمجة سعيدة، ولتصبح مستنداتك الممسوحة ضوئيًا قابلة للبحث أخيرًا!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [التعرف على نص PDF – عمليات OCR مع Aspose.OCR للـ Java](/ocr/english/java/ocr-operations/)
- [كيفية التعرف الضوئي على نص الصورة مع اللغة باستخدام Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [كيفية التعرف الضوئي على PDF في .NET مع Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}