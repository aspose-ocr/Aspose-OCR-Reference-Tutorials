---
category: general
date: 2026-04-29
description: تعلم كيفية تشغيل OCR على مسحاتك، واستخدام نموذج Hugging Face تلقائيًا،
  والتعرف على النص من المسحات باستخدام Aspose OCR في دقائق.
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: ar
og_description: كيفية تشغيل OCR على المسحات باستخدام Aspose OCR، وتحميل نموذج من Hugging
  Face تلقائيًا، والحصول على نص نظيف ومُعَلَّم بعلامات الترقيم.
og_title: كيفية تشغيل OCR باستخدام Aspose و Hugging Face – دليل كامل
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: كيفية تشغيل OCR باستخدام Aspose و Hugging Face – دليل كامل
url: /ar/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تشغّل OCR باستخدام Aspose & Hugging Face – دليل كامل

هل تساءلت يومًا **كيف تشغّل OCR** على مجموعة من المستندات الممسوحة ضوئيًا دون قضاء ساعات في تعديل الإعدادات؟ لست وحدك. في العديد من المشاريع، يحتاج المطورون إلى **التعرف على النص من المسحات** بسرعة، لكنهم يواجهون صعوبات في تنزيل النماذج ومعالجة ما بعد الاستخراج.  

خبر سار: هذا الدرس يوضح لك حلًا جاهزًا للتنفيذ **يستخدم نموذجًا من Hugging Face**، يقوم بتنزيله تلقائيًا، ويضيف علامات الترقيم بحيث يبدو الناتج كأنه كتب بواسطة إنسان. في النهاية، ستحصل على سكريبت يعالج كل صورة في مجلد وينتج ملف `.txt` نظيف بجانب كل مسح.

## ما الذي ستحتاجه

- Python 3.8+ (الكود يستخدم f‑strings، لذا الإصدارات الأقدم لن تعمل)
- حزمة `aspose-ocr` (تثبيت عبر `pip install aspose-ocr`)
- اتصال بالإنترنت لتنزيل النموذج للمرة الأولى  
- مجلد يحتوي على مسحات صور (`.png`، `.jpg` أو `.tif`)

هذا كل شيء—لا حاجة لملفات تنفيذية إضافية، ولا تعديل يدوي للنماذج. هيا نبدأ.

![مثال على تشغيل OCR](https://example.com/ocr-demo.png "مثال على تشغيل OCR")

## الخطوة 1: استيراد فئات Aspose OCR وإعداد البيئة

نبدأ بسحب الفئات الضرورية من مكتبة Aspose OCR. استيراد كل شيء في البداية يبقي السكريبت منظمًا ويسهل اكتشاف الاعتمادات المفقودة.

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*لماذا هذا مهم*: `OcrEngine` يقوم بالعمل الشاق، بينما `AsposeAI` يتيح لنا ربط نموذج لغة كبير لمعالجة ما بعد الاستخراج بشكل أذكى. إذا تخطيت الاستيراد، لن يتم تجميع باقي الكود—لذا لا تنساه.

## الخطوة 2: تكوين نموذج Hugging Face يدعم الـ GPU  

الآن نخبر Aspose من أين يجلب النموذج وعدد الطبقات التي يجب تشغيلها على الـ GPU. العلامة `allow_auto_download="true"` تقوم بـ **تنزيل النموذج تلقائيًا** نيابةً عنك.

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **نصيحة احترافية**: إذا لم يكن لديك GPU، اضبط `gpu_layers=0`. سيتحول النموذج إلى CPU، وهو أبطأ لكنه لا يزال يعمل.

### لماذا نختار نموذج Hugging Face؟

يستضيف Hugging Face مجموعة ضخمة من النماذج الجاهزة للاستخدام. بالإشارة إلى `Qwen/Qwen2.5-3B-Instruct-GGUF` تحصل على نموذج مضغوط ومُدرب على التعليمات يمكنه إضافة علامات الترقيم، تصحيح المسافات، وحتى إصلاح أخطاء OCR الصغيرة. هذا هو جوهر **استخدام نموذج Hugging Face** في التطبيق العملي.

## الخطوة 3: تهيئة محرك الذكاء الاصطناعي وتمكين معالجة الترقيم بعد الاستخراج  

محرك الذكاء الاصطناعي ليس فقط للدردشة الفاخرة—هنا نرفق *مضيف الترقيم* الذي ينظف مخرجات OCR الخام.

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*ما الذي يحدث؟* استدعاء `set_post_processor` يسجل معالجًا مدمجًا يُنفّذ بعد انتهاء محرك OCR. يأخذ السلسلة الخام ويضيف الفواصل، النقاط، والحروف الكبيرة في المواضع المناسبة، مما يجعل النص النهائي أكثر قابلية للقراءة.

## الخطوة 4: إنشاء محرك OCR وربط محرك الذكاء الاصطناعي  

ربط محرك الذكاء الاصطناعي بمحرك OCR يمنحنا كائنًا واحدًا يمكنه قراءة الأحرف وتلميع النتيجة في آنٍ واحد.

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

إذا تخطيت هذه الخطوة، سيظل OCR يعمل، لكنك ستفقد تحسين الترقيم—وسيظهر الناتج كسلسلة من الكلمات المتصلة.

## الخطوة 5: معالجة كل صورة في مجلد  

هذا هو جوهر الدرس. نمر على كل صورة، نشغّل OCR، نطبق معالج ما بعد الاستخراج، ونكتب النص المنقّح إلى ملف `.txt` موازٍ.

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### ما الذي تتوقعه

تشغيل السكريبت يطبع شيئًا مثل:

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

كل سطر يوضح درجة الثقة (فحص سريع للصحة) وينشئ ملفات مثل `invoice_001.png.txt`، `receipt_2024.tif.txt`، إلخ، تحتوي على نص مُرقّم وقابل للقراءة البشرية.

### الحالات الخاصة والبدائل

- **مسحات غير إنجليزية**: غيّر `hugging_face_repo_id` إلى نموذج متعدد اللغات (مثال: `microsoft/Multilingual-LLM-GGUF`).
- **دفعات كبيرة**: غلف الحلقة داخل `concurrent.futures.ThreadPoolExecutor` للمعالجة المتوازية، لكن احرص على حدود ذاكرة الـ GPU.
- **معالجة ما بعد مخصصة**: استبدل `"punctuation_adder"` بالسكريبت الخاص بك إذا كنت تحتاج إلى تنظيف مخصص (مثال: إزالة أرقام الفواتير).

## الخطوة 6: تنظيف الموارد  

عند انتهاء المهمة، تحرير الموارد يمنع تسرب الذاكرة، وهو أمر مهم خاصة إذا كنت تشغّل هذا داخل خدمة طويلة الأمد.

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

إهمال هذه الخطوة قد يترك ذاكرة الـ GPU محجوزة، مما سيعطل عمليات التشغيل اللاحقة.

## ملخص: كيف تشغّل OCR من البداية إلى النهاية  

في بضع أسطر فقط، أظهرنا **كيفية تشغيل OCR** على مجلد من المسحات، **استخدام نموذج Hugging Face** الذي ينزل نفسه في المرة الأولى، و**التعرف على النص من المسحات** مع إضافة الترقيم تلقائيًا. السكريبت الكامل جاهز للنسخ، تعديل المسارات، والتنفيذ.

## الخطوات التالية والمواضيع ذات الصلة  

- **معالجة ما بعد الدفعة**: استكشف `ocr_engine.run_batch_postprocessor` لمعالجة دفعات أسرع.  
- **نماذج بديلة**: جرّب عائلة `openai/whisper` إذا كنت تحتاج إلى تحويل الكلام إلى نص إلى جانب OCR.  
- **التكامل مع قواعد البيانات**: احفظ النص المستخرج في SQLite أو Elasticsearch لأرشفة قابلة للبحث.  

لا تتردد في التجربة—بدّل النموذج، عدّل `gpu_layers`، أو أضف معالج ما بعد خاص بك. مرونة Aspose OCR مع مركز نماذج Hugging Face تجعل هذا الأساس مناسبًا لأي مشروع رقمنة مستندات.

---

*برمجة سعيدة! إذا واجهت أي مشكلة، اترك تعليقًا أدناه أو راجع وثائق Aspose OCR لمزيد من خيارات التكوين.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}