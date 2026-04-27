---
category: general
date: 2026-04-26
description: كيفية تنفيذ OCR دفعي لمستنداتك واستخراج النص من المسحات الضوئية باستخدام
  بايثون. تعلم معالجة الدفعات خطوة بخطوة مع OcrEngine للحصول على مخرجات بصيغة JSON.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: ar
og_description: كيفية تنفيذ OCR دفعي لملفاتك الممسوحة واستخراج النص من المسحات في
  سكريبت واحد. الكود الكامل، النصائح، ومعالجة الحالات الخاصة.
og_title: كيفية تنفيذ OCR دفعيًا – دليل بايثون السريع
tags:
- OCR
- Python
- Automation
title: كيفية تنفيذ التعرف الضوئي على الحروف على دفعات – استخراج النص من المسحات بفعالية
url: /ar/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تقوم بعملية OCR دفعة واحدة – استخراج النص من المسح الضوئي بفعالية

هل تساءلت يوماً **كيف تقوم بعملية OCR دفعة واحدة** على جبل من ملفات PDF الممسوحة دون أن تفقد أعصابك؟ لست وحدك—المطورون يسألون باستمرار، *“كيف يمكنني استخراج النص من المسحات الضوئية مرة واحدة؟”* الخبر السار هو أن بضع أسطر من بايثون يمكن أن تحول هذه المهمة المملة إلى خط أنابيب آلي سلس.

في هذا الدرس سنستعرض حلًا كاملاً جاهزًا للتنفيذ **يستخرج النص من المسحات الضوئية**، يحفظ النتائج بصيغة JSON، ويعطيك فحصًا سريعًا في النهاية. لا خدمات خارجية، لا سحر—فقط بايثون عادي، فئة `OcrEngine`، وقليل من التعامل مع المجلدات.

## ما ستحصل عليه بعد الانتهاء

- سكربت كامل الوظيفة **يقوم بعملية OCR دفعة واحدة** على أي مجلد من الصور.
- شروحات واضحة *لماذا* يوجد كل سطر، وليس فقط *ماذا* يفعل.
- نصائح للتعامل مع المجلدات الفارغة، الملفات غير الصورية، والدفعات الكبيرة.
- طريقة للتحقق من أن مخرجات JSON تحتوي فعليًا على النص المستخرج.

### المتطلبات المسبقة (الحد الأدنى)

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| Python 3.8+ | الصياغة الحديثة وتلميحات الأنواع |
| مكتبة `OcrEngine` (أو غلاف متوافق) | الوظيفة الأساسية للـ OCR |
| دليل يحتوي على ملفات صور ممسوحة (PNG, JPG, TIFF) | بيانات الإدخال |
| صلاحيات كتابة لمجلد الإخراج | حفظ نتائج JSON |

إذا كان لديك هذه المتطلبات، رائع—لنبدأ.

![how to batch OCR workflow](image-placeholder.png){alt="مخطط سير عمل OCR دفعة واحدة"}

## الخطوة 1 – تهيئة محرك OCR (كيف تقوم بعملية OCR دفعة واحدة)

قبل أن نتمكن من معالجة أي شيء، نحتاج إلى مثال (instance) من محرك OCR. فكر فيه كـ “العقل” الذي سيقرأ كل صورة ويُخرج النص. تهيئته مرة واحدة وإعادة استخدامها عبر الدفعة كلها هو النمط الأكثر كفاءة.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **لماذا نعيد استخدام نفس المثيل؟**  
> إنشاء محرك جديد لكل ملف سيؤدي إلى تحميل نماذج ثقيلة في الذاكرة مرارًا، مما يبطئ الدفعة بشكل كبير. المثيل الواحد يبقي النموذج في الذاكرة ويسمح لك بمعالجة آلاف الصور دون تباطؤ ملحوظ.

## الخطوة 2 – تحديد مسار مجلد المسحات الضوئية (استخراج النص من المسحات الضوئية)

مسحاتك موجودة في مكان ما على القرص. دعنا نخبر السكربت أين يجدها. استخدام المسارات المطلقة يتجنب مفاجآت “الملف غير موجود” عندما يُشغل السكربت من دليل عمل مختلف.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **نصيحة احترافية:**  
> إذا كنت على نظام Windows، فإن الشرطات المائلة (`/`) تعمل بشكل جيد مع `os.path.abspath`، لذا لا تحتاج إلى الهروب من الشرطات العكسية.

## الخطوة 3 – اختيار مكان حفظ نتائج JSON

من المحتمل أنك تريد مجلدًا منظمًا لنتائج OCR. إبقاء المخرجات منفصلة عن المصدر يجعل من السهل تنظيفها لاحقًا أو تمرير JSON إلى خط أنابيب آخر.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **لماذا ننشئ المجلد برمجيًا؟**  
> يضمن ذلك أن السكربت لن يتعطل إذا كان الدليل غير موجود، وتُجعل الخاصية `exist_ok=True` العملية غير متكررة—يمكن تشغيل السكربت عدة مرات دون أخطاء.

## الخطوة 4 – تشغيل عملية الدفعة (كيف تقوم بعملية OCR دفعة واحدة)

الآن نصل إلى جوهر الموضوع: إخبار `ocr_engine` بالمرور على كل ملف في `input_dir`، تشغيل OCR، وإسقاط JSON في `output_dir`. علم `format="json"` يُخبر المحرك بترميز النتيجة بطريقة منظمة يحبها الأدوات اللاحقة.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### ما الذي يحدث خلف الكواليس؟

1. **اكتشاف الملفات** – يقوم المحرك بمسح `input_folder` بصورة متكررة، متجاهلًا الملفات المخفية.
2. **تحقق من صحة الملف** – تُرسل فقط امتدادات الصور المدعومة (`.png`, `.jpg`, `.tif`, إلخ) إلى نموذج OCR.
3. **تنفيذ OCR** – تُرسل كل صورة إلى محرك OCR؛ يُلتقط النص، درجات الثقة، وبيانات التخطيط.
4. **ترميز JSON** – تُكتب النتيجة في ملف يحمل نفس الاسم الأساسي لكن بامتداد `.json` داخل `output_folder`.

> **معالجة الحالات الخاصة:**  
> - **مجلد فارغ:** يسجل المحرك “No files found” ويعود بنعومة.  
> - **صورة تالفة:** يتخطى الملف، يسجل إدخال خطأ في `batch_errors.log`، ويستمر.  
> - **دفعة ضخمة (أكثر من 10k ملف):** يبقى استهلاك الذاكرة منخفضًا لأن كل صورة تُعالج بشكل مستقل.

## الخطوة 5 – تأكيد انتهاء التحويل

عبارة `print` بسيطة تعطي تغذية راجعة فورية في وحدة التحكم. في خطوط الأنابيب الإنتاجية قد تستبدلها بنداء تسجيل (logging) أو إشعار بريد إلكتروني.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

عند رؤية هذا السطر، يمكنك فحص مجلد `json_output` بأمان. كل ملف JSON سيبدو تقريبًا هكذا:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

يمكنك الآن تمرير هذه الملفات JSON إلى قاعدة بيانات، فهرس بحث، أو أي أداة تحليلية لاحقة.

## الأسئلة المتكررة (مع إجابات سريعة)

**س: ماذا لو احتجت لمعالجة ملفات PDF بدلاً من الصور؟**  
ج: حوّل كل صفحة PDF إلى صورة أولًا (مثلاً باستخدام `pdf2image`) وضع ملفات PNG/JPG الناتجة في `input_dir`. منطق OCR الدفعي يبقى دون تغيير.

**س: هل يمكنني تغيير صيغة الإخراج إلى نص عادي؟**  
ج: بالتأكيد. استبدل `format="json"` بـ `format="txt"` وسيكتب المحرك ملف `.txt` يحتوي فقط على النص المستخرج.

**س: مسحاتي موجودة في عدة مجلدات فرعية—هل السكربت يتعمق؟**  
ج: نعم. `batch_process` يتجول في شجرة الدليل افتراضيًا. إذا أردت مخرجات مسطحة، اضبط `flatten=True` (إذا كانت المكتبة تدعم ذلك) أو عالج أسماء ملفات JSON لاحقًا.

**س: كيف أتعامل مع النصوص غير اللاتينية؟**  
ج: ابدأ `OcrEngine` بمعامل لغة، مثل `OcrEngine(lang="spa+eng")`. حلقة الدفعة نفسها لا تحتاج أي تعديل.

## نصائح احترافية ومخاطر شائعة

- **حجم الدفعة مهم:** إذا لاحظت ارتفاعًا في استهلاك المعالج، قلل السرعة باستخدام `time.sleep(0.1)` بين الملفات.
- **التسجيل:** استبدل نداء `print` بوحدة `logging` في بايثون لتسجيل الطوابع الزمنية ومستويات الأخطاء.
- **تصادم أسماء الملفات:** إذا كان لملفين مسح ضوئي نفس الاسم الأساسي لكن في مجلدات فرعية مختلفة، قد تُستبدل ملفات JSON بعضها البعض. أضف تجزئة (hash) للمسار النسبي إلى اسم الإخراج لتجنب ذلك.
- **تسرب الذاكرة:** بعض محركات OCR تحتفظ بموارد أصلية. استدعِ `ocr_engine.close()` في نهاية السكربت إذا وفرت المكتبة طريقة تنظيف.

## السكربت الكامل – جاهز للنسخ واللصق

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**الناتج المتوقع في وحدة التحكم**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

يمكنك التحقق من JSON بفتح أي ملف في `json_output` باستخدام محرر نصوص أو بتحميله في بايثون:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

سترى النص الخام المستخرج من OCR يُطبع في وحدة التحكم.

## الخلاصة

لقد غطينا الآن **كيفية تنفيذ OCR دفعة واحدة** على دليل كامل من الصور الممسوحة و**استخراج النص من المسحات الضوئية** إلى ملفات JSON نظيفة قابلة للقراءة آليًا. النهج بسيط عمدًا: إعداد المحرك مرة واحدة، توجيهه إلى مجلد، وترك المكتبة تتولى العمل الشاق. من هنا يمكنك:

- ربط JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}