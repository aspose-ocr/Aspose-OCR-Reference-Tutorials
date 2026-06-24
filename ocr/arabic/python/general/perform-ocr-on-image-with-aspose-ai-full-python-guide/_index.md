---
category: general
date: 2026-06-19
description: تعلم كيفية إجراء التعرف الضوئي على الحروف (OCR) على الصورة باستخدام Aspose
  OCR ومعالج ما بعد الذكاء الاصطناعي في بايثون. يتضمن نموذجًا يتم تنزيله تلقائيًا،
  وتدقيق إملائي، وتسريعًا باستخدام وحدة معالجة الرسومات.
draft: false
keywords:
- perform OCR on image
- Aspose OCR Python
- AI post‑processor
- auto‑downloaded model
- spellcheck post‑processor
- GPU acceleration
language: ar
og_description: قم بإجراء التعرف الضوئي على الأحرف في الصورة باستخدام Aspose OCR ومعالج
  ما بعد الذكاء الاصطناعي. دليل خطوة بخطوة مع نموذج يتم تحميله تلقائيًا، تدقيق إملائي،
  وتسريع باستخدام وحدة معالجة الرسومات.
og_title: إجراء التعرف الضوئي على الأحرف في الصورة – دورة بايثون كاملة
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  headline: perform OCR on image with Aspose AI – Full Python Guide
  type: TechArticle
- description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  name: perform OCR on image with Aspose AI – Full Python Guide
  steps:
  - name: Initializes the Aspose OCR engine and loads a sample invoice image.
    text: Initializes the Aspose OCR engine and loads a sample invoice image.
  - name: Runs a basic OCR pass and prints the raw text.
    text: Runs a basic OCR pass and prints the raw text.
  - name: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
    text: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
  - name: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
    text: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
  - name: Releases all resources cleanly.
    text: Releases all resources cleanly.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: تنفيذ OCR على صورة باستخدام Aspose AI – دليل بايثون الكامل
url: /ar/python/general/perform-ocr-on-image-with-aspose-ai-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# perform OCR on image – Complete Python Tutorial

هل تساءلت يومًا كيف **تُجري OCR على ملفات الصور** دون الحاجة إلى التعامل مع عشرات المكتبات؟ في تجربتي، تكون المشكلة عادةً في التعامل مع محرك OCR الخام، ثم محاولة تنظيف المخرجات المليئة بالضوضاء. لحسن الحظ، Aspose OCR للغة Python مع معالجها اللاحق المدعوم بالذكاء الاصطناعي يجعل العملية بأكملها سهلة.

في هذا الدليل سنستعرض مثالًا عمليًا من البداية إلى النهاية يوضح لك بالضبط كيف **تُجري OCR على بيانات الصورة**، وتزيد الدقة باستخدام نموذج يتم تنزيله تلقائيًا، وتفعيل التدقيق الإملائي، وحتى الاستفادة من تسريع GPU عندما يكون متاحًا. بحلول الوقت الذي تنتهي فيه، ستحصل على سكربت قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع فواتير، أو مسح إيصالات، أو رقمنة مستندات.

## What You’ll Build

سننشئ برنامجًا صغيرًا بلغة Python يقوم بـ:

1. تهيئة محرك Aspose OCR وتحميل صورة فاتورة تجريبية.  
2. تنفيذ تمريرة OCR أساسية وطباعة النص الخام.  
3. ضبط **Aspose AI** مع **نموذج يتم تنزيله تلقائيًا** من Hugging Face.  
4. تشغيل **معالج AI اللاحق** (بما في ذلك **معالج التدقيق الإملائي**) لتنظيف مخرجات OCR.  
5. تحرير جميع الموارد بشكل نظيف.

بدون خدمات خارجية، بدون مفاتيح API—فقط بضع أسطر من Python وقوة Aspose.

> **Pro tip:** إذا كنت تعمل على جهاز يحتوي على GPU جيد، فإن ضبط `gpu_layers` يمكن أن يقلل الثواني من خطوة المعالجة اللاحقة.

## Prerequisites

- Python 3.8 أو أحدث (الكود يستخدم تلميحات النوع لكنها اختيارية).  
- حزم `aspose-ocr` و `aspose-ai` مثبتة عبر `pip`.  
  ```bash
  pip install aspose-ocr aspose-ai
  ```  
- صورة تجريبية (PNG أو JPG أو TIFF) موجودة في مكان يمكنك الإشارة إليه، مثل `sample_invoice.png`.  
- (اختياري) GPU يدعم CUDA والسائقات المناسبة إذا كنت تريد **تسريع GPU**.

الآن بعد أن تم إعداد الأساسيات، دعنا نغوص في الكود.

![perform OCR on image example](image.png)

## perform OCR on image – Step 1: Initialise the OCR engine and load the image

الأول الذي نحتاجه هو مثيل لمحرك OCR. يقدم Aspose OCR واجهة برمجة تطبيقات كائنية نظيفة تُجردك من معالجة الصورة منخفضة المستوى.

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()
ocr_engine.Language = "en"                     # English; change as needed

# Load the image you want to analyse
ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")
```

**Why this matters:**  
تحديد اللغة مبكرًا يخبر المحرك بمجموعة الأحرف المتوقعة، مما يمكن أن يحسن سرعة ودقة التعرف. إذا كنت تتعامل مع مستندات متعددة اللغات، ما عليك سوى استبدال `"en"` بـ `"fr"` أو `"de"` حسب الحاجة.

## Step 2: Perform basic OCR and view the raw text

الآن نقوم فعليًا بتشغيل التعرف. يحتوي كائن النتيجة على النص الخام، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها لاحقًا.

```python
# Run OCR
ocr_result = ocr_engine.Recognize()

# Show the unprocessed output
print("Raw OCR output:")
print(ocr_result.Text)
```

قد يبدو الناتج النموذجي هكذا (لاحظ الأخطاء العارضة في الأحرف):

```
Raw OCR output:
Inv0ice N0: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00
```

يمكنك رؤية الأصفار (`0`) حيث ظن المحرك أنه رأى حرف “O”. هنا يتألق **معالج AI اللاحق**.

## Configure Aspose AI – auto‑downloaded model and spellcheck

قبل أن نسلم نتيجة OCR الخام إلى طبقة AI، نحتاج إلى إخبار Aspose AI أي نموذج نريد استخدامه. يمكن للمكتبة تنزيل نموذج تلقائيًا من Hugging Face، لذا لا تحتاج إلى التعامل مع ملفات `.bin` الكبيرة بنفسك.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

# Create a model configuration that auto‑downloads the Qwen2.5‑3B‑Instruct model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"   # reduces RAM usage
model_config.gpu_layers = 20                      # use GPU if available

# Initialise the AI engine with the config
ai_engine = AsposeAI(model_config)

# Enable the built‑in spellcheck post‑processor
ai_engine.set_post_processor("spellcheck", None)
```

**Explanation of the settings**

| Setting | What it does | When to adjust |
|---------|--------------|----------------|
| `allow_auto_download` | يسمح لـ Aspose بتحميل النموذج تلقائيًا عند أول تشغيل. | أبقِ القيمة `true` ما لم تقم بتنزيل النموذج مسبقًا للاستخدام دون اتصال. |
| `hugging_face_repo_id` | معرف النموذج على Hugging Face. | استبدله بنموذج مختلف إذا كنت تحتاج إلى نموذج متخصص في مجال معين. |
| `hugging_face_quantization` | يحدد مستوى الكم (`int8`, `float16`, إلخ). | استخدم `int8` للبيئات ذات الذاكرة المحدودة؛ `float16` للدقة الأعلى. |
| `gpu_layers` | عدد طبقات المحول التي تُنفّذ على الـ GPU. | اضبطها إلى `0` للاستخدام على CPU فقط، أو قيمة تصل إلى عدد طبقات النموذج الكلي (20 لـ Qwen2.5‑3B). |

## Run the AI post‑processor on the OCR result

مع جاهزية المحرك، نمرر مخرجات OCR الخام إلى خط أنابيب AI. سيقوم **معالج التدقيق الإملائي** المدمج بتصحيح الأخطاء الواضحة، بينما يمكن للنموذج اللغوي إعادة صياغة أو ملء المعلومات المفقودة إذا فعلت معالجات إضافية لاحقًا.

```python
# Enhance the OCR result using the AI post‑processor
enhanced_result = ai_engine.run_postprocessor(ocr_result)

# Display the cleaned‑up text
print("\nAI‑enhanced OCR output:")
print(enhanced_result.Text)
```

الناتج المتوقع بعد خطوة التدقيق الإملائي:

```
AI‑enhanced OCR output:
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

لاحظ كيف تم تصحيح الأصفار إلى حروف صحيحة، وكيف تم تحويل “Am0unt” الخطأ إلى “Amount”. يعمل **معالج AI اللاحق** عن طريق إرسال النص الخام عبر النموذج المختار، والذي يعيد نسخة محسّنة بناءً على تدريبه.

### Edge Cases & Tips

- **Low‑resolution images**: إذا عانى محرك OCR، فكر في تكبير الصورة أولًا (`Pillow` يمكنه المساعدة) أو زيادة `ocr_engine.ImagePreprocessingOptions`.  
- **Non‑Latin scripts**: غيّر `ocr_engine.Language` إلى رمز ISO المناسب (`"zh"` للصينية، `"ar"` للعربية).  
- **GPU not detected**: إعداد `gpu_layers` يعود صامتًا إلى CPU إذا لم يُعثر على GPU متوافق، لذا لا تحتاج إلى معالجة أخطاء إضافية.  
- **Model size limits**: نموذج Qwen2.5‑3B حجمه ~4 GB مضغوط؛ تأكد من توفر مساحة كافية على القرص للتنزيل التلقائي.

## Release resources – clean shutdown

كائنات Aspose تحتفظ بمقابض native، لذا من الممارسات الجيدة تحريرها عند الانتهاء. هذا يمنع تسرب الذاكرة، خاصة في الخدمات التي تعمل لفترات طويلة.

```python
# Free AI resources
ai_engine.free_resources()

# Dispose of the OCR engine
ocr_engine.Dispose()
```

يمكنك تغليف السكربت بالكامل داخل كتلة `try…finally` إذا كنت تفضّل تنظيفًا صريحًا.

## Full Script – copy‑paste ready

فيما يلي البرنامج الكامل، جاهز للتنفيذ بعد استبدال `YOUR_DIRECTORY` بمسار صورتك.

```python
# -*- coding: utf-8 -*-
"""
Full example: perform OCR on image using Aspose OCR + AI post‑processor.
Author: Your Name
Date: 2026‑06‑19
"""

from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.Language = "en"
    ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Basic OCR
    ocr_result = ocr_engine.Recognize()
    print("Raw OCR output:")
    print(ocr_result.Text)

    # 3️⃣ Configure Aspose AI with auto‑downloaded model
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "int8"
    model_cfg.gpu_layers = 20   # GPU acceleration if available

    ai_engine = AsposeAI(model_cfg)
    ai_engine.set_post_processor("spellcheck", None)   # enable spellcheck

    # 4️⃣ AI post‑processing
    enhanced = ai_engine.run_postprocessor(ocr_result)
    print("\nAI‑enhanced OCR output:")
    print(enhanced.Text)

    # 5️⃣ Clean up
    ai_engine.free_resources()
    ocr_engine.Dispose()

if __name__ == "__main__":
    main()
```

شغّله باستخدام:

```bash
python perform_ocr_on_image.py
```

سترى النص الخام والنص المنقّح يُطبعان في وحدة التحكم.

## Conclusion


## What Should You Learn Next?


الدروس التالية تغطي مواضيع ذات صلة وثيقة تُبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}