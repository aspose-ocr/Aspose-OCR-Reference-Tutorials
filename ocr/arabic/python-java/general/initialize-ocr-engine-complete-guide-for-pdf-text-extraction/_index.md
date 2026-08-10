---
category: general
date: 2026-06-25
description: تهيئة محرك OCR في بايثون لاستخراج النص من ملفات PDF متعددة الصفحات باستخدام
  القواميس المخصصة وإعدادات اللغة وتحديد المناطق.
draft: false
keywords:
- initialize OCR engine
- configure OCR language
- OCR image preprocessing
- OCR custom dictionary
- recognize multi-page PDF
language: ar
og_description: تهيئة محرك OCR في بايثون لقراءة ملفات PDF الفيتنامية بشكل موثوق، وضبط
  اللغة، والمعالجة المسبقة، والقاموس المخصص للحصول على نتائج دقيقة.
og_title: تهيئة محرك OCR – دليل استخراج PDF خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  headline: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  type: TechArticle
- description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  name: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed. - An OCR library that exposes an `OcrEngine` class
      (the sample uses a hypothetical `ocr` package; replace with your actual SDK).
      - A sample multi‑page PDF (`sample.pdf`) placed in a known directory. - Basic
      familiarity with Python dictionaries and loops.'
  - name: Pro tip
    text: If you ever need to support multiple languages in the same run, you can
      switch `ocr_engine.language` on the fly before processing each page. Just remember
      to re‑initialize any heavy models if the SDK requires it.
  - name: Expected Output
    text: 'Running the script against a three‑page invoice PDF might produce:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: تهيئة محرك التعرف الضوئي على الأحرف – دليل كامل لاستخراج النص من ملفات PDF
url: /ar/python-java/general/initialize-ocr-engine-complete-guide-for-pdf-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تهيئة محرك OCR – دليل كامل لاستخراج النص من ملفات PDF

هل احتجت يومًا إلى **تهيئة محرك OCR** لمجموعة من الفواتير الفيتنامية ولم تكن متأكدًا من أين تبدأ؟ لست وحدك. في العديد من المشاريع الواقعية، العقبة الأولى هي جعل مكتبة OCR تتواصل مع ملفات PDF الخاصة بك، خاصةً عندما تحتاج إلى تعديل اللغة أو المعالجة المسبقة أو القاموس المخصص.  

في هذا الدليل سنستعرض مثالًا كاملاً قابلاً للتنفيذ يُظهر لك كيفية **تهيئة محرك OCR**، ضبط اللغة، تمكين المعالجة الذكية للصور، إضافة قاموس مخصص، وأخيرًا استخراج البيانات المهيكلة من كل صفحة في ملف PDF متعدد الصفحات. في النهاية ستحصل على سكريبت مستقل يمكنك إدراجه في مشروعك—بدون أجزاء مفقودة، بدون اختصارات “انظر الوثائق”.

## ما ستتعلمه

- كيفية **تهيئة محرك OCR** مع دعم اللغة الفيتنامية.  
- لماذا **ضبط لغة OCR** مهم للدقة.  
- استخدام خيارات **معالجة صورة OCR** مثل auto‑deskew و auto‑binarize.  
- إضافة **قاموس OCR مخصص** لتعزيز التعرف على المصطلحات المتخصصة.  
- **التعرف على ملفات PDF متعددة الصفحات** واستخراج منطقة محددة (مثل المبلغ الإجمالي).  
- تحويل النتائج الخام إلى بنية شبيهة بـ JSON نظيفة للمعالجة اللاحقة.

### المتطلبات المسبقة

- تثبيت Python 3.8+.  
- مكتبة OCR تُوفر فئة `OcrEngine` (العينة تستخدم حزمة `ocr` افتراضية؛ استبدلها بـ SDK الفعلي الخاص بك).  
- ملف PDF متعدد الصفحات تجريبي (`sample.pdf`) موجود في دليل معروف.  
- إلمام أساسي بقواميس Python والحلقات.

إذا كان لديك كل ذلك، لنبدأ.

---

## الخطوة 1: كيفية تهيئة محرك OCR في Python

أول شيء يجب عليك القيام به هو **تهيئة محرك OCR**. فكر فيه كتشغيل آلة وإخبارها باللغة التي ستزودها بها.

```python
import ocr  # Replace with your actual OCR package

# Create the engine instance
ocr_engine = ocr.OcrEngine()

# Set the language to Vietnamese – this tells the engine which character set to expect
ocr_engine.language = ocr.Language.Vietnamese
```

> **لماذا هذا مهم:**  
> معظم محركات OCR تأتي مع حزم لغات عامة. من خلال ضبط `ocr_engine.language` صراحةً، تتجنب تخمين المحرك لأحرف خاطئة، مما يقلل بشكل كبير من الأخطاء في الحروف المتحركة الشائعة في اللغة الفيتنامية.

### نصيحة احترافية
إذا احتجت يومًا إلى دعم عدة لغات في نفس التشغيل، يمكنك تبديل `ocr_engine.language` أثناء المعالجة قبل كل صفحة. فقط تذكر إعادة تهيئة أي نماذج ثقيلة إذا كان SDK يتطلب ذلك.

---

## الخطوة 2: تمكين خيارات معالجة صورة OCR

المسحات الخام نادرًا ما تكون مثالية. الصفحات المائلة، الإضاءة غير المتساوية، أو التباين المنخفض يمكن أن يعرقل حتى أفضل أدوات التعرف. لهذا السبب **نقوم بتهيئة معالجة صورة OCR** مباشرة بعد التهيئة.

```python
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,      # Auto‑rotate to correct tilt
    auto_binarize=True    # Convert to black‑and‑white for sharper edges
)
```

هذان العلمان غالبًا ما يكونان كافيين لتنظيف معظم الفواتير الممسوحة. إذا كانت ملفات PDF المصدر ذات جودة عالية بالفعل، يمكنك إيقافهما لتوفير بضع ميليثانية لكل صفحة.

---

## الخطوة 3: إضافة قاموس OCR مخصص

المصطلحات المتخصصة—مثل رموز الطلب، معرفات المنتجات، أو الاختصارات القانونية—نادرًا ما تظهر في نماذج اللغة العامة. من خلال تزويد **قاموس OCR مخصص**، تعطي المحرك ورقة غش.

```python
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]
```

> **ما الذي يحدث في الخلفية؟**  
> يعزز المحرك درجات الثقة لأي كلمة تتطابق مع إدخال في هذه القائمة، مما يجعل من غير المرجح أن تُقرأ خطأً كشيء آخر.

---

## الخطوة 4: التعرف على PDF متعدد الصفحات – استخراج كل النص مرة واحدة

الآن بعد أن تم تكوين المحرك بالكامل، يمكننا **التعرف على ملفات PDF متعددة الصفحات**. تُعيد الدالة `recognize_multi_page` قائمة حيث يمثل كل عنصر صفحة واحدة، وقد تم معالجتها مسبقًا بواسطة OCR.

```python
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)
```

إذا كنت تتعامل مع ملفات PDF ضخمة (مئات الصفحات)، فكر في معالجتها على دفعات للحفاظ على استهلاك الذاكرة منخفضًا. عادةً ما يوفر SDK واجهة برمجة تطبيقات تدفقية لهذا السيناريو.

---

## الخطوة 5: استخراج منطقة محددة من كل صفحة

معظم الفواتير تحتوي على حقل “المبلغ الإجمالي” الموجود في نفس الموقع في كل صفحة. بدلاً من تحليل النص الكامل للصفحة، يمكننا إخبار المحرك بالتركيز على مستطيل.

```python
from ocr import Rectangle  # Adjust import based on your SDK

for page_index, page in enumerate(pages, start=1):
    # Define the rectangle (x, y, width, height) that encloses the total amount
    total_region = Rectangle(400, 650, 200, 50)

    # Run OCR only on that region
    region_result = ocr_engine.recognize_region(page.image, total_region)
```

> **لماذا نستهدف منطقة معينة؟**  
> تحديد OCR على مساحة صغيرة يسرّع المعالجة ويقلل الإيجابيات الزائفة، خاصةً عندما يكون باقي الصفحة مليئًا بالضوضاء.

---

## الخطوة 6: تجميع قاموس شبيه بـ JSON لكل صفحة

وجود النص الخام أمر رائع، لكن الأنظمة اللاحقة عادةً ما تتوقع بيانات مهيكلة. أدناه نبني قاموسًا نظيفًا يلتقط رقم الصفحة، النص الكامل للصفحة، المبلغ المستخرج، وقائمة بجميع الكلمات المعترف بها مع درجات الثقة.

```python
    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    # Step 7: Output the result for the current page
    print(page_output)
```

تشغيل السكريبت سيُخرج سلسلة من القواميس—واحد لكل صفحة—تشبه الشكل التالي:

```json
{
  "page": 1,
  "full_text": "....",
  "total_amount": "1,250,000 VND",
  "words": [
    {"text": "MãĐơnHàng", "conf": 0.98},
    {"text": "KháchHàng", "conf": 0.96},
    ...
  ]
}
```

يمكنك بسهولة توجيه الإخراج إلى ملف (`> results.jsonl`) للمعالجة الدفعية لاحقًا.

---

## مثال كامل يعمل

بجمع كل ما سبق، إليك السكريبت الكامل الذي يمكنك نسخه ولصقه وتشغيله:

```python
import ocr
from ocr import Rectangle

# -------------------------------------------------
# 1️⃣ Initialize the OCR engine and configure it
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.Vietnamese
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]

# -------------------------------------------------
# 2️⃣ Recognize all pages of a multi‑page PDF
# -------------------------------------------------
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)

# -------------------------------------------------
# 3️⃣ Iterate through each page, extract region, and build output
# -------------------------------------------------
for page_index, page in enumerate(pages, start=1):
    total_region = Rectangle(400, 650, 200, 50)          # region of interest
    region_result = ocr_engine.recognize_region(page.image, total_region)

    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    print(page_output)   # Replace with logging or file write as needed
```

### النتيجة المتوقعة

تشغيل السكريبت على ملف PDF لفاتورة من ثلاث صفحات قد ينتج:

```
{'page': 1, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.99}, ...]}
{'page': 2, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.98}, ...]}
{'page': 3, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.97}, ...]}
```

لا تتردد في تمريره إلى `jq` أو أي محلل JSON للتحقق من البنية.

---

## أسئلة شائعة وحالات حافة

| السؤال | الجواب |
|----------|--------|
| **ماذا لو كان ملف PDF محميًا بكلمة مرور؟** | معظم SDKs تسمح بتمرير معامل `password` إلى `recognize_multi_page`. فقط أضف `password="mySecret"` إلى الاستدعاء. |
| **مسحاتي بالأبيض‑الأسود وليست بالألوان.** | خيار `auto_binarize` سيتعامل مع ذلك، لكن يمكنك أيضًا تحويل الصورة يدويًا باستخدام `Pillow` قبل تمريرها إلى `recognize_region`. |
| **المبلغ الإجمالي يظهر أحيانًا في إحداثيات مختلفة.** | إما حساب المستطيل ديناميكيًا (مثلاً عبر مطابقة القوالب) أو إجراء OCR كامل للصفحة ثم البحث في النص باستخدام تعبير نمطي مثل `r'\d{1,3}(,\d{3})* VND'`. |
| **الأداء بطيء على ملفات PDF مكوّنة من 500 صفحة.** | قسّم الصفحات إلى دفعات: عالج 50 صفحة، اكتب النتائج، ثم حرّر قائمة `pages` لتفريغ الذاكرة. كذلك، عطل `auto_deskew` إذا كانت مسحاتك مستقيمة بالفعل. |
| **كيف أتعامل مع لغات أخرى لاحقًا؟** | ببساطة غيّر `ocr_engine.language = ocr.Language.English` (أو أي تعداد مدعوم) قبل استدعاء `recognize_multi_page`. باقي خط الأنابيب يبقى كما هو. |

---

## نصائح للنشر في بيئات الإنتاج

1. **معالجة الأخطاء** – احط نداءات OCR بكتل `try/except`؛ سجّل فهرس الصفحة عند الفشل لتتمكن من إعادة المحاولة لاحقًا.  
2. **التسجيل** – استخدم وحدة `logging` في Python بدلاً من `print` للحصول على مرونة في مستوى التفاصيل.  
3. **التوازي** – إذا كانت مكتبة OCR آمنة للثريدات، أنشئ `ThreadPoolExecutor` لمعالجة الصفحات بشكل متزامن.  
4. **ملف التكوين** – خزن اللغة، القاموس، وإحداثيات المستطيل في ملف JSON/YAML؛ هذا يجعل السكريبت قابلًا لإعادة الاستخدام عبر المشاريع.  
5. **الاختبار** – أنشئ مجموعة اختبار صغيرة بملفات PDF معروفة وتأكد أن `total_amount` المستخرج يطابق القيم المتوقعة.  

---

## الخلاصة

لقد تعلمت للتو **

## ما الذي ينبغي أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [التعرف على نص PDF – عمليات OCR مع Aspose.OCR للـ Java](/ocr/english/java/ocr-operations/)
- [التعرف على نص الصورة مع Aspose OCR لعدة لغات](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [استخراج النص من الصورة – تحسين OCR مع Aspose.OCR للـ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}