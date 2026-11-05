---
category: general
date: 2026-06-22
description: تعلم كيفية سرد نماذج الذكاء الاصطناعي المخزنة مؤقتًا باستخدام مجموعة
  أدوات الذكاء الاصطناعي في بايثون. يتضمن خطوات لاسترجاع دليل ذاكرة التخزين المؤقت
  للنماذج وإدارة نماذج الذكاء الاصطناعي المحلية بفعالية.
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: ar
og_description: قائمة نماذج الذكاء الاصطناعي المخزنة مؤقتًا باستخدام بايثون وSDK الذكاء
  الاصطناعي. اتبع هذا الدليل خطوة بخطوة لاسترجاع دليل التخزين المؤقت للنماذج ومعالجة
  نماذج الذكاء الاصطناعي المحلية.
og_title: قائمة نماذج الذكاء الاصطناعي المخزنة مؤقتًا في بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: قائمة نماذج الذكاء الاصطناعي المخزنة مؤقتًا في بايثون – دليل كامل
url: /ar/python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# قائمة نماذج الذكاء الاصطناعي المخزنة مؤقتًا في بايثون – دليل كامل

هل تساءلت يومًا كيف **list cached AI models** على جهازك دون البحث في مجلدات غامضة؟ أنت لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى التحقق من النماذج المخزنة محليًا، خاصةً عند العمل بحدود عرض نطاق محدود أو نشرات دون اتصال. في هذا الدرس ستتعرف على طريقة سريعة ومباشرة لاستعلام AI SDK، طباعة محتويات الذاكرة المؤقتة، واكتشاف المكان الدقيق لتلك الملفات.

سنتطرق أيضًا إلى مواضيع ذات صلة مثل **retrieving the model cache directory**، التعامل مع الذاكرة المؤقتة الفارغة، وأفضل الممارسات لـ **manage AI model cache** في سكريبتات الإنتاج. في النهاية ستحصل على قطعة كود مستقلة يمكنك إدراجها في أي مشروع بايثون.

## المتطلبات المسبقة

- Python 3.8 أو أحدث مثبت.
- AI SDK (الحزمة `ai`) مثبت عبر `pip install ai-sdk` أو مستودع المؤسسة الداخلي.
- إلمام أساسي بتشغيل السكريبتات من سطر الأوامر.

لا توجد مكتبات إضافية مطلوبة، لذا يبقى المثال خفيفًا ومحمولًا.

---

## قائمة نماذج الذكاء الاصطناعي المخزنة – نظرة سريعة

أول شيء تحتاج إلى فعله هو استيراد SDK واستدعاء الدوال المساعدة الخاصة به. يوفّر SDK طريقتين مفيدتين:

1. `ai.list_local()` – تُرجع قائمة بايثون بمعرفات النماذج المخزنة مؤقتًا.
2. `ai.get_local_path()` – تُرجع الدليل المطلق حيث توجد ملفات تلك النماذج.

كلا الاستدعائين متزامنان ويطرحان خطأ واضح `AIError` إذا حدث شيء ما، مما يجعل معالجة الأخطاء مباشرة.

> **لماذا نستخدم هذه الدوال؟**  
> معرفة المجموعة الدقيقة من النماذج المخزنة يتيح لك تجنب التحميلات غير الضرورية، تصحيح عدم تطابق الإصدارات، وتنظيف القطع القديمة تلقائيًا. إنها جزء صغير من سير عمل **AI SDK Python** الأكبر، لكنها يمكن أن توفر لك ساعات من البحث اليدوي في نظام الملفات.

### الخطوة 1: استيراد AI SDK

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*لماذا هذا مهم:* استيراد الحزمة يسجّل الامتدادات C‑الأساسية ويحمل ملفات الإعداد (مثل مسارات الذاكرة المؤقتة) من بيئتك. تخطي هذه الخطوة سيؤدي إلى رفع `ModuleNotFoundError` فور استدعاء أي دالة من SDK.

### الخطوة 2: سرد جميع النماذج المخزنة مؤقتًا

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**ما ستراه:** إذا كان لديك ثلاثة نماذج مخزنة، قد يبدو الناتج كالتالي:

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

إذا كانت الذاكرة المؤقتة فارغة، ستحصل على قائمة فارغة:

```
Cached models: []
```

> **نصيحة احترافية:** غلف الاستدعاء بكتلة try/except إذا كنت تشك أن SDK قد لا يكون مهيأً بشكل صحيح.

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### الخطوة 3: استرجاع دليل ذاكرة النموذج المؤقتة

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

الناتج النموذجي على نظام شبيه بـ Unix:

```
Model cache directory: /home/you/.cache/ai/models
```

على Windows قد ترى شيئًا مثل `C:\Users\you\AppData\Local\ai\models`. معرفة هذا المسار أساسي عندما تحتاج إلى **manage AI model cache** يدويًا—ربما لحذف الإصدارات القديمة أو لنسخ الملفات إلى محرك مشترك.

---

## ملخص بصري

![مخطط يوضح كيفية سرد نماذج الذكاء الاصطناعي المخزنة، استرجاع أسمائها، وتحديد موقع دليل الذاكرة المؤقتة](https://example.com/images/list-cached-ai-models.png)

*نص بديل:* مخطط يوضح العملية لـ **list cached AI models** باستخدام AI SDK في بايثون.

## معالجة الحالات الحدية والمشكلات الشائعة

### الذاكرة المؤقتة الفارغة

إذا أعادت `ai.list_local()` قائمة فارغة، قد تتساءل ما إذا كان SDK غير مُكوَّن بشكل صحيح. تحقق مرة أخرى من متغيّر البيئة `AI_CACHE_DIR` (أو ملف إعداد SDK) للتأكد من أنه يشير إلى موقع قابل للكتابة.

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### مشاكل الأذونات

عند الوصول إلى `ai.get_local_path()`، قد يظهر `PermissionError` على الأنظمة ذات القيود. عادةً ما يكون الحل تشغيل السكريبت بحقوق المستخدم المناسبة أو تعديل قوائم التحكم في الوصول (ACLs) للمجلد.

### عدم تطابق الإصدارات

أحيانًا تحتوي الذاكرة المؤقتة على نسخة أقدم من نموذج بينما يطلب الكود نسخة أحدث. سيقوم SDK تلقائيًا بتحميل النسخة الأحدث، لكن يمكنك تجنب ذلك بفحص علامة الإصدار في القائمة:

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### تنظيف النماذج القديمة

إذا كنت بحاجة لتوفير مساحة، يمكنك حذف مجلد نموذج معين مباشرةً:

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

تشغيل `purge_model('bert-base-uncased')` سيزيل ذلك النموذج ويوفر مساحة على القرص.

---

## السكريبت الكامل الذي يمكنك نسخه‑ولصقه

فيما يلي سكريبت جاهز للتنفيذ يجمع جميع الخطوات، يضيف معالجة أخطاء أساسية، ويطبع ملخصًا ودودًا.

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**الناتج المتوقع (عند وجود محتوى في الذاكرة المؤقتة):**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

شغّل السكريبت باستخدام `python list_models.py` وستعرف فورًا ما هو موجود على القرص.

---

## الأسئلة المتكررة

**س: هل يعمل هذا على جميع أنظمة التشغيل؟**  
ج: نعم. SDK يخفِّي تفاصيل مسارات الأنظمة، لذا `ai.get_local_path()` تُرجع سلسلة صالحة على Linux، macOS، وWindows.

**س: هل يمكنني سرد النماذج من ذاكرة مؤقتة عن بُعد؟**  
ج: الدالة المدمجة `list_local()` تُظهر فقط القطع المخزنة محليًا. للوصول إلى سجلات عن بُعد يمكنك استخدام `ai.list_remote()` (إذا كانت نسخة SDK تدعم ذلك).

**س: ماذا لو لم يكن اسم SDK هو `ai`؟**  
ج: استبدل سطر الاستيراد باسم الحزمة الفعلي، مثل `import myai as ai`. جميع الاستدعاءات اللاحقة تبقى كما هي لأن عقدة الـ API ثابتة عبر جميع التطبيقات.

---

## الخلاصة

أصبح لديك الآن طريقة قوية وجاهزة للإنتاج لـ **list cached AI models** باستخدام مكتبة **AI SDK Python**، استرجاع **model cache directory**، وحتى تنظيف الملفات القديمة. هذه المعرفة تساعدك على الحفاظ على بيئتك مرتبة، تجنب التحميلات المتكررة، وتصحيح مشكلات الإصدارات بسهولة.

هل أنت مستعد للخطوة التالية؟ جرّب توسيع السكريبت لتحميل النماذج المفقودة تلقائيًا، أو دمجه في خط أنابيب CI يتحقق من صحة الذاكرة المؤقتة قبل كل بناء. استكشاف استراتيجيات **manage AI model cache** سيجعل تطبيقاتك المدعومة بالذكاء الاصطناعي أسرع وأكثر موثوقية.

برمجة سعيدة، ولتظل ذاكرتك المؤقتة خفيفة!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية معالجة مجموعة من صور OCR باستخدام List في Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [استخراج نص الصورة بـ C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [كيفية استخراج النص من أرشيفات ZIP باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}