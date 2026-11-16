---
category: general
date: 2026-05-31
description: تعلم كيفية تحويل الصور إلى نص باستخدام بايثون مع سكريبت تحويل الصور إلى
  نص بالجملة. استخرج النص من الصور الممسوحة ضوئياً باستخدام Aspose.OCR في دقائق.
draft: false
keywords:
- convert images to text python
- bulk image to text conversion
- recognize text from scanned images
language: ar
og_description: تحويل الصور إلى نص باستخدام بايثون فورًا. يوضح هذا الدليل تحويل الصور
  إلى نص بشكل جماعي وكيفية التعرف على النص من الصور الممسوحة ضوئيًا باستخدام Aspose.OCR.
og_title: تحويل الصور إلى نص بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to convert images to text python with a bulk image to text
    conversion script. Recognize text from scanned images using Aspose.OCR in minutes.
  headline: Convert Images to Text Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to convert images to text python with a bulk image to text
    conversion script. Recognize text from scanned images using Aspose.OCR in minutes.
  name: Convert Images to Text Python – Complete Step‑by‑Step Guide
  steps:
  - name: Imports the OCR engine classes.
    text: Imports the OCR engine classes.
  - name: Instantiates a `BatchOcrEngine`.
    text: Instantiates a `BatchOcrEngine`.
  - name: Points the engine at an input folder of images.
    text: Points the engine at an input folder of images.
  - name: Directs the engine to write each extracted text file into an output folder.
    text: Directs the engine to write each extracted text file into an output folder.
  - name: Fires the `recognize()` method, which **recognize text from scanned images**
      one by one.
    text: Fires the `recognize()` method, which **recognize text from scanned images**
      one by one.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: تحويل الصور إلى نص بايثون – دليل كامل خطوة بخطوة
url: /ar/python-java/general/convert-images-to-text-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصور إلى نص بايثون – دليل شامل خطوة‑بخطوة

هل تساءلت يومًا كيف **convert images to text python** دون البحث عن عشرات المكتبات؟ لست وحدك. سواء كنت تقوم برقمنة الإيصالات القديمة، أو استخراج البيانات من الفواتير الممسوحة ضوئيًا، أو بناء أرشيف PDF قابل للبحث، فإن تحويل الصور إلى ملفات نصية عادية هو مهمة يومية للعديد من المطورين.

في هذا الدرس سنستعرض خط أنابيب **bulk image to text conversion** يتعرف على النص من الصور الممسوحة، ويحفظ كل نتيجة كملف `.txt` منفصل، وكل ذلك ببضع أسطر من بايثون فقط. لا حاجة للبحث عن واجهات برمجة تطبيقات غامضة—Aspose.OCR يتولى الجزء الأكبر، وسنوضح لك بالضبط كيفية ربطه.

## ما ستتعلمه

- كيفية تثبيت وتكوين حزمة Aspose.OCR للبايثون.  
- الكود الدقيق المطلوب **convert images to text python** باستخدام `BatchOcrEngine`.  
- نصائح للتعامل مع المشكلات الشائعة مثل الصيغ غير المدعومة أو الملفات التالفة.  
- طرق للتحقق من أن خطوة **recognize text from scanned images** نجحت فعليًا.  

بنهاية هذا الدليل ستحصل على سكريبت جاهز للتنفيذ يمكنه معالجة آلاف الصور دفعة واحدة—مثالي لأي سيناريو معالجة دفعات.

## المتطلبات المسبقة

- Python 3.8+ مثبت على جهازك.  
- مجلد يحتوي على ملفات صور (PNG, JPEG, TIFF, إلخ) تريد تحويلها إلى نص.  
- حساب Aspose Cloud نشط أو ترخيص تجريبي مجاني (الطبقة المجانية كافية للاختبار).  

إذا كان لديك كل ذلك، لنبدأ.

---

## الخطوة 1 – إعداد بيئة بايثون

قبل أن نكتب أي كود OCR، تأكد من أنك تعمل داخل بيئة افتراضية نظيفة. هذا يعزل الاعتمادات ويمنع تعارض الإصدارات.

```bash
# Create a new virtual environment named venv
python -m venv venv

# Activate the environment (Windows)
venv\Scripts\activate

# Activate the environment (macOS / Linux)
source venv/bin/activate
```

> **نصيحة احترافية:** حافظ على تنظيم دليل المشروع—أنشئ مجلدًا فرعيًا باسم `ocr_project` وضع السكريبت هناك. سيسهل ذلك التعامل مع المسارات لاحقًا.

## الخطوة 2 – تثبيت Aspose.OCR للبايثون

Aspose.OCR مكتبة تجارية، لكنها تُوزَّع بحزمة wheel مجانية على نمط NuGet يمكنك سحبها من PyPI. نفّذ الأمر التالي داخل البيئة الافتراضية المُفعَّلة:

```bash
pip install aspose-ocr
```

إذا واجهت خطأ في الصلاحيات، أضف العلامة `--user` أو نفّذ الأمر باستخدام `sudo` (Linux/macOS فقط). بعد التثبيت يجب أن ترى شيئًا مشابهًا لـ:

```
Successfully installed aspose-ocr-23.9.0
```

> **لماذا Aspose؟** على عكس العديد من أدوات OCR المفتوحة، يدعم Aspose.OCR **bulk image to text conversion** مباشرةً ويتعامل مع مجموعة واسعة من صيغ الصور دون إعداد إضافي. كما يوفر فئة `BatchOcrEngine` التي تجعل مهمة “convert images to text python” عملية سطر واحد.

## الخطوة 3 – تحويل الصور إلى نص بايثون باستخدام Batch OCR

الآن نصل إلى جوهر الدرس. السكريبت التالي قابل للتنفيذ بالكامل ويقوم بـ:

1. استيراد فئات محرك OCR.  
2. إنشاء كائن `BatchOcrEngine`.  
3. توجيه المحرك إلى مجلد إدخال يحتوي على الصور.  
4. تحديد مجلد إخراج لكتابة كل ملف نصي مستخرج.  
5. تشغيل طريقة `recognize()` التي **recognize text from scanned images** واحدة تلو الأخرى.  

احفظ ما يلي باسم `batch_ocr.py` داخل مجلد مشروعك:

```python
# batch_ocr.py
# -------------------------------------------------
# Bulk Image to Text Conversion using Aspose.OCR
# -------------------------------------------------

# Step 1: Import the OCR engine classes
from asposeocr import BatchOcrEngine, OcrEngine

# Step 2: Create a batch OCR engine instance
batch_engine = BatchOcrEngine()

# Step 3: Set the folder that contains the images to be processed
# Replace 'YOUR_DIRECTORY' with the absolute path to your images folder
batch_engine.input_folder = "YOUR_DIRECTORY/input_images"

# Step 4: Set the folder where the extracted text files will be saved
# Make sure this folder exists or Aspose will raise an error
batch_engine.output_folder = "YOUR_DIRECTORY/output_texts"

# Optional: Adjust OCR settings if you need higher accuracy
# For example, enable language detection for multilingual documents
# batch_engine.ocr_engine.language = "eng+spa"  # English + Spanish

# Step 5: Run the batch recognition – each supported image in the input folder is processed
batch_engine.recognize()

# Step 6: Notify that the batch operation has finished
print("Batch processing complete. Text files saved to YOUR_DIRECTORY/output_texts.")
```

### كيف يعمل

- **`BatchOcrEngine`** يلف فئة `OcrEngine` العادية لكنه يضيف تنسيقًا على مستوى المجلد، وهو ما تحتاجه تمامًا عندما تريد **convert images to text python** على نطاق واسع.  
- خاصية `input_folder` تخبر المحرك أين يبحث عن الصور المصدرية. يقوم تلقائيًا بمسح الدليل وتحديد كل ملف مدعوم.  
- خاصية `output_folder` تحدد أين تُحفظ كل ملفات `.txt`. يطابق المحرك اسم الملف الأصلي، فمثلاً `receipt1.png` يصبح `receipt1.txt`.  
- استدعاء `recognize()` يُشغِّل الحلقة الداخلية التي تُحمِّل كل صورة، تُجري OCR، وتكتب النتيجة. الطريقة تُبقي التنفيذ محجوزًا حتى تُعالج جميع الملفات، مما يسهل ربط إجراءات أخرى (مثل ضغط مجلد الإخراج).

#### النتيجة المتوقعة

عند تشغيل السكريبت:

```bash
python batch_ocr.py
```

ستظهر لك:

```
Batch processing complete. Text files saved to YOUR_DIRECTORY/output_texts.
```

داخل `output_texts` ستجد ملف نصي عادي لكل صورة. افتح أيًا منها بمحرر نص وسترى نتيجة OCR الخام—عادةً ما تكون تقريبًا قريبًا من النص المطبوع الأصلي.

## الخطوة 4 – التحقق من النتائج ومعالجة الأخطاء

حتى أفضل محركات OCR قد تتعثر مع مسحات منخفضة الدقة أو صفحات مائلة بشدة. إليك طريقة سريعة للتحقق من صحة المخرجات وتسجيل أي فشل.

```python
import os

def verify_output(output_dir):
    txt_files = [f for f in os.listdir(output_dir) if f.lower().endswith('.txt')]
    empty_files = [f for f in txt_files if os.path.getsize(os.path.join(output_dir, f)) == 0]

    if empty_files:
        print("Warning: The following files are empty – OCR may have failed:")
        for f in empty_files:
            print(f"  • {f}")
    else:
        print("All text files contain data. OCR succeeded for every image.")

# Run verification after batch processing
verify_output(batch_engine.output_folder)
```

**لماذا نضيف هذا؟**  
- يلتقط الحالات التي ينتج فيها المحرك سلسلة فارغة صامتًا (شائع مع الصور غير القابلة للقراءة).  
- يمنحك قائمة بالملفات الإشكالية لتفحصها يدويًا أو تعيد تشغيلها بإعدادات مختلفة (مثل زيادة خيارات `OcrEngine.preprocess`).  

### الحالات الخاصة والتعديلات

| الحالة | الحل المقترح |
|-----------|----------------|
| الصور مدارة بزاوية 90° | اضبط `batch_engine.ocr_engine.rotation_correction = True`. |
| لغات مختلطة (إنجليزي + فرنسي) | استخدم `batch_engine.ocr_engine.language = "eng+fra"` قبل `recognize()`. |
| ملفات PDF ضخمة تم تحويلها إلى صور أولًا | قسّم ملفات PDF إلى صور صفحة واحدة، ثم مرّر المجلد إلى المحرك الدفعي. |
| أخطاء الذاكرة في دفعات كبيرة جدًا | عالج مجلدات فرعية أصغر بشكل متسلسل، أو زد `batch_engine.max_memory_usage`. |

## الخطوة 5 – أتمتة سير العمل بالكامل (اختياري)

إذا كنت تحتاج لتشغيل هذا التحويل كل ليلة، غلف السكريبت بملف شل بسيط أو ملف دفعي Windows، وجدوله باستخدام `cron` (Linux/macOS) أو Task Scheduler (Windows). إليك مثالًا بسيطًا لملف `run_ocr.sh` للأنظمة الشبيهة بـ Unix:

```bash
#!/usr/bin/env bash
# run_ocr.sh – Automate bulk image to text conversion

# Activate virtual environment
source /path/to/venv/bin/activate

# Execute the OCR script
python /path/to/ocr_project/batch_ocr.py

# Deactivate after completion
deactivate
```

اجعل الملف قابلًا للتنفيذ (`chmod +x run_ocr.sh`) وأضف إدخالًا إلى cron:

```cron
0 2 * * * /path/to/run_ocr.sh >> /var/log/ocr_batch.log 2>&1
```

سيقوم هذا بتشغيل التحويل كل يوم في الساعة 2 صباحًا ويسجل أي مخرجات للمراجعة لاحقًا.

---

## الخلاصة

أصبح لديك الآن طريقة مثبتة وجاهزة للإنتاج **convert images to text python** باستخدام `BatchOcrEngine` من Aspose.OCR. يتعامل السكريبت مع **bulk image to text conversion**، يكتب كل نتيجة إلى ملف مخصص، ويتضمن خطوات تحقق لضمان أنك فعليًا **recognize text from scanned images** بشكل صحيح.

من هنا يمكنك:

- تجربة إعدادات OCR مختلفة (حزم اللغات، تصحيح الميل، تقليل الضوضاء).  
- تمرير النص المُولد إلى فهرس بحث مثل Elasticsearch للبحث النصي الفوري.  
- دمج هذا الخط الأنابيب مع أدوات تحويل PDF لمعالجة ملفات PDF الممسوحة ضوئيًا دفعة واحدة.  

هل لديك أسئلة، أو لاحظت مشكلة مع نوع ملف معين؟ اترك تعليقًا أدناه، ولنحلها معًا. برمجة سعيدة، ونتمنى أن تكون عمليات OCR سريعة وخالية من الأخطاء!

## ماذا تتعلم بعد ذلك؟

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}