---
category: general
date: 2026-03-18
description: دورة أساسية في OCR باستخدام بايثون تُظهر كيفية تحويل ملفات TIFF إلى نص،
  تحميل صورة OCR، ضبط طبقات GPU، وإصلاح الأصفار البادئة باستخدام Aspose AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: ar
og_description: دورة أساسية في التعرف الضوئي على الحروف باستخدام بايثون تُرشدك إلى
  تحويل ملفات TIFF إلى نص نظيف، تحميل الصور، ضبط طبقات GPU، وإصلاح الأصفار البادئة.
og_title: أساسيات OCR بايثون – تحويل TIFF إلى نص
tags:
- OCR
- Python
- AI
- Aspose
title: أساسيات OCR بايثون – تحويل TIFF إلى نص
url: /ar/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – تحويل TIFF إلى نص مع معالجة ما بعد الذكاء الاصطناعي

هل تبحث عن طريقة للقيام بـ **basic ocr python** على المستندات الممسوحة ضوئيًا؟ في هذا الدليل سنستعرض تحويل ملف TIFF إلى نص نظيف وقابل للبحث باستخدام Aspose OCR ومعالج ما بعد الذكاء الاصطناعي.  

إذا واجهت صعوبة في **convert TIFF to text** لأن المخرجات الأولية مليئة بالأخطاء الإملائية أو الرموز الغريبة، فأنت لست وحدك. سنوضح لك أيضًا كيفية **load image OCR**، تعديل المحرك لتحديد **set GPU layers**، وحتى **fix leading zeroes** التي تظهر غالبًا في أرقام الفواتير.

## ما ستتعلمه

- كيفية تهيئة محرك Aspose OCR للمستندات المطبوعة.  
- الخطوات الدقيقة لـ **load image OCR** من ملف TIFF والحصول على النص الخام.  
- تكوين نموذج AI، تنزيله تلقائيًا، و **setting GPU layers** للحصول على استدلال أسرع.  
- إضافة تدقيق إملائي مدمج بالإضافة إلى دالة مخصصة **fixes leading zeroes**.  
- تنظيف نتيجة OCR وإطلاق الموارد بشكل صحيح.  

بنهاية هذا البرنامج التعليمي ستحصل على سكريبت Python واحد قابل لإعادة الاستخدام يحول أي ملف TIFF إلى نص مصقول وقابل للبحث—بدون الحاجة إلى النسخ واللصق اليدوي.  

### المتطلبات المسبقة

- Python 3.8+ مثبت على جهازك.  
- حزمة `aspose-ocr` (`pip install aspose-ocr`).  
- اختياريًا: وحدة معالجة رسومية (GPU) بذاكرة VRAM لا تقل عن 4 GB إذا رغبت في **set GPU layers**؛ وإلا سيتحول الكود تلقائيًا إلى CPU.  

---

## basic ocr python – load image and recognize text

أول شيء نحتاج إلى القيام به هو **load image OCR** حتى يتمكن المحرك من قراءة البكسلات. يتعامل `OcrEngine` من Aspose مع العديد من الصيغ، لكننا سنركز هنا على TIFF لأنه الأكثر شيوعًا للفواتير الممسوحة.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **نصيحة محترف:** إذا كنت تتعامل مع ملفات TIFF متعددة الصفحات، يقوم Aspose بمعالجة كل صفحة بالتتابع تلقائيًا، لذا لا تحتاج إلى حلقات إضافية.

الآن بعد تحميل الصورة، دعنا نجري تمريرة التعرف الأساسية.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

ستظهر لك نتيجة مشابهة لـ:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

هل لاحظت الـ *أصفار* قبل الحروف؟ هذا أثر شائع للـ OCR سنقوم بتنظيفه لاحقًا.

![basic ocr python workflow](/images/ocr-workflow.png "مخطط سير عمل basic ocr python")

---

## الخطوة 2: Convert TIFF to text – إعداد معالج AI ما بعد المعالجة

النص الخام من OCR مفيد، لكن معظم خطوط الإنتاج تحتاج إلى نسخة مصقولة. توفر Aspose غلافًا `AsposeAI` يمكنه تنزيل نموذج من Hugging Face، تشغيله على الـ GPU، وتطبيق التدقيق الإملائي تلقائيًا.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### لماذا **set GPU layers** مهم

معامل `gpu_layers` يخبر نموذج GGUF الأساسي بعدد طبقات الـ transformer التي يجب إبقاؤها على الـ GPU. كلما زاد عدد الطبقات = استدلال أسرع لكن استهلاك VRAM أعلى. إذا كنت تستخدم لابتوب بموارد محدودة، قلل القيمة إلى `10` أو احذفها تمامًا للبقاء على CPU.

---

## الخطوة 3: Apply spellcheck and **fix leading zeroes**

يأتي Aspose AI مع مدقق إملائي مدمج، يلتقط معظم الأخطاء الإنجليزية. ومع ذلك، الإصلاحات الخاصة بالمجال—مثل تحويل الصفر الأول `0` إلى الحرف `O` في رموز الفواتير—تتطلب معالجًا مخصصًا ما بعد المعالجة.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **لماذا يعمل هذا:** التعبير النمطي يبحث عن حد كلمة (`\b`)، ثم صفر، ثم ثلاث حروف كبيرة بالضبط. بعد ذلك يستبدل الصفر بالحرف “O”. يمكنك توسيع النمط لتغطية حالات أخرى (مثال: `0[0-9]{2}` للأرقام التي تم قراءتها خطأ).

---

## الخطوة 4: Clean the OCR result with the AI post‑processor

الآن نجمع كل شيء: السلسلة الخام من **basic ocr python**، التدقيق الإملائي، وإصلاح الأصفار. تُعيد طريقة `run_postprocessor` نسخة مُنقاة جاهزة للأنظمة اللاحقة.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

الناتج النموذجي بعد المعالج ما بعد المعالجة:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

يمكنك ملاحظة أن الصفر الأول تحول إلى `O`، وتم تصحيح الأخطاء الشائعة. النص الآن جاهز للفهرسة في محرك بحث أو لتغذيته في خط أنابيب استخراج البيانات.

---

## الخطوة 5: Release AI resources – حافظ على سعادة الـ GPU

إذا كنت تشغل عدة مهام OCR في خدمة طويلة الأمد، من الممارسات الجيدة تحرير ذاكرة الـ GPU للنموذج عند الانتهاء.

```python
ocr_ai.free_resources()
```

تخطي هذه الخطوة قد يؤدي إلى أخطاء “out‑of‑memory” في الاستدعاءات اللاحقة، خاصةً عند **set GPU layers** إلى قيمة عالية.

---

## تنويعات اختيارية وحالات حافة

| الحالة | ما الذي يجب تغييره |
|-----------|----------------|
| **مستندات مكتوبة بخط اليد** | استخدم `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` بدلاً من `PRINTED`. |
| **لا توجد وحدة معالجة رسومية متاحة** | عيّن `gpu_layers=0` أو احذف الوسيط؛ سيعمل النموذج على CPU (أبطأ لكن آمن). |
| **لغة مختلفة** | غيّر معرف مستودع Hugging Face إلى نموذج مخصص للغة، مثل `microsoft/Florence-2-base`. |
| **معالجة دفعات** | غلف الخطوات داخل حلقة `for file in glob("*.tif"):` واجمع النتائج في قائمة أو ملف CSV. |
| **أنماط أصفار أكثر تعقيدًا** | وسّع `invoice_fix` بإضافة تعبيرات نمطية أخرى، مثل `r"\b0+([A-Z]{2,})\b"` للأصفار المتعددة في البداية. |

---

## الخاتمة

لقد أكملنا الآن خط أنابيب **basic ocr python** الذي يحمل ملف TIFF، يستخرج النص الخام، ثم ينقّيه باستخدام نموذج AI مع **setting GPU layers** للأداء. يُظهر المعالج المخصص ما بعد المعالجة كيفية **fix leading zeroes**، وهو تفصيل صغير لكنه غالبًا ما يُهمل ويمكن أن يعطل التحليلات اللاحقة.

لا تتردد في التجربة: جرّب تقليل الكمية (`float16` للدقة الأعلى)، استبدل التدقيق الإملائي بقاموس مخصص للمجال، أو ربط عدة إصلاحات مخصصة معًا. النمط يبقى نفسه—load, recognize, configure AI, post‑process, and clean up.

**الخطوات التالية** التي قد تستكشفها:

- دمج المخرجات المنقاة مع قاعدة بيانات أو فهرس Elasticsearch.  
- استخدام نفس النهج **convert TIFF to text** لملفات PDF متعددة اللغات.  
- إضافة واجهة مستخدم باستخدام Flask أو FastAPI لتمكين المستخدمين غير التقنيين من رفع الملفات والحصول على نص منقّى فورًا.  

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة وخالية من الأصفار!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}