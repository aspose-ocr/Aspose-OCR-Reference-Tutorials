---
category: general
date: 2026-06-16
description: كيفية التعرف الضوئي على النص في ملفات PDF باستخدام بايثون في دقائق –
  تعلم استخراج النص من PDF، تشغيل OCR على PDF، وتحويل نص PDF الممسوح ضوئياً بكفاءة.
draft: false
keywords:
- how to OCR PDF
- extract text from PDF
- run OCR on PDF
- convert scanned PDF text
- load PDF for OCR
language: ar
og_description: 'كيفية التعرف الضوئي على النص في ملفات PDF باستخدام بايثون: تعليمات
  خطوة بخطوة لاستخراج النص من PDF، تشغيل OCR على PDF، وتحويل نص PDF الممسوح.'
og_title: كيفية التعرف الضوئي على النص في ملفات PDF باستخدام بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to OCR PDF using Python in minutes – learn to extract text from
    PDF, run OCR on PDF, and convert scanned PDF text efficiently.
  headline: How to OCR PDF in Python – Complete Guide
  type: TechArticle
- description: How to OCR PDF using Python in minutes – learn to extract text from
    PDF, run OCR on PDF, and convert scanned PDF text efficiently.
  name: How to OCR PDF in Python – Complete Guide
  steps:
  - name: Initialized an OCR engine.
    text: Initialized an OCR engine.
  - name: Set the language (optional but recommended).
    text: Set the language (optional but recommended).
  - name: Limited the page range to speed things up.
    text: Limited the page range to speed things up.
  - name: Loaded the PDF file.
    text: Loaded the PDF file.
  - name: Ran OCR on the document.
    text: Ran OCR on the document.
  - name: '**Extracted text from PDF** for immediate use.'
    text: '**Extracted text from PDF** for immediate use.'
  - name: Exported detailed results to **convert scanned PDF text** into JSON.
    text: Exported detailed results to **convert scanned PDF text** into JSON.
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: كيفية التعرف الضوئي على النص في ملفات PDF باستخدام بايثون – دليل كامل
url: /ar/python-java/general/how-to-ocr-pdf-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على النص في ملفات PDF باستخدام بايثون – دليل كامل

هل تساءلت يومًا **how to OCR PDF** عن ملفات PDF دون عناء؟ لست وحدك؛ عدد لا يحصى من المطورين يواجهون نفس المشكلة عند محاولة تحويل الصفحات الممسوحة ضوئيًا إلى نص قابل للبحث. الخبر السار؟ ببضع أسطر من بايثون يمكنك تحميل PDF للتعرف الضوئي على النص، تشغيل OCR على صفحات PDF، واستخراج سلاسل نظيفة قابلة للتعديل في ثوانٍ.

في هذا الدرس سنستعرض مثالًا واقعيًا يوضح لك بالضبط كيفية التعرف الضوئي على نص PDF، استخراج النص من صفحات PDF، وحتى تحويل نص PDF الممسوح ضوئيًا إلى نتائج مُهيكلة بصيغة JSON. لا إطالة، فقط سكريبت عملي يمكنك إدراجه في مشروعك اليوم.

## ما ستحتاجه

- Python 3.8+ (أي نسخة حديثة تعمل)
- مكتبة `ocr` (أو غلاف متوافق – سنفترض حزمة `ocr` عامة تتبع الـ API الموضح)
- ملف PDF ممسوح ضوئيًا متعدد الصفحات تريد معالجته
- بيئة تطوير متكاملة أو محرر من اختيارك (VS Code، PyCharm، أو حتى محرر نص بسيط)

هذا كل شيء. إذا كان لديك هذه المتطلبات، فأنت جاهز للبدء في استخراج النص من ملفات PDF كمحترف.

## الخطوة 1 – إعداد محرك OCR (How to OCR PDF)

أولًا: أنشئ مثالًا لمحرك OCR. فكر في المحرك كالعقل الذي سيقرأ كل بكسل في مستندك.

```python
# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

> **نصيحة احترافية:** تهيئة المحرك رخيصة، ولكن إذا كنت تخطط لمعالجة عشرات ملفات PDF دفعة واحدة، أعد استخدام كائن `engine` نفسه لتوفير الذاكرة.

![مخطط تدفق OCR يوضح كيفية التعرف الضوئي على PDF](/images/ocr-pdf-workflow.png "سير عمل التعرف الضوئي على PDF")

## الخطوة 2 – اختيار اللغة الصحيحة (Run OCR on PDF)

إذا كانت مسحاتك باللغة الإنجليزية، حدد اللغة صراحة. تخطي هذه الخطوة يترك للمحرك التخمين، مما قد يكون أبطأ وأحيانًا أقل دقة.

```python
# Step 2 (optional): Set language to English
engine.language = ocr.Language.ENGLISH
```

لماذا ذلك؟ لأن إخبار المحرك بـ **run OCR on PDF** مع لغة معروفة يحسن معدلات التعرف بشكل كبير—خاصةً للوثائق التي تحتوي على مصطلحات تقنية.

## الخطوة 3 – التركيز على صفحات محددة (Load PDF for OCR)

معالجة أرشيف ضخم مكون من 500 صفحة قد يكون مبالغًا فيه إذا كنت تحتاج فقط إلى الفصول الأولى. يمكنك تحديد نطاق الصفحات هكذا:

```python
# Step 3 (optional): Process only pages 1‑5
engine.pdf_page_range = (1, 5)
```

هذه التعديلة الصغيرة تخبر المحرك بـ **load PDF for OCR** ولكن فقط للصفحات التي تهمك، مما يوفر الوقت ودورات المعالج.

## الخطوة 4 – تحميل المستند (Load PDF for OCR)

الآن وجه المحرك إلى الملف الفعلي. تأكد من صحة المسار؛ وإلا ستواجه `FileNotFoundError`.

```python
# Step 4: Load the multi‑page PDF file
engine.load_from_file("YOUR_DIRECTORY/multipage-document.pdf")
```

في هذه المرحلة يكون المحرك قد **loaded the PDF for OCR**، وحلل البنية الداخلية، وهو جاهز لبدء العمل الشاق.

## الخطوة 5 – تشغيل عملية التعرف (Run OCR on PDF)

هذه هي اللحظة التي يحدث فيها السحر. استدعاء `recognize()` يفحص كل بكسل، يطبق نماذج اللغة، ويعيد كائن نتيجة غني.

```python
# Step 5: Run OCR on the loaded document
pdf_result = engine.recognize()
```

خلف الكواليس، المحرك **runs OCR on PDF** للصفحات، يبني طبقات نصية، وحتى يحتفظ بدرجات الثقة لكل كلمة.

## الخطوة 6 – استخراج النص الكامل (Extract Text from PDF)

معظم حالات الاستخدام تحتاج فقط إلى النص العادي. الخاصية `text` تعطيك سلسلة مدمجة لكل ما رآه المحرك.

```python
# Step 6: Retrieve the combined text of the entire PDF
print("Full PDF text:\n", pdf_result.text)
```

الآن لقد نجحت في **extracted text from PDF**—جاهز لتغذيته إلى فهرس بحث، قاعدة بيانات، أو مجرد `print()`.

## الخطوة 7 – فحص النتائج التفصيلية (Convert Scanned PDF Text)

إذا كنت تحتاج أكثر من سلاسل نصية خام—مثلاً تريد الصناديق المحيطة أو درجات الثقة—استخدم تصدير JSON. هذا في الأساس **converting scanned PDF text** إلى صيغة قابلة للقراءة آليًا.

```python
# Step 7: View detailed OCR results for each page in JSON
print(pdf_result.to_json(indent=2))
```

يتضمن JSON مصفوفات لكل صفحة، كل إدخال يحتوي على النص المعترف به، موقعه على الصفحة، ومقياس الثقة. مثالي للمعالجة اللاحقة مثل استخراج الكيانات أو التظليل المخصص.

## الأخطاء الشائعة وكيفية تجنبها

| **حروف غير صالحة** | اللغة خاطئة أو الخطوط مفقودة | اضبط `engine.language` صراحةً إلى اللغة الصحيحة. |
| **صفحات مفقودة** | `pdf_page_range` ضيق جدًا | تحقق مرة أخرى من أن الزوج `(start, end)` يطابق مستندك. |
| **بطء الأداء** | معالجة ملفات PDF الكبيرة دفعة واحدة | قسم PDF إلى أجزاء أو عالج الصفحات بالتوازي باستخدام `concurrent.futures`. |
| **إخراج فارغ** | خطأ في مسار الملف أو PDF غير قابل للقراءة | تأكد من وجود الملف وأنه غير محمي بكلمة مرور. |

معالجة هذه القضايا مبكرًا يوفر لك ساعات من تصحيح الأخطاء لاحقًا.

## توسيع المثال

- **معالجة دفعات:** تكرار عبر مجلد من ملفات PDF، وإعادة استخدام نفس كائن `engine`.
- **إخراج مخصص:** كتابة `pdf_result.text` إلى ملف `.txt`، أو إرساله مباشرة إلى محرك بحث مثل Elasticsearch.
- **استخراج الصور:** بعض مكتبات OCR تعرض الصور لكل صفحة؛ يمكنك استخراجها للتحقق البصري.

إليك مقتطف صغير يوضح كيف يمكنك معالجة مجلد دفعةً:

```python
import pathlib, json

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    engine.load_from_file(str(pdf_path))
    result = engine.recognize()
    (pdf_folder / f"{pdf_path.stem}.txt").write_text(result.text)
    (pdf_folder / f"{pdf_path.stem}.json").write_text(result.to_json(indent=2))
    print(f"Processed {pdf_path.name}")
```

## ملخص – ما تم تغطيته

بدأنا بالسؤال **how to OCR PDF** في بايثون، ثم:

1. تهيئة محرك OCR.
2. ضبط اللغة (اختياري لكن يُنصح به).
3. تحديد نطاق الصفحات لتسريع العملية.
4. تحميل ملف PDF.
5. تشغيل OCR على المستند.
6. **Extracted text from PDF** للاستخدام الفوري.
7. تصدير النتائج التفصيلية إلى **convert scanned PDF text** بصيغة JSON.

جميع هذه الخطوات معًا تمنحك أساسًا قويًا لتحويل أي PDF ممسوح ضوئيًا إلى محتوى قابل للبحث والتحرير.

## الخطوات التالية

- جرّب لغات مختلفة (`ocr.Language.SPANISH`, `ocr.Language.FRENCH`) لترى كيف يتعامل المحرك مع المستندات متعددة اللغات.
- جرب ضبط `engine.dpi` إذا كانت مسحاتك منخفضة الدقة—زيادة DPI يمكن أن تحسن الدقة.
- اجمع مخرجات OCR مع مكتبات معالجة اللغة الطبيعية مثل spaCy لاستخراج الكيانات، التواريخ، أو العبارات المفتاحية تلقائيًا.

هل لديك أسئلة حول **load PDF for OCR** أو تواجه مشكلة أثناء **run OCR on PDF**؟ اترك تعليقًا أدناه، وسنحل المشكلة معًا. برمجة سعيدة، واستمتع بتحويل تلك المسحات العنيدة إلى ذهب قابل للبحث!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية التعرف الضوئي على PDF في .NET باستخدام Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [التعرف على نص PDF – عمليات OCR مع Aspose.OCR للـ Java](/ocr/english/java/ocr-operations/)
- [تحويل الصور إلى PDF C# – حفظ نتيجة OCR متعددة الصفحات](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}