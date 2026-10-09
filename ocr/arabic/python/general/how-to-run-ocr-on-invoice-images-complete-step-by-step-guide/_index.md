---
category: general
date: 2026-01-12
description: كيفية تشغيل التعرف الضوئي على الأحرف واستخراج النص من صور الفواتير باستخدام
  Aspose OCR ونموذج خفيف الوزن من Hugging Face. تعلم تنزيل النموذج، تصحيح أخطاء OCR،
  وإجراء التعرف الضوئي على الأحرف على الصورة.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: ar
og_description: كيفية تشغيل OCR على صور الفواتير، استخراج النص، وإصلاح الأخطاء باستخدام
  نموذج لغة Hugging Face. اتبع هذا الدليل الكامل للحصول على نتائج خالية من العيوب.
og_title: كيفية تشغيل التعرف الضوئي على الأحرف في صور الفواتير – دليل كامل
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: كيفية تشغيل التعرف الضوئي على الأحرف (OCR) في صور الفواتير – دليل خطوة بخطوة
  كامل
url: /ar/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR على صور الفواتير – دليل خطوة بخطوة كامل

هل تساءلت يومًا **how to run OCR** على فاتورة ممسوحة ضوئيًا والحصول على نص نظيف وقابل للبحث دون قضاء ساعات في تنظيفه؟ لست وحدك. في العديد من المشاريع الواقعية يكون ناتج OCR الخام مليئًا بالأخطاء—مثل استبدال “O” بـ “0”، “l” بـ “1”، أو حتى كلمات كاملة مشوهة. الخبر السار؟ ببضع أسطر من Python يمكنك ليس فقط **perform OCR on image** للملفات ولكن أيضًا تصحيح **OCR errors** تلقائيًا باستخدام نموذج خفيف الوزن من Hugging Face.

في هذا الدرس سنستعرض كل ما تحتاج معرفته: من تحميل صورة الفاتورة، استخراج النص الخام، تنزيل نموذج مُكمَّن، إلى صقل النتيجة للحصول على نسخة نصية مثالية جاهزة للمعالجة اللاحقة. في النهاية ستتمكن من **extract text from invoice** ملفات PDF أو PNG في سكريبت واحد قابل للتكرار.

## المتطلبات والإعداد

قبل الغوص في التفاصيل، تأكد من أن لديك:

| المتطلب | سبب الأهمية |
|-------------|----------------|
| Python 3.9+ | بناء جملة حديث وتلميحات نوع |
| `aspose-ocr` package | يوفر `ocr.OcrEngine` المستخدم في المثال |
| `aspose-ai` package | يوفر معالج ما بعد `AsposeAI` |
| Access to a GPU (optional) | يسرّع طبقات LLM؛ وإلا فإن CPU يعمل بشكل جيد |
| Internet connection (first run) | مطلوب **download Hugging Face model** تلقائيًا |

يمكنك تثبيت المكتبات المطلوبة باستخدام:

```bash
pip install aspose-ocr aspose-ai
```

> **نصيحة احترافية:** إذا كنت تخطط لتشغيل LLM على GPU، قم بتثبيت `torch` بدعم CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

الآن بعد أن أصبح البيئة جاهزة، دعنا ننتقل إلى الكود.

---

## الخطوة 1 – تهيئة محرك OCR وتحميل صورة الفاتورة الخاصة بك

أول شيء تحتاج إلى القيام به هو إنشاء نسخة من محرك OCR الخاص بـ Aspose وتوجيهه إلى الملف الذي تريد معالجته. هذه الخطوة هي الأساس لـ **how to run OCR** على أي صورة.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **سبب الأهمية:** `load_image` يقبل PNG، JPEG، TIFF، وحتى صفحات PDF، مما يتيح لك **perform OCR on image** بغض النظر عن الصيغة.

## الخطوة 2 – تشغيل OCR الأساسي لالتقاط النص الخام

بمجرد تحميل الصورة، يمكن للمحرك إنتاج نسخة نصية خام. غالبًا ما يكون هذا الناتج مليئًا بالضوضاء، لذا سنقوم لاحقًا بتشغيل خطوة تصحيح.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

مثال على ناتج خام قد يبدو هكذا:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

لاحظ الأصفار (`0`) حيث يجب أن يكون الحرف “O”؟ هذا هو النوع من الأخطاء التي سنصلحها لاحقًا.

## الخطوة 3 – تكوين معالج ما بعد الذكاء الاصطناعي باستخدام نموذج LLM خفيف الوزن

الآن نجلب **download Hugging Face model** صغير بما يكفي للعمل على أجهزة ذات موارد محدودة ولكنه قوي بما يكفي لفهم لغة الفواتير. يستخدم المثال نموذج Qwen 2.5 3B‑Instruct GGUF، مُكمَّن إلى `int8` لتقليل استهلاك الذاكرة.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **لماذا هذا النموذج؟** تقليل الدقة إلى `int8` يقلص حجم الملف إلى ~1.2 GB، مما يجعله مناسبًا لمعظم الحواسيب المحمولة. طبقات GPU تسرّع الاستدلال، لكن الكود يتراجع بسلاسة إلى CPU إذا لم يتوفر GPU.

## الخطوة 4 – تشغيل تصحيح مستند إلى LLM على نتيجة OCR الخام

مع جاهزية النموذج، نمرر النص الخام إلى معالج ما بعد المعالجة. سيعيد LLM كتابة النسخة، مُصححًا الأخطاء الشائعة في OCR ومُطبعًا الأرقام.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

الناتج المنظف المتوقع:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

يمكنك رؤية أن الأصفار عادت لتصبح الحرف “O”، و“Am0unt” أصبحت الآن “Amount”. هذا هو جوهر **correct OCR errors** تلقائيًا.

## الخطوة 5 – تحرير الموارد والتنظيف

نماذج اللغة الكبيرة قد تحتفظ بذاكرة GPU، لذا من الممارسات الجيدة تحرير الموارد عند الانتهاء.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

إذا كنت تخطط لمعالجة العديد من الفواتير دفعة واحدة، يمكنك إبقاء النموذج محمَّلًا وتحريره فقط في نهاية السكريبت.

## مثال عملي كامل

بجمع كل ما سبق، إليك سكريبت واحد يمكنك وضعه في ملف `.py` وتشغيله:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

تشغيل السكريبت يجب أن ينتج مخرجات مشابهة للكتلة “AI‑corrected” المعروضة سابقًا. لا تتردد في تغيير مسار الصورة إلى أي فاتورة أو إيصال آخر لتتمكن من **extract text from invoice** ملفات بكميات كبيرة.

## الأسئلة المتكررة والحالات الخاصة

### ماذا لو لم يكن لدي GPU؟

معامل `gpu_layers` اختياري. عيّنه إلى `0` أو احذفه، وسيت运行 النموذج بالكامل على CPU. توقع استدلال أبطأ—حوالي 2–3 ثوانٍ لكل صفحة على حاسوب محمول حديث.

### فواتيري هي ملفات PDF متعددة الصفحات. كيف أتعامل معها؟

حوّل كل صفحة إلى صورة منفصلة (مثلاً باستخدام `pdf2image`) وكرّر عبر الصفحات بنفس السكريبت. يمكن لمحرك OCR معالجة كل صورة على حدة، وسيقوم LLM بتصحيح كل كتلة نصية.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### فشل تحميل النموذج خلف جدار حماية؟

حمّل النموذج يدويًا من مركز نماذج Hugging Face، فكّ ضغطه في مجلد محلي، ووجه `hugging_face_repo_id` إلى المسار المحلي:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### ما مدى دقة التصحيح؟

للفواتير الإنجليزية النموذج يصل إلى تصحيح >95 % من الأخطاء الشائعة في OCR. قد تحتاج الملاحظات المكتوبة يدويًا المعقدة إلى مراجعة يدوية.

## نصائح وحيل للاستخدام في الإنتاج

- **Batch processing:** غلف الخطوات 2‑4 في دالة ومرّر قائمة بمسارات الملفات. أعد استخدام نفس نسخة `AsposeAI` لتجنب إعادة تحميل النموذج.
- **Logging:** استبدل `print` بوحدة `logging` في Python لالتقاط كل من المخرجات الخام والمنقحة لأغراض التدقيق.
- **Error handling:** احط نداء OCR بكتل `try/except`. إذا فشلت صورة ما، سجّل اسم الملف واستمر.
- **Performance tuning:** جرّب تعديل `gpu_layers`. المزيد من الطبقات على GPU يسرّع الاستدلال لكنه يزيد من استهلاك VRAM.

## الخلاصة

لقد غطينا **how to run OCR** على صور الفواتير من البداية إلى النهاية، موضحين لك كيفية **perform OCR on image**، **download Hugging Face model**، و**correct OCR errors** تلقائيًا. يوضح السكريبت الكامل سير عمل عملي يمكنك دمجه في أي خط أنابيب أتمتة مبني على Python.

ما الخطوة التالية؟ جرّب توسيع الخطوط لتضمين **extract key fields** (رقم الفاتورة، التاريخ، الإجمالي) باستخدام تعبيرات نمطية على النص المصحح، أو أدخل المخرجات المنقحة إلى قاعدة بيانات لتسجيلات قابلة للبحث. يمكنك أيضًا تجربة نماذج LLM خفيفة أخرى من Hugging Face إذا احتجت لغة مختلفة أو معرفة متخصصة بمجال معين.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالكريستال!

![كيفية تشغيل OCR على صورة فاتورة](ocr_invoice_example.png "كيفية تشغيل OCR على الفاتورة")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}