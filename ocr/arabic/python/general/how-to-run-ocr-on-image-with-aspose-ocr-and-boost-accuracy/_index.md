---
category: general
date: 2026-09-22
description: تعلم كيفية تشغيل OCR على الصورة باستخدام Aspose OCR، وتكوين نموذج OCR،
  واستخراج النص من الفاتورة، وتحسين دقة OCR في بايثون.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from invoice
- improve OCR accuracy
- configure OCR model
language: ar
lastmod: 2026-09-22
og_description: تشغيل OCR على الصورة باستخدام Aspose OCR، تكوين نموذج OCR، استخراج
  النص من الفاتورة وتحسين دقة OCR في دليل كامل خطوة بخطوة.
og_image_alt: Screenshot showing raw OCR and AI‑enhanced text extracted from an invoice
  image
og_title: تشغيل التعرف الضوئي على الأحرف (OCR) على صورة باستخدام Aspose OCR – دليل
  بايثون كامل
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to run OCR on image using Aspose OCR, configure the OCR model,
    extract text from invoice and improve OCR accuracy in Python.
  headline: How to run OCR on image with Aspose OCR and boost accuracy
  type: TechArticle
tags:
- Aspose OCR
- Python
- AI post‑processing
title: كيفية تشغيل OCR على صورة باستخدام Aspose OCR وتعزيز الدقة
url: /ar/python/general/how-to-run-ocr-on-image-with-aspose-ocr-and-boost-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR على صورة باستخدام Aspose OCR وتعزيز الدقة

إذا كنت بحاجة إلى **run OCR on image** ملفات في Python، يوضح لك هذا الدليل سير عمل كامل وجاهز للإنتاج. ستتعرف على كيفية تكوين نموذج OCR، استخراج النص من صور الفواتير، وتحسين دقة OCR باستخدام معالج Aspose AI اللاحق. معالجة الفواتير الممسوحة ضوئياً هي نقطة ألم شائعة—غالبًا ما يُعيد OCR الخام كلمات مكتوبة بشكل خاطئ أو أرقامًا مكسورة. بنهاية هذا الدرس ستحصل على سكريبت جاهز للتنفيذ يُقدم استخراج نص أنظف وأكثر موثوقية، وستفهم لماذا كل خطوة من خطوات التكوين مهمة.

## المتطلبات المسبقة

* Python 3.8 أو أحدث مثبت.  
* رخصة Aspose OCR سارية (الإصدار التجريبي المجاني يعمل للتقييم).  
* صورة فاتورة نموذجية (مثال: `sample_invoice.png`) موجودة في دليل معروف.  
* إلمام أساسي بتثبيت حزم Python.  

لا توجد تبعيات نظام إضافية مطلوبة؛ يتعامل SDK مع تنزيل النماذج تلقائيًا.

## الخطوة 1: تثبيت حزمة Aspose OCR

أول شيء يجب عليك فعله هو إضافة مكتبة Aspose OCR إلى بيئتك. الحزمة تتضمن نموذج AI ومعالج ما بعد المعالجة الذي ستحتاجه لاحقًا.  

```bash
pip install aspose-ocr
```

تنفيذ هذا الأمر يثبت `asposeocr`، الذي يوفر الفئة `AsposeAI` المستخدمة لت **configure OCR model** الإعدادات مثل التنزيلات التلقائية والتنفيذ على وحدة المعالجة المركزية فقط.

## الخطوة 2: تكوين نموذج OCR (اختياري لكن موصى به)

ضبط النموذج بدقة يحسن السرعة والدقة، خاصةً عندما تقوم بـ **run OCR on image** لصور الفواتير التي تحتوي على أعداد كثيرة وحروف خاصة. يوضح الكود التالي أكثر الإعدادات فائدة:  

```python
import asposeocr as ocr   # import the Aspose OCR package

# Create an AsposeAI instance with default logging
ai = ocr.AsposeAI()

# Enable automatic model download, force CPU execution, and enlarge the context window
ai.allow_auto_download = "true"   # download missing model files automatically
ai.gpu_layers = 0                 # use CPU only – avoids GPU‑related errors on most machines
ai.context_size = 2048           # larger context improves correction quality
```

*لماذا هذه العلامات؟*  
* `allow_auto_download` يضمن وجود نموذج OCR حتى على جهاز جديد.  
* `gpu_layers = 0` يلغي الحاجة إلى GPU متوافق مع CUDA، وهو ما لا يمتلكه العديد من المطورين.  
* `context_size` يتحكم في عدد الرموز المحيطة التي يأخذها AI في الاعتبار عند تصحيح الأخطاء؛ نافذة أكبر غالبًا ما **improve OCR accuracy** على النصوص الكثيفة مثل الفواتير.

## الخطوة 3: تهيئة محرك AI

التهيئة تتحقق من جاهزية ملفات النموذج وتحملها في الذاكرة. تخطي هذه الخطوة قد يؤدي إلى خطأ وقت التشغيل عندما تستدعي المعالج لاحقًا.  

```python
# Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")
```

إذا فشل المحرك، فإن الاستثناء يوضح لك بالضبط مكان حدوث المشكلة، مما يوفر لك وقتًا في تصحيح الأخطاء.

## الخطوة 4: تشغيل محرك OCR القياسي على صورة

الآن يمكنك **run OCR on image** للملفات. الفئة `OcrEngine` تقوم باستخراج النص الخام دون أي تصحيحات تعتمد على AI.  

```python
# Path to the invoice image you want to process
image_path = "YOUR_DIRECTORY/sample_invoice.png"

# Perform raw OCR
ocr_result = ocr.OcrEngine().recognize_image(image_path)
```

`ocr_result.text` يحتوي على السلسلة النصية البسيطة التي تعرف عليها محرك OCR. بالنسبة لفاتورة نموذجية، قد ترى أرقامًا مفقودة، علامات ترقيم في غير موضعها، أو كلمات مكسورة.

## الخطوة 5: تطبيق معالج AI اللاحق لتحسين دقة OCR

معالج AI اللاحق من Aspose يحلل المخرجات الخام ويصلح الأخطاء الشائعة في OCR (مثال: “5um” → “Sum”). تنفيذ هذه الخطوة هو المفتاح لـ **improve OCR accuracy** للمستندات المالية.  

```python
# Apply the AI post‑processor
cleaned_result = ai.run_postprocessor(ocr_result)
```

المعالج اللاحق يستخدم التكوين الذي ضبطته في الخطوة 2، لذا فإن `context_size` الأكبر يساهم في تصحيحات أكثر موثوقية.

## الخطوة 6: استخراج النص من الفاتورة وعرض النتائج

في هذه المرحلة لديك نسختان من النص المستخرج: مخرجات OCR الخام والنسخة المحسنة بواسطة AI. طباعة كلاهما يتيح لك التحقق من التحسين ويعطيك أيضًا فرصة لتسجيل البيانات الأصلية لأغراض التدقيق.  

```python
# Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)

print("\n=== AI‑enhanced ===")
print(cleaned_result.text)
```

**الناتج النموذجي**  

```
=== Raw OCR ===
Inv0ice No: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00

=== AI‑enhanced ===
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

لاحظ كيف أن خطوة AI صححت الخلط بين الصفر والواحد وأصلحت تنسيق المبلغ—بالضبط النوع من التحسين الذي تحتاجه عندما **extract text from invoice** الملفات.

## الخطوة 7: تحرير الموارد

أخيرًا، حرّر الموارد الأصلية التي يستخدمها محرك AI. هذا مهم بشكل خاص في الخدمات طويلة التشغيل أو وظائف الدُفعات.  

```python
# Release resources when finished
ai.free_resources()
```

إهمال هذه الدعوة قد يؤدي إلى تسرب الذاكرة لأن النموذج الأساسي يعمل في كود أصلي.

## البرنامج الكامل الذي يمكنك نسخه‑ولصقه

فيما يلي البرنامج الكامل القابل للتنفيذ الذي يدمج كل خطوة موصوفة أعلاه. استبدل `YOUR_DIRECTORY` بالمسار الفعلي لملف الصورة الخاص بك.  

```python
import asposeocr as ocr   # import the Aspose OCR package

# Step 1: Create an AsposeAI instance (default logging)
ai = ocr.AsposeAI()

# Step 2: (Optional) Tune the model configuration for this demo
#   • Enable automatic download of the model if missing
#   • Use CPU only (no GPU layers)
#   • Increase context size for better correction quality
ai.allow_auto_download = "true"
ai.gpu_layers = 0
ai.context_size = 2048

# Step 3: Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")

# Step 4: Run the standard OCR engine on an image
image_path = "YOUR_DIRECTORY/sample_invoice.png"
ocr_result = ocr.OcrEngine().recognize_image(image_path)

# Step 5: Apply the AI post‑processor to improve the raw OCR output
cleaned_result = ai.run_postprocessor(ocr_result)

# Step 6: Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)
print("\n=== AI‑enhanced ===")
print(cleaned_result.text)

# Step 7: Release resources when finished
ai.free_resources()
```

احفظ هذا كـ `process_invoice.py` ثم شغّله:  

```bash
python process_invoice.py
```

يجب أن ترى النص الخام والنص المصحح يُطبعان في وحدة التحكم، مما يؤكد أنك نجحت في **run OCR on image**، **configure OCR model**، و **improve OCR accuracy** لمهمة استخراج الفواتير الخاصة بك.

## الأسئلة الشائعة والحالات الخاصة

| السؤال | الإجابة |
|----------|--------|
| *ماذا لو فشل النموذج في التحميل؟* | تأكد من أن جهازك متصل بالإنترنت وأن علامة `allow_auto_download` مضبوطة على `"true"`. يمكنك أيضًا تنزيل النموذج يدويًا من بوابة Aspose وتوجيه `AsposeAI` إلى المجلد المحلي عبر `ai.model_path = "path/to/model"` |
| *هل يمكنني تشغيل هذا على GPU؟* | نعم. اضبط `ai.gpu_layers` إلى عدد صحيح موجب (مثال: `2`) وقم بتثبيت مكتبات CUDA المناسبة. تنفيذ GPU يسرّع الدُفعات الكبيرة لكنه يتطلب GPU متوافق. |
| *كيف يمكنني معالجة العديد من الفواتير في مجلد؟* | ضع المنطق الأساسي داخل حلقة تتكرر على `os.listdir(folder)`. تذكر استدعاء `ai.free_resources()` فقط بعد انتهاء الحلقة، وليس بعد كل ملف، للحفاظ على تحميل النموذج. |
| *هل المعالج اللاحق آمن للفواتير غير الإنجليزية؟* | النموذج الافتراضي مُدرب على النص الإنجليزي. للغات أخرى، قم بتنزيل حزمة اللغة المقابلة واضبط `ai.language = "fr"` (أو رمز ISO المناسب). |
| *ماذا لو كانت نتيجة OCR فارغة؟* | تحقق من أن `image_path` يشير إلى صورة قابلة للقراءة وأن الملف غير تالف. يمكنك أيضًا زيادة `ai.context_size` لتزويد النموذج بمزيد من السياق للصور ذات الجودة المنخفضة. |

## الخطوات التالية

* **Batch processing** – دمج السكريبت مع `multiprocessing` لمعالجة آلاف الفواتير بشكل متوازي.  
* **Data validation** – استخدم التعبيرات النمطية للتحقق من أرقام الفواتير، التواريخ، والقيم المالية بعد الاستخراج.  
* **Integration with databases** – خزن النص المنقح مباشرةً في PostgreSQL أو MongoDB للتحليلات اللاحقة.  
* **Custom model fine‑tuning** – إذا كان لديك مجموعة بيانات مملوكة كبيرة، درّب نموذجًا متخصصًا للمجال واضبط `ai.model_path` للإشارة إليه للحصول على دقة أعلى.  

من خلال تجربة هذه الأفكار، ستحول عرض OCR البسيط إلى خط أنابيب معالجة مستندات قوي يلبي متطلبات الإنتاج.

---

*أنت الآن تعرف كيفية **run OCR on image** للملفات باستخدام Aspose OCR، تكوين نموذج OCR لأداء مثالي، وتحسين دقة OCR باستخدام معالج AI اللاحق. طبّق هذه الخطوات على سير عمل معالجة الفواتير الخاص بك وتمتع باستخراج نص أنظف وأكثر موثوقية.*

## ما الذي يجب أن تتعلمه بعد ذلك؟

- [كيفية تشغيل OCR على الفواتير – استخراج النص من صورة باستخدام Python](/ocr/english/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/)
- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [تحويل الصورة إلى نص: استخراج النص من صورة باستخدام Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}