---
category: general
date: 2026-02-22
description: كيفية حذف الملفات في بايثون ومسح ذاكرة النموذج بسرعة. تعلم كيفية سرد
  ملفات الدليل في بايثون، وتصفية الملفات حسب الامتداد، وحذف الملف في بايثون بأمان.
draft: false
keywords:
- how to delete files
- clear model cache
- list directory files python
- filter files by extension
- delete file python
language: ar
og_description: كيفية حذف الملفات في بايثون ومسح ذاكرة التخزين المؤقت للنموذج. دليل
  خطوة بخطوة يغطي سرد ملفات الدليل في بايثون، تصفية الملفات حسب الامتداد، وحذف ملف
  بايثون.
og_title: كيفية حذف الملفات في بايثون – دليل مسح ذاكرة التخزين المؤقت للنموذج
tags:
- python
- file-system
- automation
title: كيفية حذف الملفات في بايثون – دليل مسح ذاكرة النموذج
url: /ar/python/general/how-to-delete-files-in-python-clear-model-cache-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حذف الملفات في بايثون – دليل مسح ذاكرة النموذج المؤقتة

هل تساءلت يوماً **عن كيفية حذف الملفات** التي لم تعد تحتاجها، خاصةً عندما تملأ دليل ذاكرة النموذج المؤقتة؟ لست وحدك؛ يواجه العديد من المطورين هذه المشكلة عندما يجربون نماذج اللغة الكبيرة وينتهي بهم الأمر بكمية هائلة من ملفات *.gguf*.  

في هذا الدليل سنعرض لك حلاً مختصراً وجاهزاً للتنفيذ لا يقتصر فقط على **كيفية حذف الملفات** بل يشرح أيضاً **مسح ذاكرة النموذج المؤقتة**، **قائمة ملفات الدليل بايثون**، **تصفية الملفات حسب الامتداد**، و**حذف ملف بايثون** بطريقة آمنة وعبر‑منصات. في النهاية ستحصل على سكربت سطر واحد يمكنك إدراجه في أي مشروع، بالإضافة إلى مجموعة من النصائح للتعامل مع الحالات الخاصة.

![how to delete files illustration](https://example.com/clear-cache.png "how to delete files in Python")

## كيفية حذف الملفات في بايثون – مسح ذاكرة النموذج المؤقتة

### ما يغطيه الدرس
- الحصول على المسار الذي تخزن فيه مكتبة الذكاء الاصطناعي نماذجها المؤقتة.  
- سرد كل عنصر داخل ذلك الدليل.  
- اختيار الملفات التي تنتهي بـ **.gguf** فقط (هذه هي خطوة **تصفية الملفات حسب الامتداد**).  
- حذف تلك الملفات مع معالجة الأخطاء المحتملة في الأذونات.  

بدون أي تبعيات خارجية، بدون حزم طرف ثالث معقدة—فقط وحدة `os` المدمجة ومساعد صغير من الـ `ai` SDK الافتراضي.

## الخطوة 1: قائمة ملفات الدليل بايثون

أولاً نحتاج إلى معرفة ما يحتويه مجلد الذاكرة المؤقتة. تُعيد الدالة `os.listdir()` قائمة بسيطة من أسماء الملفات، وهي مثالية لجرد سريع.

```python
import os

# Assume `ai.get_local_path()` returns the absolute cache directory.
cache_dir_path = ai.get_local_path()

# Grab every entry – this is the “list directory files python” part.
all_entries = os.listdir(cache_dir_path)
print(f"Found {len(all_entries)} items in cache:")
for entry in all_entries:
    print(" •", entry)
```

**لماذا هذا مهم:**  
قائمة الدليل تمنحك رؤية واضحة. إذا تخطيت هذه الخطوة قد تحذف شيئًا لم تقصد حذفه. بالإضافة إلى ذلك، يُعد الإخراج المطبوع فحصًا sanity‑check قبل بدء حذف الملفات.

## الخطوة 2: تصفية الملفات حسب الامتداد

ليس كل عنصر ملف نموذج. نريد فقط حذف ملفات *.gguf* الثنائية، لذا نقوم بتصفية القائمة باستخدام طريقة `str.endswith()`.

```python
# Keep only files that end with .gguf – our “filter files by extension” logic.
model_files = [f for f in all_entries if f.lower().endswith(".gguf")]
print(f"\nIdentified {len(model_files)} model file(s) to delete:")
for mf in model_files:
    print(" •", mf)
```

**لماذا نقوم بالتصفية:**  
حذف شامل غير مدروس قد يمحو سجلات، ملفات إعدادات، أو حتى بيانات المستخدم. من خلال فحص الامتداد صراحةً نضمن أن **حذف ملف بايثون** يستهدف فقط الأصول المطلوبة.

## الخطوة 3: حذف ملف بايثون بأمان

الآن يأتي جوهر **كيفية حذف الملفات**. سن iterates على `model_files`، نبني مسارًا مطلقًا باستخدام `os.path.join()`، ثم نستدعي `os.remove()`. تغليف الاستدعاء داخل كتلة `try/except` يتيح لنا الإبلاغ عن مشاكل الأذونات دون تعطل السكربت.

```python
for file_name in model_files:
    file_path = os.path.join(cache_dir_path, file_name)
    try:
        os.remove(file_path)
        print(f"Removed: {file_name}")
    except PermissionError:
        print(f"⚠️  Permission denied: {file_name}")
    except FileNotFoundError:
        # This could happen if another process already deleted the file.
        print(f"⚠️  Already gone: {file_name}")
    except OSError as e:
        # Catch‑all for unexpected OS errors.
        print(f"❌  Failed to delete {file_name}: {e}")

print("\nOld model files removed.")
```

**ما ستراه:**  
إذا سارت الأمور بسلاسة، سيعرض الطرفية كل ملف كـ “Removed”. إذا حدث خطأ، ستحصل على تحذير ودود بدلاً من تتبع الأخطاء الغامض. هذا النهج يجسد أفضل الممارسات لـ **حذف ملف بايثون**—دائمًا توقع الأخطاء وتعامل معها.

## إضافية: التحقق من الحذف ومعالجة الحالات الخاصة

### التحقق من أن الدليل نظيف

بعد انتهاء الحلقة، من الجيد التأكد مرة أخرى من عدم بقاء أي ملفات *.gguf*.

```python
remaining = [f for f in os.listdir(cache_dir_path) if f.lower().endswith(".gguf")]
if not remaining:
    print("✅  Cache is now clean.")
else:
    print("⚡  Some files survived:", remaining)
```

### ماذا لو كان مجلد الذاكرة المؤقتة غير موجود؟

أحيانًا قد لا تكون مكتبة AI SDK قد أنشأت الذاكرة المؤقتة بعد. احمِ نفسك من ذلك مبكرًا:

```python
if not os.path.isdir(cache_dir_path):
    raise RuntimeError(f"The cache directory does not exist: {cache_dir_path}")
```

### حذف أعداد كبيرة من الملفات بكفاءة

إذا كنت تتعامل مع آلاف ملفات النماذج، فكر في استخدام `os.scandir()` لمؤشر أسرع، أو حتى `pathlib.Path.glob("*.gguf")`. المنطق يبقى نفسه؛ فقط طريقة العدّ تتغير.

## سكربت كامل وجاهز للتنفيذ

بجمع كل ما سبق، إليك المقتطف الكامل الذي يمكنك نسخه ولصقه في ملف باسم `clear_model_cache.py`:

```python
import os

# -------------------------------------------------
# Step 0: Obtain the cache directory from the AI SDK
# -------------------------------------------------
cache_dir_path = ai.get_local_path()

# -------------------------------------------------
# Safety check: make sure the directory exists
# -------------------------------------------------
if not os.path.isdir(cache_dir_path):
    raise RuntimeError(f"The cache directory does not exist: {cache_dir_path}")

# -------------------------------------------------
# Step 1: List everything (list directory files python)
# -------------------------------------------------
all_entries = os.listdir(cache_dir_path)

# -------------------------------------------------
# Step 2: Keep only .gguf model files (filter files by extension)
# -------------------------------------------------
model_files = [f for f in all_entries if f.lower().endswith(".gguf")]

# -------------------------------------------------
# Step 3: Delete each model file (delete file python)
# -------------------------------------------------
for file_name in model_files:
    file_path = os.path.join(cache_dir_path, file_name)
    try:
        os.remove(file_path)
        print(f"Removed: {file_name}")
    except PermissionError:
        print(f"⚠️  Permission denied: {file_name}")
    except FileNotFoundError:
        print(f"⚠️  Already gone: {file_name}")
    except OSError as e:
        print(f"❌  Failed to delete {file_name}: {e}")

# -------------------------------------------------
# Bonus: Verify everything is gone
# -------------------------------------------------
remaining = [f for f in os.listdir(cache_dir_path) if f.lower().endswith(".gguf")]
if not remaining:
    print("\n✅  Cache is now clean.")
else:
    print("\n⚡  Some files survived:", remaining)

print("\nOld model files removed.")
```

تشغيل هذا السكربت سيقوم بـ:

1. تحديد موقع ذاكرة نموذج AI.  
2. سرد كل عنصر (محققًا متطلب **قائمة ملفات الدليل بايثون**).  
3. تصفية ملفات *.gguf* (**تصفية الملفات حسب الامتداد**).  
4. حذف كل ملف بأمان (**حذف ملف بايثون**).  
5. التأكد من أن الذاكرة المؤقتة فارغة، لتمنحك راحة البال.

## الخلاصة

استعرضنا **كيفية حذف الملفات** في بايثون مع تركيز على مسح ذاكرة النموذج المؤقتة. الحل الكامل يوضح لك كيف **تسرد ملفات الدليل بايثون**، وتطبق **تصفية الملفات حسب الامتداد**، وتقوم بحذف **ملف بايثون** بأمان مع معالجة المشكلات الشائعة مثل نقص الأذونات أو ظروف السباق.  

ما الخطوة التالية؟ جرّب تعديل السكربت لامتدادات أخرى (مثل `.bin` أو `.ckpt`) أو دمجه في روتين تنظيف أكبر يُنفّذ بعد كل تحميل نموذج. يمكنك أيضًا استكشاف `pathlib` للحصول على تجربة كائنية أكثر، أو جدولة السكربت باستخدام `cron`/`Task Scheduler` للحفاظ على مساحة عملك نظيفة تلقائيًا.

هل لديك أسئلة حول الحالات الخاصة، أو تريد معرفة كيف يعمل على Windows مقابل Linux؟ اترك تعليقًا أدناه، وتمنياتنا لك بتنظيف سعيد!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}