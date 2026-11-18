---
category: general
date: 2026-06-25
description: استخراج نص PDF باستخدام OCR في بايثون. تعلم كيفية تحويل PDF إلى نص مع
  مثال واضح لـ OCR في بايثون واحصل على نتائج موثوقة بسرعة.
draft: false
keywords:
- extract pdf text OCR
- convert pdf to text
- python ocr example
- Aspose OCR Python
- multi‑page PDF OCR
language: ar
og_description: استخراج نص PDF باستخدام OCR في بايثون. يوضح هذا الدليل مثالًا على
  OCR بايثون يحول PDF إلى نص، ويتعامل بسهولة مع المستندات متعددة الصفحات.
og_title: استخراج نص PDF باستخدام OCR في بايثون – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract PDF text OCR using Python. Learn how to convert PDF to text
    with a clear python OCR example and get reliable results fast.
  headline: Extract PDF Text OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: استخراج نص PDF باستخدام OCR في بايثون – دليل خطوة بخطوة كامل
url: /ar/python-java/general/extract-pdf-text-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج نص PDF باستخدام OCR في بايثون – دليل خطوة‑بخطوة كامل

هل احتجت يوماً إلى **استخراج نص PDF باستخدام OCR** لكنك لم تكن متأكدًا أي مكتبة يمكنها التعامل مع ملفات PDF متعددة الصفحات دون عناء؟ لست وحدك. في العديد من المشاريع الواقعية—مثل العقود القانونية، الفواتير الممسوحة، أو التقارير المؤرشفة—الحصول على نص نظيف وقابل للبحث من ملف PDF هو مهارة أساسية.

في هذا الدرس سنستعرض **مثال ocr بايثون** الذي **يحوّل PDF إلى نص** باستخدام Aspose.OCR. في النهاية ستحصل على سكريبت جاهز للتنفيذ يقرأ نص كل صفحة، يعرض معاينة، وحتى يحفظ المستند بالكامل كملف `.txt` واحد. لا إطالة، مجرد حل عملي يمكنك دمجه في قاعدة الشيفرة الخاصة بك اليوم.

## ما ستتعلمه

- كيفية تثبيت واستيراد وحدة Aspose OCR للبايثون.  
- كيفية إنشاء كائن محرك OCR وتشغيل **استخراج نص PDF باستخدام OCR** على ملف PDF متعدد الصفحات.  
- طرق التكرار عبر نتائج كل صفحة، عرض معاينة، وكتابة المخرجات الكاملة إلى القرص.  
- نصائح للتعامل مع المشكلات الشائعة مثل الصفحات الفارغة أو الأحرف Unicode.  

> **المتطلبات المسبقة:** وجود Python 3.8+ مثبت، معرفة أساسية بـ pip، وملف PDF تريد معالجته. لا تحتاج إلى خبرة سابقة في OCR.

---

![مخطط تدفق استخراج نص PDF باستخدام OCR](extract-pdf-text-ocr.png "مخطط عملية استخراج نص PDF باستخدام OCR")

*نص بديل: مخطط يوضح سير عمل استخراج نص PDF باستخدام OCR في بايثون.*

## الخطوة 1: تثبيت Aspose OCR للبايثون

قبل تشغيل أي كود، تحتاج إلى حزمة Aspose.OCR. يتم توزيعها عبر PyPI، لذا أمر pip واحد يكفي.

```bash
pip install aspose-ocr
```

> **نصيحة احترافية:** إذا كنت تعمل داخل بيئة افتراضية (مستحسن جدًا)، فعّلها أولاً للحفاظ على عزل الاعتمادات.

## الخطوة 2: استيراد الوحدة وإنشاء محرك OCR

الآن بعد أن المكتبة متاحة، استوردها وأنشئ كائن `OcrEngine`. فكر في المحرك كالعقل الذي يقوم بكل الأعمال الثقيلة—التعرف على الأحرف، معالجة تخطيطات الصفحات، وإرجاع سلاسل Unicode نظيفة.

```python
# Step 2: Import the Aspose OCR module and create an engine
import aspose.ocr as ocr

engine = ocr.OcrEngine()
```

> **لماذا هذا مهم:** إنشاء المحرك مرة واحدة وإعادة استخدامه عبر الصفحات أكثر كفاءة بكثير من إنشاء محرك جديد لكل صفحة. كما يضمن إعدادات متسقة طوال المستند.

## الخطوة 3: التعرف على جميع صفحات PDF (OCR متعدد الصفحات)

طريقة `recognize_multi_page` في Aspose.OCR تقبل مسار الملف وتعيد قائمة من كائنات `OcrResult`—واحد لكل صفحة. هذه هي جوهر عملية **تحويل PDF إلى نص**.

```python
# Step 3: Run OCR on every page of the PDF
pdf_path = "YOUR_DIRECTORY/contract.pdf"   # replace with your actual file
pdf_pages = engine.recognize_multi_page(pdf_path)  # returns List[OcrResult]
```

> **حالة حافة:** إذا كان ملف PDF محميًا بكلمة مرور، ستحتاج إلى تمرير كلمة المرور عبر `engine.set_password("your_password")` قبل استدعاء `recognize_multi_page`.

## الخطوة 4: التكرار عبر النتائج وعرض معاينة

معاينة سريعة تساعدك على التأكد من أن OCR يلتقط النص فعليًا. سنطبع أول 200 حرف من كل صفحة، ويمكنك تعديل الجزء حسب الحاجة.

```python
# Step 4: Display a short preview of each page’s extracted text
for page_number, page_result in enumerate(pdf_pages, start=1):
    print(f"--- Page {page_number} ---")
    # Show the first 200 characters of the page's OCR text
    print(page_result.text[:200])
    print()  # blank line for readability
```

**نموذج المخرجات**

```
--- Page 1 ---
This Agreement is made on the 1st day of January 2025 between ...

--- Page 2 ---
WHEREAS, the Parties desire to enter into a collaborative ...

--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed this Agreement ...
```

المقتطف أعلاه يعرض جزءًا فقط، لكن النص الكامل موجود داخل `page_result.text`.

## الخطوة 5: دمج جميع الصفحات في ملف نصي واحد (اختياري)

معظم سير العمل اللاحق—فهرسة البحث، تحليل البيانات، أو الأرشفة البسيطة—يفضل ملف `.txt` واحد. لنقم بدمج الصفحات وكتابتها.

```python
# Step 5: Save the complete OCR output to a .txt file
output_path = "YOUR_DIRECTORY/contract_extracted.txt"

with open(output_path, "w", encoding="utf-8") as out_file:
    for page_result in pdf_pages:
        out_file.write(page_result.text)
        out_file.write("\n\n")  # separate pages with a blank line
print(f"All pages saved to {output_path}")
```

> **لماذا يعمل هذا:** استخدام UTF‑8 يضمن عدم فقدان الأحرف الخاصة مثل الحروف المشكّلة أو الرموز التي تظهر غالبًا في المستندات القانونية.

## الخطوة 6: التعامل مع المشكلات الشائعة

| المشكلة | العرض | الحل |
|-------|---------|-----|
| صفحات فارغة في المخرجات | `page_result.text` فارغ | تحقق من أن PDF المصدر يحتوي فعلاً على صور ممسوحة؛ بعض ملفات PDF تكون نصية بالفعل وقد تحتاج إلى نهج مختلف (مثل مكتبات استخراج نص PDF). |
| أحرف مشوهة | رموز غريبة بدل الحروف | تأكد من ضبط لغة محرك OCR بشكل صحيح: `engine.language = ocr.Language.English` (أو لغة أخرى). |
| ملفات PDF كبيرة تستغرق وقتًا طويلاً | يبدو أن السكريبت عالق على صفحة | فعّل المعالجة المتعددة الخيوط: `engine.recognize_multi_page(pdf_path, ocr.RecognizeOptions(parallel=True))`. |
| أخطاء الذاكرة في الملفات الضخمة | حدوث `MemoryError` | عالج PDF على دفعات (مثلاً 50 صفحة في كل مرة) أو زد حد الذاكرة في بايثون. |

## السكريبت الكامل – جاهز للتنفيذ

بتجميع كل ما سبق، إليك السكريبت المتكامل الذي يمكنك نسخه ولصقه في ملف باسم `extract_pdf_text_ocr.py`.

```python
# extract_pdf_text_ocr.py
# Complete python ocr example that extracts PDF text using Aspose OCR.

import aspose.ocr as ocr

def main():
    # 1️⃣ Install the library via `pip install aspose-ocr` before running.
    # 2️⃣ Set the path to your PDF.
    pdf_path = "YOUR_DIRECTORY/contract.pdf"
    output_path = "YOUR_DIRECTORY/contract_extracted.txt"

    # 3️⃣ Create the OCR engine.
    engine = ocr.OcrEngine()
    # Optional: set language for better accuracy.
    # engine.language = ocr.Language.English

    # 4️⃣ Perform multi‑page OCR.
    pdf_pages = engine.recognize_multi_page(pdf_path)

    # 5️⃣ Show a preview of each page.
    for page_number, page_result in enumerate(pdf_pages, start=1):
        print(f"--- Page {page_number} ---")
        print(page_result.text[:200])
        print()

    # 6️⃣ Write the full text to a file.
    with open(output_path, "w", encoding="utf-8") as out_file:
        for page_result in pdf_pages:
            out_file.write(page_result.text)
            out_file.write("\n\n")
    print(f"✅ All pages saved to {output_path}")

if __name__ == "__main__":
    main()
```

شغّله من الطرفية:

```bash
python extract_pdf_text_ocr.py
```

سترى معاينات الصفحات تُطبع على وحدة التحكم، متبوعةً بتأكيد أن النص الكامل تم حفظه.

## ملخص وخطوات مستقبلية

لقد استعرضنا كيفية **استخراج نص PDF باستخدام OCR** عبر مثال **ocr بايثون** مختصر ي **يحوّل PDF إلى نص** بفعالية. الخطوات الأساسية—التثبيت، الاستيراد، إنشاء المحرك، تشغيل `recognize_multi_page`، المعاينة، والحفظ—تشكل معظم سير العمل الشائع للملفات الممسوحة ضوئيًا.

**ما التالي؟**  

- **تحسين الدقة**: جرّب تعديل `engine.recognize_multi_page(..., RecognizeOptions(...))` لضبط DPI أو استخدام حزم لغات إضافية.  
- **معالجة ما بعد الاستخراج**: إزالة الفراغات الزائدة، تشغيل تدقيق إملائي، أو تمرير النص إلى خط أنابيب معالجة لغة طبيعية.  
- **معالجة دفعات**: كرّر العملية على مجلد من ملفات PDF لبناء أرشيف قابل للبحث.  

إذا واجهت أي صعوبة، تأكد من أن PDF يحتوي فعلاً على صور نقطية (OCR يعمل على الصور، وليس على النص المدمج). للملفات التي تحتوي على نص أصلاً، فكر في مكتبات مثل `pdfminer.six` أو `PyMuPDF`.

---

**برمجة سعيدة!** إذا ساعدك هذا الدليل في **استخراج نص PDF باستخدام OCR** لمشروعك، لا تتردد في مشاركة نتائجك في التعليقات، أو فتح مشكلة على صفحة Aspose OCR على GitHub لطلب ميزات. استمر في التجربة، وستحصل قريبًا على خط أنابيب قوي يحول أي PDF ممسوح إلى نص قابل للبحث والتحرير.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة‑بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [استخراج نص الصور – أساسيات OCR مع Aspose.OCR للجاڤا](/ocr/english/java/ocr-basics/)
- [كيفية إجراء OCR لنص الصورة باستخدام اللغة مع Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}