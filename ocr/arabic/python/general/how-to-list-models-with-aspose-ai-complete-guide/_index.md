---
category: general
date: 2026-07-05
description: كيفية سرد النماذج باستخدام Aspose AI، تمكين التحميل التلقائي، وتنزيل
  نموذج Hugging Face في بايثون. اتبع هذا الدليل خطوة بخطوة لإعداد التخزين المؤقت وابدأ
  في استخدام Aspose AI اليوم.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: ar
og_description: كيفية سرد النماذج باستخدام Aspose AI، تمكين التحميل التلقائي وتنزيل
  نموذج من Hugging Face. تعلم كيفية إعداد الذاكرة المؤقتة واستخدام Aspose AI في دقائق.
og_title: كيفية سرد النماذج باستخدام Aspose AI – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: كيفية سرد النماذج باستخدام Aspose AI – دليل كامل
url: /ar/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية سرد النماذج باستخدام Aspose AI – دليل شامل

كيفية سرد النماذج باستخدام Aspose AI هو سؤال يظهر في اللحظة التي تبدأ فيها تجربة نماذج اللغة الكبيرة في بايثون. في هذا الدرس سنستعرض تمكين **auto download**، تكوين ذاكرة تخزين مؤقت محلية، وجلب نموذج مباشرة من Hugging Face—حتى تتمكن من البدء دون البحث عن الملفات يدوياً.

إذا تساءلت يوماً *“كيف أستخدم Aspose للذكاء الاصطناعي المدفوع بـ OCR?”* أو *“ما هي أسهل طريقة لتعيين ذاكرة التخزين المؤقت لملفات النموذج?”* فأنت في المكان الصحيح. في النهاية ستحصل على سكريبت كامل الوظائف يقوم بسرد كل نموذج مخزن محليًا، ويقوم بتنزيل النماذج المفقودة تلقائيًا، ويظهر لك بالضبط أين توجد الملفات على القرص.

---

## ما ستحتاجه

- Python 3.9 أو أحدث (المكتبة تستخدم تلميحات النوع التي تتطلب مفسّرًا حديثًا)
- الوصول إلى `pip` لتثبيت حزمة **Aspose OCR** (`aocr`).  
  ```bash
  pip install aocr
  ```
- اتصال بالإنترنت للتنزيل الأول من Hugging Face.
- مجلد ترغب في حفظ ذاكرة التخزين المؤقت للنماذج فيه (مثال: `./model_cache`).

هذا كل شيء—لا حاويات Docker إضافية، ولا بيئات افتراضية ثقيلة بخلاف تثبيت بايثون نظيف.

## ## كيفية سرد النماذج باستخدام Aspose AI

جوهر هذا الدليل هو القدرة على **list models** التي قام Aspose AI بتخزينها محليًا. بمجرد إعداد ذاكرة التخزين المؤقت، يمكن للمكتبة تعداد كل ما تعرفه، مما يجعل تصحيح الأخطاء وإدارة الإصدارات سهلًا.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**لماذا هذا يعمل:**  
- `AsposeAI()` ينشئ نقطة الدخول عالية المستوى التي تتواصل مع محرك الاستدلال الأساسي.  
- `AsposeAIModelConfig()` يحتوي على جميع الإعدادات التي يمكنك تعديلها؛ ضبط `allow_auto_download` إلى `"true"` يخبر المكتبة بجلب الملفات المفقودة تلقائيًا من المستودع الذي تحدده.  
- `directory_model_path` هو *دليل التخزين المؤقت*—المكان الذي تُخزن فيه جميع الملفات الثنائية التي تم تنزيلها.  
- `initialize()` يطبق التكوين، ويجري التنزيل الأول إذا كان التخزين المؤقت فارغًا.  
- أخيرًا، `list_local()` يفحص مجلد التخزين المؤقت ويعيد قائمة بايثون بمعرفات النماذج، والتي نقوم بطباعتها.

### النتيجة المتوقعة (التشغيل الأول)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

إذا شغلت السكريبت مرة أخرى، ستتخطى المكتبة عملية التنزيل وتقوم ببساطة بسرد النموذج الموجود بالفعل، مما يثبت أن **how to set cache** فعلاً يُجني ثماره في التشغيلات اللاحقة.

## ## تمكين auto download للنماذج المفقودة

غالبًا ما ستعمل مع عدة نماذج عبر المشاريع. سحب كل نموذج يدويًا من Hugging Face قد يكون مرهقًا. بتمكين auto download، يتولى Aspose AI العبء الثقيل.

```python
cfg.allow_auto_download = "true"
```

> **نصيحة احترافية:** احتفظ بـ `allow_auto_download` مضبوطة على `"true"` **فقط** في بيئات التطوير أو CI. في الإنتاج قد ترغب في قفل التخزين المؤقت لتجنب حركة مرور الشبكة غير المتوقعة.

إذا قررت لاحقًا إيقافه، ما عليك سوى ضبط العلامة إلى `"false"` قبل استدعاء `initialize()` مرة أخرى.

## ## تنزيل نموذج Hugging Face أثناء التشغيل

The line

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

يخبر Aspose AI أي مستودع بعيد سيسحب منه. المكتبة تدعم أي نموذج عام على Hugging Face يقدم ملف GGUF. هل تريد نموذجًا مختلفًا؟ استبدل معرف المستودع:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

عند تشغيل السكريبت، يتحقق Aspose AI من التخزين المؤقت:

- **إذا كان النموذج موجودًا**، يتم تحميله فورًا.  
- **إذا لم يكن موجودًا**، تُفعّل علامة auto‑download عملية تنزيل، وتخزن الملف تحت `directory_model_path`، ثم تسجّله للاستخدام الفوري.

هذا النهج يلغي عملية “التنزيل ثم التشغيل” ذات الخطوتين التي تجبرك العديد من الدروس على اتباعها.

## ## كيفية استخدام Aspose AI بعد سرد النموذج

سرد النماذج هو نصف القصة فقط. بمجرد معرفتك بوجود نموذج، يمكنك بدء الاستدلال:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**لماذا هذا مهم:**  
- `run_inference()` يختصر عملية الترميز، التجميع، وإدارة وحدة معالجة الرسوميات.  
- بتمرير *اسم النموذج* الذي حصلت عليه من `list_local()`، تضمن أن استدعاء الاستدلال يطابق الملف الدقيق على القرص.

## ## كيفية تعيين موقع التخزين المؤقت لعدة مشاريع

إذا كنت تدير عدة مشاريع، قد ترغب في أن يكون لكل منها مجلد تخزين مؤقت خاص. حقل `directory_model_path` هو مجرد سلسلة نصية، لذا يمكنك بناؤه بشكل ديناميكي:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

الآن يحصل كل مشروع على مجلد فرعي معزول (`./model_cache/sentiment_analysis`)، مما يمنع تعارض الإصدارات ويسهل عملية التنظيف.

## ## المشكلات الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| **`PermissionError` عند الوصول إلى التخزين المؤقت** | مجلد التخزين المؤقت مملوك لمستخدم آخر (شائع على الخوادم المشتركة) | أنشئ المجلد يدويًا بالأذونات المناسبة: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **النموذج لا يظهر أبدًا في `list_local()`** | `allow_auto_download` مضبوطة على `"false"` والنموذج غير مخزن بعد | قم بتفعيل العلامة مؤقتًا، شغّل مرة واحدة، ثم أوقفها إذا رغبت |
| **إصدار نموذج غير متوقع** | مستودعين مختلفين يشاركان نفس الاسم لكن بملفات مختلفة | ثبت معرف المستودع الدقيق (بما في ذلك العلامة/الالتزام) أو قفل التخزين المؤقت بتعطيل auto‑download بعد أول سحب ناجح |
| **أخطاء نفاد الذاكرة** | ملفات GGUF الكبيرة على جهاز لا يملك ذاكرة RAM/VRAM كافية | استخدم نموذجًا أصغر (مثال: `Qwen2.5-1.5B`) أو اضبط `cfg.device = "cpu"` لإجبار الاستدلال على المعالج المركزي |

## ## السكريبت الكامل الذي يمكنك نسخه‑ولصقه

فيما يلي المثال الكامل الجاهز للتنفيذ والذي يدمج جميع المفاهيم السابقة. احفظه باسم `list_models_demo.py` ونفّذه باستخدام `python list_models_demo.py`.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**تشغيله** سيولد مخرجات مشابهة للمثال السابق، يتبعها إجابة مختصرة من النموذج. لا تتردد في استبدال النص المطلوب بأي شيء تريده—هذه أسرع طريقة لاختبار أن النموذج قابل للاستخدام فعليًا بعد أن قمت بـ **how to list models**.

## ## الخلاصة

لقد غطينا كل ما تحتاجه لـ **how to list models** باستخدام Aspose AI، من تمكين **auto download** إلى تكوين **cache** دائم وجلب **نموذج Hugging Face** عند الطلب. النقاط الرئيسية:

1. أنشئ كائن `AsposeAI` و `AsposeAIModelConfig`.  
2. اضبط `allow_auto_download = "true"` ووجه `directory_model_path` إلى مجلد تتحكم فيه.  
3. قم بتهيئة AI، ثم استدعِ `list_local()` لرؤية ما تم تخزينه بالضبط.  
4. استخدم اسم النموذج المُدرج للاستدلال، وستكون جاهزًا لبناء تطبيقات واقعية.

## ما التالي؟

- **جرّب نماذج مختلفة** – استبدل `cfg.hugging_face_repo_id` بمستودع آخر وشاهد كيف تتغير القائمة.  
- **ضبط الذاكرة المؤقتة بدقة**

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تجميع صور OCR باستخدام List في Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [كيفية تعيين ترخيص Aspose OCR والتحقق منه في Java](/ocr/english/java/ocr-basics/set-license/)
- [كيفية استخراج النص من صورة باستخدام Aspose.OCR لـ .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}