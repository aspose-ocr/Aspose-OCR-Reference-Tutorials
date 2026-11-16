---
category: general
date: 2026-02-22
description: تعلم كيفية سرد النماذج المخزنة مؤقتًا وعرض دليل التخزين المؤقت على جهازك
  بسرعة. يتضمن خطوات لعرض مجلد التخزين المؤقت وإدارة تخزين نماذج الذكاء الاصطناعي
  المحلية.
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: ar
og_description: اكتشف كيفية سرد النماذج المخزنة مؤقتًا، وعرض دليل التخزين المؤقت،
  ورؤية مجلد التخزين المؤقت في بضع خطوات سهلة. مثال كامل بلغة بايثون مرفق.
og_title: قائمة النماذج المخزنة مؤقتًا – دليل سريع لعرض دليل التخزين المؤقت
tags:
- AI
- caching
- Python
- development
title: قائمة النماذج المخزنة مؤقتًا – كيفية عرض مجلد الذاكرة المؤقتة وإظهار دليل التخزين
  المؤقت
url: /ar/python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# قائمة النماذج المخزنة مؤقتًا – دليل سريع لعرض دليل التخزين المؤقت

هل تساءلت يومًا كيف **تسرد النماذج المخزنة مؤقتًا** على جهازك دون الحاجة للغوص في مجلدات غامضة؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى التحقق من النماذج التي تم تخزينها محليًا، خاصةً عندما تكون مساحة القرص محدودة. الخبر السار؟ ببضع أسطر فقط يمكنك **تسرد النماذج المخزنة مؤقتًا** و**عرض دليل التخزين المؤقت**، مما يمنحك رؤية كاملة لمجلد التخزين المؤقت.

في هذا الدرس سنستعرض سكربت Python مستقل يقوم بذلك بالضبط. بنهاية الدرس ستعرف كيف تعرض مجلد التخزين المؤقت، وتفهم أين يعيش التخزين المؤقت على أنظمة تشغيل مختلفة، وحتى ترى قائمة مطبوعة مرتبة لكل نموذج تم تنزيله. لا وثائق خارجية، لا تخمين—فقط كود واضح وشروحات يمكنك نسخها ولصقها الآن.

## ما ستتعلمه

- كيفية تهيئة عميل AI (أو نموذج تجريبي) يوفر أدوات التخزين المؤقت.  
- الأوامر الدقيقة لـ **تسرد النماذج المخزنة مؤقتًا** و**عرض دليل التخزين المؤقت**.  
- أين يقع التخزين المؤقت على Windows و macOS و Linux، حتى تتمكن من الانتقال إليه يدويًا إذا رغبت.  
- نصائح للتعامل مع الحالات الخاصة مثل التخزين المؤقت الفارغ أو مسار تخزين مخصص.  

**المتطلبات المسبقة** – تحتاج إلى Python 3.8+ وعميل AI يمكن تثبيته عبر pip ويطبق الدوال `list_local()`, `get_local_path()`, ويفضل `clear_local()`. إذا لم يكن لديك واحد بعد، يستخدم المثال فئة تجريبية `YourAIClient` يمكنك استبدالها بـ SDK الحقيقي (مثل `openai`, `huggingface_hub`, إلخ).  

مستعد؟ لنبدأ.

## الخطوة 1: إعداد عميل AI (أو نموذج تجريبي)

إذا كان لديك كائن عميل بالفعل، تخطى هذا القسم. وإلا، أنشئ كائنًا صغيرًا يحاكي واجهة التخزين المؤقت. هذا يجعل السكربت قابلًا للتنفيذ حتى بدون SDK حقيقي.

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **نصيحة احترافية:** إذا كان لديك عميل حقيقي (مثلاً `from huggingface_hub import HfApi`)، استبدل استدعاء `YourAIClient()` بـ `HfApi()` وتأكد من وجود الدوال `list_local` و `get_local_path` أو غلفها بما يلزم.

## الخطوة 2: **تسرد النماذج المخزنة مؤقتًا** – استرجاعها وعرضها

الآن بعد أن أصبح العميل جاهزًا، يمكننا طلب تعداد كل ما يعرفه عن التخزين المحلي. هذا هو جوهر عملية **تسرد النماذج المخزنة مؤقتًا**.

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**الناتج المتوقع** (مع البيانات الوهمية من الخطوة 1):

```
Cached models:
 - model_1
 - model_2
 - model_3
```

إذا كان التخزين المؤقت فارغًا سترى ببساطة:

```
Cached models:
```

تلك السطر الفارغ الصغير يخبرك بأنه لا يوجد شيء مخزن بعد—مفيد عندما تكتب سكربتات لتنظيف التخزين.

## الخطوة 3: **عرض دليل التخزين المؤقت** – أين يقع؟

معرفة المسار غالبًا ما تكون نصف المعركة. أنظمة التشغيل المختلفة تضع التخزين المؤقت في مواقع افتراضية مختلفة، وبعض SDKs تسمح لك بتجاوزها عبر متغيرات البيئة. المقتطف التالي يطبع المسار المطلق حتى تتمكن من `cd` إليه أو فتحه في مستكشف الملفات.

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**الناتج النموذجي** على نظام شبيه بـ Unix:

```
Cache directory: /home/youruser/.ai_cache
```

على Windows قد ترى شيئًا مثل:

```
Cache directory: C:\Users\YourUser\.ai_cache
```

الآن تعرف بالضبط **كيف تعرض مجلد التخزين المؤقت** على أي منصة.

## الخطوة 4: جمع كل شيء معًا – سكربت واحد قابل للتنفيذ

فيما يلي البرنامج الكامل الجاهز للتنفيذ الذي يجمع الخطوات الثلاث. احفظه باسم `view_ai_cache.py` وشغّله بـ `python view_ai_cache.py`.

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

شغّله وسترى فورًا كلًا من قائمة النماذج المخزنة **وموقع** دليل التخزين المؤقت.

## الحالات الخاصة والاختلافات

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **التخزين المؤقت فارغ** | سيطبع السكربت “Cached models:” دون أي مدخلات. يمكنك إضافة تحذير شرطي: `if not models: print("⚠️ No models cached yet.")` |
| **مسار تخزين مخصص** | مرّر مسارًا عند إنشاء العميل: `YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`. سيعكس استدعاء `get_local_path()` ذلك الموقع المخصص. |
| **أخطاء الأذونات** | على الأجهزة المقيدة قد يرفع العميل استثناء `PermissionError`. غلف التهيئة بـ `try/except` واستخدم دليلًا يمكن للمستخدم الكتابة فيه. |
| **استخدام SDK حقيقي** | استبدل `YourAIClient` بفئة العميل الفعلية وتأكد من تطابق أسماء الدوال. العديد من SDKs توفر خاصية `cache_dir` يمكنك قراءتها مباشرة. |

## نصائح احترافية لإدارة التخزين المؤقت

- **تنظيف دوري:** إذا كنت تقوم بتنزيل نماذج كبيرة بشكل متكرر، جدولة مهمة cron تستدعي `shutil.rmtree(ai.get_local_path())` بعد التأكد من عدم الحاجة إليها.  
- **مراقبة استهلاك القرص:** استخدم `du -sh $(ai.get_local_path())` على Linux/macOS أو `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum` في PowerShell لمتابعة الحجم.  
- **مجلدات إصدارات:** بعض العملاء ينشئون مجلدات فرعية لكل نسخة من النموذج. عندما **تسرد النماذج المخزنة مؤقتًا**، ستظهر كل نسخة كمدخل منفصل—استفد من ذلك لإزالة الإصدارات القديمة.  

## نظرة بصرية

![لقطة شاشة لتسرد النماذج المخزنة مؤقتًا](https://example.com/images/list-cached-models.png "تسرد النماذج المخزنة مؤقتًا – مخرجات وحدة التحكم تظهر النماذج ومسار التخزين المؤقت")

*نص بديل:* *تسرد النماذج المخزنة مؤقتًا – مخرجات وحدة التحكم تعرض أسماء النماذج المخزنة ومسار دليل التخزين المؤقت.*

## الخلاصة

غطّينا كل ما تحتاجه لـ **تسرد النماذج المخزنة مؤقتًا**, **عرض دليل التخزين المؤقت**, وبشكل عام **كيفية عرض مجلد التخزين المؤقت** على أي نظام. السكربت القصير يوضح حلًا كاملاً قابلًا للتنفيذ، يشرح **لماذا** كل خطوة مهمة، ويقدم نصائح عملية للاستخدام الواقعي.  

بعد ذلك، قد تستكشف **كيفية مسح التخزين المؤقت** برمجيًا، أو دمج هذه الاستدعاءات في خط أنابيب نشر أكبر يتحقق من توفر النماذج قبل تشغيل مهام الاستدلال. بأي حال، لديك الآن الأساس لإدارة تخزين نماذج AI محليًا بثقة.

هل لديك أسئلة حول SDK AI معين؟ اترك تعليقًا أدناه، وتمنياتنا لك بتخزين مؤقت سعيد!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}