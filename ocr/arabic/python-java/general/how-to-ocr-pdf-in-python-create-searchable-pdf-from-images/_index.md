---
category: general
date: 2026-06-06
description: كيفية التعرف الضوئي على النص في ملفات PDF وإنشاء ملفات PDF قابلة للبحث
  من الصور باستخدام بايثون. تعلم إضافة نص قابل للبحث وتحويل الصورة إلى PDF/A في دقائق.
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: ar
og_description: كيفية تحويل PDF إلى نص باستخدام OCR خطوة بخطوة. تعلم إضافة نص قابل
  للبحث وتحويل الصورة إلى PDF/A باستخدام سكريبت بايثون بسيط.
og_title: كيفية تحويل PDF إلى نص باستخدام OCR – دليل سريع لإنشاء ملفات PDF قابلة للبحث
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: كيفية إجراء OCR لملف PDF باستخدام بايثون – إنشاء ملف PDF قابل للبحث من الصور
url: /ar/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحويل PDF إلى نص قابل للبحث – تحويل الصور الممسوحة ضوئياً إلى ملفات PDF قابلة للبحث

هل تساءلت يومًا **كيف تقوم بعمل OCR لملفات PDF** عندما يكون لديك فقط صورة ممسوحة ضوئيًا لفاتورة أو إيصال؟ لست وحدك. في العديد من المكاتب تصل الأوراق الواردة كملفات PNG أو JPEG مسطحة، والخطوة التالية—جعل المحتوى قابلًا للبحث—تبدو كصندوق أسود.

الخبر السار؟ ببضع أسطر من Python يمكنك **إنشاء ملفات PDF قابلة للبحث**، **إضافة نص قابل للبحث**، وحتى **تحويل الصورة إلى PDF/A** للأرشفة طويلة الأمد. في هذا الدرس سنستعرض كل خطوة، نشرح لماذا هي مهمة، ونزودك بسكريبت جاهز يمكنك وضعه في أي مشروع.

> **نصيحة احترافية:** نفس النهج يعمل مع المسحات متعددة الصفحات؛ فقط قم بتكرار العملية على الملفات والمحرك سيتولى الجزء الثقيل.

---

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي على جهازك:

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| Python 3.9 أو أحدث | صsyntax حديث ودعم أفضل للمكتبات |
| محرك OCR قائم على `pdfium` (مثل `pdfocr` أو SDK تجاري) | يتعامل مع كل من التعرف على الصور وتوليد PDF/A |
| ملف صورة (PNG, JPEG, TIFF) تريد تحويله إلى PDF قابل للبحث | مصدر النص |
| صلاحية كتابة إلى مجلد الإخراج | حتى يتمكن السكريبت من حفظ ملف PDF الجديد |

إذا لم تقم بتثبيت SDK الخاص بـ OCR بعد، نفّذ:

```bash
pip install pdfocr   # replace with your vendor's package name
```

هذا كل شيء—بدون تبعيات نظام معقدة، مجرد تثبيت عبر pip.

---

## كيف تقوم بعمل OCR لملف PDF – نظرة عامة

على مستوى عالٍ، تتكون العملية من ثلاث إجراءات بسيطة:

1. **التعرف** على النص داخل الصورة مع الحفاظ على الرسومات الأصلية.  
2. **تصدير** نتيجة OCR مع الصورة الأصلية كـ **PDF/A قابل للبحث** (نسخة PDF الصديقة للأرشفة).  
3. **التحقق** من أن الملف الناتج يحتوي على نص قابل للتحديد والبحث فوق الصورة الأصلية.

سترى أدناه كل خطوة في الكود، مع شرح *السبب* وراء الأوامر.

---

## الخطوة 1: التعرف على النص من الصورة

أولًا نطلب من محرك OCR قراءة البكسلات وإرجاع كائن نتيجة يحتوي على كل من الصورة الخام والنص المستخرج. فكر فيه كأن المحرك “يقرأ” الفاتورة لك.

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### لماذا هذا مهم

- **الحفاظ على الرسومات** يعني أن التخطيط البصري (الجداول، الشعارات، الأختام) يبقى تمامًا كما التقطه الماسح.  
- عادةً يحتوي كائن `result` على طبقة نص مخفية سندمجها لاحقًا في PDF.  
- استخدام `recognize_image` بدلاً من `recognize_pdf` يتجنب خطوة تحويل إضافية، مما يسرّع المعالجة للصور ذات الصفحة الواحدة.

#### تنوعات شائعة

- إذا كان لديك **TIFF متعدد الصفحات**، مرّر مسار الملف مباشرة؛ معظم المحركات ستعامل كل صفحة كصورة منفصلة.  
- بالنسبة لملفات PDF التي تحتوي بالفعل على صور، يمكنك استدعاء `engine.recognize_pdf("file.pdf")` وتجاوز هذه الخطوة تمامًا.

---

## الخطوة 2: تصدير نتيجة OCR كـ PDF/A قابل للبحث

الآن نأخذ الـ `result` من الخطوة 1 ونخبر المحرك بكتابة ملف جديد. العلامة المفتاحية هنا هي *PDF/A*—الإصدار المعياري ISO من PDF المصمم للحفظ طويل الأمد.

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### لماذا هذا مهم

- **PDF قابل للبحث**: يحتوي الملف الناتج على طبقة نص مخفية قابلة للتحديد. يمكنك الآن الضغط على Ctrl + F للبحث داخل المستند.  
- **امتثال PDF/A**: بعض المؤسسات (القانونية، المالية) تتطلب PDF/A لسجلات التدقيق؛ هذه الخطوة تلبي ذلك تلقائيًا.  
- الطريقة أيضًا **تضيف نصًا قابلًا للبحث** دون تسطيح الصورة، لذا يبقى الوضوح البصري مثالياً.

#### حالة خاصة: هل تحتاج إلى PDF عادي بدلاً من PDF/A؟

إذا لم تكن مهتمًا بـ PDF/A، استبدل `save_as_pdfa` بـ `save_as_pdf`. يبقى باقي سير العمل كما هو.

---

## الخطوة 3: التحقق من PDF القابل للبحث

فحص سريع يحمّيك من الأخطاء الغامضة لاحقًا. افتح الملف المُولد في أي عارض PDF، حاول تحديد كلمة، واستخدم وظيفة البحث.

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### النتيجة المتوقعة

عند تشغيل السكريبت، سيطبع الطرفية:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

عند فتح الملف، يجب أن ترى صورة الفاتورة الأصلية مع طبقة نص خفيفة غير مرئية. حدد أي كلمة وستلاحظ أنها قابلة للتحديد—**هذا هو النص القابل للبحث** الذي أضفته للتو.

---

## إضافة نص قابل للبحث إلى ملفات PDF موجودة (إضافة)

أحيانًا يكون لديك PDF بالفعل وتحتاج إلى **إضافة نص قابل للبحث** إليه. يمكن لنفس المحرك أن يدمج نتائج OCR فوق PDF موجود:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

هنا يقوم `apply_to` بدمج الطبقة المخفية مع الصفحات الأصلية، مما يتيح لك **إنشاء PDF قابل للبحث** دون الحاجة لإعادة المسح.

---

## الأخطاء الشائعة والنصائح

| الخطأ | كيفية تجنبه |
|---------|-----------------|
| **صور المصدر منخفضة الدقة** (< 150 dpi) | قم بزيادة الدقة أو اطلب مسحًا بدقة أعلى؛ دقة OCR تنخفض بشكل كبير تحت 150 dpi. |
| **غياب بيانات اللغة** | ثبّت حزم اللغة المناسبة لمحرك OCR الخاص بك (`pip install pdfocr[eng,spa]`). |
| **مجلد الإخراج غير قابل للكتابة** | شغّل السكريبت بصلاحيات كافية أو اختر دليلًا مختلفًا. |
| **فشل التحقق من PDF/A** | تأكد من عدم تضمين خطوط غير مدعومة أو JavaScript؛ معظم SDKs تتعامل مع ذلك تلقائيًا عند استخدام `save_as_pdfa`. |

---

## السكريبت الكامل – حل بملف واحد

فيما يلي سكريبت مستقل يربط كل شيء معًا. انسخه، استبدل مسارات العناصر النائبة، وستكون جاهزًا **لتحويل الصورة إلى PDF/A** في ثوانٍ.

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**ما يفعله هذا السكريبت:**  
1. يحمّل محرك OCR.  
2. يقرأ الصورة المختارة ويستخرج النص.  
3. يكتب **PDF/A قابل للبحث** يمكنك توزيعه أو أرشفته فورًا.  

لا تتردد في تغليف منطق `main` داخل دالة تعالج مجلدًا كاملًا—فقط كرّر `os.listdir()` وطبق الخطوات الثلاث على كل ملف.

---

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن أتقنت **كيفية عمل OCR لملفات PDF**، فكر في استكشاف الأفكار التالية:

- **المعالجة الدفعة:** استخدم `concurrent.futures` لعمل OCR على عشرات الفواتير بالتوازي.  
- **إدخال البيانات الوصفية:** أضف تواريخ الإنشاء أو أرقام الفواتير إلى بيانات PDF الوصفية لتسهيل الفهرسة.  
- **PDFs هجينة:** اجمع النص القابل للبحث مع الصور الأصلية المدمجة للحصول على “نسخة رقمية” من المستند الورقي.  
- **مخرجات بديلة:** صدّر إلى **DOCX** أو **HTML** إذا كانت الأنظمة اللاحقة تحتاج صيغًا قابلة للتحرير.

كل من هذه الأفكار يبني على المفاهيم الأساسية التي تعلمتها—التعرف، التصدير، والتحقق.

---

## الخلاصة

باختصار، الآن تعرف **كيفية عمل OCR لملفات PDF** عن طريق تحويل صورة بسيطة إلى **PDF/A قابل للبحث** باستخدام بضعة أسطر من Python. يتولى السكريبت الجزء الثقيل، يحافظ على الرسومات الأصلية، ويعطيك مستندًا متوافقًا مع المعايير يمكنك البحث فيه، أرشفته أو مشاركته.  

جرّبه على فواتيرك، إيصالاتك، أو عقودك الممسوحة. إذا واجهت أي صعوبات، اترك تعليقًا أدناه أو راجع الوثائق الرسمية للـ SDK—غالبًا ما تكون مليئة بأمثلة إضافية. Happy coding, and enjoy the newfound ability to make any image instantly searchable! 

![مثال على كيفية OCR PDF يظهر الصورة الأصلية وطبقة PDF القابلة للبحث](placeholder.png "مثال على كيفية OCR PDF")

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شرح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف طرق تنفيذ بديلة في مشاريعك.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}